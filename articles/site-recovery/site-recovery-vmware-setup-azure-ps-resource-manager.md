---
title: " Gerenciar um servidor de processo em execução no Azure (Gerenciador de Recursos) | Microsoft Docs"
description: Este artigo descreve como tooset backup um failback processo server (Gerenciador de recursos) no Azure.
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
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="39b47-103">Gerenciar um servidor de processo em execução no Azure (Gerenciador de recursos)</span><span class="sxs-lookup"><span data-stu-id="39b47-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="39b47-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="39b47-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="39b47-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="39b47-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="39b47-106">Durante o failback, é recomendável toodeploy servidor de processo no Azure se houver alta latência entre hello rede Virtual do Azure e sua rede local.</span><span class="sxs-lookup"><span data-stu-id="39b47-106">During failback, it is recommended toodeploy process server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="39b47-107">Este artigo descreve como você pode configurar, configurar e gerenciar servidores de processo Olá em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="39b47-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="39b47-108">Este artigo é toobe usado se você usou **Gerenciador de recursos** como modelo de implantação de saudação para máquinas virtuais de saudação durante o failover.</span><span class="sxs-lookup"><span data-stu-id="39b47-108">This article is toobe used if you used **Resource Manager** as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="39b47-109">Se você usou **clássico** como modelo de implantação hello, siga as etapas de saudação em [como tooset up e configurar um servidor de processo de Failback (clássico)](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="39b47-109">If you used **Classic** as hello deployment model, follow hello steps in [How tooset up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39b47-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="39b47-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="39b47-111">Implantar um servidor de processos no Azure</span><span class="sxs-lookup"><span data-stu-id="39b47-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="39b47-112">No cofre de saudação > **infra-estrutura de recuperação de Site** (sob o título de "Gerenciar" hello) > **servidores de configuração** (sob o título "Para VMware e máquinas físicas"), selecione o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="39b47-112">In hello Vault > **Site Recovery Infrastructure** (under hello "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select hello configuration server.</span></span>
2. <span data-ttu-id="39b47-113">Na página de detalhes do servidor de configuração Olá abre, clique em "+ processar servidor"</span><span class="sxs-lookup"><span data-stu-id="39b47-113">In hello Configuration Server details page that opens click "+ Process server"</span></span>

  ![Adicionar a Galeria do servidor de processo](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="39b47-115">Em Olá **Adicionar servidor de processo** página, selecione Olá valores a seguir</span><span class="sxs-lookup"><span data-stu-id="39b47-115">On hello **Add process server** page, select hello following values</span></span>

  ![Adicionar item da galeria do servidor de processo](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="39b47-117">**Nome do Campo**</span><span class="sxs-lookup"><span data-stu-id="39b47-117">**Field Name**</span></span>|<span data-ttu-id="39b47-118">**Valor**</span><span class="sxs-lookup"><span data-stu-id="39b47-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="39b47-119">Escolha onde deseja toodeploy seu servidor de processo</span><span class="sxs-lookup"><span data-stu-id="39b47-119">Choose where you want toodeploy your process server</span></span>|<span data-ttu-id="39b47-120">Selecione o valor de saudação **implantar um servidor de processo de failback no Azure**</span><span class="sxs-lookup"><span data-stu-id="39b47-120">Select hello value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="39b47-121">Assinatura</span><span class="sxs-lookup"><span data-stu-id="39b47-121">Subscription</span></span>|<span data-ttu-id="39b47-122">Selecione Olá assinatura do Azure onde você fez failover máquinas virtuais de saudação</span><span class="sxs-lookup"><span data-stu-id="39b47-122">Select hello Azure Subscription where you failed over hello virtual machines</span></span>|
|<span data-ttu-id="39b47-123">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="39b47-123">Resource Group</span></span>|<span data-ttu-id="39b47-124">Você pode criar um grupo de recursos toodeploy este servidor de processo ou escolha o servidor de processo Olá toodeploy em um grupo de recursos existente</span><span class="sxs-lookup"><span data-stu-id="39b47-124">You can create a Resource Group toodeploy this process server or choose toodeploy hello process server in an existing Resource Group</span></span>|
|<span data-ttu-id="39b47-125">Local</span><span class="sxs-lookup"><span data-stu-id="39b47-125">Location</span></span>|<span data-ttu-id="39b47-126">Selecione hello Azure Data Center em que máquinas virtuais de saudação onde failover em</span><span class="sxs-lookup"><span data-stu-id="39b47-126">Select hello Azure Data Center into which hello virtual machines where failed over into</span></span>|
|<span data-ttu-id="39b47-127">Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="39b47-127">Azure Network</span></span>|<span data-ttu-id="39b47-128">Selecione Olá Network(VNet) Virtual do Azure que Olá máquinas virtuais em que o failover no.</span><span class="sxs-lookup"><span data-stu-id="39b47-128">Select hello Azure Virtual Network(VNet) that hello virtual machines where failed over into.</span></span> <span data-ttu-id="39b47-129">Se você fez failover máquinas virtuais em vários VNets do Azure, em seguida, é necessário um servidor de processo implantado por rede virtual</span><span class="sxs-lookup"><span data-stu-id="39b47-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="39b47-130">Preencha Olá restante das propriedades Olá para o servidor de processo Olá</span><span class="sxs-lookup"><span data-stu-id="39b47-130">Fill in hello rest of hello properties for hello process server</span></span>

  ![Adicionar servidor de processo resumo](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="39b47-132">**Nome do Campo**</span><span class="sxs-lookup"><span data-stu-id="39b47-132">**Field Name**</span></span>|<span data-ttu-id="39b47-133">**Valor**</span><span class="sxs-lookup"><span data-stu-id="39b47-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="39b47-134">Nome do Servidor</span><span class="sxs-lookup"><span data-stu-id="39b47-134">Server Name</span></span>|<span data-ttu-id="39b47-135">Nome de exibição < / nome de Host para sua máquina de virtual do servidor de processo</span><span class="sxs-lookup"><span data-stu-id="39b47-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="39b47-136">Nome de usuário</span><span class="sxs-lookup"><span data-stu-id="39b47-136">User Name</span></span>|<span data-ttu-id="39b47-137">Um nome de usuário que se torna um administrador na máquina virtual</span><span class="sxs-lookup"><span data-stu-id="39b47-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="39b47-138">Conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="39b47-138">Storage Account</span></span>|<span data-ttu-id="39b47-139">Nome da saudação conta de armazenamento onde é colocado saudação do disco da máquina virtual do</span><span class="sxs-lookup"><span data-stu-id="39b47-139">Name of hello Storage Account where hello virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="39b47-140">Sub-rede</span><span class="sxs-lookup"><span data-stu-id="39b47-140">Subnet</span></span>|<span data-ttu-id="39b47-141">subrede de máquina virtual do hello Azure VNet toowhich Olá Olá está conectado</span><span class="sxs-lookup"><span data-stu-id="39b47-141">hello subnet of hello Azure VNet toowhich hello virtual machine is connected</span></span>|
| <span data-ttu-id="39b47-142">Endereço IP</span><span class="sxs-lookup"><span data-stu-id="39b47-142">IP Address</span></span>|<span data-ttu-id="39b47-143">Endereço IP que deseja Olá tooassume de servidor de processo depois que ele é inicializado</span><span class="sxs-lookup"><span data-stu-id="39b47-143">IP Address that you would like hello process server tooassume once it boots up</span></span>|
5. <span data-ttu-id="39b47-144">Clique em toostart do botão Okey Olá Olá máquina de virtual do servidor de processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="39b47-144">Click hello OK button toostart deploying hello process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="39b47-145">toouse capaz de toobe este servidor de processo para failback, você precisa tooregistê-lo com o servidor de configuração local hello.</span><span class="sxs-lookup"><span data-stu-id="39b47-145">toobe able toouse this process server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="39b47-146">Registrando Olá processo servidor (em execução no Azure) tooa (executado no local) do servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="39b47-146">Registering hello process server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="39b47-147">Atualizando Olá processo toolatest versão do servidor.</span><span class="sxs-lookup"><span data-stu-id="39b47-147">Upgrading hello process server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="39b47-148">Cancelar registro do servidor de processo hello (em execução no Azure) de um servidor de configuração (executado no local)</span><span class="sxs-lookup"><span data-stu-id="39b47-148">Unregistering hello process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
