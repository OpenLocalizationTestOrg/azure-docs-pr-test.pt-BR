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
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a><span data-ttu-id="247b1-104">Converter um modelo de conjunto de escala conjunto modelo tooa disco gerenciado escala</span><span class="sxs-lookup"><span data-stu-id="247b1-104">Convert a scale set template tooa managed disk scale set template</span></span>

<span data-ttu-id="247b1-105">Os clientes com um modelo do Gerenciador de recursos para a criação de uma escala definida usando o disco gerenciado não poderá toomodify-toouse gerenciados em disco.</span><span class="sxs-lookup"><span data-stu-id="247b1-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish toomodify it toouse managed disk.</span></span> <span data-ttu-id="247b1-106">Este artigo mostra como toodo esse, usando como um exemplo de uma solicitação de recepção de saudação [modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates), um repositório dirigida pela comunidade para modelos do Gerenciador de recursos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="247b1-106">This article shows how toodo this, using as an example a pull request from hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="247b1-107">solicitação de recepção completo Olá pode ser vista aqui: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), e as partes relevantes de diferença Olá Olá estão abaixo, junto com explicações:</span><span class="sxs-lookup"><span data-stu-id="247b1-107">hello full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and hello relevant parts of hello diff are below, along with explanations:</span></span>

## <a name="making-hello-os-disks-managed"></a><span data-ttu-id="247b1-108">Tornando os discos do sistema operacional Olá gerenciados</span><span class="sxs-lookup"><span data-stu-id="247b1-108">Making hello OS disks managed</span></span>

<span data-ttu-id="247b1-109">Comparação de saudação abaixo, vemos que removemos várias variáveis relacionadas toostorage disco propriedades de conta e.</span><span class="sxs-lookup"><span data-stu-id="247b1-109">In hello diff below, we can see that we have removed several variables related toostorage account and disk properties.</span></span> <span data-ttu-id="247b1-110">Tipo de conta de armazenamento não é mais necessário (Standard_LRS é o padrão de saudação), mas ainda pode especificá-lo se o que queremos.</span><span class="sxs-lookup"><span data-stu-id="247b1-110">Storage account type is no longer necessary (Standard_LRS is hello default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="247b1-111">Apenas Standard_LRS e Premium_LRS são compatíveis com um disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="247b1-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="247b1-112">Novo sufixo de conta de armazenamento, a matriz de cadeia de caracteres exclusiva e a contagem de sa foram usados em Olá antigo modelo toogenerate armazenamento nomes de conta.</span><span class="sxs-lookup"><span data-stu-id="247b1-112">New storage account suffix, unique string array, and sa count were used in hello old template toogenerate storage account names.</span></span> <span data-ttu-id="247b1-113">Essas variáveis não são mais necessárias no novo modelo de saudação porque o disco gerenciado cria automaticamente as contas de armazenamento em nome saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="247b1-113">These variables are no longer necessary in hello new template because managed disk automatically creates storage accounts on hello customer's behalf.</span></span> <span data-ttu-id="247b1-114">Da mesma forma, nome do contêiner de vhd e o nome de disco do sistema operacional não são mais necessárias porque o disco gerenciado automaticamente nomes de discos e contêineres de blob de armazenamento subjacente hello.</span><span class="sxs-lookup"><span data-stu-id="247b1-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names hello underlying storage blob containers and disks.</span></span>

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


<span data-ttu-id="247b1-115">Na comparação Olá abaixo, podemos pode consulte que atualizamos Olá computação versão too2016-04-30-visualização da api, que é hello mais antiga versão necessária para suporte de disco gerenciado com conjuntos de escala.</span><span class="sxs-lookup"><span data-stu-id="247b1-115">In hello diff below, we can see that we updated hello compute api version too2016-04-30-preview, which is hello earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="247b1-116">Observe que estamos ainda pode usar discos não gerenciados na nova versão da api Olá com sintaxe antiga Olá se desejado.</span><span class="sxs-lookup"><span data-stu-id="247b1-116">Note that we could still use unmanaged disks in hello new api version with hello old syntax if desired.</span></span> <span data-ttu-id="247b1-117">Em outras palavras, se podemos atualizar somente hello versão da api de computação e não altere mais nada, modelo Olá deve continuar toowork como antes.</span><span class="sxs-lookup"><span data-stu-id="247b1-117">In other words, if we only update hello compute api version and don't change anything else, hello template should continue toowork as before.</span></span>

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

<span data-ttu-id="247b1-118">Comparação de saudação abaixo, podemos ver que estamos removendo recursos de conta de armazenamento de saudação da matriz de recursos de saudação completamente.</span><span class="sxs-lookup"><span data-stu-id="247b1-118">In hello diff below, we can see that we are removing hello storage account resource from hello resources array completely.</span></span> <span data-ttu-id="247b1-119">Não precisamos mais dele, uma vez que o disco gerenciado os cria automaticamente em nosso nome.</span><span class="sxs-lookup"><span data-stu-id="247b1-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

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

<span data-ttu-id="247b1-120">Em comparação Olá abaixo, podemos pode consulte que estamos removendo Olá depende cláusula referindo-se de loop toohello de conjunto de escala de saudação que estava criando contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="247b1-120">In hello diff below, we can see that we are removing hello depends on clause referring from hello scale set toohello loop that was creating storage accounts.</span></span> <span data-ttu-id="247b1-121">No modelo antigo e hello, isso foi garantir que as contas de armazenamento Olá foram criadas antes do conjunto de escala Olá começou a criação, mas essa cláusula não é mais necessária com disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="247b1-121">In hello old template, this was ensuring that hello storage accounts were created before hello scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="247b1-122">Também remove a propriedade de contêineres de vhd Olá e Olá propriedade de nome de disco do sistema operacional, essas propriedades são tratados automaticamente subjacente Olá por disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="247b1-122">We also remove hello vhd containers property, and hello os disk name property as these properties are automatically handled under hello hood by managed disk.</span></span> <span data-ttu-id="247b1-123">Se nós desejavam, poderíamos adicionar `"managedDisk": { "storageAccountType": "Premium_LRS" }` na configuração de "osDisk" hello se quiséssemos discos do sistema operacional de premium.</span><span class="sxs-lookup"><span data-stu-id="247b1-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in hello "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="247b1-124">Apenas VMs com uma letra maiuscula ou do minúscula ' hello VM sku pode usar discos premium.</span><span class="sxs-lookup"><span data-stu-id="247b1-124">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

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

<span data-ttu-id="247b1-125">Não há nenhuma propriedade explícita na configuração de conjunto de escala Olá para se toouse gerenciado ou não gerenciado de disco.</span><span class="sxs-lookup"><span data-stu-id="247b1-125">There is no explicit property in hello scale set configuration for whether toouse managed or unmanaged disk.</span></span> <span data-ttu-id="247b1-126">conjunto de escala Olá sabe quais toouse com base nas propriedades de saudação que estão presentes no perfil de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="247b1-126">hello scale set knows which toouse based on hello properties that are present in hello storage profile.</span></span> <span data-ttu-id="247b1-127">Portanto, é importante ao modificar Olá tooensure de modelo que são propriedades do direito de saudação no perfil de armazenamento de saudação do conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="247b1-127">Thus, it is important when modifying hello template tooensure that hello right properties are in hello storage profile of hello scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="247b1-128">Discos de dados</span><span class="sxs-lookup"><span data-stu-id="247b1-128">Data disks</span></span>

<span data-ttu-id="247b1-129">Com alterações Olá acima, Olá escala conjunto usa gerenciado discos para Olá SO de disco, mas e quanto os discos de dados? tooadd os discos de dados, adicionar propriedade do hello "dataDisks" em "storageProfile" no mesmo nível como "osDisk" de saudação.</span><span class="sxs-lookup"><span data-stu-id="247b1-129">With hello changes above, hello scale set uses managed disks for hello OS disk, but what about data disks? tooadd data disks, add hello "dataDisks" property under "storageProfile" at hello same level as "osDisk".</span></span> <span data-ttu-id="247b1-130">valor da propriedade Olá Olá é uma lista JSON de objetos, cada um deles tem propriedades "lun" (que deve ser exclusivo por disco de dados em uma máquina virtual), "createOption" ("vazio" está atualmente Olá só há suporte para opção) e "diskSizeGB" (Olá tamanho do disco de saudação em gigabytes; deve ser maior que 0 e menor que 1024) conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="247b1-130">hello value of hello property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently hello only supported option), and "diskSizeGB" (hello size of hello disk in gigabytes; must be greater than 0 and less than 1024) as in hello following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="247b1-131">Se você especificar `n` discos nesta matriz, cada VM em escala Olá definir obtém `n` discos de dados.</span><span class="sxs-lookup"><span data-stu-id="247b1-131">If you specify `n` disks in this array, each VM in hello scale set gets `n` data disks.</span></span> <span data-ttu-id="247b1-132">No entanto, observe que estes discos de dados são dispositivos brutos.</span><span class="sxs-lookup"><span data-stu-id="247b1-132">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="247b1-133">Eles não estão formatados.</span><span class="sxs-lookup"><span data-stu-id="247b1-133">They are not formatted.</span></span> <span data-ttu-id="247b1-134">É toohello cliente tooattach, Partition e discos de saudação do formato antes de usá-los.</span><span class="sxs-lookup"><span data-stu-id="247b1-134">It is up toohello customer tooattach, paritition, and format hello disks before using them.</span></span> <span data-ttu-id="247b1-135">Opcionalmente, seria possível também especificar `"managedDisk": { "storageAccountType": "Premium_LRS" }` em cada toospecify de objeto de disco de dados que ela deve ser um disco de dados premium.</span><span class="sxs-lookup"><span data-stu-id="247b1-135">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object toospecify that it should be a premium data disk.</span></span> <span data-ttu-id="247b1-136">Apenas VMs com uma letra maiuscula ou do minúscula ' hello VM sku pode usar discos premium.</span><span class="sxs-lookup"><span data-stu-id="247b1-136">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

<span data-ttu-id="247b1-137">toolearn mais sobre como usar discos de dados com conjuntos de escala, consulte [neste artigo](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="247b1-137">toolearn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="247b1-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="247b1-138">Next steps</span></span>
<span data-ttu-id="247b1-139">Por exemplo modelos do Gerenciador de recursos usando conjuntos de escala, procure "vmss" no hello [repositório github de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="247b1-139">For example Resource Manager templates using scale sets, search for "vmss" in hello [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="247b1-140">Para obter informações gerais, confira Olá [página principal para conjuntos de escala](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="247b1-140">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

