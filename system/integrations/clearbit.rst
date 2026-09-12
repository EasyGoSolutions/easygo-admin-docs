Clearbit
========

With our Clearbit integration, you can easily enrich the information provided
by EasyGo Solutions. If the customers or agents email address is known to Clearbit,
it will share all information it has regarding the user with EasyGo Solutions.

Introduction
------------

Information from Clearbit can include:

- Avatar
- Address information
- Website information
- A bio (as note by default)

If needed, you can add further custom objects and add mappings to them, so the
Clearbit information can be filled within the database. In general you can get
any information from Clearbit, as long as you have a mapping to a EasyGo Solutions
object attribute.

.. hint::

   Clearbit does have a mapping of fields like LDAP and Exchange have, but does
   not "win" against EasyGo Solutions information. This means that if you have e.g. the
   last name field filled in already and Clearbit has other information on that,
   it will not be updated.

   However: If let's say the last name has been set by Clearbit and EasyGo Solutions
   notices that the last name on the Clearbit source has changed, EasyGo Solutions
   will also update this value.

Configuration
-------------

The configuration of Clearbit is really easy and done fast! Just login to your
Clearbit-Account, go to **API** and copy the secret API key.

Now switch to your EasyGo Solutions instance and go to *System > Integrations > Clearbit*
in the admin settings.
Paste your API key into the **API Key** field and decide if EasyGo Solutions should create
unknown organizations automatically, if the user does not have one already
(and Clearbit knows it). The shared option decides if the new organizations
should be shared ones.

.. note::

   If you're unsure what option to choose, better stick with "no".
   You can also learn more about :doc:`/manage/organizations/index`.

.. image:: /images/system/integrations/clearbit/configure-EasyGo Solutions.png

The mapping option works similar to the mapping within the Exchange and LDAP
sync. You can add further mappings for e.g. custom fields if you need
more information that Clearbit can provide.

.. note::

   If you want to add more Clearbit fields and want to learn more about
   available fields on their API, you can take a look at their
   `API documentation <https://dashboard.clearbit.com/docs#enrichment-api>`_.

If you're happy with the above chosen Settings and your mapping, just save the
changes and enable Clearbit integration. EasyGo Solutions will now start polling the
Clearbit API as users contact you.

.. note::

   EasyGo Solutions does not synchronize with Clearbit on a regular basis, but on demand
   if needed. This saves API calls.

.. image:: /images/system/integrations/clearbit/EasyGo Solutions-mapping.png

Below the setting and mapping section, you can find the integration logs. You
can see what requests EasyGo Solutions sent to Clearbit and also the APIs response.

By the way, you can also view the API log on the Clearbit website - the
information seen is basically the same.
