---
title: "notificações de proteção de identidade do Active Directory aaaAzure | Microsoft Docs"
description: "Saiba como as notificações dão suporte às suas atividades de investigação."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="8d34a-104">Notificações do Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="8d34a-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="8d34a-105">O Azure AD Identity Protection envia emails em dois tipos de notificação automatizado toohelp você gerenciar eventos de risco e risco do usuário:</span><span class="sxs-lookup"><span data-stu-id="8d34a-105">Azure AD Identity Protection sends two types of automated notification emails toohelp you manage user risk and risk events:</span></span>

* <span data-ttu-id="8d34a-106">Email de alerta de usuário comprometido</span><span class="sxs-lookup"><span data-stu-id="8d34a-106">User compromised alert email</span></span>
* <span data-ttu-id="8d34a-107">Email de resumo semanal</span><span class="sxs-lookup"><span data-stu-id="8d34a-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="8d34a-108">Email de alerta de usuário comprometido</span><span class="sxs-lookup"><span data-stu-id="8d34a-108">User compromised alert email</span></span>
<span data-ttu-id="8d34a-109">Um email de alerta de usuário comprometido é gerado quando o Azure AD Identity Protection identifica uma conta como comprometida.</span><span class="sxs-lookup"><span data-stu-id="8d34a-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="8d34a-110">email de saudação inclui toohello um link que os usuários sinalizados para relatório de risco no painel de proteção de identidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d34a-110">hello email includes a link toohello Users flagged for risk report in hello Identity Protection dashboard.</span></span> <span data-ttu-id="8d34a-111">É recomendável investigar imediatamente as notificações das contas comprometidas.</span><span class="sxs-lookup"><span data-stu-id="8d34a-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="8d34a-112">Email de resumo semanal</span><span class="sxs-lookup"><span data-stu-id="8d34a-112">Weekly digest email</span></span>
<span data-ttu-id="8d34a-113">email de resumo semanal Olá contém um resumo dos novos eventos de risco.</span><span class="sxs-lookup"><span data-stu-id="8d34a-113">hello weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="8d34a-114">Ele inclui:</span><span class="sxs-lookup"><span data-stu-id="8d34a-114">It includes:</span></span>

* <span data-ttu-id="8d34a-115">Usuários em risco</span><span class="sxs-lookup"><span data-stu-id="8d34a-115">Users at risk</span></span>
* <span data-ttu-id="8d34a-116">Atividades suspeitas</span><span class="sxs-lookup"><span data-stu-id="8d34a-116">Suspicious activities</span></span>
* <span data-ttu-id="8d34a-117">Vulnerabilidades detectadas</span><span class="sxs-lookup"><span data-stu-id="8d34a-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="8d34a-118">Toohello links relacionados a relatórios na proteção de identidade</span><span class="sxs-lookup"><span data-stu-id="8d34a-118">Links toohello related reports in Identity Protection</span></span>

<br><span data-ttu-id="8d34a-119">
![Correção](./media/active-directory-identityprotection-notifications/400.png "correção")
</span><span class="sxs-lookup"><span data-stu-id="8d34a-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="8d34a-120">É possível desativar o envio de um email de resumo semanal.</span><span class="sxs-lookup"><span data-stu-id="8d34a-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="8d34a-121">
![Riscos de usuário](./media/active-directory-identityprotection-notifications/62.png "riscos de usuário")
</span><span class="sxs-lookup"><span data-stu-id="8d34a-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="8d34a-122">**caixa de diálogo de configuração relacionados de saudação tooopen**:</span><span class="sxs-lookup"><span data-stu-id="8d34a-122">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="8d34a-123">Em Olá **Azure AD Identity Protection** folha, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="8d34a-123">On hello **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="8d34a-124">
   ![Política de risco do usuário](./media/active-directory-identityprotection-notifications/401.png "política de risco do usuário")
   </span><span class="sxs-lookup"><span data-stu-id="8d34a-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="8d34a-125">Em Olá **geral** seção, clique em **notificações**.</span><span class="sxs-lookup"><span data-stu-id="8d34a-125">In hello **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="8d34a-126">
   ![Política de risco do usuário](./media/active-directory-identityprotection-notifications/405.png "política de risco do usuário")
   </span><span class="sxs-lookup"><span data-stu-id="8d34a-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="8d34a-127">Consulte também</span><span class="sxs-lookup"><span data-stu-id="8d34a-127">See also</span></span>
* [<span data-ttu-id="8d34a-128">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="8d34a-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
