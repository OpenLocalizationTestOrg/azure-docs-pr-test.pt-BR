---
title: "Fazer referência a uma rede virtual existente em um modelo do conjunto de dimensionamento do Azure | Microsoft Docs"
description: "Saiba como adicionar uma rede virtual a um modelo existente do conjunto de dimensionamento de máquinas virtuais do Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: jeconnoc
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
ms.openlocfilehash: eb35975de5864e129f97b614a61487456dd972ef
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="add-reference-to-an-existing-virtual-network-in-an-azure-scale-set-template"></a>Adicionar referência a uma rede virtual existente em um modelo do conjunto de dimensionamento do Azure

Este artigo mostra como modificar o [modelo de conjunto de dimensionamento mínimo viável](./virtual-machine-scale-sets-mvss-start.md) para implantar em uma rede virtual existente em vez de criar uma nova.

## <a name="change-the-template-definition"></a>Alterar a definição do modelo

O modelo de conjunto de dimensionamento mínimo viável pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e o modelo para implantar o conjunto de dimensionamento em uma rede virtual existente pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json). Vamos examinar a comparação usada para criar esse modelo (`git diff minimum-viable-scale-set existing-vnet`), parte por parte:

Primeiro, adicione um parâmetro `subnetId`. Essa cadeia de caracteres será passada para a configuração do conjunto de dimensionamento, permitindo que o conjunto de dimensionamento identifique a sub-rede pré-criada na qual implantará máquinas virtuais. Essa cadeia de caracteres deve estar no formato: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`. Por exemplo implantar o conjunto de dimensionamento em uma rede virtual existente com o nome `myvnet`, sub-rede `mysubnet`, grupo de recursos `myrg` e assinatura`00000000-0000-0000-0000-000000000000`, o subnetId seria: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.

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

Em seguida, exclua o recurso de rede virtual da matriz `resources`, pois você usará uma rede virtual existente e não precisará implantar uma nova.

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

A rede virtual já existe antes do modelo ser implantado e, portanto, não é necessário especificar uma cláusula dependsOn do conjunto de dimensionamento para a rede virtual. Exclua as seguintes linhas:

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

Por fim, passe o parâmetro `subnetId` definido pelo usuário (em vez de usar `resourceId` para obter a ID de uma VNET na mesma implantação, que é o que o modelo de conjunto de dimensionamento mínimo viável faz).

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




## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
