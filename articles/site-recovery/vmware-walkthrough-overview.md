---
title: Replicar VMs do VMware para o Azure com o Azure Site Recovery | Microsoft Docs
description: "Fornece uma visão geral das etapas para replicar as cargas de trabalho em execução em VMs do VMware no Azure"
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
ms.openlocfilehash: db6f5f95929503e82a529dba26b56af1edb0767f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-vms-to-azure-with-site-recovery"></a><span data-ttu-id="bc3fa-103">Replicar VMs do VMware no Azure com o Site Recovery</span><span class="sxs-lookup"><span data-stu-id="bc3fa-103">Replicate VMware VMs to Azure with Site Recovery</span></span>

<span data-ttu-id="bc3fa-104">Este artigo fornece uma visão geral das etapas necessárias para replicar máquinas virtuais locais do VMware para o Azure, usando o serviço do [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-104">This article provides an overview of the steps required to replicate on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


![Processo de implantação](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="bc3fa-106">**Figura 1: Resumo do processo de implantação**</span><span class="sxs-lookup"><span data-stu-id="bc3fa-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="bc3fa-107">Etapa 1: Examinar a arquitetura e os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bc3fa-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="bc3fa-108">Antes de iniciar a implantação, examine a arquitetura do cenário e entenda todos os componentes que você precisa implantar</span><span class="sxs-lookup"><span data-stu-id="bc3fa-108">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="bc3fa-109">Ir para a [Etapa 1: Examinar a arquitetura](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="bc3fa-109">Go to [Step 1: Review the architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="bc3fa-110">Etapa 2: Examinar os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bc3fa-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="bc3fa-111">Verifique se os pré-requisitos estão em vigor para cada componente de implantação:</span><span class="sxs-lookup"><span data-stu-id="bc3fa-111">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="bc3fa-112">**Pré-requisitos do Azure**: você precisa de uma conta do Microsoft Azure, redes do Azure e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="bc3fa-113">**Componentes locais do Site Recovery**: Você precisa de uma máquina que execute os componentes locais do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="bc3fa-114">**Pré-requisitos do VMware local**: Você precisa configurar as contas para que o Site Recovery possa acessar os servidores e VMs do VMware.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-114">**On-premises VMware prerequisites**: You need to set up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="bc3fa-115">**VMs replicadas**: As VMs que você deseja replicar precisam atender aos requisitos do Azure e ter o componente de serviço de Mobilidade instalado.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-115">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements, and have the Mobility service component installed.</span></span>

<span data-ttu-id="bc3fa-116">[Etapa 2: Examinar os pré-requisitos e as limitações](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="bc3fa-116">Go to [Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="bc3fa-117">Etapa 3: Planejar a capacidade</span><span class="sxs-lookup"><span data-stu-id="bc3fa-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="bc3fa-118">Se você estiver fazendo uma implantação completa, precisará descobrir quais recursos de replicação serão necessários.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-118">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="bc3fa-119">Há algumas ferramentas disponíveis para ajudá-lo a fazer isso.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-119">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="bc3fa-120">Vá para a Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-120">Go to Step 2.</span></span> <span data-ttu-id="bc3fa-121">Se estiver fazendo uma configuração rápida para testar o ambiente, ignore esta etapa.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-121">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="bc3fa-122">Ir para a [Etapa 3: Planejar a capacidade](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="bc3fa-122">Go to [Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="bc3fa-123">Etapa 4: Planejar a rede</span><span class="sxs-lookup"><span data-stu-id="bc3fa-123">Step 4: Plan networking</span></span>

<span data-ttu-id="bc3fa-124">Você precisa fazer um planejamento de rede para garantir que as VMs do Azure serão conectadas a redes após o failover e que elas têm os endereços IP corretos.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-124">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="bc3fa-125">Ir para a [Etapa 4: Planejar a rede](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="bc3fa-125">Go to [Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="bc3fa-126">Etapa 5: Preparar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="bc3fa-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="bc3fa-127">Configure as redes e o armazenamento do Azure antes de começar.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="bc3fa-128">Você pode fazer isso durante a implantação, mas recomendamos fazer isso antes de começar.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="bc3fa-129">Ir para a [Etapa 5: Preparar o Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="bc3fa-129">Go to [Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="bc3fa-130">Etapa 6: Preparar o VMware</span><span class="sxs-lookup"><span data-stu-id="bc3fa-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="bc3fa-131">Você precisa configurar contas que o Site Recovery usará para:</span><span class="sxs-lookup"><span data-stu-id="bc3fa-131">You need to set up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="bc3fa-132">Acessar os servidores de virtualização do VMware para detectar automaticamente as VMs.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-132">Access VMware virtualization servers to automatically detect VMs.</span></span>
- <span data-ttu-id="bc3fa-133">Acessar as VMs para instalar o serviço de Mobilidade.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-133">Access VMs to install the Mobility service.</span></span> <span data-ttu-id="bc3fa-134">Cada VM que você deseja replicar deve ter o agente de serviço de Mobilidade instalado antes de habilitar a replicação para ele.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-134">Each VM you want to replicate must have the Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="bc3fa-135">Vá para a [Etapa 6: Preparar o VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="bc3fa-135">Go to [Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="bc3fa-136">Etapa 7: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="bc3fa-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="bc3fa-137">Você precisa configurar um cofre dos Serviços de Recuperação para orquestrar e gerenciar a replicação.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-137">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="bc3fa-138">Ao configurar o cofre, você especifica o que deseja replicar e o local para o qual deseja replicá-lo.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-138">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="bc3fa-139">Vá para a [Etapa 7: Configurar um cofre](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="bc3fa-139">Go to [Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="bc3fa-140">Etapa 8: Definir as configurações de origem e destino</span><span class="sxs-lookup"><span data-stu-id="bc3fa-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="bc3fa-141">Configure a origem e o destino usados para a replicação.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-141">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="bc3fa-142">Definir as configurações de origem inclui executar a Instalação Unificada para instalar os componentes locais do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-142">Setting up source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="bc3fa-143">Ir para a [Etapa 8: Configurar a origem e o destino](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="bc3fa-143">Go to [Step 8: Set up the source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="bc3fa-144">Etapa 9: Definir uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="bc3fa-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="bc3fa-145">Configure uma política para especificar as configurações de replicação das VMs do VMware no cofre.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-145">You set up a policy to specify replication settings for VMware VMs in the vault.</span></span>

<span data-ttu-id="bc3fa-146">Vá para a [Etapa 9: Configurar uma política de replicação](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="bc3fa-146">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="bc3fa-147">Etapa 10: Instalar o serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="bc3fa-147">Step 10: Install the Mobility service</span></span>

<span data-ttu-id="bc3fa-148">O serviço de Mobilidade deve ser instalado em cada VM que você deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-148">The Mobility service must be installed on each VM you want to replicate.</span></span> <span data-ttu-id="bc3fa-149">Há algumas maneiras de configurar o serviço com a instalação por push ou pull.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-149">There are a few ways to set up the service with push or pull installation.</span></span>

<span data-ttu-id="bc3fa-150">Vá para a [Etapa 10: Instalar o serviço de Mobilidade](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="bc3fa-150">Go to [Step 10: Install the Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="bc3fa-151">Etapa 11: Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="bc3fa-151">Step 11: Enable replication</span></span>

<span data-ttu-id="bc3fa-152">Depois que o serviço de Mobilidade estiver em execução em uma VM, você pode habilitar a replicação para ele.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-152">After the Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="bc3fa-153">Depois de habilitar, a replicação inicial da VM ocorre.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-153">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="bc3fa-154">Vá para a [Etapa 11: Habilitar a replicação](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="bc3fa-154">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="bc3fa-155">Etapa 12: Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="bc3fa-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="bc3fa-156">Após a conclusão da replicação inicial e a replicação delta estiver em execução, você poderá executar um failover de teste para verificar se tudo está funcionando como esperado.</span><span class="sxs-lookup"><span data-stu-id="bc3fa-156">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="bc3fa-157">Vá para a [Etapa 12: Executar um failover de teste](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="bc3fa-157">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
