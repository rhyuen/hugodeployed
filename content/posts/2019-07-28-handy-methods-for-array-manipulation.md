---
layout: blog
title: Handy Methods for Array Manipulation.
date: 2019-07-29T02:23:24.151Z
thumbnail: /images/uploads/scieworld.jpg
rating: 5
---
1. Exponents
```javascript

const result = Math.pow(base, exponent);
```
2. Absolute Value

```javascript
const absoluteValue = Math.abs(negativeNumber);
```

3. Putting things at the front of the array.
```javascript
let mutableArray = ["apple", "orange", "lemon", "lime"];
mutableArray.unshift();

//mutuableArray now contains ["orange", "lemon", "lime"];

let prependArray = ["batman", "superman", "wonder woman"];
prependArray.shift("Green Arrow");

// prependArray now contains ["green arrow", "batman", "superman", "wonder woman"]
