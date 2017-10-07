---
title: "aaaSet uma política de replicação para tooAzure de replicação de VM do Hyper-V (com o VMM) com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como tooset uma política de replicação para tooAzure de replicação de VM do Hyper-V (com o VMM) com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a><span data-ttu-id="c7520-103">Etapa 10: Configurar uma política de replicação para tooAzure de replicação (com o VMM) de VM do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="c7520-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) tooAzure</span></span>


<span data-ttu-id="c7520-104">Depois de configurar o [mapeamento de rede](vmm-to-azure-walkthrough-network-mapping.md), use este artigo de tooconfigure uma política de replicação T\tooreplicate máquinas virtuais de Hyper-V gerenciados no System Center Virtual Machine Manager (VMM) nuvens tooAzure local, usando Olá [ O Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7520-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article tooconfigure a replication policy T\tooreplicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="c7520-105">Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c7520-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="c7520-106">Criar uma política</span><span class="sxs-lookup"><span data-stu-id="c7520-106">Create a policy</span></span>

1. <span data-ttu-id="c7520-107">toocreate uma nova política de replicação, clique em **preparar infraestrutura** > **as configurações de replicação** > **+ criar e associar**.</span><span class="sxs-lookup"><span data-stu-id="c7520-107">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Rede](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="c7520-109">Em **Criar e associar política**, especifique um nome de política.</span><span class="sxs-lookup"><span data-stu-id="c7520-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="c7520-110">Em **frequência de cópia**, especifique com que frequência tooreplicate delta dados após a replicação inicial da saudação (a cada 30 segundos, 5 ou 15 minutos).</span><span class="sxs-lookup"><span data-stu-id="c7520-110">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="c7520-111">Uma frequência de segundo 30 não tem suporte durante a replicação de armazenamento toopremium.</span><span class="sxs-lookup"><span data-stu-id="c7520-111">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="c7520-112">limitação de saudação é determinada pelo número de saudação de instantâneos por blob (100) com suporte pelo armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="c7520-112">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="c7520-113">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="c7520-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="c7520-114">Em **retenção de ponto de recuperação**, especifique, em horas, quanto tempo uma janela de retenção Olá será possível para cada ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="c7520-114">In **Recovery point retention**, specify in hours how long hello retention window will be for each recovery point.</span></span> <span data-ttu-id="c7520-115">Computadores protegidos podem ser recuperados tooany ponto dentro de uma janela.</span><span class="sxs-lookup"><span data-stu-id="c7520-115">Protected machines can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="c7520-116">Em **Frequência do instantâneo consistente com aplicativo**, especifique com que frequência (1 a 12 horas) são criados os pontos de recuperação que incluam instantâneos consistentes com aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c7520-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="c7520-117">Hyper-V usa dois tipos de instantâneos — um instantâneo padrão que fornece um instantâneo incremental da saudação toda a máquina virtual e um instantâneo consistente com o aplicativo que usa um instantâneo point-in-time dos dados de aplicativo hello dentro da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7520-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span> <span data-ttu-id="c7520-118">Instantâneos consistentes com o aplicativo usam tooensure Volume Shadow Copy Service (VSS) que os aplicativos estejam em um estado consistente quando Olá instantâneo é tirado.</span><span class="sxs-lookup"><span data-stu-id="c7520-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span> <span data-ttu-id="c7520-119">Observe que, se você habilitar instantâneos consistentes com aplicativos, isso afetará Olá desempenho de aplicativos executados em máquinas virtuais de origem.</span><span class="sxs-lookup"><span data-stu-id="c7520-119">Note that if you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="c7520-120">Verifique se o valor de saudação definido é menor do que o número de saudação de pontos de recuperação adicionais que você configurar.</span><span class="sxs-lookup"><span data-stu-id="c7520-120">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="c7520-121">Em **hora de início da replicação inicial**, indicar quando toostart Olá a replicação inicial.</span><span class="sxs-lookup"><span data-stu-id="c7520-121">In **Initial replication start time**, indicate when toostart hello initial replication.</span></span> <span data-ttu-id="c7520-122">replicação Olá ocorre sobre a largura de banda de internet, portanto, talvez você queira tooschedule-lo fora do horário de ocupado.</span><span class="sxs-lookup"><span data-stu-id="c7520-122">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span>
7. <span data-ttu-id="c7520-123">Em **criptografar dados armazenados no Azure**, especifique se tooencrypt dados rest no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7520-123">In **Encrypt data stored on Azure**, specify whether tooencrypt at rest data in Azure storage.</span></span> <span data-ttu-id="c7520-124">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7520-124">Then click **OK**.</span></span>

    ![Política de replicação](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="c7520-126">Quando você cria uma nova política está associado automaticamente Olá nuvem do VMM.</span><span class="sxs-lookup"><span data-stu-id="c7520-126">When you create a new policy it's automatically associated with hello VMM cloud.</span></span> <span data-ttu-id="c7520-127">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7520-127">Click **OK**.</span></span> <span data-ttu-id="c7520-128">Você pode associar nuvens do VMM adicionais (e Olá VMs neles) com esta política de replicação em **replicação** > nome da política > **associar VMM nuvem**.</span><span class="sxs-lookup"><span data-stu-id="c7520-128">You can associate additional VMM clouds (and hello VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Política de replicação](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="c7520-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c7520-130">Next steps</span></span>

<span data-ttu-id="c7520-131">Vá muito[etapa 11: habilitar a replicação](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="c7520-131">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
