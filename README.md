# @medial/lambda

# A wrapper for AWS Lambda 
A wrapper to help build AWS Lambda backed HTTP services.

Features
 - Validation via [Joi](https://github.com/hapijs/joi)
 - Error responses via [Boom] (https://github.com/hapijs/boom)

**Inspired by the [hapi](https://hapi.dev/) framework.**

## Example

Medial Handler Object

```
const Lambda = require('@medial/lambda');
const Boom = require('@hapi/boom');
const Joi = require('@hapi/joi');


exports.get = Lambda.define({
  validate: {
    query: Joi.object().keys({
      world: Joi.string().default('world')
    })
  },
  handler: async function(request, h) {
    const world = request.query.world;

    return {hello: world};
  }
});
```
`exports.get` is now a AWS Lambda function. Once this function is configured for HTTP access via the AWS API Gateway - when invoked, it will return ```{"hello": "world"}``` with a response code of `200`.

You can also invoke the lambda from another lambda. The response will look like this: 
```
{
  headers: {},
  statusCode: 200,
  body: '{"hello": "world"}' // this is stringifyed object 
}
```

# Documentation
 - [Handler API](docs/HANDLER-API.md)
 - [Client API](docs/CLIENT-API.md)