---
title: "AAA\"carregar arquivos em uma conta de serviços de mídia usando Olá portal do Azure | Microsoft Docs\""
description: "Este tutorial orienta você pelas etapas de saudação de carregar arquivos em uma conta de serviços de mídia usando Olá portal do Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="5fd8b-103">Carregar arquivos em uma conta de serviços de mídia usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5fd8b-103">Upload files into a Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5fd8b-104">Portal</span><span class="sxs-lookup"><span data-stu-id="5fd8b-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="5fd8b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5fd8b-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="5fd8b-106">REST</span><span class="sxs-lookup"><span data-stu-id="5fd8b-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="5fd8b-107">toocomplete neste tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="5fd8b-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fd8b-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="5fd8b-109">Nos serviços de mídia, você pode carregar seus arquivos digitais em um ativo.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="5fd8b-110">Olá ativo pode conter vídeo, áudio, imagens, coleções de miniaturas, texto rastreia e legenda codificada arquivos (e Olá metadados sobre esses arquivos.) Depois que forem carregados arquivos hello, seu conteúdo é armazenado com segurança na nuvem de saudação para processamento adicional e streaming.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="5fd8b-111">Carregar arquivos</span><span class="sxs-lookup"><span data-stu-id="5fd8b-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="5fd8b-112">Há um limite toohello tamanho máximo com suporte para o processamento de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-112">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="5fd8b-113">Consulte [isso](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre a limitação de tamanho de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

1. <span data-ttu-id="5fd8b-114">Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="5fd8b-115">Em Olá **configurações** folha, clique em **ativos**.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-115">On hello **Settings** blade, click **Assets**.</span></span>
   
    ![Carregar arquivos](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="5fd8b-117">Clique em Olá **carregar** botão.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-117">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="5fd8b-118">Olá **carregar um ativo de vídeo** janela é exibida.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-118">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5fd8b-119">Não há nenhuma limitação de tamanho do arquivo.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="5fd8b-120">Procurar vídeo toohello desejado no seu computador, selecioná-la e Okey de ocorrências.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-120">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="5fd8b-121">Olá upload é iniciado e você pode ver o progresso de saudação em nome do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-121">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="5fd8b-122">Após a conclusão do carregamento de Olá, você verá o novo ativo de saudação listado no hello **ativos** janela.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-122">Once hello upload completes, you will see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5fd8b-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5fd8b-123">Next steps</span></span>
<span data-ttu-id="5fd8b-124">Agora você pode codificar seus ativos carregados.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="5fd8b-125">Para saber mais, veja [Codificar ativos](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="5fd8b-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="5fd8b-126">Você também pode usar as funções do Azure tootrigger um trabalho de codificação com base em um arquivo que chegam no contêiner de saudação configurada.</span><span class="sxs-lookup"><span data-stu-id="5fd8b-126">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="5fd8b-127">Para obter mais informações, confira [este exemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="5fd8b-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="5fd8b-128">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="5fd8b-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5fd8b-129">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="5fd8b-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

