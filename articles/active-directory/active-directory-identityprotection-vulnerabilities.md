---
title: Vulnerabilidades detectadas pelo Azure Active Directory Identity Protection | Microsoft Docs
description: "Visão geral das vulnerabilidades detectadas pelo Azure Active Directory Identity Protection."
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
ms.openlocfilehash: 364873ff54099a6123e40b12e819d1745751f285
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="3314e-104">Vulnerabilidades detectadas pelo Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3314e-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="3314e-105">Vulnerabilidades são pontos fracos no seu ambiente que podem ser explorados por um invasor.</span><span class="sxs-lookup"><span data-stu-id="3314e-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="3314e-106">É recomendável resolver essas vulnerabilidades para melhorar a postura de segurança de sua organização e impedir que invasores possam explorá-las.</span><span class="sxs-lookup"><span data-stu-id="3314e-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="3314e-107">![vulnerabilidades](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilidades")</span><span class="sxs-lookup"><span data-stu-id="3314e-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="3314e-108">As seções a seguir fornecem uma visão geral das vulnerabilidades relatadas pelo Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="3314e-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="3314e-109">Registro de autenticação multifator não configurado</span><span class="sxs-lookup"><span data-stu-id="3314e-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="3314e-110">Essa vulnerabilidade ajuda a controlar a implantação do Azure Multi-Factor Authentication na sua organização.</span><span class="sxs-lookup"><span data-stu-id="3314e-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="3314e-111">A Azure Multi-Factor Authentication fornece uma segunda camada de segurança para a autenticação do usuário.</span><span class="sxs-lookup"><span data-stu-id="3314e-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span></span> <span data-ttu-id="3314e-112">Ela ajuda a proteger o acesso a dados e aplicativos ao mesmo tempo que atende à demanda dos usuários para um processo de entrada simples.</span><span class="sxs-lookup"><span data-stu-id="3314e-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="3314e-113">Ele fornece autenticação forte por meio de uma variedade de opções de fácil verificação — chamada telefônica, mensagem de texto, notificação de aplicativo móvel ou verificação de código e tokens OATH de terceiros.</span><span class="sxs-lookup"><span data-stu-id="3314e-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="3314e-114">Recomendamos exigir o Azure Multi-Factor Authentication para entradas de usuário.</span><span class="sxs-lookup"><span data-stu-id="3314e-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins.</span></span> <span data-ttu-id="3314e-115">A autenticação multifator desempenha um papel fundamental nas políticas de acesso condicional baseadas em risco disponíveis por meio do Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="3314e-115">Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="3314e-116">Para obter mais detalhes, veja [O que é o Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3314e-116">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="3314e-117">Aplicativos de nuvem não gerenciados</span><span class="sxs-lookup"><span data-stu-id="3314e-117">Unmanaged cloud apps</span></span>
<span data-ttu-id="3314e-118">Essa vulnerabilidade ajuda a identificar aplicativos de nuvem não gerenciados na sua organização.</span><span class="sxs-lookup"><span data-stu-id="3314e-118">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="3314e-119">Nas empresas modernas, os departamentos de TI geralmente não estão cientes de todos os aplicativos de nuvem que os membros da sua organização usam para realizar seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="3314e-119">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span></span> <span data-ttu-id="3314e-120">É fácil ver por que os administradores teriam preocupações sobre o acesso não autorizado aos dados corporativos, perda de dados e outros riscos de segurança.</span><span class="sxs-lookup"><span data-stu-id="3314e-120">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="3314e-121">Recomendamos que sua organização implante o Cloud App Discovery para descobrir aplicativos de nuvem não gerenciados e gerencie esses aplicativos usando o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3314e-121">We recommend that your organization deploy Cloud App Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="3314e-122">Para obter mais detalhes, veja [Encontrando aplicativos de nuvem não gerenciados com o Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3314e-122">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="3314e-123">Alertas de Segurança do Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="3314e-123">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="3314e-124">Essa vulnerabilidade ajuda você a descobrir e resolver alertas sobre identidades com privilégios na sua organização.</span><span class="sxs-lookup"><span data-stu-id="3314e-124">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="3314e-125">Para permitir que os usuários executem operações com privilégios, as organizações precisam oferecer aos usuários acesso privilegiado temporário ou permanente ao Azure AD, a recursos do Azure ou do Office 365 ou a outros aplicativos SaaS.</span><span class="sxs-lookup"><span data-stu-id="3314e-125">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="3314e-126">Cada um desses usuários privilegiados aumenta a superfície de ataque da sua organização.</span><span class="sxs-lookup"><span data-stu-id="3314e-126">Each of these privileged users increases the attack surface of your organization.</span></span> <span data-ttu-id="3314e-127">Essa vulnerabilidade ajuda você a identificar os usuários com acesso privilegiado desnecessário e tomar as devidas providências para reduzir ou eliminar o risco que eles representam.</span><span class="sxs-lookup"><span data-stu-id="3314e-127">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span></span> 

<span data-ttu-id="3314e-128">Recomendamos que sua organização use o Azure AD Privileged Identity Management para gerenciar, controlar e monitorar as identidades com privilégios e o acesso delas a recursos no Azure AD e em outros serviços online da Microsoft como o Office 365 ou o Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="3314e-128">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="3314e-129">Para obter mais detalhes, veja [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3314e-129">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="3314e-130">Confira também</span><span class="sxs-lookup"><span data-stu-id="3314e-130">See also</span></span>
* [<span data-ttu-id="3314e-131">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3314e-131">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

