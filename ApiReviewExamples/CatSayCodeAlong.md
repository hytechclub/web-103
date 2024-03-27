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

There is also some code in the **script.js** file already - specifically, the definition for a function named `speak`. This function uses the [TikTok Text-to-Speech API](https://weilbyte.github.io/tiktok-tts/) to speak whatever message is passed to it.

### The [Cat as a Service](https://cataas.com/) API
The **cataas API** has a _ton_ of different ways to access random cat pictures. One of its most powerful features is to embed messages right onto images. This is possible with the `/cat/says/` endpoint.

For example, the URL to get a random cat saying "hi" would look like this: [https://cataas.com/cat/says/hi](https://cataas.com/cat/says/hi)

Notice that the message `hi` is actually not a query parameter - it is simply part of the URL path!

It ends up looking something like this:

![](Assets/CatSaysHi.jpg)

### The Plan
To utilize this API, the code should:

- Grab the message from the text box `<input>` on the page
- Create a new image url by appending the message appropriately
- Set the `src` of the `<img id="cat-pic">` to be the URL
- Speak the response using the TikTok Text-to-Speech API

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

## Part Four: Setting the Image Source
Next, set the image URL based on the message.

1. Make a new line in the body of the `run` function
1. There, set the `src` property of `catPic`
1. Set it to a new template literal
1. Start the template literal with the base URL: `https://cataas.com/cat/says/`
1. Add the message at the end of the URL with `${message}`

That's it! The line of code added should look something like this:

```js
catPic.src = `https://cataas.com/cat/says/${message}`;
```

## Part Five: Speaking the Part
Luckily, there is already a function defined to make the HTTP request. Here's what the `speak` function does:

1. Creates `ttsUrl` and `body` variables to setup the request with the necessary data
1. In a `try` block, performs a `fetch`
1. In the `fetch`, passes the appropriate data, including `method`, `headers`, and `body` to the `ttsUrl`
1. Converts the `response` to JSON
1. Creates a new `Audio` object given the response data
1. Plays the audio after one second

It basically does all the work! The only thing needed within the `run` function is to _call_ the `speak` function, `await` it, and pass in the `message` from the user. It should look like this:

```js
await speak(message);
```

Run the program, enter a message, click the button, and hear the wonderful Bradley Cooper-inspired voice speak the cat's message!

## Conclusion
By the end of the code-along, the added code in the **script.js** file should look something like this:

```js
async function run() {
  let catPic = document.querySelector("#cat-pic");
  catPic.src = "https://media.tenor.com/o8m3bKTsifUAAAAM/hold-on.gif";

  let messageInput = document.querySelector("#cat-message");
  let message = messageInput.value;

  catPic.src = `https://cataas.com/cat/says/${message}`;

  await speak(message);
}
```

## Next Steps
[Click here to see how you can make more updates to the Cat Says site!](CatSaySelfPacedWork.md)
