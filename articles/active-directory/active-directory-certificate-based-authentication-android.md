---
title: "Autenticação baseada em certificado do Azure Active Directory no Android | Microsoft Docs"
description: "Saiba mais sobre os cenários com suporte e os requisitos para configuração de autenticação baseada em certificado em soluções com dispositivos Android"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/28/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 8005bfe821fea25539c84efdccf6c49bd5f1f8ee
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a><span data-ttu-id="e9756-103">Autenticação baseada em certificado do Azure Active Directory no Android</span><span class="sxs-lookup"><span data-stu-id="e9756-103">Azure Active Directory certificate-based authentication on Android</span></span>


<span data-ttu-id="e9756-104">A CBA (autenticação baseada em certificado) permite que você seja autenticado pelo Azure Active Directory com um certificado de cliente em um dispositivo Windows, Android ou iOS ao conectar sua conta do Exchange Online a:</span><span class="sxs-lookup"><span data-stu-id="e9756-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="e9756-105">Aplicativos móveis do Office, como Microsoft Outlook e Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="e9756-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="e9756-106">Clientes do EAS (Exchange ActiveSync)</span><span class="sxs-lookup"><span data-stu-id="e9756-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="e9756-107">Configurar esse recurso elimina a necessidade de digitar uma combinação de nome de usuário e senha em determinados emails e aplicativos do Microsoft Office no seu dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="e9756-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="e9756-108">Este tópico fornece os requisitos e os cenários com suporte para configurar a CBA em um dispositivo iOS(Android) para usuários de locatários nos planos do Office 365 Enterprise, Business, Education, US Government, China e Germany.</span><span class="sxs-lookup"><span data-stu-id="e9756-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>



<span data-ttu-id="e9756-109">Esse recurso está disponível na visualização em planos do governo federal e para defesa governamental dos EUA do Office 365.</span><span class="sxs-lookup"><span data-stu-id="e9756-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>


## <a name="office-mobile-applications-support"></a><span data-ttu-id="e9756-110">Suporte a aplicativos móveis do Office</span><span class="sxs-lookup"><span data-stu-id="e9756-110">Office mobile applications support</span></span>
| <span data-ttu-id="e9756-111">Aplicativos</span><span class="sxs-lookup"><span data-stu-id="e9756-111">Apps</span></span> | <span data-ttu-id="e9756-112">Suporte</span><span class="sxs-lookup"><span data-stu-id="e9756-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="e9756-113">Aplicativo de Proteção de Informações do Azure</span><span class="sxs-lookup"><span data-stu-id="e9756-113">Azure Information Protection app</span></span> |![Verificação][1] |
| <span data-ttu-id="e9756-115">Equipes da Microsoft</span><span class="sxs-lookup"><span data-stu-id="e9756-115">Microsoft Teams</span></span> |![Verificação][1] |
| <span data-ttu-id="e9756-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="e9756-117">OneNote</span></span> |![Verificação][1] |
| <span data-ttu-id="e9756-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="e9756-119">OneDrive</span></span> |![Verificação][1] |
| <span data-ttu-id="e9756-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="e9756-121">Outlook</span></span> |![Verificação][1] |
| <span data-ttu-id="e9756-123">Aplicativos móveis do Power BI</span><span class="sxs-lookup"><span data-stu-id="e9756-123">Power BI mobile apps</span></span> |![Verificação][1] |
| <span data-ttu-id="e9756-125">Skype for Business</span><span class="sxs-lookup"><span data-stu-id="e9756-125">Skype for Business</span></span> |![Verificação][1] |
| <span data-ttu-id="e9756-127">Word/Excel/PowerPoint</span><span class="sxs-lookup"><span data-stu-id="e9756-127">Word / Excel / PowerPoint</span></span> |![Verificação][1] |
| <span data-ttu-id="e9756-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="e9756-129">Yammer</span></span> |![Verificação][1] |


### <a name="implementation-requirements"></a><span data-ttu-id="e9756-131">Requisitos de implementação</span><span class="sxs-lookup"><span data-stu-id="e9756-131">Implementation requirements</span></span>

<span data-ttu-id="e9756-132">A versão do sistema operacional do dispositivo deve ser Android 5.0 (Lollipop) e superior.</span><span class="sxs-lookup"><span data-stu-id="e9756-132">The device OS version must be Android 5.0 (Lollipop) and above.</span></span> 

<span data-ttu-id="e9756-133">Um servidor de federação deve ser configurado.</span><span class="sxs-lookup"><span data-stu-id="e9756-133">A federation server must be configured.</span></span>  

<span data-ttu-id="e9756-134">Para que o Azure Active Directory revogue um certificado do cliente, o token ADFS deve ter as seguintes declarações:</span><span class="sxs-lookup"><span data-stu-id="e9756-134">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="e9756-135">(O número de série do certificado do cliente)</span><span class="sxs-lookup"><span data-stu-id="e9756-135">(The serial number of the client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="e9756-136">(A cadeia de caracteres para o emissor do certificado do cliente)</span><span class="sxs-lookup"><span data-stu-id="e9756-136">(The string for the issuer of the client certificate)</span></span> 

<span data-ttu-id="e9756-137">O Azure Active Directory adiciona essas declarações ao token de atualização se elas estiverem disponíveis no token ADFS (ou qualquer outro token SAML).</span><span class="sxs-lookup"><span data-stu-id="e9756-137">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="e9756-138">Quando o token de atualização precisa ser validado, essas informações são usadas para verificar a revogação.</span><span class="sxs-lookup"><span data-stu-id="e9756-138">When the refresh token needs to be validated, this information is used to check the revocation.</span></span> 

<span data-ttu-id="e9756-139">Como prática recomendada, você deve atualizar as páginas de erro do ADFS com instruções sobre como obter um certificado de usuário.</span><span class="sxs-lookup"><span data-stu-id="e9756-139">As a best practice, you should update the ADFS error pages with instructions on how to get a user certificate.</span></span>  
<span data-ttu-id="e9756-140">Para obter mais detalhes, confira [Personalizando as páginas de entrada do AD FS](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9756-140">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>  

<span data-ttu-id="e9756-141">Alguns aplicativos do Office (com autenticação moderna habilitada) enviam '*prompt=login*' ao Azure AD na solicitação.</span><span class="sxs-lookup"><span data-stu-id="e9756-141">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="e9756-142">Por padrão, o Azure AD converte isso na solicitação ao ADFS para '*wauth=usernamepassworduri*' (solicita que o ADFS faça a autenticação U/P) e '*wfresh=0*' (solicita que o ADFS ignore o estado do SSO e faça uma nova autenticação).</span><span class="sxs-lookup"><span data-stu-id="e9756-142">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="e9756-143">Se você quiser habilitar a autenticação baseada em certificado para esses aplicativos, precisará modificar o comportamento padrão do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9756-143">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="e9756-144">Basta definir o '*PromptLoginBehavior*' em suas configurações de domínio federado como '*Disabled*'.</span><span class="sxs-lookup"><span data-stu-id="e9756-144">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span> <span data-ttu-id="e9756-145">Você pode usar o cmdlet [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) para executar essa tarefa:</span><span class="sxs-lookup"><span data-stu-id="e9756-145">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="e9756-146">Suporte aos clientes do Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="e9756-146">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="e9756-147">Há suporte para determinados aplicativos do Exchange ActiveSync no Android 5.0 (Lollipop) ou superior.</span><span class="sxs-lookup"><span data-stu-id="e9756-147">Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported.</span></span> <span data-ttu-id="e9756-148">Para determinar se seu aplicativo de email dá suporte a esse recurso, contate o desenvolvedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9756-148">To determine if your email application does support this feature, please contact your application developer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="e9756-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e9756-149">Next steps</span></span>

<span data-ttu-id="e9756-150">Se você quiser configurar a autenticação baseada em certificado em seu ambiente, confira [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) (Introdução à autenticação baseada em certificado no Android) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="e9756-150">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
