---
title: aaaAzure Cosmos DB Node. js API, SDK e recursos | Microsoft Docs
description: "Saiba tudo sobre Olá Node. js API e o SDK, incluindo datas de lançamento, datas de desativação e as alterações feitas entre cada versão do hello Azure Cosmos DB Node. js SDK."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a>SDK de Node.js do Azure Cosmos DB: Notas de versão e recursos
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

<tr><td>**Baixar o SDK**</td><td>[NPM](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td>**Documentação da API**</td><td>[Documentação de referência da API do Node.js](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td>**Instruções de instalação do SDK**</td><td>[Instruções de instalação](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td>**Contribuir tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td>**Exemplos**</td><td>[Exemplos de código do Node.js](documentdb-nodejs-samples.md)</td></tr>

<tr><td>**Tutorial de introdução**</td><td>[Introdução ao Olá Node. js SDK](documentdb-nodejs-get-started.md)</td></tr>

<tr><td>**Tutorial do aplicativo Web**</td><td>[Criar um aplicativo web Node.js usando o Azure Cosmos DB](documentdb-nodejs-application.md)</td></tr>

<tr><td>**Plataforma atual com suporte**</td><td> 
[Node.js v6.x](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[Node.js v4.2.0](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[Node.js v0.12](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de versão

### <a name="1.12.2"/>1.12.2</a>
*   documentação do npm corrigida.

### <a name="1.12.1"/>1.12.1</a>
* Correção de um bug no executeStoredProcedure, em que documentos envolvidos tinham caracteres especiais Unicode (LS, PS).
* Correção de bug na manipulação de documentos com caracteres de Unicode na chave de partição hello.
* Suporte fixado para criar coleções com mídia de nome hello. Problema nº 114 do Github.
* Suporte fixo para o token de autorização de permissão. Problema nº 178 do Github.

### <a name="1.12.0"/>1.12.0</a>
* Foi adicionado suporte a um novo [nível de consistência](consistency-levels.md) chamado ConsistentPrefix.
* Foi adicionado suporte para UriFactory.
* Correção de um bug de suporte ao Unicode. Problema nº 171 do Github.

### <a name="1.11.0"/>1.11.0</a>
* Suporte adicionado Olá para consultas de agregação (COUNT, MIN, MAX, SUM e AVG).
* Opção de saudação adicionado para controlar o grau de paralelismo de várias consultas de partição.
* Opção de saudação adicionado para desabilitar a verificação de SSL durante a execução no emulador do Azure Cosmos banco de dados.
* Reduzida a taxa de transferência mínima em coleções particionadas de 10,100 RU/s too2500 RU/s.
* Bug token de continuação de Olá fixa para coleção única partição. Problema nº 107 do Github.
* Bug de executeStoredProcedure Olá fixa no tratamento 0 como parâmetro único. Problema nº 155 do Github.

### <a name="1.10.2"/>1.10.2</a>
* Versão do agente de usuário fixo cabeçalho tooinclude Olá SDK.
* Limpeza de código secundária.

### <a name="1.10.1"/>1.10.1</a>
* Desabilitar a verificação de SSL ao usar Olá SDK tootarget Olá emulator(hostname=localhost).
* Adicionado suporte para habilitar o registro em log de script durante a execução do procedimento armazenado.

### <a name="1.10.0"/>1.10.0</a>
* Adicionado suporte para várias consultas paralelas de partição.
* Adição de suporte a consultas TOP/ORDER BY de coleções particionadas.

### <a name="1.9.0"/>1.9.0</a>
* Suporte à política de repetições para solicitações limitadas adicionado. (As solicitações limitadas recebem uma exceção muito grande de taxa de solicitação, código de erro 429.) Por padrão, banco de dados do Azure Cosmos repete nove vezes para cada solicitação quando o código de erro 429 é encontrado, para respeitar o tempo de retryAfter saudação no cabeçalho de resposta de saudação. Um intervalo de tempo fixo de repetição agora pode ser definido como parte da saudação RetryOptions propriedade no objeto de ConnectionPolicy Olá se você desejar tooignore Olá retryAfter tempo retornado pelo servidor entre as tentativas de saudação. Banco de dados do Azure Cosmos agora aguarda um máximo de 30 segundos para cada solicitação que está sendo limitado (independentemente da contagem de repetição) e retorna a resposta de saudação com código de erro 429. Também pode ser substituído neste momento no hello RetryOptions propriedade no objeto ConnectionPolicy.
* Cosmos DB agora retorna x-ms-acelerador--contagem de repetição e x-ms-throttle-retry-wait-time-ms como cabeçalhos de resposta de saudação na limitação de saudação de toodenote cada solicitação repetir contagem e hello tempo cumulativo Olá solicitação espera entre as tentativas de saudação.
* Olá classe RetryOptions foi adicionado, expondo a propriedade de RetryOptions Olá na classe de ConnectionPolicy Olá que pode ser usado toooverride alguns padrão Olá opções de repetição.

### <a name="1.8.0"/>1.8.0</a>
* Suporte adicionado Olá para contas do banco de dados de várias regiões.

### <a name="1.7.0"/>1.7.0</a>
* Olá adicionado suporte para o recurso de tooLive(TTL) de tempo para documentos.

### <a name="1.6.0"/>1.6.0</a>
* Implementação de [coleções particionadas](partition-data.md) e [níveis de desempenho definidos pelo usuário](performance-levels.md).

### <a name="1.5.6"/>1.5.6</a>
* Correção do bug RangePartitionResolver.resolveForRead onde ele não estava retornando links devido concat incorreta de tooa de resultados.

### <a name="1.5.5"/>1.5.5</a>
* hashPartitionResolver resolveForRead() corrigido: quando nenhuma chave de partição fornecida estava emitindo exceção, em vez de retornar uma lista de todos os links registrados.

### <a name="1.5.4"/>1.5.4</a>
* Corrige o problema [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -agente dedicado de HTTPS: evitar modificar globais do agente para fins de banco de dados do Azure Cosmos hello. Use um agente dedicado para todas as solicitações do lib hello.

### <a name="1.5.3"/>1.5.3</a>
* Corrige o problema [nº 81](https://github.com/Azure/azure-documentdb-node/issues/81) — trate corretamente os traços em IDs de mídia.

### <a name="1.5.2"/>1.5.2</a>
* Corrige o problema [nº 95](https://github.com/Azure/azure-documentdb-node/issues/95) — aviso de perda do ouvinte EventEmitter.

### <a name="1.5.1"/>1.5.1</a>
* Corrige o problema [&#92;](https://github.com/Azure/azure-documentdb-node/issues/90) -renomear a pasta Hash toohash para sistemas diferencia maiusculas de minúsculas.

### <a name="1.5.0"/>1.5.0</a>
* Implemente o suporte a fragmentação ao adicionar os resolvedores de partição de hash e de intervalo.

### <a name="1.4.0"/>1.4.0</a>
* Implementar o Upsert. Novos métodos upsertXXX em documentClient.

### <a name="1.3.0"/>1.3.0</a>
* Números de versão toobring ignorada no alinhamento com outros SDKs.

### <a name="1.2.2"/>1.2.2</a>
* Divisão p promete repositório toonew do wrapper.
* Atualize o arquivo toopackage do registro npm.

### <a name="1.2.1"/>1.2.1</a>
* Implementa o roteamento com base em ID.
* Corrige o problema [nº 49](https://github.com/Azure/azure-documentdb-node/issues/49) - a propriedade atual está em conflito com o método atual().

### <a name="1.2.0"/>1.2.0</a>
* Suporte adicionado para índice geoespaciais.
* Valida a propriedade de ID de todos os recursos. As IDs de recursos não podem conter caracteres ?, /, #, &#47;&#47; ou terminar com um espaço.
* Adiciona novo tooResourceResponse "andamento de transformação de índice" de cabeçalho.

### <a name="1.1.0"/>1.1.0</a>
* Implementa a política de indexação V2.

### <a name="1.0.3"/>1.0.3</a>
* Problema [&#40;](https://github.com/Azure/azure-documentdb-node/issues/40) - implementado eslint e Assistente de configurações no núcleo do hello e promise SDK.

### <a name="1.0.2"/>1.0.2</a>
* Problema [nº 45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promessa de wrapper não inclui o cabeçalho com erro.

### <a name="1.0.1"/>1.0.1</a>
* Implementado tooquery capacidade conflitos adicionando readConflicts, readConflictAsync e queryConflicts.
* Documentação da API atualizada.
* Problema [nº 41](https://github.com/Azure/azure-documentdb-node/issues/41) - Erro client.createDocumentAsync.

### <a name="1.0.0"/>1.0.0</a>
* SDK DO GA.

## <a name="release--retirement-dates"></a>Datas de lançamento e desativação
A Microsoft fornece notificação pelo menos **12 meses** antes de desativar um SDK na versão mais recente/suporte ordem toosmooth Olá transição tooa.

Novos recursos e funcionalidade e as otimizações são adicionadas apenas toohello atual SDK, como tal, é recomendável que você sempre atualize toohello mais recente versão do SDK mais cedo possível.

Qualquer solicitação tooCosmos banco de dados usando um SDK obsoleto é rejeitados pelo serviço de saudação.

<br/>

| Versão | Data do lançamento | Data de desativação |
| --- | --- | --- |
| [1.12.2](#1.12.2) |10 de agosto de 2017 |--- |
| [1.12.1](#1.12.1) |10 de agosto de 2017 |--- |
| [1.12.0](#1.12.0) |10 de maio de 2017 |--- |
| [1.11.0](#1.11.0) |16 de março de 2017 |--- |
| [1.10.2](#1.10.2) |27 de janeiro de 2017 |--- |
| [1.10.1](#1.10.1) |22 de dezembro de 2016 |--- |
| [1.10.0](#1.10.0) |3 de outubro de 2016 |--- |
| [1.9.0](#1.9.0) |07 de julho de 2016 |--- |
| [1.8.0](#1.8.0) |14 de junho de 2016 |--- |
| [1.7.0](#1.7.0) |26 de abril de 2016 |--- |
| [1.6.0](#1.6.0) |29 de março de 2016 |--- |
| [1.5.6](#1.5.6) |08 de março de 2016 |--- |
| [1.5.5](#1.5.5) |02 de fevereiro de 2016 |--- |
| [1.5.4](#1.5.4) |1 de fevereiro de 2016 |--- |
| [1.5.2](#1.5.2) |26 de janeiro de 2016 |--- |
| [1.5.2](#1.5.2) |22 de janeiro de 2016 |--- |
| [1.5.1](#1.5.1) |4 de janeiro de 2016 |--- |
| [1.5.0](#1.5.0) |31 de dezembro de 2015 |--- |
| [1.4.0](#1.4.0) |06 de outubro de 2015 |--- |
| [1.3.0](#1.3.0) |06 de outubro de 2015 |--- |
| [1.2.2](#1.2.2) |10 de setembro de 2015 |--- |
| [1.2.1](#1.2.1) |15 de agosto de 2015 |--- |
| [1.2.0](#1.2.0) |5 de agosto de 2015 |--- |
| [1.1.0](#1.1.0) |9 de julho de 2015 |--- |
| [1.0.3](#1.0.3) |04 de junho de 2015 |--- |
| [1.0.2](#1.0.2) |23 de maio de 2015 |--- |
| [1.0.1](#1.0.1) |15 de maio de 2015 |--- |
| [1.0.0](#1.0.0) |8 de abril de 2015 |--- |

## <a name="faq"></a>Perguntas frequentes
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Consulte também
toolearn mais sobre o banco de dados do Cosmos, consulte [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de serviço.

