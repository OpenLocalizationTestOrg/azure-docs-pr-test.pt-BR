---
title: requisitos de imagem do RemoteApp aaaAzure | Microsoft Docs
description: "Saiba mais sobre os requisitos de saudação para a criação de imagens toobe usado com o Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="a9b0e-103">Requisitos para as imagens do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="a9b0e-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a9b0e-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a9b0e-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a9b0e-106">O Azure RemoteApp usa um toohost de imagem do Windows Server 2012 R2 todos os programas de saudação que você deseja tooshare com seus usuários.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-106">Azure RemoteApp uses a Windows Server 2012 R2 image toohost all hello programs that you want tooshare with your users.</span></span> <span data-ttu-id="a9b0e-107">toocreate uma imagem personalizada, você pode iniciar com uma imagem existente ou [criar um novo](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="a9b0e-107">toocreate a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="a9b0e-108">Você sabia que o oferece de assinatura do Azure RemoteApp que acesso imagem do Windows Server 2012 R2 tooa no hello Galeria de VMs do Azure que você pode usar toocreate sua própria imagem de modelo?</span><span class="sxs-lookup"><span data-stu-id="a9b0e-108">Did you know that your Azure RemoteApp subscription gives you access tooa Windows Server 2012 R2 image in hello Azure VM gallery that you can use toocreate your own template image?</span></span> <span data-ttu-id="a9b0e-109">[Confira](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="a9b0e-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="a9b0e-110">requisitos de saudação de imagem Olá que podem ser carregados para uso com o Azure RemoteApp são:</span><span class="sxs-lookup"><span data-stu-id="a9b0e-110">hello requirements for hello image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="a9b0e-111">Aplicativos personalizados não armazenam dados localmente na imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-111">Custom applications don’t store data locally on hello image.</span></span> <span data-ttu-id="a9b0e-112">Essas imagens são sem monitoração de estado e devem conter apenas aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="a9b0e-113">Olá imagem não contém dados que podem ser perdidos.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-113">hello image does not contain data that can be lost.</span></span>
* <span data-ttu-id="a9b0e-114">tamanho da imagem Olá deve ser um múltiplo de MBs.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-114">hello image size should be a multiple of MBs.</span></span> <span data-ttu-id="a9b0e-115">Se você tentar tooupload uma imagem que não é um múltiplo exato, carregamento Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-115">If you try tooupload an image that is not an exact multiple, hello upload will fail.</span></span>
* <span data-ttu-id="a9b0e-116">tamanho da imagem Olá deve ser 127 GB ou menores.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-116">hello image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="a9b0e-117">Deve estar em um arquivo VHD (arquivos VHDX atualmente não têm suporte).</span><span class="sxs-lookup"><span data-stu-id="a9b0e-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="a9b0e-118">Olá VHD não deve ser uma máquina virtual de geração 2.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-118">hello VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="a9b0e-119">Olá VHD pode ser um tamanho fixo ou expansão dinâmica.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-119">hello VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="a9b0e-120">Um VHD de expansão dinâmica é recomendado porque ela usa menos tooAzure tooupload de tempo que um arquivo VHD de tamanho fixo.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-120">A dynamically expanding VHD is recommended because it takes less time tooupload tooAzure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="a9b0e-121">disco Olá deve ser inicializado usando o estilo de particionamento Olá registro mestre de inicialização (MBR).</span><span class="sxs-lookup"><span data-stu-id="a9b0e-121">hello disk must be initialized using hello Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="a9b0e-122">Não há suporte para a saudação estilo de partição GUID partição GPT (tabela).</span><span class="sxs-lookup"><span data-stu-id="a9b0e-122">hello GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="a9b0e-123">Olá VHD deve conter uma única instalação do Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-123">hello VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="a9b0e-124">Ele deve conter vários volumes, mas apenas um que contenha uma instalação do Windows.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="a9b0e-125">função de Host de sessão de área de trabalho remota (RDSH) Hello e o recurso Experiência Desktop de saudação devem ser instalados.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-125">hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="a9b0e-126">função de agente de Conexão de área de trabalho remota Olá deve *não* ser instalado.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-126">hello Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="a9b0e-127">Olá Encrypting File System (EFS) deve ser desabilitada.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-127">hello Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="a9b0e-128">Olá imagem deve ser submetida a Sysprep usando parâmetros de saudação **/oobe /generalize /shutdown** (não use Olá **/Mode: VM** parâmetro).</span><span class="sxs-lookup"><span data-stu-id="a9b0e-128">hello image must be SYSPREPed using hello parameters **/oobe /generalize /shutdown** (DO NOT use hello **/mode:vm** parameter).</span></span>
* <span data-ttu-id="a9b0e-129">Não há suporte para carregar o VHD de uma cadeia de instantâneo.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="a9b0e-130">Consulte [Criar uma imagem do RemoteApp do Azure](remoteapp-imageoptions.md) para obter mais informações sobre a criação de imagens para o RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9b0e-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

