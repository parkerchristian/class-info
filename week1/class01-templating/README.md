Class 01: JavaScript Templates
===

Use JavaScript templates to render list of data dynamically

## Agenda

1. Kickoff and Class Expectations
1. Code Cooking
    1. Template Literals
    1. `<template>` Element
    1. Arrow Function
    1. `.forEach`
1. Live Demo PhotoGallery
    1. DDD
    1. Template Functions
1. Mob Build PhotoGallery
1. Solo Build PhotoGallery

## Key Concepts

* Template Literals
* `<template>` Element
* Array `.forEach` method
* Template Function Recipe
* Design-Driven Development Recipe

### JavaScript Template Literals

Using templates for dynamic html allows developers to simultaneously indicate what data should be place and where it should be place in the html.

```js
const place = 'world';
const html = /*html*/`
    <p>Hello <span>${place}</span></p>
`;
```

### `<template>` element

Special DOM element that can have it's `.innerHTML` property set and
the resulting created DOM can be accessed via its `.content` property

```js
const template = document.createElement('template');
template.innerHTML = html;
const dom = template.content;
```

### Template function

A function that combines the above concepts by taking data and
returning the created DOM. It follows a standard recipe:

```js
// 1) Define a function that describes the type of 
// template being created:
function makeThingTemplate(data) {
    // 1) Create HTML string via template literal
    const html = /*html*/`
        <p>template literal for ${data.property}</p>
    `;
    // 2) Create a <template> element and assign its .innerHTML property
    const template = document.createElement('template');
    template.innerHTML = html;
    // 3) Return the dom fragment via the .content property:
    return template.content;
}
```

### Array `.forEach` method

Act on each element (item) of an array without having to specify
a `for` loop.

```js
const list = document.getElementById('list');
images.forEach(function(image) {
    const dom = makeImageTemplate(image);
    list.appendChild(dom);
});
```

### Design-Driven Development

A process for creating dynamically rendered HTML via template.

The recipe is as follows:

1. Statically design one or more instances of the final html
and css you would like to create
2. Create a test that calls a template function and asserts
that the result is the same as the static html
3. Make the test pass by returning the exact same static html 
from the template function
4. Begin to replace the static html in the template function with 
object properties passed into the template function
5. When the template is fully dynamic and the test passes, 
you now have a tested, usable template function 



