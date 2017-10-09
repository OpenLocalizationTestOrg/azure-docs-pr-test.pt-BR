---
title: dados de aaaMove do MySQL usando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como toomove dados do MySQL do banco de dados usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a>Mover dados do MySQL usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de banco de dados MySQL local. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.

Você pode copiar dados de um repositório de dados local MySQL dados repositório tooany suportada coletor. Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente suporta apenas mover tooother repositórios de dados de repositório de dados de um de dados MySQL, mas não para mover dados de outro armazenamento de dados dados repositórios tooan MySQL. 

## <a name="prerequisites"></a>Pré-requisitos
Serviço da fábrica de dados oferece suporte a fontes de MySQL local tooon conexão usando Olá Gateway de gerenciamento de dados. Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação.

Gateway é necessário mesmo que o banco de dados do hello MySQL é hospedado em uma máquina virtual de IaaS do Azure (VM). Você pode instalar o gateway de saudação em Olá mesma VM como dados Olá armazenar ou em uma máquina virtual diferente, contanto que o gateway Olá pode se conectar toohello banco de dados.

> [!NOTE]
> Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.

## <a name="supported-versions-and-installation"></a>Instalação e versões com suporte
Para Gateway de gerenciamento de dados tooconnect toohello banco de dados MySQL, você precisa tooinstall Olá [MySQL Connector/Net para o Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (versão 6.6.5 ou superior) Olá no mesmo sistema como Olá Gateway de gerenciamento de dados. Há suporte para o MySQL versão 5.1 e superior.

> [!TIP]
> Se você atingir o erro "Falha de autenticação porque o participante remoto Olá fechou fluxo de transporte hello.", considere Olá tooupgrade versão do MySQL Connector/Net toohigher.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs. 

- toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação. 
- Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. 
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados MySQL local, consulte [exemplo JSON: copiar dados do MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) deste artigo. 

Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados de MySQL toodefine usado Data Factory entidades tooa específico:

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooMySQL vinculado serviço.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **OnPremisesMySql** |Sim |
| server |Nome do servidor MySQL de saudação. |Sim |
| database |Nome do banco de dados do hello MySQL. |Sim |
| schema |Nome do esquema de saudação no banco de dados de saudação. |Não |
| authenticationType |Tipo de autenticação usado o banco de dados do tooconnect toohello MySQL. Os valores possíveis são: `Basic`. |Sim |
| Nome de Usuário |Especifique o banco de dados do usuário nome tooconnect toohello MySQL. |Sim |
| Senha |Especifique a senha da conta de usuário de saudação especificado. |Sim |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello local MySQL. |Sim |

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação. Olá typeProperties seção de conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados MySQL) tem Olá seguintes propriedades

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação em Olá instância de banco de dados MySQL serviço vinculado refere-se a. |Não (se **query** de **RelationalSource** for especificado) |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.

Por outro lado, as propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

Quando a fonte na atividade de cópia é do tipo **RelationalSource** (que inclui o MySQL), Olá propriedades a seguir está disponível na seção de typeProperties:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: select * from MyTable. |Não (se **tableName** de **dataset** for especificado) |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a>Exemplo JSON: copiar dados do MySQL tooAzure Blob
Este exemplo fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ele mostra como toocopy dados do MySQL local de banco de dados tooan armazenamento de BLOBs do Azure. No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.

> [!IMPORTANT]
> Este exemplo fornece trechos de JSON. Ele não inclui instruções passo a passo para criar a fábrica de dados hello. Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.

exemplo Hello tem Olá entidades da fábrica de dados a seguir:

1. Um serviço vinculado do tipo [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados de um resultado de consulta no blob de tooa do banco de dados MySQL por hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação. Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

**Serviço vinculado do MySQL:**

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

**Serviço vinculado de armazenamento do Azure:**

```JSON
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

**Conjunto de dados de entrada do MySQL:**

exemplo Hello supõe que você criou uma tabela "MyTable" no MySQL e contém uma coluna chamada "timestampcolumn" para dados de série temporal.

Definindo "externo": "verdadeiro" informa Olá serviço de fábrica de dados tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
            "typeProperties": {},
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

**Conjunto de dados de saída de Blob do Azure:**

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Pipeline com Atividade de cópia:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** e **coletor** tipo está definido muito**BlobSink**. consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.

```JSON
    {
        "name": "CopyMySqlToBlob",
        "properties": {
            "description": "pipeline for copy activity",
            "activities": [
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "RelationalSource",
                            "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                        },
                        "sink": {
                            "type": "BlobSink",
                            "writeBatchSize": 0,
                            "writeBatchTimeout": "00:00:00"
                        }
                    },
                    "inputs": [
                        {
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a>Mapeamento de tipo para MySQL
Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem em duas etapas a seguir:

1. Converter nativo tipos too.NET do tipo de origem
2. Converter do tipo de coletor de toonative de tipo .NET

Ao mover dados tooMySQL, hello mapeamentos a seguir são usados de tipos de too.NET de tipos do MySQL.

| Tipo do Banco de Dados MySQL | Tipo .NET Framework |
| --- | --- |
| bigint unsigned |Decimal |
| bigint |Int64 |
| bit |Decimal |
| blob |Byte[] |
| bool |Booliano |
| char |Cadeia de caracteres |
| data |Datetime |
| Datetime |Datetime |
| Decimal |Decimal |
| double precision |Duplo |
| Duplo |Duplo |
| enum |Cadeia de caracteres |
| flutuante |Single |
| int unsigned |Int64 |
| int |Int32 |
| integer unsigned |Int64 |
| inteiro |Int32 |
| long varbinary |Byte[] |
| long varchar |Cadeia de caracteres |
| longblob |Byte[] |
| longtext |Cadeia de caracteres |
| mediumblob |Byte[] |
| mediumint unsigned |Int64 |
| mediumint |Int32 |
| mediumtext |Cadeia de caracteres |
| numérico |Decimal |
| real |Duplo |
| set |Cadeia de caracteres |
| smallint unsigned |Int32 |
| smallint |Int16 |
| texto |Cadeia de caracteres |
| tempo real |timespan |
| timestamp |Datetime |
| tinyblob |Byte[] |
| tinyint unsigned |Int16 |
| tinyint |Int16 |
| tinytext |Cadeia de caracteres |
| varchar |Cadeia de caracteres |
| year |int |

## <a name="map-source-toosink-columns"></a>Mapear colunas de toosink de origem
toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Leitura repetida de fontes relacionais
Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais. No Azure Data Factory, você pode repetir a execução de uma fatia manualmente. Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha. Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada. Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
