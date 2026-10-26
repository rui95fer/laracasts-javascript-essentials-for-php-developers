# JavaScript Essentials for PHP Developers

## Episode 01 — Structure, Syntax, And Scope

- **The browser provides `alert()` to display a message in a dialog.**
  ```js
  alert('Hello, world!');
  ```

- **Single and double quotes both create strings; neither interpolates variables as PHP double quotes do. Choose quotes that reduce escaping, or escape a matching quote with a backslash.**
  ```js
  alert("It's ready.");
  alert('Click "Save".');
  alert('It\'s ready.');
  ```

- **End statements with semicolons for consistency with PHP. JavaScript can insert some semicolons automatically, but relying on that can produce unexpected behavior.**
  ```js
  alert('Changes saved.');
  alert('You can close this window.');
  ```

- **Declare functions with `function`, put parameters in parentheses, and use `return` to send a value back to the caller. Curly braces enclose the function body, much like PHP.**
  ```js
  function addPrices(firstPrice, secondPrice) {
      return firstPrice + secondPrice;
  }

  alert(addPrices(20, 5)); // 25
  ```

- **JavaScript identifiers do not require `$`; use camelCase for ordinary variable, parameter, and function names. `$` is allowed, but it is not a variable prefix as it is in PHP.**
  ```js
  function calculateTotal(unitPrice, quantity) {
      return unitPrice * quantity;
  }

  var orderTotal = calculateTotal(15, 3);
  ```

- **Use `if` to check a condition and `throw new Error()` to stop a function when an input is unacceptable. For JavaScript Numbers, division by zero does not throw automatically: `10 / 0` produces `Infinity`, and `0 / 0` produces `NaN` (“not a number”).**
  ```js
  function divide(dividend, divisor) {
      if (divisor === 0) {
          throw new Error('Cannot divide by zero.');
      }

      return dividend / divisor;
  }

  alert(divide(10, 2)); // 5
  divide(10, 0); // Throws Error: Cannot divide by zero.
  ```

- **Use `+` to concatenate strings, rather than PHP's dot operator. The same operator adds numbers, so the values' types matter.**
  ```js
  alert('Hello, ' + 'Jim'); // Hello, Jim
  alert(10 + 5);           // 15
  alert('10' + 5);         // 105 (a string)
  ```

- **Declare variables explicitly to avoid accidental globals. Assigning to an undeclared name can create a global in non-strict code; in strict mode, it throws a `ReferenceError`.**
  ```js
  // Before: message is undeclared.
  function sayHello(name) {
      message = 'Hello, ' + name;
      alert(message);
  }

  // After: message belongs to this function.
  function greetCustomer(name) {
      var message = 'Hello, ' + name;
      alert(message);
  }
  ```

- **A variable declared with `var` inside a function has function scope: it is available throughout that function, including inside its blocks. Functions can also read variables from an enclosing scope without PHP's `global` declaration.**
  ```js
  var greeting = 'Hello'; // Global in a classic browser script, not a module.

  function greetCustomer(name) {
      if (name) {
          var message = greeting + ', ' + name;
      }

      alert(message);
  }

  greetCustomer('Jim'); // Hello, Jim
  // message is not accessible outside greetCustomer().
  ```

- **Declaration creates a variable; assignment gives it a value. You can do these separately, but initialize a variable when declaring it when a useful value is available.**
  ```js
  var customerName;
  // customerName is undefined until assigned a value.
  customerName = 'Jim';

  var greeting = 'Hello, ' + customerName;
  ```

- **Use dot syntax to access properties and call methods, rather than PHP's `->`. A method is a function accessed through a value; strings are primitives, but JavaScript still lets you call their methods.**
  ```js
  var message = '  Hello, Jim  ';

  alert(message.trim());        // Hello, Jim (without surrounding spaces)
  alert(message.toUpperCase()); //   HELLO, JIM   (spaces remain)
  alert(message.length);        // 14
  // These string methods return new strings; message stays unchanged.
  ```

> **Takeaway:** JavaScript's function and conditional syntax will feel familiar from PHP; pay special attention to string operators, explicit variable declarations, and scope.

## Episode 02 — Data Types

- **JavaScript is dynamically typed: values have types, but a variable can hold values of different types over time. Plain JavaScript has no PHP-style parameter or return type declarations.**
  ```js
  var orderTotal = '25';
  console.log(typeof orderTotal); // "string"

  orderTotal = 25;
  console.log(typeof orderTotal); // "number"
  ```

- **A variable declared without an initial value holds `undefined`; an omitted function argument also leaves its parameter `undefined`.**
  ```js
  var deliveryDate;
  console.log(deliveryDate); // undefined

  function showDeliveryDate(date) {
      console.log(date);
  }

  showDeliveryDate(); // undefined
  ```

- **Single and double quotes both create strings; choose quotes that avoid escaping, or escape a matching quote with a backslash.**
  ```js
  var statusMessage = "It's ready.";
  var instruction = 'Click "Save".';
  var confirmation = 'It\'s saved.';
  ```

- **Whole numbers and decimal numbers both use JavaScript's `number` type, unlike PHP's separate integer and float types.**
  ```js
  var quantity = 3;
  var unitPrice = 19.95;

  console.log(typeof quantity);  // "number"
  console.log(typeof unitPrice); // "number"
  ```

- **The `boolean` type has two values, `true` and `false`, which represent yes/no states. Truthy and falsy rules for other types belong to the conditions lesson.**
  ```js
  var isPaid = true;
  var isShipped = false;

  console.log(typeof isPaid);    // "boolean"
  console.log(typeof isShipped); // "boolean"
  ```

- **An object groups named properties; create one with an object literal (`{}`) and use dot syntax to read a property.**
  ```js
  var customer = {
      name: 'Jim',
      isSubscribed: true
  };

  console.log(customer.name);   // Jim
  console.log(typeof customer); // "object"
  ```

- **Use `null` to express intentional absence, while `undefined` commonly indicates a value has not been supplied. `null` is a primitive (a non-object value); `typeof null` returning `"object"` is a historical quirk.**
  ```js
  var selectedCustomer = null; // No customer selected yet.
  var deliveryDate;            // No value supplied yet.

  console.log(selectedCustomer === null);     // true
  console.log(deliveryDate === undefined);    // true
  console.log(null === undefined);            // false
  console.log(typeof selectedCustomer);       // "object"
  ```

- **Use arrays for ordered lists with numeric indexes starting at zero, and objects for named key-value data like PHP associative arrays. Arrays are objects, so use `Array.isArray()` to identify them.**
  ```js
  var productNames = ['Keyboard', 'Mouse'];
  var productPrices = { keyboard: 49, mouse: 25 };

  console.log(productNames[0]);             // Keyboard
  console.log(productPrices.keyboard);      // 49
  console.log(typeof productNames);         // "object"
  console.log(Array.isArray(productNames)); // true
  ```

- **Functions are values: you can store one in a variable and call it through that variable. They are callable objects, and `typeof` identifies them with `"function"`.**
  ```js
  var calculateTotal = function (unitPrice, quantity) {
      return unitPrice * quantity;
  };

  console.log(calculateTotal(15, 3)); // 45
  console.log(typeof calculateTotal); // "function"
  ```

- **The `typeof` operator returns a string describing a value's type at runtime; remember that it cannot distinguish arrays or `null` from ordinary objects. Symbols are another primitive type, introduced here only by name and a type check.**
  ```js
  console.log(typeof undefined);         // "undefined"
  console.log(typeof 'Order confirmed'); // "string"
  console.log(typeof 25);                // "number"
  console.log(typeof true);              // "boolean"
  console.log(typeof Symbol('orderId')); // "symbol"
  console.log(typeof {});                // "object"
  console.log(typeof null);              // "object"
  console.log(typeof []);                // "object"
  console.log(typeof function () {});    // "function"
  ```

> **Takeaway:** JavaScript variables can hold different types of values; use `typeof` to inspect them, with a direct `null` check or `Array.isArray()` when you need a more precise answer.

## Episode 03 — Smooth Operators

- **Use template literals to build strings with variables or expressions: wrap the string in backticks and insert values with `${expression}`. They also allow line breaks, much like PHP heredocs.**
  ```js
  var customerName = 'Jim';
  var unitPrice = 15;
  var quantity = 3;

  console.log(`Hello, ${customerName}!`); // Hello, Jim!
  console.log(`Total: ${unitPrice * quantity}`); // Total: 45
  console.log(`Order confirmed.
  Thank you, ${customerName}!`);
  // Order confirmed.
  // Thank you, Jim!
  ```

- **JavaScript's `+` adds numbers or joins strings; if either operand is a string, it converts the other to a string. This automatic type conversion is called coercion; prefer template literals when building strings.**
  ```js
  console.log(1 + 2);   // 3
  console.log(1 + '2'); // "12"

  var quantityInput = '2';
  console.log(Number(quantityInput) + 1); // 3: explicitly convert for addition.
  ```

- **A chain of `+` operations groups from left to right, so addition can turn into concatenation partway through.**
  ```js
  console.log(1 + 2 + '2');             // "32"
  console.log('1' + 2 + 2);             // "122"
  console.log(1 + 2 + '2' + [1, 2, 3]); // "321,2,3"
  // In this concatenation, the array becomes "1,2,3".
  ```

- **Unlike `+`, subtraction, multiplication, and division convert numeric strings to numbers; an invalid numeric string produces `NaN` (“not a number”).**
  ```js
  console.log(1 - '2');       // -1
  console.log(3 * '2');       // 6
  console.log(6 / '2');       // 3
  console.log(3 * 'pending'); // NaN
  ```

- **When comparing a number with a string, relational operators convert the string to a number; an empty string becomes zero, while a nonnumeric string becomes `NaN` and makes these comparisons false.**
  ```js
  console.log(1 < '2');        // true
  console.log(1 > '');         // true: Number('') is 0.
  console.log(1 < 'pending');  // false
  console.log(1 >= 'pending'); // false
  ```

- **Two strings compare lexicographically (character by character), even when they contain digits; convert them explicitly when you need a numeric comparison.**
  ```js
  var firstPrice = '10';
  var secondPrice = '2';

  console.log(firstPrice < secondPrice);                 // true: '1' comes before '2'.
  console.log(Number(firstPrice) < Number(secondPrice)); // false
  ```

- **Falsy values become `false` in Boolean contexts such as `if` conditions; the common ones are `false`, `0`, `-0`, `''`, `null`, `undefined`, and `NaN`. `Boolean()` lets you check this conversion directly.**
  ```js
  console.log(Boolean(false));     // false
  console.log(Boolean(0));         // false
  console.log(Boolean(-0));        // false
  console.log(Boolean(''));        // false
  console.log(Boolean(null));      // false
  console.log(Boolean(undefined)); // false
  console.log(Boolean(NaN));       // false
  ```

- **Unlike PHP, JavaScript treats `'0'` and empty arrays as truthy; ordinary objects are truthy too. Numeric conversion follows different rules, so an empty array can be truthy yet convert to zero.**
  ```js
  console.log(Boolean('0')); // true
  console.log(Boolean([]));  // true
  console.log(Boolean({}));  // true
  console.log(Number([]));   // 0
  console.log(1 > []);       // true: the comparison converts [] to 0.
  ```

- **Prefer `===` and `!==` when comparing values without type conversion; `==` and `!=` allow coercion. Loose equality follows its own rules, so it does not simply equate all falsy values.**
  ```js
  console.log(1 == '1');   // true
  console.log(1 === '1');  // false
  console.log(1 != '1');   // false
  console.log(1 !== '1');  // true
  console.log(0 === 0);    // true

  console.log(0 == false);       // true
  console.log(0 == []);          // true
  console.log(0 == null);        // false
  console.log(0 == undefined);   // false
  console.log(null == undefined); // true
  ```

- **`++` and `--` change a variable by one: the prefix form returns the updated value, while the postfix form returns the previous value.**
  ```js
  var quantity = 2;

  console.log(quantity++); // 2; quantity is now 3.
  console.log(++quantity); // 4; quantity is now 4.
  console.log(quantity--); // 4; quantity is now 3.
  console.log(--quantity); // 2; quantity is now 2.
  ```

- **Spread syntax (`...`) expands an array's elements into another array, allowing you to build a new list.**
  ```js
  var currentProducts = ['Keyboard', 'Mouse'];
  var updatedProducts = [...currentProducts, 'Monitor'];

  console.log(updatedProducts); // ['Keyboard', 'Mouse', 'Monitor']
  console.log(currentProducts); // ['Keyboard', 'Mouse']
  ```

- **In a function parameter, `...` is rest syntax: it collects arguments into an array. Here, `reduce()` combines the prices using an arrow function that adds each price to a running total starting at zero.**
  ```js
  function sumPrices(...prices) {
      return prices.reduce((total, price) => total + price, 0);
  }

  console.log(sumPrices(10, 20, 5)); // 35
  console.log(sumPrices());          // 0
  ```

- **`&&` returns the first falsy operand, or the last operand if all are truthy; `||` returns the first truthy operand, or the last if all are falsy. They short-circuit, skipping operands once the result is known; `!` always returns a Boolean.**
  ```js
  console.log('ready' && 'saved'); // "saved"
  console.log(0 && 'saved');       // 0
  console.log('' || 'Guest');      // "Guest"
  console.log(!'ready');          // false

  false && console.log('Skipped'); // Does not call console.log().
  ```

- **JavaScript has no PHP-style spaceship operator (`<=>`); use familiar comparison operators for individual conditions.**
  ```js
  var orderTotal = 45;

  console.log(orderTotal < 50);   // true
  console.log(orderTotal > 50);   // false
  console.log(orderTotal === 45); // true
  ```

> **Takeaway:** Pay attention to type conversion: build strings with template literals, convert numeric input explicitly, and use strict equality for predictable comparisons.

## Episode 04 — Controlling Flow

- **Use `if`, `else if`, and `else` to choose between actions, much like PHP: only the first matching branch runs, with `else` handling the remaining cases.**
  ```js
  var orderStatus = 'paid';

  if (orderStatus === 'shipped') {
      console.log('Track your delivery.');
  } else if (orderStatus === 'paid') {
      console.log('Preparing your order.');
  } else {
      console.log('Waiting for payment.');
  }
  // Preparing your order.
  ```

- **Use the ternary operator to choose a value: `condition ? valueIfTrue : valueIfFalse`.**
  ```js
  var isPaid = true;
  var orderMessage = isPaid ? 'Ready to pack' : 'Payment required';

  console.log(orderMessage); // Ready to pack
  ```

- **Use `switch` to handle specific values; `default` handles an unmatched value, and `break` prevents execution from continuing into the next case.**
  ```js
  var orderStatus = 'paid';

  switch (orderStatus) {
      case 'paid':
          console.log('Pack the order.');
          break;
      case 'shipped':
          console.log('Show tracking details.');
          break;
      default:
          console.log('Check the order status.');
  }
  // Pack the order.
  ```

- **A `for` loop puts initialization, the condition checked before each iteration, and the counter update in one place. An iteration is one pass through the loop body.**
  ```js
  for (var packageNumber = 1; packageNumber <= 3; packageNumber++) {
      console.log(packageNumber);
  }
  // 1, 2, 3 (one per line)
  ```

- **A `while` loop checks its condition before each iteration; update the counter so the condition eventually becomes false.**
  ```js
  var packageNumber = 1;

  while (packageNumber <= 3) {
      console.log(packageNumber);
      packageNumber++;
  }
  // 1, 2, 3 (one per line)
  ```

- **A `do...while` loop checks its condition after the body, so it always runs at least once, even when the condition starts false. End it with a semicolon.**
  ```js
  var packageNumber = 1;

  do {
      console.log(packageNumber);
      packageNumber++;
  } while (packageNumber <= 0);
  // 1: the body runs before the false condition is checked.
  ```

- **Use `for...of` to read each value from an array when you do not need its index.**
  ```js
  var fruits = ['apple', 'banana', 'orange', 'cherry'];

  for (var fruit of fruits) {
      console.log(fruit);
  }
  // apple, banana, orange, cherry (one per line)
  ```

- **Use `for...in` to read an object's enumerable property names (those available to this loop), then use `object[property]` to read each value. It can also include inherited enumerable properties.**
  ```js
  var person = {
      firstName: 'John',
      lastName: 'Doe'
  };

  for (var property in person) {
      console.log(property + ': ' + person[property]);
  }
  // firstName: John
  // lastName: Doe
  ```

- **Use `break` to stop a loop immediately, such as when you find the value you need.**
  ```js
  var fruits = ['apple', 'banana', 'orange'];

  for (var fruit of fruits) {
      if (fruit === 'banana') {
          console.log('Found banana.');
          break;
      }
  }
  // Found banana.
  ```

- **Use `continue` to skip the rest of the current iteration and move on to the next one.**
  ```js
  var person = {
      firstName: 'John',
      lastName: 'Doe'
  };

  for (var property in person) {
      if (property === 'firstName') {
          continue;
      }

      console.log(property + ': ' + person[property]);
  }
  // lastName: Doe
  ```

> **Takeaway:** JavaScript's conditions and basic loops work much like PHP's; use `for...of` for array values and `for...in` for object property names.

## Episode 05 — Creating Functions

- **Functions are first-class values: you can assign them to variables, pass them as arguments, and return them from other functions. Assigning a function without `()` stores the function; adding `()` calls it.**
  ```js
  function calculateTotal(unitPrice, quantity) {
      return unitPrice * quantity;
  }

  var totalCalculator = calculateTotal;

  console.log(totalCalculator(15, 3)); // 45
  ```

- **An ordinary function returns `undefined` when it finishes without returning a value; use `return` to send a result back to the caller.**
  ```js
  function doNothing() {}

  function addPrices(firstPrice, secondPrice) {
      return firstPrice + secondPrice;
  }

  console.log(doNothing());       // undefined
  console.log(addPrices(20, 5)); // 25
  ```

- **A top-level function declaration is available before execution reaches its definition; this behavior is called hoisting.**
  ```js
  console.log(addPrices(20, 5)); // 25

  function addPrices(firstPrice, secondPrice) {
      return firstPrice + secondPrice;
  }
  ```

- **A function expression creates a function as a value; when assigning it to a variable, call it only after that assignment executes. With `var`, the variable exists as `undefined` beforehand, so calling it too early throws a `TypeError`.**
  ```js
  // subtractDiscount(25, 5); // TypeError: subtractDiscount is not a function.

  var subtractDiscount = function (price, discount) {
      return price - discount;
  };

  console.log(subtractDiscount(25, 5)); // 20
  ```

- **An arrow function with an expression body returns that expression automatically; a body in curly braces needs an explicit `return` to return a result. Arrow functions also handle context (`this`) differently from ordinary functions, a topic for a later lesson.**
  ```js
  var calculateTotal = (unitPrice, quantity) => unitPrice * quantity;

  var divide = (dividend, divisor) => {
      if (divisor === 0) {
          throw new Error('Cannot divide by zero.');
      }

      return dividend / divisor;
  };

  console.log(calculateTotal(15, 3)); // 45
  console.log(divide(10, 2));        // 5
  // divide(10, 0); // Throws Error: Cannot divide by zero.
  ```

- **An anonymous function omits a name after `function`; assigning it to a variable still lets you call it. Function expressions can also include an explicit function name.**
  ```js
  var calculateTotal = function (unitPrice, quantity) {
      return unitPrice * quantity;
  };

  console.log(calculateTotal(15, 3)); // 45
  ```

- **An immediately invoked function expression (IIFE) runs as soon as it is created and gives its variables a local scope. Wrap the function in parentheses to make it an expression, then add `()` to call it.**
  ```js
  (function () {
      var orderMessage = 'Order confirmed.';
      console.log(orderMessage);
  })(); // Order confirmed.

  // console.log(orderMessage); // ReferenceError: orderMessage is not defined.
  ```

- **A closure lets a function keep access to variables from its enclosing scope; a returned function can use that access to preserve state between calls. An IIFE's local scope alone does not demonstrate state surviving after it finishes.**
  ```js
  // Illustrative extension: keep a counter between calls.
  function createOrderCounter() {
      var count = 0;

      return function () {
          count++;
          return count;
      };
  }

  var nextOrderNumber = createOrderCounter();

  console.log(nextOrderNumber()); // 1
  console.log(nextOrderNumber()); // 2
  // count is local to createOrderCounter(), but the returned function retains access.
  ```

> **Takeaway:** Functions are values you can store and call; their syntax affects when they become available and how they return results, while their scope can keep variables local or preserve state through closures.

## Episode 06 — Scoping Out The Variables

- **Use `Math.floor(Math.random() * 10) + 1` to generate a whole number from 1 through 10. `Math.random()` returns a number from zero up to, but excluding, one; `Math.floor()` rounds down.**
  ```js
  const secretNumber = Math.floor(Math.random() * 10) + 1;
  // Multiply: 0 up to, but excluding, 10.
  // Round down: 0 through 9. Add 1: 1 through 10.
  ```

- **The browser's `prompt()` returns a string or `null` when cancelled; use `Number()` to convert input before checking for `NaN` and values outside the allowed range. The episode's check accepts decimals within the range; it does not enforce whole numbers.**
  ```js
  const input = prompt('Enter a number between 1 and 10.');
  const guess = Number(input);

  if (Number.isNaN(guess) || guess < 1 || guess > 10) {
      console.log('Please enter a valid number from 1 through 10.');
  }

  // Number('hello') is NaN; Number('5') is 5.
  // Number(null) and Number('') are 0, so this check rejects them.
  // Both endpoints (1 and 10) and a decimal such as 2.5 pass.
  ```

- **Use `continue` after invalid input and `break` after a correct guess. In this game, invalid input consumes an attempt because `continue` still runs the `for` loop's counter update.**
  ```js
  // Adapted game loop; run in a browser.
  const secretNumber = Math.floor(Math.random() * 10) + 1;
  const maxAttempts = 3;

  for (let attempt = 1; attempt <= maxAttempts; attempt++) {
      const guess = Number(prompt('Enter a number between 1 and 10.'));

      if (Number.isNaN(guess) || guess < 1 || guess > 10) {
          console.log('Please enter a valid number from 1 through 10.');
          continue;
      }

      if (guess === secretNumber) {
          console.log('Congrats, you guessed the number!');
          break;
      }

      console.log(guess < secretNumber ? 'Too low.' : 'Too high.');
  }
  ```

- **A loop counter can exceed the number of attempts made: after three unsuccessful iterations, a counter starting at one reaches four. Count completed attempts separately when reporting the total.**
  ```js
  // Adapted counting example: all three attempts are unsuccessful.
  const maxAttempts = 3;
  let attempt;
  let attemptsUsed = 0;

  for (attempt = 1; attempt <= maxAttempts; attempt++) {
      attemptsUsed++;
  }

  console.log(attempt);      // 4: the next condition check fails.
  console.log(attemptsUsed); // 3: the loop body ran three times.
  ```

- **Move game state into an IIFE and return the function you want callers to use. The returned function forms a closure: it keeps access to the enclosed variables after the IIFE finishes, while those names are unavailable outside.**
  ```js
  // Before: these names are global in a classic browser script.
  var secretNumber = Math.floor(Math.random() * 10) + 1;
  var maxAttempts = 3;

  function playGame() {
      // Game loop uses secretNumber and maxAttempts.
  }
  ```
  ```js
  // After: alternative version with private state.
  const playGame = (function () {
      const secretNumber = Math.floor(Math.random() * 10) + 1;
      const maxAttempts = 3;

      return function () {
          // Game loop omitted; this function can read both constants.
          console.log(`You have ${maxAttempts} attempts.`);
      };
  })();

  playGame(); // You have 3 attempts.
  // console.log(secretNumber); // ReferenceError in this version.
  // The secret is generated once when the IIFE runs, not on each playGame() call.
  ```

- **Use `const` for a binding that must not be reassigned, and supply its initial value when declaring it. A binding connects a name to a value; keeping that connection fixed does not make an object's contents immutable.**
  ```js
  const playGame = function () {
      console.log('Starting game.');
  };

  // playGame = function () {}; // TypeError: assignment to a constant.
  // const maxAttempts;         // SyntaxError: missing initializer.

  const settings = { maxAttempts: 3 };
  settings.maxAttempts = 5; // Allowed: the object itself can change.
  // settings = {};        // TypeError: settings cannot be reassigned.
  ```

- **Inside a function, `var` has function scope, while `let` and `const` have block scope. A block is a group of statements enclosed in curly braces, such as an `if` body; its `let` and `const` declarations are unavailable outside it.**
  ```js
  function showGameSettings() {
      if (true) {
          var maxAttempts = 3;
          let attemptsUsed = 0;
          const secretNumber = 7;
      }

      console.log(maxAttempts); // 3
      // console.log(attemptsUsed); // ReferenceError
      // console.log(secretNumber); // ReferenceError
  }

  showGameSettings();
  // console.log(maxAttempts); // ReferenceError: var stays inside the function.
  ```

- **Declare changing state with `let` in the enclosing function block when both a loop and the code after it need access. A `let` declared in a loop header or an `if` block stays local to that scope.**
  ```js
  // Before: neither variable is available after the loop.
  function showResult() {
      for (let attempts = 1; attempts <= 3; attempts++) {
          if (attempts === 2) {
              let guessed = true;
              break;
          }
      }

      // console.log(attempts, guessed); // ReferenceError
  }
  ```
  ```js
  // After: illustrative success on the second attempt.
  function showResult() {
      let attempts = 0;
      let guessed = false;

      while (attempts < 3) {
          attempts++;

          if (attempts === 2) {
              guessed = true;
              break;
          }
      }

      console.log(attempts, guessed); // 2, true
  }

  showResult();
  ```

- **A paused browser debugger can inspect variables available in the selected execution scope, including a closure's state. Scope limits ordinary access and `const` prevents reassignment; neither makes browser code a security boundary.**
  ```js
  const playGame = (function () {
      const secretNumber = Math.floor(Math.random() * 10) + 1;
      let maxAttempts = 3;

      return function () {
          debugger; // With DevTools open, inspect this function's scope.
          console.log(secretNumber, maxAttempts);
      };
  })();

  playGame();
  // While paused here, the console can read secretNumber and maxAttempts.
  // maxAttempts can be reassigned; secretNumber is a constant.
  ```

> **Takeaway:** Choose declarations by scope and reassignment: `var` stays within its function, `let` and `const` stay within their block, and closures let functions retain access to enclosed state.
