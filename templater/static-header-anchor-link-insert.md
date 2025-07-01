<%*
const vault = app.vault;
const editor = app.workspace.activeEditor.editor;

const selection = editor.getSelection().trim();
let linkText = selection || '';

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
    const headings = content.match(/^#{2,}\s.*$/gm); // H1 제외
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

// 템플릿 실행
const folderPath = await selectFolder('/');
if (!folderPath) return;

const selectedFile = await selectMarkdownFile(folderPath);
if (!selectedFile) return;

// 헤딩 선택 여부 확인
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

// 절대 경로 계산: .md 제거하고 /en/ → /support/로 치환
let absolutePath = selectedFile.path
    .replace(/\.md$/, '')
    .replace(/^en\//, 'support/'); // 루트가 en/으로 시작할 경우 support/로

// URL 인코딩 (공백 등 처리)
absolutePath = absolutePath.split('/').map(encodeURIComponent).join('/');

// 링크 텍스트 입력받기
linkText = await tp.system.prompt('Anchor link 이름 입력:', linkText);
if (!linkText) return;

// 최종 링크 조합
let finalLink = '';
if (selectedHeadingAnchor) {
    const finalAnchor = selectedHeadingAnchor.anchor.toLowerCase();
    finalLink = `[${linkText}](/${absolutePath}#${finalAnchor})`;
} else {
    finalLink = `[${linkText}](/${absolutePath})`;
}

editor.replaceSelection(finalLink);
%>