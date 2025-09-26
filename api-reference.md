API Reference
=============

Create OAuth2 token
-------------------

Before OAuth 2.0 can be used, a client id and client secret must be aquired.

An access token can be obtained by sending the client id and the client secret to `https://qredab.eu.auth0.com/oauth/token`.

#### Example of request body

```
{
  "client_id": "some_client_id",
  "client_secret": "some_client_secret",
  "audience": "https://api.qred.com",
  "grant_type": "client_credentials"
}

```

Pre-offer/loan application request body
---------------------------------------

### Full request body

```
{
  "amount": 0,
  "applicant": {
    "additionalName": "string",
    "allow_person_report_fetch": true,
    "dateOfBirth": "string",
    "email": "string",
    "familyName": "string",
    "givenName": "string",
    "nationalIdentificationNumber": "string",
    "phone": "string",
    "placeOfBirth": "string",
    "politicallyExposedPerson": true
  },
  "files": [
    {
      "base64Content": "string",
      "encodingFormat": [
        "string"
      ],
      "filename": "string"
    }
  ],
  "organization": {
    "currentMonthlyTurnover": "string",
    "email": "string",
    "iban": "string",
    "nationalOrganizationNumber": "string",
    "numberOfEmployees": "string",
    "owners": [
      {
        "additionalName": "string",
        "dateOfBirth": "string",
        "familyName": "string",
        "givenName": "string",
        "nationalIdentificationNumber": "string",
        "ownerShipPercent": 0,
        "placeOfBirth": "string"
      }
    ],
    "phone": "string",
    "url": "string"
  },
  "politicallyExposedPersons": [
    {
      "additionalName": "string",
      "dateOfBirth": "string",
      "description": "string",
      "familyName": "string",
      "givenName": "string",
      "nationalIdentificationNumber": "string",
      "placeOfBirth": "string"
    }
  ],
  "promoCode": "string",
  "purposeOfLoan": "string",
  "term": 0
}

```

### Request body with required parameters

```
{
  "amount": 0,
  "applicant": {
    "nationalIdentificationNumber": "string",
    "email": "string"
  }
  "organization": {
    "nationalOrganizationNumber": "string",
    "email": "string"
  }
}

```

### Data description

| Parameter | Type | Description |
| --- | --- | --- |
| `amount` | `Number` | The value should be greater than 0 |
| `promoCode` | `String` |  |
| `purposeOfLoan` | `String` | String should be less than 2000 characters |
| `term` | `Number` |  |

#### Applicant

| Parameter | Type | Description |
| --- | --- | --- |
| `additionalName` | `String` |  |
| `allow_person_report_fetch` | `Boolean` |  |
| `dateOfBirth` | `String` |  |
| `email` | `String` | Regex: `[a-z0-9!#$%&'+=?^_{\|}~-]+(?:\.[a-z0-9!#$%&'*+=?^_{\|}~-]+)@(?:a-z0-9?.)+[a-z0-9]*a-z0-9?` |
| `familyName` | `String` |  |
| `givenName` | `String` |  |
| `nationalIdentificationNumber` | `String` | SE: `(19\|20)[0-9]{10}`\
FI: `[0-9]{6}[-A][0-9]{3}[0-9A-Y]` |
| `phone` | `String` | SE: String should be greater than or equal to 9 digits\
FI: String should be greater than or equal to 6 digits |
| `placeOfBirth` | `String` |  |
| `politicallyExposedPerson` | `Boolean` |  |

#### Files

| Parameter | Type | Description |
| --- | --- | --- |
| `base64Content` | `Number` |  |
| `encodingFormat` | `Array` |  |
| `filename` | `String` |  |

#### Organization

| Parameter | Type | Description |
| --- | --- | --- |
| `currentMonthlyTurnover` | `String` | String should be less than 50 characters |
| `email` | `Boolean` | Regex: `[a-z0-9!#$%&'+=?^_{\|}~-]+(?:\.[a-z0-9!#$%&'*+=?^_{\|}~-]+)@(?:a-z0-9?.)+[a-z0-9]*a-z0-9?` |
| `iban` | `String` |  |
| `nationalOrganizationNumber` | `String` | SE: `[0-9]{10}`\
FI: `[0-9]{7}-[0-9]` |
| `numberOfEmployees` | `String` |  |
| `owners` | `Array` |  |
| `phone` | `String` | SE: String should be greater than or equal to 9 digits\
FI: String should be greater than or equal to 6 digits |
| `url` | `String` |  |

#### Owners

| Parameter | Type | Description |
| --- | --- | --- |
| `additionalName` | `String` |  |
| `dateOfBirth` | `String` |  |
| `familyName` | `String` |  |
| `givenName` | `String` |  |
| `nationalIdentificationNumber` | `String` | SE: `(19\|20)[0-9]{10}`\
FI: `[0-9]{6}[-A][0-9]{3}[0-9A-Y]` |
| `ownerShipPercent` | `Number` |  |
| `placeOfBirth` | `String` |  |

#### Politically exposed persons

| Parameter | Type | Description |
| --- | --- | --- |
| `additionalName` | `String` |  |
| `dateOfBirth` | `String` |  |
| `description` | `String` |  |
| `familyName` | `String` |  |
| `givenName` | `String` |  |
| `nationalIdentificationNumber` | `String` | SE: `(19\|20)[0-9]{10}`\
FI: `[0-9]{6}[-A][0-9]{3}[0-9A-Y]` |
| `placeOfBirth` | `String` |  |

Create pre-offer application
----------------------------

A pre-offer application can be created in order to request a bid by the customer. A `POST` request should be sent to `/application/pre-offer`.

The pre-offer application ID and its URL are returned in the response if the pre-offer application was succesfully created. The URL is used to obtain the information about the status of the pre-offer application and to see the bid.

#### Response

```
{
  "id": "pre_offer_application_id",
  "url": "pre_offer_application_url"
}

```

Get the bid for a pre-offer application
---------------------------------------

To receive information about the bid for the pre-offer a partner needs to fetch it from the system and check the status its status. It can be either `PENDING` or `PRE_OFFER`. This can be done via a `GET` call to `/application/pre-offer/{id}`.

#### Response for PENDING

```
{
  "status": "PENDING"
}

```

#### Response for PRE_OFFER

```
{
  "amount": 0,
  "bidValidityEndDate": "string",
  "bidValidityPeriod": "string",
  "bidValidityStartDate": "string",
  "monthlyFee": 0,
  "monthlyFeePercent": 0,
  "monthlyToPay": 0,
  "status": "PRE_OFFER",
  "term": 0,
  "totalFee": 0,
  "totalToPay": 0
}

```

#### Pre-offer application statuses

| Status | Description |
| --- | --- |
| `PENDING` | When a pre-offer has been submitted by a partner and the underwriters need to accept to send out a pre-offer. |
| `PRE_OFFER` | Waiting for the customer to accept the pre-offer bid. Will be active for 30 days before the status changes to expired. |
| `EXPIRED` | Pre-offer expired (valid 30 days) |

Accept pre-offer bid
--------------------

When accepting a bid a `POST` request is sent to `/application/pre-offer/{id}/accept`. A loan application is created on successful response and the ID and the URL are returned in the response body.

#### Response

```
{
  "id": "loan_application_id",
  "url": "loan_application_url"
}

```

Create loan application
-----------------------

A loan application can either be created through the pre-offer process or directly by sending a `POST` request to `/application`. The application ID and the URL are returned on successful creation.

Update application
------------------

Until a new customer is identified in the system, missing application information can be sent with a `PATCH` request to `/application/{id}`.

#### Information possible to update

```
{
  "applicant": {
    "email": "string",
    "nationalIdentificationNumber": "string",
    "phone": "string"
  },
  "organization": {
    "currentMonthlyTurnover": "string",
    "email": "string",
    "iban": "string",
    "numberOfEmployees": "string",
    "phone": "string",
    "url": "string"
  },
  "purposeOfLoan": "string"
}

```

The application ID and the URL are returned on successful update.

Finalize identification of an application
-----------------------------------------

To identify a new customer, not previously existing in the system, a `POST` call to `/application/{id}/finalize-identification` can be made. The application ID and the URL are returned on successfully performed operation.

This is an optional operation, which can also be done by the Qred team.

Get application status
----------------------

A single application status can be retrieved via a `GET` request to `/applicaton/{id}`.

#### Loan application statuses

| Status | Description |
| --- | --- |
| `REGISTERED` | Waiting for Qred to process the application |
| `WAITING` | Waiting for customer's approval/signature |
| `EXPIRED` | Offer expired (valid 8 days) |
| `CANCELLED` | By the customer if not seeking loan anymore. Also used if another application from other source is in process |
| `REJECTED` | Not credit worthy |
| `APPROVED` | Customer signed and paid out |

Get all applications by partner ID
----------------------------------

It is possible to get all the applications for a single partner. The `GET` request is sent to `/applications` and the partner ID is retrieved from the access token.

Swagger Reference
-----------------

Qred API Sandbox

 1.0.0

---------------------------

[ Base URL: sandbox.qred.com/webapi ]

<https://api-v2.qred.com/webapi/v2/api-docs?group=Sandbox>

Sandbox endpoints for the partner developers

[Qred - Website](https://qred.se/hem)

[Send email to Qred](mailto:support@qred.se)

[](https://developers.qred.com/docs/qred-api/api-reference)

Authorize

#### Qred API Sandbox

Qred API Sandbox

POST​/application

Create an application

Create an application

#### Parameters

Try it out

| Name | Description |
| --- | --- |
|

Authorization *

string

(header)

 |

Auth0 Jwt token to access secured endpoints

*Example* : Bearer token

 |
|

postRequest *

object

(body)

 |

Post request body for creating application

-   Example Value
-   Model

```
{
  "amount": 0,
  "applicant": {
    "additionalName": "string",
    "allow_person_report_fetch": true,
    "dateOfBirth": "string",
    "email": "string",
    "familyName": "string",
    "givenName": "string",
    "nationalIdentificationNumber": "string",
    "phone": "string",
    "placeOfBirth": "string",
    "politicallyExposedPerson": true
  },
  "files": [
    {
      "base64Content": "string",
      "encodingFormat": [
        "string"
      ],
      "filename": "string"
    }
  ],
  "organization": {
    "currentMonthlyTurnover": "string",
    "email": "string",
    "iban": "string",
    "nationalOrganizationNumber": "string",
    "numberOfEmployees": "string",
    "owners": [
      {
        "additionalName": "string",
        "dateOfBirth": "string",
        "familyName": "string",
        "givenName": "string",
        "nationalIdentificationNumber": "string",
        "ownerShipPercent": 0,
        "placeOfBirth": "string"
      }
    ],
    "phone": "string",
    "url": "string"
  },
  "politicallyExposedPersons": [
    {
      "additionalName": "string",
      "dateOfBirth": "string",
      "description": "string",
      "familyName": "string",
      "givenName": "string",
      "nationalIdentificationNumber": "string",
      "placeOfBirth": "string"
    }
  ],
  "promoCode": "string",
  "purposeOfLoan": "string",
  "term": 0
}

```

Parameter content type

application/json

 |

#### Responses

Response content type

*/*

| Code | Description |
| --- | --- |
| 200 |

OK

-   Example Value
-   Model

```
{
  "filters": {},
  "value": {}
}

```

 |
| 201 |

Created

-   Example Value
-   Model

```
{
  "id": "string",
  "url": "string"
}

```

 |
| 400 |

BAD REQUEST

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "errorContainer": {
    "errorList": [
      {
        "description": "string",
        "property": "string"
      }
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 401 |

UNAUTHORIZED

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 403 |

FORBIDDEN

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 404 |

NOT FOUND

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 500 |

INTERNAL ERROR

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |

POST​/application​/pre-offer

Create a pre-offer application

Create a pre-offer application

#### Parameters

Try it out

| Name | Description |
| --- | --- |
|

Authorization *

string

(header)

 |

Auth0 Jwt token to access secured endpoints

*Example* : Bearer token

 |
|

postRequest *

object

(body)

 |

Post request body for creating pre-offer application

-   Example Value
-   Model

```
{
  "amount": 0,
  "applicant": {
    "additionalName": "string",
    "allow_person_report_fetch": true,
    "dateOfBirth": "string",
    "email": "string",
    "familyName": "string",
    "givenName": "string",
    "nationalIdentificationNumber": "string",
    "phone": "string",
    "placeOfBirth": "string",
    "politicallyExposedPerson": true
  },
  "files": [
    {
      "base64Content": "string",
      "encodingFormat": [
        "string"
      ],
      "filename": "string"
    }
  ],
  "organization": {
    "currentMonthlyTurnover": "string",
    "email": "string",
    "iban": "string",
    "nationalOrganizationNumber": "string",
    "numberOfEmployees": "string",
    "owners": [
      {
        "additionalName": "string",
        "dateOfBirth": "string",
        "familyName": "string",
        "givenName": "string",
        "nationalIdentificationNumber": "string",
        "ownerShipPercent": 0,
        "placeOfBirth": "string"
      }
    ],
    "phone": "string",
    "url": "string"
  },
  "politicallyExposedPersons": [
    {
      "additionalName": "string",
      "dateOfBirth": "string",
      "description": "string",
      "familyName": "string",
      "givenName": "string",
      "nationalIdentificationNumber": "string",
      "placeOfBirth": "string"
    }
  ],
  "promoCode": "string",
  "purposeOfLoan": "string",
  "term": 0
}

```

Parameter content type

application/json

 |

#### Responses

Response content type

*/*

| Code | Description |
| --- | --- |
| 200 |

OK

-   Example Value
-   Model

```
{
  "filters": {},
  "value": {}
}

```

 |
| 201 |

Created

-   Example Value
-   Model

```
{
  "id": "string",
  "url": "string"
}

```

 |
| 400 |

BAD REQUEST

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "errorContainer": {
    "errorList": [
      {
        "description": "string",
        "property": "string"
      }
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 401 |

UNAUTHORIZED

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 403 |

FORBIDDEN

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 404 |

NOT FOUND

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 500 |

INTERNAL ERROR

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |

GET​/application​/pre-offer​/{id}

Get the bid offer for the pre-offer application

Get the bid offer for the pre-offer application

#### Parameters

Try it out

| Name | Description |
| --- | --- |
|

Authorization *

string

(header)

 |

Auth0 Jwt token to access secured endpoints

*Example* : Bearer token

 |
|

id *

string

(path)

 |

Connect Application UUID

*Example* : ap_0eac0726-f864-4b37-9915-c91b003fdec1

 |

#### Responses

Response content type

*/*

| Code | Description |
| --- | --- |
| 200 |

OK

-   Example Value
-   Model

```
{
  "amount": 0,
  "bidValidityEndDate": "string",
  "bidValidityPeriod": "string",
  "bidValidityStartDate": "string",
  "monthlyFee": 0,
  "monthlyFeePercent": 0,
  "monthlyToPay": 0,
  "status": "Approved",
  "term": 0,
  "totalFee": 0,
  "totalToPay": 0
}

```

 |
| 400 |

BAD REQUEST

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "errorContainer": {
    "errorList": [
      {
        "description": "string",
        "property": "string"
      }
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 401 |

UNAUTHORIZED

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 403 |

FORBIDDEN

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 404 |

NOT FOUND

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 500 |

INTERNAL ERROR

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |

POST​/application​/pre-offer​/{id}​/accept

Accept pre-offer bid

Accept pre-offer bid

#### Parameters

Try it out

| Name | Description |
| --- | --- |
|

Authorization *

string

(header)

 |

Auth0 Jwt token to access secured endpoints

*Example* : Bearer token

 |
|

id *

string

(path)

 |

Connect Application UUID

*Example* : ap_0eac0726-f864-4b37-9915-c91b003fdec1

 |

#### Responses

Response content type

*/*

| Code | Description |
| --- | --- |
| 200 |

OK

-   Example Value
-   Model

```
{
  "id": "string",
  "url": "string"
}

```

 |
| 400 |

BAD REQUEST

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "errorContainer": {
    "errorList": [
      {
        "description": "string",
        "property": "string"
      }
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 401 |

UNAUTHORIZED

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 403 |

FORBIDDEN

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 404 |

NOT FOUND

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 500 |

INTERNAL ERROR

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |

GET​/application​/{id}

Get an application status by ID

Get an application status by ID

#### Parameters

Try it out

| Name | Description |
| --- | --- |
|

Authorization *

string

(header)

 |

Auth0 Jwt token to access secured endpoints

*Example* : Bearer token

 |
|

id *

string

(path)

 |

Connect Application UUID

*Example* : ap_0eac0726-f864-4b37-9915-c91b003fdec1

 |

#### Responses

Response content type

*/*

| Code | Description |
| --- | --- |
| 200 |

OK

-   Example Value
-   Model

```
{
  "status": "Approved"
}

```

 |
| 400 |

BAD REQUEST

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "errorContainer": {
    "errorList": [
      {
        "description": "string",
        "property": "string"
      }
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 401 |

UNAUTHORIZED

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 403 |

FORBIDDEN

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 404 |

NOT FOUND

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 500 |

INTERNAL ERROR

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |

PATCH​/application​/{id}

Update an application

Patch an application

#### Parameters

Try it out

| Name | Description |
| --- | --- |
|

Authorization *

string

(header)

 |

Auth0 Jwt token to access secured endpoints

*Example* : Bearer token

 |
|

id *

string

(path)

 |

Connect Application UUID

*Example* : ap_0eac0726-f864-4b37-9915-c91b003fdec1

 |
|

patchRequest *

object

(body)

 |

Patch request body for the application with given uuid

-   Example Value
-   Model

```
{
  "amount": 0,
  "applicant": {
    "additionalName": "string",
    "allow_person_report_fetch": true,
    "dateOfBirth": "string",
    "email": "string",
    "familyName": "string",
    "givenName": "string",
    "nationalIdentificationNumber": "string",
    "phone": "string",
    "placeOfBirth": "string",
    "politicallyExposedPerson": true
  },
  "files": [
    {
      "base64Content": "string",
      "encodingFormat": [
        "string"
      ],
      "filename": "string"
    }
  ],
  "organization": {
    "currentMonthlyTurnover": "string",
    "email": "string",
    "iban": "string",
    "nationalOrganizationNumber": "string",
    "numberOfEmployees": "string",
    "owners": [
      {
        "additionalName": "string",
        "dateOfBirth": "string",
        "familyName": "string",
        "givenName": "string",
        "nationalIdentificationNumber": "string",
        "ownerShipPercent": 0,
        "placeOfBirth": "string"
      }
    ],
    "phone": "string",
    "url": "string"
  },
  "politicallyExposedPersons": [
    {
      "additionalName": "string",
      "dateOfBirth": "string",
      "description": "string",
      "familyName": "string",
      "givenName": "string",
      "nationalIdentificationNumber": "string",
      "placeOfBirth": "string"
    }
  ],
  "promoCode": "string",
  "purposeOfLoan": "string",
  "term": 0
}

```

Parameter content type

application/json

 |

#### Responses

Response content type

*/*

| Code | Description |
| --- | --- |
| 200 |

OK

-   Example Value
-   Model

```
{
  "id": "string",
  "url": "string"
}

```

 |
| 400 |

BAD REQUEST

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "errorContainer": {
    "errorList": [
      {
        "description": "string",
        "property": "string"
      }
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 403 |

FORBIDDEN

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 404 |

NOT FOUND

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 500 |

INTERNAL ERROR

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |

POST​/application​/{id}​/finalize-identification

Finalize identification of the application

Finalize identification of the application

#### Parameters

Try it out

| Name | Description |
| --- | --- |
|

Authorization *

string

(header)

 |

Auth0 Jwt token to access secured endpoints

*Example* : Bearer token

 |
|

id *

string

(path)

 |

Connect Application UUID

*Example* : ap_0eac0726-f864-4b37-9915-c91b003fdec1

 |

#### Responses

Response content type

*/*

| Code | Description |
| --- | --- |
| 200 |

OK

-   Example Value
-   Model

```
{
  "id": "string",
  "url": "string"
}

```

 |
| 400 |

BAD REQUEST

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "errorContainer": {
    "errorList": [
      {
        "description": "string",
        "property": "string"
      }
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 403 |

FORBIDDEN

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 404 |

NOT FOUND

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 500 |

BAD REQUEST

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |

GET​/applications

Get all applications by partner ID

Get all applications by partner ID provided in token

#### Parameters

Try it out

| Name | Description |
| --- | --- |
|

Authorization *

string

(header)

 |

Auth0 Jwt token to access secured endpoints

*Example* : Bearer token

 |
|

page

string

(query)

 |

Page

*Example* : 1

 |
|

perPage

string

(query)

 |

Items per page

*Example* : 1

 |

#### Responses

Response content type

*/*

| Code | Description |
| --- | --- |
| 200 |

OK

-   Example Value
-   Model

```
{
  "filters": {},
  "value": {}
}

```

 |
| 206 |

Partial Content

-   Example Value
-   Model

```
{
  "items": [
    {
      "amount": 0,
      "applicant": {
        "additionalName": "string",
        "allow_person_report_fetch": true,
        "dateOfBirth": "string",
        "email": "string",
        "familyName": "string",
        "givenName": "string",
        "nationalIdentificationNumber": "string",
        "phone": "string",
        "placeOfBirth": "string",
        "politicallyExposedPerson": true
      },
      "createDate": "string",
      "id": "string",
      "organization": {
        "email": "string",
        "nationalOrganizationNumber": "string",
        "phone": "string",
        "url": "string"
      },
      "purposeOfLoan": "BUY_EQUIPMENT",
      "status": "string",
      "term": 0,
      "updateDate": "string",
      "url": "string"
    }
  ],
  "page": 0,
  "pages": 0,
  "perPage": 0,
  "total": 0
}

```

 |
| 400 |

BAD REQUEST

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "errorContainer": {
    "errorList": [
      {
        "description": "string",
        "property": "string"
      }
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 401 |

UNAUTHORIZED

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 403 |

FORBIDDEN

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 404 |

NOT FOUND

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}

```

 |
| 500 |

INTERNAL ERROR

-   Example Value
-   Model

```
{
  "cause": {
    "localizedMessage": "string",
    "message": "string",
    "stackTrace": [
      {
        "className": "string",
        "fileName": "string",
        "lineNumber": 0,
        "methodName": "string",
        "nativeMethod": true
      }
    ],
    "suppressed": [
      null
    ]
  },
  "localizedMessage": "string",
  "message": "string",
  "stackTrace": [
    {
      "className": "string",
      "fileName": "string",
      "lineNumber": 0,
      "methodName": "string",
      "nativeMethod": true
    }
  ],
  "suppressed": [
    {
      "localizedMessage": "string",
      "message": "string",
      "stackTrace": [
        {
          "className": "string",
          "fileName": "string",
          "lineNumber": 0,
          "methodName": "string",
          "nativeMethod": true
        }
      ],
      "suppressed": [
        null
      ]
    }
  ]
}
```

`\
`

 |
