---
title: "Como gerenciar configurações de ativação de função | Microsoft Docs"
description: "Aprenda a alterar as configurações padrão para identidades com privilégios com a extensão Privileged Identity Management do Azure Active Directory."
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
ms.openlocfilehash: 23605e89cd1846d2e06e48cb5d3e0191cb9e9b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="8baf8-103">Como gerenciar as configurações de ativação de função no Privileged Identity Management do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8baf8-103">How to manage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="8baf8-104">Um administrador de função com privilégios pode personalizar o Azure AD PIM (Privileged Identity Management) em sua organização, incluindo alterar a experiência de um usuário que está ativando uma atribuição de função elegível.</span><span class="sxs-lookup"><span data-stu-id="8baf8-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-the-role-activation-settings"></a><span data-ttu-id="8baf8-105">Gerenciar as configurações de ativação de função</span><span class="sxs-lookup"><span data-stu-id="8baf8-105">Manage the role activation settings</span></span>
1. <span data-ttu-id="8baf8-106">Acesse o [portal do Azure](https://portal.azure.com) e selecione o aplicativo **Azure AD Privileged Identity Management** do painel.</span><span class="sxs-lookup"><span data-stu-id="8baf8-106">Go to the [Azure portal](https://portal.azure.com) and select the **Azure AD Privileged Identity Management** app from the dashboard.</span></span>
2. <span data-ttu-id="8baf8-107">Selecione **Gerenciar funções privilegiadas** > **Configurações** > **Funções Privilegiadas**.</span><span class="sxs-lookup"><span data-stu-id="8baf8-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="8baf8-108">Escolha a função cujas configurações você deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="8baf8-108">Choose the role whose settings you want to manage.</span></span>

<span data-ttu-id="8baf8-109">Na página de configurações para cada função, há uma série de configurações que você pode realizar.</span><span class="sxs-lookup"><span data-stu-id="8baf8-109">On the settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="8baf8-110">Essas configurações afetam apenas os usuários que são administradores elegíveis, mas não os administradores permanentes.</span><span class="sxs-lookup"><span data-stu-id="8baf8-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="8baf8-111">**Ativações**: o tempo, em horas, pelo qual uma função fica ativa antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="8baf8-111">**Activations**: The time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="8baf8-112">Isso pode ser entre 1 e 72 horas.</span><span class="sxs-lookup"><span data-stu-id="8baf8-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="8baf8-113">**Notificações**: você pode escolher se o sistema envia ou não emails para administradores confirmando que eles ativaram uma função.</span><span class="sxs-lookup"><span data-stu-id="8baf8-113">**Notifications**: You can choose whether or not the system sends emails to admins confirming that they have activated a role.</span></span> <span data-ttu-id="8baf8-114">Isso pode ser útil para detectar ativações não autorizadas ou ilegítimas.</span><span class="sxs-lookup"><span data-stu-id="8baf8-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="8baf8-115">**Tíquete de Solicitação/Incidente**: você pode escolher se exigirá ou não que administradores elegíveis incluam um número de tíquete ao ativar sua função.</span><span class="sxs-lookup"><span data-stu-id="8baf8-115">**Incident/Request Ticket**: You can choose whether or not to require eligible admins to include a ticket number when they activate their role.</span></span> <span data-ttu-id="8baf8-116">Isso pode ser útil ao realizar auditorias de acesso à função.</span><span class="sxs-lookup"><span data-stu-id="8baf8-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="8baf8-117">**Multi-Factor Authentication**: você pode escolher se deseja ou não exigir que os usuários verifiquem sua identidade com MFA antes que possam ativar suas funções.</span><span class="sxs-lookup"><span data-stu-id="8baf8-117">**Multi-Factor Authentication**: You can choose whether or not to require users to verify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="8baf8-118">Os usuários só precisam verificar isso uma vez por sessão, não precisam fazê-lo toda vez que ativam uma função.</span><span class="sxs-lookup"><span data-stu-id="8baf8-118">They only have to verify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="8baf8-119">Há duas dicas para ter em mente quando você habilita a MFA:</span><span class="sxs-lookup"><span data-stu-id="8baf8-119">There are two tips to keep in mind when you enable MFA:</span></span>

* <span data-ttu-id="8baf8-120">Os usuários que têm contas da Microsoft para seus endereços de email (normalmente @outlook.com, mas nem sempre) não é possível registrar para o Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="8baf8-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="8baf8-121">Se quiser atribuir funções aos usuários com contas da Microsoft, você deverá torná-los administradores permanentes ou desabilitar o MFA para essa função.</span><span class="sxs-lookup"><span data-stu-id="8baf8-121">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="8baf8-122">Você não pode desabilitar o MFA para funções com altos privilégios do Azure AD e do Office365.</span><span class="sxs-lookup"><span data-stu-id="8baf8-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="8baf8-123">Esse é um recurso de segurança, porque estas funções devem ser protegidas com cuidado:</span><span class="sxs-lookup"><span data-stu-id="8baf8-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="8baf8-124">Administrador de aplicativos</span><span class="sxs-lookup"><span data-stu-id="8baf8-124">Application administrator</span></span>
  * <span data-ttu-id="8baf8-125">Administrador do servidor de Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8baf8-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="8baf8-126">Administrador de cobrança</span><span class="sxs-lookup"><span data-stu-id="8baf8-126">Billing administrator</span></span>  
  * <span data-ttu-id="8baf8-127">Administrador de conformidade</span><span class="sxs-lookup"><span data-stu-id="8baf8-127">Compliance administrator</span></span>  
  * <span data-ttu-id="8baf8-128">Administrador de serviços do CRM</span><span class="sxs-lookup"><span data-stu-id="8baf8-128">CRM service administrator</span></span>
  * <span data-ttu-id="8baf8-129">Aprovador de acesso do Sistema de Proteção de Dados do Cliente</span><span class="sxs-lookup"><span data-stu-id="8baf8-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="8baf8-130">Gravador de diretório</span><span class="sxs-lookup"><span data-stu-id="8baf8-130">Directory writer</span></span>  
  * <span data-ttu-id="8baf8-131">Administrador do Exchange</span><span class="sxs-lookup"><span data-stu-id="8baf8-131">Exchange administrator</span></span>  
  * <span data-ttu-id="8baf8-132">Administrador global</span><span class="sxs-lookup"><span data-stu-id="8baf8-132">Global administrator</span></span>
  * <span data-ttu-id="8baf8-133">Administrador de serviço do Intune</span><span class="sxs-lookup"><span data-stu-id="8baf8-133">Intune service administrator</span></span>
  * <span data-ttu-id="8baf8-134">Administrador de caixa de correio</span><span class="sxs-lookup"><span data-stu-id="8baf8-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="8baf8-135">Suporte de camada 1 do parceiro</span><span class="sxs-lookup"><span data-stu-id="8baf8-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="8baf8-136">Suporte de camada 2 do parceiro</span><span class="sxs-lookup"><span data-stu-id="8baf8-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="8baf8-137">Administrador de função com privilégios</span><span class="sxs-lookup"><span data-stu-id="8baf8-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="8baf8-138">Administrador de segurança</span><span class="sxs-lookup"><span data-stu-id="8baf8-138">Security administrator</span></span>  
  * <span data-ttu-id="8baf8-139">Administrador do SharePoint</span><span class="sxs-lookup"><span data-stu-id="8baf8-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="8baf8-140">Administrador do Skype for Business</span><span class="sxs-lookup"><span data-stu-id="8baf8-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="8baf8-141">Administrador da conta de usuário</span><span class="sxs-lookup"><span data-stu-id="8baf8-141">User account administrator</span></span>  

<span data-ttu-id="8baf8-142">Para obter mais informações sobre como usar MFA com PIM, consulte [Como Exigir MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="8baf8-142">For more information about using MFA with PIM see [How to Require MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="8baf8-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8baf8-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

