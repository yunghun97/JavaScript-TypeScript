# 🎫 Call, Apply, Bind

```
함수 호출 방식과 관계없이 this를 지정할 수 있음
```

## 👩 Call

- 모든 함수에서 사용할 수 있으며, this를 특정값으로 지정할 수 있습니다.

```javascript
const mike = {
  name: "Mike",
};

const tom = {
  name: "Tom",
};

function showThisName() {
  console.log(this.name);
}

showThisName(); // 공백 출력
// 위에 const 객체의 값이 전달된다.
showThisName(mike); // mike출력 -> this가 mike가 됨
showThisName(tom); // tome 출력 -> this가 tom이 됨

function update(birthYear, occupation) {
  this.birthYear = birthYear;
  this.occupation = occupation;
}

// const mike 객체에 birthYear, occupation 필드와 값이 추가됩니다.
update.call(mike, 1999, "singer");

console.log(mike);
/** console.log 결과
 {name: mike, birthYear: 1999, occupation: "singer"} 
 * **/
```

## 👱‍♀️ Apply

- 함수 매개변수를 처리하는 방법을 제외하면 call과 완전히 같은 상황입니다.
- call은 일반적인 함수와 같이 매개변수를 직접 받지만, apply는 매개변수를 배열로 받습니다.
- 배열요소롤 함수 매개변수로 사용할 때 유리

```javascript
update.apply(mike, [1999, "Actor"]);

const nums = [1, 2, 3, 4, 5];

// NaN 출력 => 부적절한 코드
const minNum = Math.min(nums);
console.log(minNums);

// 해결방법 1. Rest Parameter(나머지 매개변수)
const minMun = Math.min(...nums);

// 해결방법 2. apply
const minNum = Math.min.apply(null, nums);
// const minNum = Math.min.apply(this로 사용할 파라미터, [1,2,3,4,5]); => Math.min은 tom, mike 처럼 this로 사용할 매개변수가 없으므로 null 값을 넣어준다.

// 해결방법 3. call + 나머지 매개변수
const minNum = Math.min.call(null, ...nums);
```

## 💂 Bind

- 함수의 this 값을 영구히 바꿀 수 있습니다.

```javascript
const mike = {
  name: "Mike",
};

function update(birthYear, occupation) {
  this.birthYear = birthYear;
  this.occupation = occupation;
}

const updateMike = update.bind(mike);

updateMike(1980, "pollice");
console.log(mike);

// 사용예제

const user = {
  name: "Mike",
  showName: function () {
    console.log(`hello, ${this.name}`);
  },
};

user.showName(); //  hello, Mike 출력

let fn = user.showName;

fn(); // hello, 출력 => fn에 할당할 때 this를 잃어버림

fn.call(user); // hello, Mike
fn.apply(user); // hello, Mike

let boundFn = fn.bind(user);

boundFn(); // hello, Mike 출력 => bind로 this를 영구히
```

##### 참고자료

##### https://www.youtube.com/watch?v=KfuyXQLFNW4
