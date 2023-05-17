API
===

.. autosummary::
   :toctree: generated

   lumache
n

# Introduction

TingTing is an AI-powered telephony system that lets you send programmed voice calls in Nepali to thousands of recipients with just a few clicks. Features include scheduling tools and customized messaging options. The TingTing API is well-documented and easy to use, providing maximum flexibility and customization for developers building custom applications or endpoints.

Authentication

Login Endpoint


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

.. code-block:: Json
	{
		"email": "test@gmail.com",

		"password": "test"
	}

