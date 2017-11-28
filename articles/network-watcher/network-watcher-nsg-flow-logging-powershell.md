---
title: "aaaManage fluxo de grupo de segurança de rede registra com o observador de rede do Azure - PowerShell | Microsoft Docs"
description: "Esta página explica como os logs de toomanage fluxo de grupo de segurança de rede no Azure observador de rede com o PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 987e8728fb6459fd6ff8eb5cd3d36ff855f2ccfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-powershell"></a><span data-ttu-id="bf54d-103">Configurar logs de fluxo de Grupo de Segurança de Rede com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf54d-103">Configuring Network Security Group Flow logs with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="bf54d-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bf54d-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="bf54d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf54d-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="bf54d-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bf54d-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="bf54d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bf54d-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="bf54d-108">API REST</span><span class="sxs-lookup"><span data-stu-id="bf54d-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="bf54d-109">Logs de fluxo de grupo de segurança de rede são um recurso do observador de rede que permite que você tooview informações sobre o tráfego IP de entrada e saída por meio de um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="bf54d-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="bf54d-110">Esses logs de fluxo são gravados no formato json e mostram saídas fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, 5-tupla informações sobre o fluxo de saudação (protocolo IP de origem/destino, porta de origem/destino) e se hello tráfego foi permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="bf54d-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="bf54d-111">Provedor de informações de registro</span><span class="sxs-lookup"><span data-stu-id="bf54d-111">Register Insights provider</span></span>

<span data-ttu-id="bf54d-112">Em ordem para o fluxo de log toowork com êxito, Olá **Insights** provedor deve ser registrado.</span><span class="sxs-lookup"><span data-stu-id="bf54d-112">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="bf54d-113">Se você não tiver certeza se hello **Insights** provedor está registrado, execute hello script a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf54d-113">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="bf54d-114">Habilitar os logs do Fluxo de Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="bf54d-114">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="bf54d-115">Olá comando tooenable fluxo logs é mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="bf54d-115">hello command tooenable flow logs is shown in hello following example:</span></span>

```powershell
$NW = Get-AzurermNetworkWatcher -ResourceGroupName NetworkWatcherRg -Name NetworkWatcher_westcentralus
$nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName nsgRG-Name nsgName
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName StorageRG -Name contosostorage123
Get-AzureRmNetworkWatcherFlowLogStatus -NetworkWatcher $NW -TargetResourceId $nsg.Id
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="bf54d-116">Desabilitar os logs do Fluxo de Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="bf54d-116">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="bf54d-117">Olá Use logs de fluxo de toodisable de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf54d-117">Use hello following example toodisable flow logs:</span></span>

```powershell
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="bf54d-118">Baixar um log de fluxo</span><span class="sxs-lookup"><span data-stu-id="bf54d-118">Download a Flow log</span></span>

<span data-ttu-id="bf54d-119">local de armazenamento de saudação de um log de fluxo é definido no momento da criação.</span><span class="sxs-lookup"><span data-stu-id="bf54d-119">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="bf54d-120">Um tooaccess ferramenta conveniente dessas contas de armazenamento tooa fluxo salvar logs é o Microsoft Azure Storage Explorer, que pode ser baixado em: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="bf54d-120">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="bf54d-121">Se uma conta de armazenamento for especificada, os arquivos de captura de pacote são salvos tooa conta de armazenamento no hello local a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf54d-121">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="bf54d-122">Para obter informações sobre a estrutura de saudação do log Olá visite [log visão geral de fluxo de grupo de segurança de rede](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bf54d-122">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf54d-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf54d-123">Next Steps</span></span>

<span data-ttu-id="bf54d-124">Saiba como muito[visualizar seus logs de fluxo NSG com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="bf54d-124">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="bf54d-125">Saiba como muito[visualizar seus logs de fluxo NSG com ferramentas de software livre](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="bf54d-125">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
