---
title: "logs de fluxo de grupo de segurança da rede do aaaManage com o observador de rede do Azure | Microsoft Docs"
description: "Esta página explica como toomanage fluxo de grupo de segurança de rede se registra no Inspetor de rede do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a><span data-ttu-id="afce8-103">Gerenciar logs de fluxo de grupo de segurança de rede no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="afce8-103">Manage network security group flow logs in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="afce8-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="afce8-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="afce8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="afce8-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="afce8-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="afce8-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="afce8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="afce8-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="afce8-108">API REST</span><span class="sxs-lookup"><span data-stu-id="afce8-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="afce8-109">Logs de fluxo de grupo de segurança de rede são um recurso do observador de rede que permite que você tooview informações sobre o tráfego IP de entrada e saída por meio de um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="afce8-109">Network security group flow logs are a feature of Network Watcher that enables you tooview information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="afce8-110">Esses logs de fluxo são gravados no formato JSON e fornecem informações importantes, incluindo:</span><span class="sxs-lookup"><span data-stu-id="afce8-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="afce8-111">Fluxos de entrada e saída por regra.</span><span class="sxs-lookup"><span data-stu-id="afce8-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="afce8-112">Olá NIC Olá fluxo aplica-se a.</span><span class="sxs-lookup"><span data-stu-id="afce8-112">hello NIC that hello flow applies to.</span></span>
- <span data-ttu-id="afce8-113">5-tupla informações sobre o fluxo de saudação (origem/destino IP, porta de origem/destino, protocolo).</span><span class="sxs-lookup"><span data-stu-id="afce8-113">5-tuple information about hello flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="afce8-114">Informação sobre o tráfego ter sido permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="afce8-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="afce8-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="afce8-115">Before you begin</span></span>

<span data-ttu-id="afce8-116">Este cenário pressupõe que você já seguiu etapas Olá [criar uma instância do observador de rede](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="afce8-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="afce8-117">cenário de saudação também pressupõe que você tenha um grupo de recursos com uma máquina virtual válido.</span><span class="sxs-lookup"><span data-stu-id="afce8-117">hello scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="afce8-118">Provedor de informações de registro</span><span class="sxs-lookup"><span data-stu-id="afce8-118">Register Insights provider</span></span>

<span data-ttu-id="afce8-119">Fluxo de log toowork com êxito, Olá **Insights** provedor deve ser registrado.</span><span class="sxs-lookup"><span data-stu-id="afce8-119">For flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="afce8-120">provedor de saudação tooregister, Olá execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="afce8-120">tooregister hello provider, take hello following steps:</span></span> 

1. <span data-ttu-id="afce8-121">Vá muito**assinaturas**e em seguida, selecione a assinatura Olá para o qual você deseja tooenable fluxo logs.</span><span class="sxs-lookup"><span data-stu-id="afce8-121">Go too**Subscriptions**, and then select hello subscription for which you want tooenable flow logs.</span></span> 
2. <span data-ttu-id="afce8-122">Em Olá **assinatura** folha, selecione **provedores de recursos**.</span><span class="sxs-lookup"><span data-stu-id="afce8-122">On hello **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="afce8-123">Examinar a lista de saudação de provedores e verifique se esse Olá **Insights** provedor está registrado.</span><span class="sxs-lookup"><span data-stu-id="afce8-123">Look at hello list of providers, and verify that hello **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="afce8-124">Se não estiver, selecione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="afce8-124">If not, then select **Register**.</span></span>

![Exibir provedores][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="afce8-126">Habilitar logs de fluxo</span><span class="sxs-lookup"><span data-stu-id="afce8-126">Enable flow logs</span></span>

<span data-ttu-id="afce8-127">Essas etapas levá-lo pelo processo de saudação de habilitar os logs de fluxo em um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="afce8-127">These steps take you through hello process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="afce8-128">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="afce8-128">Step 1</span></span>

<span data-ttu-id="afce8-129">Acesse a instância do observador de rede tooa e, em seguida, selecione **NSG fluxo logs**.</span><span class="sxs-lookup"><span data-stu-id="afce8-129">Go tooa Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Visão geral dos logs de fluxo][1]

### <a name="step-2"></a><span data-ttu-id="afce8-131">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="afce8-131">Step 2</span></span>

<span data-ttu-id="afce8-132">Selecione um grupo de segurança de rede na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="afce8-132">Select a network security group from hello list.</span></span>

![Visão geral dos logs de fluxo][2]

### <a name="step-3"></a><span data-ttu-id="afce8-134">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="afce8-134">Step 3</span></span> 

<span data-ttu-id="afce8-135">Em Olá **configurações dos logs do fluxo de** folha, definir status da saudação muito**em**e, em seguida, configure uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="afce8-135">On hello **Flow logs settings** blade, set hello status too**On**, and then configure a storage account.</span></span>  <span data-ttu-id="afce8-136">Quando terminar, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="afce8-136">When you're done, select **OK**.</span></span> <span data-ttu-id="afce8-137">Em seguida, selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="afce8-137">Then select **Save**.</span></span>

![Visão geral dos logs de fluxo][3]

## <a name="download-flow-logs"></a><span data-ttu-id="afce8-139">Baixar logs de fluxo</span><span class="sxs-lookup"><span data-stu-id="afce8-139">Download flow logs</span></span>

<span data-ttu-id="afce8-140">Os Logs de fluxo são salvos em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="afce8-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="afce8-141">Baixe o tooview de logs de fluxo-los.</span><span class="sxs-lookup"><span data-stu-id="afce8-141">Download your flow logs tooview them.</span></span>

### <a name="step-1"></a><span data-ttu-id="afce8-142">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="afce8-142">Step 1</span></span>

<span data-ttu-id="afce8-143">logs de fluxo de toodownload, selecione **você pode baixar os logs de fluxo de contas de armazenamento configurado**.</span><span class="sxs-lookup"><span data-stu-id="afce8-143">toodownload flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="afce8-144">Esta etapa usa o modo de exibição de conta de armazenamento tooa onde você pode escolher quais toodownload de logs.</span><span class="sxs-lookup"><span data-stu-id="afce8-144">This step takes you tooa storage account view where you can choose which logs toodownload.</span></span>

![Configurações dos logs do fluxo][4]

### <a name="step-2"></a><span data-ttu-id="afce8-146">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="afce8-146">Step 2</span></span>

<span data-ttu-id="afce8-147">Vá toohello conta de armazenamento correta.</span><span class="sxs-lookup"><span data-stu-id="afce8-147">Go toohello correct storage account.</span></span> <span data-ttu-id="afce8-148">Em seguida, selecione **Contêineres** > **insights-log-networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="afce8-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Configurações dos logs do fluxo][5]

### <a name="step-3"></a><span data-ttu-id="afce8-150">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="afce8-150">Step 3</span></span>

<span data-ttu-id="afce8-151">Vá toohello local do log de fluxo hello, selecioná-lo e, em seguida, selecione **baixar**.</span><span class="sxs-lookup"><span data-stu-id="afce8-151">Go toohello location of hello flow log, select it, and then select **Download**.</span></span>

![Configurações dos logs do fluxo][6]

<span data-ttu-id="afce8-153">Para obter informações sobre a estrutura de saudação do log hello, visite [visão geral do log fluxo de grupo de segurança de rede](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="afce8-153">For information about hello structure of hello log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="afce8-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="afce8-154">Next steps</span></span>

<span data-ttu-id="afce8-155">Saiba como muito[visualizar seus logs de fluxo NSG com PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="afce8-155">Learn how too[visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
