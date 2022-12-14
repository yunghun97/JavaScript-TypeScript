# ๐ซ Call, Apply, Bind

```
ํจ์ ํธ์ถ ๋ฐฉ์๊ณผ ๊ด๊ณ์์ด this๋ฅผ ์ง์ ํ  ์ ์์
```

## ๐ฉ Call

- ๋ชจ๋  ํจ์์์ ์ฌ์ฉํ  ์ ์์ผ๋ฉฐ, this๋ฅผ ํน์ ๊ฐ์ผ๋ก ์ง์ ํ  ์ ์์ต๋๋ค.

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

showThisName(); // ๊ณต๋ฐฑ ์ถ๋ ฅ
// ์์ const ๊ฐ์ฒด์ ๊ฐ์ด ์ ๋ฌ๋๋ค.
showThisName(mike); // mike์ถ๋ ฅ -> this๊ฐ mike๊ฐ ๋จ
showThisName(tom); // tome ์ถ๋ ฅ -> this๊ฐ tom์ด ๋จ

function update(birthYear, occupation) {
  this.birthYear = birthYear;
  this.occupation = occupation;
}

// const mike ๊ฐ์ฒด์ birthYear, occupation ํ๋์ ๊ฐ์ด ์ถ๊ฐ๋ฉ๋๋ค.
update.call(mike, 1999, "singer");

console.log(mike);
/** console.log ๊ฒฐ๊ณผ
 {name: mike, birthYear: 1999, occupation: "singer"} 
 * **/
```

## ๐ฑโโ๏ธ Apply

- ํจ์ ๋งค๊ฐ๋ณ์๋ฅผ ์ฒ๋ฆฌํ๋ ๋ฐฉ๋ฒ์ ์ ์ธํ๋ฉด call๊ณผ ์์ ํ ๊ฐ์ ์ํฉ์๋๋ค.
- call์ ์ผ๋ฐ์ ์ธ ํจ์์ ๊ฐ์ด ๋งค๊ฐ๋ณ์๋ฅผ ์ง์  ๋ฐ์ง๋ง, apply๋ ๋งค๊ฐ๋ณ์๋ฅผ ๋ฐฐ์ด๋ก ๋ฐ์ต๋๋ค.
- ๋ฐฐ์ด์์๋กค ํจ์ ๋งค๊ฐ๋ณ์๋ก ์ฌ์ฉํ  ๋ ์ ๋ฆฌ

```javascript
update.apply(mike, [1999, "Actor"]);

const nums = [1, 2, 3, 4, 5];

// NaN ์ถ๋ ฅ => ๋ถ์ ์ ํ ์ฝ๋
const minNum = Math.min(nums);
console.log(minNums);

// ํด๊ฒฐ๋ฐฉ๋ฒ 1. Rest Parameter(๋๋จธ์ง ๋งค๊ฐ๋ณ์)
const minMun = Math.min(...nums);

// ํด๊ฒฐ๋ฐฉ๋ฒ 2. apply
const minNum = Math.min.apply(null, nums);
// const minNum = Math.min.apply(this๋ก ์ฌ์ฉํ  ํ๋ผ๋ฏธํฐ, [1,2,3,4,5]); => Math.min์ tom, mike ์ฒ๋ผ this๋ก ์ฌ์ฉํ  ๋งค๊ฐ๋ณ์๊ฐ ์์ผ๋ฏ๋ก null ๊ฐ์ ๋ฃ์ด์ค๋ค.

// ํด๊ฒฐ๋ฐฉ๋ฒ 3. call + ๋๋จธ์ง ๋งค๊ฐ๋ณ์
const minNum = Math.min.call(null, ...nums);
```

## ๐ Bind

- ํจ์์ this ๊ฐ์ ์๊ตฌํ ๋ฐ๊ฟ ์ ์์ต๋๋ค.

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

// ์ฌ์ฉ์์ 

const user = {
  name: "Mike",
  showName: function () {
    console.log(`hello, ${this.name}`);
  },
};

user.showName(); //  hello, Mike ์ถ๋ ฅ

let fn = user.showName;

fn(); // hello, ์ถ๋ ฅ => fn์ ํ ๋นํ  ๋ this๋ฅผ ์์ด๋ฒ๋ฆผ

fn.call(user); // hello, Mike
fn.apply(user); // hello, Mike

let boundFn = fn.bind(user);

boundFn(); // hello, Mike ์ถ๋ ฅ => bind๋ก this๋ฅผ ์๊ตฌํ
```

##### ์ฐธ๊ณ ์๋ฃ

##### https://www.youtube.com/watch?v=KfuyXQLFNW4
