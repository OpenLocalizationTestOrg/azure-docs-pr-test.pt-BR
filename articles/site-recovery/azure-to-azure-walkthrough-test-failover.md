---
title: "aaaRun um failover de teste para replicação de VM do Azure com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação que você precisa para executar um failover de teste para máquinas virtuais do Azure replica tooanother região do Azure usando hello Azure Site Recovery service."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a><span data-ttu-id="04fc3-103">Etapa 6: executar um failover de teste para replicação de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="04fc3-103">Step 6: Run a test failover for Azure VM replication</span></span>

<span data-ttu-id="04fc3-104">Depois de habilitar a replicação da máquina virtual do Azure (VMs), execute as etapas de saudação neste artigo, o failover de teste de toorun de tooanother de uma região do Azure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="04fc3-104">After you've enabled replication for Azure virtual machine (VMs), follow hello steps in this article, toorun test failover from one Azure region tooanother, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="04fc3-105">Quando você terminar de artigo hello, você deve ter verificado com um failover de teste que pelo menos uma VM do Azure pode fazer failover tooyour região secundária do Azure.</span><span class="sxs-lookup"><span data-stu-id="04fc3-105">When you finish hello article, you should have verified with a test failover, that at least one Azure VM can fail over tooyour secondary Azure region.</span></span> 
- <span data-ttu-id="04fc3-106">Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="04fc3-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="04fc3-107">Atualmente, a replicação de VM do Azure está em versão prévia.</span><span class="sxs-lookup"><span data-stu-id="04fc3-107">Azure VM replication is currently in preview.</span></span>


## <a name="before-you-start"></a><span data-ttu-id="04fc3-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="04fc3-108">Before you start</span></span>

- <span data-ttu-id="04fc3-109">Antes de executar um failover de teste, é recomendável que você verifique Olá propriedades da VM e faça as alterações que você precisa.</span><span class="sxs-lookup"><span data-stu-id="04fc3-109">Before you run a test failover, we recommend that you verify hello VM properties, and make any changes you need to.</span></span> <span data-ttu-id="04fc3-110">Você pode acessar propriedades da VM Olá no **replicadas itens**.</span><span class="sxs-lookup"><span data-stu-id="04fc3-110">You can access hello VM properties in **Replicated items**.</span></span> <span data-ttu-id="04fc3-111">Olá **Essentials** folha mostra informações sobre configurações de máquinas e status.</span><span class="sxs-lookup"><span data-stu-id="04fc3-111">hello **Essentials** blade shows information about machines settings and status.</span></span>
- <span data-ttu-id="04fc3-112">É recomendável usar uma rede separada da VM do Azure para failover de teste Olá e não rede de saudação (padrão ou personalizado) que foi configurada para failover de produção.</span><span class="sxs-lookup"><span data-stu-id="04fc3-112">We recommend you use a separate Azure VM network for hello test failover, and not hello network (default or customized) that was set up for production failover.</span></span>
- <span data-ttu-id="04fc3-113">Olá teste failover failover de máquinas virtuais do Azure (e seu armazenamento) toohello região secundária do Azure.</span><span class="sxs-lookup"><span data-stu-id="04fc3-113">hello test failover fails over Azure VMs (and their storage) toohello secondary Azure region.</span></span> <span data-ttu-id="04fc3-114">Não replica quaisquer aplicativos ou recursos dependentes.</span><span class="sxs-lookup"><span data-stu-id="04fc3-114">It doesn't replicate any dependent apps or resources.</span></span> <span data-ttu-id="04fc3-115">Se os aplicativos executados em falha em VMs dependem de outros recursos, como o Active Directory ou DNS, você precisa tooreplicate dessas também, se eles não ainda estiver disponíveis em sua região secundária.</span><span class="sxs-lookup"><span data-stu-id="04fc3-115">If apps running on failed over VMs are dependent on other resources, such as Active Directory or DNS, you need tooreplicate these too, if they're not already available in your secondary region.</span></span> [<span data-ttu-id="04fc3-116">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="04fc3-116">Learn more</span></span>](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- <span data-ttu-id="04fc3-117">Se você quiser tooaccess replicadas VMs após o failover de um site local, você precisa muito[preparar tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese VMs.</span><span class="sxs-lookup"><span data-stu-id="04fc3-117">If you want tooaccess replicated VMs after failover from an on-premises site, you need too[prepare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese VMs.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="04fc3-118">Execute um teste de failover</span><span class="sxs-lookup"><span data-stu-id="04fc3-118">Run a test failover</span></span>

1. <span data-ttu-id="04fc3-119">Em **configurações** > **itens replicados**, clique em Olá VM **+ Failover de teste** ícone.</span><span class="sxs-lookup"><span data-stu-id="04fc3-119">In **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span> 

2. <span data-ttu-id="04fc3-120">Em **Failover de teste**, selecione um toouse de ponto de recuperação para failover de saudação:</span><span class="sxs-lookup"><span data-stu-id="04fc3-120">In **Test Failover**, Select a recovery point toouse for hello failover:</span></span>

    - <span data-ttu-id="04fc3-121">**Mais recentes processados**: falha Olá VM sobre toohello último ponto de recuperação que foi processado pelo serviço de recuperação de Site hello.</span><span class="sxs-lookup"><span data-stu-id="04fc3-121">**Latest processed**: Fails hello VM over toohello latest recovery point that was processed by hello Site Recovery service.</span></span> <span data-ttu-id="04fc3-122">carimbo de data / hora de saudação é mostrado.</span><span class="sxs-lookup"><span data-stu-id="04fc3-122">hello time stamp is shown.</span></span> <span data-ttu-id="04fc3-123">Com essa opção, nenhum tempo é gasto em processamento de dados, portanto, fornece um RTO (Objetivo do Tempo de Recuperação) baixo.</span><span class="sxs-lookup"><span data-stu-id="04fc3-123">With this option, no time is spent processing data, so it provides a low RTO (Recovery Time Objective).</span></span>
    - <span data-ttu-id="04fc3-124">**Mais recente consistente de aplicativo**: essa opção Falha em todas as VMs toohello ponto mais recente recuperação consistentes com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="04fc3-124">**Latest app-consistent**: This option fails over all VMs toohello latest app-consistent recovery point.</span></span> <span data-ttu-id="04fc3-125">carimbo de data / hora de saudação é mostrado.</span><span class="sxs-lookup"><span data-stu-id="04fc3-125">hello time stamp is shown.</span></span> 
    - <span data-ttu-id="04fc3-126">**Personalizar**: selecione qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="04fc3-126">**Custom**: Select any recovery point.</span></span>
 
3. <span data-ttu-id="04fc3-127">Selecione Olá destino rede virtual do Azure toowhich VMs do Azure na região secundária hello será conectada após o failover de saudação.</span><span class="sxs-lookup"><span data-stu-id="04fc3-127">Select hello target Azure virtual network toowhich Azure VMs in hello secondary region will be connected, after hello failover occurs.</span></span>
4. <span data-ttu-id="04fc3-128">toostart Olá failover, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="04fc3-128">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="04fc3-129">tootrack de andamento, clique em Olá VM tooopen suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="04fc3-129">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="04fc3-130">Ou, você pode clicar em Olá **Failover de teste** trabalho em nome do cofre hello > **configurações** > **trabalhos** > **ostrabalhosderecuperaçãodeSite**.</span><span class="sxs-lookup"><span data-stu-id="04fc3-130">Or, you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="04fc3-131">Depois de saudação failover for concluído, réplica hello Azure VM aparece no hello portal do Azure > **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="04fc3-131">After hello failover finishes, hello replica Azure VM appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="04fc3-132">Certifique-se de que Olá VM é o tamanho apropriado hello, que tenha se conectado toohello apropriado, e rede que está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="04fc3-132">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="04fc3-133">Olá toodelete VMs que foram criados durante a saudação failover de teste, clique em **failover de teste de limpeza** em Olá replicadas item ou hello plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="04fc3-133">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="04fc3-134">Em **notas**, gravar e salvar todas as observações associadas Olá failover de teste.</span><span class="sxs-lookup"><span data-stu-id="04fc3-134">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="04fc3-135">[Saiba mais](site-recovery-test-failover-to-azure.md) sobre failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="04fc3-135">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04fc3-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04fc3-136">Next steps</span></span>

<span data-ttu-id="04fc3-137">Depois de testar o failover, esse passo a passo estará concluído.</span><span class="sxs-lookup"><span data-stu-id="04fc3-137">After you've tested failover, this walkthrough is complete.</span></span> <span data-ttu-id="04fc3-138">Agora, saiba mais sobre a execução de failovers em produção:</span><span class="sxs-lookup"><span data-stu-id="04fc3-138">Now, learn about running failovers in production:</span></span>

- <span data-ttu-id="04fc3-139">[Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de failovers e como toorun-los.</span><span class="sxs-lookup"><span data-stu-id="04fc3-139">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="04fc3-140">Saiba mais sobre a falha em várias VMs[utilizando um plano de recuperação](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="04fc3-140">Learn more about failing over multiple VMs [using a recovery plan](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="04fc3-141">Saiba mais sobre [utilizar planos de recuperação](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="04fc3-141">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="04fc3-142">Saiba mais sobre [proteger novamente as VMs do Azure](site-recovery-how-to-reprotect.md) após o failover.</span><span class="sxs-lookup"><span data-stu-id="04fc3-142">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>

