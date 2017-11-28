---
title: "Definir um cofre para replicação do Hyper-V (sem o System Center VMM) para o Azure usando o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas necessárias para configurar um cofre para replicação do Hyper-V para o Azure usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 8212ff011633c3a89d3310e828b6d5f1cda6ce3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="97f5b-103">Etapa 7: configurar um cofre para replicação do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="97f5b-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="97f5b-104">Este artigo descreve como configurar um cofre e especifica o que você deseja replicar de sua localização local para o Azure, usando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="97f5b-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="97f5b-105">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="97f5b-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="97f5b-106">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="97f5b-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="97f5b-107">Selecionar uma meta de proteção</span><span class="sxs-lookup"><span data-stu-id="97f5b-107">Select a protection goal</span></span>

<span data-ttu-id="97f5b-108">Selecione o que você deseja replicar e para onde deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="97f5b-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="97f5b-109">Clique em **Cofres dos Serviços de Recuperação** > cofre.</span><span class="sxs-lookup"><span data-stu-id="97f5b-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="97f5b-110">No Menu Recursos, clique em **Site Recovery** > **Preparar Infraestrutura** > **Meta de proteção**.</span><span class="sxs-lookup"><span data-stu-id="97f5b-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="97f5b-111">Em **Objetivo de proteção**, selecione **Para o Azure** > **Sim, com o Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="97f5b-111">In **Protection goal**, select **To Azure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="97f5b-112">Selecione **Não** para confirmar que você não está usando o VMM.</span><span class="sxs-lookup"><span data-stu-id="97f5b-112">Select **No** to confirm you're not using VMM.</span></span> 

    ![Escolher metas](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="97f5b-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97f5b-114">Next steps</span></span>

<span data-ttu-id="97f5b-115">Vá para a [Etapa 8: definir a origem e o destino](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="97f5b-115">Go to [Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
