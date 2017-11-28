---
title: "aaaManage fluxo de grupo de segurança de rede registra com o observador de rede do Azure - CLI do Azure | Microsoft Docs"
description: "Esta página explica como os logs de toomanage fluxo de grupo de segurança de rede no Azure observador de rede com a CLI do Azure"
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
ms.openlocfilehash: 2d0b02e7d0a5a9ab20beb491d49a5747f976a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a><span data-ttu-id="8c48b-103">Configurar logs de fluxo de grupo de segurança de rede com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8c48b-103">Configuring Network Security Group Flow logs with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8c48b-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8c48b-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="8c48b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c48b-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="8c48b-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8c48b-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="8c48b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8c48b-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="8c48b-108">API REST</span><span class="sxs-lookup"><span data-stu-id="8c48b-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="8c48b-109">Logs de fluxo de grupo de segurança de rede são um recurso do observador de rede que permite que você tooview informações sobre o tráfego IP de entrada e saída por meio de um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="8c48b-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="8c48b-110">Esses logs de fluxo são gravados no formato json e mostram saídas fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, 5-tupla informações sobre o fluxo de saudação (protocolo IP de origem/destino, porta de origem/destino) e se hello tráfego foi permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="8c48b-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="8c48b-111">Este artigo usa nossa próxima geração CLI para o modelo de implantação de gerenciamento de recursos do hello, 2.0 do CLI do Azure, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="8c48b-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="8c48b-112">Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="8c48b-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="8c48b-113">Provedor de informações de registro</span><span class="sxs-lookup"><span data-stu-id="8c48b-113">Register Insights provider</span></span>

<span data-ttu-id="8c48b-114">Em ordem para o fluxo de log toowork com êxito, Olá **Insights** provedor deve ser registrado.</span><span class="sxs-lookup"><span data-stu-id="8c48b-114">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="8c48b-115">Se você não tiver certeza se hello **Insights** provedor está registrado, execute hello script a seguir.</span><span class="sxs-lookup"><span data-stu-id="8c48b-115">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="8c48b-116">Habilitar os logs do Fluxo de Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="8c48b-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="8c48b-117">Olá comando tooenable fluxo logs é mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="8c48b-117">hello command tooenable flow logs is shown in hello following example:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="8c48b-118">Desabilitar os logs do Fluxo de Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="8c48b-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="8c48b-119">Olá Use logs de fluxo de toodisable de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c48b-119">Use hello following example toodisable flow logs:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a><span data-ttu-id="8c48b-120">Baixar um log de fluxo</span><span class="sxs-lookup"><span data-stu-id="8c48b-120">Download a Flow log</span></span>

<span data-ttu-id="8c48b-121">local de armazenamento de saudação de um log de fluxo é definido no momento da criação.</span><span class="sxs-lookup"><span data-stu-id="8c48b-121">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="8c48b-122">Um tooaccess ferramenta conveniente dessas contas de armazenamento tooa fluxo salvar logs é o Microsoft Azure Storage Explorer, que pode ser baixado em: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="8c48b-122">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="8c48b-123">Se uma conta de armazenamento for especificada, os arquivos de captura de pacote são salvos tooa conta de armazenamento no hello local a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c48b-123">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="8c48b-124">Para obter informações sobre a estrutura de saudação do log Olá visite [log visão geral de fluxo de grupo de segurança de rede](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8c48b-124">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c48b-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8c48b-125">Next Steps</span></span>

<span data-ttu-id="8c48b-126">Saiba como muito[visualizar seus logs de fluxo NSG com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="8c48b-126">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="8c48b-127">Saiba como muito[visualizar seus logs de fluxo NSG com ferramentas de software livre](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="8c48b-127">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
