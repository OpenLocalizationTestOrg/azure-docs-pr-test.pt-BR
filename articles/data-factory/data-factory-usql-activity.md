---
title: aaaTransform dados usando o script U-SQL - Azure | Microsoft Docs
description: "Saiba como o serviço de computação tooprocess ou transformar dados executando os scripts de U-SQL na análise do Azure Data Lake."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="2643b-103">Transforme dados executando scripts U-SQL no serviço de computação do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2643b-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="2643b-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="2643b-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="2643b-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="2643b-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="2643b-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="2643b-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="2643b-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="2643b-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="2643b-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="2643b-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="2643b-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2643b-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="2643b-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2643b-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="2643b-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="2643b-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="2643b-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2643b-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="2643b-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="2643b-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="2643b-114">Um pipeline em uma fábrica de dados do Azure processa dados nos serviços de armazenamento vinculados utilizando serviços de computação vinculados.</span><span class="sxs-lookup"><span data-stu-id="2643b-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="2643b-115">Ela contém uma sequência de atividades em que cada atividade executa uma operação de processamento específica.</span><span class="sxs-lookup"><span data-stu-id="2643b-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="2643b-116">Este artigo descreve Olá **atividade U-SQL do Data Lake análise** que executa um **U-SQL** script em um **análise Azure Data Lake** serviço vinculado de computação.</span><span class="sxs-lookup"><span data-stu-id="2643b-116">This article describes hello **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="2643b-117">Crie uma conta do Azure Data Lake Analytics antes de criar um pipeline com uma atividade do U-SQL do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2643b-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="2643b-118">toolearn sobre análise Azure Data Lake, consulte [Introdução à análise Azure Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2643b-118">toolearn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="2643b-119">Saudação de revisão [criar seu primeiro tutorial pipeline](data-factory-build-your-first-pipeline.md) para obter etapas detalhadas toocreate uma fábrica de dados, vinculada a um pipeline, conjuntos de dados e serviços.</span><span class="sxs-lookup"><span data-stu-id="2643b-119">Review hello [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps toocreate a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="2643b-120">Use trechos de código JSON com o Editor de fábrica de dados ou entidades de fábrica de dados toocreate Visual Studio ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2643b-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell toocreate Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="2643b-121">Tipos de autenticação com suporte</span><span class="sxs-lookup"><span data-stu-id="2643b-121">Supported authentication types</span></span>
<span data-ttu-id="2643b-122">A atividade do U-SQL dá suporte aos tipos de autenticação abaixo no Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="2643b-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="2643b-123">Autenticação de entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="2643b-123">Service principal authentication</span></span>
* <span data-ttu-id="2643b-124">Autenticação de credencial do usuário (OAuth)</span><span class="sxs-lookup"><span data-stu-id="2643b-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="2643b-125">Recomendamos o uso da autenticação de entidade de serviço, especialmente para uma execução de U-SQL agendada.</span><span class="sxs-lookup"><span data-stu-id="2643b-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="2643b-126">O comportamento de expiração do token pode ocorrer com autenticação de credenciais do usuário.</span><span class="sxs-lookup"><span data-stu-id="2643b-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="2643b-127">Para obter detalhes de configuração, consulte Olá [vinculado propriedades do serviço](#azure-data-lake-analytics-linked-service) seção.</span><span class="sxs-lookup"><span data-stu-id="2643b-127">For configuration details, see hello [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="2643b-128">Serviço Vinculado da Análise Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="2643b-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="2643b-129">Você cria um **análise Azure Data Lake** vinculado serviço toolink uma análise do Azure Data Lake computação serviço tooan data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="2643b-129">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory.</span></span> <span data-ttu-id="2643b-130">Hello atividade U-SQL do Data Lake análise no pipeline de saudação refere-se serviço toothis vinculado.</span><span class="sxs-lookup"><span data-stu-id="2643b-130">hello Data Lake Analytics U-SQL activity in hello pipeline refers toothis linked service.</span></span> 

<span data-ttu-id="2643b-131">Olá tabela a seguir fornece descrições para Olá genéricas propriedades usadas em Olá definição JSON.</span><span class="sxs-lookup"><span data-stu-id="2643b-131">hello following table provides descriptions for hello generic properties used in hello JSON definition.</span></span> <span data-ttu-id="2643b-132">Você ainda pode escolher entre a autenticação de credencial do usuário e entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="2643b-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="2643b-133">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2643b-133">Property</span></span> | <span data-ttu-id="2643b-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="2643b-134">Description</span></span> | <span data-ttu-id="2643b-135">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2643b-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2643b-136">**tipo**</span><span class="sxs-lookup"><span data-stu-id="2643b-136">**type**</span></span> |<span data-ttu-id="2643b-137">propriedade de tipo Hello deve ser definida como: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="2643b-137">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="2643b-138">Sim</span><span class="sxs-lookup"><span data-stu-id="2643b-138">Yes</span></span> |
| <span data-ttu-id="2643b-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="2643b-139">**accountName**</span></span> |<span data-ttu-id="2643b-140">Nome da conta da Análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2643b-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="2643b-141">Sim</span><span class="sxs-lookup"><span data-stu-id="2643b-141">Yes</span></span> |
| <span data-ttu-id="2643b-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="2643b-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="2643b-143">URI da Análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2643b-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="2643b-144">Não</span><span class="sxs-lookup"><span data-stu-id="2643b-144">No</span></span> |
| <span data-ttu-id="2643b-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="2643b-145">**subscriptionId**</span></span> |<span data-ttu-id="2643b-146">Id de assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="2643b-146">Azure subscription id</span></span> |<span data-ttu-id="2643b-147">Não (se não especificado, a assinatura de saudação fábrica de dados é usada).</span><span class="sxs-lookup"><span data-stu-id="2643b-147">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="2643b-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="2643b-148">**resourceGroupName**</span></span> |<span data-ttu-id="2643b-149">Nome do grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="2643b-149">Azure resource group name</span></span> |<span data-ttu-id="2643b-150">Não (se não especificado, o grupo de recursos de saudação fábrica de dados é usada).</span><span class="sxs-lookup"><span data-stu-id="2643b-150">No (If not specified, resource group of hello data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="2643b-151">Autenticação de entidade de serviço (recomendada)</span><span class="sxs-lookup"><span data-stu-id="2643b-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="2643b-152">autenticação principal do serviço toouse, registre uma entidade de aplicativo no Azure Active Directory (AD do Azure) e conceda ele Olá acessar tooData Lake repositório.</span><span class="sxs-lookup"><span data-stu-id="2643b-152">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="2643b-153">Para encontrar as etapas detalhadas, consulte [Autenticação de serviço a serviço](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="2643b-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="2643b-154">Anote Olá valores, que você usar a seguir toodefine Olá vinculado de serviço:</span><span class="sxs-lookup"><span data-stu-id="2643b-154">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="2643b-155">ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="2643b-155">Application ID</span></span>
* <span data-ttu-id="2643b-156">Chave do aplicativo</span><span class="sxs-lookup"><span data-stu-id="2643b-156">Application key</span></span> 
* <span data-ttu-id="2643b-157">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="2643b-157">Tenant ID</span></span>

<span data-ttu-id="2643b-158">Use autenticação principal do serviço especificando Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="2643b-158">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="2643b-159">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2643b-159">Property</span></span> | <span data-ttu-id="2643b-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="2643b-160">Description</span></span> | <span data-ttu-id="2643b-161">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2643b-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2643b-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="2643b-162">**servicePrincipalId**</span></span> | <span data-ttu-id="2643b-163">Especifique a ID do cliente. do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="2643b-163">Specify hello application's client ID.</span></span> | <span data-ttu-id="2643b-164">Sim</span><span class="sxs-lookup"><span data-stu-id="2643b-164">Yes</span></span> |
| <span data-ttu-id="2643b-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="2643b-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="2643b-166">Especifique a chave de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2643b-166">Specify hello application's key.</span></span> | <span data-ttu-id="2643b-167">Sim</span><span class="sxs-lookup"><span data-stu-id="2643b-167">Yes</span></span> |
| <span data-ttu-id="2643b-168">**tenant**</span><span class="sxs-lookup"><span data-stu-id="2643b-168">**tenant**</span></span> | <span data-ttu-id="2643b-169">Especifique as informações de locatário hello (ID de locatário ou de nome de domínio) em que o aplicativo reside.</span><span class="sxs-lookup"><span data-stu-id="2643b-169">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="2643b-170">Você pode recuperá-la por focalização mouse Olá no canto superior direito Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2643b-170">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="2643b-171">Sim</span><span class="sxs-lookup"><span data-stu-id="2643b-171">Yes</span></span> |

<span data-ttu-id="2643b-172">**Exemplo: autenticação de entidade de serviço**</span><span class="sxs-lookup"><span data-stu-id="2643b-172">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="2643b-173">Autenticação de credenciais de usuário</span><span class="sxs-lookup"><span data-stu-id="2643b-173">User credential authentication</span></span>
<span data-ttu-id="2643b-174">Como alternativa, você pode usar a autenticação de credenciais de usuário para análise Data Lake especificando Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="2643b-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying hello following properties:</span></span>

| <span data-ttu-id="2643b-175">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2643b-175">Property</span></span> | <span data-ttu-id="2643b-176">Descrição</span><span class="sxs-lookup"><span data-stu-id="2643b-176">Description</span></span> | <span data-ttu-id="2643b-177">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2643b-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2643b-178">**authorization**</span><span class="sxs-lookup"><span data-stu-id="2643b-178">**authorization**</span></span> | <span data-ttu-id="2643b-179">Clique em Olá **autorizar** botão no hello Editor da fábrica de dados e insira suas credenciais que atribui a propriedade toothis de URL de autorização do hello gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2643b-179">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="2643b-180">Sim</span><span class="sxs-lookup"><span data-stu-id="2643b-180">Yes</span></span> |
| <span data-ttu-id="2643b-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="2643b-181">**sessionId**</span></span> | <span data-ttu-id="2643b-182">ID de sessão do OAuth da sessão de autorização de OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="2643b-182">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="2643b-183">Cada ID da sessão é exclusiva e pode ser usada somente uma vez.</span><span class="sxs-lookup"><span data-stu-id="2643b-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="2643b-184">Essa configuração é gerada automaticamente quando você usa Olá Editor da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="2643b-184">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="2643b-185">Sim</span><span class="sxs-lookup"><span data-stu-id="2643b-185">Yes</span></span> |

<span data-ttu-id="2643b-186">**Exemplo: autenticação de credenciais do usuário**</span><span class="sxs-lookup"><span data-stu-id="2643b-186">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="2643b-187">Expiração do token</span><span class="sxs-lookup"><span data-stu-id="2643b-187">Token expiration</span></span>
<span data-ttu-id="2643b-188">Olá código de autorização gerado usando Olá **autorizar** botão expira após algum tempo.</span><span class="sxs-lookup"><span data-stu-id="2643b-188">hello authorization code you generated by using hello **Authorize** button expires after sometime.</span></span> <span data-ttu-id="2643b-189">Consulte a tabela a seguir para tempos de expiração de saudação para diferentes tipos de contas de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="2643b-189">See hello following table for hello expiration times for different types of user accounts.</span></span> <span data-ttu-id="2643b-190">Você pode ver Olá a seguinte mensagem de erro hello quando a autenticação **token expira**: erro na operação de credencial: invalid_grant - AADSTS70002: erro ao validar credenciais.</span><span class="sxs-lookup"><span data-stu-id="2643b-190">You may see hello following error message when hello authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="2643b-191">AADSTS70008: Olá fornecido a concessão de acesso expirou ou foi revogado.</span><span class="sxs-lookup"><span data-stu-id="2643b-191">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="2643b-192">ID do Rastreamento: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID da Correlação: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Carimbo de data/hora: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="2643b-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="2643b-193">Tipo de usuário</span><span class="sxs-lookup"><span data-stu-id="2643b-193">User type</span></span> | <span data-ttu-id="2643b-194">Expira após</span><span class="sxs-lookup"><span data-stu-id="2643b-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="2643b-195">Contas de usuário NÃO gerenciadas pelo Azure Active Directory (@hotmail.com, @live.com etc.)</span><span class="sxs-lookup"><span data-stu-id="2643b-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="2643b-196">12 horas</span><span class="sxs-lookup"><span data-stu-id="2643b-196">12 hours</span></span> |
| <span data-ttu-id="2643b-197">Contas de usuários gerenciadas pelo AAD (Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="2643b-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="2643b-198">Execute a 14 dias após a última fatia de saudação.</span><span class="sxs-lookup"><span data-stu-id="2643b-198">14 days after hello last slice run.</span></span> <br/><br/><span data-ttu-id="2643b-199">90 dias, se uma fatia com base em serviços vinculados do OAuth for executada pelo menos uma vez a cada 14 dias.</span><span class="sxs-lookup"><span data-stu-id="2643b-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="2643b-200">tooavoid e resolver esse erro, autorize novamente usando Olá **autorizar** botão quando hello **token expira** e reimplante o serviço vinculado de saudação.</span><span class="sxs-lookup"><span data-stu-id="2643b-200">tooavoid/resolve this error, reauthorize using hello **Authorize** button when hello **token expires** and redeploy hello linked service.</span></span> <span data-ttu-id="2643b-201">Você também pode gerar valores para as propriedades **sessionId** e **authorization** de modo programático usando o código da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="2643b-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="2643b-202">Consulte [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), e [AuthorizationSessionGetResponse classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tópicos para obter detalhes sobre classes de fábrica de dados Olá usadas no código de saudação.</span><span class="sxs-lookup"><span data-stu-id="2643b-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about hello Data Factory classes used in hello code.</span></span> <span data-ttu-id="2643b-203">Adicione uma referência a: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll para Olá WindowsFormsWebAuthenticationDialog classe.</span><span class="sxs-lookup"><span data-stu-id="2643b-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for hello WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="2643b-204">Atividade do U-SQL da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="2643b-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="2643b-205">Olá trecho JSON a seguir define um pipeline com uma atividade de U-SQL análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2643b-205">hello following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="2643b-206">definição de atividade Olá tem uma referência toohello serviço vinculado de análise do Azure Data Lake criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2643b-206">hello activity definition has a reference toohello Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="2643b-207">Olá tabela a seguir descreve os nomes e descrições das propriedades de atividade toothis específico.</span><span class="sxs-lookup"><span data-stu-id="2643b-207">hello following table describes names and descriptions of properties that are specific toothis activity.</span></span> 

| <span data-ttu-id="2643b-208">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2643b-208">Property</span></span> | <span data-ttu-id="2643b-209">Descrição</span><span class="sxs-lookup"><span data-stu-id="2643b-209">Description</span></span> | <span data-ttu-id="2643b-210">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2643b-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2643b-211">type</span><span class="sxs-lookup"><span data-stu-id="2643b-211">type</span></span> |<span data-ttu-id="2643b-212">propriedade do tipo Hello deve ser definida muito**DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="2643b-212">hello type property must be set too**DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="2643b-213">Sim</span><span class="sxs-lookup"><span data-stu-id="2643b-213">Yes</span></span> |
| <span data-ttu-id="2643b-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="2643b-214">scriptPath</span></span> |<span data-ttu-id="2643b-215">Toofolder de caminho que contém o script hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2643b-215">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="2643b-216">Nome do arquivo hello diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2643b-216">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="2643b-217">Não (se você usar o script)</span><span class="sxs-lookup"><span data-stu-id="2643b-217">No (if you use script)</span></span> |
| <span data-ttu-id="2643b-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="2643b-218">scriptLinkedService</span></span> |<span data-ttu-id="2643b-219">Serviço vinculado que vincula o armazenamento de saudação que contém a fábrica de dados Olá script toohello</span><span class="sxs-lookup"><span data-stu-id="2643b-219">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="2643b-220">Não (se você usar o script)</span><span class="sxs-lookup"><span data-stu-id="2643b-220">No (if you use script)</span></span> |
| <span data-ttu-id="2643b-221">script</span><span class="sxs-lookup"><span data-stu-id="2643b-221">script</span></span> |<span data-ttu-id="2643b-222">Especificar script embutido em vez de especificar scriptPath e scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="2643b-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="2643b-223">Por exemplo: `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="2643b-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="2643b-224">Não (se você usar scriptPath e scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="2643b-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="2643b-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="2643b-225">degreeOfParallelism</span></span> |<span data-ttu-id="2643b-226">número máximo de saudação de nós usados simultaneamente toorun trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="2643b-226">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="2643b-227">Não</span><span class="sxs-lookup"><span data-stu-id="2643b-227">No</span></span> |
| <span data-ttu-id="2643b-228">prioridade</span><span class="sxs-lookup"><span data-stu-id="2643b-228">priority</span></span> |<span data-ttu-id="2643b-229">Determina quais trabalhos entre todos os que estão na fila devem ser selecionada toorun primeiro.</span><span class="sxs-lookup"><span data-stu-id="2643b-229">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="2643b-230">Olá Olá número menor, Olá Olá prioridade.</span><span class="sxs-lookup"><span data-stu-id="2643b-230">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="2643b-231">Não</span><span class="sxs-lookup"><span data-stu-id="2643b-231">No</span></span> |
| <span data-ttu-id="2643b-232">parâmetros</span><span class="sxs-lookup"><span data-stu-id="2643b-232">parameters</span></span> |<span data-ttu-id="2643b-233">Parâmetros de script hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="2643b-233">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="2643b-234">Não</span><span class="sxs-lookup"><span data-stu-id="2643b-234">No</span></span> |
| <span data-ttu-id="2643b-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="2643b-235">runtimeVersion</span></span> | <span data-ttu-id="2643b-236">Versão de tempo de execução do toouse do mecanismo de saudação U-SQL</span><span class="sxs-lookup"><span data-stu-id="2643b-236">Runtime version of hello U-SQL engine toouse</span></span> | <span data-ttu-id="2643b-237">Não</span><span class="sxs-lookup"><span data-stu-id="2643b-237">No</span></span> | 
| <span data-ttu-id="2643b-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="2643b-238">compilationMode</span></span> | <p><span data-ttu-id="2643b-239">Modo de compilação do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2643b-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="2643b-240">Deve ser um destes valores:</span><span class="sxs-lookup"><span data-stu-id="2643b-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="2643b-241">**Semantic:** apenas realize verificações de semântica e as verificações de integridade necessárias.</span><span class="sxs-lookup"><span data-stu-id="2643b-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="2643b-242">**Completo:** executar Olá de compilação completo, incluindo verificação de sintaxe, otimização, geração de código, etc.</span><span class="sxs-lookup"><span data-stu-id="2643b-242">**Full:** Perform hello full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="2643b-243">**SingleBox:** executar compilação completa hello, com tooSingleBox de configuração de TargetType.</span><span class="sxs-lookup"><span data-stu-id="2643b-243">**SingleBox:** Perform hello full compilation, with TargetType setting tooSingleBox.</span></span></li></ul><p><span data-ttu-id="2643b-244">Se você não especificar um valor para essa propriedade, o servidor de saudação determina o modo de compilação ideal de saudação.</span><span class="sxs-lookup"><span data-stu-id="2643b-244">If you don't specify a value for this property, hello server determines hello optimal compilation mode.</span></span> </p>| <span data-ttu-id="2643b-245">Não</span><span class="sxs-lookup"><span data-stu-id="2643b-245">No</span></span> | 

<span data-ttu-id="2643b-246">Consulte [SearchLogProcessing.txt Script definição](#sample-u-sql-script) para definição de saudação do script.</span><span class="sxs-lookup"><span data-stu-id="2643b-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for hello script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="2643b-247">Conjuntos de dados de entrada e saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="2643b-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="2643b-248">Conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="2643b-248">Input dataset</span></span>
<span data-ttu-id="2643b-249">Neste exemplo, os dados de entrada hello residem em um repositório Azure Data Lake (SearchLog.tsv arquivo na pasta de datalake/entrada hello).</span><span class="sxs-lookup"><span data-stu-id="2643b-249">In this example, hello input data resides in an Azure Data Lake Store (SearchLog.tsv file in hello datalake/input folder).</span></span> 

```json
{
    "name": "DataLakeTable",
    "properties": {
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
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a><span data-ttu-id="2643b-250">Conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="2643b-250">Output dataset</span></span>
<span data-ttu-id="2643b-251">Neste exemplo, os dados de saída de hello produzidos pelo Olá script U-SQL são armazenados em um repositório Azure Data Lake (pasta datalake/saída).</span><span class="sxs-lookup"><span data-stu-id="2643b-251">In this example, hello output data produced by hello U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="2643b-252">Exemplo de serviço vinculado do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2643b-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="2643b-253">Esta é a definição de saudação do exemplo hello que repositório Azure Data Lake vinculado usado por conjuntos de dados de entrada/saída de saudação do serviço.</span><span class="sxs-lookup"><span data-stu-id="2643b-253">Here is hello definition of hello sample Azure Data Lake Store linked service used by hello input/output datasets.</span></span> 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

<span data-ttu-id="2643b-254">Consulte [mover tooand de dados do repositório Azure Data Lake](data-factory-azure-datalake-connector.md) artigo para obter descrições das propriedades JSON.</span><span class="sxs-lookup"><span data-stu-id="2643b-254">See [Move data tooand from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="2643b-255">Exemplo de script U-SQL</span><span class="sxs-lookup"><span data-stu-id="2643b-255">Sample U-SQL Script</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="2643b-256">Olá valores para  **@in**  e  **@out**  parâmetros no script hello U-SQL são transmitidos dinamicamente por ADF usando Olá 'parameters' seção.</span><span class="sxs-lookup"><span data-stu-id="2643b-256">hello values for **@in** and **@out** parameters in hello U-SQL script are passed dynamically by ADF using hello ‘parameters’ section.</span></span> <span data-ttu-id="2643b-257">Consulte a seção de 'parameters' de saudação na definição do pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="2643b-257">See hello ‘parameters’ section in hello pipeline definition.</span></span>

<span data-ttu-id="2643b-258">Você pode especificar outras propriedades, como prioridade e degreeOfParallelism também em sua definição de pipeline para trabalhos de saudação que são executados em Olá serviço de análise do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2643b-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for hello jobs that run on hello Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="2643b-259">Parâmetros dinâmicos</span><span class="sxs-lookup"><span data-stu-id="2643b-259">Dynamic parameters</span></span>
<span data-ttu-id="2643b-260">Na definição de pipeline de exemplo hello, e parâmetros são atribuídos com valores codificados.</span><span class="sxs-lookup"><span data-stu-id="2643b-260">In hello sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="2643b-261">Em vez disso, é parâmetros dinâmicos toouse possíveis.</span><span class="sxs-lookup"><span data-stu-id="2643b-261">It is possible toouse dynamic parameters instead.</span></span> <span data-ttu-id="2643b-262">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2643b-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="2643b-263">Nesse caso, arquivos de entrada ainda são retirados da pasta de /datalake/input hello e arquivos de saída são gerados na pasta de /datalake/output hello.</span><span class="sxs-lookup"><span data-stu-id="2643b-263">In this case, input files are still picked up from hello /datalake/input folder and output files are generated in hello /datalake/output folder.</span></span> <span data-ttu-id="2643b-264">nomes de arquivo Hello são dinâmicos com base na hora de início de fatia hello.</span><span class="sxs-lookup"><span data-stu-id="2643b-264">hello file names are dynamic based on hello slice start time.</span></span>  

