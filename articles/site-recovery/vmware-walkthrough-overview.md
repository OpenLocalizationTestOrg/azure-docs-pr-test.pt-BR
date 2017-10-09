---
title: aaaReplicate VMs VMware tooAzure com o Azure Site Recovery | Microsoft Docs
description: "Fornece uma visão geral das etapas de saudação para replicar as cargas de trabalho em execução em máquinas virtuais do VMware tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a><span data-ttu-id="10417-103">Replicar máquinas virtuais do VMware tooAzure com a recuperação de Site</span><span class="sxs-lookup"><span data-stu-id="10417-103">Replicate VMware VMs tooAzure with Site Recovery</span></span>

<span data-ttu-id="10417-104">Este artigo fornece uma visão geral da saudação etapas necessárias tooreplicate local VMware máquinas virtuais tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="10417-104">This article provides an overview of hello steps required tooreplicate on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


![Processo de implantação](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="10417-106">**Figura 1: Resumo do processo de implantação**</span><span class="sxs-lookup"><span data-stu-id="10417-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="10417-107">Etapa 1: Examinar a arquitetura e os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="10417-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="10417-108">Antes de iniciar a implantação, examine a arquitetura de cenário hello e certifique-se de que entender todos os componentes de saudação é necessário toodeploy</span><span class="sxs-lookup"><span data-stu-id="10417-108">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="10417-109">Vá muito[etapa 1: revisar arquitetura Olá](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="10417-109">Go too[Step 1: Review hello architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="10417-110">Etapa 2: Examinar os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="10417-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="10417-111">Certifique-se de que ter Olá pré-requisitos em vigor para cada componente de implantação:</span><span class="sxs-lookup"><span data-stu-id="10417-111">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="10417-112">**Pré-requisitos do Azure**: você precisa de uma conta do Microsoft Azure, redes do Azure e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="10417-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="10417-113">**Componentes locais do Site Recovery**: Você precisa de uma máquina que execute os componentes locais do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="10417-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="10417-114">**Pré-requisitos do VMware no local**: tooset contas é necessário para que a recuperação de Site pode acessar servidores VMware e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="10417-114">**On-premises VMware prerequisites**: You need tooset up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="10417-115">**Replicadas VMs**: VMs que você deseja tooreplicate necessidade toocomply com os requisitos do Azure e ter o componente de serviço de mobilidade Olá instalado.</span><span class="sxs-lookup"><span data-stu-id="10417-115">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements, and have hello Mobility service component installed.</span></span>

<span data-ttu-id="10417-116">Vá muito[etapa 2: analisar os pré-requisitos e limitações](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="10417-116">Go too[Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="10417-117">Etapa 3: Planejar a capacidade</span><span class="sxs-lookup"><span data-stu-id="10417-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="10417-118">Se você estiver fazendo uma implantação completa, que você precisa toofigure quais recursos de replicação é necessário.</span><span class="sxs-lookup"><span data-stu-id="10417-118">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="10417-119">Há algumas toohelp disponíveis ferramentas você fazer isso.</span><span class="sxs-lookup"><span data-stu-id="10417-119">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="10417-120">Vá tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="10417-120">Go tooStep 2.</span></span> <span data-ttu-id="10417-121">Se você estiver fazendo uma rápida de configurar o ambiente de saudação tootest, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="10417-121">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="10417-122">Vá muito[etapa 3: planejar a capacidade](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="10417-122">Go too[Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="10417-123">Etapa 4: Planejar a rede</span><span class="sxs-lookup"><span data-stu-id="10417-123">Step 4: Plan networking</span></span>

<span data-ttu-id="10417-124">É necessário toodo algum planejamento tooensure que máquinas virtuais do Azure são conectados toonetworks após o failover, e que se eles têm Olá direito de endereços IP da rede.</span><span class="sxs-lookup"><span data-stu-id="10417-124">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="10417-125">Vá muito[etapa 4: planejar a rede](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="10417-125">Go too[Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="10417-126">Etapa 5: Preparar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="10417-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="10417-127">Configure as redes e o armazenamento do Azure antes de começar.</span><span class="sxs-lookup"><span data-stu-id="10417-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="10417-128">Você pode fazer isso durante a implantação, mas recomendamos fazer isso antes de começar.</span><span class="sxs-lookup"><span data-stu-id="10417-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="10417-129">Vá muito[etapa 5: preparar o Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="10417-129">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="10417-130">Etapa 6: Preparar o VMware</span><span class="sxs-lookup"><span data-stu-id="10417-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="10417-131">É necessário tooset as contas de recuperação de Site será usado para:</span><span class="sxs-lookup"><span data-stu-id="10417-131">You need tooset up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="10417-132">Acesso tooautomatically de servidores de virtualização de VMware detectar VMs.</span><span class="sxs-lookup"><span data-stu-id="10417-132">Access VMware virtualization servers tooautomatically detect VMs.</span></span>
- <span data-ttu-id="10417-133">Acesse o serviço de mobilidade VMs tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="10417-133">Access VMs tooinstall hello Mobility service.</span></span> <span data-ttu-id="10417-134">Cada máquina virtual que você deseja tooreplicate devem ter o agente de serviço de mobilidade de Olá instalado antes de você pode habilitar a replicação para ele.</span><span class="sxs-lookup"><span data-stu-id="10417-134">Each VM you want tooreplicate must have hello Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="10417-135">Vá muito[etapa 6: preparar VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="10417-135">Go too[Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="10417-136">Etapa 7: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="10417-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="10417-137">Você precisa tooset a um tooorchestrate de Cofre de serviços de recuperação e gerenciar a replicação.</span><span class="sxs-lookup"><span data-stu-id="10417-137">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="10417-138">Quando você configura o cofre hello, especifique o que você deseja tooreplicate, e onde você deseja tooreplicate-o para.</span><span class="sxs-lookup"><span data-stu-id="10417-138">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="10417-139">Vá muito[etapa 7: configurar um cofre](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="10417-139">Go too[Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="10417-140">Etapa 8: Definir as configurações de origem e destino</span><span class="sxs-lookup"><span data-stu-id="10417-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="10417-141">Configure a origem de saudação e de destino que é usado para replicação.</span><span class="sxs-lookup"><span data-stu-id="10417-141">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="10417-142">Definir configurações de origem inclui a execução tooinstall de instalação do Unified componentes de recuperação de Site Olá locais.</span><span class="sxs-lookup"><span data-stu-id="10417-142">Setting up source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="10417-143">Vá muito[etapa 8: configurar Olá origem e destino](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="10417-143">Go too[Step 8: Set up hello source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="10417-144">Etapa 9: Definir uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="10417-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="10417-145">Defina as configurações de replicação de toospecify uma política para VMs VMware no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="10417-145">You set up a policy toospecify replication settings for VMware VMs in hello vault.</span></span>

<span data-ttu-id="10417-146">Vá muito[etapa 9: configurar uma política de replicação](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="10417-146">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="10417-147">Etapa 10: Instalar o serviço de mobilidade Olá</span><span class="sxs-lookup"><span data-stu-id="10417-147">Step 10: Install hello Mobility service</span></span>

<span data-ttu-id="10417-148">Olá serviço de mobilidade deve ser instalado em cada máquina virtual que você deseja tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="10417-148">hello Mobility service must be installed on each VM you want tooreplicate.</span></span> <span data-ttu-id="10417-149">Há alguns tooset maneiras serviço Olá com instalação de push ou pull.</span><span class="sxs-lookup"><span data-stu-id="10417-149">There are a few ways tooset up hello service with push or pull installation.</span></span>

<span data-ttu-id="10417-150">Vá muito[etapa 10: instalar o serviço de mobilidade Olá](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="10417-150">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="10417-151">Etapa 11: Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="10417-151">Step 11: Enable replication</span></span>

<span data-ttu-id="10417-152">Depois de saudação serviço de mobilidade está em execução em uma máquina virtual, você pode habilitar replicação para ele.</span><span class="sxs-lookup"><span data-stu-id="10417-152">After hello Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="10417-153">Depois de habilitar, ocorre a replicação inicial dos Olá VM.</span><span class="sxs-lookup"><span data-stu-id="10417-153">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="10417-154">Vá muito[etapa 11: habilitar a replicação](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="10417-154">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="10417-155">Etapa 12: Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="10417-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="10417-156">Após a conclusão da replicação inicial, e a replicação delta está em execução, você pode executar um toomake de failover de teste se que tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="10417-156">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="10417-157">Vá muito[etapa 12: executar um failover de teste](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="10417-157">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
