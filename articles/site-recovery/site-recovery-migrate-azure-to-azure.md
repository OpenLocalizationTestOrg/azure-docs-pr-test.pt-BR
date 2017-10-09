---
title: "aaaMigrate VMs Azure IaaS entre regiões do Azure | Microsoft Docs"
description: "Use o Azure Site Recovery toomigrate Azure máquinas virtuais de um tooanother de região do Azure."
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
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="dad2d-103">Migrar máquinas virtuais IaaS do Azure entre regiões do Azure com o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="dad2d-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="dad2d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="dad2d-104">Overview</span></span>
<span data-ttu-id="dad2d-105">Bem-vindo tooAzure recuperação de Site!</span><span class="sxs-lookup"><span data-stu-id="dad2d-105">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="dad2d-106">Use este artigo se você deseja toomigrate Azure VMs entre regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="dad2d-106">Use this article if you want toomigrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="dad2d-107">Antes de começar, observe que:</span><span class="sxs-lookup"><span data-stu-id="dad2d-107">Before you start, note that:</span></span>

* <span data-ttu-id="dad2d-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: Azure Resource Manager e Clássico.</span><span class="sxs-lookup"><span data-stu-id="dad2d-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="dad2d-109">Azure também tem dois portais – Olá portal clássico do Azure que dá suporte ao modelo de implantação clássico hello e Olá portal do Azure com suporte para ambos os modelos de implantação.</span><span class="sxs-lookup"><span data-stu-id="dad2d-109">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="dad2d-110">etapas básicas Olá para migração são Olá mesmo se você estiver configurando a recuperação de Site no Gerenciador de recursos ou em clássico.</span><span class="sxs-lookup"><span data-stu-id="dad2d-110">hello basic steps for migration are hello same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="dad2d-111">No entanto Olá instruções de interface do usuário e capturas de tela neste artigo são relevantes para Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dad2d-111">However hello UI instructions and screenshots in this article are relevant for hello Azure portal.</span></span>
* <span data-ttu-id="dad2d-112">**Atualmente só é possível migrar de uma região tooanother. Você pode fazer failover de máquinas virtuais de tooanother de uma região do Azure, mas você não pode failback-los novamente.**</span><span class="sxs-lookup"><span data-stu-id="dad2d-112">**Currently you can only migrate from one region tooanother. You can fail over VMs from one Azure region tooanother, but you can't fail them back again.**</span></span>

<span data-ttu-id="dad2d-113">Postar comentários e perguntas na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="dad2d-113">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dad2d-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dad2d-114">Prerequisites</span></span>
<span data-ttu-id="dad2d-115">Aqui está o que você precisa para essa implantação:</span><span class="sxs-lookup"><span data-stu-id="dad2d-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="dad2d-116">**Máquinas virtuais IaaS**: Olá VMs que você deseja toomigrate.</span><span class="sxs-lookup"><span data-stu-id="dad2d-116">**IaaS virtual machines**: hello VMs you want toomigrate.</span></span> <span data-ttu-id="dad2d-117">Você pode migrar essas VMs tratando-as como computadores físicos.</span><span class="sxs-lookup"><span data-stu-id="dad2d-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="dad2d-118">Etapas de implantação.</span><span class="sxs-lookup"><span data-stu-id="dad2d-118">Deployment steps</span></span>
<span data-ttu-id="dad2d-119">Esta seção descreve as etapas de implantação Olá no novo portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="dad2d-119">This section describes hello deployment steps in hello new Azure portal.</span></span>

1. <span data-ttu-id="dad2d-120">[Crie um cofre](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="dad2d-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="dad2d-121">[Habilite a replicação](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="dad2d-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="dad2d-122">Habilite a replicação para Olá VMs que você deseja toomigrate e escolha o Azure como origem.</span><span class="sxs-lookup"><span data-stu-id="dad2d-122">Enable replication for hello VMs you want toomigrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="dad2d-123">[ Execute um failover não planejado](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="dad2d-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="dad2d-124">Depois que a replicação inicial for concluída, você pode executar um failover não planejado de um tooanother de região do Azure.</span><span class="sxs-lookup"><span data-stu-id="dad2d-124">After initial replication is complete, you can run an unplanned failover from one Azure region tooanother.</span></span> <span data-ttu-id="dad2d-125">Opcionalmente, você pode criar um plano de recuperação e executar um failover não planejado, toomigrate várias máquinas virtuais entre regiões.</span><span class="sxs-lookup"><span data-stu-id="dad2d-125">Optionally, you can create a recovery plan and run an unplanned failover, toomigrate multiple virtual machines between regions.</span></span> <span data-ttu-id="dad2d-126">[Saiba mais](site-recovery-create-recovery-plans.md) sobre planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="dad2d-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dad2d-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dad2d-127">Next steps</span></span>
<span data-ttu-id="dad2d-128">Saiba mais sobre outros cenários de replicação em [O que é o Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="dad2d-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
