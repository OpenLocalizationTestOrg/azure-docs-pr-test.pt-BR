---
title: aaaReplicate VMs Hyper-V no VMM nuvens tooAzure com o Azure Site Recovery | Microsoft Docs
description: "Fornece uma visão geral para replicar máquinas virtuais do Hyper-V no VMM tooAzure de nuvens usando o serviço do Azure Site Recovery Olá"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a><span data-ttu-id="9afbe-103">Replicar máquinas virtuais Hyper-V no tooAzure de nuvens do VMM usando o Site Recovery no portal do Azure de saudação</span><span class="sxs-lookup"><span data-stu-id="9afbe-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9afbe-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9afbe-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="9afbe-105">Azure clássico</span><span class="sxs-lookup"><span data-stu-id="9afbe-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="9afbe-106">Implantação do Resource Manager do PowerShell</span><span class="sxs-lookup"><span data-stu-id="9afbe-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="9afbe-107">Implantação clássica do PowerShell</span><span class="sxs-lookup"><span data-stu-id="9afbe-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="9afbe-108">Este artigo fornece uma visão geral da saudação etapas necessárias tooreplicate máquinas de virtuais de Hyper-V (VMs) gerenciadas no tooAzure de nuvens do System Center Virtual Machine Manager (VMM), usando Olá local [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9afbe-108">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="9afbe-109">Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="9afbe-109">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="9afbe-110">Etapa 1: Analisar a arquitetura de cenário Olá</span><span class="sxs-lookup"><span data-stu-id="9afbe-110">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="9afbe-111">Antes de iniciar a implantação, examine a arquitetura de cenário hello e certifique-se de que você compreenda todos os componentes de saudação precisar toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9afbe-111">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="9afbe-112">Vá muito[etapa 1: revisar arquitetura Olá](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="9afbe-112">Go too[Step 1: Review hello architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="9afbe-113">Etapa 2: Analisar os pré-requisitos e as limitações</span><span class="sxs-lookup"><span data-stu-id="9afbe-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="9afbe-114">Certifique-se de que você compreenda os pré-requisitos de implantação hello e limitações.</span><span class="sxs-lookup"><span data-stu-id="9afbe-114">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="9afbe-115">**Pré-requisitos do Azure**: você precisa de uma conta do Microsoft Azure, redes do Azure e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9afbe-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="9afbe-116">**Servidores do VMM no local e os hosts do Hyper-V**: verifique se os servidores VMM e os hosts do Hyper-V são compatíveis e se estão preparados para a implantação do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9afbe-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="9afbe-117">**Replicadas VMs**: Verifique se as VMs que você deseja tooreplicate atender aos requisitos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9afbe-117">**Replicated VMs**: Check that VMs you want tooreplicate comply with Azure requirements.</span></span>

<span data-ttu-id="9afbe-118">Vá muito[etapa 2: verificar os pré-requisitos e limitações](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="9afbe-118">Go too[Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="9afbe-119">Etapa 3: Planejar a capacidade</span><span class="sxs-lookup"><span data-stu-id="9afbe-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="9afbe-120">Se você estiver fazendo uma implantação completa, você precisa toofigure quais recursos de replicação é necessário.</span><span class="sxs-lookup"><span data-stu-id="9afbe-120">If you're doing a full deployment, you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="9afbe-121">Há algumas toohelp disponíveis ferramentas você fazer isso.</span><span class="sxs-lookup"><span data-stu-id="9afbe-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="9afbe-122">Se você estiver fazendo uma rápida de configurar o ambiente de saudação tootest, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="9afbe-122">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="9afbe-123">Vá muito[etapa 3: planejar a capacidade](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="9afbe-123">Go too[Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="9afbe-124">Etapa 4: Planejar a rede</span><span class="sxs-lookup"><span data-stu-id="9afbe-124">Step 4: Plan networking</span></span>

<span data-ttu-id="9afbe-125">É necessário toodo alguma rede planejamento tooensure que você pode configurar o mapeamento de rede quando você implanta o cenário de hello, máquinas virtuais do Azure será redes virtuais conectadas tooAzure após failover ocorrer e que quais estão atribuídas IP apropriada de endereços.</span><span class="sxs-lookup"><span data-stu-id="9afbe-125">You need toodo some network planning tooensure that you can configure network mapping when you deploy hello scenario, that Azure VMs will be connected tooAzure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="9afbe-126">Vá muito[etapa 4: planejar a rede](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="9afbe-126">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="9afbe-127">Etapa 5: Preparar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="9afbe-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="9afbe-128">Configure uma conta, redes e armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9afbe-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="9afbe-129">Você pode fazer isso durante a implantação, mas recomendamos fazer isso antes de começar.</span><span class="sxs-lookup"><span data-stu-id="9afbe-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="9afbe-130">Vá muito[etapa 5: preparar o Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="9afbe-130">Go too[Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="9afbe-131">Etapa 6: Preparar o VMM e o Hyper-V</span><span class="sxs-lookup"><span data-stu-id="9afbe-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="9afbe-132">Prepare servidores do VMM local hello e hosts Hyper-V para implantação da recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="9afbe-132">Prepare hello on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="9afbe-133">Vá muito[etapa 6: preparar servidores locais](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="9afbe-133">Go too[Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="9afbe-134">Etapa 7: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="9afbe-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="9afbe-135">Configurar um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="9afbe-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="9afbe-136">cofre Olá contém definições de configuração e coordena a replicação.</span><span class="sxs-lookup"><span data-stu-id="9afbe-136">hello vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="9afbe-137">Etapa 7: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="9afbe-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="9afbe-138">Etapa 8: Definir as configurações de origem e destino</span><span class="sxs-lookup"><span data-stu-id="9afbe-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="9afbe-139">Configure locais de replicação de origem e destino hello.</span><span class="sxs-lookup"><span data-stu-id="9afbe-139">Set up hello source and target replication locations.</span></span> <span data-ttu-id="9afbe-140">Adicionar o cofre do hello VMM server toohello e baixar arquivos de instalação Olá para componentes do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9afbe-140">Add hello VMM server toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="9afbe-141">Execute a instalação do provedor Azure Site Recovery no servidor do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="9afbe-141">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="9afbe-142">A instalação instala Olá provedor no servidor do VMM hello e registra o servidor de saudação no cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="9afbe-142">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="9afbe-143">Instale o agente de serviços de recuperação do Microsoft hello em cada host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="9afbe-143">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="9afbe-144">Vá muito[etapa 8: definir configurações de origem e destino](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="9afbe-144">Go too[Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="9afbe-145">Etapa 9: Configurar o mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="9afbe-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="9afbe-146">Mapa de redes virtuais de tooAzure de redes de VM do VMM no local.</span><span class="sxs-lookup"><span data-stu-id="9afbe-146">Map on-premises VMM VM networks tooAzure virtual networks.</span></span> <span data-ttu-id="9afbe-147">Após o failover, máquinas virtuais do Azure são criados no hello rede do Azure que mapeia a rede VM do toohello local no qual Olá Hyper-V de origem está localizado.</span><span class="sxs-lookup"><span data-stu-id="9afbe-147">After failover, Azure VMs are created in hello Azure network that maps toohello on-premises VM network in which hello source Hyper-V is located.</span></span>

<span data-ttu-id="9afbe-148">Vá muito[etapa 9: Configurar mapeamento de rede](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="9afbe-148">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="9afbe-149">Etapa 10: Configurar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="9afbe-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="9afbe-150">Especifique como VMs locais serão replicada tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9afbe-150">Specify how on-premises VMs will be replicated tooAzure.</span></span>

<span data-ttu-id="9afbe-151">Vá muito[etapa 10: configurar uma política de replicação](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="9afbe-151">Go too[Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="9afbe-152">Etapa 11: Habilitar a replicação para VMs</span><span class="sxs-lookup"><span data-stu-id="9afbe-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="9afbe-153">Selecione VMs Olá deseja tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="9afbe-153">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="9afbe-154">Habilitar uma máquina virtual para replicação gatilhos Olá a replicação inicial tooAzure, seguido por replicação delta em andamento.</span><span class="sxs-lookup"><span data-stu-id="9afbe-154">ENabling a VM for replication triggers hello initial replication tooAzure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="9afbe-155">Vá muito[etapa 11: habilitar a replicação](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="9afbe-155">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="9afbe-156">Etapa 12: Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="9afbe-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="9afbe-157">Execute um toomake de failover de teste se que tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="9afbe-157">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="9afbe-158">Vá muito[etapa 12: executar um failover de teste](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="9afbe-158">Go too[Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


