---
title: aaaPrepare recursos do Azure tooreplicate VMs Hyper-V (sem o System Center VMM) tooAzure usando o Azure Site Recovery | Microsoft Docs
description: "Descreve o que você precisa em vigor no Azure antes de iniciar a replicação tooAzure de VMs Hyper-V (sem VMM) usando o Azure Site Recovery"
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
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a><span data-ttu-id="7ef08-103">Etapa 5: Preparar recursos do Azure para tooAzure de replicação do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="7ef08-103">Step 5: Prepare Azure resources for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="7ef08-104">Use as instruções de saudação em tooprepare este artigo Azure recursos para que você possa replicar locais VMs Hyper-V (sem o System Center VMM) tooAzure usando Olá [Azure Site Recovery](site-recovery-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="7ef08-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="7ef08-105">Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7ef08-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="7ef08-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="7ef08-106">Before you start</span></span>

<span data-ttu-id="7ef08-107">Verifique se você leu Olá [pré-requisitos](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="7ef08-107">Make sure you've read hello [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="7ef08-108">Configurar uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="7ef08-108">Set up an Azure account</span></span>

- <span data-ttu-id="7ef08-109">Obter uma [conta do Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="7ef08-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="7ef08-110">Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ef08-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="7ef08-111">Verificar regiões Olá com suporte para a recuperação de Site, em disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="7ef08-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="7ef08-112">Saiba mais sobre [preços de recuperação de Site](site-recovery-faq.md#pricing)e obter Olá [detalhes de preços](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="7ef08-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="7ef08-113">Configurar uma rede do Azure</span><span class="sxs-lookup"><span data-stu-id="7ef08-113">Set up an Azure network</span></span>

- <span data-ttu-id="7ef08-114">Configure uma rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ef08-114">Set up an Azure network.</span></span> <span data-ttu-id="7ef08-115">As VMs do Azure são colocadas nessa rede quando são criadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="7ef08-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="7ef08-116">rede Olá deve estar no hello Cofre de serviços de recuperação com a mesma região Olá</span><span class="sxs-lookup"><span data-stu-id="7ef08-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="7ef08-117">Recuperação de site no portal do Azure de saudação pode usar redes configuradas no [Gerenciador de recursos](../resource-manager-deployment-model.md), ou no modo clássico.</span><span class="sxs-lookup"><span data-stu-id="7ef08-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="7ef08-118">É recomendável configurar uma rede antes de começar.</span><span class="sxs-lookup"><span data-stu-id="7ef08-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="7ef08-119">Se você não fizer isso, você precisa toodo-lo durante a implantação da recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="7ef08-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="7ef08-120">Saiba mais sobre os [preços de rede virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="7ef08-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="7ef08-121">Configure uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="7ef08-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="7ef08-122">Recuperação de site replica o armazenamento de tooAzure máquinas locais.</span><span class="sxs-lookup"><span data-stu-id="7ef08-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="7ef08-123">Máquinas virtuais do Azure são criados a partir do armazenamento Olá após o failover.</span><span class="sxs-lookup"><span data-stu-id="7ef08-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="7ef08-124">Configurar um padrão/premium [conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold dados replicados tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7ef08-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="7ef08-125">[Armazenamento Premium](../storage/common/storage-premium-storage.md) é normalmente usado para máquinas virtuais que precisam de um desempenho de e/s consistentemente alto e baixa latência toohost e/s intensivas cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7ef08-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="7ef08-126">Se você quiser toouse dados replicados de um toostore de conta premium, você também precisa de um armazenamento padrão toostore replicação logs de conta de captura contínua altera dados tooon locais.</span><span class="sxs-lookup"><span data-stu-id="7ef08-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="7ef08-127">Dependendo do modelo de recurso Olá desejar toouse para o failover de máquinas virtuais do Azure, você configurar uma conta no [Gerenciador de recursos de modo](../storage/common/storage-create-storage-account.md), ou [modo clássico](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="7ef08-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="7ef08-128">É recomendável que você configure uma conta de armazenamento antes de começar.</span><span class="sxs-lookup"><span data-stu-id="7ef08-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="7ef08-129">Se você não é necessário toodo-lo durante a implantação da recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="7ef08-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="7ef08-130">Olá devem estar no hello Cofre de serviços de recuperação com a mesma região hello.</span><span class="sxs-lookup"><span data-stu-id="7ef08-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="7ef08-131">Não é possível mover contas de armazenamento usada pela recuperação de Site em grupos de recursos dentro de saudação mesma assinatura, ou em assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="7ef08-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7ef08-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7ef08-132">Next steps</span></span>

<span data-ttu-id="7ef08-133">Vá muito[etapa 6: recursos do Hyper-V preparar](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="7ef08-133">Go too[Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
