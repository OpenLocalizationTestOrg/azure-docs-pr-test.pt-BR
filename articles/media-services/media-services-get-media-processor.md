---
title: "Como criar um processador de mídia usando o SDK de Serviços de Mídia do Azure para .NET | Microsoft Docs"
description: "Saiba como criar um componente de processador de mídia para codificar, converter o formato, criptografar ou descriptografar conteúdo de mídia dos Serviços de Mídia do Azure. Os exemplos de código são escritos em C# e usam a SDK dos Serviços de Mídia para .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: c2cbe41b71afa8acc184f9d7f4cfe94686de783e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="3e385-104">Como obter uma instância do processador de mídia</span><span class="sxs-lookup"><span data-stu-id="3e385-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e385-105">.NET</span><span class="sxs-lookup"><span data-stu-id="3e385-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="3e385-106">REST</span><span class="sxs-lookup"><span data-stu-id="3e385-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="3e385-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3e385-107">Overview</span></span>
<span data-ttu-id="3e385-108">Nos Serviços de Mídia, um processador de mídia é um componente que manipula uma tarefa de processamento específica, como codificação, conversão de formato, criptografia ou descriptografia de conteúdo de mídia.</span><span class="sxs-lookup"><span data-stu-id="3e385-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="3e385-109">Normalmente, você cria um processador de mídia quando está criando uma tarefa para codificar, criptografar ou converter o formato do conteúdo de mídia.</span><span class="sxs-lookup"><span data-stu-id="3e385-109">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="3e385-110">Processadores de mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="3e385-110">Azure media processors</span></span> 

<span data-ttu-id="3e385-111">O tópico a seguir fornece listas de processadores de mídia:</span><span class="sxs-lookup"><span data-stu-id="3e385-111">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="3e385-112">Codificação de processadores de mídia</span><span class="sxs-lookup"><span data-stu-id="3e385-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="3e385-113">Processadores de mídia do Analytics</span><span class="sxs-lookup"><span data-stu-id="3e385-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="3e385-114">Obter processador de mídia</span><span class="sxs-lookup"><span data-stu-id="3e385-114">Get Media Processor</span></span>

<span data-ttu-id="3e385-115">O método a seguir mostra como obter uma instância do processador de mídia.</span><span class="sxs-lookup"><span data-stu-id="3e385-115">The following method shows how to get a media processor instance.</span></span> <span data-ttu-id="3e385-116">O exemplo de código pressupõe o uso de uma variável em nível de módulo chamada **_context** para fazer referência ao contexto do servidor, conforme é descrito na seção [Como conectar-se aos Serviços de Mídia de forma programática](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="3e385-116">The code example assumes the use of a module-level variable named **_context** to reference the server context as described in the section [How to: Connect to Media Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="3e385-117">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="3e385-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3e385-118">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="3e385-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="3e385-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3e385-119">Next Steps</span></span>
<span data-ttu-id="3e385-120">Agora que você já sabe como obter uma instância do processador de mídia, vá para o tópico [Como Codificar um Ativo](media-services-dotnet-encode-with-media-encoder-standard.md) , que mostrará como usar o Codificador de Mídia Standard para codificar um ativo.</span><span class="sxs-lookup"><span data-stu-id="3e385-120">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

