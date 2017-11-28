---
title: "Configurar um cofre para a replicação VMware para o Azure usando o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas necessárias para configurar um cofre para replicação do VMware para o Azure usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: dca95ad46b8de587140c3573ba6ed5702a122032
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-to-azure"></a><span data-ttu-id="17395-103">Etapa 7: configurar um cofre para a replicação do VMware para o Azure</span><span class="sxs-lookup"><span data-stu-id="17395-103">Step 7: Set up a vault for VMware replication to Azure</span></span>


<span data-ttu-id="17395-104">Este artigo descreve como configurar um cofre e especifica o que você deseja replicar de sua localização local para o Azure, usando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="17395-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="17395-105">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="17395-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="17395-106">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="17395-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="17395-107">Selecionar uma meta de proteção</span><span class="sxs-lookup"><span data-stu-id="17395-107">Select a protection goal</span></span>

<span data-ttu-id="17395-108">Selecione o que você deseja replicar e para onde deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="17395-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="17395-109">Clique em **Cofres dos Serviços de Recuperação** > cofre.</span><span class="sxs-lookup"><span data-stu-id="17395-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="17395-110">No Menu Recursos, clique em **Site Recovery** > **Preparar Infraestrutura** > **Meta de proteção**.</span><span class="sxs-lookup"><span data-stu-id="17395-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="17395-111">Em **Meta de proteção**, selecione **Para o Azure** > **Sim, com o Hipervisor VMware vSphere**.</span><span class="sxs-lookup"><span data-stu-id="17395-111">In **Protection goal**, select **To Azure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="17395-112">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="17395-112">Next steps</span></span>

<span data-ttu-id="17395-113">Vá para a [Etapa 8: definir a origem e o destino](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="17395-113">Go to [Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
