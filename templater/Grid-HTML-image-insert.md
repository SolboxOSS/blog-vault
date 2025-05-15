<%*
var gridClass = await tp.system.suggester(
  ["img-grid-2", "img-grid-3"],
  ["img-grid-2", "img-grid-3"],
  true,
  "이미지 그리드 클래스 선택:"
);

var imgCount = (gridClass === "img-grid-2") ? 2 : 3;
var imagesHTML = "";

for (var i = 1; i <= imgCount; i++) {
  var imagePath = await tp.system.prompt(i + "번째 이미지 경로를 입력하세요:");
  var imageAlt = await tp.system.prompt(i + "번째 이미지 설명(alt)을 입력하세요:");
  imagesHTML += '  <img src="' + imagePath + '" alt="' + imageAlt + '" />\n';
}

var finalHTML = '<div class="' + gridClass + '">\n' + imagesHTML + '</div>';

tR = finalHTML;
%>