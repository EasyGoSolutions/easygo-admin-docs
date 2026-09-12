GitHub
======

It is possible to create a quick login for your helpdesk via GitHub.
To activate the quick login, you need to enable OAuth for GitHub.

Register GitHub App
-------------------

Visit https://www.github.com/settings/applications/new and enter the app
settings. As callback URL, enter ``https://EasyGo Solutions_host/auth/github/callback``
where ``EasyGo Solutions_host`` has to be replaced with your EasyGo Solutions FQDN. You can even
find and copy the callback URL from EasyGo Solutions in the **Authentication via GitHub**
section.

.. image:: /images/settings/security/third-party/github/EasyGo Solutions_connect_github_thirdparty_github.png
   :alt: Register OAuth app on www.github.com

Configure EasyGo Solutions as GitHub App
------------------------------

Enter the **APP ID** and the **APP SECRET** from the GitHub OAUTH Applications
Dashboard:

.. image:: /images/settings/security/third-party/github/enable-authentication-via-github-in-EasyGo Solutions.png
   :alt: GitHub config in EasyGo Solutions admin interface

After you configured the GitHub credentials and activated the login method, you
should see a new icon on the login page.

.. image:: /images/settings/security/third-party/github/EasyGo Solutions_connect_github_thirdparty_login.png
   :alt: GitHub logo on login page

If you click on the icon you will be redirected to GitHub and see something
similar to this:

.. image:: /images/settings/security/third-party/github/EasyGo Solutions_connect_github_thirdparty_github_authorize.png
   :alt: GitHub oauth page

After granting access, you will be redirected to your EasyGo Solutions instance
and logged in.

Now you can link accounts via *Avatar > Profile > Link Accounts* or login
via EasyGo Solutions login page.
