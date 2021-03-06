---
title: Rule array-bracket-spacing
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow or enforce spaces inside of brackets. (array-bracket-spacing)

A number of style guides require or disallow spaces between array brackets. This rule
applies to both array literals and destructuring assignment (EcmaScript 6) using arrays.

```js
var arr = [ 'foo', 'bar' ];
var [ x, y ] = z;

var arr = ['foo', 'bar'];
var [x,y] = z;
```

## Rule Details

This rule aims to maintain consistency around the spacing inside of array brackets, either by disallowing
spaces inside of brackets between the brackets and other tokens or enforcing spaces. Brackets that are
separated from the adjacent value by a new line are excepted from this rule, as this is a common pattern.
  Object literals that are used as the first or last element in an array are also ignored.

### Options

There are two options for this rule:

* `"always"` enforces a space inside of array brackets
* `"never"` enforces no space inside of array brackets (default)

Depending on your coding conventions, you can choose either option by specifying it in your configuration:

```json
"array-bracket-spacing": [2, "always"]
```

#### never

When `"never"` is set, the following patterns are considered warnings:

```js
var arr = [ 'foo', 'bar' ];
var arr = ['foo', 'bar' ];
var arr = [ ['foo'], 'bar'];
var arr = [[ 'foo' ], 'bar'];
var arr = ['foo',
  'bar'
];
var [ x, y ] = z;
var [ x,y ] = z;
var [ x, ...y ] = z;
var [ ,,x, ] = z;
```

The following patterns are not warnings:

```js
// When options are [2, "never"]
var arr = [];
var arr = ['foo', 'bar', 'baz'];
var arr = [['foo'], 'bar', 'baz'];
var arr = [
  'foo',
  'bar',
  'baz'
];
var arr = [
  'foo',
  'bar'];

var [x, y] = z;
var [x,y] = z;
var [x, ...y] = z;
var [,,x,] = z;
```

#### always

When `"always"` is used, the following patterns are considered warnings:

```js
var arr = ['foo', 'bar'];
var arr = ['foo', 'bar' ];
var arr = [ ['foo'], 'bar' ];
var arr = ['foo',
  'bar'
];
var arr = [
  'foo',
  'bar'];

var [x, y] = z;
var [x,y] = z;
var [x, ...y] = z;
var [,,x,] = z;
```

The following patterns are not warnings:

```js
var arr = [];
var arr = [ 'foo', 'bar', 'baz' ];
var arr = [ [ 'foo' ], 'bar', 'baz' ];
var arr = [
  'foo',
  'bar',
  'baz'
];

var [ x, y ] = z;
var [ x,y ] = z;
var [ x, ...y ] = z;
var [ ,,x, ] = z;
```

Note that `"always"` has a special case where `{}` and `[]` are not considered warnings.

#### Exceptions

An object literal may be used as a third array item to specify spacing exceptions. These exceptions work in the context of the first option. That is, if `"always"` is set to enforce spacing and an exception is set to `false`, it will disallow spacing for cases matching the exception. Likewise, if `"never"` is set to disallow spacing and an exception is set to `true`, it will enforce spacing for cases matching the exception.

You can add exceptions like so:

In case of `"always"` option, set an exception to `false` to enable it:

```json
"array-bracket-spacing": [2, "always", {
  "singleValue": false,
  "objectsInArrays": false,
  "arraysInArrays": false
}]
```

In case of `"never"` option, set an exception to `true` to enable it:

```json
"array-bracket-spacing": [2, "never", {
  "singleValue": true,
  "objectsInArrays": true,
  "arraysInArrays": true
}]
```

The following exceptions are available:

* `singleValue` sets the spacing of a single value inside of square brackets of an array.
* `objectsInArrays` sets the spacings between the curly braces and square brackets of object literals that are the first or last element in an array.
* `arraysInArrays` sets the spacing between the square brackets of array literals that are the first or last element in an array.

In each of the following examples, the `"always"` option is assumed.

When `"singleValue"` is set to `false`, the following patterns are considered warnings:

```js
var foo = [ 'foo' ];
var foo = [ 'foo'];
var foo = ['foo' ];
var foo = [ 1 ];
var foo = [ 1];
var foo = [1 ];
var foo = [ [ 1, 2 ] ];
var foo = [ { 'foo': 'bar' } ];
```

The following patterns are not warnings:

```js
var foo = ['foo'];
var foo = [1];
var foo = [[ 1, 1 ]];
var foo = [{ 'foo': 'bar' }];
```

When `"objectsInArrays"` is set to `false`, the following patterns are considered warnings:

```js
var arr = [ { 'foo': 'bar' } ];
var arr = [ {
  'foo': 'bar'
} ]
```

The following patterns are not warnings:

```js
var arr = [{ 'foo': 'bar' }];
var arr = [{
  'foo': 'bar'
}];
```

When `"arraysInArrays"` is set to `false`, the following patterns are considered warnings:

```js
var arr = [ [ 1, 2 ], 2, 3, 4 ];
var arr = [ [ 1, 2 ], 2, [ 3, 4 ] ];
```

The following patterns are not warnings:

```js
var arr = [[ 1, 2 ], 2, 3, 4 ];
var arr = [[ 1, 2 ], 2, [ 3, 4 ]];
```

## When Not To Use It

You can turn this rule off if you are not concerned with the consistency of spacing between array brackets.

## Related Rules

* [space-in-parens](space-in-parens)
* [object-curly-spacing](object-curly-spacing)

## Version

This rule was introduced in ESLint 0.24.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/array-bracket-spacing.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/array-bracket-spacing.md)
