# Code-Along: Cereal Mascots for Some Reason
In this code-along, create a website that showcases cereal mascot trading cards for some reason.

## Setting Up
[Click here to go to the Cereal Start project.](https://glitch.com/edit/#!/cereal-mascots-compendium)

Start by remixing the project. There is a decent amount of starter code.

#### HTML Starter Code
The **index.html** file has some basic elements, including:

- A `<button>` that calls a function named `filterList` when clicked
- A container `<div>` with an `id` of `mascot-container`
- A `<link>` that links to the **style.css** file
- A `<script>` that pulls from the **script.js** file
    - This is at the bottom of the `<body>` element so that it runs deferred

#### CSS Starter Code
There is quite a bit of CSS code in the **style.css** file - most of this is to make card flipping work later. Do not worry too much about it, but know there is a `.flipped` selector that will be of great importance.

#### JavaScript Starter Code
There is one variable in the **script.js** file - `mascots`. This is an array containing objects, each object with some properties about a different cereal mascot. This code-along is all about displaying that data in an engaging way!

#### Images
Also of note, there are some images referenced by URL.

### Beginning
There is a lot of setup, but nothing is actually functional yet. Run the project and notice that no mascots appear!

## Name Cards: Text
The first step is to simply display the names of each mascot in the `mascots` array. This will be possible using the `map` function, and the `forEach` function.

### The Basics
Start by defining and calling the function.

1. Open the **script.js** file for editing
1. At the bottom, define a new `function` named `displayCards`
1. Under the definition, call the function

It won't do anything yet, but here's how the code should look:

```js
function displayCards() {

}

displayCards();
```

### Mapping the Data
The next step is fairly involved, even though it only ends up being a single line of code. There is a lot of background information before the actual code appears - make sure it is fully understood!

#### Background: Getting Text Nodes
Each piece of data from the `mascots` array should be converted into an HTML text node containing its `name`. To explain this, start by thinking about how that would be possible for a single mascot object. Here's an example:

```js
let tony = {
  name: "Tony the Tiger",
  cereal: "Frosted Flakes",
  image: "https://i.pinimg.com/736x/51/4b/c8/514bc836deb22942d7266f23b06497a2.jpg",
  type: "animal",
  description: "Tony began to be humanized in the 1970s..."
}
```

The `name` could be stored in another variable, like this:

```js
let tonyName = tony.name;
```

That could be converted into a [text node](https://developer.mozilla.org/en-US/docs/Web/API/Document/createTextNode) like this:

```js
let tonyNode = document.createTextNode(tonyName);
```

Now, because there are multiple mascots, each piece of text can end with a dot to separate them. Instead of simply `tonyName`, the text could be a template literal like this:

```js
let tonyText = `${tonyName}. `;
```

So, to put it all together, if there were an object like `tony`, it could be converted into a text node like this:

```js
let tonyTextNode = document.createTextNode(`${tony.name}. `);
```

#### Background: Getting Text Nodes Function
In order to actually use this process on _every_ element in `mascots`, it will be necessary to convert the "text-node-ification" of an object into a **function**. The function should take in a mascot object, and return a text node. A good old-fashioned function _declaration_ might look something like this:

```js
function mascotToNode(mascot) {
  let mascotTextNode = document.createTextNode(`${mascot.name}. `);
  return mascotTextNode;
}
```

That's functional, but an _expression_ could be cleaner. Converting that function declaration into an anonymous function could go something like this:

```js
// remove name
function (mascot) {
  let mascotTextNode = document.createTextNode(`${mascot.name}. `);
  return mascotTextNode;
}
```

```js
// replace 'function' with '=>'
(mascot) => {
  let mascotTextNode = document.createTextNode(`${mascot.name}. `);
  return mascotTextNode;
}
```

```js
// simplify body
(mascot) => {
  return document.createTextNode(`${mascot.name}. `);
}
```

```js
// remove curly brackets and use implicit return
(mascot) => document.createTextNode(`${mascot.name}. `);
```

```js
// shorten parameter name
(m) => document.createTextNode(`${m.name}. `);
```

```js
// remove parameter parentheses
m => document.createTextNode(`${m.name}. `);
```

And there we have it! A clear, concise function expression that takes a mascot with a `name` and turns it into a text node!

#### Actually Mapping the Data to Text Nodes
Now that there's a function to create a text node from one object, it should be possible to create text nodes for _all_ objects. It is possible with `map`! **It's time to get back into the actual code!**

1. In the body of the `displayCards` function, name a new line
1. There, define a new variable named `mascotsHtml`
1. Set `mascotsHtml` to a call to `mascots.map`
    - Remember, the passed function will run on each element in `mascots`
    - The results will be stored in the `mascotsHtml` variable
1. Between the `(` and `)`, pass in the function expression from above
    ```js
    m => document.createTextNode(`${m.name}. `);
    ```

That's it! Now, there is an array that contains a bunch of text nodes, one for each piece of data. It should look something like this:

```js
let mascotsHtml = mascots.map(m => document.createTextNode(`${m.name}. `));
```

### Adding the Text to the Page
Now that there are a bunch of nodes, it will be necessary to throw them into the container.

#### Getting the Container
The first step is to grab the container from the HTML, and store it in a JavaScript variable.

1. Make a new line in the `displayCards` function body
1. Create a new variable named `container`
1. Set `container` to a call to `document.querySelector`
1. Pass in `'#mascot-container'` to grab `<div id="mascot-container">`

The line should look something like this:

```js
let container = document.querySelector("#mascot-container");
```

#### Appending Each Node
Next, use `forEach` to call `appendChild` on each node in the `mascotsHtml` array!

1. Make a new line in the body of the `displayCards` function
1. Call `forEach` on the `mascotsHtml` variable
1. Pass in an arrow function expression that takes one parameter: `m`
1. In the body of the expression, call `container.appendChild` on `m`

The line should look something like this:

```js
mascotsHtml.forEach(m => container.appendChild(m));
```

### Testing
Now, run the project and see what happens! It should create text nodes from all the objects in the `mascots` array, and append them all to the `<div>`. The added code in the **script.js** file should end up looking something like this:

```js
function displayCards() {
  let mascotsHtml = mascots.map(m => document.createTextNode(`${m.name}. `));

  let container = document.querySelector("#mascot-container");
  mascotsHtml.forEach(m => container.appendChild(m));
}

displayCards();
```

## Name Cards: Cards
Alright, so the site doesn't look great so far. It's just some text. We want each mascot to have their own card because that would be great for them. To start, create cards that simply have the name of each mascot. It will use an actual HTML `<div>` element instead of simply a text node.

1. Find the `mascots.map` line in the `displayCards` function
1. Add curly brackets to the function expression
1. Remove the body of the function expression, so it becomes `m => { }`
1. Make a new line between `{` and `}`
1. There, create a new variable named `mascotCard`
1. Set `mascotCard` to a call to `document.createElement("div")`
    - This will be the actual card!
1. Under that, set the `textContent` of `mascotCard` to be `m.name`
1. Finally, return `mascotCard`
    - Note that `return` is required because there are `{` and `}`

The updated code should look something like this:

```js
let mascotsHtml = mascots.map(m => {
  let mascotCard = document.createElement("div");
  mascotCard.textContent = m.name;
  
  return mascotCard;
});
```

Run the project again, and verify that the names are displayed on cards!

## Trading Cards: HTML
Okay, it's starting to come together a little bit. But... each card should have so much more. Each card should display:

- The picture
- The name
- The cereal

Each card should also flip over on click, revealing the description on the back. How is this possible????

### An Example
To see how this will look, there is some HTML to copy:

```html
<div onclick="this.classList.toggle('flipped');">
  <div>
    <img src="https://i.pinimg.com/736x/51/4b/c8/514bc836deb22942d7266f23b06497a2.jpg">
    <h4>Tony the Tiger</h4>
    <p>Frosted Flakes</p>
  </div>
  <div>Tony began to be humanized in the 1970s...</div>
</div>
```

Paste that into the container `<div>`:

```html
<div id="mascot-container">

</div>
```

Run the project to see how it looks! The goal will be to programmatically write up all that HTML for each element in the array.

## Trading Cards: Breaking Out the Function
This could get a little complex, so it will actually be a little easier to move the "mascot-card-creation" function expression somewhere else. This is not strictly necessary, but should make the code easier to write and maintain.

>Note: this is an example of _refactoring:_ the functionality should actually stay the same for now, but it will be easier to improve it later!

### Moving
Start by pulling the function expression code out of the `map`.

1. In the body of `displayCards`, find the `mascots.map` call
1. Cut the whole function parameter expression
    - This means copy it _and_ delete it
1. Paste it _above_ the `displayCards` function

At this point, the code should look something like this:

```js
m => {
  let mascotCard = document.createElement("div");
  mascotCard.textContent = m.name;
  
  return mascotCard;
};

function displayCards() {
  /* ... */
}
```

### Naming
Next, in order to actually _use_ this function expression, it needs to be stored somewhere!

1. Define a new variable named `objectToCard`
1. Set it to the function expression
1. Add a semi-colon at the end

It should look like this:

```js
let objectToCard = m => {
  let mascotCard = document.createElement("div");
  mascotCard.textContent = m.name;
  
  return mascotCard;
};
```

### Passing
Now, all that's left is to pass that function _into_ the `map` function! This will run it on every element in the `mascots` array, and convert them all into HTML objects.

1. Find the `mascots.map` function call
1. Between the parentheses, pass the function variable (`objectToCard`)

It should look something like this:

```js
let mascotsHtml = mascots.map(objectToCard);
```

Run the project again, and verify that the cards still appear as they did before!

## Trading Cards: Data to HTML
Now it's time to update that `objectToCard` function so that it creates better cards.

### Static HTML
Start by replacing every card with the raw HTML from before, containing the information about Tony the Tiger.

1. Find the `objectToCard` function expression body
1. Remove the line that sets the `textContent`
1. In its place, create a new variable named `cardHTML`
1. Set `cardHTML` to a new template literal, and make some new lines between the backticks
1. For now, paste in the HTML from within the containing `<div>` above
    - Two `<div>` elements, the first with an `<img>`, `<h4>`, and `<p>`
    - **Note: Do not copy the containing `<div>` element!!**
1. Under that, set the `innerHTML` property of the `mascotCard` object to be `cardHTML`

The updated code in the body of the `objectToCard` should now look something like this:

```js
let cardHTML = `
  <div>
    <img src="https://i.pinimg.com/736x/51/4b/c8/514bc836deb22942d7266f23b06497a2.jpg">
    <h4>Tony the Tiger</h4>
    <p>Frosted Flakes</p>
  </div>
  <div>Tony began to be humanized in the 1970s...</div>
`;

mascotCard.innerHTML = cardHTML;
```

Run the project again. Now, you should see your website with all tonys. It's pretty close - just needs the specific data!

### Dynamic HTML
Luckily, each time `objectToCard` is called, there is a parameter that has all the data for each individual mascot. This is all stored in the `m` object, under `m.image`, `m.name`, `m.cereal`, and `m.description`. Using `${expression}` notation, it will be possible to put this data into the HTML!

1. Find the `cardHTML` template string (between backticks), and get ready to update it
1. Replace the image URL with `${m.image}`
1. Replace `Tony the Tiger` with `${m.name}`
1. Replace `Frosted Flakes` with `${m.cereal}`
1. Replace `Tony began to be humanized in the 1970s...` with `${m.description}`

The updated code should end up looking something like this:

```js
let cardHTML = `
  <div>
    <img src="${m.image}">
    <h4>${m.name}</h4>
    <p>${m.cereal}</p>
  </div>
  <div>${m.description}</div>
  `
```

Now, each run through the function will pull directly from the `mascots` array data! Run the project again, and verify that each mascot has their own card.

## Trading Cards: Flipping
The cards are looking great! You know what's even cooler than the cards are looking great? The cards should be able to flip when clicked. This will be possible using `addEventListener`, and another arrow function expression.

1. Find the body of the `objectToCard` function expression
1. Make a new line under the `mascotCard.innerHTML` line
1. There, call `mascotCard.addEventListener`
1. For the first argument, pass in `"click"`
1. For the second argument, create a new arrow expression
    - Start with empty parentheses: `()`
    - Then, the arrow symbol: `=>`
    - Then, curly brackets: `{}`
1. Click between `{` and `}` and press enter to make a new line
1. There, call the `mascotCard.classList.toggle` function
    - This will add a class if it's not there, and remove it if it is
1. Pass in `"flipped"` as the argument
    - This class controls the CSS determining whether a card is flipped or not

The added code should look something like this: 

```js
mascotCard.addEventListener("click", () => {
  mascotCard.classList.toggle("flipped");
});
```

Run the project again, and verify that the cards all flip over and show the mascot descriptions when you click them!

## Filtering the Cards
Everything is looking pretty great now! But there is still the matter of that non-functional "Filter" button. It should be able to filter the cards shown based on their `type` property. This may not seem like a big deal now, but if there were 100 mascots, it would be very useful!

### Parameterization
Right now, every time the `displayCards` function runs, it uses the `mascots` array to show the cards. This will not work if we do not always want to use that array! The first step is to _parameterize_ the `displayCards` function so that it can display _any_ array of mascots.

1. Find the `displayCards` function definition
1. Between the parentheses, add `mascotsArray` as a parameter
1. In the body, replace `mascots` with `mascotsArray`
1. Find where `displayCards` is called
1. There, between the parentheses, add `mascots`

The updated code should end up looking something like this:

```js
function displayCards(mascotsArray) {
  let mascotsHtml = mascotsArray.map(objectToCard);
  // ...rest of body ...
}

displayCards(mascots);
```

Note that this will not change anything... yet!

### Prompting on Button Click
Next, hook up the button to a basic function that uses `prompt` to ask for a type by which to filter. Note that the button has an `onclick` that calls a function named `filterList` - but it has not been defined!

1. Make a new line at the bottom of the **script.js** file
1. There, define a new function named `filterList`
1. Make a new line in the body of the `filterList` function
1. There, create a new variable named `type`
1. Set `type` to the result of a `prompt` call
1. For the `prompt` call, pass in `"What type of mascot do you want to see?"`

The code for the new `filterList` function should look something like this so far:

```js
function filterList() {
  let type = prompt("What type of mascot do you want to see?");
}
```

Run the project, click the "Filter" button, and verify that the prompt appears!

### Displaying the Specific Cards
The function now knows what type of mascot to display, but... it's not doing anything with that information. Use the `filter` array method to narrow down the mascots, and then use `displayList` to display them!

1. Make a new line under the `type` variable in the body of the `filterList` function
1. There, create a new variable named `filteredList`
1. Set `filteredList` to be a call to `mascots.filter`
1. For the `filter` argument, create a new arrow function expression
    - Start with a parameter: `m` (this is the current mascot)
    - Next, the arrow: `=>`
    - No curly brackets needed
1. In the body of the function expression, check if `m.type` is equal to `type`
    - This way, only mascots with the same `type` property as the user entered will be in the resulting array!
    - Note the implicit return - it's already returning a boolean, so the conditional expression is all that's needed
1. On the next line, call the `displayCards` function, and pass in `filteredList`

The code should end up looking something like this:

```js
let filteredList = mascots.filter(m => m.type === type);
displayCards(filteredList);
```

Run the project, click the "Filter" button, and... maybe something is wrong? Yes, something is wrong! The new cards should be appended correctly, but the old ones are still there!

### Clearing the Container
Every time the `displayList` function is called, any existing cards should be removed _before_ the new ones are added.

1. Find the `displayList` function
1. Find the line where `container` is defined
1. Make a new line under that
1. There, set the `innerHTML` of the `container` object to be empty
    - Make sure this happens _above_ the `mascotsHtml.forEach`!

The new line should look like this:

```js
container.innerHTML = "";
```

Now it should work! Try to filter the cards, and make sure it works 😊

## Conclusion
By the end of the activity, the added code in the **script.js** file should look something like this:

```js
// A function to create an HTML "card" element from a mascot object
let objectToCard = m => {
  // First create a <div>
  let mascotCard = document.createElement("div");

  // Add all the HTML text to show the image, name, cereal, and description
  let cardHTML = `
    <div>
      <img src="${m.image}">
      <h4>${m.name}</h4>
      <p>${m.cereal}</p>
    </div>
    <div>${m.description}</div>
    `

  // Set the inner HTML of the element
  mascotCard.innerHTML = cardHTML;

  // Flip the card when it is clicked (toggle the .flipped selector)
  mascotCard.addEventListener("click", () => {
    mascotCard.classList.toggle("flipped");
  });

  // Return the HTML
  return mascotCard;
};

// A function to display a given array of mascot objects
function displayCards(mascotsArray) {
  // Convert ALL the mascots from the array into HTML Elements
  let mascotsHtml = mascotsArray.map(objectToCard);

  // Get the containing element
  let container = document.querySelector("#mascot-container");
  container.innerHTML = "";

  // Append each child to the container
  mascotsHtml.forEach(m => container.appendChild(m));
}

// Display the full list to start!
displayCards(mascots);

// A function that displays a filtered list
function filterList() {
  // Get what type of mascot to display
  let type = prompt("What type of mascot do you want to see?");

  // filter the list by type
  let filteredList = mascots.filter(m => m.type === type);

  // display the filtered list
  displayCards(filteredList);
}
```
