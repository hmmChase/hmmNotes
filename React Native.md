# _React Native_

- Mobile version of React
- No DOM
- Can create apps that work on both IOS and Android

* Doesn't use HTML
* Uses mobile components
* No webpack
  - uses Xcode
* Inline styling

---

## Install tools

- `brew install watchman`
  - Watchman is a tool built by Facebook to watch the file system and reload your code on the mobile emulators
- `npm i -g react-native-cli`
  - React Native CLI

## Create app

```
# Create our app
$ react-native init DinoBounce
$ cd DinoBounce
```

## Start app

```
# Start app
# In one terminal window
$ react-native npm start

# In another terminal window
# To run in iOS
$ react-native run-ios

# To run in Android
# you'll need to install other tooling to do this
$ react-native run-android

# If you want to pick a specific device on iOS,
# set it with the simulator flag
$ react-native run-ios --simulator="iPhone 4s"

# To check all the available devices you can run with iOS,
# run the below code. Pretty awesome that you can emulate
# iPhones, Ipads, iWatchs, Apple Tv
$ xcrun simctl list devices
```

---
