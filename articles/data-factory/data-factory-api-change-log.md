---
title: "aaaData fábrica - Log de alterações de API .NET | Microsoft Docs"
description: "Descreve as alterações recentes, adições de recursos, correções etc... em uma versão específica da API do .NET para hello Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8208271b-7f4c-4214-b665-d2ff503c4470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: spelluru
ms.openlocfilehash: 1d44b45c3dc8f9d483d1f1cef7068edacc610932
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---net-api-change-log"></a>Azure Data Factory - Log de alterações da API .NET
Este artigo fornece informações sobre alterações tooAzure SDK da fábrica de dados em uma versão específica. Você pode encontrar o pacote NuGet mais recente de saudação do Azure Data Factory [aqui](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)

## <a name="version-4110"></a>Versão 4.11.0
Adições de Recursos:

* Olá seguintes tipos de serviço vinculado foram adicionados:
  * [OnPremisesMongoDbLinkedService](https://msdn.microsoft.com/library/mt765129.aspx)
  * [AmazonRedshiftLinkedService](https://msdn.microsoft.com/library/mt765121.aspx)
  * [AwsAccessKeyLinkedService](https://msdn.microsoft.com/library/mt765144.aspx)
* Olá, tipos de conjunto de dados a seguir foram adicionado:
  * [MongoDbCollectionDataset](https://msdn.microsoft.com/library/mt765145.aspx)
  * [AmazonS3Dataset](https://msdn.microsoft.com/library/mt765112.aspx)
* a seguir Olá copia origem tipos foram adicionados:
  * [MongoDbSource](https://msdn.microsoft.com/library/mt765123.aspx)

## <a name="version-4100"></a>Versão 4.10.0
* Olá propriedades opcionais a seguir foram adicionado tooTextFormat:
  * [SkipLineCount](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.skiplinecount.aspx)
  * [FirstRowAsHeader](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.firstrowasheader.aspx)
  * [TreatEmptyAsNull](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.treatemptyasnull.aspx)
* Olá seguintes tipos de serviço vinculado foram adicionados:
  * [OnPremisesCassandraLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandralinkedservice.aspx)
  * [SalesforceLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.salesforcelinkedservice.aspx)
* Olá, tipos de conjunto de dados a seguir foram adicionado:
  * [OnPremisesCassandraTableDataset](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandratabledataset.aspx)
* a seguir Olá copia origem tipos foram adicionados:
  * [CassandraSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.cassandrasource.aspx)
* Adicionar [WebServiceInputs](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azuremlbatchexecutionactivity.webserviceinputs.aspx) tooAzureMLBatchExecutionActivity de propriedade
  * Habilitar passando várias entradas de serviço web tooan experiência de aprendizado de máquina do Azure

## <a name="version-491"></a>Versão 4.9.1
### <a name="bug-fix"></a>Correção de bug
* Substitua a autenticação baseada na WebApi pelo [WebLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.weblinkedservice.authenticationtype.aspx).

## <a name="version-490"></a>Versão 4.9.0
### <a name="feature-additions"></a>Adições de recursos
* Adicionar [EnableStaging](https://msdn.microsoft.com/library/mt767916.aspx) e [StagingSettings](https://msdn.microsoft.com/library/mt767918.aspx) tooCopyActivity de propriedades. Consulte [preparados cópia](data-factory-copy-activity-performance.md#staged-copy) para obter detalhes sobre o recurso de saudação.

### <a name="bug-fix"></a>Correção de bug
* Introduza uma sobrecarga do método [ActivityWindowOperationExtensions.List](https://msdn.microsoft.com/library/mt767915.aspx), que utiliza uma instância [ActivityWindowsByActivityListParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.activitywindowsbyactivitylistparameters.aspx).
* Marque [WriteBatchSize](https://msdn.microsoft.com/library/dn884293.aspx) e [WriteBatchTimeout](https://msdn.microsoft.com/library/dn884245.aspx) como opcionais no CopySink.

## <a name="version-480"></a>Versão 4.8.0
### <a name="feature-additions"></a>Adições de recursos
* Olá propriedades opcionais a seguir foram adicionado tooCopy atividade digite tooenable ajuste de desempenho de cópia:
  * [ParallelCopies](https://msdn.microsoft.com/library/mt767910.aspx)
  * [CloudDataMovementUnits](https://msdn.microsoft.com/library/mt767912.aspx)

## <a name="version-470"></a>Versão 4.7.0
### <a name="feature-additions"></a>Adições de recursos
* Adicionado o novo tipo de StorageFormat [OrcFormat](https://msdn.microsoft.com/library/mt723391.aspx) digite toocopy arquivos no formato domínio (ORC) Colunar linha otimizado.
* Adicionar [AllowPolyBase](https://msdn.microsoft.com/library/mt723396.aspx) e PolyBaseSettings tooSqlDWSink de propriedades.
  * Habilita o uso de saudação do toocopy dados no SQL Data Warehouse.

## <a name="version-461"></a>Versão 4.6.1
### <a name="bug-fixes"></a>Correções de bug
* Corrige a solicitação HTTP para listar janelas de atividade.
  * Remove o nome do grupo de recursos de saudação e o nome da fábrica de dados Olá Olá da carga de solicitação.

## <a name="version-460"></a>Versão 4.6.0
### <a name="feature-additions"></a>Adições de recursos
* Olá propriedades a seguir foram adicionadas muito[PipelineProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties_properties.aspx):
  * [PipelineMode](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.pipelinemode.aspx)
  * [ExpirationTime](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.expirationtime.aspx)
  * [Conjunto de dados](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.datasets.aspx)
* Olá propriedades a seguir foram adicionadas muito[PipelineRuntimeInfo](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.aspx):
  * [PipelineState](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.pipelinestate.aspx)
* Adicionado um novo [StorageFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.storageformat.aspx) tipo [JsonFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.jsonformat.aspx) digite toodefine conjuntos de dados cujos dados estão no formato JSON.

## <a name="version-450"></a>Versão 4.5.0
### <a name="feature-additions"></a>Adições de recursos
* Adição da [lista de operações à janela de atividade](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.activitywindowoperationsextensions.aspx).
  * Métodos adicionados tooretrieve atividade windows com filtros com base nos tipos de entidade hello (ou seja, as fábricas de dados, conjuntos de dados, pipelines e atividades).
* Olá seguintes tipos de serviço vinculado foram adicionados:
  * [ODataLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odatalinkedservice.aspx), [WebLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.weblinkedservice.aspx)
* Olá, tipos de conjunto de dados a seguir foram adicionado:
  * [ODataResourceDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odataresourcedataset.aspx), [WebTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.webtabledataset.aspx)
* a seguir Olá copia origem tipos foram adicionados:     
  * [WebSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.websource.aspx)

## <a name="version-440"></a>Versão 4.4.0
### <a name="feature-additions"></a>Adições de recursos
* Olá seguinte tipo de serviço vinculado foi adicionado como fontes de dados e coletores para atividades de cópia:
  * [AzureStorageSasLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azurestoragesaslinkedservice.aspx). Consulte [Serviço Vinculado de SAS de Armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) para obter informações conceituais e exemplos.

## <a name="version-430"></a>Versão 4.3.0
### <a name="feature-additions"></a>Adições de recursos
* Olá refúgio de tipos de serviço vinculado a seguir foram adicionados como fontes de dados para atividades de cópia:
  * [HdfsLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.hdfslinkedservice.aspx). Consulte [Mover dados do HDFS usando o Data Factory](data-factory-hdfs-connector.md) para obter informações conceituais e exemplos.
  * [OnPremisesOdbcLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisesodbclinkedservice.aspx). Consulte [Mover dados dos armazenamentos de dados ODBC usando o Azure Data Factory](data-factory-odbc-connector.md) para obter informações conceituais e exemplos.

## <a name="version-420"></a>Versão 4.2.0
### <a name="feature-additions"></a>Adições de recursos
* Olá novo tipo de atividade a seguir foram adicionado: [AzureMLUpdateResourceActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremlupdateresourceactivity.aspx). Para obter detalhes sobre a atividade de hello, consulte [modelos de atualização do Azure ML usando hello atividade de atualização de recurso](data-factory-azure-ml-batch-execution-activity.md).
* Uma nova propriedade opcional [updateResourceEndpoint](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.updateresourceendpoint.aspx) adicionou toohello [AzureMLLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.aspx).
* [LongRunningOperationInitialTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationinitialtimeout.aspx) e [LongRunningOperationRetryTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationretrytimeout.aspx) propriedades foram adicionadas toohello [DataFactoryManagementClient](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.aspx) classe.
* Permite a configuração de tempos limite de saudação para chamadas de cliente toohello serviço da fábrica de dados.

## <a name="version-410"></a>Versão 4.1.0
### <a name="feature-additions"></a>Adições de recursos
* Olá seguintes tipos de serviço vinculado foram adicionados:
  * [AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)
  * [AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)
* Olá, tipos de atividades a seguir foram adicionado:
  * [DataLakeAnalyticsUSQLActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datalakeanalyticsusqlactivity.aspx)
* Olá, tipos de conjunto de dados a seguir foram adicionado:
  * [AzureDataLakeStoreDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoredataset.aspx)
* Olá seguintes tipos de origem e do coletor de atividade de cópia foram adicionados:
  * [AzureDataLakeStoreSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresource.aspx)
  * [AzureDataLakeStoreSink](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresink.aspx)

## <a name="version-401"></a>Versão 4.0.1
### <a name="breaking-changes"></a>Alterações de última hora
Olá classes a seguir foram renomeada. novos nomes de saudação foram nomes originais de saudação de classes antes de lançar 4.0.0.

| Nome no 4.0.0 | Nome no 4.0.1 |
|:--- |:--- |
| AzureSqlDataWarehouseDataset |[AzureSqlDataWarehouseTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqldatawarehousetabledataset.aspx) |
| AzureSqlDataset |[AzureSqlTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqltabledataset.aspx) |
| AzureDataset |[AzureTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuretabledataset.aspx) |
| OracleDataset |[OracleTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.oracletabledataset.aspx) |
| RelationalDataset |[RelationalTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.relationaltabledataset.aspx) |
| SqlServerDataset |[SqlServerTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.sqlservertabledataset.aspx) |

## <a name="version-400"></a>Versão 4.0.0
### <a name="breaking-changes"></a>Alterações de última hora
* Olá classes/interfaces a seguir foram renomeada.

| Nome antigo | Novo nome |
|:--- |:--- |
| ITableOperations |[IDatasetOperations](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.idatasetoperations.aspx) |
| Tabela |[Conjunto de dados](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.dataset.aspx) |
| TableProperties |[DatasetProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetproperties.aspx) |
| TableTypeProprerties |[DatasetTypeProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasettypeproperties.aspx) |
| TableCreateOrUpdateParameters |[DatasetCreateOrUpdateParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateparameters.aspx) |
| TableCreateOrUpdateResponse |[DatasetCreateOrUpdateResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateresponse.aspx) |
| TableGetResponse |[DatasetGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetgetresponse.aspx) |
| TableListResponse |[DatasetListResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetlistresponse.aspx) |
| CreateOrUpdateWithRawJsonContentParameters |[DatasetCreateOrUpdateWithRawJsonContentParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdatewithrawjsoncontentparameters.aspx) |

* Olá **lista** métodos retornam resultados paginados agora. Se a resposta Olá contém não vazio **NextLink** propriedade, o aplicativo de cliente de saudação precisa toocontinue busca Olá próxima página até que todas as páginas são retornadas.  Aqui está um exemplo:

    ```csharp
    PipelineListResponse response = client.Pipelines.List("ResourceGroupName", "DataFactoryName");
    var pipelines = new List<Pipeline>(response.Pipelines);

    string nextLink = response.NextLink;
    while (!string.IsNullOrEmpty(nextLink))
    {
        PipelineListResponse nextResponse = client.Pipelines.ListNext(nextLink);
        pipelines.AddRange(nextResponse.Pipelines);

        nextLink = nextResponse.NextLink;
    }
    ```
* **Lista** pipeline API retorna apenas Olá resumo de um pipeline, em vez de todos os detalhes. Por exemplo, as atividades em um resumo de pipeline contém apenas nome e tipo.

### <a name="feature-additions"></a>Adições de recursos
* Olá [SqlDWSink](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsink.aspx) classe oferece suporte a duas novas propriedades, **SliceIdentifierColumnName** e **SqlWriterCleanupScript**, toosupport idempotente cópia tooAzure de dados do SQL Data warehouse. Consulte Olá [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md) artigo para obter detalhes sobre essas propriedades.
* Agora, oferecemos suporte executando o procedimento armazenado em fontes de banco de dados do SQL Azure e o Azure SQL Data Warehouse como parte do hello atividade de cópia. Olá [SqlSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqlsource.aspx) e [SqlDWSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsource.aspx) classes têm Olá seguintes propriedades: **SqlReaderStoredProcedureName** e **StoredProcedureParameters** . Consulte Olá [banco de dados do SQL Azure](data-factory-azure-sql-connector.md#sqlsource) e [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#sqldwsource) artigos em Azure.com para obter detalhes sobre essas propriedades.  
