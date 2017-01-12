# http-error

Provides the `HttpError` class and associated factory methods.

Version 1.0.0

## Usage

```
$ npm install --save @be/http-error
```

```javascript
const HttpError = require('@be/http-error');

function sqrt(val) {
	if (val < 0) {
	    throw HttpError.badRequest('Value %d cannot be negative.', val);
	} else {
	    return Math.sqrt(val);
    }
}

let err = HttpError.internalServerError('Cannot connect to the database.');

console.log(err.toString());
// Error: 500 (Internal Server Error) Cannot connect to the database.

console.log(err.toJson());
// Outputs an object.

console.log(err.toHtml());
// Outputs an HTML string.
```

The `badRequest` method and `internalServerError` method are factory methods. No `new` keyword is required. There is one factory method for each of the 400- and 500-series errors.

If you want to call the constructor yourself, you can:

```javascript
function sqrt(val) {
	if (val < 0) {
	    throw new HttpError(400, util.format('Value %d cannot be negative.', val));
	} else {
	    return Math.sqrt(val);
    }
}
```

As you can see, using the factory method...

- is more readable,
- does not require the `new` keyword,
- handles `util.format` arguments.

You can also pass in an `Error` object...

```javascript
let err = new Error('That record already exists.');

let conflict = HttpError.conflict(err);

console.log(conflict.toString());
// Error: 409 (Conflict) That record already exists.
```

This is useful when wrapping a library error into an error for your REST API.

## License

MIT License

Copyright (c) 2017 Buchanan & Edwards

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
