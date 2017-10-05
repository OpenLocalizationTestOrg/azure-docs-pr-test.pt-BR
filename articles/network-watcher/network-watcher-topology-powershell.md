---
title: Exibir a topologia do Observador de rede do Azure - PowerShell | Microsoft Docs
description: "Este artigo descreverá como usar o PowerShell para consultar sua topologia de rede."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 40e01a7a6a2ea6127ab725f04649cec47b9d9422
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="69614-103">Exibir a topologia do Observador de rede com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="69614-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="69614-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69614-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="69614-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="69614-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="69614-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="69614-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="69614-107">API REST</span><span class="sxs-lookup"><span data-stu-id="69614-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="69614-108">O recurso de topologia do Observador de rede fornece uma representação visual dos recursos de rede em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="69614-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="69614-109">No portal, essa visualização é apresentada para você automaticamente.</span><span class="sxs-lookup"><span data-stu-id="69614-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="69614-110">As informações que seguem a visualização de topologia no portal podem ser recuperadas por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69614-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="69614-111">Esse recurso torna as informações de topologia mais versáteis, já que os dados podem ser consumidos por outras ferramentas para criar a visualização.</span><span class="sxs-lookup"><span data-stu-id="69614-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="69614-112">A interconexão é modelada em duas relações.</span><span class="sxs-lookup"><span data-stu-id="69614-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="69614-113">**Confinamento** - exemplo: a VNet contém uma sub-rede que contém uma NIC</span><span class="sxs-lookup"><span data-stu-id="69614-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="69614-114">**Associados** - exemplo: a NIC está associada a uma VM</span><span class="sxs-lookup"><span data-stu-id="69614-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="69614-115">A lista a seguir contém propriedades que são retornadas ao consultar a REST API de topologia.</span><span class="sxs-lookup"><span data-stu-id="69614-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="69614-116">**nome** - o nome do recurso</span><span class="sxs-lookup"><span data-stu-id="69614-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="69614-117">**ID** - o URI do recurso.</span><span class="sxs-lookup"><span data-stu-id="69614-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="69614-118">**local** - o local onde o recurso existe.</span><span class="sxs-lookup"><span data-stu-id="69614-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="69614-119">**associações** - uma lista de associações para o objeto referenciado.</span><span class="sxs-lookup"><span data-stu-id="69614-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="69614-120">**nome** - o nome do recurso referenciado.</span><span class="sxs-lookup"><span data-stu-id="69614-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="69614-121">**resourceId** -o ID do recurso é o URI do recurso referenciado na associação.</span><span class="sxs-lookup"><span data-stu-id="69614-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="69614-122">**associationType** - a relação entre o objeto filho e pai faz referência a esse valor.</span><span class="sxs-lookup"><span data-stu-id="69614-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="69614-123">Os valores válidos são **Contém** ou **Associado**.</span><span class="sxs-lookup"><span data-stu-id="69614-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="69614-124">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="69614-124">Before you begin</span></span>

<span data-ttu-id="69614-125">Nesse cenário, você deve usar o cmdlet `Get-AzureRmNetworkWatcherTopology` para recuperar as informações de topologia.</span><span class="sxs-lookup"><span data-stu-id="69614-125">In this scenario, you use the `Get-AzureRmNetworkWatcherTopology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="69614-126">Também há um artigo sobre [Como recuperar a topologia de rede com a REST API](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="69614-126">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="69614-127">Este cenário pressupõe que você seguiu as etapas em [Criação de um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="69614-127">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="69614-128">Cenário</span><span class="sxs-lookup"><span data-stu-id="69614-128">Scenario</span></span>

<span data-ttu-id="69614-129">O cenário abordado neste artigo recupera a resposta de topologia para um grupo de recursos determinado.</span><span class="sxs-lookup"><span data-stu-id="69614-129">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="69614-130">Recuperar o Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="69614-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="69614-131">A primeira etapa é recuperar a instância do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="69614-131">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="69614-132">A variável `$networkWatcher` é passada para o cmdlet `Get-AzureRmNetworkWatcherTopology`.</span><span class="sxs-lookup"><span data-stu-id="69614-132">The `$networkWatcher` variable is passed to the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="69614-133">Recuperar a topologia</span><span class="sxs-lookup"><span data-stu-id="69614-133">Retrieve topology</span></span>

<span data-ttu-id="69614-134">O cmdlet `Get-AzureRmNetworkWatcherTopology` recupera a topologia para um grupo de recursos determinado.</span><span class="sxs-lookup"><span data-stu-id="69614-134">The `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves the topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="69614-135">Resultados</span><span class="sxs-lookup"><span data-stu-id="69614-135">Results</span></span>

<span data-ttu-id="69614-136">Os resultados retornados têm uma propriedade de nome "Recursos", que contêm o corpo da resposta json para o cmdlet `Get-AzureRmNetworkWatcherTopology`.</span><span class="sxs-lookup"><span data-stu-id="69614-136">The results returned have a property name "Resources", which contains the json response body for the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="69614-137">A resposta contém os recursos no grupo de segurança de rede e suas associações (ou seja, Contém e Associado).</span><span class="sxs-lookup"><span data-stu-id="69614-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a><span data-ttu-id="69614-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="69614-138">Next steps</span></span>

<span data-ttu-id="69614-139">Para saber como visualizar os logs de fluxo NSG com o Power BI, veja [Como visualizar logs de fluxos NSG com Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="69614-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


