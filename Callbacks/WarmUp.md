# Warm-Up: Function Machine
In JavaScript, [functions](https://javascript.info/function-basics) are a way to run a piece of code on-demand. Parameters are used as function input, and returns are used to give back an output. In math, the concept of functions is similar - often, math functions take some sort of input, and produce an output. In this warm-up, play a math-inspired function game to practice using input and output.

## Function Game
[Click here to play the Function game.](https://embed.mangahigh.com/bubblefunction?locale=en-us&guestMode=false)

The goal is to use the proper function to match the input bubbles to the bubbles on the field already. Good luck!

## BONUS: Hack the Game
As it is, the game is setup to automatically stop working after three minutes. If this happens, you'll lose all your progress! Luckily, there is a way to hack it so that you can keep playing indefinitely 🐱‍💻😎

The hacking code looks like this:

```js
Play.showLoggedOutMessage = () => { console.log("HEY!") };
```

Here's what you should do:

1. Reload the page
1. Open the JavaScript console (in Chrome with `Ctrl`+`Shift`+`J`)
1. Copy the code from above into the prompt, and press `Enter`
1. Continue playing the game
1. When `HEY!` is logged, that means you're past the timebox!

Essentially, what this code does is overrides the `showLoggedOutMessage` function so that, instead of ending the game and showing the "Please give us money" screen, it simply logs a message in the console. Just make sure to use your hacking powers for good, please 😇
