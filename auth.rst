Auth
====

The Kabbage Data Platform API uses the `OAuth
2.0 <http://tools.ietf.org/html/rfc6749>`__ protocol for authentication.
The API supports the client\_credentials grant type flow for making
authorized calls to the protected endpoints.

Obtain authorization token
--------------------------

::

    POST /auth/token

**Input**

code-block:: json

    POST /auth/token
    Content-Type: application/x-www-form-urlencoded

    grant_type=client_credentials&
    client_id=CLIENT_ID&
    client_secret=CLIENT_SECRET

**Response**

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8

.. code:: json

    {
      "access_token": "owiflakshlkashflkajshf",
      "token_type": "bearer",
      "expires_in": 86399
    }
