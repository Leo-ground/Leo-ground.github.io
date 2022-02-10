---
title: "JS_basic13_(async_await)"
date: 2022-02-09 
categories: JavaScript
---
### 본 내용은 Dream Coding Academy의 강의 내용입니다 [Go to Dream Coding][dreamCodingLink]  

[dreamCodingLink]:  https://academy.dream-coding.com "Go Dream Coding"
- - - 
### 13. 비동기의 꽃 JavaScript async 와 await 그리고 유용한 Promise APIs
- promise를 좀더 간결하고 간편하고 동기적으로 실행되는것 처럼 보이게 만들어주는 것
- .then으로 계속 연결하면 코드가 난잡해진다
- 기존에 제공된 promise 위에 간편한 API를 제공하는 것
    - syntactic sugar: 기존에 존재하는 것을 감싸서 조금더 간편하게 쓸 수 있게 제공하는 것

1. async * await
    ```javascript
        // async & await
        // clear style of using promise :)     
    ```
2. async 써보기
    ```javascript
        // 1. async
        function fetchUser1() {
            // do network request in 10 secs....

            return 'leo';
        }

        const user1 =  fetchUser1();
        console.log(user1);
        // 위처럼 네트워크에서 10초를 대기하는동안 사용자는 아무정보도 받지못한다 따라서 promise를 사용해 문제를 해결

        function fetchUser2() {
            return new Promise((resolve, reject) =>{
                resolve('leo') ;
            })
        }
            // promise안에 resolve 또는 reject를 호출하지 않은경우 계속 pending상태
            // 결과값은 undefined
        const user2 = retchUser2();
        user2.then(console.log);


        // 위의 내용을 async를 사용하면 간단하게 표현가능
        async function fetchUser() {
            //자동으로 함수안의 블록들이 promise로 변환됨
            return 'leo';
            }
        
        const user = retchUser();
        user.then(console.log);

    ```
2. await **
    ```javascript
        function delay(ms) {
            return new Promise(resolve => setTimeout(resolve, ms));
        }
        
        // await를 사용하면 delay가 끝날때 까지 기다림
        // async가 있으므로 apple을 return하는 promise를 생성
        async function getApple() {
            await delay(3000);
            //throw 'error'; 
            return 'apple';
        }

        async function getBanana() {
            await delay(3000);
            return 'banana';
        }

            //참고: 위의 함수를 promise로 변환하면
            function getBanana() {
                return delay(3000)
                .then(() => 'banana');
            }
        
        // async를 사용하지 않으면 아래처럼 callback 지옥이 됨
        function pickFruits1() {
            return getApple()
            .then(apple => {
                return getBanana()
                .then(banana => `${apple} + ${banana}`);
            });
        }
        pickFruits1().then(console.log);

        // async를 사용해 위의 소스를 간단히 수정
        // error발생의 경우 try catch문으로 받는다
        async function pickFruits() {
            try{
                const apple = await getApple(); // 1초소요
                const banana = await getBanana(); // 그다음 1초소요
            } catch() {

            }
            return `${apple} + ${banana}`;
        }

        pickFruits().then(console.log);
    ```
3. await 병렬처리
    ```javascript
        //apple과 banana의 호출순서는 동시에 해도 무관
        async function pickFruits() {
            //promise를 만드는 순간 promise의 코드블록 바로 실행됨
            const applePromise = getApple();
            const bananaPromise = getBanana();
             const apple = await applePromise; 
             const banana = await bananaPromise; 
            
            return `${apple} + ${banana}`;
        }

        pickFruits().then(console.log);
    ```
4. 유용한 Promise
    ```javascript
        // useful Promise APIs
        // .all 이라는 API사용
        // promise배열을 전달하게 되면 모든 promise들이 병렬적으로 다 받을 때까지 모아주는 API

        function pickAllFruits() {
            return Promise.all([getApple(), getBanana()])
            .then(fruits => fruits.join(' + '));
        }

        pickAllFruits().then(console.log);

        // 어떤것이든 상관없이 먼저 얻어지는 것만 가져오고 싶을때
        // .race 사용

        function pickOnlyOne() {
            return Promise.race([getApple(), getBanana()]);
        }

        pickOnlyOne().then(console.log);
    ```
5. HomeWork: 지난 promise에서 callback지옥 수정한것 추가수정!
