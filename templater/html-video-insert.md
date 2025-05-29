<%*
const vault = app.vault;
const file = tp.file.find_tfile(tp.file.path(true));
const relativeFolderPath = file.parent.path;
const videoFolderPath = `support/videos/${relativeFolderPath}`;

// 폴더가 없으면 생성
if (!(await vault.adapter.exists(videoFolderPath))) {
  await vault.createFolder(videoFolderPath);
}

// OS 자동 인식
const os = require('os').platform();
const { clipboard } = require('electron');

let filePath = "";

// OS 자동 확인 후 클립보드 경로 가져오기
if (os === 'win32') {
  filePath = clipboard.read('FileNameW');
} else if (os === 'darwin') {
  filePath = clipboard.read('public.file-url');
  if (filePath.startsWith('file://')) {
    filePath = decodeURIComponent(filePath.replace('file://', ''));
  }
}

// 클립보드에서 경로를 얻지 못한 경우 사용자 직접 입력
if (!filePath || !filePath.match(/\.(mp4|mov|webm|m4v)$/i)) {
  filePath = await tp.system.prompt('클립보드에서 파일을 찾지 못했습니다. 비디오의 전체 경로를 직접 입력하세요 (윈도우는 탐색기 경로, 맥은 Finder에서 Option+우클릭으로 경로 복사 후 입력):');
  
  if (!filePath || !filePath.match(/\.(mp4|mov|webm|m4v)$/i)) {
    new Notice('입력한 경로가 올바르지 않거나 지원되지 않는 비디오 형식입니다.');
    return;
  }
}

// 파일명 추출 및 입력
const path = require('path');
let originalFileName = path.basename(filePath);
let videoFileName = await tp.system.prompt('비디오 파일명을 입력하세요 (확장자 제외):', originalFileName.replace(/\.[^/.]+$/, ''));
if (!videoFileName) return;
const fileExt = path.extname(originalFileName);
videoFileName += fileExt;

// caption 자동 생성 및 입력
const defaultCaptionText = videoFileName
  .replace(/\.[^/.]+$/, '')
  .replace(/[-_]/g, ' ')
  .trim();
const videoCaption = await tp.system.prompt('비디오 설명(caption)을 입력하세요:', defaultCaptionText);

// 최종 경로 설정
const targetVideoPath = `${videoFolderPath}/${videoFileName}`;

// 파일 복사 수행
const fs = require('fs');
try {
  await fs.promises.copyFile(filePath, path.join(vault.adapter.basePath, targetVideoPath));
} catch (error) {
  new Notice(`비디오 복사 실패: ${error.message}`);
  return;
}

// 크기 및 정렬 선택
const size = await tp.system.suggester(
  ["video-small", "video-medium", "video-large"],
  ["video-small", "video-medium", "video-large"],
  true,
  "비디오 크기를 선택하세요:"
);
const align = await tp.system.suggester(
  ["video-left", "video-center", "video-right"],
  ["video-left", "video-center", "video-right"],
  true,
  "비디오 정렬을 선택하세요:"
);

// HTML 비디오 삽입
tR = `
<video src="/${targetVideoPath}" class="${size} ${align}" controls muted loop playsinline>
  ${videoCaption}
</video>
`;
%>