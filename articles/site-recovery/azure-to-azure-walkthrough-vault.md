---
title: "Configurar um cofre para replicação de VM do Azure entre regiões com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas necessárias para configurar um cofre para replicação do Azure entre regiões do Azure utilizando o Azure Site Recovery"
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
ms.openlocfilehash: e03d17992ee0b12049636e40188950bcc4a6f31e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="step-4-set-up-a-vault-for-azure-to-azure-replication"></a><span data-ttu-id="56300-103">Etapa 4: configurar um cofre para replicação de Azure para Azure</span><span class="sxs-lookup"><span data-stu-id="56300-103">Step 4: Set up a vault for Azure to Azure replication</span></span>

<span data-ttu-id="56300-104">Após [planejar as redes](azure-to-azure-walkthrough-network.md), utilize este artigo para configurar um cofre para VMs (máquinas virtuais) do Azure replicando para outra região do Azure, utilizando o serviço do [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="56300-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article to set up a vault, for Azure virtual machines (VMs) replicating to another Azure region, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

- <span data-ttu-id="56300-105">Ao concluir o artigo, você deverá ter um cofre dos Serviços de Recuperação configurado.</span><span class="sxs-lookup"><span data-stu-id="56300-105">When you finish the article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="56300-106">Publique eventuais comentários no final deste artigo ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="56300-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="56300-107">Atualmente, a replicação de VM do Azure está em versão prévia.</span><span class="sxs-lookup"><span data-stu-id="56300-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="56300-108">Criar um cofre</span><span class="sxs-lookup"><span data-stu-id="56300-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="56300-109">É recomendável que você crie o cofre de serviços de recuperação no local onde você deseja suas VMs para replicar.</span><span class="sxs-lookup"><span data-stu-id="56300-109">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="56300-110">Por exemplo, se o local de destino é centro dos EUA, crie o cofre no **centro dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="56300-110">For example, if your target location is the central US, create the vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="56300-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="56300-111">Next steps</span></span>

<span data-ttu-id="56300-112">Acesse a [Etapa 5: habilitar a replicação](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="56300-112">Go to [Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
