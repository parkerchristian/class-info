Class 02: Filtering Data
===

Create UIs that allow the user to filter a list of data. Implemented using the `.filter` array method and following a common pattern for allowing
multiple filters to be applied.

## Agenda

1. Career Service Kickoff and Expectations
1. Questions and Review
1. Code Cooking
    1. JavaScript Logic
    1. `.filter`
    1. Named Exports and Imports
    1. Calling callback functions
1. Live Demo PhotoGallery
    1. Filtered Properties Recipe
    1. Component Module Pattern
1. Mob Build Photo Gallery
1. Solo Build Photo Gallery

## Lab

repo: `filtered-photo-gallery`

## Key Concepts

* Refactoring - names and single-responsibility.
* JavaScript Logic
    * "truthy" and "false"
    * Logical Operators `&&` and `||` and `!`
* Array `.filter` Method
* Named Exports and Imports
* Calling Callback Functions
* Filtered Properties Recipe
* Component Module Pattern

### `truthy` and `falsey`

Input Type | Result
---|---
Undefined	|false
Null	|false
Boolean	|The result equals the input argument (no conversion).
Number	|The result is false if the argument is +0, -0, or NaN; otherwise the result is true.
String	|The result is false if the argument is the empty string (its length is zero); otherwise the result is true.
Object	|true

### Logical Operators

Operator | Meaning | Notes
---|---|---
`&&` | **and** | both things must be truthy
`||` | **or** | one of the two things must be truthy
`!` | **not** | negation, true becomes false, false becomes true

Note: JavaScript will *short-circuit* once the logical operator cannot yeild a different result. For example, with `false && testAThing()`, `testAThing` will _never_ be called because the first expression has already made it impossible for a `true` to result.

### Array `.filter` method

Create a new "filtered" array by testing each item of an array and
returning "truthy" if item should be included, or "falsey" if not.

```js
const filteredImages = images.filter(function(image) {
    return image.keyword === 'cute';
});
```

### Filtered Properties Recipe

When building filters that apply to an arbitrary number of properties, use the following recipe.

1. Use a logical operators to test if either: 
    1. the filter does not exist, or
    1. the item matches (can be comparison operator) the filter
    ```js
    const hasKeyword = !filter.keyword || item.keyword === filter.keyword;
    ```
1. Test each filter property and assigned to `variable`, return the 
logical "and" of all filters:
    ```js
    function filterImages(images, filter) {
        const filteredImages = images.filter(function(image) {
            const hasKeyword = !filter.keyword || item.keyword === filter.keyword;

            const hasHorns = !filter.horns || item.horns >= filter.horns;

            return hasKeyword && hasHorns;
        });
    }
    ```

### Named Exports and Imports

Specify more than one thing that should be exported from a module. Requires 
a specific syntax to import. Can be mixed with `export default`

```js
// module-one.js:
export function makeTemplate() {
    // ...
}

export default function loadImages(images) {
    //...
}
```

```js
// module-two.js:
import { makeTemplate } from './module-one.js';
```

```js
// module-three.js:
import loadImages from './module-one.js';
```

### Component Module Pattern

Have each logical area of the UI controlled by one module. The main `index.js`
module sits at the top and controls all the component modules.

Each of those modules 
is named based on what it renders, `images-component.js`, and
exports a default function that is prefixed with `load`, for example `loadImages`.

The load function receives:
1. Any data that is required
1. Any callbacks that are required (see next section)

The load function _may_ be callable multiple times to "refresh" data. Otherwise,
named exported function(s) can be provided for additional required behavior


### Calling Callback Function

We can create our own functions that accept callbacks. This can be used to notify
the caller of our function that some activity has occurred.

```js
const form = document.getElementById('form');

export function loadFilters(callback) {
    form.addEventListener('submit', function(event) {
        // normal form activity of gathering data
        // that generates an object
        // ...

        // call the caller back ("callback")
        callback(filter);
    })
}
```


