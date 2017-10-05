---
title: Protegendo o Acesso Privilegiado no Azure AD | Microsoft Docs
description: "Um tópico que explica as abordagens para a proteção de acesso privilegiado no Azure, Azure Active Directory e Microsoft Online Services."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: acd1c11cecfa37f607fe5d82a76a40647093f43f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a><span data-ttu-id="66216-103">Protegendo o acesso privilegiado no Azure AD</span><span class="sxs-lookup"><span data-stu-id="66216-103">Securing privileged access in Azure AD</span></span>
<span data-ttu-id="66216-104">Proteger o acesso privilegiado é a primeira etapa crítica para ajudar a proteger os ativos de negócios em uma organização moderna.</span><span class="sxs-lookup"><span data-stu-id="66216-104">Securing privileged access is a critical first step to help protect business assets in a modern organization.</span></span> <span data-ttu-id="66216-105">As contas privilegiadas são aquelas que administram e gerenciam sistemas de TI.</span><span class="sxs-lookup"><span data-stu-id="66216-105">Privileged accounts are accounts that administer and manage IT systems.</span></span> <span data-ttu-id="66216-106">Os invasores virtuais visam essas contas para obter acesso aos sistemas e aos dados de uma organização.</span><span class="sxs-lookup"><span data-stu-id="66216-106">Cyber-attackers target these accounts to gain access to an organization’s data and systems.</span></span> <span data-ttu-id="66216-107">Para proteger o acesso privilegiado, isole as contas e os sistemas do risco de exposição a um usuário mal-intencionado.</span><span class="sxs-lookup"><span data-stu-id="66216-107">To secure privileged access, you should isolate the accounts and systems from the risk of being exposed to a malicious user.</span></span>

<span data-ttu-id="66216-108">Mais usuários estão começando a obter acesso privilegiado por meio de serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="66216-108">More users are starting to get privileged access through cloud services.</span></span> <span data-ttu-id="66216-109">Isso pode incluir os administradores globais do Office365, administradores de assinatura do Azure e os usuários que têm acesso administrativo nas VMs ou em aplicativos SaaS.</span><span class="sxs-lookup"><span data-stu-id="66216-109">This can include global administrators of Office365, Azure subscription administrators, and users who have administrative access in VMs or on SaaS apps.</span></span>

<span data-ttu-id="66216-110">A Microsoft recomenda que você siga este roteiro em [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx)(Proteger o acesso privilegiado).</span><span class="sxs-lookup"><span data-stu-id="66216-110">Microsoft recommends you follow this roadmap on [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).</span></span>

<span data-ttu-id="66216-111">Para clientes que usam o Azure Active Directory, o Office 365 ou outros serviços e aplicativos da Microsoft, esses princípios se aplicarão se as contas de usuário forem gerenciadas e autenticadas tanto pelo Active Directory quanto pelo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="66216-111">For customers using Azure Active Directory, Office 365, or other Microsoft services and applications, these principles apply whether user accounts are managed and authenticated by Active Directory or in Azure Active Directory.</span></span> <span data-ttu-id="66216-112">As seções a seguir fornecem mais informações sobre os recursos do Azure AD para dar suporte à proteção de acesso privilegiado.</span><span class="sxs-lookup"><span data-stu-id="66216-112">The following sections provide more information on Azure AD features to support securing privileged access.</span></span>

## <a name="azure-multi-factor-authentication"></a><span data-ttu-id="66216-113">Autenticação Multifator do Azure</span><span class="sxs-lookup"><span data-stu-id="66216-113">Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="66216-114">Para aumentar a segurança da autenticação de administrador, você deve exigir verificação em duas etapas antes de conceder privilégios.</span><span class="sxs-lookup"><span data-stu-id="66216-114">To increase the security of administrator authentication, you should require two-step verification before granting privileges.</span></span> <span data-ttu-id="66216-115">A verificação de duas etapas é um método para verificar quem você é e que requer o uso de mais do que apenas um nome de usuário e uma senha.</span><span class="sxs-lookup"><span data-stu-id="66216-115">Two-step verification is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="66216-116">Ele fornece uma segunda camada de segurança para logons de usuário e transações.</span><span class="sxs-lookup"><span data-stu-id="66216-116">It provides a second layer of security to user sign-ins and transactions.</span></span>

<span data-ttu-id="66216-117">A MFA (Autenticação Multifator) do Azure é uma solução de verificação em duas etapas da Microsoft, que ajuda a proteger o acesso a dados e aplicativos enquanto atende às exigências de conexão simples do usuário.</span><span class="sxs-lookup"><span data-stu-id="66216-117">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution, which helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="66216-118">Ele fornece autenticação forte por meio de uma variedade de opções de verificação fácil, incluindo:</span><span class="sxs-lookup"><span data-stu-id="66216-118">It delivers strong authentication via a range of easy verification options including:</span></span>

- <span data-ttu-id="66216-119">chamadas telefônicas</span><span class="sxs-lookup"><span data-stu-id="66216-119">phone calls</span></span>
- <span data-ttu-id="66216-120">mensagens de texto</span><span class="sxs-lookup"><span data-stu-id="66216-120">text messages</span></span>
- <span data-ttu-id="66216-121">notificações de aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="66216-121">mobile app notifications</span></span>
- <span data-ttu-id="66216-122">códigos de verificação de aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="66216-122">mobile app verification codes</span></span>
- <span data-ttu-id="66216-123">tokens OATH de terceiros</span><span class="sxs-lookup"><span data-stu-id="66216-123">third-party OATH tokens</span></span>

<span data-ttu-id="66216-124">Para obter uma visão geral de como a Autenticação Multifator do Azure funciona, assista ao vídeo a seguir:</span><span class="sxs-lookup"><span data-stu-id="66216-124">For an overview of how Azure Multi-Factor Authentication works see the following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

<span data-ttu-id="66216-125">Para obter mais informações, consulte [MFA para Office 365 e MFA para Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span><span class="sxs-lookup"><span data-stu-id="66216-125">For more information, see [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span></span>

## <a name="time-bound-privileges"></a><span data-ttu-id="66216-126">Privilégios de limite de tempo</span><span class="sxs-lookup"><span data-stu-id="66216-126">Time-bound privileges</span></span>
<span data-ttu-id="66216-127">Algumas organizações podem acreditar que elas têm muitos usuários em funções altamente privilegiadas.</span><span class="sxs-lookup"><span data-stu-id="66216-127">Some organizations may find that they have too many users in highly privileged roles.</span></span> <span data-ttu-id="66216-128">Um usuário pode ter sido adicionado à função para uma atividade específica, como para se inscrever para um serviço, mas não usa esses privilégios com frequência posteriormente.</span><span class="sxs-lookup"><span data-stu-id="66216-128">A user might have been added to the role for a particular activity, like to sign up for a service, but didn't use those privileges frequently afterward.</span></span>

<span data-ttu-id="66216-129">Para reduzir o tempo de exposição de privilégios e aumentar sua visibilidade sobre o uso, limite os usuários a assumir seus privilégios JIT (just in time) somente quando eles precisarem realizar uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="66216-129">To lower the exposure time of privileges and increase your visibility into their use, limit users to only taking on their privileges "just in time" (JIT), when they need to perform a task.</span></span> <span data-ttu-id="66216-130">Para o Azure Active Directory e Microsoft Online Services, você pode usar o [Azure AD PIM (Privileged Identity Management)](http://aka.ms/AzurePIM).</span><span class="sxs-lookup"><span data-stu-id="66216-130">For Azure Active Directory and Microsoft Online Services, you can use [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span></span>

![Painel PIM][2]

## <a name="attack-detection"></a><span data-ttu-id="66216-132">Detecção de ataque</span><span class="sxs-lookup"><span data-stu-id="66216-132">Attack detection</span></span>
<span data-ttu-id="66216-133">O [Azure Active Directory Identity Protection](../active-directory-identityprotection.md) fornece uma exibição consolidada dos eventos de risco e das possíveis vulnerabilidades que afetam as identidades da sua organização.</span><span class="sxs-lookup"><span data-stu-id="66216-133">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="66216-134">Baseando-se em eventos de risco, o Identity Protection calcula um nível de risco para cada usuário, permitindo a você definir políticas baseadas em risco para proteger automaticamente as identidades da sua organização.</span><span class="sxs-lookup"><span data-stu-id="66216-134">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you to configure risk-based policies to automatically protect the identities of your organization.</span></span> <span data-ttu-id="66216-135">Essas políticas, juntamente com outros controles de acesso condicional fornecidos pelo Azure Active Directory e pelo EMS, podem bloquear automaticamente o usuário ou oferecer sugestões que incluem redefinições de senha e a imposição de autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="66216-135">These policies, along with other conditional access controls provided by Azure Active Directory and EMS, can automatically block the user or offer suggestions that include password resets and multi-factor authentication enforcement.</span></span>

![Azure AD Identity Protection][3]

## <a name="conditional-access"></a><span data-ttu-id="66216-137">Acesso condicional</span><span class="sxs-lookup"><span data-stu-id="66216-137">Conditional access</span></span>
<span data-ttu-id="66216-138">Com o controle de acesso condicional, o Active Directory do Azure verifica as condições específicas que você escolhe para autenticar o usuário antes de permitir o acesso a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66216-138">With conditional access control, Azure Active Directory checks the specific conditions you choose when authenticating a user, before allowing access to an application.</span></span> <span data-ttu-id="66216-139">Quando essas condições forem atendidas, o usuário é autenticado e autorizado a acessar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66216-139">Once those conditions are met, the user is authenticated and allowed access to the application.</span></span>

![Configurando regras de acesso condicional com MFA][4]

## <a name="related-articles"></a><span data-ttu-id="66216-141">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="66216-141">Related articles</span></span>
* <span data-ttu-id="66216-142">Habilitar o [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="66216-142">Enable [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="66216-143">Habilitar o [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span><span class="sxs-lookup"><span data-stu-id="66216-143">Enable [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span></span>
* <span data-ttu-id="66216-144">Habilitar o [Azure AD Identity Protection](../active-directory-identityprotection.md)</span><span class="sxs-lookup"><span data-stu-id="66216-144">Enable [Azure AD Identity Protection](../active-directory-identityprotection.md)</span></span>
* <span data-ttu-id="66216-145">Habilitar os [controles de acesso condicionais](../active-directory-conditional-access.md)</span><span class="sxs-lookup"><span data-stu-id="66216-145">Enable [conditional access controls](../active-directory-conditional-access.md)</span></span>

<span data-ttu-id="66216-146">Para obter mais informações sobre a criação de um roteiro de segurança completo, consulte a seção “Customer responsibilities and roadmap” (Roteiro e responsabilidades do cliente) do documento [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) (Microsoft Cloud Security for Enterprise Architects).</span><span class="sxs-lookup"><span data-stu-id="66216-146">For more information on building a complete security roadmap, see the “Customer responsibilities and roadmap” section of the [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) document.</span></span> <span data-ttu-id="66216-147">Para obter mais informações em atrair os serviços da Microsoft para ajudá-lo em qualquer um desses tópicos, entre em contato com seu representante da Microsoft ou visite nossa [página de soluções de segurança cibersegurança](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span><span class="sxs-lookup"><span data-stu-id="66216-147">For more information on engaging Microsoft services to assist with any of these topics, contact your Microsoft representative or visit our [Cybersecurity solutions page](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span></span>

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
