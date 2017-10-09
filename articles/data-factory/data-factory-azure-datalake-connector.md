---
title: "aaaCopy tooand de dados do repositório Azure Data Lake | Microsoft Docs"
description: "Saiba como toocopy tooand de dados do repositório Data Lake por meio do Azure Data Factory"
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
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="34a79-103">Copiar dados tooand do repositório Data Lake usando a fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="34a79-103">Copy data tooand from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="34a79-104">Este artigo explica como toouse atividade de cópia no Azure Data Factory toomove dados tooand do repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="34a79-104">This article explains how toouse Copy Activity in Azure Data Factory toomove data tooand from Azure Data Lake Store.</span></span> <span data-ttu-id="34a79-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) do artigo, uma visão geral de movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="34a79-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="34a79-106">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="34a79-106">Supported scenarios</span></span>
<span data-ttu-id="34a79-107">Você pode copiar dados **do repositório Azure Data Lake** toohello repositórios de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-107">You can copy data **from Azure Data Lake Store** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="34a79-108">Você pode copiar dados de saudação armazenamentos de dados a seguir **tooAzure repositório Data Lake**:</span><span class="sxs-lookup"><span data-stu-id="34a79-108">You can copy data from hello following data stores **tooAzure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="34a79-109">Crie uma conta do Data Lake Store antes de criar um pipeline com a Atividade de Cópia.</span><span class="sxs-lookup"><span data-stu-id="34a79-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="34a79-110">Para obter mais informações, consulte [Introdução ao Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34a79-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="34a79-111">Tipos de autenticação com suporte</span><span class="sxs-lookup"><span data-stu-id="34a79-111">Supported authentication types</span></span>
<span data-ttu-id="34a79-112">conector do repositório Data Lake Olá dá suporte a esses tipos de autenticação:</span><span class="sxs-lookup"><span data-stu-id="34a79-112">hello Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="34a79-113">Autenticação de entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="34a79-113">Service principal authentication</span></span>
* <span data-ttu-id="34a79-114">Autenticação de credencial do usuário (OAuth)</span><span class="sxs-lookup"><span data-stu-id="34a79-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="34a79-115">É recomendável que você use a autenticação de entidade de serviço, especialmente para uma cópia de dados agendada.</span><span class="sxs-lookup"><span data-stu-id="34a79-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="34a79-116">O comportamento de expiração do token pode ocorrer com autenticação de credenciais do usuário.</span><span class="sxs-lookup"><span data-stu-id="34a79-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="34a79-117">Para obter detalhes de configuração, consulte Olá [vinculado propriedades do serviço](#linked-service-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="34a79-117">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="34a79-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="34a79-118">Get started</span></span>
<span data-ttu-id="34a79-119">Você pode criar um pipeline com uma atividade de cópia que mova dados bidirecionalmente em um Azure Data Lake Store usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="34a79-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="34a79-120">toocreate de maneira mais fácil de saudação dados de toocopy um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="34a79-120">hello easiest way toocreate a pipeline toocopy data is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="34a79-121">Para obter um tutorial sobre como criar um pipeline usando o Assistente para cópia de saudação, consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="34a79-121">For a tutorial on creating a pipeline by using hello Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="34a79-122">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="34a79-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="34a79-123">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="34a79-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="34a79-124">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="34a79-125">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="34a79-125">Create a **data factory**.</span></span> <span data-ttu-id="34a79-126">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="34a79-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="34a79-127">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="34a79-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="34a79-128">Por exemplo, se você estiver copiando dados de um armazenamento de BLOBs do Azure tooan repositório Azure Data Lake, você criar duas toolink de serviços vinculados sua conta de armazenamento do Azure e a fábrica de dados de tooyour de armazenamento do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="34a79-128">For example, if you are copying data from an Azure blob storage tooan Azure Data Lake Store, you create two linked services toolink your Azure storage account and Azure Data Lake store tooyour data factory.</span></span> <span data-ttu-id="34a79-129">Para propriedades de serviço vinculado que específico tooAzure repositório Data Lake, consulte [vinculado propriedades do serviço](#linked-service-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="34a79-129">For linked service properties that are specific tooAzure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="34a79-130">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="34a79-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="34a79-131">O exemplo hello mencionado na última etapa do hello, você criará um contêiner de blob do conjunto de dados toospecify hello e a pasta que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="34a79-131">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="34a79-132">E, então, criar outro conjunto de dados toospecify Olá pasta e o caminho no armazenamento do Data Lake Olá que contém dados Olá copiados saudação do armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="34a79-132">And, you create another dataset toospecify hello folder and file path in hello Data Lake store that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="34a79-133">Para propriedades de conjunto de dados que são específico tooAzure repositório Data Lake, consulte [propriedades de conjunto de dados](#dataset-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="34a79-133">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="34a79-134">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="34a79-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="34a79-135">Exemplo hello mencionado anteriormente, você usar BlobSource como uma origem e AzureDataLakeStoreSink como um coletor de atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-135">In hello example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for hello copy activity.</span></span> <span data-ttu-id="34a79-136">Da mesma forma, se você está copiando do repositório Azure Data Lake tooAzure armazenamento de Blob, use AzureDataLakeStoreSource e BlobSink na atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-136">Similarly, if you are copying from Azure Data Lake Store tooAzure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in hello copy activity.</span></span> <span data-ttu-id="34a79-137">Para propriedades de atividade de cópia que específico tooAzure repositório Data Lake, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="34a79-137">For copy activity properties that are specific tooAzure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="34a79-138">Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="34a79-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="34a79-139">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="34a79-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="34a79-140">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="34a79-141">Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um repositório Azure Data Lake, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="34a79-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="34a79-142">Olá seções a seguir fornece detalhes sobre propriedades JSON que são usada toodefine Data Factory entidades específicas tooData Lake repositório.</span><span class="sxs-lookup"><span data-stu-id="34a79-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooData Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="34a79-143">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="34a79-143">Linked service properties</span></span>
<span data-ttu-id="34a79-144">Um serviço vinculado vincula uma fábrica de dados de tooa de repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="34a79-144">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="34a79-145">Criar um serviço vinculado do tipo **AzureDataLakeStore** toolink sua fábrica de dados do repositório Data Lake dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="34a79-145">You create a linked service of type **AzureDataLakeStore** toolink your Data Lake Store data tooyour data factory.</span></span> <span data-ttu-id="34a79-146">Olá, a tabela a seguir descreve os serviços de repositório de Lake tooData vinculado JSON elementos específicos.</span><span class="sxs-lookup"><span data-stu-id="34a79-146">hello following table describes JSON elements specific tooData Lake Store linked services.</span></span> <span data-ttu-id="34a79-147">Você pode escolher entre a entidade de serviço e a autenticação de credenciais de usuário.</span><span class="sxs-lookup"><span data-stu-id="34a79-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="34a79-148">Propriedade</span><span class="sxs-lookup"><span data-stu-id="34a79-148">Property</span></span> | <span data-ttu-id="34a79-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="34a79-149">Description</span></span> | <span data-ttu-id="34a79-150">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="34a79-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34a79-151">**tipo**</span><span class="sxs-lookup"><span data-stu-id="34a79-151">**type**</span></span> | <span data-ttu-id="34a79-152">propriedade do tipo Hello deve ser definida muito**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="34a79-152">hello type property must be set too**AzureDataLakeStore**.</span></span> | <span data-ttu-id="34a79-153">Sim</span><span class="sxs-lookup"><span data-stu-id="34a79-153">Yes</span></span> |
| <span data-ttu-id="34a79-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="34a79-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="34a79-155">Informações sobre Olá conta do repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="34a79-155">Information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="34a79-156">Essas informações tem um dos formatos a seguir de saudação: `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="34a79-156">This information takes one of hello following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="34a79-157">Sim</span><span class="sxs-lookup"><span data-stu-id="34a79-157">Yes</span></span> |
| <span data-ttu-id="34a79-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="34a79-158">**subscriptionId**</span></span> | <span data-ttu-id="34a79-159">Saudação de toowhich ID de assinatura do Azure conta do repositório Data Lake pertence.</span><span class="sxs-lookup"><span data-stu-id="34a79-159">Azure subscription ID toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="34a79-160">Obrigatório para coletor</span><span class="sxs-lookup"><span data-stu-id="34a79-160">Required for sink</span></span> |
| <span data-ttu-id="34a79-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="34a79-161">**resourceGroupName**</span></span> | <span data-ttu-id="34a79-162">Saudação de toowhich de nome do recurso do Azure grupo conta do repositório Data Lake pertence.</span><span class="sxs-lookup"><span data-stu-id="34a79-162">Azure resource group name toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="34a79-163">Obrigatório para coletor</span><span class="sxs-lookup"><span data-stu-id="34a79-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="34a79-164">Autenticação de entidade de serviço (recomendada)</span><span class="sxs-lookup"><span data-stu-id="34a79-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="34a79-165">autenticação principal do serviço toouse, registre uma entidade de aplicativo no Azure Active Directory (AD do Azure) e conceda ele Olá acessar tooData Lake repositório.</span><span class="sxs-lookup"><span data-stu-id="34a79-165">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="34a79-166">Para encontrar as etapas detalhadas, consulte [Autenticação de serviço a serviço](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="34a79-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="34a79-167">Anote Olá valores, que você usar a seguir toodefine Olá vinculado de serviço:</span><span class="sxs-lookup"><span data-stu-id="34a79-167">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="34a79-168">ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="34a79-168">Application ID</span></span>
* <span data-ttu-id="34a79-169">Chave do aplicativo</span><span class="sxs-lookup"><span data-stu-id="34a79-169">Application key</span></span> 
* <span data-ttu-id="34a79-170">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="34a79-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34a79-171">Se você estiver usando pipelines de dados de tooauthor Olá Assistente para cópia, certifique-se de que você conceda a entidade de serviço Olá pelo menos um **leitor** função no controle de acesso (gerenciamento de identidade e acesso) para a conta do repositório Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="34a79-171">If you are using hello Copy Wizard tooauthor data pipelines, make sure that you grant hello service principal at least a **Reader** role in access control (identity and access management) for hello Data Lake Store account.</span></span> <span data-ttu-id="34a79-172">Além disso, conceder a entidade de serviço Olá pelo menos **leitura + Execute** raiz de repositório Data Lake de tooyour permissão ("/") e seus filhos.</span><span class="sxs-lookup"><span data-stu-id="34a79-172">Also, grant hello service principal at least **Read + Execute** permission tooyour Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="34a79-173">Caso contrário, você poderá ver a mensagem de saudação "hello credenciais fornecidas são inválidas."</span><span class="sxs-lookup"><span data-stu-id="34a79-173">Otherwise you might see hello message "hello credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="34a79-174">Depois de criar ou atualizar uma entidade de serviço no AD do Azure, pode levar alguns minutos para Olá alterações tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="34a79-174">After you create or update a service principal in Azure AD, it can take a few minutes for hello changes tootake effect.</span></span> <span data-ttu-id="34a79-175">Verifique a entidade de serviço hello e configurações de ACL (lista) de controle de acesso de repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="34a79-175">Check hello service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="34a79-176">Se você ainda vir a mensagem "hello credenciais fornecidas são inválidas", aguarde um pouco e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="34a79-176">If you still see hello message "hello credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="34a79-177">Use autenticação principal do serviço especificando Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-177">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="34a79-178">Propriedade</span><span class="sxs-lookup"><span data-stu-id="34a79-178">Property</span></span> | <span data-ttu-id="34a79-179">Descrição</span><span class="sxs-lookup"><span data-stu-id="34a79-179">Description</span></span> | <span data-ttu-id="34a79-180">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="34a79-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34a79-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="34a79-181">**servicePrincipalId**</span></span> | <span data-ttu-id="34a79-182">Especifique a ID do cliente. do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="34a79-182">Specify hello application's client ID.</span></span> | <span data-ttu-id="34a79-183">Sim</span><span class="sxs-lookup"><span data-stu-id="34a79-183">Yes</span></span> |
| <span data-ttu-id="34a79-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="34a79-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="34a79-185">Especifique a chave de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="34a79-185">Specify hello application's key.</span></span> | <span data-ttu-id="34a79-186">Sim</span><span class="sxs-lookup"><span data-stu-id="34a79-186">Yes</span></span> |
| <span data-ttu-id="34a79-187">**tenant**</span><span class="sxs-lookup"><span data-stu-id="34a79-187">**tenant**</span></span> | <span data-ttu-id="34a79-188">Especifique as informações de locatário hello (ID de locatário ou de nome de domínio) em que o aplicativo reside.</span><span class="sxs-lookup"><span data-stu-id="34a79-188">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="34a79-189">Você pode recuperá-la por focalização mouse Olá no canto superior direito Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="34a79-189">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="34a79-190">Sim</span><span class="sxs-lookup"><span data-stu-id="34a79-190">Yes</span></span> |

<span data-ttu-id="34a79-191">**Exemplo: autenticação de entidade de serviço**</span><span class="sxs-lookup"><span data-stu-id="34a79-191">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="34a79-192">Autenticação de credenciais de usuário</span><span class="sxs-lookup"><span data-stu-id="34a79-192">User credential authentication</span></span>
<span data-ttu-id="34a79-193">Como alternativa, você pode usar toocopy de autenticação de credenciais de usuário de ou repositório de Lake tooData especificando Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-193">Alternatively, you can use user credential authentication toocopy from or tooData Lake Store by specifying hello following properties:</span></span>

| <span data-ttu-id="34a79-194">Propriedade</span><span class="sxs-lookup"><span data-stu-id="34a79-194">Property</span></span> | <span data-ttu-id="34a79-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="34a79-195">Description</span></span> | <span data-ttu-id="34a79-196">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="34a79-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34a79-197">**authorization**</span><span class="sxs-lookup"><span data-stu-id="34a79-197">**authorization**</span></span> | <span data-ttu-id="34a79-198">Clique em Olá **autorizar** botão no hello Editor da fábrica de dados e insira suas credenciais que atribui a propriedade toothis de URL de autorização do hello gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="34a79-198">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="34a79-199">Sim</span><span class="sxs-lookup"><span data-stu-id="34a79-199">Yes</span></span> |
| <span data-ttu-id="34a79-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="34a79-200">**sessionId**</span></span> | <span data-ttu-id="34a79-201">ID de sessão do OAuth da sessão de autorização de OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="34a79-201">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="34a79-202">Cada ID da sessão é exclusiva e pode ser usada somente uma vez.</span><span class="sxs-lookup"><span data-stu-id="34a79-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="34a79-203">Essa configuração é gerada automaticamente quando você usa Olá Editor da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="34a79-203">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="34a79-204">Sim</span><span class="sxs-lookup"><span data-stu-id="34a79-204">Yes</span></span> |

<span data-ttu-id="34a79-205">**Exemplo: autenticação de credenciais do usuário**</span><span class="sxs-lookup"><span data-stu-id="34a79-205">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="34a79-206">Expiração do token</span><span class="sxs-lookup"><span data-stu-id="34a79-206">Token expiration</span></span>
<span data-ttu-id="34a79-207">Olá código de autorização que você gerar usando Olá **autorizar** botão expira após um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="34a79-207">hello authorization code that you generate by using hello **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="34a79-208">mensagem de saudação significa que esse token de autenticação de saudação expirou:</span><span class="sxs-lookup"><span data-stu-id="34a79-208">hello following message means that hello authentication token has expired:</span></span>

<span data-ttu-id="34a79-209">Erro na operação de credencial: invalid_grant – AADSTS70002: Erro ao validar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="34a79-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="34a79-210">AADSTS70008: Olá fornecido a concessão de acesso expirou ou foi revogado.</span><span class="sxs-lookup"><span data-stu-id="34a79-210">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="34a79-211">ID do rastreamento: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID de correlação: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Carimbo de data/hora: 2015-12-15 21-09-31Z.</span><span class="sxs-lookup"><span data-stu-id="34a79-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="34a79-212">Olá tabela a seguir mostra os tempos de expiração de saudação de diferentes tipos de contas de usuário:</span><span class="sxs-lookup"><span data-stu-id="34a79-212">hello following table shows hello expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="34a79-213">Tipo de usuário</span><span class="sxs-lookup"><span data-stu-id="34a79-213">User type</span></span> | <span data-ttu-id="34a79-214">Expira após</span><span class="sxs-lookup"><span data-stu-id="34a79-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="34a79-215">Contas de usuário *não* gerenciadas pelo Azure Active Directory (por exemplo, @hotmail.com ou @live.com)</span><span class="sxs-lookup"><span data-stu-id="34a79-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="34a79-216">12 horas</span><span class="sxs-lookup"><span data-stu-id="34a79-216">12 hours</span></span> |
| <span data-ttu-id="34a79-217">Contas de usuários gerenciadas pelo Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34a79-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="34a79-218">14 dias após a última fatia de saudação executar</span><span class="sxs-lookup"><span data-stu-id="34a79-218">14 days after hello last slice run</span></span> <br/><br/><span data-ttu-id="34a79-219">90 dias, se uma fatia com base em serviços vinculados do OAuth for executada pelo menos uma vez a cada 14 dias</span><span class="sxs-lookup"><span data-stu-id="34a79-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="34a79-220">Se você alterar sua senha antes de tempo de expiração do token de saudação, token Olá expira imediatamente.</span><span class="sxs-lookup"><span data-stu-id="34a79-220">If you change your password before hello token expiration time, hello token expires immediately.</span></span> <span data-ttu-id="34a79-221">Você verá a mensagem de saudação mencionada anteriormente nesta seção.</span><span class="sxs-lookup"><span data-stu-id="34a79-221">You will see hello message mentioned earlier in this section.</span></span>

<span data-ttu-id="34a79-222">Você pode autorizar a conta hello usando Olá **autorizar** serviço vinculado do botão quando o token de saudação expira tooredeploy hello.</span><span class="sxs-lookup"><span data-stu-id="34a79-222">You can reauthorize hello account by using hello **Authorize** button when hello token expires tooredeploy hello linked service.</span></span> <span data-ttu-id="34a79-223">Você também pode gerar valores para Olá **sessionId** e **autorização** Olá propriedades programaticamente, usando o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="34a79-223">You can also generate values for hello **sessionId** and **authorization** properties programmatically by using hello following code:</span></span>


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
<span data-ttu-id="34a79-224">Para obter detalhes sobre classes de fábrica de dados Olá usados no código hello, consulte Olá [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), e [ Classe AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tópicos.</span><span class="sxs-lookup"><span data-stu-id="34a79-224">For details about hello Data Factory classes used in hello code, see hello [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="34a79-225">Adicionar uma referência tooversion `2.9.10826.1824` de `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` para Olá `WindowsFormsWebAuthenticationDialog` classe usada no código de saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-225">Add a reference tooversion `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for hello `WindowsFormsWebAuthenticationDialog` class used in hello code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="34a79-226">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="34a79-226">Dataset properties</span></span>
<span data-ttu-id="34a79-227">toospecify um dados de entrada de toorepresent do conjunto de dados em um repositório Data Lake, definir Olá **tipo** propriedade de conjunto de dados de saudação muito**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="34a79-227">toospecify a dataset toorepresent input data in a Data Lake Store, you set hello **type** property of hello dataset too**AzureDataLakeStore**.</span></span> <span data-ttu-id="34a79-228">Saudação de conjunto **linkedServiceName** serviço vinculado de propriedade de nome de toohello Olá dataset de saudação repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="34a79-228">Set hello **linkedServiceName** property of hello dataset toohello name of hello Data Lake Store linked service.</span></span> <span data-ttu-id="34a79-229">Para obter uma lista completa de seções JSON e as propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="34a79-229">For a full list of JSON sections and properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="34a79-230">As seções de um conjunto de dados no JSON, como **structure**, **availability** e **policy** são similares para todos os tipos de conjunto de dados (Banco de Dados SQL do Azure, Blob do Azure e tabela do Azure, por exemplo).</span><span class="sxs-lookup"><span data-stu-id="34a79-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="34a79-231">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações como o local e o formato de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-231">hello **typeProperties** section is different for each type of dataset and provides information such as location and format of hello data in hello data store.</span></span> 

<span data-ttu-id="34a79-232">Olá **typeProperties** seção um conjunto de dados do tipo **AzureDataLakeStore** contém Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-232">hello **typeProperties** section for a dataset of type **AzureDataLakeStore** contains hello following properties:</span></span>

| <span data-ttu-id="34a79-233">Propriedade</span><span class="sxs-lookup"><span data-stu-id="34a79-233">Property</span></span> | <span data-ttu-id="34a79-234">Descrição</span><span class="sxs-lookup"><span data-stu-id="34a79-234">Description</span></span> | <span data-ttu-id="34a79-235">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="34a79-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34a79-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="34a79-236">**folderPath**</span></span> |<span data-ttu-id="34a79-237">Contêiner de toohello do caminho e a pasta no repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="34a79-237">Path toohello container and folder in Data Lake Store.</span></span> |<span data-ttu-id="34a79-238">Sim</span><span class="sxs-lookup"><span data-stu-id="34a79-238">Yes</span></span> |
| <span data-ttu-id="34a79-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="34a79-239">**fileName**</span></span> |<span data-ttu-id="34a79-240">Nome do arquivo hello no repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="34a79-240">Name of hello file in Azure Data Lake Store.</span></span> <span data-ttu-id="34a79-241">Olá **fileName** propriedade é opcional e diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="34a79-241">hello **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="34a79-242">Se você especificar **fileName**, atividade de saudação (incluindo cópia) funciona em arquivos específicos da saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-242">If you specify **fileName**, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="34a79-243">Quando **fileName** não for especificado, cópia inclui todos os arquivos em **folderPath** no conjunto de dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="34a79-243">When **fileName** is not specified, Copy includes all files in **folderPath** in hello input dataset.</span></span><br/><br/><span data-ttu-id="34a79-244">Quando **fileName** não for especificado para um conjunto de dados de saída e **preserveHierarchy** não for especificado no coletor de atividade, nome de saudação do arquivo hello gerado está no formato de saudação dados. _GUID_. txt '.</span><span class="sxs-lookup"><span data-stu-id="34a79-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello format Data._Guid_.txt\`.</span></span> <span data-ttu-id="34a79-245">Por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="34a79-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="34a79-246">Não</span><span class="sxs-lookup"><span data-stu-id="34a79-246">No</span></span> |
| <span data-ttu-id="34a79-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="34a79-247">**partitionedBy**</span></span> |<span data-ttu-id="34a79-248">Olá **partitionedBy** propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="34a79-248">hello **partitionedBy** property is optional.</span></span> <span data-ttu-id="34a79-249">Você pode usá-lo toospecify um caminho dinâmico e o nome do arquivo de dados da série temporal.</span><span class="sxs-lookup"><span data-stu-id="34a79-249">You can use it toospecify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="34a79-250">Por exemplo, **folderPath** pode ser parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="34a79-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="34a79-251">Para obter detalhes e exemplos, consulte [Olá partitionedBy propriedade](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="34a79-251">For details and examples, see [hello partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="34a79-252">Não</span><span class="sxs-lookup"><span data-stu-id="34a79-252">No</span></span> |
| <span data-ttu-id="34a79-253">**format**</span><span class="sxs-lookup"><span data-stu-id="34a79-253">**format**</span></span> | <span data-ttu-id="34a79-254">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, e  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="34a79-254">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="34a79-255">Saudação de conjunto **tipo** propriedade em **formato** tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="34a79-255">Set hello **type** property under **format** tooone of these values.</span></span> <span data-ttu-id="34a79-256">Para obter mais informações, consulte Olá [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato ORC](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) seções Olá [formatos de arquivo e compactação com suporte do Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="34a79-256">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in hello [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="34a79-257">Se você deseja que os arquivos de toocopy "como-é" entre repositórios baseada em arquivo (cópia binário), ignore Olá `format` seção em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="34a79-257">If you want toocopy files "as-is" between file-based stores (binary copy), skip hello `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="34a79-258">Não</span><span class="sxs-lookup"><span data-stu-id="34a79-258">No</span></span> |
| <span data-ttu-id="34a79-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="34a79-259">**compression**</span></span> | <span data-ttu-id="34a79-260">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-260">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="34a79-261">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="34a79-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="34a79-262">Os níveis de suporte são **Ideal** e **Mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="34a79-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="34a79-263">Para saber mais, confira [Formatos de arquivo aos quais o Azure Data Factory dá suporte](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="34a79-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="34a79-264">Não</span><span class="sxs-lookup"><span data-stu-id="34a79-264">No</span></span> |

### <a name="hello-partitionedby-property"></a><span data-ttu-id="34a79-265">propriedade de partitionedBy Olá</span><span class="sxs-lookup"><span data-stu-id="34a79-265">hello partitionedBy property</span></span>
<span data-ttu-id="34a79-266">Você pode especificar dinâmico **folderPath** e **fileName** propriedades de dados de série temporal com hello **partitionedBy** propriedade, funções da fábrica de dados e do sistema variáveis.</span><span class="sxs-lookup"><span data-stu-id="34a79-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with hello **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="34a79-267">Para obter detalhes, consulte Olá [do Azure Data Factory - funções e variáveis de sistema](data-factory-functions-variables.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="34a79-267">For details, see hello [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="34a79-268">Em Olá seguinte exemplo, `{Slice}` é substituído pelo valor de saudação da variável de sistema de fábrica de dados Olá `SliceStart` no formato de saudação especificado (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="34a79-268">In hello following example, `{Slice}` is replaced with hello value of hello Data Factory system variable `SliceStart` in hello format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="34a79-269">nome da saudação `SliceStart` refere-se toohello a hora de início da fatia hello.</span><span class="sxs-lookup"><span data-stu-id="34a79-269">hello name `SliceStart` refers toohello start time of hello slice.</span></span> <span data-ttu-id="34a79-270">Olá `folderPath` propriedade é diferente para cada fatia, como em `wikidatagateway/wikisampledataout/2014100103` ou `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="34a79-270">hello `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="34a79-271">Em Olá seguindo o exemplo, ano hello, mês, dia e hora do `SliceStart` são extraídos em variáveis separadas que são usadas por Olá `folderPath` e `fileName` propriedades:</span><span class="sxs-lookup"><span data-stu-id="34a79-271">In hello following example, hello year, month, day, and time of `SliceStart` are extracted into separate variables that are used by hello `folderPath` and `fileName` properties:</span></span>
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
<span data-ttu-id="34a79-272">Para obter mais detalhes sobre conjuntos de dados de série temporal, agendamento e fatias, consulte Olá [conjuntos de dados no Azure Data Factory](data-factory-create-datasets.md) e [fábrica de dados de agendamento e execução](data-factory-scheduling-and-execution.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="34a79-272">For more details on time-series datasets, scheduling, and slices, see hello [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="34a79-273">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="34a79-273">Copy activity properties</span></span>
<span data-ttu-id="34a79-274">Para obter uma lista completa de seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="34a79-274">For a full list of sections and properties available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="34a79-275">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="34a79-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="34a79-276">Olá propriedades disponíveis no hello **typeProperties** seção de uma atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="34a79-276">hello properties available in hello **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="34a79-277">Para uma atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="34a79-277">For a copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="34a79-278">**AzureDataLakeStoreSource** dá suporte a saudação propriedade Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="34a79-278">**AzureDataLakeStoreSource** supports hello following property in hello **typeProperties** section:</span></span>

| <span data-ttu-id="34a79-279">Propriedade</span><span class="sxs-lookup"><span data-stu-id="34a79-279">Property</span></span> | <span data-ttu-id="34a79-280">Descrição</span><span class="sxs-lookup"><span data-stu-id="34a79-280">Description</span></span> | <span data-ttu-id="34a79-281">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="34a79-281">Allowed values</span></span> | <span data-ttu-id="34a79-282">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="34a79-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34a79-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="34a79-283">**recursive**</span></span> |<span data-ttu-id="34a79-284">Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello.</span><span class="sxs-lookup"><span data-stu-id="34a79-284">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="34a79-285">True (valor padrão), False</span><span class="sxs-lookup"><span data-stu-id="34a79-285">True (default value), False</span></span> |<span data-ttu-id="34a79-286">Não</span><span class="sxs-lookup"><span data-stu-id="34a79-286">No</span></span> |


<span data-ttu-id="34a79-287">**AzureDataLakeStoreSink** dá suporte a saudação seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="34a79-287">**AzureDataLakeStoreSink** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="34a79-288">Propriedade</span><span class="sxs-lookup"><span data-stu-id="34a79-288">Property</span></span> | <span data-ttu-id="34a79-289">Descrição</span><span class="sxs-lookup"><span data-stu-id="34a79-289">Description</span></span> | <span data-ttu-id="34a79-290">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="34a79-290">Allowed values</span></span> | <span data-ttu-id="34a79-291">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="34a79-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34a79-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="34a79-292">**copyBehavior**</span></span> |<span data-ttu-id="34a79-293">Especifica o comportamento de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-293">Specifies hello copy behavior.</span></span> |<span data-ttu-id="34a79-294"><b>PreserveHierarchy</b>: preserva a hierarquia de arquivo hello na pasta de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-294"><b>PreserveHierarchy</b>: Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="34a79-295">caminho relativo do Hello arquivo toosource da pasta de origem é idêntico toohello o caminho relativo da pasta de tootarget do arquivo de destino.</span><span class="sxs-lookup"><span data-stu-id="34a79-295">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="34a79-296"><b>FlattenHierarchy</b>: todos os arquivos da pasta de origem Olá são criados no primeiro nível saudação da pasta de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-296"><b>FlattenHierarchy</b>: All files from hello source folder are created in hello first level of hello target folder.</span></span> <span data-ttu-id="34a79-297">arquivos de destino de saudação são criados com nomes gerados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="34a79-297">hello target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="34a79-298"><b>MergeFiles</b>: mescla todos os arquivos Olá pasta tooone do arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="34a79-298"><b>MergeFiles</b>: Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="34a79-299">Se hello nome de arquivo ou blob for especificado, o nome do arquivo mesclado de Olá é nome especificado da saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-299">If hello file or blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="34a79-300">Caso contrário, o nome do arquivo hello é gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="34a79-300">Otherwise, hello file name is autogenerated.</span></span> |<span data-ttu-id="34a79-301">Não</span><span class="sxs-lookup"><span data-stu-id="34a79-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="34a79-302">exemplos de recursive e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="34a79-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="34a79-303">Esta seção descreve o comportamento resultante de saudação da operação de cópia de saudação para diferentes combinações de valores recursiva e copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="34a79-303">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="34a79-304">recursiva</span><span class="sxs-lookup"><span data-stu-id="34a79-304">recursive</span></span> | <span data-ttu-id="34a79-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="34a79-305">copyBehavior</span></span> | <span data-ttu-id="34a79-306">Comportamento resultante</span><span class="sxs-lookup"><span data-stu-id="34a79-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34a79-307">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="34a79-307">true</span></span> |<span data-ttu-id="34a79-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="34a79-308">preserveHierarchy</span></span> |<span data-ttu-id="34a79-309">Para uma pasta de origem Pasta1 com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-309">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="34a79-310">Pasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-310">Folder1</span></span><br/><span data-ttu-id="34a79-311">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="34a79-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="34a79-312">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="34a79-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="34a79-313">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="34a79-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="34a79-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="34a79-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="34a79-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="34a79-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="34a79-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="34a79-317">pasta de destino de Olá Pasta1 é criada com hello mesma estrutura como fonte de saudação</span><span class="sxs-lookup"><span data-stu-id="34a79-317">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="34a79-318">Pasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-318">Folder1</span></span><br/><span data-ttu-id="34a79-319">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="34a79-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="34a79-320">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="34a79-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="34a79-321">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="34a79-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="34a79-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="34a79-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="34a79-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="34a79-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5.</span><span class="sxs-lookup"><span data-stu-id="34a79-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="34a79-325">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="34a79-325">true</span></span> |<span data-ttu-id="34a79-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="34a79-326">flattenHierarchy</span></span> |<span data-ttu-id="34a79-327">Para uma pasta de origem Pasta1 com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-327">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="34a79-328">Pasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-328">Folder1</span></span><br/><span data-ttu-id="34a79-329">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="34a79-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="34a79-330">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="34a79-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="34a79-331">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="34a79-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="34a79-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="34a79-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="34a79-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="34a79-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="34a79-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="34a79-335">destino de saudação Pasta1 é criado com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-335">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="34a79-336">Pasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-336">Folder1</span></span><br/><span data-ttu-id="34a79-337">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="34a79-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="34a79-338">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2</span><span class="sxs-lookup"><span data-stu-id="34a79-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="34a79-339">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo3</span><span class="sxs-lookup"><span data-stu-id="34a79-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="34a79-340">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo4</span><span class="sxs-lookup"><span data-stu-id="34a79-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="34a79-341">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo5</span><span class="sxs-lookup"><span data-stu-id="34a79-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="34a79-342">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="34a79-342">true</span></span> |<span data-ttu-id="34a79-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="34a79-343">mergeFiles</span></span> |<span data-ttu-id="34a79-344">Para uma pasta de origem Pasta1 com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-344">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="34a79-345">Pasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-345">Folder1</span></span><br/><span data-ttu-id="34a79-346">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="34a79-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="34a79-347">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="34a79-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="34a79-348">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="34a79-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="34a79-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="34a79-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="34a79-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="34a79-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="34a79-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="34a79-352">destino de saudação Pasta1 é criado com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-352">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="34a79-353">Pasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-353">Folder1</span></span><br/><span data-ttu-id="34a79-354">&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos dos Arquivo1 + Arquivo2 + Arquivo3 + Arquivo4 + Arquivo5 são mesclados em um único arquivo com um nome de arquivo gerado automaticamente</span><span class="sxs-lookup"><span data-stu-id="34a79-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="34a79-355">false</span><span class="sxs-lookup"><span data-stu-id="34a79-355">false</span></span> |<span data-ttu-id="34a79-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="34a79-356">preserveHierarchy</span></span> |<span data-ttu-id="34a79-357">Para uma pasta de origem Pasta1 com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-357">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="34a79-358">Pasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-358">Folder1</span></span><br/><span data-ttu-id="34a79-359">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="34a79-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="34a79-360">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="34a79-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="34a79-361">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="34a79-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="34a79-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="34a79-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="34a79-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="34a79-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="34a79-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="34a79-365">pasta de destino de saudação Pasta1 é criada com hello estrutura a seguir</span><span class="sxs-lookup"><span data-stu-id="34a79-365">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="34a79-366">Pasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-366">Folder1</span></span><br/><span data-ttu-id="34a79-367">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="34a79-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="34a79-368">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="34a79-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="34a79-369">Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados.</span><span class="sxs-lookup"><span data-stu-id="34a79-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="34a79-370">false</span><span class="sxs-lookup"><span data-stu-id="34a79-370">false</span></span> |<span data-ttu-id="34a79-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="34a79-371">flattenHierarchy</span></span> |<span data-ttu-id="34a79-372">Para uma pasta de origem Pasta1 com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-372">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="34a79-373">Pasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-373">Folder1</span></span><br/><span data-ttu-id="34a79-374">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="34a79-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="34a79-375">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="34a79-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="34a79-376">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="34a79-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="34a79-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="34a79-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="34a79-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="34a79-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="34a79-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="34a79-380">pasta de destino de saudação Pasta1 é criada com hello estrutura a seguir</span><span class="sxs-lookup"><span data-stu-id="34a79-380">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="34a79-381">Pasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-381">Folder1</span></span><br/><span data-ttu-id="34a79-382">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="34a79-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="34a79-383">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2</span><span class="sxs-lookup"><span data-stu-id="34a79-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="34a79-384">Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados.</span><span class="sxs-lookup"><span data-stu-id="34a79-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="34a79-385">false</span><span class="sxs-lookup"><span data-stu-id="34a79-385">false</span></span> |<span data-ttu-id="34a79-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="34a79-386">mergeFiles</span></span> |<span data-ttu-id="34a79-387">Para uma pasta de origem Pasta1 com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="34a79-387">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="34a79-388">Pasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-388">Folder1</span></span><br/><span data-ttu-id="34a79-389">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="34a79-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="34a79-390">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="34a79-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="34a79-391">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="34a79-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="34a79-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="34a79-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="34a79-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="34a79-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="34a79-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="34a79-395">pasta de destino de saudação Pasta1 é criada com hello estrutura a seguir</span><span class="sxs-lookup"><span data-stu-id="34a79-395">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="34a79-396">Pasta1</span><span class="sxs-lookup"><span data-stu-id="34a79-396">Folder1</span></span><br/><span data-ttu-id="34a79-397">&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos dos Arquivo1 + Arquivo2 são mesclados em um único arquivo com um nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="34a79-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="34a79-398">Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="34a79-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="34a79-399">Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados.</span><span class="sxs-lookup"><span data-stu-id="34a79-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="34a79-400">Formatos de arquivo e de compactação com suporte</span><span class="sxs-lookup"><span data-stu-id="34a79-400">Supported file and compression formats</span></span>
<span data-ttu-id="34a79-401">Para obter detalhes, consulte Olá [compactação formatos de arquivo e no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="34a79-401">For details, see hello [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a><span data-ttu-id="34a79-402">Exemplos JSON para copiar dados tooand do repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="34a79-402">JSON examples for copying data tooand from Data Lake Store</span></span>
<span data-ttu-id="34a79-403">Olá exemplos a seguir fornece as definições de JSON de exemplo.</span><span class="sxs-lookup"><span data-stu-id="34a79-403">hello following examples provide sample JSON definitions.</span></span> <span data-ttu-id="34a79-404">Você pode usar essas definições de exemplo toocreate um pipeline usando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="34a79-404">You can use these sample definitions toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="34a79-405">Olá exemplos mostram como toocopy tooand de dados do armazenamento de BLOBs do Azure e do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="34a79-405">hello examples show how toocopy data tooand from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="34a79-406">No entanto, os dados podem ser copiados _diretamente_ de qualquer um dos Olá fontes tooany de Coletores de saudação com suporte.</span><span class="sxs-lookup"><span data-stu-id="34a79-406">However, data can be copied _directly_ from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="34a79-407">Para obter mais informações, consulte seção hello "repositórios de dados com suporte e formatos" hello [mover dados usando a atividade de cópia](data-factory-data-movement-activities.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="34a79-407">For more information, see hello section "Supported data stores and formats" in hello [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a><span data-ttu-id="34a79-408">Exemplo: Copiar dados de armazenamento de BLOBs do Azure tooAzure repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="34a79-408">Example: Copy data from Azure Blob Storage tooAzure Data Lake Store</span></span>
<span data-ttu-id="34a79-409">código de exemplo Hello nesta seção mostra:</span><span class="sxs-lookup"><span data-stu-id="34a79-409">hello example code in this section shows:</span></span>

* <span data-ttu-id="34a79-410">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="34a79-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="34a79-411">Um serviço vinculado do tipo [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="34a79-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="34a79-412">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="34a79-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="34a79-413">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="34a79-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="34a79-414">Um [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="34a79-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="34a79-415">Olá exemplos mostram como série temporal dados do armazenamento de BLOBs do Azure são copiado tooData Lake repositório a cada hora.</span><span class="sxs-lookup"><span data-stu-id="34a79-415">hello examples show how time-series data from Azure Blob Storage is copied tooData Lake Store every hour.</span></span> 

<span data-ttu-id="34a79-416">**Serviço vinculado de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="34a79-416">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="34a79-417">**Serviço vinculado do Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="34a79-417">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="34a79-418">Para obter detalhes de configuração, consulte Olá [vinculado propriedades do serviço](#linked-service-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="34a79-418">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="34a79-419">**Conjunto de dados de entrada de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="34a79-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="34a79-420">Em Olá exemplo a seguir, dados são determinados por um novo blob a cada hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="34a79-420">In hello following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="34a79-421">Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="34a79-421">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="34a79-422">caminho da pasta Olá usa Olá ano, mês e parte do dia da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-422">hello folder path uses hello year, month, and day portion of hello start time.</span></span> <span data-ttu-id="34a79-423">nome do arquivo Hello usa hora Olá parte da saudação hora de início.</span><span class="sxs-lookup"><span data-stu-id="34a79-423">hello file name uses hello hour portion of hello start time.</span></span> <span data-ttu-id="34a79-424">Olá `"external": true` configuração informa o serviço de fábrica de dados de saudação tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="34a79-424">hello `"external": true` setting informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="34a79-425">**Conjunto de dados de saída do Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="34a79-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="34a79-426">Olá exemplo copia dados tooData Lake repositório a seguir.</span><span class="sxs-lookup"><span data-stu-id="34a79-426">hello following example copies data tooData Lake Store.</span></span> <span data-ttu-id="34a79-427">Novos dados são copiados tooData Lake repositório a cada hora.</span><span class="sxs-lookup"><span data-stu-id="34a79-427">New data is copied tooData Lake Store every hour.</span></span>

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


<span data-ttu-id="34a79-428">**Atividade de cópia em um pipeline com uma origem de blob e um coletor Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="34a79-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="34a79-429">Saudação de exemplo a seguir, pipeline Olá contém uma atividade de cópia que está configurada toouse Olá conjuntos de dados de entrada e saídos.</span><span class="sxs-lookup"><span data-stu-id="34a79-429">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="34a79-430">atividade de cópia de saudação é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="34a79-430">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="34a79-431">Na definição JSON de pipeline hello, Olá `source` tipo está definido muito`BlobSource`e hello `sink` tipo está definido muito`AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="34a79-431">In hello pipeline JSON definition, hello `source` type is set too`BlobSource`, and hello `sink` type is set too`AzureDataLakeStoreSink`.</span></span>

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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a><span data-ttu-id="34a79-432">Exemplo: Copiar dados do repositório Azure Data Lake tooan BLOBs do Azure</span><span class="sxs-lookup"><span data-stu-id="34a79-432">Example: Copy data from Azure Data Lake Store tooan Azure blob</span></span>
<span data-ttu-id="34a79-433">código de exemplo Hello nesta seção mostra:</span><span class="sxs-lookup"><span data-stu-id="34a79-433">hello example code in this section shows:</span></span>

* <span data-ttu-id="34a79-434">Um serviço vinculado do tipo [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="34a79-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="34a79-435">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="34a79-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="34a79-436">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="34a79-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="34a79-437">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="34a79-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="34a79-438">Um [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que usa [AzureDataLakeStoreSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="34a79-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="34a79-439">código Olá copia dados de série temporal do repositório Data Lake tooan BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="34a79-439">hello code copies time-series data from Data Lake Store tooan Azure blob every hour.</span></span> 

<span data-ttu-id="34a79-440">**Serviço vinculado do Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="34a79-440">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="34a79-441">Para obter detalhes de configuração, consulte Olá [vinculado propriedades do serviço](#linked-service-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="34a79-441">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="34a79-442">**Serviço vinculado de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="34a79-442">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="34a79-443">**Conjunto de dados de entrada do Azure Data Lake**</span><span class="sxs-lookup"><span data-stu-id="34a79-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="34a79-444">Neste exemplo, definindo `"external"` muito`true` informa o serviço de fábrica de dados de saudação tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="34a79-444">In this example, setting `"external"` too`true` informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="34a79-445">**Conjunto de dados de saída do blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="34a79-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="34a79-446">Em Olá exemplo a seguir, os dados são gravados tooa novo blob a cada hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="34a79-446">In hello following example, data is written tooa new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="34a79-447">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="34a79-447">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="34a79-448">caminho da pasta Olá usa Olá ano, mês, dia e parte de horas da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-448">hello folder path uses hello year, month, day, and hours portion of hello start time.</span></span>

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

<span data-ttu-id="34a79-449">**Uma atividade de cópia em um pipeline com uma origem do Azure Data Lake Store e um coletor de blob**</span><span class="sxs-lookup"><span data-stu-id="34a79-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="34a79-450">Saudação de exemplo a seguir, pipeline Olá contém uma atividade de cópia que está configurada toouse Olá conjuntos de dados de entrada e saídos.</span><span class="sxs-lookup"><span data-stu-id="34a79-450">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="34a79-451">atividade de cópia de saudação é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="34a79-451">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="34a79-452">Na definição JSON de pipeline hello, Olá `source` tipo está definido muito`AzureDataLakeStoreSource`e hello `sink` tipo está definido muito`BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="34a79-452">In hello pipeline JSON definition, hello `source` type is set too`AzureDataLakeStoreSource`, and hello `sink` type is set too`BlobSink`.</span></span>

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

<span data-ttu-id="34a79-453">Na definição de atividade de cópia hello, você também pode mapear colunas de toocolumns de conjunto de dados de origem Olá no conjunto de dados de coletor de saudação.</span><span class="sxs-lookup"><span data-stu-id="34a79-453">In hello copy activity definition, you can also map columns from hello source dataset toocolumns in hello sink dataset.</span></span> <span data-ttu-id="34a79-454">Para obter detalhes, confira [Mapear colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="34a79-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="34a79-455">Desempenho e ajuste</span><span class="sxs-lookup"><span data-stu-id="34a79-455">Performance and tuning</span></span>
<span data-ttu-id="34a79-456">toolearn sobre fatores de saudação que afetam o desempenho de atividade de cópia e como toooptimize, consulte Olá [atividade de cópia guia de desempenho e ajuste](data-factory-copy-activity-performance.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="34a79-456">toolearn about hello factors that affect Copy Activity performance and how toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
