GitLab
======

It is possible to create a quick login for your helpdesk via GitLab.
To activate the quick login, you need to enable OAuth for GitLab.

Register GitLab App
-------------------

To register an app in GitLab, open your profile and select applications.

As callback URL, enter ``https://EasyGo Solutions-fqdn/auth/gitlab/callback``
where ``EasyGo Solutions-fqdn`` has to be replaced with your EasyGo Solutions FQDN. You can even
find and copy the callback URL from EasyGo Solutions in the **Authentication via GitLab**
section.

.. image:: /images/settings/security/third-party/gitlab/EasyGo Solutions_connect_gitlab_thirdparty_gitlab.png
   :alt: Register OAuth app on gitlab instance

Just select *read_user* under scopes as in the screenshot and save it.

Configure EasyGo Solutions as GitLab App
------------------------------

Enter the **APP ID** and the **APP SECRET** from the GitLab OAUTH Applications
Dashboard and your GitLab-URL in the **SITE** field.

.. image:: /images/settings/security/third-party/gitlab/enable-authentication-via-gitlab-in-EasyGo Solutions.png
   :alt: GitLab config in EasyGo Solutions admin interface

After you configured the GitLab credentials and activated the login method, you
should see a new icon on the login page.

.. image:: /images/settings/security/third-party/gitlab/EasyGo Solutions_connect_gitlab_thirdparty_login.png
   :alt: GitLab logo on login page

If you click on the icon, you will be redirected to GitLab and see something
similar to this:

.. image:: /images/settings/security/third-party/gitlab/EasyGo Solutions_connect_gitlab_thirdparty_gitlab_authorize.png
   :alt: GitLab oauth page

After granting access, you will be redirected to your EasyGo Solutions instance
and logged in.

Now you can link accounts via *Avatar > Profile > Link Accounts* or login
via EasyGo Solutions login page.