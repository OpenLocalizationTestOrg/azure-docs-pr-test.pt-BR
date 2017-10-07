---
title: "Perguntas frequentes sobre os serviços de mídia de aaaAzure | Microsoft Docs"
description: Perguntas frequentes (FAQs)
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a>Perguntas frequentes

Este artigo aborda as perguntas frequentes geradas pela comunidade de usuários de serviços de mídia do Azure (AMS) hello.

## <a name="general-ams-faqs"></a>Perguntas frequentes sobre o AMS geral
P: Como você dimensiona indexação?

R: unidades de Olá reservado são hello mesmo para codificação e tarefas de indexação. Siga as instruções [como unidades reservadas de codificação tooScale](media-services-scale-media-processing-overview.md). **Observação** o desempenho do indexador não é afetado pelo tipo de unidade reservada.

P: Carreguei, codifiquei e publiquei um vídeo. Qual seria o vídeo de saudação do motivo de saudação não reproduzido quando tento toostream-lo?

R: um dos hello mais comuns motivos é não possuem Olá streaming de ponto de extremidade do qual você está tentando tooplayback em Olá **executando** estado.  

P: Posso fazer a composição em um fluxo ao vivo?

R: composição em fluxos ao vivo no momento não é oferecida nos serviços de mídia do Azure, portanto, seria necessário toopre-compor em seu computador.

P: Pode usar o CDN do Azure com a transmissão ao vivo?

R: Media Services dá suporte à integração com o Azure CDN (para obter mais informações, consulte [como tooManage pontos de extremidade de Streaming em uma conta do Media Services](media-services-portal-manage-streaming-endpoints.md)).  Você pode usar a transmissão ao vivo o com CDN. Os Serviços de Mídia do Azure fornecem saídas de Smooth Streaming, HLS e MPEG-DASH. Todos esses formatos usam HTTP para transferir dados e obtêm os benefícios do cache de HTTP. Ao vivo de fluxo de dados de áudio/vídeo reais é dividido toofragments e este fragmentos individuais ficar armazenada em cache na CDN. Somente dados necessidades toobe atualizado é dados de manifesto de saudação. A CDN atualiza periodicamente os dados de manifesto.

P: Os Serviços de Mídia do Azure dão suporte ao armazenamento de imagens?

R: se você estiver procurando apenas toostore JPEG ou imagens PNG, você deve manter aqueles no armazenamento de BLOBs do Azure. Não há nenhum tooputting benefício-los nos serviços de mídia de conta, a menos que você deseja tookeep-los associados com seu vídeo ou áudio ativos. Ou se você pode ter uma necessidade toouse Olá imagens como sobreposições no codificador de vídeo hello. Codificador de mídia padrão suporta sobreposições de imagens na parte superior de vídeos, e que é o que ela lista JPEG e PNG como suporte para formatos de entrada. Para obter mais informações, consulte [Criando sobreposições](media-services-advanced-encoding-with-mes.md#overlay).

P: como posso copiar ativos de uma tooanother de conta de serviços de mídia.

R: toocopy ativos de uma tooanother de conta de serviços de mídia usando .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) método de extensão disponível no hello [extensões do SDK do Azure Media Services .NET](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repositório. Para saber mais, consulte o thread [deste](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) fórum.

P: quais são Olá caracteres suportados para nomeação de arquivos ao trabalhar com AMS?

Unidade: serviços de mídia de usa o valor de saudação do hello IAssetFile.Name propriedade ao criar URLs para Olá streaming de conteúdo (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esse motivo, não é permitida a codificação por porcentagem. Olá valor Olá **nome** propriedade não pode ter qualquer um dos seguintes Olá [%-caracteres reservados codificados](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Além disso, pode haver somente um ‘.’ para a extensão de nome de arquivo hello.

P: como tooconnect usando REST?

R: para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md). Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia. Você deve fazer chamadas subsequentes toohello novo URI. 

P: como é possível girar um vídeo durante o processo de codificação de saudação.

R: Olá [codificador de mídia padrão](media-services-dotnet-encode-with-media-encoder-standard.md) dá suporte a rotação de ângulos de 180/90/270. comportamento padrão de saudação é "Auto", onde ele tenta toodetect Olá rotação metadados na entrada de arquivo MP4/MOV hello e compensar a ele. Incluem hello seguinte **fontes** tooone de elemento de saudação json predefinições definidas [aqui](media-services-mes-presets-overview.md):

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
