---
title: "arquivos de aaaUpload em uma conta de serviços de mídia do Azure do Azure StorSimple | Microsoft Docs"
description: "Este artigo fornece uma breve visão geral do Gerenciador de Dados do Azure StorSimple. artigo Olá também vincula tootutorials que mostram como dados de tooextract do StorSimple e carregá-lo como ativos tooan conta de serviços de mídia do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="e9475-104">Carregar arquivos em uma conta dos Serviços de Mídia do Azure do Azure StorSimple</span><span class="sxs-lookup"><span data-stu-id="e9475-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="e9475-105">Este artigo fornece uma breve visão geral do Gerenciador de Dados do Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e9475-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="e9475-106">artigo Olá também vincula tootutorials que mostram como dados de tooextract do StorSimple e carregar esses dados como ativos tooan conta de serviços de mídia do Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="e9475-106">hello article also links tootutorials that show you how tooextract data from StorSimple and upload this data as assets tooan Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="e9475-107">O Gerenciador de Dados do Azure StorSimple está em visualização privada.</span><span class="sxs-lookup"><span data-stu-id="e9475-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="e9475-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e9475-108">Overview</span></span>

<span data-ttu-id="e9475-109">Nos serviços de mídia, você pode carregar seus arquivos digitais em um ativo.</span><span class="sxs-lookup"><span data-stu-id="e9475-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="e9475-110">Olá ativo pode conter vídeo, áudio, imagens, coleções de miniaturas, texto rastreia e legenda codificada arquivos (e Olá metadados sobre esses arquivos.) Depois que forem carregados arquivos hello, seu conteúdo é armazenado com segurança na nuvem de saudação para processamento adicional e streaming.</span><span class="sxs-lookup"><span data-stu-id="e9475-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="e9475-111">[O Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) usa armazenamento em nuvem como uma extensão da saudação solução local e automaticamente dados de camadas de armazenamento de local de saudação e armazenamento em nuvem.</span><span class="sxs-lookup"><span data-stu-id="e9475-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="e9475-112">o dispositivo StorSimple Olá dedupes e compacta os dados antes de enviá-la nuvem toohello tornando muito eficiente para o envio de nuvem de toohello arquivos grandes.</span><span class="sxs-lookup"><span data-stu-id="e9475-112">hello StorSimple device dedupes and compresses your data before sending it toohello cloud making it very efficient for sending large files toohello cloud.</span></span> <span data-ttu-id="e9475-113">Olá [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) serviço fornece APIs que permitem a você tooextract dados do StorSimple e apresentá-lo como ativos AMS.</span><span class="sxs-lookup"><span data-stu-id="e9475-113">hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you tooextract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="e9475-114">Introdução</span><span class="sxs-lookup"><span data-stu-id="e9475-114">Get started</span></span>

1. <span data-ttu-id="e9475-115">[Criar uma conta de serviços de mídia](media-services-portal-create-account.md) em que deseja que os ativos de saudação tootransfer.</span><span class="sxs-lookup"><span data-stu-id="e9475-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want tootransfer hello assets.</span></span>
2. <span data-ttu-id="e9475-116">Inscreva-se para a visualização do Gerenciador de dados, conforme descrito em Olá [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="e9475-116">Sign up for Data Manager preview, as described in hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="e9475-117">Crie uma conta do Gerenciador de Dados do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e9475-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="e9475-118">Crie um trabalho de transformação de dados que, quando executado, extrai dados de um dispositivo StorSimple e os transfere para uma conta do AMS como ativos.</span><span class="sxs-lookup"><span data-stu-id="e9475-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="e9475-119">Quando o trabalho de saudação inicia a execução, uma fila de armazenamento é criada.</span><span class="sxs-lookup"><span data-stu-id="e9475-119">When hello job starts running, a storage queue is created.</span></span> <span data-ttu-id="e9475-120">Essa fila é populada com mensagens sobre blobs transformados à medida que elas estejam prontas.</span><span class="sxs-lookup"><span data-stu-id="e9475-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="e9475-121">nome da saudação dessa fila é Olá igual ao nome de Olá Olá da definição do trabalho.</span><span class="sxs-lookup"><span data-stu-id="e9475-121">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="e9475-122">Você pode usar essa fila toodetermine quando como ativo está pronto e chamar sua toorun de operação de serviços de mídia desejado.</span><span class="sxs-lookup"><span data-stu-id="e9475-122">You can use this queue toodetermine when as asset is ready and call your desired Media Services operation toorun on it.</span></span> <span data-ttu-id="e9475-123">Por exemplo, você pode usar este tootrigger fila uma função do Azure que contém um código de serviços de mídia necessário hello.</span><span class="sxs-lookup"><span data-stu-id="e9475-123">For example, you can use this queue tootrigger an Azure Function that has hello necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="e9475-124">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e9475-124">See also</span></span>

[<span data-ttu-id="e9475-125">Use Olá .net SDK tootrigger trabalhos em Olá Gerenciador de dados</span><span class="sxs-lookup"><span data-stu-id="e9475-125">Use hello .Net SDK tootrigger jobs in hello Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="e9475-126">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="e9475-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e9475-127">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="e9475-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e9475-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e9475-128">Next steps</span></span>

<span data-ttu-id="e9475-129">Agora você pode codificar seus ativos carregados.</span><span class="sxs-lookup"><span data-stu-id="e9475-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="e9475-130">Para saber mais, veja [Codificar ativos](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="e9475-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
