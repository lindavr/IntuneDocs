---
# required metadata

title: Enroll Windows devicestitleSuffix: "Intune Azure preview"
description: "Intune Azure preview: Enable Intune mobile device management (MDM) for Windows devices."
keywords:
author: nathbarn
manager: nathbarn
ms.date: 03/21/17
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: f94dbc2e-a855-487e-af6e-8d08fabe6c3d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: damionw
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure

---

# Enroll Windows devices

[!INCLUDE[azure_preview](../includes/azure_preview.md)]

Use one of the following methods to set up enrollment for Windows devices:

- [**Windows 10 and Windows 10 Mobile automatic enrollment with Azure Active Directory Premium**](#set-up-windows-10-and-windows-10-mobile-automatic-enrollment-with-azure-active-directory-premium)
 -  This method is applicable only for Windows 10 and Windows 10 Mobile devices.
 -  You must have Azure Active Directory Premium to use this method. Otherwise, use the enrollment method for Windows 8.1 and Windows Phone 8.1.
 -  If you choose not to enable automatic enrollment, use the enrollment method for Windows 8.1 and Windows Phone 8.1.

- [**Enrollment without Azure AD Premium automatic enrollment**](#enable-windows-enrollment-without-azure-ad-premium)
 - You must use this method to enroll Windows 8.1 and Windows Phone 8.1 devices.
 - You can use this method for Windows 8.1 and later devices if you don't want to use Azure Active Directory (AD) Premium.

[!INCLUDE[AAD-enrollment](../includes/win10-automatic-enrollment-aad.md)]

## Enable Windows enrollment without Azure AD Premium

You can let users install and enroll their devices without Azure AD Premium automatic enrollment. If you create DNS CNAME resource records,  users connect and enroll in Intune without entering a server name.

1. **Create CNAMEs** (optional)<br>
 Create **CNAME** DNS resource records for your company’s domain. For example, if your company’s website is contoso.com, you would create a CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to enterpriseenrollment-s.manage.microsoft.com.

	Although creating CNAME DNS entries is optional, CNAME records make enrollment easier for users. If no enrollment CNAME record is found, users are prompted to manually enter the MDM server name, enrollment.manage.microsoft.com.

	If there is more than one verified domain, create a CNAME record for each domain. The CNAME resource records must contain the following information:

	CNAME resource records must have the following information:

  |TYPE|Host name|Points to|TTL|
  |--------|-------------|-------------|-------|
  |CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com |1 Hour|
  |CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|1 Hour|

  `EnterpriseEnrollment-s.manage.microsoft.com` – Supports a redirect to the Intune service with domain recognition from the email’s domain name

  If your company uses multiple domains for user credentials, create CNAME records for each domain.

  For example, if your company’s website is contoso.com, you would create a CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to EnterpriseEnrollment-s.manage.microsoft.com. Changes to DNS records might take up to 72 hours to propagate. You cannot verify the DNS change in Intune until the DNS record propagates.

2.  **Verify CNAME**<br>In the Azure portal, choose **More Services** > **Monitoring + Management** > **Intune**. On the Intune blade, choose **Enroll devices** > **Windows Enrollment**. Enter the URL of the verified domain of the company website in the **Specify a verified domain name** box, and then choose **Test Auto-Detection**.

3.  **Tell your users how to enroll their devices and what to expect after their devices are under management.**

	For end-user enrollment instructions, see [Enroll your Windows device in Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). You can also send users to [What can my IT admin see on my devic](https://docs.microsoft.com/intune/enduser/what-can-your-it-administrator-see-when-you-enroll-your-device-in-intune-windows).

	For more information about end-user tasks, see [Resources about the end-user experience with Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/how-to-educate-your-end-users-about-microsoft-intune).

No additional work is required unless you will deploy the Company Portal to devices.  Steps 2 and 3 in the admin console can be safely ignored.
