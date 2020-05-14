# Boiled Page sidenav singleton

Sidenav SCSS singleton for Boiled Page frontend framework. It is intended to create a side navigation with collapsible subnavigations.

## Install

Place `_sidenav.scss` file to `/assets/css/singletons` directory, and add its path to singleton block in `assets/css/app.scss` file. You will also need to add accordion script to make it working properly.

- Accordion script: <https://www.github.com/abelbrencsan/boiled-page-accordion-script>

## Usage

### Classes

Class name | Description | Example
---------- | ----------- | -------
`sidenav` | Applies side navigation. | `<ul class="sidenav"></ul>`

### Examples

#### Example 1

The following example shows a side navigation with collapsible subnavigations. `data-sidenav-subnav` attributes are used for accordion script.

```html
<nav class="sidenav">
  <ul>
    <li>
      <a href="#">Home</a>
    </li>
    <li data-sidenav-subnav>
      <button type="button" data-sidenav-subnav-trigger>Services</button>
      <ul data-sidenav-subnav-element>
        <li>
          <a href="#">Web design</a>
        </li>
        <li>
          <a href="#">Web development</a>
        </li>
        <li>
          <a href="#">Graphic design</a>
        </li>
      </ul>
    </li>
    <li data-sidenav-subnav>
      <button type="button" data-sidenav-subnav-trigger>Products</button>
      <ul data-sidenav-subnav-element>
        <li>
          <a href="#">CMS systems</a>
        </li>
        <li>
          <a href="#">CRM systems</a>
        </li>
        <li>
          <a href="#">Servers</a>
        </li>
      </ul>
    </li>
    <li>
      <a href="#">Contact</a>
    </li>
  </ul>
</nav>
```

Add `sidenav` property to `app` object in `assets/js/app.js`.

```js
sidenav: null
```

Place the following code inside `assets/js/app.js` to initalize element with `data-sidenav-subnav` attribute as an accordion.

```js
// Initialize sidenav subnavigations
app.sidenav = new Accordion({
  items: Array.prototype.map.call(document.querySelectorAll('[data-sidenav-subnav]'), function(obj) {
    return {
      trigger: obj.querySelector('[data-sidenav-subnav-trigger]'),
      element: obj.querySelector('[data-sidenav-subnav-element]')
    };
  }),
});
app.sidenav.init();
```

Place the following code inside the `onBreakpointChange` function in `assets/js/app.js` to recalculate maximum height of opened subnavigation item's element when breakpoint changes.

```js
// Recalculate maximum height of opened sidenav subnavigation item's element
app.sidenav.recalcHeight();
```
