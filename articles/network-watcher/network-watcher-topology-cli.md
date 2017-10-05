---
title: "Exibição da topologia do Observador de rede do Azure - CLI do Azure | Microsoft Docs"
description: Este artigo descreve como usar a CLI do Azure para consultar a sua topologia de rede.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5be8e103f9a1f32117a4ed3be73bff021db1186d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a><span data-ttu-id="3de37-103">Como exibir a topologia do Observador de rede com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3de37-103">View Network Watcher topology with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3de37-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3de37-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="3de37-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3de37-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="3de37-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3de37-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="3de37-107">API REST</span><span class="sxs-lookup"><span data-stu-id="3de37-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="3de37-108">O recurso de topologia do Observador de rede fornece uma representação visual dos recursos de rede em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="3de37-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="3de37-109">No portal, essa visualização é apresentada para você automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3de37-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="3de37-110">As informações que seguem a visualização de topologia no portal podem ser recuperadas por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3de37-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="3de37-111">Esse recurso torna as informações de topologia mais versáteis, já que os dados podem ser consumidos por outras ferramentas para criar a visualização.</span><span class="sxs-lookup"><span data-stu-id="3de37-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="3de37-112">Este artigo usa a CLI 1.0 do Azure para plataforma cruzada, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="3de37-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="3de37-113">Atualmente, o Observador de Rede usa a CLI 1.0 do Azure para dar suporte à CLI.</span><span class="sxs-lookup"><span data-stu-id="3de37-113">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

<span data-ttu-id="3de37-114">A interconexão é modelada em duas relações.</span><span class="sxs-lookup"><span data-stu-id="3de37-114">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="3de37-115">**Confinamento** - exemplo: a VNet contém uma sub-rede que contém uma NIC</span><span class="sxs-lookup"><span data-stu-id="3de37-115">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="3de37-116">**Associados** - exemplo: a NIC está associada a uma VM</span><span class="sxs-lookup"><span data-stu-id="3de37-116">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="3de37-117">A lista a seguir contém propriedades que são retornadas ao consultar a REST API de topologia.</span><span class="sxs-lookup"><span data-stu-id="3de37-117">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="3de37-118">**nome** - o nome do recurso</span><span class="sxs-lookup"><span data-stu-id="3de37-118">**name** - The name of the resource</span></span>
* <span data-ttu-id="3de37-119">**ID** - o URI do recurso.</span><span class="sxs-lookup"><span data-stu-id="3de37-119">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="3de37-120">**local** - o local onde o recurso existe.</span><span class="sxs-lookup"><span data-stu-id="3de37-120">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="3de37-121">**associações** - uma lista de associações para o objeto referenciado.</span><span class="sxs-lookup"><span data-stu-id="3de37-121">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="3de37-122">**nome** - o nome do recurso referenciado.</span><span class="sxs-lookup"><span data-stu-id="3de37-122">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="3de37-123">**resourceId** -o ID do recurso é o URI do recurso referenciado na associação.</span><span class="sxs-lookup"><span data-stu-id="3de37-123">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="3de37-124">**associationType** - a relação entre o objeto filho e pai faz referência a esse valor.</span><span class="sxs-lookup"><span data-stu-id="3de37-124">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="3de37-125">Os valores válidos são **Contém** ou **Associado**.</span><span class="sxs-lookup"><span data-stu-id="3de37-125">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3de37-126">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="3de37-126">Before you begin</span></span>

<span data-ttu-id="3de37-127">Nesse cenário, você deve usar o cmdlet `network watcher topology` para recuperar as informações de topologia.</span><span class="sxs-lookup"><span data-stu-id="3de37-127">In this scenario, you use the `network watcher topology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="3de37-128">Também há um artigo sobre [Como recuperar a topologia de rede com a REST API](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="3de37-128">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="3de37-129">Este cenário pressupõe que você seguiu as etapas em [Criação de um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="3de37-129">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="3de37-130">Cenário</span><span class="sxs-lookup"><span data-stu-id="3de37-130">Scenario</span></span>

<span data-ttu-id="3de37-131">O cenário abordado neste artigo recupera a resposta de topologia para um grupo de recursos determinado.</span><span class="sxs-lookup"><span data-stu-id="3de37-131">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="3de37-132">Como recuperar a topologia</span><span class="sxs-lookup"><span data-stu-id="3de37-132">Retrieve topology</span></span>

<span data-ttu-id="3de37-133">O cmdlet `network watcher topology` recupera a topologia para um grupo de recursos determinado.</span><span class="sxs-lookup"><span data-stu-id="3de37-133">The `network watcher topology` cmdlet retrieves the topology for a given resource group.</span></span> <span data-ttu-id="3de37-134">Adicione o argumento "--json" para exibir a saída no formato json</span><span class="sxs-lookup"><span data-stu-id="3de37-134">Add the argument "--json" to view the oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="3de37-135">Resultados</span><span class="sxs-lookup"><span data-stu-id="3de37-135">Results</span></span>

<span data-ttu-id="3de37-136">Os resultados retornados têm uma propriedade de nome "Recursos", que contêm o corpo da resposta json para o cmdlet `network watcher topology`.</span><span class="sxs-lookup"><span data-stu-id="3de37-136">The results returned have a property name "Resources", which contains the json response body for the `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="3de37-137">A resposta contém os recursos no grupo de segurança de rede e suas associações (ou seja, Contém e Associado).</span><span class="sxs-lookup"><span data-stu-id="3de37-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="3de37-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3de37-138">Next steps</span></span>

<span data-ttu-id="3de37-139">Saiba mais sobre as regras de segurança que são aplicadas aos recursos de rede no artigo [Visão geral de exibição do grupo de segurança](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3de37-139">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
