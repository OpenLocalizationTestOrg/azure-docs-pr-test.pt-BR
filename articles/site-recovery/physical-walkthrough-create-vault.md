---
title: "aaaSet um cofre para o servidor físico tooAzure de replicação usando o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooset a um tooAzure de servidores físicos do cofre tooreplicate usando o Azure Site Recovery"
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
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a><span data-ttu-id="8e621-103">Etapa 6: Configurar um cofre para tooAzure de replicação de servidor físico</span><span class="sxs-lookup"><span data-stu-id="8e621-103">Step 6: Set up a vault for physical server replication tooAzure</span></span>


<span data-ttu-id="8e621-104">Este artigo descreve como tooset um cofre.</span><span class="sxs-lookup"><span data-stu-id="8e621-104">This article describes how tooset up a vault.</span></span> <span data-ttu-id="8e621-105">Criar cofre Olá e especifique o que você deseja tooreplicate do seu local local tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e621-105">You create hello vault, and specify what you want tooreplicate from your on-premises location tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="8e621-106">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8e621-106">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="8e621-107">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="8e621-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="8e621-108">Selecionar uma meta de proteção</span><span class="sxs-lookup"><span data-stu-id="8e621-108">Select a protection goal</span></span>

<span data-ttu-id="8e621-109">Selecione o que você deseja tooreplicate, e onde você deseja tooreplicate para.</span><span class="sxs-lookup"><span data-stu-id="8e621-109">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="8e621-110">Clique em **Cofres dos Serviços de Recuperação** > cofre.</span><span class="sxs-lookup"><span data-stu-id="8e621-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="8e621-111">No hello recurso de Menu, clique em **recuperação de Site** > **preparar a infraestrutura** > **objetivo de proteção**.</span><span class="sxs-lookup"><span data-stu-id="8e621-111">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="8e621-112">Em **objetivo de proteção**, selecione **tooAzure** > **não virtualizados/outros**.</span><span class="sxs-lookup"><span data-stu-id="8e621-112">In **Protection goal**, select **tooAzure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8e621-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8e621-113">Next steps</span></span>

<span data-ttu-id="8e621-114">Vá muito[etapa 7: configurar a origem e destino](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="8e621-114">Go too[Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
