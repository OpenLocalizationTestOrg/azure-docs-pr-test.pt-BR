---
title: topologia do observador de rede do Azure aaaView - API REST | Microsoft Docs
description: Este artigo descreve como toouse REST API tooquery a topologia de rede.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="59a1e-103">Exibir a topologia do Observador de rede com a API REST</span><span class="sxs-lookup"><span data-stu-id="59a1e-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="59a1e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="59a1e-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="59a1e-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="59a1e-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="59a1e-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="59a1e-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="59a1e-107">API REST</span><span class="sxs-lookup"><span data-stu-id="59a1e-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="59a1e-108">recurso de topologia de saudação do observador de rede fornece uma representação visual dos recursos de rede de saudação em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="59a1e-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="59a1e-109">No portal de hello, essa visualização é apresentada tooyou automaticamente.</span><span class="sxs-lookup"><span data-stu-id="59a1e-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="59a1e-110">informações de Olá por trás de exibição de topologia Olá no portal de saudação podem ser recuperadas por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59a1e-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="59a1e-111">Esse recurso cria informações de topologia hello mais versátil como Olá dados podem ser consumidos por outros toobuild ferramentas out visualização hello.</span><span class="sxs-lookup"><span data-stu-id="59a1e-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="59a1e-112">interconexão de saudação é modelada em duas relações.</span><span class="sxs-lookup"><span data-stu-id="59a1e-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="59a1e-113">**Confinamento** - exemplo: a VNet contém uma sub-rede que contém uma NIC</span><span class="sxs-lookup"><span data-stu-id="59a1e-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="59a1e-114">**Associados** - exemplo: a NIC está associada a uma VM</span><span class="sxs-lookup"><span data-stu-id="59a1e-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="59a1e-115">Olá lista a seguir é propriedades que são retornadas ao consultar Olá API de REST de topologia.</span><span class="sxs-lookup"><span data-stu-id="59a1e-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="59a1e-116">**nome** - Olá nome do recurso de saudação</span><span class="sxs-lookup"><span data-stu-id="59a1e-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="59a1e-117">**ID** -Olá uri do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="59a1e-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="59a1e-118">**local** -Olá localização onde o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="59a1e-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="59a1e-119">**associações** -uma lista de associações toohello Referência de objeto.</span><span class="sxs-lookup"><span data-stu-id="59a1e-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="59a1e-120">**nome** -nome de saudação do hello referenciado recursos.</span><span class="sxs-lookup"><span data-stu-id="59a1e-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="59a1e-121">**resourceId** -Olá resourceId é o uri de saudação do recurso Olá referenciado na associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="59a1e-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="59a1e-122">**associationType** -relação Olá entre o objeto do hello filho e pai Olá faz referência a esse valor.</span><span class="sxs-lookup"><span data-stu-id="59a1e-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="59a1e-123">Os valores válidos são **Contém** ou **Associado**.</span><span class="sxs-lookup"><span data-stu-id="59a1e-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="59a1e-124">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="59a1e-124">Before you begin</span></span>

<span data-ttu-id="59a1e-125">Neste cenário, para recuperar informações de topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="59a1e-125">In this scenario, you retrieve hello topology information.</span></span> <span data-ttu-id="59a1e-126">ARMclient é toocall usado Olá REST API usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59a1e-126">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="59a1e-127">O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="59a1e-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="59a1e-128">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="59a1e-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="59a1e-129">Cenário</span><span class="sxs-lookup"><span data-stu-id="59a1e-129">Scenario</span></span>

<span data-ttu-id="59a1e-130">cenário de saudação abordado neste artigo recupera a resposta de topologia de saudação um determinado grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="59a1e-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="59a1e-131">Fazer logon com o ARMClient</span><span class="sxs-lookup"><span data-stu-id="59a1e-131">Log in with ARMClient</span></span>

<span data-ttu-id="59a1e-132">Faça logon no tooarmclient com suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="59a1e-132">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="59a1e-133">Como recuperar a topologia</span><span class="sxs-lookup"><span data-stu-id="59a1e-133">Retrieve topology</span></span>

<span data-ttu-id="59a1e-134">saudação de exemplo a seguir solicita topologia Olá Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="59a1e-134">hello following example requests hello topology from hello REST API.</span></span>  <span data-ttu-id="59a1e-135">exemplo Hello é parametrizada tooallow flexibilidade na criação de um exemplo.</span><span class="sxs-lookup"><span data-stu-id="59a1e-135">hello example is parameterized tooallow for flexibility in creating an example.</span></span>  <span data-ttu-id="59a1e-136">Substitua todos os valores por \< \> ao redor deles.</span><span class="sxs-lookup"><span data-stu-id="59a1e-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="59a1e-137">saudação de resposta a seguir está um exemplo de uma resposta reduzido que é retornado quando recuperar a topologia para um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="59a1e-137">hello following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="59a1e-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="59a1e-138">Next steps</span></span>

<span data-ttu-id="59a1e-139">Saiba como toovisualize seu fluxo NSG registra com o Power BI visitando [visualizar NSG fluxos de logs com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="59a1e-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

