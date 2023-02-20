# Self-Paced Work: Trading Card Updates
Follow these instructions to update the trading card website.

## New Trading Cards
Currently, all the trading cards display information about cereal mascots. If you're a big fan of cereal mascots, that's gr-r-reat! You can add more mascots. If not, you can make entirely new types of trading cards.

1. Open the **script.js** file for editing
1. Find the `mascots` array definition at the top
1. Add **at least three** new objects
    - Make sure to upload pictures for them into the **images/** folder!
1. Update any of the existing objects as desired

Here are some other ideas for types of trading cards:

- Soccer Players Or Other Athletes
- Pokemon or Digimon
- Music Artists Or Bands
- Your Own Friends
- Any Characters From Anything At All

Try to have some fun with it!

## New Styles
Currently, the theme is very yellow-orange looking. Feel free to update the colors, fonts, borders, or any other styles!

## Type on Card
Currently, each object should contain a `type` property - but this is actually not shown anywhere. Display it on the front of each card.

The type can be shown within a `<p>` element (under the cereal name) like so:

```js
<p>Type: animal</p>
```

Here are the steps to follow:

1. Open the **script.js** file for editing
1. Find the `objectToCard` function expression
1. Within the body, find the `cardHTML` variable
1. In the HTML text, add a `<p></p>` under the existing `<p></p>`
1. Make the text within the `<p>` say `Type: `
1. After the colon, add the code to insert the `type` for the given mascot

That should be it! Run the project, and very that the type appears on each card.

## Cards Unfiltered
Currently, after the list has been filtered, there is no way to get back to an unfiltered view of cards. Update the filter so that it is possible to show all cards again! This should happen if the user enters "all" when prompted.

There are a number of ways to do this. Try to figure out the simplest way!

## Search Box
The filter is cool, but what if someone wanted to search by the name of the mascot? There should be a way to do that!

### HTML & CSS
Start by creating a new label, text box, and button in the **index.html** file. Here is a basic rundown of the new elements that must be added:

- A piece of text of some kind indicating that the user should enter a "name" in the text box box
- An `<input type="text">` with an `id` attribute set to `"name"`
    - This is so that its value can be retrieved by the JavaScript
- A `<button>` with an `onclick` attribute that calls a function named `filterByName`
    - This is so that the list can be filtered when this button is clicked
    - The button should have text that indicates it can be clicked to filter

It does not have to look perfect, but it may be a good idea to update some CSS so that the label, text box, and button look nice on the page.

### JavaScript
The actual functionality can be added via JavaScript. This will look very similar to the `filterList` function.

1. Open the **script.js** file for editing
1. Make a new line at the bottom of the file
1. There, define a new function named `filterByName`
1. In the body of the function, define a new variable named `nameElement`
1. Set `nameElement` to be a call to `document.querySelector`
    - This should grab the `<input id="name">`
1. Create a new variable named `name`
1. Set `name` to be the `nameElement`'s value
1. Under that, create a new variable named `filteredList`
1. Set `filteredList` to be a call to `mascots.filter`
1. For the `filter` argument, create a new arrow function expression
    - Start with the parameter `m`
    - Then the arrow: `=>`
1. For the arrow function body, check if `m.name` is equal to `name`
1. Finally, call the `displayCards` function and pass in `filteredList`

This should be all that's necessary for a functioning search box! Run the project, enter a full name (with correct capitalization), and verify that only that result appears!

## Search Box: Starts With
The search box is somewhat helpful, but it only works if the user enters the _exact_ name of the mascot. Fix this so that it ignores capitalization, and also only checks if the name _starts with_ the search term.

There will be a couple useful string functions for this:

- [`toLowerCase`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)
- [`startsWith`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith)

Follow these steps:

1. Open the **script.js** file for editing
1. Find the `filterByName` function definition
1. In the body, find the function expression passed into `mascots.filter`
1. Add curly brackets to the arrow function expression
1. In the body (between the new `{` and `}`), make a new line
1. There, create a new variable named `nameLc`
1. Set `nameLc` to be the `name` from the text box in [all lowercase](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)
1. Under that, create a new variable named `mNameLc`
1. Set `mNameLc` to be the mascot's name in [all lowercase](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)
1. Under that, create a new variable named `nameStartsWith`
1. Set `nameStartsWith` to check if `mNameLc` [starts with](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith) the letters from `nameLc`
1. Use a `return` statement to return the `nameStartsWith` variable value

That should be it! Test out the function to make sure it returns the properly filtered list. 

## Search Box: On Text Changed
This is working pretty well! But it may get annoying to keep clicking that "Filter by Name" button. Luckily, it is possible to automatically run a function whenever text is input.

1. Open the **script.js** file for editing
1. Make a new line at the bottom of the file
1. Create a new variable named `nameElement`
1. Store the `<input id="name">` in the `nameElement` variable
1. Call `addEventListener` on `nameElement`
1. Pass in `"input"` as the first argument
1. For the second argument, create a new arrow function expression
    - Start with parentheses: `()`
    - Then the arrow symbol: `=>`
    - Then curly brackets: `{}`
1. Make a new line within the curly brackets
1. There, call the `filterByName` function

Run the project and see how it works! When text is entered in the "name" box, the list should filter automatically.

## Search Box: Refactoring and Updating
The search box is working, but there are a few updates that might make it better:

- It should not have to get the `nameElement` variable more than once
- It should filter by text in any part of the name (not just the beginning)
- The "Filter by Name" button can be removed
- The text box should look nicer
- It could check against cereal in addition to name
- It could check against description and type as well
- There could be multiple fields for the different object properties

There are a ton of other possible enhancements - try to improve the site in any way you can!
