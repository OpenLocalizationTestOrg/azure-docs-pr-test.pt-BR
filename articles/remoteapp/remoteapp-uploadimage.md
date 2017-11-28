---
title: aaaUpload uma imagem personalizada do Azure RemoteApp | Microsoft Docs
description: Saiba como tooupload um personalizado da imagem do Azure RemoteApp
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="a503a-103">Carregar uma imagem personalizada para o RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="a503a-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a503a-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="a503a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a503a-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a503a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a503a-106">Agora que você criou sua imagem de modelo personalizado ou atualizá-lo com as alterações, é necessário tooupload essa biblioteca de imagens do Azure RemoteApp imagem tooyour.</span><span class="sxs-lookup"><span data-stu-id="a503a-106">Now that you have created your custom template image or have updated it with changes, you need tooupload that image tooyour Azure RemoteApp image library.</span></span> <span data-ttu-id="a503a-107">Siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="a503a-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="a503a-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a503a-108">Before you start</span></span>
1. <span data-ttu-id="a503a-109">Verifique se atende a sua imagem personalizada Olá [requisitos da imagem](remoteapp-imagereqs.md) e [requisitos do aplicativo](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="a503a-109">Verify your custom image meets hello [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="a503a-110">Instalar Olá [módulo Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a503a-110">Install hello [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-tooupload-custom-image"></a><span data-ttu-id="a503a-111">Passo a passo sobre como imagem personalizada tooupload</span><span class="sxs-lookup"><span data-stu-id="a503a-111">Step by step on how tooupload custom image</span></span>
1. <span data-ttu-id="a503a-112">Abra o Portal de gerenciamento e navegue toohello RemoteApp página.</span><span class="sxs-lookup"><span data-stu-id="a503a-112">Open Azure Management Portal and navigate toohello RemoteApp page.</span></span>
2. <span data-ttu-id="a503a-113">Em Olá **imagens de modelo** , clique em **carregar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="a503a-113">On hello **Template images** tab, click **Upload** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="a503a-114">Insira um nome amigável para a imagem e especifique o local de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="a503a-114">Enter a friendly name for your image and specify hello storage account location.</span></span> <span data-ttu-id="a503a-115">Certifique-se de local de saudação é hello mesmo local que sua coleção do RemoteApp ou em um local onde você deseja toocreate um.</span><span class="sxs-lookup"><span data-stu-id="a503a-115">Ensure hello location is hello same location as your RemoteApp collection or a location where you want toocreate one.</span></span>
4. <span data-ttu-id="a503a-116">Quando solicitado, faça o download do hello script tooyour PC local.</span><span class="sxs-lookup"><span data-stu-id="a503a-116">When prompted, download hello script tooyour local PC.</span></span>
5. <span data-ttu-id="a503a-117">Copie parâmetros de comando Olá na área de transferência tooyour caixa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="a503a-117">Copy hello command parameters in hello text box tooyour clipboard.</span></span>
6. <span data-ttu-id="a503a-118">Abra uma janela elevada do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a503a-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="a503a-119">De saudação elevados janela Windows PowerShell, navegar toohello mesmo diretório onde você baixou o script hello.</span><span class="sxs-lookup"><span data-stu-id="a503a-119">From hello elevated Windows PowerShell window, navigate toohello same directory where you downloaded hello script.</span></span>
8. <span data-ttu-id="a503a-120">Saudação de colar copiados comando e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a503a-120">Paste hello copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="a503a-121">processo de carregamento de saudação será iniciado e duração pode depender de vários fatores, inclusive sua velocidade de rede e o tamanho da imagem de saudação</span><span class="sxs-lookup"><span data-stu-id="a503a-121">hello upload process will begin and duration may depend on many factors including your network speed and size of hello image</span></span>
9. <span data-ttu-id="a503a-122">Se o carregamento não for bem-sucedida devido a interrupções de rede ou coisas como essa, você sempre pode retomar o processo de carregamento de saudação que você começou.</span><span class="sxs-lookup"><span data-stu-id="a503a-122">If your upload does not succeed because of network interruption or things like that, you can always resume hello upload process you began.</span></span> <span data-ttu-id="a503a-123">Olá tooresume um upload, execute o script hello novamente usando a mesma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="a503a-123">tooresume an upload, run hello script again using hello same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="a503a-124">Nunca modifique o script de carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a503a-124">Never modify hello upload script.</span></span> <span data-ttu-id="a503a-125">Verificações de tem sido implementado tooensure que Olá Olá imagem atende aos requisitos de imagem e requisitos de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a503a-125">Specific checks have been implemented tooensure that hello image meets hello image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="a503a-126">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="a503a-126">Common problems</span></span>
* <span data-ttu-id="a503a-127">Certifique-se de usar o Windows PowerShell, não o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="a503a-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="a503a-128">Você precisa módulo de PowerShell do Azure Olá tooinstall porque determinados módulos são necessários durante o processo de carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a503a-128">You need tooinstall hello Azure PowerShell module because certain modules are needed during hello upload process.</span></span>
* <span data-ttu-id="a503a-129">Nunca alterar script Olá, validações existem para sua conveniência.</span><span class="sxs-lookup"><span data-stu-id="a503a-129">Never alter hello script, validations are there for your convenience.</span></span>
* <span data-ttu-id="a503a-130">Se o arquivo de vhd Olá fica bloqueado durante o carregamento, copie o arquivo hello ou movê-la tooa novo local e tente carregar novamente.</span><span class="sxs-lookup"><span data-stu-id="a503a-130">If hello vhd file gets locked out during upload, copy hello file or move it tooa new location and attempt upload again.</span></span> <span data-ttu-id="a503a-131">Pode haver algum processo do Windows impedindo o carregamento.</span><span class="sxs-lookup"><span data-stu-id="a503a-131">There might be some Windows process that is preventing upload.</span></span>  

