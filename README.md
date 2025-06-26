#   Learning JavaScript by making a PASSENGER COUNTER APP

Initial HTML setup -
``` html
<html>
    <head>
        <link rel="stylesheet" href="index.css">
    </head>
    <body>
        <h1>People entered:</h1>
        <h2 id="count-el">0</h2>
        <button id="increment-btn" onclick="increment()">INCREMENT</button>
        <!-- 2. Create a SAVE button.
        Set the id to "save-btn" and call the save() function when it's clicked -->
        <button id="save-btn" onclick="save()">SAVE</button>
        <p id="save-el">Previous entires: </p>
        <script src="index.js"></script>
    </body>
</html>
```
> Note: `<script scr="index.js"></script>` tag is used to link the JavaScript file to the HTML file.

Initial CSS setup -
``` css
body {
    background-image: url("../Images/station.jpg");
    background-size: cover;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    font-weight: bold;
    text-align: center;
}

h1 {
    margin-top: 10px;
    margin-bottom: 10px;
}

h2 {
    font-size: 50px;
    margin-top: 0;
    margin-bottom: 20px;
}

button {
    border: none;
    padding-top: 10px;
    padding-bottom: 10px;
    color: white;
    font-weight: bold;
    width: 200px;
    margin-bottom: 5px;
    border-radius: 5px;
}

#increment-btn {
    background: darkred;
}

#save-btn {
    background: darkgreen;
}
```

## Creating JavaScript variables -
We use the `let` keyword to create variables. EG. `let count = 0;`.
Also, JavaScript executes the code from top to bottom, so you can't do, say `console.log(count);` before initializing it.
> Note: `console.log(count);` is a way to print on the `console` in the browser.

### Small Challenge with variable -
``` js
// This code calculates your age in dog years.
let myAge = 21;
let humanDogRatio = 7;
let myDogAge = myAge * humanDogRatio;
console.log(myDogAge);
```

> Note: With `let`, we can reassign the value of the variable. EG. `myAge = 30;`.

Also, we can increase/decrease the value of the variable by `let count = 20; count = count + 40;` or `count += 40;`.

## Next Steps -
Pseudocode of what we need to do -
``` js
// initialize the count as 0
// listen for clicks on the increment button 
// increment the count variable when the button is clicked
// change the count-el in the HTML to reflect the count.
```
Now, we know how to  initialize the count as 0, that is, by `let count=0;`, we also know how to increment the count variable as we saw above, that is, by `count+=1;`. Now, we need to listen for the clicks on our Increment button.
For that, there are a multitude of ways, simplest of them is definiing an `on-click` event listener in the HTML, by writing something like this - `<button id="increment-btn" onclick="increment()"></button>`.
> Note that here, `onclick` is an attribute and `increment()` is a JavaScript function given as the value of this attribute.

Let's write the `increment()` function in JavaScript -
``` js
function increment() {
    // body of the function
    console.log("The increment button is clicked !");
}
```

### Understanding JavaScript functions -
Functions are like commands we want to use again and again.
To invoke or call the function, `nameOfTheFunction()`. Syntax -
``` js
function print42() {
    console.log(42);
};
```
Example - Simple function that logs the total lap time for the race.
``` javascript
let lap1 = 34
let lap2 = 35
let lap3 = 36
function totalLapTime() {
    console.log(lap1 + lap2 + lap3);
}

totalLapTime()
```

> [!NOTE]
> Note that here, we have accessed the global variables `lap1/2/3` inside the function, but this doesn't work the other way around. Hence we call the `let` variables block-scope.

Now, let's add the functionality to increment the count variable when the button is clicked.
``` js
function increment() {
    count += 1;
    console.log(count)
}
```
Now, let's change the `count-el` to reflect the new count.
First, let's remember how we can change the text of an HTML element - `document.getElementById("count-el").textContent = "New text";`.
Now, let's modify our JS code -
``` js
// camelCase convention for variable names
let countEl = document.getElementById("count-el") // gets us the hold of this <h2 id="count-el"> element
let count = 0;
function increment() {
    count += 1
    countEl.innerText = count
    console.log(countEl)
}
```

Here, what we can see is `objectName.methodName(arguments)`, a basis JS syntax.

#### The DOM(Document Object Model) -
It's Basically how you use JS to modify the website. *Document* means we are working with the HTML document. *Object* means that in JS, the document keyword is of the data-type OBJECT. *Model* means a representation or a modulation, here DOM is just the MODEL of the HTML document, just like we have a lego model of a real spaceship.

### Now, let's create a save button and a save function.
`<button id="save-btn" onclick="save()">SAVE</button>`  in HTML,
``` js
function save() {
    console.log(count)
}
```
in JS.

Now, let's add the functionality for saving the entries. Before that, let's learn about *Strings* in JS -
## Strings in JS 👍
Strings are sequences of characters. They are enclosed in single quotes or double quotes. Syntax - `let str = "Hello, World!";`.
We can concatenate the two strings, simply using the `+` operator - `let str = "Hello, " + "World!";

### String v/s Numbers 🧑‍🚒
`42 + " Hello"` would actually result in `42 Hello`, that is, `42` which is a number gets turned into a string and then gets added to the string `" Hello"`. You can say *string* always wins in such cases.

#### Escape character `\` in JS -
Example - If you want to write the `let wish = "I'd love to see the show "The Lion King"."`, JS would throw an error as for it, string starts at `"I` and ends with `"The`, which we definitely don't want. So, let's add escape character `\` before the problematic `"`, so now the string beecomes - `"I'd love to see the show \"The Lion King\"."`. Escape character `\` tells the JS that the next character should not be seen as a string delimiter. 


> [!NOTE] +=
> We can use += like this as well - `welcomeEl.innerText += "👋"`.
> Also, note that `el` we are using again and again means `element`.

## Let's create a save feature -
Create a paragraph tag - `<p id="save-el">Previous entires: </p>`
Now the JS save function which gets triggered by the save button -
``` js
let saveEl = document.getElementById("save-el")
function save() {
    let countStr = count + " - "
    saveEl.innerText += countStr
}
```
But, here is one issue, even though we are giving `+ " - "`, but it still doesn't preserve the spaces and prints something like 7 -8 -9 -13 instead of the intended 7 - 8 - 9 - 13. Hence, we should use `textContent` instead of the `innerText`.

Major Differences -
| Feature            | `innerText`                            | `textContent`                               |
| ------------------ | -------------------------------------- | ------------------------------------------- |
| Affects layout     | Yes (respects CSS like `display:none`) | No (reads all text)                         |
| Preserves spacing? | No (collapses whitespace)              | Yes (better for preserving spacing)         |
| Performance        | Slower (forces layout reflow)          | Faster (no layout processing)               |
| Use case           | When you want **visible** text         | When you want **raw** text exactly as added |

So, let's change `innerText` with `textContent` as it's computationally more efficient and preserves the spacing as well -
``` js
let saveEl = document.getElementById("save-el")
let countEl = document.getElementById("count-el")
let count = 0

function increment() {
    count += 1
    countEl.textContent = count
}

function save() {
    let countStr = count + " - "
    saveEl.textContent += countStr
}
```
We also need to update the count to 0 when we click the save button and also, change the text of the `count-el` to 0 -

SO, the final JS code is -
``` js
let count = 0
let saveEl = document.getElementById("save-el")
let countEl = document.getElementById("count-el")

function increment() {
    count += 1
    countEl.textContent = count
}

function save() {
    let countStr = count + " - "
    saveEl.textContenttStr
    countEl.textContent = 0
    count = 0
}

console.log("Let's count people on the subway!")
```
RECAP of what we have learnt -
- Add `<script src="index.js"></script>` in our body tag, at the very end.
- JS variables, `let` keyword, setting them to numbers creates the number data type variables.
- JS Strings.
- console.log() as the developer tool.
- JS functions.
- onclick = "" event listener, as the attribute of the html tags.
- The DOM (how to use JS to change the website).
- getElementById("id-name").
- innerText v/s textContent.