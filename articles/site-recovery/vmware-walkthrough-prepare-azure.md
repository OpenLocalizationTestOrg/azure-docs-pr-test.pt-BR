---
title: aaaPrepare recursos do Azure tooreplicate tooAzure VMs VMware usando o Azure Site Recovery local | Microsoft Docs
description: "Descreve o que você precisa em vigor no Azure antes de você inicia a replicação local VMs VMware tooAzure usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ac72fff0593783add789408ecfeb1812d70108b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-tooazure"></a><span data-ttu-id="2c078-103">Etapa 5: Preparar recursos do Azure para VMWare tooAzure de replicação</span><span class="sxs-lookup"><span data-stu-id="2c078-103">Step 5: Prepare Azure resources for VMWare replication tooAzure</span></span>


<span data-ttu-id="2c078-104">Use instruções Olá tooprepare este artigo Azure recursos para que você pode replicar tooAzure de máquinas locais usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="2c078-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises machines tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="2c078-105">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2c078-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="2c078-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="2c078-106">Before you start</span></span>

<span data-ttu-id="2c078-107">Verifique se você leu Olá [pré-requisitos](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="2c078-107">Make sure you've read hello [prerequisites](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="2c078-108">Configurar uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="2c078-108">Set up an Azure account</span></span>

- <span data-ttu-id="2c078-109">Obter uma [conta do Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="2c078-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="2c078-110">Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2c078-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="2c078-111">Verificar regiões Olá com suporte para a recuperação de Site, em disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="2c078-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="2c078-112">Saiba mais sobre [preços de recuperação de Site](site-recovery-faq.md#pricing)e obter Olá [detalhes de preços](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="2c078-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="2c078-113">Configurar uma rede do Azure</span><span class="sxs-lookup"><span data-stu-id="2c078-113">Set up an Azure network</span></span>

- <span data-ttu-id="2c078-114">Configure uma rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c078-114">Set up an Azure network.</span></span> <span data-ttu-id="2c078-115">As VMs do Azure são colocadas nessa rede quando são criadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="2c078-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="2c078-116">Recuperação de site no portal do Azure de saudação pode usar redes configuradas no [Gerenciador de recursos](../resource-manager-deployment-model.md), ou no modo clássico.</span><span class="sxs-lookup"><span data-stu-id="2c078-116">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="2c078-117">rede Olá deve estar no hello Cofre de serviços de recuperação com a mesma região Olá</span><span class="sxs-lookup"><span data-stu-id="2c078-117">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="2c078-118">Saiba mais sobre os [preços de rede virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="2c078-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="2c078-119">Saiba mais sobre a [Conectividade de VM do Azure](site-recovery-network-design.md) após o failover.</span><span class="sxs-lookup"><span data-stu-id="2c078-119">Learn more about [Azure VM connectivity](site-recovery-network-design.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="2c078-120">Configure uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2c078-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="2c078-121">Recuperação de site replica o armazenamento de tooAzure máquinas locais.</span><span class="sxs-lookup"><span data-stu-id="2c078-121">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="2c078-122">Máquinas virtuais do Azure são criados a partir do armazenamento Olá após o failover.</span><span class="sxs-lookup"><span data-stu-id="2c078-122">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="2c078-123">[Configure uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) para os dados replicados.</span><span class="sxs-lookup"><span data-stu-id="2c078-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="2c078-124">Recuperação de site no portal do Azure de saudação pode usar contas de armazenamento configuradas no Gerenciador de recursos ou em modo clássico.</span><span class="sxs-lookup"><span data-stu-id="2c078-124">Site Recovery in hello Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="2c078-125">conta de armazenamento Olá pode ser padrão ou [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="2c078-125">hello storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="2c078-126">Se você configurar uma conta premium, também precisará de uma conta padrão adicional para dados de log.</span><span class="sxs-lookup"><span data-stu-id="2c078-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2c078-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c078-127">Next steps</span></span>

<span data-ttu-id="2c078-128">Vá muito[etapa 6: recursos do VMware preparar](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="2c078-128">Go too[Step 6: Prepare VMware resources](vmware-walkthrough-prepare-vmware.md)</span></span>
