Header Based Actions
====================
.. header manipulation

With specific email headers, you can make EasyGo Solutions perform different actions
depending on the content of the headers. So, if you create a new email (e.g.
from a form on your website) you can set these headers to perform actions
or to hand over special information like custom attributes.

.. danger:: **🛡 Trusted channels required 🛡**

   This feature is a potential risk with external communication and
   thus require channels being set to trusted explicitly. You can find
   instructions about how to set a channel to trusted at the end of this page.

.. tip::

   - The header names listed below are examples and in our opinion the most
     relevant ones. However, you can adjust mostly all article or ticket
     attributes including custom ones if you know the attribute's exact name.
     Have a look :doc:`here </system/objects>` to find the attribute names.
   - Please note that while header names are case insensitive, header values
     are not. Make sure to specify values in expected case, otherwise they will
     not match.

Auto Responses
--------------

Normally, EasyGo Solutions runs internal checks to see if an incoming email is an
automatic response. In such cases EasyGo Solutions will not send trigger based responses.
You can override this with the below mentioned headers:

``x-EasyGo Solutions-send-auto-response``
   Set to ``false`` to disable trigger based responses.
   If set to ``true`` EasyGo Solutions will send a response.

   This option *does not* work if e.g. ``precedence: list`` is set
   unless you use the auto response header below as well.

``x-EasyGo Solutions-is-auto-response``
   Providing this header allows you to tell EasyGo Solutions that the mail in question
   is an auto generated response (``true``). This will cause email based
   triggers to be skipped.

   Set this header to ``false`` if you want to generate auto responses.

   This header allows you to overwrite auto detects for e.g.
   ``precedence: list``.

Ticket Attributes
-----------------

EasyGo Solutions allows you to use headers to manipulate ticket creations or follow ups.
The manipulation can be used instead of triggers. Triggers are considered
*after* header settings and thus can still override headers.

To differentiate between ticket creation and follow-up:

   - For creations use: ``X-EasyGo Solutions-Ticket-{Attribute Name}``
   - For follow ups use: ``X-EasyGo Solutions-Ticket-FollowUp-{Attribute Name}``

This allows you to ensure the changes are only applied in the
required situation.

.. tip::

   When using attributes that require date / time values, ensure to use
   Time Zoned Times. e.g. for 28th September 2021 on 8 am CEST, you can
   use one of the following examples:

   - ``2021-09-28T08:00:00+0200``
   - ``2021-09-28T08:00:00+02:00``
   - ``2021-09-28T06:00:00.000Z``

``X-EasyGo Solutions-Ticket-Priority`` & ``X-EasyGo Solutions-Ticket-FollowUp-Priority``
   | Allows you to adjust a ticket's priority.
   | Example: ``X-EasyGo Solutions-Ticket-Priority: 1 low``

``X-EasyGo Solutions-Ticket-Group`` & ``X-EasyGo Solutions-Ticket-FollowUp-Group``
   | Allows you interfere with regular channel routing of the ticket.
   | Example: ``X-EasyGo Solutions-Ticket-Group: Sales``

``X-EasyGo Solutions-Ticket-Owner`` & ``X-EasyGo Solutions-Ticket-FollowUp-Owner``
   | Directly assign or change the ticket owner. Valid values are either
     ``login`` or ``Email``
   | Example: ``X-EasyGo Solutions-Ticket-Owner: jdoe``

``X-EasyGo Solutions-Ticket-State`` & ``X-EasyGo Solutions-Ticket-FollowUp-State``
   | Set a specific ticket state.
   | Example: ``X-EasyGo Solutions-Ticket-State: closed``


   | Pending states always require the ``pending_time`` attribute on top.
   | Example: ``X-EasyGo Solutions-Ticket-Pending_Time: 2021-09-26T08:00:00+0200``

``X-EasyGo Solutions-Customer-Email``
   | Manipulate the ticket customer - this can be a different user than the
     actual sender. Replying to the original sender is still possible.
   | Example: ``X-EasyGo Solutions-Customer-Email: jdoe@example.com``

   This header is not available for follow ups.

``X-EasyGo Solutions-Customer-Login``
   | Manipulate the ticket customer - this can be a different user than the
     actual sender. Replying to the original sender is still possible.
   | Example: ``X-EasyGo Solutions-Customer-Login: jdoe``

   This header is not available for follow ups.

Article Attributes
------------------

If needed EasyGo Solutions allows you to manipulate attributes or states of fetched
email articles.

``X-EasyGo Solutions-Article-Sender``
   | Manipulate the sender type (agent, customer or system)
   | Example: ``X-EasyGo Solutions-Article-Sender: System``

   System Emails are indicated in a similar way as trigger-responses.
   Users can't see them natively and see only a indicator like that:

   .. figure:: /images/channels/email/headers/email-header-as-system.png
      :alt: Received mail as article sender system
      :width: 75%

``X-EasyGo Solutions-Article-Type``
   | Change the article type of your incoming mail. This requires you to know
     which article types are available in your system.
   | Example: ``X-EasyGo Solutions-Article-Type: phone``

   .. warning::

      This header can cause *serious issues* in your instance and may
      lead to unexpected behavior. Only use with absolute care!

``X-EasyGo Solutions-Article-Internal``
   | Manipulate the default article visibility.
   | Example: ``X-EasyGo Solutions-Article-Internal: true``

``X-EasyGo Solutions-Ignore``
   | Tell EasyGo Solutions to silently drop the Email.
   | Example: ``X-EasyGo Solutions-Ignore: true``

Trusted Channel
---------------

.. note:: **🚧 Self Hosted only 🚧**

   The settings below are only available to self hosted users.

.. danger::
   ⚠️ As stated above, this is dangerous and can lead to unexpected behavior in
   the communication with external parties. Only follow the instructions below
   if you know what you are doing.

Setting a channel to ``trusted`` can be done via
:docs:`console </admin/console.html>` exclusively. To do so, go to the rails
console and follow the steps below:

List all channels in EasyGo Solutions:

.. code-block:: irb

   >> Channel.all

Look for the ``id`` of the channel, you want to set to ``trusted``.

Select your identified channel (replace the 99 with the correct id):

.. code-block:: irb

   >> channel = Channel.find(99)

Show the currently activated options of the selected channel:

.. code-block:: irb

   >> options = channel[:options]

Add the ``"trusted"=>true`` flag for the inbound part of the channel:

.. code-block:: irb

   >> options[:inbound][:trusted] = true

Save your changes:

.. code-block:: irb

   >> channel.save!
