---
title: "conjunto de escala de uma máquina virtual do Azure aaaUpgrade | Microsoft Docs"
description: "Atualizar um conjunto de dimensionamento de máquinas virtuais do Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="341e8-103">Atualizar um conjunto de escala de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="341e8-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="341e8-104">Este artigo descreve como você pode implementar uma escala de máquina virtual do Azure do sistema operacional atualização tooan definida sem qualquer tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="341e8-104">This article describes how you can roll out an OS update tooan Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="341e8-105">Nesse contexto, uma atualização do sistema operacional envolve alterar versão hello ou SKU do hello SO ou Olá URI de uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="341e8-105">In this context, an OS update involves changing hello version or SKU of hello OS or changing hello URI of a custom image.</span></span> <span data-ttu-id="341e8-106">Atualizar sem tempo de inatividade significa atualizar uma máquina virtual por vez ou em grupos (por exemplo, um domínio de falha por vez), em vez de todas de uma só vez.</span><span class="sxs-lookup"><span data-stu-id="341e8-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="341e8-107">Ao fazer isso, todas as máquinas virtuais que não estiverem sendo atualizadas podem continuar em execução.</span><span class="sxs-lookup"><span data-stu-id="341e8-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="341e8-108">tooavoid ambiguidade, vamos distinguir quatro tipos de atualização do sistema operacional que talvez você queira tooperform:</span><span class="sxs-lookup"><span data-stu-id="341e8-108">tooavoid ambiguity, let’s distinguish four types of OS update you might want tooperform:</span></span>

* <span data-ttu-id="341e8-109">Alterar a versão hello ou SKU de uma imagem de plataforma.</span><span class="sxs-lookup"><span data-stu-id="341e8-109">Changing hello version or SKU of a platform image.</span></span> <span data-ttu-id="341e8-110">Por exemplo, a alteração Ubuntu versão 14.04.2-LTS de 14.04.201506100 too14.04.201507060 ou alterando Olá Ubuntu 15.10/mais recente SKU too16.04.0-LTS/latest.</span><span class="sxs-lookup"><span data-stu-id="341e8-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 too14.04.201507060, or changing hello Ubuntu 15.10/latest SKU too16.04.0-LTS/latest.</span></span> <span data-ttu-id="341e8-111">Esse cenário é abordado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="341e8-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="341e8-112">Alterando Olá URI que aponta tooa nova versão de uma imagem personalizada criada por você (**propriedades** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **imagem** > **uri**).</span><span class="sxs-lookup"><span data-stu-id="341e8-112">Changing hello URI that points tooa new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="341e8-113">Esse cenário é abordado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="341e8-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="341e8-114">Alterando a referência de imagem de saudação de um conjunto de escala que foi criado usando discos gerenciado do Azure.</span><span class="sxs-lookup"><span data-stu-id="341e8-114">Changing hello image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="341e8-115">Aplicação de patch Olá SO de dentro de uma máquina virtual (isso exemplos de instalar um patch de segurança e executar o Windows Update).</span><span class="sxs-lookup"><span data-stu-id="341e8-115">Patching hello OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="341e8-116">Esse cenário tem suporte, mas não é abordado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="341e8-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="341e8-117">Conjuntos de escala de máquina virtual implantados como parte de um cluster do [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) não são abordados aqui.</span><span class="sxs-lookup"><span data-stu-id="341e8-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="341e8-118">Consulte [Patch no SO do Windows no seu cluster de Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) para obter mais informações sobre aplicação de patch do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="341e8-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="341e8-119">Olá básica sequência para alterar Olá versão/SKU de sistema operacional de uma imagem de plataforma ou Olá URI de uma imagem personalizada será semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="341e8-119">hello basic sequence for changing hello OS version/SKU of a platform image or hello URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="341e8-120">Obter o modelo de conjunto de escala de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="341e8-120">Get hello virtual machine scale set model.</span></span>
2. <span data-ttu-id="341e8-121">Alterar a versão de hello, SKU, referência de imagem ou valor URI no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="341e8-121">Change hello version, SKU, image reference, or URI value in hello model.</span></span>
3. <span data-ttu-id="341e8-122">Atualize o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="341e8-122">Update hello model.</span></span>
4. <span data-ttu-id="341e8-123">Fazer um *manualUpgrade* chamar em máquinas virtuais Olá Olá conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="341e8-123">Do a *manualUpgrade* call on hello virtual machines in hello scale set.</span></span> <span data-ttu-id="341e8-124">Esta etapa só será relevante se *upgradePolicy* está definido muito**Manual** na sua escala definida.</span><span class="sxs-lookup"><span data-stu-id="341e8-124">This step is only relevant if *upgradePolicy* is set too**Manual** in your scale set.</span></span> <span data-ttu-id="341e8-125">Se ele for definido muito**automáticas**, todas as máquinas virtuais de saudação são atualizadas ao mesmo tempo, fazendo com que o tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="341e8-125">If it is set too**Automatic**, all hello virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="341e8-126">Com essas informações em mente, vamos ver como você poderia atualizar a versão de saudação de uma escala definidas no PowerShell e usando a API REST de saudação.</span><span class="sxs-lookup"><span data-stu-id="341e8-126">With this information in mind, let’s see how you could update hello version of a scale set in PowerShell, and by using hello REST API.</span></span> <span data-ttu-id="341e8-127">Esses exemplos abrangem caso de saudação de uma imagem de plataforma, mas este artigo fornece informações suficientes para que você tooadapt essa imagem personalizada do processo tooa.</span><span class="sxs-lookup"><span data-stu-id="341e8-127">These examples cover hello case of a platform image, but this article provides enough information for you tooadapt this process tooa custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="341e8-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="341e8-128">PowerShell</span></span>
<span data-ttu-id="341e8-129">Este exemplo atualiza um conjunto de escala de máquinas virtuais do Windows (Criando toohello nova versão do 4.0.20160229.</span><span class="sxs-lookup"><span data-stu-id="341e8-129">This example updates a Windows virtual machine scale set (creating toohello new version 4.0.20160229.</span></span> <span data-ttu-id="341e8-130">Depois de atualizar o modelo de hello, ele faz uma atualização de uma instância de máquina virtual por vez.</span><span class="sxs-lookup"><span data-stu-id="341e8-130">After updating hello model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="341e8-131">Se você estiver atualizando hello URI para uma imagem personalizada em vez de alterar uma versão da imagem de plataforma, substitua hello "hello nova versão do conjunto de" linha com um comando que atualizará Olá URI da imagem de origem.</span><span class="sxs-lookup"><span data-stu-id="341e8-131">If you are updating hello URI for a custom image instead of changing a platform image version, replace hello “set hello new version” line with a command that will update hello source image URI.</span></span> <span data-ttu-id="341e8-132">Por exemplo, se o conjunto de escala de saudação foi criado sem o uso de discos gerenciado do Azure, atualização Olá teria esta aparência:</span><span class="sxs-lookup"><span data-stu-id="341e8-132">For example, if hello scale set was created without using Azure Managed Disks, hello update would look like this:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="341e8-133">Se uma imagem personalizada com base em conjunto de escala foi criado usando discos gerenciado do Azure, e a referência de imagem Olá deve ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="341e8-133">If a custom image based scale set was created using Azure Managed Disks, then hello image reference would be updated.</span></span> <span data-ttu-id="341e8-134">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="341e8-134">For example:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a><span data-ttu-id="341e8-135">Olá API REST</span><span class="sxs-lookup"><span data-stu-id="341e8-135">hello REST API</span></span>
<span data-ttu-id="341e8-136">Aqui estão alguns exemplos de Python que usam Olá API REST do Azure tooroll uma atualização de versão do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="341e8-136">Here are a couple of Python examples that use hello Azure REST API tooroll out an OS version update.</span></span> <span data-ttu-id="341e8-137">Ambos usam lightweight Olá [azurerm](https://pypi.python.org/pypi/azurerm) biblioteca da API REST do Azure wrapper funções toodo um GET em escala Olá definir modelo, seguido por um PUT com um modelo atualizado.</span><span class="sxs-lookup"><span data-stu-id="341e8-137">Both use hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions toodo a GET on hello scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="341e8-138">Eles também examinar os modos de exibição de instâncias de máquina virtual tooidentify Olá máquinas virtuais do domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="341e8-138">They also look at virtual machine instances views tooidentify hello virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="341e8-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="341e8-139">Vmssupgrade</span></span>
 <span data-ttu-id="341e8-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) é um script de Python que usou tooroll out um tooa de atualização de sistema operacional executando escala de máquinas virtuais definir um domínio de atualização por vez.</span><span class="sxs-lookup"><span data-stu-id="341e8-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used tooroll out an OS upgrade tooa running virtual machine scale set one update domain at a time.</span></span>

![Script Vmssupgrade para escolher máquinas virtuais ou um domínio de atualização](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="341e8-142">Esse script permite que você escolher tooupdate de máquinas virtuais específicas ou especificar um domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="341e8-142">This script lets you choose specific virtual machines tooupdate or specify an update domain.</span></span> <span data-ttu-id="341e8-143">Ele dá suporte a alteração de uma versão de imagem de plataforma ou a alteração Olá URI de uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="341e8-143">It supports changing a platform image version or changing hello URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="341e8-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="341e8-144">Vmsseditor</span></span>
<span data-ttu-id="341e8-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) é um editor para fins gerais para conjuntos de escala de máquina virtual que mostra o status da máquina virtual como um mapa de dados no qual uma linha representa um domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="341e8-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="341e8-146">Entre outras coisas, você pode atualizar o modelo de saudação para um conjunto de escala com uma nova versão, SKU ou URI da imagem personalizada e escolha tooupgrade de domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="341e8-146">Among other things, you can update hello model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains tooupgrade.</span></span> <span data-ttu-id="341e8-147">Quando você fizer isso, todas as máquinas virtuais de saudação nesse domínio de atualização são atualizados toohello novo modelo.</span><span class="sxs-lookup"><span data-stu-id="341e8-147">When you do so, all hello virtual machines in that update domain are upgraded toohello new model.</span></span> <span data-ttu-id="341e8-148">Como alternativa, você pode fazer uma atualização sem interrupção com base no tamanho de lote de saudação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="341e8-148">Alternatively, you can do a rolling upgrade based on hello batch size of your choice.</span></span>  

<span data-ttu-id="341e8-149">Olá seguinte captura de tela mostra um modelo de uma escala definidas para Ubuntu 14.04-2LTS versão 14.04.201507060.</span><span class="sxs-lookup"><span data-stu-id="341e8-149">hello following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="341e8-150">Muito mais opções foram adicionadas toothis ferramenta desde que foi feita nesta captura de tela.</span><span class="sxs-lookup"><span data-stu-id="341e8-150">Many more options have been added toothis tool since this screenshot was taken.</span></span>

![Modelo de Vmsseditor de um conjunto de escala para o Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="341e8-152">Depois de clicar em **atualização** e **obter detalhes**, máquinas virtuais em UD 0 iniciar tooupdate.</span><span class="sxs-lookup"><span data-stu-id="341e8-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start tooupdate.</span></span>

![Vmsseditor mostrando atualização em andamento](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

