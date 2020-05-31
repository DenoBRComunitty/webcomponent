# webcomponent

[![Build Status](https://travis-ci.org/mixpanel/webcomponent.svg?branch=master)](https://travis-ci.org/mixpanel/webcomponent)

[![Sauce Test Status](https://saucelabs.com/browser-matrix/mixpanel-webcomponents.svg)](https://saucelabs.com/u/mixpanel-webcomponents)

Lightweight utilities for constructing [Web Components](http://webcomponents.org/)

## Usage

Register web components by extending the `WebComponent` class instead of `HTMLElement`:

```javascript
import WebComponent from 'webcomponent';
class MyWidget extends WebComponent {
  connectedCallback() {
    // ...
  }

  get myprop() {
    // ...
  }
  // etc
}
customElements.define('my-widget', MyWidget);
```

`WebComponent` is a thin wrapper around `HTMLElement` which
- works out-of-the-box in Safari (see Babel issue ["Can't extend HTMLElement in Safari"](https://phabricator.babeljs.io/T1548))
- works out-of-the-box with Babel 6's class inheritance, without the need for extra plugins (see Babel issue ["Native extends breaks HTMLELement, Array, and others"](https://github.com/babel/babel/issues/4480))
- provides some extra helper methods next to the standard [Element API](https://developer.mozilla.org/en-US/docs/Web/API/Element)

### Built-in helper methods
#### `getJSONAttribute(attrName [, errorHandler])`
Parse an attribute which has been serialized as JSON, e.g.,
```html
<my-widget data-magic-numbers="[1,2,3]">
```
```javascript
this.getJSONAttribute('data-magic-numbers') // [1, 2, 3]
```
If no `errorHandler` is passed, JSON-parsing errors will result in `null` being returned.

#### `getNumberAttribute(attrName)`
Parse a numeric attribute, e.g.,
```html
<my-widget-list num-widgets="15">
```
```javascript
this.getNumberAttribute('num-widgets') // 15
```
Non-numeric values will return `null`.

#### `isAttributeEnabled(attrName)`
Check whether a boolean-like attribute is 'enabled', taking into account usages such as:
```html
<my-widget awesome="true">     <!-- enabled -->
<my-widget awesome>            <!-- enabled -->
<my-widget awesome="awesome">  <!-- enabled -->
<my-widget awesome="false">    <!-- disabled -->
<my-widget>                    <!-- disabled -->
```

## License

MIT - https://github.com/mixpanel/webcomponent/
