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
# <a name="how-to-get-a-media-processor-instance"></a>Como obter uma instância do processador de mídia
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Visão geral
Nos Serviços de Mídia, um processador de mídia é um componente que manipula uma tarefa de processamento específica, como codificação, conversão de formato, criptografia ou descriptografia de conteúdo de mídia. Normalmente você cria um processador de mídia quando você estiver criando uma tarefa tooencode, criptografar ou converter o formato de saudação do conteúdo de mídia.

## <a name="azure-media-processors"></a>Processadores de mídia do Azure 

Olá tópico a seguir fornece listas de processadores de mídia:

* [Codificação de processadores de mídia](scenarios-and-availability.md#encoding-media-processors)
* [Processadores de mídia do Analytics](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a>Obter processador de mídia

Olá mostra do método a seguir como tooget uma instância do processador de mídia. exemplo de código Hello assume o uso de saudação de uma variável de nível de módulo chamada **Context** tooreference contexto de servidor de saudação conforme descrito na seção Olá [como: conectar programaticamente os serviços tooMedia](media-services-use-aad-auth-to-access-ams-api.md).

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Próximas etapas
Agora que você sabe como tooget uma instância do processador de mídia, vá toohello [como um ativo de tooEncode](media-services-dotnet-encode-with-media-encoder-standard.md) tópico que lhe mostrará como toouse Olá tooencode codificador de mídia padrão um ativo.

