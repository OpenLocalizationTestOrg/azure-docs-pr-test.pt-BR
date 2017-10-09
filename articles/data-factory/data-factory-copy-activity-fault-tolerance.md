---
title: "tolerância a falhas aaaAdd na atividade de cópia de fábrica de dados do Azure, ignorando linhas incompatíveis | Microsoft Docs"
description: "Saiba como tooadd a tolerância a falhas na atividade de cópia de fábrica de dados do Azure, ignorando linhas incompatíveis durante a cópia"
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
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="70f0e-103">Adicionar tolerância a falhas na Atividade de Cópia ignorando linhas incompatíveis</span><span class="sxs-lookup"><span data-stu-id="70f0e-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="70f0e-104">O Azure Data Factory [atividade de cópia](data-factory-data-movement-activities.md) oferece linhas incompatível de toohandle de duas maneiras ao copiar dados entre armazenamentos de dados de origem e do coletor:</span><span class="sxs-lookup"><span data-stu-id="70f0e-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways toohandle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="70f0e-105">Você pode anular e falhar cópia hello atividade quando dados incompatíveis encontrado (comportamento padrão).</span><span class="sxs-lookup"><span data-stu-id="70f0e-105">You can abort and fail hello copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="70f0e-106">Você pode continuar toocopy todos os dados de saudação adicionando a tolerância a falhas e ignorar as linhas de dados incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="70f0e-106">You can continue toocopy all of hello data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="70f0e-107">Além disso, você pode registrar linhas incompatível Olá no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="70f0e-107">In addition, you can log hello incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="70f0e-108">Em seguida, você pode examinar Olá log toolearn Olá causa falha hello, corrigir dados saudação na fonte de dados de saudação e repita a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="70f0e-108">You can then examine hello log toolearn hello cause for hello failure, fix hello data on hello data source, and retry hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="70f0e-109">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="70f0e-109">Supported scenarios</span></span>
<span data-ttu-id="70f0e-110">A Atividade de Cópia dá suporte a três cenários para detectar, ignorar e registrar em log dados incompatíveis:</span><span class="sxs-lookup"><span data-stu-id="70f0e-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="70f0e-111">**Incompatibilidade entre o tipo de dados de origem hello e tipo nativo do coletor Olá**</span><span class="sxs-lookup"><span data-stu-id="70f0e-111">**Incompatibility between hello source data type and hello sink native type**</span></span>

    <span data-ttu-id="70f0e-112">Por exemplo: copiar dados de um arquivo CSV no armazenamento de Blob tooa SQL de banco de dados com uma definição de esquema que contém três **INT** colunas de tipo.</span><span class="sxs-lookup"><span data-stu-id="70f0e-112">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="70f0e-113">Olá linhas do arquivo CSV que contêm dados numéricos, como `123,456,789` são copiados com êxito toohello repositório de coletor.</span><span class="sxs-lookup"><span data-stu-id="70f0e-113">hello CSV file rows that contain numeric data, such as `123,456,789` are copied successfully toohello sink store.</span></span> <span data-ttu-id="70f0e-114">No entanto, Olá linhas que contêm valores não numéricos, como `123,456,abc` são detectados como incompatíveis e são ignorados.</span><span class="sxs-lookup"><span data-stu-id="70f0e-114">However, hello rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="70f0e-115">**Incompatibilidade no número de saudação de colunas entre a origem de saudação e do coletor de saudação**</span><span class="sxs-lookup"><span data-stu-id="70f0e-115">**Mismatch in hello number of columns between hello source and hello sink**</span></span>

    <span data-ttu-id="70f0e-116">Por exemplo: copiar dados de um arquivo CSV no armazenamento de Blob tooa SQL de banco de dados com uma definição de esquema que contém seis colunas.</span><span class="sxs-lookup"><span data-stu-id="70f0e-116">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="70f0e-117">Hello arquivo CSV linhas que contêm seis colunas são copiados com êxito toohello repositório de coletor.</span><span class="sxs-lookup"><span data-stu-id="70f0e-117">hello CSV file rows that contain six columns are copied successfully toohello sink store.</span></span> <span data-ttu-id="70f0e-118">linhas do arquivo CSV Olá que contêm menos de seis ou mais colunas são detectadas como incompatíveis e são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="70f0e-118">hello CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="70f0e-119">**Violação de chave primária ao gravar o banco de dados relacional tooa**</span><span class="sxs-lookup"><span data-stu-id="70f0e-119">**Primary key violation when writing tooa relational database**</span></span>

    <span data-ttu-id="70f0e-120">Por exemplo: copiar dados de um banco de dados do SQL server tooa SQL.</span><span class="sxs-lookup"><span data-stu-id="70f0e-120">For example: Copy data from a SQL server tooa SQL database.</span></span> <span data-ttu-id="70f0e-121">Uma chave primária seja definida no banco de dados do SQL Olá coletor, mas nenhuma chave primária é definida no SQL server de origem hello.</span><span class="sxs-lookup"><span data-stu-id="70f0e-121">A primary key is defined in hello sink SQL database, but no such primary key is defined in hello source SQL server.</span></span> <span data-ttu-id="70f0e-122">linhas de saudação duplicada que existem na fonte de saudação não podem ser copiado toohello coletor.</span><span class="sxs-lookup"><span data-stu-id="70f0e-122">hello duplicated rows that exist in hello source cannot be copied toohello sink.</span></span> <span data-ttu-id="70f0e-123">Atividade de cópia copia apenas Olá primeira linha dos dados de origem Olá coletor hello.</span><span class="sxs-lookup"><span data-stu-id="70f0e-123">Copy Activity copies only hello first row of hello source data into hello sink.</span></span> <span data-ttu-id="70f0e-124">Hello subsequentes origem nas linhas que contêm o valor de chave primária Olá duplicado é detectadas como incompatíveis e é ignoradas.</span><span class="sxs-lookup"><span data-stu-id="70f0e-124">hello subsequent source rows that contain hello duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="70f0e-125">Configuração</span><span class="sxs-lookup"><span data-stu-id="70f0e-125">Configuration</span></span>
<span data-ttu-id="70f0e-126">Olá, exemplo a seguir fornece uma tooconfigure de definição de JSON ignorar as linhas de saudação incompatível na atividade de cópia:</span><span class="sxs-lookup"><span data-stu-id="70f0e-126">hello following example provides a JSON definition tooconfigure skipping hello incompatible rows in Copy Activity:</span></span>

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

| <span data-ttu-id="70f0e-127">Propriedade</span><span class="sxs-lookup"><span data-stu-id="70f0e-127">Property</span></span> | <span data-ttu-id="70f0e-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="70f0e-128">Description</span></span> | <span data-ttu-id="70f0e-129">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="70f0e-129">Allowed values</span></span> | <span data-ttu-id="70f0e-130">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="70f0e-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="70f0e-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="70f0e-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="70f0e-132">Habilite ou não a omissão das linhas incompatíveis durante a cópia.</span><span class="sxs-lookup"><span data-stu-id="70f0e-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="70f0e-133">True </span><span class="sxs-lookup"><span data-stu-id="70f0e-133">True</span></span><br/><span data-ttu-id="70f0e-134">False (padrão)</span><span class="sxs-lookup"><span data-stu-id="70f0e-134">False (default)</span></span> | <span data-ttu-id="70f0e-135">Não</span><span class="sxs-lookup"><span data-stu-id="70f0e-135">No</span></span> |
| <span data-ttu-id="70f0e-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="70f0e-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="70f0e-137">Um grupo de propriedades que pode ser especificado quando você quiser linhas incompatível do toolog hello.</span><span class="sxs-lookup"><span data-stu-id="70f0e-137">A group of properties that can be specified when you want toolog hello incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="70f0e-138">Não</span><span class="sxs-lookup"><span data-stu-id="70f0e-138">No</span></span> |
| <span data-ttu-id="70f0e-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="70f0e-139">**linkedServiceName**</span></span> | <span data-ttu-id="70f0e-140">Olá vinculado de serviço de log de saudação do armazenamento do Azure toostore que contém linhas de saudação ignorada.</span><span class="sxs-lookup"><span data-stu-id="70f0e-140">hello linked service of Azure Storage toostore hello log that contains hello skipped rows.</span></span> | <span data-ttu-id="70f0e-141">nome de saudação de um [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [o AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) serviço, que se refere a instância de armazenamento de toohello que você deseja que o arquivo de log toouse toostore Olá vinculado.</span><span class="sxs-lookup"><span data-stu-id="70f0e-141">hello name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers toohello storage instance that you want toouse toostore hello log file.</span></span> | <span data-ttu-id="70f0e-142">Não</span><span class="sxs-lookup"><span data-stu-id="70f0e-142">No</span></span> |
| <span data-ttu-id="70f0e-143">**path**</span><span class="sxs-lookup"><span data-stu-id="70f0e-143">**path**</span></span> | <span data-ttu-id="70f0e-144">caminho de Olá Olá do arquivo de log que contém a saudação ignorada linhas.</span><span class="sxs-lookup"><span data-stu-id="70f0e-144">hello path of hello log file that contains hello skipped rows.</span></span> | <span data-ttu-id="70f0e-145">Especifique o caminho de armazenamento de Blob Olá cujos dados incompatíveis do toouse toolog hello.</span><span class="sxs-lookup"><span data-stu-id="70f0e-145">Specify hello Blob storage path that you want toouse toolog hello incompatible data.</span></span> <span data-ttu-id="70f0e-146">Se você não fornecer um caminho, o serviço de saudação cria um contêiner para você.</span><span class="sxs-lookup"><span data-stu-id="70f0e-146">If you do not provide a path, hello service creates a container for you.</span></span> | <span data-ttu-id="70f0e-147">Não</span><span class="sxs-lookup"><span data-stu-id="70f0e-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="70f0e-148">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="70f0e-148">Monitoring</span></span>
<span data-ttu-id="70f0e-149">Após a conclusão da execução da atividade de cópia de saudação, você pode ver o número de saudação de linhas ignoradas na seção monitoramento de saudação:</span><span class="sxs-lookup"><span data-stu-id="70f0e-149">After hello copy activity run completes, you can see hello number of skipped rows in hello monitoring section:</span></span>

![Monitorar linhas incompatíveis ignoradas](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="70f0e-151">Se você configurar linhas incompatível do toolog Olá, você pode encontrar o arquivo de log de saudação no seguinte caminho: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` no arquivo de log Olá, você pode ver Olá linhas que foram ignoradas e Olá causa raiz de incompatibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="70f0e-151">If you configure toolog hello incompatible rows, you can find hello log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In hello log file, you can see hello rows that were skipped and hello root cause of hello incompatibility.</span></span>

<span data-ttu-id="70f0e-152">Dados originais hello e o erro correspondente Olá são registradas no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="70f0e-152">Both hello original data and hello corresponding error are logged in hello file.</span></span> <span data-ttu-id="70f0e-153">Um exemplo do conteúdo do arquivo de log de saudação é da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="70f0e-153">An example of hello log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="70f0e-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70f0e-154">Next steps</span></span>
<span data-ttu-id="70f0e-155">toolearn mais sobre a atividade de cópia de fábrica de dados do Azure, consulte [mover dados usando a atividade de cópia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="70f0e-155">toolearn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>
