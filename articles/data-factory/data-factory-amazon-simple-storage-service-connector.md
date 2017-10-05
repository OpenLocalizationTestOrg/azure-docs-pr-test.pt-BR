---
title: Mover dados do Amazon Simple Storage Service usando o Data Factory | Microsoft Docs
description: Saiba mais sobre como mover dados do Amazon S3 (Simple Storage Service) usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 3e21f7dfccc3b235071344a28c7d94f65e6bf9ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="65de7-103">Mover dados do Amazon Simple Storage Service usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="65de7-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="65de7-104">Este artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados do Amazon S3 (Simple Storage Service).</span><span class="sxs-lookup"><span data-stu-id="65de7-104">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="65de7-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="65de7-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="65de7-106">Você pode copiar dados do Amazon S3 para qualquer repositório de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="65de7-106">You can copy data from Amazon S3 to any supported sink data store.</span></span> <span data-ttu-id="65de7-107">Para obter uma lista de armazenamentos de dados com suporte da atividade de cópia, confira a tabela [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="65de7-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="65de7-108">Atualmente, a data factory dá suporte apenas para a movimentação de dados do Amazon S3 para outros armazenamentos de dados, mas não para a movimentação de dados de outros armazenamentos de dados para o Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="65de7-108">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="65de7-109">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="65de7-109">Required permissions</span></span>
<span data-ttu-id="65de7-110">Para copiar dados do Amazon S3, verifique se você recebeu as permissões a seguir:</span><span class="sxs-lookup"><span data-stu-id="65de7-110">To copy data from Amazon S3, make sure you have been granted the following permissions:</span></span>

* <span data-ttu-id="65de7-111">`s3:GetObject` e `s3:GetObjectVersion` para operações de objeto do Amazon S3</span><span class="sxs-lookup"><span data-stu-id="65de7-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="65de7-112">`s3:ListBucket` para operações de bucket do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="65de7-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="65de7-113">Se você estiver usando o assistente de cópia Data Factory, `s3:ListAllMyBuckets` também será exigido.</span><span class="sxs-lookup"><span data-stu-id="65de7-113">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="65de7-114">Parra detalhes sobre a lista completa e detalhada das permissões da Amazon S3,consulte [Especificar permissões em uma política](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="65de7-114">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="65de7-115">Introdução</span><span class="sxs-lookup"><span data-stu-id="65de7-115">Getting started</span></span>
<span data-ttu-id="65de7-116">Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem do Amazon S3 usando diferentes ferramentas ou APIs.</span><span class="sxs-lookup"><span data-stu-id="65de7-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="65de7-117">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="65de7-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="65de7-118">Para obter uma explicação rápida, confira [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) (Tutorial: criar um pipeline usando o Assistente de Cópia).</span><span class="sxs-lookup"><span data-stu-id="65de7-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="65de7-119">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="65de7-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="65de7-120">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="65de7-120">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="65de7-121">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="65de7-121">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="65de7-122">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="65de7-122">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="65de7-123">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="65de7-123">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="65de7-124">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="65de7-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="65de7-125">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="65de7-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="65de7-126">Ao usar ferramentas ou APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="65de7-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="65de7-127">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de um armazenamento de dados do Amazon S3, confira a seção [Exemplo de JSON: Copiar dados do Amazon S3 para o Blob do Azure](#json-example-copy-data-from-amazon-s3-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="65de7-127">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="65de7-128">Para obter detalhes sobre os formatos de arquivo e de compactação com suporte para uma atividade de cópia, consulte [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="65de7-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="65de7-129">As seções seguintes fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas ao Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="65de7-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="65de7-130">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="65de7-130">Linked service properties</span></span>
<span data-ttu-id="65de7-131">Um serviço vinculado vincula um armazenamento de dados a um data factory.</span><span class="sxs-lookup"><span data-stu-id="65de7-131">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="65de7-132">Crie um serviço vinculado do tipo **AwsAccessKey** para vincular o armazenamento de dados do Amazon S3 ao data factory.</span><span class="sxs-lookup"><span data-stu-id="65de7-132">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span></span> <span data-ttu-id="65de7-133">A tabela a seguir fornece a descrição para elementos JSON específicas para o serviço vinculado do Amazon S3 (AwsAccessKey).</span><span class="sxs-lookup"><span data-stu-id="65de7-133">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="65de7-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="65de7-134">Property</span></span> | <span data-ttu-id="65de7-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="65de7-135">Description</span></span> | <span data-ttu-id="65de7-136">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="65de7-136">Allowed values</span></span> | <span data-ttu-id="65de7-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="65de7-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="65de7-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="65de7-138">accessKeyID</span></span> |<span data-ttu-id="65de7-139">ID da chave de acesso secreta.</span><span class="sxs-lookup"><span data-stu-id="65de7-139">ID of the secret access key.</span></span> |<span data-ttu-id="65de7-140">string</span><span class="sxs-lookup"><span data-stu-id="65de7-140">string</span></span> |<span data-ttu-id="65de7-141">Sim</span><span class="sxs-lookup"><span data-stu-id="65de7-141">Yes</span></span> |
| <span data-ttu-id="65de7-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="65de7-142">secretAccessKey</span></span> |<span data-ttu-id="65de7-143">A chave de acesso do secreta em si.</span><span class="sxs-lookup"><span data-stu-id="65de7-143">The secret access key itself.</span></span> |<span data-ttu-id="65de7-144">Cadeia de caracteres secreta criptografada</span><span class="sxs-lookup"><span data-stu-id="65de7-144">Encrypted secret string</span></span> |<span data-ttu-id="65de7-145">Sim</span><span class="sxs-lookup"><span data-stu-id="65de7-145">Yes</span></span> |

<span data-ttu-id="65de7-146">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="65de7-146">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="65de7-147">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="65de7-147">Dataset properties</span></span>
<span data-ttu-id="65de7-148">Para especificar um conjunto de dados de modo a representar dados de entrada em um Armazenamento de Blobs do Azure, defina a propriedade de tipo do conjunto de dados para: **AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="65de7-148">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span></span> <span data-ttu-id="65de7-149">Defina a propriedade **linkedServiceName** do conjunto de dados para o nome do serviço vinculado do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="65de7-149">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span></span> <span data-ttu-id="65de7-150">Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, confira [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="65de7-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="65de7-151">As seções como structure, availability e policy são similares para todos os tipos de conjunto de dados (como banco de dados SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="65de7-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="65de7-152">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="65de7-152">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="65de7-153">A seção **typeProperties** para o conjunto de dados do tipo **AmazonS3** (que inclui o conjunto de dados do Amazon S3) tem as propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="65de7-153">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span></span>

| <span data-ttu-id="65de7-154">Propriedade</span><span class="sxs-lookup"><span data-stu-id="65de7-154">Property</span></span> | <span data-ttu-id="65de7-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="65de7-155">Description</span></span> | <span data-ttu-id="65de7-156">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="65de7-156">Allowed values</span></span> | <span data-ttu-id="65de7-157">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="65de7-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="65de7-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="65de7-158">bucketName</span></span> |<span data-ttu-id="65de7-159">O nome do bucket S3.</span><span class="sxs-lookup"><span data-stu-id="65de7-159">The S3 bucket name.</span></span> |<span data-ttu-id="65de7-160">string</span><span class="sxs-lookup"><span data-stu-id="65de7-160">String</span></span> |<span data-ttu-id="65de7-161">Sim</span><span class="sxs-lookup"><span data-stu-id="65de7-161">Yes</span></span> |
| <span data-ttu-id="65de7-162">chave</span><span class="sxs-lookup"><span data-stu-id="65de7-162">key</span></span> |<span data-ttu-id="65de7-163">A chave do objeto S3.</span><span class="sxs-lookup"><span data-stu-id="65de7-163">The S3 object key.</span></span> |<span data-ttu-id="65de7-164">string</span><span class="sxs-lookup"><span data-stu-id="65de7-164">String</span></span> |<span data-ttu-id="65de7-165">Não</span><span class="sxs-lookup"><span data-stu-id="65de7-165">No</span></span> |
| <span data-ttu-id="65de7-166">prefixo</span><span class="sxs-lookup"><span data-stu-id="65de7-166">prefix</span></span> |<span data-ttu-id="65de7-167">Prefixo da chave do objeto S3.</span><span class="sxs-lookup"><span data-stu-id="65de7-167">Prefix for the S3 object key.</span></span> <span data-ttu-id="65de7-168">Objetos cujas chaves começam com esse prefixo serão selecionados.</span><span class="sxs-lookup"><span data-stu-id="65de7-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="65de7-169">Aplica-se apenas quando a chave está vazia.</span><span class="sxs-lookup"><span data-stu-id="65de7-169">Applies only when key is empty.</span></span> |<span data-ttu-id="65de7-170">string</span><span class="sxs-lookup"><span data-stu-id="65de7-170">String</span></span> |<span data-ttu-id="65de7-171">Não</span><span class="sxs-lookup"><span data-stu-id="65de7-171">No</span></span> |
| <span data-ttu-id="65de7-172">version</span><span class="sxs-lookup"><span data-stu-id="65de7-172">version</span></span> |<span data-ttu-id="65de7-173">A versão do objeto S3 se o controle de versão do S3 está habilitado.</span><span class="sxs-lookup"><span data-stu-id="65de7-173">The version of the S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="65de7-174">string</span><span class="sxs-lookup"><span data-stu-id="65de7-174">String</span></span> |<span data-ttu-id="65de7-175">Não</span><span class="sxs-lookup"><span data-stu-id="65de7-175">No</span></span> |
| <span data-ttu-id="65de7-176">formato</span><span class="sxs-lookup"><span data-stu-id="65de7-176">format</span></span> | <span data-ttu-id="65de7-177">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="65de7-177">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="65de7-178">Defina a propriedade **type** sob formato como um desses valores.</span><span class="sxs-lookup"><span data-stu-id="65de7-178">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="65de7-179">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="65de7-179">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="65de7-180">Se você quiser copiar arquivos no estado em que se encontram entre repositórios com base em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="65de7-180">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="65de7-181">Não</span><span class="sxs-lookup"><span data-stu-id="65de7-181">No</span></span> | |
| <span data-ttu-id="65de7-182">compactação</span><span class="sxs-lookup"><span data-stu-id="65de7-182">compression</span></span> | <span data-ttu-id="65de7-183">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="65de7-183">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="65de7-184">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="65de7-184">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="65de7-185">Os níveis com suporte são **Ideal** e **Mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="65de7-185">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="65de7-186">Para obter mais informações, consulte [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="65de7-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="65de7-187">Não</span><span class="sxs-lookup"><span data-stu-id="65de7-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="65de7-188">**bucketName + chave** especifica a localização do objeto S3 em que bucket é o contêiner raiz para objetos S3 e a chave é o caminho completo para o objeto S3.</span><span class="sxs-lookup"><span data-stu-id="65de7-188">**bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="65de7-189">Conjunto de dados de exemplo com o prefixo</span><span class="sxs-lookup"><span data-stu-id="65de7-189">Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a><span data-ttu-id="65de7-190">Conjunto de dados de exemplo (com a versão)</span><span class="sxs-lookup"><span data-stu-id="65de7-190">Sample dataset (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="65de7-191">Caminhos dinâmicos para S3</span><span class="sxs-lookup"><span data-stu-id="65de7-191">Dynamic paths for S3</span></span>
<span data-ttu-id="65de7-192">No exemplo anterior, usamos valores fixos para as propriedades de **chave** e **bucketName** no conjunto de dados do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="65de7-192">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="65de7-193">Você pode fazer com que o Data Factory calcule essas propriedades dinamicamente em tempo de execução usando variáveis de sistema como SliceStart.</span><span class="sxs-lookup"><span data-stu-id="65de7-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="65de7-194">Você pode fazer o mesmo para a propriedade de **prefixo**de um conjunto de dados do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="65de7-194">You can do the same for the **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="65de7-195">Veja [Funções e variáveis do sistema do Data Factory](data-factory-functions-variables.md) para obter uma lista das funções e variáveis com suporte.</span><span class="sxs-lookup"><span data-stu-id="65de7-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="65de7-196">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="65de7-196">Copy activity properties</span></span>
<span data-ttu-id="65de7-197">Para obter uma lista completa das seções e propriedades disponíveis para definir as atividades, consulte [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="65de7-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="65de7-198">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="65de7-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="65de7-199">As propriedades disponíveis na seção **typeProperties** da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="65de7-199">Properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="65de7-200">Para a atividade de cópia, as propriedades variam conforme os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="65de7-200">For the copy activity, properties vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="65de7-201">Quando a origem da atividade de cópia é do tipo **FileSystemSource** (que inclui o Amazon S3), a seguinte propriedade está disponível na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="65de7-201">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="65de7-202">Propriedade</span><span class="sxs-lookup"><span data-stu-id="65de7-202">Property</span></span> | <span data-ttu-id="65de7-203">Descrição</span><span class="sxs-lookup"><span data-stu-id="65de7-203">Description</span></span> | <span data-ttu-id="65de7-204">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="65de7-204">Allowed values</span></span> | <span data-ttu-id="65de7-205">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="65de7-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="65de7-206">recursive</span><span class="sxs-lookup"><span data-stu-id="65de7-206">recursive</span></span> |<span data-ttu-id="65de7-207">Especifica se devemos listar recursivamente objetos S3 no diretório.</span><span class="sxs-lookup"><span data-stu-id="65de7-207">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="65de7-208">true/false</span><span class="sxs-lookup"><span data-stu-id="65de7-208">true/false</span></span> |<span data-ttu-id="65de7-209">Não</span><span class="sxs-lookup"><span data-stu-id="65de7-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-to-azure-blob-storage"></a><span data-ttu-id="65de7-210">Exemplo JSON: copiar dados do Amazon S3 para o Armazenamento do Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="65de7-210">JSON example: Copy data from Amazon S3 to Azure Blob storage</span></span>
<span data-ttu-id="65de7-211">Este exemplo mostra como copiar dados de um Amazon S3 para um Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="65de7-211">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span></span> <span data-ttu-id="65de7-212">No entanto, os dados podem ser copiados [diretamente](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para qualquer uma das fontes que são suportadas usando a atividade de cópia no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="65de7-212">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span></span>

<span data-ttu-id="65de7-213">O exemplo fornece definições de JSON para as entidades de Data Factory a seguir.</span><span class="sxs-lookup"><span data-stu-id="65de7-213">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="65de7-214">Você pode usar essas definições para criar um pipeline para copiar dados da Amazon S3 para armazenamento de Blob, usando o [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="65de7-214">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="65de7-215">Um serviço vinculado do tipo [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="65de7-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="65de7-216">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="65de7-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="65de7-217">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="65de7-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="65de7-218">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="65de7-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="65de7-219">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="65de7-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="65de7-220">O exemplo copia dados de um Amazon S3 para um blob do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="65de7-220">The sample copies data from Amazon S3 to an Azure blob every hour.</span></span> <span data-ttu-id="65de7-221">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="65de7-221">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="65de7-222">Serviço vinculado do Amazon S3</span><span class="sxs-lookup"><span data-stu-id="65de7-222">Amazon S3 linked service</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="65de7-223">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="65de7-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="65de7-224">Conjunto de dados de entrada do Amazon S3</span><span class="sxs-lookup"><span data-stu-id="65de7-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="65de7-225">Configurar **"external": true** informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="65de7-225">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span></span> <span data-ttu-id="65de7-226">Defina essa propriedade como true em um conjunto de dados de entrada que não é produzido por uma atividade no pipeline.</span><span class="sxs-lookup"><span data-stu-id="65de7-226">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="65de7-227">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="65de7-227">Azure Blob output dataset</span></span>

<span data-ttu-id="65de7-228">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="65de7-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="65de7-229">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="65de7-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="65de7-230">O caminho da pasta usa as partes ano, mês, dia e hora da hora de início.</span><span class="sxs-lookup"><span data-stu-id="65de7-230">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="65de7-231">Atividade de cópia em um pipeline com a origem do Amazon S3 e o coletor de blob</span><span class="sxs-lookup"><span data-stu-id="65de7-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="65de7-232">O pipeline contém uma atividade de cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="65de7-232">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="65de7-233">Na definição JSON do pipeline, o tipo de **fonte** está definido como **FileSystemSource** e o tipo de **coletor** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="65de7-233">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="65de7-234">Para mapear colunas de um conjunto de dados de origem para colunas de um conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="65de7-234">To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="65de7-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65de7-235">Next steps</span></span>
<span data-ttu-id="65de7-236">Confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="65de7-236">See the following articles:</span></span>

* <span data-ttu-id="65de7-237">Para saber mais sobre os principais fatores que afetam o desempenho e a movimentação dos dados (atividade de cópia) no Azure Data Factory, além de várias maneiras de otimizá-la, consulte o [Guia de desempenho e ajuste da atividade de cópia](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="65de7-237">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="65de7-238">Para obter instruções passo a passo para criar um pipeline com uma atividade de cópia, consulte o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="65de7-238">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
