---
title: "grandes quantidades de aaaUpload de dados no repositório Data Lake usando métodos offline | Microsoft Docs"
description: "TooData Lake armazenamento de blobs Olá use dados de toocopy ferramenta AdlCopy do armazenamento do Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a>Usar serviço de importação/exportação do Azure Olá para uma cópia offline tooData Lake do repositório de dados
Neste artigo, você aprenderá como dados enorme toocopy define (> 200 GB) em um repositório Azure Data Lake usando métodos de cópia offline, como Olá [serviço de importação/exportação do Azure](../storage/common/storage-import-export-service.md). Especificamente, o arquivo hello usado como exemplo neste artigo é 339,420,860,416 bytes ou aproximadamente 319 GB no disco. Vamos chamar esse arquivo de 319GB.tsv.

Olá serviço de importação/exportação do Azure ajuda a tootransfer grandes quantidades de dados mais segura tooAzure armazenamento de Blob por disco rígido de envio de unidades tooan datacenter do Azure.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta de armazenamento do Azure**.
* **Uma conta do repositório Azure Data Lake**. Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)

## <a name="preparing-hello-data"></a>Preparando dados Olá
Antes de usar o serviço de importação/exportação hello, transferidos quebra Olá dados arquivo toobe **em cópias de menos de 200 GB** em tamanho. ferramenta de importação de saudação não funciona com arquivos com mais de 200 GB. Neste tutorial, dividiremos arquivo hello em partes de 100 GB. Você pode fazer isso usando o [Cygwin](https://cygwin.com/install.html). O Cygwin dá suporte a comandos do Linux. Nesse caso, use Olá comando a seguir:

    split -b 100m 319GB.tsv

operação de divisão Olá cria arquivos com hello nomes a seguir.

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a>Prepare os discos com dados
Siga as instruções de saudação em [usando o serviço de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md) (em Olá **preparar suas unidades** seção) tooprepare seus discos rígidos. Eis Olá sequência geral:

1. Obtenha um disco rígido que atenda Olá requisito toobe usado para Olá serviço de importação/exportação do Azure.
2. Identifique uma conta de armazenamento do Azure em que dados hello serão copiados depois que ele toohello fornecido datacenter do Azure.
3. Saudação de uso [ferramenta de importação/exportação do Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), um utilitário de linha de comando. Aqui está um trecho de código de exemplo que mostra como toouse Olá ferramenta.

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    Consulte [usando o serviço de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md) para mais trechos de código de exemplo.
4. Olá, comando anterior cria um diário de local do arquivo no hello especificado. Use este arquivo de diário toocreate um trabalho de importação de saudação [portal clássico do Azure](https://manage.windowsazure.com).

## <a name="create-an-import-job"></a>Criar um trabalho de importação
Agora você pode criar um trabalho de importação usando instruções Olá [usando o serviço de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md) (em Olá **criar trabalho de importação de saudação** seção). Para este trabalho de importação, com outros detalhes também fornece Olá diário arquivo criado durante a preparação Olá unidades de disco.

## <a name="physically-ship-hello-disks"></a>Enviar fisicamente os discos de saudação
Agora você pode enviar fisicamente Olá discos tooan datacenter do Azure. Lá, os dados de saudação são copiados em blobs de armazenamento do Azure toohello fornecida ao criar o trabalho de importação de saudação. Além disso, ao criar o trabalho de hello, se você tiver optado tooprovide hello mais tarde, informações de controle você pode agora voltar produtos de saudação de trabalho e atualização de importação tooyour número de controle.

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a>Copiar dados do repositório do armazenamento do Azure blobs tooAzure Data Lake
Depois de status Olá Olá o trabalho de importação mostra que ela é concluída, você pode verificar se os dados de saudação estão disponíveis em blobs de armazenamento do Azure Olá especificadas. Você pode usar uma variedade de métodos toomove dados de saudação blobs repositório tooAzure Data Lake. Para todos os hello opções disponíveis para carregamento de dados, consulte [ingestão de dados no repositório Data Lake](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).

Nesta seção, podemos fornecer definições de JSON Olá que você pode usar toocreate um pipeline da fábrica de dados do Azure para copiar dados. Você pode usar essas definições de JSON de saudação [portal do Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), ou [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).

### <a name="source-linked-service-azure-storage-blob"></a>Serviço vinculado de origem (Azure Storage Blob)
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a>Serviço vinculado de destino (Azure Data Lake Store)
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a>Conjunto de dados de entrada
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a>Conjunto de dados de saída
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a>Pipeline (atividade de cópia)
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
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
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
Para obter mais informações, consulte [mover o blob de dados do armazenamento do Azure usando o Azure Data Factory repositório tooAzure Data Lake](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a>Reconstruir os arquivos de dados de saudação no repositório Azure Data Lake
Começamos com um arquivo que foi 319 GB e rompeu-lo em arquivos de menor tamanho, para que ele foi transferido usando o serviço de importação/exportação do Azure hello. Agora que os dados de saudação estão no repositório Azure Data Lake, podemos pode reconstruir o tamanho original do arquivo de saudação tooits. Você pode usar o hello Azure PowerShell cmldts toodo a seguir assim.

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a>Próximas etapas
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)
* [Usar a Análise Data Lake do Azure com o Repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usar o Azure HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
