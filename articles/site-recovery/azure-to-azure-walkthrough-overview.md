---
title: "Replicar VMs do Azure entre regiões do Azure | Microsoft Docs'"
description: "Resume as etapas necessárias para replicar VMs do Azure entre regiões do Azure com o serviço do Azure Site Recovery no portal do Azure"
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
ms.openlocfilehash: 9258613161a61e36b1d0c5796d5763c916d66859
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="34b58-103">Você pode replicar VMs do Azure entre regiões usando o Site Recovery</span><span class="sxs-lookup"><span data-stu-id="34b58-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="34b58-104">Este artigo fornece uma visão geral das etapas necessárias para replicar VMs (máquinas virtuais) em uma região do Azure para VMs do Azure em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="34b58-104">This article provides an overview of the steps required to replicate Azure virtual machines (VMs) in one Azure region to Azure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="34b58-105">Atualmente, a replicação de VM do Azure está em versão prévia.</span><span class="sxs-lookup"><span data-stu-id="34b58-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="34b58-106">Publique perguntas e comentários na parte inferior deste artigo ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="34b58-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="34b58-107">Etapa 1: revisar a arquitetura</span><span class="sxs-lookup"><span data-stu-id="34b58-107">Step 1: Review architecture</span></span>

<span data-ttu-id="34b58-108">Antes de iniciar a implantação, revise a arquitetura do cenário e os componentes que você precisa implantar.</span><span class="sxs-lookup"><span data-stu-id="34b58-108">Before you start deployment, review the scenario architecture, and the components you need to deploy.</span></span>

<span data-ttu-id="34b58-109">Ir para a [Etapa 1: Examinar a arquitetura](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="34b58-109">Go to [Step 1: Review the architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="34b58-110">Etapa 2: Examinar os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="34b58-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="34b58-111">Verifique se possui os pré-requisitos do Azure implantados, incluindo uma assinatura, redes virtuais, contas de armazenamento e requisitos de VM.</span><span class="sxs-lookup"><span data-stu-id="34b58-111">Check that you have the Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="34b58-112">Ir para a [Etapa 2: Verificar os pré-requisitos e as limitações](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="34b58-112">Go to [Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="34b58-113">Etapa 3: Planejar rede</span><span class="sxs-lookup"><span data-stu-id="34b58-113">Step 3: Plan networking</span></span>

<span data-ttu-id="34b58-114">Verifique se a conectividade de saída está configurada nas VMs do Azure que você deseja replicar e que as conexões locais estão configuradas.</span><span class="sxs-lookup"><span data-stu-id="34b58-114">Check that outbound connectivity is set up on Azure VMs you want to replicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="34b58-115">Ir para a [Etapa 4: Planejar a rede](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="34b58-115">Go to [Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="34b58-116">Etapa 4: criar um cofre</span><span class="sxs-lookup"><span data-stu-id="34b58-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="34b58-117">É necessário configurar um cofre dos Serviços de Recuperação para orquestrar e gerenciar a replicação e especificar a região de origem.</span><span class="sxs-lookup"><span data-stu-id="34b58-117">You need to set up a Recovery Services vault to orchestrate and manage replication, and specify the source region.</span></span>

<span data-ttu-id="34b58-118">Acesse a [Etapa 4: criar um cofre](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="34b58-118">Go to [Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="34b58-119">Etapa 5: habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="34b58-119">Step 5: Enable replication</span></span>


<span data-ttu-id="34b58-120">Para habilitar a replicação, você define as configurações de localização de destino, configura uma política de replicação e seleciona as VMs do Azure que deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="34b58-120">To enable replication, you configure target location settings, set up a replication policy, and select the Azure VMs that you want to replicate.</span></span> <span data-ttu-id="34b58-121">Depois de habilitar, a replicação inicial da VM ocorre.</span><span class="sxs-lookup"><span data-stu-id="34b58-121">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="34b58-122">Acesse a [Etapa 5: habilitar a replicação](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="34b58-122">Go to [Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="34b58-123">Etapa 6: executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="34b58-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="34b58-124">Após a conclusão da replicação inicial e a replicação delta estiver em execução, você poderá executar um failover de teste para verificar se tudo está funcionando como esperado.</span><span class="sxs-lookup"><span data-stu-id="34b58-124">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="34b58-125">Acesse a [Etapa 6: executar um failover de teste](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="34b58-125">Go to [Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


