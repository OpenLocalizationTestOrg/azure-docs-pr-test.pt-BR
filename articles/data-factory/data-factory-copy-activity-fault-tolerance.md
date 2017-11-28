---
title: "Adicionar tolerância a falhas na Atividade de Cópia do Azure Data Factory ignorando linhas incompatíveis | Microsoft Docs"
description: "Saiba como adicionar tolerância a falhas na Atividade de Cópia do Azure Data Factory ignorando linhas incompatíveis durante a cópia"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e2a108752259d5da3b401666c6bdbaad13b7ea90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="ede9d-103">Adicionar tolerância a falhas na Atividade de Cópia ignorando linhas incompatíveis</span><span class="sxs-lookup"><span data-stu-id="ede9d-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="ede9d-104">A [Atividade de Cópia](data-factory-data-movement-activities.md) do Azure Data Factory oferece duas maneiras de manipular linhas incompatíveis ao copiar dados entre os armazenamentos de dados da origem e do coletor:</span><span class="sxs-lookup"><span data-stu-id="ede9d-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways to handle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="ede9d-105">Você pode anular e fazer com que a atividade de cópia falhe quando dados incompatíveis forem encontrados (comportamento padrão).</span><span class="sxs-lookup"><span data-stu-id="ede9d-105">You can abort and fail the copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="ede9d-106">Você pode continuar copiando todos os dados adicionando tolerância a falhas e ignorando linhas de dados incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="ede9d-106">You can continue to copy all of the data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="ede9d-107">Além disso, é possível registrar em log as linhas incompatíveis no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ede9d-107">In addition, you can log the incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="ede9d-108">Em seguida, examine o log para saber a causa da falha, corrija os dados na origem de dados e repita a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ede9d-108">You can then examine the log to learn the cause for the failure, fix the data on the data source, and retry the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="ede9d-109">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="ede9d-109">Supported scenarios</span></span>
<span data-ttu-id="ede9d-110">A Atividade de Cópia dá suporte a três cenários para detectar, ignorar e registrar em log dados incompatíveis:</span><span class="sxs-lookup"><span data-stu-id="ede9d-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="ede9d-111">**Incompatibilidade entre o tipo de dados da origem e o tipo nativo do coletor**</span><span class="sxs-lookup"><span data-stu-id="ede9d-111">**Incompatibility between the source data type and the sink native type**</span></span>

    <span data-ttu-id="ede9d-112">Por exemplo: copiar dados de um arquivo CSV no armazenamento de Blobs em um banco de dados SQL com uma definição de esquema que contenha três colunas do tipo **INT**.</span><span class="sxs-lookup"><span data-stu-id="ede9d-112">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="ede9d-113">As linhas do arquivo CSV que contêm dados numéricos, como `123,456,789`, são copiadas com êxito no armazenamento de coletores.</span><span class="sxs-lookup"><span data-stu-id="ede9d-113">The CSV file rows that contain numeric data, such as `123,456,789` are copied successfully to the sink store.</span></span> <span data-ttu-id="ede9d-114">No entanto, as linhas que contêm valores não numéricos, como `123,456,abc`, são detectadas como incompatíveis e ignoradas.</span><span class="sxs-lookup"><span data-stu-id="ede9d-114">However, the rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="ede9d-115">**Incompatibilidade no número de colunas entre a origem e o coletor**</span><span class="sxs-lookup"><span data-stu-id="ede9d-115">**Mismatch in the number of columns between the source and the sink**</span></span>

    <span data-ttu-id="ede9d-116">Por exemplo: copiar dados de um arquivo CSV no armazenamento de Blobs em um banco de dados SQL com uma definição de esquema que contém seis colunas.</span><span class="sxs-lookup"><span data-stu-id="ede9d-116">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="ede9d-117">As linhas do arquivo CSV que contêm seis colunas são copiadas com êxito no armazenamento do coletor.</span><span class="sxs-lookup"><span data-stu-id="ede9d-117">The CSV file rows that contain six columns are copied successfully to the sink store.</span></span> <span data-ttu-id="ede9d-118">As linhas do arquivo CSV que contêm mais ou menos de seis colunas são detectadas como incompatíveis e ignoradas.</span><span class="sxs-lookup"><span data-stu-id="ede9d-118">The CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="ede9d-119">**Violação de chave primária ao gravar em banco de dados relacional**</span><span class="sxs-lookup"><span data-stu-id="ede9d-119">**Primary key violation when writing to a relational database**</span></span>

    <span data-ttu-id="ede9d-120">Por exemplo: copiar dados de um servidor SQL em um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="ede9d-120">For example: Copy data from a SQL server to a SQL database.</span></span> <span data-ttu-id="ede9d-121">Uma chave primária é definida no banco de dados SQL do coletor, mas nenhuma chave primária é definida no SQL Server de origem.</span><span class="sxs-lookup"><span data-stu-id="ede9d-121">A primary key is defined in the sink SQL database, but no such primary key is defined in the source SQL server.</span></span> <span data-ttu-id="ede9d-122">As linhas duplicadas que existem na origem não podem ser copiadas no coletor.</span><span class="sxs-lookup"><span data-stu-id="ede9d-122">The duplicated rows that exist in the source cannot be copied to the sink.</span></span> <span data-ttu-id="ede9d-123">A Atividade de Cópia copia apenas a primeira linha dos dados de origem no coletor.</span><span class="sxs-lookup"><span data-stu-id="ede9d-123">Copy Activity copies only the first row of the source data into the sink.</span></span> <span data-ttu-id="ede9d-124">As linhas da origem subsequentes que contêm o valor de chave primária duplicado são detectadas como incompatíveis e ignoradas.</span><span class="sxs-lookup"><span data-stu-id="ede9d-124">The subsequent source rows that contain the duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="ede9d-125">Configuração</span><span class="sxs-lookup"><span data-stu-id="ede9d-125">Configuration</span></span>
<span data-ttu-id="ede9d-126">O seguinte exemplo fornece uma definição de JSON que configura a omissão de linhas incompatíveis na Atividade de Cópia:</span><span class="sxs-lookup"><span data-stu-id="ede9d-126">The following example provides a JSON definition to configure skipping the incompatible rows in Copy Activity:</span></span>

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| <span data-ttu-id="ede9d-127">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ede9d-127">Property</span></span> | <span data-ttu-id="ede9d-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="ede9d-128">Description</span></span> | <span data-ttu-id="ede9d-129">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ede9d-129">Allowed values</span></span> | <span data-ttu-id="ede9d-130">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ede9d-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ede9d-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="ede9d-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="ede9d-132">Habilite ou não a omissão das linhas incompatíveis durante a cópia.</span><span class="sxs-lookup"><span data-stu-id="ede9d-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="ede9d-133">True </span><span class="sxs-lookup"><span data-stu-id="ede9d-133">True</span></span><br/><span data-ttu-id="ede9d-134">False (padrão)</span><span class="sxs-lookup"><span data-stu-id="ede9d-134">False (default)</span></span> | <span data-ttu-id="ede9d-135">Não</span><span class="sxs-lookup"><span data-stu-id="ede9d-135">No</span></span> |
| <span data-ttu-id="ede9d-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="ede9d-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="ede9d-137">Um grupo de propriedades que poderá ser especificado quando você desejar registrar as linhas incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="ede9d-137">A group of properties that can be specified when you want to log the incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="ede9d-138">Não</span><span class="sxs-lookup"><span data-stu-id="ede9d-138">No</span></span> |
| <span data-ttu-id="ede9d-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="ede9d-139">**linkedServiceName**</span></span> | <span data-ttu-id="ede9d-140">O serviço vinculado do Armazenamento do Azure para armazenar o log que contém as linhas ignoradas.</span><span class="sxs-lookup"><span data-stu-id="ede9d-140">The linked service of Azure Storage to store the log that contains the skipped rows.</span></span> | <span data-ttu-id="ede9d-141">O nome de um serviço vinculado [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service), que se refere à instância de armazenamento que você deseja usar para armazenar o arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="ede9d-141">The name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers to the storage instance that you want to use to store the log file.</span></span> | <span data-ttu-id="ede9d-142">Não</span><span class="sxs-lookup"><span data-stu-id="ede9d-142">No</span></span> |
| <span data-ttu-id="ede9d-143">**path**</span><span class="sxs-lookup"><span data-stu-id="ede9d-143">**path**</span></span> | <span data-ttu-id="ede9d-144">O caminho do arquivo de log que contém as linhas ignoradas.</span><span class="sxs-lookup"><span data-stu-id="ede9d-144">The path of the log file that contains the skipped rows.</span></span> | <span data-ttu-id="ede9d-145">Especifique o caminho de armazenamento de Blobs que você deseja usar para registrar em log os dados incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="ede9d-145">Specify the Blob storage path that you want to use to log the incompatible data.</span></span> <span data-ttu-id="ede9d-146">Se você não fornecer um caminho, o serviço criará um contêiner para você.</span><span class="sxs-lookup"><span data-stu-id="ede9d-146">If you do not provide a path, the service creates a container for you.</span></span> | <span data-ttu-id="ede9d-147">Não</span><span class="sxs-lookup"><span data-stu-id="ede9d-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="ede9d-148">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="ede9d-148">Monitoring</span></span>
<span data-ttu-id="ede9d-149">Depois que a execução da atividade de cópia for concluída, você verá o número de linhas ignoradas na seção de monitoramento:</span><span class="sxs-lookup"><span data-stu-id="ede9d-149">After the copy activity run completes, you can see the number of skipped rows in the monitoring section:</span></span>

![Monitorar linhas incompatíveis ignoradas](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="ede9d-151">Se você configurar para registrar em log as linhas incompatíveis, será possível encontrar o arquivo de log neste caminho: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` No arquivo de log, você poderá ver as linhas que foram ignoradas e a causa raiz da incompatibilidade.</span><span class="sxs-lookup"><span data-stu-id="ede9d-151">If you configure to log the incompatible rows, you can find the log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In the log file, you can see the rows that were skipped and the root cause of the incompatibility.</span></span>

<span data-ttu-id="ede9d-152">Os dados originais e o erro correspondente são registrados no arquivo.</span><span class="sxs-lookup"><span data-stu-id="ede9d-152">Both the original data and the corresponding error are logged in the file.</span></span> <span data-ttu-id="ede9d-153">Um exemplo do conteúdo do arquivo de log é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ede9d-153">An example of the log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="ede9d-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ede9d-154">Next steps</span></span>
<span data-ttu-id="ede9d-155">Para saber mais sobre a Atividade de Cópia do Azure Data Factory, confira [Mover dados usando a Atividade de Cópia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ede9d-155">To learn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>