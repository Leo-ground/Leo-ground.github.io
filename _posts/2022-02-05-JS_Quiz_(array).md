---
title: "JS_Quiz_(array)"
date: 2022-02-05 
categories: JavaScript
---

```
// Q1. make a string out of an array

  const fruits1 = ['apple', 'banana', 'orange'];

  //my answer
    let fruitsString1 = fruits1.toString();
    console.log(fruitsString1);

// Q2. make an array out of a string

  //my answer
    const fruits2 = '🍎, 🥝, 🍌, 🍒';
    let test = fruits2.split(',');
    console.log(test);
  
 // Q3. make this array look like this: [5, 4, 3, 2, 1]
 
 //my answer
    const array = [1, 2, 3, 4, 5];
    let q3 = array.reverse();
    console.log(q3);
  

 // Q4. make new array without the first two elements
  

 //my anser
    const array4 = [1, 2, 3, 4, 5];
    let array4_2 = array4.splice(2,3);
    console.log(array4_2);
    
 
    
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

  //my answer
    for(let student of students) {
      if(student.score >= 90) {
        console.log(student.name);
      }
    }

    // Q6. make an array of enrolled students
    
    for(let student of students) {
      if(student.enrolled) {
        console.log(student.name);
      }
    }

// Q7. make an array containing only the students' scores
// result should be: [45, 80, 90, 66, 88]

 //my answer 
    let studentsScore = [];
    students.forEach((student) => studentsScore.push(student.score));
    console.log(studentsScore);
    console.log(`studentsScore: ${studentsScore}`);

// Q8. check if there is a student with the score lower than 50

  //my answer
    let checkScore2 = students.forEach((student) => student.score<50 ? console.log(`${student.name} is < 50`) : console.log(`${student.name} is > 50`) );
    console.log(checkScore2);

// Q9. compute students' average score

   let sumScore = 0;

   students.forEach((student) => sumScore += student.score);

   let countStudents = students.length;
   console.log(sumScore/countStudents);

// Q10. make a string containing all the scores
// result should be: '45, 80, 90, 66, 88'
 
  let studentsString10 = studentsScore.toString();
  console.log(studentsString10);


// Bonus! do Q10 sorted in ascending order
// result should be: '45, 66, 80, 88, 90'
  
  let orderScore = studentsScore.sort((a,b) => a-b);
  console.log(orderScore);
```
