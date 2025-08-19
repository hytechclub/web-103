# Code-Along: Dog Fetcher
Follow these instructions to build a website that will provide the user with some pictures of dogs.

[Click here to view the Dog Fetcher Starter project.](https://hytop.onrender.com/e/dog-fetcher-start) Copy the project to begin the activity.

## Part One: Background
Typically, dogs play fetch. In this activity, _your code_ is going to be playing fetch, and the things that your code will be fetching will be dogs!

![](Assets/DogPlayingFetch.jpg)

### The Starter Code
The starter project has quite a bit of code, but it's all HTML and CSS! In the **index.html** file, there are a few elements of note:

- An `<input>` with an `id` of `"num-dogs"`
- A `<button>` with an `onclick` of `"getDogs()"`
- An `<img>` with an `id` of `"loading"`
    - This is currently hidden using CSS
- A `<div>` with an `id` of `"dog-imgs"`

All of these elements will be necessary to make the website functional.

### NOT WORKING: The [shibe.online](https://shibe.online/) API
_Note: the shibe.online API appears to be down. Use [https://hytop.onrender.com/api/fake-api/dogs](https://hytop.onrender.com/api/fake-api/dogs) instead._

The code needs something to fetch, and luckily, there is an API that provides random pictures of shiba inu dogs! These adorable pups are also known as "shibes" in internet parlance - hence the name, [shibe.online](https://shibe.online/). Take a look at the homepage to learn more about how the API works.

The _base url_ is `https://shibe.online/api/shibes`. For the purposes of this activity, the only relevant _query parameter_ will be `count`. The response will be a JSON array of strings; each one a URL pointing to a picture of a shibe.

Putting it all together, here's an example URL: [`https://shibe.online/api/shibes?count=3`](https://shibe.online/api/shibes?count=3)

The response should look something like this:

```json
[
  "https://cdn.shibe.online/shibes/039e86853cb65ed16cb3823a4fd9528ae374cfec.jpg",
  "https://cdn.shibe.online/shibes/6179b94f4e16762f29e69b48a45f16372b11ed72.jpg",
  "https://cdn.shibe.online/shibes/e0419f6e1f00e800bada84233b0bad86723077ed.jpg"
]
```

Try opening one of the URLs to see the picture! Here is one of them:

![](https://cdn.shibe.online/shibes/6179b94f4e16762f29e69b48a45f16372b11ed72.jpg)

### The Plan
To utilize this API, the code should:

- Make a request to the base URL using `fetch`
    - Use the `<input>` to determine the `count` to pass in as a query parameter
- Extract the image URLs from the response
- Create new `<img>` elements, one for each URL returned

## Part Two: Button Begins 🦇
Currently, there is no JavaScript code in the project. That's bad! Start things off by hooking up the `<button onclick="getDogs()">` with a new function definition.

1. Open the **script.js** file for editing
1. Define a new function named `getDogs`
1. In the body of the function, create a new variable named `loadingImg`
1. Set `loadingImg` to grab the `<img id="loading">` picture
    - Use `document.querySelector` for this
1. On the next line, set the `style.display` of the image to `"inline-flex"`
    - This will make the loading indicator appear

At this point, run the project, click the "Get Dogs" button, and verify that the loading indicator image appears! The code should look something like this:

```js
function getDogs() {
  let loadingImg = document.querySelector("#loading");
  loadingImg.style.display = "inline-flex";
}
```

## Part Three: Fetching Two Dogs 🐕🐕
Now the button is ready, so it's time to try to get some dogs! To start, the code can ignore the `<input>` and just try to get two dogs.

### Trying to Fetch with `fetch`
Use the `fetch` function to send a request out to the API to _try to_ get some shibe pics.

1. Make a new line in the body of the `getDogs` function
1. Create a new variable named `response`
1. Set `response` to equal a call to `fetch`
    - Pass in \``https://hytop.onrender.com/api/fake-api/dogsdogs?count=2`\` as the URL
1. Under that, create a variable named `responseJson`
1. Set `responseJson` to a call to the `json()` function on the `response` variable
1. Finally, call `alert` on `responseJson` to display the result

With that, run the code, click the "Get Dogs" button again, and see what happens. It might not quite work... it should display a pop-up, but there is an issue with this code:

```js
let response = fetch(`https://hytop.onrender.com/api/fake-api/dogs?count=2`);
let responseJson = response.json();
alert(responseJson);
```

### Catching an Error with `try`/`catch`
So something is wrong, and it _may be_ possible to debug it, but it is also possible for the _code itself_ to catch the error! Use the `try`/`catch` structure to try to figure out what is happening.

1. Above the current variables, _declare_ `response` and `responseJson` without giving them a value
    - This will allow the code to use them in and out of the `try` block
1. Under that, create a `try`/`catch` structure
    - Start with the `try` keyword
    - Then, add curly brackets `{` and `}`
    - After that, add the `catch`
    - For the `catch`, add parentheses `(` and `)`
    - Put `e` within the parentheses to represent the error
    - Finally, add another set of curly brackets `{` and `}`
1. Move the original variable sets into the `try` block
    - Make sure to get rid of the `let` because these already exist
1. In the `catch` block, call `alert` on the error
1. Also in the `catch` block, `return` from the function

The modified code should look something like this:

```js
let response, responseJson;

try {
  response = fetch(`https://hytop.onrender.com/api/fake-api/dogs?count=2`);
  responseJson = response.json();
} catch (e) {
  alert(e);
  return;
}
```

Now, try running the project and clicking the button. It still will not work, but at least the error should appear in a pop-up! It should say the following:

```
TypeError: response.json is not a function
```

### Fixing the Error with Asynchronicity
Hmm... why would `response.json` not be a function? The `fetch` call _should_ return a `Response` object... or should it? What does the `fetch` function return again?

**The `fetch` function returns a Promise object - so it must be `await`ed to yield the actual result!**

1. Start by adding the `async` keyword to the `getDogs` function definition
1. Next, add the `await` keyword in front of the `fetch` call
1. Also, add the `await` keyword in front of the `json()` call
1. Additionally, add a `finally` block after the `catch` block
1. There, make the loading indicator disappear
    - Use `.style.display = "none"` to accomplish this
1. Additionally, for testing, purposes, call `alert` on `responseJson`

Run the program, click the "Get Dogs" button again, and verify that some dog image URLs appear! Copy and paste one into a new tab to see a shibe like [this](https://images.dog.ceo/breeds/shiba/kurosuke01.jpg).

At this point, the entire code in the **script.js** file should look something like this:

```js
async function getDogs() {
  let loadingImg = document.querySelector("#loading");
  loadingImg.style.display = "inline-flex";

  let response, responseJson;
  
  try {
    response = await fetch(`https://hytop.onrender.com/api/fake-api/dogs?count=2`);
    responseJson = await response.json();
  } catch (e) {
    alert(e);
    return;
  } finally {
    loadingImg.style.display = "none";
  }

  alert(responseJson);
}
```

## Part Four: Displaying the Images
The `fetch` request is actually working! The JavaScript code is talking to an API and retrieving something from the internet. The next step is to display the results in a nicer way.

### Prepping the Container
There is already a `<div id="dog-imgs">` container in the **index.html** file - this will hold the new pictures of dogs. The first step will be to grab it, and clear out anything that's in it.

1. Remove the `alert` from the body of the `getDogs` function
1. In its place, create a new variable named `dogImgsDiv`
1. Use `document.querySelector` to grab the `<div id="dog-imgs">` and store it in the variable
1. Under that, set the `innerHTML` of the `dogImgsDiv` to be `""`

The code for this part should look something like this:

```js
let dogImgsDiv = document.querySelector("#dog-imgs");
dogImgsDiv.innerHTML = "";
```

### Looping the Response
The goal is to create one picture element _for each_ picture URL in the response. The `responseJson` object should be an array that stores something like this:

```
[
  "https://images.dog.ceo/breeds/shiba/shiba-9.jpg",
  "https://images.dog.ceo/breeds/shiba/shiba-10.jpg"
]
```

The `forEach` array function will be perfect for this! First, establish the loop.

1. Make a new line at the bottom of the `getDogs` function
1. There, call the `forEach()` function on `responseJson`
1. Between the parentheses, create a new _arrow function_
    - It should have one parameter: `dogUrl`
    - It should have an arrow: `=>`
    - It should have curly brackets: `{` and `}`

The loop code should look something like this:

```js
responseJson.forEach(dogUrl => {});
```

### Adding Each Image to the Container
Now the code is setup to run a block for every image URL retrieved from **hytop.onrender.com/api/fake-api**. For each of them, a new `<img>` element should be created and added to the `dogImgsDiv` container!

1. Within the `forEach` arrow function body, make a new line
1. There, create a new variable named `newDogImg`
1. Set `newDogImg` to be a new `"img"` element using `document.createElement`
1. Under that, set the `src` of `newDogImg` to the `dogUrl` value
1. Under that, append the `newDogImg` element to the `dogImgsDiv` element
    - Use `appendChild` to accomplish this

Run the project, click the "Get Dogs" button, and verify that the dog images actually appear now! Click it a few times to see some different pairs of dogs. The code in the body of the arrow function should look something like this:

```js
let newDogImg = document.createElement("img");
newDogImg.src = dogUrl;
dogImgsDiv.appendChild(newDogImg);
```

## Part Five: Dynamic Number of Dogs
The final step is to actually take into account the text box - this will allow the user to grab a specific number of shibes!

1. Make a new line _above_ the `let response, responseJson` line in the body of the `getDogs` function
1. There, create a new variable named `numDogsInput`
1. Set `numDogsInput` to be the `<input id="num-dogs">` element
    - Use `document.querySelector`
1. Under that, create a new variable named `numDogs`
1. Set `numDogs` to be the `value` of the `numDogsInput` element
1. Find the `fetch` call
1. In the `fetch` URL, replace the `2` with the interpolated `numDogs` value
    - Use `${numDogs}`

Run the project, enter a number of dogs, click the "Get Dogs" button, and verify that the proper number of dogs appears!

## Conclusion
Wow. There sure are some dogs in that API! In this activity, the code used `fetch` to grab data from an API (using an HTTP GET request) and display images from it.

By the end of the code-along, the **script.js** file should look something like this:

```js
async function getDogs() {
  let loadingImg = document.querySelector("#loading");
  loadingImg.style.display = "inline-flex";
  
  let numDogsInput = document.querySelector("#num-dogs");
  let numDogs = numDogsInput.value;

  let response, responseJson;

  try {
    response = await fetch(`https://hytop.onrender.com/api/fake-api/dogs?count=${numDogs}`);
    responseJson = await response.json();
  } catch (e) {
    alert(e);
    return;
  } finally {
    loadingImg.style.display = "none";
  }

  let dogImgsDiv = document.querySelector("#dog-imgs");
  dogImgsDiv.innerHTML = "";
  
  responseJson.forEach(dogUrl => {
    let newDogImg = document.createElement("img");
    newDogImg.src = dogUrl;
    dogImgsDiv.appendChild(newDogImg);
  });
}
```

## Next Steps
[Click here to see how you can make more updates to the Dog Fetcher site!](DogFetcherSelfPacedWork.md)
