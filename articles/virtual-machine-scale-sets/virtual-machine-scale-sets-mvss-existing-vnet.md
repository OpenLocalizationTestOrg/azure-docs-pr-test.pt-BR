---
title: "Fazer referência a uma rede virtual existente em um modelo do conjunto de dimensionamento do Azure | Microsoft Docs"
description: "Saiba como tooadd um virtual rede tooan modelo de conjunto de escala de máquina Virtual do Azure existente"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: negat
ms.openlocfilehash: c3034b577e17abc4643dc26d7c38ad643fa26322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="3f3d2-103">Adicionar a rede virtual existente do referência tooan em um modelo de conjunto de escala do Azure</span><span class="sxs-lookup"><span data-stu-id="3f3d2-103">Add reference tooan existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="3f3d2-104">Este artigo mostra como Olá toomodify [modelo de conjunto de escala viável mínima](./virtual-machine-scale-sets-mvss-start.md) toodeploy em uma rede virtual existente em vez de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="3f3d2-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="3f3d2-105">Alterar a definição de modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="3f3d2-105">Change hello template definition</span></span>

<span data-ttu-id="3f3d2-106">Nosso modelo de conjunto de escala viável mínima pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e nosso modelo de implantação de escala Olá definida em uma rede virtual existente pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="3f3d2-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="3f3d2-107">Vamos examinar Olá comparação usada toocreate este modelo (`git diff minimum-viable-scale-set existing-vnet`) parte por parte:</span><span class="sxs-lookup"><span data-stu-id="3f3d2-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="3f3d2-108">Primeiro, vamos adicionar um parâmetro `subnetId`.</span><span class="sxs-lookup"><span data-stu-id="3f3d2-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="3f3d2-109">Essa cadeia de caracteres será passada para a configuração do conjunto de escala hello, permitindo que o conjunto de escala Olá subrede criada previamente tooidentify Olá máquinas virtuais de toodeploy em.</span><span class="sxs-lookup"><span data-stu-id="3f3d2-109">This string will be passed into hello scale set configuration, allowing hello scale set tooidentify hello pre-created subnet toodeploy virtual machines into.</span></span> <span data-ttu-id="3f3d2-110">Essa cadeia de caracteres deve ser do formulário Olá: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span><span class="sxs-lookup"><span data-stu-id="3f3d2-110">This string must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="3f3d2-111">Por exemplo, a escala de saudação de toodeploy definida em uma rede virtual existente com o nome `myvnet`, sub-rede `mysubnet`, grupo de recursos `myrg`e a assinatura `00000000-0000-0000-0000-000000000000`, Olá subnetId seria: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span><span class="sxs-lookup"><span data-stu-id="3f3d2-111">For instance, toodeploy hello scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, hello subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "subnetId": {
+      "type": "string"
     }
   },
```

<span data-ttu-id="3f3d2-112">Em seguida, podemos excluir recursos de rede virtual de saudação do hello `resources` de matriz, já que estamos estiver usando uma rede virtual existente e não é necessário toodeploy um novo.</span><span class="sxs-lookup"><span data-stu-id="3f3d2-112">Next, we can delete hello virtual network resource from hello `resources` array, since we are using an existing virtual network and don't need toodeploy a new one.</span></span>

```diff
   "variables": {},
   "resources": [
-    {
-      "type": "Microsoft.Network/virtualNetworks",
-      "name": "myVnet",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "2016-12-01",
-      "properties": {
-        "addressSpace": {
-          "addressPrefixes": [
-            "10.0.0.0/16"
-          ]
-        },
-        "subnets": [
-          {
-            "name": "mySubnet",
-            "properties": {
-              "addressPrefix": "10.0.0.0/16"
-            }
-          }
-        ]
-      }
-    },
```

<span data-ttu-id="3f3d2-113">rede virtual Olá já existe antes da implantação de modelo hello, portanto, não há nenhuma necessidade toospecify uma cláusula dependsOn da escala de saudação definir toohello da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3f3d2-113">hello virtual network already exists before hello template is deployed, so there is no need toospecify a dependsOn clause from hello scale set toohello virtual network.</span></span> <span data-ttu-id="3f3d2-114">Assim, podemos excluir estas linhas:</span><span class="sxs-lookup"><span data-stu-id="3f3d2-114">Thus, we delete these lines:</span></span>

```diff
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
-      "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
-      ],
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
```

<span data-ttu-id="3f3d2-115">Por fim, podemos passar Olá `subnetId` parâmetro definido pelo usuário da saudação (em vez de usar `resourceId` tooget id de saudação de uma rede virtual no hello mesma implantação, que é o modelo de conjunto de dimensão Olá mínimo viável).</span><span class="sxs-lookup"><span data-stu-id="3f3d2-115">Finally, we pass in hello `subnetId` parameter set by hello user (instead of using `resourceId` tooget hello id of a vnet in hello same deployment, which is what hello minimum viable scale set template does).</span></span>

```diff
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
-                          "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
+                          "id": "[parameters('subnetId')]"
                         }
                       }
                     }
```




## <a name="next-steps"></a><span data-ttu-id="3f3d2-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f3d2-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
