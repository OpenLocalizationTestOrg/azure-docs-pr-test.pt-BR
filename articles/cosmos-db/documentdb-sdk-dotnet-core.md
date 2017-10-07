---
title: aaaAzure Cosmos DB .NET Core API, SDK e recursos | Microsoft Docs
description: "Saiba tudo sobre Olá .NET Core API e do SDK, incluindo datas de lançamento, datas de desativação e as alterações feitas entre cada versão do hello Azure Cosmos DB .NET Core SDK."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a>SDK do .NET Core do Azure Cosmos DB: notas de versão e recursos
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Feed de alterações do .NET](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Provedor de recursos REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**Baixe o SDK**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td>**Documentação da API**</td><td>[Documentação de referência de API .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Exemplos**</td><td>[Exemplos de código .NET](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Introdução**</td><td>[Introdução ao hello Azure Cosmos DB .NET Core SDK](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td>**Tutorial do aplicativo Web**</td><td>[Desenvolvimento de aplicativos Web com o Azure Cosmos DB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Framework atualmente com suporte**</td><td>[.NET Standard 1.6 e .NET Standard 1.5](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de versão

Hello Azure Cosmos DB .NET Core SDK tem paridade de recursos com versão mais recente de saudação do hello [SDK .NET do Azure Cosmos DB](documentdb-sdk-dotnet.md).

> [!NOTE] 
> Hello Azure Cosmos DB .NET Core SDK ainda não é compatível com aplicativos do Windows UWP (plataforma Universal). Se você estiver interessado em Olá .NET Core SDK que dá suporte a aplicativos UWP, envie um email muito[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0 

* Adicionado suporte para PartitionKeyRangeId como um FeedOption para definir o valor de intervalo de chave consulta resultados tooa partição específica. 
* Adicionado suporte para StartTime como um toostart ChangeFeedOption em busca de alterações de saudação depois desse tempo. 

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1

*   Corrigido um problema no hello JsonSerializable classe que pode gerar uma exceção de estouro de pilha.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0

*   Adicionado suporte para a especificação de JsonSerializerSettings personalizadas ao instanciar uma instância [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name132132"></a><a name="1.3.2"/>1.3.2

*   Suporte 1.5 padrão do .NET como uma saudação estruturas de destino.

### <a name="a-name131131"></a><a name="1.3.1"/>1.3.1

*   Corrigido um problema que afetava computadores x64 que não davam suporte à instrução SSE4 e que geravam SEHException ao executarem consultas do Azure Cosmos DB.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0

*   Adição de suporte a um novo nível de consistência chamado ConsistentPrefix.
*   Adição de suporte a métricas de consulta em partições individuais.
*   Adicionado suporte para limitar o tamanho de saudação do token de continuação Olá para consultas.
*   Adição de suporte para um rastreamento mais detalhado das solicitações com falha.
*   Feitas algumas melhorias de desempenho no hello SDK.

### <a name="a-name122122"></a><a name="1.2.2"/>1.2.2

* Corrigido um problema que ignorou o valor de PartitionKey Olá fornecido no FeedOptions para consultas de agregação.
* Correção de um problema na manipulação transparente do gerenciamento de partição durante a metade da execução da consulta Order By entre partições.

### <a name="a-name121121"></a><a name="1.2.1"/>1.2.1

* Corrigido um problema que causou deadlocks em alguns Olá async APIs quando usada dentro do contexto do ASP.NET.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0

* Correções toomake SDK mais resiliente tooautomatic failover sob determinadas condições.

### <a name="a-name112112"></a><a name="1.1.2"/>1.1.2

* Correção para um problema que causa ocasionalmente um WebException: nome remoto Olá não pôde ser resolvido.
* Olá adicionado suporte para ler um documento digitado diretamente, adicionando nova API de tooReadDocumentAsync sobrecargas.

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1

* Adicionado suporte ao LINQ para consultas de agregação (CONT.NÚM, MÍNIMO, MÁXIMO, SOMA e MÉDIA).
* Correção para um problema de vazamento de memória para o objeto de ConnectionPolicy Olá causado pelo uso de saudação do manipulador de eventos.
* Correção de um problema no qual UpsertAttachmentAsync não estava funcionando quando ETag era usada.
* Correção de um problema no qual a continuação da consulta order-by entre partições não estava funcionando ao classificar no campo de cadeia de caracteres.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0

* Suporte adicionado para consultas de agregação (COUNT, MIN, MAX, SUM e AVG). Veja [Suporte de agregação](documentdb-sql-query.md#Aggregates).
* Reduzida a taxa de transferência mínima em coleções particionadas de 10,100 RU/s too2500 RU/s.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0

Hello Azure Cosmos DB .NET Core SDK permite que você toobuild rápidos entre plataformas [ASP.NET Core](https://www.asp.net/core) e [.NET Core](https://www.microsoft.com/net/core#windows) toorun de aplicativos no Windows, Mac e Linux. Olá versão mais recente do hello Azure Cosmos DB .NET Core SDK é totalmente [Xamarin](https://www.xamarin.com) compatível e ser usado toobuild aplicativos voltados para iOS, Android e Mono (Linux).  

### <a name="a-name010-preview010-preview"></a><a name="0.1.0-preview"/>0.1.0-preview

Hello Azure Cosmos DB .NET Core Preview SDK permite que você toobuild rápidos entre plataformas [ASP.NET Core](https://www.asp.net/core) e [.NET Core](https://www.microsoft.com/net/core#windows) toorun de aplicativos no Windows, Mac e Linux.

Hello Azure Cosmos DB .NET Core Preview SDK tem paridade de recursos com versão mais recente de saudação do hello [SDK .NET do Azure Cosmos DB](documentdb-sdk-dotnet.md) e suporta Olá seguintes:
* Todos os [modos de conexão](performance-tips.md#networking): Modo de gateway, TCP Direto e HTTPs Direto. 
* Todos os [níveis de consistência](consistency-levels.md): Forte, Sessão, Desatualização Limitada e Eventual.
* [Coleções particionadas](partition-data.md). 
* [Contas e replicação geográfica de banco de dados de várias regiões](distribute-data-globally.md).

Se você tiver dúvidas relacionadas toothis SDK, postar muito[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), ou um problema de arquivo hello [repositório github](https://github.com/Azure/azure-documentdb-dotnet/issues). 

## <a name="release--retirement-dates"></a>Datas de lançamento e desativação

| Versão | Data do lançamento | Data de desativação |
| --- | --- | --- |
| [1.5.0](#1.5.0) |10 de agosto de 2017 |--- | 
| [1.4.1](#1.4.1) |7 de agosto de 2017 |--- |
| [1.4.0](#1.4.0) |2 de agosto de 2017 |--- |
| [1.3.2](#1.3.2) |12 de junho de 2017 |--- |
| [1.3.1](#1.3.1) |23 de maio de 2017 |--- |
| [1.3.0](#1.3.0) |10 de maio de 2017 |--- |
| [1.2.2](#1.2.2) |19 de abril de 2017 |--- |
| [1.2.1](#1.2.1) |29 de março de 2017 |--- |
| [1.2.0](#1.2.0) |25 de março de 2017 |--- |
| [1.1.2](#1.1.2) |20 de março de 2017 |--- |
| [1.1.1](#1.1.1) |14 de março de 2017 |--- |
| [1.1.0](#1.1.0) |16 de fevereiro de 2017 |--- |
| [1.0.0](#1.0.0) |21 de dezembro de 2016 |--- |
| [0.1.0-preview](#0.1.0-preview) |15 de novembro de 2016 |31 de dezembro de 2016 |

## <a name="see-also"></a>Consulte também
toolearn mais sobre o banco de dados do Cosmos, consulte [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de serviço. 

