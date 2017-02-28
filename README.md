# Vue Sidebar Component

[![npm version][npm-v-img]][npm-url]
[![npm download][npm-dl-img]][npm-url]

> Intellectual property of [Oneway.mobi](http://www.oneway.mobi/)

#### Notice
This component is not meant to meet all the business requirements  
so diving into `src/` to make it fits your needs is highly recommended

#### Example
See [here](https://kenberkeley.github.io/vue-sidebar-component/example.html), source in [`example.html`](./example.html)
> Suggest inspecting it with [devtools](https://github.com/vuejs/vue-devtools)

#### Requirement
* Vue 1.x
* Vue Router 0.7.x
* jQuery + BootStrap 3.x + Font Awesome 4.x (available globally)

#### Installation
`npm i vue-sidebar-component -S`

> alternatively: `<script src="dist/vue-sidebar-component.min.js"></script>`  
> which exposes **`VueSidebar`** as a global variable

#### Usage

```
<sidebar main-title="Sidebar" sub-title="Example" :routes="routes"></sidebar>

props: {
  mainTitle: String,
  subTitle: String,
  routes: { type: Object, required: true }
}
```

`routes` configuration example (more in [`example.html`](./example.html)):

```
'/': {
  title: 'Home',
  icon: 'fa fa-home',
  showInSidebar: true,
  component: {
    template: '<div>Home</div>'
  }
}
```

#### Build

`npm run build`

#### LICENSE

MIT

[npm-url]: https://www.npmjs.com/package/vue-sidebar-component
[npm-v-img]: http://img.shields.io/npm/v/vue-sidebar-component.svg
[npm-dl-img]: http://img.shields.io/npm/dm/vue-sidebar-component.svg
