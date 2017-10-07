---
title: "aaaHow dá a replicação de máquina virtual do Azure entre regiões do Azure trabalho no Azure Site Recovery?  | Microsoft Docs"
description: "Este artigo fornece uma visão geral dos componentes e arquitetura usada ao replicar máquinas virtuais do Azure entre regiões do Azure usando o serviço do Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="76f8d-104">Como funciona a replicação de VM do Azure no Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="76f8d-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="76f8d-105">Este artigo descreve Olá componentes e processos envolvidos na replicação e recuperação de máquinas virtuais (VMs) do Azure de uma região tooanother usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="76f8d-105">This article describes hello components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region tooanother by using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="76f8d-106">Replicação de VM do Azure com o serviço de recuperação de Site do hello está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="76f8d-106">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="76f8d-107">Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="76f8d-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="76f8d-108">Componentes de arquitetura</span><span class="sxs-lookup"><span data-stu-id="76f8d-108">Architectural components</span></span>

<span data-ttu-id="76f8d-109">Olá diagrama a seguir fornece uma visão geral de um ambiente de VM do Azure em uma região específica (no exemplo, Olá local do Leste dos EUA).</span><span class="sxs-lookup"><span data-stu-id="76f8d-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="76f8d-110">Em um ambiente de VM do Azure:</span><span class="sxs-lookup"><span data-stu-id="76f8d-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="76f8d-111">Os aplicativos podem ser executados em VMs com discos distribuídos em contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="76f8d-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="76f8d-112">Olá VMs pode ser incluído em uma ou mais sub-redes em uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="76f8d-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![ambiente do cliente](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="76f8d-114">Saiba mais sobre os pré-requisitos de implantação hello e os requisitos em Olá [matriz de suporte](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="76f8d-114">Learn about hello deployment prerequisites and requirements in hello [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="76f8d-115">Processo de replicação</span><span class="sxs-lookup"><span data-stu-id="76f8d-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="76f8d-116">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="76f8d-116">Step 1</span></span>

<span data-ttu-id="76f8d-117">Quando você habilitar a replicação de VM do Azure no portal do Azure de saudação, Olá recursos mostrados em Olá seguinte diagrama e tabela são criados automaticamente na região de destino hello.</span><span class="sxs-lookup"><span data-stu-id="76f8d-117">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="76f8d-118">Por padrão, os recursos são criados com base nas configurações da região de origem.</span><span class="sxs-lookup"><span data-stu-id="76f8d-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="76f8d-119">Você pode personalizar as configurações de destino de saudação conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="76f8d-119">You can customize hello target settings as required.</span></span> <span data-ttu-id="76f8d-120">[Saiba mais](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="76f8d-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Habilitar o processo de replicação, etapa 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="76f8d-122">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="76f8d-122">**Resource**</span></span> | <span data-ttu-id="76f8d-123">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="76f8d-123">**Details**</span></span>
--- | ---
<span data-ttu-id="76f8d-124">**Grupo de recursos de destino**</span><span class="sxs-lookup"><span data-stu-id="76f8d-124">**Target resource group**</span></span> | <span data-ttu-id="76f8d-125">Olá toowhich do grupo de recursos pertencem VMs replicadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="76f8d-125">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="76f8d-126">**Rede virtual de destino**</span><span class="sxs-lookup"><span data-stu-id="76f8d-126">**Target virtual network**</span></span> | <span data-ttu-id="76f8d-127">rede virtual de saudação em que VMs replicadas estão localizadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="76f8d-127">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="76f8d-128">Um mapeamento de rede é criado entre redes virtuais de origem e de destino e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="76f8d-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="76f8d-129">**Contas de armazenamento de cache**</span><span class="sxs-lookup"><span data-stu-id="76f8d-129">**Cache storage accounts**</span></span> | <span data-ttu-id="76f8d-130">Antes das alterações na fonte que VMs são replicadas toohello conta de armazenamento de destino, eles são controlados e enviados toohello conta de armazenamento de cache no local de destino hello.</span><span class="sxs-lookup"><span data-stu-id="76f8d-130">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="76f8d-131">Isso garante um impacto mínimo sobre aplicativos de produção em execução em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="76f8d-131">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="76f8d-132">**Contas de armazenamento de destino**</span><span class="sxs-lookup"><span data-stu-id="76f8d-132">**Target storage accounts**</span></span>  | <span data-ttu-id="76f8d-133">Contas de armazenamento em dados de Olá Olá destino local toowhich é replicada.</span><span class="sxs-lookup"><span data-stu-id="76f8d-133">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="76f8d-134">**Conjuntos de disponibilidade de destino**</span><span class="sxs-lookup"><span data-stu-id="76f8d-134">**Target availability sets**</span></span>  | <span data-ttu-id="76f8d-135">Conjuntos de disponibilidade no qual Olá replicada VMs estão localizadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="76f8d-135">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="76f8d-136">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="76f8d-136">Step 2</span></span>

<span data-ttu-id="76f8d-137">Como a replicação estiver habilitada, Olá serviço de mobilidade de extensão de recuperação de Site é instalado automaticamente nos Olá VM.</span><span class="sxs-lookup"><span data-stu-id="76f8d-137">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="76f8d-138">a seguir Olá ocorre:</span><span class="sxs-lookup"><span data-stu-id="76f8d-138">hello following occurs:</span></span>

1. <span data-ttu-id="76f8d-139">Olá VM está registrado com o Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="76f8d-139">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="76f8d-140">A replicação contínua está configurada para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="76f8d-140">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="76f8d-141">Grava dados em Olá VM discos estão continuamente transferidos toohello conta de armazenamento de cache no local de origem hello.</span><span class="sxs-lookup"><span data-stu-id="76f8d-141">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Habilitar o processo de replicação, etapa 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="76f8d-143">Recuperação de site nunca precisa de conectividade de entrada toohello VM.</span><span class="sxs-lookup"><span data-stu-id="76f8d-143">Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="76f8d-144">Olá VM precisa apenas conectividade de saída tooSite recuperação URLs/endereços IP, endereços IP/URLs de autenticação do Office 365 e endereços IP de conta de armazenamento de cache.</span><span class="sxs-lookup"><span data-stu-id="76f8d-144">hello VM needs only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="76f8d-145">Para obter mais informações, consulte Olá [diretrizes de rede para replicar máquinas virtuais do Azure](site-recovery-azure-to-azure-networking-guidance.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="76f8d-145">For more information, see hello [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="76f8d-146">Processo de replicação contínua</span><span class="sxs-lookup"><span data-stu-id="76f8d-146">Continuous replication process</span></span>

<span data-ttu-id="76f8d-147">Depois que a replicação contínua está funcionando, o disco gravações são imediatamente transferidos toohello conta de armazenamento de cache.</span><span class="sxs-lookup"><span data-stu-id="76f8d-147">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="76f8d-148">Recuperação de site processa dados saudação e envia toohello conta de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="76f8d-148">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="76f8d-149">Após o processamento de dados de saudação, pontos de recuperação são gerados na conta de armazenamento de destino Olá intervalos de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="76f8d-149">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="76f8d-150">Processo de failover</span><span class="sxs-lookup"><span data-stu-id="76f8d-150">Failover process</span></span>

<span data-ttu-id="76f8d-151">Quando você iniciar um failover, Olá que máquinas virtuais são criadas no grupo de recursos de destino hello, a rede virtual de destino, a sub-rede de destino e hello destino conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="76f8d-151">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="76f8d-152">Durante um failover, você pode usar qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="76f8d-152">During a failover, you can use any recovery point.</span></span>

![Processo de failover](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="76f8d-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="76f8d-154">Next steps</span></span>

- <span data-ttu-id="76f8d-155">Saiba mais sobre a [rede](site-recovery-azure-to-azure-networking-guidance.md) para a replicação de VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="76f8d-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="76f8d-156">Execute um passo a passo muito[replicar máquinas virtuais do Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="76f8d-156">Follow a walkthrough too[replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
