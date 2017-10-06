---
title: "autenticação baseada em certificado do Active Directory da aaaAzure no Android | Microsoft Docs"
description: "Saiba mais sobre cenários de saudação com suporte e requisitos de saudação para configurar a autenticação baseada em certificado em soluções com dispositivos Android"
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
ms.openlocfilehash: 148275fa3da610530c278fcd57e02e907f735d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a><span data-ttu-id="fcc51-103">Autenticação baseada em certificado do Azure Active Directory no Android</span><span class="sxs-lookup"><span data-stu-id="fcc51-103">Azure Active Directory certificate-based authentication on Android</span></span>


<span data-ttu-id="fcc51-104">Autenticação baseada em certificado (CBA) permite que você toobe autenticado pelo Active Directory do Azure com um certificado de cliente em um dispositivo Windows, Android ou iOS ao conectar-se a sua conta do Exchange online para:</span><span class="sxs-lookup"><span data-stu-id="fcc51-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="fcc51-105">Aplicativos móveis do Office, como Microsoft Outlook e Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="fcc51-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="fcc51-106">Clientes do EAS (Exchange ActiveSync)</span><span class="sxs-lookup"><span data-stu-id="fcc51-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="fcc51-107">Configurar esse recurso elimina a necessidade de saudação tooenter um nome de usuário e combinação de senha em determinados email e aplicativos do Microsoft Office em seu dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="fcc51-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="fcc51-108">Este tópico fornece requisitos hello e cenários Olá com suporte para configurar CBA em um dispositivo de iOS(Android) para usuários de locatários no Office 365 Enterprise, Business, educação, China, governo dos EUA e Alemanha planos.</span><span class="sxs-lookup"><span data-stu-id="fcc51-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>



<span data-ttu-id="fcc51-109">Esse recurso está disponível na visualização em planos do governo federal e para defesa governamental dos EUA do Office 365.</span><span class="sxs-lookup"><span data-stu-id="fcc51-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>


## <a name="office-mobile-applications-support"></a><span data-ttu-id="fcc51-110">Suporte a aplicativos móveis do Office</span><span class="sxs-lookup"><span data-stu-id="fcc51-110">Office mobile applications support</span></span>
| <span data-ttu-id="fcc51-111">Aplicativos</span><span class="sxs-lookup"><span data-stu-id="fcc51-111">Apps</span></span> | <span data-ttu-id="fcc51-112">Suporte</span><span class="sxs-lookup"><span data-stu-id="fcc51-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="fcc51-113">Aplicativo de Proteção de Informações do Azure</span><span class="sxs-lookup"><span data-stu-id="fcc51-113">Azure Information Protection app</span></span> |![Verificação][1] |
| <span data-ttu-id="fcc51-115">Equipes da Microsoft</span><span class="sxs-lookup"><span data-stu-id="fcc51-115">Microsoft Teams</span></span> |![Verificação][1] |
| <span data-ttu-id="fcc51-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="fcc51-117">OneNote</span></span> |![Verificação][1] |
| <span data-ttu-id="fcc51-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="fcc51-119">OneDrive</span></span> |![Verificação][1] |
| <span data-ttu-id="fcc51-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="fcc51-121">Outlook</span></span> |![Verificação][1] |
| <span data-ttu-id="fcc51-123">Aplicativos móveis do Power BI</span><span class="sxs-lookup"><span data-stu-id="fcc51-123">Power BI mobile apps</span></span> |![Verificação][1] |
| <span data-ttu-id="fcc51-125">Skype for Business</span><span class="sxs-lookup"><span data-stu-id="fcc51-125">Skype for Business</span></span> |![Verificação][1] |
| <span data-ttu-id="fcc51-127">Word/Excel/PowerPoint</span><span class="sxs-lookup"><span data-stu-id="fcc51-127">Word / Excel / PowerPoint</span></span> |![Verificação][1] |
| <span data-ttu-id="fcc51-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="fcc51-129">Yammer</span></span> |![Verificação][1] |


### <a name="implementation-requirements"></a><span data-ttu-id="fcc51-131">Requisitos de implementação</span><span class="sxs-lookup"><span data-stu-id="fcc51-131">Implementation requirements</span></span>

<span data-ttu-id="fcc51-132">Olá versão de SO do dispositivo deve ser Android 5.0 (pirulito) e acima.</span><span class="sxs-lookup"><span data-stu-id="fcc51-132">hello device OS version must be Android 5.0 (Lollipop) and above.</span></span> 

<span data-ttu-id="fcc51-133">Um servidor de federação deve ser configurado.</span><span class="sxs-lookup"><span data-stu-id="fcc51-133">A federation server must be configured.</span></span>  

<span data-ttu-id="fcc51-134">Para toorevoke um certificado de cliente do Active Directory do Azure, o token do AD FS Olá deve ter Olá declarações a seguir:</span><span class="sxs-lookup"><span data-stu-id="fcc51-134">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="fcc51-135">(Olá o número de série do certificado de cliente Olá)</span><span class="sxs-lookup"><span data-stu-id="fcc51-135">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="fcc51-136">(cadeia de caracteres Olá para o emissor de saudação do certificado de cliente Olá)</span><span class="sxs-lookup"><span data-stu-id="fcc51-136">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="fcc51-137">Active Directory do Azure adiciona o token de atualização de toohello essas declarações se eles estão disponíveis no token do AD FS hello (ou qualquer outro token SAML).</span><span class="sxs-lookup"><span data-stu-id="fcc51-137">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="fcc51-138">Quando o token de atualização Olá precisa toobe validado, essas informações são usadas toocheck Olá revogação.</span><span class="sxs-lookup"><span data-stu-id="fcc51-138">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="fcc51-139">Como prática recomendada, você deve atualizar páginas de erro do ADFS Olá com instruções sobre como tooget um certificado de usuário.</span><span class="sxs-lookup"><span data-stu-id="fcc51-139">As a best practice, you should update hello ADFS error pages with instructions on how tooget a user certificate.</span></span>  
<span data-ttu-id="fcc51-140">Para obter mais detalhes, consulte [Personalizando páginas Olá AD FS Sign-in](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="fcc51-140">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>  

<span data-ttu-id="fcc51-141">Alguns aplicativos do Office (com autenticação moderna habilitado) enviar '*prompt = logon*' tooAzure AD em sua solicitação.</span><span class="sxs-lookup"><span data-stu-id="fcc51-141">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="fcc51-142">Por padrão, o AD do Azure converte isso em Olá solicitação tooADFS muito '*wauth = usernamepassworduri*' (solicita autenticação do ADFS toodo U/P) e '*wfresh = 0*' (solicita o estado do ADFS tooignore SSO e fazer uma autenticação nova) .</span><span class="sxs-lookup"><span data-stu-id="fcc51-142">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="fcc51-143">Se você quiser que a autenticação baseada em certificado tooenable para esses aplicativos, você precisa comportamento do toomodify saudação padrão do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc51-143">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="fcc51-144">Apenas o conjunto de saudação '*PromptLoginBehavior*' nas configurações do domínio federado muito '*desabilitado*'.</span><span class="sxs-lookup"><span data-stu-id="fcc51-144">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="fcc51-145">Você pode usar o hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform cmdlet essa tarefa:</span><span class="sxs-lookup"><span data-stu-id="fcc51-145">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="fcc51-146">Suporte aos clientes do Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="fcc51-146">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="fcc51-147">Há suporte para determinados aplicativos do Exchange ActiveSync no Android 5.0 (Lollipop) ou superior.</span><span class="sxs-lookup"><span data-stu-id="fcc51-147">Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported.</span></span> <span data-ttu-id="fcc51-148">toodetermine se seu aplicativo de email oferece suporte a esse recurso, entre em contato com o desenvolvedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fcc51-148">toodetermine if your email application does support this feature, please contact your application developer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="fcc51-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fcc51-149">Next steps</span></span>

<span data-ttu-id="fcc51-150">Se você quiser tooconfigure a autenticação baseada em certificado em seu ambiente, consulte [Introdução à autenticação baseada em certificado no Android](active-directory-certificate-based-authentication-get-started.md) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="fcc51-150">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
