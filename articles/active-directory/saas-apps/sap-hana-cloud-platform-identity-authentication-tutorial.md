---
title: 'Tutorial: Azure Active Directory integration with SAP Cloud Platform Identity Authentication | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAP Cloud Platform Identity Authentication.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess

ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: Azure-Active-Directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/16/2019
ms.author: jeedes

ms.collection: M365-identity-device-management
---
# Tutorial: Azure Active Directory integration with SAP Cloud Platform Identity Authentication

In this tutorial, you learn how to integrate SAP Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).
Integrating SAP Cloud Platform Identity Authentication with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to SAP Cloud Platform Identity Authentication.
* You can enable your users to be automatically signed-in to SAP Cloud Platform Identity Authentication (Single Sign-On) with their Azure AD accounts.
* You can manage your accounts in one central location - the Azure portal.

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.

## Prerequisites

To configure Azure AD integration with SAP Cloud Platform Identity Authentication, you need the following items:

* An Azure AD subscription. If you don't have an Azure AD environment, you can get one-month trial [here](https://azure.microsoft.com/pricing/free-trial/)
* SAP Cloud Platform Identity Authentication single sign-on enabled subscription

## Scenario description

In this tutorial, you configure and test Azure AD single sign-on in a test environment.

* SAP Cloud Platform Identity Authentication supports **SP** and **IDP** initiated SSO

Before you dive into the technical details, it's vital to understand the concepts you're going to look at. The SAP Cloud Platform Identity Authentication and Active Directory Federation Services enable you to implement SSO across applications or services that are protected by Azure AD (as an IdP) with SAP applications and services that are protected by SAP Cloud Platform Identity Authentication.

Currently, SAP Cloud Platform Identity Authentication acts as a Proxy Identity Provider to SAP applications. Azure Active Directory in turn acts as the leading Identity Provider in this setup. 

The following diagram illustrates this relationship:

![Creating an Azure AD test user](./media/sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

With this setup, your SAP Cloud Platform Identity Authentication tenant is configured as a trusted application in Azure Active Directory.

All SAP applications and services that you want to protect this way are subsequently configured in the SAP Cloud Platform Identity Authentication management console.

Therefore, the authorization for granting access to SAP applications and services needs to take place in SAP Cloud Platform Identity Authentication (as opposed to Azure Active Directory).

By configuring SAP Cloud Platform Identity Authentication as an application through the Azure Active Directory Marketplace, you don't need to configure individual claims or SAML assertions.

> [!NOTE]
> Currently only Web SSO has been tested by both parties. The flows that are necessary for App-to-API or API-to-API communication should work but have not been tested yet. They will be tested during subsequent activities.

## Adding SAP Cloud Platform Identity Authentication from the gallery

To configure the integration of SAP Cloud Platform Identity Authentication into Azure AD, you need to add SAP Cloud Platform Identity Authentication from the gallery to your list of managed SaaS apps.

**To add SAP Cloud Platform Identity Authentication from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.

	![The Azure Active Directory button](common/select-azuread.png)

2. Navigate to **Enterprise Applications** and then select the **All Applications** option.

	![The Enterprise applications blade](common/enterprise-applications.png)

3. To add new application, click **New application** button on the top of dialog.

	![The New application button](common/add-new-app.png)

4. In the search box, type **SAP Cloud Platform Identity Authentication**, select **SAP Cloud Platform Identity Authentication** from result panel then click **Add** button to add the application.

	 ![SAP Cloud Platform Identity Authentication in the results list](common/search-new-app.png)

## Configure and test Azure AD single sign-on

In this section, you configure and test Azure AD single sign-on with [Application name] based on a test user called **Britta Simon**.
For single sign-on to work, a link relationship between an Azure AD user and the related user in [Application name] needs to be established.

To configure and test Azure AD single sign-on with [Application name], you need to complete the following building blocks:

1. **[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Configure SAP Cloud Platform Identity Authentication Single Sign-On](#configure-sap-cloud-platform-identity-authentication-single-sign-on)** - to configure the Single Sign-On settings on application side.
3. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
4. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Create SAP Cloud Platform Identity Authentication test user](#create-sap-cloud-platform-identity-authentication-test-user)** - to have a counterpart of Britta Simon in SAP Cloud Platform Identity Authentication that is linked to the Azure AD representation of user.
6. **[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.

### Configure Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal.

To configure Azure AD single sign-on with [Application name], perform the following steps:

1. In the [Azure portal](https://portal.azure.com/), on the **SAP Cloud Platform Identity Authentication** application integration page, select **Single sign-on**.

    ![Configure single sign-on link](common/select-sso.png)

2. On the **Select a Single sign-on method** dialog, select **SAML/WS-Fed** mode to enable single sign-on.

    ![Single sign-on select mode](common/select-saml-option.png)

3. On the **Set up Single Sign-On with SAML** page, click **Edit** icon to open **Basic SAML Configuration** dialog.

	![Edit Basic SAML Configuration](common/edit-urls.png)

4. On the **Basic SAML Configuration** section, if you wish to configure in **IDP** intiated mode perform the following steps:

    ![SAP Cloud Platform Identity Authentication Domain and URLs single sign-on information](common/idp-intiated.png)

    a. In the **Identifier** text box, type a URL using the following pattern:
	`<IAS-tenant-id>.accounts.ondemand.com`

    b. In the **Reply URL** text box, type a URL using the following pattern:
	`https://<IAS-tenant-id>.accounts.ondemand.com/saml2/idp/acs/<IAS-tenant-id>.accounts.ondemand.com`

	> [!NOTE]
	> These values are not real. Update these values with the actual identifier and Reply URL. Contact the [SAP Cloud Platform Identity Authentication Client support team](https://cloudplatform.sap.com/capabilities/security/trustcenter.html) to get these values. If you don't understand Identifier value, read the SAP Cloud Platform Identity Authentication documentation about [Tenant SAML 2.0 configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).

5. Click **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    ![SAP Cloud Platform Identity Authentication Domain and URLs single sign-on information](common/metadata-upload-additional-signon.png)

	In the **Sign-on URL** text box, type a URL using the following pattern:
    `{YOUR BUSINESS APPLICATION URL}`

	> [!NOTE]
	> This value is not real. Update this value with the actual sign-on URL. Please use your specific business application Sign-on URL. Contact the [SAP Cloud Platform Identity Authentication Client support team](https://cloudplatform.sap.com/capabilities/security/trustcenter.html) if you have any doubt.

6. SAP Cloud Platform Identity Authentication application expects the SAML assertions in a specific format. Configure the following claims for this application. You can manage the values of these attributes from the **User Attributes** section on application integration page. On the **Set up Single Sign-On with SAML** page, click **Edit** button to open **User Attributes** dialog.

	![image](common/edit-attribute.png)

7. If your SAP application expects an attribute such as **firstName**, add the **firstName** attribute in the **User Claims** section on the **User Attributes** dialog, configure SAML token attribute as shown in the image above and perform the following steps:

	a. Click **Add new claim** to open the **Manage user claims** dialog.

	![image](common/new-save-attribute.png)

	![image](common/new-attribute-details.png)

	b. In the **Name** textbox, type the attribute name firstName.

	c. Leave the **Namespace** blank.

	d. Select Source as **Attribute**.

	e. From the **Source attribute** list, select the attribute value user.givenname.

	f. Click **Ok**

	g. Click **Save**.

8. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, click **Download** to download the **Metadata XML** from the given options as per your requirement and save it on your computer.

	![The Certificate download link](common/metadataxml.png)

9. On the **Set up SAP Cloud Platform Identity Authentication** section, copy the appropriate URL(s) as per your requirement.

	![Copy configuration URLs](common/copy-configuration-urls.png)

	a. Login URL

	b. Azure Ad Identifier

	c. Logout URL

### Configure SAP Cloud Platform Identity Authentication Single Sign-On

1. To get SSO configured for your application, go to the SAP Cloud Platform Identity Authentication administration console. The URL has the following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`. Then read the documentation about SAP Cloud Platform Identity Authentication at [Integration with Microsoft Azure AD](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).

2. In the Azure portal, select the **Save** button.

3. Continue with the following only if you want to add and enable SSO for another SAP application. Repeat the steps under the section **Adding SAP Cloud Platform Identity Authentication from the gallery**.

4. In the Azure portal, on the **SAP Cloud Platform Identity Authentication** application integration page, select **Linked Sign-on**.

	![Configure Linked Sign-On](./media/sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)

5. Save the configuration.

> [!NOTE]
> The new application leverages the single sign-on configuration of the previous SAP application. Make sure you use the same Corporate Identity Providers in the SAP Cloud Platform Identity Authentication administration console.

### Create an Azure AD test user

The objective of this section is to create a test user in the Azure portal called Britta Simon.

1. In the Azure portal, in the left pane, select **Azure Active Directory**, select **Users**, and then select **All users**.

    ![The "Users and groups" and "All users" links](common/users.png)

2. Select **New user** at the top of the screen.

    ![New user Button](common/new-user.png)

3. In the User properties, perform the following steps.

    ![The User dialog box](common/user-properties.png)

    a. In the **Name** field enter **BrittaSimon**.
  
    b. In the **User name** field type **brittasimon@yourcompanydomain.extension**  
    For example, BrittaSimon@contoso.com

    c. Select **Show password** check box, and then write down the value that's displayed in the Password box.

    d. Click **Create**.

### Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud Platform Identity Authentication.

1. In the Azure portal, select **Enterprise Applications**, select **All applications**, then select **SAP Cloud Platform Identity Authentication**.

	![Enterprise applications blade](common/enterprise-applications.png)

2. In the applications list, select **SAP Cloud Platform Identity Authentication**.

	![The SAP Cloud Platform Identity Authentication link in the Applications list](common/all-applications.png)

3. In the menu on the left, select **Users and groups**.

    ![The "Users and groups" link](common/users-groups-blade.png)

4. Click the **Add user** button, then select **Users and groups** in the **Add Assignment** dialog.

    ![The Add Assignment pane](common/add-assign-user.png)

5. In the **Users and groups** dialog select **Britta Simon** in the Users list, then click the **Select** button at the bottom of the screen.

6. If you are expecting any role value in the SAML assertion then in the **Select Role** dialog select the appropriate role for the user from the list, then click the **Select** button at the bottom of the screen.

7. In the **Add Assignment** dialog click the **Assign** button.

### Create SAP Cloud Platform Identity Authentication test user

You don't need to create a user in SAP Cloud Platform Identity Authentication. Users who are in the Azure AD user store can use the SSO functionality.

SAP Cloud Platform Identity Authentication supports the Identity Federation option. This option allows the application to check whether users who are authenticated by the corporate identity provider exist in the user store of SAP Cloud Platform Identity Authentication.

The Identity Federation option is disabled by default. If Identity Federation is enabled, only the users that are imported in SAP Cloud Platform Identity Authentication can access the application.

For more information about how to enable or disable Identity Federation with SAP Cloud Platform Identity Authentication, see "Enable Identity Federation with SAP Cloud Platform Identity Authentication" in [Configure Identity Federation with the User Store of SAP Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).

### Test single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the SAP Cloud Platform Identity Authentication tile in the Access Panel, you should be automatically signed in to the SAP Cloud Platform Identity Authentication for which you set up SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## Additional resources

- [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [What is application access and single sign-on with Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [What is conditional access in Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
