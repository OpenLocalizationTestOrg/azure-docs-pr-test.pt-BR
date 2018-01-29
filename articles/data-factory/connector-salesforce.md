---
title: Copiar dados de/para Salesforce usando o Azure Data Factory | Microsoft Docs
description: "Saiba como copiar dados do Salesforce para armazenamentos de dados de coletor com suporte (OR) de armazenamentos de dados de fonte com suporte para Salesforce usando uma atividade de cópia em um pipeline do Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2018
ms.author: jingwang
ms.openlocfilehash: 7cd86922b0445fc81766ca54080e2fd3e64a6c61
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2018
---
# <a name="copy-data-fromto-salesforce-using-azure-data-factory"></a>Copiar dados de/para Salesforce usando o Azure Data Factory
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Versão 1 – já disponível](v1/data-factory-salesforce-connector.md)
> * [Versão 2 – Versão prévia](connector-salesforce.md)

Este artigo descreve como usar a atividade de cópia no Azure Data Factory para copiar dados de e para o Salesforce. Ele amplia o artigo [Visão geral da atividade de cópia](copy-activity-overview.md) que apresenta uma visão geral da atividade de cópia.

> [!NOTE]
> Este artigo aplica-se à versão 2 do Data Factory, que está atualmente em versão prévia. Se você estiver usando a versão 1 do serviço Data Factory, que está em GA (disponibilidade geral), consulte [Conector do Salesforce na V1](v1/data-factory-salesforce-connector.md).

## <a name="supported-capabilities"></a>Funcionalidades com suporte

Você pode copiar dados do Salesforce para qualquer armazenamento de dados de coletor com suporte ou copiar dados de qualquer armazenamento de dados de origem com suporte para o Salesforce. Para obter uma lista de armazenamentos de dados com suporte como origens/coletores da atividade de cópia, confira a tabela [Armazenamentos de dados com suporte](copy-activity-overview.md#supported-data-stores-and-formats).

Especificamente, este conector Salesforce dá suporte à:

- As edições a seguir do Salesforce: **Developer Edition, Professional Edition, Enterprise Edition, ou Unlimited Edition**.
- Cópia de dados da **produção, da área restrita e do domínio personalizado** do Salesforce.

## <a name="prerequisites"></a>Pré-requisitos

* A permissão de API deve estar habilitada no Salesforce. Consulte [Como habilito o acesso à API no Salesforce por conjunto de permissões?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)

## <a name="salesforce-request-limits"></a>Limites da solicitação Salesforce

O Salesforce tem limites para o total de solicitações de API e as solicitações simultâneas de API. Observe os seguintes pontos:

- Se o número de solicitações simultâneas exceder o limite, a limitação será atingida e você verá falhas aleatórias.
- Se o número total de solicitações exceder o limite, a conta do Salesforce será bloqueada por 24 horas.

Você também pode receber o erro "REQUEST_LIMIT_EXCEEDED" em ambos os cenários. Veja a seção "Limites de Solicitações da API" no artigo [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) (Limites do Desenvolvedor Salesforce) para obter detalhes.

## <a name="getting-started"></a>Introdução

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

As seções que se seguem fornecem detalhes sobre as propriedades que são usadas para definir entidades do Data Factory específicas ao conector do Salesforce.

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado

As propriedades a seguir têm suporte para o serviço vinculado do Salesforce:

| Propriedade | DESCRIÇÃO | Obrigatório |
|:--- |:--- |:--- |
| Tipo |A propriedade type deve ser definida para: **Salesforce**. |Sim |
| environmentUrl | Especifica a URL da instância do Salesforce. <br> – O padrão é `"https://login.salesforce.com"`. <br> – Para copiar dados da área restrita, especifique `"https://test.salesforce.com"`. <br> – Para copiar dados do domínio personalizado, especifique, por exemplo, `"https://[domain].my.salesforce.com"`. |Não  |
| Nome de Usuário |Especifique um nome de usuário para a conta de usuário. |Sim |
| Senha |Especifique um senha para a conta de usuário.<br/><br/>Você pode optar por marcar este campo como um SecureString para armazená-lo com segurança no ADF, ou armazenar a senha no Azure Key Vault e permitir que o pull de atividade de cópia possa agir a partir daí ao executar a cópia de dados - Saiba mais em [Armazenar Credenciais no Key Vault](store-credentials-in-key-vault.md). |Sim |
| securityToken |Especifique um token de segurança para a conta de usuário. Veja [Obter token de segurança](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para ver instruções sobre como redefinir/obter o token de segurança. Para saber mais sobre os tokens de segurança em geral, veja [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm) (Segurança e a API).<br/><br/>Você pode optar por marcar este campo como um SecureString para armazená-lo com segurança no ADF, ou armazenar o token de segurança no Azure Key Vault e permitir que o pull de atividade de cópia possa agir a partir daí ao executar a cópia de dados - Saiba mais em [Armazenar Credenciais no Key Vault](store-credentials-in-key-vault.md). |Sim |
| connectVia | O [Integration Runtime](concepts-integration-runtime.md) a ser usado para se conectar ao armazenamento de dados. Se não for especificado, ele usa o Integration Runtime padrão do Azure. | Não para a origem, Sim para o coletor se o serviço vinculado à fonte não possuir IR |

>[!IMPORTANT]
>Ao copiar dados **para o** Salesforce, o Microsoft Integration Runtime não poderá ser usado para executar a cópia. Em outras palavras, se seu serviço vinculado à fonte não tiver um IR especificado, explicitamente [crie um IR do Azure](create-azure-integration-runtime.md#create-azure-ir) com um local perto de seu Salesforce e associe no serviço vinculado do Salesforce como o exemplo a seguir.

**Exemplo: armazenar credenciais no ADF**

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<username>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            },
            "securityToken": {
                "type": "SecureString",
                "value": "<security token>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

**Exemplo: Armazenar credencial no Azure Key Vault**

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<username>",
            "password": {
                "type": "AzureKeyVaultSecret",
                "secretName": "<secret name of password in AKV>",
                "store":{
                    "referenceName": "<Azure Key Vault linked service>",
                    "type": "LinkedServiceReference"
                }
            },
            "securityToken": {
                "type": "AzureKeyVaultSecret",
                "secretName": "<secret name of security token in AKV>",
                "store":{
                    "referenceName": "<Azure Key Vault linked service>",
                    "type": "LinkedServiceReference"
                }
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados

Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, confira o artigo sobre [conjuntos de dados](concepts-datasets-linked-services.md). Esta seção fornece uma lista das propriedades com suporte pelo conjunto de dados do Salesforce.

Para copiar dados do Salesforce, defina a propriedade tipo do conjunto de dados como **SalesforceObject**. Há suporte para as seguintes propriedades:

| Propriedade | DESCRIÇÃO | Obrigatório |
|:--- |:--- |:--- |
| Tipo | A propriedade tipo deve ser definida para: **SalesforceObject**  | Sim |
| objectApiName | O nome do objeto de Salesforce para recuperar dados. | Não para fonte, Sim para o coletor |

> [!IMPORTANT]
> A parte "__c" do Nome da API é necessária para qualquer objeto personalizado.

![Data Factory — conexão Salesforce — nome da API](media/copy-data-from-salesforce/data-factory-salesforce-api-name.png)

**Exemplo:**

```json
{
    "name": "SalesforceDataset",
    "properties": {
        "type": "SalesforceObject",
        "linkedServiceName": {
            "referenceName": "<Salesforce linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "objectApiName": "MyTable__c"
        }
    }
}
```

>[!NOTE]
>Para retrocompatibilidade, ao copiar dados de Salesforce, usar o conjunto de dados de tipo "RelationalTable" anterior continuará funcionando, enquanto são sugeridas para alternar para o novo tipo de "SalesforceObject".

| Propriedade | DESCRIÇÃO | Obrigatório |
|:--- |:--- |:--- |
| Tipo | A propriedade type do conjunto de dados deve ser definida como: **RelationalTable** | Sim |
| tableName | Nome da tabela no Salesforce. | Não (se "query" na fonte da atividade for especificada) |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia

Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Pipelines](concepts-pipelines-activities.md). Esta seção fornece uma lista das propriedades com suporte pela fonte e coletor do Salesforce.

### <a name="salesforce-as-source"></a>Salesforce como fonte

Para copiar dados do Salesforce, defina o tipo de origem na atividade de cópia como **SalesforceSource**. As propriedades a seguir têm suporte na seção **source** da atividade de cópia:

| Propriedade | DESCRIÇÃO | Obrigatório |
|:--- |:--- |:--- |
| Tipo | A propriedade tipo da fonte da atividade de cópia deve ser definida como: **SalesforceSource** | Sim |
| query |Utiliza a consulta personalizada para ler os dados. Você pode usar uma consulta SQL-92 ou uma consulta [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm). Por exemplo: `select * from MyTable__c`. | Não (se a "tableName" no conjunto de dados for especificada) |

> [!IMPORTANT]
> A parte "__c" do Nome da API é necessária para qualquer objeto personalizado.

![Data Factory — conexão Salesforce — nome da API](media/copy-data-from-salesforce/data-factory-salesforce-api-name-2.png)

**Exemplo:**

```json
"activities":[
    {
        "name": "CopyFromSalesforce",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Salesforce input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "SalesforceSource",
                "query": "SELECT Col_Currency__c, Col_Date__c, Col_Email__c FROM AllDataType__c"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

>[!NOTE]
>Para retrocompatibilidade, ao copiar dados de Salesforce, usar o conjunto de dados de tipo "RelationalTable" anterior continuará funcionando, enquanto são sugeridas para alternar para o novo tipo de "SalesforceObject".

### <a name="salesforce-as-sink"></a>Salesforce como coletor

Para copiar dados do Salesforce, defina o tipo de coletor na atividade de cópia como **SalesforceSink**. As propriedades a seguir têm suporte na seção **sink** da atividade de cópia:

| Propriedade | DESCRIÇÃO | Obrigatório |
|:--- |:--- |:--- |
| Tipo | A propriedade type do coletor da atividade de cópia deve ser definida como: **SalesforceSink** | Sim |
| writeBehavior | O comportamento da operação de gravação.<br/>Valores permitidos são: **inserir**, e **Upsert**. | Não (o padrão é Insert) |
| externalIdFieldName | O nome do campo de ID externo para operação upsert. O campo especificado deve ser definido como "Campo de Id externa" no objeto de Salesforce, e ele não pode ter valores nulos nos dados de entrada correspondentes. | Sim para "Upsert" |
| writeBatchSize | A contagem de linhas de dados gravados no Salesforce em cada lote. | Não (o padrão é 5000) |
| ignoreNullValues | Indica se deve ignorar valores nulos de dados de entrada durante a operação de gravação.<br/>Os valores permitidos são: **True** e **False**.<br>- **true**: deixe os dados no objeto de destino inalterados ao fazer a operação upsert/atualização e insira valor definido pelo padrão ao fazer a operação de inserção.<br/>- **false**: atualize os dados no objeto de destino inalterados para NULL ao fazer a operação upsert/atualização e insira valor definido pelo padrão ao fazer a operação de inserção. | Não (padrão é falso) |

### <a name="example-salesforce-sink-in-copy-activity"></a>Exemplo: coletor Salesforce na atividade de cópia

```json
"activities":[
    {
        "name": "CopyToSalesforce",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Salesforce output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "SalesforceSink",
                "writeBehavior": "Upsert",
                "externalIdFieldName": "CustomerId__c",
                "writeBatchSize": 10000,
                "ignoreNullValues": true
            }
        }
    }
]
```

## <a name="query-tips"></a>Dicas de consulta

### <a name="retrieving-data-from-salesforce-report"></a>Recuperando dados do relatório do Salesforce

Você pode recuperar dados de relatórios do Salesforce especificando a consulta como `{call "<report name>"}`. Exemplo: `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>Recuperar registros excluídos da lixeira do Salesforce

Para consultar os registros excluídos pelo software da lixeira do Salesforce, você poderá especificar **"IsDeleted = 1"** em sua consulta. Por exemplo,

* Para consultar apenas os registros excluídos, especifique "select * from MyTable__c **where IsDeleted= 1**"
* Para consultar todos os registros, incluindo existentes e excluídos, especifique "select * from MyTable__c **m que IsDeleted = 0 ou IsDeleted = 1**"

### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>Recuperando dados usando a cláusula where na coluna DateTime

Ao especificar a consulta SQL ou SOQL, preste atenção à diferença de formato DateTime. Por exemplo: 

* **Exemplo de SOQL**:`SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= @{formatDateTime(pipeline().parameters.StartTime,'yyyy-MM-ddTHH:mm:ssZ')} AND LastModifiedDate < @{formatDateTime(pipeline().parameters.EndTime,'yyyy-MM-ddTHH:mm:ssZ')}`
* **Exemplo de SQL**: `SELECT * FROM Account WHERE LastModifiedDate >= {ts'@{formatDateTime(pipeline().parameters.StartTime,'yyyy-MM-dd HH:mm:ss')}'} AND LastModifiedDate < {ts'@{formatDateTime(pipeline().parameters.EndTime,'yyyy-MM-dd HH:mm:ss')}'}"`

## <a name="data-type-mapping-for-salesforce"></a>Mapeamento de tipo de dados para Salesforce

Ao copiar dados do Salesforce, os seguintes mapeamentos são usados de tipos de dados do Salesforce para tipos de dados provisórios do Azure Data Factory. Consulte [Mapeamentos de tipo de dados e esquema](copy-activity-schema-and-type-mapping.md) para saber mais sobre como a atividade de cópia mapeia o tipo de dados e esquema de origem para o coletor.

| Tipo de dados do Salesforce | Tipo de dados provisório do Data Factory |
|:--- |:--- |
| Numeração automática |Cadeia de caracteres |
| Caixa de seleção |BOOLEAN |
| Moeda |Duplo |
| Data |Datetime |
| Data/hora |Datetime |
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

## <a name="next-steps"></a>Próximas etapas
Para obter uma lista de armazenamentos de dados com suporte como origens e coletores pela atividade de cópia no Azure Data Factory, consulte [Armazenamentos de dados com suporte](copy-activity-overview.md#supported-data-stores-and-formats).