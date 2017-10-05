---
title: "Introdução ao Azure Data Lake Store usando o SDK do Azure para Node.js | Microsoft Docs"
description: Saiba como usar o Node.js para trabalhar com contas do Data Lake Store e o sistema de arquivos.
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 2fee173c-69ae-4e1d-8773-48618cda9e16
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: nitinme
ms.openlocfilehash: 8c7a2e6ca061bbfa077592efb73d592906c3d070
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="5be74-103">Introdução ao Azure Data Lake Store usando o SDK do Azure para Node.js</span><span class="sxs-lookup"><span data-stu-id="5be74-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5be74-104">Portal</span><span class="sxs-lookup"><span data-stu-id="5be74-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="5be74-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5be74-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="5be74-106">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="5be74-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="5be74-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="5be74-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="5be74-108">API REST</span><span class="sxs-lookup"><span data-stu-id="5be74-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="5be74-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="5be74-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="5be74-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="5be74-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="5be74-111">Python</span><span class="sxs-lookup"><span data-stu-id="5be74-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="5be74-112">Para carregar e baixar grandes quantidades de dados (arquivos grandes, um grande número de arquivos ou ambos), recomendamos o uso do [SDK do Python](data-lake-store-get-started-python.md), do [SDK do .NET](data-lake-store-get-started-net-sdk.md), da [CLI do Azure 2.0](data-lake-store-get-started-cli-2.0.md) ou do [Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5be74-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use the [Python SDK](data-lake-store-get-started-python.md), the [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="5be74-113">Essas opções têm um desempenho melhor, pois usam vários threads para paralelizar a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="5be74-113">These options have better performance as they use multiple threads to parallelize the data movement.</span></span>
> 
> 

<span data-ttu-id="5be74-114">Saiba como usar o SDK do Azure para Node.js para criar uma conta do Azure Data Lake Store e executar operações básicas, como criar pastas, carregar e baixar arquivos de dados, excluir sua conta, etc. Para saber mais sobre o Data Lake Store, veja [Visão geral do Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5be74-114">Learn how to use the Azure SDK for Node.js to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="5be74-115">Atualmente, o SDK é compatível com</span><span class="sxs-lookup"><span data-stu-id="5be74-115">Currently, the SDK supports</span></span>

* <span data-ttu-id="5be74-116">**Versão do Node.js: 0.10.0 ou superior**</span><span class="sxs-lookup"><span data-stu-id="5be74-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="5be74-117">**Versão da API REST para Conta: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="5be74-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="5be74-118">**Versão da API REST para FileSystem: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="5be74-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5be74-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5be74-119">Prerequisites</span></span>
<span data-ttu-id="5be74-120">Antes de começar este artigo, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="5be74-120">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="5be74-121">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5be74-121">**An Azure subscription**.</span></span> <span data-ttu-id="5be74-122">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5be74-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5be74-123">**Criar um aplicativo do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5be74-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="5be74-124">Você pode usar o aplicativo Azure AD para autenticar o aplicativo Data Lake Store com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5be74-124">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="5be74-125">Há diferentes abordagens para autenticar com o Azure AD, que são a **autenticação de usuário final** ou a **autenticação serviço a serviço**.</span><span class="sxs-lookup"><span data-stu-id="5be74-125">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="5be74-126">Para obter instruções e saber mais sobre como se autenticar, veja [Autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [Autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="5be74-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-to-install"></a><span data-ttu-id="5be74-127">Como instalar</span><span class="sxs-lookup"><span data-stu-id="5be74-127">How to Install</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="5be74-128">Autenticar usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5be74-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="5be74-129">Os trechos de código abaixo mostram duas maneiras diferentes de autenticação com o Data Lake Store usando o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5be74-129">The snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="5be74-130">Para ver uma discussão detalhada sobre vários métodos de autenticação com o Data Lake Store, veja [Autenticar com o Data Lake Store usando o Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="5be74-130">For a detailed discussion on various methods to use for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="5be74-131">O trecho abaixo também requer entradas, como nome de domínio do Azure AD, ID de cliente para um aplicativo do Azure AD, etc. Todos esses detalhes podem ser recuperados em um aplicativo do Azure AD que você deve ter criado, detalhes que também estão incluídos no link acima.</span><span class="sxs-lookup"><span data-stu-id="5be74-131">The snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, the details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-store-clients"></a><span data-ttu-id="5be74-132">Criar os clientes do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5be74-132">Create the Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="5be74-133">Criar uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="5be74-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object to create
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location
};

client.account.create(resourceGroupName, accountName, accountToCreate, function (err, result, request, response) {
  if (err) {
    console.log(err);
    /*err has reference to the actual request and response, so you can see what was sent and received on the wire.
      The structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'The response body if any',
        request: reference to a stripped version of http request
        response: reference to a stripped version of the response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="5be74-134">Crie um arquivo com conteúdo</span><span class="sxs-lookup"><span data-stu-id="5be74-134">Create a file with content</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var fileToCreate = '/myfolder/myfile.txt';
var options = {
  streamContents: new Buffer('some string content')
}

filesystemClient.fileSystem.listFileStatus(accountName, fileToCreate, options, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    // no result is returned, only a 201 response for success.
    console.log('response is: ' + util.inspect(response, {depth: null}));
  }
});
```

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="5be74-135">Obter uma lista de arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="5be74-135">Get a list of files and folders</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var pathToEnumerate = '/myfolder';
filesystemClient.fileSystem.listFileStatus(accountName, pathToEnumerate, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="5be74-136">Confira também</span><span class="sxs-lookup"><span data-stu-id="5be74-136">See also</span></span>
* [<span data-ttu-id="5be74-137">Microsoft Azure SDK para Node.js</span><span class="sxs-lookup"><span data-stu-id="5be74-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="5be74-138">SDK do Microsoft Azure para Node.js - Gerenciamento da Análise de Data Lake</span><span class="sxs-lookup"><span data-stu-id="5be74-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

