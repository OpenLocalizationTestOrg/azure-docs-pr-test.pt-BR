---
title: "arquitetura de saudação aaaReview para replicação de máquinas virtuais do Azure entre regiões do Azure | Microsoft Docs"
description: "Este artigo fornece uma visão geral dos componentes e arquitetura usada ao replicar máquinas virtuais do Azure entre regiões do Azure usando o serviço do Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="07ca1-103">Etapa 1: Revisar arquitetura Olá para replicação de VM do Azure entre regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="07ca1-103">Step 1: Review hello architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="07ca1-104">Depois de revisar Olá [etapas de visão geral](azure-to-azure-walkthrough-overview.md) para essa implantação, leia este componentes de saudação do artigo toounderstand e processos usados quando a replicação e a recuperação de máquinas virtuais (VMs) do Azure de tooanother de uma região do Azure, usando [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="07ca1-104">After reviewing hello [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article toounderstand hello components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region tooanother, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="07ca1-105">Quando você terminar de artigo hello, você deve ter uma compreensão clara de como funciona a região de tooanother de replicação de VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="07ca1-105">When you finish hello article, you should have a clear understanding of how Azure VM replication tooanother region works.</span></span>
- <span data-ttu-id="07ca1-106">Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="07ca1-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="07ca1-107">Replicação de VM do Azure com o serviço de recuperação de Site do hello está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="07ca1-107">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="07ca1-108">Componentes de arquitetura</span><span class="sxs-lookup"><span data-stu-id="07ca1-108">Architectural components</span></span>

<span data-ttu-id="07ca1-109">Olá diagrama a seguir fornece uma visão geral de um ambiente de VM do Azure em uma região específica (no exemplo, Olá local do Leste dos EUA).</span><span class="sxs-lookup"><span data-stu-id="07ca1-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="07ca1-110">Em um ambiente de VM do Azure:</span><span class="sxs-lookup"><span data-stu-id="07ca1-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="07ca1-111">Os aplicativos podem ser executados em VMs com discos distribuídos em contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="07ca1-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="07ca1-112">Olá VMs pode ser incluído em uma ou mais sub-redes em uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="07ca1-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![ambiente do cliente](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="07ca1-114">Processo de replicação</span><span class="sxs-lookup"><span data-stu-id="07ca1-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="07ca1-115">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="07ca1-115">Step 1</span></span>

<span data-ttu-id="07ca1-116">Quando você habilitar a replicação de VM do Azure no portal do Azure de saudação, Olá recursos mostrados em Olá seguinte diagrama e tabela são criados automaticamente na região de destino hello.</span><span class="sxs-lookup"><span data-stu-id="07ca1-116">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="07ca1-117">Por padrão, os recursos são criados com base nas configurações da região de origem.</span><span class="sxs-lookup"><span data-stu-id="07ca1-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="07ca1-118">Você pode personalizar as configurações de destino de saudação conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="07ca1-118">You can customize hello target settings as required.</span></span> <span data-ttu-id="07ca1-119">[Saiba mais](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="07ca1-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Habilitar o processo de replicação, etapa 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="07ca1-121">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="07ca1-121">**Resource**</span></span> | <span data-ttu-id="07ca1-122">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="07ca1-122">**Details**</span></span>
--- | ---
<span data-ttu-id="07ca1-123">**Grupo de recursos de destino**</span><span class="sxs-lookup"><span data-stu-id="07ca1-123">**Target resource group**</span></span> | <span data-ttu-id="07ca1-124">Olá toowhich do grupo de recursos pertencem VMs replicadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="07ca1-124">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="07ca1-125">**Rede virtual de destino**</span><span class="sxs-lookup"><span data-stu-id="07ca1-125">**Target virtual network**</span></span> | <span data-ttu-id="07ca1-126">rede virtual de saudação em que VMs replicadas estão localizadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="07ca1-126">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="07ca1-127">Um mapeamento de rede é criado entre redes virtuais de origem e de destino e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="07ca1-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="07ca1-128">**Contas de armazenamento de cache**</span><span class="sxs-lookup"><span data-stu-id="07ca1-128">**Cache storage accounts**</span></span> | <span data-ttu-id="07ca1-129">Antes das alterações na fonte que VMs são replicadas toohello conta de armazenamento de destino, eles são controlados e enviados toohello conta de armazenamento de cache no local de destino hello.</span><span class="sxs-lookup"><span data-stu-id="07ca1-129">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="07ca1-130">Isso garante um impacto mínimo sobre aplicativos de produção em execução em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="07ca1-130">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="07ca1-131">**Contas de armazenamento de destino**</span><span class="sxs-lookup"><span data-stu-id="07ca1-131">**Target storage accounts**</span></span>  | <span data-ttu-id="07ca1-132">Contas de armazenamento em dados de Olá Olá destino local toowhich é replicada.</span><span class="sxs-lookup"><span data-stu-id="07ca1-132">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="07ca1-133">**Conjuntos de disponibilidade de destino**</span><span class="sxs-lookup"><span data-stu-id="07ca1-133">**Target availability sets**</span></span>  | <span data-ttu-id="07ca1-134">Conjuntos de disponibilidade no qual Olá replicada VMs estão localizadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="07ca1-134">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="07ca1-135">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="07ca1-135">Step 2</span></span>

<span data-ttu-id="07ca1-136">Como a replicação estiver habilitada, Olá serviço de mobilidade de extensão de recuperação de Site é instalado automaticamente nos Olá VM.</span><span class="sxs-lookup"><span data-stu-id="07ca1-136">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="07ca1-137">a seguir Olá ocorre:</span><span class="sxs-lookup"><span data-stu-id="07ca1-137">hello following occurs:</span></span>

1. <span data-ttu-id="07ca1-138">Olá VM está registrado com o Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="07ca1-138">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="07ca1-139">A replicação contínua está configurada para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="07ca1-139">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="07ca1-140">Grava dados em Olá VM discos estão continuamente transferidos toohello conta de armazenamento de cache no local de origem hello.</span><span class="sxs-lookup"><span data-stu-id="07ca1-140">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Habilitar o processo de replicação, etapa 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="07ca1-142">Observe que a recuperação de Site nunca precisa de conectividade toohello VM de entrada.</span><span class="sxs-lookup"><span data-stu-id="07ca1-142">Note that Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="07ca1-143">Saída somente endereços do serviço de recuperação de tooSite conectividade URLs/IP, endereços de IP/URLs de autenticação do Office 365 e endereços IP de conta de armazenamento de cache é necessária.</span><span class="sxs-lookup"><span data-stu-id="07ca1-143">Only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="07ca1-144">Processo de replicação contínua</span><span class="sxs-lookup"><span data-stu-id="07ca1-144">Continuous replication process</span></span>

<span data-ttu-id="07ca1-145">Depois que a replicação contínua está funcionando, o disco gravações são imediatamente transferidos toohello conta de armazenamento de cache.</span><span class="sxs-lookup"><span data-stu-id="07ca1-145">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="07ca1-146">Recuperação de site processa dados saudação e envia toohello conta de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="07ca1-146">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="07ca1-147">Após o processamento de dados de saudação, pontos de recuperação são gerados na conta de armazenamento de destino Olá intervalos de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="07ca1-147">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="07ca1-148">Processo de failover</span><span class="sxs-lookup"><span data-stu-id="07ca1-148">Failover process</span></span>

<span data-ttu-id="07ca1-149">Quando você iniciar um failover, Olá que máquinas virtuais são criadas no grupo de recursos de destino hello, a rede virtual de destino, a sub-rede de destino e hello destino conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="07ca1-149">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="07ca1-150">Durante um failover, você pode usar qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="07ca1-150">During a failover, you can use any recovery point.</span></span>

![Processo de failover](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="07ca1-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07ca1-152">Next steps</span></span>

<span data-ttu-id="07ca1-153">Vá muito[etapa 2: verificar os pré-requisitos e limitações](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="07ca1-153">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>
