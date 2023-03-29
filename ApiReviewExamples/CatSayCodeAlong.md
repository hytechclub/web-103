# Code-Along: What Does the Cat Say?
Follow these instructions to build a website that will provide the user with some pictures of cats saying messages. _Not to be confused with [The Fox](https://www.youtube.com/watch?v=jofNR_WkoCE)._

[Click here to view the Cat Says Starter Repl project.](https://replit.com/@HylandOutreach/CatSays) Fork the project to begin the activity.

## Part One: Background
Before diving into the activity, take some time for research and planning.

### The Starter Code
The starter project has quite a bit of code, but it's all HTML and CSS! In the **index.html** file, there are a few elements of note:

- An `<input>` with an `id` of `"cat-message"`
- A `<button>` with an `onclick` of `"run()"`
- An `<img>` with an `id` of `"cat-pic"`

All of these elements will be necessary to make the website functional.

### The [Cat as a Service](https://cataas.com/) API
The **cataas API** has a _ton_ of different ways to access random cat pictures. One of its most powerful features is to embed messages right onto images. This is possible with the `/cat/says/` endpoint.

For example, the URL to get a random cat saying "hi" would look like this: [https://cataas.com/cat/says/hi](https://cataas.com/cat/says/hi)

Notice that the message `hi` is actually not a query parameter - it is simply part of the URL path! There is one query parameter to add, though: `json=true`. This will send along more information in JSON form that could end up being useful.

For example, the URL to get a random cat saying "hi" in JSON would look like this: [https://cataas.com/cat/says/hi?json=true](https://cataas.com/cat/says/hi?json=true)

_Note: Changing "hi" to any other message would make the new message appear on the image!_

The response should look something like this:

```json
{
  "tags": [
    "closed eyes",
    "sleepy",
    "bed"
  ],
  "createdAt": "2022-09-11T00:27:05.317Z",
  "updatedAt": "2022-10-11T07:52:32.756Z",
  "validated": true,
  "owner": "LeBonk",
  "file": "631d2b59444de200102f10c9.jpeg",
  "mimetype": "image/jpeg",
  "size": 384097,
  "_id": "2bPYDRuvU70sbgja",
  "url": "/cat/2bPYDRuvU70sbgja/says/hi"
}
```

For the purposes of this activity, the important property will be the `url` - that can be appended to the base URL to retrieve the image!

It ends up looking something like this: [https://cataas.com/cat/2bPYDRuvU70sbgja/says/hi](https://cataas.com/cat/2bPYDRuvU70sbgja/says/hi)

![](Assets/CatSaysHi.jpg)

### The Plan
To utilize this API, the code should:

- Grab the message from the text box `<input>` on the page
- Use `fetch` to request a random cat saying the message
    - Use the base URL of `https://cataas.com/cat/says/`
    - Pass the message after the slash
    - Use the `json=true` query parameter to get JSON data
- Grab the `url` property from the response
- Set the `src` of the `<img id="cat-pic">` to be the returned URL

## Part Two: Hooking Up the Button
First, define an asynchronous function to run when the button on the page is clicked.

1. Open the **script.js** file for editing
1. There, define a new function named `run` to match the `onclick` of the `<button>`
1. Add the `async` keyword in front of `function` to make it asynchronous
1. In the body of the function, create a new variable named `catPic`
1. Use `document.querySelector` to store the `<img id="cat-pic">` in the `catPic` variable
1. Under that, set the `src` of `catPic` to be a loading indicator image
    - Use ["https://media.tenor.com/o8m3bKTsifUAAAAM/hold-on.gif"](https://media.tenor.com/o8m3bKTsifUAAAAM/hold-on.gif)

Run the project, click the button, and verify that the loading indicator shows up! The code in the **script.js** file should look something like this:

```js
async function run() {
  let catPic = document.querySelector("#cat-pic");
  catPic.src = "https://media.tenor.com/o8m3bKTsifUAAAAM/hold-on.gif";
}
```

## Part Three: Getting the Message
The next step is to grab the text from the text box, aka the `<input>` from the HTML.

1. Make a new line in the body of the `run` function
1. There, create a new variable named `messageInput`
1. Use `document.querySelector` to store the `<input id="cat-message">` in the `messageInput` from the HTMl
1. Under that, create a new variable named `message`
1. Store the `value` of the `messageInput` element in the `message` variable

For testing purposes, throw an `alert` in the code to display the `message` result. Then, run the project, enter a message in the box, click the button, and verify that the message appears! Remove the `alert` after testing. The added code should end up looking something like this:

```js
let messageInput = document.querySelector("#cat-message");
let message = messageInput.value;
```

## Part Four: Catching Errors
In order to properly make an HTTP request in JavaScript, it is generally a good idea to wrap any call to `fetch` in a `try`/`catch` structure. Create this structure.

1. Make a new line in the body of the `run` function
1. There, _declare_ two variables without values: `response` and `responseJson`
    - These will be set in the `try` block
1. Under that, create a `try`/`catch` structure
    - `try`
    - curly brackets `{` and `}`
    - `catch`
    - parentheses `()`
    - `e` within the parentheses for the error value
    - curly brackets `{` and `}`
1. Within the `catch` block, make a new line
1. There, set the `src` of `catPic` to be `""`
    - This will remove the loading indicator
1. Under that, `alert` the error received
1. Under that, `return` from the function

Nothing will change, but now the code is ready for a `fetch`! The added lines should look something like this:

```js
let response, responseJson;

try {
} catch (e) {
  catPic.src = "";
  alert(e);
  return;
}
```

## Part Five: Making the Request
Now it's time to actually involve the API with `fetch`! Make the request, and grab the JSON data.

1. Make a new line in the `try` block within the `run` function
1. There, make a new variable named `url`
1. Set `url` to be the a new template literal
1. Between the backticks, add the URL with the query parameter for the cat to say "hi"
    - `https://cataas.com/cat/says/hi?json=true`
1. Replace `hi` with the interpolated value of `message` using `${}`
    - `https://cataas.com/cat/says/${message}?json=true`
1. Under that, call `fetch` on the `url` variable value
    - Add an `await` in front of the `fetch` call to yield the response
    - Store the result in the `response` variable
1. Under that, call `response.json()` to grab the JSON data in a promise
    - Add the `await` keyword in front of the `.json()` call to yield the JSON object
    - Store the result in the `responseJson` variable

For testing purposes, throw an `alert` in the code to display the `responseJson` result. Then, run the project, enter a message in the box, click the button, and verify that the response JSON data appears! It should simply say `[object Object]`, but that means it is in fact an object! Remove the `alert` after testing. The added code should end up looking something like this:

```js
let url = `https://cataas.com/cat/says/${message}?json=true`;
response = await fetch(url);
responseJson = await response.json();
```

## Part Six: Displaying the Image
Now for the fun part. The response has come back, and the data is there - all that's left is to extract the image URL, append it to the base URL, and set it as the image source!

1. Make a new line at the _bottom_ of the `run` function
1. There, create a new variable named `imageUrl`
1. Set `imageUrl` to be the a new template literal
1. Between the backticks, add the base URL, without the slash at the end
    - `https://cataas.com`
1. At the end of the literal, add the interpolated value of the response `url` property using `${}`
1. Under that, set the `src` of the `catPic` element to be the `imageUrl` value

Run the project, enter a message, click the button, and verify that a random cat appears with the message! The added code should look something like this:

```js
let imageUrl = `https://cataas.com${responseJson.url}`;
catPic.src = imageUrl;
```

## Conclusion
By the end of the code-along, the **script.js** file should look something like this:

```js
async function run() {
  let catPic = document.querySelector("#cat-pic");
  catPic.src = "https://media.tenor.com/o8m3bKTsifUAAAAM/hold-on.gif";

  let messageInput = document.querySelector("#cat-message");
  let message = messageInput.value;

  let response, responseJson;
  
  try {
    let url = `https://cataas.com/cat/says/${message}?json=true`;
    response = await fetch(url);
    responseJson = await response.json();
  } catch (e) {
    catPic.src = "";
    alert(e);
    return;
  }

  let imageUrl = `https://cataas.com${responseJson.url}`;
  catPic.src = imageUrl;
}
```

## Next Steps
[Click here to see how you can make more updates to the Cat Says site!](CatSaySelfPacedWork.md)
