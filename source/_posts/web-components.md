---
title: On Web Components
description: They're ready for the mainstream. Automation testable. Even IE11 compatible, mostly.
date: 2019/01/23
tags:
  - Components
  - Testing
  - Retrospective
---

Components were designed to share reusable code within a project. Sometimes between projects. But, what if a projects' base technology is fundamentally different (Ember, React, Vue)? **Luckily all web apps speak Javascript and the DOM which is where native web components come in.**

## Hybrids (Web Component Framework)

![Hybrids Logo](https://raw.githubusercontent.com/hybridsjs/hybrids/master/docs/assets/hybrids-logo.svg?sanitize=true)

Frameworks serve the purpose of **abstracting away browser inconsistencies**, providing a **richer API for development** and tools for **automation testing**. [Hybrids](https://hybrids.js.org/) accomplishes all this in a small 19.6kb (6.3kb gzipped) plus some for browser compatibility.

![Hybrids Browser Support](https://saucelabs.com/browser-matrix/hybrids.svg)

## Polyfills (Browser support)

To achieve this level of browser support with a modern web standard such as web components a polyfill. There are additional challenges such as CSS scoping that are essential for true web components. Hybrids integrates conditional shims and polyfills to handle this as best as it can.

## Testing (Automation)

I've found leveraging Hybrids, Karma and Jasmine can lead to some really clean automation tests. Hybrids offers an importable `html` helpers, which is the same helper it uses under the hood for its own testing and base functionality. So long as you pay close attention to when you need to target a [shadowRoot](https://developer.mozilla.org/en-US/docs/Web/API/Element/shadowRoot) rendering tests become easy with standard DOM methods to manipulate and access the details of your component.

``` javascript
it('renders logo with src and alt', () => {
  return renderComponent(html`<my-component></my-component>`).then(component => {
    let img = component.shadowRoot.querySelector('[data-test-id=componentImg]')
    expect(img.getAttribute('src')).toEqual('foo.png')
    expect(img.getAttribute('alt')).toEqual('foo')
  })
})
```

## Bundling

### Parcel

Initially I had great success bundling together Hybrids with [Parcel](https://parceljs.org/). It was as simple as pointing parcel to my html index.

However, Parcel is built for websites rather than consumable libraries. Thus I moved on to Webpack.

### Webpack

Assuming you have a `src/index.js` file that imports a component it's pretty simple to get started. I unfortunately cannot include a reference to the closed source repository here but it should get the idea across for a base webpack configuration. This config also supports JS files that [importing CSS into components which Hybrids supports](https://hybrids.js.org/template-engine/styling#css-stylesheet).

``` javascript
// ./webpack.config.js
const path = require('path');

module.exports = function(env, argv) {
  return {
    context: path.resolve(__dirname),

    entry: path.resolve(__dirname, 'src/index.js'),
    output: {
      path: path.resolve(__dirname, 'dist'),
      filename: argv.mode === 'test' ? '[name].js' : 'index.js',
    },

    module: {
      rules: [
        {
          // Inline/Component CSS
          test: /\.css$/,
          use: [ "css-loader" ],
        }, {
          // Javascript
          test: /\.m?js$/,
          exclude: /(node_modules)/,
          use: {
            loader: 'babel-loader',
            options: {
              presets: [
                [ '@babel/preset-env', { modules: false } ]
              ]
            }
          }
        }
      ]
    },
  };
};
```

## Component Structure

Finally, I landed on the this project structure which I hope you may be inspired by if you follow in these footsteps.

* src
  * components
    * component-name
      * index.js
      * view.js
      * test.js
      * style.css

---

Wish I could post the full project here and go into more detail. Even still, I hope this serves as a guiding light for those interested in exploring web components in their next project.
