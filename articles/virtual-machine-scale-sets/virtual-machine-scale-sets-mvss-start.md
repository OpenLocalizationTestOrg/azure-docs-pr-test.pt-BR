---
title: "modelos de conjunto de aaaLearn sobre escala de máquinas virtuais | Microsoft Docs"
description: "Saiba toocreate uma escala mínima de viável definir modelo para conjuntos de escala de máquinas virtuais"
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
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="48e8e-103">Saiba mais sobre os modelos do conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="48e8e-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="48e8e-104">[Modelos do Gerenciador de recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) é uma ótima maneira toodeploy grupos de recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="48e8e-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="48e8e-105">Esta série de tutorial mostra como o modelo de conjunto de toocreate uma escala viável mínima e toomodify toosuit esse modelo vários cenários.</span><span class="sxs-lookup"><span data-stu-id="48e8e-105">This tutorial series shows how toocreate a minimum viable scale set template and how toomodify this template toosuit various scenarios.</span></span> <span data-ttu-id="48e8e-106">Todos os exemplos foram obtidos neste [repositório GitHub](https://github.com/gatneil/mvss).</span><span class="sxs-lookup"><span data-stu-id="48e8e-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="48e8e-107">Este modelo é pretendido toobe simples.</span><span class="sxs-lookup"><span data-stu-id="48e8e-107">This template is intended toobe simple.</span></span> <span data-ttu-id="48e8e-108">Para obter exemplos mais completos de escala configurar modelos, consulte Olá [repositório GitHub de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates) e procure as pastas que contêm a cadeia de caracteres hello `vmss`.</span><span class="sxs-lookup"><span data-stu-id="48e8e-108">For more complete examples of scale set templates, see hello [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain hello string `vmss`.</span></span>

<span data-ttu-id="48e8e-109">Se você já estiver familiarizado com a criação de modelos, você pode ignorar toohello "Próximas etapas" seção toosee como toomodify este modelo.</span><span class="sxs-lookup"><span data-stu-id="48e8e-109">If you are already familiar with creating templates, you can skip toohello "Next steps" section toosee how toomodify this template.</span></span>

## <a name="review-hello-template"></a><span data-ttu-id="48e8e-110">Modelo de saudação de revisão</span><span class="sxs-lookup"><span data-stu-id="48e8e-110">Review hello template</span></span>

<span data-ttu-id="48e8e-111">Use GitHub tooreview nosso escala viável mínima definir modelo, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="48e8e-111">Use GitHub tooreview our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="48e8e-112">Neste tutorial, podemos examinar Olá diff (`git diff master minimum-viable-scale-set`) escala viável mínima de saudação toocreate parte por parte de modelo de conjunto.</span><span class="sxs-lookup"><span data-stu-id="48e8e-112">In this tutorial, we examine hello diff (`git diff master minimum-viable-scale-set`) toocreate hello minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="48e8e-113">Definir $schema e contentVersion</span><span class="sxs-lookup"><span data-stu-id="48e8e-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="48e8e-114">Primeiro, definimos `$schema` e `contentVersion` no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-114">First, we define `$schema` and `contentVersion` in hello template.</span></span> <span data-ttu-id="48e8e-115">Olá `$schema` elemento define Olá versão de idioma do modelo hello e é usado para o realce de sintaxe do Visual Studio e recursos semelhantes de validação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-115">hello `$schema` element defines hello version of hello template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="48e8e-116">Olá `contentVersion` elemento não será usado pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="48e8e-116">hello `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="48e8e-117">Em vez disso, ele ajuda a manter o controle de versão do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-117">Instead, it helps you keep track of hello template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="48e8e-118">Definir parâmetros</span><span class="sxs-lookup"><span data-stu-id="48e8e-118">Define parameters</span></span>
<span data-ttu-id="48e8e-119">Em seguida, definimos dois parâmetros, `adminUsername` e `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="48e8e-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="48e8e-120">Os parâmetros são valores que você especificou em tempo de saudação da implantação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-120">Parameters are values you specify at hello time of deployment.</span></span> <span data-ttu-id="48e8e-121">Olá `adminUsername` parâmetro é simplesmente uma `string` tipo, mas porque `adminPassword` é um segredo, dê-tipo `securestring`.</span><span class="sxs-lookup"><span data-stu-id="48e8e-121">hello `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="48e8e-122">Posteriormente, esses parâmetros são passados na configuração do conjunto de escala hello.</span><span class="sxs-lookup"><span data-stu-id="48e8e-122">Later, these parameters are passed into hello scale set configuration.</span></span>

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a><span data-ttu-id="48e8e-123">Definir variáveis</span><span class="sxs-lookup"><span data-stu-id="48e8e-123">Define variables</span></span>
<span data-ttu-id="48e8e-124">Modelos do Gerenciador de recursos também permitem que você defina variáveis toobe usado posteriormente no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-124">Resource Manager templates also let you define variables toobe used later in hello template.</span></span> <span data-ttu-id="48e8e-125">Nosso exemplo não usa todas as variáveis, portanto deixamos objeto JSON de saudação vazio.</span><span class="sxs-lookup"><span data-stu-id="48e8e-125">Our example doesn't use any variables, so we've left hello JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="48e8e-126">Definir recursos</span><span class="sxs-lookup"><span data-stu-id="48e8e-126">Define resources</span></span>
<span data-ttu-id="48e8e-127">Next é a seção de recursos de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-127">Next is hello resources section of hello template.</span></span> <span data-ttu-id="48e8e-128">Aqui, você define o que você realmente deseja toodeploy.</span><span class="sxs-lookup"><span data-stu-id="48e8e-128">Here, you define what you actually want toodeploy.</span></span> <span data-ttu-id="48e8e-129">Ao contrário de `parameters` e `variables` (que são objetos JSON), `resources` é uma lista JSON de objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="48e8e-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="48e8e-130">Todos os recursos exigem propriedades `type`, `name`, `apiVersion` e `location`.</span><span class="sxs-lookup"><span data-stu-id="48e8e-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="48e8e-131">O primeiro recurso desse exemplo tem o tipo `Microsft.Network/virtualNetwork`, o nome `myVnet` e a apiVersion `2016-03-30`.</span><span class="sxs-lookup"><span data-stu-id="48e8e-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="48e8e-132">(toofind hello mais recente versão da API para um tipo de recurso, consulte Olá [documentação da API REST do Azure](https://docs.microsoft.com/rest/api/).)</span><span class="sxs-lookup"><span data-stu-id="48e8e-132">(toofind hello latest API version for a resource type, see hello [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="48e8e-133">Especificar o local</span><span class="sxs-lookup"><span data-stu-id="48e8e-133">Specify location</span></span>
<span data-ttu-id="48e8e-134">local de saudação toospecify para rede virtual hello, usamos um [função de Gerenciador de recursos de modelo](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="48e8e-134">toospecify hello location for hello virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="48e8e-135">Essa função deve ser colocada entre aspas e colchetes desta forma: `"[<template-function>]"`.</span><span class="sxs-lookup"><span data-stu-id="48e8e-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="48e8e-136">Nesse caso, usamos Olá `resourceGroup` função.</span><span class="sxs-lookup"><span data-stu-id="48e8e-136">In this case, we use hello `resourceGroup` function.</span></span> <span data-ttu-id="48e8e-137">Ele usa nenhum argumento e retorna um objeto JSON com metadados sobre o grupo de recursos de saudação que esta implantação está sendo implantada.</span><span class="sxs-lookup"><span data-stu-id="48e8e-137">It takes in no arguments and returns a JSON object with metadata about hello resource group this deployment is being deployed to.</span></span> <span data-ttu-id="48e8e-138">grupo de recursos de saudação é definido pelo usuário Olá no tempo de saudação da implantação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-138">hello resource group is set by hello user at hello time of deployment.</span></span> <span data-ttu-id="48e8e-139">Então, o índice para esse objeto JSON com `.location` tooget local de saudação do objeto JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-139">We then index into this JSON object with `.location` tooget hello location from hello JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="48e8e-140">Especificar as propriedades da rede virtual</span><span class="sxs-lookup"><span data-stu-id="48e8e-140">Specify virtual network properties</span></span>
<span data-ttu-id="48e8e-141">Cada recurso do Gerenciador de recursos tem seu próprio `properties` seção para recurso de toohello específico de configurações.</span><span class="sxs-lookup"><span data-stu-id="48e8e-141">Each Resource Manager resource has its own `properties` section for configurations specific toohello resource.</span></span> <span data-ttu-id="48e8e-142">Nesse caso, podemos especificar essa rede virtual Olá deve ter uma sub-rede usando o intervalo de endereços IP privado Olá `10.0.0.0/16`.</span><span class="sxs-lookup"><span data-stu-id="48e8e-142">In this case, we specify that hello virtual network should have one subnet using hello private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="48e8e-143">Um conjunto de dimensionamento sempre está contido em uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="48e8e-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="48e8e-144">Ele não pode abranger sub-redes.</span><span class="sxs-lookup"><span data-stu-id="48e8e-144">It cannot span subnets.</span></span>

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a><span data-ttu-id="48e8e-145">Adicionar a lista dependsOn</span><span class="sxs-lookup"><span data-stu-id="48e8e-145">Add dependsOn list</span></span>
<span data-ttu-id="48e8e-146">Além disso toohello necessário `type`, `name`, `apiVersion`, e `location` propriedades de cada recurso podem ter um opcional `dependsOn` lista de cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="48e8e-146">In addition toohello required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="48e8e-147">Essa lista especifica quais outros recursos dessa implantação devem ser concluídos antes da implantação desse recurso.</span><span class="sxs-lookup"><span data-stu-id="48e8e-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="48e8e-148">Nesse caso, há apenas um elemento na lista de hello, rede virtual de saudação do exemplo anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-148">In this case, there is only one element in hello list, hello virtual network from hello previous example.</span></span> <span data-ttu-id="48e8e-149">Podemos especificar essa dependência porque Olá conjunto de escala precisa Olá tooexist de rede antes de criar todas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="48e8e-149">We specify this dependency because hello scale set needs hello network tooexist before creating any VMs.</span></span> <span data-ttu-id="48e8e-150">Dessa forma, conjunto de escala Olá pode dar essas VMs endereços IP do intervalo de endereços IP de saudação especificado anteriormente Olá propriedades de rede.</span><span class="sxs-lookup"><span data-stu-id="48e8e-150">This way, hello scale set can give these VMs private IP addresses from hello IP address range previously specified in hello network properties.</span></span> <span data-ttu-id="48e8e-151">formato de saudação de cada cadeia de caracteres na lista de dependsOn Olá é `<type>/<name>`.</span><span class="sxs-lookup"><span data-stu-id="48e8e-151">hello format of each string in hello dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="48e8e-152">Use Olá mesmo `type` e `name` usado anteriormente na definição de recurso de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="48e8e-152">Use hello same `type` and `name` used previously in hello virtual network resource definition.</span></span>

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a><span data-ttu-id="48e8e-153">Especificar as propriedades do conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="48e8e-153">Specify scale set properties</span></span>
<span data-ttu-id="48e8e-154">Conjuntos de escala têm muitas propriedades para personalizar a saudação VMs no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-154">Scale sets have many properties for customizing hello VMs in hello scale set.</span></span> <span data-ttu-id="48e8e-155">Para obter uma lista completa dessas propriedades, consulte Olá [documentação da API REST do conjunto de escala](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span><span class="sxs-lookup"><span data-stu-id="48e8e-155">For a full list of these properties, see hello [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="48e8e-156">Para este tutorial, definiremos apenas algumas propriedades mais usadas.</span><span class="sxs-lookup"><span data-stu-id="48e8e-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="48e8e-157">Fornecer o tamanho e a capacidade da VM</span><span class="sxs-lookup"><span data-stu-id="48e8e-157">Supply VM size and capacity</span></span>
<span data-ttu-id="48e8e-158">Olá conjunto de escala de necessidades tooknow o tamanho da VM toocreate ("nome do sku") e quantos essa VMs toocreate ("capacidade de sku").</span><span class="sxs-lookup"><span data-stu-id="48e8e-158">hello scale set needs tooknow what size of VM toocreate ("sku name") and how many such VMs toocreate ("sku capacity").</span></span> <span data-ttu-id="48e8e-159">toosee quais tamanhos VM estão disponíveis, consulte Olá [documentação de tamanhos de VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span><span class="sxs-lookup"><span data-stu-id="48e8e-159">toosee which VM sizes are available, see hello [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="48e8e-160">Escolher o tipo de atualizações</span><span class="sxs-lookup"><span data-stu-id="48e8e-160">Choose type of updates</span></span>
<span data-ttu-id="48e8e-161">conjunto de escala Olá também precisa tooknow como toohandle atualiza no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-161">hello scale set also needs tooknow how toohandle updates on hello scale set.</span></span> <span data-ttu-id="48e8e-162">Atualmente, há duas opções, `Manual` e `Automatic`.</span><span class="sxs-lookup"><span data-stu-id="48e8e-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="48e8e-163">Para obter mais informações sobre diferenças de saudação entre hello dois, consulte a documentação do hello em [como tooupgrade uma conjunto de escala](./virtual-machine-scale-sets-upgrade-scale-set.md).</span><span class="sxs-lookup"><span data-stu-id="48e8e-163">For more information on hello differences between hello two, see hello documentation on [how tooupgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="48e8e-164">Escolher o sistema operacional da VM</span><span class="sxs-lookup"><span data-stu-id="48e8e-164">Choose VM operating system</span></span>
<span data-ttu-id="48e8e-165">Olá conjunto de escala necessidades tooknow tooput o sistema operacional em VMs hello.</span><span class="sxs-lookup"><span data-stu-id="48e8e-165">hello scale set needs tooknow what operating system tooput on hello VMs.</span></span> <span data-ttu-id="48e8e-166">Aqui, podemos criar VMs de Olá com uma imagem de 16.04 LTS Ubuntu totalmente atualizada.</span><span class="sxs-lookup"><span data-stu-id="48e8e-166">Here, we create hello VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a><span data-ttu-id="48e8e-167">Especificar computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="48e8e-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="48e8e-168">conjunto de escala Olá implanta várias VMs.</span><span class="sxs-lookup"><span data-stu-id="48e8e-168">hello scale set deploys multiple VMs.</span></span> <span data-ttu-id="48e8e-169">Em vez de especificar o nome de cada VM, especificamos `computerNamePrefix`.</span><span class="sxs-lookup"><span data-stu-id="48e8e-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="48e8e-170">Hello conjunto de escala acrescenta um prefixo de toohello de índice para cada VM para nomes de VM tem formulário Olá `<computerNamePrefix>_<auto-generated-index>`.</span><span class="sxs-lookup"><span data-stu-id="48e8e-170">hello scale set appends an index toohello prefix for each VM, so VM names have hello form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="48e8e-171">Olá trecho de código a seguir, usamos parâmetros de saudação do antes de tooset Olá administrador username e password para todas as VMs no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-171">In hello following snippet, we use hello parameters from before tooset hello administrator username and password for all VMs in hello scale set.</span></span> <span data-ttu-id="48e8e-172">Podemos fazer isso com hello `parameters` modelo de função.</span><span class="sxs-lookup"><span data-stu-id="48e8e-172">We do this with hello `parameters` template function.</span></span> <span data-ttu-id="48e8e-173">Essa função assume uma cadeia de caracteres que especifica quais tooand toorefer de parâmetro gera o valor de saudação para esse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="48e8e-173">This function takes in a string that specifies which parameter toorefer tooand outputs hello value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="48e8e-174">Especificar a configuração de rede da VM</span><span class="sxs-lookup"><span data-stu-id="48e8e-174">Specify VM network configuration</span></span>
<span data-ttu-id="48e8e-175">Por fim, precisamos configuração de rede toospecify Olá para Olá VMs no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-175">Finally, we need toospecify hello network configuration for hello VMs in hello scale set.</span></span> <span data-ttu-id="48e8e-176">Nesse caso, precisamos apenas toospecify Olá ID de sub-rede Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="48e8e-176">In this case, we only need toospecify hello ID of hello subnet created earlier.</span></span> <span data-ttu-id="48e8e-177">Isso informa Olá conjunto de escala tooput interfaces de rede Olá nesta sub-rede.</span><span class="sxs-lookup"><span data-stu-id="48e8e-177">This tells hello scale set tooput hello network interfaces in this subnet.</span></span>

<span data-ttu-id="48e8e-178">Você pode obter ID de saudação da rede virtual hello, que contém a sub-rede hello usando Olá `resourceId` modelo de função.</span><span class="sxs-lookup"><span data-stu-id="48e8e-178">You can get hello ID of hello virtual network containing hello subnet by using hello `resourceId` template function.</span></span> <span data-ttu-id="48e8e-179">Essa função usa o tipo de saudação e o nome de um recurso e retorna Olá identificador totalmente qualificado do recurso.</span><span class="sxs-lookup"><span data-stu-id="48e8e-179">This function takes in hello type and name of a resource and returns hello fully qualified identifier of that resource.</span></span> <span data-ttu-id="48e8e-180">Essa ID tem o formato de saudação:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="48e8e-180">This ID has hello form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="48e8e-181">No entanto, Olá identificador de rede virtual Olá não é suficiente.</span><span class="sxs-lookup"><span data-stu-id="48e8e-181">However, hello identifier of hello virtual network is not enough.</span></span> <span data-ttu-id="48e8e-182">Você deve especificar a sub-rede específica Olá Olá conjunto de escala de que máquinas virtuais devem estar no.</span><span class="sxs-lookup"><span data-stu-id="48e8e-182">You must specify hello specific subnet that hello scale set VMs should be in.</span></span> <span data-ttu-id="48e8e-183">toodo, concatenar `/subnets/mySubnet` toohello ID da rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="48e8e-183">toodo this, concatenate `/subnets/mySubnet` toohello ID of hello virtual network.</span></span> <span data-ttu-id="48e8e-184">resultado de saudação é Olá totalmente qualificado ID de sub-rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-184">hello result is hello fully qualified ID of hello subnet.</span></span> <span data-ttu-id="48e8e-185">Fazer essa concatenação com hello `concat` função, que usa uma série de cadeias de caracteres e retorna sua concatenação.</span><span class="sxs-lookup"><span data-stu-id="48e8e-185">Do this concatenation with hello `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a><span data-ttu-id="48e8e-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48e8e-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
