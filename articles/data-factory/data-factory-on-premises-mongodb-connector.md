---
title: "dados de aaaMove do MongoDB usando a fábrica de dados | Microsoft Docs"
description: Saiba mais sobre como os dados de toomove do MongoDB banco de dados usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a>Mover dados do MongoDB usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de um banco de dados do MongoDB no local. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.

Você pode copiar dados de um repositório de dados local MongoDB dados repositório tooany suportada coletor. Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente suporta apenas mover tooother repositórios de dados de repositório de dados de um dados MongoDB, mas não para mover dados de outro repositório de dados dados repositórios tooan MongoDB. 

## <a name="prerequisites"></a>Pré-requisitos
Saudação do Azure Data Factory serviço toobe tooconnect capaz de tooyour local MongoDB banco de dados, você deve instalar Olá componentes a seguir:

- As versões com suporte do MongoDB são: 2.4, 2.6, 3.0 e 3.2.
- Gateway de gerenciamento de dados em Olá mesma máquina desse banco de dados de saudação de hosts ou em um tooavoid máquina separada competição por recursos com o banco de dados de saudação. Gateway de gerenciamento de dados é um software que se conecta a serviços de toocloud de fontes de dados no local de forma segura e gerenciada. Confira o artigo [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) para obter todos os detalhes sobre o Gateway de Gerenciamento de Dados. Consulte [mover dados de local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter instruções passo a passo sobre como configurar o gateway de saudação um toomove do pipeline de dados.

    Quando você instalar o gateway de hello, instala automaticamente um tooMongoDB de tooconnect do MongoDB do Microsoft ODBC driver usado.

    > [!NOTE]
    > É necessário toouse Olá gateway tooconnect tooMongoDB mesmo se ele estiver hospedado em VMs de IaaS do Azure. Se você estiver tentando tooconnect tooan instância do MongoDB hospedado na nuvem, você também pode instalar instância de gateway Olá no hello IaaS VM.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local MongoDB usando diferentes ferramentas/APIs.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir: 

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. 
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados do MongoDB no local, consulte [exemplo JSON: copiar dados do MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) deste artigo. 

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específicas tooMongoDB origem:

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá tabela a seguir fornece descrição para elementos JSON específicos muito**OnPremisesMongoDB** serviço vinculado.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **OnPremisesMongoDb** |Sim |
| server |IP endereço ou nome de host do servidor do MongoDB hello. |Sim |
| porta |Porta TCP que Olá MongoDB server usa toolisten para conexões de cliente. |Opcional, valor padrão: 27017 |
| authenticationType |Básica ou Anônima. |Sim |
| Nome de Usuário |Conta de usuário tooaccess MongoDB. |Sim (se a autenticação básica for usada). |
| Senha |Senha do usuário hello. |Sim (se a autenticação básica for usada). |
| authSource |Nome do banco de dados do MongoDB Olá que você deseja toouse toocheck suas credenciais para autenticação. |Opcional (se a autenticação básica for usada). padrão: usa a conta de administrador hello e banco de dados de saudação especificado usando a propriedade databaseName. |
| databaseName |Nome do banco de dados do MongoDB Olá que você deseja tooaccess. |Sim |
| gatewayName |Nome do gateway de saudação que acessa o repositório de dados de saudação. |Sim |
| encryptedCredential |Credencial criptografada pelo gateway. |Opcional |

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação. Olá typeProperties seção de conjunto de dados do tipo **MongoDbCollection** tem Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| collectionName |Nome da coleção de saudação no banco de dados do MongoDB. |Sim |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.

As propriedades disponíveis no hello **typeProperties** seção de atividade Olá Olá outro lado variam de acordo com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

Quando a fonte de saudação é do tipo **MongoDbSource** Olá propriedades a seguir está disponível na seção de typeProperties:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Cadeia de consulta SQL-92. Por exemplo: select * from MyTable. |Não (se **collectionName** de **dataset** for especificado) |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a>Exemplo JSON: copiar dados do MongoDB tooAzure Blob
Este exemplo fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ele mostra como toocopy dados de um tooan do MongoDB local armazenamento de BLOBs do Azure. No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.

exemplo Hello tem Olá entidades da fábrica de dados a seguir:

1. Um serviço vinculado do tipo [OnPremisesMongoDb](#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [MongoDbCollection](#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [MongoDbSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados de um resultado de consulta no blob de tooa de banco de dados do MongoDB a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

Como uma primeira etapa, configurar o gateway de gerenciamento de dados de saudação de acordo com as instruções de Olá Olá [Data Management Gateway](data-factory-data-management-gateway.md) artigo.

**Serviço vinculado ao MongoDB:**

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
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

**Conjunto de dados de entrada do MongoDB:** configuração "externo": "verdadeiro" informa Olá serviço de fábrica de dados tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

**Conjunto de dados de saída de Blob do Azure:**

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Uma atividade de cópia em um pipeline com origem no MongoDB e coletor Blob:**

pipeline de saudação contém uma atividade de cópia que é configurado toouse hello acima conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**MongoDbSource** e **coletor** tipo está definido muito**BlobSink**. consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a>Esquema do Data Factory
Serviço de fábrica de dados do Azure infere o esquema de uma coleção do MongoDB usando documentos Olá 100 mais recente na coleção de saudação. Se esses 100 documentos não contêm o esquema completo, algumas colunas podem ser ignoradas durante a operação de cópia de saudação.

## <a name="type-mapping-for-mongodb"></a>Mapeamento de tipo para o MongoDB
Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:

1. Converter nativo tipos too.NET do tipo de origem
2. Converter do tipo de coletor de toonative de tipo .NET

Ao mover Olá tooMongoDB de dados a seguir os mapeamentos são usados de tipos de too.NET de tipos do MongoDB.

| Tipo do MongoDB | Tipo .NET Framework |
| --- | --- |
| Binário |Byte[] |
| Booliano |Booliano |
| Data |DateTime |
| NumberDouble |Duplo |
| NumberInt |Int32 |
| NumberLong |Int64 |
| ObjectID |Cadeia de caracteres |
| Cadeia de caracteres |Cadeia de caracteres |
| UUID |Guid |
| Objeto |Renormalizado para colunas simples com “_” como separador aninhado |

> [!NOTE]
> toolearn sobre o suporte para matrizes usando tabelas virtuais, consulte muito[suporte para tipos complexos usando tabelas virtuais](#support-for-complex-types-using-virtual-tables) seção abaixo.

No momento, não há suporte para Olá seguintes tipos de dados do MongoDB: DBPointer, JavaScript, Max/Min chave, Expressão Regular, o símbolo, o carimbo de hora, indefinido

## <a name="support-for-complex-types-using-virtual-tables"></a>Suporte para tipos complexos usando tabelas virtuais
A fábrica de dados do Azure usa um internos ODBC driver tooconnect tooand copiar dados de seu banco de dados do MongoDB. Para tipos complexos, como objetos ou matrizes com tipos diferentes em documentos Olá, o driver Olá novamente normaliza dados em tabelas virtuais correspondentes. Especificamente, se uma tabela contiver essas colunas, o driver hello gera Olá tabelas virtuais a seguir:

* Um **tabela base**, que contém Olá os mesmos dados que a tabela real Olá com exceção das colunas de tipo complexo de saudação. tabela base Olá usa Olá mesmo nome como tabela de saudação real que ele representa.
* Um **tabela virtual** para cada coluna de tipo complexo, que expande dados saudação aninhado. tabelas virtuais Olá são nomeadas usando nome hello da tabela real Olá, um separador "_" e o nome de saudação do objeto ou matriz de saudação.

Tabelas virtuais Consulte toohello dados na tabela real hello, habilitando tooaccess de driver Olá Olá dados desnormalizados. Veja a seção Exemplo abaixo para obter detalhes. Você pode acessar conteúdo de saudação do MongoDB matrizes ao consultar e unir tabelas virtuais hello.

Você pode usar o hello [Assistente para cópia de](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively exibição Olá a lista de tabelas no banco de dados do MongoDB incluindo tabelas virtuais hello e visualizar dados hello dentro. Também pode criar uma consulta no Assistente para cópia de saudação e validar os resultados de saudação toosee.

### <a name="example"></a>Exemplo
Por exemplo, "TabelaDeExemplo" abaixo é uma tabela do MongoDB com uma coluna com uma matriz de Objetos em cada célula – Faturas, e uma coluna com uma matriz de tipos escalares – Classificações.

| _id | Nome do Cliente | Faturas | Nível de Serviço | Classificações |
| --- | --- | --- | --- | --- |
| 1111 |ABC |[{invoice_id:”123”, item:”torradeira”, price:”456”, discount:”0,2”}, {invoice_id:”124”, item:”forno”,price: ”1235”,discount: ”0,2”}] |Silver |[5,6] |
| 2222 |XYZ |[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}] |Gold |[1,2] |

driver de saudação poderia gerar vários toorepresent de tabelas virtuais nessa única tabela. Olá primeiro virtual tabela é Olá base chamado "ExampleTable", mostrado abaixo. tabela base Olá contém todos os dados de saudação da tabela original hello, mas dados saudação de matrizes de saudação foi omitidos e são expandidos em tabelas virtuais hello.

| _id | Nome do Cliente | Nível de Serviço |
| --- | --- | --- |
| 1111 |ABC |Silver |
| 2222 |XYZ |Gold |

Olá tabelas a seguir mostram Olá tabelas virtuais que representam matrizes de saudação original no exemplo hello. Essas tabelas contêm seguinte hello:

* Uma referência de volta toohello coluna de chave primária correspondente toohello linha original da matriz original da saudação (por meio da coluna de ID Olá)
* Uma indicação da posição de saudação do dados hello dentro da matriz original Olá
* Olá expandido dados para cada elemento na matriz de saudação

Tabela "TabelaDeExemplo_Faturas":

| _id | TabelaDeExemplo_Faturas_dim1_idx | invoice_id | item | preço | Desconto |
| --- | --- | --- | --- | --- | --- |
| 1111 |0 |123 |torradeira |456 |0,2 |
| 1111 |1 |124 |forno |1235 |0,2 |
| 2222 |0 |135 |geladeira |12543 |0,0 |

Tabela "TabelaDeExemplo_Classificações":

| _id | TabelaDeExemplo_Classificações_dim1_idx | TabelaDeExemplo_Classificações |
| --- | --- | --- |
| 1111 |0 |5 |
| 1111 |1 |6 |
| 2222 |0 |1 |
| 2222 |1 |2 |

## <a name="map-source-toosink-columns"></a>Mapear colunas de toosink de origem
toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Leitura repetida de fontes relacionais
Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais. No Azure Data Factory, você pode repetir a execução de uma fatia manualmente. Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha. Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada. Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.

## <a name="next-steps"></a>Próximas etapas
Consulte [mover dados entre locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) do artigo para obter instruções passo a passo para criar um pipeline de dados que move dados de um local de dados armazenam tooan repositório de dados do Azure.
