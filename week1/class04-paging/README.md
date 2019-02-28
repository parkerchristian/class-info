Class 04: Paging
===

Create a pageable pokedex, implemented using the `.slice` array method and following a common pattern for paging through data.

## Agenda

1. Questions and Review
1. Code Cooking
    1. `.slice`
1. Live Demo Pokedex Paging
    1. Page, PerPage, Total Pages
1. Mob Build Photo Gallery
1. Solo Build Photo Gallery

## Lab

repo: `pokedex`

## Key Concepts

* `.slice`
* Paging: Page, PerPage, Total Pages

### Array `.slice` method

Returns a new array that is based on a portion of an array existing array, based on a start and end index.

Start index: *inclusive*
End index: *exclusive*

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const firstThree = numbers.slice(0, 3);
console.log(firstThree);
// [ 1, 2, 3 ]

const lastSeven = numbers.slice(3);
console.log(lastSeven);
```

Can be used to copy an array:

```js
const copy = array.slice();
```

See [docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) for full details

### Paging Patterns

Paging typically requires three pieces of information:

1. Current Page
1. Results Per Page
1. Total size of Results (The UI wants this)

#### Calculate the "Slice"

Because slicing is not dependent on the content of the array, the page 
slicing function can work for any array

```js
export default function pageArray(array, pagingOptions) {
    const page = pagingOptions.page;
    const perPage = pagingOptions.perPage;
    const startIndex = (page - 1) * perPage;
    const endIndex = startIndex + perPage;

    return array.slice(startIndex, endIndex);
}
```

#### Calculate Total Pages

The UI often needs to show the Total Pages

```js
const totalPages = Math.ceil(totalCount / perPage);
```

Disable UI when out of range. Can't go less than first page, or more than total pages.