---
title: "Como funciona a replicação de máquina virtual do Azure entre regiões do Azure no Azure Site Recovery?  | Microsoft Docs"
description: "Este artigo fornece uma visão geral dos componentes e da arquitetura usados ao replicar VMs do Azure entre regiões do Azure com o serviço Azure Site Recovery."
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
ms.openlocfilehash: ec397eaeda963f257d1bd996f1f57189bcde17ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="98417-104">Como funciona a replicação de VM do Azure no Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="98417-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="98417-105">Este artigo descreve os componentes e os processos envolvidos na replicação e recuperação de VMs (máquinas virtuais) do Azure de uma região para outra usando o serviço [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98417-105">This article describes the components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region to another by using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="98417-106">Atualmente, a replicação de VM do Azure com o serviço Site Recovery está em versão prévia.</span><span class="sxs-lookup"><span data-stu-id="98417-106">Azure VM replication with the Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="98417-107">Publique eventuais comentários no final deste artigo ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="98417-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="98417-108">Componentes de arquitetura</span><span class="sxs-lookup"><span data-stu-id="98417-108">Architectural components</span></span>

<span data-ttu-id="98417-109">O diagrama a seguir fornece uma exibição de alto nível de um ambiente de VM do Azure em uma região específica (neste exemplo, a localização Leste dos EUA).</span><span class="sxs-lookup"><span data-stu-id="98417-109">The following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, the East US location).</span></span> <span data-ttu-id="98417-110">Em um ambiente de VM do Azure:</span><span class="sxs-lookup"><span data-stu-id="98417-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="98417-111">Os aplicativos podem ser executados em VMs com discos distribuídos em contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="98417-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="98417-112">As VMs podem ser incluídas em uma ou mais sub-redes de uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="98417-112">The VMs can be included in one or more subnets within a virtual network.</span></span>

![customer-environment](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="98417-114">Saiba mais sobre os pré-requisitos e requisitos de implantação na [matriz de suporte](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="98417-114">Learn about the deployment prerequisites and requirements in the [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="98417-115">Processo de replicação</span><span class="sxs-lookup"><span data-stu-id="98417-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="98417-116">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="98417-116">Step 1</span></span>

<span data-ttu-id="98417-117">Quando você habilita a replicação de VM do Azure no portal do Azure, os recursos mostrados na tabela e no diagrama a seguir são criados automaticamente na região de destino.</span><span class="sxs-lookup"><span data-stu-id="98417-117">When you enable Azure VM replication in the Azure portal, the resources shown in the following diagram and table are automatically created in the target region.</span></span> <span data-ttu-id="98417-118">Por padrão, os recursos são criados com base nas configurações da região de origem.</span><span class="sxs-lookup"><span data-stu-id="98417-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="98417-119">Você pode personalizar as configurações de destino, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="98417-119">You can customize the target settings as required.</span></span> <span data-ttu-id="98417-120">[Saiba mais](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="98417-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Habilitar o processo de replicação, etapa 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="98417-122">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="98417-122">**Resource**</span></span> | <span data-ttu-id="98417-123">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="98417-123">**Details**</span></span>
--- | ---
<span data-ttu-id="98417-124">**Grupo de recursos de destino**</span><span class="sxs-lookup"><span data-stu-id="98417-124">**Target resource group**</span></span> | <span data-ttu-id="98417-125">O grupo de recursos ao qual as VMs replicadas pertencem após o failover.</span><span class="sxs-lookup"><span data-stu-id="98417-125">The resource group to which replicated VMs belong after failover.</span></span>
<span data-ttu-id="98417-126">**Rede virtual de destino**</span><span class="sxs-lookup"><span data-stu-id="98417-126">**Target virtual network**</span></span> | <span data-ttu-id="98417-127">A rede virtual na qual as VMs replicadas estão localizadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="98417-127">The virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="98417-128">Um mapeamento de rede é criado entre redes virtuais de origem e de destino e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="98417-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="98417-129">**Contas de armazenamento de cache**</span><span class="sxs-lookup"><span data-stu-id="98417-129">**Cache storage accounts**</span></span> | <span data-ttu-id="98417-130">Antes que as alterações nas VMs de origem sejam replicadas para a conta de armazenamento de destino, elas são acompanhadas e enviadas para a conta de armazenamento de cache no local de destino.</span><span class="sxs-lookup"><span data-stu-id="98417-130">Before changes on source VMs are replicated to the target storage account, they are tracked and sent to the cache storage account in the target location.</span></span> <span data-ttu-id="98417-131">Isso garante um impacto mínimo sobre os aplicativos de produção em execução na VM.</span><span class="sxs-lookup"><span data-stu-id="98417-131">This ensures minimal impact on production apps running on the VM.</span></span>
<span data-ttu-id="98417-132">**Contas de armazenamento de destino**</span><span class="sxs-lookup"><span data-stu-id="98417-132">**Target storage accounts**</span></span>  | <span data-ttu-id="98417-133">Contas de armazenamento no local de destino para as quais os dados são replicados.</span><span class="sxs-lookup"><span data-stu-id="98417-133">Storage accounts in the target location to which the data is replicated.</span></span>
<span data-ttu-id="98417-134">**Conjuntos de disponibilidade de destino**</span><span class="sxs-lookup"><span data-stu-id="98417-134">**Target availability sets**</span></span>  | <span data-ttu-id="98417-135">Conjuntos de disponibilidade nos quais as VMs replicadas estão localizadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="98417-135">Availability sets in which the replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="98417-136">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="98417-136">Step 2</span></span>

<span data-ttu-id="98417-137">Conforme a replicação é habilitada, a extensão Serviço de mobilidade do Site Recovery é automaticamente instalada na VM.</span><span class="sxs-lookup"><span data-stu-id="98417-137">As replication is enabled, the Site Recovery extension Mobility service is automatically installed on the VM.</span></span> <span data-ttu-id="98417-138">Ocorre o seguinte:</span><span class="sxs-lookup"><span data-stu-id="98417-138">The following occurs:</span></span>

1. <span data-ttu-id="98417-139">A VM é registrada no Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="98417-139">The VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="98417-140">A replicação contínua é configurada na VM.</span><span class="sxs-lookup"><span data-stu-id="98417-140">Continuous replication is configured for the VM.</span></span> <span data-ttu-id="98417-141">As gravações de dados nos discos de VM são continuamente transferidas para a conta de armazenamento de cache no local de origem.</span><span class="sxs-lookup"><span data-stu-id="98417-141">Data writes on the VM disks are continuously transferred to the cache storage account in the source location.</span></span>

   ![Habilitar o processo de replicação, etapa 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="98417-143">O Site Recovery nunca precisa de conectividade de entrada à VM.</span><span class="sxs-lookup"><span data-stu-id="98417-143">Site Recovery never needs inbound connectivity to the VM.</span></span> <span data-ttu-id="98417-144">A VM precisa apenas de conectividade de saída aos endereços IP/URLs do serviço Site Recovery, endereços IP/URLs de autenticação do Office 365 e endereços IP da conta de armazenamento de cache.</span><span class="sxs-lookup"><span data-stu-id="98417-144">The VM needs only outbound connectivity to Site Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="98417-145">Para obter mais informações, consulte o artigo [Diretrizes de rede para replicação de máquinas virtuais do Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="98417-145">For more information, see the [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="98417-146">Processo de replicação contínua</span><span class="sxs-lookup"><span data-stu-id="98417-146">Continuous replication process</span></span>

<span data-ttu-id="98417-147">Depois que a replicação contínua estiver funcionando, as gravações de disco serão transferidas imediatamente para a conta de armazenamento de cache.</span><span class="sxs-lookup"><span data-stu-id="98417-147">After continuous replication is working, disk writes are immediately transferred to the cache storage account.</span></span> <span data-ttu-id="98417-148">O Site Recovery processa os dados e envia-os para a conta de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="98417-148">Site Recovery processes the data and sends it to the target storage account.</span></span> <span data-ttu-id="98417-149">Depois que os dados são processados, pontos de recuperação são gerados na conta de armazenamento de destino em intervalos de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="98417-149">After the data is processed, recovery points are generated in the target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="98417-150">Processo de failover</span><span class="sxs-lookup"><span data-stu-id="98417-150">Failover process</span></span>

<span data-ttu-id="98417-151">Quando você inicia um failover, as VMs são criadas no grupo de recursos de destino, na rede virtual de destino, na sub-rede de destino e no conjunto de disponibilidade de destino.</span><span class="sxs-lookup"><span data-stu-id="98417-151">When you initiate a failover, the VMs are created in the target resource group, target virtual network, target subnet, and the target availability set.</span></span> <span data-ttu-id="98417-152">Durante um failover, você pode usar qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="98417-152">During a failover, you can use any recovery point.</span></span>

![Processo de failover](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="98417-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="98417-154">Next steps</span></span>

- <span data-ttu-id="98417-155">Saiba mais sobre a [rede](site-recovery-azure-to-azure-networking-guidance.md) para a replicação de VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="98417-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="98417-156">Siga um passo a passo para [replicar VMs do Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="98417-156">Follow a walkthrough to [replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
