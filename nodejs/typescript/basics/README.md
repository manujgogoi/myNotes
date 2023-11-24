# What is TypeScript?

> TypeScript is an Open Source language and is a supreset of JavaScript

- It offers additional features to JavaScript including static types
- Using types is completely **optional**.
- Compiles down to regular JS.
- Can be used for front-end JS as well as backend with Node.js
- Includes most features from ES6, ES7 (classes, arrow functions, etc...)
- Types from the third party libraries can be added with **type definitions**

## Compiling TypeScript

- TypeScript uses .ts and .tsx extensions
- TSC (TypeScript Compiler) is used to compile .ts files down to JS.
- Can watch files and report errors at compile time
- Many tools include TS compilation by default
- Most IDEs have great support for TS
- The **tsconfig.json** file is used to configure how TypeScript works.

## Installation (Mac)

- Create a project directory (ts-tuts)
- cd to ts-tuts
- Run this command:- `yarn add typescript --dev`

## Test

- $ `npx tsc -v`
- Create a file called index.ts in the project root.

```ts
let v: number = 30;
v = 90;
console.log(v);
```

- To compile the code run the following command

```bash
npx tsc index.ts
```

- It will generate a compiled `index.js` file.

## Create a configuration file

```bash
npx tsc --init
```

It will create a new file called **tsconfig.json**.

- Open the file and change the target as given below:

```json
"target": "es2016",
```

- From now we can compile using

```bash
npx tsc
```

- In `tsconfig.json` file uncomment the `outDir` and add the following

```json
"rootDir": "./src",                                  /* Specify the root folder within your source files. */
"outDir": "./dist",                                   /* Specify an output folder for all emitted files. */
```

- Delete the index.js file and create two dirs in root dir called `dist` and `src`. Move the `index.ts` file to src dir.
  Run the following command

```bash
npx tsc
```

- In `dist` dir create a new file called `index.html` and add the following code.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>TypeScript Tutorial</title>
  </head>
  <body>
    <h1>TypeScript</h1>

    <script src="index.js"></script>
  </body>
</html>
```
- Run the following commmand to watch changes continuously:
```bash
npx tsc --watch
```

- Using **Go Live** vs code extension open the dist/index.html file using live server (In browser).

```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```