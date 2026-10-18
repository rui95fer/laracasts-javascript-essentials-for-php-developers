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
