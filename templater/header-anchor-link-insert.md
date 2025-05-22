<%*
const vault = app.vault;
const editor = app.workspace.activeEditor.editor;

const selection = editor.getSelection().trim();
let linkText = selection || '';

const currentFile = tp.file.find_tfile(tp.file.path(true));
const currentPath = currentFile.parent.path;

// 폴더 선택
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

// Markdown 파일 선택
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

// 헤딩 앵커 선택
async function selectHeadingAnchor(file) {
    const content = await vault.cachedRead(file);
    const headings = content.match(/^#+\s.*$/gm);
    if (!headings) {
        new Notice('헤딩이 없습니다.');
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

// 상대경로 정확히 계산하는 함수
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

const selectedHeadingAnchor = await selectHeadingAnchor(selectedFile);
if (!selectedHeadingAnchor) return;

// 파일 경로에서 .md 확장자만 제거 (.html 추가하지 않음)
const targetPath = selectedFile.path.replace(/\.md$/, '');

// 상대경로 생성 및 URL 인코딩
const relativeFilePath = getRelativePath(currentPath, targetPath);

// 링크 텍스트 입력받기
linkText = await tp.system.prompt('Anchor link 이름 입력:', linkText);
if (!linkText) return;

// 헤딩 앵커를 모두 소문자로 변환 (추가적으로 확실하게 적용)
const finalAnchor = selectedHeadingAnchor.anchor.toLowerCase();

// 최종 Anchor Link 삽입 (.html 없음)
const finalLink = `[${linkText}](${relativeFilePath}#${finalAnchor})`;
editor.replaceSelection(finalLink);
%>