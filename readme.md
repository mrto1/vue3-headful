# vue3-headful

vue3-headful allows to set the title and several meta tags of your document from any Vue.js view in any Vue3 App.
vue3-headful is a tiny wrapper around [Headful](https://github.com/troxler/headful), a generic library to set meta tags with JavaScript.

## Install

```
npm i vue3-headful
```

## Usage

Register the component:

```js
import Vue from 'vue';
import vue3Headful from 'vue3-headful';

Vue.component('vue3-headful', vue3Headful);

new Vue({
    // your configuration
});
```

And then use the `vue3-headful` component in every of your views:

```html
<template>
    <div>
        <vue3-headful
            title="Title from vue-headful"
            description="Description from vue-headful"
        />
    </div>
</template>
```

## Documentation

vue3-headful is only a wrapper around [Headful](https://github.com/troxler/headful) and by itself does not do that much.
vue3-headful supports all the [head properties that are supported by Headful](https://github.com/mrto1/vue3-headful#documentation).
You can find a non-complete list of head properties in the following example:

```html
<vue3-headful
    title=""
    description=""
    keywords=""
    image=""
    lang=""
    ogLocale=""
    url=""
/>
```

If there are any other head properties or attributes you want to set, you can use `html` (for arbitrary elements in the whole document) or `head` (for elements within `<head>`) as follows.
The selectors can be any valid CSS selector.

```html
<vue-headful
    :html="{
        body: {id: 'aPageId'},
        h1: {'data-foo': 'bar'},
    }"
    :head="{
        'meta[charset]': {charset: 'utf-8'},
    }"
/>

<!-- Results in:
<head>
    <meta charset="utf-8">
</head>
<body id="aPageId">
<h1 data-foo="bar"></h1>
-->
```

If you want to **remove a previously defined attribute from an element**, you can set it to `null` as in the example below:

```html
<vue-headful :title="null"/>
<!-- Results in:
<title></title>
<meta itemprop="name">
<meta property="og:title">
<meta name="twitter:title">
-->
```

Note that neither Headful nor vue3-headful add missing HTML elements, they only add attribute values.
So it is important that you add everything that you want to have populated in your HTML first.
For example, to specify the title and description you have to prepare the HTML as follows.

```html
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <meta itemprop="name">
    <meta property="og:title">
    <meta name="twitter:title">
    <meta name="description"/>
    <meta itemprop="description">
    <meta property="og:description">
    <meta name="twitter:description">
</head>
<body>
<!-- ... -->
</body>
</html>
```

vue3-headful also supports dynamic properties (e.g. `v-bind:title="variableName"` or `:title="variableName"`) and adds watchers to everything.
That means you can also set head properties asynchronously, for example after an API request.

```html
<template>
    <vue3-headful
        :title="title"
        description="Static description"
    />
</template>

<script>
    export default {
        data() {
            return {
                title: 'Dynamic title',
            };
        },
        mounted() {
            // dummy async operation to show watcher on properties
            setTimeout(() => {
                this.title = 'Dynamic async title';
            }, 3000);
        },
    };
</script>
```

Also see the non-complete list of meta tags and other head properties you can define using vue3-headful:

* `<html lang>`
* `<title>`
* `<meta name="description">`
* `<meta itemprop="description">`
* `<meta property="og:description">`
* `<meta name="twitter:description">`
* `<meta name="keywords">`
* `<meta itemprop="image">`
* `<meta property="og:image">`
* `<meta name="twitter:image">`
* `<meta property="og:locale">`
* `<link rel="canonical">`
* `<meta property="og:url">`
* `<meta name="twitter:url">`

For more information on everything you can put into `<head>`, have a look at <https://gethead.info/>.


## Compatibility

vue3-headful works with every current and most reasonably old web browsers.
