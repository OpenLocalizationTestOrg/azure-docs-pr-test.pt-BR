---
title: "Visão geral da API REST de operações aaaMedia serviços | Microsoft Docs"
description: "Visão geral da API de REST de serviços de mídia"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b54f4d9123486d6cae832c9817688b0f3da5b401
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-operations-rest-api-overview"></a>Visão geral da API REST das operações dos Serviços de Mídia
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Olá **REST do Media Services operações** API é usada para criar trabalhos, ativos, as políticas de acesso e outras operações em objetos em uma conta de serviço de mídia. Para saber mais, consulte [Referência da API REST das Operações dos Serviços de Mídia](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).

Os serviços de mídia do Microsoft Azure é um serviço que aceita solicitações HTTP com base em OData e pode responder em verbose JSON ou atom+pub. Como os serviços de mídia está em conformidade com as diretrizes de design tooAzure, há um conjunto de cabeçalhos HTTP necessários que cada cliente deve usar ao se conectar a serviços tooMedia, bem como um conjunto de cabeçalhos opcionais que podem ser usados. Olá, seções a seguir descrevem os cabeçalhos hello e verbos HTTP pode ser usado ao criar solicitações e receber respostas de serviços de mídia.

Este tópico fornece uma visão geral de como toouse REST v2 com serviços de mídia.

## <a name="considerations"></a>Considerações

Olá considerações a seguir se aplicam ao usar o REST.

* Ao consultar entidades, há um limite de 1000 entidades retornadas ao mesmo tempo porque pública v2 do REST limita os resultados da consulta resultados too1000. Você precisa toouse **ignorar** e **levar** (.NET) / **superior** (REST), conforme descrito em [Este exemplo .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) e [nesta API REST exemplo](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). 
* Quando usando JSON e especificando Olá toouse **Metadata** palavra-chave na solicitação de saudação (por exemplo, tooreferences um objeto vinculado) você deve definir Olá **aceitar** cabeçalho muito[formato JSON detalhado ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (consulte Olá exemplo a seguir). OData não entende Olá **Metadata** propriedade Olá solicitação, a menos que você defina tooverbose.  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a>Os cabeçalhos de solicitação HTTP padrão suportados pelos serviços de mídia
Para todas as chamadas feitas nos serviços de mídia, há um conjunto de cabeçalhos necessários, você deve incluir na solicitação e também um conjunto de cabeçalhos opcionais convém tooinclude. Olá Olá de listas de tabela a seguir os cabeçalhos obrigatórios:

| Cabeçalho | Tipo | Valor |
| --- | --- | --- |
| Autorização |Portador |Portador é Olá aceita apenas o mecanismo de autorização. valor de saudação também deve incluir o token de acesso de saudação fornecido pelo ACS. |
| x-ms-version |Decimal |2.11 |
| DataServiceVersion |Decimal |3.0 |
| MaxDataServiceVersion |Decimal |3.0 |

> [!NOTE]
> Como os serviços de mídia usa OData tooexpose seu repositório de metadados de ativo subjacente por meio de APIs REST, hello DataServiceVersion e MaxDataServiceVersion cabeçalhos deve ser incluído em qualquer solicitação; No entanto, se não, atualmente Media Services assume Olá valor de DataServiceVersion em uso é 3.0.
> 
> 

a seguir Olá é um conjunto de cabeçalhos opcionais:

| Cabeçalho | Tipo | Valor |
| --- | --- | --- |
| Data |Data do RFC 1123 |Carimbo de hora da solicitação de saudação |
| Aceitar |Tipo de conteúdo |Olá solicitou o tipo de conteúdo de resposta de saudação como seguinte Olá:<p> -application/json;odata=verbose<p> - application/atom+xml<p> As respostas podem ter um tipo de conteúdo diferente, como uma busca de blob, onde uma resposta bem-sucedida irá conter o fluxo de blob hello como carga de saudação. |
| Codificação aceita |Gzip, deflate |Codificar GZIP e DEFLATE, quando aplicável. Observação: para grandes recursos, os Serviços de Mídia podem ignorar esse cabeçalho e retornar dados não compactados. |
| Idioma aceito |"en", "es", e assim por diante. |Especifica o idioma preferido de saudação resposta hello. |
| Conjunto de caracteres aceito |Tipo de conjunto de caracteres como "UTF-8" |Padrão é UTF-8. |
| Método X-HTTP |Método HTTP |Permite que os clientes ou firewalls que não suportam métodos HTTP como PUT ou DELETE toouse desses métodos, desviados via uma chamada GET. |
| Tipo de conteúdo |Tipo de conteúdo |Tipo de conteúdo do corpo da solicitação Olá em solicitações PUT ou POST. |
| ID da solicitação de cliente |Cadeia de caracteres |Um valor definido pelo chamador que identifica Olá recebe a solicitação. Se especificado, esse valor será incluído na mensagem de resposta de saudação como uma solicitação de saudação toomap maneira. <p><p>**Importante**<p>Os valores devem ser limitados a 2096b (2K). |

## <a name="standard-http-response-headers-supported-by-media-services"></a>Cabeçalhos de resposta HTTP padrão suportados pelos serviços de mídia
a seguir Olá é um conjunto de cabeçalhos que podem ser retornados tooyou dependendo do recurso de saudação que estava solicitando e Olá ação pretendido tooperform.

| Cabeçalho | Tipo | Valor |
| --- | --- | --- |
| ID da solicitação |Cadeia de caracteres |Um identificador exclusivo para a operação atual hello, serviço gerado. |
| ID da solicitação de cliente |Cadeia de caracteres |Um identificador especificado pelo chamador Olá na solicitação original do hello, se presente. |
| Data |Data do RFC 1123 |Data de saudação que Olá solicitação foi processada. |
| Tipo de conteúdo |Varia |tipo de conteúdo Olá Olá do corpo da resposta. |
| Codificação de conteúdo |Varia |Gzip ou deflate, conforme apropriado. |

## <a name="standard-http-verbs-supported-by-media-services"></a>Verbos HTTP padrão suportados pelos serviços de mídia.
a seguir Olá é uma lista completa de verbos HTTP que podem ser usados quando fazem solicitações HTTP:

| Verbo | Descrição |
| --- | --- |
| GET |Retorna Olá valor atual de um objeto. |
| POST |Cria um objeto com base em dados Olá fornecidos ou envia um comando. |
| PUT |Substitui um objeto ou cria um objeto nomeado (quando aplicável). |
| EXCLUIR |Exclui um objeto. |
| MESCLAR |Atualiza um objeto existente com alterações de propriedade nomeada. |
| HEAD |Retorna metadados de um objeto para uma resposta GET. |

## <a name="discover-media-services-model"></a>Descobrir o modelo Serviços de Mídia
entidades de serviços de mídia toomake mais detectáveis, operação Olá $metadata podem ser usadas. Permite que você tooretrieve todos os tipos válidos de entidade, propriedades de entidade, associações, funções, ações e assim por diante. Olá exemplo a seguir mostra como tooconstruct Olá URI: https://media.windows.net/API/$ metadados.

Você deve anexar "? api-version=2.x" toohello final de saudação URI se você quiser tooview Olá metadados em um navegador ou não incluir o cabeçalho x-ms-version de saudação na solicitação.

## <a name="connect-toomedia-services"></a>Conectar os serviços de tooMedia

Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md). Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia. Você deve fazer chamadas subsequentes toohello novo URI.

## <a name="next-steps"></a>Próximas etapas

tooaccess AMS APIs com REST, consulte [tooaccess de autenticação de uso do AD do Azure Olá API de serviços de mídia do Azure com REST](media-services-rest-connect-with-aad.md).

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

