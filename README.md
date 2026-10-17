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
