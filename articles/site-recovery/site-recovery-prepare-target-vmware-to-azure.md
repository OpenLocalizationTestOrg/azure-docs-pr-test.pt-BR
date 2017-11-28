---
title: Preparar destino (VMware para Azure) | Microsoft Docs
description: "Este artigo descreve como configurar seu ambiente do Azure para iniciar a replicação de máquinas virtuais VMware no Azure."
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
ms.openlocfilehash: c84a775564769ddc796aa9d75add019ef1003175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="7ed4d-103">Preparar destino (VMware para Azure)</span><span class="sxs-lookup"><span data-stu-id="7ed4d-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ed4d-104">VMware no Azure</span><span class="sxs-lookup"><span data-stu-id="7ed4d-104">VMware to Azure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="7ed4d-105">Físico para Azure</span><span class="sxs-lookup"><span data-stu-id="7ed4d-105">Physical to Azure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="7ed4d-106">Este artigo descreve como configurar seu ambiente do Azure para iniciar a replicação de máquinas virtuais VMware no Azure.</span><span class="sxs-lookup"><span data-stu-id="7ed4d-106">This article describes how to prepare your Azure environment to start replicating VMware virtual machines to Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ed4d-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7ed4d-107">Prerequisites</span></span>

<span data-ttu-id="7ed4d-108">O artigo pressupõe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7ed4d-108">The article assumes the following:</span></span>
- <span data-ttu-id="7ed4d-109">Você criou um Cofre dos Serviços de Recuperação para proteger suas máquinas virtuais VMware.</span><span class="sxs-lookup"><span data-stu-id="7ed4d-109">You have created a Recovery Services Vault to protect your VMware virtual machines.</span></span> <span data-ttu-id="7ed4d-110">Você pode criar um Cofre dos Serviços de Recuperação no [Portal do Azure](http://portal.azure.com "Portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="7ed4d-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="7ed4d-111">Você [configurou seu ambiente local](./site-recovery-set-up-vmware-to-azure.md) para replicar máquinas virtuais VMware no Azure.</span><span class="sxs-lookup"><span data-stu-id="7ed4d-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) to replicate VMware virtual machines to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="7ed4d-112">Preparar o destino</span><span class="sxs-lookup"><span data-stu-id="7ed4d-112">Prepare target</span></span>

<span data-ttu-id="7ed4d-113">Depois de concluir a **Etapa 1: Selecionar meta de proteção** e a **Etapa 2: Preparar origem**, você segue para a **Etapa 3: Destino**</span><span class="sxs-lookup"><span data-stu-id="7ed4d-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![Preparar o destino](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. <span data-ttu-id="7ed4d-115">**Assinatura:** no menu suspenso, escolha a assinatura na qual você quer replicar suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="7ed4d-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your virtual machines to.</span></span>
2. <span data-ttu-id="7ed4d-116">**Modelo de Implantação:** escolha o modelo de implantação (Clássico ou Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="7ed4d-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="7ed4d-117">Com base no modelo de implantação escolhido, uma validação é executada para garantir que você tenha pelo menos uma conta de armazenamento compatível e a rede virtual na assinatura de destino na qual replicar e fazer failover da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7ed4d-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your virtual machine to.</span></span>

<span data-ttu-id="7ed4d-118">Depois que as validações são concluídas com êxito, clique em OK de modo a passar para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="7ed4d-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="7ed4d-119">Caso não tenha uma rede virtual ou conta de armazenamento do Resource Manager compatível, ou queira adicionar mais, você pode fazer isso clicando nos botões **+ Conta de Armazenamento** ou **+ Rede** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="7ed4d-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ed4d-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7ed4d-120">Next steps</span></span>
<span data-ttu-id="7ed4d-121">[Definir configurações de replicação](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="7ed4d-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
