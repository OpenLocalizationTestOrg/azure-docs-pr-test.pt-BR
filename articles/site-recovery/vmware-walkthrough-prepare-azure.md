---
title: Preparar recursos do Azure para replicar as VMs VMware locais para o Azure usando o Azure Site Recovery | Microsoft Docs
description: "Descreve o que você precisa em vigor no Azure antes de iniciar a replicação de VMs VMware locais para o Azure, usando o Azure Site Recovery"
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
ms.openlocfilehash: 40abff72278c9f8d9f701023fd473fe52c17b421
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-to-azure"></a><span data-ttu-id="36013-103">Etapa 5: preparar os recursos do Azure para a replicação de VMware para o Azure</span><span class="sxs-lookup"><span data-stu-id="36013-103">Step 5: Prepare Azure resources for VMWare replication to Azure</span></span>


<span data-ttu-id="36013-104">Use as instruções neste artigo para preparar recursos do Azure para que você possa replicar as máquinas locais no Azure usando o serviço [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36013-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises machines to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="36013-105">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="36013-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="36013-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="36013-106">Before you start</span></span>

<span data-ttu-id="36013-107">Não se esqueça de ler os [pré-requisitos](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="36013-107">Make sure you've read the [prerequisites](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="36013-108">Configurar uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="36013-108">Set up an Azure account</span></span>

- <span data-ttu-id="36013-109">Obter uma [conta do Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="36013-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="36013-110">Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36013-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="36013-111">Verifique as regiões suportadas do Site Recovery, em Disponibilidade Geográfica nos [Detalhes dos Preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="36013-111">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="36013-112">Saiba mais sobre os [Preços do Site Recovery](site-recovery-faq.md#pricing) e obtenha os [Detalhes de preços](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="36013-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="36013-113">Configurar uma rede do Azure</span><span class="sxs-lookup"><span data-stu-id="36013-113">Set up an Azure network</span></span>

- <span data-ttu-id="36013-114">Configure uma rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="36013-114">Set up an Azure network.</span></span> <span data-ttu-id="36013-115">As VMs do Azure são colocadas nessa rede quando são criadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="36013-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="36013-116">O Site Recovery no portal do Azure pode usar redes configuradas no [Gerenciador de Recursos](../resource-manager-deployment-model.md), ou no modo clássico.</span><span class="sxs-lookup"><span data-stu-id="36013-116">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="36013-117">A rede deve estar na mesma região que o cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="36013-117">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="36013-118">Saiba mais sobre os [preços de rede virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="36013-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="36013-119">Saiba mais sobre a [Conectividade de VM do Azure](site-recovery-network-design.md) após o failover.</span><span class="sxs-lookup"><span data-stu-id="36013-119">Learn more about [Azure VM connectivity](site-recovery-network-design.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="36013-120">Configure uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="36013-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="36013-121">O Site Recovery replica máquinas locais para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="36013-121">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="36013-122">As VMs do Azure são criadas a partir do armazenamento após o failover.</span><span class="sxs-lookup"><span data-stu-id="36013-122">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="36013-123">[Configure uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) para os dados replicados.</span><span class="sxs-lookup"><span data-stu-id="36013-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="36013-124">O Site Recovery no portal do Azure pode usar contas de armazenamento configuradas no Gerenciador de Recursos, ou no modo clássico.</span><span class="sxs-lookup"><span data-stu-id="36013-124">Site Recovery in the Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="36013-125">A conta de armazenamento pode ser padrão ou [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="36013-125">The storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="36013-126">Se você configurar uma conta premium, também precisará de uma conta padrão adicional para dados de log.</span><span class="sxs-lookup"><span data-stu-id="36013-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="36013-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="36013-127">Next steps</span></span>

<span data-ttu-id="36013-128">Vá para a [Etapa 6: Preparar recursos de VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="36013-128">Go to [Step 6: Prepare VMware resources](vmware-walkthrough-prepare-vmware.md)</span></span>
