---
title: Non-Ember Things in Ember
description: No `ember install`? No problem!
date: 2018/04/26
tags:
  - Ember
---

The Ember community is great and [full of great ember-cli friendly addons](https://www.npmjs.com/search?q=ember) to add to your project. Using [Redux](https://github.com/reactjs/redux)? Check out [ember-redux](https://www.npmjs.com/package/ember-redux). Need [FastClick](https://github.com/ftlabs/fastclick)? Check out... well, actually your best bet is [ember-hammertime](https://www.npmjs.com/package/ember-hammertime) but you get the point.

But **sometimes you just _need_ to incorporate something that isn't Ember ready**. Today that's easier than ever!

## Show Me

In this example we'll be adding `url-polyfill` to our Ember app. _I know `ember-url` is out there but it lacks some of the functionality `url-polyfill` offers._

1. `yarn add url-polyfill` or `npm install --save url-polyfill`
2. In your `ember-cli-build.js` within the `module.exports = function() {` add the following...
```js
app.import('node_modules/url-polyfill/url-polyfill.js');
```

You're done!

For bonus points, you can even configure which import you use based on the environment...
```js
app.import({
  development: 'PATH/file.js',
  production: 'PATH/file.min.js',
});
```

This also works with css files to bring in your favorite CSS framework, animation library or other tool. If you're still using bower, simply point your import path to `bower_components/DEPENDENCY/FILE.EXT`.

### But, wait, I have some setup I need to do!

That's cool too! An initializer is likely what you'll want.
```bash
ember generate initializer myInitializer
```

Then within there you can run any initialization code your heart desires and it'll run at app load.

## Want to go further?

Make an ember-addon for your favorite tool and publish it on npm! The community would appreciate it and love the easy of an `ember install`.

Go make great things. Or... combine great things into an even greater thing!

