---
title: aaaPrepare recursos do Azure tooreplicate VMs Hyper-V (com o System Center VMM) tooAzure usando o Azure Site Recovery | Microsoft Docs
description: "Descreve o que você precisa em vigor no Azure antes de você iniciar a replicação tooAzure de VMs Hyper-V (com o VMM), usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1568bdc3-e767-477b-b040-f13699ab5644
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 86bfbab7722fe5bd5b93b92e398d1d441505d3b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="78e4b-103">Etapa 5: Preparar recursos do Azure para tooAzure de replicação (com o VMM) do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="78e4b-103">Step 5: Prepare Azure resources for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="78e4b-104">Depois de verificar [requisitos de rede](vmm-to-azure-walkthrough-network.md), use instruções Olá tooprepare este artigo Azure recursos para que você pode replicar máquinas virtuais de Hyper-V local no System Center Virtual Machine Manager (VMM) nuvens tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="78e4b-104">After verifying [network requirements](vmm-to-azure-walkthrough-network.md), use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="78e4b-105">Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="78e4b-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-an-azure-account"></a><span data-ttu-id="78e4b-106">Configurar uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="78e4b-106">Set up an Azure account</span></span>

- <span data-ttu-id="78e4b-107">Obter uma [conta do Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="78e4b-107">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="78e4b-108">Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78e4b-108">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="78e4b-109">Verificar regiões Olá com suporte para a recuperação de Site, em disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="78e4b-109">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="78e4b-110">Saiba mais sobre [preços de recuperação de Site](site-recovery-faq.md#pricing)e obter Olá [detalhes de preços](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="78e4b-110">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="78e4b-111">Verifique se sua conta do Azure tem Olá correto [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="78e4b-111">Make sure your Azure account has hello correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure VMs.</span></span> <span data-ttu-id="78e4b-112">[Saiba mais](../active-directory/role-based-access-built-in-roles.md) sobre o controle de acesso baseado em função do Azure.</span><span class="sxs-lookup"><span data-stu-id="78e4b-112">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="78e4b-113">Configurar uma rede do Azure</span><span class="sxs-lookup"><span data-stu-id="78e4b-113">Set up an Azure network</span></span>

- <span data-ttu-id="78e4b-114">Configurar uma [rede do Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="78e4b-114">Set up an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span></span> <span data-ttu-id="78e4b-115">As VMs do Azure são colocadas nessa rede quando são criadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="78e4b-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="78e4b-116">rede Olá deve estar no hello Cofre de serviços de recuperação com a mesma região Olá</span><span class="sxs-lookup"><span data-stu-id="78e4b-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="78e4b-117">Recuperação de site no portal do Azure de saudação pode usar redes configuradas no [Gerenciador de recursos](../resource-manager-deployment-model.md), ou no modo clássico.</span><span class="sxs-lookup"><span data-stu-id="78e4b-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="78e4b-118">É recomendável configurar uma rede antes de começar.</span><span class="sxs-lookup"><span data-stu-id="78e4b-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="78e4b-119">Se você não fizer isso, você precisa toodo-lo durante a implantação da recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="78e4b-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="78e4b-120">Saiba mais sobre os [preços de rede virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="78e4b-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="78e4b-121">Configure uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="78e4b-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="78e4b-122">Recuperação de site replica o armazenamento de tooAzure máquinas locais.</span><span class="sxs-lookup"><span data-stu-id="78e4b-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="78e4b-123">Máquinas virtuais do Azure são criados a partir do armazenamento Olá após o failover.</span><span class="sxs-lookup"><span data-stu-id="78e4b-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="78e4b-124">Configurar um padrão/premium [conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold dados replicados tooAzure.</span><span class="sxs-lookup"><span data-stu-id="78e4b-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="78e4b-125">[Armazenamento Premium](../storage/common/storage-premium-storage.md) é normalmente usado para máquinas virtuais que precisam de um desempenho de e/s consistentemente alto e baixa latência toohost e/s intensivas cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="78e4b-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="78e4b-126">Se você quiser toouse dados replicados de um toostore de conta premium, você também precisa de um armazenamento padrão toostore replicação logs de conta de captura contínua altera dados tooon locais.</span><span class="sxs-lookup"><span data-stu-id="78e4b-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="78e4b-127">Dependendo do modelo de recurso Olá desejar toouse para o failover de máquinas virtuais do Azure, você configurar uma conta no [Gerenciador de recursos de modo](../storage/common/storage-create-storage-account.md), ou [modo clássico](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="78e4b-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="78e4b-128">É recomendável que você configure uma conta de armazenamento antes de começar.</span><span class="sxs-lookup"><span data-stu-id="78e4b-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="78e4b-129">Se você não é necessário toodo-lo durante a implantação da recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="78e4b-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="78e4b-130">Olá devem estar no hello Cofre de serviços de recuperação com a mesma região hello.</span><span class="sxs-lookup"><span data-stu-id="78e4b-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="78e4b-131">Não é possível mover contas de armazenamento usada pela recuperação de Site em grupos de recursos dentro de saudação mesma assinatura, ou em assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="78e4b-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="78e4b-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="78e4b-132">Next steps</span></span>

<span data-ttu-id="78e4b-133">Vá muito[etapa 6: preparar VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="78e4b-133">Go too[Step 6: Prepare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>
