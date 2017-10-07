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
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a>Gerenciar a Análise Azure Data Lake usando o Azure PowerShell
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Saiba como contas de análise do Azure Data Lake toomanage, fontes de dados, trabalhos e itens de catálogo usando o PowerShell do Azure. 

## <a name="prerequisites"></a>Pré-requisitos

Ao criar uma conta da análise Data Lake, é necessário tooknow:

* **ID da assinatura**: Olá ID de assinatura do Azure na qual reside a conta da análise Data Lake.
* **Grupo de recursos**: nome Olá Olá do Azure do grupo de recursos que contém sua conta da análise Data Lake.
* **Nome de conta da análise data Lake**: Olá nome deve conter apenas letras minúsculas e números de conta.
* **Conta padrão do Data Lake Store**: cada conta do Data Lake Analytics tem uma conta padrão do Data Lake Store. Essas contas devem ser em Olá mesmo local.
* **Local**: local de Olá da sua conta da análise Data Lake, como "Leste dos EUA 2" ou outros locais de suporte. Os locais com suporte podem ser vistos em nossa [página de preços](https://azure.microsoft.com/pricing/details/data-lake-analytics/).

trechos do PowerShell Olá neste tutorial usam essas variáveis toostore essas informações

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a>Fazer logon

Faça logon usando uma ID de assinatura.

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

Faça logon usando um nome de assinatura.

```
Login-AzureRmAccount -SubscriptionName $subname 
```

Olá `Login-AzureRmAccount` cmdlet sempre solicitará credenciais. Você pode evitar que está sendo solicitado usando Olá cmdlets a seguir:

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a>Gerenciamento de contas

### <a name="create-a-data-lake-analytics-account"></a>Criar uma conta da Análise Data Lake

Se você ainda não tiver um [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, crie um. 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

Toda conta do Data Lake Analytics requer uma conta padrão do Data Lake Store usada para o armazenamento de logs. Você pode reutilizar uma conta existente ou criar uma. 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

Quando um Grupo de Recursos e uma conta do Data Lake Store estiverem disponíveis, crie uma conta do Data Lake Analytics.

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a>Obter informações sobre uma conta

Obtenha detalhes sobre uma conta.

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

Verifica a existência de saudação de uma conta específica de análise Data Lake. Olá cmdlet retorna um `True` ou `False`.

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

Verifica a existência de saudação de uma conta específica do repositório Data Lake. Olá cmdlet retorna um `True` ou `False`.

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a>Listar contas

Contas de análise de lista Data Lake na assinatura atual hello.

```powershell
Get-AdlAnalyticsAccount
```

Liste contas do Data Lake Analytics em um grupo de recursos específico.

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a>Gerenciar regras de firewall

Liste regras de firewall.

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

Adicione uma regra de firewall.

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Altere uma regra de firewall.

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Remova uma regra de firewall.

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



Permita endereços IP do Azure.

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a>Gerenciar fontes de dados
Análise do Azure Data Lake atualmente suporta Olá fontes de dados a seguir:

* [Repositório Azure Data Lake](../data-lake-store/data-lake-store-overview.md)
* [Armazenamento do Azure](../storage/common/storage-introduction.md)

Quando você cria uma conta de análise, você deve designar uma fonte de dados do repositório Data Lake conta toobe saudação padrão. Olá repositório Data Lake conta padrão é usada toostore metadados de trabalho e o trabalho de logs de auditoria. Após criar uma conta do Data Lake Analytics, você pode adicionar outras contas do Data Lake Store e/ou contas de Armazenamento. 

### <a name="find-hello-default-data-lake-store-account"></a>Localizar a conta de repositório Data Lake saudação padrão

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

Você pode encontrar a conta de repositório Data Lake saudação padrão filtrando a lista Olá de fontes de dados por Olá `IsDefault` propriedade:

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a>Adicionar uma fonte de dados

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a>Listar fontes de dados

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a>Enviar trabalhos de U-SQL

### <a name="submit-a-string-as-a-u-sql-script"></a>Enviar uma cadeia de caracteres como um script U-SQL

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


### <a name="submit-a-file-as-a-u-sql-script"></a>Enviar um arquivo como um script U-SQL

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a>Listar trabalhos em uma conta

### <a name="list-all-hello-jobs-in-hello-account"></a>Liste todos os trabalhos de saudação na conta de saudação. 

saída de Hello inclui Olá trabalhos em execução e os trabalhos que tem sido concluída recentemente.

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a>Listar um número específico de trabalhos

Por padrão a lista de saudação de trabalhos é classificada em tempo de envio. Modo saudação enviado mais recentemente trabalhos são exibidos primeiro. Por padrão, Olá conta ADLA lembra trabalhos por 180 dias, mas Olá Ge AdlJob cmdlet por padrão retorna apenas Olá primeiros 500. Use - toolist parâmetro superior um número específico de trabalhos.

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a>Listar trabalhos com base no valor de saudação da propriedade do trabalho

Usando Olá `-State` parâmetro. É possível combinar qualquer um desses valores:

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

Saudação de uso `-Result` toodetect parâmetro se terminou de trabalhos foi concluída com êxito. O parâmetro possui esses valores:

* Cancelado
* Com falha
* Nenhum
* Bem-sucedido

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


Olá `-Submitter` parâmetro ajuda a identificar quem enviou um trabalho.

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

Olá `-SubmittedAfter` é útil na filtragem tooa intervalo de tempo.


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a>Cenários comuns para listagem de trabalhos


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

## <a name="filtering-a-list-of-jobs"></a>Filtrar uma lista de trabalhos

Uma vez que tenha uma lista de trabalhos na sessão atual do PowerShell. Você pode usar a lista saudação normal do PowerShell cmdlets toofilter.

Filtro de uma lista de trabalhos toohello trabalhos enviados em Olá últimas 24 horas

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

Filtrar uma lista de trabalhos toohello trabalhos em Olá últimas 24 horas

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

Filtre uma lista de trabalhos toohello trabalhos que foi iniciada. Um trabalho poderá falhar no tempo de compilação e, portanto, ele nunca será iniciado. Vamos examinar os trabalhos de saudação falhado que realmente começou a ser executado e, em seguida, falha.

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a>Analisar uma lista de trabalhos

Saudação de uso `Group-Object` cmdlet tooanalyze uma lista de trabalhos.

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
Ao executar uma análise, pode ser útil tooadd propriedades toohello trabalho objetos toomake filtragem e agrupamento mais simples. saudação de trecho de código a seguir mostra como tooannotate uma JobInfo com calculada propriedades.

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

## <a name="get-information-about-pipelines-and-recurrences"></a>Obter informações sobre pipelines e recorrências

Saudação de uso `Get-AdlJobPipeline` informações de pipeline do cmdlet toosee Olá trabalhos enviados anteriormente.

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

Saudação de uso `Get-AdlJobRecurrence` cmdlet toosee Olá as informações de recorrência para trabalhos enviados anteriormente.

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a>Obter informações sobre um trabalho

### <a name="get-job-status"></a>Obter status do trabalho

Obter status de saudação de um trabalho específico.

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a>Examine as saídas do trabalho Olá

Após o término de trabalho hello, verifique se o arquivo de saída de hello existe listando arquivos de saudação em uma pasta.

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a>Gerenciar trabalhos em execução

### <a name="cancel-a-job"></a>Cancelar um trabalho

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a>Aguarde até que um trabalho toofinish

Em vez de repetir `Get-AdlAnalyticsJob` até que um trabalho for concluído, você pode usar o hello `Wait-AdlJob` toowait cmdlet para Olá tooend de trabalho.

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a>Gerenciar políticas de computação

### <a name="list-existing-compute-policies"></a>Listar as políticas de computação existentes

Olá `Get-AdlAnalyticsComputePolicy` cmdlet recupera informações sobre as políticas de computação para uma conta da análise Data Lake.

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a>Criar uma política de computação

Olá `New-AdlAnalyticsComputePolicy` cmdlet cria uma nova política de computação para uma conta da análise Data Lake. Este exemplo define Olá máximo toohello disponível de AUs especificado too50 de usuário e too250 de prioridade do trabalho mínimo hello.

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a>Verificação de existência de saudação de um arquivo.

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a>Carregando e baixando arquivos

Carregar um arquivo.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

Carregar uma pasta inteira de forma recursiva.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

Baixar um arquivo.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

Baixar uma pasta inteira de forma recursiva.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> Se hello upload ou download de processo for interrompido, você pode tentar o processo de saudação tooresume executando o cmdlet de saudação novamente com hello ``-Resume`` sinalizador.

## <a name="manage-catalog-items"></a>Gerenciar itens do catálogo

Catálogo de saudação U-SQL é usada toostructure dados e código para que eles possam ser compartilhados por scripts U-SQL. Catálogo de saudação permite Olá maior desempenho possível com dados no Azure Data Lake. Para saber mais, consulte [Usar o Catálogo do U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-items-in-hello-u-sql-catalog"></a>Itens de lista do catálogo de saudação U-SQL

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

Lista todos os assemblies de saudação em todos os bancos de dados de saudação em uma conta de ADLA.

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

### <a name="get-details-about-a-catalog-item"></a>Obter detalhes sobre um item de catálogo

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a>Criar credenciais em um catálogo

Em um banco de dados U-SQL, crie um objeto de credencial para um banco de dados hospedado no Azure. Atualmente, as credenciais de U-SQL são Olá único tipo de item de catálogo que você pode criar por meio do PowerShell.

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

### <a name="get-basic-information-about-an-adla-account"></a>Obter informações básicas sobre uma conta do ADLA

Especificado um nome de conta, Olá código a seguir procura informações básicas sobre a conta de saudação

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

## <a name="working-with-azure"></a>Trabalhando com o Azure

### <a name="get-details-of-azurerm-errors"></a>Obter os detalhes de erros do AzureRm

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a>Verifique se você está executando como um administrador

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a>Localizar um TenantID

De um nome de assinatura:

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

De uma ID de assinatura:

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

De um endereço de domínio, como "contoso.com"


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a>Listar todas as IDs de assinaturas e de locatário

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a>Criar uma conta do Data Lake Analytics usando um modelo

Você também pode usar um modelo de grupo de recursos do Azure usando Olá script do PowerShell a seguir:

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

Para saber mais, confira [Implantar um aplicativo com um modelo do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-template-deploy.md) e [Criando modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

**Modelo de exemplo**

Salvar Olá depois do texto como um `.json` e, em seguida, usar Olá precede o modelo de saudação de toouse de script do PowerShell. 

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

## <a name="next-steps"></a>Próximas etapas
* [Visão geral da Análise do Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* Introdução ao Data Lake Analytics usando o [Portal do Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)
* Gerenciar o Azure Data Lake Analytics usando o [Portal do Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md) 
