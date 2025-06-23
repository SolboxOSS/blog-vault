<%*
const editor = app.workspace.activeEditor.editor;
const content = editor.getValue();
const updated = content.replace(/<br>/g, '<br />');
editor.setValue(updated);
%>