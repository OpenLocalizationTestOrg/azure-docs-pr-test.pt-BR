---
title: "aaaGet iniciado com análise Azure Data Lake usando 2.0 do CLI do Azure | Microsoft Docs"
description: "Saiba como toouse Olá 2.0 de Interface de linha de comando do Azure toocreate uma conta da análise Data Lake, criar um trabalho de análise Data Lake usando U-SQL e enviar o trabalho de saudação. "
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
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="f6e69-103">Introdução ao Azure Data Lake Analytics usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f6e69-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="f6e69-104">Neste tutorial, você desenvolverá um trabalho que lê um arquivo TSV (Valores Separados por Tabulação) e irá convertê-lo em um arquivo CSV (valores separados por vírgula).</span><span class="sxs-lookup"><span data-stu-id="f6e69-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="f6e69-105">ferramentas de toogo por meio de saudação mesmo tutorial usando outros com suporte, use Olá suspensa lista na parte superior da saudação desta seção.</span><span class="sxs-lookup"><span data-stu-id="f6e69-105">toogo through hello same tutorial using other supported tools, use hello dropdown list on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6e69-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f6e69-106">Prerequisites</span></span>
<span data-ttu-id="f6e69-107">Antes de começar este tutorial, você deve ter Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6e69-107">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="f6e69-108">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f6e69-108">**An Azure subscription**.</span></span> <span data-ttu-id="f6e69-109">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6e69-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f6e69-110">**CLI 2.0 do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f6e69-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="f6e69-111">Consulte [Instalar e configurar a CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f6e69-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="f6e69-112">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="f6e69-112">Log in tooAzure</span></span>

<span data-ttu-id="f6e69-113">toolog em tooyour assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="f6e69-113">toolog in tooyour Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="f6e69-114">Você é solicitado toobrowse tooa URL e insira um código de autenticação.</span><span class="sxs-lookup"><span data-stu-id="f6e69-114">You are requested toobrowse tooa URL, and enter an authentication code.</span></span>  <span data-ttu-id="f6e69-115">E, em seguida, siga Olá instruções tooenter suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="f6e69-115">And then follow hello instructions tooenter your credentials.</span></span>

<span data-ttu-id="f6e69-116">Depois de fazer logon, o comando de logon de saudação lista suas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="f6e69-116">Once you have logged in, hello login command lists your subscriptions.</span></span>

<span data-ttu-id="f6e69-117">toouse uma assinatura específica:</span><span class="sxs-lookup"><span data-stu-id="f6e69-117">toouse a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="f6e69-118">Criar conta da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="f6e69-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="f6e69-119">Você precisa ter uma conta do Data Lake Analytics antes de executar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="f6e69-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="f6e69-120">toocreate uma conta da análise Data Lake, você deve especificar Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6e69-120">toocreate a Data Lake Analytics account, you must specify hello following items:</span></span>

* <span data-ttu-id="f6e69-121">**Grupo de recursos do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f6e69-121">**Azure Resource Group**.</span></span> <span data-ttu-id="f6e69-122">É necessário criar uma conta do Data Lake Analytics em um grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e69-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="f6e69-123">[Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md) permite que você toowork com recursos de saudação em seu aplicativo como um grupo.</span><span class="sxs-lookup"><span data-stu-id="f6e69-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you toowork with hello resources in your application as a group.</span></span> <span data-ttu-id="f6e69-124">Você pode implantar, atualizar ou excluir todos os recursos de saudação para seu aplicativo em uma única operação coordenado.</span><span class="sxs-lookup"><span data-stu-id="f6e69-124">You can deploy, update, or delete all of hello resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="f6e69-125">toolist Olá grupos de recursos existentes em sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="f6e69-125">toolist hello existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="f6e69-126">toocreate um novo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="f6e69-126">toocreate a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="f6e69-127">**Nome da conta do Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="f6e69-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="f6e69-128">Cada conta do Data Lake Analytics tem um nome.</span><span class="sxs-lookup"><span data-stu-id="f6e69-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="f6e69-129">**Local**.</span><span class="sxs-lookup"><span data-stu-id="f6e69-129">**Location**.</span></span> <span data-ttu-id="f6e69-130">Use um dos Olá data centers do Azure que dá suporte à análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f6e69-130">Use one of hello Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="f6e69-131">**Conta padrão do Data Lake Store**: cada conta do Data Lake Analytics tem uma conta padrão do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f6e69-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="f6e69-132">conta de repositório Data Lake existente Olá de toolist:</span><span class="sxs-lookup"><span data-stu-id="f6e69-132">toolist hello existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="f6e69-133">toocreate uma nova conta do repositório Data Lake:</span><span class="sxs-lookup"><span data-stu-id="f6e69-133">toocreate a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="f6e69-134">Use Olá sintaxe toocreate uma conta da análise Data Lake a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6e69-134">Use hello following syntax toocreate a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="f6e69-135">Depois de criar uma conta, você pode usar o hello contas de saudação toolist comandos a seguir e mostrar os detalhes da conta:</span><span class="sxs-lookup"><span data-stu-id="f6e69-135">After creating an account, you can use hello following commands toolist hello accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a><span data-ttu-id="f6e69-136">Carregar dados tooData Lake repositório</span><span class="sxs-lookup"><span data-stu-id="f6e69-136">Upload data tooData Lake Store</span></span>
<span data-ttu-id="f6e69-137">Neste tutorial, você processa alguns logs de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f6e69-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="f6e69-138">log de saudação de pesquisa pode ser armazenado no repositório Data Lake ou armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e69-138">hello search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="f6e69-139">Olá portal do Azure fornece uma interface de usuário para copiar alguns exemplo dados arquivos toohello repositório Data Lake conta padrão, que incluem um arquivo de log de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f6e69-139">hello Azure portal provides a user interface for copying some sample data files toohello default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="f6e69-140">Consulte [preparar os dados de origem](data-lake-analytics-get-started-portal.md) conta de repositório Data Lake tooupload Olá dados toohello padrão.</span><span class="sxs-lookup"><span data-stu-id="f6e69-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) tooupload hello data toohello default Data Lake Store account.</span></span>

<span data-ttu-id="f6e69-141">arquivos de tooupload usando 2.0 do CLI, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6e69-141">tooupload files using CLI 2.0, use hello following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="f6e69-142">A Análise Data Lake também pode acessar o armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e69-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="f6e69-143">Para carregar o armazenamento de Blob de tooAzure de dados, consulte [hello usando a CLI do Azure com o armazenamento do Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f6e69-143">For uploading data tooAzure Blob storage, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="f6e69-144">Enviar trabalhos da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="f6e69-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="f6e69-145">trabalhos de análise Data Lake Olá são escritos em Olá linguagem U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f6e69-145">hello Data Lake Analytics jobs are written in hello U-SQL language.</span></span> <span data-ttu-id="f6e69-146">toolearn mais sobre U-SQL, consulte [Introdução à linguagem U-SQL](data-lake-analytics-u-sql-get-started.md) e [U-SQL idioma eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="f6e69-146">toolearn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="f6e69-147">**toocreate um script de trabalho de análise Data Lake**</span><span class="sxs-lookup"><span data-stu-id="f6e69-147">**toocreate a Data Lake Analytics job script**</span></span>

<span data-ttu-id="f6e69-148">Criar um arquivo de texto com o script U-SQL a seguir e salve a estação de trabalho tooyour arquivo de texto de saudação:</span><span class="sxs-lookup"><span data-stu-id="f6e69-148">Create a text file with following U-SQL script, and save hello text file tooyour workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="f6e69-149">Este script U-SQL lê o arquivo de dados de origem de hello usando **Extractors.Tsv()**e, em seguida, cria um arquivo csv usando **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="f6e69-149">This U-SQL script reads hello source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="f6e69-150">Não modifique dois caminhos de saudação, a menos que você copia o arquivo de origem de saudação em um local diferente.</span><span class="sxs-lookup"><span data-stu-id="f6e69-150">Don't modify hello two paths unless you copy hello source file into a different location.</span></span>  <span data-ttu-id="f6e69-151">Análise data Lake cria a pasta de saída de hello se ele não existir.</span><span class="sxs-lookup"><span data-stu-id="f6e69-151">Data Lake Analytics creates hello output folder if it doesn't exist.</span></span>

<span data-ttu-id="f6e69-152">É mais simples toouse os caminhos relativos para os arquivos armazenados em contas do repositório Data Lake padrão.</span><span class="sxs-lookup"><span data-stu-id="f6e69-152">It is simpler toouse relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="f6e69-153">Você também pode usar caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="f6e69-153">You can also use absolute paths.</span></span>  <span data-ttu-id="f6e69-154">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f6e69-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="f6e69-155">Você deve usar arquivos de tooaccess caminhos absolutos em contas de armazenamento vinculadas.</span><span class="sxs-lookup"><span data-stu-id="f6e69-155">You must use absolute paths tooaccess files in linked Storage accounts.</span></span>  <span data-ttu-id="f6e69-156">sintaxe de saudação para arquivos armazenados na conta de armazenamento do Azure vinculada é:</span><span class="sxs-lookup"><span data-stu-id="f6e69-156">hello syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="f6e69-157">Não há suporte para o contêiner de Blob do Azure com blobs públicos.</span><span class="sxs-lookup"><span data-stu-id="f6e69-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="f6e69-158">Não há suporte para o contêiner de Blob do Azure com contêineres públicos.</span><span class="sxs-lookup"><span data-stu-id="f6e69-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="f6e69-159">**trabalhos de toosubmit**</span><span class="sxs-lookup"><span data-stu-id="f6e69-159">**toosubmit jobs**</span></span>

<span data-ttu-id="f6e69-160">Use Olá sintaxe toosubmit um trabalho a seguir.</span><span class="sxs-lookup"><span data-stu-id="f6e69-160">Use hello following syntax toosubmit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="f6e69-161">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f6e69-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="f6e69-162">**trabalhos de toolist e mostrar detalhes do trabalho**</span><span class="sxs-lookup"><span data-stu-id="f6e69-162">**toolist jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="f6e69-163">**trabalhos de toocancel**</span><span class="sxs-lookup"><span data-stu-id="f6e69-163">**toocancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="f6e69-164">Recuperar os resultados do trabalho</span><span class="sxs-lookup"><span data-stu-id="f6e69-164">Retrieve job results</span></span>

<span data-ttu-id="f6e69-165">Depois que um trabalho é concluído, você pode usar Olá Olá comandos toolist nos arquivos de saída a seguir e baixar arquivos de saudação:</span><span class="sxs-lookup"><span data-stu-id="f6e69-165">After a job is completed, you can use hello following commands toolist hello output files, and download hello files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="f6e69-166">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f6e69-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="f6e69-167">Pipelines e recorrências</span><span class="sxs-lookup"><span data-stu-id="f6e69-167">Pipelines and recurrences</span></span>

<span data-ttu-id="f6e69-168">**Obter informações sobre pipelines e recorrências**</span><span class="sxs-lookup"><span data-stu-id="f6e69-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="f6e69-169">Saudação de uso `az dla job pipeline` comandos informações de pipeline Olá toosee trabalhos enviados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f6e69-169">Use hello `az dla job pipeline` commands toosee hello pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="f6e69-170">Saudação de uso `az dla job recurrence` comandos toosee as informações de recorrência Olá para trabalhos enviados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f6e69-170">Use hello `az dla job recurrence` commands toosee hello recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="f6e69-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f6e69-171">Next steps</span></span>

* <span data-ttu-id="f6e69-172">Olá toosee documento de referência do Data Lake análise CLI 2.0, consulte [análise Data Lake](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="f6e69-172">toosee hello Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="f6e69-173">Olá toosee documento de referência da CLI de repositório Data Lake 2.0, consulte [repositório Data Lake](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="f6e69-173">toosee hello Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="f6e69-174">toosee uma consulta mais complexa, consulte [site analisar logs usando a análise do Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="f6e69-174">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
