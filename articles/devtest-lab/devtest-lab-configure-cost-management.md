---
title: "aaaView Olá mensal laboratório estimado tendência de custos no Azure DevTest Labs | Microsoft Docs"
description: "Saiba mais sobre o gráfico de tendências de custo estimado mensal do hello Azure DevTest Labs."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="11fd6-103">Exibição Olá mensal laboratório estimado tendência de custos no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="11fd6-103">View hello monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="11fd6-104">recurso de gerenciamento de custos de saudação do DevTest Labs ajuda a acompanhar o custo de saudação do seu laboratório.</span><span class="sxs-lookup"><span data-stu-id="11fd6-104">hello Cost Management feature of DevTest Labs helps you track hello cost of your lab.</span></span> <span data-ttu-id="11fd6-105">Este artigo ilustra como Olá toouse **mensal tendências de custo estimado** tooview gráfico Olá estimado custo acumulado do mês do calendário atual e Olá custo final do mês projetado para Olá mês do calendário atual.</span><span class="sxs-lookup"><span data-stu-id="11fd6-105">This article illustrates how toouse hello **Monthly Estimated Cost Trend** chart tooview hello current calendar month's estimated cost-to-date and hello projected end-of-month cost for hello current calendar month.</span></span> <span data-ttu-id="11fd6-106">Neste artigo, você aprenderá como tooview Olá mensal gráfico de tendências de custo estimado em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="11fd6-106">In this article, you learn how tooview hello monthly estimated cost trend chart in hello Azure portal.</span></span>

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="11fd6-107">Exibir gráfico de tendência mensal de custo estimado de saudação</span><span class="sxs-lookup"><span data-stu-id="11fd6-107">Viewing hello Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="11fd6-108">Olá tooview gráfico de tendência mensal de custo estimado, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="11fd6-108">tooview hello Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="11fd6-109">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="11fd6-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="11fd6-110">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="11fd6-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="11fd6-111">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="11fd6-111">From hello list of labs, select hello desired lab.</span></span>   
4. <span data-ttu-id="11fd6-112">Na folha do laboratório hello, selecione **configurações de custo**.</span><span class="sxs-lookup"><span data-stu-id="11fd6-112">On hello lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="11fd6-113">No laboratório de saudação **configurações de custo** folha, selecione **tendências de custo de laboratório**.</span><span class="sxs-lookup"><span data-stu-id="11fd6-113">On hello lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="11fd6-114">Olá, captura de tela a seguir mostra um exemplo de um gráfico de custo.</span><span class="sxs-lookup"><span data-stu-id="11fd6-114">hello following screen shot shows an example of a cost chart.</span></span> 
   
    ![Gráfico de custo](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="11fd6-116">Olá **custo estimado** valor é bom dia estimado custo acumulado do mês do calendário atual.</span><span class="sxs-lookup"><span data-stu-id="11fd6-116">hello **Estimated cost** value is hello current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="11fd6-117">Olá **custo projetado** hello custo estimado de saudação todo mês do calendário atual, calculado usando custo de laboratório Olá para Olá cinco dias anteriores.</span><span class="sxs-lookup"><span data-stu-id="11fd6-117">hello **Projected cost** is hello estimated cost for hello entire current calendar month, calculated using hello lab cost for hello previous five days.</span></span>

<span data-ttu-id="11fd6-118">os valores de custo Olá são arredondados toohello próximo número de inteiro.</span><span class="sxs-lookup"><span data-stu-id="11fd6-118">hello cost amounts are rounded up toohello next whole number.</span></span> <span data-ttu-id="11fd6-119">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="11fd6-119">For example:</span></span> 

* <span data-ttu-id="11fd6-120">Arredonda 5.01 too6</span><span class="sxs-lookup"><span data-stu-id="11fd6-120">5.01 rounds up too6</span></span> 
* <span data-ttu-id="11fd6-121">Arredonda 5.50 too6</span><span class="sxs-lookup"><span data-stu-id="11fd6-121">5.50 rounds up too6</span></span>
* <span data-ttu-id="11fd6-122">Arredonda 5.99 too6</span><span class="sxs-lookup"><span data-stu-id="11fd6-122">5.99 rounds up too6</span></span>

<span data-ttu-id="11fd6-123">Como ele declara acima gráfico hello, custos Olá exibidos no gráfico de saudação são *estimado* custos usando [pré-pago](https://azure.microsoft.com/offers/ms-azr-0003p/) oferecem taxas.</span><span class="sxs-lookup"><span data-stu-id="11fd6-123">As it states above hello chart, hello costs you see in hello chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="11fd6-124">Além disso, Olá seguem *não* incluído no cálculo do custo de saudação:</span><span class="sxs-lookup"><span data-stu-id="11fd6-124">Additionally, hello following are *not* included in hello cost calculation:</span></span>

* <span data-ttu-id="11fd6-125">As assinaturas do Dreamspark e o CSP não há suporte atualmente como Azure DevTest Labs usa Olá [APIs de cobrança do Azure](../billing/billing-usage-rate-card-overview.md) toocalculate laboratório de saudação de custo, que não dá suporte a assinaturas do Dreamspark ou de CSP.</span><span class="sxs-lookup"><span data-stu-id="11fd6-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses hello [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) toocalculate hello lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="11fd6-126">Suas tarifas da oferta.</span><span class="sxs-lookup"><span data-stu-id="11fd6-126">Your offer rates.</span></span> <span data-ttu-id="11fd6-127">No momento, não estamos toouse capaz de suas taxas de oferta (mostradas em sua assinatura) que você tenha negociado com a Microsoft ou Microsoft parceiros.</span><span class="sxs-lookup"><span data-stu-id="11fd6-127">Currently, we are not able toouse your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="11fd6-128">Estamos usando as tarifas pré-pagas.</span><span class="sxs-lookup"><span data-stu-id="11fd6-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="11fd6-129">Seus impostos</span><span class="sxs-lookup"><span data-stu-id="11fd6-129">Your taxes</span></span>
* <span data-ttu-id="11fd6-130">Seus descontos</span><span class="sxs-lookup"><span data-stu-id="11fd6-130">Your discounts</span></span>
* <span data-ttu-id="11fd6-131">Sua moeda de cobrança.</span><span class="sxs-lookup"><span data-stu-id="11fd6-131">Your billing currency.</span></span> <span data-ttu-id="11fd6-132">No momento, o custo de laboratório Olá é exibido apenas na moeda USD.</span><span class="sxs-lookup"><span data-stu-id="11fd6-132">Currently, hello lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="11fd6-133">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="11fd6-133">Related blog posts</span></span>
* [<span data-ttu-id="11fd6-134">Dois tookeep coisas mais seu custo na faixa de DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="11fd6-134">Two more things tookeep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="11fd6-135">Por que os limites de custo?</span><span class="sxs-lookup"><span data-stu-id="11fd6-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="11fd6-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11fd6-136">Next steps</span></span>
<span data-ttu-id="11fd6-137">Aqui estão algumas coisas tootry lado:</span><span class="sxs-lookup"><span data-stu-id="11fd6-137">Here are some things tootry next:</span></span>

* <span data-ttu-id="11fd6-138">[Definir políticas de laboratório](devtest-lab-set-lab-policy.md) -Saiba como tooset Olá várias políticas usadas toogovern como seu laboratório e suas VMs são usados.</span><span class="sxs-lookup"><span data-stu-id="11fd6-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how tooset hello various policies used toogovern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="11fd6-139">[Criar imagem personalizada](devtest-lab-create-template.md) – durante a criação de uma VM, você especifica uma base, que pode ser uma imagem personalizada ou uma imagem do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="11fd6-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="11fd6-140">Este artigo ilustra como toocreate um personalizado da imagem de um arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="11fd6-140">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="11fd6-141">[Configurar imagens do Marketplace](devtest-lab-configure-marketplace-images.md) — os DevTest Labs dão suporte à criação de VMs com base em imagens do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="11fd6-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="11fd6-142">Este artigo ilustra como toospecify que, se houver, imagens do Azure Marketplace podem ser usado ao criar máquinas virtuais em um laboratório.</span><span class="sxs-lookup"><span data-stu-id="11fd6-142">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="11fd6-143">[Criar uma máquina virtual em um laboratório](devtest-lab-add-vm-with-artifacts.md) -ilustra como toocreate uma VM por meio de uma imagem de base (ou personalizadas ou Marketplace) e como toowork com artefatos em sua VM.</span><span class="sxs-lookup"><span data-stu-id="11fd6-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

