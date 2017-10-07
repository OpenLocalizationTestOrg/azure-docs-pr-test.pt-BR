---
title: aaaCreate uma imagem do Azure RemoteApp com base em uma VM do Azure | Microsoft Docs
description: "Saiba como toocreate uma imagem do Azure RemoteApp, iniciando com uma máquina virtual do Azure."
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
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="c6e30-103">Criar uma imagem de RemoteApp do Azure com base em uma máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="c6e30-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c6e30-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="c6e30-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c6e30-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="c6e30-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c6e30-106">Você pode criar imagens do Azure RemoteApp (que contêm aplicativos Olá que compartilhar em sua coleção) de uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e30-106">You can create Azure RemoteApp images (which hold hello apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="c6e30-107">Você também pode escolher toouse uma imagem de máquina virtual, adicionamos toohello Galeria de imagens de VM do Azure que atenda a todos os requisitos de imagem do Azure RemoteApp Olá - você pode usar essa imagem VM como um ponto de partida para sua VM, se desejar.</span><span class="sxs-lookup"><span data-stu-id="c6e30-107">You could also choose toouse a virtual machine image we added toohello Azure VM image gallery that meets all hello Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="c6e30-108">Basta procure imagem de "Windows Server Desktop Host da sessão remota" hello na biblioteca de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6e30-108">Just look for hello "Windows Server Remote Desktop Session Host" image in hello library.</span></span>

<span data-ttu-id="c6e30-109">Há dois toocreate etapas sua própria imagem com base em uma VM do Azure - criar imagem hello e, em seguida, carregá-lo do tooAzure de biblioteca Olá VM do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c6e30-109">There are two steps toocreate your own image based on an Azure VM - create hello image and then upload it from hello Azure VM library tooAzure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="c6e30-110">Criar uma imagem personalizada com base em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="c6e30-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="c6e30-111">Use essas etapas toocreate uma imagem com base em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e30-111">Use these steps toocreate an image based on an Azure VM.</span></span>

1. <span data-ttu-id="c6e30-112">Crie uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e30-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="c6e30-113">Você pode usar o hello "Windows Server Desktop Host da sessão remota" ou imagem "Windows Server Remote Desktop sessão Host com o Microsoft Office 365 ProPlus" hello na Galeria de imagens de máquina virtual do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c6e30-113">You can use hello "Windows Server Remote Desktop Session Host" or hello "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from hello Azure virtual machine image gallery.</span></span> <span data-ttu-id="c6e30-114">Esta imagem atende a todos os requisitos de imagem de modelo para RemoteApp do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c6e30-114">This image meets all hello Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="c6e30-115">Para obter detalhes, consulte [Criar uma VM que executa o Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6e30-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="c6e30-116">Conectar toohello VM e instalar e configurar aplicativos Olá que você deseja tooshare por meio do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c6e30-116">Connect toohello VM and install and configure hello apps that you want tooshare through RemoteApp.</span></span> <span data-ttu-id="c6e30-117">Verifique se tooperform quaisquer configurações adicionais do Windows necessárias para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c6e30-117">Make sure tooperform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="c6e30-118">Para obter detalhes, consulte [como tooLog no tooa Máquina Virtual executando o Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6e30-118">For details, see [How tooLog on tooa Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="c6e30-119">Se você estiver usando uma das imagens do Host de sessão de área de trabalho remota do Windows Server hello, há um script de validação incluído que garantirá a que sua VM atende Olá RemoteApp pre-reqs.</span><span class="sxs-lookup"><span data-stu-id="c6e30-119">If you are using one of hello Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets hello RemoteApp pre-reqs.</span></span> <span data-ttu-id="c6e30-120">script de toorun, clique duas vezes em **ValidateRemoteAppImage** na área de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6e30-120">toorun script, double-click **ValidateRemoteAppImage** on hello desktop.</span></span> <span data-ttu-id="c6e30-121">Certifique-se de que todos os erros relatados pelo script hello são corrigidos antes da próxima etapa de toohello de continuar.</span><span class="sxs-lookup"><span data-stu-id="c6e30-121">Ensure that all errors reported by hello script are fixed before proceeding toohello next step.</span></span>
4. <span data-ttu-id="c6e30-122">SYSPREP generalize e capture a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6e30-122">SYSPREP generalize and capture hello image.</span></span> <span data-ttu-id="c6e30-123">Consulte [como tooCapture tooUse uma máquina Virtual do Windows como um modelo](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="c6e30-123">See [How tooCapture a Windows Virtual Machine tooUse as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a><span data-ttu-id="c6e30-124">Importar imagem Olá para biblioteca de imagens do Azure RemoteApp Olá</span><span class="sxs-lookup"><span data-stu-id="c6e30-124">Import hello image into hello Azure RemoteApp image library</span></span>
<span data-ttu-id="c6e30-125">Use a nova imagem essas etapas tooimport Olá no Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="c6e30-125">Use these steps tooimport hello new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="c6e30-126">Em Olá **imagens de modelo** guia:</span><span class="sxs-lookup"><span data-stu-id="c6e30-126">In hello **Template Images** tab:</span></span>
   
   * <span data-ttu-id="c6e30-127">Se você não tiver nenhuma imagem existente, clique em **Carregar ou Importar uma Imagem de Modelo**.</span><span class="sxs-lookup"><span data-stu-id="c6e30-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="c6e30-128">Se você já tem pelo menos uma imagem, clique em  **+**  tooadd uma nova imagem.</span><span class="sxs-lookup"><span data-stu-id="c6e30-128">If you have at least one image already, click **+** tooadd a new image.</span></span>
2. <span data-ttu-id="c6e30-129">Selecione a biblioteca **Importar uma imagem de suas Máquinas Virtuais** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c6e30-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="c6e30-130">Na página seguinte do hello, selecione sua imagem personalizada da lista de saudação e confirme se você seguiu as etapas de saudação listadas quando você criou sua imagem.</span><span class="sxs-lookup"><span data-stu-id="c6e30-130">On hello next page, select your custom image from hello list and confirm that you followed hello steps listed when you created your image.</span></span> <span data-ttu-id="c6e30-131">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c6e30-131">Click **Next**.</span></span>
4. <span data-ttu-id="c6e30-132">Insira um nome para a nova imagem do RemoteApp hello, escolha Olá local e clique em processo de importação do hello marca de seleção toostart hello.</span><span class="sxs-lookup"><span data-stu-id="c6e30-132">Enter a name for hello new RemoteApp image and pick hello location, then click hello checkmark toostart hello import process.</span></span>

> [!NOTE]
> <span data-ttu-id="c6e30-133">Você pode importar imagens de qualquer local do Azure tem suportada por máquinas virtuais do Azure tooany local do Azure com suporte pelo Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c6e30-133">You can import images from any Azure location supported by Azure Virtual Machines tooany Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="c6e30-134">Dependendo de locais de saudação importação Olá pode demorar até too25 minutos.</span><span class="sxs-lookup"><span data-stu-id="c6e30-134">Depending on hello locations hello import can take up too25 minutes.</span></span>
> 
> 

<span data-ttu-id="c6e30-135">Agora você está pronto toocreate sua nova coleção, ou um [nuvem](remoteapp-create-cloud-deployment.md) coleção ou [híbrida](remoteapp-create-hybrid-deployment.md), dependendo de suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="c6e30-135">Now you are ready toocreate your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

