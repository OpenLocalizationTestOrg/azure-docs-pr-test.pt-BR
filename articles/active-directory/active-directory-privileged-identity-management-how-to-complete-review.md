---
title: "aaaHow toocomplete uma revisão de acesso | Microsoft Docs"
description: "Depois que você iniciou uma revisão de acesso no Azure AD Privileged Identity Management, saiba como toocomplete-lo e exibir resultados de Olá"
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
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="2a853-103">Como toocomplete um acesso examinar no Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="2a853-103">How toocomplete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="2a853-104">os administradores de função com privilégios podem examinar o acesso privilegiado após uma [revisão de segurança ter sido iniciada](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="2a853-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="2a853-105">O Azure AD Privileged Identity Management (PIM) automaticamente enviará um email solicitando que os usuários tooreview seu acesso.</span><span class="sxs-lookup"><span data-stu-id="2a853-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users tooreview their access.</span></span> <span data-ttu-id="2a853-106">Se um usuário não obteve um email, você pode enviá-los instruções Olá [como tooperform segurança examine](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="2a853-106">If a user did not get an email, you can send them hello instructions in [how tooperform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="2a853-107">Após o período de revisão de segurança hello, ou todos os usuários de saudação terminar seus Self revisar, siga as etapas de saudação nesta revisão de saudação do artigo toomanage e ver os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a853-107">After hello security review period is over, or all hello users have finished their self-review, follow hello steps in this article toomanage hello review and see hello results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="2a853-108">Gerenciar revisões de segurança</span><span class="sxs-lookup"><span data-stu-id="2a853-108">Manage security reviews</span></span>
1. <span data-ttu-id="2a853-109">Vá toohello [portal do Azure](https://portal.azure.com/) e selecione hello **do Azure AD Privileged Identity Management** aplicativo em seu painel.</span><span class="sxs-lookup"><span data-stu-id="2a853-109">Go toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="2a853-110">Selecione Olá **acessar revisões** seção do painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a853-110">Select hello **Access reviews** section of hello dashboard.</span></span>
3. <span data-ttu-id="2a853-111">Selecione a revisão de acesso de saudação que você deseja toomanage.</span><span class="sxs-lookup"><span data-stu-id="2a853-111">Select hello access review that you want toomanage.</span></span>

<span data-ttu-id="2a853-112">Na folha de detalhe da avaliação do acesso hello, há várias formas para gerenciar essa revisão.</span><span class="sxs-lookup"><span data-stu-id="2a853-112">On hello access review's detail blade there are a number options for managing that review.</span></span>

![Botões de análise de acesso do PIM - captura de tela][1]

### <a name="remind"></a><span data-ttu-id="2a853-114">Lembrar</span><span class="sxs-lookup"><span data-stu-id="2a853-114">Remind</span></span>
<span data-ttu-id="2a853-115">Se uma revisão de acesso está configurada para que os usuários de saudação examinar se, Olá **lembrar** botão envia uma notificação.</span><span class="sxs-lookup"><span data-stu-id="2a853-115">If an access review is set up so that hello users review themselves, hello **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="2a853-116">Parar</span><span class="sxs-lookup"><span data-stu-id="2a853-116">Stop</span></span>
<span data-ttu-id="2a853-117">Todas as revisões de acesso têm uma data de término, mas você pode usar o hello **parar** toofinish botão antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="2a853-117">All access reviews have an end date, but you can use hello **Stop** button toofinish it early.</span></span> <span data-ttu-id="2a853-118">Se todos os usuários ainda não foram revisados neste momento, eles não será capaz de tooafter Parar análise hello.</span><span class="sxs-lookup"><span data-stu-id="2a853-118">If any users haven't been reviewed by this time, they won't be able tooafter you stop hello review.</span></span> <span data-ttu-id="2a853-119">Não é possível reiniciar uma análise após ela ter sido interrompida.</span><span class="sxs-lookup"><span data-stu-id="2a853-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="2a853-120">Aplicar</span><span class="sxs-lookup"><span data-stu-id="2a853-120">Apply</span></span>
<span data-ttu-id="2a853-121">Depois de uma revisão de acesso é concluída, seja porque você atingiu a data de término hello ou parado-lo manualmente, Olá **aplicar** botão implementa o resultado de saudação da revisão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a853-121">After an access review is completed, either because you reached hello end date or stopped it manually, hello **Apply** button implements hello outcome of hello review.</span></span> <span data-ttu-id="2a853-122">Se o acesso do usuário foi negado na revisão Olá, esta é a etapa de saudação removerá sua atribuição de função.</span><span class="sxs-lookup"><span data-stu-id="2a853-122">If a user's access was denied in hello review, this is hello step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="2a853-123">Exportação</span><span class="sxs-lookup"><span data-stu-id="2a853-123">Export</span></span>
<span data-ttu-id="2a853-124">Se você quiser resultados de saudação do tooapply de revisão de segurança Olá manualmente, você pode exportar revisão hello.</span><span class="sxs-lookup"><span data-stu-id="2a853-124">If you want tooapply hello results of hello security review manually, you can export hello review.</span></span> <span data-ttu-id="2a853-125">Olá **exportar** botão começará a baixar um arquivo CSV.</span><span class="sxs-lookup"><span data-stu-id="2a853-125">hello **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="2a853-126">Você pode gerenciar resultados Olá no Excel ou em outros programas que abrem os arquivos CSV.</span><span class="sxs-lookup"><span data-stu-id="2a853-126">You can manage hello results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="2a853-127">Exclusão</span><span class="sxs-lookup"><span data-stu-id="2a853-127">Delete</span></span>
<span data-ttu-id="2a853-128">Se você não estiver interessado em Olá analise qualquer adicional, excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="2a853-128">If you are not interested in hello review any further, delete it.</span></span> <span data-ttu-id="2a853-129">Olá **excluir** botão remove Olá revisão da saudação aplicativo PIM.</span><span class="sxs-lookup"><span data-stu-id="2a853-129">hello **Delete** button removes hello review from hello PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a853-130">Você não receberá um aviso antes da exclusão, portanto certifique-se de que você deseja toodelete examinar.</span><span class="sxs-lookup"><span data-stu-id="2a853-130">You will not get a warning before deletion occurs, so be sure that you want toodelete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2a853-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a853-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
