---
title: locais de aaaNamed no Active Directory do Azure | Microsoft Docs
description: "Configurando denominado locais, você poderá evitar IP endereços pertencentes a sua organização geram falsos positivos para locais de tooatypical viagem impossível Olá corre o risco de tipo de evento."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="5c844-103">Localizações nomeadas no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c844-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="5c844-104">Com hello denominado recursos locais do Active Directory do Azure, você pode rotular intervalos de endereço IP confiável em sua organização.</span><span class="sxs-lookup"><span data-stu-id="5c844-104">With hello named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="5c844-105">Em seu ambiente, você pode usar locais nomeadas no contexto de saudação da detecção de saudação do [eventos de risco](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="5c844-105">In your environment, you can use named locations in hello context of hello detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="5c844-106">recurso de saudação ajuda a reduzir o número de saudação de relatado falsos positivos para Olá *viagem impossível tooatypical locais* corre o risco de tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="5c844-106">hello feature helps reduce hello number of reported false positives for hello *Impossible travel tooatypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="5c844-107">Configuração</span><span class="sxs-lookup"><span data-stu-id="5c844-107">Configuration</span></span>

<span data-ttu-id="5c844-108">tooconfigure um local nomeado:</span><span class="sxs-lookup"><span data-stu-id="5c844-108">tooconfigure a named location:</span></span>

1. <span data-ttu-id="5c844-109">Entrar toohello [portal do Azure](https://portal.azure.com) como administrador global.</span><span class="sxs-lookup"><span data-stu-id="5c844-109">Sign in toohello [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="5c844-110">No painel esquerdo do hello, clique em **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5c844-110">In hello left pane, click **Azure Active Directory**.</span></span>

    ![link do Active Directory do Azure Olá no painel esquerdo da saudação](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="5c844-112">Em Olá **Active Directory do Azure** folha em Olá **segurança** seção, clique em **acesso condicional**.</span><span class="sxs-lookup"><span data-stu-id="5c844-112">On hello **Azure Active Directory** blade, in hello **Security** section, click **Conditional access**.</span></span>

    ![Olá comando de acesso condicional](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="5c844-114">Em Olá **acesso condicional** folha em Olá **gerenciar** seção, clique em **chamado locais**.</span><span class="sxs-lookup"><span data-stu-id="5c844-114">On hello **Conditional Access** blade, in hello **Manage** section, click **Named locations**.</span></span>

    ![Olá nomeados locais comando](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="5c844-116">Em Olá **chamado locais** folha, clique em **novo local**.</span><span class="sxs-lookup"><span data-stu-id="5c844-116">On hello **Named locations** blade, click **New location**.</span></span>

    ![Olá novo comando de local](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="5c844-118">Em Olá **novo** folha, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c844-118">On hello **New** blade, do hello following:</span></span>

    ![blade de nova Olá](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="5c844-120">a.</span><span class="sxs-lookup"><span data-stu-id="5c844-120">a.</span></span> <span data-ttu-id="5c844-121">Em Olá **nome** , digite um nome para seu local nomeada.</span><span class="sxs-lookup"><span data-stu-id="5c844-121">In hello **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="5c844-122">b.</span><span class="sxs-lookup"><span data-stu-id="5c844-122">b.</span></span> <span data-ttu-id="5c844-123">Em Olá **intervalos IP** , digite um intervalo de IP.</span><span class="sxs-lookup"><span data-stu-id="5c844-123">In hello **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="5c844-124">intervalo IP Hello precisa toobe em Olá *CIDR* formato (CIDR).</span><span class="sxs-lookup"><span data-stu-id="5c844-124">hello IP range needs toobe in hello *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="5c844-125">c.</span><span class="sxs-lookup"><span data-stu-id="5c844-125">c.</span></span> <span data-ttu-id="5c844-126">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5c844-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="5c844-127">O que você deve saber</span><span class="sxs-lookup"><span data-stu-id="5c844-127">What you should know</span></span>

<span data-ttu-id="5c844-128">**Atualizações em massa**: quando você cria ou atualiza locais nomeadas, as atualizações em massa, você pode carregar ou baixar um arquivo CSV com os intervalos IP hello.</span><span class="sxs-lookup"><span data-stu-id="5c844-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with hello IP ranges.</span></span> <span data-ttu-id="5c844-129">Um carregamento adiciona intervalos IP hello na lista de toohello Olá arquivos em vez de substituir a lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c844-129">An upload adds hello IP ranges in hello file toohello list instead of overwriting hello list.</span></span>

![Olá Upload e Download de links](./media/active-directory-named-locations/09.png)


<span data-ttu-id="5c844-131">**Limitações**: você pode definir um máximo de 60 locais nomeados, com um tooeach de intervalo atribuído IP deles.</span><span class="sxs-lookup"><span data-stu-id="5c844-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned tooeach of them.</span></span> <span data-ttu-id="5c844-132">Se você tiver apenas um local nomeado configurado, você pode definir intervalos IP too500 para ele.</span><span class="sxs-lookup"><span data-stu-id="5c844-132">If you have just one named location configured, you can define up too500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5c844-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c844-133">Next steps</span></span>

<span data-ttu-id="5c844-134">toolearn mais informações sobre eventos de risco, consulte [eventos de risco do Active Directory do Azure](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="5c844-134">toolearn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

