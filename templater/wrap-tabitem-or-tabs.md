<%*
const selected = tp.file.selection();
if (!selected || selected.trim() === "") {
  tR = "⚠️ Please select text before running this template.";
  return;
}

// 선택한 문장을 줄 단위로 나눔
const lines = selected.split("\n");

// 선택지: Tabs 또는 TabItem
const wrapType = await tp.system.suggester(["Tabs", "TabItem"], ["Tabs", "TabItem"]);

if (wrapType === "Tabs") {
  const hasTabItem = lines.some(line => line.includes("<TabItem"));
  if (!hasTabItem) {
    tR = "❌ Error: No <TabItem> block found in the selected text. Tabs require at least one <TabItem>.";
    return;
  }

  // Tabs로 감싸기
  tR = `import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs>
${selected}
</Tabs>`;
} else {
  // TabItem 개별 생성 흐름
  const label = await tp.system.prompt("Enter label for TabItem", "Tab Label");
  const value = await tp.system.prompt("Enter value for TabItem", label);

  tR = `<TabItem value="${value}" label="${label}">
${selected}
</TabItem>`;
}
%>
