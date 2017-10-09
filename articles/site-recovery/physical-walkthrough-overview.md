---
title: "aaaReplicate físico tooAzure de servidores com o Azure Site Recovery local | Microsoft Docs"
description: "Fornece uma visão geral das etapas de saudação para replicar as cargas de trabalho em execução no local Windows/Linux servidores físicos tooAzure com hello serviço Azure Site Recovery."
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
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a><span data-ttu-id="99c25-103">Replicar tooAzure servidores físicos com a recuperação de Site</span><span class="sxs-lookup"><span data-stu-id="99c25-103">Replicate physical servers tooAzure with Site Recovery</span></span>

<span data-ttu-id="99c25-104">Este artigo fornece uma visão geral da saudação etapas necessárias tooreplicate local Windows/Linux servidores físicos tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="99c25-104">This article provides an overview of hello steps required tooreplicate on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="99c25-105">Etapa 1: Examinar a arquitetura e os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="99c25-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="99c25-106">Antes de iniciar a implantação, examine a arquitetura de cenário de saudação e certifique-se de que entender todos os componentes de saudação é necessário tooset a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="99c25-106">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need tooset up hello deployment.</span></span>

<span data-ttu-id="99c25-107">Vá muito[etapa 1: revisar arquitetura Olá](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="99c25-107">Go too[Step 1: Review hello architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="99c25-108">Etapa 2: Examinar os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="99c25-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="99c25-109">Certifique-se de que ter Olá pré-requisitos em vigor para cada componente de implantação:</span><span class="sxs-lookup"><span data-stu-id="99c25-109">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="99c25-110">**Pré-requisitos do Azure**: você precisa de uma conta do Microsoft Azure, redes do Azure e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99c25-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="99c25-111">**Componentes locais do Site Recovery**: Você precisa de uma máquina que execute os componentes locais do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="99c25-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="99c25-112">**As máquinas replicadas**: precisam de servidores que você deseja tooreplicate toocomply com locais e os requisitos do Azure.</span><span class="sxs-lookup"><span data-stu-id="99c25-112">**Replicated machines**: Servers you want tooreplicate need toocomply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="99c25-113">Vá muito[etapa 2: analisar os pré-requisitos e limitações](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="99c25-113">Go too[Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="99c25-114">Etapa 3: Planejar a capacidade</span><span class="sxs-lookup"><span data-stu-id="99c25-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="99c25-115">Se você estiver fazendo uma implantação completa, que você precisa toofigure quais recursos de replicação é necessário.</span><span class="sxs-lookup"><span data-stu-id="99c25-115">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="99c25-116">Se você estiver fazendo uma rápida de configurar o ambiente de saudação tootest, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="99c25-116">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="99c25-117">Vá muito[etapa 3: planejar a capacidade](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="99c25-117">Go too[Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="99c25-118">Etapa 4: Planejar a rede</span><span class="sxs-lookup"><span data-stu-id="99c25-118">Step 4: Plan networking</span></span>

<span data-ttu-id="99c25-119">É necessário toodo algum planejamento tooensure que máquinas virtuais do Azure são conectados toonetworks após o failover, e que se eles têm Olá direito de endereços IP da rede.</span><span class="sxs-lookup"><span data-stu-id="99c25-119">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="99c25-120">Vá muito[etapa 4: planejar a rede](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="99c25-120">Go too[Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="99c25-121">Etapa 5: Preparar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="99c25-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="99c25-122">Configure as redes e o armazenamento do Azure antes de começar.</span><span class="sxs-lookup"><span data-stu-id="99c25-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="99c25-123">Vá muito[etapa 5: preparar o Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="99c25-123">Go too[Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="99c25-124">Etapa 6: Configurar um cofre</span><span class="sxs-lookup"><span data-stu-id="99c25-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="99c25-125">Configurar um tooorchestrate de Cofre de serviços de recuperação e gerenciar a replicação.</span><span class="sxs-lookup"><span data-stu-id="99c25-125">You set up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="99c25-126">Quando você configura o cofre hello, especifique o que você deseja tooreplicate, e onde você deseja tooreplicate-o para.</span><span class="sxs-lookup"><span data-stu-id="99c25-126">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="99c25-127">Vá muito[etapa 6: configurar um cofre](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="99c25-127">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="99c25-128">Etapa 7: Definir as configurações de origem e destino</span><span class="sxs-lookup"><span data-stu-id="99c25-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="99c25-129">Definir configurações para Olá fonte e de destino site (Azure).</span><span class="sxs-lookup"><span data-stu-id="99c25-129">Configure settings for hello source and target (Azure) site.</span></span> <span data-ttu-id="99c25-130">Configurações de origem inclui a execução tooinstall de instalação do Unified componentes de recuperação de Site local hello.</span><span class="sxs-lookup"><span data-stu-id="99c25-130">Source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="99c25-131">Vá muito[etapa 7: configurar Olá origem e destino](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="99c25-131">Go too[Step 7: Set up hello source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="99c25-132">Etapa 8: Configurar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="99c25-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="99c25-133">Configurar uma política toospecify físicos como servidores devem replicar.</span><span class="sxs-lookup"><span data-stu-id="99c25-133">You set up a policy toospecify how physical servers should replicate.</span></span>

<span data-ttu-id="99c25-134">Vá muito[etapa 8: configurar uma política de replicação](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="99c25-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="99c25-135">Etapa 9: Instale o serviço de mobilidade Olá</span><span class="sxs-lookup"><span data-stu-id="99c25-135">Step 9: Install hello Mobility service</span></span>

<span data-ttu-id="99c25-136">Olá serviço de mobilidade deve ser instalado em cada servidor que você deseja tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="99c25-136">hello Mobility service must be installed on each server you want tooreplicate.</span></span> <span data-ttu-id="99c25-137">Há alguns tooset maneiras serviço hello, com a instalação por push ou pull.</span><span class="sxs-lookup"><span data-stu-id="99c25-137">There are a few ways tooset up hello service, with push or pull installation.</span></span>

<span data-ttu-id="99c25-138">Vá muito[etapa 9: Instale o serviço de mobilidade Olá](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="99c25-138">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="99c25-139">Etapa 10: Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="99c25-139">Step 10: Enable replication</span></span>

<span data-ttu-id="99c25-140">Olá serviço de mobilidade em execução em um servidor, você pode habilitar a replicação para ele.</span><span class="sxs-lookup"><span data-stu-id="99c25-140">After hello Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="99c25-141">Depois de habilitar, ocorre a replicação inicial dos Olá VM.</span><span class="sxs-lookup"><span data-stu-id="99c25-141">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="99c25-142">Vá muito[etapa 10: habilitar a replicação](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="99c25-142">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="99c25-143">Etapa 11: Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="99c25-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="99c25-144">Após a conclusão da replicação inicial e a replicação delta está em execução, você pode executar um toomake de failover de teste se que tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="99c25-144">After initial replication finishes and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="99c25-145">Vá muito[etapa 11: executar um failover de teste](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="99c25-145">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

