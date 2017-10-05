---
title: "Replicar servidores físicos locais no Azure com o Azure Site Recovery | Microsoft Docs"
description: "Fornece uma visão geral das etapas para replicação de cargas de trabalho em execução em servidores físicos locais com Windows/Linux para o Azure com o serviço Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 0a09b35e98dc0b2f5283c2a707a3a2b8ac9a39f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-physical-servers-to-azure-with-site-recovery"></a><span data-ttu-id="badf6-103">Replicar servidores físicos no Azure com o Site Recovery</span><span class="sxs-lookup"><span data-stu-id="badf6-103">Replicate physical servers to Azure with Site Recovery</span></span>

<span data-ttu-id="badf6-104">Este artigo fornece uma visão geral das etapas necessárias para replicar servidores físicos locais com Windows/Linux no Azure usando o serviço do [Azure Site Recovery](site-recovery-overview.md) no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="badf6-104">This article provides an overview of the steps required to replicate on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="badf6-105">Etapa 1: Examinar a arquitetura e os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="badf6-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="badf6-106">Antes de iniciar a implantação, examine a arquitetura do cenário e entenda todos os componentes que você precisa configurar na implantação.</span><span class="sxs-lookup"><span data-stu-id="badf6-106">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to set up the deployment.</span></span>

<span data-ttu-id="badf6-107">Ir para a [Etapa 1: Examinar a arquitetura](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="badf6-107">Go to [Step 1: Review the architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="badf6-108">Etapa 2: Examinar os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="badf6-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="badf6-109">Verifique se os pré-requisitos estão em vigor para cada componente de implantação:</span><span class="sxs-lookup"><span data-stu-id="badf6-109">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="badf6-110">**Pré-requisitos do Azure**: você precisa de uma conta do Microsoft Azure, redes do Azure e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="badf6-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="badf6-111">**Componentes locais do Site Recovery**: Você precisa de uma máquina que execute os componentes locais do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="badf6-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="badf6-112">**Máquinas replicadas**: os servidores que você deseja replicar precisam atender aos requisitos locais e do Azure.</span><span class="sxs-lookup"><span data-stu-id="badf6-112">**Replicated machines**: Servers you want to replicate need to comply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="badf6-113">Acesse [Etapa 2: Examinar os pré-requisitos e as limitações](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="badf6-113">Go to [Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="badf6-114">Etapa 3: Planejar a capacidade</span><span class="sxs-lookup"><span data-stu-id="badf6-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="badf6-115">Se você estiver fazendo uma implantação completa, precisará descobrir quais recursos de replicação serão necessários.</span><span class="sxs-lookup"><span data-stu-id="badf6-115">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="badf6-116">Se estiver fazendo uma configuração rápida para testar o ambiente, ignore esta etapa.</span><span class="sxs-lookup"><span data-stu-id="badf6-116">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="badf6-117">Ir para a [Etapa 3: Planejar a capacidade](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="badf6-117">Go to [Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="badf6-118">Etapa 4: Planejar a rede</span><span class="sxs-lookup"><span data-stu-id="badf6-118">Step 4: Plan networking</span></span>

<span data-ttu-id="badf6-119">Você precisa fazer um planejamento de rede para garantir que as VMs do Azure serão conectadas a redes após o failover e que elas têm os endereços IP corretos.</span><span class="sxs-lookup"><span data-stu-id="badf6-119">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="badf6-120">Ir para a [Etapa 4: Planejar a rede](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="badf6-120">Go to [Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="badf6-121">Etapa 5: Preparar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="badf6-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="badf6-122">Configure as redes e o armazenamento do Azure antes de começar.</span><span class="sxs-lookup"><span data-stu-id="badf6-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="badf6-123">Ir para a [Etapa 5: Preparar o Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="badf6-123">Go to [Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="badf6-124">Etapa 6: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="badf6-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="badf6-125">Configure um cofre dos Serviços de Recuperação para orquestrar e gerenciar a replicação.</span><span class="sxs-lookup"><span data-stu-id="badf6-125">You set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="badf6-126">Ao configurar o cofre, você especifica o que deseja replicar e o local para o qual deseja replicá-lo.</span><span class="sxs-lookup"><span data-stu-id="badf6-126">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="badf6-127">Vá para a [Etapa 6: configurar um cofre](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="badf6-127">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="badf6-128">Etapa 7: Definir as configurações de origem e destino</span><span class="sxs-lookup"><span data-stu-id="badf6-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="badf6-129">Definir configurações para o site de origem e de destino (Azure).</span><span class="sxs-lookup"><span data-stu-id="badf6-129">Configure settings for the source and target (Azure) site.</span></span> <span data-ttu-id="badf6-130">As configurações de origem incluem executar a Instalação Unificada para instalar os componentes locais do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="badf6-130">Source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="badf6-131">Acesse a [Etapa 7: Configurar a origem e o destino](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="badf6-131">Go to [Step 7: Set up the source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="badf6-132">Etapa 8: Configurar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="badf6-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="badf6-133">Configure uma política para especificar como os servidores físicos devem replicar.</span><span class="sxs-lookup"><span data-stu-id="badf6-133">You set up a policy to specify how physical servers should replicate.</span></span>

<span data-ttu-id="badf6-134">Acesse a [Etapa 8: Configurar uma política de replicação](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="badf6-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="badf6-135">Etapa 9: instalar o Serviço de mobilidade manualmente</span><span class="sxs-lookup"><span data-stu-id="badf6-135">Step 9: Install the Mobility service</span></span>

<span data-ttu-id="badf6-136">O serviço de mobilidade deve ser instalado em cada servidor que você deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="badf6-136">The Mobility service must be installed on each server you want to replicate.</span></span> <span data-ttu-id="badf6-137">Há algumas maneiras de configurar o serviço com a instalação por push ou pull.</span><span class="sxs-lookup"><span data-stu-id="badf6-137">There are a few ways to set up the service, with push or pull installation.</span></span>

<span data-ttu-id="badf6-138">Ir para a [Etapa 9: Instalar o Serviço de mobilidade](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="badf6-138">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="badf6-139">Etapa 10: Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="badf6-139">Step 10: Enable replication</span></span>

<span data-ttu-id="badf6-140">Depois que o serviço de Mobilidade estiver em execução em um servidor, você pode habilitar a replicação para ele.</span><span class="sxs-lookup"><span data-stu-id="badf6-140">After the Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="badf6-141">Depois de habilitar, a replicação inicial da VM ocorre.</span><span class="sxs-lookup"><span data-stu-id="badf6-141">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="badf6-142">Acesse a [Etapa 10: Habilitar a replicação](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="badf6-142">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="badf6-143">Etapa 11: Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="badf6-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="badf6-144">Após a conclusão da replicação inicial e a replicação delta estiver em execução, você poderá executar um failover de teste para verificar se tudo está funcionando como esperado.</span><span class="sxs-lookup"><span data-stu-id="badf6-144">After initial replication finishes and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="badf6-145">Acesse a [Etapa 11: Executar um failover de teste](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="badf6-145">Go to [Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

