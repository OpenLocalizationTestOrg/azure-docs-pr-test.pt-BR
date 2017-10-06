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
# <a name="encoding-error-codes"></a>Códigos de erro de codificação

Olá tabela a seguir lista os códigos de erro que podem ser retornados no caso de erro encontrado durante a saudação a execução da tarefa de codificação.  detalhes do erro tooget no seu código .NET, use Olá [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) classe. detalhes do erro tooget no seu código restante, use Olá [propriedades errordetail com](https://msdn.microsoft.com/library/jj853026.aspx) API REST.

| ErrorDetail.Code | Causas possíveis para erro |
| --- | --- |
| Desconhecido |Erro desconhecido ao executar a tarefa de saudação |
| ErrorDownloadingInputAssetMalformedContent |Categoria de erros que abrange erros ao baixar um ativo de entrada, como nomes de arquivo inválidos, arquivo com comprimento zero, formatos incorretos e assim por diante. |
| ErrorDownloadingInputAssetServiceFailure |Categoria de erros que aborda problemas no lado do serviço Olá - erros de rede ou armazenamento de exemplo durante o download. |
| ErrorParsingConfiguration |Categoria de erros em que a tarefa <see cref="MediaTask.PrivateData"/> (configuração) não é válida, por exemplo configuração Olá não é válido do sistema predefinido ou contém XML inválido. |
| ErrorExecutingTaskMalformedContent |Categoria de erros durante a execução de saudação da tarefa de saudação em que problemas de saudação entrada arquivos de mídia causam falha. |
| ErrorExecutingTaskUnsupportedFormat |Categoria de erros em que o processador de mídia Olá não pode processar arquivos de Olá fornecidos - mídia de formato não tem suporte ou não coincide com hello configuração. Por exemplo, tentando tooproduce uma saída somente de áudio de um ativo que tem apenas vídeo |
| ErrorProcessingTask |Categoria de outros erros que Olá processador de mídia encontra durante o processamento de saudação da tarefa de saudação que são toocontent não relacionado. |
| ErrorUploadingOutputAsset |Categoria de erros ao carregar Olá ativo de saída |
| ErrorCancelingTask |Categoria de erros toocover falhas durante a tentativa de saudação toocancel tarefa |
| TransientError |Categoria de erros toocover problemas transitórios (por exemplo. problemas temporários de rede com o Armazenamento do Azure) |

Ajuda de tooget de saudação **os serviços de mídia** equipe, abra um [tíquete de suporte](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Artigos relacionados
* [Executar tarefas avançadas de codificação ao personalizar predefinições do Codificador de Mídia Padrão](media-services-custom-mes-presets-with-dotnet.md)
* [Cotas e limitações](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
