---
title: "aaaManage análise Azure Data Lake usando a Interface de linha de comando do Azure | Microsoft Docs"
description: "Saiba como contas de análise Data Lake toomanage, fontes de dados, trabalhos e os usuários usando a CLI do Azure"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="bede0-103">Gerenciar a Análise Azure Data Lake usando a CLI (interface de linha de comando) do Azure</span><span class="sxs-lookup"><span data-stu-id="bede0-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="bede0-104">Saiba como contas de análise do Azure Data Lake toomanage, fontes de dados, os usuários e trabalhos usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="bede0-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure CLI.</span></span> <span data-ttu-id="bede0-105">tópicos de gerenciamento toosee usando outras ferramentas, clique em ' hello, selecione acima.</span><span class="sxs-lookup"><span data-stu-id="bede0-105">toosee management topics using other tools, click hello tab select above.</span></span>


<span data-ttu-id="bede0-106">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="bede0-106">**Prerequisites**</span></span>

<span data-ttu-id="bede0-107">Antes de começar este tutorial, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="bede0-107">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="bede0-108">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="bede0-108">**An Azure subscription**.</span></span> <span data-ttu-id="bede0-109">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bede0-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bede0-110">**CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="bede0-110">**Azure CLI**.</span></span> <span data-ttu-id="bede0-111">Consulte [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="bede0-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="bede0-112">Baixe e instale Olá **pré-lançamento** [ferramentas CLI do Azure](https://github.com/MicrosoftBigData/AzureDataLake/releases) em ordem toocomplete nesta demonstração.</span><span class="sxs-lookup"><span data-stu-id="bede0-112">Download and install hello **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order toocomplete this demo.</span></span>
* <span data-ttu-id="bede0-113">**Autenticação**usando Olá seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="bede0-113">**Authentication**, using hello following command:</span></span>
  
        azure login
    <span data-ttu-id="bede0-114">Para obter mais informações sobre autenticação usando uma conta corporativa ou escolar, consulte [conectar tooan assinatura do Azure do hello CLI do Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="bede0-114">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="bede0-115">**Modo do comutador toohello Azure Resource Manager**usando Olá seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="bede0-115">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="bede0-116">**toolist Olá repositório Data Lake e análise Data Lake comandos:**</span><span class="sxs-lookup"><span data-stu-id="bede0-116">**toolist hello Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="bede0-117">Gerenciar Contas</span><span class="sxs-lookup"><span data-stu-id="bede0-117">Manage accounts</span></span>
<span data-ttu-id="bede0-118">Antes de executar qualquer trabalho da Análise Data Lake, você deve ter uma conta da Análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bede0-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="bede0-119">Ao contrário do Azure HDInsight, você não paga por uma conta da Análise quando ela não estiver executando um trabalho.</span><span class="sxs-lookup"><span data-stu-id="bede0-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="bede0-120">Você só paga pelo tempo de saudação quando ele está executando um trabalho.</span><span class="sxs-lookup"><span data-stu-id="bede0-120">You only pay for hello time when it is running a job.</span></span>  <span data-ttu-id="bede0-121">Para saber mais, consulte [Visão geral sobre a Análise Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bede0-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="bede0-122">Criar contas</span><span class="sxs-lookup"><span data-stu-id="bede0-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="bede0-123">Atualizar contas</span><span class="sxs-lookup"><span data-stu-id="bede0-123">Update accounts</span></span>
<span data-ttu-id="bede0-124">Olá, seguinte comando atualiza propriedades de saudação de uma conta existente do Data Lake análise</span><span class="sxs-lookup"><span data-stu-id="bede0-124">hello following command updates hello properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="bede0-125">Listar contas</span><span class="sxs-lookup"><span data-stu-id="bede0-125">List accounts</span></span>
<span data-ttu-id="bede0-126">Listar contas da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="bede0-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="bede0-127">Listar contas da Análise Data Lake em um grupo de recursos específico</span><span class="sxs-lookup"><span data-stu-id="bede0-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="bede0-128">Obter detalhes de uma conta específica da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="bede0-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="bede0-129">Excluir contas da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="bede0-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="bede0-130">Gerenciar as fontes de dados da conta</span><span class="sxs-lookup"><span data-stu-id="bede0-130">Manage account data sources</span></span>
<span data-ttu-id="bede0-131">Análise data Lake atualmente suporta Olá fontes de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="bede0-131">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="bede0-132">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="bede0-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="bede0-133">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="bede0-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="bede0-134">Quando você cria uma conta de análise, você deve designar uma conta de armazenamento do armazenamento do Azure Data Lake conta toobe saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="bede0-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account toobe hello default storage account.</span></span> <span data-ttu-id="bede0-135">Olá padrão publicitário conta de armazenamento é usada toostore metadados de trabalho e o trabalho de logs de auditoria.</span><span class="sxs-lookup"><span data-stu-id="bede0-135">hello default ADL storage account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="bede0-136">Depois de criar uma conta da Análise, é possíveis adicionar outras contas do Armazenamento do Data Lake e/ou uma conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bede0-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-hello-default-adl-storage-account"></a><span data-ttu-id="bede0-137">Localizar a conta de armazenamento de publicitário saudação padrão</span><span class="sxs-lookup"><span data-stu-id="bede0-137">Find hello default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="bede0-138">valor de saudação é listado em propriedades: datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="bede0-138">hello value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="bede0-139">Adicionar outras contas de armazenamento de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="bede0-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="bede0-140">Há suporte apenas para nomes curtos do Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="bede0-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="bede0-141">Não use o FQDN, por exemplo "myblob.blob.core.windows.net".</span><span class="sxs-lookup"><span data-stu-id="bede0-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="bede0-142">Adicionar outras contas do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="bede0-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="bede0-143">[-d] é uma opção facultativa tooindicate seja Olá Data Lake conta Olá Data Lake que está sendo adicionado.</span><span class="sxs-lookup"><span data-stu-id="bede0-143">[-d] is an optional switch tooindicate whether hello Data Lake being added is hello default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="bede0-144">Atualizar a fonte de dados existente</span><span class="sxs-lookup"><span data-stu-id="bede0-144">Update existing data source</span></span>
<span data-ttu-id="bede0-145">tooset um padrão de saudação do repositório Data Lake conta toobe existente:</span><span class="sxs-lookup"><span data-stu-id="bede0-145">tooset an existing Data Lake Store account toobe hello default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="bede0-146">tooupdate uma chave de conta de armazenamento de Blob existente:</span><span class="sxs-lookup"><span data-stu-id="bede0-146">tooupdate an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="bede0-147">Listar fontes de dados:</span><span class="sxs-lookup"><span data-stu-id="bede0-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Fonte de dados de lista da Análise Data Lake  ](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="bede0-149">Excluir fontes de dados:</span><span class="sxs-lookup"><span data-stu-id="bede0-149">Delete data sources:</span></span>
<span data-ttu-id="bede0-150">toodelete uma conta do repositório Data Lake:</span><span class="sxs-lookup"><span data-stu-id="bede0-150">toodelete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="bede0-151">toodelete uma conta de armazenamento de Blob:</span><span class="sxs-lookup"><span data-stu-id="bede0-151">toodelete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="bede0-152">Gerenciar trabalhos</span><span class="sxs-lookup"><span data-stu-id="bede0-152">Manage jobs</span></span>
<span data-ttu-id="bede0-153">Você deve ter uma conta da Análise Data Lake antes de criar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="bede0-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="bede0-154">Para saber mais, consulte [Gerenciar contas da Análise Data Lake](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="bede0-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="bede0-155">Listar trabalhos</span><span class="sxs-lookup"><span data-stu-id="bede0-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Fonte de dados de lista da Análise Data Lake  ](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="bede0-157">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="bede0-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="bede0-158">Enviar trabalhos</span><span class="sxs-lookup"><span data-stu-id="bede0-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="bede0-159">prioridade de padrão de saudação de um trabalho é 1000 e grau de padrão de saudação de paralelismo de um trabalho é 1.</span><span class="sxs-lookup"><span data-stu-id="bede0-159">hello default priority of a job is 1000, and hello default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="bede0-160">Cancelar trabalhos</span><span class="sxs-lookup"><span data-stu-id="bede0-160">Cancel jobs</span></span>
<span data-ttu-id="bede0-161">Use a id do trabalho Olá lista comando toofind hello e use Cancelar toocancel Olá trabalho.</span><span class="sxs-lookup"><span data-stu-id="bede0-161">Use hello list command toofind hello job id, and then use cancel toocancel hello job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="bede0-162">Gerenciar o catálogo</span><span class="sxs-lookup"><span data-stu-id="bede0-162">Manage catalog</span></span>
<span data-ttu-id="bede0-163">Catálogo de saudação U-SQL é usada toostructure dados e código para que eles possam ser compartilhados por scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="bede0-163">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="bede0-164">Catálogo de saudação permite Olá maior desempenho possível com dados no Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bede0-164">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="bede0-165">Para saber mais, consulte [Usar o Catálogo do U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="bede0-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="bede0-166">Listar itens do catálogo</span><span class="sxs-lookup"><span data-stu-id="bede0-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="bede0-167">tipos de saudação incluem o banco de dados, esquema, assembly, fonte de dados externa, tabela, função com valor de tabela ou as estatísticas de tabela.</span><span class="sxs-lookup"><span data-stu-id="bede0-167">hello types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="bede0-168">Usar grupos ARM</span><span class="sxs-lookup"><span data-stu-id="bede0-168">Use ARM groups</span></span>
<span data-ttu-id="bede0-169">Aplicativos normalmente são compostos por vários componentes, como, por exemplo, um aplicativo Web, banco de dados, servidor de banco de dados, armazenamento e serviços de terceiros.</span><span class="sxs-lookup"><span data-stu-id="bede0-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="bede0-170">Gerenciador de recursos do Azure (ARM) permite que você toowork com recursos de saudação em seu aplicativo como um grupo, chamado tooas um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bede0-170">Azure Resource Manager (ARM) enables you toowork with hello resources in your application as a group, referred tooas an Azure Resource Group.</span></span> <span data-ttu-id="bede0-171">Você pode implantar, atualizar, monitorar ou excluir todos os recursos de saudação para seu aplicativo em uma única operação coordenado.</span><span class="sxs-lookup"><span data-stu-id="bede0-171">You can deploy, update, monitor or delete all of hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="bede0-172">Usar um modelo para a implantação e esse modelo pode ser útil para ambientes diferentes, como teste, preparação e produção.</span><span class="sxs-lookup"><span data-stu-id="bede0-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="bede0-173">Você pode esclarecer cobrança para sua organização exibindo custos acumulados de saudação para todo o grupo hello.</span><span class="sxs-lookup"><span data-stu-id="bede0-173">You can clarify billing for your organization by viewing hello rolled-up costs for hello entire group.</span></span> <span data-ttu-id="bede0-174">Para saber mais, consulte [Visão geral do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bede0-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="bede0-175">Um serviço de análise Data Lake pode incluir Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="bede0-175">A Data Lake Analytics service can include hello following components:</span></span>

* <span data-ttu-id="bede0-176">Conta da Análise Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="bede0-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="bede0-177">Conta padrão do Armazenamento do Azure Data Lake obrigatória</span><span class="sxs-lookup"><span data-stu-id="bede0-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="bede0-178">Adicionar outras contas do Armazenamento do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="bede0-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="bede0-179">Contas do Armazenamento do Azure adicionais</span><span class="sxs-lookup"><span data-stu-id="bede0-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="bede0-180">Você pode criar todos esses componentes em um toomake de grupo ARM-los toomanage mais fácil.</span><span class="sxs-lookup"><span data-stu-id="bede0-180">You can create all these components under one ARM group toomake them easier toomanage.</span></span>

![Conta e armazenamento da Análise Azure Data Lake](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="bede0-182">Uma conta da análise Data Lake e contas de armazenamento dependente de saudação devem ser colocadas em Olá mesmo data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="bede0-182">A Data Lake Analytics account and hello dependent storage accounts must be placed in hello same Azure data center.</span></span>
<span data-ttu-id="bede0-183">No entanto o grupo ARM Olá pode estar localizado em um data center diferente.</span><span class="sxs-lookup"><span data-stu-id="bede0-183">hello ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="bede0-184">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bede0-184">See also</span></span>
* [<span data-ttu-id="bede0-185">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="bede0-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="bede0-186">Introdução à Análise do Data Lake usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bede0-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="bede0-187">Gerenciar a Análise do Azure Data Lake usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bede0-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="bede0-188">Monitorar e solucionar problemas em trabalhos da Análise do Azure Data Lake usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bede0-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

