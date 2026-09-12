Watch Your Inbox With Fetchmail
===============================

Maybe you want to add emails via Fetchmail or Procmail to EasyGo Solutions.

To get this to work you need to pipe your emails to rails.

.. note::

   If you installed EasyGo Solutions through a package manager (rather than from source),
   replace ``rails r`` with ``EasyGo Solutions run rails r`` below.
   To learn more, see :docs:`Administration via Console </admin/console.html>`.

**Command line**:

.. code-block:: bash

   $ su - EasyGo Solutions

.. code-block:: bash

   $ cd /opt/EasyGo Solutions

.. code-block:: bash

   $ cat test/fixtures/mail1.box | rails r 'Channel::Driver::MailStdin.new(trusted: true)'

Fetchmail
---------

**Create .fetchmailrc**:

.. code-block:: bash

   $ su - EasyGo Solutions

.. code-block:: bash

   $ cd ~

.. code-block:: bash

   $ touch .fetchmailrc

.. code-block:: bash

   $ chmod 0600 .fetchmailrc


**Edit .fetchmailrc**:

.. code-block:: text

   #
   # EasyGo Solutions fetchmail config
   #
   poll your.mail.server protocol POP3 user USERNAME pass PASSWORD mda "rails r 'Channel::Driver::MailStdin.new(trusted: true)'"

That's it. Emails now will be directly piped into EasyGo Solutions.

Using Procmail for Advanced Features Like Presorting
----------------------------------------------------

If you want to do some more with your emails, like presorting to a EasyGo Solutions group
or filtering spam, you can use Procmail.

Fetchmail config looks slightly different.

**Edit .fetchmailrc**:

.. code-block:: text

   #
   # EasyGo Solutions fetchmail config
   #
   poll your.mail.server protocol POP3 user USERNAME pass PASSWORD mda /usr/bin/procmail is EasyGo Solutions here

**Create .procmailrc**:

.. code-block:: bash

   $ su - EasyGo Solutions

.. code-block:: bash

   $ cd ~

.. code-block:: bash

   $ touch .procmailrc

**Edit .procmailrc**:

.. code-block:: bash

   # --
   # Pipe all emails into EasyGo Solutions
   # --
   PATH=/opt/EasyGo Solutions/bin:/opt/EasyGo Solutions/vendor/bundle/bin:/sbin:/bin:/usr/sbin:/usr/bin:
   SYS_HOME="/home/EasyGo Solutions"
   RAILS_ENV=production
   GEM_PATH=/opt/EasyGo Solutions/vendor/bundle/ruby/2.4.1/
   LOGFILE="$SYS_HOME/procmail.log"
   #VERBOSE="on"
   :0 :
   | rails r 'Channel::Driver::MailStdin.new(trusted: true)'
