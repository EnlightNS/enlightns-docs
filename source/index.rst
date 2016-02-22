.. EnlightNS documentation master file, created by
   sphinx-quickstart on Thu Sep 10 18:49:50 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to EnlightNS's API Documentation!
=========================================

This page outlines the EnlightNS APIs and their usage.

The API is hosted at ``https://api.enlightns.com``

POST /api-token-auth
^^^^^^^^^^^^^^^^^^^^
Returns the API authentication token for subsequent calls

**Request Headers**

::

    Content-Type: application/json

..

**Request Body**

::

    {
        "email": "your.email@example.com",
        "password": "p455w0rd"
    }

..

**Response**

::

    {
        "token": "<your_auth_token>"
    }

..


GET /user/record/
^^^^^^^^^^^^^^^^^
Lists a user's records

**Request Headers**

::

    Authorization: <your_auth_token>

..

**GET Parameters**

- ``type`` (*optionnal*), used to filter record type
    - ``A``
    - ``A,AAAA``
    - ``CNAME``


**Response**

::

    [
        {
            "id": 402,
            "name": "domain1.enlightns.info",
            "type": "A",
            "content": "54.238.66.12",
            "ttl": 3600,
            "auth": null,
            "active": true,
            "is_free": true,
            "owner": "your_user"
        },
        {
            "id": 418,
            "name": "domain2.enlightns.info",
            "type": "CNAME",
            "content": "domain2.enlightns.info",
            "ttl": 60,
            "auth": null,
            "active": true,
            "is_free": true,
            "owner": "your_user"
        }
    ]

..

GET /user/record/<record_id>
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Gets the details for one record

**Request Headers**

::

    Authorization: <your_auth_token>

..

**Request Parameters**

- ``record_id``: ID of the record to retrieve

**Response**

::

    {
        "id": 26,
        "name": "ns2.enlightns.org",
        "type": "A",
        "content": "192.99.43.21",
        "ttl": 86400,
        "auth": null,
        "active": true,
        "is_free": false,
        "owner": "d2s3admin"
    }

..


PUT /user/record/<record_id>
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Updates the content of a record

**Request Headers**

::

    Authorization: <your_auth_token>
    Content-Type: application/json

..

**Request Parameters**

- ``record_id``: ID of the record to update

**Request Body**

::


    {
        "content": "<new_record_content>"
    }

..

**Response**

::

    {
        "id": 402,
        "name": "domain1.enlightns.info",
        "type": "A",
        "content": "<new_record_content>",
        "ttl": 3600,
        "auth": null,
        "active": true,
        "is_free": true,
        "owner": "your_user"
    }

..

GET /tools/whatismyip/
^^^^^^^^^^^^^^^^^^^^^^
Returns your public IP

**Response**

::

    {
        "ip": "184.55.30.206"
    }

..


GET /nic/update/?username=<username>&password=<password>&ip=<ip_address>&hostname=<hostname>
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Update your IP using a one liner
*HTTP is available ONLY for this API and very old router who wouldn't support HTTPS*

**Request Parameters**

- ``username``: the email you registered with
- ``password``: your password
- ``ip``:       your IP address
- ``hostname``: your hostname (my_hostname.example.com)

**Response**

::

    good 74.152.77.75

..