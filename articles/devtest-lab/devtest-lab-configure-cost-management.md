---
title: "Exibir a tendência de custo estimado mensal do laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Saiba mais sobre o gráfico de tendência de custo estimado mensal do Azure DevTest Labs."
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
ms.openlocfilehash: b3ad1ead522908d4b41b7cca98d20ac91664998e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="view-the-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="2285e-103">Exibir a tendência de custo estimado mensal do laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2285e-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="2285e-104">O recurso de gerenciamento de custos dos Laboratórios de Desenvolvimento/Teste ajuda a rastrear o custo de laboratório.</span><span class="sxs-lookup"><span data-stu-id="2285e-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span></span> <span data-ttu-id="2285e-105">Este artigo ilustra como usar o gráfico **Tendência de custo estimado mensal** para exibir o custo estimado até a data do mês do calendário atual e o custo projetado do final do mês para o mês do calendário atual.</span><span class="sxs-lookup"><span data-stu-id="2285e-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span></span> <span data-ttu-id="2285e-106">Neste artigo, você aprenderá a exibir o gráfico de tendência de custo estimado mensal no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2285e-106">In this article, you learn how to view the monthly estimated cost trend chart in the Azure portal.</span></span>

## <a name="viewing-the-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="2285e-107">Visualizando o gráfico Tendência de custo estimado mensal</span><span class="sxs-lookup"><span data-stu-id="2285e-107">Viewing the Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="2285e-108">Para exibir o gráfico Tendência de custo estimado mensal, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="2285e-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="2285e-109">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2285e-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="2285e-110">Selecione **Mais Serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="2285e-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="2285e-111">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="2285e-111">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="2285e-112">Na folha do laboratório, selecione **Configurações de custo**.</span><span class="sxs-lookup"><span data-stu-id="2285e-112">On the lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="2285e-113">Na folha **Configurações de custo** do laboratório, selecione **Tendência de custo do laboratório**.</span><span class="sxs-lookup"><span data-stu-id="2285e-113">On the lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="2285e-114">A captura de tela a seguir mostra um exemplo de um gráfico de custo.</span><span class="sxs-lookup"><span data-stu-id="2285e-114">The following screen shot shows an example of a cost chart.</span></span> 
   
    ![Gráfico de custo](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="2285e-116">O valor **Custo estimado** é o custo estimado até a data do mês do calendário atual.</span><span class="sxs-lookup"><span data-stu-id="2285e-116">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="2285e-117">O **Custo projetado** é o custo estimado para todo o mês do calendário atual, calculado usando o custo do laboratório nos cinco dias anteriores.</span><span class="sxs-lookup"><span data-stu-id="2285e-117">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span></span>

<span data-ttu-id="2285e-118">Observe que os valores do custo são arredondados para o próximo número inteiro.</span><span class="sxs-lookup"><span data-stu-id="2285e-118">The cost amounts are rounded up to the next whole number.</span></span> <span data-ttu-id="2285e-119">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2285e-119">For example:</span></span> 

* <span data-ttu-id="2285e-120">5.01 arredonda até 6</span><span class="sxs-lookup"><span data-stu-id="2285e-120">5.01 rounds up to 6</span></span> 
* <span data-ttu-id="2285e-121">5.50 arredonda até 6</span><span class="sxs-lookup"><span data-stu-id="2285e-121">5.50 rounds up to 6</span></span>
* <span data-ttu-id="2285e-122">5.99 arredonda até 6</span><span class="sxs-lookup"><span data-stu-id="2285e-122">5.99 rounds up to 6</span></span>

<span data-ttu-id="2285e-123">Como é indicado acima do gráfico, os custos vistos no gráfico são custos *estimados* usando as tarifas da oferta [Pré-paga](https://azure.microsoft.com/offers/ms-azr-0003p/) .</span><span class="sxs-lookup"><span data-stu-id="2285e-123">As it states above the chart, the costs you see in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="2285e-124">Além disso, o seguinte *não* está incluído no cálculo de custo:</span><span class="sxs-lookup"><span data-stu-id="2285e-124">Additionally, the following are *not* included in the cost calculation:</span></span>

* <span data-ttu-id="2285e-125">As assinaturas do CSP e do Dreamspark não têm suporte atualmente, pois o Azure DevTest Labs usa as [APIs de cobrança do Azure](../billing/billing-usage-rate-card-overview.md) para calcular o custo do laboratório e essas APIs não dão suporte a assinaturas do Dreamspark ou do CSP.</span><span class="sxs-lookup"><span data-stu-id="2285e-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="2285e-126">Suas tarifas da oferta.</span><span class="sxs-lookup"><span data-stu-id="2285e-126">Your offer rates.</span></span> <span data-ttu-id="2285e-127">No momento, não é possível usar as tarifas de oferta (mostradas em sua assinatura) que você negociou com a Microsoft ou parceiros Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2285e-127">Currently, we are not able to use your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="2285e-128">Estamos usando as tarifas pré-pagas.</span><span class="sxs-lookup"><span data-stu-id="2285e-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="2285e-129">Seus impostos</span><span class="sxs-lookup"><span data-stu-id="2285e-129">Your taxes</span></span>
* <span data-ttu-id="2285e-130">Seus descontos</span><span class="sxs-lookup"><span data-stu-id="2285e-130">Your discounts</span></span>
* <span data-ttu-id="2285e-131">Sua moeda de cobrança.</span><span class="sxs-lookup"><span data-stu-id="2285e-131">Your billing currency.</span></span> <span data-ttu-id="2285e-132">No momento, o custo do laboratório é exibido apenas na moeda USD.</span><span class="sxs-lookup"><span data-stu-id="2285e-132">Currently, the lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="2285e-133">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="2285e-133">Related blog posts</span></span>
* [<span data-ttu-id="2285e-134">Mais duas coisas para manter o custo sob controle em laboratórios de DevTest</span><span class="sxs-lookup"><span data-stu-id="2285e-134">Two more things to keep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="2285e-135">Por que os limites de custo?</span><span class="sxs-lookup"><span data-stu-id="2285e-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="2285e-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2285e-136">Next steps</span></span>
<span data-ttu-id="2285e-137">Eis aqui algumas coisas para experimentar a seguir:</span><span class="sxs-lookup"><span data-stu-id="2285e-137">Here are some things to try next:</span></span>

* <span data-ttu-id="2285e-138">[Definir políticas de laboratório](devtest-lab-set-lab-policy.md) - saiba como definir as várias políticas usadas para controlar como seu laboratório e suas VMs são usados.</span><span class="sxs-lookup"><span data-stu-id="2285e-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="2285e-139">[Criar imagem personalizada](devtest-lab-create-template.md) – durante a criação de uma VM, você especifica uma base, que pode ser uma imagem personalizada ou uma imagem do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2285e-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="2285e-140">Este artigo ilustra como criar uma imagem personalizada de um arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="2285e-140">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="2285e-141">[Configurar imagens do Marketplace](devtest-lab-configure-marketplace-images.md) — os DevTest Labs dão suporte à criação de VMs com base em imagens do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2285e-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="2285e-142">Este artigo ilustra como especificar quais imagens (caso haja alguma) do Azure Marketplace podem ser usadas durante a criação de VMs em um laboratório.</span><span class="sxs-lookup"><span data-stu-id="2285e-142">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="2285e-143">[Criar uma VM em um laboratório](devtest-lab-add-vm-with-artifacts.md) – ilustra como criar uma VM de uma imagem base (personalizada ou do Marketplace) e como trabalhar com artefatos na VM.</span><span class="sxs-lookup"><span data-stu-id="2285e-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

