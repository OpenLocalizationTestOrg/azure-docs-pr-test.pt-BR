---
title: "Introdução ao Azure Data Lake Analytics usando a CLI do Azure 2.0 | Microsoft Docs"
description: 'Saiba como usar a interface de linha de comando do Azure 2.0 para criar uma conta do Data Lake Analytics, criar um trabalho do Data Lake Analytics usando U-SQL e enviar o trabalho. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: fe2b84aac718ff5eddd4d73b5dc2120362952c1e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="d14cb-103">Introdução ao Azure Data Lake Analytics usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d14cb-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="d14cb-104">Neste tutorial, você desenvolverá um trabalho que lê um arquivo TSV (Valores Separados por Tabulação) e irá convertê-lo em um arquivo CSV (valores separados por vírgula).</span><span class="sxs-lookup"><span data-stu-id="d14cb-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="d14cb-105">Para acompanhar o mesmo tutorial usando outras ferramentas compatíveis,use a lista suspensa na parte superior desta seção.</span><span class="sxs-lookup"><span data-stu-id="d14cb-105">To go through the same tutorial using other supported tools, use the dropdown list on the top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d14cb-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d14cb-106">Prerequisites</span></span>
<span data-ttu-id="d14cb-107">Antes de começar este tutorial, você deve ter os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d14cb-107">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="d14cb-108">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d14cb-108">**An Azure subscription**.</span></span> <span data-ttu-id="d14cb-109">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d14cb-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d14cb-110">**CLI 2.0 do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d14cb-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="d14cb-111">Consulte [Instalar e configurar a CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d14cb-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="d14cb-112">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="d14cb-112">Log in to Azure</span></span>

<span data-ttu-id="d14cb-113">Para entrar na sua assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="d14cb-113">To log in to your Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="d14cb-114">Você precisará navegar até uma URL e inserir um código de autenticação.</span><span class="sxs-lookup"><span data-stu-id="d14cb-114">You are requested to browse to a URL, and enter an authentication code.</span></span>  <span data-ttu-id="d14cb-115">E siga as instruções para inserir suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="d14cb-115">And then follow the instructions to enter your credentials.</span></span>

<span data-ttu-id="d14cb-116">Uma vez feito o logon, o comando de logon listará suas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="d14cb-116">Once you have logged in, the login command lists your subscriptions.</span></span>

<span data-ttu-id="d14cb-117">Para usar uma assinatura específica:</span><span class="sxs-lookup"><span data-stu-id="d14cb-117">To use a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="d14cb-118">Criar conta da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="d14cb-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="d14cb-119">Você precisa ter uma conta do Data Lake Analytics antes de executar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="d14cb-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="d14cb-120">Para criar uma conta do Data Lake Analytics, você deve especificar os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d14cb-120">To create a Data Lake Analytics account, you must specify the following items:</span></span>

* <span data-ttu-id="d14cb-121">**Grupo de recursos do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d14cb-121">**Azure Resource Group**.</span></span> <span data-ttu-id="d14cb-122">É necessário criar uma conta do Data Lake Analytics em um grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d14cb-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="d14cb-123">O [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) permite trabalhar com os recursos do seu aplicativo como um grupo.</span><span class="sxs-lookup"><span data-stu-id="d14cb-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to work with the resources in your application as a group.</span></span> <span data-ttu-id="d14cb-124">Você pode implantar, atualizar ou excluir todos os recursos para seu aplicativo em uma única operação coordenada.</span><span class="sxs-lookup"><span data-stu-id="d14cb-124">You can deploy, update, or delete all of the resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="d14cb-125">Para listar os grupos de recursos existentes em sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="d14cb-125">To list the existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="d14cb-126">Para criar um novo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="d14cb-126">To create a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="d14cb-127">**Nome da conta do Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d14cb-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="d14cb-128">Cada conta do Data Lake Analytics tem um nome.</span><span class="sxs-lookup"><span data-stu-id="d14cb-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="d14cb-129">**Local**.</span><span class="sxs-lookup"><span data-stu-id="d14cb-129">**Location**.</span></span> <span data-ttu-id="d14cb-130">Use um dos datacenters do Azure que dá suporte ao Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d14cb-130">Use one of the Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="d14cb-131">**Conta padrão do Data Lake Store**: cada conta do Data Lake Analytics tem uma conta padrão do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d14cb-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="d14cb-132">Para listar a conta existente do Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="d14cb-132">To list the existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="d14cb-133">Para criar uma nova conta do Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="d14cb-133">To create a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="d14cb-134">Use o seguinte código para criar uma conta do Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="d14cb-134">Use the following syntax to create a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="d14cb-135">Depois de criar uma conta, você pode usar os seguintes comandos para listar as contas e mostrar seus detalhes:</span><span class="sxs-lookup"><span data-stu-id="d14cb-135">After creating an account, you can use the following commands to list the accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-to-data-lake-store"></a><span data-ttu-id="d14cb-136">Carregar dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="d14cb-136">Upload data to Data Lake Store</span></span>
<span data-ttu-id="d14cb-137">Neste tutorial, você processa alguns logs de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d14cb-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="d14cb-138">O log de pesquisa pode ser armazenado no Repositório Data Lake ou no Armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="d14cb-138">The search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="d14cb-139">O portal do Azure fornece uma interface do usuário para copiar alguns arquivos de dados de exemplo para a conta padrão do Data Lake Store, o que inclui um arquivo de log de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d14cb-139">The Azure portal provides a user interface for copying some sample data files to the default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="d14cb-140">Consulte [Preparar dados de origem](data-lake-analytics-get-started-portal.md) para carregar os dados na conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d14cb-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) to upload the data to the default Data Lake Store account.</span></span>

<span data-ttu-id="d14cb-141">Para carregar arquivos usando a CLI 2.0, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d14cb-141">To upload files using CLI 2.0, use the following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="d14cb-142">A Análise Data Lake também pode acessar o armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="d14cb-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="d14cb-143">Para carregar dados no Armazenamento de Blob do Azure, consulte [Usando a CLI do Azure com o Armazenamento do Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d14cb-143">For uploading data to Azure Blob storage, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="d14cb-144">Enviar trabalhos da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="d14cb-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="d14cb-145">Os trabalhos da Análise Data Lake são escritos na linguagem U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d14cb-145">The Data Lake Analytics jobs are written in the U-SQL language.</span></span> <span data-ttu-id="d14cb-146">Para saber mais sobre o U-SQL, confira [Introdução à linguagem U-SQL](data-lake-analytics-u-sql-get-started.md) e [Referência da linguagem U-SQL](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="d14cb-146">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="d14cb-147">**Para criar um script de trabalho da Análise Data Lake**</span><span class="sxs-lookup"><span data-stu-id="d14cb-147">**To create a Data Lake Analytics job script**</span></span>

<span data-ttu-id="d14cb-148">Crie um arquivo de texto com o seguinte script U-SQL e salve o arquivo de texto em sua estação de trabalho:</span><span class="sxs-lookup"><span data-stu-id="d14cb-148">Create a text file with following U-SQL script, and save the text file to your workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="d14cb-149">Este script U-SQL lê o arquivo de dados de origem usando **Extractors.Tsv()**, em seguida, cria um arquivo csv usando **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="d14cb-149">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="d14cb-150">Não modifique os dois caminhos, a menos que você copie o arquivo de origem para um local diferente.</span><span class="sxs-lookup"><span data-stu-id="d14cb-150">Don't modify the two paths unless you copy the source file into a different location.</span></span>  <span data-ttu-id="d14cb-151">O Data Lake Analytics criará a pasta de saída se ela não existir.</span><span class="sxs-lookup"><span data-stu-id="d14cb-151">Data Lake Analytics creates the output folder if it doesn't exist.</span></span>

<span data-ttu-id="d14cb-152">É mais simples usar caminhos relativos para arquivos armazenados em contas padrão do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d14cb-152">It is simpler to use relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="d14cb-153">Você também pode usar caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="d14cb-153">You can also use absolute paths.</span></span>  <span data-ttu-id="d14cb-154">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d14cb-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="d14cb-155">Você deve usar caminhos absolutos para acessar os arquivos em contas do Armazenamento vinculadas.</span><span class="sxs-lookup"><span data-stu-id="d14cb-155">You must use absolute paths to access files in linked Storage accounts.</span></span>  <span data-ttu-id="d14cb-156">A sintaxe para os arquivos armazenados na conta do Armazenamento do Azure vinculada é:</span><span class="sxs-lookup"><span data-stu-id="d14cb-156">The syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="d14cb-157">Não há suporte para o contêiner de Blob do Azure com blobs públicos.</span><span class="sxs-lookup"><span data-stu-id="d14cb-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="d14cb-158">Não há suporte para o contêiner de Blob do Azure com contêineres públicos.</span><span class="sxs-lookup"><span data-stu-id="d14cb-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="d14cb-159">**Para enviar trabalhos**</span><span class="sxs-lookup"><span data-stu-id="d14cb-159">**To submit jobs**</span></span>

<span data-ttu-id="d14cb-160">Use a sintaxe a seguir para enviar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="d14cb-160">Use the following syntax to submit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="d14cb-161">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d14cb-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="d14cb-162">**Para listar trabalhos e mostrar detalhes do trabalho**</span><span class="sxs-lookup"><span data-stu-id="d14cb-162">**To list jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="d14cb-163">**Para cancelar trabalhos**</span><span class="sxs-lookup"><span data-stu-id="d14cb-163">**To cancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="d14cb-164">Recuperar os resultados do trabalho</span><span class="sxs-lookup"><span data-stu-id="d14cb-164">Retrieve job results</span></span>

<span data-ttu-id="d14cb-165">Depois que um trabalho é concluído, use os seguintes comandos para listar os arquivos de saída e baixá-los:</span><span class="sxs-lookup"><span data-stu-id="d14cb-165">After a job is completed, you can use the following commands to list the output files, and download the files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="d14cb-166">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d14cb-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="d14cb-167">Pipelines e recorrências</span><span class="sxs-lookup"><span data-stu-id="d14cb-167">Pipelines and recurrences</span></span>

<span data-ttu-id="d14cb-168">**Obter informações sobre pipelines e recorrências**</span><span class="sxs-lookup"><span data-stu-id="d14cb-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="d14cb-169">Utilize os comandos `az dla job pipeline` para consultar as informações de pipeline para trabalhos enviados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d14cb-169">Use the `az dla job pipeline` commands to see the pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="d14cb-170">Utilize os comandos `az dla job recurrence` para consultar as informações de recorrência para trabalhos enviados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d14cb-170">Use the `az dla job recurrence` commands to see the recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="d14cb-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d14cb-171">Next steps</span></span>

* <span data-ttu-id="d14cb-172">Para ver o documento de referência da CLI 2.0 do Data Lake Analytics, veja [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="d14cb-172">To see the Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="d14cb-173">Para ver o documento de referência da CLI 2.0 do Data Lake Store, veja [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="d14cb-173">To see the Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="d14cb-174">Para ver uma consulta mais complexa, consulte [Analisar logs de site usando a Análise Data Lake do Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="d14cb-174">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
