---
title: aaaMove dados da tabela da Web usando o Azure Data Factory | Microsoft Docs
description: "Saiba mais sobre como toomove de uma tabela em uma Web de páginas de dados usando o Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a>Mover dados de uma fonte de tabela da Web usando o Azure Data Factory
Este artigo descreve como toouse hello atividade de cópia em dados do Azure Data Factory toomove de uma tabela em uma página da Web tooa suporte para o repositório de dados do coletor. Este artigo aproveita Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo que apresenta uma visão geral de movimentação de dados com Copiar atividade e hello lista de repositórios de dados têm suportada como/coletores de fontes.

Fábrica de dados atualmente oferece suporte somente a movimentação de dados de uma data de tooother Web tabela armazena, mas não movendo os dados de outros dados armazena tooa Web tabela de destino.

> [!IMPORTANT]
> No momento, esse conector da Web dá suporte apenas à extração do conteúdo da tabela de uma página HTML. tooretrieve de dados de um ponto de extremidade HTTP/s usar [conector HTTP](data-factory-http-connector.md) em vez disso.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs. 

- toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação. 
- Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. 
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de uma tabela da web, consulte [exemplo JSON: copiar dados da tabela de Web tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) deste artigo. 

Olá seções a seguir fornece detalhes sobre as propriedades JSON que a tabela usada toodefine fábrica de dados entidades tooa específico da Web:

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooWeb vinculado serviço.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **Web** |Sim |
| Url |Origem da URL toohello da Web |Sim |
| authenticationType |Anônima. |Sim |

### <a name="using-anonymous-authentication"></a>Usando a autenticação anônima

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação. Olá typeProperties seção de conjunto de dados do tipo **WebTable** tem Olá seguintes propriedades

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| type |Tipo de conjunto de dados de saudação. deve ser definido muito**WebTable** |Sim |
| path |Um relativa URL toohello de recursos que contém a tabela de saudação. |Não. Quando não for especificado, somente URL Olá especificado na definição de serviço vinculada de saudação é usado. |
| índice |índice de saudação da tabela de saudação no recurso de saudação. Consulte [índice de obtenção de uma tabela em uma página HTML](#get-index-of-a-table-in-an-html-page) seção de índice de toogetting de etapas de uma tabela em uma página HTML. |Sim |

**Exemplo:**

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.

Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

Atualmente, quando a fonte de saudação na atividade de cópia é do tipo **WebSource**, sem propriedades adicionais são suportadas.


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a>Exemplo JSON: copiar dados da tabela de Web tooAzure Blob
Olá mostra de exemplo a seguir:

1. Um serviço vinculado do tipo [Web](#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [WebTable](#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [WebSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados de uma tabela de Web tooan BLOBs do Azure a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

saudação de exemplo a seguir mostra como toocopy dados de uma tabela de Web tooan Azure blob. No entanto, os dados podem ser copiados diretamente tooany de saudação coletores Olá indicado em [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo usando hello atividade de cópia na fábrica de dados do Azure.

**Serviço vinculado do Web** Este exemplo usa Olá Web vinculado de serviço com a autenticação anônima. Confira a seção [Serviço vinculado à Web](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
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

**Conjunto de dados de entrada do WebTable** configuração **externo** muito**true** informa o serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade em Olá fábrica de dados.

> [!NOTE]
> Consulte [índice de obtenção de uma tabela em uma página HTML](#get-index-of-a-table-in-an-html-page) seção de índice de toogetting de etapas de uma tabela em uma página HTML.  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


**Conjunto de dados de saída de Blob do Azure**

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
            "folderPath": "adfgetstarted/Movies"
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

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**WebSource** e **coletor** tipo está definido muito**BlobSink**.

Consulte [propriedades de tipo WebSource](#copy-activity-type-properties) para lista de saudação de propriedades com suporte pelo Olá WebSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a>Obter índice de uma tabela em uma página HTML
1. Iniciar **Excel 2016** e alternar toohello **dados** guia.  
2. Clique em **nova consulta** na barra de ferramentas hello, ponto muito**de outras fontes** e clique em **da Web**.

    ![Menu do Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. Em Olá **da Web** caixa de diálogo, digite **URL** que você usaria no serviço JSON vinculado (por exemplo: https://en.wikipedia.org/wiki/) juntamente com o caminho, você especificaria Olá conjunto de dados (por exemplo: AFI % 27s_100_Years... 100_Movies) e clique em **Okey**.

    ![Do diálogo da Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    URL usada neste exemplo: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies
4. Se você vir **conteúdo da Web de acesso** caixa de diálogo, o direito de saudação selecione **URL**, **autenticação**e clique em **conectar**.

   ![Acessar caixa de diálogo de conteúdo da Web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. Clique em uma **tabela** Olá árvore exibir toosee o conteúdo da tabela de saudação de item e, em seguida, clique em **editar** botão na parte inferior da saudação.  

   ![Diálogo de navegador](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. Em Olá **Editor de consultas** janela, clique em **Editor Avançado** botão na barra de ferramentas de saudação.

    ![Botão Editor Avançado](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. Na caixa de diálogo Editor Avançado hello, Olá número próximo muito "Origem" é o índice de saudação.

    ![Editor Avançado – índice](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

Se você estiver usando o Excel 2013, use [Microsoft Power Query para Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget índice de saudação. Consulte [página de web conectar tooa](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) artigo para obter detalhes. etapas de saudação são semelhantes, se você estiver usando [Microsoft Power BI para a área de trabalho](https://powerbi.microsoft.com/desktop/).

> [!NOTE]
> colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
