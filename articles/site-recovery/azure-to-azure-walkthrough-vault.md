---
title: "aaaSet um cofre para VM do Azure repliction entre regiões com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooset um cofre para a replicação entre regiões do Azure usando o Azure Site Recovery do Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a><span data-ttu-id="88e34-103">Etapa 4: Configurar um cofre para replicação tooAzure do Azure</span><span class="sxs-lookup"><span data-stu-id="88e34-103">Step 4: Set up a vault for Azure tooAzure replication</span></span>

<span data-ttu-id="88e34-104">Depois de [Planejando redes](azure-to-azure-walkthrough-network.md), use este tooset artigo um cofre, para máquinas virtuais (VMs) do Azure replicando tooanother região do Azure, usando Olá [Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="88e34-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article tooset up a vault, for Azure virtual machines (VMs) replicating tooanother Azure region, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="88e34-105">Quando você terminar de artigo hello, você deve ter um cofre de serviços de recuperação configurado.</span><span class="sxs-lookup"><span data-stu-id="88e34-105">When you finish hello article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="88e34-106">Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="88e34-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="88e34-107">Atualmente, a replicação de VM do Azure está em versão prévia.</span><span class="sxs-lookup"><span data-stu-id="88e34-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="88e34-108">Criar um cofre</span><span class="sxs-lookup"><span data-stu-id="88e34-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="88e34-109">É recomendável que você crie Olá Cofre de serviços de recuperação no local de saudação onde você deseja que seu tooreplicate VMs.</span><span class="sxs-lookup"><span data-stu-id="88e34-109">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="88e34-110">Por exemplo, se o local de destino é hello central nos, criar hello cofre no **centro dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="88e34-110">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="88e34-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88e34-111">Next steps</span></span>

<span data-ttu-id="88e34-112">Vá muito[etapa 5: habilitar a replicação](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="88e34-112">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
