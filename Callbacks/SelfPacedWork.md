# Self-Paced Work: Funktional Functions Updates
Follow these instructions to update the Funktional Functions website.

## New Cycle Speed
Currently, when the color cycle is running, it changes colors once every **250** milliseconds. Update this to make it a little less hectic - try 500 milliseconds instead.

## New Colors
Currently, there are only six colors for the filter. Add a few more colors to randomly cycle.

>Note: to make the filter stronger or weaker, check the `.filter` ruleset in the **style.css** file, and update the `opacity` value.

## Play/Pause Button
Currently, the button text for the "🎸 ⏯" button is always the same. However, to make it more dynamic, update the code so that it changes the button text based on whether or not the music is playing. If the music is playing, it should display ⏸. If the music is not playing, it should display ▶.

1. Open the **script.js** file for editing
1. Find the `playBass` function
1. In the body of the `if`, under `bassAudio.play()`, make a new line
1. There, set `playPauseBassButton.textContent` to `"🎸 ⏸"`
1. In the body of the `else`, under `bassAudio.pause()`, make a new line
1. There, set `playPauseBassButton.textContent` to `"🎸 ▶"`

Run the program, click the button, and make sure the play and pause symbols show up appropriately!

## Display Current Filter Color
As of now, the filter color changes, but a visitor to the site might not know what the current color actually is. Add a piece of code to display the current color of the background filter.

### HTML: A New Paragraph
Start by adding a new `<p>` element in the HTML.

1. Open the **index.html** file for editing
1. Make a new line under the `<h1></h1>`
1. There, add a new `<p></p>` element
1. Set the `id` of the `<p>` to be `"filter-color"`

### JS: Setting the Paragraph Text
Next, update the `<p>` element text every time the filter color changes.

1. Open the **script.js** file for editing
1. Make a new line under the `backgroundFilterDiv` variable initialization
1. There, create a new variable named `filterColorParagraph`
1. Set `filterColorParagraph` to a call to `document.querySelector`
1. Pass in `"#filter-color"` to store the proper `<p>` element in the variable
1. Make a new line at the bottom of the `randomBgFilter` function
1. There, set `filterColorParagraph.textContent` to be `randomColor`

Run the program, start the cycle, and verify that the current filter color appears on the page!

## Easter Egg: Header Click
Add a secret way to change the background image - when a site visitor clicks the "FUNKTIONAL FUNCTIONS" header, a new picture should appear!

1. Open the **script.js** file for editing
1. Make a new line at the bottom of the file
1. There, Define a new function named `slyBackground`
    - `function` keyword
    - Function name (`slyBackground`)
    - Parentheses (`()`)
    - Curly brackets (`{}`)
1. Make a new line in the body of the function (between `{` and `}`)
1. There, set `document.body.style.backgroundImage` to `"url('assets/sly.jpg')"`
    - This will change the background image of the page
1. Make a new line _under_ the function definition (after `}`)
1. There, create a new variable named `header`
1. Set `header` to select the `"h1"` using `document.querySelector`
1. Under that, call `header.addEventListener`
1. Pass in `"click"` and `slyBackground` to the `addEventListener` call

Run the program, click the header, and verify that the background changes!

### Header Click Music
In addition to changing the background image, start playing a different piece of music when the header is clicked.

1. Make a new line above the `slyBackground` function definition
1. There, create a new variable named `danceToTheMusic`
    - Set `danceToTheMusic` to be a `new Audio` object
    - Set the audio file to be `"assets/dancetothemusic.mp3"`
1. Make a new line in the _body_ of the `slyBackground` function
1. There, reate an `if`/`else` structure
    - `if` keyword
    - Parentheses (`()`)
    - Curly brackets (`{}`)
    - `else` keyword
    - Curly brackets (`{}`)
1. For the `if` condition, check if `danceToTheMusic.paused`
1. In the body of the `if`, call the `danceToTheMusic.play` function
1. In the body of the `else`, call the `danceToTheMusic.pause` function

Run the program, click the header again, and verify that the new music can start and stop playing!

## Next Steps
[Click here for some additional challenges.](Challenges.md)
