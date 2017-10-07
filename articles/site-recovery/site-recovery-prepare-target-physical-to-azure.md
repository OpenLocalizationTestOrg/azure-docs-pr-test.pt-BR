---
title: "Preparar o destino (físico tooAzure) | Microsoft Docs"
description: "Este artigo descreve como tooprepare toostart seu ambiente do Azure que replicação de servidores físicos executando tooAzure Windows ou Linux."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 126fb86133e1a00f5669410943565c4cd78e4369
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a><span data-ttu-id="6bc4a-103">Preparar o destino (tooAzure VMware)</span><span class="sxs-lookup"><span data-stu-id="6bc4a-103">Prepare target (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6bc4a-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="6bc4a-104">VMware tooAzure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="6bc4a-105">TooAzure físico</span><span class="sxs-lookup"><span data-stu-id="6bc4a-105">Physical tooAzure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="6bc4a-106">Este artigo descreve como tooprepare toostart seu ambiente do Azure que replicação de servidores físicos (x64) executando o Windows ou Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="6bc4a-106">This article describes how tooprepare your Azure environment toostart replicating physical servers (x64) running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bc4a-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6bc4a-107">Prerequisites</span></span>

<span data-ttu-id="6bc4a-108">artigo de saudação pressupõe seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="6bc4a-108">hello article assumes hello following:</span></span>
- <span data-ttu-id="6bc4a-109">Você criou um cofre de serviços de recuperação tooprotect seus servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="6bc4a-109">You have created a Recovery Services Vault tooprotect your physical servers.</span></span> <span data-ttu-id="6bc4a-110">Você pode criar um cofre de serviços de recuperação de saudação [portal do Azure](http://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="6bc4a-110">You can create a Recovery Services Vault from hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="6bc4a-111">Você tem [configurar seu ambiente local](./site-recovery-set-up-physical-to-azure.md) tooreplicate tooAzure de servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="6bc4a-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) tooreplicate physical servers tooAzure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="6bc4a-112">Preparar o destino</span><span class="sxs-lookup"><span data-stu-id="6bc4a-112">Prepare target</span></span>

<span data-ttu-id="6bc4a-113">Depois de concluir a saudação **objetivo de proteção etapa 1: selecione** e **etapa 2: preparar fonte**, você será direcionado muito**etapa 3: destino**</span><span class="sxs-lookup"><span data-stu-id="6bc4a-113">After completing hello **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken too**Step 3: Target**</span></span>

![Preparar o destino](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. <span data-ttu-id="6bc4a-115">**Assinatura:** de saudação menu suspenso, selecione Olá assinatura que você deseja tooreplicate seus servidores físicos em.</span><span class="sxs-lookup"><span data-stu-id="6bc4a-115">**Subscription:** From hello drop down menu, select hello Subscription that you want tooreplicate your physical servers to.</span></span>
2. <span data-ttu-id="6bc4a-116">**Modelo de implantação:** modelo de implantação de saudação Select (clássico ou Gerenciador de recursos)</span><span class="sxs-lookup"><span data-stu-id="6bc4a-116">**Deployment Model:** Select hello deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="6bc4a-117">Com base em Olá escolhida o modelo de implantação, validação é executada tooensure que você tem pelo menos uma conta de armazenamento e rede virtual em Olá tooreplicate de assinatura de destino e o failover seus servidores físicos em.</span><span class="sxs-lookup"><span data-stu-id="6bc4a-117">Based on hello chosen deployment model, a validation is run tooensure that you have at least one compatible storage account and virtual network in hello target subscription tooreplicate and failover your physical servers to.</span></span>

<span data-ttu-id="6bc4a-118">Depois que as validações de saudação concluída com êxito, clique em toogo Okey toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="6bc4a-118">Once hello validations complete successfully, click OK toogo toohello next step.</span></span>

<span data-ttu-id="6bc4a-119">Se você não tiver uma conta de armazenamento compatível com o Gerenciador de recursos ou a rede virtual, ou gostaria tooadd mais, você pode fazer isso clicando Olá **+ conta de armazenamento** ou **+ rede** botões na parte superior de saudação do hello folha.</span><span class="sxs-lookup"><span data-stu-id="6bc4a-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like tooadd more, you can do so by clicking hello **+ Storage Account** or **+ Network** buttons on hello top of hello blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bc4a-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6bc4a-120">Next steps</span></span>
<span data-ttu-id="6bc4a-121">[Definir configurações de replicação](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="6bc4a-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
