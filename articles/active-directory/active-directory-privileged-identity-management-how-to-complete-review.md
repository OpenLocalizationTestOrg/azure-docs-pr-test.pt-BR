---
title: "Como concluir uma análise de acesso | Microsoft Docs"
description: "Depois de iniciar uma análise de acesso no Azure AD Privileged Identity Management, saiba como concluí-la e exibir os resultados"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: ca2a1c7c287e4cf6b1b50cfb0068861b6f525596
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-complete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="6b1eb-103">Como concluir uma análise de acesso no Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="6b1eb-103">How to complete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="6b1eb-104">os administradores de função com privilégios podem examinar o acesso privilegiado após uma [revisão de segurança ter sido iniciada](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="6b1eb-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="6b1eb-105">O Azure AD PIM (Privileged Identity Management) automaticamente enviará um email solicitando que os usuários revisem seu acesso.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span></span> <span data-ttu-id="6b1eb-106">Se um usuário não recebeu um email, você pode enviar para ele as instruções em [Como executar uma análise de segurança](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="6b1eb-106">If a user did not get an email, you can send them the instructions in [how to perform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="6b1eb-107">Depois do período de revisão de segurança, ou todos os usuários terminarem a autorrevisão, siga as etapas neste artigo para gerenciar a revisão e ver os resultados.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-107">After the security review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="6b1eb-108">Gerenciar revisões de segurança</span><span class="sxs-lookup"><span data-stu-id="6b1eb-108">Manage security reviews</span></span>
1. <span data-ttu-id="6b1eb-109">Acesse o [portal do Azure](https://portal.azure.com/) e selecione o aplicativo **Azure AD Privileged Identity Management** no painel.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="6b1eb-110">Clique na seção **Revisões de acesso** do painel.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-110">Select the **Access reviews** section of the dashboard.</span></span>
3. <span data-ttu-id="6b1eb-111">Selecione a análise de acesso que você deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-111">Select the access review that you want to manage.</span></span>

<span data-ttu-id="6b1eb-112">Na folha de detalhes da análise de acesso, há uma série de opções para o gerenciamento da análise.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-112">On the access review's detail blade there are a number options for managing that review.</span></span>

![Botões de análise de acesso do PIM - captura de tela][1]

### <a name="remind"></a><span data-ttu-id="6b1eb-114">Lembrar</span><span class="sxs-lookup"><span data-stu-id="6b1eb-114">Remind</span></span>
<span data-ttu-id="6b1eb-115">Se uma análise de acesso é configurada para que os usuários examinem a si mesmos, o botão **Lembrar** envia uma notificação.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="6b1eb-116">Parar</span><span class="sxs-lookup"><span data-stu-id="6b1eb-116">Stop</span></span>
<span data-ttu-id="6b1eb-117">Todas as revisões de acesso têm uma data de término, mas você pode usar o botão **Parar** para concluí-las mais cedo.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="6b1eb-118">Se quaisquer usuários ainda não tiverem sido examinados até este momento, eles não poderão ser após você parar a análise.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span></span> <span data-ttu-id="6b1eb-119">Não é possível reiniciar uma análise após ela ter sido interrompida.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="6b1eb-120">Aplicar</span><span class="sxs-lookup"><span data-stu-id="6b1eb-120">Apply</span></span>
<span data-ttu-id="6b1eb-121">Após uma análise de acesso ser concluída, seja porque você atingiu a data de término ou a interrompeu manualmente, o botão **Aplicar** implementa o resultado da análise.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span></span> <span data-ttu-id="6b1eb-122">Se o acesso de um usuário foi negado na análise, esta é a etapa que removerá sua atribuição de função.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="6b1eb-123">Exportação</span><span class="sxs-lookup"><span data-stu-id="6b1eb-123">Export</span></span>
<span data-ttu-id="6b1eb-124">Se você desejar aplicar os resultados da revisão de segurança manualmente, poderá exportar a revisão.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-124">If you want to apply the results of the security review manually, you can export the review.</span></span> <span data-ttu-id="6b1eb-125">O botão **Exportar** começará a baixar um arquivo CSV.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-125">The **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="6b1eb-126">Você pode gerenciar os resultados no Excel ou em outros programas que abrem arquivos CSV.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-126">You can manage the results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="6b1eb-127">Excluir</span><span class="sxs-lookup"><span data-stu-id="6b1eb-127">Delete</span></span>
<span data-ttu-id="6b1eb-128">Se você não estiver mais interessado na revisão, exclua-a.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-128">If you are not interested in the review any further, delete it.</span></span> <span data-ttu-id="6b1eb-129">O botão **Excluir** remove a análise do aplicativo PIM.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-129">The **Delete** button removes the review from the PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b1eb-130">Você não receberá nenhum aviso antes da exclusão, portanto, certifique-se de que deseja excluir a revisão.</span><span class="sxs-lookup"><span data-stu-id="6b1eb-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6b1eb-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6b1eb-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
