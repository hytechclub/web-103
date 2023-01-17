# Code-Along: Personal Quiz
Follow these instructions to customize an interactive quiz about yourself!

## 1. Setup
https://replit.com/@HylandOutreach/PersonalQuizStarter

## 2. Hooking Up the Button
Define the function and make it alert

```js
function startQuiz() {
  alert("Loading...");
}
```

## 3. Adding a Personal Greeting

```js
let nameInput = document.querySelector("#name");
let name = nameInput.value;

alert(`Hello, ${name}! Get ready for some questions...`);
```

## 4. Asking One Question

```js
let score = 0;
let numQuestions = 3.0;

let answer1 = prompt("What is my name?");
if (answer1 === "Ash Ketchum") {
  score = score + 1;
}
```

## 5. Asking Two More Questions

```js
let answer2 = prompt("Where do I live?");
if (answer2 === "Kanto") {
  score = score + 1;
}

let answer3 = prompt("What is my cat's name?");
if (answer3 === "Pikachu") {
  score = score + 1;
}
```

## 6. Calculating and Displaying the Result

```js
alert("Calculating...");
let scorePercent = 100 * (score / numQuestions);

if (scorePercent > 60) {
  alert("You passed 😎");
} else {
  alert("You failed 😭");
}
```

## 7. Revealing the Final Score

```js
let scoreElement = document.querySelector("#score");
scoreElement.textContent = `You got ${score} correct (${scorePercent}%)`;
```

## 8. Presenting the Stars

```js
for (let i = 0; i < score; i++) {
  let starImg = document.createElement("img");
  starImg.src = "star.png";
  document.body.appendChild(starImg);
}
```

## Final Code

```js
function startQuiz() {
  alert("Loading...");

  let nameInput = document.querySelector("#name");
  let name = nameInput.value;

  alert(`Hello, ${name}! Get ready for some questions...`);
  
  let score = 0;
  let numQuestions = 3.0;

  let answer1 = prompt("What is my name?");
  if (answer1 === "Ash Ketchum") {
    score = score + 1;
  }

  let answer2 = prompt("Where do I live?");
  if (answer2 === "Kanto") {
    score = score + 1;
  }

  let answer3 = prompt("What is my cat's name?");
  if (answer3 === "Pikachu") {
    score = score + 1;
  }

  alert("Calculating...");
  let scorePercent = 100 * (score / numQuestions);

  if (scorePercent > 60) {
    alert("You passed 😎");
  } else {
    alert("You failed 😭");
  }

  let scoreElement = document.querySelector("#score");
  scoreElement.textContent = `You got ${score} correct (${scorePercent}%)`;

  for (let i = 0; i < score; i++) {
    let starImg = document.createElement("img");
    starImg.src = "star.png";
    document.body.appendChild(starImg);
  }
}
```
