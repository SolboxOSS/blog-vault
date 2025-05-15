<%*
var imagePath = await tp.system.prompt('이미지 경로를 입력하세요:');
var imageAlt = await tp.system.prompt('이미지 설명(alt)을 입력하세요:');
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

var result = '<img src="' + imagePath + '" alt="' + imageAlt + '" class="' + size + ' ' + align + '" />';

tR = result;
%>