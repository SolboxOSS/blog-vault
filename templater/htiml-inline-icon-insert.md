<%*
const vault = app.vault;
const file = tp.file.find_tfile(tp.file.path(true));

// 현재 파일의 폴더 경로 유지 (en 포함)
const relativeFolderPath = file.parent.path;

// 이미지가 저장될 최종 경로 설정 (/support/icons/)
const imgFolderPath = `support/icons/${relativeFolderPath}`;

// 폴더가 없으면 생성
if (!(await vault.adapter.exists(imgFolderPath))) {
  await vault.createFolder(imgFolderPath);
}

// 이미지 파일명 입력받기
let imgFileName = await tp.system.prompt('이미지 파일명을 입력하세요 (확장자 제외):');
if (!imgFileName) return;
imgFileName += '.png';

// 입력한 파일명에서 특수문자(-, _)를 공백으로 대체한 뒤 alt 기본값으로 제공
const defaultAltText = imgFileName
  .replace(/\.[^/.]+$/, '')             // 확장자 제거
  .replace(/[-_]/g, ' ')                // 하이픈(-), 언더바(_) 공백으로 대체
  .trim();

// 이미지 설명(alt) 입력받기 (기본값 제공)
var imageAlt = await tp.system.prompt('이미지 설명(alt)을 입력하세요:', defaultAltText);

// 이미지 최종경로
const targetImgPath = `${imgFolderPath}/${imgFileName}`;

// 클립보드 이미지 처리
const { clipboard, nativeImage } = require('electron');
const image = clipboard.readImage();

if (image.isEmpty()) {
  new Notice('클립보드에 이미지가 없습니다.');
  return;
}

const imgBuffer = image.toPNG();
await vault.adapter.writeBinary(targetImgPath, imgBuffer);

// HTML 형식으로 최종 삽입 (클래스는 inline-icon으로 고정)
tR = `<img src="/${targetImgPath}" alt="${imageAlt}" class="inline-icon" />`;
%>