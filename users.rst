Users
=====

The users endpoint supports creating, fetching, and searching for users
within the data platform. It is protected and requires authentication.

Create data platform user
-------------------------

::

    POST /users

This endpoint accepts an external identifier which can later be used to
retrieve the data platform user identifier.

**Input**

::

    POST /users
    Content-Type: application/json

.. code:: json

    {
      "LocaleCode": "en-US",
      "ExternalId": "123456"
    }

**Response**

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8

.. code:: json

    {
      "Id": "f9c17928-5587-4da9-babb-941796efd8f5",
      "LocaleCode": "en-US",
      "ExternalId": "123456"
    }

Retrieve data platform user
---------------------------

::

    GET /users/{userid}

**Response**

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8

.. code:: json

    {
      "Id": "f9c17928-5587-4da9-babb-941796efd8f5",
      "LocaleCode": "en-US",
      "ExternalId": "123456"
    }

Search for data platform user
-----------------------------

::

    GET /users?externalid={externalid}

**Response**

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8

.. code:: json

    [
      {
        "Id": "f9c17928-5587-4da9-babb-941796efd8f5",
        "LocaleCode": "en-US",
        "ExternalId": "123456"
      },
      {
        "Id": "a5c12867-5587-4da9-babb-941796efd8f5",
        "LocaleCode": "en-US",
        "ExternalId": "123456"
      }
    ]
