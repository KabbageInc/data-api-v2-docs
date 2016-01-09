Providers
=========

The providers endpoint returns the list of providers based upon the
partner, country, and region. It is a protected endpoint and requires
authentication.

Retrieve available providers
----------------------------

::

    GET /providers

**Response**

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8

.. code:: json

    [
      {
        "Name": "PayPal"
      },
      {
        "Name": "eBay"
      },
      {
        "Name": "Yahoo"
      },
      {
        "Name": "Xero"
      },
      {
        "Name": "BankAccount"
      },
      {
        "Name": "Facebook"
      },
      {
        "Name": "Twitter"
      },
      {
        "Name": "AmazonMWS"
      },
      {
        "Name": "..."
      }
    ]
