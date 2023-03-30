# API Example: Trivia App
This site uses a Trivia API to grab some multiple choice questions and use them to quiz the user.

- [Preview: https://trivia.hylandoutreach.repl.co](https://trivia.hylandoutreach.repl.co)
- [Project: https://replit.com/@HylandOutreach/Trivia](https://replit.com/@HylandOutreach/Trivia)
- [APIs: Open Trivia Database](https://opentdb.com/api_config.php)

## Improvement Ideas
As it stands, this website is fairly basic. Here are some things that could make it better.

### Option Choices
Currently, the quiz will always be `5` questions, and they will always be `"easy"` questions. Add a way for the user to decide how many questions, and what difficulty to use! These are set as the `numQuestions` and `difficulty` variables in the `startQuiz` function.

The simple way to do this would be to use more `prompt` statements to ask the user to enter the information. The more powerful way would be to create a number text box and a difficulty dropdown on the HTML page, and then grab those values before making the request!

### Categories
The API also allows for specific categories of questions. These are listed on the [API site](https://opentdb.com/api_config.php); but it is also possible to [get these categories from the API itself](https://opentdb.com/api_category.php)!

Create a way for the user to decide which category they would like. This could be a dropdown in the HTML, populated by an API request... or it could be another simple `prompt`. Note that the category passed in the URL is numeric.

### Interactive DOM
Currently, the site uses `prompt`s to ask all the questions to the user. This is functional, but it is not a modern, user-friendly experience. Update the code so that the questions are added _directly to the HTML_, and the user is able to select their answer by clicking it. This may be a significant challenge, but the data should all be the same - it will not be necessary to update the API calls at all!

### Quiz Feedback
Currently, when the quiz completes, there is simply a raw score that appears. There is no way for the user to know which questions they answered correctly or incorrectly. Update the code so that it keeps track of which questions were correct and incorrect, and displays that information after the quiz completes! 

## API Information
The [Open Trivia Database API](https://opentdb.com/api_config.php) is one of the simpler ones. There are a few options available via query parameters, such as:

- `amount` (number of questions)
- `category` (numeric value representing a variety of categories)
- `difficulty` ("easy", "medium", or "hard")
- `type` ("multiple" for multiple choice, "boolean" for true/false)

The URL could end up looking something like this: [https://opentdb.com/api.php?amount=2&category=25&difficulty=medium&type=multiple](https://opentdb.com/api.php?amount=2&category=25&difficulty=medium&type=multiple)

The response will be something like this:

```json
{
  "response_code": 0,
  "results": [
    {
      "category": "Entertainment: Music",
      "type": "multiple",
      "difficulty": "hard",
      "question": "This album, now considered to be one of the greatest of all time, was a commercial failure when it was released.",
      "correct_answer": "The Velvet Underground and Nico",
      "incorrect_answers": [
        "Abbey Road",
        "Led Zeppelin IV",
        "Pet Sounds"
      ]
    }
  ]
}
```

The questions are within the `results` property, which contains an array of question objects. Each question object has a `question` property with the question text, a `correct_answer` property with the correct answer, and an `incorrect_answers` property which is an array of strings, each one a different incorrect answer to the question.

## Code Information
The code is organized into a few different functions and variables in the **script.js** file.

- `ANSWER_LETTERS`: just the letters used to mark possible question answers - it's a string, and also an array
- `decodeHtml`: a function that converts the encoded text from the API into normal text
- `getAnswerstext`: a function that takes an array of answer strings, and displays them with letters
    - Each one looks like `A) This is an answer`
    - They are `join`ed together by a newline character (`"\n"`)
- `generateQuestionTextAndAnswer`: a function that takes a question object, and returns the question text, along with the correct letter answer
- `startQuiz`: the function that runs when the "Start Quiz" button is clicked - it makes the request to the API, converts the results into proper questions, and runs the quiz through `prompt` statements
