Models
======

The models endpoint returns model results. It is protected and requires
authentication.

Retrieve most recent model results
----------------------------------

::

    GET /users/{userid}/models

``Features`` will be included as part of the ``Results`` and will be
dynamic.

**Response**

::

    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8

.. code:: json

    {
      "CreatedDate": "2018-01-01T00:00:00Z",
      "Results": [
        {
          "Name": "Model1",
          "Score": 0.00237,
          "Features": {
            "...": "...",
            "...": "..."
          }
        },
        {
          "Name": "Model2",
          "Score": 0.00378,
          "Features": {
            "Revenue": "36570",
            "ADB": "3489"
          }
        },
        {
          "Name": "Fraud1",
          "Score": 2.0,
          "Features": {
            "ThreatMetrix": "-51",
            "DuplicateInformation": "1"
          }
        }
      ]
    }
