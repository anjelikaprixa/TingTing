API
===

.. autosummary::
   :toctree: generated

   lumache
n

Introduction
=============

TingTing is an AI-powered telephony system that lets you send programmed voice calls in Nepali to thousands of recipients with just a few clicks. Features include scheduling tools and customized messaging options. The TingTing API is well-documented and easy to use, providing maximum flexibility and customization for developers building custom applications or endpoints.

Authentication
---------------

Login Endpoint
~~~~~~~~~~~~~~

.. list-table:: Title
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/accounts/login/
     - email, password  
     - POST

After successful authentication you will get an access token. This token needs to be provided for every further request.

Sample Input:
::
	{
		"email": "test@gmail.com",

		"password": "test"
	}

User Detail Endpoint
~~~~~~~~~~~~~~~~~~~~
.. list-table:: Title
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/accounts/user_details/
     -   
     - GET

You can get all details of the user that is currently logged in via a GET request.

Refresh Token Endpoint
~~~~~~~~~~~~~~~~~~~~~~
.. list-table:: Title
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/accounts/token/refresh/?
     -   
     - POST
    
The access token provided during authentication expires after some time and a new one is required. The refresh token is used to generate a new access token.

Campaign
--------

Get Campaign Endpoint
~~~~~~~~~~~~~~~~~~~~~

.. list-table:: Title
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * -{{url}}/api/system/campaigns
     -   
     - GET

Information of all campaigns of logged in users are retrieved at this endpoint. The information includes the campaign id, name, user phones, services, descriptions and usable tags. The id is to be used in the future to update, delete or begin the campaign. Tags can be used to send personalized messages to users while  starting the campaign.

Here is an example of the result:

.. code-block:: json

   {
       "pagination": {
           "total_items": 3,
           "total_pages": 1,
           "page_number": 1,
           "has_next": false,
           "has_previous": false,
           "links": []
       },
       "result": {
           "messages": "Campaign Successfully Retrieved",
           "campaign-lists": [
               {
                   "id": 8,
                   "name": "sample individual campaign",
                   "user_phone": [],
                   "services": "PHONE",
                   "description": "This campaign is to notify users that an IPO has been opened",
                   "usable_tags": []
               },
               {
                   "id": 5,
                   "name": "test1",
                   "user_phone": [],
                   "services": "SMS",
                   "description": "test campaign",
                   "usable_tags": ["tags_name", "tags_age"]
               },
               {
                   "id": 3,
                   "name": "Sample",
                   "user_phone": [],
                   "services": "PHONE",
                   "description": "Description",
                   "usable_tags": []
               }
           ]
       }
   }
