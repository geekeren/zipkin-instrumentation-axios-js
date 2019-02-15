# zipkin-js-instrumentation-axios

[![NPM Version](https://img.shields.io/npm/v/zipkin-js-instrumentation-axios.svg?style=flat)](https://www.npmjs.com/package/zipkin-js-instrumentation-axios)
[![License](http://img.shields.io/npm/l/rn-expandable-text.svg?style=flat-square)](https://opensource.org/licenses/Apache-2.0)



Adds Zipkin tracing to the [axios](https://www.npmjs.com/package/axios) JS HTTP client library. It **supports all features of `axios`**.

## Installation

```
npm install zipkin-js-instrumentation-axios --save

```

## Usage

```javascript
const axios = require('axios');
const wrapAxios = require('./index.js');
const { Tracer, ExplicitContext, ConsoleRecorder } = require('zipkin');

const ctxImpl = new ExplicitContext();
const recorder = new ConsoleRecorder();
const localServiceName = 'service-a'; // name of this application
const tracer = new Tracer({ ctxImpl, recorder, localServiceName });

const remoteServiceName = 'weather-api';
const zipkinAxios = wrapAxios(axios, { tracer, localServiceName, remoteServiceName });

zipkinAxios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```