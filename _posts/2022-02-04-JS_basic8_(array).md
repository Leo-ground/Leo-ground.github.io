---
title: "JS_basic8_(array)"
date: 2022-02-04 
categories: JavaScript
---
### 본 내용은 Dream Coding Academy의 강의 내용입니다 [Go to Dream Coding][dreamCodingLink]  

[dreamCodingLink]:  https://academy.dream-coding.com "Go Dream Coding"
- - - 
### 8. 자바스크립트 배열 개념과 APIs 총정리
- 비슷한 데이터들을 한 곳에 모으는것: 자료구조
- 어떤방식으로 어떤형식으로 데이터를 담는지에 따라 나뉨
- 자료구조와 Object의 차이
- Object: 서로 연관된 특징과 행동들을 묶음 (토끼, 당근, 자동차 등등)
- 자료구조: 동일한 타입의 Object들을 담는것
- JavaScript는 동적 타입언어이기 때문에 여러 타입이 섞인다
- 검색, 삽입, 정렬, 삭제를 효율적으로 하는 방법 (알고리즘, 자료구조)
- - - 

1. Declaration
    ```javascript
    const arr1 = new Array();
    const arr2 = [1, 2]; //배열은 인덱스를 기준으로 설정 0번째: 1
    ```
2. Index position
    ```javascript
    const fruits = ['apple', 'banana'];
    console.log(fruits);
    console.log(fruits.length);
    console.log(fruits[0]); //computed property와 혼동 주의 ['age'];
    console.log(fruits[1]); //banana
    console.log(fruits[2]); //undefined

    //배열의 마지막 값은 보통 length를 이용해서 구한다
    console.log(fruits[fruits.length - 1]);
    ```
3. Looping over an array
    ```javascript
    //print all fruits
    //a. for 사용
    for (let i = 0; i < fruits.length; i++) {
        console.log(fruits[i]);
    }

    //b. for of 사용
    for(let fruit of fruits){
        console.log(fruit);
    }

    //c. forEach
    //forEach는 callback함수를 반환
    // value, index, array를 사용한다, 모든 parameter가 필요한것은 아님
    fruits.forEach(function (fruit, index) {
        console.log(fruit, index, array);
    });

    //arrow function을 이용해 간단히 작성가능
    fruits.forEach((fruit) => console.log(fruit));
    ```
4. Addtion, deletion, copy
    ```javascript
    // push: add an item to the end
    fruits.push('orange','peach');
    console.log(fruits);

    // pop: remove an item from the end
    fruits.pop();
    console.log(fruits); //맨 뒤쪽의 값이 삭제됨

    // unshift: add an item to the begining
    fruits.unshift('lemon');
    console.log(fruits);

    // shift: remove an item from the begining
    fruits.shift();
    console.log(fruits);

    // note!! shift, unshift are slower than pop, push
    // splice: remove an item by index position
    fruits.push('mango','melon','tomato');
    //start index번호, 지울 갯수 (갯수 지정을 안하면 마지막까지 지움)
    //추가하고 싶은 데이터 작성도 가능
    //지워진 자리에 넣고 싶은 데이터가 들어가게됨
    fruits.splice(1, 1, 'hoho','haha');

    // combine two arrays
    // concat을 사용해 배열의 뒤쪽으로 합친다
    const fruits2 = ['paper', 'coconut'];
    const newFruits = fruits.concat(fruits2);
    console.log(newFruits);
    ```
    
5. Searching
    ```javascript
    // find the index
    console.clear() ;
    console.log(fruits);
    console.log(fruits.indexOf('apple')); // 0, 없을경우 -1 출력
    
    // includes
    // 해당 요소 포함되어 있는지 확인
    console.log(fruits.includes('apple'))// true (boolean)

    // lastIndexOf
    // 해당 배열에 동일 값이지만 다른 index로 존재하는 경우에 사용
    // indexof는 가장 앞쪽의 값을 찾음
    // 따라서 뒤쪽의 값을 찾을 때는 lastIndex of 사용
    console.log(fruits.lstIndexOf('apple'))
    ```
