---
title: "JS_Quiz_(array)"
date: 2022-02-05 
categories: JavaScript
---
### 본 내용은 Dream Coding Academy의 강의 내용입니다 [Go to Dream Coding][dreamCodingLink]  

[dreamCodingLink]:  https://academy.dream-coding.com "Go Dream Coding"
- - - 
```

  // Q1. make a string out of an array

    const fruits1 = ['apple', 'banana', 'orange'];

    //my answer
      let fruitsString1 = fruits1.toString();
      console.log(fruitsString1);
  
    //answer
      const result =fruits.join('|'); //구분자를 넣지 않아도 , 가 기본적으로 넣어짐
      console.log(result);


  // Q2. make an array out of a string

    //my answer
      const fruits2 = '🍎, 🥝, 🍌, 🍒';
      let test = fruits2.split(',');
      console.log(test);

    //answer
      const result = fruits.split(',',2); // 구분자를 입력안하면 하나의 인덱스에 들어오게됨
      // 구분자 다음 입력값은 limit으로 2번째 배열값까지만 구분되어서 출력됨(optional)
      console.log(result);
    
  // Q3. make this array look like this: [5, 4, 3, 2, 1]
  
    //my answer
        const array = [1, 2, 3, 4, 5];
        let q3 = array.reverse();
        console.log(q3);
    
    //answer
        const result = array.reverse();
        console.log(result);
        console.log(array); //배열자체도 변환시키고 리턴값도 변환시킨다!



  // Q4. make new array without the first two elements
    
    // my anser
        const array4 = [1, 2, 3, 4, 5];
        let array4_2 = array4.splice(2,3);
        console.log(array4_2);

    // answer
      const result = array.splice(0,2); //배열자체에서 삭제함, return값으로 삭제한 값이 나옴
      console.log(result); // [1, 2]
      console.log(array); // [3, 4, 5]
      // 따라서 새로운 배열을 만드는 것이 아니다! 
      
      // slice를 사용해야한다 (배열해서 원하는 부분만 return해서 받아올때)
      const result = array.slice(2,5); // end의 값은 배제가 된다 
      console.log(result); // [3, 4, 5]
      console.log(array); // [1, 2, 3, 4, 5]
  
      
  // Q5 ~ Q10    
    class Student {
      constructor(name, age, enrolled, score) {
        this.name = name;
        this.age = age;
        this.enrolled = enrolled;
        this.score = score;
      }
    }
    const students = [
      new Student('A', 29, true, 45),
      new Student('B', 28, false, 80),
      new Student('C', 30, true, 90),
      new Student('D', 40, false, 66),
      new Student('E', 18, true, 88),
    ];


  // Q5. find a student with the score 90

    // my answer
      for(let student of students) {
        if(student.score >= 90) {
          console.log(student.name);
        }
      }

    // answer
    // find() 사용: 콜백함수의 조건에 맞으면 true(멈추고),해당 배열의 값을 출력, 없으면 false(다음 값 시도), 계속 없으면 undefind
    // value는  array값을 하나씩 입력해줌
      const result = students.find(function(student){
        // console.log(student, index); 확인해보기 (parameter에 index추가해야함)
        return student.score === 90;
      });

      //arrow function사용
      const result = students.find((student) => student.score ===90);
      console.log(result)

  // Q6. make an array of enrolled students
    
    // my answer
      for(let student of students) {
        if(student.enrolled) {
          console.log(student.name);
        }
      }
    
    // answer
    // filter() 사용 : 콜백함수가 true인 값만 전달
      const result = students.filter((student) => student.enrolled)
      console.log(result)

  // Q7. make an array containing only the students' scores
  // result should be: [45, 80, 90, 66, 88]

  // my answer 
      let studentsScore = [];
      students.forEach((student) => studentsScore.push(student.score));
      console.log(studentsScore);
      console.log(`studentsScore: ${studentsScore}`);

  // ansswer
  // map() 을 사용: 기존의 배열을 call back fn을 통해서 새로운 값을 도출해 해당 배열에 다시 맵핑시키는 것(retrun값으로 대체)
      const result = students.map((student) => student.score);
      console.log(result); 

  // Q8. check if there is a student with the score lower than 50

    // my answer
      let checkScore2 = students.forEach((student) => student.score<50 ? console.log(`${student.name} is < 50`) : console.log(`${student.name} is > 50`) );
      console.log(checkScore2);

      // answer
      // some()사용: 배열의 요소중 callback함수가 return이 true가 되는 요소가 있는지 없는지 boolean return
      const result = students.some((student) => student.score < 50);
      console.log(result); //true

      // every()사용: 배열의 모든 요소들이 callback함수 결과 모두 true가 되어야 true로 return
      const result2 = students.some((student) => student.score < 50);
      console.log(result2); //false

      const result3 = !students.some((student) => student.score >= 50);
      console.log(result3); //true

  // Q9. compute students' average score

    // my answer 
    let sumScore = 0;

    students.forEach((student) => sumScore += student.score);

    let countStudents = students.length;
    console.log(sumScore/countStudents);

    // answer
    // reduce() 사용: (callback 함수를 전달 or initial value를 전달)
    // callback함수에서 return 할때 누적된 값을 전달
    // 배열의 모든 값을 누적하거나 모을때 사용하는 API
    // 배열의 값 하나하나는 curr에 전달
    // prev return값이 다음에 호출될때 prev로 연결된다
    const result = students.reduce((prev, curr) => {
      console.log('----------');
      console.log(prev);
      console.log(curr);

      return curr.score;
    }, 0) //initial value 설정시 해당 값부터 시작됨(처음 prev값으로 설정됨)
    console.log(result);

    // arrowFunction으로 줄이면
    const result = students.reduce((prev, curr) => prev +curr.score, 0);
    console.log(result / students.length);

    //reduceRight은 배열의 뒤쪽부터 시작


  // Q10. make a string containing all the scores
  // result should be: '45, 80, 90, 66, 88'
  
    // my answer
    // API 섞어서 출력가능
      let studentsString10 = studentsScore.toString();
      console.log(studentsString10);

    // answer
      const result = students.map((student) => student.score).join();

    //50점 이상
    const result = students.map((student) => student.score)//[45, 80,90, 66, 88]값만 다음 filter로 넘김
    .filter(score => score >= 50)  //[45, 80,90, 66, 88] 중에서 50 이상인 값만 다음 조인으로 넘김
    .join();

  // Bonus! do Q10 sorted in ascending order
  // result should be: '45, 66, 80, 88, 90'
    
    // my answer
      let orderScore = studentsScore.sort((a,b) => a-b);
      console.log(orderScore);

    //answer
    // a: 이전값, b:현재값 이 전달되는데 -값이 전달되면 a 값이 b보다 작다고 판단됨
    const result = students.map(student => student.score)
    .sort((a,b)=> a - b)
    .join();

    console.log(result);
```
