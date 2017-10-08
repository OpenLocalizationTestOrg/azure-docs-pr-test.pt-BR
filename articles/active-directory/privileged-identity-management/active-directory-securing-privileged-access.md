---
title: aaaSecuring acesso privilegiado no AD do Azure | Microsoft Docs
description: "Um tópico que explica Olá abordagens para proteger o acesso privilegiado no Azure, Active Directory do Azure e serviços Online da Microsoft."
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
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a><span data-ttu-id="5622e-103">Protegendo o acesso privilegiado no Azure AD</span><span class="sxs-lookup"><span data-stu-id="5622e-103">Securing privileged access in Azure AD</span></span>
<span data-ttu-id="5622e-104">Com privilégios de proteger o acesso é a primeira etapa crítica toohelp proteger ativos de negócios em uma organização moderno.</span><span class="sxs-lookup"><span data-stu-id="5622e-104">Securing privileged access is a critical first step toohelp protect business assets in a modern organization.</span></span> <span data-ttu-id="5622e-105">As contas privilegiadas são aquelas que administram e gerenciam sistemas de TI.</span><span class="sxs-lookup"><span data-stu-id="5622e-105">Privileged accounts are accounts that administer and manage IT systems.</span></span> <span data-ttu-id="5622e-106">Essas contas toogain acesso tooan organização dados e sistemas de destino invasores virtuais.</span><span class="sxs-lookup"><span data-stu-id="5622e-106">Cyber-attackers target these accounts toogain access tooan organization’s data and systems.</span></span> <span data-ttu-id="5622e-107">acesso privilegiado do toosecure, você deve isolar as contas de saudação e sistemas de risco de saudação do que está sendo exposto usuário mal-intencionado tooa.</span><span class="sxs-lookup"><span data-stu-id="5622e-107">toosecure privileged access, you should isolate hello accounts and systems from hello risk of being exposed tooa malicious user.</span></span>

<span data-ttu-id="5622e-108">Mais usuários estão começando tooget privilegiado acesso por meio de serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5622e-108">More users are starting tooget privileged access through cloud services.</span></span> <span data-ttu-id="5622e-109">Isso pode incluir os administradores globais do Office365, administradores de assinatura do Azure e os usuários que têm acesso administrativo nas VMs ou em aplicativos SaaS.</span><span class="sxs-lookup"><span data-stu-id="5622e-109">This can include global administrators of Office365, Azure subscription administrators, and users who have administrative access in VMs or on SaaS apps.</span></span>

<span data-ttu-id="5622e-110">A Microsoft recomenda que você siga este roteiro em [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx)(Proteger o acesso privilegiado).</span><span class="sxs-lookup"><span data-stu-id="5622e-110">Microsoft recommends you follow this roadmap on [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).</span></span>

<span data-ttu-id="5622e-111">Para clientes que usam o Azure Active Directory, o Office 365 ou outros serviços e aplicativos da Microsoft, esses princípios se aplicarão se as contas de usuário forem gerenciadas e autenticadas tanto pelo Active Directory quanto pelo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5622e-111">For customers using Azure Active Directory, Office 365, or other Microsoft services and applications, these principles apply whether user accounts are managed and authenticated by Active Directory or in Azure Active Directory.</span></span> <span data-ttu-id="5622e-112">Olá seções a seguir fornecem mais informações sobre toosupport de recursos do AD do Azure protegendo o acesso privilegiado.</span><span class="sxs-lookup"><span data-stu-id="5622e-112">hello following sections provide more information on Azure AD features toosupport securing privileged access.</span></span>

## <a name="azure-multi-factor-authentication"></a><span data-ttu-id="5622e-113">Autenticação Multifator do Azure</span><span class="sxs-lookup"><span data-stu-id="5622e-113">Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="5622e-114">segurança de saudação tooincrease de autenticação de administrador, você deve exigir verificação em duas etapas antes de conceder privilégios.</span><span class="sxs-lookup"><span data-stu-id="5622e-114">tooincrease hello security of administrator authentication, you should require two-step verification before granting privileges.</span></span> <span data-ttu-id="5622e-115">Verificação em duas etapas é um método de verificação que você tiver que requer o uso de saudação de mais do que apenas um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="5622e-115">Two-step verification is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="5622e-116">Ele fornece uma segunda camada de segurança toouser entradas e transações.</span><span class="sxs-lookup"><span data-stu-id="5622e-116">It provides a second layer of security toouser sign-ins and transactions.</span></span>

<span data-ttu-id="5622e-117">Azure multi-Factor Authentication (MFA) é uma solução de verificação em duas etapas da Microsoft, que ajuda a proteger aplicativos e acesso toodata atendendo a demanda do usuário para um processo de logon simple.</span><span class="sxs-lookup"><span data-stu-id="5622e-117">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution, which helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="5622e-118">Ele fornece autenticação forte por meio de uma variedade de opções de verificação fácil, incluindo:</span><span class="sxs-lookup"><span data-stu-id="5622e-118">It delivers strong authentication via a range of easy verification options including:</span></span>

- <span data-ttu-id="5622e-119">chamadas telefônicas</span><span class="sxs-lookup"><span data-stu-id="5622e-119">phone calls</span></span>
- <span data-ttu-id="5622e-120">mensagens de texto</span><span class="sxs-lookup"><span data-stu-id="5622e-120">text messages</span></span>
- <span data-ttu-id="5622e-121">notificações de aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="5622e-121">mobile app notifications</span></span>
- <span data-ttu-id="5622e-122">códigos de verificação de aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="5622e-122">mobile app verification codes</span></span>
- <span data-ttu-id="5622e-123">tokens OATH de terceiros</span><span class="sxs-lookup"><span data-stu-id="5622e-123">third-party OATH tokens</span></span>

<span data-ttu-id="5622e-124">Para obter uma visão geral de como funciona o Azure multi-Factor Authentication, consulte Olá vídeo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5622e-124">For an overview of how Azure Multi-Factor Authentication works see hello following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

<span data-ttu-id="5622e-125">Para obter mais informações, consulte [MFA para Office 365 e MFA para Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span><span class="sxs-lookup"><span data-stu-id="5622e-125">For more information, see [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span></span>

## <a name="time-bound-privileges"></a><span data-ttu-id="5622e-126">Privilégios de limite de tempo</span><span class="sxs-lookup"><span data-stu-id="5622e-126">Time-bound privileges</span></span>
<span data-ttu-id="5622e-127">Algumas organizações podem acreditar que elas têm muitos usuários em funções altamente privilegiadas.</span><span class="sxs-lookup"><span data-stu-id="5622e-127">Some organizations may find that they have too many users in highly privileged roles.</span></span> <span data-ttu-id="5622e-128">Um usuário pode ter sido adicionado toohello função para uma atividade específica, como toosign um serviço, mas não use esses privilégios frequentemente posteriormente.</span><span class="sxs-lookup"><span data-stu-id="5622e-128">A user might have been added toohello role for a particular activity, like toosign up for a service, but didn't use those privileges frequently afterward.</span></span>

<span data-ttu-id="5622e-129">tempo de exposição de saudação toolower de privilégios e aumentar sua visibilidade sobre seu uso, limite os usuários tooonly levando em seus privilégios "just in time" (JIT), quando eles precisarem de tooperform uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="5622e-129">toolower hello exposure time of privileges and increase your visibility into their use, limit users tooonly taking on their privileges "just in time" (JIT), when they need tooperform a task.</span></span> <span data-ttu-id="5622e-130">Para o Azure Active Directory e Microsoft Online Services, você pode usar o [Azure AD PIM (Privileged Identity Management)](http://aka.ms/AzurePIM).</span><span class="sxs-lookup"><span data-stu-id="5622e-130">For Azure Active Directory and Microsoft Online Services, you can use [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span></span>

![Painel PIM][2]

## <a name="attack-detection"></a><span data-ttu-id="5622e-132">Detecção de ataque</span><span class="sxs-lookup"><span data-stu-id="5622e-132">Attack detection</span></span>
<span data-ttu-id="5622e-133">O [Azure Active Directory Identity Protection](../active-directory-identityprotection.md) fornece uma exibição consolidada dos eventos de risco e das possíveis vulnerabilidades que afetam as identidades da sua organização.</span><span class="sxs-lookup"><span data-stu-id="5622e-133">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="5622e-134">Com base em eventos de risco, proteção de identidade calcula um nível de risco do usuário para cada usuário, permitindo que você tooconfigure risco políticas tooautomatically proteger Olá identidades da sua organização.</span><span class="sxs-lookup"><span data-stu-id="5622e-134">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you tooconfigure risk-based policies tooautomatically protect hello identities of your organization.</span></span> <span data-ttu-id="5622e-135">Essas políticas, juntamente com outros controles de acesso condicional fornecidos pelo Active Directory do Azure e o EMS, automaticamente podem bloquear usuário hello ou oferecer sugestões que incluem as redefinições de senha e a imposição de autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="5622e-135">These policies, along with other conditional access controls provided by Azure Active Directory and EMS, can automatically block hello user or offer suggestions that include password resets and multi-factor authentication enforcement.</span></span>

![Azure AD Identity Protection][3]

## <a name="conditional-access"></a><span data-ttu-id="5622e-137">Acesso condicional</span><span class="sxs-lookup"><span data-stu-id="5622e-137">Conditional access</span></span>
<span data-ttu-id="5622e-138">Com controle de acesso condicional, o Active Directory do Azure verifica condições específicas de saudação que escolha ao autenticar um usuário, antes de permitir acesso tooan aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5622e-138">With conditional access control, Azure Active Directory checks hello specific conditions you choose when authenticating a user, before allowing access tooan application.</span></span> <span data-ttu-id="5622e-139">Quando essas condições forem atendidas, o usuário de Olá é autenticado e acesso toohello aplicativo autorizado.</span><span class="sxs-lookup"><span data-stu-id="5622e-139">Once those conditions are met, hello user is authenticated and allowed access toohello application.</span></span>

![Configurando regras de acesso condicional com MFA][4]

## <a name="related-articles"></a><span data-ttu-id="5622e-141">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="5622e-141">Related articles</span></span>
* <span data-ttu-id="5622e-142">Habilitar o [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="5622e-142">Enable [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="5622e-143">Habilitar o [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span><span class="sxs-lookup"><span data-stu-id="5622e-143">Enable [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span></span>
* <span data-ttu-id="5622e-144">Habilitar o [Azure AD Identity Protection](../active-directory-identityprotection.md)</span><span class="sxs-lookup"><span data-stu-id="5622e-144">Enable [Azure AD Identity Protection](../active-directory-identityprotection.md)</span></span>
* <span data-ttu-id="5622e-145">Habilitar os [controles de acesso condicionais](../active-directory-conditional-access.md)</span><span class="sxs-lookup"><span data-stu-id="5622e-145">Enable [conditional access controls](../active-directory-conditional-access.md)</span></span>

<span data-ttu-id="5622e-146">Para obter mais informações sobre a criação de um roteiro de segurança completa, consulte a seção "responsabilidades do cliente e roteiro" Olá Olá [Microsoft Cloud Security para arquitetos de Enterprise](http://aka.ms/securecustomer) documento.</span><span class="sxs-lookup"><span data-stu-id="5622e-146">For more information on building a complete security roadmap, see hello “Customer responsibilities and roadmap” section of hello [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) document.</span></span> <span data-ttu-id="5622e-147">Para obter mais informações sobre a interação Microsoft services tooassist com qualquer um destes tópicos, entre em contato com o representante da Microsoft ou visite nossa [página de soluções de segurança cibernética](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span><span class="sxs-lookup"><span data-stu-id="5622e-147">For more information on engaging Microsoft services tooassist with any of these topics, contact your Microsoft representative or visit our [Cybersecurity solutions page](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span></span>

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
