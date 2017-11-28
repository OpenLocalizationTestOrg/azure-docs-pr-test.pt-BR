---
title: "aaaManage análise Azure Data Lake usando o Azure PowerShell | Microsoft Docs"
description: "Saiba como contas de análise Data Lake toomanage, fontes de dados, trabalhos e itens de catálogo. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: ad14d53c-fed4-478d-ab4b-6d2e14ff2097
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/23/2017
ms.author: mahi
ms.openlocfilehash: 5954f0efb7d5a9778727edfccae83aec046343bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="779f5-103">Gerenciar a Análise Azure Data Lake usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="779f5-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="779f5-104">Saiba como contas de análise do Azure Data Lake toomanage, fontes de dados, trabalhos e itens de catálogo usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="779f5-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="779f5-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="779f5-105">Prerequisites</span></span>

<span data-ttu-id="779f5-106">Ao criar uma conta da análise Data Lake, é necessário tooknow:</span><span class="sxs-lookup"><span data-stu-id="779f5-106">When creating a Data Lake Analytics account, you need tooknow:</span></span>

* <span data-ttu-id="779f5-107">**ID da assinatura**: Olá ID de assinatura do Azure na qual reside a conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="779f5-107">**Subscription ID**: hello Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="779f5-108">**Grupo de recursos**: nome Olá Olá do Azure do grupo de recursos que contém sua conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="779f5-108">**Resource group**: hello name of hello Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="779f5-109">**Nome de conta da análise data Lake**: Olá nome deve conter apenas letras minúsculas e números de conta.</span><span class="sxs-lookup"><span data-stu-id="779f5-109">**Data Lake Analytics account name**: hello account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="779f5-110">**Conta padrão do Data Lake Store**: cada conta do Data Lake Analytics tem uma conta padrão do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="779f5-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="779f5-111">Essas contas devem ser em Olá mesmo local.</span><span class="sxs-lookup"><span data-stu-id="779f5-111">These accounts must be in hello same location.</span></span>
* <span data-ttu-id="779f5-112">**Local**: local de Olá da sua conta da análise Data Lake, como "Leste dos EUA 2" ou outros locais de suporte.</span><span class="sxs-lookup"><span data-stu-id="779f5-112">**Location**: hello location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="779f5-113">Os locais com suporte podem ser vistos em nossa [página de preços](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="779f5-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="779f5-114">trechos do PowerShell Olá neste tutorial usam essas variáveis toostore essas informações</span><span class="sxs-lookup"><span data-stu-id="779f5-114">hello PowerShell snippets in this tutorial use these variables toostore this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="779f5-115">Fazer logon</span><span class="sxs-lookup"><span data-stu-id="779f5-115">Log in</span></span>

<span data-ttu-id="779f5-116">Faça logon usando uma ID de assinatura.</span><span class="sxs-lookup"><span data-stu-id="779f5-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="779f5-117">Faça logon usando um nome de assinatura.</span><span class="sxs-lookup"><span data-stu-id="779f5-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="779f5-118">Olá `Login-AzureRmAccount` cmdlet sempre solicitará credenciais.</span><span class="sxs-lookup"><span data-stu-id="779f5-118">hello `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="779f5-119">Você pode evitar que está sendo solicitado usando Olá cmdlets a seguir:</span><span class="sxs-lookup"><span data-stu-id="779f5-119">You can avoid being prompted by using hello following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="779f5-120">Gerenciamento de contas</span><span class="sxs-lookup"><span data-stu-id="779f5-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="779f5-121">Criar uma conta da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="779f5-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="779f5-122">Se você ainda não tiver um [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, crie um.</span><span class="sxs-lookup"><span data-stu-id="779f5-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="779f5-123">Toda conta do Data Lake Analytics requer uma conta padrão do Data Lake Store usada para o armazenamento de logs.</span><span class="sxs-lookup"><span data-stu-id="779f5-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="779f5-124">Você pode reutilizar uma conta existente ou criar uma.</span><span class="sxs-lookup"><span data-stu-id="779f5-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="779f5-125">Quando um Grupo de Recursos e uma conta do Data Lake Store estiverem disponíveis, crie uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="779f5-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="779f5-126">Obter informações sobre uma conta</span><span class="sxs-lookup"><span data-stu-id="779f5-126">Get information about an account</span></span>

<span data-ttu-id="779f5-127">Obtenha detalhes sobre uma conta.</span><span class="sxs-lookup"><span data-stu-id="779f5-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="779f5-128">Verifica a existência de saudação de uma conta específica de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="779f5-128">Check hello existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="779f5-129">Olá cmdlet retorna um `True` ou `False`.</span><span class="sxs-lookup"><span data-stu-id="779f5-129">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="779f5-130">Verifica a existência de saudação de uma conta específica do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="779f5-130">Check hello existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="779f5-131">Olá cmdlet retorna um `True` ou `False`.</span><span class="sxs-lookup"><span data-stu-id="779f5-131">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="779f5-132">Listar contas</span><span class="sxs-lookup"><span data-stu-id="779f5-132">Listing accounts</span></span>

<span data-ttu-id="779f5-133">Contas de análise de lista Data Lake na assinatura atual hello.</span><span class="sxs-lookup"><span data-stu-id="779f5-133">List Data Lake Analytics accounts within hello current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="779f5-134">Liste contas do Data Lake Analytics em um grupo de recursos específico.</span><span class="sxs-lookup"><span data-stu-id="779f5-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="779f5-135">Gerenciar regras de firewall</span><span class="sxs-lookup"><span data-stu-id="779f5-135">Managing firewall rules</span></span>

<span data-ttu-id="779f5-136">Liste regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="779f5-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="779f5-137">Adicione uma regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="779f5-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="779f5-138">Altere uma regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="779f5-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="779f5-139">Remova uma regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="779f5-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="779f5-140">Permita endereços IP do Azure.</span><span class="sxs-lookup"><span data-stu-id="779f5-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="779f5-141">Gerenciar fontes de dados</span><span class="sxs-lookup"><span data-stu-id="779f5-141">Managing data sources</span></span>
<span data-ttu-id="779f5-142">Análise do Azure Data Lake atualmente suporta Olá fontes de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="779f5-142">Azure Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="779f5-143">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="779f5-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="779f5-144">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="779f5-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="779f5-145">Quando você cria uma conta de análise, você deve designar uma fonte de dados do repositório Data Lake conta toobe saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="779f5-145">When you create an Analytics account, you must designate a Data Lake Store account toobe hello default data source.</span></span> <span data-ttu-id="779f5-146">Olá repositório Data Lake conta padrão é usada toostore metadados de trabalho e o trabalho de logs de auditoria.</span><span class="sxs-lookup"><span data-stu-id="779f5-146">hello default Data Lake Store account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="779f5-147">Após criar uma conta do Data Lake Analytics, você pode adicionar outras contas do Data Lake Store e/ou contas de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="779f5-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-hello-default-data-lake-store-account"></a><span data-ttu-id="779f5-148">Localizar a conta de repositório Data Lake saudação padrão</span><span class="sxs-lookup"><span data-stu-id="779f5-148">Find hello default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="779f5-149">Você pode encontrar a conta de repositório Data Lake saudação padrão filtrando a lista Olá de fontes de dados por Olá `IsDefault` propriedade:</span><span class="sxs-lookup"><span data-stu-id="779f5-149">You can find hello default Data Lake Store account by filtering hello list of datasources by hello `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="779f5-150">Adicionar uma fonte de dados</span><span class="sxs-lookup"><span data-stu-id="779f5-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="779f5-151">Listar fontes de dados</span><span class="sxs-lookup"><span data-stu-id="779f5-151">List data sources</span></span>

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="779f5-152">Enviar trabalhos de U-SQL</span><span class="sxs-lookup"><span data-stu-id="779f5-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="779f5-153">Enviar uma cadeia de caracteres como um script U-SQL</span><span class="sxs-lookup"><span data-stu-id="779f5-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="779f5-154">Enviar um arquivo como um script U-SQL</span><span class="sxs-lookup"><span data-stu-id="779f5-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="779f5-155">Listar trabalhos em uma conta</span><span class="sxs-lookup"><span data-stu-id="779f5-155">List jobs in an account</span></span>

### <a name="list-all-hello-jobs-in-hello-account"></a><span data-ttu-id="779f5-156">Liste todos os trabalhos de saudação na conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="779f5-156">List all hello jobs in hello account.</span></span> 

<span data-ttu-id="779f5-157">saída de Hello inclui Olá trabalhos em execução e os trabalhos que tem sido concluída recentemente.</span><span class="sxs-lookup"><span data-stu-id="779f5-157">hello output includes hello currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="779f5-158">Listar um número específico de trabalhos</span><span class="sxs-lookup"><span data-stu-id="779f5-158">List a specific number of jobs</span></span>

<span data-ttu-id="779f5-159">Por padrão a lista de saudação de trabalhos é classificada em tempo de envio.</span><span class="sxs-lookup"><span data-stu-id="779f5-159">By default hello list of jobs is sorted on submit time.</span></span> <span data-ttu-id="779f5-160">Modo saudação enviado mais recentemente trabalhos são exibidos primeiro.</span><span class="sxs-lookup"><span data-stu-id="779f5-160">So hello most recently submitted jobs appear first.</span></span> <span data-ttu-id="779f5-161">Por padrão, Olá conta ADLA lembra trabalhos por 180 dias, mas Olá Ge AdlJob cmdlet por padrão retorna apenas Olá primeiros 500.</span><span class="sxs-lookup"><span data-stu-id="779f5-161">By default, hello ADLA account remembers jobs for 180 days, but hello Ge-AdlJob  cmdlet by default returns only hello first 500.</span></span> <span data-ttu-id="779f5-162">Use - toolist parâmetro superior um número específico de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="779f5-162">Use -Top parameter toolist a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a><span data-ttu-id="779f5-163">Listar trabalhos com base no valor de saudação da propriedade do trabalho</span><span class="sxs-lookup"><span data-stu-id="779f5-163">List jobs based on hello value of job property</span></span>

<span data-ttu-id="779f5-164">Usando Olá `-State` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="779f5-164">Using hello `-State` parameter.</span></span> <span data-ttu-id="779f5-165">É possível combinar qualquer um desses valores:</span><span class="sxs-lookup"><span data-stu-id="779f5-165">You can combine any of these values:</span></span>

* `Accepted`
* `Compiling`
* `Ended`
* `New`
* `Paused`
* `Queued`
* `Running`
* `Scheduling`
* `Start`

```powershell
# List hello running jobs
Get-AdlJob -Account $adla -State Running

# List hello jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List hello jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="779f5-166">Saudação de uso `-Result` toodetect parâmetro se terminou de trabalhos foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="779f5-166">Use hello `-Result` parameter toodetect whether ended jobs completed successfully.</span></span> <span data-ttu-id="779f5-167">O parâmetro possui esses valores:</span><span class="sxs-lookup"><span data-stu-id="779f5-167">It has these values:</span></span>

* <span data-ttu-id="779f5-168">Cancelado</span><span class="sxs-lookup"><span data-stu-id="779f5-168">Cancelled</span></span>
* <span data-ttu-id="779f5-169">Com falha</span><span class="sxs-lookup"><span data-stu-id="779f5-169">Failed</span></span>
* <span data-ttu-id="779f5-170">Nenhum</span><span class="sxs-lookup"><span data-stu-id="779f5-170">None</span></span>
* <span data-ttu-id="779f5-171">Bem-sucedido</span><span class="sxs-lookup"><span data-stu-id="779f5-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="779f5-172">Olá `-Submitter` parâmetro ajuda a identificar quem enviou um trabalho.</span><span class="sxs-lookup"><span data-stu-id="779f5-172">hello `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="779f5-173">Olá `-SubmittedAfter` é útil na filtragem tooa intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="779f5-173">hello `-SubmittedAfter` is useful in filtering tooa time range.</span></span>


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="779f5-174">Cenários comuns para listagem de trabalhos</span><span class="sxs-lookup"><span data-stu-id="779f5-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in hello last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within hello past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="779f5-175">Filtrar uma lista de trabalhos</span><span class="sxs-lookup"><span data-stu-id="779f5-175">Filtering a list of jobs</span></span>

<span data-ttu-id="779f5-176">Uma vez que tenha uma lista de trabalhos na sessão atual do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="779f5-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="779f5-177">Você pode usar a lista saudação normal do PowerShell cmdlets toofilter.</span><span class="sxs-lookup"><span data-stu-id="779f5-177">You can use normal PowerShell cmdlets toofilter hello list.</span></span>

<span data-ttu-id="779f5-178">Filtro de uma lista de trabalhos toohello trabalhos enviados em Olá últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="779f5-178">Filter a list of jobs toohello jobs submitted in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="779f5-179">Filtrar uma lista de trabalhos toohello trabalhos em Olá últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="779f5-179">Filter a list of jobs toohello jobs that ended in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="779f5-180">Filtre uma lista de trabalhos toohello trabalhos que foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="779f5-180">Filter a list of jobs toohello jobs that started running.</span></span> <span data-ttu-id="779f5-181">Um trabalho poderá falhar no tempo de compilação e, portanto, ele nunca será iniciado.</span><span class="sxs-lookup"><span data-stu-id="779f5-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="779f5-182">Vamos examinar os trabalhos de saudação falhado que realmente começou a ser executado e, em seguida, falha.</span><span class="sxs-lookup"><span data-stu-id="779f5-182">Let's look at hello failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="779f5-183">Analisar uma lista de trabalhos</span><span class="sxs-lookup"><span data-stu-id="779f5-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="779f5-184">Saudação de uso `Group-Object` cmdlet tooanalyze uma lista de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="779f5-184">Use hello `Group-Object` cmdlet tooanalyze a list of jobs.</span></span>

```
# Count hello number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count hello number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count hello number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count hello number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="779f5-185">Ao executar uma análise, pode ser útil tooadd propriedades toohello trabalho objetos toomake filtragem e agrupamento mais simples.</span><span class="sxs-lookup"><span data-stu-id="779f5-185">When performing an analysis, it can be useful tooadd properties toohello Job objects toomake filtering and grouping simpler.</span></span> <span data-ttu-id="779f5-186">saudação de trecho de código a seguir mostra como tooannotate uma JobInfo com calculada propriedades.</span><span class="sxs-lookup"><span data-stu-id="779f5-186">hello following  snippet shows how tooannotate a JobInfo with calculated properties.</span></span>

```
function annotate_job( $j )
{
    $dic1 = @{
        Label='AUHours';
        Expression={ ($_.DegreeOfParallelism * ($_.EndTime-$_.StartTime).TotalHours)}}
    $dic2 = @{
        Label='DurationSeconds';
        Expression={ ($_.EndTime-$_.StartTime).TotalSeconds}}
    $dic3 = @{
        Label='DidRun';
        Expression={ ($_.StartTime -ne $null)}}

    $j2 = $j | select *, $dic1, $dic2, $dic3
    $j2
}

$jobs = Get-AdlJob -Account $adla -Top 10
$jobs = $jobs | %{ annotate_job( $_ ) }
```

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="779f5-187">Obter informações sobre pipelines e recorrências</span><span class="sxs-lookup"><span data-stu-id="779f5-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="779f5-188">Saudação de uso `Get-AdlJobPipeline` informações de pipeline do cmdlet toosee Olá trabalhos enviados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="779f5-188">Use hello `Get-AdlJobPipeline` cmdlet toosee hello pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="779f5-189">Saudação de uso `Get-AdlJobRecurrence` cmdlet toosee Olá as informações de recorrência para trabalhos enviados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="779f5-189">Use hello `Get-AdlJobRecurrence` cmdlet toosee hello recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="779f5-190">Obter informações sobre um trabalho</span><span class="sxs-lookup"><span data-stu-id="779f5-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="779f5-191">Obter status do trabalho</span><span class="sxs-lookup"><span data-stu-id="779f5-191">Get job status</span></span>

<span data-ttu-id="779f5-192">Obter status de saudação de um trabalho específico.</span><span class="sxs-lookup"><span data-stu-id="779f5-192">Get hello status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a><span data-ttu-id="779f5-193">Examine as saídas do trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="779f5-193">Examine hello job outputs</span></span>

<span data-ttu-id="779f5-194">Após o término de trabalho hello, verifique se o arquivo de saída de hello existe listando arquivos de saudação em uma pasta.</span><span class="sxs-lookup"><span data-stu-id="779f5-194">After hello job has ended, check if hello output file exists by listing hello files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="779f5-195">Gerenciar trabalhos em execução</span><span class="sxs-lookup"><span data-stu-id="779f5-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="779f5-196">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="779f5-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a><span data-ttu-id="779f5-197">Aguarde até que um trabalho toofinish</span><span class="sxs-lookup"><span data-stu-id="779f5-197">Wait for a job toofinish</span></span>

<span data-ttu-id="779f5-198">Em vez de repetir `Get-AdlAnalyticsJob` até que um trabalho for concluído, você pode usar o hello `Wait-AdlJob` toowait cmdlet para Olá tooend de trabalho.</span><span class="sxs-lookup"><span data-stu-id="779f5-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use hello `Wait-AdlJob` cmdlet toowait for hello job tooend.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="779f5-199">Gerenciar políticas de computação</span><span class="sxs-lookup"><span data-stu-id="779f5-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="779f5-200">Listar as políticas de computação existentes</span><span class="sxs-lookup"><span data-stu-id="779f5-200">List existing compute policies</span></span>

<span data-ttu-id="779f5-201">Olá `Get-AdlAnalyticsComputePolicy` cmdlet recupera informações sobre as políticas de computação para uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="779f5-201">hello `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="779f5-202">Criar uma política de computação</span><span class="sxs-lookup"><span data-stu-id="779f5-202">Create a compute policy</span></span>

<span data-ttu-id="779f5-203">Olá `New-AdlAnalyticsComputePolicy` cmdlet cria uma nova política de computação para uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="779f5-203">hello `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="779f5-204">Este exemplo define Olá máximo toohello disponível de AUs especificado too50 de usuário e too250 de prioridade do trabalho mínimo hello.</span><span class="sxs-lookup"><span data-stu-id="779f5-204">This example sets  hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a><span data-ttu-id="779f5-205">Verificação de existência de saudação de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="779f5-205">Check for hello existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="779f5-206">Carregando e baixando arquivos</span><span class="sxs-lookup"><span data-stu-id="779f5-206">Uploading and downloading</span></span>

<span data-ttu-id="779f5-207">Carregar um arquivo.</span><span class="sxs-lookup"><span data-stu-id="779f5-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="779f5-208">Carregar uma pasta inteira de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="779f5-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="779f5-209">Baixar um arquivo.</span><span class="sxs-lookup"><span data-stu-id="779f5-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="779f5-210">Baixar uma pasta inteira de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="779f5-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="779f5-211">Se hello upload ou download de processo for interrompido, você pode tentar o processo de saudação tooresume executando o cmdlet de saudação novamente com hello ``-Resume`` sinalizador.</span><span class="sxs-lookup"><span data-stu-id="779f5-211">If hello upload or download process is interrupted, you can attempt tooresume hello process by running hello cmdlet again with hello ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="779f5-212">Gerenciar itens do catálogo</span><span class="sxs-lookup"><span data-stu-id="779f5-212">Manage catalog items</span></span>

<span data-ttu-id="779f5-213">Catálogo de saudação U-SQL é usada toostructure dados e código para que eles possam ser compartilhados por scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="779f5-213">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="779f5-214">Catálogo de saudação permite Olá maior desempenho possível com dados no Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="779f5-214">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="779f5-215">Para saber mais, consulte [Usar o Catálogo do U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="779f5-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-hello-u-sql-catalog"></a><span data-ttu-id="779f5-216">Itens de lista do catálogo de saudação U-SQL</span><span class="sxs-lookup"><span data-stu-id="779f5-216">List items in hello U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="779f5-217">Lista todos os assemblies de saudação em todos os bancos de dados de saudação em uma conta de ADLA.</span><span class="sxs-lookup"><span data-stu-id="779f5-217">List all hello assemblies in all hello databases in an ADLA Account.</span></span>

```powershell
$dbs = Get-AdlCatalogItem -Account $adla -ItemType Database

foreach ($db in $dbs)
{
    $asms = Get-AdlCatalogItem -Account $adla -ItemType Assembly -Path $db.Name

    foreach ($asm in $asms)
    {
        $asmname = "[" + $db.Name + "].[" + $asm.Name + "]"
        Write-Host $asmname
    }
}
```

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="779f5-218">Obter detalhes sobre um item de catálogo</span><span class="sxs-lookup"><span data-stu-id="779f5-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="779f5-219">Criar credenciais em um catálogo</span><span class="sxs-lookup"><span data-stu-id="779f5-219">Create credentials in a catalog</span></span>

<span data-ttu-id="779f5-220">Em um banco de dados U-SQL, crie um objeto de credencial para um banco de dados hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="779f5-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="779f5-221">Atualmente, as credenciais de U-SQL são Olá único tipo de item de catálogo que você pode criar por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="779f5-221">Currently, U-SQL credentials are hello only type of catalog item that you can create through PowerShell.</span></span>

```powershell
$dbName = "master"
$credentialName = "ContosoDbCreds"
$dbUri = "https://contoso.database.windows.net:8080"

New-AdlCatalogCredential -AccountName $adla `
          -DatabaseName $db `
          -CredentialName $credentialName `
          -Credential (Get-Credential) `
          -Uri $dbUri
```

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="779f5-222">Obter informações básicas sobre uma conta do ADLA</span><span class="sxs-lookup"><span data-stu-id="779f5-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="779f5-223">Especificado um nome de conta, Olá código a seguir procura informações básicas sobre a conta de saudação</span><span class="sxs-lookup"><span data-stu-id="779f5-223">Given an account name, hello following code looks up basic information about hello account</span></span>

```
$adla_acct = Get-AdlAnalyticsAccount -Name "saveenrdemoadla"
$adla_name = $adla_acct.Name
$adla_subid = $adla_acct.Id.Split("/")[2]
$adla_sub = Get-AzureRmSubscription -SubscriptionId $adla_subid
$adla_subname = $adla_sub.Name
$adla_defadls_datasource = Get-AdlAnalyticsDataSource -Account $adla_name  | ? { $_.IsDefault } 
$adla_defadlsname = $adla_defadls_datasource.Name

Write-Host "ADLA Account Name" $adla_name
Write-Host "Subscription Id" $adla_subid
Write-Host "Subscription Name" $adla_subname
Write-Host "Defautl ADLS Store" $adla_defadlsname
Write-Host 

Write-Host '$subname' " = ""$adla_subname"" "
Write-Host '$subid' " = ""$adla_subid"" "
Write-Host '$adla' " = ""$adla_name"" "
Write-Host '$adls' " = ""$adla_defadlsname"" "
```

## <a name="working-with-azure"></a><span data-ttu-id="779f5-224">Trabalhando com o Azure</span><span class="sxs-lookup"><span data-stu-id="779f5-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="779f5-225">Obter os detalhes de erros do AzureRm</span><span class="sxs-lookup"><span data-stu-id="779f5-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="779f5-226">Verifique se você está executando como um administrador</span><span class="sxs-lookup"><span data-stu-id="779f5-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="779f5-227">Localizar um TenantID</span><span class="sxs-lookup"><span data-stu-id="779f5-227">Find a TenantID</span></span>

<span data-ttu-id="779f5-228">De um nome de assinatura:</span><span class="sxs-lookup"><span data-stu-id="779f5-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="779f5-229">De uma ID de assinatura:</span><span class="sxs-lookup"><span data-stu-id="779f5-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="779f5-230">De um endereço de domínio, como "contoso.com"</span><span class="sxs-lookup"><span data-stu-id="779f5-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="779f5-231">Listar todas as IDs de assinaturas e de locatário</span><span class="sxs-lookup"><span data-stu-id="779f5-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="779f5-232">Criar uma conta do Data Lake Analytics usando um modelo</span><span class="sxs-lookup"><span data-stu-id="779f5-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="779f5-233">Você também pode usar um modelo de grupo de recursos do Azure usando Olá script do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="779f5-233">You can also use an Azure Resource Group template using hello following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update hello JSON template path 

# Log in tooAzure
Login-AzureRmAccount -SubscriptionId $subId

# Create hello resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create hello Data Lake Analytics account with hello default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="779f5-234">Para saber mais, confira [Implantar um aplicativo com um modelo do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-template-deploy.md) e [Criando modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="779f5-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="779f5-235">**Modelo de exemplo**</span><span class="sxs-lookup"><span data-stu-id="779f5-235">**Example template**</span></span>

<span data-ttu-id="779f5-236">Salvar Olá depois do texto como um `.json` e, em seguida, usar Olá precede o modelo de saudação de toouse de script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="779f5-236">Save hello following text as a `.json` file, and then use hello preceding PowerShell script toouse hello template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Analytics account toocreate."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Store account toocreate."
      }
    }
  },
  "resources": [
    {
      "name": "[parameters('adlStoreName')]",
      "type": "Microsoft.DataLakeStore/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ ],
      "tags": { }
    },
    {
      "name": "[parameters('adlAnalyticsName')]",
      "type": "Microsoft.DataLakeAnalytics/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ "[concat('Microsoft.DataLakeStore/accounts/',parameters('adlStoreName'))]" ],
      "tags": { },
      "properties": {
        "defaultDataLakeStoreAccount": "[parameters('adlStoreName')]",
        "dataLakeStoreAccounts": [
          { "name": "[parameters('adlStoreName')]" }
        ]
      }
    }
  ],
  "outputs": {
    "adlAnalyticsAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeAnalytics/accounts',parameters('adlAnalyticsName')))]"
    },
    "adlStoreAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeStore/accounts',parameters('adlStoreName')))]"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="779f5-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="779f5-237">Next steps</span></span>
* [<span data-ttu-id="779f5-238">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="779f5-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="779f5-239">Introdução ao Data Lake Analytics usando o [Portal do Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="779f5-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="779f5-240">Gerenciar o Azure Data Lake Analytics usando o [Portal do Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="779f5-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
