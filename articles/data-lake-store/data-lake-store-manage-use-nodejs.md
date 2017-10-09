---
title: "aaaGet de Introdução ao repositório Azure Data Lake usando o Azure SDK para Node.js | Microsoft Docs"
description: "Saiba como o sistema de arquivos toouse Node. js toowork com contas do repositório Data Lake e hello."
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
ms.openlocfilehash: ce36a2e0de4e091a4e85ed784a3381415ef6f9e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="c9335-103">Introdução ao Azure Data Lake Store usando o SDK do Azure para Node.js</span><span class="sxs-lookup"><span data-stu-id="c9335-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9335-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c9335-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="c9335-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9335-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="c9335-106">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="c9335-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="c9335-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="c9335-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="c9335-108">API REST</span><span class="sxs-lookup"><span data-stu-id="c9335-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="c9335-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="c9335-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="c9335-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="c9335-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="c9335-111">Python</span><span class="sxs-lookup"><span data-stu-id="c9335-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="c9335-112">Para carregar e baixar a grande quantidade de dados (arquivos grandes, um grande número de arquivos ou ambos), é recomendável que você use Olá [SDK de Python](data-lake-store-get-started-python.md), Olá [.NET SDK](data-lake-store-get-started-net-sdk.md), [CLI do Azure 2.0](data-lake-store-get-started-cli-2.0.md), ou [PowerShell do Azure](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c9335-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="c9335-113">Essas opções têm um desempenho melhor que usam vários threads tooparallelize Olá a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="c9335-113">These options have better performance as they use multiple threads tooparallelize hello data movement.</span></span>
> 
> 

<span data-ttu-id="c9335-114">Saiba como toouse hello Azure SDK para Node.js toocreate uma conta do repositório Azure Data Lake e executar operações básicas, como criar pastas, carregar e baixar arquivos de dados, exclua sua conta, etc. Para saber mais sobre o Data Lake Store, veja [Visão geral do Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9335-114">Learn how toouse hello Azure SDK for Node.js toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="c9335-115">Atualmente, há suporte Olá SDK</span><span class="sxs-lookup"><span data-stu-id="c9335-115">Currently, hello SDK supports</span></span>

* <span data-ttu-id="c9335-116">**Versão do Node.js: 0.10.0 ou superior**</span><span class="sxs-lookup"><span data-stu-id="c9335-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="c9335-117">**Versão da API REST para Conta: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="c9335-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="c9335-118">**Versão da API REST para FileSystem: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="c9335-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9335-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c9335-119">Prerequisites</span></span>
<span data-ttu-id="c9335-120">Antes de começar este artigo, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c9335-120">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="c9335-121">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c9335-121">**An Azure subscription**.</span></span> <span data-ttu-id="c9335-122">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9335-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c9335-123">**Criar um aplicativo do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9335-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="c9335-124">Você pode usar Olá AD do Azure tooauthenticate Olá repositório Data Lake aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9335-124">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="c9335-125">Há diferentes abordagens tooauthenticate com o AD do Azure, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**.</span><span class="sxs-lookup"><span data-stu-id="c9335-125">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="c9335-126">Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c9335-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="c9335-127">Como tooInstall</span><span class="sxs-lookup"><span data-stu-id="c9335-127">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="c9335-128">Autenticar usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9335-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="c9335-129">trechos de código Olá abaixo mostram duas maneiras diferentes de autenticação no repositório Data Lake usando o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9335-129">hello snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="c9335-130">Para obter uma discussão detalhada sobre toouse de vários métodos de autenticação com o repositório Data Lake, consulte [autenticar com o repositório Data Lake usando o Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c9335-130">For a detailed discussion on various methods toouse for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="c9335-131">trecho de saudação abaixo também exige entradas como nome de domínio do AD do Azure, ID do cliente para um aplicativo do Azure AD, etc. Todos esses detalhes podem ser recuperados de um aplicativo do AD do Azure que você deve criado, detalhes de saudação do qual também são incluídos no link acima.</span><span class="sxs-lookup"><span data-stu-id="c9335-131">hello snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, hello details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a><span data-ttu-id="c9335-132">Criar clientes de repositório Olá Data Lake</span><span class="sxs-lookup"><span data-stu-id="c9335-132">Create hello Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="c9335-133">Criar uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="c9335-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object toocreate
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
    /*err has reference toohello actual request and response, so you can see what was sent and received on hello wire.
      hello structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'hello response body if any',
        request: reference tooa stripped version of http request
        response: reference tooa stripped version of hello response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="c9335-134">Crie um arquivo com conteúdo</span><span class="sxs-lookup"><span data-stu-id="c9335-134">Create a file with content</span></span>
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

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="c9335-135">Obter uma lista de arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="c9335-135">Get a list of files and folders</span></span>
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

## <a name="see-also"></a><span data-ttu-id="c9335-136">Confira também</span><span class="sxs-lookup"><span data-stu-id="c9335-136">See also</span></span>
* [<span data-ttu-id="c9335-137">Microsoft Azure SDK para Node.js</span><span class="sxs-lookup"><span data-stu-id="c9335-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="c9335-138">SDK do Microsoft Azure para Node.js - Gerenciamento da Análise de Data Lake</span><span class="sxs-lookup"><span data-stu-id="c9335-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

