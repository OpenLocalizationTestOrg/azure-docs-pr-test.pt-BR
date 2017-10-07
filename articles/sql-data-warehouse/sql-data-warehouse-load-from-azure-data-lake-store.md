---
title: "aaaLoad - tooSQL do repositório Azure Data Lake do Data Warehouse | Microsoft Docs"
description: "Saiba como toouse PolyBase tabelas externas dados tooload do repositório Azure Data Lake no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a>Carregar dados do Azure Data Lake Store no SQL Data Warehouse
Este documento fornece todas as etapas necessárias tooload seus próprios dados do Azure Data Lake ADLS (repositório) no SQL Data Warehouse usando PolyBase.
Enquanto você estiver toorun capaz de consultas de ad hoc em dados de saudação armazenados no ADLS usando tabelas externas hello, como uma prática recomendada é recomendável importar dados de saudação para Olá SQL Data Warehouse.
Tempo estimado: 10 minutos, supondo que você tem pré-requisitos Olá necessário toocomplete.
Neste tutorial, você aprenderá a:

1. Crie tooload de objetos de banco de dados externo do repositório Azure Data Lake.
2. Conecte-se tooan diretório de armazenamento do Azure Data Lake.
3. Carregue os dados no SQL Data Warehouse.

## <a name="before-you-begin"></a>Antes de começar
toorun neste tutorial, você precisa:

* Toouse de aplicativo do Active Directory do Azure para autenticação de serviços. toocreate, siga [autenticação do Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)

>[!NOTE] 
> É necessário o ID do cliente hello, chave e valor de ponto de extremidade Token OAuth 2.0 do seu tooyour tooconnect de aplicativo do Active Directory do Azure Data Lake do SQL Data Warehouse. Detalhes de como tooget esses valores são link de saudação acima.
>Observação para registro do aplicativo do Azure Active Directory usar Olá ID do aplicativo como Olá ID do cliente.

* SQL Server Management Studio ou o SQL Server Data Tools, toodownload SSMS e conecte-se consulte [SSMS de consulta](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)

* Um Data Warehouse do Azure SQL toocreate um siga: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision

* Um Azure Data Lake Store com ou sem a criptografia habilitada. um siga toocreate: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal




## <a name="configure-hello-data-source"></a>Configurar fonte de dados de saudação
PolyBase usa o local do T-SQL objetos externos toodefine hello e atributos de dados externos de saudação. Olá externos são armazenados em SQL Data Warehouse e Olá dados de referência que th é armazenada externamente.


###  <a name="create-a-credential"></a>Criar uma credencial
tooaccess o Azure Data Lake armazenar, você precisará toocreate tooencrypt uma chave mestra de banco de dados a seu segredo de credencial usado na próxima etapa do hello.
Você, em seguida, criar uma credencial no escopo do banco de dados, que armazena as credenciais do serviço principal do hello configuradas no AAD. Para aqueles que usaram o PolyBase tooconnect tooWindows Blobs de armazenamento do Azure, observe a credencial Olá sintaxe é diferente.
tooconnect tooAzure repositório Data Lake, você deve **primeiro** criar um aplicativo do Azure Active Directory, crie uma chave de acesso e conceder Olá aplicativo acesso toohello Azure Data Lake recurso. Instrucitons tooperform essas etapas estão localizadas [aqui](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a>Criar fonte de dados externa Olá
Use este [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] comando toostore local de saudação de Olá dados e tipo de saudação de dados.
Você pode encontrar hello ADL URI no hello portal do Azure e www.portal.azure.com.

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a>Configurar o formato de dados
tooimport dados de saudação do ADLS, você precisa de formato de arquivo externo toospecify hello. Esse comando tem opções específicas do formato toodescribe seus dados.
O exemplo abaixo é um formato de arquivo normalmente usado que é um arquivo de texto delimitado por pipe.
A nossa documentação T-SQL possui uma lista completa para [CRIAR UM FORMATO DE ARQUIVO EXTERNO][CREATE EXTERNAL FILE FORMAT]

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE
                    )
);
```

## <a name="create-hello-external-tables"></a>Criar tabelas externas de saudação
Agora que você especificou o formato de origem e o arquivo de dados hello, você está tabelas externas de saudação toocreate pronto. As tabelas externas servem para interagir com dados externos. PolyBase usa recursiva directory traversal tooread todos os arquivos em todos os subdiretórios do diretório de saudação especificado no parâmetro de local de saudação. Além disso, a saudação de exemplo a seguir mostra como toocreate Olá objeto. É necessário toocustomize Olá instrução toowork com dados Olá que tiver em ADLS.

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a>Considerações sobre a tabela externa
É fácil criar uma tabela externa, mas existem algumas nuances que precisam toobe discutido.

O carregamento de dados com o PolyBase é fortemente tipado. Isso significa que cada linha de dados Olá sendo incluídos deve atender a definição de esquema de tabela hello.
Se uma determinada linha não corresponder a definição de esquema hello, linha hello é rejeitada de carga hello.

Olá REJECT_TYPE e REJECT_VALUE opções permitem que você toodefine quantas linhas ou a porcentagem de dados Olá deve estar presente na tabela final hello.
Durante o carregamento, se Olá rejeitar valor é atingido, o carregamento de saudação falhará. a causa mais comum Olá de linhas rejeitadas é uma incompatibilidade de definição de esquema.
Por exemplo, se uma coluna incorretamente for dado esquema de saudação do int quando dados Olá no arquivo hello são uma cadeia de caracteres, cada linha falhará tooload.

Olá local Especifica pasta Olá de nível superior que você deseja tooread dados.
Nesse caso, se houvesse subdiretórios /DimProduct/ PolyBase importaria todos os dados de saudação em subdiretórios hello.

## <a name="load-hello-data"></a>Carregar dados de saudação
tooload de dados de repositório Azure Data Lake usar Olá [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrução. Carregando com CTAS usa Olá fortemente tipado tabela externa que você criou.

CTAS cria uma nova tabela e a popula com resultados de saudação de uma instrução select. CTAS define Olá nova tabela toohave Olá mesmos colunas e tipos de dados, como a instrução select de resultados de saudação do hello. Se você selecionar todas as colunas de saudação de uma tabela externa, nova tabela de saudação é uma réplica de colunas de saudação e tipos de dados na tabela externa hello.

Neste exemplo, estamos criando uma tabela distribuída de hash chamada DimProduct da nossa tabela externa DimProduct_external.

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a>Otimizar a compactação columnstore
Por padrão, o SQL Data Warehouse armazena tabela hello como um índice columnstore clusterizado. Após a conclusão de uma carga, algumas das linhas de dados de saudação não podem ser compactadas no Olá columnstore.  Há várias razões para isso acontecer. mais, consulte toolearn [gerenciar índices de columnstore][manage columnstore indexes].

consulta de toooptimize desempenho e compactação columnstore depois de uma carga recriar Olá tabela tooforce Olá columnstore index toocompress todas as linhas de saudação.

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

Para obter mais informações sobre como manter os índices columnstore, consulte Olá [gerenciar índices de columnstore] [ manage columnstore indexes] artigo.

## <a name="optimize-statistics"></a>Otimizar estatísticas
É melhor estatísticas de coluna única toocreate imediatamente após uma carga. Há algumas opções de estatísticas. Por exemplo, se você criar estatísticas de coluna única em todas as colunas pode levar um longo tempo toorebuild todas as estatísticas de saudação. Se você souber que determinadas colunas não serão toobe em predicados de consulta, você pode ignorar a criação de estatísticas nessas colunas.

Se você decidir toocreate estatísticas de coluna única em todas as colunas de cada tabela, você pode usar o exemplo de código do procedimento armazenado hello `prc_sqldw_create_stats` em Olá [estatísticas] [ statistics] artigo.

saudação de exemplo a seguir é um bom ponto de partida para a criação de estatísticas. Cria estatísticas de coluna única em cada coluna na tabela de dimensões hello e em cada coluna de junção em tabelas de fatos hello. Você sempre poderá adicionar colunas de tabela de fatos única ou várias colunas de estatísticas tooother posteriormente.


## <a name="achievement-unlocked"></a>Missão cumprida!
Você carregou com êxito os dados no SQL Data Warehouse do Azure. Bom trabalho!

##<a name="next-steps"></a>Próximas etapas
Carregamento de dados é Olá de primeira etapa toodeveloping uma solução de depósito de dados usando o SQL Data Warehouse. Confira nossos recursos de desenvolvimento em [Tabelas](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) e [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).


<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
