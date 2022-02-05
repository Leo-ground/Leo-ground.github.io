---
title: "JS_basic7_(class_object)"
date: 2022-02-04 
categories: JavaScript
---

### 7. 오브젝트 넌 뭐니? 
1. Literals and properties
    ```javascript
    // one of the JavaScript's data types.
    // a collection of related data and/or functionality.
    // Nearly all objects in JavaScript are instances of Object
    // object = { key : value};

    const obj1 = {}; // 'object literal' syntax
    const obj2 = new Object(); // 'object constructor' syntax

    const name = 'leo';
    const age = 4;

    // 해당값을 함수에서 사용하기 위해서는 두개의 파라미터를 명시해야하며
    // 함수의 정의와 호출시에도 명시해야된다
    // 이러한 방식의 경우 파라미터가 하나가 추가되면 수정사항이 많아진다

    print(name, age);
    function print(name, age){
        console.log(name);
        console.log(age);
    }

    // 이러한 문제점을 해결하기 위해 Object를 사용

    const leo = { name: 'leo', age: 4};

    function print(person){ // 하나의 object파라미터를 받아오게 함.
        console.log(person.name);
        console.log(person.age);
    }

    print(leo);

    // JavaScript는 런타임시 타입이 결정되어 object정의 후 값 추가가 가능
    // 하지만 유지보수에 어려움이 있기때문에 사용하지 않는 것을 추천
    leo.hasJob=trus;
    console.log(leo.hasJob);

    //삭제도 가능함
    delete leo.hasJob;
    console.log(leo.hasJob);
    ```
2. Computed properties
    ```javascript
    // object 접근시 . 을 사용하는 방법
    // *코딩하는 그 순간 key의 해당하는 값을 받아오고 싶을때 사용
    console.log(leo.name);
    //[string]을 사용하는 방법(Computed properties)
    // key should be always string
    // *런타임에서 키가 결정될때 사용
    console.log(leo['name']);
    leo['hasJob' = true; // property 추가
    console.log(leo.hasJob);

    // 위에서 *이 의미하는 내용
    // 아래의 함수와 같이 key를 사용자의 입력값으로 결정된다고 하면
    // 코딩하는 당시에는 key가 어떤 값인지 알수가 없다 (. 사용불가)
    // 따라서 이러한 경우에 coputed properties를 사용
    function printValue(obj, key) {
        console.log(obj.key); // undefined
        console.log(obj[key]);
        //동적으로 key의 value를 받아와야할때 유용하게 사용된다
    } 

    printValue(leo, 'name'); 
    printValue(4, 'age'); 
    ```
3. Property value shorthand
    ```javascript
    const person1 = { name: 'bob', age: 2};
    const person2 = { name: 'steve', age: 3};
    const person3 = { name: 'dave', age: 4};
    //사람을 계속 추가할때마다 작성해야하는 불편함이 있음

    //함수로 name,age를 파라미터로 받아서 object로 return을 해줌
    function makePerson(name, age){
        return {
            name: name,
            age: age,
            //JavaScript에서는 property short handle 기능으로
            //key와 value의 명칭이 같으면 하나만 써도됨
            //name,
            //age,
        };
    }
    const person4 = makePerson('leo',30);
    console.log(person4)

    // makePerson 함수는 템플릿기능을 한다.
    // class등장전에 이러한 함수를 템플릿으로 사용했다
    // 이렇게 object를 생성하는 템플릿 함수는 이름을 대문자 시작으로 하며
    // return을 사용하지 않고, class의 constructor 처럼
    // this를 사용한다
    function Person(name, age) {
        //this = {};
        this.name = name;
        this.age = age;
        // return this;
    }
    // 호출할 때는 class에서 object를 만드는 것처럼 new를 사용
    const person5 = new Person('hoho', 30)
    ```
4. Constructor function
    - 위의 Person 함수와 같은 함수를 말한다.

5. in operator: property existence check (key in obj)
    ```javascript
    // 해당하는 object안에  key가 있는지 없는지 확인
    console.log('name' in leo); //true
    console.log('age' in leo); //true
    console.log('random' in leo); //false
    console.log(leo.random); //undefined
    ```
6. for..in vs for..of
    ```javascript
    // 프로젝트에서 유용하게 사용된다
    
    // for (key in obj)
    // obj에 있는 키들이 블럭을 돌때 마다 key에 할당된다. 
    for (key in leo){
        console.log(key);
    }

    // for (value of iterable)
    // 배열, list의 경우에 사용한다 (순차적인 데이터)
    const array = [1, 2,3, 4, 5];

    //기존의 방식
    for(let i = 0; i < array.length ; i++>) {
        console.log(array[i]);
    }

    //for..of 사용
    for(value of array){
        console.log(value);
    }
    ```
7. Fun cloning
    ```javascript
    // Object.assign(dest, [obj1, obj2, obj3...])
    const user = { name: 'leo', age: '20' };
    const user2 = user;
    //위의 의미는 user는 obj의 ref메모리 주소를 가리키며,
    // ref는 name, age를 가리킨다
    // user2에 user에 해당하는 ref를 가리키게 할당함
    // 따라서 user2의 name의 값을 변경하고 user를 출력하면
    user2.name = 'coder';
    console.log(user); // name이 coder로 출력된다

    // old way
    // 빈 object를 만들고
    // for..in과 computed property를 사용해 user3에 user의 값을 넣는다
    // 이 경우는 user의 ref값과 user3의 ref가 다름
    const user3 ={} ;
    for (key in user) {
        user3[key] = user[key];
    }
    console.log(user3);

    //Object.assign 사용
    //Object는 JavaScript에 기본적으로 탑제된 object이며, 모든 object들은 Object를 상속받음
    const user4 = {}; //empty object생성
    Object.assign(user4, user); // target, source
    console.log(user4);
    //또는 아래와 같이 작성가능
    const user44 = Object.assign({}, user);
    
    //another example
    const fruit1 = { color: 'red' };
    const fruit2 = { color: 'blue', size: 'big' };
    const mixed =  Object.assign({}, fruit1, fruit2);
    //동일한 key값을 갖게되면 뒤쪽에 나온 obj의 값이 덮어 씌워진다
    console.log(mixed.color); //blue
    console.log(mixed.size); //big
    ```

    
