---
title: "logs de aaaManage fluxo de grupo de segurança de rede com o observador de rede do Azure - API REST | Microsoft Docs"
description: "Esta página explica como os logs de toomanage fluxo de grupo de segurança de rede no Azure observador de rede com a API REST"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2ab25379-0fd3-4bfe-9d82-425dfc7ad6bb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: be81e35f4d01c67efef99773e9b4e2ae4b8e209e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="23d46-103">Configurar logs de fluxo do Grupo de segurança de rede usando a API REST</span><span class="sxs-lookup"><span data-stu-id="23d46-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="23d46-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="23d46-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="23d46-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="23d46-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="23d46-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="23d46-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="23d46-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="23d46-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="23d46-108">API REST</span><span class="sxs-lookup"><span data-stu-id="23d46-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="23d46-109">Logs de fluxo de grupo de segurança de rede são um recurso do observador de rede que permite que você tooview informações sobre o tráfego IP de entrada e saída por meio de um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="23d46-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="23d46-110">Esses logs de fluxo são gravados no formato json e mostram saídas fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, 5-tupla informações sobre o fluxo de saudação (protocolo IP de origem/destino, porta de origem/destino) e se hello tráfego foi permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="23d46-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="23d46-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="23d46-111">Before you begin</span></span>

<span data-ttu-id="23d46-112">ARMclient é toocall usado Olá REST API usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23d46-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="23d46-113">O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="23d46-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="23d46-114">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="23d46-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="23d46-115">Para a API de REST do Inspetor de rede chamadas Olá nome do grupo de recursos na solicitação Olá que URI é o grupo de recursos de saudação que contém Olá observador de rede, não os recursos de saudação estiver executando ações de diagnóstico Olá em.</span><span class="sxs-lookup"><span data-stu-id="23d46-115">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="23d46-116">Cenário</span><span class="sxs-lookup"><span data-stu-id="23d46-116">Scenario</span></span>

<span data-ttu-id="23d46-117">cenário de saudação abordado neste artigo mostra como tooenable, desabilitar e consulta de fluem de logs usando Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="23d46-117">hello scenario covered in this article shows you how tooenable, disable, and query flow logs using hello REST API.</span></span> <span data-ttu-id="23d46-118">toolearn mais informações sobre logs de fluxo de grupo de segurança de rede, visite [registro de fluxo de grupo de segurança de rede - visão geral de](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="23d46-118">toolearn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="23d46-119">Neste cenário, você:</span><span class="sxs-lookup"><span data-stu-id="23d46-119">In this scenario, you will:</span></span>

* <span data-ttu-id="23d46-120">Habilitar logs de fluxo</span><span class="sxs-lookup"><span data-stu-id="23d46-120">Enable flow logs</span></span>
* <span data-ttu-id="23d46-121">Desabilitar logs de fluxo</span><span class="sxs-lookup"><span data-stu-id="23d46-121">Disable flow logs</span></span>
* <span data-ttu-id="23d46-122">Consultar status dos logs de fluxo</span><span class="sxs-lookup"><span data-stu-id="23d46-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="23d46-123">Fazer logon com o ARMClient</span><span class="sxs-lookup"><span data-stu-id="23d46-123">Log in with ARMClient</span></span>

<span data-ttu-id="23d46-124">Faça logon no tooarmclient com suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="23d46-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="23d46-125">Provedor de informações de registro</span><span class="sxs-lookup"><span data-stu-id="23d46-125">Register Insights provider</span></span>

<span data-ttu-id="23d46-126">Em ordem para o fluxo de log toowork com êxito, Olá **Insights** provedor deve ser registrado.</span><span class="sxs-lookup"><span data-stu-id="23d46-126">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="23d46-127">Se você não tiver certeza se hello **Insights** provedor está registrado, execute hello script a seguir.</span><span class="sxs-lookup"><span data-stu-id="23d46-127">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="23d46-128">Habilitar os logs do fluxo de Grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="23d46-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="23d46-129">Olá comando tooenable fluxo logs é mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="23d46-129">hello command tooenable flow logs is shown in hello following example:</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'true',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="23d46-130">resposta de Olá retornada de saudação anterior de exemplo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="23d46-130">hello response returned from hello preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="23d46-131">Desabilitar os logs de fluxo do Grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="23d46-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="23d46-132">Olá Use logs de fluxo de toodisable de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="23d46-132">Use hello following example toodisable flow logs.</span></span> <span data-ttu-id="23d46-133">Olá chamada é Olá mesmo como ativar logs de fluxo, exceto **false** está definido para a propriedade Olá habilitado.</span><span class="sxs-lookup"><span data-stu-id="23d46-133">hello call is hello same as enabling flow logs, except **false** is set for hello enabled property.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'false',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="23d46-134">resposta de Olá retornada de saudação anterior de exemplo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="23d46-134">hello response returned from hello preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": false,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="query-flow-logs"></a><span data-ttu-id="23d46-135">Consultar logs de fluxo</span><span class="sxs-lookup"><span data-stu-id="23d46-135">Query flow logs</span></span>

<span data-ttu-id="23d46-136">Olá após chamada REST consultas Olá status do fluxo de logs em um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="23d46-136">hello following REST call queries hello status of flow logs on a Network Security Group.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/queryFlowLogStatus?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="23d46-137">a seguir Olá é um exemplo de resposta Olá retornado:</span><span class="sxs-lookup"><span data-stu-id="23d46-137">hello following is an example of hello response returned:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
   "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="download-a-flow-log"></a><span data-ttu-id="23d46-138">Baixar um log de fluxo</span><span class="sxs-lookup"><span data-stu-id="23d46-138">Download a flow log</span></span>

<span data-ttu-id="23d46-139">local de armazenamento de saudação de um log de fluxo é definido no momento da criação.</span><span class="sxs-lookup"><span data-stu-id="23d46-139">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="23d46-140">Um tooaccess ferramenta conveniente dessas contas de armazenamento tooa fluxo salvar logs é o Microsoft Azure Storage Explorer, que pode ser baixado em: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="23d46-140">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="23d46-141">Se uma conta de armazenamento for especificada, os arquivos de captura de pacote são salvos tooa conta de armazenamento no hello local a seguir:</span><span class="sxs-lookup"><span data-stu-id="23d46-141">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="23d46-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="23d46-142">Next steps</span></span>

<span data-ttu-id="23d46-143">Saiba como muito[visualizar seus logs de fluxo NSG com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="23d46-143">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="23d46-144">Saiba como muito[visualizar seus logs de fluxo NSG com ferramentas de software livre](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="23d46-144">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
