---
title: 'Azure Cosmos DB: API, SDK e recursos em Java do DocumentDB, | Microsoft Docs'
description: "Saiba tudo sobre Olá API Java e o SDK, incluindo datas de lançamento, datas de desativação e as alterações feitas entre cada versão do hello Azure Cosmos DB documentos Java SDK."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a>Azure Cosmos DB: notas de versão e recursos do SDK Java do DocumentDB
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

<tr><td>**Baixe o SDK**</td><td>[Maven](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td>**Documentação da API**</td><td>[Documentação de referência de API Java](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td>**Contribuir tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td>**Introdução**</td><td>[Introdução ao SDK do Java de saudação](documentdb-java-get-started.md)</td></tr>

<tr><td>**Tutorial do aplicativo Web**</td><td>[Desenvolvimento de aplicativos Web com o Azure Cosmos DB](documentdb-java-application.md)</td></tr>

<tr><td>**Tempo de execução atual com suporte**</td><td>[JDK 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de versão

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Divide toorequest correções de bugs críticos de processamento durante a partição.
* Corrigido um problema com hello forte e BoundedStaleness níveis de consistência.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Adição de suporte a um novo nível de consistência chamado ConsistentPrefix.
* Corrigido um bug na leitura da coleção no modo de sessão.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Suporte habilitado para coleção particionada com 2.500 RU/s e escala em incrementos de 100 RU/s.
* Correção de bug no assembly nativo hello, que pode causar exceção NullRef em algumas consultas.

### <a name="a-name196196"></a><a name="1.9.6"/>1.9.6
* Correção de bug na configuração do mecanismo de consulta Olá que pode causar exceções para consultas no modo de Gateway.
* Corrigidos alguns bugs no contêiner de sessão Olá que podem causar uma exceção "Recurso proprietário não encontrado" de solicitações imediatamente após a criação de coleção.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Suporte adicionado para consultas de agregação (COUNT, MIN, MAX, SUM e AVG). Veja [Suporte de agregação](documentdb-sql-query.md#Aggregates).
* Adicionado suporte para alteração de feed.
* Adicionado suporte para informações de cota de coleção por meio de RequestOptions.setPopulateQuotaInfo.
* Foi adicionado suporte para o log de script de procedimento armazenado por meio de RequestOptions.setScriptLoggingEnabled.
* Corrigido um bug em que a consulta no modo de DirectHttps pode travar ao encontrar falhas de limitação.
* Corrigido um bug no modo de sessão de consistência.
* Corrigido um erro que pode causar a NullReferenceException no HttpContext quando a taxa de solicitação é alta.
* Desempenho aprimorado de modo DirectHttps.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Acréscimo de suporte a proxy com base em instância simples do cliente com API ConnectionPolicy.setProxy().
* Adicionado DocumentClient.close() tooproperly desligamento DocumentClient instância da API.
* Desempenho aprimorado de consultas no modo de conectividade direta derivando plano de consulta de saudação do assembly nativo de saudação em vez da saudação Gateway.
* Definir FAIL_ON_UNKNOWN_PROPERTIES = false para que os usuários não precisam toodefine JsonIgnoreProperties em seu POJO.
* Registro em log refatorado toouse SLF4J.
* Alguns outros bugs corrigidos no leitor de consistência.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Correção de bug na conexão Olá gerenciamento perdas de conexão tooprevent no modo de conectividade direta.
* Correção de bug na consulta TOP Olá onde ele pode gerar exceção NullReferenece.
* Melhor desempenho, reduzindo o número de saudação da chamada de rede de caches internos Olá.
* Acréscimo do código de status, ActivityID e URI de Solicitação em DocumentClientException para melhor solução de problemas.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Corrigido um problema no gerenciamento de conexão de saudação de estabilidade.

### <a name="a-name191191"></a><a name="1.9.1"/>1.9.1
* Adicionado suporte para o nível de consistência BoundedStaleness.
* Adicionado suporte para conectividade direta para operações CRUD para coleções particionadas.
* Corrigido um erro na consulta de um banco de dados com SQL.
* Correção de bug no cache de sessão Olá onde o token de sessão pode ser definido incorretamente.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Adicionado suporte para várias consultas paralelas de partição.
* Adição de suporte a consultas TOP/ORDER BY de coleções particionadas.
* Adicionado suporte para consistência forte.
* Adicionado suporte para solicitações com base em nome ao usar a conectividade direta.
* Toomake fixa ActivityId permanecer consistente em todas as tentativas de solicitação.
* Correção de bug relacionado toohello cache de sessão ao recriar uma coleção com hello mesmo nome.
* Adicionado Polygon e LineString DataTypes ao especificar a política de indexação de coleção para consultas espaciais de isolamento geográfico.
* Problemas corrigidos com Java Doc para Java 1.8.

### <a name="a-name181181"></a><a name="1.8.1"/>1.8.1
* Correção de bug no PartitionKeyDefinitionMap toocache coleções de partição única e não fazer extra buscar partição solicitações de chave.
* Corrigido uma repetição do bug toonot quando é fornecido um valor de chave de partição incorreto.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Suporte adicionado Olá para contas do banco de dados de várias regiões.
* Adicionado suporte para repetição automática em solicitações limitadas com hello de toocustomize opções max tentativas e repita máx de tempo de espera.  Consulte RetryOptions e ConnectionPolicy.getRetryOptions().
* IPartitionResolver preterido com base no código de particionamento personalizado. Use coleções particionadas para uma taxa de transferência e armazenamento superiores.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Adicionado suporte à política de repetição para limitação.  

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Adicionado suporte para documentos em tempo de toolive (TTL).

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Implementação de [coleções particionadas](partition-data.md) e [níveis de desempenho definidos pelo usuário](performance-levels.md).

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* Correção de bug em valores de hash toogenerate HashPartitionResolver em little endian toobe consistente com outros SDKs.

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Adicionar & intervalo de Hash tooassist de resolvedores de partição com aplicativos de fragmentação por várias partições.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Implementar o Upsert. Novos métodos upsertXXX adicionaram toosupport Upsert recurso.
* Implementar o roteamento com base em ID. Nenhuma alteração pública de API, todas as alterações são internas.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Versão ignorada toobring o número de versão no alinhamento com outros SDKs

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Oferece suporte ao Índice Geoespacial.
* Valida a propriedade de ID de todos os recursos. As IDs de recursos não podem conter caracteres ?, /, #, \, ou terminar com um espaço.
* Adiciona novo tooResourceResponse "andamento de transformação de índice" de cabeçalho.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implementa a política de indexação V2

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* SDK DO GA

## <a name="release--retirement-dates"></a>Datas de lançamento e desativação
A Microsoft fornecerá notificação pelo menos **12 meses** antes de desativar um SDK na versão mais recente/suporte ordem toosmooth Olá transição tooa.

Novos recursos e funcionalidade e as otimizações são adicionadas apenas toohello atual SDK, como tal, é recomendável que você sempre atualize toohello mais recente versão do SDK mais cedo possível.

TooCosmos qualquer solicitação usando um SDK obsoleto do banco de dados serão rejeitados pelo serviço de saudação.

> [!WARNING]
> Todas as versões do hello SDK do DocumentDB para tooversion anterior Java **1.0.0** será desativado em **29 de fevereiro de 2016**.
> 
> 

<br/>

| Versão | Data do lançamento | Data de desativação |
| --- | --- | --- |
| [1.12.0](#1.12.0) |11 de julho de 2017 |--- |
| [1.11.0](#1.11.0) |10 de maio de 2017 |--- |
| [1.10.0](#1.10.0) |11 de março de 2017 |--- |
| [1.9.6](#1.9.6) |21 de fevereiro de 2017 |--- |
| [1.9.5](#1.9.5) |31 de janeiro de 2017 |--- |
| [1.9.4](#1.9.4) |24 de novembro de 2016 |--- |
| [1.9.3](#1.9.3) |30 de outubro de 2016 |--- |
| [1.9.2](#1.9.2) |28 de outubro de 2016 |--- |
| [1.9.1](#1.9.1) |26 de outubro de 2016 |--- |
| [1.9.0](#1.9.0) |3 de outubro de 2016 |--- |
| [1.8.1](#1.8.1) |30 de junho de 2016 |--- |
| [1.8.0](#1.8.0) |14 de junho de 2016 |--- |
| [1.7.1](#1.7.1) |30 de abril de 2016 |--- |
| [1.7.0](#1.7.0) |27 de abril de 2016 |--- |
| [1.6.0](#1.6.0) |29 de março de 2016 |--- |
| [1.5.1](#1.5.1) |31 de dezembro de 2015 |--- |
| [1.5.0](#1.5.0) |4 de dezembro de 2015 |--- |
| [1.4.0](#1.4.0) |5 de outubro de 2015 |--- |
| [1.3.0](#1.3.0) |5 de outubro de 2015 |--- |
| [1.2.0](#1.2.0) |5 de agosto de 2015 |--- |
| [1.1.0](#1.1.0) |9 de julho de 2015 |--- |
| [1.0.1](#1.0.1) |12 de maio de 2015 |--- |
| [1.0.0](#1.0.0) |7 de abril de 2015 |--- |
| 0.9.5-prelease |9 de março de 2015 |29 de fevereiro de 2016 |
| 0.9.4-prelease |17 de fevereiro de 2015 |29 de fevereiro de 2016 |
| 0.9.3-prelease |13 de janeiro de 2015 |29 de fevereiro de 2016 |
| 0.9.2-prelease |19 de dezembro de 2014 |29 de fevereiro de 2016 |
| 0.9.1-prelease |19 de dezembro de 2014 |29 de fevereiro de 2016 |
| 0.9.0-prelease |10 de dezembro de 2014 |29 de fevereiro de 2016 |

## <a name="faq"></a>Perguntas frequentes
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Consulte também
toolearn mais sobre o banco de dados do Cosmos, consulte [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de serviço.

