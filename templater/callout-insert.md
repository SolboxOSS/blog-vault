<%*
var type = await tp.system.suggester(
  ["note", "info", "tip", "caution", "danger", "important", "warning"],
  ["note", "info", "tip", "caution", "danger", "important", "warning"],
  true,
  "Callout 유형(type)을 선택하세요:"
);

var name = await tp.system.prompt("Callout 이름(Name)을 입력하세요 (없으면 빈칸으로):");

var calloutHeader = "::: " + type;
if (name && name.trim().length > 0) {
  calloutHeader += " " + name.trim();
}

var finalCallout = calloutHeader + "\n[여기에 작성하고 싶은 내용을 작성]\n:::";

tR = finalCallout;
%>