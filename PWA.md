# _PWA_

- http://frontend.turing.io/lessons/module-4/pwas/index.html
- Progressive web apps
- Allow web apps to behave on mobile devices similar to native apps
  - responsive design
  - performant on slower network speeds
  - installable and launchable from the home screen
  - all content served over HTTPS
  - provides some form of offline experience
- Must be served over HTTPS

---

# _Manifest_

- https://developers.google.com/web/fundamentals/web-app-manifest/

* a JSON file
* Tells the browser about your web application and how it should behave when 'installed' on the users mobile device or desktop
* `<link rel="manifest" href="/manifest.json">`

- Provides:
  - Access to hardware
  - Home screen icon
  - Works offline
  - Loading screens

```
{
  "short_name": "Maps",
  "name": "Google Maps",
  "icons": [
    {
      "src": "/images/icons-192.png",
      "type": "image/png",
      "sizes": "192x192"
    },
    {
      "src": "/images/icons-512.png",
      "type": "image/png",
      "sizes": "512x512"
    }
  ],
  "start_url": "/maps/?source=pwa",
  "background_color": "#3367D6",
  "display": "standalone",
  "scope": "/maps/",
  "theme_color": "#3367D6"
}
```

## name

- the name used to add to the homescreen

## short_name

- name used for the homescreen icon

## start_url

- The `start_url` tells the browser where your application should start when it is launched
- Prevents the app from starting on whatever page the user was on when they added your app to their home screen.
- Your `start_url` should direct the user straight into your app, rather than a product landing page. Think about the what the user will want to do once they open your app, and place them there.

```
`"start_url": "/?utm_source=a2hs"`
```

- The URL that loads when a user launches the application (e.g. when added to home screen), typically the index. Note that this has to be a relative URL, relative to the manifest url.

```
`"start_url": "/pwa-examples/a2hs/index.html"`
```

## icons

- array of image objects used for homescreen, splash page, ...

## background_color

- color of the loading screen, splash page, ...

## theme_color

- color of the toolbar (URL bar if you have it)

## display

- specify how the page looks
- fullscreen, standalone, browser

---

# _Service Workers_

- https://developers.google.com/web/fundamentals/primers/service-workers/

- Whenever a browser parses an HTML file, it makes a fetch request for all the assets needed
  - stylesheets
  - fonts
  - images
  - scripts

* Able to intercept network requests
* Able to set/read from the browser cache

## Lifecycle

- Register the service worker in you app
  - Returns a promise


    * `app.js`

```
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker
      .register('./service-worker.js')
      .then(registration => {
        console.log('Service Worker registered');
      })
      .catch(error => {
        console.log('Service Worker not registered', error);
      });
  });
} else {
  // fallback code
  // service worker polyfill
}
```

    * `service-worker.js`

```
// listen for fetch events

this.addEventListener('fetch', event => {
  console.log('event: ', event);
});
```

- Installation
  - Can be used to create a cache

```
// create cache
this.addEventListener('install', event => {
  // create folder
  event.open('asset-v1').then(cache => {
    // specify what to put into cache and where to find them
    return cache.addAll([
      // index
      '/',
      // app.js
      '/app.js',
      // css
      '/css/app.css',
      // jQuery
      '/lib/jquery-3.2.1.js',
      // logo
      '/img/logo.png'
    ]);
  });
});
```

- Active
  - Use for versioning assets
    - keeps assets from becoming stale
    - every time you change an asset, you must change the version number

```
this.addEventListener('activate', event => {
  // list of assets to keep
  let cacheWhitelist = ['assets-v2'];

  event.waitUntil(
    // look into assets and return list of keys
    caches.keys().then(keyList => {
      return Promise.all(
        // map over keylist
        keyList.map(key => {
          // is the asset if in the cache, don't keep it
          if (cacheWhitelist.indexOf(key) === -1) {
            // delete the asset
            return caches.delete(key);
          }
        })
      );
    })
  );
});
```

## Offline functionality

- Put assets into cache when user first goes to page
- Whenever there is a network request for an asset
  - check if the asset is in the cache
    - if not, then make a network request for the asset

---

# _Caching_
