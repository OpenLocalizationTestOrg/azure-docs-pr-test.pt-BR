---
title: "Migrar VMs IaaS do Azure entre regiões do Azure | Microsoft Docs"
description: "Use o Azure Site Recovery para migrar máquinas virtuais IaaS do Azure de uma região do Azure para outra."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: ef2972c077a2b1dd2b2fd6ce53cc6560520ea870
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="6d307-103">Migrar máquinas virtuais IaaS do Azure entre regiões do Azure com o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="6d307-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="6d307-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6d307-104">Overview</span></span>
<span data-ttu-id="6d307-105">Bem-vindo ao Azure Site Recovery!</span><span class="sxs-lookup"><span data-stu-id="6d307-105">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="6d307-106">Use este artigo se você deseja migrar VMs do Azure entre regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d307-106">Use this article if you want to migrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="6d307-107">Antes de começar, observe que:</span><span class="sxs-lookup"><span data-stu-id="6d307-107">Before you start, note that:</span></span>

* <span data-ttu-id="6d307-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: Azure Resource Manager e Clássico.</span><span class="sxs-lookup"><span data-stu-id="6d307-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="6d307-109">O Azure também tem dois portais – o portal clássico do Azure, que dá suporte ao modelo de implantação clássica, e o portal do Azure, com suporte para ambos os modelos de implantação.</span><span class="sxs-lookup"><span data-stu-id="6d307-109">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="6d307-110">As etapas básicas para migração são as mesmas se você estiver configurando o Site Recovery no Resource Manager ou no clássico.</span><span class="sxs-lookup"><span data-stu-id="6d307-110">The basic steps for migration are the same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="6d307-111">No entanto, as instruções de interface do usuário e capturas de tela neste artigo são relevantes para o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d307-111">However the UI instructions and screenshots in this article are relevant for the Azure portal.</span></span>
* <span data-ttu-id="6d307-112">**No momento, você pode apenas migrar de uma região para outra. Você pode executar o failover de VMs de uma região do Azure para outra, mas não pode executar o failback delas novamente.**</span><span class="sxs-lookup"><span data-stu-id="6d307-112">**Currently you can only migrate from one region to another. You can fail over VMs from one Azure region to another, but you can't fail them back again.**</span></span>

<span data-ttu-id="6d307-113">Publique eventuais comentários ou perguntas no final deste artigo ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6d307-113">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d307-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6d307-114">Prerequisites</span></span>
<span data-ttu-id="6d307-115">Aqui está o que você precisa para essa implantação:</span><span class="sxs-lookup"><span data-stu-id="6d307-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="6d307-116">**Máquinas virtuais IaaS**: as VMs que você deseja migrar.</span><span class="sxs-lookup"><span data-stu-id="6d307-116">**IaaS virtual machines**: The VMs you want to migrate.</span></span> <span data-ttu-id="6d307-117">Você pode migrar essas VMs tratando-as como computadores físicos.</span><span class="sxs-lookup"><span data-stu-id="6d307-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="6d307-118">Etapas de implantação.</span><span class="sxs-lookup"><span data-stu-id="6d307-118">Deployment steps</span></span>
<span data-ttu-id="6d307-119">Esta seção descreve as etapas de implantação no novo Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d307-119">This section describes the deployment steps in the new Azure portal.</span></span>

1. <span data-ttu-id="6d307-120">[Crie um cofre](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="6d307-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="6d307-121">[Habilite a replicação](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="6d307-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="6d307-122">Habilite a replicação para as VMs que você deseja migrar e escolha o Azure como fonte.</span><span class="sxs-lookup"><span data-stu-id="6d307-122">Enable replication for the VMs you want to migrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="6d307-123">[ Execute um failover não planejado](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="6d307-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="6d307-124">Depois que a replicação inicial for concluída, você poderá executar um failover não planejado de uma região do Azure para outra.</span><span class="sxs-lookup"><span data-stu-id="6d307-124">After initial replication is complete, you can run an unplanned failover from one Azure region to another.</span></span> <span data-ttu-id="6d307-125">Se preferir, você pode criar um plano de recuperação e executar um failover não planejado para migrar várias máquinas virtuais entre regiões.</span><span class="sxs-lookup"><span data-stu-id="6d307-125">Optionally, you can create a recovery plan and run an unplanned failover, to migrate multiple virtual machines between regions.</span></span> <span data-ttu-id="6d307-126">[Saiba mais](site-recovery-create-recovery-plans.md) sobre planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="6d307-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d307-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d307-127">Next steps</span></span>
<span data-ttu-id="6d307-128">Saiba mais sobre outros cenários de replicação em [O que é o Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6d307-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
