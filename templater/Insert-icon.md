<%*
const vault = app.vault;
const ICON_FOLDER = "support/icons";

// 해당 폴더의 PNG 파일 불러오기
const allFiles = (await vault.adapter.list(ICON_FOLDER)).files;
const pngFiles = allFiles.filter(f => f.endsWith(".png"));

// 선택 목록 준비
const fileNames = pngFiles.map(f => f.split("/").pop());
const filePaths = pngFiles;

const selectedPath = await tp.system.suggester(fileNames, filePaths, true, "아이콘을 선택하세요:");
if (!selectedPath) {
  new Notice("선택된 아이콘이 없습니다.");
  return;
}

// 기본 alt 텍스트 생성 (확장자 제거 → 특수문자 처리 → 공백 변환)
const rawName = selectedPath.split("/").pop().replace(/\.png$/, '');
const defaultAlt = rawName.replace(/[-_]/g, ' ').trim();

// 사용자로부터 alt 텍스트 확인 및 수정
const altText = await tp.system.prompt("아이콘 설명 (alt) 입력:", defaultAlt);

// 최종 img 태그 생성
tR = `<img src="/${selectedPath}" alt="${altText}" class="inline-icon" />`;
%>