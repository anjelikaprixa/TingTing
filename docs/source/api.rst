API
===

.. autosummary::
   :toctree: generated

   TingTing



Authentication
---------------

Login Endpoint
~~~~~~~~~~~~~~

.. list-table:: 
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
.. list-table:: 
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
.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/accounts/token/refresh/
     -   
     - POST
    
The access token provided during authentication expires after some time and a new one is required. The refresh token is used to generate a new access token.

Campaign
--------

Get Campaign Endpoint
~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
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

Add Campaign Endpoint
~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - Other Values
     - HTTP Methods
   * - {{url}}/api/system/campaigns/
     - name, services, individual_number, or send_to_number_file
     - description
     - POST

To add a campaign, you'll need to access the campaign endpoint using the HTTP POST method. The required inputs for creating a campaign include the name of the campaign, the services offered by the campaign, and the recipient phone numbers.

To add individual recipients, you'll need to provide their phone number as an individual input in a list. If you want to add multiple recipients, you can send a file containing the phone numbers in .xlsx format.

Sample Input:

.. code-block:: json

   {
       "name": "sample individual campaign",
       "services": "PHONE",
       "individual_number": [9876543210, 98675432123]
   }

   {
       "name": "sample bulk campaign",
       "services": "SMS",
       "send_to_number_file": "numbers.csv"
   }

The description field for the campaign is to keep the general explanation of the campaign and it is optional.

Sample input with description:

.. code-block:: json

   {
       "name": "sample individual campaign",
       "services": "PHONE",
       "individual_number": [9876543210, 98675432123],
       "description": "This campaign is to notify users that an IPO has been opened"
   }


Update Campaign Endpoint
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - Other Values
     - HTTP Methods
   * - {{url}}/api/system/campaigns/<campaign_id>/update
     - Campaign ID
     - name, services, description
     - PUT

To update a campaign, you'll need to provide the campaign ID in the URL of the API endpoint. In addition to the campaign ID, you'll also need to provide the new values that will replace the existing values in the campaign.

{{url}}/api/system/campaigns/10/update/

Sample Input:

.. code-block:: json

   {
       	"name":"new campaign name",	
	"services": "SMS",
	"description": "Election campaign for 2023"
   }

Note that the <campaign_id> in the URL should be replaced with the ID of the campaign you want to update.

Delete Campaign Endpoint
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/system/campaigns/<campaign_id>/delete
     - Campaign ID
     - DEL
     
Note that the <campaign_id> in the URL should be replaced with the ID of the campaign you want to delete.

Campaign Details Endpoint
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/system/campaigns/<campaign_id>/details
     - Campaign ID
     - DEL
     
Note that the <campaign_id> in the URL should be replaced with the ID of the campaign you want to delete.

Test Voice Endpoint
~~~~~~~~~~~~~~~~~~~~~~
To test a voice, a sample message needs to be provided.

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/system/test/voice/
     - message
     - POST
     
To test a voice, a sample message needs to be provided.


     
Begin Campaign Endpoint
~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - Other Values
     - HTTP Methods
   * - {{url}}/api/system/campaigns/<campaign_id>/begin/
     - message
     - audio,voice_input, schedule_date,aud_file,priority,status
     - POST
     
Note that the <campaign_id> in the URL should be replaced with the ID of the campaign you want to begin.

Note: that if you have a text message as well as an audio in your campaign, you need to define which one your campaign should start with using the priority attribute.

The options are “message” and “audio”.

Sample Input:


.. code-block:: json

   {
       "priority": "message"
   }
   
You can also add your own message or audio. If you want to change the existing message or aud_file, you can do so by providing your own.

.. code-block:: json

   {
       "message" : "Hi, this is to notify that you have been selected for the election"
   }
   
Furthermore, you can also add available tags to your message using variables and passing it inside curly braces.

Sample Tags:

Message: “Hi {tags_name}, you are {tags_age} years old and your salary is {tags_salary}.”

If you want to schedule a campaign you need to pass a schedule date and time  in the following format:

.. code-block:: json

   {
       "schedule_date": "2023-05-09T17:07"
   }

Sample Input for personal message:

 
 .. code-block:: json

   {
       "message": "sample text message"
   }
   
Sample input for personal audio:

 .. code-block:: json

   {
       "aud_file": "path/containing/audio.mp3"
   }
   
You also have the option to change the voice input for the campaign you want to begin. The options are “np_rija”, “np_prasanna” and “np_binod”

Sample Input:

 .. code-block:: json

   {
       "message": "Message to Convey",
	"voice_input": "np_prasanna"
   }
   
To re-run a campaign you need to provide the campaign id in the same URL with “status” in the data. Specific actions inside the campaign specified by the status can also be re-started by entering the following input format.

Valid options are 'hungup', 'unanswered', 'failed', 'terminated' and 'completed'

Sample input to re-run a campaign based on the status:

 .. code-block:: json

   {
       "message": "Here you send your message you want to convey",
	"status": "Failed"
   }

This will start the campaign for all numbers whose status is failed.


Sample input encompassing all attributes:

 .. code-block:: json

   {
	"message": "Hi {tags_name}, you are {tags_age} years old and your salary is {tags_salary}.",
	"aud_file" :   "path/containing/audio.mp3",
	"priority": "message",
	"voice_input": "np_prasanna",
	"schedule_date": "2023-05-09T17:07",
	"status": "failed"
   }

Phone Numbers
--------------

Owned Numbers Endpoint
~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/system/owned/phone_numbers
     - 
     - GET
  
By accessing this endpoint, you can retrieve details for all phone numbers associated with the currently logged-in user. These details include the phone number itself, its capabilities for voice, SMS, MMS, and fax, the rate of the number, the SID, friendly name, and other relevant information.

Numbers List Endpoint
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/system/phone_numbers
     - 
     - GET
  
By accessing this endpoint, you can retrieve details for all phone numbers not associated with any users and are available to buy. These details include the phone number itself, its capabilities for voice, SMS, MMS, and fax, the rate of the number, the SID, friendly name, and other relevant information.

Buy Number Endpoint
~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/system/phone_numbers
     - SID
     - POST
     
Through the POST method of this endpoint, you will be able to buy a number that is in the numbers list by providing the SID of the number you want to buy.

Sample Input:

 .. code-block:: json

   {
	"phone_sid":"b7142c5ae3b673d944d81c83bda4f5de"
   }
   
Release Number Endpoint
~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/system/phone_numbers
     - SID
     - DEL
     
Through the DEL method of this endpoint, you will be able to release a number that you currently own by providing the SID of the number you want to release.


Sample Input:

 .. code-block:: json

   {
	"phone_sid":"b7142c5ae3b673d944d81c83bda4f5de"
   }
   
Campaign Action
----------------

Number List Endpoint
~~~~~~~~~~~~~~~~~~~~~
.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/system/campaigns/number/<campaign_id>
     - Campaign ID
     - GET

Note that the <campaign_id> in the URL should be replaced with the ID of the campaign you want to retrieve the numbers of. 	The details include the id of the number, the number itself, the campaign name it is affiliated to, its status, the duration, playback and credit consumed by the number. If tags are available, tags will also be retrieved from this endpoint.

The ID will be used to then delete and edit the number from the campaign.

Add Number to a Campaign Endpoint
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/system/campaigns/number/<campaign_id>
     - Campaign ID, number
     - POST
  
Note that the <campaign_id> in the URL should be replaced with the ID of the campaign you want to add a number to and the number to add should be passed as an integer in the following way:

Sample Input:

 .. code-block:: json

   {
	"number": 9843812344
   }
   

Note that if you want to add numerous numbers to a campaign you have to send data in the format of the sample input repeatedly. 
To add tags to a number added in a bulk campaign, you will need to provide the tags inside the available tags attribute. Note that the tags you use should be in the “usable_tags” of the campaign.

Sample Input:

 .. code-block:: json

   {
	"number": 9832123432,
	"available_tags":{"tags_name": "name","tags_age": 25}
   }
 
Delete Action Endpoint
~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/system/campaigns/number/<number_id>/delete/
     - Number ID
     - DEL 

Note that the <number_id> in the URL should be replaced with the ID of the number you want to delete from the campaign.
 
 
Number Information Endpoint
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/system/number/<number_id>/
     - Number ID
     - GET
     
Note that the <number_id> in the URL should be replaced with the ID of the number you want to retrieve the information of.


Number Edit Endpoint
~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 50
   :header-rows: 1

   * - URL
     - Required Values
     - HTTP Methods
   * - {{url}}/api/system/number/<number_id>/
     - Number ID, Values to change
     - POST

Note that the <number_id> in the URL should be replaced with the ID of the number you want to edit the details of.  The attributes of the number you want to change also needs to be provided.

If you already have tags while creating the campaign, you can edit your tags while also editing your number. To do so you will need to provide the available tags along with the new number you want to keep.

Sample Input:

 .. code-block:: json

   {
	"number": 9832123432,
	"available_tags":{"tags_name": "name","tags_age": 25}
   }


OTP 
----

Send OTP Endpoint
~~~~~~~~~~~~~~~~~~

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 1

   * - URL
     - Required Values
     - Other Values
     - HTTP Methods
   * - {{url}}/api/system/send/otp
     - number, message, sms_send_options
     - otp_length, otp_options
     - POST
     
By utilizing this endpoint, you can send OTPs to users by specifying the recipient's phone number as a string, along with the message containing the OTP and the desired delivery method - either through “voice” or “text” through the sms_send_option attribute. The OTP can be integrated in the message by passing it inside curly braces of the messages attribute.

For Example,

 .. code-block:: json

   {
	"message" : "Hi Your OTP is {otp}"
   }

In addition, you have the flexibility to choose between sending your own OTP or generating it automatically through the OTP options attribute. The available options are "personnel" and "generated". If you choose "personnel", you'll need to provide the OTP yourself. On the other hand, if you select "generated", the OTP will be auto-generated. In the “generated” scenario, you can specify the length for the auto-generated OTP. If nothing is provided, by default a generated OTP will be provided.

Sample Input For Customized OTP

 .. code-block:: json

   {
	"number": "9851023212",
	"message": "Hi your OTP is {otp}",
	"sms_send_options": "text",
	"otp_options": "personnel",
	"otp": "12345"
   }

Sample Input For Auto-Generated OTP


 .. code-block:: json

   {
	"number": "9851023212",
	"message": "Hi your OTP is {otp}",
	"sms_send_options": "voice",
	"otp_options": "generated",
	"otp_length": "4"
   }




