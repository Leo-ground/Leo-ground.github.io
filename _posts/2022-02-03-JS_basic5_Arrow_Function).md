---
title: "JS_basic5_Arrow_Function)"
date: 2022-02-03 
categories: JavaScript
---

# 5. Arrow Function은 무엇인가? 함수의 선언과 표현
- function 이란: input (변수)를 받아서 ouput (return값)을 return해줌
- function의 이름을 보면 해당 기능을 알 수있게 지어야 한다.

1. Function declaration
    ```javascript
    // fundamental building block in the program
    // subprogram can be used multiple times
    // performs a task or calculates a value
    
    // 1. Function declaration
    // function name(param1, param2){ body... return ;}
    // one function === one thing
    // naming: doSomething, command, verb
    // e.g. createCardAndPoint -> createCard, createPoint
    // function is object in JS
 
    //함수의 정의
    function printHello() {
        console.log('Hello');
    }

    printHello(); //함수의 호출
    //위의 함수는 사용이 제한적임 (Hello만 출력)
    //따라서 변수를 사용
    function log(message){
        console.log(message);
    }
    log('Hello@');
    log(1234); //string으로 변환되어 출력된다
    ```

2. Parameters
    ```javascript
    //premitive parameters: passed by value
    //object parameters: passed by reference
    function changeName(obj) {
        obj.name = 'coder';
    }
    const leo = { name: 'leo' };
    changeName(leo);
    console.log(leo) //coder
    //ref변경된 사항이 메모리에 저장되어 추후에 확인이 가능함
    ```
3. Default parameters (added in ES6)
    - pramter에 값이 없을경우 undefined대신에 입력하는 값을 지정
    ```javascript
    function showMessage(message, from = 'unknown') { //unknown이 default parameter
        console.log(`${message} by ${from}`);
        //default parameter가 나오기 이전에는 하기내용을 추가해서 사용함
        //if(from === undefined) {
        //    from = 'unknown';
        //}
        console.log(`${message} by ${from}`);
    }
    showMessage('Hi!');

4. Rest parameters (added in ES6)
    ```javascript
    function printAll(...args){ //배열 parameter
        for (let i = 0; i < args.length; i++){
            console.log(args[i]);
        }

        //of를 사용해 간단하게 출력가능
        for (const arg of args) {
            console.log(arg);
        }

        //forEach를  사용해 간단하게 출력가능
        args.forEach((arg) => console.log(arg));

    }
    printAll('dream','coding','ellie');

5. Local scope
    - 밖에서는 안이 보이지 않고 안에서만 밖을 볼 수 있다.
    ```javascript
    let globalMessage = 'global'; //global variable
    function printMessage() {
        let message = 'hello';
        console.log(message); //local variable
        console.log(globalMessage);

        function printAnother() {
            conseole.log(message);
            let childMessage = 'hello';
        }
        console.log(childMessage); //에러 발생
    }    
    printMessage();
    console.log(message); //에러발생
    ```

6. Return a value
    - return을 명시하지 않은 함수들은 (return undefined;)가 생략된 것.
    ```javascript
    function sum(a, b){
        return a + b;
    }
    const result = sum(1, 2); //3
    console.log(`sum: ${sum(1, 2)}`);

7. Early return, early exit
    ```javascript
    //bad
    //블럭안에 로직을 넣게 되면 가독성이 떨어짐 
    function upgradeUser(user) {
        if(user.point > 10) {
            //long upgrade logic...
        }
    }

    //good
    //조건에 맞지 않을 때는 빨리 return을 시킴
    function upgradeUser(user) {
        if (user.point <= 10) {
            return;
        }
        // long upgrade logic...
    }
    ```
- - -
1. Function expression
    - a function declaration can be called earier than it is defiend.(hoisted)
    - a function expression is created when the execution reaches it.
    ```javascript
    //변수를 선언하면서 함수를 선언 (함수명이 없음)
    const print = function () {  //anonymous function
       //funcion print() 이름이 있는 것은 named function
       //named function의 경우 var 처럼 함수 선언전에 호출해서 사용가능(hoisted)
        console.log('print');
    };
    print();
    const printAgain = print;
    printAgain();
    const sumAgain = sum; //위의 sum 함수
    console.log(sumAgain(1,3));

2. Callback function using function expression
    ```javascript
    // 함수를 parameter에 넣어 해당 조건이 맞으면 함수를 호출하게 함
    function randomQuiz(answer, printYes, printNo){
        if(answer === 'love you') {
            printYes();
        }else {
            printNo();
        }
    }

    // anonymous function
    const printYes = function () {
        console.log('yes!');
    };

    // named function
    // better debugging in debugger's stack traces
    // recursions 함수안에서 함수를 호출 할때 
    const printNo = function print() {
        console.log('No!');
        //print(); //recursions
    };
    randomQuiz('wrong', printYes, printNo);
    randomQuiz('love you', printYes, printNo);


    // Arrow function
    // always anonymous
    const simplePrint = function () {
        console.log('simplePrint!');
    };
    
     const simplePrint = () => console.log('simplePrint!');
     const add = (a,b) => a + b;
     //위 함수를 바꾸면
     //const add = function (a, b) {
     //    return a + b;
     //}
     
     // block이 필요한경우 아래와 같이 사용가능
     const simpleMultiply = (a,b) =>{
         //do something more
         return a * b;
     };

     // IIFE: Immediately Invoked Function Expression
     // 보통은 함수를 선언하고 호출하지만
     function hello() {
         console.log('IIFE');
     }
     hello();

     //함수를 선언함과 동시에 호출하는 경우
     (function hello() {
         console.log('IIFE');
     })();

- - -
- Fun quiz time
- function calculate(command, a, b)
- command: add, substract, divide, multiply, remainder
 

```javascript
    function calculate(command, a, b) {
        switch(command){
        case 'add':
            console.log(a + b);
            break;
        case 'substract':
            console.log(a - b);
            break;
        case 'divide':
            console.log(a / b);
            break;
        case 'multiply':
            console.log(a * b);
            break;
        case 'remainder':
            console.log(a % b);
            break;
        default:
             console.log('you wrote wrong command');
             break;
        }
    }

    calculate('add',1,2);
    calculate('substract',1,2);
    calculate('divide',1,2);
    calculate('multiply',1,2);
    calculate('remainder',1,2);
    calculate('chuchu',1,2);
```
