# JavaScript introduction : Text-based Browser games in JavaScript

You had a chance to learn a bit about JavaScript in the last session, and the material is available at http://coderdojosv.github.io/Intro-Web-Series/

We are going to use some of the concepts learned in that session, and add to your knowledge with even more tricks.  Because Khan Academy is an excellent environment for [learning JavaScript](https://www.khanacademy.org/computing/computer-programming), and in particular, for learning some grahpics programming, we will use their environment.  If you prefer another environment (like [Thimble by Mozilla](http://thimble.mozilla.org), [CodePen.io](http://codepen.io) or [JSBin](http://jsbin.com) then feel free to continue using that tonight.

In this lesson, we will make two games that run in a browser.  First up is ["the number guessing game"](https://www.khanacademy.org/computer-programming/number-guessing-game/5054838707191808), and that code will form the basis of ["Hangman"](https://www.khanacademy.org/computer-programming/hangman/5040068583096320)

The goal for this session is for you to learn a little more JavaScript by example, and to apply your knowledge to improve the starter code and/or the appearance of the game.

# Background

By now, you know enough Web Development basics to understand this HTML code:
```html
<h1>Number Guessing Game</h1>    
Type a number between 1 and 100 (then press guess)
<input id="guess" type="text">
<input type="button" value="guess" onClick="guessOne()"/>
<p id="message">&nbsp;</p>
```

The most important thing to observe from this simple HTML is that a call is made out to JavaScript when the player enters their guess.  In this case, the "guessOne()" function will be called.  

Challenges:

1. Change the button to use an ```html<button>``` tag.  
2. If instead, you want a warmup before diving into JavaScript tonight, then just use CSS to change the appearance of the h1 element (maybe to a different font or color)

# JavaScript

In prior lessons, you may have seen the use of alert and prompt.  As you learn more, you will find that alerts and prompts are not the best tool.  Some development environments actively disallow them.  Khan Anademy is one that disallows alerts in JavaScript.  Other development environments may run your JavaScript on every key press, and the alert button can be very annoying.  

From this point on, we will send any output to a web page element we prepared for our use.  In this example, we are going to write everything we need to tell the player into the area with the "message" id.

Before diving into the technical details, there's one more thing.  In Khan Academy's site, there is no easy way to have your html call your own javascript that is in a separate file.  (This differs from Thimble and JsBin.)  So, we will go back to the less clean approach of putting the javascript code right into the html page.  

## Code Snippet 1 -- Declarations
Let's take a look at the first few lines in our JavaScript
```javascript
<script>
var guessCount = 0;
var MAX_GUESSES=6;
var randomNumber = Math.floor((Math.random() * 100) + 1); //picks a random number between 1 and 100

function guessOne(){
```
The most important thing to observe is that we declared that we have a function called *guessOne*, which is the code that gets called when the guess button is pressed.  We'll talk about that code in a minute.  First, lets talk about variables.

Remember that code is written to tell the computer what to do AND to tell programmers what you think needs to be done. Using good variable names helps.  Placing the variables in the right place helps.  
These variables need to be kept alive between runs of the code, so they are not in the guessOne function.  This means they are global variables.  You should use as few global variables as possible, and professional developers have ways of not using global variables at all.

What are the variables we declared?

1. I declared a variable called guessCount.  I'm using a style called CamelCase for ordinary variable names.
2. I declared MAX_GUESSES.  I used ALL_UPPERCASE because I want to hint that this is has a constant value, meaning it never changes.  (Also, programmers use _ to separate words because you cannot use - in variable names.) 
3. I declared randomNumber and used a little bit of math to get the random number.  

Activity: 

1. Change the range for guesses, say from 1 to 1000.  TELL THE PLAYER WHAT THE RANGE IS!!!!!!
2. Ask someone at your table to try the game with your new range.

Challenges

1. Use javascript addEventListener to make the call to guessOne() happen.  If you try tonight's Super Challenge, you will need to do this.  Do a web search for "javascript button addeventlistener onclick"  Remove the "onClick" from the html.
2. Change the maximum number of guesses.  What is the lowest number that allows a player making perfect guesses to win for every possible number.  Hint: if the range was 1 to 32, the answer is 5.
3. Use constants to set the range and to give a better message to the player.  (For example, "Your guess is lower than the correct number, but is in range." or "Your guess is higher than the maximum number the answer might be")



## Code Snippet 2 -- The guessOne() function, part 1

Here is the first half of the guessOne() function
```javascript
function guessOne(){
  // Get a guess from the player
  var guess = document.getElementById("guess").value;

  if (guess == randomNumber){
    document.getElementById("message").innerHTML= "It took you " +guessCount+ " guesses";
    return;  // prevents saying 'ran out' if guessed in last round
  } else if (guess < randomNumber){
    document.getElementById("message").innerHTML= "Guess again. The number is higher than "+guess;
  } else {
    document.getElementById("message").innerHTML= "Guess again. The number is lower than "+guess;
  }
  guessCount += 1;
```

Notice that JavaScript pulls the player's guess out of the "guess" field and puts it into the variable named "guess".  This variable is declared inside the guessOne function and will disappear when the guessOne function completes.  

Next, notice the "control logic".  There is an if, an else-if, and a final else (which you can think of as the word "otherwise" if that helps.) 

Challenges:

1. This code isn't rugged.  The Player can type in anything.  If the player typed in "zombie", the code would show "the number is lower than zombie"  !!   Use Javascript's parseInt function with parenthesis around ```javascript document.getElementById("guess").value``` to turn it into a number.  (We were lucky javascript's comparison worked when comparing a string to a number.)
2. Use another else if to test if the number is > randomNumber and use the final else to say "I didn't recognize that".  I didn't write this yet, but you may need to check if guess == NaN rather than using the catch-all else.   

##  Code Snippet 3 -- The guessOne() function, part 2
Here's the rest of the function so far
```javascript

  if (guessCount >= MAX_GUESSES) {
    document.getElementById("message").innerHTML= "Sorry, you ran out of guesses.  The number was " + randomNumber;
  }
  
  // Lend a hand by clearing out their last guess
  document.getElementById("guess").value = "";  
}    
```

You know what the first section is doing.. It's checking if the player used up the guesses.  But it is not stopping the game!  Hmm, maybe you should fix that!

The last line is there to be nice to the player.  It clears out their guess.  Otherwise, they have to backspace out their old answer.

Challenge: 

1. Fix the game to stop allowing guesses after the player exceeds the MAX_GUESSES.  Write the code that would end the game.  Tip: you could hide the input field and the guess button.  Do you know which css property affects visibility? 
2. Improve the game so that the player can start a new game.  Suggestion: create a new function called "startGame" and have startGame set all the global variables.  After you tell the player that they won or lost, either show a "new game" button (easier) or chane the guess button and temporarily change the button handler.  Another game suggestion: keep running counts of wins and losses.  

Take a moment and have someone else at your table play the game that you wrote.  If they find any bugs, then take a moment to fix them.

Super Challenge

Instead of having a "guess" button, you could create a listener on the guess html text input box.  That listener should be assigned to keyboard events and look as each key is pressed.  If it's a number, it's good.  If it's enter, it should call guessOne.  Otherwise, it should reject what the player typed.  Congratulations, Your game is now zombie-proof!!



## The [Hangman](https://www.khanacademy.org/computer-programming/hangman/5040068583096320) game

The code so far creates a decent structure fo the game "Hangman".  Let's revisit the HTML and put in a few more elements.
```html
<h1>Hangman!</h1>
Type a letter (then press guess)
<input id="guess" type="text">
<input type="button" value="guess" onClick="guessOne()"/>
<input type="button" value="quit" onClick="quit()"/>
<p id="message">&nbsp;</p>
<p>
<font size="+3"><span id="answer">puzzle loading..</span></font>
</p>
```

The most important thing to observe is a new element called "answer"  We will use this to keep the current state of the puzzle.

Challenges:

1.  The "obviously missing" feature in the game you see is the hangman himself.  Prepare for that by adding an HTML element where you will load an image representing the number missed.  Maybe you will want ```html<img id="hangman">```
2.  Similarly, it is missing an area where you can show the letters that were already guessed.  

## Code Snippet 1 -- Declarations
Let's take a look at the first few lines in our JavaScript
```javascript
<script>
// declare three global variables

// Create an array of words-- randomly choose one on init
var WORDS = [
	"javascript",
	"hangman",
	"coderdojo",
	"games"
];

// word stores the word we want the player to guess
var word="";
// answerArray stores the answer board (starting with all _ and gradually filled in)
var answerArray = [];
```

The number game calculated a random number,  This game fetches a random word from the WORDS array.  (Use ALL_UPPERCASE to show this never changes for the life of the game)

Activity

1. Change the WORDs array to have a few different words.  Ask someone at your table to try the game with your words

Challenges-- future improvements to the game

1.  Keep an array of letters guessed by the player, so they don't keep guessing the wrong letter again.
2.  The huge "obviously missing" item is the hang man himself.  Prepare for that by adding an HTML element where you will load an image representing the number missed.

##  Code Snippet 2 -- Game initialization

The initialization of the game is moved to a function called init.  Don't forget to call it!

```javascript
function init(){
	// Pick a random word
	word = WORDS[Math.floor(Math.random() * WORDS.length)];
	// Set up the answer array
	answerArray = [];
	for (var i = 0; i < word.length; i++) {
	  answerArray[i] = "_";
	}
  document.getElementById("answer").innerHTML= answerArray.join(" ");
	document.getElementById("message").innerHTML= "Type a letter then press guess, or press quit to stop playing."
}
init();
```


##  Code Snippet 3 -- The game loop

So, this is a lot like the number guessing game, except we are guessing letters.  

The two big changes here are that we are manipllating the "correct answer" array as the player gets letters correct, and that we are temporarily storing a message to display to the player after we've processed everythign that could happen. 

Here's that code
```javascript
function guessOne() {
	// Get a guess from the player
	var guess = document.getElementById("guess").value;
	var showThisMessage = "";
	
  if (guess.length !== 1) {
		showThisMessage ="Please enter only a single letter";
	} else {
		// Update the game with the guess
		var i=0; // an indexer into the array 
		for (var i = 0; i < word.length; i++) {
			if (word[i] === guess) {
				answerArray[i] = guess;
				showThisMessage = "YES! "+guess+" is in the answer";
			}
		}
		var remaining_letters = 0;
		// recount the remaining letters
		for (i = 0; i < word.length; i++) {
			if (word[i] === '_') {
			    remaining_letters += 1;
			}
		}
		if (remainingLetters == 0) {
			showThisMessage = "YES! You guessed the word";
		}

		if (showThisMessage === "") {
			showThisMessage = "Sorry, no "+guess;
		}
		
		// Update the puzzle
		document.getElementById("answer").innerHTML = answerArray.join(" ");
		
		// Lend a hand by clearing out their last guess
		document.getElementById("guess").value = "";
	}
	document.getElementById("message").innerHTML = showThisMessage;
}

```

There are quite a few other tricks here.  

1. JavaScript behaves like all other computer languages when testing numbers, but it is a little strange when testing string values.  (Strings are one of the types of Javascript Objects.)    Fortunately, it introduced string compare operators that act like you would expect, and they use one more = character.  So, use === when testing strings (or anything other than numbers) for equality.  (Any object should be compared using === or !== unless you really know what you are doing.  And the JavaScript guru Douglas Crockford says if you know what you are doing, you will always use === and !==)  
2. This code uses quite a stunt for showing the answer string.  The call ``javascript answerArray.join(" ");``` will take all the members (the letters) of the answerArray and blast them into a string.  If we supply join with a function parameter of the space character, it will put spaces between each letter.  Magically, we can get that we want with little effort.   


Challenges:

1.  Many of the challenges from the number game are valid for this game, including
..restarting the game
..dealing with user errors, like asking for the same letter twice
..using a listener instead of a guess button
..dealing with edge case bugs, like if the word has a space character
2.  Enhancing the game with a hangman graphic 
3.  Ending the game if the player is out of guesses (if the hangman was hung!) 
