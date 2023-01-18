# Self-Paced Work: Quiz Updates
Make some updates to your personal quiz website!

## 1. More Custom Questions
Fill out your quiz with more questions about yourself! Add as many as you can, and make sure to update the `numQuestions` variable so the final score calculation is accurate.

## 2. HTML & CSS Updates
Currently, the webpage really only serves as a way to start the quiz. Make it your own by adding information, updating the color scheme, and anything else you'd like to do!

## 3. Multiple Choice Questions
The fill-in-the-blank style of the questions is a little easier to program, but it makes the questions much harder. Update the questions so that they show a list of possible answers! A question could look something like this:

```
Where do I live?

A) Kanto
B) Banto
C) Ranto
D) Flanto
```

The user could then enter `A` or `a`, so the answer variable could be checked against that.

## 4. Different Images
Stars are cool, but you might be able to find something better. Search the internet for an appropriate victory icon, and replace the `star.png` url in the JavaScript with the new URL!

## 5. (BUG) Extra Stars
Currently, if a player completes the quiz more than once, all the additional stars are appended to the page - they are never removed! Figure out how to remove the star `<img>` elements whenever the quiz starts, so that the number of stars will always match the number of correct answers.

## 6. (CHALLENGE) Fully DOM Quiz
The `alert` and `prompt` statements are functional, but they might not be the optimal user experience. Get rid of _all_ `alert` and `prompt` statements in the `startQuiz` function, and replace them with HTML elements!

For example, for the first question, you could add HTML like this:

```html
<p>What is my name?</p>
<p><input id="answer1"></p>
```

Then, instead of setting the `answer1` variable based on a `prompt`, you could grab the value from the `<input id="answer1">` like this:

```js
let answer1Input = document.querySelector("#answer1");
let answer1 = answer1Input.value;
```

From there, the `answer1` variable could be used in the same way.

### DOM Dropdowns or Radio Buttons
Another option would be to use `<select>` dropdowns or `<input type="radio">` buttons for a multiple choice quiz.

- [Dropdowns](https://www.w3schools.com/tags/tag_select.asp)
- [Radio Buttons](https://www.geeksforgeeks.org/how-to-get-value-of-selected-radio-button-using-javascript/)

The code may need a little more updating, but the user experience will be excellent!
