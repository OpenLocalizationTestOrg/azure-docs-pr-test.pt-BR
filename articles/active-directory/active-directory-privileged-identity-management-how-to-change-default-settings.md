---
title: "configurações de ativação de função aaaHow toomanage | Microsoft Docs"
description: "Saiba como toochange Olá configurações padrão de identidades com privilégios com hello extensão do Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="0aaaf-103">Como configurações de ativação de função toomanage no Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="0aaaf-103">How toomanage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="0aaaf-104">Um administrador com privilégios de função pode personalizar o Azure AD Privileged Identity Management (PIM) em sua organização, incluindo alterar a experiência de saudação para um usuário que está sendo ativado uma atribuição de função qualificado.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing hello experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-hello-role-activation-settings"></a><span data-ttu-id="0aaaf-105">Gerenciar configurações de ativação de função hello</span><span class="sxs-lookup"><span data-stu-id="0aaaf-105">Manage hello role activation settings</span></span>
1. <span data-ttu-id="0aaaf-106">Vá toohello [portal do Azure](https://portal.azure.com) e selecione hello **do Azure AD Privileged Identity Management** aplicativo a partir do painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-106">Go toohello [Azure portal](https://portal.azure.com) and select hello **Azure AD Privileged Identity Management** app from hello dashboard.</span></span>
2. <span data-ttu-id="0aaaf-107">Selecione **Gerenciar funções privilegiadas** > **Configurações** > **Funções Privilegiadas**.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="0aaaf-108">Escolha a função hello cujas configurações você deseja toomanage.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-108">Choose hello role whose settings you want toomanage.</span></span>

<span data-ttu-id="0aaaf-109">Na página de configurações de saudação para cada função, há uma série de configurações que você pode configurar.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-109">On hello settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="0aaaf-110">Essas configurações afetam apenas os usuários que são administradores elegíveis, mas não os administradores permanentes.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="0aaaf-111">**Ativações**: tempo de saudação, em horas, que uma função permanece ativa antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-111">**Activations**: hello time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="0aaaf-112">Isso pode ser entre 1 e 72 horas.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="0aaaf-113">**Notificações**: você pode escolher se ou não o sistema de Olá envia emails tooadmins confirmando que eles ativou a uma função.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-113">**Notifications**: You can choose whether or not hello system sends emails tooadmins confirming that they have activated a role.</span></span> <span data-ttu-id="0aaaf-114">Isso pode ser útil para detectar ativações não autorizadas ou ilegítimas.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="0aaaf-115">**Tíquete de solicitação deincidente/**: você pode escolher se ou não toorequire administradores qualificados tooinclude um tíquete de número quando elas ativaram sua função.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-115">**Incident/Request Ticket**: You can choose whether or not toorequire eligible admins tooinclude a ticket number when they activate their role.</span></span> <span data-ttu-id="0aaaf-116">Isso pode ser útil ao realizar auditorias de acesso à função.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="0aaaf-117">**Autenticação multifator**: você pode escolher se ou não toorequire usuários tooverify sua identidade com MFA antes de poder ativar suas funções.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-117">**Multi-Factor Authentication**: You can choose whether or not toorequire users tooverify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="0aaaf-118">Eles apenas têm tooverify isso vez por sessão, não toda vez que eles ativaram uma função.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-118">They only have tooverify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="0aaaf-119">Há dois tookeep de dicas em mente quando você habilitar a MFA:</span><span class="sxs-lookup"><span data-stu-id="0aaaf-119">There are two tips tookeep in mind when you enable MFA:</span></span>

* <span data-ttu-id="0aaaf-120">Os usuários que têm contas da Microsoft para seus endereços de email (normalmente @outlook.com, mas nem sempre) não é possível registrar para o Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="0aaaf-121">Se você quiser tooassign funções toousers com contas da Microsoft, torná-los administradores permanentes ou desabilite o MFA para essa função.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-121">If you want tooassign roles toousers with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="0aaaf-122">Você não pode desabilitar o MFA para funções com altos privilégios do Azure AD e do Office365.</span><span class="sxs-lookup"><span data-stu-id="0aaaf-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="0aaaf-123">Esse é um recurso de segurança, porque estas funções devem ser protegidas com cuidado:</span><span class="sxs-lookup"><span data-stu-id="0aaaf-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="0aaaf-124">Administrador de aplicativos</span><span class="sxs-lookup"><span data-stu-id="0aaaf-124">Application administrator</span></span>
  * <span data-ttu-id="0aaaf-125">Administrador do servidor de Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="0aaaf-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="0aaaf-126">Administrador de cobrança</span><span class="sxs-lookup"><span data-stu-id="0aaaf-126">Billing administrator</span></span>  
  * <span data-ttu-id="0aaaf-127">Administrador de conformidade</span><span class="sxs-lookup"><span data-stu-id="0aaaf-127">Compliance administrator</span></span>  
  * <span data-ttu-id="0aaaf-128">Administrador de serviços do CRM</span><span class="sxs-lookup"><span data-stu-id="0aaaf-128">CRM service administrator</span></span>
  * <span data-ttu-id="0aaaf-129">Aprovador de acesso do Sistema de Proteção de Dados do Cliente</span><span class="sxs-lookup"><span data-stu-id="0aaaf-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="0aaaf-130">Gravador de diretório</span><span class="sxs-lookup"><span data-stu-id="0aaaf-130">Directory writer</span></span>  
  * <span data-ttu-id="0aaaf-131">Administrador do Exchange</span><span class="sxs-lookup"><span data-stu-id="0aaaf-131">Exchange administrator</span></span>  
  * <span data-ttu-id="0aaaf-132">Administrador global</span><span class="sxs-lookup"><span data-stu-id="0aaaf-132">Global administrator</span></span>
  * <span data-ttu-id="0aaaf-133">Administrador de serviço do Intune</span><span class="sxs-lookup"><span data-stu-id="0aaaf-133">Intune service administrator</span></span>
  * <span data-ttu-id="0aaaf-134">Administrador de caixa de correio</span><span class="sxs-lookup"><span data-stu-id="0aaaf-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="0aaaf-135">Suporte de camada 1 do parceiro</span><span class="sxs-lookup"><span data-stu-id="0aaaf-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="0aaaf-136">Suporte de camada 2 do parceiro</span><span class="sxs-lookup"><span data-stu-id="0aaaf-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="0aaaf-137">Administrador de função com privilégios</span><span class="sxs-lookup"><span data-stu-id="0aaaf-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="0aaaf-138">Administrador de segurança</span><span class="sxs-lookup"><span data-stu-id="0aaaf-138">Security administrator</span></span>  
  * <span data-ttu-id="0aaaf-139">Administrador do SharePoint</span><span class="sxs-lookup"><span data-stu-id="0aaaf-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="0aaaf-140">Administrador do Skype for Business</span><span class="sxs-lookup"><span data-stu-id="0aaaf-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="0aaaf-141">Administrador da conta de usuário</span><span class="sxs-lookup"><span data-stu-id="0aaaf-141">User account administrator</span></span>  

<span data-ttu-id="0aaaf-142">Para obter mais informações sobre como usar MFA com PIM consulte [como tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="0aaaf-142">For more information about using MFA with PIM see [How tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="0aaaf-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0aaaf-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

