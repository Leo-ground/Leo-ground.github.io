---
title: "JS_basic11_(Callback)"
date: 2022-02-07 
categories: JavaScript
---

### 11.  비동기 처리의 시작 콜백 이해하기, 콜백 지옥 체험 😱 JavaScript Callback

1. 동기와 비동기
    ```javascript
        // JavaScript is synchronous.
        // Execute the code block by order after hoisting.
        // hoisting: var, function declaration들이 제일 위로 올라가는것
        // 비동기는 언제 코드가 실행될지 예측할 수 없음

        console.log('1');
        //ex setTimeout() 
        // 브라우저에서 제공되는 API로, 설정한 시간이 지나면 설정한 call back fn을 호출
        setTimeout(function(){
            console.log('2')
        },1000);
        
        //arrow fn 활용한 작성
        setTimeout(() => console.log('2'),1000);
    ```
2. 콜백 마지막 정리
    ```javascript
        //여기서 call back함수는 setTimeout()이라는 함수안에 파라미터로 전달한 function은 지금당장 실행하지 않고, 1초가 지난후 내가 요청한 함수를 불러줘, 즉 지금말고 나중에 불러줘서 call back
    
    // Snynchronous callback
        function printImmediately(print) {
            print();
        }

        printImediately(()=> console.log('hello'));
        //출력순서 1,3, hello, 2
        // printImediately 정의는 제일위 , 그다음 순차적으로 실행
        // 단 2의 경우 setTimeout()으로 마지막에 출력(비동기)


    // ASnynchronous callback
        function printWithDelay(print, timeout) {
            setTimeout(print, timeout);
        }

        printWithDely(()=> console.log('async callback'), 2000);
        //출력순서 1,3, hello, 2, async callback
        // 함수정의는 제일위 , 그다음 순차적으로 실행
        // 단 2, aysnc callback 의 경우 비동기
    ```
3. 콜백 지옥 체험
    ```javascript
        //Callback Hell example
        class UserStorage {
            loginUser(id, password, onSuccess, onError){
                setTimeout(()=>{
                    if(
                        (id === 'leo' && password ==== 'dream') ||
                        (id === 'coder' && password === 'academy')
                    ){
                        onSuccess(id);
                    } else {
                        onError(new Error('not found'));
                    }
                }, 2000);
            }

            getRoles(user, onSuccess, onError) {
                setTimeout( () => {
                    if (user === 'leo'){
                        onSuccess({ name: 'leo', role: 'admin'});
                    } else {
                        onError(new Error('no access'));
                    }
                }, 1000);
            }
        }

        const userStorage = new UserStorage();
        const id = prompt('enter your id');
        const password = prompt('enter your password');
        userStorage.loginUser(
            id,
            password,
            user => {
                userStorage.getRoles(
                    user, 
                    userWithRole=>{
                        alert(`Hello ${userWithRole.name}, you have a ${userWithRole.role} role`);
                    },
                    error=>{
                        console.log(error)
                    }    
                );
            },
            error => {
                console.log(error)
            }
        );

        loginUser('leo', 'dream')

        // 가독성이 떨어짐
        // 연결성, 비즈니스로직을 한 눈에 확인하기가 굉장히 힘듦
        // 에러, 디버깅 발생시 분석, 유지, 보수가 굉장히 어렵다.
    ```
