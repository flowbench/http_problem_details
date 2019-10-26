[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)

# HTTP Problem Details (RFC 7807) for Node.js

This library implements HTTP Problem details (RFC 7807) for HTTP APIs.

## Installation

```
npm install http-problem-details
```

or

```
yarn add http-problem-details
```

## Usage

`http-problem-details` current supports these options:

* `type` (string) - A URI reference [[RFC3986](https://tools.ietf.org/html/rfc3986)] that identifies the problem type.
* `title` (string) - A short, human-readable summary of the problem type.
* `status` (number) - The HTTP status code ([[RFC7231], Section 6](https://tools.ietf.org/html/rfc7231#section-6)) generated by the origin server for this occurrence of the problem. If only `status` is provided `type` will be set to `about:blank` and `title` will be become the reason phrase as of the HTTP spec, e.g. "Not Found" if `status` is `404`.
* `instance` (stringt) - A URI reference that identifies the specific occurrence of the problem.
* Extension Members - Provide additional information.

`type` and `instance` are validated to be valid URIs and will throw errors if not.

### Example

To generate this `problem+json` result

```json
{
    "type": "https://example.com/probs/out-of-credit",
    "title": "You do not have enough credit.",
    "detail": "Your current balance is 30, but that costs 50.",
    "instance": "/account/12345/msgs/abc",
    "status": 400
}
```

this code is required:

```javascript
const ProblemDocument = require('http-problem-details').ProblemDocument;

const doc = new ProblemDocument({
  type: 'https://example.com/probs/out-of-credit',
  title: 'You do not have enough credit.',
  detail: 'Your current balance is 30, but that costs 50.',
  instance: '/account/12345/msgs/abc',
  status: 400
});
```

### Example with Extension Members

To generate this `problem+json` result

```json
{
    "type": "https://example.com/probs/out-of-credit",
    "title": "You do not have enough credit.",
    "balance": 30,
    "accounts": ["/account/12345", "/account/67890"]
}
```

this code is required:

```javascript
const ProblemDocument = require('http-problem-details').ProblemDocument;
const ProblemDocumentExtension = require('http-problem-details').ProblemDocumentExtension;

const extension = new ProblemDocumentExtension({
  balance: 30,
  accounts: ['/account/12345', '/account/67890']
});

const doc = new ProblemDocument({
  type: 'https://example.com/probs/out-of-credit',
  title: 'You do not have enough credit.'
}, extension);
```

## Using http-problem-details with express
Usage of `http-problem-details` is described in `express-http-problem-details` ( [repository](https://github.com/PDMLab/express-http-problem-details) | [npm](https://www.npmjs.com/package/docker-compose)).

## Running the tests

```
npm test
```

## TypeScript
`http-problem-details` is implemented in TypeScript, hence providing typings out of the box.

## Want to help?

This project is just getting off the ground and could use some help with cleaning things up and refactoring.

If you want to contribute - we'd love it! Just open an issue to work against so you get full credit for your fork. You can open the issue first so we can discuss and you can work your fork as we go along.

If you see a bug, please be so kind as to show how it's failing, and we'll do our best to get it fixed quickly.

Before sending a PR, please [create an issue](https://github.com/PDMLab/http-problem-details/issues/new) to introduce your idea and have a reference for your PR.

We're using [conventional commits](https://www.conventionalcommits.org), so please use it for your commits as well.

Also please add tests and make sure to run `npm run lint-ts`.

## License

MIT License

Copyright (c) 2017 - 2019 PDMLab

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


