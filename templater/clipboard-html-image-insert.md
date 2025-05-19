<%*
const vault = app.vault;
const file = tp.file.find_tfile(tp.file.path(true));
const folderName = file.parent.path.split('/').slice(-1)[0]; 
const imgFolderPath = `support/images/${folderName}`;

if (!(await vault.adapter.exists(imgFolderPath))) {
  await vault.createFolder(imgFolderPath);
}

// 이미지 파일명 입력받기
let imgFileName = await tp.system.prompt('이미지 파일명을 입력하세요 (확장자 제외):');
if (!imgFileName) return;
imgFileName += '.png';

// 이미지 최종경로
const targetImgPath = `${imgFolderPath}/${imgFileName}`;

// 클립보드 이미지 처리
const {clipboard, nativeImage} = require('electron');
const image = clipboard.readImage();

if (image.isEmpty()) {
  new Notice('클립보드에 이미지가 없습니다.');
  return;
}

const imgBuffer = image.toPNG();
await vault.adapter.writeBinary(targetImgPath, imgBuffer);

// HTML 이미지 속성 추가입력
var imageAlt = await tp.system.prompt('이미지 설명(alt)을 입력하세요:');
var size = await tp.system.suggester(
    ["img-small", "img-medium", "img-large"],
    ["img-small", "img-medium", "img-large"],
    true,
    "이미지 크기를 선택하세요:"
);
var align = await tp.system.suggester(
    ["img-left", "img-center", "img-right"],
    ["img-left", "img-center", "img-right"],
    true,
    "이미지 정렬을 선택하세요:"
);

// HTML 형식으로 최종 삽입
tR = `<img src="/${targetImgPath}" alt="${imageAlt}" class="${size} ${align}" />`;
%>