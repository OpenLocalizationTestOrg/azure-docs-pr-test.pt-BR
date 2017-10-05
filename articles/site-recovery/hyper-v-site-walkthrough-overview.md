---
title: Replicar VMs do Hyper-V para o Azure com o Azure Site Recovery | Microsoft Docs
description: "Descreve como implantar orquestrar a replicação, o failover e a recuperação de VMs do Hyper-V locais para o Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: da10b213bc2543942b5ac77cf5c5d8547c00220c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-to-azure"></a><span data-ttu-id="3d925-103">Replicar máquinas virtuais do Hyper-V (sem o VMM) para o Azure</span><span class="sxs-lookup"><span data-stu-id="3d925-103">Replicate Hyper-V virtual machines (without VMM) to Azure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d925-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3d925-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="3d925-105">Azure clássico</span><span class="sxs-lookup"><span data-stu-id="3d925-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="3d925-106">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3d925-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="3d925-107">Este artigo fornece uma visão geral das etapas necessárias para replicar máquinas virtuais locais do Hyper-V para o Azure, usando o [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d925-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> <span data-ttu-id="3d925-108">Nessa implantação, VMs de Hyper-V não são gerenciadas pelo System Center Virtual Machine Manager (VMM).</span><span class="sxs-lookup"><span data-stu-id="3d925-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="3d925-109">Depois de ler este artigo, poste comentários no final ou faça perguntas técnicas no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3d925-109">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="3d925-110">Etapa 1: Examinar a arquitetura e os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3d925-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="3d925-111">Antes de iniciar a implantação, examine a arquitetura do cenário e entenda todos os componentes que você precisa implantar</span><span class="sxs-lookup"><span data-stu-id="3d925-111">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="3d925-112">Ir para a [Etapa 1: Examinar a arquitetura](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="3d925-112">Go to [Step 1: Review the architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="3d925-113">Etapa 2: Examinar os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3d925-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="3d925-114">Verifique se os pré-requisitos estão em vigor para cada componente de implantação:</span><span class="sxs-lookup"><span data-stu-id="3d925-114">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="3d925-115">**Pré-requisitos do Azure**: você precisa de uma conta do Microsoft Azure, redes do Azure e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3d925-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="3d925-116">**Pré-requisitos do Hyper-V local**: verifique se os hosts Hyper-V estão preparados para a implantação do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3d925-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="3d925-117">**VMs replicadas**: as VMs que você deseja replicar precisam atender aos requisitos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d925-117">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements.</span></span>

<span data-ttu-id="3d925-118">Ir para a [Etapa 2: Verificar os pré-requisitos e as limitações](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="3d925-118">Go to [Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="3d925-119">Etapa 3: Planejar a capacidade</span><span class="sxs-lookup"><span data-stu-id="3d925-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="3d925-120">Se você estiver fazendo uma implantação completa, precisará descobrir quais recursos de replicação serão necessários.</span><span class="sxs-lookup"><span data-stu-id="3d925-120">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="3d925-121">Há algumas ferramentas disponíveis para ajudá-lo a fazer isso.</span><span class="sxs-lookup"><span data-stu-id="3d925-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="3d925-122">Vá para a Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="3d925-122">Go to Step 2.</span></span> <span data-ttu-id="3d925-123">Se estiver fazendo uma configuração rápida para testar o ambiente, ignore esta etapa.</span><span class="sxs-lookup"><span data-stu-id="3d925-123">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="3d925-124">Ir para a [Etapa 3: Planejar a capacidade](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="3d925-124">Go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="3d925-125">Etapa 4: Planejar a rede</span><span class="sxs-lookup"><span data-stu-id="3d925-125">Step 4: Plan networking</span></span>

<span data-ttu-id="3d925-126">Você precisa fazer um planejamento de rede para garantir que as VMs do Azure serão conectadas a redes após o failover e que elas têm os endereços IP corretos.</span><span class="sxs-lookup"><span data-stu-id="3d925-126">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="3d925-127">Ir para a [Etapa 4: Planejar a rede](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="3d925-127">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="3d925-128">Etapa 5: Preparar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="3d925-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="3d925-129">Configure as redes e o armazenamento do Azure antes de começar.</span><span class="sxs-lookup"><span data-stu-id="3d925-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="3d925-130">Você pode fazer isso durante a implantação, mas recomendamos fazer isso antes de começar.</span><span class="sxs-lookup"><span data-stu-id="3d925-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="3d925-131">Ir para a [Etapa 5: Preparar o Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="3d925-131">Go to [Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="3d925-132">Etapa 6: Preparar o Hyper-V</span><span class="sxs-lookup"><span data-stu-id="3d925-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="3d925-133">Verifique se os Hyper-V Servers atendem aos requisitos de implantação do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3d925-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="3d925-134">Ir para a [Etapa 6: Preparar o Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="3d925-134">Go to [Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="3d925-135">Etapa 7: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="3d925-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="3d925-136">Você precisa configurar um cofre dos Serviços de Recuperação para orquestrar e gerenciar a replicação.</span><span class="sxs-lookup"><span data-stu-id="3d925-136">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="3d925-137">Ao configurar o cofre, você especifica o que deseja replicar e o local para o qual deseja replicá-lo.</span><span class="sxs-lookup"><span data-stu-id="3d925-137">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="3d925-138">Ir para a [Etapa 7: Criar um cofre](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="3d925-138">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="3d925-139">Etapa 8: Definir as configurações de origem e destino</span><span class="sxs-lookup"><span data-stu-id="3d925-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="3d925-140">Configure a origem e o destino usados para a replicação.</span><span class="sxs-lookup"><span data-stu-id="3d925-140">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="3d925-141">A definição das configurações de origem inclui adicionar hosts Hyper-V a um site do Hyper-V, instalar o Provedor do Site Recovery e o agente dos Serviços de Recuperação em cada host Hyper-V e registrar o site no cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="3d925-141">Setting up source settings includes adding Hyper-V hosts to a Hyper-V site, installing the Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering the site in the Recovery Services vault.</span></span>

<span data-ttu-id="3d925-142">Ir para a [Etapa 8: Configurar a origem e o destino](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="3d925-142">Go to [Step 8: Set up the source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="3d925-143">Etapa 9: Configurar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="3d925-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="3d925-144">Configure uma política para especificar as configurações de replicação das VMs do Hyper-V no cofre.</span><span class="sxs-lookup"><span data-stu-id="3d925-144">You set up a policy to specify replication settings for Hyper-V VMs in the vault.</span></span>

<span data-ttu-id="3d925-145">Ir para a [Etapa 9: Configurar uma política de replicação](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="3d925-145">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="3d925-146">Etapa 10: Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="3d925-146">Step 10: Enable replication</span></span>

<span data-ttu-id="3d925-147">Depois que você tiver uma política de replicação em vigor, após a habilitação, ocorrerá a replicação inicial da VM.</span><span class="sxs-lookup"><span data-stu-id="3d925-147">After you have a replication policy in place,  After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="3d925-148">Ir para a [Etapa 10: Habilitar a replicação](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="3d925-148">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="3d925-149">Etapa 11: Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="3d925-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="3d925-150">Após a conclusão da replicação inicial e a replicação delta estiver em execução, você poderá executar um failover de teste para verificar se tudo está funcionando como esperado.</span><span class="sxs-lookup"><span data-stu-id="3d925-150">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="3d925-151">Ir para a [Etapa 11: Executar um failover de teste](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="3d925-151">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
