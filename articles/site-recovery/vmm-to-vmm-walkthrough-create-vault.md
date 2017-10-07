---
title: "aaaCreate um cofre para o site secundário do Hyper-V replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como toocreate um cofre ao replicar máquinas virtuais do Hyper-V tooa System Center VMM secundário do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="35144-103">Etapa 5: Criar um cofre do site secundário do Hyper-V replicação tooa</span><span class="sxs-lookup"><span data-stu-id="35144-103">Step 5: Create a vault for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="35144-104">Depois de preparar local [/clusters de hosts Hyper-V e de servidores do System Center Virtual Machine Manager (VMM)](vmm-to-vmm-walkthrough-vmm-hyper-v.md) para o site secundário usando o Hyper-V replicação tooa [do Azure Site Recovery](site-recovery-overview.md), você pode criar um Cofre de serviços de recuperação e selecione Olá replicação cenário.</span><span class="sxs-lookup"><span data-stu-id="35144-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication tooa secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select hello replication scenario.</span></span>

<span data-ttu-id="35144-105">Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="35144-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="35144-106">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="35144-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="35144-107">Escolher um objetivo de proteção</span><span class="sxs-lookup"><span data-stu-id="35144-107">Choose a protection goal</span></span>

<span data-ttu-id="35144-108">Selecione o que você deseja tooreplicate e onde você deseja tooreplicate para.</span><span class="sxs-lookup"><span data-stu-id="35144-108">Select what you want tooreplicate and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="35144-109">Clique em **Site Recovery** > **Etapa 1: Preparar a Infraestrutura** > **Meta de proteção**.</span><span class="sxs-lookup"><span data-stu-id="35144-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="35144-110">Selecione **toorecovery site**e selecione **Sim, com o Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="35144-110">Select **toorecovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="35144-111">Selecione **Sim** tooindicate você estiver usando os hosts do VMM toomanage Olá Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="35144-111">Select **Yes** tooindicate you're using VMM toomanage hello Hyper-V hosts.</span></span>
4. <span data-ttu-id="35144-112">Selecione **Sim** se você tiver um servidor VMM secundário.</span><span class="sxs-lookup"><span data-stu-id="35144-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="35144-113">Se você estiver implantando a replicação entre nuvens em um único servidor VMM, clique em **Não**.</span><span class="sxs-lookup"><span data-stu-id="35144-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="35144-114">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="35144-114">Then click **OK**.</span></span>

    ![Escolher metas](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="35144-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="35144-116">Next steps</span></span>

<span data-ttu-id="35144-117">Vá muito[etapa 6: configurar a origem de replicação hello e de destino](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="35144-117">Go too[Step 6: Set up hello replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>
