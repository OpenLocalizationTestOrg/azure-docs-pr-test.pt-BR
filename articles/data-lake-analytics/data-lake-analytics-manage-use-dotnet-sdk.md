---
title: Gerenciar o Azure Data Lake Analytics usando o SDK do .NET do Azure | Microsoft Docs
description: "Saiba como gerenciar trabalhos, fontes de dados e usuários da Análise Data Lake. "
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
ms.openlocfilehash: 0f8a95f96ce4c816dfb9132923faa9a9bf20c205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="33f9c-103">Gerenciar o Azure Data Lake Analytics usando o SDK do .NET do Azure</span><span class="sxs-lookup"><span data-stu-id="33f9c-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="33f9c-104">Saiba como gerenciar contas, fontes de dados, usuários e trabalhos do Azure Data Lake Analytics usando o SDK do .NET do Azure.</span><span class="sxs-lookup"><span data-stu-id="33f9c-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure .NET SDK.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="33f9c-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="33f9c-105">Prerequisites</span></span>

* <span data-ttu-id="33f9c-106">**Visual Studio 2015, Visual Studio 2013 atualização 4 ou Visual Studio 2012 com Visual C++ instalado**.</span><span class="sxs-lookup"><span data-stu-id="33f9c-106">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="33f9c-107">**SDK do Microsoft Azure para .NET versão 2.5 ou posterior**.</span><span class="sxs-lookup"><span data-stu-id="33f9c-107">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="33f9c-108">Instale-o usando o [Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="33f9c-108">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="33f9c-109">**Pacotes NuGet necessários**</span><span class="sxs-lookup"><span data-stu-id="33f9c-109">**Required NuGet Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="33f9c-110">Instalar os pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="33f9c-110">Install NuGet packages</span></span>

|<span data-ttu-id="33f9c-111">Pacote</span><span class="sxs-lookup"><span data-stu-id="33f9c-111">Package</span></span>|<span data-ttu-id="33f9c-112">Versão</span><span class="sxs-lookup"><span data-stu-id="33f9c-112">Version</span></span>|
|-------|-------|
|[<span data-ttu-id="33f9c-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span><span class="sxs-lookup"><span data-stu-id="33f9c-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| <span data-ttu-id="33f9c-114">2.3.1</span><span class="sxs-lookup"><span data-stu-id="33f9c-114">2.3.1</span></span>|
|[<span data-ttu-id="33f9c-115">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="33f9c-115">Microsoft.Azure.Management.DataLake.Analytics</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|<span data-ttu-id="33f9c-116">3.0.0</span><span class="sxs-lookup"><span data-stu-id="33f9c-116">3.0.0</span></span>|
|[<span data-ttu-id="33f9c-117">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="33f9c-117">Microsoft.Azure.Management.DataLake.Store</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|<span data-ttu-id="33f9c-118">2.2.0</span><span class="sxs-lookup"><span data-stu-id="33f9c-118">2.2.0</span></span>|
|[<span data-ttu-id="33f9c-119">Microsoft.Azure.Management.ResourceManager</span><span class="sxs-lookup"><span data-stu-id="33f9c-119">Microsoft.Azure.Management.ResourceManager</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="33f9c-120">1.6.0 – versão prévia</span><span class="sxs-lookup"><span data-stu-id="33f9c-120">1.6.0-preview</span></span>|
|[<span data-ttu-id="33f9c-121">Microsoft.Azure.Graph.RBAC</span><span class="sxs-lookup"><span data-stu-id="33f9c-121">Microsoft.Azure.Graph.RBAC</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="33f9c-122">3.4.0 – versão prévia</span><span class="sxs-lookup"><span data-stu-id="33f9c-122">3.4.0-preview</span></span>|

<span data-ttu-id="33f9c-123">Você pode instalar esses pacotes por meio da linha de comando do NuGet com os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="33f9c-123">You can install these packages via the NuGet command line with the following commands:</span></span>

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a><span data-ttu-id="33f9c-124">Variáveis comuns</span><span class="sxs-lookup"><span data-stu-id="33f9c-124">Common variables</span></span>

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a><span data-ttu-id="33f9c-125">Autenticação</span><span class="sxs-lookup"><span data-stu-id="33f9c-125">Authentication</span></span>

<span data-ttu-id="33f9c-126">Você tem várias opções para fazer logon no Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="33f9c-126">You have multiple options for logging on to Azure Data Lake Analytics.</span></span> <span data-ttu-id="33f9c-127">O trecho a seguir mostra um exemplo de autenticação usando a autenticação de usuário interativo com um pop-up.</span><span class="sxs-lookup"><span data-stu-id="33f9c-127">The following snippet shows an example of authentication with interactive user authentication with a pop-up.</span></span>

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

<span data-ttu-id="33f9c-128">O código-fonte para **GetCreds_User_Popup** e o código para outras opções de autenticação são abordados em [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options) (Opções de autenticação .NET do Data Lake Analytics)</span><span class="sxs-lookup"><span data-stu-id="33f9c-128">The source code for **GetCreds_User_Popup** and the code for other options for authentication are covered in [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span></span>


## <a name="create-the-client-management-objects"></a><span data-ttu-id="33f9c-129">Criar objetos de gerenciamento do cliente</span><span class="sxs-lookup"><span data-stu-id="33f9c-129">Create the client management objects</span></span>

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

## <a name="manage-accounts"></a><span data-ttu-id="33f9c-130">Gerenciar Contas</span><span class="sxs-lookup"><span data-stu-id="33f9c-130">Manage accounts</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="33f9c-131">Criar um grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="33f9c-131">Create an Azure Resource Group</span></span>

<span data-ttu-id="33f9c-132">Se você ainda não criou um, deve ter um Grupo de Recursos do Azure para criar os componentes do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="33f9c-132">If you haven't already created one, you must have an Azure Resource Group to create your Data Lake Analytics components.</span></span> <span data-ttu-id="33f9c-133">Você precisa das suas credenciais de autenticação, da ID de assinatura e de um local.</span><span class="sxs-lookup"><span data-stu-id="33f9c-133">You  need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="33f9c-134">O código abaixo mostra como criar um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="33f9c-134">The following code shows how to create a resource group:</span></span>

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
<span data-ttu-id="33f9c-135">Para obter mais informações, consulte [Grupos de Recursos do Azure e Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span><span class="sxs-lookup"><span data-stu-id="33f9c-135">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>

### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="33f9c-136">Criar uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="33f9c-136">Create a Data Lake Store account</span></span>

<span data-ttu-id="33f9c-137">Cada conta do ADLA exige uma conta do ADLS.</span><span class="sxs-lookup"><span data-stu-id="33f9c-137">Ever ADLA account requires an ADLS account.</span></span> <span data-ttu-id="33f9c-138">Se ainda não tiver uma para usar, você poderá criar uma com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="33f9c-138">If you don't already have one to use, you can create one with the following code:</span></span>

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="33f9c-139">Criar uma conta da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="33f9c-139">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="33f9c-140">O código a seguir cria uma conta do ADLS</span><span class="sxs-lookup"><span data-stu-id="33f9c-140">The following code creates an ADLS account</span></span>

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a><span data-ttu-id="33f9c-141">Listar contas do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="33f9c-141">List Data Lake Store accounts</span></span>

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="33f9c-142">Listar contas da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="33f9c-142">List Data Lake Analytics accounts</span></span>

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a><span data-ttu-id="33f9c-143">Verificando se uma conta existe</span><span class="sxs-lookup"><span data-stu-id="33f9c-143">Checking if an account exists</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="33f9c-144">Obter informações sobre uma conta</span><span class="sxs-lookup"><span data-stu-id="33f9c-144">Get information about an account</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a><span data-ttu-id="33f9c-145">Excluir uma conta</span><span class="sxs-lookup"><span data-stu-id="33f9c-145">Delete an account</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-the-default-data-lake-store-account"></a><span data-ttu-id="33f9c-146">Obter a conta padrão do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="33f9c-146">Get the default Data Lake Store account</span></span>

<span data-ttu-id="33f9c-147">Toda conta do Data Lake Analytics requer uma conta padrão do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="33f9c-147">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="33f9c-148">Use este código para determinar a conta de Armazenamento padrão para uma conta do Analytics.</span><span class="sxs-lookup"><span data-stu-id="33f9c-148">Use this code to determine the default Store account for an Analytics account.</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a><span data-ttu-id="33f9c-149">Gerenciar as fontes de dados</span><span class="sxs-lookup"><span data-stu-id="33f9c-149">Manage data sources</span></span>

<span data-ttu-id="33f9c-150">No momento, a Análise Data Lake dá suporte às seguintes fontes de dados:</span><span class="sxs-lookup"><span data-stu-id="33f9c-150">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="33f9c-151">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="33f9c-151">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="33f9c-152">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="33f9c-152">Azure Storage Account</span></span>](../storage/common/storage-introduction.md)

### <a name="link-to-an-azure-storage-account"></a><span data-ttu-id="33f9c-153">Vincular a uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="33f9c-153">Link to an Azure Storage account</span></span>

<span data-ttu-id="33f9c-154">Você pode criar links para as contas de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="33f9c-154">You can create links to Azure Storage accounts.</span></span>

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a><span data-ttu-id="33f9c-155">Listar fontes de dados de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="33f9c-155">List Azure Storage data sources</span></span>

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

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="33f9c-156">Listar as fontes de dados do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="33f9c-156">List Data Lake Store data sources</span></span>

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

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="33f9c-157">Carregar e baixar arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="33f9c-157">Upload and download folders and files</span></span>
<span data-ttu-id="33f9c-158">Você pode usar o objeto de gerenciamento de cliente do sistema de arquivos do Data Lake Store para carregar e baixar arquivos ou pastas individuais do Azure para seu computador local, usando os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="33f9c-158">You can use the Data Lake Store file system client management object to upload and download individual files or folders from Azure to your local computer, using the following methods:</span></span>

- <span data-ttu-id="33f9c-159">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="33f9c-159">UploadFolder</span></span>
- <span data-ttu-id="33f9c-160">UploadFile</span><span class="sxs-lookup"><span data-stu-id="33f9c-160">UploadFile</span></span>
- <span data-ttu-id="33f9c-161">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="33f9c-161">DownloadFolder</span></span>
- <span data-ttu-id="33f9c-162">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="33f9c-162">DownloadFile</span></span>

<span data-ttu-id="33f9c-163">O primeiro parâmetro para esses métodos é o nome da conta de armazenamento do Data Lake Store, seguido de parâmetros para o caminho de origem e o caminho de destino.</span><span class="sxs-lookup"><span data-stu-id="33f9c-163">The first parameter for these methods is the name of the Data Lake Store Account, followed by parameters for the source path and the destination path.</span></span>

<span data-ttu-id="33f9c-164">O exemplo a seguir mostra como baixar uma pasta no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="33f9c-164">The following example shows how to download a folder in the Data Lake Store.</span></span>

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="33f9c-165">Criar um arquivo em uma conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="33f9c-165">Create a file in a Data Lake Store account</span></span>

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

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="33f9c-166">Verificar os caminhos da conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="33f9c-166">Verify Azure Storage account paths</span></span>
<span data-ttu-id="33f9c-167">O código a seguir verifica se existe uma conta de Armazenamento do Azure (storageAccntName) em uma conta do Data Lake Analytics (analyticsAccountName) e se existe um contêiner (containerName) na conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="33f9c-167">The following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in the Azure Storage account.</span></span>

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="33f9c-168">Gerenciar catálogo e trabalhos</span><span class="sxs-lookup"><span data-stu-id="33f9c-168">Manage catalog and jobs</span></span>
<span data-ttu-id="33f9c-169">O objeto DataLakeAnalyticsCatalogManagementClient fornece métodos para gerenciar o banco de dados SQL fornecido para cada conta do Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="33f9c-169">The DataLakeAnalyticsCatalogManagementClient object provides methods for managing the SQL database provided for each Azure Data Lake Analytics account.</span></span> <span data-ttu-id="33f9c-170">O DataLakeAnalyticsJobManagementClient fornece métodos para enviar e gerenciar os trabalhos executados no banco de dados com os scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="33f9c-170">The DataLakeAnalyticsJobManagementClient provides methods to submit and manage jobs run on the database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="33f9c-171">Listar bancos de dados e esquemas</span><span class="sxs-lookup"><span data-stu-id="33f9c-171">List databases and schemas</span></span>
<span data-ttu-id="33f9c-172">Entre as várias coisas que você pode listar, as mais comuns são os bancos de dados e seu esquema.</span><span class="sxs-lookup"><span data-stu-id="33f9c-172">Among the several things you can list, the most common are databases and their schema.</span></span> <span data-ttu-id="33f9c-173">O código a seguir obtém uma coleção de bancos de dados, em seguida, enumera o esquema de cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="33f9c-173">The following code obtains a collection of databases, and then enumerates the schema for each database.</span></span>

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

### <a name="list-table-columns"></a><span data-ttu-id="33f9c-174">Listar colunas da tabela</span><span class="sxs-lookup"><span data-stu-id="33f9c-174">List table columns</span></span>
<span data-ttu-id="33f9c-175">O código a seguir mostra como acessar o banco de dados com um cliente de gerenciamento de Catálogo do Data Lake Analytics para listar as colunas em uma tabela especificada.</span><span class="sxs-lookup"><span data-stu-id="33f9c-175">The following code shows how to access the database with a Data Lake Analytics Catalog management client to list the columns in a specified table.</span></span>

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

### <a name="list-failed-jobs"></a><span data-ttu-id="33f9c-176">Listar trabalhos com falha</span><span class="sxs-lookup"><span data-stu-id="33f9c-176">List failed jobs</span></span>
<span data-ttu-id="33f9c-177">O código a seguir lista informações sobre os trabalhos que falharam.</span><span class="sxs-lookup"><span data-stu-id="33f9c-177">The following code lists information about jobs that failed.</span></span>

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a><span data-ttu-id="33f9c-178">Listar pipelines</span><span class="sxs-lookup"><span data-stu-id="33f9c-178">List pipelines</span></span>
<span data-ttu-id="33f9c-179">O código a seguir lista informações sobre cada pipeline de trabalhos enviados para a conta.</span><span class="sxs-lookup"><span data-stu-id="33f9c-179">The following code lists information about each pipeline of jobs submitted to the account.</span></span>

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a><span data-ttu-id="33f9c-180">Listar recorrências</span><span class="sxs-lookup"><span data-stu-id="33f9c-180">List recurrences</span></span>
<span data-ttu-id="33f9c-181">O código a seguir lista informações sobre cada recorrência de trabalhos enviados para a conta.</span><span class="sxs-lookup"><span data-stu-id="33f9c-181">The following code lists information about each recurrence of jobs submitted to the account.</span></span>

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a><span data-ttu-id="33f9c-182">Cenários comuns de gráfico</span><span class="sxs-lookup"><span data-stu-id="33f9c-182">Common graph scenarios</span></span>

### <a name="look-up-user-in-the-aad-directory"></a><span data-ttu-id="33f9c-183">Pesquisar o usuário no diretório do AAD</span><span class="sxs-lookup"><span data-stu-id="33f9c-183">Look up user in the AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-the-objectid-of-a-user-in-the-aad-directory"></a><span data-ttu-id="33f9c-184">Obter o ObjectId de um usuário no diretório do AAD</span><span class="sxs-lookup"><span data-stu-id="33f9c-184">Get the ObjectId of a user in the AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a><span data-ttu-id="33f9c-185">Gerenciar políticas de computação</span><span class="sxs-lookup"><span data-stu-id="33f9c-185">Manage compute policies</span></span>
<span data-ttu-id="33f9c-186">O objeto DataLakeAnalyticsAccountManagementClient fornece métodos para gerenciar as políticas de computação para uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="33f9c-186">The DataLakeAnalyticsAccountManagementClient object provides methods for managing the compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="33f9c-187">Listar políticas de computação</span><span class="sxs-lookup"><span data-stu-id="33f9c-187">List compute policies</span></span>
<span data-ttu-id="33f9c-188">O código a seguir recupera uma lista de políticas de computação para uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="33f9c-188">The following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="33f9c-189">Criar uma nova política de computação</span><span class="sxs-lookup"><span data-stu-id="33f9c-189">Create a new compute policy</span></span>
<span data-ttu-id="33f9c-190">O código a seguir cria uma nova política de computação para uma conta do Data Lake Analytics, definindo a quantidade máxima de AUs disponíveis para o usuário especificado como 50 e a prioridade mínima de trabalho como 250.</span><span class="sxs-lookup"><span data-stu-id="33f9c-190">The following code creates a new compute policy for a Data Lake Analytics account, setting the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a><span data-ttu-id="33f9c-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33f9c-191">Next steps</span></span>
* [<span data-ttu-id="33f9c-192">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="33f9c-192">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="33f9c-193">Gerenciar o Azure Data Lake Analytics usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="33f9c-193">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="33f9c-194">Monitorar e solucionar problemas em trabalhos do Azure Data Lake Analytics usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="33f9c-194">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
