SAML with Keycloak
==================

Step 1: Keycloak Configuration
------------------------------

- **To add EasyGo Solutions as a client,**
  save the XML configuration to disk
  (``https://your.EasyGo Solutions.domain/auth/saml/metadata``)
  and use *Clients > Clients list > Import client* in the Keycloak admin
  panel.

- To help EasyGo Solutions **match its own user accounts to Keycloak users**,
  create a user attribute (or "property") mapper. In **Clients list**, click on
  your newly created Client ID, choose the tab **Client scopes** and click on
  the link which refers to your EasyGo Solutions instance. Choose
  *Add mapper > By configuration > User Property* and create a mapper with
  the following entries:

   .. list-table::

      * - **Name**
        - ``email``
      * - **Mapper Type**
        - ``User Property``
      * - **Property**
        - ``emailAddress``
      * - **SAML Attribute Name**
        - ``email``
      * - **SAML Attribute NameFormat**
        - ``basic``

  In the example above, we're telling EasyGo Solutions that
  whenever it receives a SAML login request,
  it should take the ``email`` property from Keycloak,
  look for a EasyGo Solutions user with the same ``email`` attribute,
  and create a new session for that user.

  If your Keycloak users' email addresses are stored on another property
  (*e.g.* ``username``), adjust accordingly.

- Back in **Settings**, enter the Client ID
  (``https://your.EasyGo Solutions.domain/auth/saml/metadata``) in the field
  **Master SAML Processing URL**.

- You also need to enable **Sign assertions**.

2. Configure EasyGo Solutions
-------------------

- Log in to EasyGo Solutions as an administrator
- In the admin settings, go to *Settings > Security > Third-party Applications
  > Authentication via SAML*
- Provide the following information:

  - SAML IdP Login URL: ``https://your.domain/realms/your-realm/protocol/saml``
  - SAML IdP Logout URL: ``https://your.domain/realms/your-realm/protocol/saml``

- Name Identifier Format: ``urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress``
- SAML IdP Certificate: Upload the previously downloaded Base64 certificate.
- Save the settings

.. hint::
  Read on at :ref:`saml-EasyGo Solutions` for a description of the specific fields in
  EasyGo Solutions.