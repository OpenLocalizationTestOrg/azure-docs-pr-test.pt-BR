---
title: dados de aaaMove do DB2 usando o Azure Data Factory | Microsoft Docs
description: "Saiba como toomove dados do DB2 local banco de dados usando a atividade de cópia de fábrica de dados do Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a>Mover dados do DB2 usando a Atividade de Cópia do Azure Data Factory
Este artigo descreve como você pode usar a atividade de cópia em dados do Azure Data Factory toocopy de um repositório de dados do tooa de banco de dados do DB2 de local. Você pode copiar o repositório de tooany de dados que está listado como um coletor com suporte no hello [as atividades de movimentação de dados do Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats) artigo. Este tópico se baseia no artigo de fábrica de dados hello, que apresenta uma visão geral de movimentação de dados usando a atividade de cópia e lista de combinações de repositório de dados Olá com suporte. 

Fábrica de dados atualmente oferece suporte à movimentação de dados somente de um tooa de banco de dados DB2 [repositório de dados com suporte do coletor](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Movimentação de dados de outros dados armazena tooa não há suporte para o banco de dados do DB2.

## <a name="prerequisites"></a>Pré-requisitos
Fábrica de dados oferece suporte a banco de dados DB2 local de conexão tooan usando Olá [gateway de gerenciamento de dados](data-factory-data-management-gateway.md). Para instruções passo a passo tooset os dados de gateway Olá pipeline toomove seus dados, consulte Olá [mover dados de local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artigo.

Mesmo se hello DB2 estiver hospedado no Azure IaaS VM, é necessário um gateway. Você pode instalar o gateway de Olá Olá mesmo IaaS VM como Olá repositório de dados. Se o gateway Olá pode se conectar a banco de dados toohello, você pode instalar o gateway de saudação em uma máquina virtual diferente.

gateway de gerenciamento de dados Olá fornece um driver DB2 interno, portanto você não precisa toomanually instalar um toocopy de dados do driver do DB2.

> [!NOTE]
> Para obter dicas sobre solução de problemas do gateway e conexão, consulte Olá [solucionar problemas do gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) artigo.


## <a name="supported-versions"></a>Versões com suporte
conector Olá DB2 da fábrica de dados oferece suporte a saudação plataformas IBM DB2 e versões com o Gerenciador de acesso ao banco de dados arquitetura DRDA (Distributed Relational) SQL versões 9, 10 e 11 a seguir:

* IBM DB2 para z/OS versão 11.1
* IBM DB2 para z/OS versão 10.1
* IBM DB2 para i (AS400) versão 7.2
* IBM DB2 para i (AS400) versão 7.1
* IBM DB2 para LUW (Linux, UNIX e Windows) versão 11
* IBM DB2 para LUW versão 10.5
* IBM DB2 para LUW versão 10.1

> [!TIP]
> Se você receber a mensagem de erro hello "hello pacote correspondente tooan SQL instrução solicitação de execução não foi encontrada. SQLSTATE = 51002 SQLCODE =-805, "motivo Olá é um pacote necessário não foi criado para o usuário normal Olá Olá SO. tooresolve esse problema, siga estas instruções para seu tipo de servidor DB2:
> - DB2 para i (AS400): permitem que um usuário avançado Criar coleção de saudação de usuário normal Olá antes de executar a atividade de cópia. coleção de saudação toocreate, use Olá comando:`create collection <username>`
> - O DB2 for z/OS ou LUW: Use uma conta de privilégios altos – um usuário avançado ou administrador que tem autoridades de pacote e de associação, BINDADD, CONCEDER permissões de tooPUBLIC de executar – cópia de saudação toorun uma vez. pacote necessário Olá é criado automaticamente durante a cópia de saudação. Posteriormente, você pode alternar usuário normal toohello voltar para a execução de cópia subsequentes.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma cópia de dados de toomove de atividade de um repositório de dados DB2 local usando diversas ferramentas e APIs: 

- toocreate de maneira mais fácil de saudação um pipeline é toouse Olá Assistente para cópia de fábrica de dados do Azure. Para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de saudação, consulte Olá [Tutorial: criar um pipeline usando o Assistente para cópia de saudação](data-factory-copy-data-wizard-tutorial.md). 
- Você também pode usar ferramentas toocreate um pipeline, incluindo Olá portal do Azure, Visual Studio, do PowerShell do Azure, um Gerenciador de recursos do Azure modelo, Olá API .NET e Olá API REST. Para obter instruções passo a passo toocreate um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Crie a fábrica de dados tooyour do repositórios de dados de entrada e saída de toolink serviços vinculados.
2. Criar conjuntos de dados toorepresent entrada e saída de dados para a operação de cópia de saudação. 
3. Criar um pipeline com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. 

Quando você usa Olá Assistente para cópia, definições de JSON para serviços de fábrica de dados vinculado hello, conjuntos de dados e entidades de pipeline são criados automaticamente para você. Quando você usar ferramentas ou APIs (exceto Olá API .NET), você define entidades da fábrica de dados de saudação usando o formato JSON de saudação. Olá [exemplo JSON: copiar dados do DB2 tooAzure armazenamento de Blob](#json-example-copy-data-from-db2-to-azure-blob) mostra definições de JSON Olá para Olá entidades da fábrica de dados que são usados toocopy dados de um repositório de dados DB2 local.

Olá seções a seguir fornece detalhes sobre Olá propriedades JSON que são usadas toodefine Olá fábrica de dados entidades específico tooa DB2 repositório de dados.

## <a name="db2-linked-service-properties"></a>Propriedades do serviço vinculado do DB2
Olá, a tabela a seguir lista propriedades JSON de saudação tooa específico do serviço vinculado do DB2.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| **tipo** |Essa propriedade deve ser definida muito**OnPremisesDB2**. |Sim |
| **server** |nome de saudação do servidor de saudação DB2. |Sim |
| **database** |nome de saudação do banco de dados de saudação DB2. |Sim |
| **schema** |nome de saudação do esquema de saudação no banco de dados do DB2 de saudação. Essa propriedade diferencia maiúsculas de minúsculas. |Não |
| **authenticationType** |tipo de saudação de autenticação que é o banco de dados usado tooconnect toohello DB2. Olá os valores possíveis são: anônima, básica e do Windows. |Sim |
| **username** |Olá nome hello conta de usuário se você usar a autenticação básica ou do Windows. |Não |
| **password** |Olá senha Olá conta de usuário. |Não |
| **gatewayName** |nome de saudação de gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello local DB2. |Sim |

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista de seções de saudação e propriedades que estão disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. Seções, como **estrutura**, **disponibilidade**e hello **política** um conjunto de dados JSON, são semelhantes para todos os tipos de conjunto de dados (SQL Azure, armazenamento de BLOBs do Azure, tabela do Azure armazenamento e assim por diante).

Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação. Olá **typeProperties** seção um conjunto de dados do tipo **RelationalTable**, que inclui o conjunto de dados Olá DB2, tem Olá propriedade a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| **tableName** |Olá nome da tabela de saudação na instância de banco de dados de saudação DB2 que Olá serviço vinculado se refere. Essa propriedade diferencia maiúsculas de minúsculas. |Não (se hello **consulta** propriedade de uma atividade de cópia do tipo **RelationalSource** for especificado) |

## <a name="copy-activity-properties"></a>Propriedades da Atividade de Cópia
Para obter uma lista de seções de saudação e propriedades que estão disponíveis para a definição de atividades de cópia, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades da Atividade de Cópia, como **name**, **description**, tabela **inputs**, tabela **outputs** e **policy** estão disponíveis para todos os tipos de atividade. Olá propriedades que estão disponíveis no hello **typeProperties** seção de atividade Olá para cada tipo de atividade. Para a atividade de cópia, propriedades de saudação variam dependendo Olá tipos de fontes de dados e coletores.

Para a atividade de cópia, quando a fonte de saudação é do tipo **RelationalSource** (que inclui DB2), Olá propriedades a seguir está disponível no hello **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| **query** |Use Olá consulta personalizada tooread Olá dados. |Cadeia de caracteres de consulta SQL. Por exemplo: `"query": "select * from "MySchema"."MyTable""` |Não (se hello **tableName** propriedade de um conjunto de dados for especificada) |

> [!NOTE]
> Os nomes de esquema e tabela diferenciam maiúsculas de minúsculas. Na instrução de consulta hello, colocar os nomes de propriedade usando "" (aspas duplas). Por exemplo:
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a>Exemplo JSON: copiar dados do DB2 tooAzure armazenamento de Blob
Este exemplo fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). exemplo Hello mostra como banco de dados toocopy um DB2 dados tooBlob armazenamento. No entanto, os dados podem ser copiados muito[tipo de coletor de armazenar os dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a atividade de cópia de fábrica de dados do Azure.

exemplo Hello tem Olá entidades da fábrica de dados a seguir:

- Um serviço vinculado do DB2 do tipo [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)
- Um serviço vinculado de armazenamento de Blobs do Azure do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
- Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)
- Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
- Um [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que usa Olá [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) propriedades

exemplo Hello copia dados de um resultado de consulta em um banco de dados de DB2 tooan BLOBs do Azure por hora. propriedades JSON Olá que são usadas no exemplo hello são descritas nas seções Olá seguir definições de entidade hello.

Primeiramente, instale e configure um gateway de dados. Olá as instruções são [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

**Serviço vinculado do DB2**

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

**Serviço vinculado do armazenamento de Blob do Azure**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

**Conjunto de dados de entrada do DB2**

exemplo Hello pressupõe que você criou uma tabela denominada "MyTable" que tem uma coluna chamada "timestamp" dos dados de série de tempo de saudação do DB2.

Olá **externo** propriedade for definida muito "true". Essa configuração informa o serviço de fábrica de dados de saudação que este conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello. Observe que Olá **tipo** propriedade for definida muito**RelationalTable**.


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

**Conjunto de dados de saída de Blob do Azure**

Os dados são gravados tooa novo blob a cada hora por configuração Olá **frequência** propriedade muito "Hora" e hello **intervalo** too1 de propriedade. Olá **folderPath** propriedade para o blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e hora Olá Olá da hora de início.

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Pipeline de atividade de cópia de saudação**

pipeline de saudação contém uma atividade de cópia que está configurada toouse especificado conjuntos de dados de entrada e saídos e que é toorun agendado a cada hora. Na definição JSON para o pipeline de saudação do hello, Olá **fonte** tipo está definido muito**RelationalSource** e hello **coletor** tipo está definido muito**BlobSink**. consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá "Orders" tabela.

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a>Mapeamento de tipo para DB2
Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, atividade de cópia executa conversões de tipo automática de tipo de toosink de tipo de fonte usando Olá abordagem em duas etapas a seguir:

1. Converter de um tipo de .NET native fonte tipo tooa
2. Converter de um tipo de coletor nativo de tooa de tipo .NET

mapeamentos de seguir Hello são usados quando copiar atividade converte dados de saudação de um tipo de .NET do DB2 tipo tooa:

| Tipo do banco de dados DB2 | Tipo .NET Framework |
| --- | --- |
| SmallInt |Int16 |
| Número inteiro |Int32 |
| BigInt |Int64 |
| Real |Single |
| Duplo |Duplo |
| Float |Duplo |
| Decimal |Decimal |
| DecimalFloat |Decimal |
| Numérico |Decimal |
| Data |DateTime |
| Hora |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |Cadeia de caracteres |
| VarChar |Cadeia de caracteres |
| LongVarChar |Cadeia de caracteres |
| DB2DynArray |Cadeia de caracteres |
| Binário |Byte[] |
| VarBinary |Byte[] |
| LongVarBinary |Byte[] |
| Graphic |Cadeia de caracteres |
| VarGraphic |Cadeia de caracteres |
| LongVarGraphic |Cadeia de caracteres |
| Clob |Cadeia de caracteres |
| Blob |Byte[] |
| DbClob |Cadeia de caracteres |
| SmallInt |Int16 |
| Número inteiro |Int32 |
| BigInt |Int64 |
| Real |Single |
| Duplo |Duplo |
| Float |Duplo |
| Decimal |Decimal |
| DecimalFloat |Decimal |
| Numérico |Decimal |
| Data |DateTime |
| Hora |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |Cadeia de caracteres |

## <a name="map-source-toosink-columns"></a>Mapear colunas de toosink de origem
toolearn como colunas toomap Olá toocolumns de conjunto de dados de origem no conjunto de dados de coletor Olá, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-reads-from-relational-sources"></a>Leituras repetidas de fontes relacionais
Quando você copiar dados de um repositório de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais. No Azure Data Factory, você pode repetir a execução de uma fatia manualmente. Você também pode configurar a repetição de saudação **política** propriedade para um conjunto de dados de toorerun uma fatia quando ocorre uma falha. Certifique-se de que Olá tais dados são lidos não importa como fatia de saudação muitas vezes é independentemente de como você executar novamente a fatia hello e execute novamente. Para saber mais, confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Desempenho e ajuste
Saiba mais sobre os principais fatores que afetam o desempenho de saudação do desempenho de toooptimize de atividade de cópia e maneiras de saudação [Copiar atividade guia de desempenho e ajuste](data-factory-copy-activity-performance.md).
