Class 02: Sorting Data
===

Create a sortable table of contacts, implemented using the `.sort` array method and following a common pattern for sorting dynamically based on a chosen field.

## Agenda

1. Questions and Review
1. Code Cooking
    1. ternary expression
    1. `.toLocaleString()`
    1. `.sort`
1. Live Demo PhotoGallery
    1. Sort on field name pattern
1. Mob Build Photo Gallery
1. Solo Build Photo Gallery

## Lab

repo: `sorted-contacts`

## Key Concepts

* ternary expression
* `.toLocaleString()`
* `.sort`
* Sort on field name pattern

### Ternary Expression

Instead of:

```js
let active = ''
if(contact.isActive) {
    active = 'Yes';
}
else {
    active = 'No';
}
```

You can write:

```js
const active = contact.isActive ? 'Yes' : 'No';
```

### `.toLocaleString()`

Use `.toLocaleString()` to format numbers and dates
using the system settings of the users browsers

### Array `.sort` method

Sorts the current array (and returns the current array). Instead of controlling the sorting algorithm, we need to tell JavaScript for any two items in the array, how do they compare relatively to one another:

```js
const sortedContacts = contacts.sort((a, b) => {
    if(a.name === b.name) {
        return 0;
    }
    if(a.name > b.name) {
        return 1;
    }
    return -1;
});
```

### Sort on Field Name Pattern

Use a dynamic object property to allow the field
to be sorted on to be supplied as a function argument:

```js
const sortedContacts = contacts.sort((a, b) => {
    if(a[sortField] === b[sortField]) {
        return 0;
    }
    if(a[sortField] > b[sortField]) {
        return 1;
    }
    return -1;
});
```