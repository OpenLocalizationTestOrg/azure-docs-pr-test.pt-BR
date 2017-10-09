---
title: "aaaReplicate VMs do Azure entre regiões do Azure | Microsoft Docs"
description: "Resume Olá etapas necessárias tooreplicate VMs do Azure entre regiões do Azure com o serviço do Azure Site Recovery Olá no hello portal do Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="0c56f-103">Você pode replicar VMs do Azure entre regiões usando o Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0c56f-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="0c56f-104">Este artigo fornece uma visão geral da saudação etapas necessárias tooreplicate máquinas virtuais (VMs) do Azure em uma região do Azure tooAzure VMs em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="0c56f-104">This article provides an overview of hello steps required tooreplicate Azure virtual machines (VMs) in one Azure region tooAzure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="0c56f-105">Atualmente, a replicação de VM do Azure está em versão prévia.</span><span class="sxs-lookup"><span data-stu-id="0c56f-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="0c56f-106">Postar perguntas e comentários na parte inferior da saudação deste artigo ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0c56f-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="0c56f-107">Etapa 1: revisar a arquitetura</span><span class="sxs-lookup"><span data-stu-id="0c56f-107">Step 1: Review architecture</span></span>

<span data-ttu-id="0c56f-108">Antes de iniciar a implantação, revise Olá cenário arquitetura e componentes Olá necessários toodeploy.</span><span class="sxs-lookup"><span data-stu-id="0c56f-108">Before you start deployment, review hello scenario architecture, and hello components you need toodeploy.</span></span>

<span data-ttu-id="0c56f-109">Vá muito[etapa 1: revisar arquitetura Olá](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="0c56f-109">Go too[Step 1: Review hello architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="0c56f-110">Etapa 2: Examinar os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0c56f-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="0c56f-111">Verifique que você tenha Olá pré-requisitos do Azure em locais, incluindo uma assinatura, redes virtuais, contas de armazenamento e os requisitos de VM.</span><span class="sxs-lookup"><span data-stu-id="0c56f-111">Check that you have hello Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="0c56f-112">Vá muito[etapa 2: verificar os pré-requisitos e limitações](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="0c56f-112">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="0c56f-113">Etapa 3: Planejar a rede</span><span class="sxs-lookup"><span data-stu-id="0c56f-113">Step 3: Plan networking</span></span>

<span data-ttu-id="0c56f-114">Verifique se a conectividade de saída está configurada em VMs do Azure que você deseja tooreplicate e conexões locais são configurados.</span><span class="sxs-lookup"><span data-stu-id="0c56f-114">Check that outbound connectivity is set up on Azure VMs you want tooreplicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="0c56f-115">Vá muito[etapa 4: planejar a rede](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="0c56f-115">Go too[Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="0c56f-116">Etapa 4: criar um cofre</span><span class="sxs-lookup"><span data-stu-id="0c56f-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="0c56f-117">Necessário tooset a um tooorchestrate de Cofre de serviços de recuperação e gerenciar a replicação e especificar a região de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c56f-117">You need tooset up a Recovery Services vault tooorchestrate and manage replication, and specify hello source region.</span></span>

<span data-ttu-id="0c56f-118">Vá muito[etapa 4: criar um cofre](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="0c56f-118">Go too[Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="0c56f-119">Etapa 5: habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="0c56f-119">Step 5: Enable replication</span></span>


<span data-ttu-id="0c56f-120">replicação tooenable, definir configurações de local de destino, configurar uma política de replicação e selecione Olá VMs do Azure que você deseja tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="0c56f-120">tooenable replication, you configure target location settings, set up a replication policy, and select hello Azure VMs that you want tooreplicate.</span></span> <span data-ttu-id="0c56f-121">Depois de habilitar, ocorre a replicação inicial dos Olá VM.</span><span class="sxs-lookup"><span data-stu-id="0c56f-121">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="0c56f-122">Vá muito[etapa 5: habilitar a replicação](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="0c56f-122">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="0c56f-123">Etapa 6: executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="0c56f-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="0c56f-124">Após a conclusão da replicação inicial, e a replicação delta está em execução, você pode executar um toomake de failover de teste se que tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="0c56f-124">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="0c56f-125">Vá muito[etapa 6: executar um failover de teste](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="0c56f-125">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


