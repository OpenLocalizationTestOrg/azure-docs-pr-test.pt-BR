---
title: aaaMove dados de armazenamentos de dados ODBC | Microsoft Docs
description: "Saiba mais sobre como os dados toomove de dados ODBC armazena utilizando a fábrica de dados do Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a>Mover dados de armazenamentos de dados ODBC usando o Azure Data Factory
Este artigo explica como armazenar toouse hello atividade de cópia em dados de toomove do Azure Data Factory de um local de dados ODBC. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.

Você pode copiar dados de um repositório de dados ODBC dados repositório tooany suportada coletor. Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente suporta apenas mover tooother repositórios de dados de repositório de dados de uma data ODBC, mas não para movimentação de dados de repositório de dados ODBC de tooan para repositórios de outros dados. 

## <a name="enabling-connectivity"></a>Habilitando a conectividade
Serviço da fábrica de dados oferece suporte a fontes ODBC conexão local tooon usando Olá Data Management Gateway. Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação. Use o armazenamento de dados ODBC Olá gateway tooconnect tooan mesmo se ele estiver hospedado em uma VM de IaaS do Azure.

Você pode instalar o gateway de saudação em Olá mesmo local do computador ou Olá VM do Azure como armazenamento de dados ODBC hello. No entanto, recomendamos que você instale o gateway de saudação em um computador separado/Azure IaaS VM tooavoid contenção de recursos e para melhorar o desempenho. Quando você instalar o gateway de saudação em um computador separado, máquina Olá deve ser tooaccess capaz de máquina de saudação com armazenamento de dados ODBC hello.

Olá Data Management Gateway, além de também é necessário o driver ODBC do tooinstall Olá para Olá repositório de dados no computador do gateway hello.

> [!NOTE]
> Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados de um repositório de dados ODBC usando diferentes ferramentas/APIs.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir: 

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. 
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados ODBC, consulte [exemplo JSON: tooAzure Blob do repositório de dados de cópia de dados ODBC](#json-example-copy-data-from-odbc-data-store-to-azure-blob) deste artigo. 

Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados usado toodefine fábrica de dados entidades tooODBC específico:

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooODBC vinculado serviço.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **OnPremisesOdbc** |Sim |
| connectionString |Olá credencial de acesso não parte de cadeia de caracteres de conexão hello e opcional criptografados credencial. Consulte exemplos Olá seções a seguir. |Sim |
| credencial |parte de credencial de acesso Olá de cadeia de caracteres de conexão de saudação especificada no formato de valor de propriedade específica do driver. Exemplo: "Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;". |Não |
| authenticationType |Tipo de autenticação usado o repositório de dados ODBC tooconnect toohello. Os valores possíveis são: Anonymous e Basic. |Sim |
| Nome de Usuário |Especifique o nome de usuário se você estiver usando a autenticação Básica. |Não |
| Senha |Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação. |Não |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar armazenamento de dados ODBC tooconnect toohello. |Sim |

### <a name="using-basic-authentication"></a>Usando a autenticação Básica

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a>Usando a autenticação Básica com credenciais criptografadas
Você pode criptografar credenciais Olá Olá [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versão do Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 versão ou anterior do hello PowerShell do Azure).  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>Usando a autenticação anônima

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação. Olá typeProperties seção de conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados do ODBC) tem Olá seguintes propriedades

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação no repositório de dados ODBC hello. |Sim |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.

As propriedades disponíveis no hello **typeProperties** seção de atividade Olá Olá outro lado variam de acordo com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

Atividade de cópia, quando a fonte é do tipo **RelationalSource** (que inclui ODBC), Olá propriedades a seguir está disponível na seção de typeProperties:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: select * from MyTable. |Sim |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a>Exemplo JSON: tooAzure Blob do repositório de dados de cópia de dados ODBC
Este exemplo fornece definições de JSON que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Ele mostra como tooan armazenamento de BLOBs do Azure da fonte de dados de toocopy do ODBC. No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.

exemplo Hello tem Olá entidades da fábrica de dados a seguir:

1. Um serviço vinculado do tipo [OnPremisesOdbc](#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados de um resultado de consulta em um repositório de dados ODBC tooa blob a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação. Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

**Serviço vinculado do ODBC** Este exemplo usa Olá autenticação básica. Veja a seção [Serviço vinculado a ODBC](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
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

**Conjunto de dados de entrada do ODBC**

exemplo Hello supõe que você criou uma tabela "MyTable" em um banco de dados ODBC e contém uma coluna chamada "timestampcolumn" para dados de série temporal.

Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


**Atividade de cópia em um pipeline com origem ODBC (RelationalSource) e coletor Blob (BlobSink)**

pipeline de saudação contém uma atividade de cópia que esteja configurado toouse esses conjuntos de dados de entrada e saídos e toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** e **coletor** tipo está definido muito**BlobSink**. consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.

```json
{
    "name": "CopyODBCToBlob",
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
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a>Mapeamento de tipos para ODBC
Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem em duas etapas a seguir:

1. Converter nativo tipos too.NET do tipo de origem
2. Converter do tipo de coletor de toonative de tipo .NET

Ao mover dados de armazenamentos de dados ODBC, tipos de dados ODBC são tipos de too.NET mapeadas conforme mencionado em Olá [mapeamentos de tipo de dados ODBC](https://msdn.microsoft.com/library/cc668763.aspx) tópico.

## <a name="map-source-toosink-columns"></a>Mapear colunas de toosink de origem
toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Leitura repetida de fontes relacionais
Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais. No Azure Data Factory, você pode repetir a execução de uma fatia manualmente. Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha. Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada. Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="ge-historian-store"></a>Repositório GE Historian
Criar um toolink de serviço vinculado de ODBC um [GE Proficy historiador (agora historiador GE)](http://www.geautomation.com/products/proficy-historian) tooan data factory do Azure do repositório de dados conforme mostrado no exemplo a seguir de saudação:

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

Instalar o Gateway de gerenciamento de dados em uma máquina local e registrar gateway Olá Olá portal. gateway Olá instalado no computador local usa o driver ODBC Olá para GE historiador tooconnect toohello repositório de dados historiador GE. Portanto, instale o driver Olá se ele não estiver instalado no computador do gateway hello. Veja a seção [Habilitando a conectividade](#enabling-connectivity) para obter detalhes.

Antes de usar Olá GE historiador armazenar em uma solução de fábrica de dados, verifique se gateway Olá pode se conectar a toohello repositório de dados usando as instruções na próxima seção, Olá.

Artigo de saudação de leitura desde o início de saudação para uma visão geral detalhada do uso de dados ODBC armazena como repositórios de dados de origem em uma operação de cópia.  

## <a name="troubleshoot-connectivity-issues"></a>Solucionar problemas de conectividade
tootroubleshoot problemas de conexão, use Olá **diagnóstico** guia de **Gerenciador de configuração de Gateway de gerenciamento de dados**.

1. Iniciar o **Gerenciador de Configuração de Gateway de Gerenciamento de Dados**. Você pode executar "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" diretamente (ou) pesquisa para **Gateway** toofind um link muito**Microsoft Data Management Gateway** aplicativo conforme Olá a imagem a seguir.

    ![Gateway de pesquisa](./media/data-factory-odbc-connector/search-gateway.png)
2. Alternar toohello **diagnóstico** guia.

    ![Diagnóstico de gateway](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. Selecione Olá **tipo** de dados armazenar (serviço vinculado).
4. Especifique **autenticação** e digite **credenciais** (ou) Insira **cadeia de caracteres de conexão** que é o repositório de dados de toohello tooconnect usado.
5. Clique em **Testar conexão** tootest Olá conexão toohello dados repositório.

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
