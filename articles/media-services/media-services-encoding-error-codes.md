---
title: "códigos de erro de codificação de serviços de mídia aaaAzure | Microsoft Docs"
description: "Este tópico lista os códigos de erro que podem ser retornados no caso de erro encontrado durante a saudação a execução da tarefa de codificação."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="41c11-103">Códigos de erro de codificação</span><span class="sxs-lookup"><span data-stu-id="41c11-103">Encoding error codes</span></span>

<span data-ttu-id="41c11-104">Olá tabela a seguir lista os códigos de erro que podem ser retornados no caso de erro encontrado durante a saudação a execução da tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="41c11-104">hello following table lists error codes that could be returned in case an error was encountered during hello encoding task execution.</span></span>  <span data-ttu-id="41c11-105">detalhes do erro tooget no seu código .NET, use Olá [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="41c11-105">tooget error details in your .NET code, use hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="41c11-106">detalhes do erro tooget no seu código restante, use Olá [propriedades errordetail com](https://msdn.microsoft.com/library/jj853026.aspx) API REST.</span><span class="sxs-lookup"><span data-stu-id="41c11-106">tooget error details in your REST code, use hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="41c11-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="41c11-107">ErrorDetail.Code</span></span> | <span data-ttu-id="41c11-108">Causas possíveis para erro</span><span class="sxs-lookup"><span data-stu-id="41c11-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="41c11-109">Desconhecido</span><span class="sxs-lookup"><span data-stu-id="41c11-109">Unknown</span></span> |<span data-ttu-id="41c11-110">Erro desconhecido ao executar a tarefa de saudação</span><span class="sxs-lookup"><span data-stu-id="41c11-110">Unknown error while executing hello task</span></span> |
| <span data-ttu-id="41c11-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="41c11-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="41c11-112">Categoria de erros que abrange erros ao baixar um ativo de entrada, como nomes de arquivo inválidos, arquivo com comprimento zero, formatos incorretos e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="41c11-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="41c11-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="41c11-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="41c11-114">Categoria de erros que aborda problemas no lado do serviço Olá - erros de rede ou armazenamento de exemplo durante o download.</span><span class="sxs-lookup"><span data-stu-id="41c11-114">Category of errors that covers problems on hello service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="41c11-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="41c11-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="41c11-116">Categoria de erros em que a tarefa <see cref="MediaTask.PrivateData"/> (configuração) não é válida, por exemplo configuração Olá não é válido do sistema predefinido ou contém XML inválido.</span><span class="sxs-lookup"><span data-stu-id="41c11-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example hello configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="41c11-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="41c11-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="41c11-118">Categoria de erros durante a execução de saudação da tarefa de saudação em que problemas de saudação entrada arquivos de mídia causam falha.</span><span class="sxs-lookup"><span data-stu-id="41c11-118">Category of errors during hello execution of hello task where issues inside hello input media files cause failure.</span></span> |
| <span data-ttu-id="41c11-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="41c11-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="41c11-120">Categoria de erros em que o processador de mídia Olá não pode processar arquivos de Olá fornecidos - mídia de formato não tem suporte ou não coincide com hello configuração.</span><span class="sxs-lookup"><span data-stu-id="41c11-120">Category of errors where hello media processor cannot process hello files provided - media format not supported, or does not match hello Configuration.</span></span> <span data-ttu-id="41c11-121">Por exemplo, tentando tooproduce uma saída somente de áudio de um ativo que tem apenas vídeo</span><span class="sxs-lookup"><span data-stu-id="41c11-121">For example, trying tooproduce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="41c11-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="41c11-122">ErrorProcessingTask</span></span> |<span data-ttu-id="41c11-123">Categoria de outros erros que Olá processador de mídia encontra durante o processamento de saudação da tarefa de saudação que são toocontent não relacionado.</span><span class="sxs-lookup"><span data-stu-id="41c11-123">Category of other errors that hello media processor encounters during hello processing of hello task that are unrelated toocontent.</span></span> |
| <span data-ttu-id="41c11-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="41c11-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="41c11-125">Categoria de erros ao carregar Olá ativo de saída</span><span class="sxs-lookup"><span data-stu-id="41c11-125">Category of errors when uploading hello output asset</span></span> |
| <span data-ttu-id="41c11-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="41c11-126">ErrorCancelingTask</span></span> |<span data-ttu-id="41c11-127">Categoria de erros toocover falhas durante a tentativa de saudação toocancel tarefa</span><span class="sxs-lookup"><span data-stu-id="41c11-127">Category of errors toocover failures when attempting toocancel hello Task</span></span> |
| <span data-ttu-id="41c11-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="41c11-128">TransientError</span></span> |<span data-ttu-id="41c11-129">Categoria de erros toocover problemas transitórios (por exemplo.</span><span class="sxs-lookup"><span data-stu-id="41c11-129">Category of errors toocover transient issues (eg.</span></span> <span data-ttu-id="41c11-130">problemas temporários de rede com o Armazenamento do Azure)</span><span class="sxs-lookup"><span data-stu-id="41c11-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="41c11-131">Ajuda de tooget de saudação **os serviços de mídia** equipe, abra um [tíquete de suporte](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="41c11-131">tooget help from hello **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="41c11-132">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="41c11-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="41c11-133">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="41c11-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="41c11-134">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="41c11-134">Related articles</span></span>
* [<span data-ttu-id="41c11-135">Executar tarefas avançadas de codificação ao personalizar predefinições do Codificador de Mídia Padrão</span><span class="sxs-lookup"><span data-stu-id="41c11-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="41c11-136">Cotas e limitações</span><span class="sxs-lookup"><span data-stu-id="41c11-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
