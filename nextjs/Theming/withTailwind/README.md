# Next.js Theming With TailwindCSS

## Packages

1. [next-themes](https://www.npmjs.com/package/next-themes)

```sh
npm i next-themes
```

## Steps

### Step 1

In `tailwind.config.js` file add the following

```js
module.exports = {
  //   .....
  darkMode: "class",
};
```

### Step 2

Add `attribute="class"` in `<ThemeProvider>` as follows

File: providers.js

```js
return <ThemeProvider attribute="class">{children}</ThemeProvider>;
```

### Other steps are simillar to [withoutTailwind](../withoutTailwind/README.md)
