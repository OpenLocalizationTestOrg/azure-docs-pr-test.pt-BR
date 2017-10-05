---
title: "Notificações do Azure Active Directory Identity Protection | Microsoft Docs"
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
ms.openlocfilehash: 079d16bbf75cd2b3b94269d684e1ae1a0e6aa967
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="8c8ec-104">Notificações do Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="8c8ec-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="8c8ec-105">O Azure AD Identity Protection envia dois tipos de emails de notificação automatizados para ajudar você a gerenciar o risco do usuário e eventos de risco:</span><span class="sxs-lookup"><span data-stu-id="8c8ec-105">Azure AD Identity Protection sends two types of automated notification emails to help you manage user risk and risk events:</span></span>

* <span data-ttu-id="8c8ec-106">Email de alerta de usuário comprometido</span><span class="sxs-lookup"><span data-stu-id="8c8ec-106">User compromised alert email</span></span>
* <span data-ttu-id="8c8ec-107">Email de resumo semanal</span><span class="sxs-lookup"><span data-stu-id="8c8ec-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="8c8ec-108">Email de alerta de usuário comprometido</span><span class="sxs-lookup"><span data-stu-id="8c8ec-108">User compromised alert email</span></span>
<span data-ttu-id="8c8ec-109">Um email de alerta de usuário comprometido é gerado quando o Azure AD Identity Protection identifica uma conta como comprometida.</span><span class="sxs-lookup"><span data-stu-id="8c8ec-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="8c8ec-110">O email inclui um link para os Usuários sinalizados para o relatório de risco no painel do Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="8c8ec-110">The email includes a link to the Users flagged for risk report in the Identity Protection dashboard.</span></span> <span data-ttu-id="8c8ec-111">É recomendável investigar imediatamente as notificações das contas comprometidas.</span><span class="sxs-lookup"><span data-stu-id="8c8ec-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="8c8ec-112">Email de resumo semanal</span><span class="sxs-lookup"><span data-stu-id="8c8ec-112">Weekly digest email</span></span>
<span data-ttu-id="8c8ec-113">O email de resumo semanal contém um resumo dos novos eventos de risco.</span><span class="sxs-lookup"><span data-stu-id="8c8ec-113">The weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="8c8ec-114">Ele inclui:</span><span class="sxs-lookup"><span data-stu-id="8c8ec-114">It includes:</span></span>

* <span data-ttu-id="8c8ec-115">Usuários em risco</span><span class="sxs-lookup"><span data-stu-id="8c8ec-115">Users at risk</span></span>
* <span data-ttu-id="8c8ec-116">Atividades suspeitas</span><span class="sxs-lookup"><span data-stu-id="8c8ec-116">Suspicious activities</span></span>
* <span data-ttu-id="8c8ec-117">Vulnerabilidades detectadas</span><span class="sxs-lookup"><span data-stu-id="8c8ec-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="8c8ec-118">Links para os relatórios relacionados no Identity Protection</span><span class="sxs-lookup"><span data-stu-id="8c8ec-118">Links to the related reports in Identity Protection</span></span>

<br><span data-ttu-id="8c8ec-119">
![Correção](./media/active-directory-identityprotection-notifications/400.png "correção")
</span><span class="sxs-lookup"><span data-stu-id="8c8ec-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="8c8ec-120">É possível desativar o envio de um email de resumo semanal.</span><span class="sxs-lookup"><span data-stu-id="8c8ec-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="8c8ec-121">
![Riscos de usuário](./media/active-directory-identityprotection-notifications/62.png "riscos de usuário")
</span><span class="sxs-lookup"><span data-stu-id="8c8ec-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="8c8ec-122">**Para abrir o diálogo de configurações relacionadas**:</span><span class="sxs-lookup"><span data-stu-id="8c8ec-122">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="8c8ec-123">Na folha **Azure AD Identity Protection**, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="8c8ec-123">On the **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="8c8ec-124">
   ![Política de risco do usuário](./media/active-directory-identityprotection-notifications/401.png "política de risco do usuário")
   </span><span class="sxs-lookup"><span data-stu-id="8c8ec-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="8c8ec-125">Na seção **Geral**, clique em **Notificações**.</span><span class="sxs-lookup"><span data-stu-id="8c8ec-125">In the **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="8c8ec-126">
   ![Política de risco do usuário](./media/active-directory-identityprotection-notifications/405.png "política de risco do usuário")
   </span><span class="sxs-lookup"><span data-stu-id="8c8ec-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="8c8ec-127">Consulte também</span><span class="sxs-lookup"><span data-stu-id="8c8ec-127">See also</span></span>
* [<span data-ttu-id="8c8ec-128">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="8c8ec-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
