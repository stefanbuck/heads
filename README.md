# heads [![Build Status](https://travis-ci.org/zeke/heads.svg?branch=master)](https://travis-ci.org/zeke/heads)

Make parallel HEAD requests for an array of URLs and get back their HTTP status codes.

## Why?

You've got a collection of URLs, and you want to make sure they're all working.

If you just need to check whether a URL is resolving, a `HEAD` request is preferable
to a `GET` because it only downloads the response headers instead of the whole
response body.

To keep things snappy, `heads` makes multiple requests in parallel instead of one
at a time.

## Installation

```sh
npm install heads --save
```

## Usage

Heads expects an array of URL strings:

```js
const heads = require("heads")
const urls = [
  'https://google.com',
  'https://github.com',
  'https://github.com/nonexistent-url'
]

heads(urls)
  .then(function(codes) {
   // [200, 200, 404]
   codes.every(code => code === 200)
  })
  .catch(function(err) {
    // handle error
  })
```

Node-style callbacks are supported too:

```js
heads(urls, function(err, codes) { /*...*/ })
```

If you just need to look up one URL, pass it as an argument instead of an array:

```js
heads('http://mysite.com').then(...)
```

## Tests

```sh
npm install
npm test
```

## Dependencies

- [async](https://github.com/caolan/async): Higher-order functions and common patterns for asynchronous code
- [got](https://github.com/sindresorhus/got): Simplified HTTP requests
- [pify](https://github.com/sindresorhus/pify): Promisify a callback-style function

## Dev Dependencies

- [tap-spec](https://github.com/scottcorgan/tap-spec): Formatted TAP output like Mocha&#39;s spec reporter
- [tape](https://github.com/substack/tape): tap-producing test harness for node and browsers

## License

MIT

_Generated by [package-json-to-readme](https://github.com/zeke/package-json-to-readme)_
