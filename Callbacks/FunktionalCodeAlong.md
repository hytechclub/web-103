# Code-Along: Funktional Functions
In this code-along, add some funktionality to buttons on a website using callbacks.

## Setting Up
[Click here to go to the Funktional Functions Starter project.](https://hytop.onrender.com/e/funktional-functions)

Start by copying the project. Take a look at the current code in the **script.js** file:

- `bassAudio` object and `playBass` function definition - these make it possible to play an audio track!
- `chooseRandom` function definition - this makes it possible to choose a random item from an array, and exclude any item in particular
- Many `document.querySelector` calls - these will all store HTML elements in variables to make them easier to access later in the code

There is a lot of setup, but nothing is actually functional yet. Run the project and notice that none of the buttons actually work!

## Hooking Up the Bass Button
All of the bass-playing functionality is ready to go, but the function is not being called anywhere! Hook it up to the button with `addEventListener`.

1. Open the **index.html** file
1. Notice the "🎸 ⏯" `<button>` element has an `id` of `"play-pause-bass"`
1. Open the **script.js** file for editing
1. Notice the `playPauseBassButton` variable stores the proper HTML button
1. Make a new line at the bottom of the file
1. Call `addEventListener` on the `playPauseBassButton` object
1. Pass in `"click"` as the first argument
1. Pass in `playBass` as the second argument
    - Note: this is the _actual function as a variable_, not a function call!

Run the project again, click the "🎸 ⏯" button, and verify that Bootsy Collins starts playing!

The added line of code should look something like this:

```js
playPauseBassButton.addEventListener("click", playBass);
```

## Defining the Random Background Filter Function
Now the "🎸 ⏯" button is good to go - the next button to hook up is the "Swap Color" button. This one doesn't have a function defined yet, but the function _should_ change the background filter to a random color.

1. Make a new line at the bottom of the **script.js** file
1. There, create a new variable named `randomBgFilter`
1. Set `randomBgFilter` to be a new function
    - `function` keyword
    - Parentheses
    - Curly brackets
1. In the body of the function (between `{` and `}`), make a new line
1. There, set the `backgroundColor` of `backgroundFilterDiv.style` to `"yellow"`

Nothing will change quite yet... the `randomBgFilter` function still needs to be hooked up to the proper button! The new function code should look something like this:

```js
let randomBgFilter = function() {
  backgroundFilterDiv.style.backgroundColor = "yellow";
}
```

## Hooking Up the Swap Color Button
Now a basic version of the function is ready, but it needs to be hooked up.

1. Open the **index.html** file
1. Notice the "Swap Color" `<button>` element has an `id` of `"color-swapper"`
1. Open the **script.js** file for editing
1. Notice the `colorSwapperButton` variable stores the proper HTML button
1. Make a new line at the bottom of the file
1. Call `addEventListener` on the `colorSwapperButton` object
1. Pass in `"click"` as the first argument
1. Pass in `randomBgFilter` as the second argument
    - Note: this is the _actual function as a variable_, not a function call!

Run the project again, click the "Swap Color" button, and verify that the filter changes to yellow!

The added line of code should look something like this:

```js
colorSwapperButton.addEventListener("click", randomBgFilter);
```

## Filling Out the Random Background Filter Function
At this point, the `randomBgFilter` function is doing _something_, but it's not working quite right. Instead of only setting the color to yellow, it should choose a random color from an array.

1. Make a new line at the _top_ of the body of the `randomBgFilter` function
1. There, create a new variable named `currentColor`
1. Set `currentColor` to `backgroundFilterDiv.style.backgroundColor`
    - This is the current filter color so the function can make sure it's a new color this time
1. Under that, create a new variable named `colors`
1. Set `colors` to be an array containing **red**, **orange**, **yellow**, **cyan**, **green**, and **purple**
1. Under that, create a new variable named `randomColor`
1. Set `randomColor` to be a call to `chooseRandom`
    - This function is defined earlier in the **script.js** file
1.  Pass in `colors` as the first argument, and `currentColor` as the second
    - This will choose a random color while avoiding the current color
1. Next, change the `"yellow"` to `randomColor` so it uses the randomly chosen color

Run the project, click the "Swap Color" button a bunch, and verify that there is a new color each time! The body of the `randomFilterBg` function should look something like this:

```js
let currentColor = backgroundFilterDiv.style.backgroundColor;
let colors = ["red", "orange", "yellow", "cyan", "green", "purple"];
let randomColor = chooseRandom(colors, currentColor);
backgroundFilterDiv.style.backgroundColor = randomColor;
```

## Defining the Start Cycle Function and Hooking Up the Button
Now, it's pretty funkalicious that the background color can change. However, it would be even _more_ funkalicious if it could happen automatically! This is possible with `setInterval`, and the `randomBgFilter` function already defined.

1. Make a new line at the bottom of the **script.js** file
1. Define a new function named `startCycle`
    - `function` keyword
    - Function name (`startCycle`)
    - Parentheses
    - Curly brackets
1. In the body of the `startCycle` function (between `{` and `}`), make a new line
1. There, call the `setInterval` function
1. Pass in `randomBgFilter` as the first argument, and `250` as the second
    - This will cause the function to run once every **250ms**
1. Outside the function definition, make a new line
1. Hook up the `startCycleButton` to run the `startCycle` function when clicked
    - Use `startCycleButton.addEventListener`

Run the project, click the "Start Cycle" button, and see the colors cycle automatically!

The code should look something like this:

```js
function startCycle() {
  setInterval(randomBgFilter, 250);
}

startCycleButton.addEventListener("click", startCycle);
```

## Stopping the Cycle: Tracking the Cycle Interval Id
Now the cycle has begun, but there is no way to stop it! That could get annoying. Luckily, there is a way to keep track of any currently running function intervals - the `setInterval` function will _return_ an ID value that can be used to track its usage.

1. Make a new line _above_ the `startCycle` function definition
1. There, define a new variable named `cycleIntervalId` (do not set it to anything)
1. In the body of the `startCycle` function, set `cycleIntervalId` to the value returned from `setInterval`
1. Next, wrap the `setInterval` call in an `if` statement
1. For the `if` condition, check if `cycleIntervalId` is unset using `!cycleIntervalId`
    - This means there is not currently an interval running

This will not change any functionality yet, but it will now be possible to stop the interval. The added code should look something like this: 

```js
let cycleIntervalId;

function startCycle() {
  if (!cycleIntervalId) {
    cycleIntervalId = setInterval(randomBgFilter, 250);
  }
}
```

## Defining the Stop Cycle Function and Hooking Up the Button
All that's left is to define a new function to stop the cycle, and hook it up to the proper button.

1. Make a new line at the bottom of the **script.js** file
1. There, define a new function named `stopCycle`
1. In the body of the `stopCycle` function, call the `clearInterval` function
1. Pass in `cycleIntervalId` to the `clearInterval` call
    - This will stop the `startCycle` function from running
1. Under that, still in the body, set the `cycleIntervalId` to `null`
    - This ensures that a new cycle will be able to start
1. Outside the function definition, make a new line
1. Hook up the `stopCycleButton` to run the `stopCycle` function when clicked
    - Use `stopCycleButton.addEventListener`

Run the project, start the cycle, and make sure the "Stop Cycle" button makes it stop! The code at the bottom should look something like this:

```js
function stopCycle() {
  clearInterval(cycleIntervalId);
  cycleIntervalId = null;
}

stopCycleButton.addEventListener("click", stopCycle);
```

## Conclusion
This code-along showed a small sample of what is possible with event listeners and intervals. Almost anything on a website can be controlled with these tools!

By the end of the activity, the additional code in the **script.js** file should look something like this:

```js
// Hook up Bass Button
playPauseBassButton.addEventListener("click", playBass);

// Define a function to change the background to a random color filter
let randomBgFilter = function() {
  let currentColor = backgroundFilterDiv.style.backgroundColor;
  let colors = ["red", "orange", "yellow", "cyan", "green", "purple"];
  let randomColor = chooseRandom(colors, currentColor);
  backgroundFilterDiv.style.backgroundColor = randomColor;
}

// Hook up the "Swap Color" button to call the function
colorSwapperButton.addEventListener("click", randomBgFilter);

// Prepare Interval ID - this will keep track of the currently running function
let cycleIntervalId;

// Start the cycle if there is not one currently running
function startCycle() {
  if (!cycleIntervalId) {
    cycleIntervalId = setInterval(randomBgFilter, 250);
  }
}

// Hook up Start Cycle Button
startCycleButton.addEventListener("click", startCycle);

// Stop any currently running cycle
function stopCycle() {
  clearInterval(cycleIntervalId);
  cycleIntervalId = null;
}

// Hook up Stop Cycle Button
stopCycleButton.addEventListener("click", stopCycle);
```

## Next Steps
[Click here to view the self-paced work instructions.](SelfPacedWork.md)
