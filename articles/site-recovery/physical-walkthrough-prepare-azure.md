---
title: "aaaPrepare recursos do Azure tooreplicate tooAzure servidores físicos usando o Azure Site Recovery local | Microsoft Docs"
description: "Descreve o que você precisa em vigor no Azure antes de iniciar a replicação tooAzure de servidores locais, usando o serviço do Azure Site Recovery Olá"
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
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b1d008dac278bc7797188a3c9c15f2a3b5fe12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a><span data-ttu-id="dc82d-103">Etapa 5: Preparar recursos do Azure para tooAzure de replicação de servidor físico</span><span class="sxs-lookup"><span data-stu-id="dc82d-103">Step 5: Prepare Azure resources for physical server replication tooAzure</span></span>


<span data-ttu-id="dc82d-104">Use instruções Olá tooprepare este artigo Azure recursos para que você pode replicar tooAzure de servidores no local usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="dc82d-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="dc82d-105">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="dc82d-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="dc82d-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="dc82d-106">Before you start</span></span>

<span data-ttu-id="dc82d-107">Verifique se você leu Olá [pré-requisitos](physical-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="dc82d-107">Make sure you've read hello [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="dc82d-108">Configurar uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="dc82d-108">Set up an Azure account</span></span>

- <span data-ttu-id="dc82d-109">Obter uma [conta do Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="dc82d-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="dc82d-110">Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc82d-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="dc82d-111">Verificar regiões Olá com suporte para a recuperação de Site, em **disponibilidade geográfica** na [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="dc82d-111">Check hello supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="dc82d-112">Saiba mais sobre [preços de recuperação de Site](site-recovery-faq.md#pricing)e obter Olá [detalhes de preços](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="dc82d-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="dc82d-113">Configurar uma rede do Azure</span><span class="sxs-lookup"><span data-stu-id="dc82d-113">Set up an Azure network</span></span>

- <span data-ttu-id="dc82d-114">Configure uma rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc82d-114">Set up an Azure network.</span></span> <span data-ttu-id="dc82d-115">As VMs do Azure são colocadas nessa rede quando são criadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="dc82d-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="dc82d-116">Recuperação de site no portal do Azure de saudação pode usar redes configuradas no [Gerenciador de recursos](../resource-manager-deployment-model.md), ou no modo clássico.</span><span class="sxs-lookup"><span data-stu-id="dc82d-116">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="dc82d-117">rede Olá deve estar no hello Cofre de serviços de recuperação com a mesma região hello.</span><span class="sxs-lookup"><span data-stu-id="dc82d-117">hello network should be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="dc82d-118">Saiba mais sobre os [preços de rede virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="dc82d-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="dc82d-119">Saiba mais sobre a [Conectividade de VM do Azure](physical-walkthrough-network.md) após o failover.</span><span class="sxs-lookup"><span data-stu-id="dc82d-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="dc82d-120">Configure uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="dc82d-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="dc82d-121">Recuperação de site replica armazenamento tooAzure dos servidores no local.</span><span class="sxs-lookup"><span data-stu-id="dc82d-121">Site Recovery replicates on-premises servers tooAzure storage.</span></span> <span data-ttu-id="dc82d-122">Máquinas virtuais do Azure são criados a partir do armazenamento Olá após o failover.</span><span class="sxs-lookup"><span data-stu-id="dc82d-122">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="dc82d-123">[Configure uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) para os dados replicados.</span><span class="sxs-lookup"><span data-stu-id="dc82d-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="dc82d-124">Recuperação de site no portal do Azure de saudação pode usar contas de armazenamento configuradas no Gerenciador de recursos ou em modo clássico.</span><span class="sxs-lookup"><span data-stu-id="dc82d-124">Site Recovery in hello Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="dc82d-125">conta de armazenamento Olá pode ser padrão ou [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="dc82d-125">hello storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="dc82d-126">Se você configurar uma conta premium, também precisará de uma conta padrão adicional para dados de log.</span><span class="sxs-lookup"><span data-stu-id="dc82d-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dc82d-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc82d-127">Next steps</span></span>

<span data-ttu-id="dc82d-128">Vá muito[etapa 6: configurar um cofre](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="dc82d-128">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>
