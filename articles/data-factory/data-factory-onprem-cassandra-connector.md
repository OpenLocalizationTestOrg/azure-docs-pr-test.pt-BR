---
title: "dados de aaaMove de Cassandra utilizando a fábrica de dados | Microsoft Docs"
description: Saiba mais sobre como dados toomove Cassandra um local de banco de dados usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a>Mover dados de um banco de dados Cassandra local usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de um banco de dados de Cassandra local. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.

Você pode copiar dados de um repositório de dados local Cassandra dados repositório tooany suportada coletor. Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente suporta apenas mover tooother repositórios de dados de repositório de dados de um dados Cassandra, mas não para mover dados de outro armazenamento de dados dados repositórios tooa Cassandra. 

## <a name="supported-versions"></a>Versões com suporte
Olá Cassandra conector dá suporte a saudação seguintes versões do Cassandra: 2. x.

## <a name="prerequisites"></a>Pré-requisitos
Saudação do Azure Data Factory serviço toobe tooconnect capaz de tooyour local Cassandra banco de dados, você deve instalar um Gateway de gerenciamento de dados em Olá mesmo esse banco de dados de saudação de hosts de máquina ou em um tooavoid máquina separada competição por recursos com hello banco de dados. Gateway de gerenciamento de dados é um componente que se conecta a serviços de toocloud de fontes de dados no local de forma segura e gerenciada. Confira o artigo [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) para obter todos os detalhes sobre o Gateway de Gerenciamento de Dados. Consulte [mover dados de local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter instruções passo a passo sobre como configurar o gateway de saudação um toomove do pipeline de dados.

Você deve usar o banco de dados do hello gateway tooconnect tooa Cassandra mesmo se o banco de dados de saudação é hospedado na nuvem hello, por exemplo, em uma VM de IaaS do Azure. Y, você pode ter um gateway de saudação em Olá VM mesmo banco de dados Olá hosts ou em uma máquina virtual separada, contanto que o gateway de saudação pode se conectar toohello banco de dados.  

Quando você instalar o gateway de Olá, ele instala automaticamente um banco de dados do Microsoft Cassandra ODBC driver usado tooconnect tooCassandra. Portanto, você não precisa toomanually instalar qualquer driver no computador do gateway Olá ao copiar dados do banco de dados de Cassandra hello. 

> [!NOTE]
> Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs. 

- toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação. 
- Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. 
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados local Cassandra, consulte [exemplo JSON: copiar dados de Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) deste artigo. 

Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados de Cassandra toodefine usado Data Factory entidades tooa específico:

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooCassandra vinculado serviço.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **OnPremisesCassandra** |Sim |
| host |Um ou mais endereços IP ou nomes de host dos servidores Cassandra.<br/><br/>Especifique uma lista separada por vírgulas de endereços IP ou host nomes tooconnect tooall servidores simultaneamente. |Sim |
| porta |Olá porta TCP que Olá servidor Cassandra usa toolisten para conexões de cliente. |Não, valor padrão: 9042 |
| authenticationType |Básica, ou Anônima |Sim |
| Nome de Usuário |Especifique o nome de usuário para a conta de usuário de saudação. |Sim, se authenticationType é definido tooBasic. |
| Senha |Especifique a senha da conta de usuário de saudação. |Sim, se authenticationType é definido tooBasic. |
| gatewayName |nome de saudação do gateway de saudação que é usado tooconnect toohello Cassandra banco de dados no local. |Sim |
| encryptedCredential |Credencial criptografada pelo gateway hello. |Não |

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação. Olá typeProperties seção de conjunto de dados do tipo **CassandraTable** tem Olá seguintes propriedades

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| keyspace |Nome da saudação keyspace ou esquema Cassandra banco de dados. |Sim (se a **consulta** para **CassandraSource** não estiver definida). |
| tableName |Nome da tabela de saudação no banco de dados Cassandra. |Sim (se a **consulta** para **CassandraSource** não estiver definida). |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.

Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

Quando a fonte é do tipo **CassandraSource**, Olá propriedades a seguir está disponível na seção de typeProperties:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Consulta SQL-92 ou consulta CQL. Veja [Referência ao CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>Ao usar a consulta SQL, especifique **keyspace name.table nome** toorepresent Olá tabela tooquery. |Não (se tableName e keyspace no conjunto de dados estiverem definidos). |
| consistencyLevel |nível de consistência de saudação especifica quantas réplicas deve responder a solicitação de leitura de tooa antes de retornar o aplicativo de cliente de toohello de dados. Verificações de Cassandra Olá número especificado de réplicas para a solicitação de leitura de saudação do toosatisfy de dados. |ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE. Confira [Configuring data consistency (Configurando a consistência de dados)](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) para obter detalhes. |Não. O valor padrão é ONE. |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a>Exemplo JSON: copiar dados de Cassandra tooAzure Blob
Este exemplo fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ele mostra como dados toocopy Cassandra um local de banco de dados tooan armazenamento de BLOBs do Azure. No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.

> [!IMPORTANT]
> Este exemplo fornece trechos de JSON. Ele não inclui instruções passo a passo para criar a fábrica de dados hello. Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.

exemplo Hello tem Olá entidades da fábrica de dados a seguir:

* Um serviço vinculado do tipo [OnPremisesCassandra](#linked-service-properties).
* Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [CassandraTable](#dataset-properties).
* Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* O [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [CassandraSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

**Serviço vinculado Cassandra:**

Este exemplo usa Olá **Cassandra** serviço vinculado. Consulte [serviço vinculado de Cassandra](#linked-service-properties) seção de propriedades de saudação suportados por esse serviço vinculado.  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

**Serviço vinculado de armazenamento do Azure:**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

**Conjunto de dados de entrada do Cassandra:**

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Configuração **externo** muito**true** informa o serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

**Conjunto de dados de saída de Blob do Azure:**

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Atividade de cópia em um pipeline com origem Cassandra e coletor de Blob:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**CassandraSource** e **coletor** tipo está definido muito**BlobSink**.

Consulte [propriedades de tipo RelationalSource](#copy-activity-properties) para lista de saudação de propriedades com suporte pelo Olá RelationalSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a>Mapeamento de tipo para Cassandra
| Tipo Cassandra | Tipo baseado no .Net |
| --- | --- |
| ASCII |Cadeia de caracteres |
| BIGINT |Int64 |
| BLOB |Byte[] |
| BOOLEAN |BOOLEAN |
| DECIMAL |DECIMAL |
| DOUBLE |DOUBLE |
| FLOAT |Single |
| INET |Cadeia de caracteres |
| INT |Int32 |
| TEXT |Cadeia de caracteres |
| TIMESTAMP |DateTime |
| TIMEUUID |Guid |
| UUID |Guid |
| VARCHAR |Cadeia de caracteres |
| VARINT |Decimal |

> [!NOTE]
> Para a coleção de tipos (mapa, conjunto, lista, etc.), consulte muito[trabalhar com tipos de coleção Cassandra usando a tabela virtual](#work-with-collections-using-virtual-table) seção.
>
> Não há suporte para tipos definidos pelo usuário.
>
> comprimento de saudação de comprimentos de coluna binária e de colunas de cadeia de caracteres não pode ser maior que 4000.
>
>

## <a name="work-with-collections-using-virtual-table"></a>Trabalhar com coleções usando tabela virtual
A fábrica de dados do Azure usa um interna tooconnect tooand copiar dados do driver ODBC do banco de dados Cassandra. Para tipos de coleção, incluindo o mapa, conjunto e lista, o driver Olá renormalizes dados saudação em tabelas virtuais correspondentes. Especificamente, se uma tabela contiver colunas coleção, o driver hello gera Olá tabelas virtuais a seguir:

* Um **tabela base**, que contém Olá os mesmos dados que a tabela real Olá com exceção das colunas da coleção de saudação. tabela base Olá usa Olá mesmo nome como tabela de saudação real que ele representa.
* Um **tabela virtual** para cada coluna de coleção, que expande dados saudação aninhado. tabelas virtuais de saudação que representam coleções são nomeadas usando Olá nome de tabela real hello, um separador de "*vt*" e o nome de saudação da coluna de saudação.

Tabelas virtuais Consulte toohello dados na tabela real hello, habilitando tooaccess de driver Olá Olá dados desnormalizados. Confira a seção Exemplo para obter detalhes. Você pode acessar o conteúdo de Olá de coleções de Cassandra ao consultar e unir tabelas virtuais hello.

Você pode usar o hello [Assistente para cópia de](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively exibição Olá a lista de tabelas no banco de dados de Cassandra incluindo tabelas virtuais hello e visualizar dados hello dentro. Também pode criar uma consulta no Assistente para cópia de saudação e validar os resultados de saudação toosee.

### <a name="example"></a>Exemplo
Por exemplo, hello seguir "ExampleTable" é uma tabela de banco de dados de Cassandra que contém uma coluna de chave primária da inteiro chamado "pk_int", uma coluna de texto denominado valor, uma coluna de lista, uma coluna de mapa e uma coluna de conjunto (chamado de "StringSet").

| pk_int | Valor | Listar | Mapa | StringSet |
| --- | --- | --- | --- | --- |
| 1 |"valor de exemplo 1" |["1", "2", "3"] |{"S1": "a", "S2": "b"} |{"A", "B", "C"} |
| 3 |"valor de exemplo 3" |["100", "101", "102", "105"] |{"S1": "t"} |{"A", "E"} |

driver de saudação poderia gerar vários toorepresent de tabelas virtuais nessa única tabela. Olá colunas de chave estrangeira em tabelas virtuais Olá fazer referência a colunas de chave primária Olá na tabela real hello e indicar qual real linha da tabela linha hello tabela virtual corresponde à.

primeira tabela virtual que Olá é a tabela base hello, denominada "ExampleTable" é mostrada no Olá a tabela a seguir. tabela base Olá contém Olá mesmo dados da tabela de banco de dados original hello, exceto as coleções de saudação, que são omitidos dessa tabela e expandidas em outras tabelas virtuais.

| pk_int | Valor |
| --- | --- |
| 1 |"valor de exemplo 1" |
| 3 |"valor de exemplo 3" |

Olá, tabelas a seguir mostram tabelas Olá virtual renormalize dados saudação de colunas de lista e mapa StringSet hello. Olá colunas com nomes que terminam com index"ou"c_have"para indicar posição Olá dos dados hello dentro da lista original hello ou um mapa. colunas de saudação com nomes que terminam com Value"contêm dados de saudação expandido da coleção de saudação.

#### <a name="table-exampletablevtlist"></a>Tabela "ExampleTable_vt_List":
| pk_int | List_index | List_value |
| --- | --- | --- |
| 1 |0 |1 |
| 1 |1 |2 |
| 1 |2 |3 |
| 3 |0 |100 |
| 3 |1 |101 |
| 3 |2 |102 |
| 3 |3 |103 |

#### <a name="table-exampletablevtmap"></a>Tabela "ExampleTable_vt_Map":
| pk_int | Map_key | Map_value |
| --- | --- | --- |
| 1 |S1 |O  |
| 1 |S2 |b |
| 3 |S1 |t |

#### <a name="table-exampletablevtstringset"></a>Tabela "ExampleTable_vt_StringSet":
| pk_int | StringSet_value |
| --- | --- |
| 1 |O  |
| 1 |b |
| 1 |C |
| 3 |O  |
| 3 |E |

## <a name="map-source-toosink-columns"></a>Mapear colunas de toosink de origem
toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Leitura repetida de fontes relacionais
Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais. No Azure Data Factory, você pode repetir a execução de uma fatia manualmente. Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha. Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada. Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
