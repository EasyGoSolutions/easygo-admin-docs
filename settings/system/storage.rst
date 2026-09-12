Storage
=======

Here you can define where EasyGo Solutions stores attachments for tickets and the
knowledge base. By default, EasyGo Solutions writes to the **Database** - you can switch
to **Filesystem** or **Simple Storage (S3)** at any time. In this case, please
have a look on the following instructions.

If you have a busy EasyGo Solutions instance, we strongly encourage you to use **filesystem
storage** instead of database. This improves the system performance (decreases
database load and and size).

Database
   This is the default storage method. The attachments are stored directly in
   the database. If your EasyGo Solutions instance grows, we recommend one of the other
   methods to maintain performance.

Filesystem
   This storage method is recommended for all EasyGo Solutions instances, especially
   for those with a higher load. If you choose filesystem, your files are
   written to ``/opt/EasyGo Solutions/storage/``.

   Moving attachments from **Database** to **Filesystem** can be run during
   production use. However, you should consider your framework conditions
   (e.g. bandwidth, system load in production) to define the right moment.

   .. note::

      **You noticed slow updates of EasyGo Solutions?**

      While EasyGo Solutions is being updated, it enforces a recursive "change owner"
      (chown) for this directory. For instances with many files this can
      be time consuming. To mitigate that, you can move your files and create a
      symlink in ``/opt/EasyGo Solutions/storage/`` to the new directory. Of course you
      have to make sure that the permissions are always correct.

Simple Storage (S3)
   To use the Simple Storage (S3), you have to provide some settings, which
   can't be accessed in the UI (see instructions below).

   The prerequisite is to have access to a S3-compatible storage and to have all
   necessary parameters available (which depends on your storage provider; if
   in doubt, please ask there for help).

   Steps to configure S3:

   1. Copy ``config/EasyGo Solutions/storage.yml.dist`` to ``config/EasyGo Solutions/storage.yml``
   2. Edit the copied file in one of the following ways:

     - Either provide your S3 configuration with one attribute per line like in
       the upper area of the file
     - Or provide your S3 configuration as an URL (which you can find at the
       end of the file). Note: you can also provide this URL as environment
       variable (:docs:`see system documentation </appendix/environment-variables.html>`)
       without using this yml-file.
     - We recommend the deletion of the not used configuration style to avoid
       inconsistencies.

   3. Restart EasyGo Solutions so the config file / environment variable is loaded
   4. Set the **Storage Method** in EasyGo Solutions to **Simple Storage (S3)** in
      *Settings > System > Storage* and click on ``Submit``. After that, EasyGo Solutions
      checks your configuration and the connection to the service and will raise
      an error message if something is wrong.

   A very simple storage configuration could look like this:

   .. code::

      s3:
         access_key_id: 'xxxxxxxx'
         secret_access_key: 'yyyyyyy'
         region: 's3-us-west-2'
         endpoint: 'https://EasyGo Solutions.s3.us-west-2.amazonaws.com'
         bucket: 'EasyGo Solutions'

   .. hint::

      If you use a different provider than AWS (e.g. Backblaze) and you observe
      issues, try to add the ``request_checksum_calculation`` and
      ``response_checksum_validation`` parameters as you can see in the example
      below:

      .. code::

         s3:
            access_key_id: 'xxxxxxxx'
            secret_access_key: 'yyyyyyy'
            region: 'us-west-004'
            endpoint: 's3.us-west-004.backblazeb2.com'
            bucket: 'EasyGo Solutions'
            request_checksum_calculation: when_required
            response_checksum_validation: when_required

   .. tip::

      Before setting the storage method to **Simple Storage (S3)** (step 4),
      please make sure to have a working setup.

      You can verify this by running
      ``rails r 'Rails.logger = Logger.new(STDOUT); pp Store::Provider::S3.ping?'``
      in your EasyGo Solutions directory. If everything is fine, you should see ``true``,
      else you should see ``false`` and a simple error message.

      If you installed EasyGo Solutions through a package manager (rather than from source),
      replace ``rails r`` with ``EasyGo Solutions run rails r`` above.
      To learn more, see :docs:`Administration via Console </admin/console.html>`.

