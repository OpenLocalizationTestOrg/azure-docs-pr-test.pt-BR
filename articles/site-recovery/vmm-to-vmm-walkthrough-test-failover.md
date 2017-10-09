---
title: "aaaRun um failover de teste para o site secundário do Hyper-V VM replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como toorun um failover de teste para a VM do Hyper-V replicação tooa System Center VMM secundário do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="ca2bb-103">Etapa 10: Executar um failover de teste para o site secundário do Hyper-V replicação tooa</span><span class="sxs-lookup"><span data-stu-id="ca2bb-103">Step 10: Run a test failover for Hyper-V replication tooa secondary site</span></span>


<span data-ttu-id="ca2bb-104">Após habilitar a replicação para máquinas virtuais de Hyper-V (VMs) [do Azure Site Recovery](site-recovery-overview.md), use toorun este artigo um failover de teste.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article toorun a test failover.</span></span> <span data-ttu-id="ca2bb-105">Um failover de teste verifica se a replicação está funcionando, sem afetar o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="ca2bb-106">Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ca2bb-106">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="ca2bb-107">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ca2bb-107">Before you start</span></span>

- <span data-ttu-id="ca2bb-108">Quando você estiver ativando um failover de teste, você pode especificar a réplica de teste de saudação do hello rede toowhich que VMs se conectará.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-108">When you're triggering a test failover, you can specify hello network toowhich hello test replica VMs will connect.</span></span> <span data-ttu-id="ca2bb-109">[Saiba mais](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) sobre opções de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about hello network options.</span></span>
- <span data-ttu-id="ca2bb-110">É recomendável não escolher uma rede que foi selecionada durante o mapeamento de rede.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="ca2bb-111">Olá instruções neste artigo descrevem como toofail em uma única VM.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-111">hello instructions in this article describe how toofail over a single VM.</span></span> <span data-ttu-id="ca2bb-112">Leia sobre [Criando planos de recuperação](site-recovery-create-recovery-plans.md) se você quiser toofail entre várias VMs juntos.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want toofail over multiple VMs together.</span></span>
- <span data-ttu-id="ca2bb-113">Leia sobre [limitações para failovers de teste](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="ca2bb-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="ca2bb-114">Olá, endereço IP fornecido tooa VM durante o failover de teste é Olá deve receber o mesmo endereço IP que Olá VM para um failover planejado ou não planejado (presumindo que o endereço IP de saudação está disponível na rede de failover de teste de saudação).</span><span class="sxs-lookup"><span data-stu-id="ca2bb-114">hello IP address given tooa VM during test failover is hello same IP address that hello VM would receive for a planned or unplanned failover (presuming that hello IP address is available in hello test failover network).</span></span> <span data-ttu-id="ca2bb-115">Se o endereço IP de saudação não está disponível na rede de failover de teste hello, Olá VM recebe outro endereço IP que está disponível na rede de failover de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-115">If hello IP address isn't available in hello test failover network, hello VM receives another IP address that is available in hello test failover network.</span></span>
- <span data-ttu-id="ca2bb-116">Se você quiser toodo um failover de teste em sua rede de produção, para validação completa da máquina de conectividade de rede de ponta a ponta, observe que:</span><span class="sxs-lookup"><span data-stu-id="ca2bb-116">If you do want toodo a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="ca2bb-117">Olá que VM primária deve ser desligado quando você está fazendo o failover de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-117">hello primary VM should be shut down when you're doing hello test failover.</span></span> <span data-ttu-id="ca2bb-118">Caso contrário, duas VMs com hello mesma identidade estará sendo executada em hello mesma rede em hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-118">Otherwise, two VMs with hello same identity will be running in hello same network at hello same time.</span></span> 
    - <span data-ttu-id="ca2bb-119">Se você fizer alterações tootest VMs, essas alterações serão perdidas quando você limpar Olá failover de teste.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-119">If you make changes tootest VMs, those changes are lost when you clean up hello test failover.</span></span> <span data-ttu-id="ca2bb-120">Essas alterações não são replicada toohello back VM primária.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-120">These changes aren't replicated back toohello primary VM.</span></span>
    - <span data-ttu-id="ca2bb-121">Testando um uma rede de produção leva toodowntime para suas cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-121">Testing a a production network leads toodowntime for your production workloads.</span></span> <span data-ttu-id="ca2bb-122">Peça aos usuários que não toouse aplicativo hello quando a análise de recuperação de desastres hello está em andamento.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-122">Ask users not toouse hello app when hello disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="ca2bb-123">Executar um failover de teste para uma VM</span><span class="sxs-lookup"><span data-stu-id="ca2bb-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="ca2bb-124">toofail em uma única VM, em **itens replicados**, clique em Olá VM > **Failover de teste**.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-124">toofail over a single VM, in **Replicated Items**, click hello VM > **Test Failover**.</span></span>
2. <span data-ttu-id="ca2bb-125">Em **Failover de teste**, especificar como máquinas virtuais de teste será conectado toonetworks após o failover de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-125">In **Test Failover**, specify how test VMs will be connected toonetworks after hello test failover.</span></span> 
3. <span data-ttu-id="ca2bb-126">Clique em **Okey** toobegin Olá failover.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-126">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="ca2bb-127">Controlar o andamento da saudação **trabalhos** guia.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-127">Track progress on hello **Jobs** tab.</span></span>
5. <span data-ttu-id="ca2bb-128">Após o failover estiver concluído, verifique se esse teste saudação inicial de VMs com êxito.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-128">After failover is complete, verify that hello test VMs start successfully.</span></span>
6. <span data-ttu-id="ca2bb-129">Quando terminar, clique em **failover de teste de limpeza** no plano de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-129">When you're done, click **Cleanup test failover** on hello recovery plan.</span></span>
7. <span data-ttu-id="ca2bb-130">Em **notas**, gravar e salvar todas as observações associadas Olá failover de teste.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-130">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="ca2bb-131">Esta etapa exclui Olá virtual máquinas e redes que foram criadas durante o failover de teste.</span><span class="sxs-lookup"><span data-stu-id="ca2bb-131">This step deletes hello virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ca2bb-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca2bb-132">Next steps</span></span>

<span data-ttu-id="ca2bb-133">Depois que você testou implantação hello, saiba mais sobre outros tipos de [failover](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="ca2bb-133">After you've tested hello deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
