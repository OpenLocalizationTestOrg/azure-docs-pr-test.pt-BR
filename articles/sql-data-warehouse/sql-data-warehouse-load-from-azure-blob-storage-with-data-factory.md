---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: armazenamento de blob de dados aaaLoad do Azure no Azure SQL Data Warehouse (Azure Data Factory) | Microsoft Docs
description: Saiba mais dados tooload com o Azure Data Factory
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 689fb02e-eb98-4f7c-81e6-6c1d22d53901
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: barbkess
ms.custom: loading
ms.openlocfilehash: 29a220679a11cedefb0dfd06c0a6838f81a90447
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a>Carregar dados do Armazenamento de Blobs do Azure no Azure SQL Data Warehouse (Azure Data Factory).
> [!div class="op_single_selector"]
> * [Fábrica de dados](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 Este tutorial mostra como toocreate um pipeline de dados do Azure Data Factory toomove de tooSQL de Blob de armazenamento do Azure Data Warehouse. Com hello etapas a seguir, você irá:

* Configurar dados de exemplo em um Blob de Armazenamento do Azure.
* Conecte-se recursos tooAzure fábrica de dados.
* Crie um pipeline de dados de toomove de tooSQL de Blobs de armazenamento do Data Warehouse.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>Antes de começar
toofamiliarize-se com a fábrica de dados do Azure, consulte [tooAzure Introdução fábrica de dados][Introduction tooAzure Data Factory].

### <a name="create-or-identify-resources"></a>Criar ou identificar recursos
Antes de iniciar este tutorial, você precisa toohave Olá recursos a seguir.

* **Blob de armazenamento do Azure**: Este tutorial usa blobs de armazenamento do Azure como fonte de dados Olá para o pipeline do Azure Data Factory hello e, portanto você precisa de dados de exemplo de saudação do toohave um toostore disponíveis. Se você não tiver um já, saiba como muito[criar uma conta de armazenamento][Create a storage account].
* **SQL Data Warehouse**: estes tutorial move Olá dados de Blob de armazenamento do Azure muito SQL Data Warehouse e, portanto precisam de toohave um data warehouse online que é carregado com hello dados de exemplo AdventureWorksDW. Se você ainda não tiver um data warehouse, saiba como muito[provisionar um][Create a SQL Data Warehouse]. Se você tiver um data warehouse, mas não foi provisionada com dados de exemplo hello, você pode [carregá-lo manualmente][Load sample data into SQL Data Warehouse].
* **O Azure Data Factory**: Azure Data Factory concluirá a carga real hello e, portanto você toohave um que você pode usar o pipeline de movimentação de dados toobuild hello. Se você não tiver um já, saiba como toocreate uma etapa 1 de [Introdução ao Azure Data Factory (Editor de fábrica de dados)][Get started with Azure Data Factory (Data Factory Editor)].
* **AZCopy**: você precisa os dados de exemplo hello AZCopy toocopy do tooyour seu cliente local Blob de armazenamento do Azure. Para obter instruções de instalação, consulte Olá [AZCopy documentação][AZCopy documentation].

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a>Etapa 1: Copiar dados de exemplo tooAzure Blob de armazenamento
Uma vez que todas as partes de saudação pronto, você está pronto toocopy exemplo dados tooyour Blob de armazenamento do Azure.

1. [Baixe os dados de exemplo][Download sample data]. Esses dados adicionará outro três anos de dados de vendas tooyour dados de exemplo AdventureWorksDW.
2. Use esta saudação do AZCopy comando toocopy três anos de dados tooyour Blob de armazenamento do Azure.

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-tooazure-data-factory"></a>Etapa 2: Conectar recursos tooAzure fábrica de dados
Agora que os dados de saudação estão em vigor podemos criar dados de saudação do hello Azure Data Factory pipeline toomove do armazenamento de BLOBs do Azure no SQL Data Warehouse.

tooget iniciado, abra Olá [portal do Azure] [ Azure portal] e selecione sua fábrica de dados no menu esquerdo hello.

### <a name="step-21-create-linked-service"></a>Etapa 2.1: criar serviço vinculado
Vincule sua conta de armazenamento do Azure e a fábrica de dados do SQL Data Warehouse tooyour.  

1. Primeiro, iniciar o processo de registro de saudação clicando seção 'Serviços vinculados' hello sua fábrica de dados e, em seguida, clique em 'Novo repositório de dados.' Escolha um nome tooregister o armazenamento do azure no armazenamento do Azure selecione como o tipo e, em seguida, insira o nome da conta e chave de conta.
2. tooregister SQL Data Warehouse navegue toohello seção de 'Criar e implantar', selecione 'Novo repositório de dados' e 'Azure SQL Data Warehouse'. Copie e cole nesse modelo e, em seguida, preencha as informações específicas.

```JSON
{
    "name": "<Linked Service Name>",
    "properties": {
        "description": "",
        "type": "AzureSqlDW",
        "typeProperties": {
             "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
         }
    }
}
```

### <a name="step-22-define-hello-dataset"></a>Etapa 2.2: Definir o conjunto de dados de saudação
Depois de criar hello serviços vinculados, temos toodefine Olá os conjuntos de dados.  Aqui, isso significa definir Olá estrutura de dados de saudação que está sendo movidos de seu data warehouse de tooyour de armazenamento.  Ler mais sobre a criação

1. Inicie esse processo navegando seção 'Criar e implantar' toohello sua fábrica de dados.
2. Clique em 'Novo conjunto de dados' e 'Armazenamento de BLOBs do Azure' toolink sua fábrica de dados do armazenamento tooyour.  Você pode usar o hello abaixo script toodefine seus dados no armazenamento de BLOBs do Azure:

```JSON
{
    "name": "<Dataset Name>",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "<linked storage name>",
        "typeProperties": {
            "folderPath": "<containter name>",
            "fileName": "FactInternetSales.csv",
            "format": {
            "type": "TextFormat",
            "columnDelimiter": ",",
            "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
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


1. Agora, definiremos também nosso conjunto de dados para o SQL Data Warehouse.  Começamos Olá mesma forma, clicando em 'Novo conjunto de dados' e, em seguida, 'Azure SQL Data Warehouse'.

```JSON
{
    "name": "DWDataset",
    "properties": {
        "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "FactInternetSales"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

## <a name="step-3-create-and-run-your-pipeline"></a>Etapa 3: criar e executar o pipeline
Por fim, vamos configurar e executar pipeline Olá na fábrica de dados do Azure.  Esta é a operação de saudação que irá concluir a movimentação de dados reais de saudação.  Você pode encontrar uma exibição completa de operações de saudação que pode ser concluída com o SQL Data Warehouse e o Azure Data Factory [aqui][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].

Na seção de 'Criar e implantar' hello Agora clique 'Mais comandos' e 'Novo Pipeline'.  Depois de criar o pipeline hello, você pode usar o hello abaixo código tootransfer Olá dados tooyour do data warehouse:

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
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
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a>Próximas etapas
Além disso, inicie toolearn exibindo:

* [Roteiro de aprendizagem do Azure Data Factory][Azure Data Factory learning path].
* [Conector do SQL Data Warehouse do Azure][Azure SQL Data Warehouse Connector]. Este é um tópico de referência principal Olá para o uso do Azure Data Factory do Azure SQL Data warehouse.

Estes tópicos fornecem informações detalhadas sobre o Azure Data Factory. Discussão de banco de dados do SQL Azure ou HDinsight, mas Olá informações também se aplicam a tooAzure SQL Data Warehouse.

* [Tutorial: Introdução ao Azure Data Factory] [ Tutorial: Get started with Azure Data Factory] este é Olá tutorial de núcleo para processamento de dados com o Azure Data Factory. Neste tutorial você criará seu pipeline primeiro que usa tootransform HDInsight e analise logs da web mensalmente. Observe que não há nenhuma atividade de cópia neste tutorial.
* [Tutorial: Copiar dados de Blob de armazenamento do Azure tooAzure banco de dados SQL][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]. Neste tutorial, você criará um pipeline de dados do Azure Data Factory toocopy de Blob de armazenamento do Azure tooAzure banco de dados SQL.

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
