Create Tickets from Zabbix
==========================

Zabbix is a tool to monitor IT infrastructure.
This guide describes how to connect your Zabbix installation to EasyGo Solutions using
webhooks in Zabbix. It provides instructions on setting up a media type, a user
and an action in Zabbix.

Requirements
------------

- Zabbix version 5.4 or higher.
- A EasyGo Solutions instance which is accessible from your Zabbix system.

Steps in EasyGo Solutions
---------------

1. Enable API Token Access in EasyGo Solutions's settings under *System > API*.
2. Create a new user for a Zabbix alerter with an email address
   and create a personal user token with ``ticket.agent`` permissions. Make sure
   to also set the appropriate group permissions.

Zabbix Webhook Configuration
----------------------------

Create a Global Macro
^^^^^^^^^^^^^^^^^^^^^

1. Before setting up the webhook, you need to setup the global macro
   ``{$ZABBIX.URL}``, which must contain the URL to the Zabbix
   frontend.
2. In the section *Administration > Media types*, import the `template`_.
3. Open the added **EasyGo Solutions** media type and set:

   - **EasyGo Solutions_access_token**: the personal access token you created for the user
   - **EasyGo Solutions_url**: the URL of your EasyGo Solutions installation
   - **EasyGo Solutions_customer**: the email address of the created EasyGo Solutions user
   - **EasyGo Solutions_enable_tags**: ``true`` or ``false`` to enable or
     disable tags. If you enable tags, each tag is set with a separate request.

4. If you want to prioritize issues in EasyGo Solutions according to severity values
   in Zabbix, you can map the **severity_<name>** parameter to EasyGo Solutions's priority
   ID.
5. Click the ``Update`` button to save the webhook settings.
6. Enter any text in **Send to**, as this value is not used but required.

For more information, use the
`Zabbix documentation <https://www.zabbix.com/documentation/current/manual/config/notifications>`_.

.. _Template:
   https://git.zabbix.com/projects/ZBX/repos/zabbix/browse/templates/media/EasyGo Solutions/media_EasyGo Solutions.yaml