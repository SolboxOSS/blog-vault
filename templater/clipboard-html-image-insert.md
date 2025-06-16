<%*
const vault = app.vault;
const file = tp.file.find_tfile(tp.file.path(true));
const relativeFolderPath = file.parent.path;
const imgFolderPath = `support/images/${relativeFolderPath}`;

// 폴더 없으면 생성
if (!(await vault.adapter.exists(imgFolderPath))) {
  await vault.createFolder(imgFolderPath);
}

const { clipboard, nativeImage } = require('electron');
const image = clipboard.readImage();

if (image.isEmpty()) {
  new Notice('클립보드에 이미지가 없습니다.');
  return;
}

// 이미지 파일명 입력받기 (중복 검사 포함)
let imgFileName = '';
while (true) {
  imgFileName = await tp.system.prompt('이미지 파일명을 입력하세요 (확장자 제외):');
  if (!imgFileName) return;
  const finalImgFileName = `${imgFileName}.png`;
  const targetImgPath = `${imgFolderPath}/${finalImgFileName}`;

  if (await vault.adapter.exists(targetImgPath)) {
    new Notice(`⚠️ 경고: "${finalImgFileName}" 파일이 이미 존재합니다. 다른 이름을 입력하세요.`);
  } else {
    imgFileName = finalImgFileName;
    break;
  }
}

// 기본 alt 텍스트 생성 (특수문자 처리)
const defaultAltText = imgFileName
  .replace(/\.[^/.]+$/, '')
  .replace(/[-_]/g, ' ')
  .trim();

// 이미지 설명(alt) 입력받기 (기본값 제공, 추가 수정 가능)
var imageAlt = await tp.system.prompt('이미지 설명(alt)을 입력하세요:', defaultAltText);

// 이미지 최종경로
const finalTargetImgPath = `${imgFolderPath}/${imgFileName}`;

// 이미지 저장
const imgBuffer = image.toPNG();
await vault.adapter.writeBinary(finalTargetImgPath, imgBuffer);

// 이미지 크기 및 정렬 입력받기
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
tR = `<img src="/${finalTargetImgPath}" alt="${imageAlt}" class="${size} ${align}" />`;
%>