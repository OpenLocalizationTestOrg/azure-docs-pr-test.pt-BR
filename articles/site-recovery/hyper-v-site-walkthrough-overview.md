---
title: aaaReplicate tooAzure de VMs Hyper-V com o Azure Site Recovery | Microsoft Docs
description: "Descreve como tooorchestrate replicação, failover e recuperação de local Hyper-V VMs tooAzure"
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
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a><span data-ttu-id="94613-103">Replicar tooAzure de máquinas virtuais (sem VMM) do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="94613-103">Replicate Hyper-V virtual machines (without VMM) tooAzure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="94613-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="94613-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="94613-105">Azure clássico</span><span class="sxs-lookup"><span data-stu-id="94613-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="94613-106">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="94613-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="94613-107">Este artigo fornece uma visão geral da saudação etapas necessárias tooreplicate local Hyper-V máquinas virtuais tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="94613-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> <span data-ttu-id="94613-108">Nessa implantação, VMs de Hyper-V não são gerenciadas pelo System Center Virtual Machine Manager (VMM).</span><span class="sxs-lookup"><span data-stu-id="94613-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="94613-109">Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="94613-109">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="94613-110">Etapa 1: Examinar a arquitetura e os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="94613-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="94613-111">Antes de iniciar a implantação, examine a arquitetura de cenário hello e certifique-se de que entender todos os componentes de saudação é necessário toodeploy</span><span class="sxs-lookup"><span data-stu-id="94613-111">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="94613-112">Vá muito[etapa 1: revisar arquitetura Olá](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="94613-112">Go too[Step 1: Review hello architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="94613-113">Etapa 2: Examinar os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="94613-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="94613-114">Certifique-se de que ter Olá pré-requisitos em vigor para cada componente de implantação:</span><span class="sxs-lookup"><span data-stu-id="94613-114">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="94613-115">**Pré-requisitos do Azure**: você precisa de uma conta do Microsoft Azure, redes do Azure e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="94613-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="94613-116">**Pré-requisitos do Hyper-V local**: verifique se os hosts Hyper-V estão preparados para a implantação do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="94613-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="94613-117">**Replicadas VMs**: máquinas virtuais que você deseja tooreplicate necessário toocomply com os requisitos do Azure.</span><span class="sxs-lookup"><span data-stu-id="94613-117">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements.</span></span>

<span data-ttu-id="94613-118">Vá muito[etapa 2: verificar os pré-requisitos e limitações](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="94613-118">Go too[Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="94613-119">Etapa 3: Planejar a capacidade</span><span class="sxs-lookup"><span data-stu-id="94613-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="94613-120">Se você estiver fazendo uma implantação completa, que você precisa toofigure quais recursos de replicação é necessário.</span><span class="sxs-lookup"><span data-stu-id="94613-120">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="94613-121">Há algumas toohelp disponíveis ferramentas você fazer isso.</span><span class="sxs-lookup"><span data-stu-id="94613-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="94613-122">Vá tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="94613-122">Go tooStep 2.</span></span> <span data-ttu-id="94613-123">Se você estiver fazendo uma rápida de configurar o ambiente de saudação tootest, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="94613-123">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="94613-124">Vá muito[etapa 3: planejar a capacidade](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="94613-124">Go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="94613-125">Etapa 4: Planejar a rede</span><span class="sxs-lookup"><span data-stu-id="94613-125">Step 4: Plan networking</span></span>

<span data-ttu-id="94613-126">É necessário toodo algum planejamento tooensure que máquinas virtuais do Azure são conectados toonetworks após o failover, e que se eles têm Olá direito de endereços IP da rede.</span><span class="sxs-lookup"><span data-stu-id="94613-126">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="94613-127">Vá muito[etapa 4: planejar a rede](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="94613-127">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="94613-128">Etapa 5: Preparar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="94613-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="94613-129">Configure as redes e o armazenamento do Azure antes de começar.</span><span class="sxs-lookup"><span data-stu-id="94613-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="94613-130">Você pode fazer isso durante a implantação, mas recomendamos fazer isso antes de começar.</span><span class="sxs-lookup"><span data-stu-id="94613-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="94613-131">Vá muito[etapa 5: preparar o Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="94613-131">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="94613-132">Etapa 6: Preparar o Hyper-V</span><span class="sxs-lookup"><span data-stu-id="94613-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="94613-133">Verifique se os Hyper-V Servers atendem aos requisitos de implantação do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="94613-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="94613-134">Vá muito[etapa 6: preparar Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="94613-134">Go too[Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="94613-135">Etapa 7: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="94613-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="94613-136">Você precisa tooset a um tooorchestrate de Cofre de serviços de recuperação e gerenciar a replicação.</span><span class="sxs-lookup"><span data-stu-id="94613-136">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="94613-137">Quando você configura o cofre hello, especifique o que você deseja tooreplicate, e onde você deseja tooreplicate-o para.</span><span class="sxs-lookup"><span data-stu-id="94613-137">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="94613-138">Vá muito[etapa 7: criar um cofre](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="94613-138">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="94613-139">Etapa 8: Definir as configurações de origem e destino</span><span class="sxs-lookup"><span data-stu-id="94613-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="94613-140">Configure a origem de saudação e de destino que é usado para replicação.</span><span class="sxs-lookup"><span data-stu-id="94613-140">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="94613-141">Definir configurações de origem inclui a adição de site do Hyper-V de tooa do Hyper-V hosts, instalando hello provedor de recuperação de Site e o agente de serviços de recuperação em cada host Hyper-V e registrando site Olá no hello que Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="94613-141">Setting up source settings includes adding Hyper-V hosts tooa Hyper-V site, installing hello Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering hello site in hello Recovery Services vault.</span></span>

<span data-ttu-id="94613-142">Vá muito[etapa 8: configurar Olá origem e destino](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="94613-142">Go too[Step 8: Set up hello source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="94613-143">Etapa 9: Definir uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="94613-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="94613-144">Defina as configurações de replicação de toospecify uma política para VMs Hyper-V no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="94613-144">You set up a policy toospecify replication settings for Hyper-V VMs in hello vault.</span></span>

<span data-ttu-id="94613-145">Vá muito[etapa 9: configurar uma política de replicação](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="94613-145">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="94613-146">Etapa 10: Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="94613-146">Step 10: Enable replication</span></span>

<span data-ttu-id="94613-147">Depois que você tiver uma política de replicação no local, depois de habilitar, ocorre a replicação inicial da saudação VM.</span><span class="sxs-lookup"><span data-stu-id="94613-147">After you have a replication policy in place,  After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="94613-148">Vá muito[etapa 10: habilitar a replicação](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="94613-148">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="94613-149">Etapa 11: Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="94613-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="94613-150">Após a conclusão da replicação inicial, e a replicação delta está em execução, você pode executar um toomake de failover de teste se que tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="94613-150">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="94613-151">Vá muito[etapa 11: executar um failover de teste](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="94613-151">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
