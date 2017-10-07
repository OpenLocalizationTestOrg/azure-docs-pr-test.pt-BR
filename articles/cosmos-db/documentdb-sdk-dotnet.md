---
title: aaaAzure Cosmos DB .NET SDK & recursos | Microsoft Docs
description: "Saiba tudo sobre Olá .NET API e do SDK, incluindo datas de lançamento, datas de desativação e as alterações feitas entre cada versão do hello Azure Cosmos DB .NET SDK."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ec30e0130067a9b8d4c9176cf7465bac8925bf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a>SDK do .NET do Azure Cosmos DB: download e notas de versão
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

<tr><td>**Baixe o SDK**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td>**Documentação da API**</td><td>[Documentação de referência de API .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Exemplos**</td><td>[Exemplos de código .NET](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Introdução**</td><td>[Introdução ao hello Azure Cosmos DB .NET SDK](documentdb-get-started.md)</td></tr>

<tr><td>**Tutorial do aplicativo Web**</td><td>[Desenvolvimento de aplicativos Web com o Azure Cosmos DB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Framework atualmente com suporte**</td><td>[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de versão

### <a name="a-name11701170"></a><a name="1.17.0"/>1.17.0 

* Adicionado suporte para PartitionKeyRangeId como um FeedOption para definir o valor de intervalo de chave consulta resultados tooa partição específica. 
* Adicionado suporte para StartTime como um toostart ChangeFeedOption em busca de alterações de saudação depois desse tempo.

### <a name="a-name11611161"></a><a name="1.16.1"/>1.16.1
* Corrigido um problema no hello JsonSerializable classe que pode gerar uma exceção de estouro de pilha.

### <a name="a-name11601160"></a><a name="1.16.0"/>1.16.0
*   Corrigido um problema em que é necessário recompilar do aplicativo hello devido a introdução de toohello de JsonSerializerSettings como um parâmetro opcional no construtor de DocumentClient hello.
* Olá marcada DocumentClient construtor obsoleto que necessária JsonSerializerSettings como Olá última tooallow de parâmetro para valores padrão de parâmetros ConnectionPolicy e ConsistencyLevel ao passar no parâmetro JsonSerializerSettings.

### <a name="a-name11501150"></a><a name="1.15.0"/>1.15.0
*   Adicionado suporte para a especificação de JsonSerializerSettings personalizadas ao instanciar [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name11411141"></a><a name="1.14.1"/>1.14.1
*   Correção de um problema que afetava computadores x64 que não tinham suporte à instrução SSE4 e geravam uma SEHException ao executarem consultas da API DocumentDB do Azure Cosmos DB.

### <a name="a-name11401140"></a><a name="1.14.0"/>1.14.0
*   Adição de suporte a um novo nível de consistência chamado ConsistentPrefix.
*   Adição de suporte a métricas de consulta em partições individuais.
*   Adicionado suporte para limitar o tamanho de saudação do token de continuação Olá para consultas.
*   Adição de suporte para um rastreamento mais detalhado das solicitações com falha.
*   Feitas algumas melhorias de desempenho no hello SDK.

### <a name="a-name11341134"></a><a name="1.13.4"/>1.13.4
* Funcionalmente equivalente a 1.13.3. Algumas alterações internas.

### <a name="a-name11331133"></a><a name="1.13.3"/>1.13.3
* Funcionalmente equivalente a 1.13.2. Algumas alterações internas.

### <a name="a-name11321132"></a><a name="1.13.2"/>1.13.2
* Corrigido um problema que ignorou o valor de PartitionKey Olá fornecido no FeedOptions para consultas de agregação.
* Correção de um problema na manipulação transparente do gerenciamento de partição durante a metade da execução da consulta Order By entre partições.

### <a name="a-name11311131"></a><a name="1.13.1"/>1.13.1
* Corrigido um problema que causou deadlocks em alguns Olá async APIs quando usada dentro do contexto do ASP.NET.

### <a name="a-name11301130"></a><a name="1.13.0"/>1.13.0
* Correções toomake SDK mais resiliente tooautomatic failover sob determinadas condições.

### <a name="a-name11221122"></a><a name="1.12.2"/>1.12.2
* Correção para um problema que causa ocasionalmente um WebException: nome remoto Olá não pôde ser resolvido.
* Olá adicionado suporte para ler um documento digitado diretamente, adicionando nova API de tooReadDocumentAsync sobrecargas.

### <a name="a-name11211121"></a><a name="1.12.1"/>1.12.1
* Adicionado suporte ao LINQ para consultas de agregação (CONT.NÚM, MÍNIMO, MÁXIMO, SOMA e MÉDIA).
* Correção para um problema de vazamento de memória para o objeto de ConnectionPolicy Olá causado pelo uso de saudação do manipulador de eventos.
* Correção de um problema no qual UpsertAttachmentAsync não estava funcionando quando ETag era usada.
* Correção de um problema no qual a continuação da consulta order-by entre partições não estava funcionando ao classificar no campo de cadeia de caracteres.

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Suporte adicionado para consultas de agregação (COUNT, MIN, MAX, SUM e AVG). Veja [Suporte de agregação](documentdb-sql-query.md#Aggregates).
* Reduzida a taxa de transferência mínima em coleções particionadas de 10,100 RU/s too2500 RU/s.

### <a name="a-name11141114"></a><a name="1.11.4"/>1.11.4
* Correção para um problema no qual algumas Olá entre partições consultas com falha no processo de host de 32 bits de saudação.
* Para corrigir um problema no qual contêiner de sessão Olá não estava sendo atualizado com o token Olá para solicitações com falha no modo de Gateway.
* Correção para um problema no qual uma consulta com chamadas a UDF na projeção estava falhando em alguns casos.
* Correções de desempenho do lado cliente para aumentar a saudação de leitura e gravação a taxa de transferência de solicitações de saudação.

### <a name="a-name11131113"></a><a name="1.11.3"/>1.11.3
* Para corrigir um problema no qual contêiner de sessão Olá não estava sendo atualizado com o token Olá para solicitações com falha.
* Adicionado suporte para Olá SDK toowork em um processo de host de 32 bits. Observe que, se você usar consultas entre partições, processamento de host de 64 bits é recomendado para melhorar o desempenho.
* Desempenho aprimorado para cenários que envolvem consultas com um grande número de valores de chave de partição em uma expressão em.
* Preenchido várias estatísticas de cota de recursos no hello ResourceResponse para solicitações de leitura de conjunto de documentos quando a opção de solicitação PopulateQuotaInfo está definida.

### <a name="a-name11111111"></a><a name="1.11.1"/>1.11.1
* Correção de desempenho menor para Olá API CreateDocumentCollectionIfNotExistsAsync introduzido no 1.11.0.
* Correção de desempenho no hello SDK para cenários que envolvem um alto grau de solicitações simultâneas.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Suporte para Olá novas classes e métodos de tooprocess [alterar feed](change-feed.md) de documentos dentro de uma coleção.
* Suporte para continuação de consulta entre partições e algumas melhorias de desempenho para consultas entre partições.
* Acréscimo dos métodos CreateDatabaseIfNotExistsAsync e CreateDocumentCollectionIfNotExistsAsync.
* Suporte para LINQ para funções do sistema: IsDefined, IsNull e IsPrimitive.
* Corrigi para binplacing automática da pasta bin do Microsoft.Azure.Documents.ServiceInterop.dll e DocumentDB.Spatial.Sql.dll assemblies tooapplication ao usar o pacote do Nuget Olá com projetos com ferramentas do Project.
* Suporte para emitir rastreamentos ETW do lado cliente, que podem ser úteis em cenários de depuração.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Adicionado suporte a conectividade direta para coleções particionadas.
* Melhor desempenho para o nível de consistência envelhecimento limitado de saudação.
* Adicionado Polygon e LineString DataTypes ao especificar a política de indexação de coleção para consultas espaciais de isolamento geográfico.
* Adicionado suporte ao LINQ para StringEnumConverter, IsoDateTimeConverter e UnixDateTimeConverter ao converter predicados.
* Várias correções de bugs do SDK.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Corrigido um problema que causou Olá NotFoundException a seguir: Olá ler a sessão não está disponível para o token de sessão de entrada hello. Esta exceção ocorreu em alguns casos, ao consultar regiões leitura saudação de uma conta distribuídos geograficamente.
* Olá exposto ResponseStream propriedade Olá classe ResourceResponse, que permite que o fluxo subjacente do toohello acesso direto de uma resposta.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Olá modificado ResourceResponse, FeedResponse, StoredProcedureResponse e MediaResponse classes tooimplement hello correspondente a interface pública para que eles podem ser simulados para teste controlado por implantação (TDD).
* Foi corrigido um problema que causava um cabeçalho de chave de partição malformado ao usar um objeto JsonSerializerSettings personalizado para serialização de dados.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Corrigido um problema que causou toofail de consultas de longa execução com erro: token de autorização não é válido em Olá hora atual.
* Fixo de um problema que removido Olá SqlParameterCollection original de várias consultas superior/Ordenar por partição.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Adição de suporte a consultas paralelas de coleções particionadas.
* Adição de suporte a consultas ORDER BY e TOP entre partições para coleções particionadas.
* Olá fixa referências tooDocumentDB.Spatial.Sql.dll e Microsoft.Azure.Documents.ServiceInterop.dll que são necessárias ao fazer referência a um projeto de banco de dados do Azure Cosmos com um pacote de Nuget de banco de dados do Azure Cosmos toohello Referência ausentes.
* Parâmetros de toouse de capacidade de saudação fixo de tipos diferentes ao usar funções definidas pelo usuário em LINQ. 
* Corrigido um bug para contas global replicados onde Upsert chamadas estavam sendo direcionado tooread locais em vez de locais de gravação.
* Métodos adicionados toohello IDocumentClient interface ausentes: 
  * Método UpsertAttachmentAsync que usa mediaStream e opções como parâmetros
  * Método CreateAttachmentAsync que usa opções como um parâmetro
  * Método CreateOfferQuery que usa querySpec como um parâmetro.
* Classes públicas sem lacre que são expostas na interface de IDocumentClient hello.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Suporte adicionado Olá para contas do banco de dados de várias regiões.
* Suporte adicionado para repetição de solicitações limitadas.  Usuário pode personalizar o número de tentativas hello e tempo de espera máximo Olá Configurando a propriedade de ConnectionPolicy.RetryOptions hello.
* Adicionar uma nova interface IDocumentClient que define Olá assinaturas de todos os métodos e propriedades de DocumenClient.  Como parte dessa alteração, também alterado métodos de extensão que criar toomethods IQueryable e IOrderedQueryable em Olá classe DocumentClient em si.
* Adicionado Olá tooset opção configuração ServicePoint.ConnectionLimit para um determinado ponto de extremidade do banco de dados do Azure Cosmos Uri.  Use o valor padrão do ConnectionPolicy.MaxConnectionLimit toochange hello, que é definido too50.
* IPartitionResolver e sua implementação foram preteridos.  O suporte para IPartitionResolver agora é obsoleto. Recomendamos que você use Coleções Particionadas para taxa de transferência e armazenamento superiores.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Adicionada uma sobrecarga tooUri com base em método ExecuteStoredProcedureAsync que usa RequestOptions como um parâmetro.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Adicionado suporte para documentos em tempo de toolive (TTL).

### <a name="a-name163163"></a><a name="1.6.3"/>1.6.3
* Correção de um bug no pacote Nuget do SDK do .NET para empacotamento como parte de uma solução do Serviço de Nuvem do Azure.

### <a name="a-name162162"></a><a name="1.6.2"/>1.6.2
* Implementação de [coleções particionadas](partition-data.md) e [níveis de desempenho definidos pelo usuário](performance-levels.md). 

### <a name="a-name153153"></a><a name="1.5.3"/>1.5.3
* **[Fixa]**  Ponto de extremidade de consultar o Azure Cosmos DB gera: ' System.Net.Http.HttpRequestException: erro ao copiar o fluxo de conteúdo tooa'.

### <a name="a-name152152"></a><a name="1.5.2"/>1.5.2
* Expansão do suporte do LINQ, incluindo novos operadores para paginação, expressões condicionais e comparação de intervalo.
  * Levar operador tooenable comportamento SELECT TOP em LINQ
  * Comparações de intervalo CompareTo operador tooenable cadeia de caracteres
  * Operadores condicionais (?) e de união (??)
* **[Corrigido]** ArgumentOutOfRangeException ao combinar a projeção do Modelo com o Where-In na consulta LINQ. [#81](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* **[Fixa]**  Se Select não Olá Olá de expressão último provedor LINQ não assumido Nenhuma projeção e produzido SELECT * incorretamente.  [Nº 58](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Implementação de Upsert, adição de métodos UpsertXXXAsync
* Melhorias de desempenho de todas as solicitações
* Suporte ao provedor LINQ para os métodos conditional, coalesce e CompareTo em cadeias de caracteres
* **[Fixa]**  Implementar contém o método na lista toogenerate Olá SQL mesmo em IEnumerable e matriz--> provedor LINQ
* **[Fixa]**  BackoffRetryUtility usa Olá mesmo HttpRequestMessage em vez de criar um novo novamente
* **[Obsoleto]** UriFactory.CreateCollection--> agora deve usar UriFactory.CreateDocumentCollection

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1
* **[Corrigido]** Problemas de localização ao usar informações de cultura em outro idioma que não o inglês, como nl-NL, etc. 

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Adicionado roteamento baseado em ID
  * Novo tooassist UriFactory auxiliar com a construção de links de recursos baseada em ID
  * Novas sobrecargas em tootake DocumentClient no URI
* Adicionado IsValid() e IsValidDetailed () em LINQ para geoespaciais
* Suporte ao provedor LINQ aprimorado:
  * **Matemática** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan e Truncate
  * **Cadeia de caracteres** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString e ToUpper
  * **Array** - Concat, Contains, Count
  * **IN** 

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Suporte adicionado para modificar políticas de indexação.
  * Novo método ReplaceDocumentCollectionAsync no DocumentClient
  * Nova propriedade IndexTransformationProgress em ResourceResponse<T> para acompanhar o progresso em percentual de alterações na política de índice
  * DocumentCollection.IndexingPolicy agora é mutável
* Suporte adicionado para consulta e indexação espacial.
  * Novo namespace Microsoft.Azure.Documents.Spatial para serializar/desserializar tipos espaciais, como Ponto e Polígono
  * Nova classe SpatialIndex para indexação de dados GeoJSON armazenados no Cosmos DB
* **[Corrigido]** : consulta SQL incorreta gerada usando a expressão LINQ [Nº 38](https://github.com/Azure/azure-documentdb-net/issues/38).

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Adicionada dependência de Newtonsoft.Json v5.0.7.
* As alterações feitas toosupport Order By:
  
  * Suporte ao provedor LINQ para OrderBy() ou OrderByDescending()
  * Toosupport IndexingPolicy Order By 
    
    **Possível alteração interruptiva** 
    
    Se você tiver um código que coleções provisiona com uma política personalizada de indexação, o toobe de necessidades de código existente atualizado classe de novo IndexingPolicy toosupport hello. Se você não tem uma política personalizada de indexação, essa alteração não afeta você.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Adicionado suporte para particionamento de dados usando as novas classes de HashPartitionResolver e RangePartitionResolver hello e hello IPartitionResolver.
* Adicionada serialização DataContract.
* Adicionado suporte a GUID no provedor LINQ.
* Adicionado suporte a UDF no LINQ.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* SDK DO GA

## <a name="release--retirement-dates"></a>Datas de lançamento e desativação
A Microsoft fornece notificação pelo menos **12 meses** antes de desativar um SDK na versão mais recente/suporte ordem toosmooth Olá transição tooa.

Novos recursos e funcionalidade e as otimizações são adicionadas apenas toohello atual SDK, como tal, é recomendável que você sempre atualize toohello mais recente versão do SDK mais cedo possível. 

Qualquer tooAzure solicitações Cosmos de banco de dados usando um SDK obsoleto são rejeitados pelo serviço de saudação.

<br/>

| Versão | Data do lançamento | Data de desativação |
| --- | --- | --- |
| [1.17.0](#1.17.0) |10 de agosto de 2017 |--- |
| [1.16.1](#1.16.1) |7 de agosto de 2017 |--- |
| [1.16.0](#1.16.0) |2 de agosto de 2017 |--- |
| [1.15.0](#1.15.0) |30 de junho de 2017 |--- |
| [1.14.1](#1.14.1) |23 de maio de 2017 |--- |
| [1.14.0](#1.14.0) |10 de maio de 2017 |--- |
| [1.13.4](#1.13.4) |9 de maio de 2017 |--- |
| [1.13.3](#1.13.3) |6 de maio de 2017 |--- |
| [1.13.2](#1.13.2) |19 de abril de 2017 |--- |
| [1.13.1](#1.13.1) |29 de março de 2017 |--- |
| [1.13.0](#1.13.0) |24 de março de 2017 |--- |
| [1.12.2](#1.12.2) |20 de março de 2017 |--- |
| [1.12.1](#1.12.1) |14 de março de 2017 |--- |
| [1.12.0](#1.12.0) |15 de fevereiro de 2017 |--- |
| [1.11.4](#1.11.4) |06 de fevereiro de 2017 |--- |
| [1.11.3](#1.11.3) |26 de janeiro de 2017 |--- |
| [1.11.1](#1.11.1) |21 de dezembro de 2016 |--- |
| [1.11.0](#1.11.0) |08 de dezembro de 2016 |--- |
| [1.10.0](#1.10.0) |27 de setembro de 2016 |--- |
| [1.9.5](#1.9.5) |1º de setembro de 2016 |--- |
| [1.9.4](#1.9.4) |24 de agosto de 2016 |--- |
| [1.9.3](#1.9.3) |15 de agosto de 2016 |--- |
| [1.9.2](#1.9.2) |23 de julho de 2016 |--- |
| [1.8.0](#1.8.0) |14 de junho de 2016 |--- |
| [1.7.1](#1.7.1) |6 de maio de 2016 |--- |
| [1.7.0](#1.7.0) |26 de abril de 2016 |--- |
| [1.6.3](#1.6.3) |08 de abril de 2016 |--- |
| [1.6.2](#1.6.2) |29 de março de 2016 |--- |
| [1.5.3](#1.5.3) |19 de fevereiro de 2016 |--- |
| [1.5.2](#1.5.2) |14 de dezembro de 2015 |--- |
| [1.5.1](#1.5.1) |23 de novembro de 2015 |--- |
| [1.5.0](#1.5.0) |5 de outubro de 2015 |--- |
| [1.4.1](#1.4.1) |25 de agosto de 2015 |--- |
| [1.4.0](#1.4.0) |13 de agosto de 2015 |--- |
| [1.3.0](#1.3.0) |5 de agosto de 2015 |--- |
| [1.2.0](#1.2.0) |6 de julho de 2015 |--- |
| [1.1.0](#1.1.0) |30 de abril de 2015 |--- |
| [1.0.0](#1.0.0) |8 de abril de 2015 |--- |


## <a name="faq"></a>Perguntas frequentes
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Consulte também
toolearn mais sobre o banco de dados do Cosmos, consulte [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de serviço. 

