---
title: Criar uma imagem do Azure RemoteApp baseada em uma VM do Azure | Microsoft Docs
description: "Saiba como criar uma imagem para o RemoteApp do Azure começando com uma máquina virtual do Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ee64b86835af8e6237cddcd8acc779fc6dac8214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="507c5-103">Criar uma imagem de RemoteApp do Azure com base em uma máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="507c5-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="507c5-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="507c5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="507c5-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="507c5-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="507c5-106">Você pode criar imagens do RemoteApp do Azure (que contêm os aplicativos que você compartilha em sua coleção) de uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="507c5-106">You can create Azure RemoteApp images (which hold the apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="507c5-107">Você também pode optar por usar uma máquina virtual que adicionamos à galeria de imagens de VM do Azure que atende a todos os requisitos de imagem de RemoteApp do Azure - você pode usar essa imagem de VM como ponto de partida para a sua própria VM, se desejar.</span><span class="sxs-lookup"><span data-stu-id="507c5-107">You could also choose to use a virtual machine image we added to the Azure VM image gallery that meets all the Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="507c5-108">Basta procurar a imagem "Host da Sessão da Área de Trabalho Remota do Windows Server" na biblioteca.</span><span class="sxs-lookup"><span data-stu-id="507c5-108">Just look for the "Windows Server Remote Desktop Session Host" image in the library.</span></span>

<span data-ttu-id="507c5-109">Há duas etapas para criar sua própria imagem com base em uma VM do Azure: criar a imagem e, em seguida, carregá-la da biblioteca de VM do Azure para o RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="507c5-109">There are two steps to create your own image based on an Azure VM - create the image and then upload it from the Azure VM library to Azure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="507c5-110">Criar uma imagem personalizada com base em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="507c5-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="507c5-111">Use estas etapas para criar uma imagem com base em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="507c5-111">Use these steps to create an image based on an Azure VM.</span></span>

1. <span data-ttu-id="507c5-112">Crie uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="507c5-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="507c5-113">Você pode usar a imagem do “Host da Sessão da Área de Trabalho Remota do Windows Server” ou “Host da Sessão da Área de Trabalho Remota do Windows Server com o Microsoft Office 365 ProPlus” da galeria de imagens de máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="507c5-113">You can use the "Windows Server Remote Desktop Session Host" or the "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from the Azure virtual machine image gallery.</span></span> <span data-ttu-id="507c5-114">Essa imagem atende a todos os requisitos de imagem de modelo do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="507c5-114">This image meets all the Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="507c5-115">Para obter detalhes, consulte [Criar uma VM que executa o Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="507c5-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="507c5-116">Conecte-se à VM e instale e configure os aplicativos que deseja compartilhar por meio do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="507c5-116">Connect to the VM and install and configure the apps that you want to share through RemoteApp.</span></span> <span data-ttu-id="507c5-117">Certifique-se de executar quaisquer configurações adicionais do Windows necessárias para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="507c5-117">Make sure to perform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="507c5-118">Para mais detalhes, consulte [Como fazer logon em uma máquina virtual executando o Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="507c5-118">For details, see [How to Log on to a Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="507c5-119">Se estiver usando uma das imagens do Host da Sessão da Área de Trabalho Remota do Windows Server, haverá um script de validação incluído que garantirá que a sua VM atenda aos pré-requisitos do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="507c5-119">If you are using one of the Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets the RemoteApp pre-reqs.</span></span> <span data-ttu-id="507c5-120">Para executar o script, clique duas vezes em **ValidateRemoteAppImage** na área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="507c5-120">To run script, double-click **ValidateRemoteAppImage** on the desktop.</span></span> <span data-ttu-id="507c5-121">Certifique-se de que todos os erros relatados pelo script sejam corrigidos antes de prosseguir para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="507c5-121">Ensure that all errors reported by the script are fixed before proceeding to the next step.</span></span>
4. <span data-ttu-id="507c5-122">O SYSPREP generaliza e captura a imagem.</span><span class="sxs-lookup"><span data-stu-id="507c5-122">SYSPREP generalize and capture the image.</span></span> <span data-ttu-id="507c5-123">Consulte [Como capturar uma máquina virtual do Windows para usar como modelo](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="507c5-123">See [How to Capture a Windows Virtual Machine to Use as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-the-image-into-the-azure-remoteapp-image-library"></a><span data-ttu-id="507c5-124">Importar a imagem para a biblioteca de imagens do RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="507c5-124">Import the image into the Azure RemoteApp image library</span></span>
<span data-ttu-id="507c5-125">Use estas etapas para importar a nova imagem para o RemoteApp do Azure:</span><span class="sxs-lookup"><span data-stu-id="507c5-125">Use these steps to import the new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="507c5-126">Na guia **Imagens de modelo** :</span><span class="sxs-lookup"><span data-stu-id="507c5-126">In the **Template Images** tab:</span></span>
   
   * <span data-ttu-id="507c5-127">Se você não tiver nenhuma imagem existente, clique em **Carregar ou Importar uma Imagem de Modelo**.</span><span class="sxs-lookup"><span data-stu-id="507c5-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="507c5-128">Se você já tiver pelo menos uma imagem, clique em **+** para adicionar uma nova imagem.</span><span class="sxs-lookup"><span data-stu-id="507c5-128">If you have at least one image already, click **+** to add a new image.</span></span>
2. <span data-ttu-id="507c5-129">Selecione a biblioteca **Importar uma imagem de suas Máquinas Virtuais** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="507c5-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="507c5-130">Na próxima página, selecione a imagem personalizada na lista e verifique se você seguiu as etapas listadas ao criar a imagem.</span><span class="sxs-lookup"><span data-stu-id="507c5-130">On the next page, select your custom image from the list and confirm that you followed the steps listed when you created your image.</span></span> <span data-ttu-id="507c5-131">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="507c5-131">Click **Next**.</span></span>
4. <span data-ttu-id="507c5-132">Insira um nome para a nova imagem do RemoteApp, selecione o local e clique na marca de seleção para iniciar o processo de importação.</span><span class="sxs-lookup"><span data-stu-id="507c5-132">Enter a name for the new RemoteApp image and pick the location, then click the checkmark to start the import process.</span></span>

> [!NOTE]
> <span data-ttu-id="507c5-133">Você pode importar imagens de qualquer local do Azure com suporte nas Máquinas Virtuais do Azure para qualquer local do Azure que tenha suporte no Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="507c5-133">You can import images from any Azure location supported by Azure Virtual Machines to any Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="507c5-134">Dependendo dos locais, a importação pode levar até 25 minutos.</span><span class="sxs-lookup"><span data-stu-id="507c5-134">Depending on the locations the import can take up to 25 minutes.</span></span>
> 
> 

<span data-ttu-id="507c5-135">Agora você está pronto para criar a nova coleção, uma coleção na [nuvem](remoteapp-create-cloud-deployment.md) ou [híbrida](remoteapp-create-hybrid-deployment.md), dependendo de suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="507c5-135">Now you are ready to create your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

