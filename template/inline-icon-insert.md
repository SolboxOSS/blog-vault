<%*
const vault = app.vault;
const clipboard = navigator.clipboard;
const currentFile = tp.file.find_tfile(tp.file.path(true));
const currentFolderPath = currentFile.parent.path;
const imgFolderPath = `${currentFolderPath}/attachments/icons`;

// 이미지 저장 경로가 없으면 생성
if (!(await vault.adapter.exists(imgFolderPath))) {
  await vault.createFolder(imgFolderPath);
}

// 이미지 파일명 입력받기 (확장자 제외)
let imgFileName = await tp.system.prompt('이미지 파일명을 입력하세요 (확장자 제외)');
if (!imgFileName) {
  new Notice("이미지 파일명이 입력되지 않아 취소되었습니다.");
  return;
}

// 이미지 설명 입력받기 (기본값: 파일명 특수문자 '-' 등 제거)
const defaultDescription = imgFileName.replace(/[-_]/g, ' ');
let imgDescription = await tp.system.prompt('이미지 설명을 입력하세요', defaultDescription);
if (!imgDescription) imgDescription = defaultDescription;

// 클립보드에서 이미지 데이터를 가져와서 저장
const imgBlob = await clipboard.read();
if (!imgBlob || imgBlob.length === 0 || !imgBlob[0].types.includes('image/png')) {
  new Notice("클립보드에 이미지가 없습니다. 이미지 복사 후 다시 시도해주세요.");
  return;
}

const arrayBuffer = await imgBlob[0].getType('image/png').then(blob => blob.arrayBuffer());
await vault.adapter.writeBinary(`${imgFolderPath}/${imgFileName}.png`, arrayBuffer);

// 마크다운 이미지 링크 생성 및 삽입 (#inline-icon 추가)
const markdownImageLink = `![${imgDescription}](./attachments/icons/${imgFileName}.png#inline-icon)`;
tR = markdownImageLink;
-%>