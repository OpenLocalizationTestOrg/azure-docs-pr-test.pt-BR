---
title: aaaAzure Cosmos DB Python API, SDK e recursos | Microsoft Docs
description: "Saiba tudo sobre Olá Python API e o SDK, incluindo datas de lançamento, datas de desativação e as alterações feitas entre cada versão da saudação do SDK do Azure Cosmos DB Python."
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
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a>SDK do Python do Azure Cosmos DB: notas de versão e recursos
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

<tr><td>**Baixar o SDK**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**Documentação da API**</td><td>[Documentação de referência da API do Python](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**Instruções de instalação do SDK**</td><td>[Instruções de instalação do SDK do Python](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**Contribuir tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**Introdução**</td><td>[Introdução ao SDK de Python de saudação](documentdb-python-application.md)</td></tr>

<tr><td>**Plataforma atual com suporte**</td><td>[Python 2.7](https://www.python.org/downloads/) e [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de versão
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* Adição de suporte a um novo nível de consistência chamado ConsistentPrefix.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* Suporte adicionado para consultas de agregação (COUNT, MIN, MAX, SUM e AVG).
* Adição de uma opção para desabilitar a verificação do SSL quando executada no Emulador do Cosmos DB.
* Remover restrição de saudação do módulo de solicitações dependentes toobe 2.10.0 exatamente.
* Reduzida a taxa de transferência mínima em coleções particionadas de 10,100 RU/s too2500 RU/s.
* Adicionado suporte para habilitar o registro em log de script durante a execução do procedimento armazenado.
* Versão da API REST muito aumentado ' 2017-01-19' com esta versão.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Fez alterações editoriais toodocumentation comentários.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Suporte ao Python 3.5 adicionado.
* Suporte ao pool de conexões usando um módulo de solicitações adicionado.
* Suporte à consistência da sessão adicionado.
* Suporte às consultas TOP/ORDERBY de coleções particionadas adicionado.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Suporte à política de repetições para solicitações limitadas adicionado. (As solicitações limitadas recebem uma exceção muito grande de taxa de solicitação, código de erro 429.) Por padrão, banco de dados do Azure Cosmos repete nove vezes para cada solicitação quando o código de erro 429 é encontrado, para respeitar o tempo de retryAfter saudação no cabeçalho de resposta de saudação. Um intervalo de tempo fixo de repetição agora pode ser definido como parte da saudação RetryOptions propriedade no objeto de ConnectionPolicy Olá se você desejar tooignore Olá retryAfter tempo retornado pelo servidor entre as tentativas de saudação. Banco de dados do Azure Cosmos agora aguarda um máximo de 30 segundos para cada solicitação que está sendo limitado (independentemente da contagem de repetição) e retorna a resposta de saudação com código de erro 429. Neste momento também pode ser substituída em Olá RetryOptions propriedade no objeto ConnectionPolicy.
* Cosmos DB agora retorna x-ms-acelerador--contagem de repetição e x-ms-throttle-retry-wait-time-ms como cabeçalhos de resposta de saudação em cada Acelerador de saudação solicitação toodenote tempo de nova tentativa contagem e hello cummulative Olá solicitação espera entre as tentativas de saudação.
* Classe de RetryPolicy Olá removido e propriedade correspondente da saudação (retry_policy) exposto na classe de document_client hello e introduzida em vez disso, uma classe RetryOptions expondo a propriedade de RetryOptions Olá na classe ConnectionPolicy que pode ser usado toooverride alguns dos padrão Olá opções de repetição.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Suporte adicionado Olá para contas do banco de dados de várias regiões.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Olá adicionado suporte para o recurso de tooLive(TTL) de tempo para documentos.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Correções de bug relacionado lado tooserver particionamento tooallow de caracteres especiais no caminho de partitionkey.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Implementação de [coleções particionadas](partition-data.md) e [níveis de desempenho definidos pelo usuário](performance-levels.md). 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Adicionar & intervalo de Hash tooassist de resolvedores de partição com aplicativos de fragmentação por várias partições.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Implementar o Upsert. Novos métodos UpsertXXX adicionaram toosupport Upsert recurso.
* Implementar o roteamento com base em ID. Nenhuma alteração pública de API, todas as alterações são internas.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Oferece suporte ao índice Geoespacial.
* Valida a propriedade de ID de todos os recursos. As IDs de recursos não podem conter caracteres ?, /, #, \, ou terminar com um espaço.
* Adiciona novo tooResourceResponse "andamento de transformação de índice" de cabeçalho.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implementa a política de indexação V2.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* Oferece suporte à conexão de proxy.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* SDK DO GA.

## <a name="release--retirement-dates"></a>Datas de lançamento e de baixa
A Microsoft fornecerá notificação pelo menos **12 meses** antes de desativar um SDK na versão mais recente/suporte ordem toosmooth Olá transição tooa.

Novos recursos e funcionalidade e as otimizações são adicionadas apenas toohello atual SDK, como tal, é recomendável que você sempre atualize toohello mais recente versão do SDK mais cedo possível. 

TooCosmos qualquer solicitação usando um SDK obsoleto do banco de dados serão rejeitados pelo serviço de saudação.

> [!WARNING]
> Todas as versões do hello SDK do DocumentDB do Azure para tooversion anterior Python **1.0.0** será desativado em **29 de fevereiro de 2016**. 
> 
> 

<br/>

| Versão | Data do lançamento | Data de desativação |
| --- | --- | --- |
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
toolearn mais sobre o banco de dados do Cosmos, consulte [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de serviço. 

