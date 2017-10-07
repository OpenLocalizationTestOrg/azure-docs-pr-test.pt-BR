---
title: "dados de aaaCopy para/da Oracle usando a fábrica de dados | Microsoft Docs"
description: "Saiba como toocopy dados de/para o banco de dados Oracle que está no local usando o Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a>Copiar dados para dentro e fora do Oracle local usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de/para o banco de dados Oracle local. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.

## <a name="supported-scenarios"></a>Cenários com suporte
Você pode copiar dados **de um banco de dados Oracle** toohello repositórios de dados a seguir:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Você pode copiar dados de saudação armazenamentos de dados a seguir **tooan banco de dados Oracle**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a>Pré-requisitos
Fábrica de dados dá suporte a fontes de Oracle local tooon conexão usando Olá Gateway de gerenciamento de dados. Consulte [Data Management Gateway](data-factory-data-management-gateway.md) toolearn artigo sobre o Gateway de gerenciamento de dados e [mover dados de local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter instruções passo a passo sobre como configurar o gateway de saudação um pipeline de dados dados de toomove.

Gateway é necessário mesmo que hello Oracle é hospedado em uma VM de IaaS do Azure. Você pode instalar o gateway de saudação em Olá mesmo IaaS VM como Olá dados armazenar ou em uma máquina virtual diferente, contanto que o gateway Olá pode se conectar toohello banco de dados.

> [!NOTE]
> Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.

## <a name="supported-versions-and-installation"></a>Instalação e versões com suporte
Este conector Oracle dá suporte a duas versões de drivers:

- **Driver da Microsoft para Oracle (recomendado)**: inicial do Gateway de gerenciamento de dados versão 2.7, um driver Microsoft para Oracle é automaticamente instalado junto com o gateway Olá, portanto você não precisa tooadditionally identificador Olá driver em ordem tooestablish conectividade tooOracle e você também pode ter o melhor desempenho de cópia usando este driver. Há suporte para as versões abaixo de bancos de dados Oracle:
    - Oracle 12c R1 (12.1)
    - Oracle 11g R1, R2 (11.1, 11.2)
    - Oracle 10g R1, R2 (10.1, 10.2)
    - Oracle 9i R1, R2 (9.0.1, 9.2)
    - Oracle 8i R3 (8.1.7)

> [!IMPORTANT]
> Atualmente o driver da Microsoft para Oracle suporta apenas copiar dados do Oracle, mas não gravar tooOracle. E observe a capacidade de conexão de teste Olá no guia de diagnóstico do Gateway de gerenciamento de dados não oferece suporte a este driver. Como alternativa, você pode usar a conectividade de Olá Olá cópia Assistente toovalidate.
>

- **Provedor de dados Oracle para .NET:** você também pode escolher dados de toocopy toouse provedor de dados Oracle de / tooOracle. Esse componente está incluído nos [Componentes de Acesso a Dados do Oracle para Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/). Instale a versão apropriada da saudação (32/64 bits) na máquina Olá onde Olá gateway está instalado. [Provedor de dados Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) pode acessar tooOracle banco de dados 10g versão 2 ou posterior.

    Se você escolher "Instalação XCopy", execute as etapas no hello Readme. htm. Recomendamos que você escolha instalador Olá com a interface do usuário (não-XCopy um).

    Depois de instalar o provedor de saudação **reiniciar** Olá serviço de host do Gateway de gerenciamento de dados em seu computador usando os serviços miniaplicativo (ou) Gerenciador de configuração de Gateway de gerenciamento de dados.  

Se você usar o pipeline de cópia cópia Assistente tooauthor hello, o tipo de driver de saudação será determinado automaticamente. O driver da Microsoft será usado por padrão, a menos que sua versão do gateway seja menor do que 2.7 ou você escolher o Oracle como um coletor.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com atividade de cópia que move dados de/para um banco de dados Oracle local por meio de ferramentas/APIs diferentes.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar uma **data factory**. Um data factory pode conter um ou mais pipelines. 
2. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica. Por exemplo, se você estiver copiando dados de um banco de dados de Oralce tooan armazenamento de BLOBs do Azure, você criar duas toolink de serviços vinculados seu banco de dados Oracle e a fábrica de dados de tooyour de conta de armazenamento do Azure. Para propriedades de serviço vinculado que tooOracle específico, consulte [vinculado propriedades do serviço](#linked-service-properties) seção.
3. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. Exemplo hello mencionado na última etapa do hello, você pode criar uma tabela de saudação do conjunto de dados toospecify no banco de dados Oracle que contém os dados de entrada hello. E, criar outro contêiner de blob do conjunto de dados toospecify hello e pasta Olá que contém dados saudação copiados da saudação banco de dados Oracle. Para propriedades de conjunto de dados que tooOracle específico, consulte [propriedades de conjunto de dados](#dataset-properties) seção.
4. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. Exemplo hello mencionado anteriormente, você usar OracleSource como uma origem e BlobSink como um coletor de atividade de cópia de saudação. Da mesma forma, se você está copiando do armazenamento de BLOBs do Azure tooOracle banco de dados, use BlobSource e OracleSink na atividade de cópia de saudação. Para propriedades de atividade de cópia tooOracle específico no banco de dados, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção. Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um banco de dados do Oracle no local, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-oracle-database) deste artigo.

Olá seções a seguir fornece detalhes sobre propriedades JSON que são entidades de fábrica de dados toodefine usado:

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooOracle vinculado serviço.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **OnPremisesOracle** |Sim |
| driverType | Especifique quais dados do driver toouse toocopy de / tooOracle banco de dados. Valores permitidos são **Microsoft** ou **ODP** (padrão). Consulte [suporte para instalação e da versão](#supported-versions-and-installation) seção detalhes do driver. | Não |
| connectionString | Especifique informações necessárias a instância de banco de dados Oracle toohello tooconnect para a propriedade connectionString de saudação. | Sim |
| gatewayName | Nome do gateway de saudação que é usado tooconnect toohello servidor Oracle local |Sim |

**Exemplo: usando o driver da Microsoft:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Exemplo: usando o driver ODP**

Consulte também[este site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) para Olá formatos permitido.

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções, como estrutura, disponibilidade e política de um JSON do conjunto de dados, são parecidas para todos os tipos de conjunto de dados (Oracle, blob do Azure, tabela do Azure etc.).

seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação. seção de typeProperties Olá Olá conjunto de dados do tipo OracleTable tem Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação na Olá banco de dados Oracle que Olá serviço vinculado refere-se a. |Não (se **oracleReaderQuery** de **OracleSource** for especificado) |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.

> [!NOTE]
> Hello atividade de cópia usa apenas uma entrada e produz apenas uma saída.

Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

### <a name="oraclesource"></a>OracleSource
Atividade de cópia, quando a fonte de saudação é do tipo **OracleSource** Olá propriedades a seguir está disponível em **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| oracleReaderQuery |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: select * from MyTable <br/><br/>Se não for especificado, Olá instrução SQL executada: selecione * de MyTable |Não (se **tableName** de **dataset** for especificado) |

### <a name="oraclesink"></a>OracleSink
**OracleSink** dá suporte a saudação propriedades a seguir:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| writeBatchTimeout |Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar. |timespan<br/><br/> Exemplo: "00:30:00" (30 minutos). |Não |
| writeBatchSize |Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize. |Inteiro (número de linhas) |Não (padrão: 100) |
| sqlWriterCleanupScript |Especifique uma consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa. |Uma instrução de consulta. |Não |
| sliceIdentifierColumnName |Especifique o nome de coluna para a atividade de cópia toofill com identificador de fatia gerado automaticamente, que é usado tooclean os dados de uma fatia específica quando executada novamente. |Nome de uma coluna com tipo de dados de binário (32). |Não |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a>Exemplos JSON para copiar dados tooand do banco de dados Oracle
Olá, exemplo a seguir fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Eles mostram como dados toocopy / tooan Oracle banco de dados para/do armazenamento de BLOBs do Azure. No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a>Exemplo: Copiar dados de Oracle tooAzure Blob

exemplo Hello tem Olá entidades da fábrica de dados a seguir:

1. Um serviço vinculado do tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) como fonte e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) como coletor.

exemplo Hello copia dados de uma tabela em um blob de tooa do banco de dados de Oracle local por hora. Para obter mais informações sobre várias propriedades usadas no exemplo hello, consulte a documentação nas seções a seguir exemplos de saudação.

**Serviço vinculado do Oracle:**

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Serviço vinculado do armazenamento de Blob do Azure:**

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Conjunto de dados de entrada do Oracle:**

exemplo Hello supõe que você criou uma tabela "MyTable" no Oracle e contém uma coluna chamada "timestampcolumn" para dados de série temporal.

Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
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

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.

```json
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

**Pipeline com Atividade de cópia:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é agendado toorun por hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**OracleSource** e **coletor** tipo está definido muito**BlobSink**.  consulta SQL Olá especificada com **oracleReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a>Exemplo: Copiar dados de Blob do Azure tooOracle
Este exemplo mostra como toocopy dados de um armazenamento de BLOBs do Azure tooan locais banco de dados Oracle. No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes de saudação mencionados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.  

exemplo Hello tem Olá entidades da fábrica de dados a seguir:

1. Um serviço vinculado do tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) como fonte e [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) como coletor.

exemplo Hello copia dados de uma tabela de tooa de blob no banco de dados Oracle local a cada hora. Para obter mais informações sobre várias propriedades usadas no exemplo hello, consulte a documentação nas seções a seguir exemplos de saudação.

**Serviço vinculado do Oracle:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Serviço vinculado do armazenamento de Blob do Azure:**
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Conjunto de dados de entrada de Blob do Azure**

Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1). Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa year, month e parte do dia da hora de início da saudação e nome do arquivo usa a parte de hora Olá Olá da hora de início. "externo": "verdadeira" configuração informa o serviço de fábrica de dados de saudação que essa tabela é toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
            "frequency": "Day",
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

**Conjunto de dados de saída Oracle:**

exemplo Hello pressupõe que você tenha criado uma tabela "MyTable" no Oracle. Criar tabela de saudação no Oracle com hello mesmo número de colunas, conforme o esperado toocontain de arquivo CSV de Blob hello. Novas linhas são adicionadas a tabela de toohello a cada hora.

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

**Pipeline com Atividade de cópia:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e hello **coletor** tipo está definido muito**OracleSink**.  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a>Dicas de solução de problemas
### <a name="problem-1-net-framework-data-provider"></a>Problema 1: Provedor de dados do .NET Framework

Veja a seguir Olá **mensagem de erro**:

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

**Possíveis causas:**

1. Olá .NET Framework Data Provider for Oracle não foi instalado.
2. Olá .NET Framework Data Provider for Oracle foi instalada too.NET Framework 2.0 e não for encontrado em pastas de saudação do .NET Framework 4.0.

**Resolução/Solução Alternativa:**

1. Se você ainda não instalou Olá provedor .NET para Oracle, [instalá-lo](http://www.oracle.com/technetwork/topics/dotnet/downloads/) e repita o cenário de saudação.
2. Se você receber a mensagem de erro de saudação mesmo após a instalação do provedor de hello, Olá seguintes etapas:
   1. Abra a configuração de máquina do .NET 2.0 na pasta de saudação: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.
   2. Procurar **provedor de dados Oracle para .NET**, e você deve ser capaz de toofind uma entrada conforme Olá seguindo o exemplo em **System. Data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Provedor de dados oracle para .NET" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" />”
3. Copiar esse arquivo de Machine. config toohello entrada hello v 4.0 pasta a seguir: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config e alteração Olá versão too4.xxx.x.x.
4. Instalar "< caminho do instalado ODP.NET > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll" no cache de assembly global (GAC) do hello executando `gacutil /i [provider path]`. # # dicas de solução de problemas

### <a name="problem-2-datetime-formatting"></a>Problema 2: formatação de datetime

Veja a seguir Olá **mensagem de erro**:

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

**Resolução/Solução Alternativa:**

Cadeia de caracteres de consulta de saudação tooadjust talvez seja necessário em sua atividade de cópia com base em como as datas são configuradas no banco de dados Oracle, conforme mostrado na seguinte Olá exemplo (usando a função to_date Olá):

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a>Mapeamento de tipo para Oracle
Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:

1. Converter nativo tipos too.NET do tipo de origem
2. Converter do tipo de coletor de toonative de tipo .NET

Ao mover dados do Oracle, Olá mapeamentos a seguir é usada com too.NET tipo de dados do Oracle e vice-versa.

| Tipo de dados do Oracle | Tipo de dados do .NET Framework |
| --- | --- |
| BFILE |Byte[] |
| BLOB |Byte[] |
| CHAR |Cadeia de caracteres |
| CLOB |Cadeia de caracteres |
| DATE |DateTime |
| FLOAT |Decimal, cadeia de caracteres (se precisão > 28) |
| INTEGER |Decimal, cadeia de caracteres (se precisão > 28) |
| INTERVALO ano tooMONTH |Int32 |
| INTERVALO dia tooSECOND |TimeSpan |
| LONG |Cadeia de caracteres |
| LONG RAW |Byte[] |
| NCHAR |Cadeia de caracteres |
| NCLOB |Cadeia de caracteres |
| NUMBER |Decimal, cadeia de caracteres (se precisão > 28) |
| NVARCHAR2 |Cadeia de caracteres |
| RAW |Byte[] |
| ROWID |Cadeia de caracteres |
| TIMESTAMP |DateTime |
| TIMESTAMP WITH LOCAL TIME ZONE |DateTime |
| TIMESTAMP WITH TIME ZONE |DateTime |
| UNSIGNED INTEGER |NUMBER |
| VARCHAR2 |Cadeia de caracteres |
| XML |Cadeia de caracteres |

> [!NOTE]
> Tipo de dados **ano intervalo tooMONTH** e **tooSECOND de dia de intervalo** não são suportados ao usar o driver do Microsoft.

## <a name="map-source-toosink-columns"></a>Mapear colunas de toosink de origem
toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Leitura repetida de fontes relacionais
Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais. No Azure Data Factory, você pode repetir a execução de uma fatia manualmente. Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha. Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada. Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
