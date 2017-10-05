---
title: Carregar arquivo VHD no Azure DevTest Labs usando o PowerShell | Microsoft Docs
description: "Carregar arquivo VHD na conta de armazenamento do laboratório usando o PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 3c43ef77b8fa10cd6dbd726968264f32f7a3dd0f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-powershell"></a><span data-ttu-id="ca33c-103">Carregar arquivo VHD na conta de armazenamento do laboratório usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca33c-103">Upload VHD file to lab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="ca33c-104">No Azure DevTest Labs, os arquivos VHD podem ser usados para criar imagens personalizadas, que são usadas para provisionar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="ca33c-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="ca33c-105">As etapas a seguir mostrarão como usar o PowerShell para carregar um arquivo VHD em uma conta de armazenamento do laboratório.</span><span class="sxs-lookup"><span data-stu-id="ca33c-105">The following steps walk you through using PowerShell to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="ca33c-106">Depois de carregar seu arquivo VHD, a [seção Próximas etapas](#next-steps) lista alguns dos artigos que ilustram como criar uma imagem personalizada do arquivo VHD carregado.</span><span class="sxs-lookup"><span data-stu-id="ca33c-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="ca33c-107">Para saber mais sobre discos e VHDs no Azure, confira [Sobre discos e VHDs para máquinas virtuais](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="ca33c-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="ca33c-108">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="ca33c-108">Step-by-step instructions</span></span>

<span data-ttu-id="ca33c-109">As etapas a seguir mostram como carregar um arquivo VHD no Azure DevTest Labs usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca33c-109">The following steps walk you through uploading a VHD file to Azure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="ca33c-110">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ca33c-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="ca33c-111">Selecione **Mais serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="ca33c-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="ca33c-112">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="ca33c-112">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="ca33c-113">Na folha do laboratório, selecione **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="ca33c-113">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="ca33c-114">Na folha **Configuração** do laboratório, selecione **Imagens personalizadas (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="ca33c-114">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="ca33c-115">Na folha **Imagens personalizadas**, selecione **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ca33c-115">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="ca33c-116">Na folha **Imagem personalizada**, selecione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="ca33c-116">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="ca33c-117">Na folha **VHD**, selecione **Carregar um VHD usando o PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ca33c-117">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Carregar o VHD usando o PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="ca33c-119">Na folha **Carregar uma imagem usando o PowerShell**, copie o script do PowerShell gerado em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="ca33c-119">On the **Upload an image using PowerShell** blade, copy the generated PowerShell script to a text editor.</span></span>

1. <span data-ttu-id="ca33c-120">Modifique o parâmetro **LocalFilePath** do cmdlet **Add-AzureVhd** para apontar para o local do arquivo VHD que deseja carregar.</span><span class="sxs-lookup"><span data-stu-id="ca33c-120">Modify the **LocalFilePath** parameter of the **Add-AzureVhd** cmdlet to point to the location of the VHD file you want to upload.</span></span>

1. <span data-ttu-id="ca33c-121">Em um prompt do PowerShell, execute o cmdlet **Add-AzureVhd** (com o parâmetro **LocalFilePath** modificado).</span><span class="sxs-lookup"><span data-stu-id="ca33c-121">At a PowerShell prompt, run the **Add-AzureVhd** cmdlet (with the modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="ca33c-122">O processo de carregamento de um arquivo VHD pode ser demorado, dependendo do tamanho do arquivo VHD e da velocidade de conexão.</span><span class="sxs-lookup"><span data-stu-id="ca33c-122">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca33c-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca33c-123">Next steps</span></span>

- [<span data-ttu-id="ca33c-124">Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ca33c-124">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="ca33c-125">Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca33c-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
