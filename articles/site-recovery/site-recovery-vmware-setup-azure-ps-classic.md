---
title: " Gerenciar um servidor de processo em execução em Azure(Classic) | Microsoft Docs"
description: Este artigo descreve como configurar um failback Server(Classic) do processo no Azure.
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
ms.openlocfilehash: 479bbd207bcf715138c340f9e4d2634120bab85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="ec3b8-103">Gerenciar um servidor de processo em execução no Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="ec3b8-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec3b8-104">Azure Clássico </span><span class="sxs-lookup"><span data-stu-id="ec3b8-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="ec3b8-105">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="ec3b8-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="ec3b8-106">Durante o failback, é recomendável implantar o servidor de processo no Azure se houver alta latência entre a rede Virtual do Azure e sua rede local.</span><span class="sxs-lookup"><span data-stu-id="ec3b8-106">During failback, it is recommended to deploy Process Server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="ec3b8-107">Este artigo descreve como você pode definir, configurar e gerenciar os servidores de processo em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="ec3b8-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="ec3b8-108">Use este artigo se você tiver utilizado o Classic como o modelo de implantação para as máquinas virtuais durante o failover.</span><span class="sxs-lookup"><span data-stu-id="ec3b8-108">This article is to be used if you used Classic as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="ec3b8-109">Se você usou o Gerenciador de Recursos como o modelo de implantação, siga as etapas em [Como configurar um servidor de processo de Failback (Gerenciador de recursos)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="ec3b8-109">If you used Resource Manager as the deployment model follow the steps in [How to set up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec3b8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ec3b8-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="ec3b8-111">Implantar um Servidor de Processos no Azure</span><span class="sxs-lookup"><span data-stu-id="ec3b8-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="ec3b8-112">No Azure Marketplace, criar uma máquina virtual usando o **servidor Microsoft Azure Site Recovery processo V2**</span><span class="sxs-lookup"><span data-stu-id="ec3b8-112">In Azure Marketplace, create a virtual machine using the **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="ec3b8-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="ec3b8-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="ec3b8-114">Certifique-se de que você selecione o modelo de implantação como **clássico**</span><span class="sxs-lookup"><span data-stu-id="ec3b8-114">Ensure that you select the deployment model as **Classic**</span></span> </br><span data-ttu-id="ec3b8-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="ec3b8-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="ec3b8-116">No assistente criar máquina virtual > configurações básicas, certifique-se de selecionar a assinatura e o local para onde foi feito o failover de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="ec3b8-116">In the Create virtual machine wizard > Basic Settings, ensure you select the Subscription and Location to where you failed over the virtual machines.</span></span></br><span data-ttu-id="ec3b8-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="ec3b8-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="ec3b8-118">Verifique se a máquina virtual está conectada à rede Virtual do Azure ao qual a falha pela máquina virtual está conectado.</span><span class="sxs-lookup"><span data-stu-id="ec3b8-118">Ensure that the virtual machine is connected to the Azure Virtual Network to which the failed over virtual machine is connected.</span></span></br><span data-ttu-id="ec3b8-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="ec3b8-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="ec3b8-120">Depois de máquina virtual do servidor de processo é configurada, você precisa entrar e registrá-lo com o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="ec3b8-120">Once the Process Server virtual machine is provisioned, you need to log in and register it with the Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="ec3b8-121">Para poder usar este servidor de processo para failback, você precisa registrá-lo com o servidor de configuração local.</span><span class="sxs-lookup"><span data-stu-id="ec3b8-121">To be able to use this Process Server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="ec3b8-122">Registrando o servidor de processo (em execução no Azure) para um servidor de configuração (em execução local)</span><span class="sxs-lookup"><span data-stu-id="ec3b8-122">Registering the Process Server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="ec3b8-123">Atualizar o servidor de processo para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="ec3b8-123">Upgrading the Process Server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="ec3b8-124">Cancelando o registro de servidor de processo (em execução no Azure) de um servidor de configuração (em execução local)</span><span class="sxs-lookup"><span data-stu-id="ec3b8-124">Unregistering the Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
