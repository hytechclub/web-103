# Color Schemer
Follow these instructions to update a website that generates aesthetically pleasing color schemes.

[Click here to view the Color Schemer Starter project.](https://glitch.com/edit/#!/color-schemer) Remix the project to begin the activity.

## Part Zero: Background
This project is already fairly substantial in terms of the code and the functionality.

### The User Experience
Currently, the user is able to select a color, click the "Generate a New Scheme" button, and see the colors change. There is also a "Randomize" button that will choose a random seed color, and then get the scheme.

This is functional, but it would be cool to be able to see some different types of color schemes... right now, it always uses "quad" mode.

### The API
The code uses <a href="https://www.thecolorapi.com/">T H E <span style="color: darkred">C O L O R</span> A P I</a> to pull matching colors for a given seed. A ton of data is returned from each request, but only some parts of it will be relevant.

For example, a `scheme` with the color red (`FF0000`), in `quad` mode, with `4` colors, could look like this:

#### URL
[https://www.thecolorapi.com/scheme?hex=FF0000&mode=quad&count=4](https://www.thecolorapi.com/scheme?hex=FF0000&mode=quad&count=4)

#### Response (Abbreviated)
```json
{
  "mode": "quad",
  "count": "4",
  "colors": [{
    "hex": {
      "value": "#70D10E",
    },
    "image": {
      "named": "https://www.thecolorapi.com/id?format=svg&hex=70D10E"
    },
    "contrast": {
      "value": "#000000"
    }
  },
  {
    "hex": {
      "value": "#0BE4E4",
    },
    "image": {
      "named": "https://www.thecolorapi.com/id?format=svg&hex=0BE4E4"
    },
    "contrast": {
      "value": "#000000"
    }
  }]
}
```

All of the color objects within the `colors` property array contain the hex values used to update the website styles.

### The Code
There are several functions in the **script.js** file that make the current site work how it does, as well as some set variables.

- `colorCustomProps`: this is the ordered array of [CSS custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties) that determine the colors for the page
- `chooseRandomFromList`: this chooses a random item from an array, and returns it
- `randomizeSeedColor`: this chooses a random hex value, and updates the HTML color input
- `randomizeSchemeType`: this function is not called yet - but it randomizes the value of the currently-non-existent scheme type dropdown
- `setNewScheme`: this takes some color objects and updates the custom properties to reflect their hex values
- `newScheme`: this makes the request to the API, and updates the scheme with the new colors
- `randomize`: this randomizes the seed color, and then sets the new scheme

_Note: You don't really need to understand all the code - you can still work with it!_

### The Goal
These instructions show how to add a new dropdown where the user can decide which type of color scheme they would like!

## Part One: HTML
The first step is to add the dropdown in the HTML. This will be possible using a `<select></select>` element that contains `<option></option>` child elements. Each `<option>` should have a `value` attribute representing the scheme type, and the `<select>` should have an `id` attribute so it is identifiable in the JavaScript. All of this should be wrapped in a `<p></p>` element, with a `<span></span>` that introduces the input.

### Creating the Dropdown

1. Open the **index.html** file for editing
1. Make a new line under the `<p>First, pick...</p>` element
1. There, create a new `<p></p>` element
1. Within the `<p>` and `</p>`, make a new line
1. There, create a `<span>` element that says "Next, pick a scheme type:"
1. Under that, create a `<select></select>` element
1. Give the `<select>` element an `id` of `"scheme-type"`

Run the project, and verify that a new input appears! So far, the added HTML should look something like this:

```html
<p>
  <span>Next, pick a scheme type:</span>
  <select id="scheme-type"></select>
</p>
```

### Adding the Options
The input is useless without any options, so add some options. There should be four options total, for these types:

- `quad`
- `analogic`
- `complement`
- `monochrome`

First, make a new line within the `<select>` and `</select>` tags. Then, for each of the four types:

1. Create a new `<option></option>` element
1. Add a `value` attribute with the given type
1. Add a capitalized name within the `<option>` and `</option>` tags

Run the project, and verify that all the options appear! The added options should look something like this:

```html
<option value="quad">Quad</option>
<option value="analogic">Analogic</option>
<option value="complement">Complement</option>
<option value="monochrome">Monochrome</option>
```

## Part Two: JavaScript
Now the HTML should all be good to go, but it's not actually doing anything yet! The next step is to include the scheme type from the dropdown as a query parameter in the API request.

1. Open the **script.js** file for editing
1. Find the `newScheme` function definition
1. Under the `hex` variable creation, make a new line
1. There, create a new variable named `schemeTypeInput`
1. Use `document.querySelector` to grab the `<select id="scheme-type">` from the HTML, and store it in the `schemeTypeInput` variable
1. Under that, create a new variable named `schemeType`
1. Set `schemeType` to be the `value` of `schemeTypeInput`
1. In the `url` template literal below, remove the `quad` after `mode=`
1. Replace `quad` with the interpolated `schemeType` value

Run the project, select a new scheme type (like monochrome), click the "Generate a New Scheme" button, and see a scheme of the new type! The updated code in the `newScheme` function should look something like this:

```js
async function newScheme() {
  // ...
  let schemeTypeInput = document.querySelector("#scheme-type");
  let schemeType = schemeTypeInput.value;

  let url = `https://www.thecolorapi.com/scheme?hex=${hex}&mode=${schemeType}&count=4`;
  // ...
}
```

## Part Three: Randomization
The final step is to include the scheme type in the randomization that happens when the "Randomize" button is clicked. Luckily, there is already a function that does this!

1. Open the **script.js** file
1. Find the `randomize` function definition
1. Make a new line above the call to the `newScheme` function
1. There, call the `randomizeSchemeType` function

Run the project, click the "Randomize" button, and verify that a random scheme type is selected! The updated code in the `randomize` function should look something like this:

```js
async function randomize() {
  randomizeSeedColor();
  randomizeSchemeType();
  await newScheme();
}
```

## Conclusion
The update may have been a small part of the overall functionality of the site, but being able to work with existing code and make it better is a huge part of software development. There are quite a few additional updates you could try to make - if you have any interest, try to make it whatever you'd like! Here are some ideas:

- Update the sample text and content so that it is more reflective of a real website
- Add additional colors through CSS custom properties, and grab more colors from the API call
- Display the colors (and even their names) every time a new color scheme is set
- Add more scheme types based on the scheme modes: `monochrome-dark`, `monochrome-light`, `analogic-complement`, and `triad`

Feel free to use the API for any desired purpose.
