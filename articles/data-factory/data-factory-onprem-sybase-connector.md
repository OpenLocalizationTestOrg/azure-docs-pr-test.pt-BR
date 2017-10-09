---
title: dados de aaaMove do Sybase usando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como toomove dados do banco de dados Sybase usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ad003ec502028d56db9570fe08af329eb5b71817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a>Mover dados do Sybase usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia de dados do Azure Data Factory toomove de banco de dados Sybase local. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.

Você pode copiar dados de um repositório de dados local Sybase dados repositório tooany suportada coletor. Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente suporta apenas mover tooother repositórios de dados de repositório de dados de um de dados Sybase, mas não para mover dados de outro armazenamento de dados dados repositórios tooa Sybase. 

## <a name="prerequisites"></a>Pré-requisitos
Serviço da fábrica de dados oferece suporte a fontes de Sybase local tooon conexão usando Olá Gateway de gerenciamento de dados. Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação.

Gateway é necessário mesmo que o banco de dados do Sybase Olá é hospedado em uma VM de IaaS do Azure. Você pode instalar o gateway de saudação em Olá mesmo IaaS VM como Olá dados armazenar ou em uma máquina virtual diferente, contanto que o gateway Olá pode se conectar toohello banco de dados.

> [!NOTE]
> Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.

## <a name="supported-versions-and-installation"></a>Instalação e versões com suporte
Para Gateway de gerenciamento de dados tooconnect toohello banco de dados Sybase, você precisa Olá tooinstall [provedor de dados do Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 ou acima em Olá mesmo sistema como Olá Gateway de gerenciamento de dados. Há suporte para o Sybase versão 16 e superior.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs. 

- toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação. 
- Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. 
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados Sybase local, consulte [exemplo JSON: copiar dados do Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) deste artigo. 

Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados de Sybase toodefine usado Data Factory entidades tooa específico:

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooSybase vinculado serviço.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **OnPremisesSybase** |Sim |
| server |Nome do servidor do Sybase hello. |Sim |
| database |Nome do banco de dados do Sybase hello. |Sim |
| schema |Nome do esquema de saudação no banco de dados de saudação. |Não |
| authenticationType |Tipo de autenticação usado o banco de dados do Sybase tooconnect toohello. Os valores possíveis são: Anonymous, Basic e Windows. |Sim |
| Nome de Usuário |Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows. |Não |
| Senha |Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação. |Não |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados Sybase local de toohello de tooconnect. |Sim |

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação. Olá **typeProperties** seção de conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados Sybase) tem Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação em Olá instância de banco de dados Sybase serviço vinculado refere-se a. |Não (se **query** de **RelationalSource** for especificado) |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para definir as atividades, consulte o artigo [Criando pipelines](data-factory-create-pipelines.md). As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.

Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

Quando a fonte de saudação é do tipo **RelationalSource** (que inclui Sybase), Olá propriedades a seguir está disponível em **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: select * from MyTable. |Não (se **tableName** de **dataset** for especificado) |


## <a name="json-example-copy-data-from-sybase-tooazure-blob"></a>Exemplo JSON: copiar dados do Sybase tooAzure Blob
Olá, exemplo a seguir fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Eles mostram como banco de dados toocopy do Sybase dados tooAzure armazenamento de Blob. No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.   

exemplo Hello tem Olá entidades da fábrica de dados a seguir:

1. Um serviço vinculado do tipo [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados de um resultado de consulta no blob de tooa do banco de dados Sybase a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação. Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

**Serviço vinculado Sybase:**

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
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

**Serviço vinculado do armazenamento de Blob do Azure:**

```JSON
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

**Conjunto de dados de entrada do Sybase:**

exemplo Hello supõe que você criou uma tabela "MyTable" na Sybase e contém uma coluna chamada "timestamp" para dados de série temporal.

Definindo "externo": true informa o serviço de fábrica de dados de saudação que este conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello. Observe que Olá **tipo** Olá serviço vinculado está definido como: **RelationalTable**.

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
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
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é agendado toorun por hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** e **coletor** tipo está definido muito**BlobSink**. consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados saudação da saudação DBA. Tabela de pedidos no banco de dados de saudação.

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
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
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a>Mapeamento de tipo para Sybase
Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, hello atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:

1. Converter nativo tipos too.NET do tipo de origem
2. Converter do tipo de coletor de toonative de tipo .NET

Sybase dá suporte a T-SQL e tipos T-SQL. Para uma tabela de mapeamento de tipo de too.NET de tipos de sql, consulte [conector do SQL Azure](data-factory-azure-sql-connector.md) artigo.

## <a name="map-source-toosink-columns"></a>Mapear colunas de toosink de origem
toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Leitura repetida de fontes relacionais
Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais. No Azure Data Factory, você pode repetir a execução de uma fatia manualmente. Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha. Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada. Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
