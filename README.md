# JavaScript introduction : Browser games (text)

You had a chance to learn a bit about JavaScript in the last session, and the material is still available at http://coderdojosv.github.io/Intro-Web-Series/

We are going to use some of the concepts learned in that session, and add to your knowledge with even more tricks that we can do.  Because Khan Academy is an excellent environemnt for [learning JavaScript](https://www.khanacademy.org/computing/computer-programming), we will use their environment.  Using Khan Academy will be necessary when we cover graphics programming in JavaScript, but for this lesson, if you prefer another environment (like http://thimble.mozilla.org or http://jsbin.com) then feel free ton continue using that.

In this lesson, we will make two games.  First up is ["the number guessing game"](https://www.khanacademy.org/computer-programming/number-guessing-game/5054838707191808), and that code will form the basis of ["hangman"](https://www.khanacademy.org/computer-programming/hangman/5040068583096320)

# Background

By now, you know enough Web Development basics to understand this HTML code:
```html
<h1>Number Guessing Game</h1>    
Type a number (then press guess)
<input id="guess" type="text">
<input type="button" value="guess" onClick="guessOne()"/>
<p id="message">&nbsp;</p>
```

The most important thing to observe from this simple HTML is that a call is made out to JavaScript when the player enters their guess.  In this case, the "guessOne()" function will be called.  

Challenges:
1. Change the button to use an ```html<button>``` tag
2. Use ```javascript addEventListener``` to make the call to GuessOne happen.  The best approach would be to listen to the form and have it make a guess if the player presses Enter/Return.


# JavaScript

In prior lessons, you may have seen the use of alert and prompt.  It is increasingly poor practice to use those.  Some development environments actively break them.  (Khan Anademy is one).  Other development environments may run your JavaScript on every key press, and the alert button can be very annoying.

From this point on, we will send any output to a web page element prepared for our use.  In this example, we are going to write everything we need to tell the player into the "message" area.

Before diving into the technical details, there's one more thing.  In Khan Academy's site, there is no easy way to have your html call your own javascript that is in a separate file.  (This differs from Thimble and JsBin.)  So, we will go back to the less professional approach of putting the javascript code right into the html page.  

Let's take a look at the first few lines in our Javascript
```javascript
<script>
var guessCount = 0;
var MAX_GUESSES=6;
var randomNumber = Math.floor((Math.random() * 100) + 1); //picks a random number between 1 and 100

function guessOne(){
  // Get a guess from the player
  var guess = document.getElementById("guess").value;
```

The first thing to observe is that we defined the guessOne function, which is the code that gets called when the guess button is pressed.

Also, notice that javascript pulls the player's guess out of the "guess" field and puts it into the variable named "guess".  This variable is declared inside the guessOne function and will disappear when the guessOne function completes.

Notice that there are a few other variables that are before the function.  These variables need to be kept alive between runs of the code.  Remember that code is written to tell the computer what to do AND to tell another programmer what you think needs to be done.  Using good variable names helps.  We declared a variable called guessCount.  

Challenges
1. Change the range for guesses, say from 1 to 1000.
2. Write the code that would stop the game if the player exceeds the MAX_GUESSES. Tip: you could hide the input field and the button.
