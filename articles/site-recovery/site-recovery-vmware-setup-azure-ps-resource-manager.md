---
title: " Gerenciar um servidor de processo em execução no Azure (Gerenciador de Recursos) | Microsoft Docs"
description: Este artigo descreve como configurar um servidor de processo de failback (Resource Manager) no Azure.
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
ms.openlocfilehash: 2b9b31abd5d11d02935a74e47d26be9803cdc920
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="e76b8-103">Gerenciar um servidor de processo em execução no Azure (Gerenciador de recursos)</span><span class="sxs-lookup"><span data-stu-id="e76b8-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e76b8-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="e76b8-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="e76b8-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="e76b8-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="e76b8-106">Durante o failback, é recomendável implantar o servidor de processo no Azure se houver alta latência entre a rede Virtual do Azure e sua rede local.</span><span class="sxs-lookup"><span data-stu-id="e76b8-106">During failback, it is recommended to deploy process server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="e76b8-107">Este artigo descreve como você pode definir, configurar e gerenciar os servidores de processo em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="e76b8-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e76b8-108">Use este artigo se você tiver utilizado o **Resource Manager** como o modelo de implantação para as máquinas virtuais durante o failover.</span><span class="sxs-lookup"><span data-stu-id="e76b8-108">This article is to be used if you used **Resource Manager** as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="e76b8-109">Se você usou **Clássico** como o modelo de implantação, siga as etapas em [Como configurar um servidor de processo de Failback (Clássico)](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="e76b8-109">If you used **Classic** as the deployment model, follow the steps in [How to set up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e76b8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e76b8-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="e76b8-111">Implantar um servidor de processos no Azure</span><span class="sxs-lookup"><span data-stu-id="e76b8-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="e76b8-112">Em Cofre > **Infraestrutura do Site Recovery** (no cabeçalho “Gerenciar”) > **Servidores de Configuração** (no cabeçalho “Para VMware e Máquinas Físicas”), selecione o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e76b8-112">In the Vault > **Site Recovery Infrastructure** (under the "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select the configuration server.</span></span>
2. <span data-ttu-id="e76b8-113">Na página de detalhes do servidor de configuração que é aberta, clique em "+ servidor de processo"</span><span class="sxs-lookup"><span data-stu-id="e76b8-113">In the Configuration Server details page that opens click "+ Process server"</span></span>

  ![Adicionar a Galeria do servidor de processo](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="e76b8-115">Sobre o **Adicionar servidor de processo** , selecione os seguintes valores</span><span class="sxs-lookup"><span data-stu-id="e76b8-115">On the **Add process server** page, select the following values</span></span>

  ![Adicionar item da galeria do servidor de processo](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="e76b8-117">**Nome do Campo**</span><span class="sxs-lookup"><span data-stu-id="e76b8-117">**Field Name**</span></span>|<span data-ttu-id="e76b8-118">**Valor**</span><span class="sxs-lookup"><span data-stu-id="e76b8-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="e76b8-119">Escolha onde você deseja implantar o servidor de processo</span><span class="sxs-lookup"><span data-stu-id="e76b8-119">Choose where you want to deploy your process server</span></span>|<span data-ttu-id="e76b8-120">Selecione o valor **implantar um servidor de processo de failback no Azure**</span><span class="sxs-lookup"><span data-stu-id="e76b8-120">Select the value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="e76b8-121">Assinatura</span><span class="sxs-lookup"><span data-stu-id="e76b8-121">Subscription</span></span>|<span data-ttu-id="e76b8-122">Selecione a assinatura do Azure onde você fez failover das máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="e76b8-122">Select the Azure Subscription where you failed over the virtual machines</span></span>|
|<span data-ttu-id="e76b8-123">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e76b8-123">Resource Group</span></span>|<span data-ttu-id="e76b8-124">Você pode criar um grupo de recursos para implantar este servidor de processo ou optar por implantar o servidor de processo em um grupo de recursos existente</span><span class="sxs-lookup"><span data-stu-id="e76b8-124">You can create a Resource Group to deploy this process server or choose to deploy the process server in an existing Resource Group</span></span>|
|<span data-ttu-id="e76b8-125">Local</span><span class="sxs-lookup"><span data-stu-id="e76b8-125">Location</span></span>|<span data-ttu-id="e76b8-126">Selecione o Data Center do Azure no qual as máquinas virtuais onde falhou em</span><span class="sxs-lookup"><span data-stu-id="e76b8-126">Select the Azure Data Center into which the virtual machines where failed over into</span></span>|
|<span data-ttu-id="e76b8-127">Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="e76b8-127">Azure Network</span></span>|<span data-ttu-id="e76b8-128">Selecione o Network(VNet) Virtual do Azure que as máquinas virtuais onde o failover em.</span><span class="sxs-lookup"><span data-stu-id="e76b8-128">Select the Azure Virtual Network(VNet) that the virtual machines where failed over into.</span></span> <span data-ttu-id="e76b8-129">Se você fez failover máquinas virtuais em vários VNets do Azure, em seguida, é necessário um servidor de processo implantado por rede virtual</span><span class="sxs-lookup"><span data-stu-id="e76b8-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="e76b8-130">Preencha o restante das propriedades do servidor de processo</span><span class="sxs-lookup"><span data-stu-id="e76b8-130">Fill in the rest of the properties for the process server</span></span>

  ![Adicionar servidor de processo resumo](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="e76b8-132">**Nome do Campo**</span><span class="sxs-lookup"><span data-stu-id="e76b8-132">**Field Name**</span></span>|<span data-ttu-id="e76b8-133">**Valor**</span><span class="sxs-lookup"><span data-stu-id="e76b8-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="e76b8-134">Nome do Servidor</span><span class="sxs-lookup"><span data-stu-id="e76b8-134">Server Name</span></span>|<span data-ttu-id="e76b8-135">Nome de exibição < / nome de Host para sua máquina de virtual do servidor de processo</span><span class="sxs-lookup"><span data-stu-id="e76b8-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="e76b8-136">Nome de usuário</span><span class="sxs-lookup"><span data-stu-id="e76b8-136">User Name</span></span>|<span data-ttu-id="e76b8-137">Um nome de usuário que se torna um administrador na máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e76b8-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="e76b8-138">Conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e76b8-138">Storage Account</span></span>|<span data-ttu-id="e76b8-139">Nome da conta de armazenamento em que é colocado do disco virtual da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e76b8-139">Name of the Storage Account where the virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="e76b8-140">Sub-rede</span><span class="sxs-lookup"><span data-stu-id="e76b8-140">Subnet</span></span>|<span data-ttu-id="e76b8-141">A sub-rede da rede virtual do Azure à qual a máquina virtual está conectada</span><span class="sxs-lookup"><span data-stu-id="e76b8-141">The subnet of the Azure VNet to which the virtual machine is connected</span></span>|
| <span data-ttu-id="e76b8-142">Endereço IP</span><span class="sxs-lookup"><span data-stu-id="e76b8-142">IP Address</span></span>|<span data-ttu-id="e76b8-143">Endereço IP que você deseja que o servidor de processo uma vez assumi-lo inicializado</span><span class="sxs-lookup"><span data-stu-id="e76b8-143">IP Address that you would like the process server to assume once it boots up</span></span>|
5. <span data-ttu-id="e76b8-144">Clique no botão Okey para iniciar a máquina virtual do processo servidor de implantação.</span><span class="sxs-lookup"><span data-stu-id="e76b8-144">Click the OK button to start deploying the process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="e76b8-145">Para poder usar este servidor de processo para failback, você precisa registrá-lo com o servidor de configuração local.</span><span class="sxs-lookup"><span data-stu-id="e76b8-145">To be able to use this process server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="e76b8-146">Registrando o servidor de processo (em execução no Azure) para um servidor de configuração (em execução local)</span><span class="sxs-lookup"><span data-stu-id="e76b8-146">Registering the process server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="e76b8-147">Atualizar o servidor de processo para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="e76b8-147">Upgrading the process server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="e76b8-148">Cancelando o registro de servidor de processo (em execução no Azure) de um servidor de configuração (em execução local)</span><span class="sxs-lookup"><span data-stu-id="e76b8-148">Unregistering the process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
