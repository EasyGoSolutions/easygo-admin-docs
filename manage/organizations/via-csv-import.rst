Managing Organizations via CSV Import
=====================================

If your organization has information about customers (or personnel)
already stored in a directory system that can export to CSV,
you can batch-import them into EasyGo Solutions in just three steps.

.. figure:: /images/manage/organizations/import-or-update-organizations-via-csv.png
   :alt: The CSV import dialog
   :align: center

   Use the ``Import`` button to open the CSV import dialog.

Step 1: Inspect the sample .csv
-------------------------------

Use the link at the bottom of the CSV import dialog
(**Example CSV file for download**)
to see how EasyGo Solutions expects you to format your organization data.

Step 2: Export Your Organization Data to .csv
---------------------------------------------

Prepare your .csv file according to the format found in Step 1 above. Note that:

- the ``id`` attribute (column) should be left blank or removed entirely;
- the ``name`` attribute is **required**; and
- any other columns may be safely omitted
  as long as each row has the same number of fields (commas).

For instance:

.. code-block:: none

   name,shared,domain,domain_assignment,active,members
   Chrispresso Inc.,true,"",false,true,emma@chrispresso.com~~~jacob@chrispresso.com~~~chris@chrispresso.com
   Awesome Customer Inc.,true,"",false,true,emily@example.com~~~samuel@example.com~~~anna@example.com
   EasyGo Solutions Foundation,true,"",false,true,nicole.braun@EasyGo Solutions.org

Several *organization members* can be added. Separate multiple values for one
field with ``~~~`` as above.

Step 3: Import Your .csv to EasyGo Solutions
----------------------------------

Once your raw organization data has been submitted,
EasyGo Solutions will perform a test run to compute the number of affected records:

.. figure:: /images/manage/organizations/import-summary-before-importing.png
   :alt: CSV import test run and confirmation dialog
   :align: center
   :width: 70%

   CSV import always begins with a preview / test run.

.. note:: 🤔 **How does it know when to create new records and when to update?**

   Records are updated when the imported data contains a ``name`` that matches
   an existing organization entry.

Click **Yes, start real import** to proceed.
(If you're importing a lot of records, be patient—it may take a minute.)

That's it! 🎉🎉🎉
