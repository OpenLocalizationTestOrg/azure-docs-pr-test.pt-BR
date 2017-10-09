---
title: "aaaOverview e a comparação do Azure na demandam codificadores de mídia | Microsoft Docs"
description: "Este tópico fornece uma visão geral e uma comparação dos codificadores de mídia sob demanda do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a>Visão geral e comparação de codificadores de mídia sob demanda do Azure
## <a name="encoding-overview"></a>Visão Geral de Codificação
Serviços de mídia do Azure fornece várias opções para Olá codificação de mídia na nuvem hello.

Começando com os serviços de mídia, é importante toounderstand diferença de saudação entre codecs e formatos de arquivo.
Codecs são Olá de software que implementa os algoritmos de compactação/descompactação Olá enquanto formatos de arquivo são contêineres que armazenam o vídeo Olá compactado.

Serviços de mídia fornecem empacotamento dinâmico que permite que você toodeliver sua taxa de bits adaptável MP4 ou Smooth Streaming codificado conteúdo de streaming formatos suportados pelo Media Services (MPEG DASH, HLS, Smooth Streaming) sem a necessidade de toore-package nesses formatos de fluxo contínuo.

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. aproveitar tootake [empacotamento dinâmico](media-services-dynamic-packaging-overview.md), você precisa toodo Olá seguinte:
>
>Além disso, codifica o arquivo de origem em um conjunto de arquivos MP4 de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável (etapas de codificação Olá são demonstradas posteriormente neste tutorial).

Serviços de mídia oferece suporte a seguinte Olá em codificadores de demanda que são descritos neste artigo:

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Fluxo de trabalho do Media Encoder Premium](media-services-encode-asset.md#media-encoder-premium-workflow)

Este artigo fornece uma visão geral de sob demanda codificadores de mídia e fornece links tooarticles que fornecem informações mais detalhadas. tópico de Olá também fornece a comparação de codificadores hello.

>[!NOTE]
>Por padrão, cada conta dos Serviços de Mídia pode ter uma tarefa de codificação ativa por vez. Você pode reservar unidades de codificação que permitem que você toohave várias tarefas de codificação em execução simultaneamente, uma para cada unidade reservada de codificação que comprar. Para saber mais, consulte [Dimensionamento das unidades de codificação](media-services-scale-media-processing-overview.md).

## <a name="media-encoder-standard"></a>Media Encoder Standard
### <a name="how-toouse"></a>Como toouse
[Como tooencode com o codificador de mídia padrão](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a>Formatos
[Formatos e codecs](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a>Predefinições
Codificador de mídia padrão é configurado usando uma das predefinições de codificador Olá descritas [aqui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Metadados de entrada e saída
Olá codificadores metadados de entrada é descrito [aqui](media-services-input-metadata-schema.md).

Olá codificadores metadados de saída é descrito [aqui](media-services-output-metadata-schema.md).

### <a name="generate-thumbnails"></a>Gerar miniaturas
Para obter informações, consulte [como miniaturas toogenerate usando o codificador de mídia padrão](media-services-advanced-encoding-with-mes.md#thumbnails).

### <a name="trim-videos-clipping"></a>Cortar vídeos (recorte)
Para obter informações, consulte [como vídeos tootrim usando o codificador de mídia padrão](media-services-advanced-encoding-with-mes.md#trim_video).

### <a name="create-overlays"></a>Criar sobreposições
Para obter informações, consulte [como sobreposições toocreate usando o codificador de mídia padrão](media-services-advanced-encoding-with-mes.md#overlay).

### <a name="see-also"></a>Consulte também
[blog de serviços de mídia Olá](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a>Fluxo de trabalho do Media Encoder Premium
### <a name="overview"></a>Visão geral
[Apresentando a codificação Premium nos Serviços de Mídia do Azure](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a>Como toouse
O fluxo de trabalho do Media Encoder Premium é configurado usando fluxos de trabalho complexos. Arquivos de fluxo de trabalho pode ser criados e atualizado com hello [Designer de fluxo de trabalho](media-services-workflow-designer.md) ferramenta.

[Como tooUse Premium de codificação no Azure Media Services](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a>Problemas conhecidos
Se o vídeo de entrada não contém a legenda codificada, Olá saída que ativo ainda conterá um arquivo TTML vazio.


## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Artigos relacionados
* [Executar tarefas avançadas de codificação ao personalizar predefinições do Codificador de Mídia Padrão](media-services-custom-mes-presets-with-dotnet.md)
* [Cotas e limitações](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
