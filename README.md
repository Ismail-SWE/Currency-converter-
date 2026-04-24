# Currency Exchanger

A real-time currency converter web app built with HTML, Bootstrap 5, and Vanilla JavaScript using the Frankfurter API.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
  - [AI Collaboration](#ai-collaboration)
- [Author](#author)

## Overview

### The challenge

Users should be able to:

- View a live table of exchange rates fetched from the Frankfurter API
- Select a base currency and a desired currency
- Enter an amount and convert it in real time by clicking the Convert button

### Screenshot

![](./screenshot.jpg)

### Links

- Solution URL: [Add solution URL here](https://your-solution-url.com)
- Live Site URL: [Add live site URL here](https://your-live-site-url.com)

## My process

### Built with

- Semantic HTML5 markup
- Bootstrap 5 (via CDN) for layout and styling
- Vanilla JavaScript (ES6+)
- OOP — Classes, private fields, constructors
- Frankfurter API for real-time exchange rates
- `async/await` for API requests

### What I learned

**Bootstrap spacing utilities:**
```html
<!-- px-4: left/right padding, p-3: all sides padding -->
<div class="container px-4">
<div class="row p-3">
```

**Bootstrap Grid — responsive columns:**
```html
<!-- 50% on small screens, 25% on 576px+ screens -->
<div class="col-6 col-sm-3">
```

**Bootstrap Flexbox utilities:**
```html
<!-- align elements to the bottom -->
<div class="d-flex align-items-end">
```

**JavaScript Classes with private fields:**
```js
class Currency {
    #code;
    #rate;

    constructor(code, rate) {
        this.#code = code;
        this.#rate = rate;
    }

    get code() { return this.#code; }
    get rate() { return this.#rate; }
}
```

**Why `async #init()` instead of `async constructor()`:**
```js
// constructor cannot be async — so we delegate to a private method
constructor() {
    this.#init();
}

async #init() {
    const response = await fetch('https://api.frankfurter.app/latest?from=USD');
    const result = await response.json();
}
```

**Destructuring API response:**
```js
const { base, amount, rates } = result;
// base   → "USD"
// amount → 1
// rates  → { EUR: 0.91, GBP: 0.85, ... }
```

**Object.entries() + map() to create Currency objects:**
```js
const otherCurrencies = Object.entries(rates).map(
    ([code, rate]) => new Currency(code, rate)
);
```

**Spread operator to merge arrays:**
```js
this.#currencies = [baseCurrency, ...otherCurrencies];
```

**Cross-rate conversion formula:**
```js
const result = (amount * toCurrency / fromCurrency).toFixed(2);
```

**CORS issue when fetching from `file://` or `localhost`:**  
Frankfurter API blocks requests from local origins. Solved by disabling web security in Chrome during development:
```bash
open -n -a /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
  --args --user-data-dir="/tmp/chrome_dev" --disable-web-security
```

### Continued development

- Add currency flags for better UI
- Add historical rate chart using Chart.js
- Make the app fully responsive on mobile
- Deploy to GitHub Pages or Netlify
- Handle API errors gracefully with user-friendly messages

### Useful resources

- [Frankfurter API](https://www.frankfurter.app/) - Free, open-source exchange rate API
- [Bootstrap 5 Docs](https://getbootstrap.com/docs/5.3/) - Spacing, Grid, Flexbox utilities
- [MDN — Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) - Private fields and class syntax
- [MDN — async/await](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Promises) - Async functions and promises

### AI Collaboration

Used **Claude (Anthropic)** throughout the project as a learning assistant:

- Explained Bootstrap utility classes (`container`, `row`, `col`, `px-4`, `p-3`, `d-flex`, `align-items-end`, `form-control`, `form-select`, `btn`, `table-striped`) one by one
- Broke down JavaScript OOP concepts — classes, private fields (`#`), constructors, `this`, getters, and methods
- Explained `async/await`, `fetch`, destructuring, `Object.entries()`, `map()`, `forEach()`, and spread operator (`...`)
- Helped debug a CORS error blocking the Frankfurter API request from localhost
- Explained the cross-rate conversion formula step by step

What worked well: asking Claude to explain each line of code individually rather than all at once made the concepts much easier to absorb.

## Author

- GitHub - [Add your username here](https://github.com/Ismail-SWE)
