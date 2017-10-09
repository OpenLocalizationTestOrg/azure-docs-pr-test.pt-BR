---
title: "dados de aaaMove do Salesforce usando a fábrica de dados | Microsoft Docs"
description: Saiba mais sobre como dados de toomove do Salesforce usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a>Mover dados do Salesforce usando o Azure Data Factory
Este artigo descreve como você pode usar a atividade de cópia em um Azure fábrica toocopy de dados de repositório de dados do Salesforce tooany listado na coluna coletor Olá Olá [suporte para origens e coletores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Este artigo aproveita Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia e combinações de repositório de dados com suporte.

A fábrica de dados do Azure atualmente suporta somente a movimentação de dados do Salesforce muito[suporte para armazenamentos de dados do coletor](data-factory-data-movement-activities.md#supported-data-stores-and-formats), mas não oferece suporte a movimentação de dados de outros tooSalesforce de repositórios de dados.

## <a name="supported-versions"></a>Versões com suporte
Esse conector dá suporte a saudação seguintes edições do Salesforce: Developer Edition, Professional Edition, Enterprise Edition ou edição ilimitado. E ele dá suporte à cópia na produção, da área restrita e do domínio personalizado do Salesforce.

## <a name="prerequisites"></a>Pré-requisitos
* A permissão de API deve estar habilitada. Consulte [Como habilito o acesso à API no Salesforce por conjunto de permissões?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)
* toocopy dados de armazenamentos de dados do Salesforce tooon local, você deve ter pelo menos Data Management Gateway 2.0 instalado no seu ambiente local.

## <a name="salesforce-request-limits"></a>Limites da solicitação Salesforce
O Salesforce tem limites para o total de solicitações de API e as solicitações simultâneas de API. Observe Olá pontos a seguir:

- Se o número de saudação de solicitações simultâneas exceder o limite de hello, a limitação ocorre e você verá falhas aleatórias.
- Se o número total de saudação de solicitações excede o limite de hello, Olá conta Salesforce será bloqueado por 24 horas.

Você também pode receber um erro de "REQUEST_LIMIT_EXCEEDED" hello em ambos os cenários. Consulte a seção hello "limites de solicitação de API" hello [limites de desenvolvedor da equipe de vendas](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) artigo para obter detalhes.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados do Salesforce usando diferentes ferramentas/APIs.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir: 

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. 
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados do Salesforce, consulte [exemplo JSON: copiar dados de Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) deste artigo. 

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooSalesforce: 

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá a tabela a seguir fornece descrições dos elementos JSON toohello específico do serviço vinculado da equipe de vendas.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **Salesforce**. |Sim |
| environmentUrl | Especifique a instância de URL da equipe de vendas de saudação. <br><br> – O padrão é "https://login.salesforce.com". <br> -toocopy dados de área restrita, especifique "https://test.salesforce.com". <br> -toocopy dados do domínio personalizado, especificar, por exemplo, "https://[domain].my.salesforce.com". |Não |
| Nome de Usuário |Especifique um nome de usuário para a conta de usuário de saudação. |Sim |
| Senha |Especifique uma senha para a conta de usuário de saudação. |Sim |
| securityToken |Especifique um token de segurança para a conta de usuário de saudação. Consulte [obter token de segurança](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obter instruções sobre como tooreset/obter um token de segurança. em geral, consulte toolearn sobre tokens de segurança [API de segurança e hello](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Sim |

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa de seções e propriedades que estão disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure e outros).

Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação. Olá typeProperties seção um conjunto de dados do tipo hello **RelationalTable** tem Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação na equipe de vendas. |Não (se uma **consulta** de **RelationalSource** for especificada) |

> [!IMPORTANT]
> parte "__c" Olá Olá nome da API é necessária para qualquer objeto personalizado.

![Data Factory — conexão Salesforce — nome da API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa de seções e propriedades que estão disponíveis para a definição de atividades, consulte Olá [criar pipelines](data-factory-create-pipelines.md) artigo. As propriedades como o nome, descrição, tabelas de entrada e saída, e várias políticas estão disponíveis para todos os tipos de atividades.

Propriedades de saudação que estão disponíveis em Olá typeProperties seção de atividade hello, Olá outro lado, variam de acordo com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

Atividade de cópia, quando a fonte de saudação é do tipo hello **RelationalSource** (que inclui a equipe de vendas), Olá propriedades a seguir está disponível na seção de typeProperties:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Uma consulta SQL-92 ou uma consulta [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm). Por exemplo: `select * from MyTable__c`. |Não (se hello **tableName** de saudação **dataset** for especificado) |

> [!IMPORTANT]
> parte "__c" Olá Olá nome da API é necessária para qualquer objeto personalizado.

![Data Factory — conexão Salesforce — nome da API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a>Dicas de consulta
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>Recuperando dados usando a cláusula where na coluna DateTime
Especifique quando a consulta SOQL ou SQL hello, preste atenção toohello diferença de formato de data e hora. Por exemplo:

* **Exemplo de SOQL**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`
* **Exemplo de SQL**:
    * **Usando a consulta de saudação do Assistente de cópia toospecify:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`
    * **Usando JSON editando toospecify Olá consulta (escape char adequadamente):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`

### <a name="retrieving-data-from-salesforce-report"></a>Recuperando dados do relatório do Salesforce
Você pode recuperar dados de relatórios do Salesforce especificando a consulta como `{call "<report name>"}`, por exemplo. `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>Recuperar registros excluídos da lixeira do Salesforce
tooquery registros de saudação flexíveis excluído da Lixeira do Salesforce, você pode especificar **"IsDeleted = 1"** em sua consulta. Por exemplo,

* tooquery somente os registros Olá excluído, especifique "Selecione * de MyTable__c **onde IsDeleted = 1**"
* tooquery todos Olá registros incluindo Olá existente e hello excluído, especifique "Selecione * de MyTable__c **onde IsDeleted = 0 ou IsDeleted = 1**"

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a>Exemplo JSON: copiar dados de Salesforce tooAzure Blob
Olá, exemplo a seguir fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Eles mostram como dados de toocopy da equipe de vendas tooAzure armazenamento de Blob. No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.   

Aqui estão os artefatos de fábrica de dados Olá que você precisará de cenário de saudação do toocreate tooimplement. seções de saudação que siga a lista de saudação fornecem detalhes sobre essas etapas.

* Um serviço vinculado do tipo hello [Salesforce](#linked-service-properties)
* Um serviço vinculado do tipo hello [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Uma entrada [dataset](data-factory-create-datasets.md) do tipo hello [RelationalTable](#dataset-properties)
* Uma saída [dataset](data-factory-create-datasets.md) do tipo hello [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

**Serviço vinculado Salesforce**

Este exemplo usa Olá **Salesforce** serviço vinculado. Consulte Olá [serviço vinculado do Salesforce](#linked-service-properties) seção de propriedades de saudação que são suportados por esse serviço vinculado.  Consulte [obter token de segurança](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obter instruções sobre como tooreset/get hello token de segurança.

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
**Serviço vinculado de armazenamento do Azure**

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
**Conjunto de dados de entrada do Salesforce**

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
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

> [!IMPORTANT]
> parte "__c" Olá Olá nome da API é necessária para qualquer objeto personalizado.

![Data Factory — conexão Salesforce — nome da API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

**Conjunto de dados de saída do blob do Azure**

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
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Pipeline com Atividade de cópia**

Olá, pipeline contém atividade de cópia, o que é configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource**e hello **coletor** tipo está definido muito**BlobSink**.

Consulte [propriedades de tipo RelationalSource](#copy-activity-properties) para lista de saudação de propriedades que são suportados pelo Olá RelationalSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> parte "__c" Olá Olá nome da API é necessária para qualquer objeto personalizado.

![Data Factory — conexão Salesforce — nome da API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a>Mapeamento de tipo para Salesforce
| Tipo Salesforce | Tipo baseado no .NET |
| --- | --- |
| Numeração automática |Cadeia de caracteres |
| Caixa de seleção |Booliano |
| Moeda |Duplo |
| Data |DateTime |
| Data/hora |DateTime |
| Email |Cadeia de caracteres |
| ID |Cadeia de caracteres |
| Relação de pesquisa |Cadeia de caracteres |
| Lista de seleção múltipla |Cadeia de caracteres |
| Número |Duplo |
| Porcentagem |Duplo |
| Telefone |Cadeia de caracteres |
| Lista de seleção |Cadeia de caracteres |
| Texto |Cadeia de caracteres |
| Área de texto |Cadeia de caracteres |
| Área de texto (longo) |Cadeia de caracteres |
| Área de texto (Rich) |Cadeia de caracteres |
| Texto (criptografado) |Cadeia de caracteres |
| URL |Cadeia de caracteres |

> [!NOTE]
> colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a>Desempenho e ajuste
Consulte Olá [atividade de cópia guia de desempenho e ajuste](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
