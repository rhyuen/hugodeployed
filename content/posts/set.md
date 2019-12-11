---
title: "new Set(...[{one}, {two}])"
date: 2019-12-10T07:02:21-08:00
draft: false
---

I was playing around with `Set` and Objects and wanted to record some behaviour that I noticed.

```javascript

const array = [1, 2, 2, 3, 4, 5];
const arraySet = new Set(array);
//EXPECTED arraySet = Set(1, 2, 3, 4, 5)
//An extra 2 is removed.

const arrayOfObjects = [
    {name: "two", value: 2}, 
    {name: "two", value: 2}, 
    {name: "three", value: 3}, 
    {name: "four", value: 4}
];
const arrayOfObjectsSet = new Set(arrayOfObjects);
/*EXPECTED arrayOfObjectsSet = Set( 
    {name: "two", value: 2}, 
    {name: "three", value: 3}, 
    {name: "four", value: 4}
)
*/
```

It seems the Set() constructor doesn't do anything for objects.  I recall reading in the MDN Docs something that says that.  However, I only really paid attention to it after I tried out `new Set()` for both `Number` and `Object`.