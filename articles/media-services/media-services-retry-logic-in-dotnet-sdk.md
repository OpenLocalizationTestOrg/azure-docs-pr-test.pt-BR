---
title: "lógica de aaaRetry em Olá SDK de serviços de mídia para .NET | Microsoft Docs"
description: "tópico de saudação dá uma visão geral de lógica de repetição em Olá SDK do Media Services para .NET."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 527b61a6-c862-4bd8-bcbc-b9aea1ffdee3
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 18d0a9d68e55a48bc769fb6ae5711ddba78ed8e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retry-logic-in-hello-media-services-sdk-for-net"></a>Lógica de repetição em Olá SDK do Media Services para .NET
Ao trabalhar com os serviços do Microsoft Azure, algumas falhas transitórias podem ocorrer. Se ocorrer uma falha temporária, na maioria dos casos, após várias tentativas alguns hello operação for bem-sucedida. Olá SDK de serviços de mídia para .NET implementa Olá repetição lógica toohandle falhas transitórias associadas com exceções e erros causados por solicitações da web, executar consultas, salvar as alterações e operações de armazenamento.  Por padrão, Olá SDK de serviços de mídia para .NET executa quatro repetições antes de relançar o aplicativo de tooyour hello exceção. código Olá em seu aplicativo deve tratar essa exceção corretamente.  

 a seguir Olá é uma diretriz breve das políticas de solicitação da Web, armazenamento, consulta e SaveChanges:  

* Olá política de armazenamento é usada para operações de armazenamento de blob (carregamentos ou download de arquivos de ativo).  
* Olá diretiva de solicitação da Web é usada para solicitações de web genéricos (por exemplo, para obter uma autenticação de token e resolver usuários Olá ponto de extremidade do cluster).  
* Olá diretiva de consulta é usada para consultar entidades do REST (por exemplo, mediaContext.Assets.Where(...)).  
* Olá SaveChanges política é usada para fazer qualquer coisa que as alterações de dados no serviço de saudação (por exemplo, criar uma entidade de uma entidade, chamar uma função de serviço para uma operação de atualização).  
  
  Este tópico lista os tipos de exceção e lógica de repetição de códigos de erro que são manipulados pelo Olá SDK do Media Services para .NET.  

## <a name="exception-types"></a>Tipos de exceção
Olá tabela a seguir descreve as exceções que Olá SDK do Media Services para .NET identificadores ou não lida com algumas operações que podem causar falhas transitórias.  

| Exceção | Solicitação da Web | Armazenamento | Consultar | SaveChanges |
| --- | --- | --- | --- | --- |
| WebException<br/>Para obter mais informações, consulte Olá [códigos de status WebException](media-services-retry-logic-in-dotnet-sdk.md#WebExceptionStatus) seção. |Sim |Sim |Sim |Sim |
| DataServiceClientException<br/> Para saber mais, consulte [Códigos de status de erro HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Não |Sim |Sim |Sim |
| DataServiceQueryException<br/> Para saber mais, consulte [Códigos de status de erro HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Não |Sim |Sim |Sim |
| DataServiceRequestException<br/> Para saber mais, consulte [Códigos de status de erro HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Não |Sim |Sim |Sim |
| DataServiceTransportException |Não |Não |Sim |Sim |
| TimeoutException |Sim |Sim |Sim |Não |
| SocketException |Sim |Sim |Sim |Sim |
| StorageException |Não |Sim |Não |Não |
| IOException |Não |Sim |Não |Não |

### <a name="WebExceptionStatus"></a> Códigos de status WebException
Olá tabela a seguir mostra quais erro WebException lógica de repetição de saudação de códigos é implementada. Olá [WebExceptionStatus](http://msdn.microsoft.com/library/system.net.webexceptionstatus.aspx) enumeração define os códigos de status de saudação.  

| Status | Solicitação da Web | Armazenamento | Consultar | SaveChanges |
| --- | --- | --- | --- | --- |
| ConnectFailure |Sim |Sim |Sim |Sim |
| NameResolutionFailure |Sim |Sim |Sim |Sim |
| ProxyNameResolutionFailure |Sim |Sim |Sim |Sim |
| SendFailure |Sim |Sim |Sim |Sim |
| PipelineFailure |Sim |Sim |Sim |Não |
| ConnectionClosed |Sim |Sim |Sim |Não |
| KeepAliveFailure |Sim |Sim |Sim |Não |
| UnknownError |Sim |Sim |Sim |Não |
| ReceiveFailure |Sim |Sim |Sim |Não |
| RequestCanceled |Sim |Sim |Sim |Não |
| Tempo limite |Sim |Sim |Sim |Não |
| ProtocolError <br/>repetição de saudação em erro de protocolo é controlada pela manipulação de código de status HTTP hello. Para saber mais, consulte [Códigos de status de erro HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Sim |Sim |Sim |Sim |

### <a name="HTTPStatusCode"></a> Códigos de status de erro HTTP
Quando as operações de consulta e SaveChanges lançam DataServiceClientException, DataServiceQueryException ou DataServiceQueryException, Olá código de status de erro HTTP é retornado em Olá propriedade StatusCode.  Olá tabela a seguir mostra quais códigos de erro de lógica de repetição de saudação é implementada.  

| Status | Solicitação da Web | Armazenamento | Consultar | SaveChanges |
| --- | --- | --- | --- | --- |
| 401 |Não |Sim |Não |Não |
| 403 |Não |Sim<br/>Tratar repetições sem esperas longas. |Não |Não |
| 408 |Sim |Sim |Sim |Sim |
| 429 |Sim |Sim |Sim |Sim |
| 500 |Sim |Sim |Sim |Não |
| 502 |Sim |Sim |Sim |Não |
| 503 |Sim |Sim |Sim |Sim |
| 504 |Sim |Sim |Sim |Não |

Se você quiser tootake uma olhada na implementação real Olá Olá SDK do Media Services para lógica de repetição do .NET, consulte [azure sdk para o media services](https://github.com/Azure/azure-sdk-for-media-services/tree/dev/src/net/Client/TransientFaultHandling).

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

