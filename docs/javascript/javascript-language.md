# JavaScript Language

JavaScript is the language that powers the interactive web! We use JavaScript as the primary language in these courses at CodeWizardsHQ:

| Elementary                           | Middle School          | High School                     |
| ------------------------------------ | ---------------------- | ------------------------------- |
| Interactive Websites with JavaScript | Interactive JavaScript | Fundamentals of Web Development |
| Capstone 3                           | Web Interfaces         | User Interface Development      |
|                                      | Capstone 2             | Capstone 1                      |
|                                      | Mastering APIs         | APIs and Databases              |
|                                      | Capstone 3             | Capstone 2                      |
|                                      |                        | DevOps and Software Engineering |
|                                      |                        | Capstone 3                      |

In this section of our documentation, you'll find references to most of the core JavaScript language features that we use in our CodeWizardsHQ courses.

You'll also find many _Further reading_ sections, which pull from these excellent JavaScript resources:

-   [MDN JavaScript Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
-   [The Modern JavaScript Tutorial](https://javascript.info/)
-   [Eloquent JavaScript](https://eloquentjavascript.net/)

<hr>

## Comments

Programmers use comments to make notes in their source code for themselves or other programmers that will read their code later. They can also be used to "deactivate" lines of code that you don't want to run while you're working on a program.

### Single Line Comments

Single line comments are denoted by the `//` characters. You can put them above or to the right of the line of code they reference:

```javascript
// Validate the user is logged in and redirect them to the appropriate page.
if (isLoggedIn(user)) {
    redirectToHomepage();
} else {
    redirectToLogin();
}

var minHeight = 60; // This is measured in inches, not feet!
```

### Deactivating Code

You can deactivate sections of code with comments:

```javascript
if (age < 18) {
    // Turning this off for now
    // prompt_user();
    redirectToKidZone();
} else {
    loginUser();
}
```

### Multiline Comments

Multiline comments start with `/*` and end with `*/`

```javascript
/*
This calculates the hypotenuse of a right triangle when given the sides
of the right triangle. It's the Pythagorean Theorem. The ** is how you
write exponents in JavaScript, and fractional exponents are like roots,
so 0.5 is the square root.
*/
var hypotenuse = (sideA ** 2 + sideB ** 2) ** 0.5;
```

Many programmers prefer to put `*` on each line of a multiline comment and indent a bit for clarity:

```javascript
/*
 *   This calculates the hypotenuse of a right triangle when given the sides
 *   of the right triangle. It's the Pythagorean Theorem. The ** is how you
 *   write exponents in JavaScript, and fractional exponents are like roots,
 *   so 0.5 is the square root.
 */
var hypotenuse = (sideA ** 2 + sideB ** 2) ** 0.5;
```

_Further Reading_

-   [MDN - JavaScript Basics: Comments](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics#comments)
-   [Eloquent JavaScript - Comments](https://eloquentjavascript.net/02_program_structure.html#h_/OBuIOX390)
-   [The Modern JavaScript Tutorial - Comments](https://javascript.info/comments)

<hr>

## Conditional Statements

Conditional statements allow you to run a block of code when a boolean condition is true.

### `if`

The `if` statement is the simplest form of conditional statement. If the expression to the right of the `if` keyword is `true`, the code block will execute:

```javascript
var isHungry = true;

if (isHungry) {
    console.log("You should eat!");
}
```

Example Output:

```text
You should eat!
```

Usually, a conditional expression uses [comparison operators](#comparison-operators) to generate a `boolean` result:

```javascript
var age = 19;

if (age >= 18) {
    console.log("You are legally an adult, congrats!");
}
```

Example Output:

```text
You are legally an adult, congrats!
```

### `else if`

The `else if` conditional statement is used to group _logically related_ conditional statements together. The first conditional expression that evaluates to `true` will run:

```javascript
var favoriteFood = "Tacos";

if (favoriteFood == "Sushi") {
    console.log("We're going out for Japanese food to night!");
} else if (favoriteFood == "Pasta") {
    console.log("How about we eat some Italian food tonight?");
} else if (favoriteFood == "Tacos") {
    console.log("Time for some Mexican food!");
} else if (favoriteFood == "Samosa") {
    console.log("Let's eat Indian food tonight!");
}
```

Example Output:

```text
Time for some Mexican food!
```

### `else`

The `else` conditional statement runs when all other conditional statements in a group are `false`. You can think of it as the _default_ option:

```javascript
var favoriteFood = "Hot Dogs with Cream Cheese";

if (favoriteFood == "Sushi") {
    console.log("We're going out for Japanese food to night!");
} else if (favoriteFood == "Pasta") {
    console.log("How about we eat some Italian food tonight?");
} else if (favoriteFood == "Tacos") {
    console.log("Time for some Mexican food!");
} else if (favoriteFood == "Samosa") {
    console.log("Let's eat Indian food tonight!");
} else {
    console.log("I don't know what that favorite food is!");
}
```

```text
I don't know what that favorite food is!
```

### `Comparison Operators`

Here are the comparison operators that you can use in conditional expressions to generate a `boolean` value:

| Operator | Description              |
| -------- | ------------------------ |
| `>`      | Greater-than             |
| `>=`     | Greater-than or equal-to |
| `<`      | Less-than                |
| `<=`     | Less-than or equal-to    |
| `==`     | Equal-to                 |
| `!=`     | Not equal-to             |

### `Complex Conditional Statements`

Complex conditional statements involve combining more than one conditional expression with [logical operators](#logical-operators):

```javascript
var age = 15;
var heightInFeet = 4.6;

if (age >= 13 && heightInFeet > 5) {
    console.log("You may ride the roller coaster.");
} else {
    console.log("You may NOT ride the roller coaster.");
}
```

Example Output:

```text
You may NOT ride the roller coaster.
```

You can string as many logical operators together as you want to build more complex conditional statements. Note that it's often easier to read and reason about if you surround each major section with parentheses, as in the example below:

```javascript
var isHungry = false;
var isThirsty = true;

var foodAmount = 10;
var drinkAmount = 0;

if ((isHungry && foodAmount > 0) || (isThirsty && drinkAmount > 0)) {
    enterKitchen();
} else {
    playVideoGames();
}
```

### `Logical Operators`

Logical operators allow you to combine multiple conditional expressions in a single conditional statement:

<!-- prettier-ignore -->
| Operator   | Description                                         |
|------------|-----------------------------------------------------|
| `&&` (and) | `true` when both conditional expressions are `true` |
| `||` (or)  | `true` when either conditional expression is `true` |
| `!` (not)  | Reverses the value of a conditional expression      |

#### Using the `&&` operator

The `&&` (and) operator evaluates to `true` when both conditional expressions are `true`:

```javascript
var age = 15;
var heightInFeet = 5.2;

if (age >= 13 && heightInFeet > 5) {
    console.log("You may ride the roller coaster.");
} else {
    console.log("You may NOT ride the roller coaster.");
}
```

Example Output:

```text
You may ride the roller coaster.
```

#### Using the `||` operator

The `||` (or) operator evaluates to `true` when either conditional expression is `true`:

```javascript
var isHungry = true;
var isThirsty = false;

if (isHungry || isThirsty) {
    console.log("You should go to the kitchen.");
} else {
    console.log("Do whatever, you're good!");
}
```

Example Output:

```text
You should go to the kitchen.
```

#### Using the `!` operator

The `!` (not) operator reverses a conditional expression:

```javascript
var isTired = true;

if (!isTired) {
    console.log("Let's go outside and play.");
} else {
    console.log("Let's take a nap.");
}
```

Example Output:

```text
Let's take a nap.
```

### Nested Conditional Statements

Conditional statements can be nested inside other conditional statements. Use indentation to make the nesting obvious at a glance:

```javascript
var role = "admin";

if (role == "admin" || role == "developer") {
    console.log("You can see the secret stuff in this app.");
    if (role == "admin") {
        console.log("You can also see the SUPER secret stuff in this app.");
    }
}
```

Example Output:

```text
You can see the secret stuff in this app.
You can also see the SUPER secret stuff in this app.
```

_Further Reading_

-   [MDN - JavaScript Building Blocks: Conditionals](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/conditionals)
-   [Eloquent JavaScript - Conditional Execution](https://eloquentjavascript.net/02_program_structure.html#h_wpz5oi2dy7)
-   [The Modern JavaScript Tutorial - Conditional Branching](https://javascript.info/ifelse)

<hr>

## Data Types

Every value has a data type in JavaScript. The data type determines what kinds of operations you can perform on the value.

### `boolean`

The `boolean` data type represents a `true` or a `false` value:

```javascript
var isHungry = true;
var isThirsty = false;
```

#### Generating `boolean` values in a conditional statement

You normally won't use a `boolean` directly, but instead will generate a `boolean` in a conditional statement:

```javascript
var age = 19;

// This generates `true`
if (age >= 18) {
    console.log("You are an adult!");
}

// This generates `false`
if (age < 18) {
    console.log("You are a child.");
}
```

#### Truthy and falsy values

Booleans are not the only values that can be True/False. Every value in JavaScript is either _truthy_ or _falsy_, which means they can be used in conditional statements without a boolean comparison operation. Empty strings and the number 0 are _falsy_, and all other strings and numbers are _truthy_.

Here's an example of a _falsy_ value:

```javascript
var username = "";

if (username) {
    console.log(`Hello, ${username}!`);
} else {
    console.log("The username is blank");
}
```

Example Output:

```text
The username is blank
```

Here's an example of a _truthy_ value:

```javascript
var numBananas = 2;

if (numBananas) {
    console.log("We have bananas!");
} else {
    console.log("We have no bananas!");
}
```

Example Output:

```text
We have bananas!
```

### `number`

The `number` data type represents any number:

```javascript
var totalCost = 29.99;
var numBananas = 2;
```

#### Converting `string` to `number`

You can use the `parseInt()` function to convert a `string` to an integer `number`:

```javascript
var age = parseInt("13");
console.log(age); // 13
```

This is often combined with the `prompt()` function when you prompt the user for a numeric data type:

```javascript
var age = parseInt(prompt("How old are you? "));
```

The `parseFloat()` function works the same way, except the `number` will be a decimal number:

```javascript
var heightInInches = parseFloat("60.5");
console.log(heightInInches); // 60.5
```

Instead of `parseInt()` or `parseFloat()`, you can use the `+` operator to convert a `string` to a `number`:

```javascript
var age = +"13";
console.log(age); // 13

var heightInInches = +"60.5";
console.log(heightInInches); // 60.5
```

### `string`

The `string` data type represents a text value:

```javascript
var name = "Daniel";
```

#### String concatenation

If you need to combine a variable and a `string`, you can use the `+` operator. This technique is called **string concatenation**:

```javascript
var name = "Daniel";
var greeting = "Hello, " + name;

console.log(greeting); // Hello, Daniel
```

#### String interpolation

Another way to combine a variable and a `string` is using `template-literal` strings. This technique is called **string interpolation**, and it is the preferred way to combine variables and `strings`. Note that the string must be surrounded by backtick quotes, which are usually near the 1 key on your keyboard:

```javascript
var name = "Daniel";
var age = 35;

console.log(`I'm ${name} and I'm ${age} years old.`);
```

Example Output:

```text
I'm Daniel and I'm 35 years old.
```

#### Multiline strings

Template literal strings allow you to write large blocks of text in a single `console.log()` statement:

```javascript
var menu = `
    Welcome to Dan's Taco Stand!

    Tacos       $2
    Burritos    $5
    Nachos      $3

    Place your order by clicking *Order Now*
`;

console.log(menu);
```

Example Output:

```text

    Welcome to Dan's Taco Stand!

    Tacos       $2
    Burritos    $5
    Nachos      $3

    Place your order by clicking *Order Now*
```

#### Getting the number of characters in a `str`

You can use the `string.length` property to get the number of characters in a `string`:

```javascript
var name = "Daniel";

name.length; // 6
```

#### Checking if a `string` ends with a set of characters

The `string.endsWith()` method lets you check if a `string` ends with a given pattern:

```javascript
var emailAddresses = ["djs@cwhq.com", "alecg@auburn.edu", "samh@bridges.com"];

for (var emailAddress of emailAddresses) {
    if (emailAddress.endsWith(".edu")) {
        console.log(`${emailAddress} is a school address`);
    } else if (emailAddress.endsWith("cwhq.com")) {
        console.log(`${emailAddress} is a CWHQ employee address`);
    } else {
        console.log(`I don't know what ${emailAddress} is for`);
    }
}
```

Example Output:

```text
djs@cwhq.com is a CWHQ employee address
alecg@auburn.edu is a school address
I don't know what sam@bridges.com is for
```

#### Sanitizing user input

User's do strange things, but using `string.toLowerCase()` and `string.trim()` can help your program to validate `string` data types.

`string.toLowerCase()` makes a `string` lowercase:

```javascript
// Imagine a user entered "Pizza" with an uppercase P
var favoriteFood = "Pizza";

if (favoriteFood.toLowerCase() == "pizza") {
    console.log("That's my favorite food!");
}
```

Example Output:

```text
That's my favorite food!
```

`string.trim()` removes leading or trailing whitespace from a `string`:

```javascript
// Imagine a user entered " pizza" with a leading space character
var favoriteFood = " pizza";

if (favoriteFood.trim() == "pizza") {
    console.log("That's my favorite food!");
}
```

Example Output:

```text
That's my favorite food!
```

You can chain these methods together to sanitize a `string` completely:

```javascript
// What a mess! Extra spaces before/after and odd capitalization
var favoriteFood = " PIzZa  ";

if (favoriteFood.trim().toLowerCase() == "pizza") {
    console.log("That's my favorite food!");
}
```

Example Output:

```text
That's my favorite food!
```

_Further Reading_

-   [MDN - JavaScript Data Types and Data Structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
-   [The Modern JavaScript Tutorial - Data Types](https://javascript.info/data-types)
-   [Eloquent JavaScript - Values, Types, and Operators](https://eloquentjavascript.net/01_values.html)
-   [MDN - Truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy)
-   [MDN - Falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
-   [MDN - JavaScript Reference: Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
-   [MDN - JavaScript Reference: String.prototype.trim()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/Trim)
-   [MDN - JavaScript Reference: String.prototype.toLowerCase()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)

<hr>

## Data Structures

Data structures allow you to efficiently store and access groups of items. Think of them like different storage containers you may use around the house.

### `array`

The `array` data structure is used to store data in ordered _slots_. It is known as _mutable sequence type_, which means it can be modified after creation.

Usually, the items in a `array` are homogeneous, which means they represent a group of similar items of the same data type:

```javascript
var names = ["alecg", "danielj", "dimas"];
var menuPrices = [4.5, 5.75, 3.0];
var ids = [184, 294, 832, 98, 4];
```

You can write an `array` on multiple lines if you want. The trailing comma is recommended but not required:

```javascript
var foods = ["tacos", "pizza", "nachos", "ice cream", "asparagus"];
```

#### Accessing items in an `array`

You can access individual items in an `array` using the `[]` characters and the index number of the item. The index numbers start at 0:

```javascript
var names = ["alecg", "danielj", "dimas"];

console.log(names[0]); // alecg
console.log(names[1]); // danielj
console.log(names[2]); // dimas
```

#### Adding an item to an `array`

To add an item to an `array` after it has been created, you can use the `array.push()` method. The `array.push()` method adds the item to the end of the `array`:

```javascript
var names = ["alecg", "danielj", "dimas"];

names.push("samh");

console.log(names); // ['alecg', 'danielj', 'dimas', 'samh'];
```

#### Updating an item in an `array`

To update an `array` item, replace the value at the index:

```javascript
var names = ["alecg", "danielj", "dimas"];

names[1] = "django";

console.log(names); // ['alecg', 'django', 'dimas']
```

#### Removing an item from an `array`

To remove an item from an `array`, you can use the `array.splice()` method. You tell `array.splice` the index number to start removing items from and the number of items to remove:

```javascript
array.splice(indexToRemove, numItemsToRemove);
```

Here's an example that removes the first item from an `array`:

```javascript
var names = ["alecg", "danielj", "dimas"];

names.splice(0, 1);

console.log(names); // ['danielj', 'dimas']
```

If you want to remove an item from the end of an `array`, use the `array.pop()` method:

```javascript
var names = ["alecg", "danielj", "dimas"];

names.pop();

console.log(names); // ['alecg', 'danielj'];
```

#### Looping through an `array`

To loop through the items in an `array`, use a [`for...of`](#for...of) loop. Note the convention of using the plural `names` for the `array` and the singular `name` for the loop-iteration variable:

```javascript
var names = ["alecg", "danielj", "dimas"];

console.log("This documentation is brought to you by:");
for (var name of names) {
    console.log(name);
}
```

Example Output:

```text
This documentation is brought to you by:
alecg
danielj
dimas
```

You can also loop through an array using a traditional [`for`](#for) loop if you need to use the index number of each item for something:

```javascript
var names = ["alecg", "danielj", "dimas"];

console.log("This documentation is brought to you by:");
for (var i = 0; i < names.length; i++) {
    console.log(names[i]);
}
```

Example Output:

```text
This documentation is brought to you by:
alecg
danielj
dimas
```

#### Getting the number of items in an `array`

To get the number of items in an `array`, use the `array.length()` method:

```javascript
var names = ["alecg", "danielj", "dimas"];

var numNames = names.length;

console.log(numNames); // 3
```

#### Checking if an item is contained in an `array`

To check if an item is contained in an `array`, use the `array.includes()` method:

```javascript
var names = ["alecg", "danielj", "dimas"];

console.log(names.includes("alecg")); // True
console.log(names.includes("samh")); // False
```

_Further Reading_

-   [MDN - The JavaScript Reference - Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
-   [Eloquent JavaScript - Data Structures: Objects and Arrays](https://eloquentjavascript.net/04_data.html)
-   [The Modern JavaScript Tutorial - Arrays](https://javascript.info/arrays)
-   [MDN - The JavaScript Reference - Array.push()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
-   [MDN - The JavaScript Reference - Array.pop()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)
-   [MDN - The JavaScript Reference - Array.splice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
-   [MDN - The JavaScript Reference - Array.includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)

### `object`

The `object` data structure is used to store data in key/value pairs.

```javascript
var staff = {
    danielj: "Curriculum Developer",
    alecg: "Curriculum Instructor",
    dimas: "Designer",
};
```

You can use strings for the keys as well, but we'll follow the above form in these docs:

```javascript
var staff = {
    danielj: "Curriculum Developer",
    alecg: "Curriculum Instructor",
    dimas: "Designer",
};
```

#### Accessing items in an `object`

You have to know the key to access an individual item in an `object`:

```javascript
var staff = {
    danielj: "Curriculum Developer",
    alecg: "Curriculum Instructor",
    dimas: "Designer",
};

var danielJob = staff.danielj;
console.log(`Daniel is a ${danielJob}.`);  // Daniel is a Curriculum Developer.

var alecJob = staff.alecg;
console.log(`Alec is a ${alecJob}.`);  // Alec is a Curriculum Instructor.

var dimaJob = staff.dimas.;
console.log(`Dima is a ${dimaJob}.`);  // Dima is a Designer.
```

#### Adding an item to an `object`

You can add an item to an `object` by providing the key/value pair (it's the same syntax as updating an item):

```javascript
var staff = {
    danielj: "Curriculum Developer",
    alecg: "Curriculum Instructor",
    dimas: "Designer",
};

staff.django = "Director Of Pug Snorts";

console.log(staff); // {danielj: 'Curriculum Developer', alecg: 'Curriculum Instructor', dimas: 'Designer', django: 'Director Of Pug Snorts'}
```

#### Updating an item in an `object`

To update an item in an `object`, you must know the key:

```javascript
var staff = {
    danielj: "Curriculum Developer",
    alecg: "Curriculum Instructor",
    dimas: "Designer",
};

staff.danielj = "Burrito Taste-Tester";

console.log(staff); // {danielj: 'Burrito Taste-Tester', alecg: 'Curriculum Instructor', dimas: 'Designer'}
```

#### Removing an item from an `object`

To remove an item from an `object`, use the `delete` operator:

```javascript
var staff = {
    danielj: "Curriculum Developer",
    alecg: "Curriculum Instructor",
    dimas: "Designer",
};

delete staff.danielj;

console.log(staff); // {alecg: 'Curriculum Instructor', dimas: 'Designer'}
```

#### Looping through an `object`

To loop through an `object`, you use the `for...in` loop like this:

```javascript
var staff = {
    danielj: "Curriculum Developer",
    alecg: "Curriculum Instructor",
    dimas: "Designer",
};

for (var key in staff) {
    // Note the [] used to access the value in the object
    console.log(`${key} is a ${staff[key]}.`);
}
```

Example Output:

```text
danielj is a Curriculum Developer.
alecg is a Curriculum Instructor.
dimas is a Designer.
```

#### Getting the keys from an `object`

If you need to get all of the keys from an `object`, use the `object.keys()` method. Note that the keys will be returned as an `array`:

```javascript
var staff = {
    danielj: "Curriculum Developer",
    alecg: "Curriculum Instructor",
    dimas: "Designer",
};

var names = staff.keys();

console.log(`Here are all the names in the staff object: ${names}`);
```

Example Output:

```text
Here are all the names in the staff object: ['danielj', 'alecg', 'dimas']
```

#### Getting the values from an `object`

If you need to get all of the values from an `object`, use the `object.values()` method. Note, the values will be returned as an `array`:

```javascript
var staff = {
    danielj: "Curriculum Developer",
    alecg: "Curriculum Instructor",
    dimas: "Designer",
};

var jobs = staff.values();

console.log(`Here are all the jobs in the staff object: ${jobs}`);
```

Example Output:

```text
Here are all the jobs in the staff object: ['Curriculum Developer', 'Curriculum Instructor', 'Designer']
```

#### Getting the number of items in an `object`

You can get the keys from an `object` and then use the `array.length` method to get the number of items in an `object`:

```javascript
var staff = {
    danielj: "Curriculum Developer",
    alecg: "Curriculum Instructor",
    dimas: "Designer",
};

var numberOfStaff = staff.keys().length;

console.log(`We have ${numberOfStaff} people on our staff.`); // We have 3 people on our staff.
```

_Further Reading_

-   [MDN - The JavaScript Reference - Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
-   [Eloquent JavaScript - Objects and Arrays](https://eloquentjavascript.net/04_data.html)
-   [The Modern JavaScript Tutorial - Objects](https://javascript.info/object)
-   [MDN - The JavaScript Reference - for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)
-   [MDN - The JavaScript Reference - Object.values()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values)
-   [MDN - The JavaScript Reference - Object.keys()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
-   [MDN - The JavaScript Reference - delete operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete)

<hr>

## Functions

Functions allow you to group related statements together to perform a task. They help to implement the **D.R.Y.**(Don't Repeat Yourself) principle because they reduce unnecessary repetition.

### Built-in functions

JavaScript comes with many built-in functions. We'll cover some of the most common that you'll see in CodeWizardsHQ courses below.

##### `parseFloat()`

The `parseFloat()` function converts data to a `number` data type with a decimal point:

```javascript
var pi = parseFloat("3.14");

console.log(pi); // 3.14
typeof pi; // 'number

var two = parseFloat(2);

console.log(two); // 2.0
typeof two; // 'number'
```

##### `prompt()`

The `prompt()` function allows you to prompt a user. The user's response is returned as a `string`, which you can store in a variable:

```javascript
var name = prompt("What is your name? ");
console.log(`Nice to meet you, ${name}!`);
```

Example Output:

```text
What is your name? Daniel
Nice to meet you, Daniel!
```

##### `alert()`

The `alert()` function allows you to alert a user with a message box.

```javascript
function sayHi() {
    alert("Welcome to my page!");
}
sayHi();
```

<figure markdown>
![alert example](https://github.com/codewizardshq/docs/blob/main/docs/assets/browser-apis-and-jquery/alert.gif?raw=true){ width="100%" }
<figcaption></figcaption>
</figure>

##### `confirm()`

The `confirm()` function allows you create a popup message for the user to confirm or cancel. This function returns `true` if the user has click ok.

```javascript
var wizardName = prompt("Enter name");
var nameConfirm = confirm(`Confirm ${wizardName}?`);

if (nameConfirm) {
    document.getElementById("name").innerHTML = `Welcome ${wizardName}!`;
} else {
    document.getElementById("name").innerHTML = `Cancelled`;
}
```

<figure markdown>
![confirm example](https://github.com/codewizardshq/docs/blob/main/docs/assets/browser-apis-and-jquery/confirm.gif?raw=true){ width="100%" }
<figcaption></figcaption>
</figure>

<figure markdown>
![cancelconfirm example](https://github.com/codewizardshq/docs/blob/main/docs/assets/browser-apis-and-jquery/cancelconfirm.gif?raw=true){ width="100%" }
<figcaption></figcaption>
</figure>

##### `parseInt()`

The `parseInt()` function converts data to a `number` data type without a decimal point:

```javascript
var intPI = parseInt(3.14);

console.log(intPI); // 3
typeof intPI; // 'number'

var meaningOfLife = parseInt("42");

console.log(meaningOfLife); // 42
typeof meaningOfLife; // 'number'
```

##### `console.log()`

The `console.log()` function displays text in the developer console:

```javascript
console.log("Hello, world!"); // Hello, world!
```

###### Using special characters with `console.log()`

You can use special characters such as `\n` and `\t` to format the text a bit. The `\n` adds a newline (like hitting **enter** on your keyboard) and the `\t` adds a tab:

```javascript
console.log("Line 1\nLine 2\nLine 3\n");
console.log("\tThis is tabbed over\n\tThis too.");
```

Example Output:

```text
Line 1
Line 2
Line 3

        This is tabbed over
        This too.
```

_Further Reading_

-   [MDN - Web APIs: console.log()](https://developer.mozilla.org/en-US/docs/Web/API/Console/log)
-   [MDN - The JavaScript Reference: parseInt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
-   [MDN - The JavaScript Reference: parseFloat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)
-   [MDN - The JavaScript Reference: window.prompt()](https://developer.mozilla.org/en-US/docs/Web/API/Window/prompt)

### User-defined functions

You define a function using the `function` keyword. Functions definitions can go anywhere in your file, but it helps to keep them all organized in a single area for readability:

```javascript
function sayHello() {
    console.log("Hello!");
}
```

#### Calling a function

Defining a function does not run the statements in the body of the function. To run a function, you _call_ it like this:

```javascript
function sayHello() {
    console.log("Hello!");
}

sayHello(); // Hello!
```

#### Adding parameters to a function

When you define a function, you can add parameters that the function caller should pass in. Parameters are like variables, but the value of the variable is set by the function caller, not the function definer:

```javascript
function sayHello(name) {
    console.log(`Hello, ${name}!`);
}
```

#### Passing arguments to a function

If a function accepts parameters, you need to pass them in when you call the function. The values you pass to the function are called the _arguments_ to the function:

```javascript
function sayHello(name) {
    console.log(`Hello, ${name}!`);
}

sayHello("Daniel"); // Hello, Daniel!
```

#### Returning a value from a function

You can return a value from a function by using the `return` keyword:

```javascript
function add(number1, number2) {
    var total = number1 + number2;
    return total;
}
```

#### Capturing a function's return value

If a function returns a value, you can capture it in a variable:

```javascript
function add(number1, number2) {
    var total = number1 + number2;
    return total;
}

var total = add(2, 3);
console.log(total); // 5
```

You can also use the value immediately in another function, like `console.log()` or as part of a `template-literal` string:

```javascript
function add(number1, number2) {
    var total = number1 + number2;
    return total;
}

console.log(add(2, 3)); // 5
console.log(`2 + 3 = ${add(2, 3)}`); // 2 + 3 = 5
```

#### Indentation in functions

Indentation is not required in JavaScript, but you should do it for readability. If you have another statement inside your function that also requires indentation (like a conditional statement or loop), you should also indent the body of that statement:

```javascript
function sayHello(name) {
    console.log(`Hello, ${name}!`);
    if (name == "Daniel") {
        console.log("That's a cool name!");
    } else {
        console.log("Nice to meet you!");
    }
}

sayHello("Daniel");
sayHello("Alec");
```

Example Output:

```text
Hello, Daniel!
That's a cool name!

Hello, Alec!
Nice to meet you!
```

#### Using an early `return` statement to exit a function

A `return` statement can be used to exit a function. This is normally used when you want to verify (with a conditional statement) that some preconditions are valid before continuing to execute a function body:

```javascript
function greetCodewizard(name) {
    var staff = ["danielj", "alecg", "dimas"];
    if (!staff.includes(name)) {
        console.log("I don't know you!");
        return;
    }
    console.log(`Hello, ${name}!`);
}

greetCodewizard("danielj"); // Hello, danielj!
greetCodewizard("django"); // I don't know you!
```

_Further Reading_

-   [MDN - JavaScript Building Blocks: Functions](https://developer.mozilla.org/en-US/docs/Web/API/Console/log)
-   [EloquentJavaScript - Functions](https://eloquentjavascript.net/03_functions.html)
-   [The Modern JavaScript Tutorial - Functions](https://javascript.info/function-basics)

<hr>

## Loops

If you need to repeat something in your programs, you'll need to use one of JavaScript's looping mechanisms.

### `for`

JavaScript's `for` loop is one of the more complicated pieces of syntax in the language. The _header_ of the `for` loop controls how many times the loop runs, and it consists of three parts:

```javascript
// header
for (counter; loopContinuationCondition; incrementOrDecrement) {
    // body
}
```

The `counter` is a variable that will hold a number representing the current loop iteration (usually). The `loopContinuationCondition` is a `boolean` condition that determines whether the loop should continue. The `incrementOrDecrement` is a statement that modifies the `counter` after each loop completes.

To see all three elements in action, consider this `for` loop, which loops 3 times and prints "Hello" to the console three times:

```javascript
for (var counter = 0; counter < 3; counter++) {
    console.log("Hello");
}
```

Example Output:

```text
Hello
Hello
Hello
```

Generally, the `counter` is called `i`. This is a shorthand that many programmers use, and you'll see it in many courses at CWHQ. The name of the variable is completely up to the programmer:

```javascript
for (var i = 0; i < 3; i++) {
    console.log("Hello");
}
```

Example Output:

```text
Hello
Hello
Hello
```

#### Counter-controlled repetition with the `for` loop

A `for` loop is used to loop a certain number of times (called counter-controlled repetition). You generally perform some action in the body of a `for` loop:

```javascript
for (var i = 0; i < 3; i++) {
    console.log(`${i} taco`);
}
```

Example Output:

```text
0 taco
1 taco
2 taco
```

You can use a `for` loop to loop over an `array`, but the `for...of` loop is easier:

```javascript
var fruits = ["apple", "banana", "cherry"];

for (var i = 0; i < fruits.length; i++) {
    console.log(`Index number: ${i}  Fruit: ${fruits[i]}`);
}
```

Example Output:

```text
Index number: 0  Fruit: apple
Index number: 1  Fruit: banana
Index number: 2  Fruit: cherry
```

#### Looping through `arrays` with the `for...of` loop

The `for...of` loop is the easiest way to loop through the items in an `array`. Note the convention of a plural `array` name (fruits) and a singular loop-iteration variable (fruit):

```javascript
var fruits = ["apple", "banana", "cherry"];

for (var fruit of fruits) {
    console.log(fruit);
}
```

Example Output:

```text
apple
banana
cherry
```

##### Searching for a value in a `for...of` loop

You can use a conditional statement inside a `for...of` loop to search for a particular item in an `array` and then do something:

```javascript
var fruits = ["orange", "banana", "cherry", "apple"];

for (var fruit of fruits) {
    if (fruit == "orange") {
        console.log(`${fruit} is the best fruit`);
    }
}
```

Example Output:

```text
orange is the best fruit
```

##### Finding a value in a `for...of` loop to use after the loop finishes

You can store an item from the `for...of` loop for later use by creating a variable before the `for...of` loop with some default value.

```javascript
var fruits = ["orange", "banana", "cherry", "apple"];

var bestFruit;

for (var fruit of fruits) {
    if (fruit == "orange") {
        bestFruit = fruit;
    }
}

// The best fruit is orange.
console.log(`The best fruit is ${bestFruit}.`);
```

##### Creating a new `array` in a `for...of` loop

Often, you'll want to loop through an `array` and build a new `array` from the contents of the original `array`. This technique is called mapping, and it's a common thing to do with `arrays` and `for...of` loops:

```javascript
var prices = [10, 12, 5, 8];
var discounted_prices = [];

for (var price of prices) {
    discounted_price = price - price * 0.1;
    discounted_prices.push(discounted_price);
}

// Here are your discounted prices: [9, 10.8, 4.5, 7.2]
console.log(`Here are your discounted prices: ${discounted_prices}`);
```

#### Looping through `objects` with the `for...in` loop

The `for...in` loop is the easiest way to loop through the items in an `object`. The `prop` variable name is a convention, it represents each key (property) of the `object`:

```javascript
var users = {
    danielj: "Admin",
    django: "Support Staff",
    samh: "Platform Developer",
};

for (var prop in users) {
    console.log(`Username: ${prop} Role: ${users[prop]}`);
}
```

Example Output:

```text
Username: danielj Role: Admin
Username: django Role: Support Staff
Username: samh Role: Platform Developer
```

_Further Reading_

-   [MDN - JavaScript Reference - for](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for)
-   [MDN - JavaScript Reference - for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
-   [MDN - JavaScript Reference - for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)
-   [Eloquent JavaScript - for loops](https://eloquentjavascript.net/02_program_structure.html#h_oupMC+5FKN)
-   [The Modern JavaScript Tutorial - The "for" loop](https://javascript.info/while-for#the-for-loop)

### `while`

A `while` loop is generally used to perform indefinite repetition (when you don't know how many times you want to loop).

For example, you can use a `while` loop to ask a user something until they answer correctly:

```javascript
var keepLooping = true; // This variable controls whether we loop or not.

while (keepLooping) {
    var userGuess = prompt("What is the meaning of life? ");

    if (userGuess == "42") {
        console.log("That's correct!");
        keepLooping = false; // Stops the loop.
    } else {
        console.log("That's incorrect! Please try again.");
    }
}
```

Example Output:

```text
What is the meaning of life? To make money
That's incorrect! Please try again.
What is the meaning of life? To eat tacos
That's incorrect! Please try again.
What is the meaning of life? 42
That's correct!
```

#### Using `break` to exit a loop

You can also use a `break` statement instead of using a variable to control how many times an indefinite `while` loop runs:

```javascript
while (true) {
    userGuess = prompt("What is the meaning of life? ");

    if (userGuess == "42") {
        console.log("That's correct!");
        break; // Stops the loop.
    } else {
        console.log("That's incorrect! Please try again.");
    }
}
```

Example Output:

```text
What is the meaning of life? To make money
That's incorrect! Please try again.
What is the meaning of life? To eat tacos
That's incorrect! Please try again.
What is the meaning of life? 42
That's correct!
```

#### Counter-controlled repetition

You can use a `while` loop to perform counter-controlled repetition as well, but
the `for` loop is generally preferred for this:

```javascript
var counter = 0;

while (counter < 5) {
    console.log(counter);
    counter++; // If you forget this, you'll have an infinite loop!
}
```

Example Output:

```text
0
1
2
3
4
```

_Further Reading_

-   [MDN - JavaScript Reference: while](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/while)
-   [Eloquent JavaScript - while and do loops](https://eloquentjavascript.net/02_program_structure.html#h_FaGGgUI+MM)
-   [The Modern JavaScript Tutorial - The "while" loop](https://javascript.info/while-for#the-while-loop)

<hr>

## Math Operations

JavaScript can perform most mathematical operations with ease. There are standard operators for all of the arithmetic operations and the `Math` object has access to many more operations for things like Trigonometry.

#### Arithmetic Operators

The four basic arithmetic operations (addition, subtraction, multiplication, division) are similar to how you would use them with calculator:

```javascript
var total = 8 + 2;
var difference = 8 - 2;
var product = 8 * 2;
var quotient = 8 / 2;

console.log(`8 + 2 = ${total}`); // 8 + 2 = 10
console.log(`8 - 2 = ${difference}`); // 8 - 2 = 6
console.log(`8 * 2 = ${product}`); // 8 * 2 = 16
console.log(`8 / 2 = ${quotient}`); // 8 / 2 = 4
```

#### Other Operators

There are a few other common operators that JavaScript provides for common math operations.

##### Modulo

The modulo operator (`%`) returns the remainder after division:

```javascript
10 % 3; // 1
```

##### Power

The power operator (`**`) multiplies a number by itself a given number of times:

```javascript
3 ** 2; // 9
```

_Further Reading_

-   [MDN - The JavaScript Guide: Arithmetic Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#arithmetic_operators)
-   [Eloquent JavaScript - Arithmetic](https://eloquentjavascript.net/01_values.html#i_RfBT3HMnYs)
-   [The Modern JavaScript Tutorial - Basic operators, maths](https://javascript.info/operators)

<hr>

#### The `Math` object

JavaScript's `Math` object can be used to gain access to certain constants (such as PI), to perform trig calculations, or to get random numbers, among other things.

##### Getting random numbers with `Math.random()`

The `Math.random()` method returns a random decimal number between 0 and 1:

```javascript
var randomNumber = Math.random();
console.log(randomNumber); // 0.1524438866958424
```

If you'd like to get a random whole number between a `min` and `max`, this helper function is useful:

```javascript
function random(min, max) {
    var num = Math.floor(Math.random() * (max - min + 1)) + min;
    return num;
}

var randomNumber = random(1, 10);
console.log(randomNumber); // 9
```

##### Rounding numbers

To round a number down, use `Math.floor()`:

```javascript
var roundedNumber = Math.floor(4.6);
console.log(roundedNumber); // 4
```

To round a number up, use `Math.ceil()`:

```javascript
var roundedNumber = Math.ceil(4.2);
console.log(roundedNumber); // 5
```

To round a number to the nearest integer, use `Math.round()`:

```javascript
var roundedNumber = Math.round(4.4);
console.log(roundedNumber); // 4

roundedNumber = Math.round(4.5);
console.log(roundedNumber); // 5
```

_Further Reading_

-   [MDN - The JavaScript Reference: Math](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)

<hr>

## Using `this`

In JavaScript, you can use the `this` keyword to get a reference to an element when an event is triggered (like a click event).

```html
<!DOCTYPE html>

<html>
    <head>
        <title>Using "this" in JavaScript</title>
        <style>
            button {
                display: block;
                margin: 48px auto;
                font-size: 24px;
            }
        </style>
    </head>

    <body>
        <button id="my-button" onclick="changeButtonText(this);">
            Original Button Text
        </button>

        <script>
            function changeButtonText(element) {
                element.textContent = "Updated Button Text";
            }
        </script>
    </body>
</html>
```

<figure markdown>
!['this' example](https://github.com/codewizardshq/docs/blob/main/docs/assets/javascript/using-this-with-onclick.gif?raw=true){ width="100%" }
<figcaption></figcaption>
</figure>

## Variables

Variables assign a name to a value. The naming convention in JavaScript is to use _camelCase_ for variable names.

### Creating a variable

You create a variable using the `var` keyword:

```javascript
var myVariable;
```

Usually, you create a variable and assign a value to the variable the assignment operator (`=`) at once:

```javascript
var myName = "Daniel";
var myAge = 35;
```

### Updating a numeric variable

You can update the value stored in a numeric variable like this:

```javascript
var score = 0;
score = score + 1; // 0 + 1

console.log(score); // 1

score = score + 1; // 1 + 1

console.log(score); // 2
```

The same works for decreasing the value of a numeric variable:

```javascript
var score = 3;
score = score - 1; // 3 - 1

console.log(score); // 2

score = score - 1; // 2 - 1

console.log(score); // 1
```

There is a shorthand notation for increasing and decreasing the value of a numeric variable:

```javascript
var score = 0;
score += 1; // 0 + 1

console.log(score); // 1

score += 1; // 1 + 1

console.log(score); // 2

score -= 1; // 2 - 1

console.log(score); // 1

score -= 1; // 1 - 1

console.log(score); // 0
```

For an even more compact notation, you can use `++` or `--` to increase/decrease the value of a numeric variable:

```javascript
var score = 0;
score++; // 0 + 1

console.log(score); // 1

score++; // 1 + 1

console.log(score); // 2

score--; // 2 - 1

console.log(score); // 1

score--; // 1 - 1

console.log(score); // 0
```

### Global vs. local variables

Any variable created outside of function definition is considered a `global` variable:

```javascript
// This is a global variable.
var score = 0;

function updateScore() {
    score = score + 1; // 1
}

console.log(score); // 0

updateScore(); // Changes the global `score` variable

console.log(score); // 1
```

Updates to `global` variables affect the variable throughout the program. If you want a variable to exist only inside of a function, you can make it local to the function by creating the variable (with the `var` keyword) _inside_ the function:

```javascript
// This is a global variable.
var score = 0;

function updateScore() {
    // This is a local variable, it only exists within `updateScore()`
    var score = 1;
}

console.log(score); // 0

updateScore(); // Doesn't change the global `score` variable

console.log(score); // 0
```

_Further Reading_

-   [MDN - JavaScript First Steps - Variables](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Variables)
-   [Eloquent JavaScript - Bindings](https://eloquentjavascript.net/02_program_structure.html#h_lnOC+GBEtu)
-   [The Modern JavaScript Tutorial - Variables](https://javascript.info/variables)
