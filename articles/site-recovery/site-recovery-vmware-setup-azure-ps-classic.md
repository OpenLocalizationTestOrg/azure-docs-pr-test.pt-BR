---
title: " Gerenciar um servidor de processo em execução em Azure(Classic) | Microsoft Docs"
description: Este artigo descreve como tooset backup um failback Server(Classic) do processo no Azure.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="eb159-103">Gerenciar um servidor de processo em execução no Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="eb159-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb159-104">Azure Clássico </span><span class="sxs-lookup"><span data-stu-id="eb159-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="eb159-105">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="eb159-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="eb159-106">Durante o failback, é recomendável toodeploy servidor de processo no Azure se houver alta latência entre hello rede Virtual do Azure e sua rede local.</span><span class="sxs-lookup"><span data-stu-id="eb159-106">During failback, it is recommended toodeploy Process Server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="eb159-107">Este artigo descreve como você pode configurar, configurar e gerenciar servidores de processo Olá em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="eb159-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="eb159-108">Este artigo é toobe usado se você usou clássico como modelo de implantação de saudação para máquinas virtuais de saudação durante o failover.</span><span class="sxs-lookup"><span data-stu-id="eb159-108">This article is toobe used if you used Classic as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="eb159-109">Se você usou o Gerenciador de recursos como Olá implantação modelo siga Olá etapas [como tooset up e configurar um servidor de processo de Failback (Gerenciador de recursos)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="eb159-109">If you used Resource Manager as hello deployment model follow hello steps in [How tooset up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb159-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eb159-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="eb159-111">Implantar um Servidor de Processos no Azure</span><span class="sxs-lookup"><span data-stu-id="eb159-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="eb159-112">No Azure Marketplace, criar uma máquina virtual usando Olá **V2 de servidor do Microsoft Azure Site Recovery processo**</span><span class="sxs-lookup"><span data-stu-id="eb159-112">In Azure Marketplace, create a virtual machine using hello **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="eb159-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="eb159-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="eb159-114">Certifique-se de que você selecione o modelo de implantação hello como **clássico**</span><span class="sxs-lookup"><span data-stu-id="eb159-114">Ensure that you select hello deployment model as **Classic**</span></span> </br><span data-ttu-id="eb159-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="eb159-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="eb159-116">No Assistente de máquina virtual de criar hello > configurações básicas, certifique-se de selecionar Olá toowhere assinatura e local de failover de máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb159-116">In hello Create virtual machine wizard > Basic Settings, ensure you select hello Subscription and Location toowhere you failed over hello virtual machines.</span></span></br><span data-ttu-id="eb159-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="eb159-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="eb159-118">Certifique-se de que a máquina virtual hello está conectada Olá de toowhich de rede Virtual do Azure toohello failover da máquina virtual está conectado.</span><span class="sxs-lookup"><span data-stu-id="eb159-118">Ensure that hello virtual machine is connected toohello Azure Virtual Network toowhich hello failed over virtual machine is connected.</span></span></br><span data-ttu-id="eb159-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="eb159-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="eb159-120">Depois que a máquina de virtual do servidor de processo Olá é provisionada, você precisa toolog no e registrá-lo com hello servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="eb159-120">Once hello Process Server virtual machine is provisioned, you need toolog in and register it with hello Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="eb159-121">toouse capaz de toobe este servidor de processo para failback, você precisa tooregistê-lo com o servidor de configuração local hello.</span><span class="sxs-lookup"><span data-stu-id="eb159-121">toobe able toouse this Process Server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="eb159-122">Saudação (em execução no Azure) do servidor de processo tooa (executado no local) do servidor de configuração de registro</span><span class="sxs-lookup"><span data-stu-id="eb159-122">Registering hello Process Server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="eb159-123">Saudação do servidor em processo toolatest a versão da atualização.</span><span class="sxs-lookup"><span data-stu-id="eb159-123">Upgrading hello Process Server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="eb159-124">Olá Cancelando o registro do servidor de processo (em execução no Azure) de um servidor de configuração (executado no local)</span><span class="sxs-lookup"><span data-stu-id="eb159-124">Unregistering hello Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
