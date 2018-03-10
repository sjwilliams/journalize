# journalize

A collection of functions useful for making prose reader friendly. Inspired by (and initially based on) Django's [`django.contrib.humanize`](https://docs.djangoproject.com/en/dev/ref/contrib/humanize/).

[![build status](https://img.shields.io/travis/rdmurphy/journalize/master.svg?style=flat-square)](https://travis-ci.org/rdmurphy/journalize)
[![Coveralls branch](https://img.shields.io/coveralls/rdmurphy/journalize/master.svg?style=flat-square)](https://coveralls.io/github/rdmurphy/journalize)
[![npm version](https://img.shields.io/npm/v/journalize.svg?style=flat-square)](https://www.npmjs.com/package/journalize)
[![npm](https://img.shields.io/npm/dm/journalize.svg?style=flat-square)](https://www.npmjs.com/package/journalize)

* [Why did you create this?](#why-did-you-create-this)
* [Installation](#installation)
* [API Docs](#api-docs)
* [What if I do want to use this in Nunjucks?](#what-if-i-do-want-to-use-this-in-nunjucks)
* [License](#license)

## Why did you create this?

I've always really appreciated the built-in functionality provided by Django's `humanize`, and I wanted to port it over to JavaScript/Node.js. Originally this was to be a [collection of custom filters](#what-if-i-do-want-to-use-this-in-nunjucks), but I think it could be just as useful as a generic library.

## Installation

```sh
npm install journalize

# or

yarn add journalize
```

`journalize` tries to support the many ways to load packages in the Node.js ecosystem.

If you use a module bundler like [Browserify](http://browserify.org) or [Webpack](http://webpack.github.io), a version of `journalize` is built to be compatible.

```js
const journalize = require('journalize');

// you can also reach in and grab specific functions
const intcomma = require('journalize').intcomma;
// or
const { intcomma } = require('journalize');
```

It also supports ES6 imports:

```js
import { intcomma } from 'journalize';

// or if you want the whole thing
import * as journalize from 'journalize';
```

## API Docs

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

* [apdate](#apdate)
* [apmonth](#apmonth)
* [apnumber](#apnumber)
* [apstate](#apstate)
* [aptime](#aptime)
* [capfirst](#capfirst)
* [intcomma](#intcomma)
* [intword](#intword)
* [ordinal](#ordinal)
* [pluralize](#pluralize)
* [postal](#postal)
* [yesno](#yesno)

### apdate

Returns an AP-formatted date string that corresponds with the supplied
Date. If an `input` is not passed, it will use the result of `new Date();`.

**Parameters**

* `date` **[Date](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date)?** JavaScript Date object, defaults to current date if
  not passed (optional, default `new Date()`)

**Examples**

```javascript
var journalize = require('journalize');

// Remember that JavaScript zero-indexes months!
journalize.apdate(new Date(2016, 10, 8));
// returns 'Nov. 8, 2016'

// Uses the current date if no parameter is passed
journalize.apdate();
// returns 'July 4, 2016' (pretend it is actually July 4, 2016)
```

Returns **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**

### apmonth

Returns an AP-formatted month string that corresponds with the supplied
Date. If an `input` is not passed, it will use the result of `new Date();`.

**Parameters**

* `date` **[Date](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date)?** JavaScript Date object, defaults to current date if
  not passed (optional, default `new Date()`)

**Examples**

```javascript
var journalize = require('journalize');

// Remember that JavaScript zero-indexes months!
journalize.apmonth(new Date(2016, 10, 8));
// returns 'Nov.'

// Uses the current date if no parameter is passed
journalize.apmonth();
// returns 'July' (pretend it is actually July)
```

Returns **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**

### apnumber

Converts an integer to string representation per AP style rules. If an
integer is not one that would be converted, it is returned in its original
form.

If a non-integer is given, it will be returned in its original form as
well.

**Parameters**

* `val` **[Number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)**

**Examples**

```javascript
var journalize = require('journalize');

journalize.apnumber(8);
// returns 'eight'

journalize.apnumber(42);
// returns 42
```

Returns **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**

### apstate

Converts state names into AP abbreviations, and back. If the supplied
string has no match, or if there is a match and the lookup is empty, the
original value is returned. If the value is not a string, the original will
also be returned.

If `reverse` is true, `apstate` will convert an abbreviation back to a full
string.

**Parameters**

* `val` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**
* `reverse` **[Boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** (optional, default `false`)

**Examples**

```javascript
var journalize = require('journalize');

journalize.apstate('Arizona');
// returns 'Ariz.'

journalize.apstate('District of Columbia');
// returns 'D.C.'

journalize.apstate('Texas');
// returns 'Texas'

journalize.apstate('Ontario');
// returns 'Ontario'

journalize.apstate('D.C.', true);
// returns 'District of Columbia'
```

Returns **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**

### aptime

Returns an AP-formatted time string that corresponds with the supplied
Date. If an `input` is not passed, it will use the result of `new Date();`.

**Parameters**

* `date` **[Date](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date)?** JavaScript Date object, defaults to current date if
  not passed (optional, default `new Date()`)

**Examples**

```javascript
var journalize = require('journalize');

// Bright and early
journalize.aptime(new Date(2016, 10, 8, 6, 30));
// returns '6:30 a.m.'

// It can handle `p.m.` too
journalize.aptime(new Date(2016, 10, 8, 16, 30));
// returns '4:30 p.m.'

// Uses the current time if no parameter is passed
journalize.aptime();
// returns '6:45 p.m.' (pretend it is actually 6:45 p.m. right now)
```

Returns **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**

### capfirst

Capitalizes the first character of a value and returns it.

**Parameters**

* `val` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**

**Examples**

```javascript
var journalize = require('journalize');

journalize.capfirst('hello world');
// returns 'Hello world'
```

Returns **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**

### intcomma

Alters a string or number to include commas. If `val` is undefined or null,
an empty string is returned.

**Parameters**

* `val` **([Number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number) \| [String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String))**

**Examples**

```javascript
var journalize = require('journalize');

journalize.intcomma(10311);
// returns '10,311'

journalize.intcomma('1234567.1234567');
// returns '1,234,567.1234567'
```

Returns **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**

### intword

Converts a large integer into a string representation. Only makes sense for
numbers at least 1 million or more.

**Parameters**

* `val` **[Number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)**

**Examples**

```javascript
var journalize = require('journalize');

journalize.intword(1000000);
// returns '1 million'

journalize.intword(6500000000000);
// returns '6.5 trillion'
```

Returns **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**

### ordinal

Converts an integer into its ordinal form. Handles the special cases of 11,
12 and 13, too. If a non-integer is submitted, it will be returned in its
original form.

**Parameters**

* `val` **[Number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)**

**Examples**

```javascript
var journalize = require('journalize');

journalize.ordinal(5);
// returns '5th'

journalize.ordinal(13);
// returns '13th'

journalize.ordinal(103);
// returns '103rd'
```

Returns **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**

### pluralize

Returns a plural suffix if the value is not 1. By default, `pluralize`
uses "s" as the suffix. If a `String` is provided, `pluralize` will attempt
to convert it into a `Number`. If an `Array` is provided instead of a
number, the length of the `Array` is used to determine the suffix. An
alternative plural suffix can be provided as the second parameter, and if
necessary, an alternative singular suffix can be provided as the third.

**Parameters**

* `value` **([Number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number) \| [String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array))**
* `pluralSuffix` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** (optional, default `'s'`)
* `singularSuffix` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** (optional, default `''`)

**Examples**

```javascript
var journalize = require('journalize');

// typical usage
'vote' + journalize.pluralize(0); // votes
'vote' + journalize.pluralize(1); // vote
'vote' + journalize.pluralize(2); // votes

// the plural suffix may be changed
'class' + journalize.pluralize(0, 'es'); // classes
'class' + journalize.pluralize(1, 'es'); // class
'class' + journalize.pluralize(2, 'es'); // classes

// some words also need a custom singular suffix
'cand' + journalize.pluralize(0, 'ies', 'y'); // candies
'cand' + journalize.pluralize(1, 'ies', 'y'); // candy
'cand' + journalize.pluralize(2, 'ies', 'y'); // candies
```

Returns **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**

### postal

Converts state and U.S. territory names into USPS postal codes, and back. If
the supplied string has no match, or if there is a match and the lookup is
empty, the original value is returned. If the value is not a string, the
original will also be returned.

If `reverse` is true, `postal` will convert a postal code back to a full
string.

**Parameters**

* `val` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**
* `reverse` **[Boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** (optional, default `false`)

**Examples**

```javascript
var journalize = require('journalize');

journalize.postal('Arizona');
// returns 'AZ'

journalize.postal('District of Columbia');
// returns 'DC'

journalize.postal('Texas');
// returns 'TX'

journalize.postal('Ontario');
// returns 'Ontario'

journalize.postal('DC', true);
// returns 'District of Columbia'
```

Returns **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**

### yesno

Given a mapping of arguments for `true`, `false`, and (optionally)
`null`/`undefined`, return a string according to the value. If `maybe` is not
provided, a `null` or `undefined` value will return the `no` argument.

**Parameters**

* `val` **([Boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean) \| [Null](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/null) \| [undefined](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/undefined))**
* `yes` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** (optional, default `'yes'`)
* `no` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** (optional, default `'no'`)
* `maybe` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** (optional, default `'maybe'`)

**Examples**

```javascript
var journalize = require('journalize');

journalize.yesno(true);
// returns 'yes'
journalize.yesno(false);
// returns 'no'
journalize.yesno(null);
// returns 'maybe'

journalize.yesno(true, 'yay', 'nay', 'shruggie');
// returns 'yay'
journalize.yesno(false, 'yay', 'nay', 'shruggie');
// returns 'nay'
journalize.yesno(null, 'yay', 'nay', 'shruggie');
// returns 'shruggie'
```

## What if I do want to use this in [Nunjucks](http://mozilla.github.io/nunjucks/)?

Great question! I cannot speak to whether this is the best way, but it's what
I've done without issue since `journalize` was released.

Once you have your `nunjucks` environment, you can loop through the
properties of `journalize` and add each function as a filter.

```js
const journalize = require('journalize');
const nunjucks = require('nunjucks');

const env = nunjucks.configure(/* */);

/*
Set up `journalize`.
 */
for (let key in journalize) {
  let func = journalize[key];

  if (typeof func === 'function') {
    env.addFilter(key, func); // this would work with env.addGlobal, too
  }
}
```

Now every function of `journalize` is now available in your templates!

## License

MIT
