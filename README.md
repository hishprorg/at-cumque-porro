# @hishprorg/at-cumque-porro <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

Define an accessor property on an object. In an engine without descriptors, in loose mode, when only a getter is provided, nonEnumerable is false, and nonConfigurable is false, wil fall back to assignment - otherwise, it will throw.

The two `non*` options can also be passed `null`, which will use the existing state if available.

The `loose` option will mean that if you attempt to set a nonconfigurable/nonwritable accessor property with `set`, in an environment without descriptor support, it will fall back to normal assignment (and eagerly evaluate the getter).

## Usage

```javascript
var defineAccessorProperty = require('@hishprorg/at-cumque-porro');
var assert = require('assert');

var str = 'value';
var strThunk = function () { return str; };
var strSetter = function (v) { str = v; };
var random = function () { return Math.random(); };

var obj = {};
defineAccessorProperty(
	obj,
	'key',
	{
		get: strThunk,
		set: strSetter,
	}
);
defineAccessorProperty(
	obj,
	'key2',
	{
		get: random, // at least one of "get" or "set" must be provided
		nonConfigurable: true, // optional
		nonEnumerable: true, // optional
		loose: false, // optional
	}
);

assert.deepEqual(
	Object.getOwnPropertyDescriptors(obj),
	{
		key: {
			configurable: true,
			enumerable: true,
			get: strThunk,
			set: strSetter,
		},
		key2: {
			configurable: false,
			enumerable: false,
			get: random,
			set: undefined,
		},
	}
);
```

[package-url]: https://npmjs.org/package/@hishprorg/at-cumque-porro
[npm-version-svg]: https://versionbadg.es/ljharb/@hishprorg/at-cumque-porro.svg
[deps-svg]: https://david-dm.org/ljharb/@hishprorg/at-cumque-porro.svg
[deps-url]: https://david-dm.org/ljharb/@hishprorg/at-cumque-porro
[dev-deps-svg]: https://david-dm.org/ljharb/@hishprorg/at-cumque-porro/dev-status.svg
[dev-deps-url]: https://david-dm.org/ljharb/@hishprorg/at-cumque-porro#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@hishprorg/at-cumque-porro.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@hishprorg/at-cumque-porro.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@hishprorg/at-cumque-porro.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@hishprorg/at-cumque-porro
[codecov-image]: https://codecov.io/gh/ljharb/@hishprorg/at-cumque-porro/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/ljharb/@hishprorg/at-cumque-porro/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/ljharb/@hishprorg/at-cumque-porro
[actions-url]: https://github.com/hishprorg/at-cumque-porro/actions
