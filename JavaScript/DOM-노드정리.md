DOM-노드정리
========

## DOM(Document Object Model)
## 노드(node)
- 연결망에서 특정 지점과 지점을 연결하는데 표시하는 것.
- `요소 노드(Element node)` : 태그 e.g) `<html>`,`<p>`..
- `텍스트 노드(text node)` : 태그 안에 들어가는 컨텐츠 
- `속성 노드(attribute node)` : 요소 안에 포함되는 속성 e.g) `<p title="abc">`

## getElementById
- html 문서에서 지정된 아이디 속성을 포함하는 단 하나의 요소를 참조 -> 하나의 객체가 됨
```js
document.getElementById("idname")
```
## getElementByTagName
- 특정 태그를 사용하는 요소들을 배열로 얻어낼 수 있다.
- id와 다르게 여러개의 같은 이름을 사용하는 태그를 얻게 된다.
```js
document.getElementByTagName("li")
document.getElementByTagName("li").length;

for (var i=0; i<document.getElementByTagName("li").length; i++){
    alert(typeof document.getElementByTagName("li")[i]);
}

//변수로 지정하기
var items = document.getElementByTagName("li");
for(var i=0; i<items.length; i++){
    alert(typeof items[i]);
}

//모든 요소를 배열에 넣기
alert(typeof document.getElementByTagName("*").length);
```

## getAttribute
```js
object.getAttribute("속성명")

var paras = document.getElementByTagName("p");
for (var i=0; i<paras.length; i++){
    alert(paras[i].getAttribute("title"));
}
```

## setAttribute
- 특정 속성 노드의 값을 바꿀 수 있다.
```js
object.setAttribute("바꾸고 싶은 속성","바꿀 값")

var shopping = document.getElementById("parchases");
shopping.setAttribute("title","a list of goods");
```