---
title: "aaaHow toostart uma revisão de acesso | Microsoft Docs"
description: "Saiba como toocreate um acesso examinar de identidades com privilégios com hello aplicativo Privileged Identity Management do Azure."
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
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="8d00d-103">Como toostart um acesso examinar no Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="8d00d-103">How toostart an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="8d00d-104">As atribuições de função se tornam "obsoletas" quando os usuários têm acesso privilegiado de que não precisam mais.</span><span class="sxs-lookup"><span data-stu-id="8d00d-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="8d00d-105">Em ordem tooreduce Olá os riscos associados com essas atribuições de funções obsoletas administradores com privilégios de função devem examinar regularmente funções hello que os usuários tem sido fornecidos.</span><span class="sxs-lookup"><span data-stu-id="8d00d-105">In order tooreduce hello risk associated with these stale role assignments, privileged role administrators should regularly review hello roles that users have been given.</span></span> <span data-ttu-id="8d00d-106">Este documento aborda etapas Olá para iniciar uma revisão de acesso no Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="8d00d-106">This document covers hello steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="8d00d-107">Iniciar uma revisão de acesso</span><span class="sxs-lookup"><span data-stu-id="8d00d-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="8d00d-108">Se você não adicionou o painel de tooyour do aplicativo de PIM Olá no hello portal do Azure, consulte as etapas de saudação em [guia de Introdução ao Privileged Identity Management do Azure](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="8d00d-108">If you haven't added hello PIM application tooyour dashboard in hello Azure portal, see hello steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="8d00d-109">Na página principal do aplicativo do PIM de Olá, há três toostart de maneiras uma revisão de acesso:</span><span class="sxs-lookup"><span data-stu-id="8d00d-109">From hello PIM application main page, there are three ways toostart an access review:</span></span>

* <span data-ttu-id="8d00d-110">**Acessar revisões** > **Adicionar**</span><span class="sxs-lookup"><span data-stu-id="8d00d-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="8d00d-111">**Funções** > **botão** Revisar</span><span class="sxs-lookup"><span data-stu-id="8d00d-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="8d00d-112">Selecione Olá função específica toobe revisado na lista de funções hello > **revisão** botão</span><span class="sxs-lookup"><span data-stu-id="8d00d-112">Select hello specific role toobe reviewed from hello roles list > **Review** button</span></span>

<span data-ttu-id="8d00d-113">Quando você clica na Olá **examine** botão hello **iniciar uma revisão de acesso** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="8d00d-113">When you click on hello **Review** button, hello **Start an access review** blade appears.</span></span> <span data-ttu-id="8d00d-114">Nesta folha, você está indo tooconfigure Olá revisão com um nome e tempo limite, escolha tooreview uma função e decide quem executará revisão hello.</span><span class="sxs-lookup"><span data-stu-id="8d00d-114">On this blade, you're going tooconfigure hello review with a name and time limit, choose a role tooreview, and decide who will perform hello review.</span></span>

![Iniciar uma análise de acesso – captura de tela][1]

### <a name="configure-hello-review"></a><span data-ttu-id="8d00d-116">Configurar análise Olá</span><span class="sxs-lookup"><span data-stu-id="8d00d-116">Configure hello review</span></span>
<span data-ttu-id="8d00d-117">toocreate um acesso revisar, é necessário tooname-lo e definir uma data de início e término.</span><span class="sxs-lookup"><span data-stu-id="8d00d-117">toocreate an access review, you need tooname it and set a start and end date.</span></span>

![Configurar a análise – captura de tela][2]

<span data-ttu-id="8d00d-119">Verifique o comprimento de saudação do hello revisar tempo suficiente para que os usuários toocomplete.</span><span class="sxs-lookup"><span data-stu-id="8d00d-119">Make hello length of hello review long enough for users toocomplete it.</span></span> <span data-ttu-id="8d00d-120">Se terminar antes da data de término hello, você pode interromper sempre revisão Olá no início.</span><span class="sxs-lookup"><span data-stu-id="8d00d-120">If you finish before hello end date, you can always stop hello review early.</span></span>

### <a name="choose-a-role-tooreview"></a><span data-ttu-id="8d00d-121">Escolha uma função tooreview</span><span class="sxs-lookup"><span data-stu-id="8d00d-121">Choose a role tooreview</span></span>
<span data-ttu-id="8d00d-122">Cada análise se concentra em apenas uma função.</span><span class="sxs-lookup"><span data-stu-id="8d00d-122">Each review focuses on only one role.</span></span> <span data-ttu-id="8d00d-123">A menos que você iniciou Olá acesso revisão da folha de uma função específica, você precisará toochoose uma função agora.</span><span class="sxs-lookup"><span data-stu-id="8d00d-123">Unless you started hello access review from a specific role blade, you'll need toochoose a role now.</span></span>

1. <span data-ttu-id="8d00d-124">Navegue muito**examinar associação de função**</span><span class="sxs-lookup"><span data-stu-id="8d00d-124">Navigate too**Review role membership**</span></span>
   
    ![Examinar a associação de função – captura de tela][3]
2. <span data-ttu-id="8d00d-126">Escolha uma função na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d00d-126">Choose one role from hello list.</span></span>

### <a name="decide-who-will-perform-hello-review"></a><span data-ttu-id="8d00d-127">Decidir quem executará revisão Olá</span><span class="sxs-lookup"><span data-stu-id="8d00d-127">Decide who will perform hello review</span></span>
<span data-ttu-id="8d00d-128">Há três opções para executar uma análise.</span><span class="sxs-lookup"><span data-stu-id="8d00d-128">There are three options for performing a review.</span></span> <span data-ttu-id="8d00d-129">Você pode atribuir Olá revisão toosomeone toocomplete else, você poderá fazê-lo, ou você pode fazer com que a cada usuário revisar seu próprios acesso.</span><span class="sxs-lookup"><span data-stu-id="8d00d-129">You can assign hello review toosomeone else toocomplete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="8d00d-130">Navegue muito**selecionar revisores**</span><span class="sxs-lookup"><span data-stu-id="8d00d-130">Navigate too**Select reviewers**</span></span>
   
    ![Selecionar revisores – captura de tela][4]
2. <span data-ttu-id="8d00d-132">Escolha uma das opções de saudação:</span><span class="sxs-lookup"><span data-stu-id="8d00d-132">Choose one of hello options:</span></span>
   
   * <span data-ttu-id="8d00d-133">**Selecionar revisor**: use essa opção quando você não souber quem precisa de acesso.</span><span class="sxs-lookup"><span data-stu-id="8d00d-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="8d00d-134">Com essa opção, você pode atribuir o proprietário do recurso Olá revisão tooa ou toocomplete do Gerenciador de grupo.</span><span class="sxs-lookup"><span data-stu-id="8d00d-134">With this option, you can assign hello review tooa resource owner or group manager toocomplete.</span></span>
   * <span data-ttu-id="8d00d-135">**Me**: útil se você quiser toopreview como acesso revisões de trabalho, ou se desejar tooreview em nome de pessoas que não é possível.</span><span class="sxs-lookup"><span data-stu-id="8d00d-135">**Me**: Useful if you want toopreview how access reviews work, or you want tooreview on behalf of people who can't.</span></span>
   * <span data-ttu-id="8d00d-136">**Membros reveja próprios**: Use esta opção toohave Olá usuários revisão suas atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="8d00d-136">**Members review themselves**: Use this option toohave hello users review their own role assignments.</span></span>

### <a name="start-hello-review"></a><span data-ttu-id="8d00d-137">Revisão de saudação inicial</span><span class="sxs-lookup"><span data-stu-id="8d00d-137">Start hello review</span></span>
<span data-ttu-id="8d00d-138">Por fim, você tem Olá opção toorequire que os usuários forneçam um motivo se eles aprovar o acesso.</span><span class="sxs-lookup"><span data-stu-id="8d00d-138">Finally, you have hello option toorequire that users provide a reason if they approve their access.</span></span> <span data-ttu-id="8d00d-139">Adicione uma descrição de revisão de saudação se desejar e selecione **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="8d00d-139">Add a description of hello review if you like, and select **Start**.</span></span>

<span data-ttu-id="8d00d-140">Certifique-se de permitir que os usuários saibam que se trata de uma revisão de acesso aguardar que eles e mostrá-los [como tooperform um acesso examine](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="8d00d-140">Make sure you let your users know that there's an access review waiting for them, and show them [How tooperform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-hello-access-review"></a><span data-ttu-id="8d00d-141">Gerenciar Olá acesso revisão</span><span class="sxs-lookup"><span data-stu-id="8d00d-141">Manage hello access review</span></span>
<span data-ttu-id="8d00d-142">Você pode acompanhar o progresso de saudação como revisores Olá concluir suas revisões em Olá painel PIM do AD do Azure, em Olá acesso revisões de seção.</span><span class="sxs-lookup"><span data-stu-id="8d00d-142">You can track hello progress as hello reviewers complete their reviews in hello Azure AD PIM dashboard, in hello access reviews section.</span></span> <span data-ttu-id="8d00d-143">Sem direitos de acesso serão alterados no diretório Olá até [revisão Olá conclui](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="8d00d-143">No access rights will be changed in hello directory until [hello review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="8d00d-144">Até que o período de revisão hello está acima, pode lembrar usuários toocomplete revisão ou parada Olá revisão no início do access Olá seção examina.</span><span class="sxs-lookup"><span data-stu-id="8d00d-144">Until hello review period is over, you can remind users toocomplete their review, or stop hello review early from hello access reviews section.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="8d00d-145">Sumário do PIM</span><span class="sxs-lookup"><span data-stu-id="8d00d-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
