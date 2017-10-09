---
title: aaaUpload VHD arquivo tooAzure DevTest Labs usando AzCopy | Microsoft Docs
description: Carregar conta de armazenamento do toolab do arquivo VHD usando AzCopy
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
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a><span data-ttu-id="c5c32-103">Carregar conta de armazenamento do toolab do arquivo VHD usando AzCopy</span><span class="sxs-lookup"><span data-stu-id="c5c32-103">Upload VHD file toolab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="c5c32-104">No Azure DevTest Labs, arquivos VHD podem ser imagens personalizadas usadas toocreate, que são máquinas virtuais de tooprovision usado.</span><span class="sxs-lookup"><span data-stu-id="c5c32-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="c5c32-105">Olá etapas a seguir orientam usando tooupload de utilitário de linha de comando AzCopy Olá conta de armazenamento de um VHD arquivo tooa lab.</span><span class="sxs-lookup"><span data-stu-id="c5c32-105">hello following steps walk you through using hello AzCopy command-line utility tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="c5c32-106">Depois de carregar seu arquivo VHD, Olá [próximas etapas seção](#next-steps) lista alguns artigos que ilustram como toocreate uma imagem personalizada do hello carregado o arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="c5c32-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="c5c32-107">Para saber mais sobre discos e VHDs no Azure, confira [Sobre discos e VHDs para máquinas virtuais](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="c5c32-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="c5c32-108">O AzCopy é um utilitário de linha de comando somente para Windows.</span><span class="sxs-lookup"><span data-stu-id="c5c32-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="c5c32-109">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="c5c32-109">Step-by-step instructions</span></span>

<span data-ttu-id="c5c32-110">Olá seguindo as etapas da extensão de arquivo por meio de carregar um VHD tooAzure DevTest Labs usando [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="c5c32-110">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="c5c32-111">Obter nome de saudação do laboratório de saudação conta de armazenamento usando Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="c5c32-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

1. <span data-ttu-id="c5c32-112">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c5c32-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="c5c32-113">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5c32-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="c5c32-114">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="c5c32-114">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="c5c32-115">Na folha do laboratório hello, selecione **configuração**.</span><span class="sxs-lookup"><span data-stu-id="c5c32-115">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="c5c32-116">Laboratório Olá **configuração** folha, selecione **imagens personalizadas (VHDs)**.</span><span class="sxs-lookup"><span data-stu-id="c5c32-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="c5c32-117">Em Olá **imagens personalizadas** folha, selecione **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c5c32-117">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="c5c32-118">Em Olá **imagem personalizada** folha, selecione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="c5c32-118">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="c5c32-119">Em Olá **VHD** folha, selecione **carregar um VHD usando o PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c5c32-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Carregar o VHD usando o PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="c5c32-121">Olá **carregue uma imagem usando o PowerShell** folha exibe uma chamada toohello **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c5c32-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="c5c32-122">Olá primeiro parâmetro (*destino*) contém Olá URI para um contêiner de blob (*carrega*) em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5c32-122">hello first parameter (*Destination*) contains hello URI for a blob container (*uploads*) in hello following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="c5c32-123">Anote Olá completo URI como ele é usado em etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="c5c32-123">Make note of hello full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="c5c32-124">Carregar arquivo VHD hello usando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="c5c32-124">Upload hello VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="c5c32-125">[Baixe e instale a versão mais recente de saudação do AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="c5c32-125">[Download and install hello latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="c5c32-126">Abra uma janela de comando e navegue diretório de instalação do toohello AzCopy.</span><span class="sxs-lookup"><span data-stu-id="c5c32-126">Open a command window and navigate toohello AzCopy installation directory.</span></span> <span data-ttu-id="c5c32-127">Opcionalmente, você pode adicionar o caminho de sistema de tooyour Olá AzCopy instalação local.</span><span class="sxs-lookup"><span data-stu-id="c5c32-127">Optionally, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="c5c32-128">Por padrão, AzCopy é instalado toohello diretório a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5c32-128">By default, AzCopy is installed toohello following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="c5c32-129">Usando Olá armazenamento conta chave e blob URI do contêiner, execute Olá comando no prompt de comando Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="c5c32-129">Using hello storage account key and blob container URI, run hello following command at hello command prompt.</span></span> <span data-ttu-id="c5c32-130">Olá *vhdFileName* valor precisa toobe entre aspas.</span><span class="sxs-lookup"><span data-stu-id="c5c32-130">hello *vhdFileName* value needs toobe in quotes.</span></span> <span data-ttu-id="c5c32-131">processo de saudação de carregamento de um arquivo VHD pode ser demorado, dependendo do tamanho de saudação do arquivo VHD hello e a velocidade de conexão.</span><span class="sxs-lookup"><span data-stu-id="c5c32-131">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="c5c32-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c5c32-132">Next steps</span></span>

- [<span data-ttu-id="c5c32-133">Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c5c32-133">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="c5c32-134">Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5c32-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)