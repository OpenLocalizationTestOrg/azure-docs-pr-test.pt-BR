---
title: "arquitetura de saudação aaaReview para o site secundário do Hyper-V replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Este artigo fornece uma visão geral da arquitetura de saudação para replicar máquinas virtuais do Hyper-V tooa secundário System Center VMM site local com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="968e4-103">Etapa 1: Revisar arquitetura Olá para o site secundário do Hyper-V replicação tooa</span><span class="sxs-lookup"><span data-stu-id="968e4-103">Step 1: Review hello architecture for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="968e4-104">Este artigo descreve os componentes de saudação e processos envolvidos ao replicar máquinas de virtuais (VMs) Hyper-V nas nuvens do System Center Virtual Machine Manager (VMM), site VMM secundário tooa usando Olá local [Azure Site Recovery](site-recovery-overview.md)serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="968e4-104">This article describes hello components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM site using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="968e4-105">Lançar os comentários na parte inferior deste artigo ou de saudação do hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="968e4-105">Post any comments at hello bottom of this article, or in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="968e4-106">Componentes de arquitetura</span><span class="sxs-lookup"><span data-stu-id="968e4-106">Architectural components</span></span>

<span data-ttu-id="968e4-107">Aqui está o que você precisa para a replicação de site VMM secundário de tooa VMs Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="968e4-107">Here's what you need for replicating Hyper-V VMs tooa secondary VMM site.</span></span>

<span data-ttu-id="968e4-108">**Componente**</span><span class="sxs-lookup"><span data-stu-id="968e4-108">**Component**</span></span> | <span data-ttu-id="968e4-109">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="968e4-109">**Location**</span></span> | <span data-ttu-id="968e4-110">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="968e4-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="968e4-111">**As tabelas**</span><span class="sxs-lookup"><span data-stu-id="968e4-111">**Azure**</span></span> | <span data-ttu-id="968e4-112">Assinatura no Azure.</span><span class="sxs-lookup"><span data-stu-id="968e4-112">Subscription in Azure.</span></span> | <span data-ttu-id="968e4-113">Crie um cofre de serviços de recuperação no hello assinatura do Azure, tooorchestrate e gerenciar a replicação entre os locais do VMM.</span><span class="sxs-lookup"><span data-stu-id="968e4-113">You create a Recovery Services vault in hello Azure subscription, tooorchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="968e4-114">**Servidor VMM**</span><span class="sxs-lookup"><span data-stu-id="968e4-114">**VMM server**</span></span> | <span data-ttu-id="968e4-115">Você precisa de locais primário e secundário para o VMM.</span><span class="sxs-lookup"><span data-stu-id="968e4-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="968e4-116">É recomendável um servidor do VMM no site primário hello e um no site secundário Olá</span><span class="sxs-lookup"><span data-stu-id="968e4-116">We recommend a VMM server in hello primary site, and one in hello secondary site</span></span> 
<span data-ttu-id="968e4-117">**Servidor Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="968e4-117">**Hyper-V server**</span></span> |  <span data-ttu-id="968e4-118">Um ou mais servidores Hyper-V host nas nuvens de saudação primários e secundários do VMM.</span><span class="sxs-lookup"><span data-stu-id="968e4-118">One or more Hyper-V host servers in hello primary and secondary VMM clouds.</span></span> | <span data-ttu-id="968e4-119">Dados são replicados entre Olá servidores primários e secundários Hyper-V host via LAN hello ou VPN, usando a autenticação Kerberos ou certificados.</span><span class="sxs-lookup"><span data-stu-id="968e4-119">Data is replicated between hello primary and secondary Hyper-V host servers over hello LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="968e4-120">**VMs Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="968e4-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="968e4-121">No servidor de host do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="968e4-121">On Hyper-V host server.</span></span> | <span data-ttu-id="968e4-122">servidor de host de origem Olá deve ter pelo menos uma VM que você deseja tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="968e4-122">hello source host server should have at least one VM that you want tooreplicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="968e4-123">Processo de replicação</span><span class="sxs-lookup"><span data-stu-id="968e4-123">Replication process</span></span>

1. <span data-ttu-id="968e4-124">Configurar Olá conta do Azure, crie um cofre de serviços de recuperação e especificar o que você deseja tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="968e4-124">You set up hello Azure account, create a Recovery Services vault, and specify what you want tooreplicate.</span></span>
2. <span data-ttu-id="968e4-125">Configurar o hello origem e destino as configurações de replicação, que inclui a instalação Olá provedor Azure Site Recovery em servidores do VMM e o agente de serviços de recuperação do Microsoft Azure Olá em cada host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="968e4-125">You configure hello source and target replication settings, which includes installing hello Azure Site Recovery Provider on VMM servers, and hello Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="968e4-126">Você criar uma política de replicação para a fonte de saudação nuvem do VMM.</span><span class="sxs-lookup"><span data-stu-id="968e4-126">You create a replication policy for hello source VMM cloud.</span></span> <span data-ttu-id="968e4-127">política de saudação é aplicado tooall as VMs localizadas nos hosts na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="968e4-127">hello policy is applied tooall VMs located on hosts in hello cloud.</span></span>
4. <span data-ttu-id="968e4-128">Habilitar replicação para cada VMM e ocorre a replicação inicial de uma VM acordo com as configurações de saudação que você escolher.</span><span class="sxs-lookup"><span data-stu-id="968e4-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with hello settings you choose.</span></span>
5. <span data-ttu-id="968e4-129">Após a replicação inicial, a replicação de alterações delta começa.</span><span class="sxs-lookup"><span data-stu-id="968e4-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="968e4-130">As alterações acompanhadas para um item são mantidas em um arquivo .hrl.</span><span class="sxs-lookup"><span data-stu-id="968e4-130">Tracked changes for an item are held in a .hrl file.</span></span>


![Tooon local no local](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="968e4-132">Processo de failover e failback</span><span class="sxs-lookup"><span data-stu-id="968e4-132">Failover and failback process</span></span>

1. <span data-ttu-id="968e4-133">Você pode executar um [failover](site-recovery-failover.md) planejado ou não planejado entre sites locais.</span><span class="sxs-lookup"><span data-stu-id="968e4-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="968e4-134">Se você executar um failover planejado, máquinas virtuais de origem são encerrados tooensure sem perda de dados.</span><span class="sxs-lookup"><span data-stu-id="968e4-134">If you run a planned failover, then source VMs are shut down tooensure no data loss.</span></span>
2. <span data-ttu-id="968e4-135">Você pode fazer o failover de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md) tooorchestrate failover de várias máquinas.</span><span class="sxs-lookup"><span data-stu-id="968e4-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) tooorchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="968e4-136">Se você executar um failover não planejado tooa site secundário, depois de executar failover em máquinas Olá no local secundário Olá não está habilitado para proteção ou replicação.</span><span class="sxs-lookup"><span data-stu-id="968e4-136">If you perform an unplanned failover tooa secondary site, after hello failover machines in hello secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="968e4-137">Se você tiver executado um failover planejado, após o failover hello, as máquinas no local secundário Olá são protegidas.</span><span class="sxs-lookup"><span data-stu-id="968e4-137">If you ran a planned failover, after hello failover, machines in hello secondary location are protected.</span></span>
5. <span data-ttu-id="968e4-138">Em seguida, você confirmar Olá failover toostart acessando Olá carga de trabalho da réplica Olá VM.</span><span class="sxs-lookup"><span data-stu-id="968e4-138">Then, you commit hello failover toostart accessing hello workload from hello replica VM.</span></span>
6. <span data-ttu-id="968e4-139">Quando seu site primário está disponível novamente, você pode iniciar tooreplicate replicação inversa da saudação site secundário toohello primário.</span><span class="sxs-lookup"><span data-stu-id="968e4-139">When your primary site is available again, you initiate reverse replication tooreplicate from hello secondary site toohello primary.</span></span> <span data-ttu-id="968e4-140">Replicação inversa coloca máquinas virtuais de saudação em um estado protegido, mas o datacenter secundário Olá ainda é local ativo hello.</span><span class="sxs-lookup"><span data-stu-id="968e4-140">Reverse replication brings hello virtual machines into a protected state, but hello secondary datacenter is still hello active location.</span></span>
7. <span data-ttu-id="968e4-141">site primário do hello toomake em local ativo Olá novamente, você iniciar um failover planejado de tooprimary secundário, seguido de outra replicação inversa.</span><span class="sxs-lookup"><span data-stu-id="968e4-141">toomake hello primary site into hello active location again, you initiate a planned failover from secondary tooprimary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="968e4-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="968e4-142">Next steps</span></span>

<span data-ttu-id="968e4-143">Vá muito[etapa 2: Examinar Olá pré-requisitos e limitações](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="968e4-143">Go too[Step 2: Review hello prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
