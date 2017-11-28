---
title: aaaVulnerabilities detectados pelo Azure Active Directory Identity Protection | Microsoft Docs
description: "Visão geral de vulnerabilidades Olá detectados pelo Azure Active Directory Identity Protection."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="e72f7-104">Vulnerabilidades detectadas pelo Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e72f7-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="e72f7-105">Vulnerabilidades são pontos fracos no seu ambiente que podem ser explorados por um invasor.</span><span class="sxs-lookup"><span data-stu-id="e72f7-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="e72f7-106">É recomendável que você resolver essas vulnerabilidades tooimprove Olá a postura de segurança da sua organização e impedir que invasores explorando-los.</span><span class="sxs-lookup"><span data-stu-id="e72f7-106">We recommend that you address these vulnerabilities tooimprove hello security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="e72f7-107">![vulnerabilidades](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilidades")</span><span class="sxs-lookup"><span data-stu-id="e72f7-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="e72f7-108">Olá seções a seguir fornecem uma visão geral das vulnerabilidades Olá relatado pela proteção de identidade.</span><span class="sxs-lookup"><span data-stu-id="e72f7-108">hello following sections provide you with an overview of hello vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="e72f7-109">Registro de autenticação multifator não configurado</span><span class="sxs-lookup"><span data-stu-id="e72f7-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="e72f7-110">Essa vulnerabilidade ajuda a controlar a implantação de saudação do Azure multi-Factor Authentication na sua organização.</span><span class="sxs-lookup"><span data-stu-id="e72f7-110">This vulnerability helps you control hello deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="e72f7-111">Autenticação multifator do Azure fornece uma segunda camada toouser de autenticação de segurança.</span><span class="sxs-lookup"><span data-stu-id="e72f7-111">Azure multi-factor authentication provides a second layer of security toouser authentication.</span></span> <span data-ttu-id="e72f7-112">Ele ajuda a proteger acesso toodata e aplicativos atendendo a demanda do usuário para um processo de logon simple.</span><span class="sxs-lookup"><span data-stu-id="e72f7-112">It helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="e72f7-113">Ele fornece autenticação forte por meio de uma variedade de opções de fácil verificação — chamada telefônica, mensagem de texto, notificação de aplicativo móvel ou verificação de código e tokens OATH de terceiros.</span><span class="sxs-lookup"><span data-stu-id="e72f7-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="e72f7-114">Recomendamos exigir o Azure Multi-Factor Authentication para entradas de usuário. A autenticação multifator desempenha um papel fundamental nas políticas de acesso condicional baseadas em risco disponíveis por meio do Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="e72f7-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="e72f7-115">Para obter mais detalhes, veja [O que é o Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e72f7-115">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="e72f7-116">Aplicativos de nuvem não gerenciados</span><span class="sxs-lookup"><span data-stu-id="e72f7-116">Unmanaged cloud apps</span></span>
<span data-ttu-id="e72f7-117">Essa vulnerabilidade ajuda a identificar aplicativos de nuvem não gerenciados na sua organização.</span><span class="sxs-lookup"><span data-stu-id="e72f7-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="e72f7-118">Os departamentos de TI nas empresas modernas, geralmente são não sabe nada sobre todos os aplicativos de nuvem Olá que os usuários em sua organização estiver usando toodo seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="e72f7-118">In modern enterprises, IT departments are often unaware of all hello cloud applications that users in their organization are using toodo their work.</span></span> <span data-ttu-id="e72f7-119">É fácil toosee por que os administradores terão preocupações sobre dados de toocorporate de acesso não autorizado, perda de dados e outros riscos de segurança.</span><span class="sxs-lookup"><span data-stu-id="e72f7-119">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="e72f7-120">É recomendável que sua organização implantar aplicativos em nuvem Cloud App Discovery toodiscover não gerenciado e toomanage esses aplicativos usando o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="e72f7-120">We recommend that your organization deploy Cloud App Discovery toodiscover unmanaged cloud applications, and toomanage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="e72f7-121">Para obter mais detalhes, veja [Encontrando aplicativos de nuvem não gerenciados com o Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e72f7-121">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="e72f7-122">Alertas de Segurança do Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="e72f7-122">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="e72f7-123">Essa vulnerabilidade ajuda você a descobrir e resolver alertas sobre identidades com privilégios na sua organização.</span><span class="sxs-lookup"><span data-stu-id="e72f7-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="e72f7-124">toocarry de usuários tooenable operações privilegiadas, as organizações precisam toogrant usuários privilegiados temporários ou permanentes de acesso no AD do Azure, os recursos do Azure ou Office 365 ou outros aplicativos SaaS.</span><span class="sxs-lookup"><span data-stu-id="e72f7-124">tooenable users toocarry out privileged operations, organizations need toogrant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="e72f7-125">Cada um desses usuários privilegiados aumenta Olá de superfície de ataque da sua organização.</span><span class="sxs-lookup"><span data-stu-id="e72f7-125">Each of these privileged users increases hello attack surface of your organization.</span></span> <span data-ttu-id="e72f7-126">Essa vulnerabilidade ajuda a identificar os usuários com acesso privilegiado desnecessário e tomar a ação apropriada tooreduce ou eliminar o risco de saudação que representam.</span><span class="sxs-lookup"><span data-stu-id="e72f7-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action tooreduce or eliminate hello risk they pose.</span></span> 

<span data-ttu-id="e72f7-127">É recomendável que sua organização usa o Azure AD Privileged Identity Management toomanage, controle e identidades com privilégios de monitor e seus tooresources de acesso no AD do Azure, bem como outros Microsoft online services como Office 365 ou Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="e72f7-127">We recommend that your organization uses Azure AD Privileged Identity Management toomanage, control, and monitor privileged identities and their access tooresources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="e72f7-128">Para obter mais detalhes, veja [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e72f7-128">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="e72f7-129">Confira também</span><span class="sxs-lookup"><span data-stu-id="e72f7-129">See also</span></span>
* [<span data-ttu-id="e72f7-130">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e72f7-130">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

