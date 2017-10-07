---
title: topologia do observador de rede do Azure aaaView - CLI do Azure | Microsoft Docs
description: Este artigo descreve como toouse CLI do Azure tooquery a topologia de rede.
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
ms.openlocfilehash: afa7e7dd844ecb2ab4c616ba99fa0a433f1e4ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a><span data-ttu-id="d4422-103">Como exibir a topologia do Observador de rede com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d4422-103">View Network Watcher topology with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d4422-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4422-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="d4422-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d4422-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="d4422-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d4422-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="d4422-107">API REST</span><span class="sxs-lookup"><span data-stu-id="d4422-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="d4422-108">recurso de topologia de saudação do observador de rede fornece uma representação visual dos recursos de rede de saudação em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="d4422-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="d4422-109">No portal de hello, essa visualização é apresentada tooyou automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d4422-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="d4422-110">informações de Olá por trás de exibição de topologia Olá no portal de saudação podem ser recuperadas por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4422-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="d4422-111">Esse recurso cria informações de topologia hello mais versátil como Olá dados podem ser consumidos por outros toobuild ferramentas out visualização hello.</span><span class="sxs-lookup"><span data-stu-id="d4422-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="d4422-112">Este artigo usa a CLI 1.0 do Azure para plataforma cruzada, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="d4422-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="d4422-113">Atualmente, o Observador de Rede usa a CLI 1.0 do Azure para dar suporte à CLI.</span><span class="sxs-lookup"><span data-stu-id="d4422-113">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

<span data-ttu-id="d4422-114">interconexão de saudação é modelada em duas relações.</span><span class="sxs-lookup"><span data-stu-id="d4422-114">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="d4422-115">**Confinamento** - exemplo: a VNet contém uma sub-rede que contém uma NIC</span><span class="sxs-lookup"><span data-stu-id="d4422-115">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="d4422-116">**Associados** - exemplo: a NIC está associada a uma VM</span><span class="sxs-lookup"><span data-stu-id="d4422-116">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="d4422-117">Olá lista a seguir é propriedades que são retornadas ao consultar Olá API de REST de topologia.</span><span class="sxs-lookup"><span data-stu-id="d4422-117">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="d4422-118">**nome** - Olá nome do recurso de saudação</span><span class="sxs-lookup"><span data-stu-id="d4422-118">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="d4422-119">**ID** -Olá uri do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4422-119">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="d4422-120">**local** -Olá localização onde o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4422-120">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="d4422-121">**associações** -uma lista de associações toohello Referência de objeto.</span><span class="sxs-lookup"><span data-stu-id="d4422-121">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="d4422-122">**nome** -nome de saudação do hello referenciado recursos.</span><span class="sxs-lookup"><span data-stu-id="d4422-122">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="d4422-123">**resourceId** -Olá resourceId é o uri de saudação do recurso Olá referenciado na associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4422-123">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="d4422-124">**associationType** -relação Olá entre o objeto do hello filho e pai Olá faz referência a esse valor.</span><span class="sxs-lookup"><span data-stu-id="d4422-124">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="d4422-125">Os valores válidos são **Contém** ou **Associado**.</span><span class="sxs-lookup"><span data-stu-id="d4422-125">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d4422-126">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d4422-126">Before you begin</span></span>

<span data-ttu-id="d4422-127">Nesse cenário, você usa Olá `network watcher topology` informações de topologia do cmdlet tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="d4422-127">In this scenario, you use hello `network watcher topology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="d4422-128">Também há um artigo sobre como muito[recuperar a topologia de rede com a API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="d4422-128">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="d4422-129">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="d4422-129">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="d4422-130">Cenário</span><span class="sxs-lookup"><span data-stu-id="d4422-130">Scenario</span></span>

<span data-ttu-id="d4422-131">cenário de saudação abordado neste artigo recupera a resposta de topologia de saudação um determinado grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d4422-131">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="d4422-132">Como recuperar a topologia</span><span class="sxs-lookup"><span data-stu-id="d4422-132">Retrieve topology</span></span>

<span data-ttu-id="d4422-133">Olá `network watcher topology` cmdlet recupera a topologia de saudação um determinado grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d4422-133">hello `network watcher topology` cmdlet retrieves hello topology for a given resource group.</span></span> <span data-ttu-id="d4422-134">Adicione o argumento hello "– json" tooview Olá oput no formato json</span><span class="sxs-lookup"><span data-stu-id="d4422-134">Add hello argument "--json" tooview hello oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="d4422-135">Resultados</span><span class="sxs-lookup"><span data-stu-id="d4422-135">Results</span></span>

<span data-ttu-id="d4422-136">Olá resultados retornados tem uma propriedade de nome "recursos", que contém o corpo da resposta json Olá para Olá `network watcher topology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d4422-136">hello results returned have a property name "Resources", which contains hello json response body for hello `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="d4422-137">resposta de saudação contém recursos Olá Olá grupo de segurança de rede e suas associações (ou seja, Contains, associado).</span><span class="sxs-lookup"><span data-stu-id="d4422-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d4422-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4422-138">Next steps</span></span>

<span data-ttu-id="d4422-139">Saiba mais sobre as regras de segurança de saudação que são recursos de rede aplicada tooyour visitando [visão geral de exibição de grupo de segurança](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d4422-139">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
