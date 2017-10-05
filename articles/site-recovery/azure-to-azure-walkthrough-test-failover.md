---
title: "Executar um failover de teste para replicação de VM do Azure com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas necessárias para executar um failover de teste para VMs do Azure replicando para outra região do Azure utilizando o serviço do Azure Site Recovery."
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
ms.openlocfilehash: 8babb0d016729f318442af93596d206c38d91206
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a><span data-ttu-id="047b1-103">Etapa 6: executar um failover de teste para replicação de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="047b1-103">Step 6: Run a test failover for Azure VM replication</span></span>

<span data-ttu-id="047b1-104">Após habilitar a replicação para VMs (máquinas virtuais) do Azure, siga as etapas neste artigo para executar o failover de teste de uma região do Azure para outra, utilizando o serviço do [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="047b1-104">After you've enabled replication for Azure virtual machine (VMs), follow the steps in this article, to run test failover from one Azure region to another, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

- <span data-ttu-id="047b1-105">Ao concluir o artigo, você deverá ter verificado com um failover de teste que pelo menos uma VM do Azure pode fazer failover para a região do Azure secundária.</span><span class="sxs-lookup"><span data-stu-id="047b1-105">When you finish the article, you should have verified with a test failover, that at least one Azure VM can fail over to your secondary Azure region.</span></span> 
- <span data-ttu-id="047b1-106">Publique eventuais comentários no final deste artigo ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="047b1-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="047b1-107">Atualmente, a replicação de VM do Azure está em versão prévia.</span><span class="sxs-lookup"><span data-stu-id="047b1-107">Azure VM replication is currently in preview.</span></span>


## <a name="before-you-start"></a><span data-ttu-id="047b1-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="047b1-108">Before you start</span></span>

- <span data-ttu-id="047b1-109">Antes de executar um failover de teste, é recomendável verificar as propriedades da VM e efetuar as alterações necessárias.</span><span class="sxs-lookup"><span data-stu-id="047b1-109">Before you run a test failover, we recommend that you verify the VM properties, and make any changes you need to.</span></span> <span data-ttu-id="047b1-110">É possível acessar as propriedades da VM em **Itens replicados**.</span><span class="sxs-lookup"><span data-stu-id="047b1-110">You can access the VM properties in **Replicated items**.</span></span> <span data-ttu-id="047b1-111">A folha **Conceitos básicos** mostra as informações sobre as configurações e o status dos computadores.</span><span class="sxs-lookup"><span data-stu-id="047b1-111">The **Essentials** blade shows information about machines settings and status.</span></span>
- <span data-ttu-id="047b1-112">É recomendável utilizar uma rede de VM do Azure separada para o failover de teste e não a rede (padrão ou personalizada) que foi configurada para failover de produção.</span><span class="sxs-lookup"><span data-stu-id="047b1-112">We recommend you use a separate Azure VM network for the test failover, and not the network (default or customized) that was set up for production failover.</span></span>
- <span data-ttu-id="047b1-113">O failover de teste falha em VMs do Azure (e seu armazenamento) na região do Azure secundária.</span><span class="sxs-lookup"><span data-stu-id="047b1-113">The test failover fails over Azure VMs (and their storage) to the secondary Azure region.</span></span> <span data-ttu-id="047b1-114">Não replica quaisquer aplicativos ou recursos dependentes.</span><span class="sxs-lookup"><span data-stu-id="047b1-114">It doesn't replicate any dependent apps or resources.</span></span> <span data-ttu-id="047b1-115">Se os aplicativos em execução com falhas nas VMs dependem de outros recursos, como o Active Directory ou o DNS, isso também será necessário replicar, se eles ainda não estiverem disponíveis em sua região secundária.</span><span class="sxs-lookup"><span data-stu-id="047b1-115">If apps running on failed over VMs are dependent on other resources, such as Active Directory or DNS, you need to replicate these too, if they're not already available in your secondary region.</span></span> [<span data-ttu-id="047b1-116">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="047b1-116">Learn more</span></span>](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- <span data-ttu-id="047b1-117">Se você quiser acessar VMs replicadas após o failover de um site local será necessário [preparar para conectar](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) a essas VMs.</span><span class="sxs-lookup"><span data-stu-id="047b1-117">If you want to access replicated VMs after failover from an on-premises site, you need to [prepare to connect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) to these VMs.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="047b1-118">Execute um teste de failover</span><span class="sxs-lookup"><span data-stu-id="047b1-118">Run a test failover</span></span>

1. <span data-ttu-id="047b1-119">Em **Configurações** > **Itens Replicados**, clique no ícone da VM **+ Failover de Teste**.</span><span class="sxs-lookup"><span data-stu-id="047b1-119">In **Settings** > **Replicated Items**, click the VM **+Test Failover** icon.</span></span> 

2. <span data-ttu-id="047b1-120">Em **Failover de Teste**, selecione um ponto de recuperação para usar no failover:</span><span class="sxs-lookup"><span data-stu-id="047b1-120">In **Test Failover**, Select a recovery point to use for the failover:</span></span>

    - <span data-ttu-id="047b1-121">**Processado mais recente**: falha na VM para o ponto de recuperação único que foi processado pelo serviço do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="047b1-121">**Latest processed**: Fails the VM over to the latest recovery point that was processed by the Site Recovery service.</span></span> <span data-ttu-id="047b1-122">A carimbo de data/hora é mostrado.</span><span class="sxs-lookup"><span data-stu-id="047b1-122">The time stamp is shown.</span></span> <span data-ttu-id="047b1-123">Com essa opção, nenhum tempo é gasto em processamento de dados, portanto, fornece um RTO (Objetivo do Tempo de Recuperação) baixo.</span><span class="sxs-lookup"><span data-stu-id="047b1-123">With this option, no time is spent processing data, so it provides a low RTO (Recovery Time Objective).</span></span>
    - <span data-ttu-id="047b1-124">**Consistente com o aplicativo mais recente**: essa opção falha em todas as VMs para o ponto de recuperação consistente com o aplicativo mais recente.</span><span class="sxs-lookup"><span data-stu-id="047b1-124">**Latest app-consistent**: This option fails over all VMs to the latest app-consistent recovery point.</span></span> <span data-ttu-id="047b1-125">A carimbo de data/hora é mostrado.</span><span class="sxs-lookup"><span data-stu-id="047b1-125">The time stamp is shown.</span></span> 
    - <span data-ttu-id="047b1-126">**Personalizar**: selecione qualquer ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="047b1-126">**Custom**: Select any recovery point.</span></span>
 
3. <span data-ttu-id="047b1-127">Selecione a rede virtual de destino do Azure para qual as VMs do Azure na região secundária serão conectadas, após o failover ocorrer.</span><span class="sxs-lookup"><span data-stu-id="047b1-127">Select the target Azure virtual network to which Azure VMs in the secondary region will be connected, after the failover occurs.</span></span>
4. <span data-ttu-id="047b1-128">Para iniciar o failover, clique em **Ok**.</span><span class="sxs-lookup"><span data-stu-id="047b1-128">To start the failover, click **OK**.</span></span> <span data-ttu-id="047b1-129">Para acompanhar o progresso, clique na VM para abrir suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="047b1-129">To track progress, click the VM to open its properties.</span></span> <span data-ttu-id="047b1-130">Ou você pode clicar no trabalho **Failover de Teste** no nome do cofre > **Configurações** > **Trabalhos** > **Trabalhos do Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="047b1-130">Or, you can click the **Test Failover** job in the vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="047b1-131">Após a conclusão do failover, a réplica da VM do Azure aparece no portal do Azure > **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="047b1-131">After the failover finishes, the replica Azure VM appears in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="047b1-132">Verifique se a VM é do tamanho apropriado, se está conectada à rede adequada e se está em execução.</span><span class="sxs-lookup"><span data-stu-id="047b1-132">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="047b1-133">Para excluir as VMs que foram criadas durante o failover de teste, clique em **Failover de teste de limpeza** no item replicado ou no plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="047b1-133">To delete the VMs that were created during the test failover, click **Cleanup test failover** on the replicated item or the recovery plan.</span></span> <span data-ttu-id="047b1-134">Em **Observações**, registre e salve todas as observações associadas ao failover de teste.</span><span class="sxs-lookup"><span data-stu-id="047b1-134">In **Notes**, record and save any observations associated with the test failover.</span></span> 

<span data-ttu-id="047b1-135">[Saiba mais](site-recovery-test-failover-to-azure.md) sobre failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="047b1-135">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="047b1-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="047b1-136">Next steps</span></span>

<span data-ttu-id="047b1-137">Depois de testar o failover, esse passo a passo estará concluído.</span><span class="sxs-lookup"><span data-stu-id="047b1-137">After you've tested failover, this walkthrough is complete.</span></span> <span data-ttu-id="047b1-138">Agora, saiba mais sobre a execução de failovers em produção:</span><span class="sxs-lookup"><span data-stu-id="047b1-138">Now, learn about running failovers in production:</span></span>

- <span data-ttu-id="047b1-139">[Saiba mais](site-recovery-failover.md) sobre diferentes tipos de failovers e como executá-los.</span><span class="sxs-lookup"><span data-stu-id="047b1-139">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="047b1-140">Saiba mais sobre a falha em várias VMs[utilizando um plano de recuperação](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="047b1-140">Learn more about failing over multiple VMs [using a recovery plan](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="047b1-141">Saiba mais sobre [utilizar planos de recuperação](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="047b1-141">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="047b1-142">Saiba mais sobre [proteger novamente as VMs do Azure](site-recovery-how-to-reprotect.md) após o failover.</span><span class="sxs-lookup"><span data-stu-id="047b1-142">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>

