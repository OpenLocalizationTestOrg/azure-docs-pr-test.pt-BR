---
title: "Solicitações de aumento de cota de núcleo do Azure Resource Manager | Microsoft Docs"
description: "Solicitações de aumento de cota de núcleo do Azure Resource Manager"
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a><span data-ttu-id="ceab9-103">Solicitações de aumento de cota de núcleo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ceab9-103">Resource Manager core quota increase requests</span></span>

<span data-ttu-id="ceab9-104">As cotas de núcleo do Resource Manager são aplicadas no nível da região e no nível de família de SKU.</span><span class="sxs-lookup"><span data-stu-id="ceab9-104">Resource Manager core quotas are enforced at the region level and SKU family level.</span></span>
<span data-ttu-id="ceab9-105">Saiba mais sobre como as cotas são aplicadas na página [Limites de serviço da assinatura do Azure ](http://aka.ms/quotalimits).</span><span class="sxs-lookup"><span data-stu-id="ceab9-105">Learn more about how quotas are enforced on the [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="ceab9-106">Para saber mais sobre as famílias de SKU, compare custo e desempenho na página [Preços de máquinas virtuais](http://aka.ms/pricingcompute).</span><span class="sxs-lookup"><span data-stu-id="ceab9-106">To learn more about SKU Families, you may compare cost and performance on the [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="ceab9-107">Para solicitar um aumento, crie um caso de suporte de Cota para Núcleos no Portal do Azure, [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ceab9-107">To request an increase, create a Quota support case for Cores in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="ceab9-108">Saiba como [criar uma solicitação de suporte](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ceab9-108">Learn how to [create a support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in the Azure portal</span></span>

1. <span data-ttu-id="ceab9-109">Na página de nova solicitação de suporte, selecione o Tipo de problema como "Cota" e o Tipo de cota como "Núcleos".</span><span class="sxs-lookup"><span data-stu-id="ceab9-109">On the new support request page, select Issue type as "Quota" and Quota type as "Cores".</span></span>

    ![Folha de Noções Básicas de Cota](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. <span data-ttu-id="ceab9-111">Selecione o Modelo de implantação como "Resource Manager" e selecione um local.</span><span class="sxs-lookup"><span data-stu-id="ceab9-111">Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![Folha Problema de Cota](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="ceab9-113">Selecione as Famílias de SKU que exigem um aumento.</span><span class="sxs-lookup"><span data-stu-id="ceab9-113">Select the SKU Families that require an increase.</span></span>

    ![Série de SKU selecionada](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="ceab9-115">Insira os novos limites desejados na assinatura.</span><span class="sxs-lookup"><span data-stu-id="ceab9-115">Enter the new limits you would like on the subscription.</span></span>

    ![Nova solicitação de cota do SKU](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="ceab9-117">Para remover uma linha, desmarque o SKU no menu suspenso de família de SKU ou clique no ícone "x" de descarte.</span><span class="sxs-lookup"><span data-stu-id="ceab9-117">To remove a line, uncheck the SKU from the SKU family dropdown or click the discard "x" icon.</span></span>
<span data-ttu-id="ceab9-118">Depois de inserir a cota desejada para cada família de SKU, clique em "Avançar" na página Etapa do problema para continuar com a criação da solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="ceab9-118">After entering the desired quota for each SKU family, click "Next" on the Problem step page to continue with the support request creation.</span></span>
