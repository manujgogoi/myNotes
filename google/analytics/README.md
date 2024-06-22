# Google Analytics

## Next 14 App

- Create an Account on analytics.google.com
- Create a Property - Main
- manual installation (Web)

### Sample of Manual installation code (Don't do this. do the recommended steps)

> Below is the Google tag for this account. Copy and paste it in the code of every page of your website, immediately after the <head> element. Don’t add more than one Google tag to each page.

```js
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-31490VRTPJ"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-31490VRTPJ');
</script>
```

### Recommended step

- In next14 app terminal
- install `@next/third-parties@latest` package

```sh
$ npm install @next/third-parties@latest
```

- In next 14 app's root layout
- Import `GoogleAnalytics`

```js
import { GoogleAnalytics } from "@next/third-parties/google";
```

- Add the following code

```js
<body className={`${inter.className} antialiased`}>
  <ThemeProvider>
    <div className="overflow-hidden">
      <main className="bg-slate-100 dark:bg-black">
        <NavBar />
        {children}
      </main>
    </div>
  </ThemeProvider>
  <GoogleAnalytics gaId="G-31490VRTPJ" />
</body>
```
