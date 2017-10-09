---
title: aaaConvert uma escala do Azure Resource Manager definir modelo toouse gerenciado disco | Microsoft Docs
description: Converta um modelo de conjunto de escala conjunto modelo tooa disco gerenciado escala.
keywords: "conjuntos de escala de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: bc8c377a-8c3f-45b8-8b2d-acc2d6d0b1e8
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/18/2017
ms.author: negat
ms.openlocfilehash: 66c2217647e57ed2cfa39660c0175710ae2e63be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a>Converter um modelo de conjunto de escala conjunto modelo tooa disco gerenciado escala

Os clientes com um modelo do Gerenciador de recursos para a criação de uma escala definida usando o disco gerenciado não poderá toomodify-toouse gerenciados em disco. Este artigo mostra como toodo esse, usando como um exemplo de uma solicitação de recepção de saudação [modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates), um repositório dirigida pela comunidade para modelos do Gerenciador de recursos de exemplo. solicitação de recepção completo Olá pode ser vista aqui: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), e as partes relevantes de diferença Olá Olá estão abaixo, junto com explicações:

## <a name="making-hello-os-disks-managed"></a>Tornando os discos do sistema operacional Olá gerenciados

Comparação de saudação abaixo, vemos que removemos várias variáveis relacionadas toostorage disco propriedades de conta e. Tipo de conta de armazenamento não é mais necessário (Standard_LRS é o padrão de saudação), mas ainda pode especificá-lo se o que queremos. Apenas Standard_LRS e Premium_LRS são compatíveis com um disco gerenciado. Novo sufixo de conta de armazenamento, a matriz de cadeia de caracteres exclusiva e a contagem de sa foram usados em Olá antigo modelo toogenerate armazenamento nomes de conta. Essas variáveis não são mais necessárias no novo modelo de saudação porque o disco gerenciado cria automaticamente as contas de armazenamento em nome saudação do cliente. Da mesma forma, nome do contêiner de vhd e o nome de disco do sistema operacional não são mais necessárias porque o disco gerenciado automaticamente nomes de discos e contêineres de blob de armazenamento subjacente hello.

```diff
   "variables": {
-    "storageAccountType": "Standard_LRS",
     "namingInfix": "[toLower(substring(concat(parameters('vmssName'), uniqueString(resourceGroup().id)), 0, 9))]",
     "longNamingInfix": "[toLower(parameters('vmssName'))]",
-    "newStorageAccountSuffix": "[concat(variables('namingInfix'), 'sa')]",
-    "uniqueStringArray": [
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '0')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '1')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '2')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '3')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '4')))]"
-    ],
-    "saCount": "[length(variables('uniqueStringArray'))]",
-    "vhdContainerName": "[concat(variables('namingInfix'), 'vhd')]",
-    "osDiskName": "[concat(variables('namingInfix'), 'osdisk')]",
     "addressPrefix": "10.0.0.0/16",
     "subnetPrefix": "10.0.0.0/24",
     "virtualNetworkName": "[concat(variables('namingInfix'), 'vnet')]",
```


Na comparação Olá abaixo, podemos pode consulte que atualizamos Olá computação versão too2016-04-30-visualização da api, que é hello mais antiga versão necessária para suporte de disco gerenciado com conjuntos de escala. Observe que estamos ainda pode usar discos não gerenciados na nova versão da api Olá com sintaxe antiga Olá se desejado. Em outras palavras, se podemos atualizar somente hello versão da api de computação e não altere mais nada, modelo Olá deve continuar toowork como antes.

```diff
@@ -86,7 +74,7 @@
       "version": "latest"
     },
     "imageReference": "[variables('osType')]",
-    "computeApiVersion": "2016-03-30",
+    "computeApiVersion": "2016-04-30-preview",
     "networkApiVersion": "2016-03-30",
     "storageApiVersion": "2015-06-15"
   },
```

Comparação de saudação abaixo, podemos ver que estamos removendo recursos de conta de armazenamento de saudação da matriz de recursos de saudação completamente. Não precisamos mais dele, uma vez que o disco gerenciado os cria automaticamente em nosso nome.

```diff
@@ -113,19 +101,6 @@
       }
     },
-    {
-      "type": "Microsoft.Storage/storageAccounts",
-      "name": "[concat(variables('uniqueStringArray')[copyIndex()], variables('newStorageAccountSuffix'))]",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "[variables('storageApiVersion')]",
-      "copy": {
-        "name": "storageLoop",
-        "count": "[variables('saCount')]"
-      },
-      "properties": {
-        "accountType": "[variables('storageAccountType')]"
-      }
-    },
     {
       "type": "Microsoft.Network/publicIPAddresses",
       "name": "[variables('publicIPAddressName')]",
       "location": "[resourceGroup().location]",
```

Em comparação Olá abaixo, podemos pode consulte que estamos removendo Olá depende cláusula referindo-se de loop toohello de conjunto de escala de saudação que estava criando contas de armazenamento. No modelo antigo e hello, isso foi garantir que as contas de armazenamento Olá foram criadas antes do conjunto de escala Olá começou a criação, mas essa cláusula não é mais necessária com disco gerenciado. Também remove a propriedade de contêineres de vhd Olá e Olá propriedade de nome de disco do sistema operacional, essas propriedades são tratados automaticamente subjacente Olá por disco gerenciado. Se nós desejavam, poderíamos adicionar `"managedDisk": { "storageAccountType": "Premium_LRS" }` na configuração de "osDisk" hello se quiséssemos discos do sistema operacional de premium. Apenas VMs com uma letra maiuscula ou do minúscula ' hello VM sku pode usar discos premium.

```diff
@@ -183,7 +158,6 @@
       "location": "[resourceGroup().location]",
       "apiVersion": "[variables('computeApiVersion')]",
       "dependsOn": [
-        "storageLoop",
         "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
         "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
       ],
@@ -200,16 +174,8 @@
         "virtualMachineProfile": {
           "storageProfile": {
             "osDisk": {
-              "vhdContainers": [
-                "[concat('https://', variables('uniqueStringArray')[0], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[1], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[2], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[3], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[4], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]"
-              ],
-              "name": "[variables('osDiskName')]",
             },
             "imageReference": "[variables('imageReference')]"
           },

```

Não há nenhuma propriedade explícita na configuração de conjunto de escala Olá para se toouse gerenciado ou não gerenciado de disco. conjunto de escala Olá sabe quais toouse com base nas propriedades de saudação que estão presentes no perfil de armazenamento hello. Portanto, é importante ao modificar Olá tooensure de modelo que são propriedades do direito de saudação no perfil de armazenamento de saudação do conjunto de escala de saudação.


## <a name="data-disks"></a>Discos de dados

Com alterações Olá acima, Olá escala conjunto usa gerenciado discos para Olá SO de disco, mas e quanto os discos de dados? tooadd os discos de dados, adicionar propriedade do hello "dataDisks" em "storageProfile" no mesmo nível como "osDisk" de saudação. valor da propriedade Olá Olá é uma lista JSON de objetos, cada um deles tem propriedades "lun" (que deve ser exclusivo por disco de dados em uma máquina virtual), "createOption" ("vazio" está atualmente Olá só há suporte para opção) e "diskSizeGB" (Olá tamanho do disco de saudação em gigabytes; deve ser maior que 0 e menor que 1024) conforme mostrado no exemplo a seguir de saudação: 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

Se você especificar `n` discos nesta matriz, cada VM em escala Olá definir obtém `n` discos de dados. No entanto, observe que estes discos de dados são dispositivos brutos. Eles não estão formatados. É toohello cliente tooattach, Partition e discos de saudação do formato antes de usá-los. Opcionalmente, seria possível também especificar `"managedDisk": { "storageAccountType": "Premium_LRS" }` em cada toospecify de objeto de disco de dados que ela deve ser um disco de dados premium. Apenas VMs com uma letra maiuscula ou do minúscula ' hello VM sku pode usar discos premium.

toolearn mais sobre como usar discos de dados com conjuntos de escala, consulte [neste artigo](./virtual-machine-scale-sets-attached-disks.md).


## <a name="next-steps"></a>Próximas etapas
Por exemplo modelos do Gerenciador de recursos usando conjuntos de escala, procure "vmss" no hello [repositório github de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates).

Para obter informações gerais, confira Olá [página principal para conjuntos de escala](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

