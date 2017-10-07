---
title: "aaaManage análise Azure Data Lake usando o SDK .NET do Azure | Microsoft Docs"
description: "Saiba como toomanage análise Data Lake trabalhos, fontes de dados, os usuários. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 811d172d-9873-4ce9-a6d5-c1a26b374c79
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 98630ba411823644a8bce1f1b0c1331f689cbb0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a>Gerenciar o Azure Data Lake Analytics usando o SDK do .NET do Azure
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Saiba como contas de análise do Azure Data Lake toomanage, fontes de dados, os usuários e trabalhos usando Olá SDK .NET do Azure. 

## <a name="prerequisites"></a>Pré-requisitos

* **Visual Studio 2015, Visual Studio 2013 atualização 4 ou Visual Studio 2012 com Visual C++ instalado**.
* **SDK do Microsoft Azure para .NET versão 2.5 ou posterior**.  Instale-o usando Olá [instalador de plataforma da Web](http://www.microsoft.com/web/downloads/platform.aspx).
* **Pacotes NuGet necessários**

### <a name="install-nuget-packages"></a>Instalar os pacotes NuGet

|Pacote|Versão|
|-------|-------|
|[Microsoft.Rest.ClientRuntime.Azure.Authentication](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| 2.3.1|
|[Microsoft.Azure.Management.DataLake.Analytics](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|3.0.0|
|[Microsoft.Azure.Management.DataLake.Store](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|2.2.0|
|[Microsoft.Azure.Management.ResourceManager](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|1.6.0 – versão prévia|
|[Microsoft.Azure.Graph.RBAC](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|3.4.0 – versão prévia|

Você pode instalar esses pacotes por meio da linha de comando do NuGet Olá com hello comandos a seguir:

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a>Variáveis comuns

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a>Autenticação

Você tem várias opções para o logon tooAzure análise Data Lake. Olá trecho a seguir mostra um exemplo de autenticação com a autenticação de usuário interativa com um pop-up.

``` csharp
using System;
using System.IO;
using System.Threading;
using System.Security.Cryptography.X509Certificates;

using Microsoft.Rest;
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.DataLake.Analytics;
using Microsoft.Azure.Management.DataLake.Analytics.Models;
using Microsoft.Azure.Management.DataLake.Store;
using Microsoft.Azure.Management.DataLake.Store.Models;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Microsoft.Azure.Graph.RBAC;

public static Program
{
   public static string TENANT = "microsoft.onmicrosoft.com";
   public static string CLIENTID = "1950a258-227b-4e31-a9cf-717495945fc2";
   public static System.Uri ARM_TOKEN_AUDIENCE = new System.Uri( @"https://management.core.windows.net/");
   public static System.Uri ADL_TOKEN_AUDIENCE = new System.Uri( @"https://datalake.azure.net/" );
   public static System.Uri GRAPH_TOKEN_AUDIENCE = new System.Uri( @"https://graph.windows.net/" );

   static void Main(string[] args)
   {
      string MY_DOCUMENTS= System.Environment.GetFolderPath( System.Environment.SpecialFolder.MyDocuments);
      string TOKEN_CACHE_PATH = System.IO.Path.Combine(MY_DOCUMENTS, "my.tokencache");

      var tokenCache = GetTokenCache(TOKEN_CACHE_PATH);
      var armCreds = GetCreds_User_Popup(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var adlCreds = GetCreds_User_Popup(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var graphCreds = GetCreds_User_Popup(TENANT, GRAPH_TOKEN_AUDIENCE, CLIENTID, tokenCache);
   }
}
```

Olá código-fonte para **GetCreds_User_Popup** e Olá código para outras opções de autenticação são abordadas em [opções de autenticação do .NET de análise do Data Lake](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)


## <a name="create-hello-client-management-objects"></a>Criar objetos de gerenciamento de cliente de saudação

``` csharp
var resourceManagementClient = new ResourceManagementClient(armCreds) { SubscriptionId = subid };

var adlaAccountClient = new DataLakeAnalyticsAccountManagementClient(armCreds);
adlaAccountClient.SubscriptionId = subid;

var adlsAccountClient = new DataLakeStoreAccountManagementClient(armCreds);
adlsAccountClient.SubscriptionId = subid;

var adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClient(adlCreds);
var adlaJobClient = new DataLakeAnalyticsJobManagementClient(adlCreds);

var adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(adlCreds);

var  graphClient = new GraphRbacManagementClient(graphCreds);
graphClient.TenantID = domain;

```

## <a name="manage-accounts"></a>Gerenciar Contas

### <a name="create-an-azure-resource-group"></a>Criar um grupo de recursos do Azure

Se você já não tiver criado uma, você deve ter toocreate um grupo de recursos do Azure os componentes da análise Data Lake. Você precisa das suas credenciais de autenticação, da ID de assinatura e de um local. Olá mostrado no código a seguir como toocreate um grupo de recursos:

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
Para obter mais informações, consulte [Grupos de Recursos do Azure e Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).

### <a name="create-a-data-lake-store-account"></a>Criar uma conta do Repositório Data Lake

Cada conta do ADLA exige uma conta do ADLS. Se você ainda não tiver um toouse, você pode criar uma com hello código a seguir:

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a>Criar uma conta da Análise Data Lake

saudação de código a seguir cria uma conta ADLS

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a>Listar contas do Data Lake Store

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a>Listar contas da Análise Data Lake

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a>Verificando se uma conta existe

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a>Obter informações sobre uma conta

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a>Excluir uma conta

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-hello-default-data-lake-store-account"></a>Obter a conta de repositório Data Lake saudação padrão

Toda conta do Data Lake Analytics requer uma conta padrão do Data Lake Store. Use essa conta de armazenamento do código toodetermine saudação padrão para uma conta da análise.

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a>Gerenciar as fontes de dados

Análise data Lake atualmente suporta Olá fontes de dados a seguir:

* [Repositório Azure Data Lake](../data-lake-store/data-lake-store-overview.md)
* [Conta de Armazenamento do Azure](../storage/common/storage-introduction.md)

### <a name="link-tooan-azure-storage-account"></a>Vincular conta de armazenamento do Azure tooan

Você pode criar links tooAzure contas de armazenamento.

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a>Listar fontes de dados de Armazenamento do Azure

``` csharp
var stg_accounts = adlaAccountClient.StorageAccounts.ListByAccount(rg, adla);

if (stg_accounts != null)
{
  foreach (var stg_account in stg_accounts)
  {
      Console.WriteLine($"Storage account: {0}", stg_account.Name);
  }
}
```

### <a name="list-data-lake-store-data-sources"></a>Listar as fontes de dados do Data Lake Store

``` csharp
var adls_accounts = adlsClient.Account.List();

if (adls_accounts != null)
{
  foreach (var adls_accnt in adls_accounts)
  {
      Console.WriteLine($"ADLS account: {0}", adls_accnt.Name);
  }
}
```

### <a name="upload-and-download-folders-and-files"></a>Carregar e baixar arquivos e pastas
Você pode usar tooupload de objeto do hello repositório Data Lake arquivo sistema cliente gerenciamento e baixar arquivos ou pastas individuais do Azure tooyour computador local, usando Olá métodos a seguir:

- UploadFolder
- UploadFile
- DownloadFolder
- DownloadFile

primeiro parâmetro Hello desses métodos é o nome de saudação do Olá conta do repositório Data Lake, seguido por parâmetros de caminho de origem hello e caminho de destino de saudação.

saudação de exemplo a seguir mostra como toodownload uma pasta no hello repositório Data Lake.

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a>Criar um arquivo em uma conta do Data Lake Store

``` csharp
using (var memstream = new MemoryStream())
{
   using (var sw = new StreamWriter(memstream, UTF8Encoding.UTF8))
   {
      sw.WriteLine("Hello World");
      sw.Flush();

      adlsFileSystemClient.FileSystem.Create(adls, "/Samples/Output/randombytes.csv", memstream);
   }
}
```

### <a name="verify-azure-storage-account-paths"></a>Verificar os caminhos da conta de Armazenamento do Azure
Hello código a seguir verifica se existe uma conta de armazenamento do Azure (storageAccntName) em uma conta da análise Data Lake (analyticsAccountName), e se existe um contêiner (containerName) na conta de armazenamento do Azure hello.

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a>Gerenciar catálogo e trabalhos
Olá DataLakeAnalyticsCatalogManagementClient fornece métodos para gerenciar o banco de dados do SQL Olá fornecido para cada conta da análise Azure Data Lake. Olá DataLakeAnalyticsJobManagementClient fornece métodos toosubmit e gerenciar os trabalhos são executados no banco de dados de saudação com scripts U-SQL.

### <a name="list-databases-and-schemas"></a>Listar bancos de dados e esquemas
Entre Olá várias coisas que você pode listar, hello mais comuns são bancos de dados e seu esquema. Olá código a seguir obtém uma coleção de bancos de dados e, em seguida, enumera esquema Olá para cada banco de dados.

``` csharp
var databases = adlaCatalogClient.Catalog.ListDatabases(adla);
foreach (var db in databases)
{
  Console.WriteLine($"Database: {db.Name}");
  Console.WriteLine(" - Schemas:");
  var schemas = adlaCatalogClient.Catalog.ListSchemas(adla, db.Name);
  foreach (var schm in schemas)
  {
      Console.WriteLine($"\t{schm.Name}");
  }
}
```

### <a name="list-table-columns"></a>Listar colunas da tabela
Olá código a seguir mostra como tooaccess Olá banco de dados com um colunas Data Lake análise Catalog gerenciamento cliente toolist Olá em uma tabela especificada.

``` csharp
var tbl = adlaCatalogClient.Catalog.GetTable(adla, "master", "dbo", "MyTableName");
IEnumerable<USqlTableColumn> columns = tbl.ColumnList;

foreach (USqlTableColumn utc in columns)
{
  string scriptPath = "/Samples/Scripts/SearchResults_Wikipedia_Script.txt";
  Stream scriptStrm = adlsFileSystemClient.FileSystem.Open(_adlsAccountName, scriptPath);
  string scriptTxt = string.Empty;
  using (StreamReader sr = new StreamReader(scriptStrm))
  {
      scriptTxt = sr.ReadToEnd();
  }

  var jobName = "SR_Wikipedia";
  var jobId = Guid.NewGuid();
  var properties = new USqlJobProperties(scriptTxt);
  var parameters = new JobInformation(jobName, JobType.USql, properties, priority: 1, degreeOfParallelism: 1, jobId: jobId);
  var jobInfo = adlaJobClient.Job.Create(adla, jobId, parameters);
  Console.WriteLine($"Job {jobName} submitted.");

}
```

### <a name="list-failed-jobs"></a>Listar trabalhos com falha
Olá código a seguir lista informações sobre trabalhos que falharam.

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a>Listar pipelines
Olá código a seguir lista informações sobre cada pipeline de trabalhos enviados toohello conta.

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a>Listar recorrências
Olá código a seguir lista informações sobre cada recorrência de trabalhos enviados toohello conta.

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a>Cenários comuns de gráfico

### <a name="look-up-user-in-hello-aad-directory"></a>Pesquisar o usuário no diretório de saudação do AAD

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-hello-objectid-of-a-user-in-hello-aad-directory"></a>Obter Olá ObjectId do usuário no diretório de saudação do AAD

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a>Gerenciar políticas de computação
Olá DataLakeAnalyticsAccountManagementClient fornece métodos para gerenciar Olá computação políticas para uma conta da análise Data Lake.

### <a name="list-compute-policies"></a>Listar políticas de computação
saudação de código a seguir recupera uma lista de políticas de computação para uma conta da análise Data Lake.

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a>Criar uma nova política de computação
saudação de código a seguir cria uma nova política de computação para uma conta da análise Data Lake, configuração Olá máximo Austrália disponível toohello especificado too50 de usuário e too250 de prioridade do trabalho mínimo hello.

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a>Próximas etapas
* [Visão geral da Análise do Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Gerenciar o Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-manage-use-portal.md)
* [Monitorar e solucionar problemas em trabalhos do Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
