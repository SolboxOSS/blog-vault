<%*
const selected = tp.file.selection().trim();

if (!selected) {
  new Notice('먼저 배열할 HTML 이미지를 선택해주세요.');
  return;
}

const lines = selected.split("\n").filter(line => line.trim().length > 0);
if (lines.length !== 2 && lines.length !== 3) {
  new Notice('이미지는 반드시 2개 또는 3개를 선택해야 합니다.');
  return;
}

const gridType = lines.length;

let finalHTML = `<div class="img-grid-${gridType}">\n`;
lines.forEach(line => {
  finalHTML += line.trim() + "\n";
});
finalHTML += "</div>";

tR = finalHTML;
%>