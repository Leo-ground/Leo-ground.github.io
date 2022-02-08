---
title: "JS_basic12_(Promise)"
date: 2022-02-08 
categories: JavaScript
---

### 11.  프로미스 개념부터 활용까지 JavaScript Promise
- JavaScript에서 제공하는 비동기를 간편하게 처리할 수 있게 도와주는 Object
- 정해진 장시간의 기능을 수행하고나서 정상적으로 기능이 수행되어졌다면 성공의 메세지와 함께 처리된 결과값을 전달
- 만약 기능을 수행하다가 예상치 못한 문제가 발생했다면 에러를 전달해줌

0. 중점사항
    ```javascript
        // Promise is a JavaScript object for asynchronous operation.
        // 2가지 포인트 
        //  1. State: 프로세스가 헤비한 오퍼레이션 수행중인지
        //              성공했는지, 실패했는지 이해
        //      pending -> fulfilled or rejected
        //      
        //  2. Producer와 Consumer의 차이점 알기: 서로다른 견해 이해
        //      Producer: 우리가 원하는 데이터를 제공하는사람
        //      Consumer: 제공된 데이터를 사용하는 사람

    ```
1. Promise만들기
    ```javascript
        // 1. Producer
        // when new Promise is created, the excutor runs automatically.
        const promise = new Promise((resolve, reject) => {
            // doing some heavy work (network, read files)
            console.log('doing something....');
            setTimeout(()=>{
                //resolve('leo'); 
                reject(new Error('no network'));
                //Error: JavaScript에서 제공하는 Object
            }, 2000);
        })
        // Promise를 만드는 순간 바로 excuter함수가 실행됨
        // 만약 네트워크 요청을 사용자가 요구했을때만 해야하는 경우라면
        // 이런식으로 작성하면 요구하지 않아도 불필요한 요청이 발생
        
    ```
2. Promise 사용하기
    ```javascript
        // 2. Consumers: then, catch, finally
        // then: promise가 정상적으로 실행되어서 resolve라는 콜백 함수를 통해 전달한 값이 value의 parameter로 전달되어 들어옴
        // Error를 catch로 핸들링 하지 않으면 uncaught error가 발생
        promise 
            .then((value) => {
                console.log(value);
            })
            .catch(error=>{ //reject의 값을 가져옴
                console.log(error);
            })
            .finally(()=> {
                console.log('finally');
            })
        //chaining으로 then을 호출하면 다시promise리턴 되고 다시 catch를 수행
        // finally: 성공,실패 관계없이 마지막에 무조건 호출
    ```
3. Promise 연결하기
    ```javascript
        // 3. Promise chaining
        const fetchNumber = new Promise((resolve, reject) =>{
            setTimeout(()=> resolve(1), 1000);
        });
        //then은 값을 전달해도되고 다른 promise를 전달해도 됨
        fetchNumber
        .then(num => num*2)
        .then(num => num*3)
        .then(num => {
            return new Promise((resolve,reject)=>{
                setTimeout(()=> resolve(num-1, 1000));
            });
        })
        .then(num => console.log(num));
    ```
4. 오류를 잘 처리 하자
    ```javascript
        // 4. Error Handling
        const getHen = () =>
            new Promise((resolve, reject) => {
                setTimeout(() => resolve('chicken'), 1000);
            });
        const getEgg = hen =>
            new Promise((resolve, reject) => {
                setTimeout(() => resolve(`${hen} => Egg`), 1000);
                setTimeout(() => reject(new Error(`error! ${hen} => Egg`)), 1000);
            });
        const cook = egg =>
            new Promise((resolve, reject) => {
                setTimeout(() => resolve(`${egg} => SunnySide`), 1000);
            });
        
        getHen()
        .then(hen => getEgg(hen))
        .catch(error => { //핸들하고 싶은 promise다음에 바로 catch작성
            return 'bread';
        }) 
        .then(egg => cook(egg))  //egg오류시 bread가 넘어온다
        .then(meal => console.log(meal))
        .catch(console.log); //마지막에만 작성한 경우egg를 받아올때 바로 넘어옴
        //전달받은 값을 바로 전달하게 되면 .then(getEgg)로 작성가능
        // getHen()
        //    .then(getEgg)
        //    .then(cook)
        //    .then(console.log)
        //    .catch(console.log);
    ```
5. Callback hell => Promise
    ```javascript
        //Callback Hell example
            class UserStorage {
                loginUser(id, password){
                    return new Promise((resolve, reject) => {
                        setTimeout(()=>{
                        if(
                            (id === 'leo' && password ==== 'dream') ||
                            (id === 'coder' && password === 'academy')
                        ){
                            resolve(id);
                        } else {
                            reject(new Error('not found'));
                        }
                    }, 2000);
                    });
                    
                }

                getRoles(user) {
                    return new Promise((resolve, reject) => {
                        setTimeout( () => {
                            if (user === 'leo'){
                                resolve({ name: 'leo', role: 'admin'});
                            } else {
                                reject(new Error('no access'));
                            }
                        }, 1000);
                    });                    
                }
            }

            const userStorage = new UserStorage();
            const id = prompt('enter your id');
            const password = prompt('enter your password');
            userStorage.loginUser(id, password)
            .then(userStorage.getRoles)
            .then(user => alert(
                `Hello ${userWithRole.name}, you have a ${userWithRole.role} role`
            ))
            .catch(console.log)



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
    ```
