---
title: "JS_basic10_(JSON)"
date: 2022-02-06 
categories: JavaScript
---

### 10.  JSON 개념 정리 와 활용방법
- Browser위에서 동작하는 웹사이트 or 웹어플리케이션 Clint들이 Server와 통신 할 수 있게 하는 것: HTTP (Hypertext Transfer Protocal)
- HTTP 프로토콜은 Client가 Server로 request (데이터 요청)
- Server는 request에 해당하는 값을 response (데이터 응답)
- Hypertext: 하이퍼링크. text, 이미지 등 
- Http를 통해서 서버에 데이터를 요청해 받아올 수 있는 방법
    - AJAX(Asynchronous JavaScript And XML)
        - 웹페이지에서 서버에게 동적으로 데이터를 요청하고 받아오는 기술
        - 대표적인 예:object로 XHR (XMLHttpRequest): 브라우저 API에서 제공하는 object중에 하나로, 간단하게 서버에게 데이터를 요청하고 받아올 수 잇다.
        - 최근 fetch() API로 간단하게 가능
    - XML: HTML과 같은 Mark up 언어중 하나
    - 서버와 데이터를 주고 받을 때는 XML 뿐만 아니라 다양한 데이터 포멧을 사용할 수 있다
    - XHR은 실제 XML이외의 다른 포멧사용이 가능하다
- 최근 많이 사용하는 포멧 JSON: JavaScript Object Notation 
        - JavaScript의 Object처럼 key와 value로 이루어져 있다
        - Object{ket: value}
        - 브라우저 뿐만아니라 모바일에서 서버와 데이터를 주고받을 때, 서버와 통신할때뿐만아니라 Object를 파일시스템에 저장할 때 사용
- - -
- JSON
    - simplest data interchange format
    - lightweight text-based structure
    - easy to read
    - key-value pairs
    - used for serialization and transmission of data between the network the network connection
    - independent programming language and platform!!!!
- JSON 공부방법
    - object를 serialize해서 어떻게 JSON String으로 변환할지
    - serialize된 JSON을 다시 object로 변환 할지
- - - 

1. Object to JSON
    ```javascript
     // stringify(obj)   
     let json = JSON.stringify(true);
     console.log(json); // true (String)

     json = JSON.stringify(['apple', 'banna']);
     console.log(json); //["apple", "banna"] (String)

     const rabbit = {
         name: 'tori',
         color: 'white',
         size: null,
         birthDate: new Date(),
         symbol: Symbol('id'),
         jump: () => {
             console.log(`${name} can jump!`);
         },
     }

     json = JSON.stringify(rabbit);
     console.log(json);  //jump()는 object에 포함되지 않음
     // JavaScript에만 있는 Symbol도 JSON으로 변환되지 않음
    
    //replacer: 특정한 key값만 출력하기 위해서는 replacer위치에 하기처럼 명시 (형태는 callback fn, array)
    json = JSON.stringify(rabbit,['name','color']);
     console.log(json);
    
    // replacer에 callback fn 사용
    json = JSON.stringify(rabbit, (key, value) => {
        console.log(`key: ${key}, value: ${value}`);
        return key === 'name' ? 'leo' : value;
    });
     console.log(json);
    ```

2. JSON to Object
    ```javascript
    // parse(json)
    json = JSON.stringify(rabbit); //obj를 json으로 변환 위 1번과정
    // json을 object로 변환
    const obj = JSON.parse(json);
    console.log(obj);
    rabbit.jump() ; //사용가능
    obj.jump(); //사용 불가능 에러발생
    //rabbit을 json으로 변환시에 jump()는 포함되지 않음
    //따라서  json을 obj로 다시 변환시 jump()는 존재하지 않음

    console.log(rabbit.birthDate.getdate()); // date 출력
    console.log(obj.birthDate); //json으로 변환시 저장되었던 값이 출력
    // ex: 2022-02-06T13:25:57.063Z
    // 따라서 reviver 위치에 callback fn를 사용해 date를 수정해서 출력
    const obj = JSON.parse(json), (key,value) => {
        console.log(`key: ${key}, value: ${value}`);
        return key === 'birthDate' ? new Date(value) : value;
    };
    console.log(obj.birthDate.getDate());
    ```
- - - 

- 참고
- JSON에 대해 조금더 공부를 하고 싶으시면: 
- MDN ➡️ https://developer.mozilla.org/en-US/d...
- JavaScript.info ➡️ https://javascript.info/json
- JavaScript.info 한국어 ➡️ https://ko.javascript.info/json 

- 유용한 사이트:
- JSON Diff checker: http://www.jsondiff.com/
- JSON Beautifier/editor: https://jsonbeautifier.org/
- JSON Parser: https://jsonparser.org/
- JSON Validator: https://tools.learningcontainer.com/j...
