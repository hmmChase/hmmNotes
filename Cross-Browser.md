# _Cross-Browser Compatibility_

- Describes the issues and strategies behind making sure your applications work in a consistent manner across as many browsers and platforms as possible

---

## The Approaches:

### Progressive Enhancement

- A strategy where you build your application to work at a baseline level, perhaps somewhere in the middle of the road
- You establish a basic user experience that all browsers you wish to support will be able to provide
- Then you progressively build in more advanced functionality that will be available for platforms that can leverage it

### Graceful Degradation

- Means that you are building your application with as many of the latest and greatest bells and whistles you’d like to provide from the start
- Your default experience is targeted towards the most modern platforms, but then you will degrade it gracefully for older environments - your app will support a lower level of user experience in older browsers

---

## Strategies & Solutions

### Fallbacks

- A fallback is a contingency plan – an option or route to be taken when the preferred choice in unavailable

### CSS Vendor Prefixes

```
background: -moz-linear-gradient(top,  #1e5799 0%, #2989d8 50%, #207cca 51%, #7db9e8 100%);
background: -webkit-linear-gradient(top,  #1e5799 0%,#2989d8 50%,#207cca 51%,#7db9e8 100%);
filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#1e5799', endColorstr='#7db9e8',GradientType=0);
```

### IE Conditional Comments

```
`<!--[if lte IE 8]>
  <script src="ie-fix.js"></script>
  <link href="ie-fix.css" rel="stylesheet" type="text/css" />
<![endif]-->`
```

### Feature Detection

```
if (window.Notification && Notification.permission === "granted") {
  let pushMessage = new Notification('Hi there, notification here!');
} else {
  // perhaps append a jQuery element to the page itself with the same message
  $('#notification-box').append('<li>Hi there, notification here!</li>');
}
```

### Polyfills & Shims

```
if (window.Promise && window.fetch) {
  // carry on, all is good here!
} else {
  // load shim for fetch & promises
  // then carry on, all will be good!
}
```

---

## Cross-Browser Compatibility Tools

### [Modernizr](https://github.com/modernizr/modernizr)

- Provides tons of polyfills for APIs which vary across browsers

### [CSS Normalize](https://necolas.github.io/normalize.css/)

- Will standardize the styling of certain browser elements across browsers

### [Selenium Testing](http://www.seleniumhq.org/)

- Provides a way for you to author tests that reproduce interactions that your users will engage in on your application
- You can test different browsers by using different [`drivers`](https://github.com/SeleniumHQ/selenium/tree/master/javascript/node/selenium-webdriver). There is a corresponding driver for each browser.

### [Sauce Labs](https://saucelabs.com/)

- Provides extensive automated testing for different areas of coverage

### Virtual Machines

- Allows you to run an entirely different operating system
- [VirtualBox](https://www.virtualbox.org/wiki/VirtualBox)

### [Browser Stack](https://www.browserstack.com/)

- Allows you to view your application on multiple different browsers at different resolutions and sizes to test appearance and functionality directly within the browser of your choosing
