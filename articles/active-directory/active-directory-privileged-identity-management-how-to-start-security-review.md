---
title: "Como iniciar uma revisão de acesso | Microsoft Docs"
description: "Saiba como criar uma análise de acesso para identidades com privilégios com o aplicativo Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 2b516e2f05aa883c5e37f5864e5ee8a2b37d3a46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-start-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="4027b-103">Como iniciar uma análise de acesso no Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="4027b-103">How to start an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="4027b-104">As atribuições de função se tornam "obsoletas" quando os usuários têm acesso privilegiado de que não precisam mais.</span><span class="sxs-lookup"><span data-stu-id="4027b-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="4027b-105">Para reduzir o risco associado a essas atribuições de função obsoletas, os administradores de função com privilégios devem revisar regularmente as funções que os usuários receberam.</span><span class="sxs-lookup"><span data-stu-id="4027b-105">In order to reduce the risk associated with these stale role assignments, privileged role administrators should regularly review the roles that users have been given.</span></span> <span data-ttu-id="4027b-106">Este documento aborda as etapas para iniciar uma revisão de acesso no Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="4027b-106">This document covers the steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="4027b-107">Iniciar uma revisão de acesso</span><span class="sxs-lookup"><span data-stu-id="4027b-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="4027b-108">Se você não adicionou o aplicativo PIM ao painel no portal do Azure, consulte as etapas em [Introdução ao Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="4027b-108">If you haven't added the PIM application to your dashboard in the Azure portal, see the steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="4027b-109">Na página principal do aplicativo PIM, há três maneiras de iniciar uma revisão de acesso:</span><span class="sxs-lookup"><span data-stu-id="4027b-109">From the PIM application main page, there are three ways to start an access review:</span></span>

* <span data-ttu-id="4027b-110">**Acessar revisões** > **Adicionar**</span><span class="sxs-lookup"><span data-stu-id="4027b-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="4027b-111">**Funções** > **botão** Revisar</span><span class="sxs-lookup"><span data-stu-id="4027b-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="4027b-112">Selecione a função específica a ser revisada na lista de funções > **botão** Revisar</span><span class="sxs-lookup"><span data-stu-id="4027b-112">Select the specific role to be reviewed from the roles list > **Review** button</span></span>

<span data-ttu-id="4027b-113">Quando você clica no botão **Revisar**, a folha **Iniciar uma revisão de acesso** é exibida.</span><span class="sxs-lookup"><span data-stu-id="4027b-113">When you click on the **Review** button, the **Start an access review** blade appears.</span></span> <span data-ttu-id="4027b-114">Nessa folha, você vai configurar a análise com um nome e o limite de tempo, escolher uma função para examinar e decidir quem vai realizar a análise.</span><span class="sxs-lookup"><span data-stu-id="4027b-114">On this blade, you're going to configure the review with a name and time limit, choose a role to review, and decide who will perform the review.</span></span>

![Iniciar uma análise de acesso – captura de tela][1]

### <a name="configure-the-review"></a><span data-ttu-id="4027b-116">Configurar a análise</span><span class="sxs-lookup"><span data-stu-id="4027b-116">Configure the review</span></span>
<span data-ttu-id="4027b-117">Para criar uma análise de acesso, você precisa nomeá-la e definir uma data de início e de término.</span><span class="sxs-lookup"><span data-stu-id="4027b-117">To create an access review, you need to name it and set a start and end date.</span></span>

![Configurar a análise – captura de tela][2]

<span data-ttu-id="4027b-119">Deixe a duração da análise longa o suficiente para que os usuários a concluam.</span><span class="sxs-lookup"><span data-stu-id="4027b-119">Make the length of the review long enough for users to complete it.</span></span> <span data-ttu-id="4027b-120">Se você terminar antes da data de término, sempre poderá interromper a análise antes.</span><span class="sxs-lookup"><span data-stu-id="4027b-120">If you finish before the end date, you can always stop the review early.</span></span>

### <a name="choose-a-role-to-review"></a><span data-ttu-id="4027b-121">Escolher uma função para analisar</span><span class="sxs-lookup"><span data-stu-id="4027b-121">Choose a role to review</span></span>
<span data-ttu-id="4027b-122">Cada análise se concentra em apenas uma função.</span><span class="sxs-lookup"><span data-stu-id="4027b-122">Each review focuses on only one role.</span></span> <span data-ttu-id="4027b-123">A menos que tenha iniciado a análise de acesso em uma folha de função específica, você precisará escolher uma função agora.</span><span class="sxs-lookup"><span data-stu-id="4027b-123">Unless you started the access review from a specific role blade, you'll need to choose a role now.</span></span>

1. <span data-ttu-id="4027b-124">Navegue até **Analisar associação de função**</span><span class="sxs-lookup"><span data-stu-id="4027b-124">Navigate to **Review role membership**</span></span>
   
    ![Examinar a associação de função – captura de tela][3]
2. <span data-ttu-id="4027b-126">Escolha uma função na lista.</span><span class="sxs-lookup"><span data-stu-id="4027b-126">Choose one role from the list.</span></span>

### <a name="decide-who-will-perform-the-review"></a><span data-ttu-id="4027b-127">Decidir quem executará a análise</span><span class="sxs-lookup"><span data-stu-id="4027b-127">Decide who will perform the review</span></span>
<span data-ttu-id="4027b-128">Há três opções para executar uma análise.</span><span class="sxs-lookup"><span data-stu-id="4027b-128">There are three options for performing a review.</span></span> <span data-ttu-id="4027b-129">Você pode atribuir a revisão a alguém para ser concluída, pode fazer isso por conta própria ou deixar que cada usuário revise seu próprios acesso.</span><span class="sxs-lookup"><span data-stu-id="4027b-129">You can assign the review to someone else to complete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="4027b-130">Navegue até **Selecionar revisores**</span><span class="sxs-lookup"><span data-stu-id="4027b-130">Navigate to **Select reviewers**</span></span>
   
    ![Selecionar revisores – captura de tela][4]
2. <span data-ttu-id="4027b-132">Escolha uma das opções:</span><span class="sxs-lookup"><span data-stu-id="4027b-132">Choose one of the options:</span></span>
   
   * <span data-ttu-id="4027b-133">**Selecionar revisor**: use essa opção quando você não souber quem precisa de acesso.</span><span class="sxs-lookup"><span data-stu-id="4027b-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="4027b-134">Com essa opção, você pode atribuir a revisão a um proprietário de recurso ou ao gerente do grupo para conclusão.</span><span class="sxs-lookup"><span data-stu-id="4027b-134">With this option, you can assign the review to a resource owner or group manager to complete.</span></span>
   * <span data-ttu-id="4027b-135">**Me (Eu)**: útil se você deseja visualizar como as análises de acesso funcionam ou se deseja realizar a análise em nome de pessoas que não podem fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="4027b-135">**Me**: Useful if you want to preview how access reviews work, or you want to review on behalf of people who can't.</span></span>
   * <span data-ttu-id="4027b-136">**Members review themselves (Os membros realizam a própria análise)**: use essa opção para fazer com que os usuários examinem suas próprias atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="4027b-136">**Members review themselves**: Use this option to have the users review their own role assignments.</span></span>

### <a name="start-the-review"></a><span data-ttu-id="4027b-137">Iniciar a análise</span><span class="sxs-lookup"><span data-stu-id="4027b-137">Start the review</span></span>
<span data-ttu-id="4027b-138">Finalmente, você terá a opção de exigir que os usuários forneçam um motivo se eles aprovarem o acesso.</span><span class="sxs-lookup"><span data-stu-id="4027b-138">Finally, you have the option to require that users provide a reason if they approve their access.</span></span> <span data-ttu-id="4027b-139">Adicione uma descrição da análise se desejar e selecione **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="4027b-139">Add a description of the review if you like, and select **Start**.</span></span>

<span data-ttu-id="4027b-140">Certifique-se de permitir que os usuários saibam que há uma análise de acesso esperando por eles e mostre a eles [Como executar uma análise de acesso](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="4027b-140">Make sure you let your users know that there's an access review waiting for them, and show them [How to perform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-the-access-review"></a><span data-ttu-id="4027b-141">Gerenciar a análise de acesso</span><span class="sxs-lookup"><span data-stu-id="4027b-141">Manage the access review</span></span>
<span data-ttu-id="4027b-142">Você pode acompanhar o progresso conforme os revisores concluem suas análises no painel do Azure AD PIM na seção de análises de acesso.</span><span class="sxs-lookup"><span data-stu-id="4027b-142">You can track the progress as the reviewers complete their reviews in the Azure AD PIM dashboard, in the access reviews section.</span></span> <span data-ttu-id="4027b-143">Nenhum direito de acesso será alterado no diretório até a [análise ser concluída](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="4027b-143">No access rights will be changed in the directory until [the review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="4027b-144">Até o período de análise terminar, você pode lembrar os usuários de concluir sua análise ou interromper a análise antes da seção de análises de acesso.</span><span class="sxs-lookup"><span data-stu-id="4027b-144">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="4027b-145">Sumário do PIM</span><span class="sxs-lookup"><span data-stu-id="4027b-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
