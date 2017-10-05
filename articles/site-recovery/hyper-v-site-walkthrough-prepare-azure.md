---
title: Preparar recursos do Azure para replicar VMs do Hyper-V (sem o System Center VMM) para o Azure usando o Azure Site Recovery | Microsoft Docs
description: "Descreve o que você precisa em vigor no Azure antes de iniciar a replicação de VMs do Hyper-V (Sem VMM) para o Azure usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1a30cadaab7e053184f0be133f1da5bfddc1fd91
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-to-azure"></a><span data-ttu-id="29df6-103">Etapa 5: preparar os recursos do Azure para a replicação do Hyper-V para o Azure</span><span class="sxs-lookup"><span data-stu-id="29df6-103">Step 5: Prepare Azure resources for Hyper-V replication to Azure</span></span>

<span data-ttu-id="29df6-104">Use as instruções neste artigo para preparar recursos do Azure para que você possa replicar VMs Hyper-V locais no Azure usando o serviço [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29df6-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="29df6-105">Depois de ler este artigo, poste comentários no final ou faça perguntas técnicas no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="29df6-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="29df6-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="29df6-106">Before you start</span></span>

<span data-ttu-id="29df6-107">Não se esqueça de ler os [pré-requisitos](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="29df6-107">Make sure you've read the [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="29df6-108">Configurar uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="29df6-108">Set up an Azure account</span></span>

- <span data-ttu-id="29df6-109">Obter uma [conta do Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="29df6-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="29df6-110">Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29df6-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="29df6-111">Verifique as regiões suportadas do Site Recovery, em Disponibilidade Geográfica nos [Detalhes dos Preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="29df6-111">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="29df6-112">Saiba mais sobre os [Preços do Site Recovery](site-recovery-faq.md#pricing) e obtenha os [Detalhes de preços](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="29df6-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="29df6-113">Configurar uma rede do Azure</span><span class="sxs-lookup"><span data-stu-id="29df6-113">Set up an Azure network</span></span>

- <span data-ttu-id="29df6-114">Configure uma rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="29df6-114">Set up an Azure network.</span></span> <span data-ttu-id="29df6-115">As VMs do Azure são colocadas nessa rede quando são criadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="29df6-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="29df6-116">A rede deve estar na mesma região que o cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="29df6-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="29df6-117">O Site Recovery no portal do Azure pode usar redes configuradas no [Gerenciador de Recursos](../resource-manager-deployment-model.md), ou no modo clássico.</span><span class="sxs-lookup"><span data-stu-id="29df6-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="29df6-118">É recomendável configurar uma rede antes de começar.</span><span class="sxs-lookup"><span data-stu-id="29df6-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="29df6-119">Caso você não faça isso, será necessário fazê-lo durante a implantação da Recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="29df6-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="29df6-120">Saiba mais sobre os [preços de rede virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="29df6-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="29df6-121">Configure uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="29df6-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="29df6-122">O Site Recovery replica máquinas locais para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="29df6-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="29df6-123">As VMs do Azure são criadas a partir do armazenamento após o failover.</span><span class="sxs-lookup"><span data-stu-id="29df6-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="29df6-124">Configure uma [conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) padrão ou premium para reter os dados replicados para o Azure.</span><span class="sxs-lookup"><span data-stu-id="29df6-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="29df6-125">O [armazenamento premium](../storage/common/storage-premium-storage.md) normalmente é usado para máquinas virtuais que precisam de um desempenho de E/S consistentemente alto e baixa latência para hospedar cargas de trabalho com uso intensivo de E/S.</span><span class="sxs-lookup"><span data-stu-id="29df6-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="29df6-126">Se você desejar usar uma conta premium para armazenar dados replicados, também precisará de uma conta de armazenamento standard para armazenar os logs de replicação que capturam as alterações contínuas nos dados locais.</span><span class="sxs-lookup"><span data-stu-id="29df6-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="29df6-127">Dependendo do modelo de recurso que você deseja usar para as VMs do Azure com failover, você configurará uma conta no [modo Resource Manager](../storage/common/storage-create-storage-account.md) ou no [modo clássico](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="29df6-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="29df6-128">É recomendável que você configure uma conta de armazenamento antes de começar.</span><span class="sxs-lookup"><span data-stu-id="29df6-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="29df6-129">Caso você não faça isso, será necessário fazê-lo durante a implantação do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="29df6-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="29df6-130">As contas devem estar na mesma região que o cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="29df6-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="29df6-131">Não é possível mover contas de armazenamento usadas pelo Site Recovery entre grupos de recursos na mesma assinatura ou entre assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="29df6-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="29df6-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="29df6-132">Next steps</span></span>

<span data-ttu-id="29df6-133">Vá para a [Etapa 6: preparar recursos do Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="29df6-133">Go to [Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
