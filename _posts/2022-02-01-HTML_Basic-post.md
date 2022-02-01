---
title: "HTML_Basic"
date: 2021-02-01 
categories: HTML
---

## HTML_Basic
1. Mark up 언어 : Tag를 이용해 구조적으로 작성된 언어
2. HTML 구조
  - <head> 사용자에게 보이지 않는 내용: 메타데이터만 존재
      <meta charset="utf-8"> : HTML문서에 사용되는 문자 set
      <meta name-"viewport" content="width=device=width"> 페이지 전체 사용
      <title>JS</tittle> 북마크, 브라우저 탭에 표현되는 내용
  - <body>
  - 웹사이트의 구조는 보통(Header, Nav-bar, Main-contents, side-bar, footer)로 구성
    - Section tag ( header, nav, main, aside, footer
  - 박스모델로 구성하는것이 중요!!
3.  Box 와 Item
  -BOX tag: header, footer, nav, aside, main, section, article, div, span, form
  -ITEM tag: a, button, label, img, video, audio, map, canvas, table : 사용자에게 보여지는 것
4. Block 와 Inline
  -<p class="editor-note">This is Content</p> 
    - <p class="editor-note">This is Content</p> 전체: element or tag or node
    - <p>:opening tag
    - </p>: closing tag
    - class="editor-note": Attribute
  -Block element: 한줄에 하나만 차지함
  -Inline element: 공간이 있으면 다른 tag옆에 배치가 가능함
5.Tag 간단 사용법
  -<a>
    ```
    <a href="https://google.com" target="_blank">Click</a>
    ```
    href: 주소, target: 창을 여는 방법
  -<p>,<b>,<span>: Inline tag 예시: 하나의 라인에 표현이 가능함
  
    ```
    <p>This is a sentence. That is...</p>
    <p>This is a sentence. <b>That</b> is...</p>
    <p>This is a sentence. <span>That</span> is...</p>
    ```
  -<div>사용시 라인이 넘어가게 된다
    
    ```
    <p>This is a sentence. <div>That</div> is...</p>
    ```
  
  -ol,ul,li: mdn에서 해당 태그의 속성 사용방법을 알 수있다  
   
   ```
    <ol type="i" reversed>
      <li>1</li>
      <li>2</li>
      <li>3</li>
    </ol>
    <ul>
      <li></li>
     <li></li>
     <li></li>
    </ul>
   ``` 
  
  - input : 사용자 입력을 받음, attribute를 통해 명시적으로 그룹화
   
  ```
    <label for="input_name">Name:</label>
    <input id="input_name" type="text">
    ```
  
## 추가내용
  - HTML, CSS, JS 관련 공식문서는 MDN을 통해서 확인
  - MDN > HTML elements reference (테그들의 설명과 예제, 각 섹션별로 테그가 나위어져 있음, 모든 브라우저에 적용가능한지 꼭 확인)
  - jsbin.com 브라우저상으로 html소스확인
  - validator.w3.org 해당소스의 태그들이 정확한지 확인해줌
  
