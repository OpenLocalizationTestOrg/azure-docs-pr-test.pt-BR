---
title: aaaAzure discos de dados anexado do Virtual Machine escala conjuntos | Microsoft Docs
description: "Saiba como toouse anexou discos de dados com conjuntos de escala de máquinas virtuais"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="2125b-103">Conjuntos de Dimensionamento de VMs do Azure e discos de dados anexados</span><span class="sxs-lookup"><span data-stu-id="2125b-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="2125b-104">Azure [conjuntos de escala de máquina virtual](/azure/virtual-machine-scale-sets/) agora oferecem suporte a máquinas virtuais com discos de dados anexado.</span><span class="sxs-lookup"><span data-stu-id="2125b-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="2125b-105">Discos de dados podem ser definidos no perfil de armazenamento Olá para conjuntos de escala que foram criadas com discos gerenciado do Azure.</span><span class="sxs-lookup"><span data-stu-id="2125b-105">Data disks can be defined in hello storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="2125b-106">Anteriormente hello somente opções de armazenamento diretamente conectado disponíveis com VMs em conjuntos de escala foram unidade Olá sistema operacional e unidades temporárias.</span><span class="sxs-lookup"><span data-stu-id="2125b-106">Previously hello only directly attached storage options available with VMs in scale sets were hello OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="2125b-107">Quando você cria uma escala com discos de dados anexados definidos, você ainda precisará toomount e Olá formato discos de dentro de uma VM toouse-los (assim como para autônomo VMs do Azure).</span><span class="sxs-lookup"><span data-stu-id="2125b-107">When you create a scale set with attached data disks defined, you still need toomount and format hello disks from within a VM toouse them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="2125b-108">Uma maneira conveniente toodo trata toouse uma extensão de script personalizado que chama um script padrão toopartition e formatar todos os discos de dados de saudação em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2125b-108">A convenient way toodo this is toouse a custom script extension which calls a standard script toopartition and format all hello data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="2125b-109">Criar uma escala com discos de dados anexados</span><span class="sxs-lookup"><span data-stu-id="2125b-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="2125b-110">Um toocreate de maneira simples definir uma escala com discos conectados é Olá toouse [CLI do Azure](https://github.com/Azure/azure-cli) _vmss criar_ comando.</span><span class="sxs-lookup"><span data-stu-id="2125b-110">A simple way toocreate a scale set with attached disks is toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="2125b-111">saudação de exemplo a seguir cria um grupo de recursos do Azure e um conjunto de escala VM de 10 Ubuntu máquinas virtuais, cada um com discos de dados anexados 2, de 50 GB e 100 GB, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="2125b-111">hello following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="2125b-112">Observe que Olá _vmss criar_ comando padrões determinados valores de configuração se você não especificá-los.</span><span class="sxs-lookup"><span data-stu-id="2125b-112">Note that hello _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="2125b-113">toosee Olá as opções disponíveis que você pode substituir tente:</span><span class="sxs-lookup"><span data-stu-id="2125b-113">toosee hello available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="2125b-114">Outro toocreate de maneira um com discos de dados anexados a escala é toodefine uma escala definida em um modelo do Azure Resource Manager, inclua um _dataDisks_ seção Olá _storageProfile_e implantar Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="2125b-114">Another way toocreate a scale set with attached data disks is toodefine a scale set in an Azure Resource Manager template, include a _dataDisks_ section in hello _storageProfile_, and deploy hello template.</span></span> <span data-ttu-id="2125b-115">50 GB e 100 GB disco exemplo Hello acima seria definido como esse modelo hello:</span><span class="sxs-lookup"><span data-stu-id="2125b-115">hello 50 GB and 100 GB disk example above would be defined like this in hello template:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
<span data-ttu-id="2125b-116">Você pode ver um exemplo completo e pronto toodeploy de um modelo de conjunto de escala com um disco anexado definido aqui: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span><span class="sxs-lookup"><span data-stu-id="2125b-116">You can see a complete, ready toodeploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a><span data-ttu-id="2125b-117">Adicionar uma escala existente do tooan de disco de dados definido</span><span class="sxs-lookup"><span data-stu-id="2125b-117">Adding a data disk tooan existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="2125b-118">Você pode anexar apenas conjunto escala de tooa de discos de dados que foi criado com [discos gerenciado do Azure](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="2125b-118">You can only attach data disks tooa scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="2125b-119">Você pode adicionar uma escala VM dados disco tooa definida usando a CLI do Azure _anexar disco de vmss az_ comando.</span><span class="sxs-lookup"><span data-stu-id="2125b-119">You can add a data disk tooa VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="2125b-120">Especifique um lun que ainda não esteja em uso.</span><span class="sxs-lookup"><span data-stu-id="2125b-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="2125b-121">Olá CLI de exemplo a seguir adiciona uma unidade de 50 GB toolun 3:</span><span class="sxs-lookup"><span data-stu-id="2125b-121">hello following CLI example adds a 50 GB drive toolun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="2125b-122">Olá PowerShell de exemplo a seguir adiciona uma unidade de 50 GB toolun 3:</span><span class="sxs-lookup"><span data-stu-id="2125b-122">hello following PowerShell example adds a 50 GB drive toolun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="2125b-123">Diferentes tamanhos de VM tem limites diferentes em números de saudação de unidades conectadas que dão suporte.</span><span class="sxs-lookup"><span data-stu-id="2125b-123">Different VM sizes have different limits on hello numbers of attached drives they support.</span></span> <span data-ttu-id="2125b-124">Verificar Olá [características de tamanho de máquina virtual](../virtual-machines/windows/sizes.md) antes de adicionar um novo disco.</span><span class="sxs-lookup"><span data-stu-id="2125b-124">Check hello [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="2125b-125">Você também pode adicionar um disco com a adição de um novo toohello de entrada _dataDisks_ propriedade Olá _storageProfile_ de uma escala de conjunto de definição e aplicar alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="2125b-125">You can also add a disk by adding a new entry toohello _dataDisks_ property in hello _storageProfile_ of a scale set definition and applying hello change.</span></span> <span data-ttu-id="2125b-126">tootest, encontrar uma definição de conjunto de escala existente no hello [Gerenciador de recursos do Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2125b-126">tootest this, find an existing scale set definition in hello [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="2125b-127">Selecione _editar_ e adicionar uma nova lista de toohello de disco de discos de dados.</span><span class="sxs-lookup"><span data-stu-id="2125b-127">Select _Edit_ and add a new disk toohello list of data disks.</span></span> <span data-ttu-id="2125b-128">Por exemplo</span><span class="sxs-lookup"><span data-stu-id="2125b-128">E.g.</span></span> <span data-ttu-id="2125b-129">usando o exemplo hello acima:</span><span class="sxs-lookup"><span data-stu-id="2125b-129">using hello example above:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

<span data-ttu-id="2125b-130">Em seguida, selecione _colocar_ tooapply Olá altera o conjunto de escala de tooyour.</span><span class="sxs-lookup"><span data-stu-id="2125b-130">Then select _PUT_ tooapply hello changes tooyour scale set.</span></span> <span data-ttu-id="2125b-131">Este exemplo funcionaria enquanto você estiver usando um tamanho VM que oferece suporte a mais de dois discos de dados anexado.</span><span class="sxs-lookup"><span data-stu-id="2125b-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="2125b-132">Quando você faz uma escala de tooa alteração definição como adicionar ou remover um disco de dados, aplica VMs tooall recentemente criado, mas só se aplica tooexisting VMs se hello _upgradePolicy_ propriedade está definida muito "automática".</span><span class="sxs-lookup"><span data-stu-id="2125b-132">When you make a change tooa scale set definition such as adding or removing a data disk, it applies tooall newly created VMs, but only applies tooexisting VMs if hello _upgradePolicy_ property is set too"Automatic".</span></span> <span data-ttu-id="2125b-133">Se ele for definido muito "Manual", você precisa toomanually aplicar tooexisting de modelo novo Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="2125b-133">If it is set too"Manual", you need toomanually apply hello new model tooexisting VMs.</span></span> <span data-ttu-id="2125b-134">Você pode fazer isso no portal de saudação usando Olá _atualização AzureRmVmssInstance_ PowerShell ou usando Olá _az vmss update-instâncias_ comando CLI.</span><span class="sxs-lookup"><span data-stu-id="2125b-134">You can do this in hello portal, using hello _Update-AzureRmVmssInstance_ PowerShell command, or using hello _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a><span data-ttu-id="2125b-135">Adicionar discos de dados preenchida previamente tooan escala existente definido</span><span class="sxs-lookup"><span data-stu-id="2125b-135">Adding pre-populated data disks tooan existent scale set</span></span> 
> <span data-ttu-id="2125b-136">Quando você adiciona discos tooan existente conjunto de escala de modelo, por design, Olá disco sempre será criado vazio.</span><span class="sxs-lookup"><span data-stu-id="2125b-136">When you add disks tooan existent scale set model, by design, hello disk will always be created empty.</span></span> <span data-ttu-id="2125b-137">Este cenário também inclui novas instâncias criadas pelo conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="2125b-137">This scenario also includes new instances created by hello scale set.</span></span> <span data-ttu-id="2125b-138">Esse comportamento ocorre porque a definição de scaleset Olá tem um disco de dados vazio.</span><span class="sxs-lookup"><span data-stu-id="2125b-138">This behaviour is because hello scaleset definition has an empty data disk.</span></span> <span data-ttu-id="2125b-139">Em ordem toocreate dados preenchida previamente unidades para um modelo de conjunto de escala existente, você pode escolher qualquer uma das duas opções:</span><span class="sxs-lookup"><span data-stu-id="2125b-139">In order toocreate pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="2125b-140">Copie dados de saudação instância 0 VM toohello os discos de dados em Olá outras VMs executando um script personalizado.</span><span class="sxs-lookup"><span data-stu-id="2125b-140">Copy data from hello instance 0 VM toohello data disk(s) in hello other VMs by running a custom script.</span></span>
* <span data-ttu-id="2125b-141">Criar uma imagem gerenciada com disco Olá sistema operacional e disco de dados (com dados Olá necessário) e criar um novo scaleset com imagem hello.</span><span class="sxs-lookup"><span data-stu-id="2125b-141">Create a managed image with hello OS disk plus data disk (with hello required data) and create a new scaleset with hello image.</span></span> <span data-ttu-id="2125b-142">Dessa forma, cada nova VM criada terá um dados em disco que é fornecida na definição de saudação do hello scaleset.</span><span class="sxs-lookup"><span data-stu-id="2125b-142">This way every new VM created will have a data disk that that is provided in hello definition of hello scaleset.</span></span> <span data-ttu-id="2125b-143">Desde que essa definição fará referência tooan imagem com um disco de dados que tiver personalizado a dados, todas as máquinas virtuais em Olá scaleset automaticamente aparecerá com essas alterações.</span><span class="sxs-lookup"><span data-stu-id="2125b-143">Since this definition will refer tooan image with a data disk that has customized data, every virtual machine on hello scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="2125b-144">Olá toocreate de forma que uma imagem personalizada pode ser encontrada aqui: [criar uma imagem gerenciada de uma VM generalizada no Azure](/azure/virtual-machines/windows/capture-image-resource/)</span><span class="sxs-lookup"><span data-stu-id="2125b-144">hello way toocreate a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="2125b-145">Olá, o usuário deve toocapture Olá instância VM 0 que tem Olá dados necessários e, em seguida, usar esse vhd para definição de imagem hello.</span><span class="sxs-lookup"><span data-stu-id="2125b-145">hello user needs toocapture hello instance 0 VM which has hello required data, and then use that vhd for hello image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="2125b-146">Remoção de um disco de dados de um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="2125b-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="2125b-147">Você pode remover um disco de dados de um conjunto de dimensionamento de VM usando o comando _az vmss disk detach_ da CLI.</span><span class="sxs-lookup"><span data-stu-id="2125b-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="2125b-148">Por exemplo hello comando a seguir remove Olá disco definido no lun 2:</span><span class="sxs-lookup"><span data-stu-id="2125b-148">For example hello following command removes hello disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="2125b-149">Da mesma forma você também pode remover um disco de uma escala de conjunto, removendo uma entrada de saudação _dataDisks_ propriedade Olá _storageProfile_ e aplicar a alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="2125b-149">Similarly you can also remove a disk from a scale set by removing an entry from hello _dataDisks_ property in hello _storageProfile_ and applying hello change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="2125b-150">Observações adicionais</span><span class="sxs-lookup"><span data-stu-id="2125b-150">Additional notes</span></span>
<span data-ttu-id="2125b-151">Suporte para discos de dados anexados do conjunto de discos gerenciado do Azure e a escala está disponível na versão da API [ _2016-04-30-visualização_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) ou posterior do hello API Microsoft. Compute.</span><span class="sxs-lookup"><span data-stu-id="2125b-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of hello Microsoft.Compute API.</span></span>

<span data-ttu-id="2125b-152">Saudação inicial de implementação de suporte de disco anexado para conjuntos de escala, você não pode anexar ou desanexar discos de dados para/de VMs individuais em um conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="2125b-152">In hello initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="2125b-153">Suporte do portal do Azure para discos de dados anexados em conjuntos de escala é limitada inicialmente.</span><span class="sxs-lookup"><span data-stu-id="2125b-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="2125b-154">Dependendo dos requisitos, que você pode usar modelos do Azure, PowerShell, CLI, SDKs e API REST toomanage discos conectados.</span><span class="sxs-lookup"><span data-stu-id="2125b-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API toomanage attached disks.</span></span>


