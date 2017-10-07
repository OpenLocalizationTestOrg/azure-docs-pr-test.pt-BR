---
title: "aaaManage análise Azure Data Lake usando o Azure SDK para Node.js | Microsoft Docs"
description: "Saiba como contas de análise Data Lake toomanage, fontes de dados, trabalhos e os usuários usando o Azure SDK para Node.js"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 9de1bcf4-b15b-4d0b-9284-8889ecf0c438
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 07acd058bf252af2fc98c4cfe87a135e0b79900f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-sdk-for-nodejs"></a><span data-ttu-id="af2c4-103">Gerenciar a Análise Azure Data Lake usando o SDK do Azure para Node.js</span><span class="sxs-lookup"><span data-stu-id="af2c4-103">Manage Azure Data Lake Analytics using Azure SDK for Node.js</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="af2c4-104">Hello Azure SDK para Node.js pode ser usado para gerenciar contas de análise do Azure Data Lake, trabalhos e catálogos.</span><span class="sxs-lookup"><span data-stu-id="af2c4-104">hello Azure SDK for Node.js can be used for managing Azure Data Lake Analytics accounts, jobs and catalogs.</span></span> <span data-ttu-id="af2c4-105">tópico de gerenciamento toosee usando outras ferramentas, clique em ' hello, selecione acima.</span><span class="sxs-lookup"><span data-stu-id="af2c4-105">toosee management topic using other tools, click hello tab select above.</span></span>

<span data-ttu-id="af2c4-106">Agora, ele oferece suporte a:</span><span class="sxs-lookup"><span data-stu-id="af2c4-106">Right now it supports:</span></span>

* <span data-ttu-id="af2c4-107">**Versão do Node.js: 0.10.0 ou superior**</span><span class="sxs-lookup"><span data-stu-id="af2c4-107">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="af2c4-108">**Versão da API REST para Conta: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="af2c4-108">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="af2c4-109">**Versão da API REST para Catálogo: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="af2c4-109">**REST API version for Catalog: 2015-10-01-preview**</span></span>
* <span data-ttu-id="af2c4-110">**Versão da API REST para Trabalho: 2016-03-20-preview**</span><span class="sxs-lookup"><span data-stu-id="af2c4-110">**REST API version for Job: 2016-03-20-preview**</span></span>

## <a name="features"></a><span data-ttu-id="af2c4-111">Recursos</span><span class="sxs-lookup"><span data-stu-id="af2c4-111">Features</span></span>
* <span data-ttu-id="af2c4-112">Gerenciamento de contas: criar, obter, listar, atualizar e excluir.</span><span class="sxs-lookup"><span data-stu-id="af2c4-112">Account management: create, get, list, update, and delete.</span></span>
* <span data-ttu-id="af2c4-113">Gerenciamento de trabalhos: enviar, obter, listar e cancelar.</span><span class="sxs-lookup"><span data-stu-id="af2c4-113">Job management: submit, get, list, and cancel.</span></span>
* <span data-ttu-id="af2c4-114">Gerenciamento de catálogos: obter e listar.</span><span class="sxs-lookup"><span data-stu-id="af2c4-114">Catalog management: get and list.</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="af2c4-115">Como tooInstall</span><span class="sxs-lookup"><span data-stu-id="af2c4-115">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-analytics
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="af2c4-116">Autenticar usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af2c4-116">Authenticate using Azure Active Directory</span></span>
 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-analytics-client"></a><span data-ttu-id="af2c4-117">Crie saudação do cliente de análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="af2c4-117">Create hello Data Lake Analytics client</span></span>
```javascript
var adlaManagement = require("azure-arm-datalake-analytics");
var acccountClient = new adlaManagement.DataLakeAnalyticsAccountClient(credentials, 'your-subscription-id');
var jobClient = new adlaManagement.DataLakeAnalyticsJobClient(credentials, 'azuredatalakeanalytics.net');
var catalogClient = new adlaManagement.DataLakeAnalyticsCatalogClient(credentials, 'azuredatalakeanalytics.net');
```

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="af2c4-118">Criar uma conta da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="af2c4-118">Create a Data Lake Analytics account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlaacct';
var location = 'eastus2';

// A Data Lake Store account must already have been created toocreate
// a Data Lake Analytics account. See hello Data Lake Store readme for
// information on doing so. For now, we assume one exists already.
var datalakeStoreAccountName = 'existingadlsaccount';

// account object toocreate
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location,
  properties: {
    defaultDataLakeStoreAccount: datalakeStoreAccountName,
    dataLakeStoreAccounts: [
      {
        name: datalakeStoreAccountName
      }
    ]
  }
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

## <a name="get-a-list-of-jobs"></a><span data-ttu-id="af2c4-119">Obter uma lista de trabalhos</span><span class="sxs-lookup"><span data-stu-id="af2c4-119">Get a list of jobs</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
jobClient.job.list(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="get-a-list-of-databases-in-hello-data-lake-analytics-catalog"></a><span data-ttu-id="af2c4-120">Obter uma lista de bancos de dados em Olá catálogo de análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="af2c4-120">Get a list of databases in hello Data Lake Analytics Catalog</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
catalogClient.catalog.listDatabases(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="af2c4-121">Consulte também</span><span class="sxs-lookup"><span data-stu-id="af2c4-121">See also</span></span>
* [<span data-ttu-id="af2c4-122">Microsoft Azure SDK para Node.js</span><span class="sxs-lookup"><span data-stu-id="af2c4-122">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="af2c4-123">SDK do Microsoft Azure para Node.js - Gerenciamento do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="af2c4-123">Microsoft Azure SDK for Node.js - Data Lake Store Management</span></span>](https://github.com/Azure/azure-sdk-for-node/tree/autorest/lib/services/dataLake.Store)

