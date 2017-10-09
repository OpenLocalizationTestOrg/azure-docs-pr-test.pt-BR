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
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a>Adicionar a rede virtual existente do referência tooan em um modelo de conjunto de escala do Azure

Este artigo mostra como Olá toomodify [modelo de conjunto de escala viável mínima](./virtual-machine-scale-sets-mvss-start.md) toodeploy em uma rede virtual existente em vez de criar um novo.

## <a name="change-hello-template-definition"></a>Alterar a definição de modelo de saudação

Nosso modelo de conjunto de escala viável mínima pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e nosso modelo de implantação de escala Olá definida em uma rede virtual existente pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json). Vamos examinar Olá comparação usada toocreate este modelo (`git diff minimum-viable-scale-set existing-vnet`) parte por parte:

Primeiro, vamos adicionar um parâmetro `subnetId`. Essa cadeia de caracteres será passada para a configuração do conjunto de escala hello, permitindo que o conjunto de escala Olá subrede criada previamente tooidentify Olá máquinas virtuais de toodeploy em. Essa cadeia de caracteres deve ser do formulário Olá: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`. Por exemplo, a escala de saudação de toodeploy definida em uma rede virtual existente com o nome `myvnet`, sub-rede `mysubnet`, grupo de recursos `myrg`e a assinatura `00000000-0000-0000-0000-000000000000`, Olá subnetId seria: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.

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

Em seguida, podemos excluir recursos de rede virtual de saudação do hello `resources` de matriz, já que estamos estiver usando uma rede virtual existente e não é necessário toodeploy um novo.

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

rede virtual Olá já existe antes da implantação de modelo hello, portanto, não há nenhuma necessidade toospecify uma cláusula dependsOn da escala de saudação definir toohello da rede virtual. Assim, podemos excluir estas linhas:

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

Por fim, podemos passar Olá `subnetId` parâmetro definido pelo usuário da saudação (em vez de usar `resourceId` tooget id de saudação de uma rede virtual no hello mesma implantação, que é o modelo de conjunto de dimensão Olá mínimo viável).

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
