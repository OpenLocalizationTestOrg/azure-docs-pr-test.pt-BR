---
title: "aaaSet um cofre para tooAzure de replicação (sem o System Center VMM) do Hyper-V usando o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooset um cofre para tooAzure de replicação do Hyper-V usando o Azure Site Recovery"
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
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="49e02-103">Etapa 7: configurar um cofre para replicação do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="49e02-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="49e02-104">Este artigo descreve como tooset até um cofre e especifique o que você deseja tooreplicate de sua localização no local, tooAzure usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="49e02-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="49e02-105">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="49e02-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="49e02-106">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="49e02-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="49e02-107">Selecionar uma meta de proteção</span><span class="sxs-lookup"><span data-stu-id="49e02-107">Select a protection goal</span></span>

<span data-ttu-id="49e02-108">Selecione o que você deseja tooreplicate, e onde você deseja tooreplicate para.</span><span class="sxs-lookup"><span data-stu-id="49e02-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="49e02-109">Clique em **Cofres dos Serviços de Recuperação** > cofre.</span><span class="sxs-lookup"><span data-stu-id="49e02-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="49e02-110">No hello recurso de Menu, clique em **recuperação de Site** > **preparar a infraestrutura** > **objetivo de proteção**.</span><span class="sxs-lookup"><span data-stu-id="49e02-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="49e02-111">Em **objetivo de proteção**, selecione **tooAzure** > **Sim, com o Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="49e02-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="49e02-112">Selecione **não** tooconfirm não estiver usando o VMM.</span><span class="sxs-lookup"><span data-stu-id="49e02-112">Select **No** tooconfirm you're not using VMM.</span></span> 

    ![Escolher metas](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="49e02-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49e02-114">Next steps</span></span>

<span data-ttu-id="49e02-115">Vá muito[etapa 8: configurar a origem e destino](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="49e02-115">Go too[Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
