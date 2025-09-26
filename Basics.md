Basics
======

Qred API is an interface between partners and Qred, which is based on REST principles and using standard HTTP request and response status codes.

Use the sandbox Qred APi base url,`https://sandbox.qred.com/webapi/`, to test your requests. The sandbox endpoints are also available via Swagger in the [Qred API Reference](https://developers.qred.com/docs/qred-api/api-reference). Switch to `https://api-v2.qred.com/webapi/` when in production.

Authentication
--------------

All requests to Qred API require authentication and authorization. This is achieved by adding an OAuth access token to the request header. See how to obtain the OAuth access token in the [Qred API Reference](https://developers.qred.com/docs/qred-api/api-reference).

Responses
---------

All responses are returned as a JSON object.
