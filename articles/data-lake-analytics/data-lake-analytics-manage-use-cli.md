---
title: Gerenciar o Azure Data Lake Analytics usando a Interface de Linha de Comando do Azure | Microsoft Docs
description: "Saiba como gerenciar contas, fontes de dados, trabalhos e os usuários da Análise Data Lake  usando a CLI do Azure"
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
ms.openlocfilehash: f90bada3572c0ed40b07d76ec02c1b499bbd1428
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="d8168-103">Gerenciar a Análise Azure Data Lake usando a CLI (interface de linha de comando) do Azure</span><span class="sxs-lookup"><span data-stu-id="d8168-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="d8168-104">Saiba como gerenciar contas, fontes de dados, usuários e trabalhos do Azure Data Lake Analytics usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8168-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure CLI.</span></span> <span data-ttu-id="d8168-105">Para ver os tópicos de gerenciamento usando outras ferramentas, clique na guia Selecionar acima.</span><span class="sxs-lookup"><span data-stu-id="d8168-105">To see management topics using other tools, click the tab select above.</span></span>


<span data-ttu-id="d8168-106">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="d8168-106">**Prerequisites**</span></span>

<span data-ttu-id="d8168-107">Antes de começar este tutorial, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d8168-107">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="d8168-108">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d8168-108">**An Azure subscription**.</span></span> <span data-ttu-id="d8168-109">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8168-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d8168-110">**CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d8168-110">**Azure CLI**.</span></span> <span data-ttu-id="d8168-111">Consulte [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d8168-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="d8168-112">Baixe e instale o **pré-lançamento das** [ferramentas de CLI do Azure](https://github.com/MicrosoftBigData/AzureDataLake/releases) para concluir esta demonstração.</span><span class="sxs-lookup"><span data-stu-id="d8168-112">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span></span>
* <span data-ttu-id="d8168-113">**Autenticação**, usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d8168-113">**Authentication**, using the following command:</span></span>
  
        azure login
    <span data-ttu-id="d8168-114">Para obter mais informações sobre a autenticação usando uma conta de trabalho ou escolar, veja [Conectar-se a uma assinatura do Azure da CLI do Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d8168-114">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="d8168-115">**Alterne para o modo Gerenciador de Recursos do Azure**usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d8168-115">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="d8168-116">**Para listar os comandos do Repositório Data Lake e da Análise Data Lake:**</span><span class="sxs-lookup"><span data-stu-id="d8168-116">**To list the Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="d8168-117">Gerenciar contas</span><span class="sxs-lookup"><span data-stu-id="d8168-117">Manage accounts</span></span>
<span data-ttu-id="d8168-118">Antes de executar qualquer trabalho da Análise Data Lake, você deve ter uma conta da Análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d8168-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="d8168-119">Ao contrário do Azure HDInsight, você não paga por uma conta da Análise quando ela não estiver executando um trabalho.</span><span class="sxs-lookup"><span data-stu-id="d8168-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="d8168-120">Você paga apenas pelo tempo em que um trabalho é executado.</span><span class="sxs-lookup"><span data-stu-id="d8168-120">You only pay for the time when it is running a job.</span></span>  <span data-ttu-id="d8168-121">Para saber mais, consulte [Visão geral sobre a Análise Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8168-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="d8168-122">Criar contas</span><span class="sxs-lookup"><span data-stu-id="d8168-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="d8168-123">Atualizar contas</span><span class="sxs-lookup"><span data-stu-id="d8168-123">Update accounts</span></span>
<span data-ttu-id="d8168-124">O comando a seguir atualiza as propriedades de uma conta existente da Análise Data Lake </span><span class="sxs-lookup"><span data-stu-id="d8168-124">The following command updates the properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="d8168-125">Listar contas</span><span class="sxs-lookup"><span data-stu-id="d8168-125">List accounts</span></span>
<span data-ttu-id="d8168-126">Listar contas da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="d8168-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="d8168-127">Listar contas da Análise Data Lake em um grupo de recursos específico</span><span class="sxs-lookup"><span data-stu-id="d8168-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="d8168-128">Obter detalhes de uma conta específica da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="d8168-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="d8168-129">Excluir contas da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="d8168-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="d8168-130">Gerenciar as fontes de dados da conta</span><span class="sxs-lookup"><span data-stu-id="d8168-130">Manage account data sources</span></span>
<span data-ttu-id="d8168-131">No momento, a Análise Data Lake dá suporte às seguintes fontes de dados:</span><span class="sxs-lookup"><span data-stu-id="d8168-131">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="d8168-132">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d8168-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="d8168-133">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d8168-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="d8168-134">Quando você cria uma conta da Análise, é necessário designar uma conta do Armazenamento do Azure Data Lake como a conta de armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="d8168-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span></span> <span data-ttu-id="d8168-135">A conta de armazenamento do ADL padrão é usada para armazenar os logs de auditoria de trabalho e os metadados de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d8168-135">The default ADL storage account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="d8168-136">Depois de criar uma conta da Análise, é possíveis adicionar outras contas do Armazenamento do Data Lake e/ou uma conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8168-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-the-default-adl-storage-account"></a><span data-ttu-id="d8168-137">Localize a conta de armazenamento padrão do ADL</span><span class="sxs-lookup"><span data-stu-id="d8168-137">Find the default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="d8168-138">O valor é listado em properties:datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="d8168-138">The value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="d8168-139">Adicionar outras contas de armazenamento de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="d8168-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="d8168-140">Há suporte apenas para nomes curtos do Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="d8168-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="d8168-141">Não use o FQDN, por exemplo "myblob.blob.core.windows.net".</span><span class="sxs-lookup"><span data-stu-id="d8168-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="d8168-142">Adicionar outras contas do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="d8168-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="d8168-143">[-d] é uma opção para indicar se o Data Lake que está sendo adicionado é a conta padrão do Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d8168-143">[-d] is an optional switch to indicate whether the Data Lake being added is the default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="d8168-144">Atualizar a fonte de dados existente</span><span class="sxs-lookup"><span data-stu-id="d8168-144">Update existing data source</span></span>
<span data-ttu-id="d8168-145">Para definir uma conta existente do Repositório do Data Lake padrão:</span><span class="sxs-lookup"><span data-stu-id="d8168-145">To set an existing Data Lake Store account to be the default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="d8168-146">Para atualizar uma chave de conta do Armazenamento de Blobs existente:</span><span class="sxs-lookup"><span data-stu-id="d8168-146">To update an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="d8168-147">Listar fontes de dados:</span><span class="sxs-lookup"><span data-stu-id="d8168-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Fonte de dados de lista da Análise Data Lake  ](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="d8168-149">Excluir fontes de dados:</span><span class="sxs-lookup"><span data-stu-id="d8168-149">Delete data sources:</span></span>
<span data-ttu-id="d8168-150">Para excluir uma conta do Repositório do Data Lake:</span><span class="sxs-lookup"><span data-stu-id="d8168-150">To delete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="d8168-151">Para excluir uma conta do Armazenamento de Blobs:</span><span class="sxs-lookup"><span data-stu-id="d8168-151">To delete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="d8168-152">Gerenciar trabalhos</span><span class="sxs-lookup"><span data-stu-id="d8168-152">Manage jobs</span></span>
<span data-ttu-id="d8168-153">Você deve ter uma conta da Análise Data Lake antes de criar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="d8168-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="d8168-154">Para saber mais, consulte [Gerenciar contas da Análise Data Lake](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="d8168-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="d8168-155">Listar trabalhos</span><span class="sxs-lookup"><span data-stu-id="d8168-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Fonte de dados de lista da Análise Data Lake  ](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="d8168-157">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="d8168-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="d8168-158">Enviar trabalhos</span><span class="sxs-lookup"><span data-stu-id="d8168-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="d8168-159">A prioridade padrão de um trabalho é de 1.000 e o nível padrão de paralelismo de um trabalho é 1.</span><span class="sxs-lookup"><span data-stu-id="d8168-159">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="d8168-160">Cancelar trabalhos</span><span class="sxs-lookup"><span data-stu-id="d8168-160">Cancel jobs</span></span>
<span data-ttu-id="d8168-161">Use o comando “list” para localizar o ID do trabalho e use “cancel” para cancelar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="d8168-161">Use the list command to find the job id, and then use cancel to cancel the job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="d8168-162">Gerenciar o catálogo</span><span class="sxs-lookup"><span data-stu-id="d8168-162">Manage catalog</span></span>
<span data-ttu-id="d8168-163">O catálogo do U-SQL é usado para estruturar dados e código para que eles possam ser compartilhados por scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d8168-163">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="d8168-164">O catálogo possibilita o melhor desempenho possível com dados no Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d8168-164">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="d8168-165">Para saber mais, consulte [Usar o Catálogo do U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="d8168-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="d8168-166">Listar itens do catálogo</span><span class="sxs-lookup"><span data-stu-id="d8168-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="d8168-167">Os tipos incluem database, schema, assembly, external data source, table, table valued function ou table statistics.</span><span class="sxs-lookup"><span data-stu-id="d8168-167">The types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="d8168-168">Usar grupos ARM</span><span class="sxs-lookup"><span data-stu-id="d8168-168">Use ARM groups</span></span>
<span data-ttu-id="d8168-169">Aplicativos normalmente são compostos por vários componentes, como, por exemplo, um aplicativo Web, banco de dados, servidor de banco de dados, armazenamento e serviços de terceiros.</span><span class="sxs-lookup"><span data-stu-id="d8168-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="d8168-170">O Gerenciador de Recursos do Azure (ARM) permite trabalhar com os recursos do seu aplicativo como um grupo, designado um Grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8168-170">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span></span> <span data-ttu-id="d8168-171">Você pode implantar, atualizar, monitorar ou excluir todos os recursos do seu aplicativo com uma única operação coordenada.</span><span class="sxs-lookup"><span data-stu-id="d8168-171">You can deploy, update, monitor or delete all of the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="d8168-172">Usar um modelo para a implantação e esse modelo pode ser útil para ambientes diferentes, como teste, preparação e produção.</span><span class="sxs-lookup"><span data-stu-id="d8168-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="d8168-173">Você pode esclarecer a cobrança para sua organização exibindo os custos acumulados para todo o grupo.</span><span class="sxs-lookup"><span data-stu-id="d8168-173">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span></span> <span data-ttu-id="d8168-174">Para saber mais, consulte [Visão geral do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8168-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="d8168-175">Um serviço de Análise Data Lake pode incluir os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="d8168-175">A Data Lake Analytics service can include the following components:</span></span>

* <span data-ttu-id="d8168-176">Conta da Análise Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d8168-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="d8168-177">Conta padrão do Armazenamento do Azure Data Lake obrigatória</span><span class="sxs-lookup"><span data-stu-id="d8168-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="d8168-178">Adicionar outras contas do Armazenamento do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d8168-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="d8168-179">Contas do Armazenamento do Azure adicionais</span><span class="sxs-lookup"><span data-stu-id="d8168-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="d8168-180">Você pode criar todos esses componentes em um grupo ARM para torná-los mais fáceis de serem gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d8168-180">You can create all these components under one ARM group to make them easier to manage.</span></span>

![Conta e armazenamento da Análise Azure Data Lake](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="d8168-182">Uma conta da Análise Data Lake e as contas de armazenamento dependentes devem ser colocadas no mesmo data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8168-182">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span></span>
<span data-ttu-id="d8168-183">No entanto, o grupo ARM pode estar localizado em um data center diferente.</span><span class="sxs-lookup"><span data-stu-id="d8168-183">The ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="d8168-184">Confira também</span><span class="sxs-lookup"><span data-stu-id="d8168-184">See also</span></span>
* [<span data-ttu-id="d8168-185">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d8168-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="d8168-186">Introdução à Análise do Data Lake usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d8168-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d8168-187">Gerenciar a Análise do Azure Data Lake usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d8168-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="d8168-188">Monitorar e solucionar problemas em trabalhos da Análise do Azure Data Lake usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d8168-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

