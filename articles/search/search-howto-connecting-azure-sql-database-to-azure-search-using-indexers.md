---
title: aaaConnecting banco de dados do Azure SQL tooAzure pesquisa usando indexadores | Microsoft Docs
description: Saiba como dados toopull tooan de banco de dados SQL Azure Search indexe usando indexadores.
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: e9bbf352-dfff-4872-9b17-b1351aae519f
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/13/2017
ms.author: eugenesh
ms.openlocfilehash: b28a11cf18ef994de99e09af90bbfeb171ef3cde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-sql-database-tooazure-search-using-indexers"></a>Conectar-se o banco de dados do Azure SQL tooAzure pesquisar usando indexadores

Antes de consultar um [índice do Azure Search](search-what-is-an-index.md), você deve populá-lo com seus dados. Se os dados de saudação residem em um banco de dados do SQL Azure, uma **indexador da pesquisa do Azure para o banco de dados do Azure SQL** (ou **indexador do SQL Azure** abreviada) pode automatizar o processo de indexação hello, que significa que menos código toowrite e menos infraestrutura toocare sobre.

Este artigo aborda a mecânica de saudação do uso [indexadores](search-indexer-overview.md), mas também descreve recursos disponíveis apenas com bancos de dados do SQL Azure (por exemplo, controle de alterações integrado). 

Em adição tooAzure bancos de dados SQL Azure Search fornece indexadores para [o banco de dados do Azure Cosmos](search-howto-index-documentdb.md), [armazenamento de BLOBs do Azure](search-howto-indexing-azure-blob-storage.md), e [armazenamento de tabela do Azure](search-howto-indexing-azure-tables.md). toorequest suporte para outras fontes de dados, forneça seus comentários em Olá [Fórum de comentários da pesquisa do Azure](https://feedback.azure.com/forums/263029-azure-search/).

## <a name="indexers-and-data-sources"></a>Indexadores e fontes de dados

Um **fonte de dados** Especifica quais dados tooindex, as credenciais para acesso a dados e políticas que identificam com eficiência as alterações nos dados de saudação (linhas novo, modificados ou excluídos). Ela é definida como um recurso independente para que possa ser usada por vários indexadores.

Um **indexador** é um recurso que conecta uma fonte de dados individual a um índice de pesquisa de destino. Um indexador é usado em Olá maneiras a seguir:

* Execute uma cópia única de dados de saudação toopopulate um índice.
* Atualize um índice com alterações na fonte de dados de saudação em uma agenda.
* Execute sob demanda tooupdate um índice, conforme necessário.

Um indexador único só pode consumir uma tabela ou exibição, mas você pode criar vários indexadores, se você quiser toopopulate vários índices de pesquisa. Para obter mais informações sobre os conceitos, consulte [Operações do indexador: Fluxo de trabalho típico](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations#typical-workflow).

Você pode definir e configurar um indexador do SQL Azure usando:

* Assistente para importar dados em Olá [portal do Azure](https://portal.azure.com)
* [SDK do .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer?view=azure-dotnet) do Azure Search
* [API REST](https://docs.microsoft.com/en-us/rest/api/searchservice/indexer-operations) do Azure Search

Neste artigo, vamos usar Olá API REST toocreate **indexadores** e **fontes de dados**.

## <a name="when-toouse-azure-sql-indexer"></a>Quando toouse indexador do SQL Azure
Dependendo de vários fatores relacionados tooyour dados, uso de saudação do indexador do SQL Azure pode ou não pode ser apropriado. Se seus dados se ajusta Olá requisitos a seguir, você pode usar o indexador do SQL Azure.

| Critérios | Detalhes |
|----------|---------|
| Os dados são originados de uma única tabela ou exibição | Se os dados de saudação é espalhados entre várias tabelas, você pode criar uma única exibição de dados de saudação. No entanto, se você usar um modo de exibição, não será capaz de toouse integrada do SQL Server alteração detecção toorefresh um índice com alterações incrementais. Para obter mais informações, consulte [Capturando linhas alteradas e excluídas](#CaptureChangedRows) abaixo. |
| Os tipos de dados são compatíveis | Quase todos os tipos SQL de saudação têm suporte em um índice de pesquisa do Azure. Para obter uma lista, consulte [Mapeando tipos de dados](#TypeMapping). |
| A sincronização de dados em tempo real não é necessária | Um indexador pode reindexar a tabela, no máximo, a cada cinco minutos. Se os dados forem alterados com frequência e hello alterações toobe necessidade refletida no índice de saudação em segundos ou minutos único, é recomendável usar Olá [API REST](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) ou [.NET SDK](search-import-data-dotnet.md) toopush linhas atualizadas diretamente. |
| A indexação incremental é possível | Se você tiver um grande conjunto de dados e indexador de saudação do plano toorun em um agendamento, pesquisa do Azure deve ser capaz de tooefficiently identificar linhas novas, alteradas ou excluídas. A indexação não incremental só será permitida se você estiver indexando sob demanda (não com base em um agendamento) ou menos de 100.000 linhas. Para obter mais informações, consulte [Capturando linhas alteradas e excluídas](#CaptureChangedRows) abaixo. |

## <a name="create-an-azure-sql-indexer"></a>Criar um Indexador SQL do Azure

1. Crie fonte de dados de saudação:

   ```
    POST https://myservice.search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:<your server>.database.windows.net,1433;Database=<your database>;User ID=<your user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "name of hello table or view that you want tooindex" }
    }
   ```

   Você pode obter a cadeia de caracteres de conexão de saudação do hello [portal do Azure](https://portal.azure.com); use Olá `ADO.NET connection string` opção.

2. Crie o índice de pesquisa do Azure de destino Olá se você não tiver uma. Você pode criar um índice usando Olá [portal](https://portal.azure.com) ou hello [criar índice API](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Certifique-se de que Olá esquema de seu índice de destino é compatível com o esquema de Olá Olá da tabela de origem - consulte [tipos de dados de mapeamento entre a pesquisa do Azure e SQL](#TypeMapping).

3. Crie indexador hello, dando a ele um nome e a referência de índice de origem e destino de dados hello:

    ```
    POST https://myservice.search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myindexer",
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name"
    }
    ```

Um indexador criado dessa maneira não tem um agenda. Ele é executado automaticamente assim que é criado. Você pode executá-lo novamente a qualquer momento usando uma solicitação **executar indexador** :

    POST https://myservice.search.windows.net/indexers/myindexer/run?api-version=2016-09-01
    api-key: admin-key

Você pode personalizar vários aspectos do comportamento do indexador, como tamanho do lote e quantos documentos podem ser ignorados antes de uma execução do indexador falhar. Para obter mais informações, consulte [Criar API do indexador](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer).

Talvez seja necessário um banco de dados de tooyour tooconnect tooallow os serviços do Azure. Consulte [conectar do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) para obter instruções sobre como toodo que.

toomonitor Olá status do indexador e histórico de execução (número de itens indexados, falhas, etc.), use um **status do indexador** solicitação:

    GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2016-09-01
    api-key: admin-key

resposta de saudação deve ser a seguir toohello semelhante:

    {
        "@odata.context":"https://myservice.search.windows.net/$metadata#Microsoft.Azure.Search.V2015_02_28.IndexerExecutionInfo",
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2015-02-21T00:23:24.957Z",
            "endTime":"2015-02-21T00:36:47.752Z",
            "errors":[],
            "itemsProcessed":1599501,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        },
        "executionHistory":
        [
            {
                "status":"success",
                "errorMessage":null,
                "startTime":"2015-02-21T00:23:24.957Z",
                "endTime":"2015-02-21T00:36:47.752Z",
                "errors":[],
                "itemsProcessed":1599501,
                "itemsFailed":0,
                "initialTrackingState":null,
                "finalTrackingState":null
            },
            ... earlier history items
        ]
    }

Histórico de execução contém até too50 de execuções de saudação concluída mais recentemente, que são classificados em ordem cronológica inversa de saudação (de forma que a execução mais recente Olá vem primeira na resposta de saudação).
Informações adicionais sobre resposta Olá podem ser encontradas em [obter Status do indexador](http://go.microsoft.com/fwlink/p/?LinkId=528198)

## <a name="run-indexers-on-a-schedule"></a>Executar indexadores de acordo com uma agenda
Você também pode organizar Olá indexador toorun periodicamente em um agendamento. toodo isso, adicione Olá **agenda** propriedade ao criar ou atualizar o indexador hello. exemplo Hello abaixo mostra um indexador de saudação tooupdate PUT solicitação:

    PUT https://myservice.search.windows.net/indexers/myindexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name",
        "schedule" : { "interval" : "PT10M", "startTime" : "2015-01-01T00:00:00Z" }
    }

Olá **intervalo** parâmetro é obrigatório. intervalo de saudação se refere a tempo toohello entre o início de saudação de duas execuções do indexador consecutivos. Olá menor permitido intervalo é de 5 minutos; Olá mais longo é um dia. Ele deve ser formatado como um valor XSD de "dayTimeDuration" (um subconjunto restrito de um [valor de duração ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) ). saudação padrão para isso é: `P(nD)(T(nH)(nM))`. Exemplos: `PT15M` para cada 15 minutos, `PT2H` para cada 2 horas.

Olá opcional **startTime** indica quando hello execuções programadas devem começar. Se ele for omitido, a hora UTC atual de saudação é usada. Neste momento pode estar em Olá após – nesse caso execução primeiro hello está agendada como se o indexador hello está sendo executado continuamente desde Olá startTime.  

Só é possível ocorrer uma execução de um indexador por vez. Se um indexador está em execução quando a execução é agendada, execução de saudação é adiada até Olá próximo horário agendado.

Vamos considerar um exemplo toomake isso mais concreto. Suponha que estamos Olá seguindo um agendamento por hora configurado:

    "schedule" : { "interval" : "PT1H", "startTime" : "2015-03-01T00:00:00Z" }

Veja o que acontece:

1. primeira execução do indexador Olá inicia em ou em torno de 1º de março de 2015, 12:00 a.m. UTC.
2. Vamos supor que essa execução demore 20 minutos (ou menos de uma hora).
3. início da execução da segunda Olá em ou em torno de 1º de março de 2015, 1:00 a.m.
4. Agora suponha que essa execução demore mais de uma hora, por exemplo, 70 minutos, então ela será concluída aproximadamente às 2:10.
5. Agora é hora de 2:00:00, para Olá terceira execução toostart. No entanto, como Olá segunda execução de 1h ainda está em execução, execução de terceiro Olá é ignorada. início da execução de terceiro Olá às 3h.

Você pode adicionar, alterar ou excluir uma agenda de um indexador existente usando uma solicitação de **indexador PUT** .

<a name="CaptureChangedRows"></a>

## <a name="capture-new-changed-and-deleted-rows"></a>Capturar linhas novas, alteradas e excluídas

Pesquisa do Azure usa **indexação incremental** tooavoid com índice toore Olá toda a tabela ou exibição sempre é executado de um indexador. A pesquisa do Azure fornece que dois alterar detecção políticas toosupport incremental de indexação. 

### <a name="sql-integrated-change-tracking-policy"></a>Política de controle integrado de alterações do SQL
Se o banco de dados SQL oferece suporte ao [controle de alterações](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server), recomendamos o uso da **Política de controle integrado de alterações do SQL**. Essa é a política de mais eficiente de saudação. Além disso, ele permite pesquisa do Azure tooidentify excluída linhas sem a necessidade de tooadd uma tabela de tooyour de coluna explícita "exclusão reversível".

#### <a name="requirements"></a>Requisitos 

+ Requisitos de versão do banco de dados:
  * O SQL Server 2012 SP3 e posterior, se você estiver usando o SQL Server em VMs do Azure.
  * Banco de Dados SQL do Azure V12, se você estiver usando o Banco de Dados SQL do Azure.
+ Apenas tabelas (sem exibições). 
+ No banco de dados Olá [habilitar o controle de alterações](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server) para a tabela de saudação. 
+ Nenhuma chave primária composta (uma chave primária que contém mais de uma coluna) na tabela de saudação.  

#### <a name="usage"></a>Uso

toouse essa política, criar ou atualizar a fonte de dados como este:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy"
      }
    }

Ao usar a política de controle integrado de alterações do SQL, não especifique uma política separada de detecção de exclusão de dados, pois essa política tem suporte interno para identificação de linhas excluídas. No entanto, para Olá exclusões toobe detectado "forma mágica", chave de documento hello em seu índice de pesquisa deve ser Olá igual a chave primária Olá Olá tabela SQL. 

<a name="HighWaterMarkPolicy"></a>

### <a name="high-water-mark-change-detection-policy"></a>Política de detecção de alteração de marca d’água alta

Essa política de detecção de alteração se baseia em uma coluna de "marca d'água de alta" capturar versão hello ou hora da última atualização uma linha. Se você estiver usando uma exibição, deverá usar uma política de marca d'água alta. coluna de marca d'água alta de saudação deve atender Olá requisitos a seguir.

#### <a name="requirements"></a>Requisitos 

* Todas as inserções especificam um valor para a coluna de saudação.
* Item de tooan todas as atualizações também alterar o valor de saudação da coluna hello.
* valor de saudação dessa coluna aumenta com cada insert ou update.
* Consultas com hello onde a seguir e cláusulas ORDER BY podem ser executadas com eficiência:`WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`

> [!IMPORTANT] 
> É altamente recomendável usar Olá [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) tipo de dados para a coluna de marca d'água alta de saudação. Se qualquer outro tipo de dados for usado, o controle de alterações não é garantida toocapture todas as alterações na presença de saudação de transações em execução simultaneamente com uma consulta de indexador. Ao usar **rowversion** em uma configuração com réplicas somente leitura, você deve apontar o indexador Olá na réplica primária hello. Apenas uma réplica primária pode ser usada para cenários de sincronização de dados.

#### <a name="usage"></a>Uso

toouse uma política de marca d'água alta, criar ou atualizar a fonte de dados como este:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
           "highWaterMarkColumnName" : "[a rowversion or last_updated column name]"
      }
    }

> [!WARNING]
> Se a tabela de origem Olá não tem um índice na coluna de marca d'água alta de hello, consultas usadas pelo indexador SQL Olá atinjam o tempo limite. Em particular, Olá `ORDER BY [High Water Mark Column]` cláusula requer um índice toorun com eficiência ao Olá tabela tiver muitas linhas.
>
>

Se você encontrar erros de tempo limite, você pode usar o hello `queryTimeout` indexador configuração configuração tooset Olá consulta tooa valor de tempo limite maior do que o tempo limite da saudação padrão 5 minutos. Por exemplo, tooset Olá tempo limite too10 minutos, criar ou atualizar o indexador Olá com hello a seguinte configuração:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

Você também pode desabilitar Olá `ORDER BY [High Water Mark Column]` cláusula. No entanto, isso não é recomendado porque se a execução do indexador Olá é interrompida por um erro, indexador Olá tem toore processo todas as linhas se ele é executado mais tarde - mesmo que o indexador Olá já processou quase todas as linhas de saudação pelo tempo de saudação que foi interrompida. Olá toodisable `ORDER BY` cláusula, use Olá `disableOrderByHighWaterMarkColumn` configuração na definição do indexador hello:  

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "disableOrderByHighWaterMarkColumn" : true } }
    }

### <a name="soft-delete-column-deletion-detection-policy"></a>Política de detecção de exclusão de coluna por exclusão reversível
Quando linhas são excluídas da tabela de origem hello, provavelmente desejará toodelete as linhas do índice de pesquisa de saudação. Se você usar Olá SQL integrado a política de controle de alterações, isso é resolvido para você. No entanto, política de controle de alterações de marca d'água alta de saudação não ajudam com linhas excluídas. Quais toodo?

Se as linhas de saudação fisicamente são removidas da tabela Olá, pesquisa do Azure tem forma tooinfer Olá presença dos registros que não existem mais.  No entanto, você pode usar linhas de exclusão do hello "exclusão reversível" técnica toologically sem removê-los da tabela de saudação. Adicione uma coluna tooyour tabela ou exibição e marcar linhas como excluído usando essa coluna.

Ao usar a técnica de exclusão reversível Olá, você pode especificar política de exclusão reversível hello como a seguir ao criar ou atualizar a fonte de dados de saudação:

    {
        …,
        "dataDeletionDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
           "softDeleteColumnName" : "[a column name]",
           "softDeleteMarkerValue" : "[hello value that indicates that a row is deleted]"
        }
    }

Olá **softDeleteMarkerValue** deve ser uma cadeia de caracteres – use a representação de cadeia de caracteres de saudação do seu valor real. Por exemplo, se você tiver uma coluna de inteiros em que as linhas excluídas são marcadas com valor Olá 1, use `"1"`. Se você tiver uma coluna de bits em que as linhas excluídas são marcadas com hello valor booliano true, use `"True"`.

<a name="TypeMapping"></a>

## <a name="mapping-between-sql-and-azure-search-data-types"></a>Mapeamento entre tipos de dados SQL e do Azure Search
| Tipo de dados SQL | Tipos de campos de índice de destino permitidos | Observações |
| --- | --- | --- |
| bit |Edm.Boolean, Edm.String | |
| int, smallint, tinyint |Edm.Int32, Edm.Int64, Edm.String | |
| bigint |Edm.Int64, Edm.String | |
| real, float |Edm.Double, Edm.String | |
| smallmoney, numérico decimal dinheiro |Edm.String |O Azure Search não dá suporte à conversão de tipos decimais em Edm.Double porque isso causaria a perda de precisão |
| char, nchar, varchar, nvarchar |Edm.String<br/>Collection(Edm.String) |Uma cadeia de caracteres SQL pode ser usado toopopulate um campo Collection se a cadeia de caracteres de saudação representa uma matriz JSON de cadeias de caracteres:`["red", "white", "blue"]` |
| smalldatetime, datetime, datetime2, date, datetimeoffset |Edm.DateTimeOffset, Edm.String | |
| uniqueidentifer |Edm.String | |
| geografia |Edm.GeographyPoint |Somente instâncias de Geografia do tipo POINT com SRID 4326 (que é o padrão de saudação) têm suporte |
| rowversion |N/D |Colunas de versão de linha não podem ser armazenadas no índice de pesquisa hello, mas eles podem ser usados para controle de alterações |
| tempo, timespan, binário, varbinário, imagem, xml, geometria, tipos CLR |N/D |Sem suporte |

## <a name="configuration-settings"></a>Definições de configuração
O indexador do SQL expõe várias definições de configuração:

| Configuração | Tipo de dados | Finalidade | Valor padrão |
| --- | --- | --- | --- |
| queryTimeout |string |Conjuntos de Olá tempo limite de execução de consulta SQL |5 minutos ("00:05:00") |
| disableOrderByHighWaterMarkColumn |bool |Faz com que a consulta SQL Olá usada por Olá marca d'água alta política tooomit Olá cláusula ORDER BY. Consulte [Política de marca d'água alta](#HighWaterMarkPolicy) |false |

Essas configurações são usadas em Olá `parameters.configuration` objeto na definição do indexador hello. Por exemplo, minutos de too10 do tempo limite de consulta de saudação tooset, criar ou atualizar o indexador Olá com hello seguinte configuração:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

## <a name="faq"></a>Perguntas frequentes

**P: Posso usar o indexador SQL do Azure com bancos de dados SQL em execução em VMs IaaS no Azure?**

Sim. No entanto, é necessário tooallow seu banco de dados de tooyour de tooconnect do serviço de pesquisa. Para obter mais informações, consulte [configurar uma conexão de um indexador de pesquisa do Azure tooSQL Server em uma VM do Azure](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md).

**P: Posso usar o indexador SQL do Azure com bancos de dados SQL em execução local?**

Não diretamente. Não recomendamos ou dar suporte a uma conexão direta, como fazer isso exige tooopen o tráfego de tooInternet de bancos de dados. Os clientes tiveram sucesso com esse cenário usando tecnologias de ponte como o Azure Data Factory. Para obter mais informações, consulte [índice de pesquisa do Azure por Push dados tooan usando o Azure Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-azure-search-connector).

**P: Posso usar o indexador SQL do Azure com outros bancos de dados que não o SQL Server em execução em IaaS no Azure?**

Não. Não há suporte para esse cenário, porque não testamos indexador Olá com bancos de dados diferente do SQL Server.  

**P: Posso criar vários indexadores em execução com base em um agendamento?**

Sim. No entanto, somente um indexador pode ser executado por vez em um nó. Se você precisar vários indexadores em execução simultaneamente, considere o dimensionamento de seu toomore do serviço de pesquisa de uma unidade de pesquisa.

**P: A execução de um indexador afeta minha carga de trabalho de consulta?**

Sim. Indexador for executado em um de nós de saudação em seu serviço de pesquisa, e os recursos do nó são compartilhados entre indexação e que atende ao tráfego de consulta e outras solicitações de API. Se você executar cargas de trabalho de indexação e consulta intensivas e receber uma alta taxa de erros 503 ou tempos de resposta maiores, considere a possibilidade de [dimensionar o serviço de pesquisa](search-capacity-planning.md).

**P: Posso usar uma réplica secundária em um [cluster de failover](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) como fonte de dados?**

Isso depende. Para a indexação completa de uma tabela ou exibição, você pode usar uma réplica secundária. 

Para a indexação incremental, o Azure Search dá suporte a duas políticas de detecção de alteração: controle de alterações integrado do SQL e Marca D'água Alta.

Em réplicas somente leitura, o banco de dados SQL não dá suporte ao controle de alterações integrado. Portanto, você deve usar a política de Marca D'água Alta. 

Nossa recomendação padrão é toouse Olá rowversion tipo de dados para a coluna de marca d'água alta de saudação. No entanto, o uso de rowversion depende da função `MIN_ACTIVE_ROWVERSION` do Banco de Dados SQL, para a qual não há suporte em réplicas somente leitura. Portanto, você deve apontar réplica primária do hello indexador tooa se você estiver usando rowversion.

Se você tentar toouse rowversion em uma réplica somente leitura, você verá Olá erro a seguir: 

    "Using a rowversion column for change tracking is not supported on secondary (read-only) availability replicas. Please update hello datasource and specify a connection toohello primary availability replica.Current database 'Updateability' property is 'READ_ONLY'".

**P: Posso usar uma coluna não rowversion alternativa para o controle de alterações de marca d'água alta?**

Isso não é recomendável. Somente **rowversion** permite a sincronização de dados confiável. No entanto, dependendo da lógica do aplicativo, isso poderá ser seguro se:

+ Você pode garantir que, quando o indexador Olá é executado, não existem transações pendentes na tabela de saudação que está sendo indexado (por exemplo, todas as atualizações de tabela ocorrem como um lote em um agendamento, e agendamento Olá pesquisa do Azure é definido tooavoid sobreposição com tabela de saudação agendamento de atualização).  

+ Periodicamente, você fazer toopick uma reindexação completa a todas as linhas ausentes. 
