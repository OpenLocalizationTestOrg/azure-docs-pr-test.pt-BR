---
title: "Replicar VMs do Hyper-V para um site secundário do VMM com o Azure Site Recovery | Microsoft Docs"
description: "Fornece uma visão geral para replicar máquinas virtuais do Hyper-V para um site secundário do VMM usando o portal do Azure."
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
ms.openlocfilehash: b422dd2cf23426de2f154a553b38509082536309
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site"></a><span data-ttu-id="74562-103">Replicar máquinas virtuais do Hyper-V em nuvens de VMM para um site de VMM secundário</span><span class="sxs-lookup"><span data-stu-id="74562-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="74562-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="74562-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="74562-105">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="74562-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="74562-106">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="74562-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="74562-107">Este artigo fornece uma visão geral das etapas necessárias para a replicação de máquinas virtuais (VMs) do Hyper-V locais gerenciadas em nuvens do System Center Virtual Machine Manager (VMM) para um local secundário de VMM usando o [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="74562-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, to a secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span>

<span data-ttu-id="74562-108">Depois de ler este artigo, poste comentários na parte inferior ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="74562-108">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="74562-109">Etapa 1: Analisar a arquitetura do cenário</span><span class="sxs-lookup"><span data-stu-id="74562-109">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="74562-110">Antes de iniciar a implantação, examine a arquitetura do cenário e entenda todos os componentes que você precisa implantar.</span><span class="sxs-lookup"><span data-stu-id="74562-110">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="74562-111">Vá para a [Etapa 1: Examinar a arquitetura](vmm-to-vmm-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="74562-111">Go to [Step 1: Review the architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="74562-112">Etapa 2: Examinar os pré-requisitos e as limitações</span><span class="sxs-lookup"><span data-stu-id="74562-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="74562-113">Certifique-se de que você compreende os pré-requisitos e as limitações da implantação.</span><span class="sxs-lookup"><span data-stu-id="74562-113">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="74562-114">**Pré-requisitos do Azure**: você precisa de uma assinatura do Microsoft Azure e de um cofre do Azure Recovery Services para orquestrar e gerenciar a replicação.</span><span class="sxs-lookup"><span data-stu-id="74562-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, to orchestrate and manage replication.</span></span>
<span data-ttu-id="74562-115">**Servidores do VMM no local e os hosts do Hyper-V**: verifique se os servidores VMM e os hosts do Hyper-V são compatíveis e se estão preparados para a implantação do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="74562-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="74562-116">Vá para a [Etapa 2: Verificar os pré-requisitos e as limitações](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="74562-116">Go to [Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="74562-117">Etapa 3: Planejar a rede</span><span class="sxs-lookup"><span data-stu-id="74562-117">Step 3: Plan networking</span></span>

<span data-ttu-id="74562-118">Você precisa fazer algumas planejamento para garantir que você pode configurar o mapeamento de rede entre redes de VM do VMM quando você implanta o cenário.</span><span class="sxs-lookup"><span data-stu-id="74562-118">You need to do some network planning to ensure that you can configure network mapping between VMM VM networks when you deploy the scenario.</span></span>

<span data-ttu-id="74562-119">Vá para [Etapa 3: Planejar a rede](vmm-to-vmm-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="74562-119">Go to [Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="74562-120">Etapa 4: Preparar o VMM e o Hyper-V</span><span class="sxs-lookup"><span data-stu-id="74562-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="74562-121">Prepare os servidores do VMM e os hosts do Hyper-V para implantação do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="74562-121">Prepare the VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="74562-122">Vá para a [Etapa 4: Preparar servidores locais](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="74562-122">Go to [Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="74562-123">Etapa 5: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="74562-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="74562-124">Configure um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="74562-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="74562-125">O cofre contém definições de configuração e orquestra a replicação.</span><span class="sxs-lookup"><span data-stu-id="74562-125">The vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="74562-126">[Etapa 5: Configurar um cofre](vmm-to-vmm-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="74562-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="74562-127">Etapa 6: Definir as configurações de origem e de destino</span><span class="sxs-lookup"><span data-stu-id="74562-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="74562-128">Configure os locais de VMM de replicação de origem e destino.</span><span class="sxs-lookup"><span data-stu-id="74562-128">Set up the source and target replication VMM locations.</span></span> <span data-ttu-id="74562-129">Adicione os servidores do VMM ao cofre e baixe os arquivos de instalação de componentes do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="74562-129">Add the VMM servers to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="74562-130">Execute a instalação do Provedor do Azure Site Recovery no servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="74562-130">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="74562-131">O Provedor é instalado no servidor do VMM e registra o servidor no cofre.</span><span class="sxs-lookup"><span data-stu-id="74562-131">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="74562-132">Você pode instalar o agente de Serviços de Recuperação da Microsoft em cada host do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="74562-132">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="74562-133">Vá para a [Etapa 6: Definir as configurações de origem e de destino](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="74562-133">Go to [Step 6: Set up the source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="74562-134">Etapa 7: configurar o mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="74562-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="74562-135">Mapeie as redes de VM do VMM nos locais de origem e destino.</span><span class="sxs-lookup"><span data-stu-id="74562-135">Map VMM VM networks in the source and target locations.</span></span> <span data-ttu-id="74562-136">Após o failover, as máquinas virtuais são criadas na rede de destino que é mapeada para a rede de VM de origem em que a VM do Hyper-V de origem está localizada.</span><span class="sxs-lookup"><span data-stu-id="74562-136">After failover, VMs are created in the target network that maps to the source VM network in which the source Hyper-V VM is located.</span></span>

<span data-ttu-id="74562-137">Vá para a [Etapa 7: Configurar o mapeamento de rede](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="74562-137">Go to [Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="74562-138">Etapa 8: Configurar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="74562-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="74562-139">Especifica como as VMs serão replicadas entre os locais do VMM.</span><span class="sxs-lookup"><span data-stu-id="74562-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="74562-140">Vá para a [Etapa 8: Configurar uma política de replicação](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="74562-140">Go to [Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="74562-141">Etapa 9: Habilitar a replicação para VMs</span><span class="sxs-lookup"><span data-stu-id="74562-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="74562-142">Selecione as VMs que você deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="74562-142">Select the VMs you want to replicate.</span></span> <span data-ttu-id="74562-143">Habilitar uma máquina virtual para replicação dispara a replicação inicial para o site secundário, seguida pela replicação delta em andamento.</span><span class="sxs-lookup"><span data-stu-id="74562-143">Enabling a VM for replication triggers the initial replication to the secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="74562-144">Vá para a [Etapa 9: Habilitar a replicação](vmm-to-vmm-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="74562-144">Go to [Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="74562-145">Etapa 10: Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="74562-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="74562-146">Execute um failover de teste para verificar se tudo está funcionando como esperado.</span><span class="sxs-lookup"><span data-stu-id="74562-146">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="74562-147">Vá para [Etapa 10: Executar um failover de teste](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="74562-147">Go to [Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
