---
title: "tooCreate aaaHow um processador de mídia usando hello Azure Media Services SDK para .NET | Microsoft Docs"
description: "Saiba como toocreate uma tooencode de componente de processador de mídia, converter o formato, criptografar ou descriptografar o conteúdo de mídia do Azure Media Services. Exemplos de código são escritos em c# e usam Olá SDK do Media Services para .NET."
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
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="c3c32-104">Como obter uma instância do processador de mídia</span><span class="sxs-lookup"><span data-stu-id="c3c32-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3c32-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c3c32-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="c3c32-106">REST</span><span class="sxs-lookup"><span data-stu-id="c3c32-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c3c32-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c3c32-107">Overview</span></span>
<span data-ttu-id="c3c32-108">Nos Serviços de Mídia, um processador de mídia é um componente que manipula uma tarefa de processamento específica, como codificação, conversão de formato, criptografia ou descriptografia de conteúdo de mídia.</span><span class="sxs-lookup"><span data-stu-id="c3c32-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="c3c32-109">Normalmente você cria um processador de mídia quando você estiver criando uma tarefa tooencode, criptografar ou converter o formato de saudação do conteúdo de mídia.</span><span class="sxs-lookup"><span data-stu-id="c3c32-109">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="c3c32-110">Processadores de mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="c3c32-110">Azure media processors</span></span> 

<span data-ttu-id="c3c32-111">Olá tópico a seguir fornece listas de processadores de mídia:</span><span class="sxs-lookup"><span data-stu-id="c3c32-111">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="c3c32-112">Codificação de processadores de mídia</span><span class="sxs-lookup"><span data-stu-id="c3c32-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="c3c32-113">Processadores de mídia do Analytics</span><span class="sxs-lookup"><span data-stu-id="c3c32-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="c3c32-114">Obter processador de mídia</span><span class="sxs-lookup"><span data-stu-id="c3c32-114">Get Media Processor</span></span>

<span data-ttu-id="c3c32-115">Olá mostra do método a seguir como tooget uma instância do processador de mídia.</span><span class="sxs-lookup"><span data-stu-id="c3c32-115">hello following method shows how tooget a media processor instance.</span></span> <span data-ttu-id="c3c32-116">exemplo de código Hello assume o uso de saudação de uma variável de nível de módulo chamada **Context** tooreference contexto de servidor de saudação conforme descrito na seção Olá [como: conectar programaticamente os serviços tooMedia](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="c3c32-116">hello code example assumes hello use of a module-level variable named **_context** tooreference hello server context as described in hello section [How to: Connect tooMedia Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="c3c32-117">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="c3c32-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c3c32-118">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="c3c32-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c3c32-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3c32-119">Next Steps</span></span>
<span data-ttu-id="c3c32-120">Agora que você sabe como tooget uma instância do processador de mídia, vá toohello [como um ativo de tooEncode](media-services-dotnet-encode-with-media-encoder-standard.md) tópico que lhe mostrará como toouse Olá tooencode codificador de mídia padrão um ativo.</span><span class="sxs-lookup"><span data-stu-id="c3c32-120">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

