---
title: aaaCopy dados para/do Azure SQL Data Warehouse | Microsoft Docs
description: Saiba como toocopy dados para/do Azure SQL Data Warehouse usando o Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a>Copiar dados tooand do Azure SQL Data Warehouse usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de/para o Azure SQL Data Warehouse. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.  

> [!TIP]
> tooachieve melhor desempenho, use dados tooload no Azure SQL Data Warehouse. Olá [Use tooload dados no Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) seção tem detalhes. Para ver um passo a passo com um caso de uso, veja [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Azure Data Factory).

## <a name="supported-scenarios"></a>Cenários com suporte
Você pode copiar dados **do Azure SQL Data Warehouse** toohello repositórios de dados a seguir:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Você pode copiar dados de saudação armazenamentos de dados a seguir **tooAzure SQL Data Warehouse**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> Ao copiar dados de tooAzure do SQL Server ou banco de dados do SQL Azure SQL Data Warehouse, se a tabela de saudação não existe no repositório de destino hello, fábrica de dados pode criar automaticamente tabela Olá no SQL Data Warehouse usando o esquema de saudação da tabela de saudação na fonte de saudação armazenamento de dados. Consulte [Criação automática de tabela](#auto-table-creation) para obter detalhes.

## <a name="supported-authentication-type"></a>Tipos de autenticação com suporte
O conector do SQL Data Warehouse do Azure dá suporte à autenticação básica.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados de um banco de dados bidirecionalmente em um SQL Data Warehouse do Azure usando diferentes ferramentas/APIs.

toocreate de maneira mais fácil de saudação um pipeline que copia dados de/para o Azure SQL Data Warehouse é assistente toouse Olá de cópia de dados. Consulte [Tutorial: carregar dados no SQL Data Warehouse com o Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar uma **data factory**. Um data factory pode conter um ou mais pipelines. 
2. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica. Por exemplo, se você estiver copiando dados de um data warehouse de BLOBs do Azure storage tooan SQL Azure, você criar duas toolink de serviços vinculados sua conta de armazenamento do Azure e a fábrica de dados do SQL Azure data warehouse tooyour. Para propriedades de serviço vinculado que tooAzure específica do SQL Data Warehouse, consulte [vinculado propriedades do serviço](#linked-service-properties) seção. 
3. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. O exemplo hello mencionado na última etapa do hello, você criará um contêiner de blob do conjunto de dados toospecify hello e a pasta que contém os dados de entrada hello. E, você cria outra tabela de saudação de toospecify de conjunto de dados no data warehouse Olá SQL do Azure que contém dados Olá copiados saudação do armazenamento de blob. Para propriedades de conjunto de dados que são específico tooAzure SQL Data Warehouse, consulte [propriedades de conjunto de dados](#dataset-properties) seção.
4. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. Exemplo hello mencionado anteriormente, você usar BlobSource como uma origem e SqlDWSink como um coletor de atividade de cópia de saudação. Da mesma forma, se você está copiando do Azure SQL Data Warehouse tooAzure armazenamento de Blob, use SqlDWSource e BlobSink na atividade de cópia de saudação. Para propriedades de atividade de cópia que tooAzure específica do SQL Data Warehouse, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção. Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados.

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um depósito de dados do SQL Azure, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) deste artigo.

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAzure SQL Data Warehouse:

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooAzure serviço vinculado do SQL Data Warehouse.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **AzureSqlDW** |Sim |
| connectionString |Especifique informações necessárias a instância do tooconnect toohello Azure SQL Data Warehouse para a propriedade connectionString de saudação. Há suporte somente para autenticação básica. |Sim |

> [!IMPORTANT]
> Configurar [Firewall de banco de dados do SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) e Olá o servidor de banco de dados muito[permitir que serviços do Azure tooaccess Olá servidor](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Além disso, se você estiver copiando dados tooAzure SQL Data Warehouse incluindo Azure fora de fontes de dados local com o gateway da fábrica de dados, configure o intervalo de endereços IP apropriado para a máquina de saudação que está enviando dados tooAzure SQL Data Warehouse.

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação. Olá **typeProperties** seção de conjunto de dados de saudação do tipo **AzureSqlDWTable** tem Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação ou exibição no banco de dados de Data warehouse do SQL Azure de saudação que Olá serviço vinculado refere-se a. |Sim |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.

> [!NOTE]
> Hello atividade de cópia usa apenas uma entrada e produz apenas uma saída.

Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

### <a name="sqldwsource"></a>SqlDWSource
Quando a fonte é do tipo **SqlDWSource**, Olá propriedades a seguir está disponível em **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| SqlReaderQuery |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: select * from MyTable. |Não |
| sqlReaderStoredProcedureName |Nome da saudação procedimento armazenado que lê dados da tabela de origem hello. |Nome da saudação de procedimento armazenado. Olá a última instrução de SQL deve ser uma instrução SELECT no procedimento armazenado de saudação. |Não |
| storedProcedureParameters |Parâmetros de saudação de procedimento armazenado. |Pares de nome/valor. Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação. |Não |

Se hello **sqlReaderQuery** é especificada para Olá SqlDWSource, hello atividade de cópia executa esta consulta em relação a saudação dados do Azure SQL Data Warehouse origem tooget Olá.

Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).

Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de saudação definidas na seção de estrutura de saudação do conjunto de dados Olá JSON são usado toobuild toorun uma consulta em relação a hello Azure SQL Data Warehouse. Exemplo: `select column1, column2 from mytable`. Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.

#### <a name="sqldwsource-example"></a>Exemplo de SqlDWSource

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
**definição do procedimento armazenada de saudação:**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a>SqlDWSink
**SqlDWSink** dá suporte a saudação propriedades a seguir:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Especifique uma consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa. Para obter detalhes, consulte a [seção de repetição](#repeatability-during-copy). |Uma instrução de consulta. |Não |
| allowPolyBase |Indica se toouse PolyBase (quando aplicável) em vez de mecanismo BULKINSERT. <br/><br/> **Usar o PolyBase é hello recomendado a maneira como os dados tooload no SQL Data Warehouse.** Consulte [Use tooload dados no Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) seção de detalhes e restrições. |Verdadeiro <br/>False (padrão) |Não |
| polyBaseSettings |Um grupo de propriedades que podem ser especificadas ao hello **allowPolybase** propriedade for definida muito**true**. |&nbsp; |Não |
| rejectValue |Especifica o número de saudação ou a porcentagem de linhas que pode ser rejeitada antes Olá consulta falhe. <br/><br/>Saiba mais sobre do PolyBase Olá rejeitar opções Olá **argumentos** seção [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tópico. |0 (padrão), 1, 2, … |Não |
| rejectType |Especifica se a opção de rejectValue de saudação é especificada como um valor literal ou uma porcentagem. |Valor (padrão), Percentual |Não |
| rejectSampleValue |Determina o número de saudação de linhas tooretrieve antes Olá PolyBase recalcula a porcentagem de saudação de linhas rejeitadas. |1, 2, … |Sim, se **rejectType** for **percentual** |
| useTypeDefault |Especifica como toohandle faltando valores delimitados por arquivos de texto quando PolyBase recupera dados do arquivo de texto de saudação.<br/><br/>Saiba mais sobre essa propriedade da seção argumentos Olá [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (padrão) |Não |
| writeBatchSize |Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize |Inteiro (número de linhas) |Não (padrão: 10000) |
| writeBatchTimeout |Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar. |timespan<br/><br/> Exemplo: "00:30:00" (30 minutos). |Não |

#### <a name="sqldwsink-example"></a>Exemplo de SqlDWSink

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a>Usar dados tooload no Azure SQL Data Warehouse
Usar o **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** é uma maneira eficiente de carregar grandes quantidades de dados no SQL Data Warehouse do Azure com alta taxa de transferência. Você pode ver um ganho grande na taxa de transferência hello usando PolyBase em vez do mecanismo BULKINSERT saudação padrão. Veja [número de referência do desempenho de cópia](data-factory-copy-activity-performance.md#performance-reference) com comparação detalhada. Para ver um passo a passo com um caso de uso, veja [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Azure Data Factory).

* Se sua fonte de dados está em **BLOBs do Azure ou do repositório Azure Data Lake**e formato de saudação é compatível com o PolyBase, você pode copiar diretamente tooAzure SQL Data Warehouse usando PolyBase. Veja **[Cópia direta usando o PolyBase](#direct-copy-using-polybase)** com detalhes.
* Se o repositório de dados de origem e o formato não tiver suporte originalmente pelo PolyBase, você pode usar o hello  **[cópia testados usando PolyBase](#staged-copy-using-polybase)**  recurso em vez disso. Ele também fornece melhor taxa de transferência automaticamente converter dados de saudação em formato compatível com o PolyBase e armazenando dados saudação no armazenamento de BLOBs do Azure. Em seguida, ele carrega os dados no SQL Data Warehouse.

Saudação de conjunto `allowPolyBase` propriedade muito**true** conforme mostrado no seguinte exemplo para o Azure Data Factory toouse toocopy dados no Azure SQL Data Warehouse de saudação. Quando você define allowPolyBase tootrue, você pode especificar propriedades específicas do PolyBase usando Olá `polyBaseSettings` grupo de propriedades. Consulte Olá [SqlDWSink](#SqlDWSink) seção para obter detalhes sobre as propriedades que você pode usar com polyBaseSettings.

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a>Cópia direta usando o PolyBase
O SQL Data Warehouse PolyBase dá suporte diretamente ao Blob do Azure e ao Azure Data Lake Store (usando a entidade de serviço) como origem e com os requisitos de formato de arquivo específico. Se sua fonte de dados atende aos critérios de saudação descritos nesta seção, você pode copiar diretamente da fonte tooAzure de repositório de dados que do SQL Data Warehouse usando PolyBase. Caso contrário, poderá aproveitar a [Cópia de preparo usando o PolyBase](#staged-copy-using-polybase).

> [!TIP]
> toocopy dados do repositório Data Lake tooSQL Data Warehouse com eficiência, saiba mais de [do Azure Data Factory torna insights toouncover mais fácil e conveniente de dados, mesmo ao usar o repositório Data Lake com o SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).

Se Olá requisitos não forem atendidos, o Azure Data Factory verifica as configurações de saudação e automaticamente reverterá toohello mecanismo BULKINSERT Olá para movimentação de dados.

1. O **serviço vinculado de origem** é do tipo: **AzureStorage** ou **AzureDataLakeStore com autenticação da entidade de serviço**.  
2. Olá **conjunto de dados de entrada** é do tipo: **AzureBlob** ou **AzureDataLakeStore**, e Olá tipo de formato em `type` propriedades é **OrcFormat** , ou **TextFormat** com hello configurações a seguir:

   1. `rowDelimiter` deve ser **\n**.
   2. `nullValue`está definido muito**cadeia de caracteres vazia** (""), ou `treatEmptyAsNull` está definido muito**true**.
   3. `encodingName`está definido muito**utf-8**, que é **padrão** valor.
   4. `escapeChar`, `quoteChar`, `firstRowAsHeader` e `skipLineCount` não foram especificados.
   5. `compression` pode ser **sem compactação**, **GZip** ou **Deflate**.

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. Não há nenhum `skipHeaderLineCount` em **BlobSource** ou **AzureDataLakeStore** para hello atividade de cópia no pipeline de saudação.
4. Não há nenhum `sliceIdentifierColumnName` em **SqlDWSink** para hello atividade de cópia no pipeline de saudação. (O PolyBase garante que todos os dados são atualizados ou que nada é atualizado em uma execução única. tooachieve **repetibilidade**, você pode usar `sqlWriterCleanupScript`).
5. Não há nenhum `columnMapping` que está sendo usado em Olá associado na atividade de cópia.

### <a name="staged-copy-using-polybase"></a>Cópia de preparo usando o PolyBase
Quando sua fonte de dados não atendem aos critérios de saudação apresentados na seção anterior hello, você pode habilitar a cópia de dados por meio de um armazenamento de Blob de preparo do Azure provisório (não pode ser o armazenamento Premium). Nesse caso, Azure Data Factory automaticamente executa transformações em Olá dados toomeet formato requisitos de dados de PolyBase e, em seguida, use dados tooload no SQL Data Warehouse e no último limpar seus dados temporários saudação do armazenamento de Blob. Confira [Cópia de Preparo](data-factory-copy-activity-performance.md#staged-copy) para obter detalhes sobre como copiar dados por meio de um trabalho de preparo do Blob do Azure em geral.

> [!NOTE]
> Quando copiar dados de um local de dados armazenam no Azure SQL Data Warehouse usando PolyBase e preparação, se a sua versão do Gateway de gerenciamento de dados está abaixo 2.4, o JRE (Java Runtime Environment) é necessária no gateway do computador que é usado tootransform sua fonte de dados em formato adequado. Sugerir que atualizar seu tooavoid mais recente do gateway toohello tal dependência.
>

toouse esse recurso, criar um [serviço vinculado do armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) que se refere a toohello conta de armazenamento do Azure que tem o armazenamento de blob provisório hello, especifique Olá `enableStaging` e `stagingSettings` propriedades para hello atividade de cópia conforme mostrado na saudação de código a seguir:

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a>Práticas recomendadas ao usar o PolyBase
Olá seções a seguir fornecem toohello de práticas recomendada adicionais que são mencionados na [práticas recomendadas para o Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).

### <a name="required-database-permission"></a>Permissão de banco de dados obrigatória
toouse PolyBase, ele requer Olá usuário que está sendo usado tooload dados no SQL Data Warehouse tem Olá [permissão "CONTROL"](https://msdn.microsoft.com/library/ms191291.aspx) no banco de dados de destino de saudação. Tooachieve unidirecional que é tooadd esse usuário como um membro da função "db_owner". Saiba como toodo que seguindo [nesta seção](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).

### <a name="row-size-and-data-type-limitation"></a>Limitação de tamanho da linha e tipo de dados
Cargas de Polybase estão limitadas tooloading linhas ambos menor do que **1 MB** e não é possível carregar tooVARCHR(MAX), nvarchar (max) ou varbinary (max). Consulte também[aqui](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).

Se você tiver dados de origem com linhas de tamanho maior que 1 MB, convém tabelas de origem toosplit Olá verticalmente em várias partes pequenas onde maior tamanho de linha hello de cada um deles não exceda o limite de saudação. tabelas menores Hello, em seguida, podem ser carregadas usando PolyBase e mesclados no Azure SQL Data Warehouse.

### <a name="sql-data-warehouse-resource-class"></a>Classe de recursos do SQL Data Warehouse
tooachieve melhor transferência possíveis, considere tooassign maior recurso classe toohello usuário sendo tooload de dados usados no SQL Data Warehouse por meio do PolyBase. Saiba como toodo que seguindo [alterar um exemplo de classe de recurso de usuário](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

### <a name="tablename-in-azure-sql-data-warehouse"></a>tableName no Azure SQL Data Warehouse
Olá tabela a seguir fornece exemplos de como Olá toospecify **tableName** propriedade no conjunto de dados JSON para várias combinações de nome de esquema e tabela.

| Esquema do BD | Nome da tabela | Propriedade JSON tableName |
| --- | --- | --- |
| dbo |MyTable |MyTable ou dbo.MyTable ou [dbo].[MyTable] |
| dbo1 |MyTable |dbo1.MyTable ou [dbo1].[MyTable] |
| dbo |My.Table |[My.Table] ou [dbo].[My.Table] |
| dbo1 |My.Table |[dbo1]. [My.Table] |

Se você vir Olá erro a seguir, pode ser um problema com valor de saudação especificado para a propriedade tableName de saudação. Consulte a tabela Olá Olá maneira correta toospecify valores para a propriedade do hello tableName JSON.  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a>Colunas com valores padrão
Atualmente, só aceita um recurso na fábrica de dados de PolyBase Olá mesmo número de colunas na tabela de destino de saudação. Digamos que você tenha uma tabela com quatro colunas e uma delas esteja definida com um valor padrão. dados de entrada Hello ainda devem conter quatro colunas. Fornecer um conjunto de dados de entrada de 3-coluna produziria uma toohello semelhante erro seguinte mensagem:

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
O valor NULL é uma forma especial do valor padrão. Se a coluna de saudação é anulável, dados de entrada hello (de blob) para essa coluna podem ser vazios (não pode estar ausente da saudação conjunto de dados de entrada). PolyBase insere NULL para eles no hello Azure SQL Data Warehouse.  

## <a name="auto-table-creation"></a>Criação automática de tabela
Se você estiver usando o Assistente de cópia toocopy dados do SQL Server ou banco de dados do Azure SQL tooAzure SQL Data Warehouse e hello tabela que corresponde a tabela de origem toohello não existem no repositório de destino hello, fábrica de dados pode criar automaticamente tabela Olá em Olá depósito de dados usando o esquema de tabela de origem hello.

Fábrica de dados cria a tabela de saudação no repositório de destino Olá com hello mesmo nome no repositório de dados de origem de saudação da tabela. tipos de dados Olá para colunas são escolhidos com base em Olá mapeamento de tipo a seguir. Se necessário, ele executa toofix de conversões de tipo quaisquer incompatibilidades entre repositórios de origem e de destino. Ele também usa a distribuição de tabelas em um Round Robin.

| Tipo de coluna do Banco de Dados SQL da origem | Tipo de coluna do SQL DW de destino (limitação de tamanho) |
| --- | --- |
| int | int |
| BigInt | BigInt |
| SmallInt | SmallInt |
| TinyInt | TinyInt |
| Bit | Bit |
| Decimal | Decimal |
| Numérico | Decimal |
| Float | Float |
| Money | Money |
| Real | Real |
| SmallMoney | SmallMoney |
| Binário | Binário |
| Varbinary | Varbinary (até too8000) |
| Data | Data |
| DateTime | DateTime |
| DateTime2 | DateTime2 |
| Hora | Hora |
| Datetimeoffset | Datetimeoffset |
| SmallDateTime | SmallDateTime |
| Texto | Varchar (até too8000) |
| NText | NVarChar (até too4000) |
| Imagem | VarBinary (até too8000) |
| UniqueIdentifier | UniqueIdentifier |
| Char | Char |
| NChar | NChar |
| VarChar | VarChar (até too8000) |
| NVarChar | NVarChar (até too4000) |
| xml | Varchar (até too8000) |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a>Mapeamento de tipo do SQL Data Warehouse do Azure
Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:

1. Converter nativo tipos too.NET do tipo de origem
2. Converter do tipo de coletor de toonative de tipo .NET

Ao mover dados muito & do Azure SQL Data Warehouse, hello mapeamentos a seguir são usados do tipo SQL de too.NET e vice-versa.

mapeamento de saudação é igual a saudação [mapeamento de tipo de dados do SQL Server do ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).

| Tipo de mecanismo do Banco de Dados do SQL Server | Tipo .NET Framework |
| --- | --- |
| bigint |Int64 |
| binário |Byte[] |
| bit |Booliano |
| char |String, Char[] |
| data |DateTime |
| DateTime |DateTime |
| datetime2 |DateTime |
| Datetimeoffset |Datetimeoffset |
| Decimal |Decimal |
| Atributo FILESTREAM (varbinary(max)) |Byte[] |
| Float |Duplo |
| imagem |Byte[] |
| int |Int32 |
| money |Decimal |
| nchar |String, Char[] |
| ntext |String, Char[] |
| numérico |Decimal |
| nvarchar |String, Char[] |
| real |Single |
| rowversion |Byte[] |
| smalldatetime |DateTime |
| smallint |Int16 |
| smallmoney |Decimal |
| sql_variant |Objeto * |
| texto |String, Char[] |
| tempo real |timespan |
| timestamp |Byte[] |
| tinyint |Byte |
| uniqueidentifier |Guid |
| varbinary |Byte[] |
| varchar |String, Char[] |
| xml |xml |

Você também pode mapear colunas de origem toocolumns de conjunto de dados do conjunto de coletor de dados na definição de atividade de cópia de saudação. Para obter detalhes, confira [Mapear colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a>Exemplos JSON para copiar dados tooand do SQL Data Warehouse
Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Eles mostram como toocopy tooand de dados do Azure SQL Data Warehouse e o armazenamento de BLOBs do Azure. No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a>Exemplo: Copiar dados do Azure SQL Data Warehouse tooAzure Blob
exemplo Hello define Olá entidades da fábrica de dados a seguir:

1. Um serviço vinculado do tipo [AzureSqlDW](#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureSqlDWTable](#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. O [pipeline](data-factory-create-pipelines.md) com a Atividade de cópia que usa [SqlDWSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados de série temporal (por hora, diariamente, etc.) de uma tabela no blob do Azure SQL Data Warehouse banco de dados tooa a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

**Serviço vinculado do SQL Data Warehouse do Azure:**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Serviço vinculado do armazenamento de Blob do Azure:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Conjunto de dados de entrada do SQL Data Warehouse do Azure:**

exemplo Hello supõe que você criou uma tabela "MyTable" no Azure SQL Data Warehouse e contém uma coluna chamada "timestampcolumn" para dados de série temporal.

Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
**Conjunto de dados de saída de Blob do Azure:**

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Atividade de cópia em um pipeline com SqlDWSource e BlobSink:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**SqlDWSource** e **coletor** tipo está definido muito**BlobSink**. consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
> [!NOTE]
> No exemplo hello, **sqlReaderQuery** é especificado para Olá SqlDWSource. Hello atividade de cópia executa esta consulta Olá dados do Azure SQL Data Warehouse origem tooget hello.
>
> Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).
>
> Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de saudação definidas na seção de estrutura de saudação do conjunto de dados Olá JSON são usado toobuild uma consulta (selecione column1, column2 de mytable) toorun contra hello Azure SQL Data Warehouse. Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a>Exemplo: Copiar dados de tooAzure de BLOBs do Azure SQL Data Warehouse
exemplo Hello define Olá entidades da fábrica de dados a seguir:

1. Um serviço vinculado do tipo [AzureSqlDW](#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureSqlDWTable](#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com Atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlDWSink](#copy-activity-properties).

exemplo Hello copia dados de série temporal (por hora, diariamente, etc) da tabela de tooa de BLOBs do Azure no banco de dados do Azure SQL Data Warehouse, a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

**Serviço vinculado do SQL Data Warehouse do Azure:**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Serviço vinculado do armazenamento de Blob do Azure:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Conjunto de dados de entrada de Blob do Azure:**

Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1). Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa year, month e parte do dia da hora de início da saudação e nome do arquivo usa a parte de hora Olá Olá da hora de início. "externo": "verdadeira" configuração informa o serviço de fábrica de dados de saudação que essa tabela é toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
**Conjunto de dados de saída do SQL Data Warehouse do Azure:**

exemplo Hello copiará a tabela de tooa de dados denominada "MyTable" no Azure SQL Data Warehouse. Criar tabela de saudação no Azure SQL Data Warehouse com hello mesmo número de colunas, conforme o esperado toocontain de arquivo CSV de Blob hello. Novas linhas são adicionadas a tabela de toohello a cada hora.

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Atividade de cópia em um pipeline com BlobSource e SqlDWSink:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e **coletor** tipo está definido muito**SqlDWSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
Para obter instruções, consulte Olá [carregar 1 TB no Azure SQL Data Warehouse em 15 minutos com o Azure Data Factory](data-factory-load-sql-data-warehouse.md) e [carregar os dados com o Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) artigo hello Azure SQL Data Warehouse documentação.

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
