---
title: Replicar VMs do Hyper-V em nuvens do VMM para o Azure com o Azure Site Recovery | Microsoft Docs
description: "Fornece uma visão geral para replicar VMs do Hyper-V em nuvens do VMM para o Azure usando o serviço Azure Site Recovery"
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
ms.openlocfilehash: af68d21184c137b2b0f1bb4c1afb9bf507e8332d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-site-recovery-in-the-azure-portal"></a><span data-ttu-id="de46a-103">Replicar máquinas virtuais Hyper-V em nuvens VMM no Azure usando o Site Recovery no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="de46a-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using Site Recovery in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="de46a-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="de46a-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="de46a-105">Azure clássico</span><span class="sxs-lookup"><span data-stu-id="de46a-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="de46a-106">Implantação do Resource Manager do PowerShell</span><span class="sxs-lookup"><span data-stu-id="de46a-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="de46a-107">Implantação clássica do PowerShell</span><span class="sxs-lookup"><span data-stu-id="de46a-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="de46a-108">Este artigo fornece uma visão geral das etapas necessárias para a replicação de máquinas virtuais (VMs) do Hyper-V locais gerenciadas em nuvens do System Center VMM (Virtual Machine Manager) o azure, usando o serviço [Azure Site Recovery](site-recovery-overview.md) no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="de46a-108">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="de46a-109">Depois de ler este artigo, poste comentários na parte inferior ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="de46a-109">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="de46a-110">Etapa 1: Analisar a arquitetura do cenário</span><span class="sxs-lookup"><span data-stu-id="de46a-110">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="de46a-111">Antes de iniciar a implantação, examine a arquitetura do cenário e entenda todos os componentes que você precisa implantar.</span><span class="sxs-lookup"><span data-stu-id="de46a-111">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="de46a-112">Ir para a [Etapa 1: Examinar a arquitetura](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="de46a-112">Go to [Step 1: Review the architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="de46a-113">Etapa 2: Analisar os pré-requisitos e as limitações</span><span class="sxs-lookup"><span data-stu-id="de46a-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="de46a-114">Certifique-se de que você compreende os pré-requisitos e as limitações da implantação.</span><span class="sxs-lookup"><span data-stu-id="de46a-114">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="de46a-115">**Pré-requisitos do Azure**: você precisa de uma conta do Microsoft Azure, redes do Azure e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="de46a-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="de46a-116">**Servidores do VMM no local e os hosts do Hyper-V**: verifique se os servidores VMM e os hosts do Hyper-V são compatíveis e se estão preparados para a implantação do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="de46a-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="de46a-117">**VMs replicadas**: verifique se as VMs que você deseja replicar atendem aos requisitos do Azure.</span><span class="sxs-lookup"><span data-stu-id="de46a-117">**Replicated VMs**: Check that VMs you want to replicate comply with Azure requirements.</span></span>

<span data-ttu-id="de46a-118">Ir para a [Etapa 2: Verificar os pré-requisitos e as limitações](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="de46a-118">Go to [Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="de46a-119">Etapa 3: Planejar a capacidade</span><span class="sxs-lookup"><span data-stu-id="de46a-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="de46a-120">Se você estiver fazendo uma implantação completa, precisará descobrir quais recursos de replicação serão necessários.</span><span class="sxs-lookup"><span data-stu-id="de46a-120">If you're doing a full deployment, you need to figure out what replication resources you need.</span></span> <span data-ttu-id="de46a-121">Há algumas ferramentas disponíveis para ajudá-lo a fazer isso.</span><span class="sxs-lookup"><span data-stu-id="de46a-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="de46a-122">Se estiver fazendo uma configuração rápida para testar o ambiente, ignore esta etapa.</span><span class="sxs-lookup"><span data-stu-id="de46a-122">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="de46a-123">Ir para a [Etapa 3: Planejar a capacidade](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="de46a-123">Go to [Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="de46a-124">Etapa 4: Planejar a rede</span><span class="sxs-lookup"><span data-stu-id="de46a-124">Step 4: Plan networking</span></span>

<span data-ttu-id="de46a-125">Você precisa planejar para assegurar a configuração do mapeamento de rede ao implantar o cenário, a conexão das VMs do Azure a redes virtuais do Azure após failover e a atribuição dos endereços IP apropriados.</span><span class="sxs-lookup"><span data-stu-id="de46a-125">You need to do some network planning to ensure that you can configure network mapping when you deploy the scenario, that Azure VMs will be connected to Azure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="de46a-126">Ir para a [Etapa 4: Planejar a rede](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="de46a-126">Go to [Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="de46a-127">Etapa 5: Preparar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="de46a-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="de46a-128">Configure uma conta, redes e armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="de46a-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="de46a-129">Você pode fazer isso durante a implantação, mas recomendamos fazer isso antes de começar.</span><span class="sxs-lookup"><span data-stu-id="de46a-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="de46a-130">Ir para a [Etapa 5: Preparar o Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="de46a-130">Go to [Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="de46a-131">Etapa 6: Preparar o VMM e o Hyper-V</span><span class="sxs-lookup"><span data-stu-id="de46a-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="de46a-132">Prepare os servidores do VMM locais e os hosts do Hyper-V para implantação do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="de46a-132">Prepare the on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="de46a-133">Vá para a [Etapa 6: Preparar servidores locais](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="de46a-133">Go to [Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="de46a-134">Etapa 7: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="de46a-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="de46a-135">Configurar um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="de46a-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="de46a-136">O cofre contém definições de configuração e orquestra a replicação.</span><span class="sxs-lookup"><span data-stu-id="de46a-136">The vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="de46a-137">Etapa 7: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="de46a-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="de46a-138">Etapa 8: Definir as configurações de origem e destino</span><span class="sxs-lookup"><span data-stu-id="de46a-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="de46a-139">Configure os locais de replicação de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="de46a-139">Set up the source and target replication locations.</span></span> <span data-ttu-id="de46a-140">Adicione o servidor do VMM ao cofre e baixe os arquivos de instalação de componentes do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="de46a-140">Add the VMM server to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="de46a-141">Execute a instalação do Provedor do Azure Site Recovery no servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="de46a-141">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="de46a-142">O Provedor é instalado no servidor do VMM e registra o servidor no cofre.</span><span class="sxs-lookup"><span data-stu-id="de46a-142">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="de46a-143">Você pode instalar o agente de Serviços de Recuperação da Microsoft em cada host do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="de46a-143">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="de46a-144">Vá para a [Etapa 8: Definir as configurações de origem e destino](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="de46a-144">Go to [Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="de46a-145">Etapa 9: Configurar o mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="de46a-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="de46a-146">Mapear redes de VM do VMM locais para redes virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="de46a-146">Map on-premises VMM VM networks to Azure virtual networks.</span></span> <span data-ttu-id="de46a-147">Após o failover, as VMs do Azure são criadas na rede do Azure que é mapeada para a rede de VM local na qual a VM do Hyper-V de origem está localizada.</span><span class="sxs-lookup"><span data-stu-id="de46a-147">After failover, Azure VMs are created in the Azure network that maps to the on-premises VM network in which the source Hyper-V is located.</span></span>

<span data-ttu-id="de46a-148">Vá para a [Etapa 9: Configurar o mapeamento de rede](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="de46a-148">Go to [Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="de46a-149">Etapa 10: Configurar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="de46a-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="de46a-150">Especifique como as VMs locais serão replicadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="de46a-150">Specify how on-premises VMs will be replicated to Azure.</span></span>

<span data-ttu-id="de46a-151">Vá para a [Etapa 10: Configurar uma política de replicação](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="de46a-151">Go to [Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="de46a-152">Etapa 11: Habilitar a replicação para VMs</span><span class="sxs-lookup"><span data-stu-id="de46a-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="de46a-153">Selecione as VMs que você deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="de46a-153">Select the VMs you want to replicate.</span></span> <span data-ttu-id="de46a-154">Habilitar uma VM para replicação dispara a replicação inicial no Azure, seguida pela replicação delta em andamento.</span><span class="sxs-lookup"><span data-stu-id="de46a-154">ENabling a VM for replication triggers the initial replication to Azure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="de46a-155">Vá para a [Etapa 11: Habilitar a replicação](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="de46a-155">Go to [Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="de46a-156">Etapa 12: Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="de46a-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="de46a-157">Execute um failover de teste para verificar se tudo está funcionando como esperado.</span><span class="sxs-lookup"><span data-stu-id="de46a-157">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="de46a-158">Vá para a [Etapa 12: Executar um failover de teste](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="de46a-158">Go to [Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


