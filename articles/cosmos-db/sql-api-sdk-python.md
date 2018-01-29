---
title: 'Azure Cosmos DB: SQL Python API, SDK e recursos | Microsoft Docs'
description: "Saiba tudo sobre o SDK e a API do SQL Python, incluindo datas de lançamento, datas de desativação e alterações feitas entre cada versão do SDK do Python para o Azure Cosmos DB."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 1/4/2018
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6801c5b62be08e4dcb32ad342b15e9ad3f3e20a8
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="azure-cosmos-db-python-sdk-for-sql-api-release-notes-and-resources"></a>SDK do Python do Azure Cosmos DB para a API do SQL: notas de versão e recursos
> [!div class="op_single_selector"]
> * [.NET](sql-api-sdk-dotnet.md)
> * [Feed de alterações do .NET](sql-api-sdk-dotnet-changefeed.md)
> * [.NET Core](sql-api-sdk-dotnet-core.md)
> * [Node.js](sql-api-sdk-node.md)
> * [Java](sql-api-sdk-java.md)
> * [Python](sql-api-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Provedor de recursos REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

<table>

<tr><td>**Baixar o SDK**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**Documentação da API**</td><td>[Documentação de referência da API do Python](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**Instruções de instalação do SDK**</td><td>[Instruções de instalação do SDK do Python](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**Contribuir para o SDK**</td><td>[Github](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**Introdução**</td><td>[Introdução ao SDK do Python](sql-api-python-application.md)</td></tr>

<tr><td>**Plataforma atual com suporte**</td><td>[Python 2.7](https://www.python.org/downloads/) e [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de versão
### <a name="a-name231231"></a><a name="2.3.1"/>2.3.1
* Documentação atualizada para fazer referência ao Azure Cosmos DB em vez do Azure DocumentDB.

### <a name="a-name230230"></a><a name="2.3.0"/>2.3.0
* Esta versão do SDK requer a versão mais recente do Emulador do Azure Cosmos DB disponível para fazer o download em https://aka.ms/cosmosdb-emulator.

### <a name="a-name221221"></a><a name="2.2.1"/>2.2.1
* Correção de bug de dicionário de agregação.
* Correção de bug de barras de filtragem no link de recursos.
* Testes adicionados para codificação Unicode.

### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* Adição de suporte a um novo nível de consistência chamado ConsistentPrefix.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* Suporte adicionado para consultas de agregação (COUNT, MIN, MAX, SUM e AVG).
* Adição de uma opção para desabilitar a verificação do SSL quando executada no Emulador do Cosmos DB.
* Removida a restrição do módulo de solicitações dependentes para serem exatamente 2.10.0.
* Taxa de transferência mínima reduzida em coleções particionadas de 10.100 RU/s a 2500 RU/s.
* Adicionado suporte para habilitar o registro em log de script durante a execução do procedimento armazenado.
* Versão da API REST aumentado para '2017-01-19' nesta versão.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Alterações editoriais feitas a comentários de documentação.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Suporte ao Python 3.5 adicionado.
* Suporte ao pool de conexões usando um módulo de solicitações adicionado.
* Suporte à consistência da sessão adicionado.
* Suporte às consultas TOP/ORDERBY de coleções particionadas adicionado.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Suporte à política de repetições para solicitações limitadas adicionado. (As solicitações limitadas recebem uma exceção muito grande de taxa de solicitação, código de erro 429.) Por padrão, o Azure Cosmos DB tenta cada solicitação novamente nove vezes quando o código de erro 429 é encontrado, respeitando o tempo retryAfter no cabeçalho de resposta. Um intervalo de repetição fixo agora poderá ser definido como parte da propriedade RetryOptions no objeto ConnectionPolicy, se você quiser ignorar o tempo retryAfter retornado pelo servidor entre as repetições. O Azure Cosmos DB agora aguarda um período máximo de 30 segundos para cada solicitação que está sendo limitada (independentemente da contagem de repetições) e retorna a resposta com o código de erro 429. Esse tempo também pode ser substituído na propriedade RetryOptions, no objeto ConnectionPolicy.
* O Cosmos DB agora retorna x-ms-throttle-retry-count e x-ms-throttle-retry-wait-time-ms como os cabeçalhos de resposta em cada solicitação para indicar a contagem de repetições restritas e o tempo cumulativo que a solicitação aguardou entre as tentativas.
* A classe RetryPolicy foi removida e a propriedade correspondente (retry_policy) foi exposta na classe document_client. Como alternativa, foi introduzida uma classe RetryOptions, expondo a propriedade RetryOptions na classe ConnectionPolicy, que pode ser usada para substituir algumas das opções de repetição padrão.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Suporte adicionado para contas de banco de dados de várias regiões.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Adicionado o suporte para o recurso TTL (tempo de vida) para documentos.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Correções de bugs relacionadas ao particionamento no lado do servidor a fim de permitir caracteres especiais no caminho de partitionkey.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Implementação de [coleções particionadas](partition-data.md) e [níveis de desempenho definidos pelo usuário](performance-levels.md). 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Adicionar resolvedores de hash e intervalo para ajudar com a fragmentação de arquivos em várias partições.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Implementar o Upsert. Novos métodos UpsertXXX adicionados para dar suporte ao recurso Upsert.
* Implementar o roteamento com base em ID. Nenhuma alteração pública de API, todas as alterações são internas.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Oferece suporte ao índice Geoespacial.
* Valida a propriedade de ID de todos os recursos. As IDs de recursos não podem conter caracteres ?, /, #, \, ou terminar com um espaço.
* Adiciona o novo cabeçalho "andamento de transformação do índice" ao ResourceResponse.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implementa a política de indexação V2.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* Oferece suporte à conexão de proxy.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* SDK DO GA.

## <a name="release--retirement-dates"></a>Datas de lançamento e de baixa
A Microsoft notifica pelo menos **12 meses** antes de desativar um SDK, a fim de realizar uma transição tranquila para uma versão mais recente/com suporte.

Os novos recursos, funcionalidades e otimizações são adicionados apenas ao SDK atual. Portanto, recomendamos que você atualize sempre que possível para a versão do SDK mais recente. 

Qualquer solicitação feita ao Cosmos DB com o uso de um SDK desativado é rejeitada pelo serviço.

> [!WARNING]
> Todas as versões do SDK do Azure SQL para Python anteriores à versão **1.0.0** foram desativadas em **29 de fevereiro de 2016**. 
> 
> 

<br/>

| Versão | Data do lançamento | Data de desativação |
| --- | --- | --- |
| [2.3.1](#2.3.1) |21 de dezembro de 2017 |--- |
| [2.3.0](#2.3.0) |10 de novembro, 2017 |--- |
| [2.2.1](#2.2.1) |29 de setembro de 2017 |--- |
| [2.2.0](#2.2.0) |10 de maio de 2017 |--- |
| [2.1.0](#2.1.0) |1º de maio de 2017 |--- |
| [2.0.1](#2.0.1) |30 de outubro de 2016 |--- |
| [2.0.0](#2.0.0) |29 de setembro de 2016 |--- |
| [1.9.0](#1.9.0) |07 de julho de 2016 |--- |
| [1.8.0](#1.8.0) |14 de junho de 2016 |--- |
| [1.7.0](#1.7.0) |26 de abril de 2016 |--- |
| [1.6.1](#1.6.1) |08 de abril de 2016 |--- |
| [1.6.0](#1.6.0) |29 de março de 2016 |--- |
| [1.5.0](#1.5.0) |03 de janeiro de 2016 |--- |
| [1.4.2](#1.4.2) |06 de outubro de 2015 |--- |
| [1.4.1](#1.4.1) |06 de outubro de 2015 |--- |
| [1.2.0](#1.2.0) |06 de agosto de 2015 |--- |
| [1.1.0](#1.1.0) |9 de julho de 2015 |--- |
| [1.0.1](#1.0.1) |25 de maio de 2015 |--- |
| [1.0.0](#1.0.0) |7 de abril de 2015 |--- |
| 0.9.4-prelease |14 de janeiro de 2015 |29 de fevereiro de 2016 |
| 0.9.3-prelease |09 de dezembro de 2014 |29 de fevereiro de 2016 |
| 0.9.2-prelease |25 de novembro de 2014 |29 de fevereiro de 2016 |
| 0.9.1-prelease |23 de setembro de 2014 |29 de fevereiro de 2016 |
| 0.9.0-prelease |21 de agosto de 2014 |29 de fevereiro de 2016 |

## <a name="faq"></a>Perguntas frequentes
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Consulte também
Para saber mais sobre o Cosmos DB, consulte a página de serviço do [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). 

