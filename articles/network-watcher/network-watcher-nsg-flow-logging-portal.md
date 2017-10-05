---
title: "Gerenciar logs de fluxo de Grupo de Segurança de Rede com o Observador de Rede do Azure | Microsoft Docs"
description: "Esta página explica como gerenciar logs de fluxo de Grupo de Segurança de Rede no Observador de Rede do Azure"
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
ms.openlocfilehash: 41cb5ffab9bd3a3bed75ffdb6a7383ca1690f810
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-group-flow-logs-in-the-azure-portal"></a><span data-ttu-id="f9e09-103">Gerenciar logs do fluxo do Grupo de Segurança de Rede no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f9e09-103">Manage network security group flow logs in the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f9e09-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f9e09-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="f9e09-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9e09-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="f9e09-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f9e09-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="f9e09-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f9e09-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="f9e09-108">API REST</span><span class="sxs-lookup"><span data-stu-id="f9e09-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="f9e09-109">Logs de fluxo do Grupo de Segurança de Rede são um recurso do Observador de Rede que permite que você exiba informações sobre o tráfego IP de entrada e saída por meio de um Grupo de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="f9e09-109">Network security group flow logs are a feature of Network Watcher that enables you to view information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="f9e09-110">Esses logs de fluxo são gravados no formato JSON e fornecem informações importantes, incluindo:</span><span class="sxs-lookup"><span data-stu-id="f9e09-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="f9e09-111">Fluxos de entrada e saída por regra.</span><span class="sxs-lookup"><span data-stu-id="f9e09-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="f9e09-112">A NIC à qual o fluxo se aplica.</span><span class="sxs-lookup"><span data-stu-id="f9e09-112">The NIC that the flow applies to.</span></span>
- <span data-ttu-id="f9e09-113">Informações de cinco tuplas sobre o fluxo (IP de origem/destino, porta de origem/destino, protocolo).</span><span class="sxs-lookup"><span data-stu-id="f9e09-113">5-tuple information about the flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="f9e09-114">Informação sobre o tráfego ter sido permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="f9e09-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f9e09-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f9e09-115">Before you begin</span></span>

<span data-ttu-id="f9e09-116">Este cenário pressupõe que você já seguiu as etapas em [Criar uma instância de Observador de Rede](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="f9e09-116">This scenario assumes you have already followed the steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="f9e09-117">O cenário também pressupõe que você tem um grupo de recursos com uma máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="f9e09-117">The scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="f9e09-118">Provedor de informações de registro</span><span class="sxs-lookup"><span data-stu-id="f9e09-118">Register Insights provider</span></span>

<span data-ttu-id="f9e09-119">Para o registro de fluxo em log funcionar, o provedor **Microsoft.Insights** deve ser registrado.</span><span class="sxs-lookup"><span data-stu-id="f9e09-119">For flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="f9e09-120">Para registrar o provedor, siga as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f9e09-120">To register the provider, take the following steps:</span></span> 

1. <span data-ttu-id="f9e09-121">Va até **Assinaturas** e selecione a assinatura para a qual deseja habilitar os logs de fluxo.</span><span class="sxs-lookup"><span data-stu-id="f9e09-121">Go to **Subscriptions**, and then select the subscription for which you want to enable flow logs.</span></span> 
2. <span data-ttu-id="f9e09-122">Na folha **Assinatura**, selecione **Provedores de Recursos**.</span><span class="sxs-lookup"><span data-stu-id="f9e09-122">On the **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="f9e09-123">Confira a lista de provedores e verifique se o provedor **microsoft.insights** está registrado.</span><span class="sxs-lookup"><span data-stu-id="f9e09-123">Look at the list of providers, and verify that the **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="f9e09-124">Se não estiver, selecione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="f9e09-124">If not, then select **Register**.</span></span>

![Exibir provedores][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="f9e09-126">Habilitar logs de fluxo</span><span class="sxs-lookup"><span data-stu-id="f9e09-126">Enable flow logs</span></span>

<span data-ttu-id="f9e09-127">Estas etapas guiarão você pelo processo de habilitação dos logs de fluxo em um Grupo de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="f9e09-127">These steps take you through the process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="f9e09-128">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="f9e09-128">Step 1</span></span>

<span data-ttu-id="f9e09-129">Vá até uma instância do Observador de Rede e selecione **Logs de fluxo de NSG**.</span><span class="sxs-lookup"><span data-stu-id="f9e09-129">Go to a Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Visão geral dos logs de fluxo][1]

### <a name="step-2"></a><span data-ttu-id="f9e09-131">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="f9e09-131">Step 2</span></span>

<span data-ttu-id="f9e09-132">Selecione um Grupo de Segurança de Rede na lista.</span><span class="sxs-lookup"><span data-stu-id="f9e09-132">Select a network security group from the list.</span></span>

![Visão geral dos logs de fluxo][2]

### <a name="step-3"></a><span data-ttu-id="f9e09-134">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="f9e09-134">Step 3</span></span> 

<span data-ttu-id="f9e09-135">Na folha **Configurações dos logs do fluxo**, defina o status como **Ligado** e configure uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f9e09-135">On the **Flow logs settings** blade, set the status to **On**, and then configure a storage account.</span></span>  <span data-ttu-id="f9e09-136">Quando terminar, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9e09-136">When you're done, select **OK**.</span></span> <span data-ttu-id="f9e09-137">Em seguida, selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f9e09-137">Then select **Save**.</span></span>

![Visão geral dos logs de fluxo][3]

## <a name="download-flow-logs"></a><span data-ttu-id="f9e09-139">Baixar logs de fluxo</span><span class="sxs-lookup"><span data-stu-id="f9e09-139">Download flow logs</span></span>

<span data-ttu-id="f9e09-140">Os Logs de fluxo são salvos em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f9e09-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="f9e09-141">Baixe os logs de fluxo para exibi-los.</span><span class="sxs-lookup"><span data-stu-id="f9e09-141">Download your flow logs to view them.</span></span>

### <a name="step-1"></a><span data-ttu-id="f9e09-142">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="f9e09-142">Step 1</span></span>

<span data-ttu-id="f9e09-143">Para baixar os logs de fluxo, selecione **É possível baixar logs de fluxo nas contas de armazenamento configuradas**.</span><span class="sxs-lookup"><span data-stu-id="f9e09-143">To download flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="f9e09-144">Esta etapa leva você até uma exibição da conta de armazenamento em que você pode escolher quais logs baixar.</span><span class="sxs-lookup"><span data-stu-id="f9e09-144">This step takes you to a storage account view where you can choose which logs to download.</span></span>

![Configurações dos logs do fluxo][4]

### <a name="step-2"></a><span data-ttu-id="f9e09-146">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="f9e09-146">Step 2</span></span>

<span data-ttu-id="f9e09-147">Vá para a conta de armazenamento correta.</span><span class="sxs-lookup"><span data-stu-id="f9e09-147">Go to the correct storage account.</span></span> <span data-ttu-id="f9e09-148">Em seguida, selecione **Contêineres** > **insights-log-networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="f9e09-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Configurações dos logs do fluxo][5]

### <a name="step-3"></a><span data-ttu-id="f9e09-150">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="f9e09-150">Step 3</span></span>

<span data-ttu-id="f9e09-151">Vá para o local do log de fluxo, selecione-o e, em seguida, selecione **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="f9e09-151">Go to the location of the flow log, select it, and then select **Download**.</span></span>

![Configurações dos logs do fluxo][6]

<span data-ttu-id="f9e09-153">Para saber mais sobre a estrutura do log, visite a [Visão geral do log do fluxo de Grupo de Segurança de Rede](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9e09-153">For information about the structure of the log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9e09-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f9e09-154">Next steps</span></span>

<span data-ttu-id="f9e09-155">Saiba como [visualizar seus logs de fluxo NSG com o PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="f9e09-155">Learn how to [visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
