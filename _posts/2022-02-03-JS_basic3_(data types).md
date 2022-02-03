---
title: "JS_basic3_(data types)"
date: 2022-02-03 
categories: JavaScript
---

# 3. 데이터타입, data types, let vs var, hoisting 

1. 프로그래밍의 3가지 중점(입력, 연산, 출력)
    - CPU에 최적화된 연산
    - 메모리를 최소화하여 사용

2. Variable
    - 변수: 변경될 수 있는 값
    1. let (added in ES6), rw(read,write)
        ```javascript
        let name = 'leo'; //변수의 선언과 할당
        console.log(name);
        name='hello'; // 변수에 새로운 값 할당
        condole.log(name);
        ```
        - 어플리케이션 실행시 사용시 사용가능한 메모리 할당함.
        - 처음에는 비어져 있다. 어플리케이션마다 사용하는 메모리가 제한적
        - name 정의시 하나의 메모리 저장소를 가르킬 수 있는 포인터가 생성됨
        - 해당 포인터가 지시하는 저장소에 변수의 값 (leo를 입력)
        - 값의 변경시 해당 포인터가 지시하는 저장소의 값 변경 (leo->hello)
    2. Block SCope
        - 코드를 Block { } 안에 작성하면 블럭 밖에서는 안을 볼 수 없다
        ```javascript
        let globalName = 'global name'; 
        //블록 밖에 선언하는 변수: global 변수(블록안,밖어디서나 접근가능)
        {
            let name = 'leo'; //변수의 선언과 할당
            console.log(name);
            name='hello'; // 변수에 새로운 값 할당
            console.log(name);
        }
        console.log(name); // 블록안의 값을 볼 수 없어 출력 내용이 없다
        console.log(globalName);
        ```
        - global 변수는 어플리케이션 실행부터 끝날때 까지 메모리에 탑재되어 있다. 가능한 사용을 자제하며, class 등 다른 방법을 통해 사용하는 것을 추천
        - block 변수는 해당 블록이 종료되면서 사라진다
    - let이전에는 var를 사용했다 (이제는 사용금지!!)
        - 일반적인 프로그래밍언어에서 변수 설정시 변수 선언을 하고 값을 할당 하지만, var를 사용시 선언도 하기전에 값을 할당하고,
        값이 없어도 'undefined'로 출력이 가능해짐
        - 즉 오류가 발생하지 않아 큰 문제를 야기한다. (주석참고)
        ```javascript
            //var (don't ever use this!)
            //var hoisting (move declaration from bottom to top)
            //변수의 선언 위치에 상관없이 제일 위쪽으로 끌어올림
            //has no block scope (블록에서 선언해도 아무곳에서나 출력가능)
            console.log(age); //undefined 
            age = 4;
            console.log(age); //4
            var age; //선언

            {
                name = 'leo';
                var name;
            }
            console.log(name); // leo 출력
        ```
    3. Constant, r(read only)
        - 값을 한번 할당하면 절대 변하지 않는 값
        - 변수를 할당하면 해당 변수가 포인터로 값이 입력된 메모리를 가리키는데, constant사용시 이 포인터가 잠기게 되어 값 변경 안됨
        - Mutable data type(값이 계속 변경가능한 변수): let
        - Immutable data type (값이 한번 할당되면 변경 안됨): const
        ```javascript
            //favor immutable data type always for a few reasons;
            //- security 
            //- thread safey (다양한 쓰레드 들이 동시에 변수에 접근해 값을 변경할 때 문제가 발생)
            //- reduce human mistakes
            const daysInWeek = 7;
            const maxNumber = 5;
            
            //Note!
            //Immutable data types: premitive types, frozen objects (i.e. object.freeze())
            //Mutable data types: all objects by default are mutable in JS
        ```
    4. Variable types

        ```javascript
            //primitive- single item: number, string, boolean, null, undefined, symbol
            //object- box container
            //function- first-class function (function을 변수에 할당,retunr가능)

            //javaScript에서는 타입이 dynamic하게 결정이 되기 때문에 하기처럼 number 등 타입을 명시하지 않아도 됨.
            let a = 12;
            let b = 1.2; 

            //typeScript의 경우는 명시해줘야 한다
            let a: number = 12;
            let b: number = 1.2;

            const count = 17; //integer
            const size = 17.1; //decimal number
            console.log(`value: ${count}, type: ${typeof count}`);
            console.log(`value: ${size}, type: ${typeof size}`);

            //number - special numeric values: infinity, -infinity, NaN
            const infinity = 1/0 ;
            const negativeInfinity = -1/0;
            const nAn = 'not a number' / 2;

            console.log(infinity);  //infinity
            console.log(negativeInfinity); //negativeInfinity
            console.log(nAn); //nAn

            //number의 사이즈 (-2^53)~(2^53);
            //bigInt(fairly new, don't use it yet)
            const bigInt = 123456789012345678901234567890n;
            console.log(`value: ${bigInt}, type:${typeof bigInt}`);
            Number.MAX_SAFE_INTEGER;


            //string
            const char = 'c';
            const brendan = 'brendan';
            const greeting = 'hello' + brendan; //문자 합 가능
            console.log(`value: ${greeting}, type: ${typeof greeting}`);
            const helloBob = `hi ${brendan}!`; //templete literals(stirng)-> '를 사용하지 않고 $로 간단하게 표현가능
            console.log(`value: ${helloBob},type: ${typeof helloBob}`);


            //boolean
            //false: 0, null, undefined, NaN, ''
            //true: any other value
            const canRead = true;
            const test = 3 < 1; //false
            console.log(`value: ${canRead}, type: ${typeof canRead}`);
            console.log(`value: ${test}, type: ${typeof test}`);

            //null : empty인값
            let nothing = null; 
            console.log(`value: ${nothing}, type: ${typeof nothing}`);

            //undefined : 선언되었지만 값을 모름, 값이 있는지 없는지 모름
            let x; 
            console.log(`value: ${x}, type: ${typeof x}`);

            //symbol, create unique identifiers for objects
            //map 등의 자료구조에서 고유한 식별자가 필요하거나 
            //동시에 다발적으로 일어날수 있는 코드에서 우선순위를 주려고 할 때 많이 사용
            //간혹 식별자를 String을 이용해서 사용하지만, 동일한 String을 사용하면 동일한 식별자로 간주
            //Symbol은 동일한 String으로 작성해도 다르게 간주한다
            const symbol1 = Symbol('id');
            const symbol2 = Symbol('id');
            console.log(symbol1 === symbol2); //false

            //String이 같으면 동일한 symbol로 만들어 주고 싶을때
            const gSymbol1 = Symbol.for('id');
            const gSymbol2 = Symbol.for('id');
            console.log(gSymbol1 === gSymbol2); //true
            console.log(`value: ${symbol1}, type: ${typeof symbol1}`);
            //symbol은 그냥 출력시 오류가 발생
            //항상 .description을 사용해 String으로 변환해서 출력해야함
            console.log(`value: ${symbol1.description}, type: ${typeof symbol1}`);

            //object, real-life object, data structure
            const leo = {name: 'leo', age: 20};
            //object의 경우  leo -> ref메모리주소 ->name, age를 가리킨다
            //따라서 const로 leo의 포인터 변경이 불가능해 object의 바깥은 수정이 불가능 하지만 name과 age의 포인터는 수정이 가능해 해당 값을 수정할 수 있다.
            leo.age=21;
        ```
    5. Dynamic typing: dynamically typed language
        - 자바스크립트는 런타임시 할당된 값에 따라 타입이 변경된다.
            - static type언어: 타입을 선언할때 같이 선언
        - 이런 dynamic 타입은 위험해 주의해야한다.
        ```javascript
        let text = 'hello'; //string
        console.log(`value: ${text}, type: ${typeof text}`);
        text = 1; //number
        console.log(`value: ${text}, type: ${typeof text}`);

        text = '7'+5; 
        //5를 string으로 간주해서 합한다: 75
        console.log(`value: ${text}, type: ${typeof text}`);

        
        text = '8'/'2'; 
        //문자는 나눌수가 없어 숫자로 간주해서 출력: 4, number
        console.log(`value: ${text}, type: ${typeof text}`);

        //처음의 타입이 string이기때문에 string인줄 알고 string관련 함수를 사용할경우 에러가 발생하게 된다
        
