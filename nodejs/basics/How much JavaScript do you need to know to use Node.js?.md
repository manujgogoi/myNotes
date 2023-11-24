# How much JavaScript do you need to know to use Node.js?

## What is recommended to learn before diving deep with Node.js?

- [Lexical Structure](#lexical-structure)
- [Expressions](#expressions)
- Data Types
- Classes
- Variables
- Functions
- this operator
- Arrow Functions
- Loops
- Scopes
- Arrays
- Template Literals
- Strict Mode
- ECMAScript 2015 (ES6) and beyond

## Lexical Structure

(JavaScript's lexical grammar)

JavaScript source text is just a sequence of characters — in order for the interpreter to understand it, the string has to be parsed to a more structured representation. The initial step of parsing is called **_lexical analysis_**, in which the text gets scanned from left to right and is converted into a **sequence of individual, atomic input elements**. Some input elements are insignificant to the interpreter, and will be stripped after this step — they include **_white space_** and **_comments_**. The others, including identifiers, keywords, literals, and punctuators (mostly operators), will be used for further syntax analysis. **_Line terminators_** and **_multiline comments_** are also syntactically insignificant, but they guide the process for automatic **semicolons insertion** to make certain invalid token sequences become valid.

[Read More](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar)

## Expressions

### Primary Expressions

Basic keywords and general expressions in JavaScript. These expressions have the highest precedence.

- `this`

  - The this keyword refers to a special property of an execution context.

- `Literals`

  - Basic `null`, `boolean`, `number`, and `string` literals.

- `[]`

  - Array initializer/ literal systax.

- `{}``

  - Object initializer/literal syntax.

- `function`

  - The `function` keyword defines a function expression.

- `class`

  - The `class` keyword defines a class expression.

- `function\*``

  - The `function\*`` keyword defines a generator function expression.

- `async function``

  - The `async function`` defines an async function expression.

- `async function\*``

  - The `async function\*`` keywords define an async generator function expression.

- `/ab+c/i`

  - Regular expression literal syntax.

- `string`

  - Template literal syntax.

- `( )`

  - Grouping operator.
