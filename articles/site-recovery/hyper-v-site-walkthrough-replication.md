---
title: "Habilite uma política de replicação para replicação de VM Hyper-V (sem o System Center VMM) para o Azure com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas necessárias para configurar uma política de replicação durante a replicação de VMs Hyper-V no armazenamento do Azure"
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
ms.openlocfilehash: ca5bec5cf1152e6259b9fe7a869edd2d62b88e1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-to-azure"></a><span data-ttu-id="be28c-103">Etapa 9: configurar uma política de replicação para a replicação da VM Hyper-V para o Azure</span><span class="sxs-lookup"><span data-stu-id="be28c-103">Step 9: Set up a replication policy for Hyper-V VM replication to Azure</span></span>

<span data-ttu-id="be28c-104">Este artigo descreve como configurar uma política de replicação quando você estiver replicando VMs Hyper-V para o Azure (sem o System Center VMM) usando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="be28c-104">This article describes how to set up a replication policy when you're replicating Hyper-V VMs to Azure (without System Center VMM) using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="be28c-105">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="be28c-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="be28c-106">Sobre instantâneos</span><span class="sxs-lookup"><span data-stu-id="be28c-106">About snapshots</span></span>

<span data-ttu-id="be28c-107">O Hyper-V usa dois tipos de instantâneos: um instantâneo padrão, que fornece um instantâneo incremental de toda a máquina virtual, e um instantâneo consistente com aplicativos, que cria um instantâneo pontual dos dados do aplicativo na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be28c-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span>
    - <span data-ttu-id="be28c-108">Os instantâneos consistentes com aplicativos usam o Serviço de VSS (Cópias de Sombra de Volume) para garantir que os aplicativos estejam em um estado consistente quando o instantâneo for obtido.</span><span class="sxs-lookup"><span data-stu-id="be28c-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span>
    - <span data-ttu-id="be28c-109">Se você habilitar instantâneos consistentes com o aplicativo, isso afetará o desempenho de aplicativos executados em máquinas virtuais de origem.</span><span class="sxs-lookup"><span data-stu-id="be28c-109">If you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="be28c-110">Verifique se o valor definido é menor do que o número de pontos de recuperação adicionais que você configurar.</span><span class="sxs-lookup"><span data-stu-id="be28c-110">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="be28c-111">Configurar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="be28c-111">Set up a replication policy</span></span>

1. <span data-ttu-id="be28c-112">Para criar uma nova política de replicação, clique em **Preparar a Infraestrutura** > **Configurações de Replicação** > **+Criar e associar**.</span><span class="sxs-lookup"><span data-stu-id="be28c-112">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Rede](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="be28c-114">Em **Criar e associar política**, especifique um nome de política.</span><span class="sxs-lookup"><span data-stu-id="be28c-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="be28c-115">Em **Frequência de cópia**, especifique com que frequência você deseja replicar os dados delta após a replicação inicial (a cada 30 segundos, 5 ou 15 minutos).</span><span class="sxs-lookup"><span data-stu-id="be28c-115">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="be28c-116">Não há suporte para uma frequência de 30 segundos ao replicar para armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="be28c-116">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="be28c-117">A limitação é determinada pelo número de instantâneos por blob (100) com suporte pelo armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="be28c-117">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="be28c-118">[Saiba mais](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="be28c-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="be28c-119">Em **Retenção do ponto de recuperação**, especifique (em horas) qual será a duração da janela de retenção para cada ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="be28c-119">In **Recovery point retention**, specify in hours how long the retention window is for each recovery point.</span></span> <span data-ttu-id="be28c-120">VMs podem ser recuperadas para qualquer ponto em uma janela.</span><span class="sxs-lookup"><span data-stu-id="be28c-120">VMs can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="be28c-121">Em **Frequência do instantâneo consistente com aplicativo**, especifique com que frequência (1 a 12 horas) são criados os pontos de recuperação que contêm instantâneos consistentes com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="be28c-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="be28c-122">Em **Hora de início para replicação inicial**, especifique quando a replicação inicial deve começar.</span><span class="sxs-lookup"><span data-stu-id="be28c-122">In **Initial replication start time**, specify when to start the initial replication.</span></span> <span data-ttu-id="be28c-123">A replicação ocorre pela largura de banda da Internet, pois talvez você queira agendá-la fora dos horários de pico.</span><span class="sxs-lookup"><span data-stu-id="be28c-123">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span> <span data-ttu-id="be28c-124">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="be28c-124">Then click **OK**.</span></span>

    ![Política de replicação](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="be28c-126">Quando você cria uma nova política, ela é automaticamente associada ao site do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="be28c-126">When you create a new policy, it's automatically associated with the Hyper-V site.</span></span> <span data-ttu-id="be28c-127">É possível associar um site do Hyper-V (e as VMs nele) a várias políticas de replicação em **Replicação** > nome da política > **Associar Site do Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="be28c-127">You can associate a Hyper-V site (and the VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="be28c-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be28c-128">Next steps</span></span>

<span data-ttu-id="be28c-129">Acesse a [Etapa 10: Habilitar a replicação](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="be28c-129">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
