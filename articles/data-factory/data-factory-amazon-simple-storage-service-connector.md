---
title: "dados de aaaMove do serviço de armazenamento simples Amazon usando a fábrica de dados | Microsoft Docs"
description: "Saiba mais sobre como dados toomove do serviço de armazenamento simples Amazon (S3) por meio do Azure Data Factory."
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
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="a72ac-103">Mover dados do Amazon Simple Storage Service usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a72ac-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="a72ac-104">Este artigo explica como toouse hello atividade de cópia de dados do Azure Data Factory toomove do serviço de armazenamento simples Amazon (S3).</span><span class="sxs-lookup"><span data-stu-id="a72ac-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="a72ac-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="a72ac-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="a72ac-106">Você pode copiar dados de repositório de dados do Amazon S3 tooany suportada coletor.</span><span class="sxs-lookup"><span data-stu-id="a72ac-106">You can copy data from Amazon S3 tooany supported sink data store.</span></span> <span data-ttu-id="a72ac-107">Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="a72ac-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a72ac-108">Fábrica de dados atualmente suporta apenas mover os dados do Amazon S3 tooother armazenamentos de dados, mas não movendo os dados de outros dados armazena tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="a72ac-108">Data Factory currently supports only moving data from Amazon S3 tooother data stores, but not moving data from other data stores tooAmazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="a72ac-109">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="a72ac-109">Required permissions</span></span>
<span data-ttu-id="a72ac-110">toocopy dados do Amazon S3, certifique-se de ter recebido Olá as seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="a72ac-110">toocopy data from Amazon S3, make sure you have been granted hello following permissions:</span></span>

* <span data-ttu-id="a72ac-111">`s3:GetObject` e `s3:GetObjectVersion` para operações de objeto do Amazon S3</span><span class="sxs-lookup"><span data-stu-id="a72ac-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="a72ac-112">`s3:ListBucket` para operações de bucket do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="a72ac-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="a72ac-113">Se você estiver usando o Assistente para cópia de fábrica de dados, de saudação `s3:ListAllMyBuckets` também é necessária.</span><span class="sxs-lookup"><span data-stu-id="a72ac-113">If you are using hello Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="a72ac-114">Para obter detalhes sobre a lista completa de saudação do Amazon S3 permissões, consulte [especificando permissões em uma política de](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="a72ac-114">For details about hello full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="a72ac-115">Introdução</span><span class="sxs-lookup"><span data-stu-id="a72ac-115">Getting started</span></span>
<span data-ttu-id="a72ac-116">Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem do Amazon S3 usando diferentes ferramentas ou APIs.</span><span class="sxs-lookup"><span data-stu-id="a72ac-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="a72ac-117">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="a72ac-117">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a72ac-118">Para obter uma explicação rápida, confira [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) (Tutorial: criar um pipeline usando o Assistente de Cópia).</span><span class="sxs-lookup"><span data-stu-id="a72ac-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="a72ac-119">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="a72ac-119">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a72ac-120">Para obter instruções passo a passo toocreate um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="a72ac-120">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="a72ac-121">Se você usar ferramentas ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="a72ac-121">Whether you use tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="a72ac-122">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="a72ac-122">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="a72ac-123">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="a72ac-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="a72ac-124">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="a72ac-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="a72ac-125">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="a72ac-125">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="a72ac-126">Quando você usar ferramentas ou APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="a72ac-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="a72ac-127">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados do Amazon S3, consulte Olá [exemplo JSON: copiar dados do Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="a72ac-127">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon S3 data store, see hello [JSON example: Copy data from Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="a72ac-128">Para obter detalhes sobre os formatos de arquivo e de compactação com suporte para uma atividade de cópia, consulte [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="a72ac-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="a72ac-129">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="a72ac-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a72ac-130">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="a72ac-130">Linked service properties</span></span>
<span data-ttu-id="a72ac-131">Um serviço vinculado vincula uma fábrica de dados de tooa de repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="a72ac-131">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="a72ac-132">Criar um serviço vinculado do tipo **AwsAccessKey** toolink tooyour fábrica de dados do repositório de seus dados do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="a72ac-132">You create a linked service of type **AwsAccessKey** toolink your Amazon S3 data store tooyour data factory.</span></span> <span data-ttu-id="a72ac-133">Olá, a tabela a seguir fornece o serviço de descrição de JSON de elementos específico tooAmazon S3 (AwsAccessKey) vinculado.</span><span class="sxs-lookup"><span data-stu-id="a72ac-133">hello following table provides description for JSON elements specific tooAmazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="a72ac-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a72ac-134">Property</span></span> | <span data-ttu-id="a72ac-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="a72ac-135">Description</span></span> | <span data-ttu-id="a72ac-136">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="a72ac-136">Allowed values</span></span> | <span data-ttu-id="a72ac-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a72ac-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a72ac-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="a72ac-138">accessKeyID</span></span> |<span data-ttu-id="a72ac-139">ID da chave de acesso ao segredo hello.</span><span class="sxs-lookup"><span data-stu-id="a72ac-139">ID of hello secret access key.</span></span> |<span data-ttu-id="a72ac-140">string</span><span class="sxs-lookup"><span data-stu-id="a72ac-140">string</span></span> |<span data-ttu-id="a72ac-141">Sim</span><span class="sxs-lookup"><span data-stu-id="a72ac-141">Yes</span></span> |
| <span data-ttu-id="a72ac-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="a72ac-142">secretAccessKey</span></span> |<span data-ttu-id="a72ac-143">chave de acesso ao segredo Olá em si.</span><span class="sxs-lookup"><span data-stu-id="a72ac-143">hello secret access key itself.</span></span> |<span data-ttu-id="a72ac-144">Cadeia de caracteres secreta criptografada</span><span class="sxs-lookup"><span data-stu-id="a72ac-144">Encrypted secret string</span></span> |<span data-ttu-id="a72ac-145">Sim</span><span class="sxs-lookup"><span data-stu-id="a72ac-145">Yes</span></span> |

<span data-ttu-id="a72ac-146">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="a72ac-146">Here is an example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="a72ac-147">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="a72ac-147">Dataset properties</span></span>
<span data-ttu-id="a72ac-148">toospecify toorepresent um conjunto de dados de entrada dados no armazenamento de BLOBs do Azure, defina a propriedade tipo saudação do conjunto de dados de saudação muito**AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="a72ac-148">toospecify a dataset toorepresent input data in Azure Blob storage, set hello type property of hello dataset too**AmazonS3**.</span></span> <span data-ttu-id="a72ac-149">Saudação de conjunto **linkedServiceName** serviço vinculado de propriedade de nome de toohello Olá dataset de saudação Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="a72ac-149">Set hello **linkedServiceName** property of hello dataset toohello name of hello Amazon S3 linked service.</span></span> <span data-ttu-id="a72ac-150">Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, confira [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="a72ac-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="a72ac-151">As seções como structure, availability e policy são similares para todos os tipos de conjunto de dados (como banco de dados SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="a72ac-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="a72ac-152">Olá **typeProperties** seção é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="a72ac-152">hello **typeProperties** section is different for each type of dataset, and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="a72ac-153">Olá **typeProperties** seção um conjunto de dados do tipo **AmazonS3** (que inclui o conjunto de dados Olá Amazon S3) tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="a72ac-153">hello **typeProperties** section for a dataset of type **AmazonS3** (which includes hello Amazon S3 dataset) has hello following properties:</span></span>

| <span data-ttu-id="a72ac-154">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a72ac-154">Property</span></span> | <span data-ttu-id="a72ac-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="a72ac-155">Description</span></span> | <span data-ttu-id="a72ac-156">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="a72ac-156">Allowed values</span></span> | <span data-ttu-id="a72ac-157">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a72ac-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a72ac-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="a72ac-158">bucketName</span></span> |<span data-ttu-id="a72ac-159">nome de bucket Olá S3.</span><span class="sxs-lookup"><span data-stu-id="a72ac-159">hello S3 bucket name.</span></span> |<span data-ttu-id="a72ac-160">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="a72ac-160">String</span></span> |<span data-ttu-id="a72ac-161">Sim</span><span class="sxs-lookup"><span data-stu-id="a72ac-161">Yes</span></span> |
| <span data-ttu-id="a72ac-162">chave</span><span class="sxs-lookup"><span data-stu-id="a72ac-162">key</span></span> |<span data-ttu-id="a72ac-163">chave do objeto Olá S3.</span><span class="sxs-lookup"><span data-stu-id="a72ac-163">hello S3 object key.</span></span> |<span data-ttu-id="a72ac-164">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="a72ac-164">String</span></span> |<span data-ttu-id="a72ac-165">Não</span><span class="sxs-lookup"><span data-stu-id="a72ac-165">No</span></span> |
| <span data-ttu-id="a72ac-166">prefixo</span><span class="sxs-lookup"><span data-stu-id="a72ac-166">prefix</span></span> |<span data-ttu-id="a72ac-167">Prefixo da chave do objeto Olá S3.</span><span class="sxs-lookup"><span data-stu-id="a72ac-167">Prefix for hello S3 object key.</span></span> <span data-ttu-id="a72ac-168">Objetos cujas chaves começam com esse prefixo serão selecionados.</span><span class="sxs-lookup"><span data-stu-id="a72ac-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="a72ac-169">Aplica-se apenas quando a chave está vazia.</span><span class="sxs-lookup"><span data-stu-id="a72ac-169">Applies only when key is empty.</span></span> |<span data-ttu-id="a72ac-170">string</span><span class="sxs-lookup"><span data-stu-id="a72ac-170">String</span></span> |<span data-ttu-id="a72ac-171">Não</span><span class="sxs-lookup"><span data-stu-id="a72ac-171">No</span></span> |
| <span data-ttu-id="a72ac-172">version</span><span class="sxs-lookup"><span data-stu-id="a72ac-172">version</span></span> |<span data-ttu-id="a72ac-173">versão de saudação do objeto de Olá S3, se o controle de versão S3 estiver habilitado.</span><span class="sxs-lookup"><span data-stu-id="a72ac-173">hello version of hello S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="a72ac-174">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="a72ac-174">String</span></span> |<span data-ttu-id="a72ac-175">Não</span><span class="sxs-lookup"><span data-stu-id="a72ac-175">No</span></span> |
| <span data-ttu-id="a72ac-176">formato</span><span class="sxs-lookup"><span data-stu-id="a72ac-176">format</span></span> | <span data-ttu-id="a72ac-177">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="a72ac-177">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="a72ac-178">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="a72ac-178">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="a72ac-179">Para obter mais informações, consulte Olá [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [formato Parquet ](data-factory-supported-file-and-compression-formats.md#parquet-format) seções.</span><span class="sxs-lookup"><span data-stu-id="a72ac-179">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="a72ac-180">Se você deseja que os arquivos de toocopy como-entre repositórios baseada em arquivo (cópia binário), skip Olá formato seção em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="a72ac-180">If you want toocopy files as-is between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="a72ac-181">Não</span><span class="sxs-lookup"><span data-stu-id="a72ac-181">No</span></span> | |
| <span data-ttu-id="a72ac-182">compactação</span><span class="sxs-lookup"><span data-stu-id="a72ac-182">compression</span></span> | <span data-ttu-id="a72ac-183">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="a72ac-183">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="a72ac-184">tipos de saudação com suporte são: **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="a72ac-184">hello supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="a72ac-185">níveis de saudação com suporte são: **ideal** e **mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="a72ac-185">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="a72ac-186">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="a72ac-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="a72ac-187">Não</span><span class="sxs-lookup"><span data-stu-id="a72ac-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="a72ac-188">**bucketName + tecla** Especifica o local de saudação do objeto Olá S3, onde bucket é recipiente raiz Olá S3 objetos e a chave é Olá caminho completo toohello S3 objeto.</span><span class="sxs-lookup"><span data-stu-id="a72ac-188">**bucketName + key** specifies hello location of hello S3 object, where bucket is hello root container for S3 objects, and key is hello full path toohello S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="a72ac-189">Conjunto de dados de exemplo com o prefixo</span><span class="sxs-lookup"><span data-stu-id="a72ac-189">Sample dataset with prefix</span></span>

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
### <a name="sample-dataset-with-version"></a><span data-ttu-id="a72ac-190">Conjunto de dados de exemplo (com a versão)</span><span class="sxs-lookup"><span data-stu-id="a72ac-190">Sample dataset (with version)</span></span>

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

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="a72ac-191">Caminhos dinâmicos para S3</span><span class="sxs-lookup"><span data-stu-id="a72ac-191">Dynamic paths for S3</span></span>
<span data-ttu-id="a72ac-192">Olá exemplo anterior usa valores fixos para Olá **chave** e **bucketName** propriedades no conjunto de dados Olá Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="a72ac-192">hello preceding sample uses fixed values for hello **key** and **bucketName** properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="a72ac-193">Você pode fazer com que o Data Factory calcule essas propriedades dinamicamente em tempo de execução usando variáveis de sistema como SliceStart.</span><span class="sxs-lookup"><span data-stu-id="a72ac-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="a72ac-194">Você pode fazer hello mesmo para Olá **prefixo** propriedade de um conjunto de dados do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="a72ac-194">You can do hello same for hello **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="a72ac-195">Veja [Funções e variáveis do sistema do Data Factory](data-factory-functions-variables.md) para obter uma lista das funções e variáveis com suporte.</span><span class="sxs-lookup"><span data-stu-id="a72ac-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="a72ac-196">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="a72ac-196">Copy activity properties</span></span>
<span data-ttu-id="a72ac-197">Para obter uma lista completa das seções e propriedades disponíveis para definir as atividades, consulte [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="a72ac-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="a72ac-198">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="a72ac-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="a72ac-199">As propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="a72ac-199">Properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="a72ac-200">Para a atividade de cópia hello, propriedades variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="a72ac-200">For hello copy activity, properties vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="a72ac-201">Quando uma fonte na atividade de cópia de saudação é do tipo **FileSystemSource** (que inclui Amazon S3), Olá propriedade a seguir está disponível em **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="a72ac-201">When a source in hello copy activity is of type **FileSystemSource** (which includes Amazon S3), hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="a72ac-202">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a72ac-202">Property</span></span> | <span data-ttu-id="a72ac-203">Descrição</span><span class="sxs-lookup"><span data-stu-id="a72ac-203">Description</span></span> | <span data-ttu-id="a72ac-204">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="a72ac-204">Allowed values</span></span> | <span data-ttu-id="a72ac-205">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="a72ac-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a72ac-206">recursiva</span><span class="sxs-lookup"><span data-stu-id="a72ac-206">recursive</span></span> |<span data-ttu-id="a72ac-207">Especifica se a lista de toorecursively S3 objetos no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="a72ac-207">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="a72ac-208">true/false</span><span class="sxs-lookup"><span data-stu-id="a72ac-208">true/false</span></span> |<span data-ttu-id="a72ac-209">Não</span><span class="sxs-lookup"><span data-stu-id="a72ac-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a><span data-ttu-id="a72ac-210">Exemplo JSON: copiar dados do Amazon S3 tooAzure armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="a72ac-210">JSON example: Copy data from Amazon S3 tooAzure Blob storage</span></span>
<span data-ttu-id="a72ac-211">Este exemplo mostra como toocopy dados do Amazon S3 tooan armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a72ac-211">This sample shows how toocopy data from Amazon S3 tooan Azure Blob storage.</span></span> <span data-ttu-id="a72ac-212">No entanto, dados podem ser copiados diretamente muito[qualquer um dos coletores Olá suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a atividade de cópia de saudação na fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="a72ac-212">However, data can be copied directly too[any of hello sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using hello copy activity in Data Factory.</span></span>

<span data-ttu-id="a72ac-213">exemplo Hello fornece definições de JSON para Olá entidades da fábrica de dados a seguir.</span><span class="sxs-lookup"><span data-stu-id="a72ac-213">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="a72ac-214">Você pode usar essas definições toocreate um pipeline toocopy os dados de armazenamento de tooBlob Amazon S3, usando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a72ac-214">You can use these definitions toocreate a pipeline toocopy data from Amazon S3 tooBlob storage, by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="a72ac-215">Um serviço vinculado do tipo [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a72ac-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="a72ac-216">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a72ac-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="a72ac-217">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a72ac-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="a72ac-218">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a72ac-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="a72ac-219">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a72ac-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a72ac-220">exemplo Hello copia dados do Amazon S3 tooan BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="a72ac-220">hello sample copies data from Amazon S3 tooan Azure blob every hour.</span></span> <span data-ttu-id="a72ac-221">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a72ac-221">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="a72ac-222">Serviço vinculado do Amazon S3</span><span class="sxs-lookup"><span data-stu-id="a72ac-222">Amazon S3 linked service</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="a72ac-223">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a72ac-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="a72ac-224">Conjunto de dados de entrada do Amazon S3</span><span class="sxs-lookup"><span data-stu-id="a72ac-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="a72ac-225">Configuração **"externo": true** informa que o serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="a72ac-225">Setting **"external": true** informs hello Data Factory service that hello dataset is external toohello data factory.</span></span> <span data-ttu-id="a72ac-226">Defina essa propriedade tootrue em um conjunto de dados de entrada não é produzido por uma atividade no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="a72ac-226">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

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


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="a72ac-227">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="a72ac-227">Azure Blob output dataset</span></span>

<span data-ttu-id="a72ac-228">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="a72ac-228">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a72ac-229">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="a72ac-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="a72ac-230">caminho da pasta Olá usa partes de ano, mês, dia e horário Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="a72ac-230">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="a72ac-231">Atividade de cópia em um pipeline com a origem do Amazon S3 e o coletor de blob</span><span class="sxs-lookup"><span data-stu-id="a72ac-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="a72ac-232">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="a72ac-232">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="a72ac-233">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**FileSystemSource**, e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a72ac-233">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

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
> <span data-ttu-id="a72ac-234">colunas de toomap de um toocolumns de conjunto de dados de origem de um conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a72ac-234">toomap columns from a source dataset toocolumns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a72ac-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a72ac-235">Next steps</span></span>
<span data-ttu-id="a72ac-236">Consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a72ac-236">See hello following articles:</span></span>

* <span data-ttu-id="a72ac-237">toolearn sobre a chave de fatores que afetam o desempenho de movimentação de dados (Copiar atividade) na fábrica de dados e toooptimize de várias maneiras, consulte Olá [Copiar atividade guia de desempenho e ajuste](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="a72ac-237">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="a72ac-238">Para obter instruções passo a passo para criar um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="a72ac-238">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
