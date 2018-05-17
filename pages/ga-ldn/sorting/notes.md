## Sorting

First sort fish.

Everything looks fine.

Now sort newFish. Why does this not work as expected?

## The Javascript default sort function

It's not very good. It sorts everything according to ASCII position. So Capital Letters always come first!

## Compare functions

We can provide Javascript with a more subtle way of comparing elements.

We do this one pair at a time. The compare function should return:

- a positive number if `a` and `b` need reordering
- a negative number if `a` and `b` are already in the right order
- 0 if `a` and `b` can be considered identical for sorting purposes.

Check with the students:
If `a` is bigger than `b` is the sort order right or wrong? A: WRONG

Do we need a positive or a negative number? A: POSITIVE

If `a` is smaller than `b` is the sort order right or wrong? A: RIGHT

Do we need a positive or a negative number? A: NEGATIVE

Can we think of a simple bit of maths we can do that fits this bill? A: Subtraction!

### Sorting numbers

Together we provide a function to sort the `numbers` array.

Write the numbers on the board and compare the elements pairwise. How can we write a comparison function?

```
numbers.sort((a, b) => a - b)
```

Why does this work?

### Sorting case insensitive

Show the students the fact that comparison between strings does 'the right thing' within case:

```
> "rob" < "mike"
false
> "rob" < "zebedee"
true
```

```
moreFish.sort((a, b) => {
	if(a.toUpperCase() > b.toUpperCase()) return 1;
	if(a.toUpperCase() < b.toUpperCase()) return -1;
	return 0
})
```

### Why Javascript sort is not ideal
- Sorts "in-place"!
- Hard to work out, from looking at the comparison function, what it's going to do.
- We'll look at a better way in a bit.

## Filtering
This is where we arrive at some very light regex.

`Array.filter` calls a single-argument function for each element. Should return true or false.

```
fish.filter(f => f < 'Place');
numbers.filter(x => x > 5);
numbers.filter(x => [2, 8, 20].includes(x));
```

# Lodash

Lodash is a library (not a framework!) with some useful helper functions.

> Lodash makes JavaScript easier by taking the hassle out of working with arrays, numbers, objects, strings, etc.
Lodash’s modular methods are great for:
> - Iterating arrays, objects, & strings
> - Manipulating & testing values
> - ...something else which I'm not going into

### Lodash sort

```
_.orderBy(fish);
```
This is a terrible syntax, when you're using the default sorting.
And it doesn't beat the problem with `moreFish` by default.

But,
```
_.orderBy(moreFish, x => x.toUpperCase())
```

But we can do some relatively neat stuff with objects which has a better readability:
```
_.orderBy(fishData, 'lifespan')
_.orderBy(fishData, 'lifespan', 'desc')
_.orderBy(fishData, ['deepSea', 'lifespan'])
```

I don't understand *exactly* what the second argument to `orderBy` does and the docs are pretty hard to understand.

For example, WTF is this doing?:

```
> moreFish
["Salmon", "Herring", "haddock", "plaice", "sole", "Shark"]
> _.sortBy(moreFish, [2, 0, 1, 5, 3, 4])
["Shark", "plaice", "haddock", "Salmon", "sole", "Herring"]
```

### Lodash filter
It can work very much like vanilla JS filter:
```
_.filter(numbers, x => x > 8)
```

But there's some nice syntactic sugar as well:

```
