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
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a><span data-ttu-id="1220d-103">Adicionar que modelo do conjunto de tooan uma imagem personalizada escala do Azure</span><span class="sxs-lookup"><span data-stu-id="1220d-103">Add a custom image tooan Azure scale set template</span></span>

<span data-ttu-id="1220d-104">Este artigo mostra como Olá toomodify [modelo de conjunto de escala viável mínima](./virtual-machine-scale-sets-mvss-start.md) toodeploy da imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="1220d-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy from custom image.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="1220d-105">Alterar a definição de modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="1220d-105">Change hello template definition</span></span>

<span data-ttu-id="1220d-106">Nosso modelo de conjunto de escala viável mínima pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e nosso modelo de implantação de escala Olá definida a partir de uma imagem personalizada pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="1220d-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="1220d-107">Vamos examinar Olá comparação usada toocreate este modelo (`git diff minimum-viable-scale-set custom-image`) parte por parte:</span><span class="sxs-lookup"><span data-stu-id="1220d-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="1220d-108">Criando uma imagem de disco gerenciada</span><span class="sxs-lookup"><span data-stu-id="1220d-108">Creating a managed disk image</span></span>

<span data-ttu-id="1220d-109">Se você já tiver uma imagem de disco gerenciado personalizado (um recurso do tipo `Microsoft.Compute/images`), você poderá ignorar esta seção.</span><span class="sxs-lookup"><span data-stu-id="1220d-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="1220d-110">Primeiro, adicionamos uma `sourceImageVhdUri` parâmetro, que é Olá URI toohello generalizado blob no armazenamento do Azure que contém a saudação toodeploy de imagem personalizada do.</span><span class="sxs-lookup"><span data-stu-id="1220d-110">First, we add a `sourceImageVhdUri` parameter, which is hello URI toohello generalized blob in Azure Storage that contains hello custom image toodeploy from.</span></span>


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

<span data-ttu-id="1220d-111">Em seguida, adicionamos um recurso do tipo `Microsoft.Compute/images`, que é a imagem de disco gerenciado de Olá baseada em blob Olá generalizado localizado no URI `sourceImageVhdUri`.</span><span class="sxs-lookup"><span data-stu-id="1220d-111">Next, we add a resource of type `Microsoft.Compute/images`, which is hello managed disk image based on hello generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="1220d-112">Essa imagem deve estar no hello mesma região que o conjunto de escala de saudação que utiliza.</span><span class="sxs-lookup"><span data-stu-id="1220d-112">This image must be in hello same region as hello scale set that uses it.</span></span> <span data-ttu-id="1220d-113">Nas propriedades de saudação da imagem hello, especificamos tipo hello SO, localização de saudação do blob de saudação (de saudação `sourceImageVhdUri` parâmetro) e o tipo de conta de armazenamento hello:</span><span class="sxs-lookup"><span data-stu-id="1220d-113">In hello properties of hello image, we specify hello OS type, hello location of hello blob (from hello `sourceImageVhdUri` parameter), and hello storage account type:</span></span>

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

<span data-ttu-id="1220d-114">Em Olá conjunto de escala de recurso, adicionamos uma `dependsOn` cláusula toohello imagem personalizada toomake se imagem Olá criada antes do conjunto de escala Olá tenta toodeploy da imagem de referência:</span><span class="sxs-lookup"><span data-stu-id="1220d-114">In hello scale set resource, we add a `dependsOn` clause referring toohello custom image toomake sure hello image gets created before hello scale set tries toodeploy from that image:</span></span>

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

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a><span data-ttu-id="1220d-115">Alterando a escala do conjunto de imagem de disco gerenciado propriedades toouse Olá</span><span class="sxs-lookup"><span data-stu-id="1220d-115">Changing scale set properties toouse hello managed disk image</span></span>

<span data-ttu-id="1220d-116">Em Olá `imageReference` de escala Olá definido `storageProfile`, em vez de especificar o publicador hello, oferta, sku e versão de uma imagem de plataforma, especificamos Olá `id` de saudação `Microsoft.Compute/images` recursos:</span><span class="sxs-lookup"><span data-stu-id="1220d-116">In hello `imageReference` of hello scale set `storageProfile`, instead of specifying hello publisher, offer, sku, and version of a platform image, we specify hello `id` of hello `Microsoft.Compute/images` resource:</span></span>

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

<span data-ttu-id="1220d-117">Neste exemplo, usamos Olá `resourceId` função tooget Olá ID de recurso de imagem Olá criado no hello mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="1220d-117">In this example, we use hello `resourceId` function tooget hello resource ID of hello image created in hello same template.</span></span> <span data-ttu-id="1220d-118">Se você criar imagem de disco gerenciado Olá com antecedência, você deve fornecer id de saudação da imagem em vez disso.</span><span class="sxs-lookup"><span data-stu-id="1220d-118">If you have created hello managed disk image beforehand, you should provide hello id of that image instead.</span></span> <span data-ttu-id="1220d-119">Essa id deve ser do formulário Olá: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span><span class="sxs-lookup"><span data-stu-id="1220d-119">This id must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1220d-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1220d-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
