Provider Accounts
=================

The provider accounts endpoint supports adding and fetching a user's
provider accounts. It is protected and requires authentication.

Retrieve all user provider account details
------------------------------------------

::

    GET /users/{userid}/provideraccounts

``Properties`` are provider specific and may not be required.

The provider account includes a ``Status`` within the response.
Enumerated values include:

-  **Complete** if the provider account has successfully connected
-  **Error** if the data platform failed while adding the provider
   account
-  **Processing** if the data platform is currently communicating with
   the provider account

One or more flags may be returned as a result of issues encountered
while processing the provider account. These flags will contain a
``Category`` and ``Reason``.

``Category`` will be one of the following:

-  **Unauthorized** if the data platform has lost access to the provider
   account
-  **Incomplete** if the provider account requires additional
   information
-  **Error** if the data platform has received an error communicating
   with the provider
-  **Locked** if the provider has locked the provider account

``Reason`` will be one of the following:

-  **CommunicationError** if the data platform encounters a network
   error communicating with the provider
-  **DatabaseError** if the data platform cannot connect to the database
-  **Unauthorized** if the data platform no longer has access to the
   provider due to invalid credentials
-  **Revoked** if the provider has revoked the data platform access
-  **Expired** if the provider credentials have expired
-  **Suspended** if the provider credentials have been suspended
-  **ClosedAccount** if the provider has closed the account
-  **NewTermsRequired** if the provider requires additional terms to be
   accepted before data can be retrieved
-  **NeedsInformationUpdate** if the provider requires additional
   information be reviewed before data can be retrieved
-  **NeedsToViewPromotion** if the provider requires a promotion be
   accepted before data can be retrieved
-  **ForcedDisconnect** if the provider has forced a disconnect from the
   data platform
-  **Exception** if an error occurred communicating with the provider

**Response**

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8

.. code:: json

    [
      {
        "Id": 123,
        "Name": "Business Checking",
        "ProviderName": "BankAccount",
        "Status": "Complete",
        "Flags": [],
        "CreatedDate": "2010-01-01T00:00:00Z",
        "Properties": {
          "...": "...",
          "...": "..."
        }
      },
      {
        "Id": 120,
        "Name": "Business Checking 2",
        "ProviderName": "BankAccount",
        "Status": "Complete",
        "Flags": [
          {
            "Reason": "Unauthorized",
            "Category": "Revoked",
            "CreationDate": "2010-02-01T00:00:00Z"
          }
        ],
        "ExpirationDate": "2018-01-01T00:00:00Z",
        "CreatedDate": "2010-01-01T00:00:00Z",
        "Properties": {
          "...": "...",
          "...": "..."
        }
      }
    ]

Retrieve specific user provider account details
-----------------------------------------------

::

    GET /users/{userid}/provideraccounts/{provideraccountid}

**Response**

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8

.. code:: json

    {
      "Id": 123,
      "Name": "Business Checking",
      "ProviderName": "BankAccount",
      "Status": "Complete",
      "Flags": [],
      "ExpirationDate": "2018-01-01T00:00:00Z",
      "CreatedDate": "2010-01-01T00:00:00Z",
      "Properties": {
        "...": "...",
        "...": "..."
      }
    }

Connect user provider account
-----------------------------

::

    POST /users/{userid}/provideraccounts/connect

``Parameters`` are provider specific and may not be required.

The consuming application should send the user to the ``RedirectUrl``
from the response where they can authenticate and authorize the data
platform. When authentication is complete they will be returned to the
``CallbackUrl`` from the input.

Providers that require authentication require a ``CallbackUrl``.

**Input**

::

    POST /users/{userid}/provideraccounts/connect
    Content-Type: application/json

.. code:: json

    {
      "CallbackUrl": "https://yoursite.com/callback",
      "ProviderName": "BankAccount",
      "Parameters": {
        "...": "...",
        "...": "..."
      }
    }

**Response**

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8

.. code:: json

    {
      "Token": "f9c17928-5587-4da9-babb-941796efd8f5",
      "Result": "Processing",
      "RedirectUrl": "https://dataservice.kabbage.com/"
    }

Get provider account connect status
-----------------------------------

::

    GET /users/{userid}/provideraccounts/connect/{token}

Requires ``Token`` from the provider account connect POST response.

``Result`` will be one of the following:

-  **Processing** if the data platform is still connecting to the
   provider
-  **Success** if the data platform has successfully connected to the
   provider
-  **Error** if the data platform has received an error connecting to
   the provider
-  **Duplicate** if the provider account was already added to the data
   platform under another user
-  **Blacklisted** if the provider account has been added to a blacklist
   in the data platform

**Response**

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8

.. code:: json

    {
      "Id": 1234,
      "Name": "Business Checking",
      "Token": "f9c17928-5587-4da9-babb-941796efd8f5",
      "Result": "Error",
      "ErrorCode": "501",
      "ErrorMessage": "Invalid credentials"
    }

Refresh user provider account
-----------------------------

::

    POST /users/{userid}/provideraccounts/{provideraccountid}/refresh

Refresh provider account.

**Input**

::

    POST /users/{userid}/provideraccounts/{provideraccountid}/refresh
    Content-Type: application/json

**Response**

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8

Delete user provider account
----------------------------

::

    DELETE /users/{userid}/provideraccounts/{provideraccountid}

Delete provider account.

**Input**

::

    DELTE /users/{userid}/provideraccounts/{provideraccountid}
    Content-Type: application/json

**Response**

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8
