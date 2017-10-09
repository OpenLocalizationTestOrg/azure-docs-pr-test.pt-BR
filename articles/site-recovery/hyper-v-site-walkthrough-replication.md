---
title: "aaaSet uma política de replicação para tooAzure de replicação (sem o System Center VMM) de VM do Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação precisar tooset uma política de replicação durante a replicação de armazenamento de tooAzure de VMs Hyper-V"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a><span data-ttu-id="604b7-103">Etapa 9: Configurar uma política de replicação para tooAzure de replicação de VM do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="604b7-103">Step 9: Set up a replication policy for Hyper-V VM replication tooAzure</span></span>

<span data-ttu-id="604b7-104">Este artigo descreve como tooset uma política de replicação quando você estiver replicando tooAzure de VMs Hyper-V (sem o System Center VMM) usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="604b7-104">This article describes how tooset up a replication policy when you're replicating Hyper-V VMs tooAzure (without System Center VMM) using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="604b7-105">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="604b7-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="604b7-106">Sobre instantâneos</span><span class="sxs-lookup"><span data-stu-id="604b7-106">About snapshots</span></span>

<span data-ttu-id="604b7-107">Hyper-V usa dois tipos de instantâneos — um instantâneo padrão que fornece um instantâneo incremental da saudação toda a máquina virtual e um instantâneo consistente com o aplicativo que usa um instantâneo point-in-time dos dados de aplicativo hello dentro da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="604b7-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span>
    - <span data-ttu-id="604b7-108">Instantâneos consistentes com o aplicativo usam tooensure Volume Shadow Copy Service (VSS) que os aplicativos estejam em um estado consistente quando Olá instantâneo é tirado.</span><span class="sxs-lookup"><span data-stu-id="604b7-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span>
    - <span data-ttu-id="604b7-109">Se você habilitar instantâneos consistentes com aplicativos, isso afetará o desempenho de saudação de aplicativos executados em máquinas virtuais de origem.</span><span class="sxs-lookup"><span data-stu-id="604b7-109">If you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="604b7-110">Verifique se o valor de saudação definido é menor do que o número de saudação de pontos de recuperação adicionais que você configurar.</span><span class="sxs-lookup"><span data-stu-id="604b7-110">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="604b7-111">Configurar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="604b7-111">Set up a replication policy</span></span>

1. <span data-ttu-id="604b7-112">toocreate uma nova política de replicação, clique em **preparar infraestrutura** > **as configurações de replicação** > **+ criar e associar**.</span><span class="sxs-lookup"><span data-stu-id="604b7-112">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Rede](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="604b7-114">Em **Criar e associar política**, especifique um nome de política.</span><span class="sxs-lookup"><span data-stu-id="604b7-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="604b7-115">Em **frequência de cópia**, especifique com que frequência tooreplicate delta dados após a replicação inicial da saudação (a cada 30 segundos, 5 ou 15 minutos).</span><span class="sxs-lookup"><span data-stu-id="604b7-115">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="604b7-116">Uma frequência de segundo 30 não tem suporte durante a replicação de armazenamento toopremium.</span><span class="sxs-lookup"><span data-stu-id="604b7-116">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="604b7-117">limitação de saudação é determinada pelo número de saudação de instantâneos por blob (100) com suporte pelo armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="604b7-117">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="604b7-118">[Saiba mais](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="604b7-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="604b7-119">Em **retenção de ponto de recuperação**, especifique em horas quanto tempo é uma janela de retenção Olá para cada ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="604b7-119">In **Recovery point retention**, specify in hours how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="604b7-120">Máquinas virtuais podem ser recuperados tooany ponto dentro de uma janela.</span><span class="sxs-lookup"><span data-stu-id="604b7-120">VMs can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="604b7-121">Em **Frequência do instantâneo consistente com aplicativo**, especifique com que frequência (1 a 12 horas) são criados os pontos de recuperação que contêm instantâneos consistentes com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="604b7-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="604b7-122">Em **hora de início da replicação inicial**, especifique quando toostart Olá a replicação inicial.</span><span class="sxs-lookup"><span data-stu-id="604b7-122">In **Initial replication start time**, specify when toostart hello initial replication.</span></span> <span data-ttu-id="604b7-123">replicação Olá ocorre sobre a largura de banda de internet, portanto, talvez você queira tooschedule-lo fora do horário de ocupado.</span><span class="sxs-lookup"><span data-stu-id="604b7-123">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span> <span data-ttu-id="604b7-124">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="604b7-124">Then click **OK**.</span></span>

    ![Política de replicação](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="604b7-126">Quando você cria uma nova política, ela está associada automaticamente com o site do Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="604b7-126">When you create a new policy, it's automatically associated with hello Hyper-V site.</span></span> <span data-ttu-id="604b7-127">Você pode associar um site Hyper-V (e hello VMs nele) com várias políticas de replicação no **replicação** > nome da política > **associar o Site de Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="604b7-127">You can associate a Hyper-V site (and hello VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="604b7-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="604b7-128">Next steps</span></span>

<span data-ttu-id="604b7-129">Vá muito[etapa 10: habilitar a replicação](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="604b7-129">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
