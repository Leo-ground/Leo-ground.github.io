---
title: "JS_basic4_(operator_if_loop)"
date: 2022-02-03 
categories: JavaScript
---

# 4. 코딩의 기본 operator, if, for loop

1. String concatenation
    ```javascript
    console.log('my' +' cat'); 
    console.log('1'+2);
    console.log(`string literals: 1+2 = ${1+2}`);
    ```
2. Numeric operators
    ```javascript
    console.log(1+1); //add
    console.log(1-1); //substract
    console.log(1/1); //divide
    console.log(1*1); //multiply
    console.log(5%2); //remainder
    console.log(2 ** 3); //exponentiation
    ```
3. Increment and decrement operators
    ```javascript
    let counter = 2;
    const preIncrement = ++counter;
    //counter= counter+1;
    //preIncrement = counter;
    console.log(`preIncrement: ${preIncrement}, counter: ${counter}`)//3,3
    const postIncrement = counter++;
    //postIncrement = counter
    //counter = counter+1;     
     console.log(`preIncrement: ${preIncrement}, counter: ${counter}`)//3,4
    //--도 같은 방식으로 적용된다
    ```
4. Assignment operators
    ```javascript
    let x = 3;
    let y = 6;
    x += y; // x = x + y;
    x -= y; 
    x *= y;
    x /= y;

5. Comparison operators
    ```javascript
    console.log(10 < 6); // less than
    console.log(10 <= 6); //less than or equal
    console.log(10 > 6) // greater than
    console.log(10 >= 6); //greater than or equal

6. Logical operators: ||(or), &&(and), !(not)
    ```javascript
    const value1 = false;
    const value2 = 4 < 2;

    // ||(or), finds the first truthy value
    console.log(`or: ${value1 || value2 || check()}`); //true
    //or연산자는 첫번째가 true면 이미 true이기때문에 뒷부분 연산을 하지 않아
    // value1=true 인경우 no way~가 출력되지 않고 바로 true만 출력하게 된다
    // 즉 simple한 값을 앞부분에 놓고 함수등 무거운 것들은 뒤쪽으로 하는게 좋다

    function check() {
        for (let i = 0; i < 10; i++) {
            //wasting time
            console.log('no way~');
        }
        return true;
    }

    //&& (and), finds the first falsy value
    console.log(`or: ${value1 || value2 || check()}`); //false
    //and 연산자의 경우 첫번째가 false면 뒤부분 연산을 하지 않는다

    //often used to compress long if-statment
    //nullableObject && nullableObject.something
    if(nullableObject != null){ //null확인
        nullableObject.something;
    }

    //!(not)
    console.log(!value1);
    ```

7. Equality
    ```javascript
    const stringFinve = '5';
    const numberFive = 5;

    // == loose equality, with type conversion
    console.log(stringFive == numberFive); //true
    console.log(stringFive != numberFive); //false

    // === strict equality, no type conversion
    console.log(stringFive === numberFive); //false
    console.log(stringFive !== numberFive); //true

    //****object equality by reference
    //object의 경우 ref 포인터만 변경이 안된다
    const ellie1 = { name: 'ellie' };
    const ellie2 = { name: 'ellie' }; 
    const ellie3 = ellie1; //ellie1과 같은 ref 가리킨다
    console.log(ellie1 == ellie2);  //false
    console.log(ellie1 === ellie2); //false
    console.log(ellie1 === ellie3); //true

    //equality - puzzler
    console.log(0 == false); //true
    console.log(0 === false); //false
    console.log('' == false); //true
    console.log('' === false); //false
    console.log(null == undefined); //true
    console.log(null === undefined); //false
    ```

8. Conditional operators: if
    ```javascript
    // if, else if, else
    const name = 'ellie'; //coder, leo 인경우 각각 두번쨰, 세번째 출력
    if(name === 'ellie') {
        console.log('Welcome, Ellie!');
    }else if (name === 'coder'){
        console.log('You are amazing coder');
    }else {
        console.log('unknown');
    }
    ```

9. Ternary operator: ?
    ```javascript
    //condition ? value1 : value2;
    console.log(name === 'ellie' ? 'yes' : 'no');
    ```

10. Switch statement
    ```javascript
    //use for multiple if checks
    //use for enum-like value check
    //use for multiple type checks in TS
    const browser = 'IE';
    switch (browser) {
        case 'IE' :
            console.log('go away!');
            break;
        case 'Chrome':
        //    console.log('love you!'); 
        //    break;
        // 같은 내용의 경우 연달아 case를 명시해 주면 됨
        case 'Firefox':
            console.log('love you!');
            break;
        default:
            console.log('same all!');
            break
    }

11. Loops
    ```javascript
    //while loop, while the condition is truthy,
    //body code is executed.
    let i = 3;
    while (i > 0){
        console.log(`while: ${i}`);
        i--;
    }

    //do while loop, body code is executed first,
    //then check the condition.
    do {
        console.log(`do while: ${i}`);
        i--;
    } while (i > 0);
    //block을 먼저 실행하고 싶은면 do-while
    //조건에 맞는것만 실행하고 싶으면 while

    // for loop, for(begin; condition; step)
    for (i = 3; i > 0; i--){
        console.log(`for: ${i}`);
    }

    for (let i = 3; i > 0; i = i - 2){
        //inline variable declaration
        console.log(`inline variable for: ${i}`);
    }

    //nested loops
    //cpu 연산시 O(n**2)이므로 되도록 피하는것이 좋다
    for(let i = 0; i < 10; i++){
        for (let j = 0; j < 10; j++){
            console.log(`i: ${1}, j:${j}`);
        }
    }

    //break, continue
    //Q1. interate from 0 to 10 and print only even numbers(use continue)
    for(let i = 0; i < 11; i++){
        if(i % 2 === 0){
            console.log(`even number: ${i}`);
        }
    }

    for(let i = 0; i < 11; i++){
        if(i % 2 !== 0){
            continue;
        }
        console.log(`even number: ${i}`);
    }

    for(let i = 0; i < 11; i++){
        switch(i) {
            case 2:
                console.log(`even number: ${i}`);
                continue;
            case 4:
                console.log(`even number: ${i}`);
                continue;
            case 6:
                console.log(`even number: ${i}`);
                continue;
            case 8:
                console.log(`even number: ${i}`);
                continue;
        }
    }   
    
    //Q2. iterate from 0 to 10 and print numbers unitl reacing 8(use break)
    for(let i = 0; i < 11; i++){
        if(i >8){
            break;
        }
        console.log(`number: ${i}`);
    }
