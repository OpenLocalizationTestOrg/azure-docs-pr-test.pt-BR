---
title: "Fazer referência a uma imagem personalizada no modelo do conjunto de dimensionamento do Azure | Microsoft Docs"
description: "Saiba como tooadd um personalizado imagem tooan modelo de conjunto de escalas da máquina Virtual do Azure existente"
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
ms.date: 5/10/2017
ms.author: negat
ms.openlocfilehash: 6a17d989e44d241b460238c0106350c3ef038e56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a>Adicionar que modelo do conjunto de tooan uma imagem personalizada escala do Azure

Este artigo mostra como Olá toomodify [modelo de conjunto de escala viável mínima](./virtual-machine-scale-sets-mvss-start.md) toodeploy da imagem personalizada.

## <a name="change-hello-template-definition"></a>Alterar a definição de modelo de saudação

Nosso modelo de conjunto de escala viável mínima pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e nosso modelo de implantação de escala Olá definida a partir de uma imagem personalizada pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json). Vamos examinar Olá comparação usada toocreate este modelo (`git diff minimum-viable-scale-set custom-image`) parte por parte:

### <a name="creating-a-managed-disk-image"></a>Criando uma imagem de disco gerenciada

Se você já tiver uma imagem de disco gerenciado personalizado (um recurso do tipo `Microsoft.Compute/images`), você poderá ignorar esta seção.

Primeiro, adicionamos uma `sourceImageVhdUri` parâmetro, que é Olá URI toohello generalizado blob no armazenamento do Azure que contém a saudação toodeploy de imagem personalizada do.


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "hello source of hello generalized blob containing hello custom image"
+      }
     }
   },
   "variables": {},
```

Em seguida, adicionamos um recurso do tipo `Microsoft.Compute/images`, que é a imagem de disco gerenciado de Olá baseada em blob Olá generalizado localizado no URI `sourceImageVhdUri`. Essa imagem deve estar no hello mesma região que o conjunto de escala de saudação que utiliza. Nas propriedades de saudação da imagem hello, especificamos tipo hello SO, localização de saudação do blob de saudação (de saudação `sourceImageVhdUri` parâmetro) e o tipo de conta de armazenamento hello:

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2016-04-30-preview",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

Em Olá conjunto de escala de recurso, adicionamos uma `dependsOn` cláusula toohello imagem personalizada toomake se imagem Olá criada antes do conjunto de escala Olá tenta toodeploy da imagem de referência:

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a>Alterando a escala do conjunto de imagem de disco gerenciado propriedades toouse Olá

Em Olá `imageReference` de escala Olá definido `storageProfile`, em vez de especificar o publicador hello, oferta, sku e versão de uma imagem de plataforma, especificamos Olá `id` de saudação `Microsoft.Compute/images` recursos:

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

Neste exemplo, usamos Olá `resourceId` função tooget Olá ID de recurso de imagem Olá criado no hello mesmo modelo. Se você criar imagem de disco gerenciado Olá com antecedência, você deve fornecer id de saudação da imagem em vez disso. Essa id deve ser do formulário Olá: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.


## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
