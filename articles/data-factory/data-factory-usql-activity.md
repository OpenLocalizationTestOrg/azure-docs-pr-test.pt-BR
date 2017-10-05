---
title: Transformar dados usando o script U-SQL - Azure | Microsoft Docs
description: "Saiba como processar ou transformar dados executando scripts U-SQL no serviço de computação do Azure Data Lake Analytics."
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
ms.openlocfilehash: 49a809af92ed1bc6664fbdd3bf1aabf36afb8180
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="746ef-103">Transforme dados executando scripts U-SQL no serviço de computação do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="746ef-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="746ef-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="746ef-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="746ef-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="746ef-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="746ef-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="746ef-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="746ef-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="746ef-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="746ef-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="746ef-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="746ef-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="746ef-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="746ef-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="746ef-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="746ef-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="746ef-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="746ef-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="746ef-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="746ef-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="746ef-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="746ef-114">Um pipeline em uma fábrica de dados do Azure processa dados nos serviços de armazenamento vinculados utilizando serviços de computação vinculados.</span><span class="sxs-lookup"><span data-stu-id="746ef-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="746ef-115">Ela contém uma sequência de atividades em que cada atividade executa uma operação de processamento específica.</span><span class="sxs-lookup"><span data-stu-id="746ef-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="746ef-116">Este artigo descreve a **Atividade do U-SQL do Data Lake Analytics** que executa um script **U-SQL** em um serviço vinculado de computação do **Azure Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="746ef-116">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="746ef-117">Crie uma conta do Azure Data Lake Analytics antes de criar um pipeline com uma atividade do U-SQL do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="746ef-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="746ef-118">Para saber mais sobre o Azure Data Lake Analytics, veja [Introdução ao Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="746ef-118">To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="746ef-119">Veja o tutorial [Criar seu primeiro pipeline](data-factory-build-your-first-pipeline.md) para obter etapas detalhadas de como criar um Data Factory, serviços vinculados, conjuntos de dados e um pipeline.</span><span class="sxs-lookup"><span data-stu-id="746ef-119">Review the [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps to create a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="746ef-120">Use os trechos de código JSON com o Editor do Data Factory, Visual Studio ou Azure PowerShell para criar as entidades do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="746ef-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell to create Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="746ef-121">Tipos de autenticação com suporte</span><span class="sxs-lookup"><span data-stu-id="746ef-121">Supported authentication types</span></span>
<span data-ttu-id="746ef-122">A atividade do U-SQL dá suporte aos tipos de autenticação abaixo no Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="746ef-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="746ef-123">Autenticação de entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="746ef-123">Service principal authentication</span></span>
* <span data-ttu-id="746ef-124">Autenticação de credencial do usuário (OAuth)</span><span class="sxs-lookup"><span data-stu-id="746ef-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="746ef-125">Recomendamos o uso da autenticação de entidade de serviço, especialmente para uma execução de U-SQL agendada.</span><span class="sxs-lookup"><span data-stu-id="746ef-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="746ef-126">O comportamento de expiração do token pode ocorrer com autenticação de credenciais do usuário.</span><span class="sxs-lookup"><span data-stu-id="746ef-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="746ef-127">Para obter os detalhes de configuração, consulte a seção [Propriedades do serviço vinculado](#azure-data-lake-analytics-linked-service).</span><span class="sxs-lookup"><span data-stu-id="746ef-127">For configuration details, see the [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="746ef-128">Serviço Vinculado da Análise Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="746ef-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="746ef-129">Você cria um serviço vinculado do **Azure Data Lake Analytics** para vincular um serviço de computação do Azure Data Lake Analytics a um Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="746ef-129">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="746ef-130">A atividade de U-SQL do Data Lake Analytics no pipeline se refere a esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="746ef-130">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="746ef-131">A tabela a seguir apresenta as descrições das propriedades genéricas usadas na definição JSON.</span><span class="sxs-lookup"><span data-stu-id="746ef-131">The following table provides descriptions for the generic properties used in the JSON definition.</span></span> <span data-ttu-id="746ef-132">Você ainda pode escolher entre a autenticação de credencial do usuário e entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="746ef-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="746ef-133">Propriedade</span><span class="sxs-lookup"><span data-stu-id="746ef-133">Property</span></span> | <span data-ttu-id="746ef-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="746ef-134">Description</span></span> | <span data-ttu-id="746ef-135">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="746ef-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="746ef-136">**tipo**</span><span class="sxs-lookup"><span data-stu-id="746ef-136">**type**</span></span> |<span data-ttu-id="746ef-137">A propriedade de tipo deve ser definida como: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="746ef-137">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="746ef-138">Sim</span><span class="sxs-lookup"><span data-stu-id="746ef-138">Yes</span></span> |
| <span data-ttu-id="746ef-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="746ef-139">**accountName**</span></span> |<span data-ttu-id="746ef-140">Nome da conta da Análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="746ef-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="746ef-141">Sim</span><span class="sxs-lookup"><span data-stu-id="746ef-141">Yes</span></span> |
| <span data-ttu-id="746ef-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="746ef-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="746ef-143">URI da Análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="746ef-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="746ef-144">Não</span><span class="sxs-lookup"><span data-stu-id="746ef-144">No</span></span> |
| <span data-ttu-id="746ef-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="746ef-145">**subscriptionId**</span></span> |<span data-ttu-id="746ef-146">Id de assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="746ef-146">Azure subscription id</span></span> |<span data-ttu-id="746ef-147">Não (se não for especificado, a assinatura do Data Factory é usada).</span><span class="sxs-lookup"><span data-stu-id="746ef-147">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="746ef-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="746ef-148">**resourceGroupName**</span></span> |<span data-ttu-id="746ef-149">Nome do grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="746ef-149">Azure resource group name</span></span> |<span data-ttu-id="746ef-150">Não (se não for especificado, o grupo de recursos do Data Factory é usado).</span><span class="sxs-lookup"><span data-stu-id="746ef-150">No (If not specified, resource group of the data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="746ef-151">Autenticação de entidade de serviço (recomendada)</span><span class="sxs-lookup"><span data-stu-id="746ef-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="746ef-152">Para usar a autenticação de entidade de serviço, registre uma entidade de aplicativo no Azure AD (Azure Active Directory) e conceda a ela o acesso ao Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="746ef-152">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="746ef-153">Para encontrar as etapas detalhadas, consulte [Autenticação de serviço a serviço](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="746ef-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="746ef-154">Anote os seguintes valores, que são usados para definir o serviço vinculado:</span><span class="sxs-lookup"><span data-stu-id="746ef-154">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="746ef-155">ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="746ef-155">Application ID</span></span>
* <span data-ttu-id="746ef-156">Chave do aplicativo</span><span class="sxs-lookup"><span data-stu-id="746ef-156">Application key</span></span> 
* <span data-ttu-id="746ef-157">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="746ef-157">Tenant ID</span></span>

<span data-ttu-id="746ef-158">Use a autenticação de entidade de serviço especificando as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="746ef-158">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="746ef-159">Propriedade</span><span class="sxs-lookup"><span data-stu-id="746ef-159">Property</span></span> | <span data-ttu-id="746ef-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="746ef-160">Description</span></span> | <span data-ttu-id="746ef-161">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="746ef-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="746ef-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="746ef-162">**servicePrincipalId**</span></span> | <span data-ttu-id="746ef-163">Especifique a ID do cliente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="746ef-163">Specify the application's client ID.</span></span> | <span data-ttu-id="746ef-164">Sim</span><span class="sxs-lookup"><span data-stu-id="746ef-164">Yes</span></span> |
| <span data-ttu-id="746ef-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="746ef-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="746ef-166">Especifique a chave do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="746ef-166">Specify the application's key.</span></span> | <span data-ttu-id="746ef-167">Sim</span><span class="sxs-lookup"><span data-stu-id="746ef-167">Yes</span></span> |
| <span data-ttu-id="746ef-168">**tenant**</span><span class="sxs-lookup"><span data-stu-id="746ef-168">**tenant**</span></span> | <span data-ttu-id="746ef-169">Especifique as informações de locatário (domínio nome ou ID do Locatário) em que o aplicativo reside.</span><span class="sxs-lookup"><span data-stu-id="746ef-169">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="746ef-170">É possível recuperá-las focalizando o mouse no canto superior direito do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="746ef-170">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="746ef-171">Sim</span><span class="sxs-lookup"><span data-stu-id="746ef-171">Yes</span></span> |

<span data-ttu-id="746ef-172">**Exemplo: autenticação de entidade de serviço**</span><span class="sxs-lookup"><span data-stu-id="746ef-172">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="746ef-173">Autenticação de credenciais de usuário</span><span class="sxs-lookup"><span data-stu-id="746ef-173">User credential authentication</span></span>
<span data-ttu-id="746ef-174">Como alternativa, você pode usar a autenticação de credenciais do usuário do Data Lake Analytics especificando as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="746ef-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying the following properties:</span></span>

| <span data-ttu-id="746ef-175">Propriedade</span><span class="sxs-lookup"><span data-stu-id="746ef-175">Property</span></span> | <span data-ttu-id="746ef-176">Descrição</span><span class="sxs-lookup"><span data-stu-id="746ef-176">Description</span></span> | <span data-ttu-id="746ef-177">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="746ef-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="746ef-178">**authorization**</span><span class="sxs-lookup"><span data-stu-id="746ef-178">**authorization**</span></span> | <span data-ttu-id="746ef-179">Clique no botão **Autorizar** no Editor do Data Factory e insira as suas credenciais, que atribuem a URL de autorização gerada automaticamente a essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="746ef-179">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="746ef-180">Sim</span><span class="sxs-lookup"><span data-stu-id="746ef-180">Yes</span></span> |
| <span data-ttu-id="746ef-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="746ef-181">**sessionId**</span></span> | <span data-ttu-id="746ef-182">A ID de sessão OAuth da sessão de autorização OAuth.</span><span class="sxs-lookup"><span data-stu-id="746ef-182">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="746ef-183">Cada ID da sessão é exclusiva e pode ser usada somente uma vez.</span><span class="sxs-lookup"><span data-stu-id="746ef-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="746ef-184">Essa configuração é gerada automaticamente quando você usa o Editor do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="746ef-184">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="746ef-185">Sim</span><span class="sxs-lookup"><span data-stu-id="746ef-185">Yes</span></span> |

<span data-ttu-id="746ef-186">**Exemplo: autenticação de credenciais do usuário**</span><span class="sxs-lookup"><span data-stu-id="746ef-186">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="746ef-187">Expiração do token</span><span class="sxs-lookup"><span data-stu-id="746ef-187">Token expiration</span></span>
<span data-ttu-id="746ef-188">O código de autorização gerado usando o botão **Autorizar** expira após algum tempo.</span><span class="sxs-lookup"><span data-stu-id="746ef-188">The authorization code you generated by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="746ef-189">Confira a tabela a seguir para ver os tempos de expiração para os diferentes tipos de contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="746ef-189">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="746ef-190">Talvez você veja a mensagem de erro a seguir quando o **token de autenticação expirar**: Erro de operação de credencial: invalid_grant - AADSTS70002: erro ao validar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="746ef-190">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="746ef-191">AADSTS70008: a concessão de acesso fornecida expirou ou foi revogada.</span><span class="sxs-lookup"><span data-stu-id="746ef-191">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="746ef-192">ID do Rastreamento: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID da Correlação: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Carimbo de data/hora: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="746ef-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="746ef-193">Tipo de usuário</span><span class="sxs-lookup"><span data-stu-id="746ef-193">User type</span></span> | <span data-ttu-id="746ef-194">Expira após</span><span class="sxs-lookup"><span data-stu-id="746ef-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="746ef-195">Contas de usuário NÃO gerenciadas pelo Azure Active Directory (@hotmail.com, @live.com etc.)</span><span class="sxs-lookup"><span data-stu-id="746ef-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="746ef-196">12 horas</span><span class="sxs-lookup"><span data-stu-id="746ef-196">12 hours</span></span> |
| <span data-ttu-id="746ef-197">Contas de usuários gerenciadas pelo AAD (Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="746ef-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="746ef-198">14 dias após a última execução da fatia.</span><span class="sxs-lookup"><span data-stu-id="746ef-198">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="746ef-199">90 dias, se uma fatia com base em serviços vinculados do OAuth for executada pelo menos uma vez a cada 14 dias.</span><span class="sxs-lookup"><span data-stu-id="746ef-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="746ef-200">Para evitar/resolver este erro, reautorize usando o botão **Autorizar** quando o **token expirar** e reimplante o serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="746ef-200">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="746ef-201">Você também pode gerar valores para as propriedades **sessionId** e **authorization** de modo programático usando o código da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="746ef-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="746ef-202">Veja os tópicos [Classe AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [Classe AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) e [Classe AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) para obter detalhes sobre as classes do Data Factory usadas no código.</span><span class="sxs-lookup"><span data-stu-id="746ef-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="746ef-203">Adicione uma referência a: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll para a classe WindowsFormsWebAuthenticationDialog.</span><span class="sxs-lookup"><span data-stu-id="746ef-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="746ef-204">Atividade do U-SQL da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="746ef-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="746ef-205">O seguinte trecho de código JSON define um pipeline com uma Atividade do U-SQL da Análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="746ef-205">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="746ef-206">A definição de atividade tem uma referência para o serviço vinculado da Análise Azure Data Lake criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="746ef-206">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline to compute events for en-gb locale and date less than 2012/02/19.",
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

<span data-ttu-id="746ef-207">A tabela a seguir descreve os nomes e as descrições de propriedades que são específicas a esta atividade.</span><span class="sxs-lookup"><span data-stu-id="746ef-207">The following table describes names and descriptions of properties that are specific to this activity.</span></span> 

| <span data-ttu-id="746ef-208">Propriedade</span><span class="sxs-lookup"><span data-stu-id="746ef-208">Property</span></span> | <span data-ttu-id="746ef-209">Descrição</span><span class="sxs-lookup"><span data-stu-id="746ef-209">Description</span></span> | <span data-ttu-id="746ef-210">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="746ef-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="746ef-211">Tipo</span><span class="sxs-lookup"><span data-stu-id="746ef-211">type</span></span> |<span data-ttu-id="746ef-212">A propriedade type deve ser definida como **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="746ef-212">The type property must be set to **DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="746ef-213">Sim</span><span class="sxs-lookup"><span data-stu-id="746ef-213">Yes</span></span> |
| <span data-ttu-id="746ef-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="746ef-214">scriptPath</span></span> |<span data-ttu-id="746ef-215">Caminho para a pasta que contém o script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="746ef-215">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="746ef-216">O nome do arquivo diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="746ef-216">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="746ef-217">Não (se você usar o script)</span><span class="sxs-lookup"><span data-stu-id="746ef-217">No (if you use script)</span></span> |
| <span data-ttu-id="746ef-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="746ef-218">scriptLinkedService</span></span> |<span data-ttu-id="746ef-219">Serviço vinculado que vincula o armazenamento que contém o script para a fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="746ef-219">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="746ef-220">Não (se você usar o script)</span><span class="sxs-lookup"><span data-stu-id="746ef-220">No (if you use script)</span></span> |
| <span data-ttu-id="746ef-221">script</span><span class="sxs-lookup"><span data-stu-id="746ef-221">script</span></span> |<span data-ttu-id="746ef-222">Especificar script embutido em vez de especificar scriptPath e scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="746ef-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="746ef-223">Por exemplo: `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="746ef-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="746ef-224">Não (se você usar scriptPath e scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="746ef-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="746ef-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="746ef-225">degreeOfParallelism</span></span> |<span data-ttu-id="746ef-226">O número máximo de nós usados simultaneamente para executar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="746ef-226">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="746ef-227">Não</span><span class="sxs-lookup"><span data-stu-id="746ef-227">No</span></span> |
| <span data-ttu-id="746ef-228">prioridade</span><span class="sxs-lookup"><span data-stu-id="746ef-228">priority</span></span> |<span data-ttu-id="746ef-229">Determina quais trabalhos de todos os que estão na fila devem ser selecionados para serem executados primeiro.</span><span class="sxs-lookup"><span data-stu-id="746ef-229">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="746ef-230">Quanto menor o número, maior a prioridade.</span><span class="sxs-lookup"><span data-stu-id="746ef-230">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="746ef-231">Não</span><span class="sxs-lookup"><span data-stu-id="746ef-231">No</span></span> |
| <span data-ttu-id="746ef-232">parameters</span><span class="sxs-lookup"><span data-stu-id="746ef-232">parameters</span></span> |<span data-ttu-id="746ef-233">Parâmetros do script U-SQL</span><span class="sxs-lookup"><span data-stu-id="746ef-233">Parameters for the U-SQL script</span></span> |<span data-ttu-id="746ef-234">Não</span><span class="sxs-lookup"><span data-stu-id="746ef-234">No</span></span> |
| <span data-ttu-id="746ef-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="746ef-235">runtimeVersion</span></span> | <span data-ttu-id="746ef-236">Versão de tempo de execução do mecanismo U-SQL a ser usado</span><span class="sxs-lookup"><span data-stu-id="746ef-236">Runtime version of the U-SQL engine to use</span></span> | <span data-ttu-id="746ef-237">Não</span><span class="sxs-lookup"><span data-stu-id="746ef-237">No</span></span> | 
| <span data-ttu-id="746ef-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="746ef-238">compilationMode</span></span> | <p><span data-ttu-id="746ef-239">Modo de compilação do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="746ef-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="746ef-240">Deve ser um destes valores:</span><span class="sxs-lookup"><span data-stu-id="746ef-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="746ef-241">**Semantic:** apenas realize verificações de semântica e as verificações de integridade necessárias.</span><span class="sxs-lookup"><span data-stu-id="746ef-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="746ef-242">**Full:** execute a compilação completa, incluindo verificação de sintaxe, otimização, geração de código, etc.</span><span class="sxs-lookup"><span data-stu-id="746ef-242">**Full:** Perform the full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="746ef-243">**SingleBox:** execute a compilação completa, com a configuração de TargetType como SingleBox.</span><span class="sxs-lookup"><span data-stu-id="746ef-243">**SingleBox:** Perform the full compilation, with TargetType setting to SingleBox.</span></span></li></ul><p><span data-ttu-id="746ef-244">Se você não especificar um valor para essa propriedade, o servidor determinará o modo de compilação ideal.</span><span class="sxs-lookup"><span data-stu-id="746ef-244">If you don't specify a value for this property, the server determines the optimal compilation mode.</span></span> </p>| <span data-ttu-id="746ef-245">Não</span><span class="sxs-lookup"><span data-stu-id="746ef-245">No</span></span> | 

<span data-ttu-id="746ef-246">Consulte [Definição do Script SearchLogProcessing.txt](#sample-u-sql-script) para ver a definição do script.</span><span class="sxs-lookup"><span data-stu-id="746ef-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for the script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="746ef-247">Conjuntos de dados de entrada e saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="746ef-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="746ef-248">Conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="746ef-248">Input dataset</span></span>
<span data-ttu-id="746ef-249">Neste exemplo, os dados de entrada residem em um Repositório Azure Data Lake (arquivo SearchLog.tsv na pasta datalake/input).</span><span class="sxs-lookup"><span data-stu-id="746ef-249">In this example, the input data resides in an Azure Data Lake Store (SearchLog.tsv file in the datalake/input folder).</span></span> 

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

### <a name="output-dataset"></a><span data-ttu-id="746ef-250">Conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="746ef-250">Output dataset</span></span>
<span data-ttu-id="746ef-251">Neste exemplo, os dados de saída produzidos pelo script U-SQL são armazenados em um Repositório Azure Data Lake (pasta datalake/output).</span><span class="sxs-lookup"><span data-stu-id="746ef-251">In this example, the output data produced by the U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

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

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="746ef-252">Exemplo de serviço vinculado do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="746ef-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="746ef-253">Veja a definição de exemplo de serviço vinculado do Azure Data Lake Store usado pelos conjuntos de dados de entrada/saída.</span><span class="sxs-lookup"><span data-stu-id="746ef-253">Here is the definition of the sample Azure Data Lake Store linked service used by the input/output datasets.</span></span> 

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

<span data-ttu-id="746ef-254">Consulte o artigo [Mover dados de e para o Azure Data Lake Store](data-factory-azure-datalake-connector.md) para obter descrições das propriedades de JSON.</span><span class="sxs-lookup"><span data-stu-id="746ef-254">See [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="746ef-255">Exemplo de script U-SQL</span><span class="sxs-lookup"><span data-stu-id="746ef-255">Sample U-SQL Script</span></span>

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
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="746ef-256">Os valores dos parâmetros **@in** e **@out** no script U-SQL são passados dinamicamente pelo ADF usando a seção “parameters”.</span><span class="sxs-lookup"><span data-stu-id="746ef-256">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by ADF using the ‘parameters’ section.</span></span> <span data-ttu-id="746ef-257">Veja a seção "parâmetros" na definição do pipeline.</span><span class="sxs-lookup"><span data-stu-id="746ef-257">See the ‘parameters’ section in the pipeline definition.</span></span>

<span data-ttu-id="746ef-258">Você pode especificar outras propriedades, por exemplo, degreeOfParallelism e prioridade, bem como em sua definição de pipeline para os trabalhos executados no serviço Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="746ef-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="746ef-259">Parâmetros dinâmicos</span><span class="sxs-lookup"><span data-stu-id="746ef-259">Dynamic parameters</span></span>
<span data-ttu-id="746ef-260">Na definição de pipeline de exemplo, os parâmetros in e out são atribuídos com valores embutidos em código.</span><span class="sxs-lookup"><span data-stu-id="746ef-260">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="746ef-261">É possível usar parâmetros dinâmicos em vez disso.</span><span class="sxs-lookup"><span data-stu-id="746ef-261">It is possible to use dynamic parameters instead.</span></span> <span data-ttu-id="746ef-262">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="746ef-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="746ef-263">Nesse caso, os arquivos de entrada ainda são obtidos da pasta /datalake/input e os arquivos de saída são gerados na pasta /datalake/output.</span><span class="sxs-lookup"><span data-stu-id="746ef-263">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span></span> <span data-ttu-id="746ef-264">Os nomes de arquivo são dinâmicos com base na hora de início da fatia.</span><span class="sxs-lookup"><span data-stu-id="746ef-264">The file names are dynamic based on the slice start time.</span></span>  

