---
title: topologia do observador de rede do Azure aaaView - PowerShell | Microsoft Docs
description: Este artigo descreve como toouse PowerShell tooquery a topologia de rede.
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
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="4b0e2-103">Exibir a topologia do Observador de rede com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b0e2-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4b0e2-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b0e2-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="4b0e2-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4b0e2-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="4b0e2-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4b0e2-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="4b0e2-107">API REST</span><span class="sxs-lookup"><span data-stu-id="4b0e2-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="4b0e2-108">recurso de topologia de saudação do observador de rede fornece uma representação visual dos recursos de rede de saudação em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="4b0e2-109">No portal de hello, essa visualização é apresentada tooyou automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="4b0e2-110">informações de Olá por trás de exibição de topologia Olá no portal de saudação podem ser recuperadas por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="4b0e2-111">Esse recurso cria informações de topologia hello mais versátil como Olá dados podem ser consumidos por outros toobuild ferramentas out visualização hello.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="4b0e2-112">interconexão de saudação é modelada em duas relações.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="4b0e2-113">**Confinamento** - exemplo: a VNet contém uma sub-rede que contém uma NIC</span><span class="sxs-lookup"><span data-stu-id="4b0e2-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="4b0e2-114">**Associados** - exemplo: a NIC está associada a uma VM</span><span class="sxs-lookup"><span data-stu-id="4b0e2-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="4b0e2-115">Olá lista a seguir é propriedades que são retornadas ao consultar Olá API de REST de topologia.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="4b0e2-116">**nome** - Olá nome do recurso de saudação</span><span class="sxs-lookup"><span data-stu-id="4b0e2-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="4b0e2-117">**ID** -Olá uri do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="4b0e2-118">**local** -Olá localização onde o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="4b0e2-119">**associações** -uma lista de associações toohello Referência de objeto.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="4b0e2-120">**nome** -nome de saudação do hello referenciado recursos.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="4b0e2-121">**resourceId** -Olá resourceId é o uri de saudação do recurso Olá referenciado na associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="4b0e2-122">**associationType** -relação Olá entre o objeto do hello filho e pai Olá faz referência a esse valor.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="4b0e2-123">Os valores válidos são **Contém** ou **Associado**.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4b0e2-124">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="4b0e2-124">Before you begin</span></span>

<span data-ttu-id="4b0e2-125">Nesse cenário, você usa Olá `Get-AzureRmNetworkWatcherTopology` informações de topologia do cmdlet tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-125">In this scenario, you use hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="4b0e2-126">Também há um artigo sobre como muito[recuperar a topologia de rede com a API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="4b0e2-126">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="4b0e2-127">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-127">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="4b0e2-128">Cenário</span><span class="sxs-lookup"><span data-stu-id="4b0e2-128">Scenario</span></span>

<span data-ttu-id="4b0e2-129">cenário de saudação abordado neste artigo recupera a resposta de topologia de saudação um determinado grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-129">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="4b0e2-130">Recuperar o Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="4b0e2-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="4b0e2-131">Olá primeira etapa é a instância do tooretrieve Olá observador de rede.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-131">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="4b0e2-132">Olá `$networkWatcher` variável é passada toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-132">hello `$networkWatcher` variable is passed toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="4b0e2-133">Como recuperar a topologia</span><span class="sxs-lookup"><span data-stu-id="4b0e2-133">Retrieve topology</span></span>

<span data-ttu-id="4b0e2-134">Olá `Get-AzureRmNetworkWatcherTopology` cmdlet recupera a topologia de saudação um determinado grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-134">hello `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves hello topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="4b0e2-135">Resultados</span><span class="sxs-lookup"><span data-stu-id="4b0e2-135">Results</span></span>

<span data-ttu-id="4b0e2-136">Olá resultados retornados tem uma propriedade de nome "recursos", que contém o corpo da resposta json Olá para Olá `Get-AzureRmNetworkWatcherTopology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4b0e2-136">hello results returned have a property name "Resources", which contains hello json response body for hello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="4b0e2-137">resposta de saudação contém recursos Olá Olá grupo de segurança de rede e suas associações (ou seja, Contains, associado).</span><span class="sxs-lookup"><span data-stu-id="4b0e2-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4b0e2-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4b0e2-138">Next steps</span></span>

<span data-ttu-id="4b0e2-139">Saiba como toovisualize seu fluxo NSG registra com o Power BI visitando [visualizar NSG fluxos de logs com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="4b0e2-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


