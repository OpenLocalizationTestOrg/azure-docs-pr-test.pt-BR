---
title: "Configurar uma política de replicação para a replicação da VM do Hyper-V (com o VMM) para o Azure com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como configurar uma política de replicação para a replicação de VMs do Hyper-V (com o VMM) para o Azure com o Azure Site Recovery"
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
ms.openlocfilehash: 592e1c3f647e5b1f1d9aa776657e8f89b60349e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-to-azure"></a><span data-ttu-id="27701-103">Etapa 10: Configurar uma política de replicação para a replicação da VM do Hyper-V (com o VMM) para o Azure</span><span class="sxs-lookup"><span data-stu-id="27701-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) to Azure</span></span>


<span data-ttu-id="27701-104">Depois de configurar o [mapeamento de rede](vmm-to-azure-walkthrough-network-mapping.md), use este artigo para configurar uma política de replicação T\para replicar máquinas virtuais do Hyper-V gerenciadas nas nuvens do System Center Virtual Machine Manager (VMM) para o Azure local usando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="27701-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article to configure a replication policy T\to replicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="27701-105">Depois de ler este artigo, poste comentários na parte inferior ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="27701-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="27701-106">Criar uma política</span><span class="sxs-lookup"><span data-stu-id="27701-106">Create a policy</span></span>

1. <span data-ttu-id="27701-107">Para criar uma nova política de replicação, clique em **Preparar a Infraestrutura** > **Configurações de Replicação** > **+Criar e associar**.</span><span class="sxs-lookup"><span data-stu-id="27701-107">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Rede](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="27701-109">Em **Criar e associar política**, especifique um nome de política.</span><span class="sxs-lookup"><span data-stu-id="27701-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="27701-110">Em **Frequência de cópia**, especifique com que frequência você deseja replicar os dados delta após a replicação inicial (a cada 30 segundos, 5 ou 15 minutos).</span><span class="sxs-lookup"><span data-stu-id="27701-110">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="27701-111">Não há suporte para uma frequência de 30 segundos ao replicar para armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="27701-111">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="27701-112">A limitação é determinada pelo número de instantâneos por blob (100) com suporte pelo armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="27701-112">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="27701-113">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="27701-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="27701-114">Em **Retenção do ponto de recuperação**, especifique, em horas, qual será a duração da janela de retenção para cada ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="27701-114">In **Recovery point retention**, specify in hours how long the retention window will be for each recovery point.</span></span> <span data-ttu-id="27701-115">Os computadores protegidos podem ser recuperados para qualquer ponto nessa janela.</span><span class="sxs-lookup"><span data-stu-id="27701-115">Protected machines can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="27701-116">Em **Frequência do instantâneo consistente com aplicativo**, especifique com que frequência (1 a 12 horas) são criados os pontos de recuperação que incluam instantâneos consistentes com aplicativos.</span><span class="sxs-lookup"><span data-stu-id="27701-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="27701-117">O Hyper-V usa dois tipos de instantâneos: um instantâneo padrão, que fornece um instantâneo incremental de toda a máquina virtual, e um instantâneo consistente com aplicativos, que cria um instantâneo pontual dos dados do aplicativo na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27701-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span> <span data-ttu-id="27701-118">Os instantâneos consistentes com aplicativos usam o Serviço de VSS (Cópias de Sombra de Volume) para garantir que os aplicativos estejam em um estado consistente quando o instantâneo for obtido.</span><span class="sxs-lookup"><span data-stu-id="27701-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span> <span data-ttu-id="27701-119">Observe que, se você habilitar instantâneos consistentes com aplicativos, isso afetará o desempenho de aplicativos executados em máquinas virtuais de origem.</span><span class="sxs-lookup"><span data-stu-id="27701-119">Note that if you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="27701-120">Verifique se o valor definido é menor do que o número de pontos de recuperação adicionais que você configurar.</span><span class="sxs-lookup"><span data-stu-id="27701-120">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="27701-121">Em **Hora de início para replicação inicial**, indique quando a replicação inicial deve começar.</span><span class="sxs-lookup"><span data-stu-id="27701-121">In **Initial replication start time**, indicate when to start the initial replication.</span></span> <span data-ttu-id="27701-122">A replicação ocorre pela largura de banda da Internet, pois talvez você queira agendá-la fora dos horários de pico.</span><span class="sxs-lookup"><span data-stu-id="27701-122">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span>
7. <span data-ttu-id="27701-123">Em **Criptografar os dados armazenados no Azure**, especifique se os dados em repouso serão criptografados no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="27701-123">In **Encrypt data stored on Azure**, specify whether to encrypt at rest data in Azure storage.</span></span> <span data-ttu-id="27701-124">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27701-124">Then click **OK**.</span></span>

    ![Política de replicação](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="27701-126">Quando você cria uma nova política, ela é automaticamente associada à nuvem do VMM.</span><span class="sxs-lookup"><span data-stu-id="27701-126">When you create a new policy it's automatically associated with the VMM cloud.</span></span> <span data-ttu-id="27701-127">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27701-127">Click **OK**.</span></span> <span data-ttu-id="27701-128">É possível associar nuvens do VMM adicionais (e as VMs nelas) a essa política de replicação em **Replicação** > nome da política > **Associar Nuvem do VMM**.</span><span class="sxs-lookup"><span data-stu-id="27701-128">You can associate additional VMM clouds (and the VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Política de replicação](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="27701-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27701-130">Next steps</span></span>

<span data-ttu-id="27701-131">Vá para a [Etapa 11: Habilitar a replicação](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="27701-131">Go to [Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
