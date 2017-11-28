---
title: "Configurar um cofre para a replicação de servidor físico para o Azure usando o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas necessárias para configurar um cofre para replicar servidores físicos para o Azure usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: deb5ad0495edc969b374795eeb2698326dd4ff4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-to-azure"></a><span data-ttu-id="3d5a7-103">Etapa 6: Configurar um cofre para a replicação de servidor físico para o Azure</span><span class="sxs-lookup"><span data-stu-id="3d5a7-103">Step 6: Set up a vault for physical server replication to Azure</span></span>


<span data-ttu-id="3d5a7-104">Este artigo descreve como configurar um cofre.</span><span class="sxs-lookup"><span data-stu-id="3d5a7-104">This article describes how to set up a vault.</span></span> <span data-ttu-id="3d5a7-105">Você cria o cofre e especifica o que deseja replicar de sua localização local para o Azure, usando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d5a7-105">You create the vault, and specify what you want to replicate from your on-premises location to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="3d5a7-106">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3d5a7-106">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="3d5a7-107">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="3d5a7-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="3d5a7-108">Selecionar uma meta de proteção</span><span class="sxs-lookup"><span data-stu-id="3d5a7-108">Select a protection goal</span></span>

<span data-ttu-id="3d5a7-109">Selecione o que você deseja replicar e para onde deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="3d5a7-109">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="3d5a7-110">Clique em **Cofres dos Serviços de Recuperação** > cofre.</span><span class="sxs-lookup"><span data-stu-id="3d5a7-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="3d5a7-111">No Menu Recursos, clique em **Site Recovery** > **Preparar Infraestrutura** > **Meta de proteção**.</span><span class="sxs-lookup"><span data-stu-id="3d5a7-111">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="3d5a7-112">Em **Meta de proteção**, selecione **Para o Azure** > **Não virtualizado/Outro**.</span><span class="sxs-lookup"><span data-stu-id="3d5a7-112">In **Protection goal**, select **To Azure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3d5a7-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d5a7-113">Next steps</span></span>

<span data-ttu-id="3d5a7-114">Ir para a [Etapa 7: Definir a origem e o destino](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="3d5a7-114">Go to [Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
