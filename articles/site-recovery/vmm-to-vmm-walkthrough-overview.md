---
title: "aaaReplicate VMs Hyper-V tooa site VMM secundário com o Azure Site Recovery | Microsoft Docs"
description: "Fornece uma visão geral para replicar máquinas virtuais do Hyper-V tooa site VMM secundário usando Olá portal do Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a><span data-ttu-id="23b17-103">Replicar máquinas virtuais Hyper-V no site tooa VMM secundário nuvens do VMM</span><span class="sxs-lookup"><span data-stu-id="23b17-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="23b17-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="23b17-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="23b17-105">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="23b17-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="23b17-106">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="23b17-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="23b17-107">Este artigo fornece uma visão geral das etapas necessárias tooreplicate máquinas de virtuais de Hyper-V (VMs) gerenciadas em nuvens do System Center Virtual Machine Manager (VMM), local de VMM secundário tooa, locais de saudação usando [Azure Site Recovery](site-recovery-overview.md)em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="23b17-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span>

<span data-ttu-id="23b17-108">Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="23b17-108">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="23b17-109">Etapa 1: Analisar a arquitetura de cenário Olá</span><span class="sxs-lookup"><span data-stu-id="23b17-109">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="23b17-110">Antes de iniciar a implantação, examine a arquitetura de cenário hello e certifique-se de que você compreenda todos os componentes de saudação precisar toodeploy.</span><span class="sxs-lookup"><span data-stu-id="23b17-110">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="23b17-111">Vá muito[etapa 1: revisar arquitetura Olá](vmm-to-vmm-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="23b17-111">Go too[Step 1: Review hello architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="23b17-112">Etapa 2: Analisar os pré-requisitos e as limitações</span><span class="sxs-lookup"><span data-stu-id="23b17-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="23b17-113">Certifique-se de que você compreenda os pré-requisitos de implantação hello e limitações.</span><span class="sxs-lookup"><span data-stu-id="23b17-113">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="23b17-114">**Pré-requisitos do Azure**: você precisa de uma assinatura Microsoft Azure e serviços de recuperação do Azure cofre, tooorchestrate e gerenciar a replicação.</span><span class="sxs-lookup"><span data-stu-id="23b17-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, tooorchestrate and manage replication.</span></span>
<span data-ttu-id="23b17-115">**Servidores do VMM no local e os hosts do Hyper-V**: verifique se os servidores VMM e os hosts do Hyper-V são compatíveis e se estão preparados para a implantação do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="23b17-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="23b17-116">Vá muito[etapa 2: verificar os pré-requisitos e limitações](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="23b17-116">Go too[Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="23b17-117">Etapa 3: Planejar a rede</span><span class="sxs-lookup"><span data-stu-id="23b17-117">Step 3: Plan networking</span></span>

<span data-ttu-id="23b17-118">É necessário toodo alguns tooensure que você pode configurar o mapeamento de rede entre redes de VM do VMM quando você implanta o cenário de saudação de planejamento da rede.</span><span class="sxs-lookup"><span data-stu-id="23b17-118">You need toodo some network planning tooensure that you can configure network mapping between VMM VM networks when you deploy hello scenario.</span></span>

<span data-ttu-id="23b17-119">Vá muito[etapa 3: planejar a rede](vmm-to-vmm-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="23b17-119">Go too[Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="23b17-120">Etapa 4: Preparar o VMM e o Hyper-V</span><span class="sxs-lookup"><span data-stu-id="23b17-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="23b17-121">Prepare servidores VMM hello e hosts Hyper-V para implantação da recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="23b17-121">Prepare hello VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="23b17-122">Vá muito[etapa 4: preparar servidores locais](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="23b17-122">Go too[Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="23b17-123">Etapa 5: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="23b17-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="23b17-124">Configurar um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="23b17-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="23b17-125">cofre Olá contém definições de configuração e coordena a replicação.</span><span class="sxs-lookup"><span data-stu-id="23b17-125">hello vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="23b17-126">[Etapa 5: Configurar um cofre](vmm-to-vmm-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="23b17-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="23b17-127">Etapa 6: Definir as configurações de origem e de destino</span><span class="sxs-lookup"><span data-stu-id="23b17-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="23b17-128">Configure locais de VMM de replicação de origem e destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="23b17-128">Set up hello source and target replication VMM locations.</span></span> <span data-ttu-id="23b17-129">Adicionar o cofre do hello VMM servidores toohello e baixar arquivos de instalação Olá para componentes do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="23b17-129">Add hello VMM servers toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="23b17-130">Execute a instalação do provedor Azure Site Recovery no servidor do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="23b17-130">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="23b17-131">A instalação instala Olá provedor no servidor do VMM hello e registra o servidor de saudação no cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="23b17-131">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="23b17-132">Instale o agente de serviços de recuperação do Microsoft hello em cada host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="23b17-132">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="23b17-133">Vá muito[etapa 6: definir configurações de origem e destino Olá](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="23b17-133">Go too[Step 6: Set up hello source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="23b17-134">Etapa 7: configurar o mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="23b17-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="23b17-135">Mapear redes de VM do VMM nos locais de origem e destino hello.</span><span class="sxs-lookup"><span data-stu-id="23b17-135">Map VMM VM networks in hello source and target locations.</span></span> <span data-ttu-id="23b17-136">Após o failover, máquinas virtuais são criadas na rede de destino Olá essa rede VM de origem do maps toohello em qual Olá VM do Hyper-V de origem está localizado.</span><span class="sxs-lookup"><span data-stu-id="23b17-136">After failover, VMs are created in hello target network that maps toohello source VM network in which hello source Hyper-V VM is located.</span></span>

<span data-ttu-id="23b17-137">Vá muito[etapa 7: Configurar mapeamento de rede](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="23b17-137">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="23b17-138">Etapa 8: Configurar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="23b17-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="23b17-139">Especifica como as VMs serão replicadas entre os locais do VMM.</span><span class="sxs-lookup"><span data-stu-id="23b17-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="23b17-140">Vá muito[etapa 8: configurar uma política de replicação](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="23b17-140">Go too[Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="23b17-141">Etapa 9: Habilitar a replicação para VMs</span><span class="sxs-lookup"><span data-stu-id="23b17-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="23b17-142">Selecione VMs Olá deseja tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="23b17-142">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="23b17-143">Habilitar uma VM para o site secundário do toohello de replicação inicial de saudação do replicação gatilhos, seguido por replicação delta em andamento.</span><span class="sxs-lookup"><span data-stu-id="23b17-143">Enabling a VM for replication triggers hello initial replication toohello secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="23b17-144">Vá muito[etapa 9: habilitar replicação](vmm-to-vmm-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="23b17-144">Go too[Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="23b17-145">Etapa 10: Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="23b17-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="23b17-146">Execute um toomake de failover de teste se que tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="23b17-146">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="23b17-147">Vá muito[etapa 10: executar um failover de teste](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="23b17-147">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
