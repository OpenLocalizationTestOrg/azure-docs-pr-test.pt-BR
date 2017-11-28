---
title: "Localizações nomeadas no Azure Active Directory | Microsoft Docs"
description: "Ao configurar localizações nomeadas, você pode evitar que endereços IP que pertencem à sua organização gerem falsos positivos para o tipo de evento de risco Viagem impossível a localizações atípicas."
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
ms.openlocfilehash: ff31ded1d9d60e47e0ae5f01119de78cd7f2df38
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="aeb62-103">Localizações nomeadas no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aeb62-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="aeb62-104">Com o recurso de localizações nomeadas do Azure Active Directory, você pode rotular os intervalos de endereços IP confiáveis em suas organizações.</span><span class="sxs-lookup"><span data-stu-id="aeb62-104">With the named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="aeb62-105">Em seu ambiente, você pode usar localizações nomeadas no contexto da detecção de [eventos de risco](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="aeb62-105">In your environment, you can use named locations in the context of the detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="aeb62-106">O recurso ajuda a reduzir o número de falsos positivos relatados para o tipo de evento de risco *Impossível viajar para localizações atípicas*.</span><span class="sxs-lookup"><span data-stu-id="aeb62-106">The feature helps reduce the number of reported false positives for the *Impossible travel to atypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="aeb62-107">Configuração</span><span class="sxs-lookup"><span data-stu-id="aeb62-107">Configuration</span></span>

<span data-ttu-id="aeb62-108">Para configurar uma localização nomeada:</span><span class="sxs-lookup"><span data-stu-id="aeb62-108">To configure a named location:</span></span>

1. <span data-ttu-id="aeb62-109">Entre no [Portal do Azure](https://portal.azure.com) como administrador global.</span><span class="sxs-lookup"><span data-stu-id="aeb62-109">Sign in to the [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="aeb62-110">No painel esquerdo, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aeb62-110">In the left pane, click **Azure Active Directory**.</span></span>

    ![O link do Azure Active Directory no painel esquerdo](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="aeb62-112">Na folha **Azure Active Directory**, na seção **Segurança**, clique em **Acesso condicional**.</span><span class="sxs-lookup"><span data-stu-id="aeb62-112">On the **Azure Active Directory** blade, in the **Security** section, click **Conditional access**.</span></span>

    ![O comando Acesso condicional](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="aeb62-114">Na folha **Acesso Condicional**, na seção **Gerenciar**, clique em **Localizações nomeadas**.</span><span class="sxs-lookup"><span data-stu-id="aeb62-114">On the **Conditional Access** blade, in the **Manage** section, click **Named locations**.</span></span>

    ![O comando Localizações nomeadas](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="aeb62-116">Na folha **Localizações nomeadas**, clique em **Novo local**.</span><span class="sxs-lookup"><span data-stu-id="aeb62-116">On the **Named locations** blade, click **New location**.</span></span>

    ![O comando Novo local](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="aeb62-118">Na folha **Novo**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="aeb62-118">On the **New** blade, do the following:</span></span>

    ![A Nova folha](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="aeb62-120">a.</span><span class="sxs-lookup"><span data-stu-id="aeb62-120">a.</span></span> <span data-ttu-id="aeb62-121">Na caixa **Nome**, digite um nome para a localização nomeada.</span><span class="sxs-lookup"><span data-stu-id="aeb62-121">In the **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="aeb62-122">b.</span><span class="sxs-lookup"><span data-stu-id="aeb62-122">b.</span></span> <span data-ttu-id="aeb62-123">Na caixa **Intervalos de IP**, digite um intervalo de IP.</span><span class="sxs-lookup"><span data-stu-id="aeb62-123">In the **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="aeb62-124">O intervalo de IP precisa estar no formato *CIDR* (Roteamento Entre Domínios Sem Classe).</span><span class="sxs-lookup"><span data-stu-id="aeb62-124">The IP range needs to be in the *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="aeb62-125">c.</span><span class="sxs-lookup"><span data-stu-id="aeb62-125">c.</span></span> <span data-ttu-id="aeb62-126">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="aeb62-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="aeb62-127">O que você deve saber</span><span class="sxs-lookup"><span data-stu-id="aeb62-127">What you should know</span></span>

<span data-ttu-id="aeb62-128">**Atualizações em massa**: quando você cria ou atualiza localizações nomeadas, para atualizações em massa, você pode carregar ou baixar um arquivo CSV com os intervalos de IP.</span><span class="sxs-lookup"><span data-stu-id="aeb62-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with the IP ranges.</span></span> <span data-ttu-id="aeb62-129">Um carregamento adiciona os intervalos de IP no arquivo à lista em vez de substituir a lista.</span><span class="sxs-lookup"><span data-stu-id="aeb62-129">An upload adds the IP ranges in the file to the list instead of overwriting the list.</span></span>

![Os links para carregar e baixar arquivos](./media/active-directory-named-locations/09.png)


<span data-ttu-id="aeb62-131">**Limitações**: você pode definir um máximo de 60 localizações nomeadas com um intervalo de IP atribuído a cada uma delas.</span><span class="sxs-lookup"><span data-stu-id="aeb62-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned to each of them.</span></span> <span data-ttu-id="aeb62-132">Se você tiver apenas uma localização nomeada configurada, poderá definir até 500 intervalos de IP para ela.</span><span class="sxs-lookup"><span data-stu-id="aeb62-132">If you have just one named location configured, you can define up to 500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="aeb62-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aeb62-133">Next steps</span></span>

<span data-ttu-id="aeb62-134">Para saber mais sobre eventos de risco, veja [Eventos de risco do Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="aeb62-134">To learn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

