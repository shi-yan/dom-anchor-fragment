Fragment Anchor
===============

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](http://opensource.org/licenses/MIT)
[![NPM Package](https://img.shields.io/npm/v/dom-anchor-fragment.svg)](https://www.npmjs.com/package/dom-anchor-fragment)
[![Build Status](https://travis-ci.org/hypothesis/dom-anchor-fragment.svg?branch=master)](https://travis-ci.org/hypothesis/dom-anchor-fragment)
[![Coverage Status](https://coveralls.io/repos/tilgovi/dom-anchor-fragment/badge.svg?branch=master)](https://coveralls.io/r/hypothesis/dom-anchor-fragment?branch=master)

This library offers conversion between a DOM `Range` instance and a fragment
selector as defined by the Web Annotation Data Model.

For more information on `Range` see
[the documentation](https://developer.mozilla.org/en-US/docs/Web/API/Range).

For more information on the fragment selector see
[the specification](http://www.w3.org/TR/annotation-model/#fragment-selector).

Installation
============

There are a few different ways to include the library.

With a CommonJS bundler to `require('dom-anchor-fragment')`:

    npm install dom-anchor-fragment

With a script tag, include one of the scripts from the `dist` directory.

With AMD loaders, these scripts should also work.

Usage
=====

The module exposes a single constructor function, `FragmentAnchor`.

## `new FragmentAnchor(id)`

The `id` argument is required, but it is not necessary for any node to exist
in the DOM with a matching `id` property. Only when this anchor is converted
to a `Range` will the instance check the validity of the identifier.

## `FragmentAnchor.fromRange(range)`

Provided with an existing `Range` instance this will return a `FragmentAnchor`
instance that stores the `id` attribute of the common ancestor container. If
the common ancestor container has no `id` attribute then the anchor will take
the `id` of its first ancestor that does have a non-empty `id` attribute.

If no element can be found in the ancestry of the `Range` that has a non-empty
`id` attribute then this function will raise an exception.

## `FragmentAnchor.fromSelector(selector)`

Provided with an `Object` containing a `value` key that has a `String` value
this will return a `FragmentAnchor` that refers to that value.

## `FragmentAnchor.prototype.toRange()`

This method returns a `Range` object that selects the contents of the element
identified by the anchor.

## `FragmentAnchor.prototype.toSelector()`

This method returns an `Object` that has keys `type` and `value` where `type`
is `"FragmentSelector"` and the value is the `id` referred to be the anchor.
