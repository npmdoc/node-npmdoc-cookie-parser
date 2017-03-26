# api documentation for  [cookie-parser (v1.4.3)](https://github.com/expressjs/cookie-parser)  [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-cookie-parser.svg)](https://travis-ci.org/npmdoc/node-npmdoc-cookie-parser)
#### cookie parsing with signatures

[![NPM](https://nodei.co/npm/cookie-parser.png?downloads=true)](https://www.npmjs.com/package/cookie-parser)

[![apidoc](https://npmdoc.github.io/node-npmdoc-cookie-parser/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-cookie-parser_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-cookie-parser/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-cookie-parser/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "TJ Holowaychuk",
        "email": "tj@vision-media.ca",
        "url": "http://tjholowaychuk.com"
    },
    "bugs": {
        "url": "https://github.com/expressjs/cookie-parser/issues"
    },
    "contributors": [
        {
            "name": "Douglas Christopher Wilson",
            "email": "doug@somethingdoug.com"
        }
    ],
    "dependencies": {
        "cookie": "0.3.1",
        "cookie-signature": "1.0.6"
    },
    "description": "cookie parsing with signatures",
    "devDependencies": {
        "istanbul": "0.4.3",
        "mocha": "2.5.3",
        "supertest": "1.1.0"
    },
    "directories": {},
    "dist": {
        "shasum": "0fe31fa19d000b95f4aadf1f53fdc2b8a203baa5",
        "tarball": "https://registry.npmjs.org/cookie-parser/-/cookie-parser-1.4.3.tgz"
    },
    "engines": {
        "node": ">= 0.8.0"
    },
    "files": [
        "LICENSE",
        "HISTORY.md",
        "index.js"
    ],
    "gitHead": "ad0b2cb834affe3929f0a690cd0494cd0b96d6be",
    "homepage": "https://github.com/expressjs/cookie-parser",
    "keywords": [
        "cookie",
        "middleware"
    ],
    "license": "MIT",
    "maintainers": [
        {
            "name": "defunctzombie",
            "email": "shtylman@gmail.com"
        },
        {
            "name": "dougwilson",
            "email": "doug@somethingdoug.com"
        }
    ],
    "name": "cookie-parser",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/expressjs/cookie-parser.git"
    },
    "scripts": {
        "test": "mocha --reporter spec --bail --check-leaks test/",
        "test-cov": "istanbul cover node_modules/mocha/bin/_mocha -- --reporter dot --check-leaks test/",
        "test-travis": "istanbul cover node_modules/mocha/bin/_mocha --report lcovonly -- --reporter spec --check-leaks test/"
    },
    "version": "1.4.3"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module cookie-parser](#apidoc.module.cookie-parser)
1.  [function <span class="apidocSignatureSpan">cookie-parser.</span>JSONCookie (str)](#apidoc.element.cookie-parser.JSONCookie)
1.  [function <span class="apidocSignatureSpan">cookie-parser.</span>JSONCookies (obj)](#apidoc.element.cookie-parser.JSONCookies)
1.  [function <span class="apidocSignatureSpan">cookie-parser.</span>signedCookie (str, secret)](#apidoc.element.cookie-parser.signedCookie)
1.  [function <span class="apidocSignatureSpan">cookie-parser.</span>signedCookies (obj, secret)](#apidoc.element.cookie-parser.signedCookies)



# <a name="apidoc.module.cookie-parser"></a>[module cookie-parser](#apidoc.module.cookie-parser)

#### <a name="apidoc.element.cookie-parser.JSONCookie"></a>[function <span class="apidocSignatureSpan">cookie-parser.</span>JSONCookie (str)](#apidoc.element.cookie-parser.JSONCookie)
- description and source-code
```javascript
function JSONCookie(str) {
  if (typeof str !== 'string' || str.substr(0, 2) !== 'j:') {
    return undefined;
  }

  try {
    return JSON.parse(str.slice(2));
  } catch (err) {
    return undefined;
  }
}
```
- example usage
```shell
...

### cookieParser(secret, options)

- 'secret' a string or array used for signing cookies. This is optional and if not specified, will not parse signed cookies. If
a string is provided, this is used as the secret. If an array is provided, an attempt will be made to unsign the cookie with each
 secret in order.
- 'options' an object that is passed to 'cookie.parse' as the second option. See [cookie](https://www.npmjs.org/package/cookie)
for more information.
  - 'decode' a function to decode the value of the cookie

### cookieParser.JSONCookie(str)

Parse a cookie value as a JSON cookie. This will return the parsed JSON value if it was a JSON cookie, otherwise it will return
the passed value.

### cookieParser.JSONCookies(cookies)

Given an object, this will iterate over the keys and call 'JSONCookie' on each value. This will return the same object passed in
.
...
```

#### <a name="apidoc.element.cookie-parser.JSONCookies"></a>[function <span class="apidocSignatureSpan">cookie-parser.</span>JSONCookies (obj)](#apidoc.element.cookie-parser.JSONCookies)
- description and source-code
```javascript
function JSONCookies(obj) {
  var cookies = Object.keys(obj);
  var key;
  var val;

  for (var i = 0; i < cookies.length; i++) {
    key = cookies[i];
    val = JSONCookie(obj[key]);

    if (val) {
      obj[key] = val;
    }
  }

  return obj;
}
```
- example usage
```shell
...
- 'options' an object that is passed to 'cookie.parse' as the second option. See [cookie](https://www.npmjs.org/package/cookie)
for more information.
  - 'decode' a function to decode the value of the cookie

### cookieParser.JSONCookie(str)

Parse a cookie value as a JSON cookie. This will return the parsed JSON value if it was a JSON cookie, otherwise it will return
the passed value.

### cookieParser.JSONCookies(cookies)

Given an object, this will iterate over the keys and call 'JSONCookie' on each value. This will return the same object passed in
.

### cookieParser.signedCookie(str, secret)

Parse a cookie value as a signed cookie. This will return the parsed unsigned value if it was a signed cookie and the signature
was valid, otherwise it will return the passed value.
...
```

#### <a name="apidoc.element.cookie-parser.signedCookie"></a>[function <span class="apidocSignatureSpan">cookie-parser.</span>signedCookie (str, secret)](#apidoc.element.cookie-parser.signedCookie)
- description and source-code
```javascript
function signedCookie(str, secret) {
  if (typeof str !== 'string') {
    return undefined;
  }

  if (str.substr(0, 2) !== 's:') {
    return str;
  }

  var secrets = !secret || Array.isArray(secret)
    ? (secret || [])
    : [secret];

  for (var i = 0; i < secrets.length; i++) {
    var val = signature.unsign(str.slice(2), secrets[i]);

    if (val !== false) {
      return val;
    }
  }

  return false;
}
```
- example usage
```shell
...

Parse a cookie value as a JSON cookie. This will return the parsed JSON value if it was a JSON cookie, otherwise it will return
the passed value.

### cookieParser.JSONCookies(cookies)

Given an object, this will iterate over the keys and call 'JSONCookie' on each value. This will return the same object passed in
.

### cookieParser.signedCookie(str, secret)

Parse a cookie value as a signed cookie. This will return the parsed unsigned value if it was a signed cookie and the signature
was valid, otherwise it will return the passed value.

The 'secret' argument can be an array or string. If a string is provided, this is used as the secret. If an array is provided, an
 attempt will be made to unsign the cookie with each secret in order.

### cookieParser.signedCookies(cookies, secret)
...
```

#### <a name="apidoc.element.cookie-parser.signedCookies"></a>[function <span class="apidocSignatureSpan">cookie-parser.</span>signedCookies (obj, secret)](#apidoc.element.cookie-parser.signedCookies)
- description and source-code
```javascript
function signedCookies(obj, secret) {
  var cookies = Object.keys(obj);
  var dec;
  var key;
  var ret = Object.create(null);
  var val;

  for (var i = 0; i < cookies.length; i++) {
    key = cookies[i];
    val = obj[key];
    dec = signedCookie(val, secret);

    if (val !== dec) {
      ret[key] = dec;
      delete obj[key];
    }
  }

  return ret;
}
```
- example usage
```shell
...

### cookieParser.signedCookie(str, secret)

Parse a cookie value as a signed cookie. This will return the parsed unsigned value if it was a signed cookie and the signature
was valid, otherwise it will return the passed value.

The 'secret' argument can be an array or string. If a string is provided, this is used as the secret. If an array is provided, an
 attempt will be made to unsign the cookie with each secret in order.

### cookieParser.signedCookies(cookies, secret)

Given an object, this will iterate over the keys and check if any value is a signed cookie. If it is a signed cookie and the signature
 is valid, the key will be deleted from the object and added to the new object that is returned.

The 'secret' argument can be an array or string. If a string is provided, this is used as the secret. If an array is provided, an
 attempt will be made to unsign the cookie with each secret in order.

## Example
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
