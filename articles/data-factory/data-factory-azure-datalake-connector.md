---
title: Copiar dados de e para o Azure Data Lake Store | Microsoft Docs
description: Saiba como copiar dados de e para o Data Lake Store usando o Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 11629fbc83f0554e2097eb4322701654c0bc2028
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="b8579-103">Copiar dados de e para o Data Lake Store usando o Data Factory</span><span class="sxs-lookup"><span data-stu-id="b8579-103">Copy data to and from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="b8579-104">Este artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados de e para o Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b8579-104">This article explains how to use Copy Activity in Azure Data Factory to move data to and from Azure Data Lake Store.</span></span> <span data-ttu-id="b8579-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), uma visão geral da movimentação de dados com a Atividade de Cópia.</span><span class="sxs-lookup"><span data-stu-id="b8579-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="b8579-106">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="b8579-106">Supported scenarios</span></span>
<span data-ttu-id="b8579-107">Você pode copiar dados **do Azure Data Lake Store** para os seguintes armazenamentos de dados:</span><span class="sxs-lookup"><span data-stu-id="b8579-107">You can copy data **from Azure Data Lake Store** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="b8579-108">Você pode copiar dados dos seguintes armazenamentos de dados para o **Azure Data Lake Store**:</span><span class="sxs-lookup"><span data-stu-id="b8579-108">You can copy data from the following data stores **to Azure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="b8579-109">Crie uma conta do Data Lake Store antes de criar um pipeline com a Atividade de Cópia.</span><span class="sxs-lookup"><span data-stu-id="b8579-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="b8579-110">Para obter mais informações, consulte [Introdução ao Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b8579-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="b8579-111">Tipos de autenticação com suporte</span><span class="sxs-lookup"><span data-stu-id="b8579-111">Supported authentication types</span></span>
<span data-ttu-id="b8579-112">O conector do Data Lake Store dá suporte a esses tipos de autenticação:</span><span class="sxs-lookup"><span data-stu-id="b8579-112">The Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="b8579-113">Autenticação de entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="b8579-113">Service principal authentication</span></span>
* <span data-ttu-id="b8579-114">Autenticação de credencial do usuário (OAuth)</span><span class="sxs-lookup"><span data-stu-id="b8579-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="b8579-115">É recomendável que você use a autenticação de entidade de serviço, especialmente para uma cópia de dados agendada.</span><span class="sxs-lookup"><span data-stu-id="b8579-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="b8579-116">O comportamento de expiração do token pode ocorrer com autenticação de credenciais do usuário.</span><span class="sxs-lookup"><span data-stu-id="b8579-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="b8579-117">Para obter os detalhes de configuração, consulte a seção [Propriedades do serviço vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-117">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="b8579-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="b8579-118">Get started</span></span>
<span data-ttu-id="b8579-119">Você pode criar um pipeline com uma atividade de cópia que mova dados bidirecionalmente em um Azure Data Lake Store usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="b8579-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="b8579-120">A maneira mais fácil de criar um pipeline para copiar dados é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="b8579-120">The easiest way to create a pipeline to copy data is to use the **Copy Wizard**.</span></span> <span data-ttu-id="b8579-121">Para encontrar um tutorial sobre a criação de um pipeline usando o Assistente de Cópia, consulte [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="b8579-121">For a tutorial on creating a pipeline by using the Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="b8579-122">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="b8579-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b8579-123">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="b8579-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="b8579-124">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="b8579-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="b8579-125">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="b8579-125">Create a **data factory**.</span></span> <span data-ttu-id="b8579-126">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="b8579-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="b8579-127">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="b8579-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="b8579-128">Por exemplo, se você está copiando dados de um Armazenamento de Blobs do Azure para um Azure Data Lake Store, crie dois serviços vinculados para vincular sua Conta de Armazenamento do Azure e o Azure Data Lake Store ao data factory.</span><span class="sxs-lookup"><span data-stu-id="b8579-128">For example, if you are copying data from an Azure blob storage to an Azure Data Lake Store, you create two linked services to link your Azure storage account and Azure Data Lake store to your data factory.</span></span> <span data-ttu-id="b8579-129">Para propriedades do serviço vinculado que são específicas do Azure Data Lake Store, consulte a seção de [propriedades do serviço vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-129">For linked service properties that are specific to Azure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="b8579-130">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="b8579-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="b8579-131">No exemplo mencionado na última etapa, você cria um conjunto de dados para especificar o contêiner de blobs e a pasta que contém os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="b8579-131">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="b8579-132">Em seguida, você cria outro conjunto de dados para o caminho de pasta e arquivo no Data Lake Store que contém os dados copiados do Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="b8579-132">And, you create another dataset to specify the folder and file path in the Data Lake store that holds the data copied from the blob storage.</span></span> <span data-ttu-id="b8579-133">Para propriedades do conjunto de dados que são específicas do Azure Data Lake Store, consulte a seção [propriedades do conjunto de dados](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-133">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="b8579-134">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="b8579-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="b8579-135">No exemplo mencionado anteriormente, você usa BlobSource como fonte e AzureDataLakeStoreSink como coletor para a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="b8579-135">In the example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for the copy activity.</span></span> <span data-ttu-id="b8579-136">De modo similar, se você estiver copiando do Azure Data Lake Store para o Armazenamento de Blobs do Azure, use AzureDataLakeStoreSource e BlobSink na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="b8579-136">Similarly, if you are copying from Azure Data Lake Store to Azure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in the copy activity.</span></span> <span data-ttu-id="b8579-137">Para propriedades da atividade de cópia que são específicas do Azure Data Lake Store, consulte a seção de [propriedades da atividade de cópia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-137">For copy activity properties that are specific to Azure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="b8579-138">Para obter detalhes sobre como usar um armazenamento de dados como uma origem ou um coletor, clique no link na seção anterior para o seu armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="b8579-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="b8579-139">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="b8579-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="b8579-140">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="b8579-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="b8579-141">Para obter exemplos com definições de JSON das entidades do Data Factory usadas para copiar dados bidirecionalmente em um Azure Data Lake Store, confira a seção [Exemplos de JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b8579-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="b8579-142">As seções que a seguir fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas ao Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b8579-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Data Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b8579-143">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="b8579-143">Linked service properties</span></span>
<span data-ttu-id="b8579-144">Um serviço vinculado vincula um armazenamento de dados a um data factory.</span><span class="sxs-lookup"><span data-stu-id="b8579-144">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="b8579-145">Crie um serviço vinculado do tipo **AzureDataLakeStore** para vincular os dados do Data Lake Store ao data factory.</span><span class="sxs-lookup"><span data-stu-id="b8579-145">You create a linked service of type **AzureDataLakeStore** to link your Data Lake Store data to your data factory.</span></span> <span data-ttu-id="b8579-146">A tabela a seguir descreve elementos JSON específicos para serviços vinculados do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b8579-146">The following table describes JSON elements specific to Data Lake Store linked services.</span></span> <span data-ttu-id="b8579-147">Você pode escolher entre a entidade de serviço e a autenticação de credenciais de usuário.</span><span class="sxs-lookup"><span data-stu-id="b8579-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="b8579-148">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b8579-148">Property</span></span> | <span data-ttu-id="b8579-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="b8579-149">Description</span></span> | <span data-ttu-id="b8579-150">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b8579-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b8579-151">**tipo**</span><span class="sxs-lookup"><span data-stu-id="b8579-151">**type**</span></span> | <span data-ttu-id="b8579-152">A propriedade type deve ser definida como **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="b8579-152">The type property must be set to **AzureDataLakeStore**.</span></span> | <span data-ttu-id="b8579-153">Sim</span><span class="sxs-lookup"><span data-stu-id="b8579-153">Yes</span></span> |
| <span data-ttu-id="b8579-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="b8579-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="b8579-155">Informações sobre a conta do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b8579-155">Information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="b8579-156">Essas informações usam um dos seguintes formatos: `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="b8579-156">This information takes one of the following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="b8579-157">Sim</span><span class="sxs-lookup"><span data-stu-id="b8579-157">Yes</span></span> |
| <span data-ttu-id="b8579-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="b8579-158">**subscriptionId**</span></span> | <span data-ttu-id="b8579-159">ID de assinatura do Azure à qual a conta do Data Lake Store pertence.</span><span class="sxs-lookup"><span data-stu-id="b8579-159">Azure subscription ID to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="b8579-160">Obrigatório para coletor</span><span class="sxs-lookup"><span data-stu-id="b8579-160">Required for sink</span></span> |
| <span data-ttu-id="b8579-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="b8579-161">**resourceGroupName**</span></span> | <span data-ttu-id="b8579-162">Nome do grupo de recursos do Azure ao qual a conta do Data Lake Store pertence.</span><span class="sxs-lookup"><span data-stu-id="b8579-162">Azure resource group name to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="b8579-163">Obrigatório para coletor</span><span class="sxs-lookup"><span data-stu-id="b8579-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="b8579-164">Autenticação de entidade de serviço (recomendada)</span><span class="sxs-lookup"><span data-stu-id="b8579-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="b8579-165">Para usar a autenticação de entidade de serviço, registre uma entidade de aplicativo no Azure AD (Azure Active Directory) e conceda a ela o acesso ao Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b8579-165">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="b8579-166">Para encontrar as etapas detalhadas, consulte [Autenticação de serviço a serviço](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="b8579-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="b8579-167">Anote os seguintes valores, que são usados para definir o serviço vinculado:</span><span class="sxs-lookup"><span data-stu-id="b8579-167">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="b8579-168">ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b8579-168">Application ID</span></span>
* <span data-ttu-id="b8579-169">Chave do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b8579-169">Application key</span></span> 
* <span data-ttu-id="b8579-170">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="b8579-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8579-171">Se estiver usando o Assistente de Cópia para criar pipelines de dados, lembre-se de conceder à entidade de serviço, pelo menos uma função de **Leitor** no controle de acesso (gerenciamento de identidade e acesso) para a conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b8579-171">If you are using the Copy Wizard to author data pipelines, make sure that you grant the service principal at least a **Reader** role in access control (identity and access management) for the Data Lake Store account.</span></span> <span data-ttu-id="b8579-172">Além disso, conceda à entidade de serviço pelo menos a permissão de **Leitura + Execução** para sua raiz do Data Lake Store ("/") e seus filhos.</span><span class="sxs-lookup"><span data-stu-id="b8579-172">Also, grant the service principal at least **Read + Execute** permission to your Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="b8579-173">Caso contrário, você poderá ver a mensagem "As credenciais fornecidas são inválidas".</span><span class="sxs-lookup"><span data-stu-id="b8579-173">Otherwise you might see the message "The credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="b8579-174">Depois de criar ou atualizar uma entidade de serviço no Azure AD, poderá levar alguns minutos para que as alterações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="b8579-174">After you create or update a service principal in Azure AD, it can take a few minutes for the changes to take effect.</span></span> <span data-ttu-id="b8579-175">Verifique as configurações da ACL (lista de controle de acesso) do Data Lake Store e da entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="b8579-175">Check the service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="b8579-176">Se você ainda vir a mensagem “As credenciais fornecidas são inválidas”, aguarde alguns instantes e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="b8579-176">If you still see the message "The credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="b8579-177">Use a autenticação de entidade de serviço especificando as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="b8579-177">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="b8579-178">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b8579-178">Property</span></span> | <span data-ttu-id="b8579-179">Descrição</span><span class="sxs-lookup"><span data-stu-id="b8579-179">Description</span></span> | <span data-ttu-id="b8579-180">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b8579-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b8579-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="b8579-181">**servicePrincipalId**</span></span> | <span data-ttu-id="b8579-182">Especifique a ID do cliente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b8579-182">Specify the application's client ID.</span></span> | <span data-ttu-id="b8579-183">Sim</span><span class="sxs-lookup"><span data-stu-id="b8579-183">Yes</span></span> |
| <span data-ttu-id="b8579-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="b8579-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="b8579-185">Especifique a chave do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b8579-185">Specify the application's key.</span></span> | <span data-ttu-id="b8579-186">Sim</span><span class="sxs-lookup"><span data-stu-id="b8579-186">Yes</span></span> |
| <span data-ttu-id="b8579-187">**tenant**</span><span class="sxs-lookup"><span data-stu-id="b8579-187">**tenant**</span></span> | <span data-ttu-id="b8579-188">Especifique as informações de locatário (domínio nome ou ID do Locatário) em que o aplicativo reside.</span><span class="sxs-lookup"><span data-stu-id="b8579-188">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="b8579-189">É possível recuperá-las focalizando o mouse no canto superior direito do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8579-189">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="b8579-190">Sim</span><span class="sxs-lookup"><span data-stu-id="b8579-190">Yes</span></span> |

<span data-ttu-id="b8579-191">**Exemplo: autenticação de entidade de serviço**</span><span class="sxs-lookup"><span data-stu-id="b8579-191">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="b8579-192">Autenticação de credenciais de usuário</span><span class="sxs-lookup"><span data-stu-id="b8579-192">User credential authentication</span></span>
<span data-ttu-id="b8579-193">Como alternativa, você pode usar a autenticação de credenciais do usuário para copiar de ou para o Data Lake Store especificando as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="b8579-193">Alternatively, you can use user credential authentication to copy from or to Data Lake Store by specifying the following properties:</span></span>

| <span data-ttu-id="b8579-194">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b8579-194">Property</span></span> | <span data-ttu-id="b8579-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="b8579-195">Description</span></span> | <span data-ttu-id="b8579-196">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b8579-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b8579-197">**authorization**</span><span class="sxs-lookup"><span data-stu-id="b8579-197">**authorization**</span></span> | <span data-ttu-id="b8579-198">Clique no botão **Autorizar** no Editor do Data Factory e insira as suas credenciais, que atribuem a URL de autorização gerada automaticamente a essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="b8579-198">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="b8579-199">Sim</span><span class="sxs-lookup"><span data-stu-id="b8579-199">Yes</span></span> |
| <span data-ttu-id="b8579-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="b8579-200">**sessionId**</span></span> | <span data-ttu-id="b8579-201">A ID de sessão OAuth da sessão de autorização OAuth.</span><span class="sxs-lookup"><span data-stu-id="b8579-201">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="b8579-202">Cada ID da sessão é exclusiva e pode ser usada somente uma vez.</span><span class="sxs-lookup"><span data-stu-id="b8579-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="b8579-203">Essa configuração é gerada automaticamente quando você usa o Editor do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b8579-203">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="b8579-204">Sim</span><span class="sxs-lookup"><span data-stu-id="b8579-204">Yes</span></span> |

<span data-ttu-id="b8579-205">**Exemplo: autenticação de credenciais do usuário**</span><span class="sxs-lookup"><span data-stu-id="b8579-205">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="b8579-206">Expiração do token</span><span class="sxs-lookup"><span data-stu-id="b8579-206">Token expiration</span></span>
<span data-ttu-id="b8579-207">O código de autorização gerado usando o botão **Autorizar** expira após um determinado período.</span><span class="sxs-lookup"><span data-stu-id="b8579-207">The authorization code that you generate by using the **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="b8579-208">A mensagem a seguir significa que o token de autenticação expirou:</span><span class="sxs-lookup"><span data-stu-id="b8579-208">The following message means that the authentication token has expired:</span></span>

<span data-ttu-id="b8579-209">Erro na operação de credencial: invalid_grant – AADSTS70002: Erro ao validar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="b8579-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="b8579-210">AADSTS70008: a concessão de acesso fornecida expirou ou foi revogada.</span><span class="sxs-lookup"><span data-stu-id="b8579-210">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="b8579-211">ID do rastreamento: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID de correlação: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Carimbo de data/hora: 2015-12-15 21-09-31Z.</span><span class="sxs-lookup"><span data-stu-id="b8579-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="b8579-212">A tabela a seguir mostra os tempos de expiração de diferentes tipos de contas de usuário:</span><span class="sxs-lookup"><span data-stu-id="b8579-212">The following table shows the expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="b8579-213">Tipo de usuário</span><span class="sxs-lookup"><span data-stu-id="b8579-213">User type</span></span> | <span data-ttu-id="b8579-214">Expira após</span><span class="sxs-lookup"><span data-stu-id="b8579-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="b8579-215">Contas de usuário *não* gerenciadas pelo Azure Active Directory (por exemplo, @hotmail.com ou @live.com)</span><span class="sxs-lookup"><span data-stu-id="b8579-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="b8579-216">12 horas</span><span class="sxs-lookup"><span data-stu-id="b8579-216">12 hours</span></span> |
| <span data-ttu-id="b8579-217">Contas de usuários gerenciadas pelo Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8579-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="b8579-218">14 dias após a última execução da fatia</span><span class="sxs-lookup"><span data-stu-id="b8579-218">14 days after the last slice run</span></span> <br/><br/><span data-ttu-id="b8579-219">90 dias, se uma fatia com base em serviços vinculados do OAuth for executada pelo menos uma vez a cada 14 dias</span><span class="sxs-lookup"><span data-stu-id="b8579-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="b8579-220">Se você alterar sua senha antes do momento de expiração do token, o token expirará imediatamente.</span><span class="sxs-lookup"><span data-stu-id="b8579-220">If you change your password before the token expiration time, the token expires immediately.</span></span> <span data-ttu-id="b8579-221">Você verá a mensagem mencionada anteriormente nesta seção.</span><span class="sxs-lookup"><span data-stu-id="b8579-221">You will see the message mentioned earlier in this section.</span></span>

<span data-ttu-id="b8579-222">Você pode reautorizar a conta usando o botão **Autorizar** quando o token expirar para reimplantar o serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="b8579-222">You can reauthorize the account by using the **Authorize** button when the token expires to redeploy the linked service.</span></span> <span data-ttu-id="b8579-223">Você também pode gerar valores para as propriedades **sessionId** e **authorization** programaticamente usando o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8579-223">You can also generate values for the **sessionId** and **authorization** properties programmatically by using the following code:</span></span>


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
<span data-ttu-id="b8579-224">Para encontrar detalhes sobre as classes do Data Factory usadas no código, consulte os tópicos [Classe AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [Classe AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) e [Classe AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8579-224">For details about the Data Factory classes used in the code, see the [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="b8579-225">Adicione uma referência à versão `2.9.10826.1824` de `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` para a classe `WindowsFormsWebAuthenticationDialog` usada no código.</span><span class="sxs-lookup"><span data-stu-id="b8579-225">Add a reference to version `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for the `WindowsFormsWebAuthenticationDialog` class used in the code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="b8579-226">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="b8579-226">Dataset properties</span></span>
<span data-ttu-id="b8579-227">Para especificar um conjunto de dados para representar os dados de entrada em um Data Lake Store, defina a propriedade **type** do conjunto de dados para **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="b8579-227">To specify a dataset to represent input data in a Data Lake Store, you set the **type** property of the dataset to **AzureDataLakeStore**.</span></span> <span data-ttu-id="b8579-228">Defina a propriedade **linkedServiceName** do conjunto de dados para o nome do serviço vinculado do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b8579-228">Set the **linkedServiceName** property of the dataset to the name of the Data Lake Store linked service.</span></span> <span data-ttu-id="b8579-229">Para obter uma lista completa das seções e propriedades JSON disponíveis para definir conjuntos de dados, consulte o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="b8579-229">For a full list of JSON sections and properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b8579-230">As seções de um conjunto de dados no JSON, como **structure**, **availability** e **policy** são similares para todos os tipos de conjunto de dados (Banco de Dados SQL do Azure, Blob do Azure e tabela do Azure, por exemplo).</span><span class="sxs-lookup"><span data-stu-id="b8579-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="b8579-231">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização e o formato dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="b8579-231">The **typeProperties** section is different for each type of dataset and provides information such as location and format of the data in the data store.</span></span> 

<span data-ttu-id="b8579-232">A seção **typeProperties** do conjunto de um conjunto de dados do tipo **AzureDataLakeStore** contém a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="b8579-232">The **typeProperties** section for a dataset of type **AzureDataLakeStore** contains the following properties:</span></span>

| <span data-ttu-id="b8579-233">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b8579-233">Property</span></span> | <span data-ttu-id="b8579-234">Descrição</span><span class="sxs-lookup"><span data-stu-id="b8579-234">Description</span></span> | <span data-ttu-id="b8579-235">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b8579-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b8579-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="b8579-236">**folderPath**</span></span> |<span data-ttu-id="b8579-237">Caminho para o contêiner e a pasta no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b8579-237">Path to the container and folder in Data Lake Store.</span></span> |<span data-ttu-id="b8579-238">Sim</span><span class="sxs-lookup"><span data-stu-id="b8579-238">Yes</span></span> |
| <span data-ttu-id="b8579-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="b8579-239">**fileName**</span></span> |<span data-ttu-id="b8579-240">O nome do arquivo no Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b8579-240">Name of the file in Azure Data Lake Store.</span></span> <span data-ttu-id="b8579-241">A propriedade **fileName** é opcional e diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b8579-241">The **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="b8579-242">Caso você especifique um **fileName**, a atividade (incluindo Cópia) funcionará no arquivo específico.</span><span class="sxs-lookup"><span data-stu-id="b8579-242">If you specify **fileName**, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="b8579-243">Quando **fileName** não for especificado, a Cópia incluirá todos os arquivos do **folderPath** para o conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="b8579-243">When **fileName** is not specified, Copy includes all files in **folderPath** in the input dataset.</span></span><br/><br/><span data-ttu-id="b8579-244">Quando **fileName** não for especificado para um conjunto de dados de saída e **preserveHierarchy** não for especificado em um coletor de atividade, o nome do arquivo gerado está no formato Data._Guid_.txt\`.</span><span class="sxs-lookup"><span data-stu-id="b8579-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the format Data._Guid_.txt\`.</span></span> <span data-ttu-id="b8579-245">Por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="b8579-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="b8579-246">Não</span><span class="sxs-lookup"><span data-stu-id="b8579-246">No</span></span> |
| <span data-ttu-id="b8579-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="b8579-247">**partitionedBy**</span></span> |<span data-ttu-id="b8579-248">A propriedade **partitionedBy** é opcional.</span><span class="sxs-lookup"><span data-stu-id="b8579-248">The **partitionedBy** property is optional.</span></span> <span data-ttu-id="b8579-249">Você pode usá-la para especificar um caminho de pasta dinâmico e o nome de arquivo para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="b8579-249">You can use it to specify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="b8579-250">Por exemplo, **folderPath** pode ser parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="b8579-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="b8579-251">Para encontrar detalhes e exemplos, consulte [A propriedade partitionedBy](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="b8579-251">For details and examples, see [The partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="b8579-252">Não</span><span class="sxs-lookup"><span data-stu-id="b8579-252">No</span></span> |
| <span data-ttu-id="b8579-253">**format**</span><span class="sxs-lookup"><span data-stu-id="b8579-253">**format**</span></span> | <span data-ttu-id="b8579-254">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="b8579-254">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="b8579-255">Defina a propriedade **type** sob **format** para um desses valores.</span><span class="sxs-lookup"><span data-stu-id="b8579-255">Set the **type** property under **format** to one of these values.</span></span> <span data-ttu-id="b8579-256">Para obter mais informações, consulte as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato ORC](data-factory-supported-file-and-compression-formats.md#orc-format) e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format) no artigo [Formatos de arquivo aos quais o Azure Data Factory dá suporte](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="b8579-256">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in the [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="b8579-257">Se você quiser copiar arquivos no estado em que se encontram entre repositórios com base em arquivo (cópia binária), ignore a seção `format` nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="b8579-257">If you want to copy files "as-is" between file-based stores (binary copy), skip the `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="b8579-258">Não</span><span class="sxs-lookup"><span data-stu-id="b8579-258">No</span></span> |
| <span data-ttu-id="b8579-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="b8579-259">**compression**</span></span> | <span data-ttu-id="b8579-260">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="b8579-260">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="b8579-261">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="b8579-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="b8579-262">Os níveis de suporte são **Ideal** e **Mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="b8579-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="b8579-263">Para saber mais, confira [Formatos de arquivo aos quais o Azure Data Factory dá suporte](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="b8579-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="b8579-264">Não</span><span class="sxs-lookup"><span data-stu-id="b8579-264">No</span></span> |

### <a name="the-partitionedby-property"></a><span data-ttu-id="b8579-265">A propriedade partitionedBy</span><span class="sxs-lookup"><span data-stu-id="b8579-265">The partitionedBy property</span></span>
<span data-ttu-id="b8579-266">Você pode especificar propriedades **folderPath** e **fileName** dinâmicas para dados de série temporal com a propriedade **partitionedBy**, funções do Data Factory e variáveis do sistema.</span><span class="sxs-lookup"><span data-stu-id="b8579-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with the **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="b8579-267">Para encontrar detalhes, consulte o artigo [Azure Data Factory – Funções e Variáveis do Sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="b8579-267">For details, see the [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="b8579-268">No exemplo a seguir, `{Slice}` é substituído pelo valor da variável do sistema do Data Factory `SliceStart` no formato especificado (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="b8579-268">In the following example, `{Slice}` is replaced with the value of the Data Factory system variable `SliceStart` in the format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="b8579-269">O nome `SliceStart` se refere à hora de início da fatia.</span><span class="sxs-lookup"><span data-stu-id="b8579-269">The name `SliceStart` refers to the start time of the slice.</span></span> <span data-ttu-id="b8579-270">A propriedade `folderPath` é diferente para cada fatia, como em `wikidatagateway/wikisampledataout/2014100103` ou `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="b8579-270">The `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="b8579-271">No exemplo a seguir, o ano, o mês, o dia e a hora de `SliceStart` são extraídos em variáveis separadas usadas pelas propriedades `folderPath` e `fileName`:</span><span class="sxs-lookup"><span data-stu-id="b8579-271">In the following example, the year, month, day, and time of `SliceStart` are extracted into separate variables that are used by the `folderPath` and `fileName` properties:</span></span>
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="b8579-272">Para obter mais detalhes sobre conjuntos de dados de série temporal, agendamento e fatias, consulte os artigos [Conjuntos de dados no Azure Data Factory](data-factory-create-datasets.md) e [Agendamento e execução com o Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="b8579-272">For more details on time-series datasets, scheduling, and slices, see the [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="b8579-273">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="b8579-273">Copy activity properties</span></span>
<span data-ttu-id="b8579-274">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="b8579-274">For a full list of sections and properties available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b8579-275">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="b8579-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="b8579-276">As propriedades disponíveis na seção **typeProperties** de uma atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="b8579-276">The properties available in the **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="b8579-277">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="b8579-277">For a copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="b8579-278">**AzureDataLakeStoreSource** dá suporte à seguinte propriedade na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="b8579-278">**AzureDataLakeStoreSource** supports the following property in the **typeProperties** section:</span></span>

| <span data-ttu-id="b8579-279">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b8579-279">Property</span></span> | <span data-ttu-id="b8579-280">Descrição</span><span class="sxs-lookup"><span data-stu-id="b8579-280">Description</span></span> | <span data-ttu-id="b8579-281">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="b8579-281">Allowed values</span></span> | <span data-ttu-id="b8579-282">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b8579-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b8579-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="b8579-283">**recursive**</span></span> |<span data-ttu-id="b8579-284">Indica se os dados são lidos recursivamente das subpastas ou somente da pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="b8579-284">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="b8579-285">True (valor padrão), False</span><span class="sxs-lookup"><span data-stu-id="b8579-285">True (default value), False</span></span> |<span data-ttu-id="b8579-286">Não</span><span class="sxs-lookup"><span data-stu-id="b8579-286">No</span></span> |


<span data-ttu-id="b8579-287">**AzureDataLakeStoreSink** dá suporte às seguintes propriedades na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="b8579-287">**AzureDataLakeStoreSink** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="b8579-288">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b8579-288">Property</span></span> | <span data-ttu-id="b8579-289">Descrição</span><span class="sxs-lookup"><span data-stu-id="b8579-289">Description</span></span> | <span data-ttu-id="b8579-290">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="b8579-290">Allowed values</span></span> | <span data-ttu-id="b8579-291">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b8579-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b8579-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="b8579-292">**copyBehavior**</span></span> |<span data-ttu-id="b8579-293">Especifica o comportamento da cópia.</span><span class="sxs-lookup"><span data-stu-id="b8579-293">Specifies the copy behavior.</span></span> |<span data-ttu-id="b8579-294"><b>PreserveHierarchy</b>: preserva a hierarquia de arquivos na pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="b8579-294"><b>PreserveHierarchy</b>: Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="b8579-295">O caminho relativo do arquivo de origem para a pasta de origem é idêntico ao caminho relativo do arquivo de destino para a pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="b8579-295">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="b8579-296"><b>FlattenHierarchy</b>: todos os arquivos da pasta de origem são criados no primeiro nível da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="b8579-296"><b>FlattenHierarchy</b>: All files from the source folder are created in the first level of the target folder.</span></span> <span data-ttu-id="b8579-297">Os arquivos de destino são criados com nomes gerados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b8579-297">The target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="b8579-298"><b>MergeFiles</b>: mescla todos os arquivos da pasta de origem em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="b8579-298"><b>MergeFiles</b>: Merges all files from the source folder to one file.</span></span> <span data-ttu-id="b8579-299">Se o nome do arquivo ou do blob for especificado, o nome do arquivo mesclado será o nome especificado.</span><span class="sxs-lookup"><span data-stu-id="b8579-299">If the file or blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="b8579-300">Caso contrário, o nome do arquivo será gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b8579-300">Otherwise, the file name is autogenerated.</span></span> |<span data-ttu-id="b8579-301">Não</span><span class="sxs-lookup"><span data-stu-id="b8579-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="b8579-302">exemplos de recursive e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="b8579-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="b8579-303">Esta seção descreve o comportamento resultante da operação de cópia para diferentes combinações de valores recursive e copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="b8579-303">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="b8579-304">recursiva</span><span class="sxs-lookup"><span data-stu-id="b8579-304">recursive</span></span> | <span data-ttu-id="b8579-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="b8579-305">copyBehavior</span></span> | <span data-ttu-id="b8579-306">Comportamento resultante</span><span class="sxs-lookup"><span data-stu-id="b8579-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8579-307">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="b8579-307">true</span></span> |<span data-ttu-id="b8579-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="b8579-308">preserveHierarchy</span></span> |<span data-ttu-id="b8579-309">Para uma pasta de origem Pasta1 com a seguinte estrutura: </span><span class="sxs-lookup"><span data-stu-id="b8579-309">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="b8579-310">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-310">Folder1</span></span><br/><span data-ttu-id="b8579-311">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b8579-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b8579-312">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b8579-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b8579-313">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b8579-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b8579-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b8579-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b8579-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b8579-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b8579-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b8579-317">a pasta de destino Pasta1 é criada com a mesma estrutura da origem</span><span class="sxs-lookup"><span data-stu-id="b8579-317">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="b8579-318">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-318">Folder1</span></span><br/><span data-ttu-id="b8579-319">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b8579-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b8579-320">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b8579-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b8579-321">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b8579-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b8579-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b8579-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b8579-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b8579-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5.</span><span class="sxs-lookup"><span data-stu-id="b8579-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="b8579-325">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="b8579-325">true</span></span> |<span data-ttu-id="b8579-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="b8579-326">flattenHierarchy</span></span> |<span data-ttu-id="b8579-327">Para uma pasta de origem Pasta1 com a seguinte estrutura: </span><span class="sxs-lookup"><span data-stu-id="b8579-327">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="b8579-328">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-328">Folder1</span></span><br/><span data-ttu-id="b8579-329">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b8579-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b8579-330">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b8579-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b8579-331">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b8579-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b8579-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b8579-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b8579-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b8579-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b8579-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b8579-335">a Pasta1 de destino é criada com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="b8579-335">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="b8579-336">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-336">Folder1</span></span><br/><span data-ttu-id="b8579-337">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b8579-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="b8579-338">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b8579-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="b8579-339">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b8579-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="b8579-340">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b8579-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="b8579-341">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b8579-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="b8579-342">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="b8579-342">true</span></span> |<span data-ttu-id="b8579-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="b8579-343">mergeFiles</span></span> |<span data-ttu-id="b8579-344">Para uma pasta de origem Pasta1 com a seguinte estrutura: </span><span class="sxs-lookup"><span data-stu-id="b8579-344">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="b8579-345">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-345">Folder1</span></span><br/><span data-ttu-id="b8579-346">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b8579-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b8579-347">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b8579-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b8579-348">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b8579-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b8579-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b8579-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b8579-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b8579-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b8579-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b8579-352">a Pasta1 de destino é criada com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="b8579-352">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="b8579-353">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-353">Folder1</span></span><br/><span data-ttu-id="b8579-354">&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos dos Arquivo1 + Arquivo2 + Arquivo3 + Arquivo4 + Arquivo5 são mesclados em um único arquivo com um nome de arquivo gerado automaticamente</span><span class="sxs-lookup"><span data-stu-id="b8579-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="b8579-355">false</span><span class="sxs-lookup"><span data-stu-id="b8579-355">false</span></span> |<span data-ttu-id="b8579-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="b8579-356">preserveHierarchy</span></span> |<span data-ttu-id="b8579-357">Para uma pasta de origem Pasta1 com a seguinte estrutura: </span><span class="sxs-lookup"><span data-stu-id="b8579-357">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="b8579-358">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-358">Folder1</span></span><br/><span data-ttu-id="b8579-359">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b8579-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b8579-360">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b8579-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b8579-361">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b8579-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b8579-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b8579-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b8579-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b8579-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b8579-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b8579-365">a pasta de destino Pasta1 é criada com a seguinte estrutura</span><span class="sxs-lookup"><span data-stu-id="b8579-365">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="b8579-366">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-366">Folder1</span></span><br/><span data-ttu-id="b8579-367">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b8579-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b8579-368">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b8579-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="b8579-369">Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados.</span><span class="sxs-lookup"><span data-stu-id="b8579-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="b8579-370">false</span><span class="sxs-lookup"><span data-stu-id="b8579-370">false</span></span> |<span data-ttu-id="b8579-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="b8579-371">flattenHierarchy</span></span> |<span data-ttu-id="b8579-372">Para uma pasta de origem Pasta1 com a seguinte estrutura: </span><span class="sxs-lookup"><span data-stu-id="b8579-372">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="b8579-373">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-373">Folder1</span></span><br/><span data-ttu-id="b8579-374">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b8579-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b8579-375">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b8579-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b8579-376">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b8579-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b8579-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b8579-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b8579-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b8579-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b8579-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b8579-380">a pasta de destino Pasta1 é criada com a seguinte estrutura</span><span class="sxs-lookup"><span data-stu-id="b8579-380">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="b8579-381">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-381">Folder1</span></span><br/><span data-ttu-id="b8579-382">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b8579-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="b8579-383">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b8579-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="b8579-384">Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados.</span><span class="sxs-lookup"><span data-stu-id="b8579-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="b8579-385">false</span><span class="sxs-lookup"><span data-stu-id="b8579-385">false</span></span> |<span data-ttu-id="b8579-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="b8579-386">mergeFiles</span></span> |<span data-ttu-id="b8579-387">Para uma pasta de origem Pasta1 com a seguinte estrutura: </span><span class="sxs-lookup"><span data-stu-id="b8579-387">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="b8579-388">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-388">Folder1</span></span><br/><span data-ttu-id="b8579-389">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b8579-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b8579-390">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b8579-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b8579-391">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b8579-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b8579-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b8579-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b8579-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b8579-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b8579-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b8579-395">a pasta de destino Pasta1 é criada com a seguinte estrutura</span><span class="sxs-lookup"><span data-stu-id="b8579-395">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="b8579-396">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b8579-396">Folder1</span></span><br/><span data-ttu-id="b8579-397">&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos dos Arquivo1 + Arquivo2 são mesclados em um único arquivo com um nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b8579-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="b8579-398">Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b8579-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="b8579-399">Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados.</span><span class="sxs-lookup"><span data-stu-id="b8579-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="b8579-400">Formatos de arquivo e de compactação com suporte</span><span class="sxs-lookup"><span data-stu-id="b8579-400">Supported file and compression formats</span></span>
<span data-ttu-id="b8579-401">Para obter detalhes, consulte o artigo [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="b8579-401">For details, see the [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-data-lake-store"></a><span data-ttu-id="b8579-402">Exemplos JSON para cópia de dados de e para o Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b8579-402">JSON examples for copying data to and from Data Lake Store</span></span>
<span data-ttu-id="b8579-403">Os exemplos a seguir fornecem as definições de JSON de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b8579-403">The following examples provide sample JSON definitions.</span></span> <span data-ttu-id="b8579-404">Você pode usar essas definições de exemplo para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b8579-404">You can use these sample definitions to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b8579-405">Os exemplos mostram como copiar dados de e para o Data Lake Store e o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8579-405">The examples show how to copy data to and from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="b8579-406">No entanto, os dados podem ser copiados _diretamente_ de qualquer uma das fontes para qualquer um dos coletores com suporte.</span><span class="sxs-lookup"><span data-stu-id="b8579-406">However, data can be copied _directly_ from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="b8579-407">Para obter mais informações, consulte a seção "Fontes de dados e formatos com suporte" no artigo [Mover dados usando a Atividade de Cópia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b8579-407">For more information, see the section "Supported data stores and formats" in the [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-to-azure-data-lake-store"></a><span data-ttu-id="b8579-408">Exemplo: copiar dados do Armazenamento de Blobs do Azure para o Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b8579-408">Example: Copy data from Azure Blob Storage to Azure Data Lake Store</span></span>
<span data-ttu-id="b8579-409">O código de exemplo nessa seção mostra:</span><span class="sxs-lookup"><span data-stu-id="b8579-409">The example code in this section shows:</span></span>

* <span data-ttu-id="b8579-410">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="b8579-411">Um serviço vinculado do tipo [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="b8579-412">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="b8579-413">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="b8579-414">Um [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="b8579-415">O exemplo mostra como os dados de série temporal do Armazenamento de Blobs do Azure são copiados para o Data Lake Store de hora em hora.</span><span class="sxs-lookup"><span data-stu-id="b8579-415">The examples show how time-series data from Azure Blob Storage is copied to Data Lake Store every hour.</span></span> 

<span data-ttu-id="b8579-416">**Serviço vinculado de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="b8579-416">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="b8579-417">**Serviço vinculado do Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="b8579-417">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="b8579-418">Para obter os detalhes de configuração, consulte a seção [Propriedades do serviço vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-418">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="b8579-419">**Conjunto de dados de entrada de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="b8579-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="b8579-420">No exemplo a seguir, os dados são coletados de um novo blob de hora em hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="b8579-420">In the following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="b8579-421">O caminho de pasta e nome de arquivo para o blob são avaliados dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="b8579-421">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b8579-422">O caminho da pasta usa as partes do ano, mês e dia da hora de início.</span><span class="sxs-lookup"><span data-stu-id="b8579-422">The folder path uses the year, month, and day portion of the start time.</span></span> <span data-ttu-id="b8579-423">O nome de arquivo usa a parte de hora da hora de início.</span><span class="sxs-lookup"><span data-stu-id="b8579-423">The file name uses the hour portion of the start time.</span></span> <span data-ttu-id="b8579-424">A configuração `"external": true` informa ao serviço Data Factory que a tabela é externa ao Data Factory e não é produzida por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b8579-424">The `"external": true` setting informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

<span data-ttu-id="b8579-425">**Conjunto de dados de saída do Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="b8579-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="b8579-426">O exemplo a seguir copia dados para o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b8579-426">The following example copies data to Data Lake Store.</span></span> <span data-ttu-id="b8579-427">Os novos dados são copiados para o Data Lake Store de hora em hora.</span><span class="sxs-lookup"><span data-stu-id="b8579-427">New data is copied to Data Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="b8579-428">**Atividade de cópia em um pipeline com uma origem de blob e um coletor Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="b8579-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="b8579-429">No exemplo a seguir, o pipeline contém uma atividade de cópia configurada para usar os conjuntos de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="b8579-429">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="b8579-430">A atividade de cópia está programada para ser executado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="b8579-430">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="b8579-431">Na definição de JSON do pipeline, o tipo `source` é definido como `BlobSource` e o tipo `sink` é definido como `AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="b8579-431">In the pipeline JSON definition, the `source` type is set to `BlobSource`, and the `sink` type is set to `AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-to-an-azure-blob"></a><span data-ttu-id="b8579-432">Exemplo: copiar dados do Azure Data Lake Store para um Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="b8579-432">Example: Copy data from Azure Data Lake Store to an Azure blob</span></span>
<span data-ttu-id="b8579-433">O código de exemplo nessa seção mostra:</span><span class="sxs-lookup"><span data-stu-id="b8579-433">The example code in this section shows:</span></span>

* <span data-ttu-id="b8579-434">Um serviço vinculado do tipo [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="b8579-435">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="b8579-436">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="b8579-437">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="b8579-438">Um [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que usa [AzureDataLakeStoreSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b8579-439">O código copia dados da série temporal do Data Lake Store para um Blob do Azure de hora em hora.</span><span class="sxs-lookup"><span data-stu-id="b8579-439">The code copies time-series data from Data Lake Store to an Azure blob every hour.</span></span> 

<span data-ttu-id="b8579-440">**Serviço vinculado do Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="b8579-440">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="b8579-441">Para obter os detalhes de configuração, consulte a seção [Propriedades do serviço vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b8579-441">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="b8579-442">**Serviço vinculado de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="b8579-442">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="b8579-443">**Conjunto de dados de entrada do Azure Data Lake**</span><span class="sxs-lookup"><span data-stu-id="b8579-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="b8579-444">Nesse exemplo, configurar `"external"` e `true` informa ao serviço Data Factory que a tabela é externa ao Data Factory e não é produzida por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b8579-444">In this example, setting `"external"` to `true` informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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
<span data-ttu-id="b8579-445">**Conjunto de dados de saída do blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="b8579-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="b8579-446">No exemplo a seguir, os dados são gravados em um novo blob de hora em hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="b8579-446">In the following example, data is written to a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="b8579-447">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="b8579-447">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b8579-448">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="b8579-448">The folder path uses the year, month, day, and hours portion of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="b8579-449">**Uma atividade de cópia em um pipeline com uma origem do Azure Data Lake Store e um coletor de blob**</span><span class="sxs-lookup"><span data-stu-id="b8579-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="b8579-450">No exemplo a seguir, o pipeline contém uma atividade de cópia configurada para usar os conjuntos de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="b8579-450">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="b8579-451">A atividade de cópia está programada para ser executado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="b8579-451">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="b8579-452">Na definição de JSON do pipeline, o tipo `source` é definido como `AzureDataLakeStoreSource` e o tipo `sink` é definido como `BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="b8579-452">In the pipeline JSON definition, the `source` type is set to `AzureDataLakeStoreSource`, and the `sink` type is set to `BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

<span data-ttu-id="b8579-453">Na definição da atividade de cópia, você também pode mapear colunas do conjunto de dados de origem para colunas no conjunto de dados do coletor.</span><span class="sxs-lookup"><span data-stu-id="b8579-453">In the copy activity definition, you can also map columns from the source dataset to columns in the sink dataset.</span></span> <span data-ttu-id="b8579-454">Para obter detalhes, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapear colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="b8579-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b8579-455">Desempenho e ajuste</span><span class="sxs-lookup"><span data-stu-id="b8579-455">Performance and tuning</span></span>
<span data-ttu-id="b8579-456">Para saber mais sobre os fatores que afetam o desempenho da Atividade de Cópia e como otimizá-lo, veja o artigo [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="b8579-456">To learn about the factors that affect Copy Activity performance and how to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
