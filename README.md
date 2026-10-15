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
