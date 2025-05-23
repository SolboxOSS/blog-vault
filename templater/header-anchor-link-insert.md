<%*
const vault = app.vault;
const editor = app.workspace.activeEditor.editor;

const selection = editor.getSelection().trim();
let linkText = selection || '';

const currentFile = tp.file.find_tfile(tp.file.path(true));
const currentPath = currentFile.parent.path;

async function selectFolder(path) {
    const folders = (await vault.adapter.list(path)).folders;
    const folderChoice = await tp.system.suggester(
        folders.map(f => f.replace(path, '')).filter(f => f),
        folders.filter(f => f),
        true,
        "폴더를 선택하세요:"
    );
    return folderChoice || null;
}

async function selectMarkdownFile(folder) {
    async function getMarkdownFiles(path) {
        const files = (await vault.adapter.list(path)).files.filter(f => f.endsWith('.md'));
        const folders = (await vault.adapter.list(path)).folders;
        for (let subfolder of folders) {
            files.push(...await getMarkdownFiles(subfolder));
        }
        return files;
    }
    const mdFiles = await getMarkdownFiles(folder);
    const selectedFilePath = await tp.system.suggester(
        mdFiles.map(f => f.replace(folder, '')),
        mdFiles,
        true,
        "파일을 선택하세요:"
    );
    return vault.getAbstractFileByPath(selectedFilePath) || null;
}

async function selectHeadingAnchor(file) {
    const content = await vault.cachedRead(file);
    const headings = content.match(/^#{2,}\s.*$/gm);  // H1 제외 (H2 이상만)
    if (!headings) {
        new Notice('선택 가능한 헤딩이 없습니다.');
        return null;
    }
    const anchors = headings.map(h => h.replace(/^#+\s/, '').trim()).map(h => ({
        display: h,
        anchor: h.toLowerCase().replace(/[^\w\s-]/g, '').replace(/\s+/g, '-')
    }));
    const selectedAnchor = await tp.system.suggester(
        anchors.map(a => a.display),
        anchors,
        true,
        "헤딩 앵커를 선택하세요:"
    );
    return selectedAnchor;
}

function getRelativePath(from, to) {
    const fromParts = from.split('/').filter(Boolean);
    const toParts = to.split('/').filter(Boolean);

    while (fromParts.length && toParts.length && fromParts[0] === toParts[0]) {
        fromParts.shift();
        toParts.shift();
    }

    const up = fromParts.map(() => '..');
    const relativeParts = [...up, ...toParts];
    const encodedPath = relativeParts.map(part => encodeURIComponent(part)).join('/');

    return encodedPath.startsWith('.') ? encodedPath : './' + encodedPath;
}

// 템플릿 실행
const folderPath = await selectFolder('/');
if (!folderPath) return;

const selectedFile = await selectMarkdownFile(folderPath);
if (!selectedFile) return;

// 헤딩 선택 여부 추가 확인
const continueHeading = await tp.system.suggester(
    ["예 (헤딩 선택)", "아니오 (파일 링크만)"],
    ["yes", "no"],
    true,
    "계속해서 헤더를 지정하시겠습니까?"
);

let selectedHeadingAnchor = null;

if (continueHeading === "yes") {
    selectedHeadingAnchor = await selectHeadingAnchor(selectedFile);
    if (!selectedHeadingAnchor) return;
}

// 파일의 원본 경로 (.md 유지)
const targetPath = selectedFile.path;

// 상대경로 생성 및 URL 인코딩
const relativeFilePath = getRelativePath(currentPath, targetPath);

// 링크 텍스트 입력받기
linkText = await tp.system.prompt('Anchor link 이름 입력:', linkText);
if (!linkText) return;

let finalLink = '';

if (selectedHeadingAnchor) {
    // 헤딩 앵커를 소문자로 변환하여 추가
    const finalAnchor = selectedHeadingAnchor.anchor.toLowerCase();
    finalLink = `[${linkText}](${relativeFilePath}#${finalAnchor})`;
} else {
    finalLink = `[${linkText}](${relativeFilePath})`;
}

editor.replaceSelection(finalLink);
%>