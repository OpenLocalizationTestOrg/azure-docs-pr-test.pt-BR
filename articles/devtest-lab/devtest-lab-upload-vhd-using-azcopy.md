---
title: Carregar arquivo VHD no Azure DevTest Labs usando o AzCopy | Microsoft Docs
description: "Carregar arquivo VHD na conta de armazenamento do laboratório usando o AzCopy"
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
ms.openlocfilehash: a4f43354740d9f17570932b0b9c753f46d67dc33
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-azcopy"></a><span data-ttu-id="5cf8c-103">Carregar arquivo VHD na conta de armazenamento do laboratório usando o AzCopy</span><span class="sxs-lookup"><span data-stu-id="5cf8c-103">Upload VHD file to lab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="5cf8c-104">No Azure DevTest Labs, os arquivos VHD podem ser usados para criar imagens personalizadas, que são usadas para provisionar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="5cf8c-105">As etapas a seguir mostrarão como usar o utilitário de linha de comando AzCopy para carregar um arquivo VHD em uma conta de armazenamento do laboratório.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-105">The following steps walk you through using the AzCopy command-line utility to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="5cf8c-106">Depois de carregar seu arquivo VHD, a [seção Próximas etapas](#next-steps) lista alguns dos artigos que ilustram como criar uma imagem personalizada do arquivo VHD carregado.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="5cf8c-107">Para saber mais sobre discos e VHDs no Azure, confira [Sobre discos e VHDs para máquinas virtuais](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="5cf8c-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="5cf8c-108">O AzCopy é um utilitário de linha de comando somente para Windows.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="5cf8c-109">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="5cf8c-109">Step-by-step instructions</span></span>

<span data-ttu-id="5cf8c-110">As etapas a seguir mostram como carregar um arquivo VHD no Azure DevTest Labs usando o [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="5cf8c-110">The following steps walk you through uploading a VHD file to Azure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="5cf8c-111">Obtenha o nome da conta de armazenamento do laboratório usando o Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="5cf8c-111">Get the name of the lab's storage account using the Azure portal:</span></span>

1. <span data-ttu-id="5cf8c-112">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="5cf8c-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="5cf8c-113">Selecione **Mais serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="5cf8c-114">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-114">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="5cf8c-115">Na folha do laboratório, selecione **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-115">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="5cf8c-116">Na folha **Configuração** do laboratório, selecione **Imagens personalizadas (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="5cf8c-117">Na folha **Imagens personalizadas**, selecione **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-117">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="5cf8c-118">Na folha **Imagem personalizada**, selecione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-118">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="5cf8c-119">Na folha **VHD**, selecione **Carregar um VHD usando o PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Carregar o VHD usando o PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="5cf8c-121">A folha **Carregar uma imagem usando o PowerShell** exibe uma chamada ao cmdlet **Add-AzureVhd**.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="5cf8c-122">O primeiro parâmetro (*Destino*) contém o URI do contêiner de blob (*carregamentos*) no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="5cf8c-122">The first parameter (*Destination*) contains the URI for a blob container (*uploads*) in the following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="5cf8c-123">Anote o URI completo, pois ele será usado em etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-123">Make note of the full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="5cf8c-124">Carregar o arquivo VHD usando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="5cf8c-124">Upload the VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="5cf8c-125">[Baixe e instale a versão mais recente do AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="5cf8c-125">[Download and install the latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="5cf8c-126">Abra uma janela de comando e navegue até o diretório de instalação do AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-126">Open a command window and navigate to the AzCopy installation directory.</span></span> <span data-ttu-id="5cf8c-127">Se quiser, você pode alterar o local da instalação do AzCopy para o caminho do sistema.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-127">Optionally, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="5cf8c-128">Por padrão, o AzCopy é instalado no seguinte diretório:</span><span class="sxs-lookup"><span data-stu-id="5cf8c-128">By default, AzCopy is installed to the following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="5cf8c-129">Usando a chave da conta de armazenamento e o URI do contêiner de blob, execute o seguinte comando no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-129">Using the storage account key and blob container URI, run the following command at the command prompt.</span></span> <span data-ttu-id="5cf8c-130">O valor *vhdFileName* precisa estar entre aspas.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-130">The *vhdFileName* value needs to be in quotes.</span></span> <span data-ttu-id="5cf8c-131">O processo de carregamento de um arquivo VHD pode ser demorado, dependendo do tamanho do arquivo VHD e da velocidade de conexão.</span><span class="sxs-lookup"><span data-stu-id="5cf8c-131">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="5cf8c-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5cf8c-132">Next steps</span></span>

- [<span data-ttu-id="5cf8c-133">Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5cf8c-133">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="5cf8c-134">Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5cf8c-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)