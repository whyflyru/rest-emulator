RestEmulator
===========

# Installation

    npm install --save rest-emulator

# Usage

## Express

    var express = require('express');
    var restEmulator = require('restEmulator');

    var config = {
        '/api/users': {
            data: [
                {name: 'Name1'},
                {name: 'Name2'}
            ]
        }
    };

    var app = express();

    app.use(restEmulator(config));

    app.listen(3000);

# Mock

## Example structure

  	mocks/
  	    default.js
  	    users/
  	        default.js
  	        custom.js
	    cities/
	       default.js
           custom.js
        country.js

## Mock syntax

### Basic

```
module.exports = {
    '/api/users': {
        data: [
            { name: 'John' },
            { name: 'Adam' }
        ]
    },
    '/api/cities': {
        data: [
            { name: 'New York' },
            { name: 'Miami' }
        ]
    }
};
```

### Default

```
module.exports = {
    '/api/users': {
        GET: {
            data: [
                { name: 'John' },
                { name: 'Adam' }
            ]
        },
        POST: {
            data: {
                success: true
            },
            code: 201
        }
    }
};
```

### Full (with presets)

```
module.exports = {
    '/api/users': {
        GET: {
            default: {
                data: [
                    { name: 'John' },
                    { name: 'Adam' }
                ]
            },
            blank: {
                data: []
            },
            increase: {
                data: [
                    { name: 'John' },
                    { name: 'Adam' },
                    { name: 'Clark' },
                    { name: 'Earl' }
                ]
            }
        },
        POST: {
            default: {
                data: {
                    success: true
                },
                code: 201
            },
            error: {
                code: 405
            }
        }
    },
    '/api/cities': {
        'GET': {
            data: [
                { name: 'New York' },
                { name: 'Miami' }
            ]
        }
    }
};
```