---
title: "JS_basic6_(class_object)"
date: 2022-02-03 
categories: JavaScript
---

### 6. 클래스와 오브젝트의 차이점(class vs object), 객체지향 언어 클래스 정리

1. class
    - 붕어빵 틀, 청사진, template 으로 많이 불린다
    - class에는 값은 없고 template만 정의해 놓는다
    - '이 class에는 어떠한 데이터만 들어 올 수 있어 등 정의하고 선언!
    1. template
    2. declare once
    3. no data in

2. object
    - class에 데이터를 넣어서 만드는 것이 object
    - 클래스를 통해 다수의 object생성가능
    - class는 정의만 한 것 이라 메모리에 올라가진 않지만 object는 올라간다
    1. instance of a class
    2. created many times
    3. data in
- - -
1. Class declarations
    ```javascript
    // Object-oriented programming
    // class: template
    // object: instance of a class
    // JavaScript classes
    // - introduced in ES6 (class가 나오기전 function을 사용했다)
    // - syntactical sugar over protptype-based inheritance
    
    class Person {
        // constructor :fields에 전달된 data를 할당 (생성자)
        constructor(name, age) {
            //fields
            this.name = name;
            this.age = age;
        }

        // methods
        speak() {
            console.log(`${this.name}: hello!`);
        }
    }

    //object 생성
    const leo = new Person('leo', 20);
    console.log(leo.name); //leo
    console.log(leo.age); // 20
    leo.speak(); // leo: hello!
    ```
2. Getter and setters
    ```javascript
    class User {
        constructor(firstName, lastName, age) {
            this.firstName = firstName;
            this.lastName = lastName;
            this.age = age;
            //getter, setter를 정의하면
            //this.age는 메모리에 있는 데이터를 읽어오는게 아니라
            //get age()를 호출
            //= age;는 바로 값을 메모리에 할당하는 것이아니라
            //set age(value)를 호출
        }
            //*****최종: User class에는 firstName,lastName, _age 3개의 필드존재 

        //값을 return
        get age() {
            //return this.age;
            //setter의 무한반복과 같은 이유로
            return this._age;
        }

        //값을 설정
        set age(value) {
            //this.age = value; 
            //즉 = value는 다시 setter를 호출하고 무한반복 된다
            //따라서 사용되는 변수를 아래와 같이 바꾼다
            this._age = value;

            //if (value < 0 ) {
            //    throw Error('age can not be negative');
            //}
           this._age = value < 0 ? 0 : value; 
        
        }
    }

    //나이가 -1로 출력되 때문에 이러한 상황을 막는 방어 로직필요(get,set)
    const user1 = new User('Steve', 'Job'. -1);
    console.log(user1.age); //호출은 .age로 함(_age가 아님)
    ```
3. Fields (public, private)
    - Too soon!
    ```javascript
    class Experiment {
        publicField = 2;
        #privateField = 0; //class내부에서만 읽고 바꿀수 있다
    }

    const experiment = new Experiment();
    console.log(experiment.publicField);
    console.log(experiment.privateField); //undefined
    ```

4. Static properties and methods
    - Too soon!
    ```javascript
    class Article {
        // Class안에 있는 fields와 method들은 새로운 object를 만들때 마다
        // 그대로 복제되어서 값만 지정한 값으로 변경되어 만들어진다.
        // object나 data에 상관없이 class가 가진 고유한 값과
        // 동일하게 반복되어 사용되어 지는 method들을 사용할때 유용하다
        // object에 상관없이 class에 연결

        static publisher = 'leo ground';
        constructor(articleNumber) {
            this.articleNumber = articleNumber;
        }

        static printPublisher() {
            console.log(Article.publisher);
        } 
    }

    const article1 = new Article(1);
    const article2 = new Article(2);
    console.log(article1.publisher); //static지정을 안했으면 좌측처럼 작성, 지금처럼 static을 선언하면 지금의 출력값은 undefined
    //따라서 class로 연결해야한다
    console.log(Article.publisher);
    Article.printPublisher();

    //들어오는 data에 상관없이 동일한 값을 가질때 사용하며 메모리의 부담을 덜어준다.

5. Inheritance 상속과 다양성
    - a way for one class to extend another class.
    ```javascript
    class Shape {
        constructor(width, height, color) {
            this.width = width;
            this.height = height;
            this.color = color;
        }

    draw() {
        console.log(`drawing ${this.color} color of`);
    }
    
    getArea() {
        return width * this.height;
    }

    class Rectangle extends Shape {} //Rectangle에 Shape있는 모든것이 포함됨
    //따라서 Shape class를 수정하면 나머지 상속받은 class들도 다 수정됨
    class Triangle extends Shape {
        //overriding 필요한 함수만 재정의 가능
        draw() {
            console.log('ㅅ'); 
            //Shape에 정의된 draw함수는 호출되지 않음
            super.draw(); //부모의 draw를 호출함
        }
        getArea() {
            return (this.width * this.height) /2;
        }

        // #6 Object의 toString을 오버라이딩함
        toString() {
            return `Triangle: color: ${this.color}`;
        }
    }

    const rectangle = new Rectangle(20, 20, 'blue');
    rectangle.draw();
    console.log(rectangle.getArea());
    const triangle = new Triangle(20, 20, 'red');
    triangle.draw();
    console.log(triangle.getArea());
    }

6. Class checking: instanceOf
    ```javascript
    console.log(rectangle instanceof Rectangle); //true 
    console.log(triangle instanceof Rectangle); //false
    console.log(triangle instanceof Triangle); //true
    console.log(triangle instanceof Shape); //true
    console.log(triangle instanceof Object); //true
    
    ```
- 참고 : MDN javaScript reference page: Built-ins
