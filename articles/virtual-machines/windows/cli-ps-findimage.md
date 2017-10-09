---
title: imagens do aaaSelect VM do Windows no Azure | Microsoft Docs
description: "Saiba como toouse do Azure PowerSHell toodetermine Olá publisher, oferta, SKU e versão para imagens de VM do Marketplace."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="50091-103">Como as imagens de toofind VM do Windows no hello Azure Marketplace com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="50091-103">How toofind Windows VM images in hello Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="50091-104">Este tópico descreve como toouse do Azure PowerShell toofind VM imagens no hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="50091-104">This topic describes how toouse Azure PowerShell toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="50091-105">Use este toospecify informações sobre uma imagem do Marketplace quando você criar uma VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="50091-105">Use this information toospecify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="50091-106">Certifique-se de que instalou e configurou o hello mais recente [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="50091-106">Make sure that you installed and configured hello latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="50091-107">Tabela das imagens do Windows mais usadas</span><span class="sxs-lookup"><span data-stu-id="50091-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="50091-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="50091-108">PublisherName</span></span> | <span data-ttu-id="50091-109">Oferta</span><span class="sxs-lookup"><span data-stu-id="50091-109">Offer</span></span> | <span data-ttu-id="50091-110">Sku</span><span class="sxs-lookup"><span data-stu-id="50091-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="50091-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="50091-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="50091-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="50091-112">WindowsServer</span></span> |<span data-ttu-id="50091-113">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="50091-113">2016-Datacenter</span></span> |
| <span data-ttu-id="50091-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="50091-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="50091-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="50091-115">WindowsServer</span></span> |<span data-ttu-id="50091-116">2016-Datacenter-Server-Core</span><span class="sxs-lookup"><span data-stu-id="50091-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="50091-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="50091-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="50091-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="50091-118">WindowsServer</span></span> |<span data-ttu-id="50091-119">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="50091-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="50091-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="50091-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="50091-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="50091-121">WindowsServer</span></span> |<span data-ttu-id="50091-122">2016-Nano-Server</span><span class="sxs-lookup"><span data-stu-id="50091-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="50091-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="50091-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="50091-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="50091-124">WindowsServer</span></span> |<span data-ttu-id="50091-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="50091-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="50091-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="50091-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="50091-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="50091-127">WindowsServer</span></span> |<span data-ttu-id="50091-128">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="50091-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="50091-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="50091-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="50091-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="50091-130">DynamicsNAV</span></span> |<span data-ttu-id="50091-131">2017</span><span class="sxs-lookup"><span data-stu-id="50091-131">2017</span></span> |
| <span data-ttu-id="50091-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="50091-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="50091-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="50091-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="50091-134">2016</span><span class="sxs-lookup"><span data-stu-id="50091-134">2016</span></span> |
| <span data-ttu-id="50091-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="50091-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="50091-136">SQL2016-WS2016</span><span class="sxs-lookup"><span data-stu-id="50091-136">SQL2016-WS2016</span></span> |<span data-ttu-id="50091-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="50091-137">Enterprise</span></span> |
| <span data-ttu-id="50091-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="50091-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="50091-139">SQL2014SP2-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="50091-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="50091-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="50091-140">Enterprise</span></span> |
| <span data-ttu-id="50091-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="50091-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="50091-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="50091-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="50091-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="50091-143">2012R2</span></span> |
| <span data-ttu-id="50091-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="50091-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="50091-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="50091-145">WindowsServerEssentials</span></span> |<span data-ttu-id="50091-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="50091-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="50091-147">Localizar imagens específicas</span><span class="sxs-lookup"><span data-stu-id="50091-147">Find specific images</span></span>


<span data-ttu-id="50091-148">Ao criar uma nova máquina virtual com o Gerenciador de recursos do Azure, em alguns casos é necessário toospecify uma imagem com a combinação de saudação do hello propriedades da imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="50091-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need toospecify an image with hello combination of hello following image properties:</span></span>

* <span data-ttu-id="50091-149">Editor</span><span class="sxs-lookup"><span data-stu-id="50091-149">Publisher</span></span>
* <span data-ttu-id="50091-150">Oferta</span><span class="sxs-lookup"><span data-stu-id="50091-150">Offer</span></span>
* <span data-ttu-id="50091-151">SKU</span><span class="sxs-lookup"><span data-stu-id="50091-151">SKU</span></span>

<span data-ttu-id="50091-152">Por exemplo, usar esses valores com hello [AzureRMVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet do PowerShell, ou com um modelo de grupo de recursos no qual você deve especificar o tipo de saudação da VM toobe criado.</span><span class="sxs-lookup"><span data-stu-id="50091-152">For example, use these values with hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify hello type of VM toobe created.</span></span>

<span data-ttu-id="50091-153">Se você precisar toodetermine esses valores, você pode executar Olá [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), e [AzureRMVMImageSku Get](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets imagens de saudação toonavigate.</span><span class="sxs-lookup"><span data-stu-id="50091-153">If you need toodetermine these values, you can run hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello images.</span></span> <span data-ttu-id="50091-154">Você determina estes valores:</span><span class="sxs-lookup"><span data-stu-id="50091-154">You determine these values:</span></span>

1. <span data-ttu-id="50091-155">Editores de imagem de saudação de lista.</span><span class="sxs-lookup"><span data-stu-id="50091-155">List hello image publishers.</span></span>
2. <span data-ttu-id="50091-156">Para um determinado editor, liste suas ofertas.</span><span class="sxs-lookup"><span data-stu-id="50091-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="50091-157">Para uma determinada oferta, liste seus SKUs.</span><span class="sxs-lookup"><span data-stu-id="50091-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="50091-158">Primeiro, lista Editores Olá com hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="50091-158">First, list hello publishers with hello following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="50091-159">Preencha o nome do publicador escolhido e execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="50091-159">Fill in your chosen publisher name and run hello following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="50091-160">Preencha o nome da oferta escolhido e execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="50091-160">Fill in your chosen offer name and run hello following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="50091-161">Da saída de saudação de saudação `Get-AzureRMVMImageSku` de comando, você tem todas as informações de saudação, você precisa de imagem de saudação toospecify para uma nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="50091-161">From hello output of hello `Get-AzureRMVMImageSku` command, you have all hello information you need toospecify hello image for a new virtual machine.</span></span>

<span data-ttu-id="50091-162">a seguir Olá mostra um exemplo completo:</span><span class="sxs-lookup"><span data-stu-id="50091-162">hello following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="50091-163">Saída:</span><span class="sxs-lookup"><span data-stu-id="50091-163">Output:</span></span>

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

<span data-ttu-id="50091-164">Para o publicador de "MicrosoftWindowsServer" hello:</span><span class="sxs-lookup"><span data-stu-id="50091-164">For hello "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="50091-165">Saída:</span><span class="sxs-lookup"><span data-stu-id="50091-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="50091-166">Oferta de "WindowsServer" hello:</span><span class="sxs-lookup"><span data-stu-id="50091-166">For hello "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="50091-167">Saída:</span><span class="sxs-lookup"><span data-stu-id="50091-167">Output:</span></span>

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

<span data-ttu-id="50091-168">Nesta lista, copiar Olá escolhida o nome da SKU, e você tem todas as informações de saudação de saudação `Set-AzureRMVMSourceImage` cmdlet do PowerShell ou para um modelo de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="50091-168">From this list, copy hello chosen SKU name, and you have all hello information for hello `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50091-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="50091-169">Next steps</span></span>
<span data-ttu-id="50091-170">Agora você pode escolher a imagem de saudação com precisão você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="50091-170">Now you can choose precisely hello image you want toouse.</span></span> <span data-ttu-id="50091-171">toocreate uma máquina virtual rapidamente usando informações da imagem hello, que você acabou de encontrar, consulte [criar uma máquina virtual do Windows com o PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="50091-171">toocreate a virtual machine quickly by using hello image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
