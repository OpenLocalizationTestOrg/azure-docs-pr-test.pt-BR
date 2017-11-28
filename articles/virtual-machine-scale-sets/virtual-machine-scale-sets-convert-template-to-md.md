---
title: "Conversão de um modelo de conjunto de dimensionamento do Azure Resource Manager para usar disco gerenciado | Microsoft Docs"
description: "Conversão de um modelo de conjunto de dimensionamento para um modelo de conjunto de dimensionamento de disco gerenciado."
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
ms.openlocfilehash: 2f5cb85703888c5056611d466f508547ee72e44b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="convert-a-scale-set-template-to-a-managed-disk-scale-set-template"></a><span data-ttu-id="9d0c0-104">Conversão de um modelo de conjunto de dimensionamento para um modelo de conjunto de dimensionamento de disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="9d0c0-104">Convert a scale set template to a managed disk scale set template</span></span>

<span data-ttu-id="9d0c0-105">Clientes com um modelo do Resource Manager para criar um conjunto de dimensionamento não usando disco gerenciado podem modificá-lo para usar um disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish to modify it to use managed disk.</span></span> <span data-ttu-id="9d0c0-106">Este artigo mostra como fazer isso usando como exemplo uma solicitação pull dos [modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates), um repositório de amostras de modelos do Resource Manager orientado pela comunidade.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-106">This article shows how to do this, using as an example a pull request from the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="9d0c0-107">A solicitação pull completa pode ser vista em: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), e as partes relevantes da comparação estão abaixo, junto com explicações:</span><span class="sxs-lookup"><span data-stu-id="9d0c0-107">The full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and the relevant parts of the diff are below, along with explanations:</span></span>

## <a name="making-the-os-disks-managed"></a><span data-ttu-id="9d0c0-108">Como fazer os discos gerenciados do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="9d0c0-108">Making the OS disks managed</span></span>

<span data-ttu-id="9d0c0-109">Na comparação a seguir, podemos ver que removemos diversas variáveis relacionadas às propriedades de disco de armazenamento e conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-109">In the diff below, we can see that we have removed several variables related to storage account and disk properties.</span></span> <span data-ttu-id="9d0c0-110">O tipo de conta de armazenamento não é mais necessário (Standard_LRS é o padrão), mas, se desejar, você ainda pode especificá-lo.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-110">Storage account type is no longer necessary (Standard_LRS is the default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="9d0c0-111">Apenas Standard_LRS e Premium_LRS são compatíveis com um disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="9d0c0-112">Novos sufixos de conta de armazenamento, matrizes de cadeias de caracteres exclusivas e contagem de sa foram usados no modelo antigo para gerar nomes de contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-112">New storage account suffix, unique string array, and sa count were used in the old template to generate storage account names.</span></span> <span data-ttu-id="9d0c0-113">Essas variáveis não são mais necessárias no modelo novo porque o disco gerenciado cria automaticamente contas de armazenamento em nome do cliente.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-113">These variables are no longer necessary in the new template because managed disk automatically creates storage accounts on the customer's behalf.</span></span> <span data-ttu-id="9d0c0-114">Da mesma forma, o nome do contêiner de vhd e o nome do disco do sistema operacional não são mais necessários porque o disco gerenciado nomeia automaticamente os discos e os contêineres de blob de armazenamento subjacente.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names the underlying storage blob containers and disks.</span></span>

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


<span data-ttu-id="9d0c0-115">Na comparação a seguir, podemos ver que atualizamos a versão de api de computação para 2016-04-30-preview, que é a versão mais antiga necessária para suporte de disco gerenciado com conjuntos de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-115">In the diff below, we can see that we updated the compute api version to 2016-04-30-preview, which is the earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="9d0c0-116">Observe que, se desejado, ainda podemos usar discos não gerenciados na versão de api nova com a sintaxe antiga.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-116">Note that we could still use unmanaged disks in the new api version with the old syntax if desired.</span></span> <span data-ttu-id="9d0c0-117">Em outras palavras, se atualizarmos somente a versão de api de computação e não alterarmos mais nada, o modelo deverá continuar a funcionar como antes.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-117">In other words, if we only update the compute api version and don't change anything else, the template should continue to work as before.</span></span>

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

<span data-ttu-id="9d0c0-118">Na comparação a seguir, podemos ver que removemos completamente o recurso de conta de armazenamento da matriz de recursos.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-118">In the diff below, we can see that we are removing the storage account resource from the resources array completely.</span></span> <span data-ttu-id="9d0c0-119">Não precisamos mais dele, uma vez que o disco gerenciado os cria automaticamente em nosso nome.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

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

<span data-ttu-id="9d0c0-120">Na comparação a seguir, removemos os dependes na cláusula referente do conjunto de dimensionamento para o loop que criava contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-120">In the diff below, we can see that we are removing the depends on clause referring from the scale set to the loop that was creating storage accounts.</span></span> <span data-ttu-id="9d0c0-121">No modelo antigo, isso era para garantir que as contas de armazenamento fossem criadas antes do conjunto de dimensionamento iniciar a criação, mas essa cláusula não é mais necessária em um disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-121">In the old template, this was ensuring that the storage accounts were created before the scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="9d0c0-122">Removemos também a propriedade de contêineres do vhd e a propriedade de nome de disco do sistema operacional, uma vez que essas propriedades são tratadas automaticamente pelo disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-122">We also remove the vhd containers property, and the os disk name property as these properties are automatically handled under the hood by managed disk.</span></span> <span data-ttu-id="9d0c0-123">Se desejar, adicione `"managedDisk": { "storageAccountType": "Premium_LRS" }` na configuração "osDisk" para discos do sistema operacional premium.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in the "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="9d0c0-124">Somente VMs com uma letra "s" maiúscula ou minúscula no sku da VM pode usar discos premium.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-124">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

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

<span data-ttu-id="9d0c0-125">Não há nenhuma propriedade explícita na configuração do conjunto de dimensionamento para se usar disco gerenciado ou não gerenciado.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-125">There is no explicit property in the scale set configuration for whether to use managed or unmanaged disk.</span></span> <span data-ttu-id="9d0c0-126">O conjunto de dimensionamento sabe que usar com base nas propriedades que estão presentes no perfil de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-126">The scale set knows which to use based on the properties that are present in the storage profile.</span></span> <span data-ttu-id="9d0c0-127">Portanto, ao modificar o modelo é importante garantir que as propriedades corretas estão no perfil de armazenamento do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-127">Thus, it is important when modifying the template to ensure that the right properties are in the storage profile of the scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="9d0c0-128">Discos de dados</span><span class="sxs-lookup"><span data-stu-id="9d0c0-128">Data disks</span></span>

<span data-ttu-id="9d0c0-129">Com as alterações acima, o conjunto de dimensionamento usa managed disks para o disco do sistema operacional, mas como ficam os discos de dados?</span><span class="sxs-lookup"><span data-stu-id="9d0c0-129">With the changes above, the scale set uses managed disks for the OS disk, but what about data disks?</span></span> <span data-ttu-id="9d0c0-130">Para adicionar discos de dados, adicione a propriedade "dataDisks" em "storageProfile" no mesmo nível que "osDisk".</span><span class="sxs-lookup"><span data-stu-id="9d0c0-130">To add data disks, add the "dataDisks" property under "storageProfile" at the same level as "osDisk".</span></span> <span data-ttu-id="9d0c0-131">O valor da propriedade é uma lista JSON de objetos, cada um tem propriedades "lun" (que deve ser exclusiva por disco de dados em uma VM), "createOption" ("empty" atualmente é a única opção com suporte) e "diskSizeGB" (o tamanho do disco em gigabytes; deve ser maior que 0 e menor que 1024) como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d0c0-131">The value of the property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently the only supported option), and "diskSizeGB" (the size of the disk in gigabytes; must be greater than 0 and less than 1024) as in the following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="9d0c0-132">Se você especificar `n` discos nesta matriz, cada VM no conjunto de dimensionamento obtém `n` discos de dados.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-132">If you specify `n` disks in this array, each VM in the scale set gets `n` data disks.</span></span> <span data-ttu-id="9d0c0-133">No entanto, observe que estes discos de dados são dispositivos brutos.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-133">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="9d0c0-134">Eles não estão formatados.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-134">They are not formatted.</span></span> <span data-ttu-id="9d0c0-135">Cabe ao cliente anexar, particionar e formatar os discos antes de usá-los.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-135">It is up to the customer to attach, paritition, and format the disks before using them.</span></span> <span data-ttu-id="9d0c0-136">Opcionalmente, também podemos especificar `"managedDisk": { "storageAccountType": "Premium_LRS" }` em cada objeto de disco de dados para especificar que deve ser um disco de dados premium.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-136">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object to specify that it should be a premium data disk.</span></span> <span data-ttu-id="9d0c0-137">Somente VMs com uma letra "s" maiúscula ou minúscula no sku da VM pode usar discos premium.</span><span class="sxs-lookup"><span data-stu-id="9d0c0-137">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

<span data-ttu-id="9d0c0-138">Para saber mais sobre como usar discos de dados com conjuntos de dimensionamento, veja [este artigo](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="9d0c0-138">To learn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9d0c0-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9d0c0-139">Next steps</span></span>
<span data-ttu-id="9d0c0-140">Para modelos do Resource Manager de exemplo usando conjuntos de escala, procure por "vmss" no [repositório github de Modelos de Início Rápido do Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="9d0c0-140">For example Resource Manager templates using scale sets, search for "vmss" in the [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="9d0c0-141">Para obter informações gerais, confira a [página de aterrissagem principal para conjuntos de escala](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="9d0c0-141">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

