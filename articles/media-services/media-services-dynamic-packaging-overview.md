---
title: "Visão geral do empacotamento dinâmico de serviços de mídia aaaAzure | Microsoft Docs"
description: "Olá tópico apresenta e visão geral do empacotamento dinâmico."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a>Empacotamento dinâmico
## <a name="overview"></a>Visão geral
Serviços de mídia do Microsoft Azure pode ser usado toodeliver mídia muitos formatos de arquivo, formatos de streaming de mídia e proteção de conteúdo formatos tooa variedade de tecnologias de cliente de origem (por exemplo, iOS, XBOX, Silverlight, Windows 8). Esses clientes entendem protocolos diferentes, por exemplo: o iOS requer um formato HTTP Live Streaming (HLS) V4, enquanto Silverlight e Xbox requerem Smooth Streaming. Se você tiver um conjunto de taxa de bits adaptável (múltiplas taxas de bits) MP4 arquivos (ISO Base Media 14496-12) ou um conjunto de arquivos de Smooth Streaming de taxa de bits adaptável que você deseja tooclients tooserve que compreendam MPEG DASH, HLS ou Smooth Streaming, você deve aproveitar da mídia Serviços de empacotamento dinâmico.

Com o empacotamento dinâmico, tudo o que você precisa é toocreate um ativo que contém um conjunto de arquivos MP4 de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável. Em seguida, com base no formato de saudação especificado no manifesto de saudação ou solicitação de fragmento, Olá sob demanda de Streaming server irá garantir que você receba o fluxo de saudação no protocolo hello escolhido. Como resultado, você só precisa toostore e pagamento para arquivos de saudação em único formato de armazenamento e serviços de mídia criará e enviará a resposta apropriada hello, com base nas solicitações de um cliente.

Olá diagrama a seguir mostra Olá tradicional codificação e fluxo de trabalho de empacotamento estático.

![Codificação estática](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

Olá diagrama a seguir mostra o fluxo de trabalho do hello empacotamento dinâmico.

![Codificação dinâmica](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a>Cenário comum
1. Carrega um arquivo de entrada (chamado de arquivo de mezanino). Por exemplo, h. 264, MP4 ou WMV (para obter lista de saudação de formatos com suporte, consulte [formatos suportados pelo codificador de mídia padrão da saudação](media-services-media-encoder-standard-formats.md).
2. Codifica seus conjuntos de taxa de bits adaptável mezanino arquivo tooH.264 MP4.
3. Publica o ativo de saudação que contém a taxa de bits adaptável Olá MP4 set criando Olá localizador sob demanda.
4. Criar hello tooaccess URLs de streaming e transmitir o conteúdo.

## <a name="preparing-assets-for-dynamic-streaming"></a>Preparação de ativos para streaming dinâmico
tooprepare seu ativo para dinâmico streaming, você tem duas opções:

1. [Carregue um arquivo mestre](media-services-dotnet-upload-files.md).
2. [Usar conjuntos de taxa de bits adaptável para Olá codificador de mídia padrão codificador tooproduce MP4 h. 264](media-services-dotnet-encode-with-media-encoder-standard.md).
3. [Transmita seu conteúdo](media-services-deliver-content-overview.md).

## <a id="unsupported_formats"></a>Formatos sem suporte pelo empacotamento dinâmico
Olá seguintes formatos de arquivo de origem não há suporte para empacotamento dinâmico.

* Arquivos mp4 Dolby digital.
* Arquivos suaves Dolby digital.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

