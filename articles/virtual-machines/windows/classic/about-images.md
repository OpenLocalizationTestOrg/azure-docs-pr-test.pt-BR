---
title: "imagens de aaaAbout para máquinas virtuais do Windows | Microsoft Docs"
description: "Saiba mais sobre como as imagens são usadas com máquinas virtuais do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="ba92f-103">Sobre imagens de máquinas virtuais do Windows</span><span class="sxs-lookup"><span data-stu-id="ba92f-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ba92f-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ba92f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ba92f-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="ba92f-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ba92f-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba92f-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ba92f-107">Para obter informações sobre como localizar e usar imagens no modelo do Gerenciador de recursos de hello, consulte [aqui](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba92f-107">For information about finding and using images in hello Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="ba92f-108">Trabalhando com imagens</span><span class="sxs-lookup"><span data-stu-id="ba92f-108">Working with images</span></span>

<span data-ttu-id="ba92f-109">Você pode usar o módulo do PowerShell do Azure hello e tooyour de disponíveis imagens assinatura do Azure de saudação de toomanage portal do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ba92f-109">You can use hello Azure PowerShell module and hello Azure portal toomanage hello images available tooyour Azure subscription.</span></span> <span data-ttu-id="ba92f-110">módulo do PowerShell do Azure Olá fornece mais opções de comando, para que você pode identificar exatamente o que você deseja toosee ou fazer.</span><span class="sxs-lookup"><span data-stu-id="ba92f-110">hello Azure PowerShell module provides more command options, so you can pinpoint exactly what you want toosee or do.</span></span> <span data-ttu-id="ba92f-111">Olá portal do Azure fornece uma interface gráfica para muitas tarefas administrativas diárias de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba92f-111">hello Azure portal provides a GUI for many of hello everyday administrative tasks.</span></span>

<span data-ttu-id="ba92f-112">Aqui estão alguns exemplos que usam o módulo do PowerShell do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ba92f-112">Here are some examples that use hello Azure PowerShell module.</span></span>

* <span data-ttu-id="ba92f-113">**Obter todas as imagens**:`Get-AzureVMImage`retorna uma lista de todas as imagens de saudação disponíveis na sua assinatura atual: suas imagens e aquelas fornecidas pelo Azure ou parceiros.</span><span class="sxs-lookup"><span data-stu-id="ba92f-113">**Get all images**:`Get-AzureVMImage`returns a list of all hello images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="ba92f-114">lista de saudação resultante pode ser grande.</span><span class="sxs-lookup"><span data-stu-id="ba92f-114">hello resulting list could be large.</span></span> <span data-ttu-id="ba92f-115">Olá próximo exemplos mostram como tooget uma lista mais curta.</span><span class="sxs-lookup"><span data-stu-id="ba92f-115">hello next examples show how tooget a shorter list.</span></span>
* <span data-ttu-id="ba92f-116">**Obter as famílias de imagem**:`Get-AzureVMImage | select ImageFamily` obtém uma lista das famílias de imagem, mostrando as cadeias de caracteres da propriedade **ImageFamily**.</span><span class="sxs-lookup"><span data-stu-id="ba92f-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="ba92f-117">**Obtenha todas as imagens em uma família específica**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="ba92f-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="ba92f-118">**Localizar imagens da VM**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` esse cmdlet funciona por meio da propriedade de DataDiskConfiguration hello, que se aplica somente a imagens tooVM de filtragem.</span><span class="sxs-lookup"><span data-stu-id="ba92f-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering hello DataDiskConfiguration property, which only applies tooVM Images.</span></span> <span data-ttu-id="ba92f-119">Este exemplo também filtra Olá tooonly Olá rótulo e a imagem de nome de saída.</span><span class="sxs-lookup"><span data-stu-id="ba92f-119">This example also filters hello output tooonly hello label and image name.</span></span>
* <span data-ttu-id="ba92f-120">**Salvar uma imagem generalizada**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="ba92f-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="ba92f-121">**Salvar uma imagem especializada**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="ba92f-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="ba92f-122">parâmetro OSState de saudação é necessário toocreate uma imagem VM, que inclui o disco do sistema operacional hello e discos de dados conectados.</span><span class="sxs-lookup"><span data-stu-id="ba92f-122">hello OSState parameter is required toocreate a VM image, which includes hello operating system disk and attached data disks.</span></span> <span data-ttu-id="ba92f-123">Se você não usar o parâmetro hello, Olá cmdlet cria uma imagem do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="ba92f-123">If you don’t use hello parameter, hello cmdlet creates an OS image.</span></span> <span data-ttu-id="ba92f-124">valor Olá parâmetro hello indica se a imagem de saudação é generalizada ou especializada, baseado em se o disco do sistema operacional Olá foi preparado para reutilização.</span><span class="sxs-lookup"><span data-stu-id="ba92f-124">hello value of hello parameter indicates whether hello image is generalized or specialized, based on whether hello operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="ba92f-125">**Excluir uma imagem**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="ba92f-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba92f-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ba92f-126">Next Steps</span></span>
<span data-ttu-id="ba92f-127">Você também pode [criar uma máquina Windows usando o portal do Azure de saudação](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="ba92f-127">You can also [create a Windows machine using hello Azure portal](tutorial.md).</span></span>
