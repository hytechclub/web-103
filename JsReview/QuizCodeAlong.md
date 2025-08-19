# Code-Along: Personal Quiz
Follow this guide to create and customize an interactive quiz. These instructions use Ash Ketchum as an example subject, but make sure to change the questions and answers to be about you!

## Part 1 - Setup
Start by copying the existing project. It contains all of the HTML and CSS, but none of the JavaScript.

[Click here to copy the project!](https://hytop.onrender.com/e/personal-quiz-starter)

Open the preview to see how it looks. Everything should show up on the page, but the button will not be functional yet...

## Part 2 - Hooking Up the Button
There is currently no JavaScript code, so nothing happens when the button is clicked! Take a look at the `<button>` element in the HTML:

```html
<button onclick="startQuiz()">Start the Quiz</button>
```

The `onclick` attribute is trying to call a function named `startQuiz` - you have to define it!

1. Open the **script.js** file for editing
1. At the top, define a function named `startQuiz`
    - `function` keyword
    - Function name (`startQuiz`)
    - Parentheses (`()`)
    - Curly brackets (`{}`)
1. Make a new line in the _body_ of the function
    - Between the curly brackets
1. There, add an `alert` statement that says "Loading..."
1. Run the project again, click the button, and verify that a pop-up appears!

The code in the **script.js** file should look something like this:

```js
function startQuiz() {
  alert("Loading...");
}
```

## Part 3 - Adding a Personal Greeting
The button is working, but it's not doing anything too exciting yet. Welcome the user to the quiz with a personalized message using the name they entered in the text input!

1. Make a new line in the body of the `startQuiz` function
1. There, create a new variable named `nameInput`
1. Set the `nameInput` value to get the `<input id="name">` element from the HTML
    - Use `document.querySelector` to accomplish this
1. Under that, create a new variable named `name`
1. Set the `name` value to get the actual text from the `nameInput` element
    - Use `.value` to accomplish this
1. Under that, add an `alert` that says "Hello, NAME! Get ready for some questions..."
1. Make the message into a template string, and replace "NAME" with `${name}` to use the text from the box
1. Run the project again, enter a name in the text box, click the button, and verify that the greeting is personalized!

The additional code within the body of the `startQuiz` function should look something like this:

```js
let nameInput = document.querySelector("#name");
let name = nameInput.value;

alert(`Hello, ${name}! Get ready for some questions...`);
```

## Part 4 - Preparing the Score
Now it's time to get into the quiz! Start by setting up some storage variables to keep track of the player's score.

1. Make a new line in the body of the `startQuiz` function
1. There, create a new variable named `score`
1. Set the `score` value to `0` to start
1. Under that, create a new variable named `numQuestions`
1. Set the `numQuestions` value to `3.0` for now
    - The `.0` is for calculation purposes

Note that nothing will actually change when clicking the button again - these variables will be used a bit later. The additional code within the body of the `startQuiz` function should look something like this:

```js
let score = 0;
let numQuestions = 3.0;
```

## Part 5 - Asking One Question
Now that the variables are initialized, this quiz needs some questions! Start with this one:

| Question | Answer |
|-|-|
| What is my name? | Ash Ketchum |

1. Make a new line at the bottom of the `startQuiz` function
1. There, create a variable named `answer1`
1. Set `answer1` to the result of a `prompt` asking "What is my name?"
1. Under that, create an `if` statement
    - `if` keyword
    - Parentheses (`()`)
    - Curly brackets (`{}`)
1. For the condition (between parentheses), check if `answer1` is equal to `"Ash Ketchum"`
    - Use `===` to compare the two
1. In the body of the `if` (between curly brackets), make a new line
1. There, set `score` to be `score + 1`
    - This increases the score by 1!
1. Click the button, and verify that the new prompt appears!

The additional code within the body of the `startQuiz` function should look something like this:

```js
let answer1 = prompt("What is my name?");
if (answer1 === "Ash Ketchum") {
  score = score + 1;
}
```

## Part 6 - Asking More Questions
Additional questions will use _almost exactly_ the same code as the first question. The only things that will change are:

- The answer variable name (e.g., `answer2` instead of `answer1`)
- The question text (e.g., `"Where do I live?"` instead of `"What is my name?"`)

Other than that, you can follow the steps from **Part 5** to add each additional question! Add at least two more:

| Question | Answer |
|-|-|
| Where do I live? | Kanto |
| What is my cat's name? | Pikachu |

>Note: If there are more or less than three questions, the value of the `numQuestions` variable will need to change

The code for the additional questions should look something like this:

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

Now the quiz is complete, but the player has no idea if they got the questions right or wrong!

## Part 7 - Calculating and Displaying the Result
At this point, the `startQuiz` function knows the number of correct answers (stored in the `score` variable), so the final result can be calculated. There will be a little math involved, and then the player will get a nice message saying whether they passed or failed.

1. Make a new line at the bottom of the `startQuiz` function
1. There, add an `alert` that says "Calculating..."
1. Under that, create a variable named `scorePercent`
1. Set the `scorePercent` variable to be `100` times `score` divided by `numQuestions`
    - This is their final percentage based on how many they got right
1. Under that, create an `if`/`else` structure
    - `if` keyword
    - Parentheses
    - Curly brackets
    - `else` keyword
    - More curly brackets
1. For the condition (between parentheses), check if `scorePercent` is greater than `60`
1. In the body of the `if`, use an `alert` to say "You passed 😎"
1. In the body of the `else`, use an `alert` to say "You failed 😭"
1. Run the project, take the quiz, and make sure the calculation is correct!

The additional code within the body of the `startQuiz` function should look something like this:

```js
alert("Calculating...");
let scorePercent = 100 * (score / numQuestions);

if (scorePercent > 60) {
  alert("You passed 😎");
} else {
  alert("You failed 😭");
}
```

## Part 8 - Revealing the Final Score
A simple "pass" or "fail" is nice, but the player might want to know their exact score. There is actually already a `<p>` element in the HTML just for this purpose! Its text can update dynamically based on the quiz result.

1. Make a new line at the bottom of the `startQuiz` function
1. There, create a new variable named `scoreElement`
1. Set the `scoreElement` value to get the `<p id="score">` element from the HTML
    - Use `document.querySelector` to accomplish this
1. Set the text of the `<p>` to a message saying "You got SCORE correct (PERCENT%)"
    - Use `.textContent` to accomplish this
1. Make the message into a template string, and replace "SCORE" and "PERCENT" with `${score}` and `${scorePercent}`
    - This will use the actual score and percentage values
1. Run the project, take the quiz again, and verify that the correct score appears on the page after it!

The added code should look something like this:

```js
let scoreElement = document.querySelector("#score");
scoreElement.textContent = `You got ${score} correct (${scorePercent}%)`;
```

## Part 9 - Presenting the Stars
The quiz is functionally complete now, but the player might want a bit more of a prize for their efforts. Add some star images to the page based on how many questions the player got right!

1. Make a new line at the bottom of the `startQuiz` function
1. There, create a `for` loop structure
    - `for` keyword
    - Parentheses (`()`)
    - Curly brackets (`{}`)
1. Add statements within the parentheses to repeat a number of times
    - `let i = 0;`
    - `i < NUMBER;`
    - `i++`
1. Make the loop repeat `score` times instead of `NUMBER` times
    - This way, the code in the loop will run once for every correct answer
1. Make a new line in the body of the loop (between curly brackets)
1. There, create a new variable named `starImg`
1. Set `starImg` to be a newly created `<img>` element
    - Use `document.createElement` to accomplish this
1. Under that, set the `src` of `starImg` to be `"https://github.com/hytechclub/web-103/blob/main/Assets/star.png?raw=true"`
    - The **star.png** file should be accessible through the URL
1. Under that, append the `starImg` element to the `body` of the page
    - Use `document.body.appendChild` to accomplish this
1. Run the project, take the quiz again, and see how many stars you see!

The added code should look something like this:

```js
for (let i = 0; i < score; i++) {
  let starImg = document.createElement("img");
  starImg.src = "https://github.com/hytechclub/web-103/blob/main/Assets/star.png?raw=true";
  document.body.appendChild(starImg);
}
```

## Conclusion
And that's it! The quiz should be fully functional and fully fun. The code in the **script.js** file should look something like this at the end:

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
    starImg.src = "https://github.com/hytechclub/web-103/blob/main/Assets/star.png?raw=true";
    document.body.appendChild(starImg);
  }
}
```

## Next Steps: Self-Paced Work
[Click here for self-paced work instructions!](SelfPacedWork.md)
