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
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a>Introdução ao Azure Data Lake Store usando o SDK do Azure para Node.js
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [SDK .NET](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [CLI 2.0 do Azure](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> Para carregar e baixar a grande quantidade de dados (arquivos grandes, um grande número de arquivos ou ambos), é recomendável que você use Olá [SDK de Python](data-lake-store-get-started-python.md), Olá [.NET SDK](data-lake-store-get-started-net-sdk.md), [CLI do Azure 2.0](data-lake-store-get-started-cli-2.0.md), ou [PowerShell do Azure](data-lake-store-get-started-powershell.md). Essas opções têm um desempenho melhor que usam vários threads tooparallelize Olá a movimentação de dados.
> 
> 

Saiba como toouse hello Azure SDK para Node.js toocreate uma conta do repositório Azure Data Lake e executar operações básicas, como criar pastas, carregar e baixar arquivos de dados, exclua sua conta, etc. Para saber mais sobre o Data Lake Store, veja [Visão geral do Data Lake Store](data-lake-store-overview.md). Atualmente, há suporte Olá SDK

* **Versão do Node.js: 0.10.0 ou superior**
* **Versão da API REST para Conta: 2015-10-01-preview**
* **Versão da API REST para FileSystem: 2015-10-01-preview**

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Criar um aplicativo do Azure Active Directory**. Você pode usar Olá AD do Azure tooauthenticate Olá repositório Data Lake aplicativo com o Azure AD. Há diferentes abordagens tooauthenticate com o AD do Azure, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**. Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).

## <a name="how-tooinstall"></a>Como tooInstall
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a>Autenticar usando o Azure Active Directory
trechos de código Olá abaixo mostram duas maneiras diferentes de autenticação no repositório Data Lake usando o Azure AD. Para obter uma discussão detalhada sobre toouse de vários métodos de autenticação com o repositório Data Lake, consulte [autenticar com o repositório Data Lake usando o Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

trecho de saudação abaixo também exige entradas como nome de domínio do AD do Azure, ID do cliente para um aplicativo do Azure AD, etc. Todos esses detalhes podem ser recuperados de um aplicativo do AD do Azure que você deve criado, detalhes de saudação do qual também são incluídos no link acima.

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a>Criar clientes de repositório Olá Data Lake
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a>Criar uma conta do Repositório Data Lake
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

## <a name="create-a-file-with-content"></a>Crie um arquivo com conteúdo
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

## <a name="get-a-list-of-files-and-folders"></a>Obter uma lista de arquivos e pastas
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

## <a name="see-also"></a>Confira também
* [Microsoft Azure SDK para Node.js](https://github.com/azure/azure-sdk-for-node)
* [SDK do Microsoft Azure para Node.js - Gerenciamento da Análise de Data Lake](https://www.npmjs.com/package/azure-arm-datalake-analytics)

