---
title: "Note about sort stable in JavaScript"
tags: [tech, english, javascript]
share-img: /img/javascript.jpg
---

# Question

What is the order of array `arr` after running this JavaScript code:

```
const arr = [
    { x: 1 },
    { x: 2 },
    { x: 3 },
    { x: 4 }
];
arr.sort((a, b) => 0);
```

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-2750437710821247"
     data-ad-slot="8905029259"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>

# Answer

JavaScript has a build in function `sort`, as described in [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort).

Syntax:

```
arr.sort([compareFunction])
```

This function takes a function `compareFunction` as parameter. From the document:

**compareFunction** (optional)
> Specifies a function that defines the sort order. If omitted, the array is sorted according to each character's Unicode code point value, according to the string conversion of each element.

The compare function has following form:

```
function compare(a, b) {
  if (a is less than b by some ordering criterion) {
    return -1;
  }
  if (a is greater than b by the ordering criterion) {
    return 1;
  }
  // a must be equal to b
  return 0;
}
```

This is straightforward, it takes two parameters (from array[0], array[1]; then array[1], array[2] and so on), then compares this two values and swap those two elements depends on return value is `1`, `-1` or `0`.

The problem is with `0` value. As from comment of the above source code:

>   // a must be equal to b

Back to the question, most of programmers may think the `arr` order is unchanged because we return 0 for `compareFunction`. But it's not neccessary for all cases. There is a chance that `arr` is reordered after running `arr.sort((a, b) => 0)`. This may cause unexpected behaviour.

Actually, JavaScript `sort` function is `not neccessary stable`. This means that if we return 0, the order of two elements may be changed if they are not equal.

From the document:

> If compareFunction(a, b) returns 0, leave a and b unchanged with respect to each other, but sorted with respect to all different elements. Note: the ECMAscript standard does not guarantee this behaviour, and thus not all browsers (e.g. Mozilla versions dating back to at least 2003) respect this.

This means, `sort` function may reorder the source array if we return 0. So while implementing with `sort`, we must be careful if `return 0` for `compareFunction`.

There are also libraries that provide `stable sort` method, for example [lodash sortBy method](https://lodash.com/docs/4.17.10#sortBy)

As from their document:

> Creates an array of elements, sorted in ascending order by the results of running each element in a collection thru each iteratee. This method performs a stable sort, that is, it preserves the original sort order of equal elements. The iteratees are invoked with one argument: (value).

So it performs a `stable sort`.

# Lesson learned

Always check if a sort function is stable or not while using it.

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-2750437710821247"
     data-ad-slot="8905029259"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>