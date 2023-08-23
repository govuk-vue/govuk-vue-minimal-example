# govuk-vue-minimal-example

This is a minimal example of how to start using [GOV.UK Vue](https://github.com/govuk-vue/govuk-vue).

A live demo is available at [govuk-vue-minimal-example.github.io](https://govuk-vue-minimal-example.github.io).

### Running the app locally

[Clone this repo](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) then
install dependencies:

```sh
npm install
```

Start the dev server:

```sh
npm run dev
```

This server will hot reload, so any changes you make will be shown instantly.

### Compile and minify for production

```sh
npm run build
```

Your app will be compiled to static files in the `dist` directory.

## How this project was set up

This project was set up using the following steps.

### Create a new Vue 3 project using `create-vue`

```sh
npm create vue@3
```

For this example all optional add-ons, including TypeScript support, were disabled. You can enable these if you need them.

### Install dependencies

```sh
cd your-project-name
npm install
```

### Remove unneeded files

`create-vue` creates some files we don't need. Delete `src/assets/base.css`, `src/assets/logo.svg` and the `components` directory.

### Install GOV.UK Vue

```
npm install govuk-vue
```

Import `GovUkVue` in `main.js`:

```js
import { GovUkVue } from 'govuk-vue'
```

Add the `GovUkVue` plugin to the app. Change the last line of `main.js` from:

```js
createApp(App).mount('#app')
```

to:

```js
createApp(App).use(GovUkVue).mount('#app')
```

In `index.html`, replace `<head>` with the following:

```html
<head>
  <meta charset="utf-8">
  <title>GOV.UK Vue Minimal Example</title>
  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
  <meta name="theme-color" content="#0b0c0c">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <link rel="shortcut icon" sizes="16x16 32x32 48x48" href="/assets/images/favicon.ico" type="image/x-icon">
  <link rel="mask-icon" href="/assets/images/govuk-mask-icon.svg" color="#0b0c0c">
  <link rel="apple-touch-icon" sizes="180x180" href="/assets/images/govuk-apple-touch-icon-180x180.png">
  <link rel="apple-touch-icon" sizes="167x167" href="/assets/images/govuk-apple-touch-icon-167x167.png">
  <link rel="apple-touch-icon" sizes="152x152" href="/assets/images/govuk-apple-touch-icon-152x152.png">
  <link rel="apple-touch-icon" href="/assets/images/govuk-apple-touch-icon.png">
</head>
```

Add the `govuk-template` class to `<html>` and `govuk-template__body js-enabled` to `<body>`.

### Install Sass and import GOV.UK Frontend styles

Install GOV.UK Frontend:

```sh
npm install govuk-frontend --save-dev
```

Sass is required to compile the GOV.UK Frontend styles:

```sh
npm install sass --save-dev
```

Rename `src/assets/main.css` to `main.scss` and update the import at the top of `main.js`.

Update content of `main.scss` to:

```scss
@import "node_modules/govuk-frontend/govuk/all";
```

Delete everything else in `main.scss`

### Copy GOV.UK Frontend static assets

GOV.UK Frontend includes the GDS Transport font and some images (like the favicon and the crest in the footer). By default it looks
for these in the `/assets/` path under the server root. We need to make these assets available under this
path, so we use the [vite-plugin-static-copy](https://www.npmjs.com/package/vite-plugin-static-copy) plugin to
automatically copy these files.

Install the plugin:

```sh
npm install vite-plugin-static-copy --save-dev
```

In `vite.config.js`, import the plugin:

```js
import { viteStaticCopy } from 'vite-plugin-static-copy'
```

and add the following to the `plugins` option:

```js
viteStaticCopy({
  targets: [
    {
      src: 'node_modules/govuk-frontend/govuk/assets/*',
      dest: 'assets'
    }
  ]
})
```

### Add content to App.vue

You'll now be able to use GOV.UK Vue components anywhere in your app. The plugin makes all the components available globally,
so you don't need to import components individually.

`App.vue` is the entry point of our app. See `src/App.vue` for an example of how to set up a standard GOV.UK page using 
`GvHeader`, `GvFooter` and GOV.UK layout classes.

Run the app with `npm run dev`.