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
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="da715-103">Gerenciar o Azure Data Lake Analytics usando o SDK do .NET do Azure</span><span class="sxs-lookup"><span data-stu-id="da715-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="da715-104">Saiba como contas de análise do Azure Data Lake toomanage, fontes de dados, os usuários e trabalhos usando Olá SDK .NET do Azure.</span><span class="sxs-lookup"><span data-stu-id="da715-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure .NET SDK.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="da715-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="da715-105">Prerequisites</span></span>

* <span data-ttu-id="da715-106">**Visual Studio 2015, Visual Studio 2013 atualização 4 ou Visual Studio 2012 com Visual C++ instalado**.</span><span class="sxs-lookup"><span data-stu-id="da715-106">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="da715-107">**SDK do Microsoft Azure para .NET versão 2.5 ou posterior**.</span><span class="sxs-lookup"><span data-stu-id="da715-107">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="da715-108">Instale-o usando Olá [instalador de plataforma da Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="da715-108">Install it using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="da715-109">**Pacotes NuGet necessários**</span><span class="sxs-lookup"><span data-stu-id="da715-109">**Required NuGet Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="da715-110">Instalar os pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="da715-110">Install NuGet packages</span></span>

|<span data-ttu-id="da715-111">Pacote</span><span class="sxs-lookup"><span data-stu-id="da715-111">Package</span></span>|<span data-ttu-id="da715-112">Versão</span><span class="sxs-lookup"><span data-stu-id="da715-112">Version</span></span>|
|-------|-------|
|[<span data-ttu-id="da715-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span><span class="sxs-lookup"><span data-stu-id="da715-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| <span data-ttu-id="da715-114">2.3.1</span><span class="sxs-lookup"><span data-stu-id="da715-114">2.3.1</span></span>|
|[<span data-ttu-id="da715-115">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="da715-115">Microsoft.Azure.Management.DataLake.Analytics</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|<span data-ttu-id="da715-116">3.0.0</span><span class="sxs-lookup"><span data-stu-id="da715-116">3.0.0</span></span>|
|[<span data-ttu-id="da715-117">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="da715-117">Microsoft.Azure.Management.DataLake.Store</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|<span data-ttu-id="da715-118">2.2.0</span><span class="sxs-lookup"><span data-stu-id="da715-118">2.2.0</span></span>|
|[<span data-ttu-id="da715-119">Microsoft.Azure.Management.ResourceManager</span><span class="sxs-lookup"><span data-stu-id="da715-119">Microsoft.Azure.Management.ResourceManager</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="da715-120">1.6.0 – versão prévia</span><span class="sxs-lookup"><span data-stu-id="da715-120">1.6.0-preview</span></span>|
|[<span data-ttu-id="da715-121">Microsoft.Azure.Graph.RBAC</span><span class="sxs-lookup"><span data-stu-id="da715-121">Microsoft.Azure.Graph.RBAC</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="da715-122">3.4.0 – versão prévia</span><span class="sxs-lookup"><span data-stu-id="da715-122">3.4.0-preview</span></span>|

<span data-ttu-id="da715-123">Você pode instalar esses pacotes por meio da linha de comando do NuGet Olá com hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="da715-123">You can install these packages via hello NuGet command line with hello following commands:</span></span>

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a><span data-ttu-id="da715-124">Variáveis comuns</span><span class="sxs-lookup"><span data-stu-id="da715-124">Common variables</span></span>

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a><span data-ttu-id="da715-125">Autenticação</span><span class="sxs-lookup"><span data-stu-id="da715-125">Authentication</span></span>

<span data-ttu-id="da715-126">Você tem várias opções para o logon tooAzure análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da715-126">You have multiple options for logging on tooAzure Data Lake Analytics.</span></span> <span data-ttu-id="da715-127">Olá trecho a seguir mostra um exemplo de autenticação com a autenticação de usuário interativa com um pop-up.</span><span class="sxs-lookup"><span data-stu-id="da715-127">hello following snippet shows an example of authentication with interactive user authentication with a pop-up.</span></span>

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

<span data-ttu-id="da715-128">Olá código-fonte para **GetCreds_User_Popup** e Olá código para outras opções de autenticação são abordadas em [opções de autenticação do .NET de análise do Data Lake](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span><span class="sxs-lookup"><span data-stu-id="da715-128">hello source code for **GetCreds_User_Popup** and hello code for other options for authentication are covered in [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span></span>


## <a name="create-hello-client-management-objects"></a><span data-ttu-id="da715-129">Criar objetos de gerenciamento de cliente de saudação</span><span class="sxs-lookup"><span data-stu-id="da715-129">Create hello client management objects</span></span>

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

## <a name="manage-accounts"></a><span data-ttu-id="da715-130">Gerenciar Contas</span><span class="sxs-lookup"><span data-stu-id="da715-130">Manage accounts</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="da715-131">Criar um grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="da715-131">Create an Azure Resource Group</span></span>

<span data-ttu-id="da715-132">Se você já não tiver criado uma, você deve ter toocreate um grupo de recursos do Azure os componentes da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da715-132">If you haven't already created one, you must have an Azure Resource Group toocreate your Data Lake Analytics components.</span></span> <span data-ttu-id="da715-133">Você precisa das suas credenciais de autenticação, da ID de assinatura e de um local.</span><span class="sxs-lookup"><span data-stu-id="da715-133">You  need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="da715-134">Olá mostrado no código a seguir como toocreate um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="da715-134">hello following code shows how toocreate a resource group:</span></span>

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
<span data-ttu-id="da715-135">Para obter mais informações, consulte [Grupos de Recursos do Azure e Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span><span class="sxs-lookup"><span data-stu-id="da715-135">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>

### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="da715-136">Criar uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="da715-136">Create a Data Lake Store account</span></span>

<span data-ttu-id="da715-137">Cada conta do ADLA exige uma conta do ADLS.</span><span class="sxs-lookup"><span data-stu-id="da715-137">Ever ADLA account requires an ADLS account.</span></span> <span data-ttu-id="da715-138">Se você ainda não tiver um toouse, você pode criar uma com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="da715-138">If you don't already have one toouse, you can create one with hello following code:</span></span>

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="da715-139">Criar uma conta da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="da715-139">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="da715-140">saudação de código a seguir cria uma conta ADLS</span><span class="sxs-lookup"><span data-stu-id="da715-140">hello following code creates an ADLS account</span></span>

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a><span data-ttu-id="da715-141">Listar contas do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="da715-141">List Data Lake Store accounts</span></span>

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="da715-142">Listar contas da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="da715-142">List Data Lake Analytics accounts</span></span>

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a><span data-ttu-id="da715-143">Verificando se uma conta existe</span><span class="sxs-lookup"><span data-stu-id="da715-143">Checking if an account exists</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="da715-144">Obter informações sobre uma conta</span><span class="sxs-lookup"><span data-stu-id="da715-144">Get information about an account</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a><span data-ttu-id="da715-145">Excluir uma conta</span><span class="sxs-lookup"><span data-stu-id="da715-145">Delete an account</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-hello-default-data-lake-store-account"></a><span data-ttu-id="da715-146">Obter a conta de repositório Data Lake saudação padrão</span><span class="sxs-lookup"><span data-stu-id="da715-146">Get hello default Data Lake Store account</span></span>

<span data-ttu-id="da715-147">Toda conta do Data Lake Analytics requer uma conta padrão do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="da715-147">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="da715-148">Use essa conta de armazenamento do código toodetermine saudação padrão para uma conta da análise.</span><span class="sxs-lookup"><span data-stu-id="da715-148">Use this code toodetermine hello default Store account for an Analytics account.</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a><span data-ttu-id="da715-149">Gerenciar as fontes de dados</span><span class="sxs-lookup"><span data-stu-id="da715-149">Manage data sources</span></span>

<span data-ttu-id="da715-150">Análise data Lake atualmente suporta Olá fontes de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="da715-150">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="da715-151">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="da715-151">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="da715-152">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="da715-152">Azure Storage Account</span></span>](../storage/common/storage-introduction.md)

### <a name="link-tooan-azure-storage-account"></a><span data-ttu-id="da715-153">Vincular conta de armazenamento do Azure tooan</span><span class="sxs-lookup"><span data-stu-id="da715-153">Link tooan Azure Storage account</span></span>

<span data-ttu-id="da715-154">Você pode criar links tooAzure contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="da715-154">You can create links tooAzure Storage accounts.</span></span>

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a><span data-ttu-id="da715-155">Listar fontes de dados de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="da715-155">List Azure Storage data sources</span></span>

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

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="da715-156">Listar as fontes de dados do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="da715-156">List Data Lake Store data sources</span></span>

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

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="da715-157">Carregar e baixar arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="da715-157">Upload and download folders and files</span></span>
<span data-ttu-id="da715-158">Você pode usar tooupload de objeto do hello repositório Data Lake arquivo sistema cliente gerenciamento e baixar arquivos ou pastas individuais do Azure tooyour computador local, usando Olá métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="da715-158">You can use hello Data Lake Store file system client management object tooupload and download individual files or folders from Azure tooyour local computer, using hello following methods:</span></span>

- <span data-ttu-id="da715-159">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="da715-159">UploadFolder</span></span>
- <span data-ttu-id="da715-160">UploadFile</span><span class="sxs-lookup"><span data-stu-id="da715-160">UploadFile</span></span>
- <span data-ttu-id="da715-161">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="da715-161">DownloadFolder</span></span>
- <span data-ttu-id="da715-162">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="da715-162">DownloadFile</span></span>

<span data-ttu-id="da715-163">primeiro parâmetro Hello desses métodos é o nome de saudação do Olá conta do repositório Data Lake, seguido por parâmetros de caminho de origem hello e caminho de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="da715-163">hello first parameter for these methods is hello name of hello Data Lake Store Account, followed by parameters for hello source path and hello destination path.</span></span>

<span data-ttu-id="da715-164">saudação de exemplo a seguir mostra como toodownload uma pasta no hello repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da715-164">hello following example shows how toodownload a folder in hello Data Lake Store.</span></span>

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="da715-165">Criar um arquivo em uma conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="da715-165">Create a file in a Data Lake Store account</span></span>

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

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="da715-166">Verificar os caminhos da conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="da715-166">Verify Azure Storage account paths</span></span>
<span data-ttu-id="da715-167">Hello código a seguir verifica se existe uma conta de armazenamento do Azure (storageAccntName) em uma conta da análise Data Lake (analyticsAccountName), e se existe um contêiner (containerName) na conta de armazenamento do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="da715-167">hello following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in hello Azure Storage account.</span></span>

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="da715-168">Gerenciar catálogo e trabalhos</span><span class="sxs-lookup"><span data-stu-id="da715-168">Manage catalog and jobs</span></span>
<span data-ttu-id="da715-169">Olá DataLakeAnalyticsCatalogManagementClient fornece métodos para gerenciar o banco de dados do SQL Olá fornecido para cada conta da análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da715-169">hello DataLakeAnalyticsCatalogManagementClient object provides methods for managing hello SQL database provided for each Azure Data Lake Analytics account.</span></span> <span data-ttu-id="da715-170">Olá DataLakeAnalyticsJobManagementClient fornece métodos toosubmit e gerenciar os trabalhos são executados no banco de dados de saudação com scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="da715-170">hello DataLakeAnalyticsJobManagementClient provides methods toosubmit and manage jobs run on hello database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="da715-171">Listar bancos de dados e esquemas</span><span class="sxs-lookup"><span data-stu-id="da715-171">List databases and schemas</span></span>
<span data-ttu-id="da715-172">Entre Olá várias coisas que você pode listar, hello mais comuns são bancos de dados e seu esquema.</span><span class="sxs-lookup"><span data-stu-id="da715-172">Among hello several things you can list, hello most common are databases and their schema.</span></span> <span data-ttu-id="da715-173">Olá código a seguir obtém uma coleção de bancos de dados e, em seguida, enumera esquema Olá para cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="da715-173">hello following code obtains a collection of databases, and then enumerates hello schema for each database.</span></span>

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

### <a name="list-table-columns"></a><span data-ttu-id="da715-174">Listar colunas da tabela</span><span class="sxs-lookup"><span data-stu-id="da715-174">List table columns</span></span>
<span data-ttu-id="da715-175">Olá código a seguir mostra como tooaccess Olá banco de dados com um colunas Data Lake análise Catalog gerenciamento cliente toolist Olá em uma tabela especificada.</span><span class="sxs-lookup"><span data-stu-id="da715-175">hello following code shows how tooaccess hello database with a Data Lake Analytics Catalog management client toolist hello columns in a specified table.</span></span>

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

### <a name="list-failed-jobs"></a><span data-ttu-id="da715-176">Listar trabalhos com falha</span><span class="sxs-lookup"><span data-stu-id="da715-176">List failed jobs</span></span>
<span data-ttu-id="da715-177">Olá código a seguir lista informações sobre trabalhos que falharam.</span><span class="sxs-lookup"><span data-stu-id="da715-177">hello following code lists information about jobs that failed.</span></span>

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a><span data-ttu-id="da715-178">Listar pipelines</span><span class="sxs-lookup"><span data-stu-id="da715-178">List pipelines</span></span>
<span data-ttu-id="da715-179">Olá código a seguir lista informações sobre cada pipeline de trabalhos enviados toohello conta.</span><span class="sxs-lookup"><span data-stu-id="da715-179">hello following code lists information about each pipeline of jobs submitted toohello account.</span></span>

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a><span data-ttu-id="da715-180">Listar recorrências</span><span class="sxs-lookup"><span data-stu-id="da715-180">List recurrences</span></span>
<span data-ttu-id="da715-181">Olá código a seguir lista informações sobre cada recorrência de trabalhos enviados toohello conta.</span><span class="sxs-lookup"><span data-stu-id="da715-181">hello following code lists information about each recurrence of jobs submitted toohello account.</span></span>

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a><span data-ttu-id="da715-182">Cenários comuns de gráfico</span><span class="sxs-lookup"><span data-stu-id="da715-182">Common graph scenarios</span></span>

### <a name="look-up-user-in-hello-aad-directory"></a><span data-ttu-id="da715-183">Pesquisar o usuário no diretório de saudação do AAD</span><span class="sxs-lookup"><span data-stu-id="da715-183">Look up user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-hello-objectid-of-a-user-in-hello-aad-directory"></a><span data-ttu-id="da715-184">Obter Olá ObjectId do usuário no diretório de saudação do AAD</span><span class="sxs-lookup"><span data-stu-id="da715-184">Get hello ObjectId of a user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a><span data-ttu-id="da715-185">Gerenciar políticas de computação</span><span class="sxs-lookup"><span data-stu-id="da715-185">Manage compute policies</span></span>
<span data-ttu-id="da715-186">Olá DataLakeAnalyticsAccountManagementClient fornece métodos para gerenciar Olá computação políticas para uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da715-186">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="da715-187">Listar políticas de computação</span><span class="sxs-lookup"><span data-stu-id="da715-187">List compute policies</span></span>
<span data-ttu-id="da715-188">saudação de código a seguir recupera uma lista de políticas de computação para uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da715-188">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="da715-189">Criar uma nova política de computação</span><span class="sxs-lookup"><span data-stu-id="da715-189">Create a new compute policy</span></span>
<span data-ttu-id="da715-190">saudação de código a seguir cria uma nova política de computação para uma conta da análise Data Lake, configuração Olá máximo Austrália disponível toohello especificado too50 de usuário e too250 de prioridade do trabalho mínimo hello.</span><span class="sxs-lookup"><span data-stu-id="da715-190">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a><span data-ttu-id="da715-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="da715-191">Next steps</span></span>
* [<span data-ttu-id="da715-192">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="da715-192">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="da715-193">Gerenciar o Azure Data Lake Analytics usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="da715-193">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="da715-194">Monitorar e solucionar problemas em trabalhos do Azure Data Lake Analytics usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="da715-194">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
