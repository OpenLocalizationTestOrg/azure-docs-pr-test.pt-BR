---
title: "aaaIntegrating repositório Data Lake com outros serviços do Azure | Microsoft Docs"
description: "Noções básicas sobre como o Repositório Data Lake é integrado com outros serviços do Azure"
documentationcenter: 
services: data-lake-store
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 48a5d1f4-3850-4c22-bbc4-6d1d394fba8a
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 839689f04623f8225884e7aa9c0b533a09323e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-data-lake-store-with-other-azure-services"></a>Integrando o Repositório Data Lake com outros Serviços do Azure
Repositório Azure Data Lake pode ser usado em conjunto com outros serviços do Azure de tooenable uma grande variedade de cenários. Hello artigo a seguir lista os serviços de saudação repositório Data Lake pode ser integrado a.

## <a name="use-data-lake-store-with-azure-hdinsight"></a>Usar o Repositório Data Lake com o Azure HDInsight
Você pode provisionar um [HDInsight do Azure](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/) cluster que usa o repositório Data Lake como armazenamento Olá HDFS compatíveis. Para esta versão, para clusters Hadoop e Storm no Windows e Linux, é possível usar o Repositório Data Lake somente como um armazenamento adicional. Esses clusters ainda usam o armazenamento do Azure (WASB) como armazenamento de padrão de saudação. No entanto, para clusters do HBase no Windows e Linux, você pode usar o repositório Data Lake como armazenamento de padrão de hello, ou armazenamento adicional ou ambos.

Para obter instruções sobre como tooprovision uma HDInsight cluster com repositório Data Lake, consulte:

* [Provisionar um cluster HDInsight com o Repositório do Data Lake usando o Portal do Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Provisionar um cluster HDInsight com Data Lake Store como o armazenamento padrão usando o Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Provisionar um cluster HDInsight com Data Lake Store como o armazenamento adicional usando o Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell.md)

## <a name="use-data-lake-store-with-azure-data-lake-analytics"></a>Usar o Repositório Data Lake com a Análise Azure Data Lake
[Análise do Azure Data Lake](../data-lake-analytics/data-lake-analytics-overview.md) permite que você toowork com dados grandes em escala de nuvem. Ela provisiona recursos de maneira dinâmica e permite fazer a análise de terabytes ou até mesmo de exabytes de dados que podem ser armazenados em várias fontes de dados com suporte, sendo uma delas o Repositório Data Lake. Análise data Lake é especialmente otimizado toowork com repositório Azure Data Lake - fornecendo mais alto o nível de desempenho, a taxa de transferência e a paralelização para você Olá cargas de trabalho grande de dados.

Para obter instruções sobre como toouse análise Data Lake com repositório Data Lake, consulte [Introdução à análise Data Lake usando repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md).

## <a name="use-data-lake-store-with-azure-data-factory"></a>Usar o Repositório Data Lake com o Azure Data Factory
Você pode usar [do Azure Data Factory](https://azure.microsoft.com/services/data-factory/) tooingest dados de tabelas do Azure, banco de dados do SQL Azure, data warehouse do SQL Azure, Blobs de armazenamento do Azure e bancos de dados local. Sendo um cidadão de primeira classe no hello ecossistema do Azure, Azure Data Factory pode ser usado tooorchestrate Olá ingestão de dados a partir desses tooAzure fonte repositório Data Lake.

Para obter instruções sobre como toouse a fábrica de dados do Azure com o repositório Data Lake, consulte [mover tooand de dados do repositório Data Lake utilizando a fábrica de dados](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="copy-data-from-azure-storage-blobs-into-data-lake-store"></a>Copiar dados de Blobs do Armazenamento do Azure para o Repositório Data Lake
Repositório Azure Data Lake fornece uma ferramenta de linha de comando, AdlCopy, que permite que você toocopy dados do armazenamento de BLOBs do Azure em uma conta do repositório Data Lake. Para obter mais informações, consulte [copiar dados do repositório Azure armazenamento de Blobs tooData Lake](data-lake-store-copy-data-azure-storage-blob.md).

## <a name="copy-data-between-azure-sql-database-and-data-lake-store"></a>Copiar dados entre o Banco de Dados SQL do Azure e o Repositório Data Lake
Você pode usar o Apache Sqoop tooimport e exportar dados entre o banco de dados do SQL Azure e o repositório Data Lake. Para saber mais, confira [Copiar dados entre o Repositório Data Lake e o Banco de Dados SQL do Azure usando o Sqoop](data-lake-store-data-transfer-sql-sqoop.md).

## <a name="use-data-lake-store-with-stream-analytics"></a>Usar o Repositório Data Lake com o Stream Analytics
Você pode usar o repositório Data Lake como uma saudação gera toostore dados transmitidos usando o Azure Stream Analytics. Para saber mais, confira [Transmitir dados do Blob de Armazenamento do Azure para o Repositório Data Lake usando o Stream Analytics do Azure](data-lake-store-stream-analytics.md).

## <a name="use-data-lake-store-with-power-bi"></a>Usar o Repositório Data Lake com o Power BI
Você pode usar dados do Power BI tooimport de um tooanalyze de conta do repositório Data Lake e visualizar dados hello. Para saber mais, confira [Analisar dados no Repositório Data Lake usando o Power BI](data-lake-store-power-bi.md).

## <a name="use-data-lake-store-with-data-catalog"></a>Usar o Repositório Data Lake com o Catálogo de Dados
Você pode registrar os dados do repositório Data Lake Olá detectável em toda a organização Olá para dados de saudação do toomake do Data Catalog do Azure. Para saber mais, confira [Registrar dados do Repositório Data Lake no Catálogo de Dados do Azure](data-lake-store-with-data-catalog.md).

## <a name="use-data-lake-store-with-sql-server-integration-services-ssis"></a>Usar o Data Lake Store com o SSIS (SQL Server Integration Services)
Você pode usar o Gerenciador de conexão do repositório Azure Data Lake Olá no SSIS tooconnect um pacote do SSIS com repositório Azure Data Lake. Para obter mais informações, consulte [Usar o Data Lake Store com o SSIS](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager).

## <a name="use-data-lake-store-with-sql-data-warehouse"></a>Usar o Data Lake Store com o SQL Data Warehouse
Você pode usar dados tooload do repositório Azure Data Lake no SQL Data Warehouse. Para obter mais informações, consulte [Usar o Data Lake Store com o SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store.md).

## <a name="see-also"></a>Consulte também
* [Visão geral do Repositório Azure Data Lake](data-lake-store-overview.md)
* [Introdução ao Repositório Data Lake usando o Portal](data-lake-store-get-started-portal.md)
* [Introdução ao Repositório Data Lake usando o PowerShell](data-lake-store-get-started-powershell.md)  

