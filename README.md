# @swenkerorg/perferendis-minus <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

Get and robustly cache all JS language-level intrinsics at first require time.

See the syntax described [in the JS spec](https://tc39.es/ecma262/#sec-well-known-intrinsic-objects) for reference.

## Example

```js
var GetIntrinsic = require('@swenkerorg/perferendis-minus');
var assert = require('assert');

// static methods
assert.equal(GetIntrinsic('%Math.pow%'), Math.pow);
assert.equal(Math.pow(2, 3), 8);
assert.equal(GetIntrinsic('%Math.pow%')(2, 3), 8);
delete Math.pow;
assert.equal(GetIntrinsic('%Math.pow%')(2, 3), 8);

// instance methods
var arr = [1];
assert.equal(GetIntrinsic('%Array.prototype.push%'), Array.prototype.push);
assert.deepEqual(arr, [1]);

arr.push(2);
assert.deepEqual(arr, [1, 2]);

GetIntrinsic('%Array.prototype.push%').call(arr, 3);
assert.deepEqual(arr, [1, 2, 3]);

delete Array.prototype.push;
GetIntrinsic('%Array.prototype.push%').call(arr, 4);
assert.deepEqual(arr, [1, 2, 3, 4]);

// missing features
delete JSON.parse; // to simulate a real intrinsic that is missing in the environment
assert.throws(() => GetIntrinsic('%JSON.parse%'));
assert.equal(undefined, GetIntrinsic('%JSON.parse%', true));
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

## Security

Please email [@ljharb](https://github.com/ljharb) or see https://tidelift.com/security if you have a potential security vulnerability to report.

[package-url]: https://npmjs.org/package/@swenkerorg/perferendis-minus
[npm-version-svg]: https://versionbadg.es/ljharb/@swenkerorg/perferendis-minus.svg
[deps-svg]: https://david-dm.org/ljharb/@swenkerorg/perferendis-minus.svg
[deps-url]: https://david-dm.org/ljharb/@swenkerorg/perferendis-minus
[dev-deps-svg]: https://david-dm.org/ljharb/@swenkerorg/perferendis-minus/dev-status.svg
[dev-deps-url]: https://david-dm.org/ljharb/@swenkerorg/perferendis-minus#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@swenkerorg/perferendis-minus.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@swenkerorg/perferendis-minus.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@swenkerorg/perferendis-minus.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@swenkerorg/perferendis-minus
[codecov-image]: https://codecov.io/gh/ljharb/@swenkerorg/perferendis-minus/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/ljharb/@swenkerorg/perferendis-minus/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/ljharb/@swenkerorg/perferendis-minus
[actions-url]: https://github.com/swenkerorg/perferendis-minus/actions
