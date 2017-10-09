---
title: dados de aaaMove do SAP Business Warehouse usando o Azure Data Factory | Microsoft Docs
description: "Saiba mais sobre como toomove dados do SAP Business Warehouse utilizando a fábrica de dados do Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a>Mover dados do SAP Business Warehouse usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia de dados do Azure Data Factory toomove de um local SAP Business Warehouse (BW). Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.

Você pode copiar dados de um repositório de dados local do SAP Business Warehouse dados repositório tooany suportada coletor. Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente oferece suporte somente a movimentação de dados de um tooother de dados do SAP Business Warehouse armazena, mas não para mover dados de outros dados armazena tooan SAP Business Warehouse. 

## <a name="supported-versions-and-installation"></a>Instalação e versões com suporte
Este conector dá suporte ao SAP Business Warehouse versão 7.x. Ele oferece suporte à cópia de dados do InfoCubes e QueryCubes (incluindo consultas BEx) usando consultas MDX.

tooenable Olá conectividade toohello instância SAP BW, instale Olá componentes a seguir:
- **Gateway de gerenciamento de dados**: Data Factory serviço oferece suporte à conexão de dados locais tooon repositórios (incluindo SAP Business Warehouse) usando um componente denominado Data Management Gateway. toolearn sobre o Gateway de gerenciamento de dados e instruções passo a passo para configurar o gateway hello, consulte [toocloud repositório de dados de repositório de dados movendo entre dados locais](data-factory-move-data-between-onprem-and-cloud.md) artigo. Gateway é necessário mesmo se Olá SAP Business Warehouse estiver hospedado em uma máquina virtual de IaaS do Azure (VM). Você pode instalar o gateway de saudação em Olá mesma VM como dados Olá armazenar ou em uma máquina virtual diferente, contanto que o gateway Olá pode se conectar toohello banco de dados.
- **Biblioteca do SAP NetWeaver** no computador do gateway hello. Você pode obter a biblioteca do SAP Netweaver saudação do administrador do SAP ou diretamente do hello [Centro de Download de Software SAP](https://support.sap.com/swdc). Pesquise Olá **SAP Observação #1025361** local de download de saudação tooget para a versão mais recente do hello. Certifique-se de que a arquitetura Olá para a biblioteca do SAP NetWeaver hello (32 bits ou 64 bits) corresponde à sua instalação de gateway. Instale todos os arquivos incluídos no toohello acordo do SAP NetWeaver RFC SDK de saudação nota da SAP. biblioteca do SAP NetWeaver Olá também está incluída no hello instalação das ferramentas de cliente do SAP.

> [!TIP]
> Coloque dlls Olá extraídos da saudação SDK de RFC NetWeaver na pasta system32.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs. 

- toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação. 
- Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. 
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um local SAP Business Warehouse, consulte [exemplo JSON: copiar dados do SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) deste artigo. 

Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados de SAP BW toodefine usado Data Factory entidades tooan específico:

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooSAP Business Warehouse (BW) vinculado de serviço.

Propriedade | Descrição | Valores permitidos | Obrigatório
-------- | ----------- | -------------- | --------
server | Nome do servidor de saudação no qual Olá SAP BW instância reside. | string | Sim
systemNumber | Número de sistema de saudação sistema SAP BW. | Número decimal de dois dígitos representado como uma cadeia de caracteres. | Sim
clientId | ID do cliente do cliente Olá Olá sistema SAP W. | Número decimal de três dígitos representado como uma cadeia de caracteres. | Sim
Nome de Usuário | Nome de usuário de saudação que tem acesso toohello SAP server | string | Sim
Senha | Senha do usuário hello. | string | Sim
gatewayName | Nome do gateway Olá Olá serviço da fábrica de dados deve usar a instância de SAP BW tooconnect toohello local. | string | Sim
encryptedCredential | cadeia de caracteres de credencial Olá criptografado. | string | Não

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação. Não existem propriedades específicas do tipo de suporte para o conjunto de dados de SAP BW de saudação do tipo **RelationalTable**. 


## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.

Por outro lado, as propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

Quando a fonte na atividade de cópia é do tipo **RelationalSource** (que inclui o SAP BW), Olá propriedades a seguir está disponível na seção de typeProperties:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query | Especifica Olá MDX consulta tooread dados da instância do SAP BW hello. | Consulta MDX. | Sim |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a>Exemplo JSON: copiar dados do SAP Business Warehouse tooAzure Blob
Olá, exemplo a seguir fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Este exemplo mostra como toocopy dados de um tooan do SAP Business Warehouse local armazenamento de BLOBs do Azure. No entanto, os dados podem ser copiados **diretamente** tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.  

> [!IMPORTANT]
> Este exemplo fornece trechos de JSON. Ele não inclui instruções passo a passo para criar a fábrica de dados hello. Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.

exemplo Hello tem Olá entidades da fábrica de dados a seguir:

1. Um serviço vinculado do tipo [SapBw](#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados de uma instância de SAP Business Warehouse tooan BLOBs do Azure por hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação. Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

### <a name="sap-business-warehouse-linked-service"></a>Serviço vinculado do SAP Business Warehouse
Isso vinculado links serviço sua fábrica de dados do SAP BW instância toohello. propriedade do tipo Hello está definida muito**SapBw**. seção de typeProperties Olá fornece informações de conexão para a instância do SAP BW hello. 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Serviço vinculado de armazenamento do Azure
Isso vinculado links serviço sua fábrica de dados de toohello de conta de armazenamento do Azure. propriedade do tipo Hello está definida muito**AzureStorage**. seção de typeProperties Olá fornece informações de conexão para Olá conta de armazenamento do Azure.

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

### <a name="sap-bw-input-dataset"></a>Conjunto de dados de entrada do SAP BW
Este conjunto de dados define o conjunto de dados do hello SAP Business Warehouse. Defina o tipo de saudação do conjunto de dados de Data Factory Olá muito**RelationalTable**. No momento, você não especifica quaisquer propriedades específicas ao tipo para um conjunto de dados do SAP BW. consulta de saudação na definição de atividade de cópia de saudação especifica quais tooread dados da instância do SAP BW Olá. 

Definindo a propriedade externa tootrue informa o serviço de fábrica de dados de saudação tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.

Propriedades de frequência e intervalo define a agenda de saudação. Nesse caso, dados saudação é lido da instância do SAP BW Olá por hora. 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a>Conjunto de dados de saída de Blob do Azure
Este conjunto de dados define o conjunto de dados de Blob do Azure de saída hello. propriedade de tipo de saudação é definida tooAzureBlob. seção de typeProperties Olá fornece onde Olá dados copiados da instância do SAP BW Olá são armazenados. Olá os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a>Pipeline com Atividade de cópia
Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** (de origem SAP BW) e **coletor** tipo está definido muito**BlobSink**. consulta de saudação especificada para hello **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a>Mapeamento de tipo para SAP BW
Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem em duas etapas a seguir:

1. Converter nativo tipos too.NET do tipo de origem
2. Converter do tipo de coletor de toonative de tipo .NET

Ao mover dados do SAP BW, Olá mapeamentos a seguir é usado de tipos de too.NET de tipos do SAP BW.

Tipo de dados no hello ABAP dicionário | Tipo de Dados do .NET
-------------------------------- | --------------
ACCP |  int
CHAR | Cadeia de caracteres
CLNT | Cadeia de caracteres
CURR | Decimal
CUKY | Cadeia de caracteres
DEC | Decimal
FLTP | Duplo
INT1 | Byte
INT2 | Int16
INT4 | int
LANG | string
LCHR | Cadeia de caracteres
LRAW | Byte[]
PREC | Int16
QUAN | Decimal
RAW | Byte[]
RAWSTRING | Byte[]
STRING | Cadeia de caracteres
UNIDADE | string
DATS | Cadeia de caracteres
NUMC | Cadeia de caracteres
TIMS | Cadeia de caracteres

> [!NOTE]
> colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).


## <a name="map-source-toosink-columns"></a>Mapear colunas de toosink de origem
toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Leitura repetida de fontes relacionais
Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais. No Azure Data Factory, você pode repetir a execução de uma fatia manualmente. Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha. Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada. Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
