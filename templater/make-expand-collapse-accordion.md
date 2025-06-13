<%*
const selected = tp.file.selection();
if (!selected || selected.trim() === "") {
  tR = "⚠️ Please select some text before running this template.";
  return;
}

// 첫 줄 추출 + markdown heading 문자 제거
let firstLine = selected.split("\n")[0].trim();
firstLine = firstLine.replace(/^#+\s*/, ""); // "#", "##", "### " 등 제거

// 사용자에게 summary 입력 받기
const summary = await tp.system.prompt("Enter summary for <details>", firstLine);

// 아코디언 형식으로 출력
tR = `<details>
<summary>${summary}</summary>

${selected}

</details>`;
%>