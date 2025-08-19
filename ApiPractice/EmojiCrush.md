# Emoji Crush
Follow these instructions to create a website that displays information about a random emoji.

[Click here to view the Emoji Crush Starter project.](https://hytop.onrender.com/e/emoji-crush-start) Copy the project to begin the activity.

## Part Zero: Background
There is basically no starter code for this project, but the API will make it relatively simple to add functionality to the site.

### The API
The API that makes this possible is named EmojiHub. There are a couple endpoints available, but the important one is the one that returns data about a random emoji. The URL is static, but it will return a variety of random different emoji.

#### URL
[https://emojihub.yurace.pro/api/random](https://emojihub.yurace.pro/api/random)

#### Response
```json
{
  "name": "shark",
  "category": "animals and nature",
  "group": "animal marine",
  "htmlCode": [
    "&#129416;"
    ],
  "unicode": [
    "U+1F988"
  ]
}
```

The important pieces of data are the `name`, the `category`, and the `htmlCode`.

### The Goal
The goal is to generate a random emoji, and add some information to the site when the button is clicked!

## Part One: HTML From JavaScript
To start, it may be worthwhile to look at the HTML on its own, for one example emoji.

### Demonstrating the HTML
Purely for demonstration purposes, add some code to make information about the eye emoji appear.

1. Open the **index.html** file for editing
1. Find the `<div id="emoji-text"></div>` element
1. Make a new line within the opening and closing tags
1. There, add a `<p></p>` element that says `"You should send them the &#128065; emoji`
1. Wrap the emoji code in a `<span></span>`
    - This will allow it to be styled with CSS
1. Under the `<p></p>`, make another `<p></p>`
1. Make it say `"This emoji is named eye and it is from the smileys and people category"`
1. Wrap the "eye" and "smileys and people" text in `<span></span>` elements
1. Under that, add another `<p></p>`
1. Make it say `"Sending them this emoji will definitely make them like you"`
1. Wrap the "definitely" in an `<i></i>` to make it _italic_

Alternatively to all that, feel free to copy and paste this code into the **index.html** file:

```html
<p>You should send them the <span>&#128065;</span> emoji</p>
<p>This emoji is named <span>eye</span> and it is from the <span>smileys and people</span> category</p>
<p>Sending them this emoji will <i>definitely</i> make them like you</p>
```

Run the project to see how it looks!

### Building HTML from JavaScript
To start making this more functional, define a function that will dynamically add the HTML to the page.

1. Open the **script.js** file for editing
1. Define a function named `showEmoji`
1. In the body of the `showEmoji` function, create a variable named `textElement`
1. Use `document.querySelector` to grab the `<div id="emoji-text">` from the HTML, and store it in the `textElement` variable
1. On the next line, set the `textElement.innerHTML` property to be a new template literal
1. Make some new lines within the template literal, and paste in the HTML code from above
1. Remove the HTML code from the **index.html** file as it is no longer needed

Run the project, click the "Click Me" button, and verify that information about the eye emoji appears! The added code should look something like this:

```js
function showEmoji() {
  let textElement = document.querySelector("#emoji-text");

  textElement.innerHTML = `
<p>You should send them the <span>&#128065;</span> emoji</p>
<p>This emoji is named <span>eye</span> and it is from the <span>smileys and people</span> category</p>
<p>Sending them this emoji will <i>definitely</i> make them like you</p>
`;
}
```

## Part Two: Dummy Data
Now this works for one emoji, but it is still very static. The raw HTML contains hard-coded values. Instead, use some dummy data to prepare the `showEmoji` function for working with real live data.

The main idea with this is to create some mock data to _pretend_ the API is returning actual data. That way, it will be possible to define how to _handle_ the data even before there is real data! This separation of concerns can be very helpful in software development; breaking large problems into bite-sized tasks can make them feel much less overwhelming. Take it one step at a time!

### Defining the Dummy Data
The example data can be created based on a response from the API. The important thing is that it should be in the same format, and have all the same properties and structure. The shark example from the response above will be used for this dummy data.

1. Open the **script.js** file for editing
1. Make a new line at the very top of the file
1. There, create a new variable named `exampleData`
1. Set `exampleData` to be an empty object
1. Add a `name` property to the object with a value of `"shark"`
1. Add a `category` property to the object with a value of `"animals and nature"`
1. Add a `group` property to the object with a value of `"animal marine"`
1. Add a `htmlCode` property to the object with a value of `["&#129416;"]`
    - Note: this is an array with one element
1. Add a `unicode` property to the object with a value of `["U+1F988"]`
    - Note: this is an array with one element

The added variable should end up looking something like this:

```js
let exampleData = {
  name: "shark",
  category: "animals and nature",
  group: "animal marine",
  htmlCode: ["&#129416;"],
  unicode:["U+1F988"]
};
```

This simulates the response that would be received from a real `fetch` API call.

### Extracting the Dummy Data
The next step is for the `showEmoji` function to grab that data, find the relevant pieces, and use those pieces in the rendered HTML.

1. Open the **script.js** file for editing
1. Find the `showEmoji` function body
1. Make a new line under the `textElement` variable creation
1. There, create a new variable named `emojiData`, set to `exampleData`
1. Under that, create a new variable named `emoji`
1. Set `emoji` to be the first element from the `htmlCode` property of the `emojiData` object
1. Under that, create another new variable named `name`
1. Set `name` to be the `name` property of the `emojiData` object
1. Under that, create another new variable named `category`
1. Set `category` to be the `category` property of the `emojiData` object

The added code should look something like this:

```js
let emojiData = exampleData;

let emoji = emojiData.htmlCode[0];
let name = emojiData.name;
let category = emojiData.category;
```

Now all the data has been extracted, but it still has to be used!

### Passing the Dummy Data
Next, insert that data into the rendered HTML.

1. Open the **script.js** file for editing, and find the body of the `showEmoji` function
1. Find where the `textElement.innerHTML` property is set
1. In the template literal, remove the eye HTML code in the first `<span>`
1. Replace the code with the interpolated value of the `emoji` variable
1. Replace the word `eye` with the interpolated `name` value
1. Replace the "smileys and people" with the interpolated `category` value

Run the project, click the button, and verify that shark emoji information appears! The updated code with the interpolated variables in the template literal should look something like this:

```js
  textElement.innerHTML = `
<p>You should send them the <span>${emoji}</span> emoji</p>
<p>This emoji is named <span>${name}</span> and it is from the <span>${category}</span> category</p>
<p>Sending them this emoji will <i>definitely</i> make them like you</p>
`;
}
```

## Part Three: Real Data
Now it's time to get real. Instead of using that dummy data, the code should make a call to the EmojiHub API, and return that data.

### Defining the Function to Fetch Data
The first step is to setup the `fetch` call.

1. Open the **script.js** file for editing
1. Define a new function named `fetchEmojiData`
    - Make the function asynchronous with the `async` keyword
1. In the function body, _declare_ a new variable named `emojiData`
1. Under that, setup a `try`/`catch` structure
1. In the `try` block, create a new variable named `response`
1. Set `response` to an `await`ed call to `fetch`
1. Pass in the proper URL to the function call: `https://emojihub.yurace.pro/api/random`
1. Under that in the `try`, set `emojiData` to an `await`ed `response.json()` function call
1. In the `catch` block, alert the error message
1. Outside of the `try`/`catch`, at the bottom of the body, return `emojiData`

The function definition should look something like this:

```js
async function fetchEmojiData() {
  let emojiData;

  try {
    let response = await fetch(`https://emojihub.yurace.pro/api/random`);
    emojiData = await response.json();
  } catch (e) {
    alert(e);
  }

  return emojiData;
}
```

### Calling the Function
Now that the function has been defined, it must be called!

1. Open the **script.js** file for editing
1. Make the `showEmoji` function asynchronous with the `async` keyword
1. In the body of the `showEmoji` function, find the `emojiData` variable creation
1. Replace `exampleData` with an `await`ed call to the `fetchEmojiData` function
1. Remove the `exampleData` variable from the top of the file

Now, run the project, click the button, and verify that a random emoji appears! The added code for this part should look like this:

```js
let emojiData = await fetchEmojiData();
```

## Conclusion
It is certainly more difficult to build something from scratch, but it also helps reinforce the concepts quite a bit. This API has fairly simple data, but it can be used in powerful and creative ways!

### Final Code
The code in the **script.js** file should look something like this:

```js
async function fetchEmojiData() {
  let emojiData;

  try {
    let response = await fetch(`https://emojihub.yurace.pro/api/random`);
    emojiData = await response.json();
  } catch (e) {
    alert(e);
  }

  return emojiData;
}

async function showEmoji() {
  let textElement = document.querySelector("#emoji-text");
  let emojiData = await fetchEmojiData();

  let emoji = emojiData.htmlCode[0];
  let name = emojiData.name;
  let category = emojiData.category;

  textElement.innerHTML = `
<p>You should send them the <span>${emoji}</span> emoji</p>
<p>This emoji is named <span>${name}</span> and it is from the <span>${category}</span> category</p>
<p>Sending them this emoji will <i>definitely</i> make them like you</p>
`;
}
```

### Update Ideas
The site is pretty good as-is, but there is always room for improvement. Here are some ideas:

- Update the CSS for the page
- Allow the user to select a category for the emoji like [this](https://emojihub.yurace.pro/api/random/category/food-and-drink)
- Display more than one emoji if requested
- Display the group in addition to the category

Feel free to use the API for any desired purpose.
