---
title: Conectar um aplicativo MongoDB ao BD Cosmos do Azure usando o Node.js | Microsoft Docs
description: Saiba como conectar um aplicativo MongoDB existente do Node.js ao BD Cosmos do Azure
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: a26477d692cc98ed16c195233ade5434cc536a36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a><span data-ttu-id="ab049-103">BD Cosmos do Azure: migrar um aplicativo Web MongoDB do Node.js existente</span><span class="sxs-lookup"><span data-stu-id="ab049-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span></span> 

<span data-ttu-id="ab049-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ab049-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="ab049-105">É possível criar e consultar rapidamente documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab049-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="ab049-106">Este início rápido demonstra como usar um aplicativo [MongoDB](mongodb-introduction.md) existente escrito no Node.js e como conectá-lo ao banco de dados do BD Cosmos do Azure, que dá suporte a conexões de cliente do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ab049-106">This quickstart demonstrates how to use an existing [MongoDB](mongodb-introduction.md) app written in Node.js and connect it to your Azure Cosmos DB database, which supports MongoDB client connections.</span></span> <span data-ttu-id="ab049-107">Em outras palavras, o aplicativo Node.js só sabe que está se conectando a um banco de dados usando as APIs do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ab049-107">In other words, your Node.js application only knows that it's connecting to a database using MongoDB APIs.</span></span> <span data-ttu-id="ab049-108">Está claro para o aplicativo que os dados estão armazenados no BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab049-108">It is transparent to the application that the data is stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="ab049-109">Quando terminar, você terá um aplicativo MEAN (MongoDB, Express, AngularJS e Node.js) executando no [BD Cosmos do Azure](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="ab049-109">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> 

![Aplicativo MEAN.js em execução no Serviço de Aplicativo do Azure](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ab049-111">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ab049-111">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ab049-112">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="ab049-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="ab049-113">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ab049-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ab049-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ab049-114">Prerequisites</span></span> 
<span data-ttu-id="ab049-115">Além da CLI do Azure, você precisa do [Node.js](https://nodejs.org/) e do [Git](http://www.git-scm.com/downloads) instalados localmente para executar os comandos `npm` e `git`.</span><span class="sxs-lookup"><span data-stu-id="ab049-115">In addition to Azure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally to run `npm` and `git` commands.</span></span>

<span data-ttu-id="ab049-116">Você deve ter conhecimento prático de Node.js.</span><span class="sxs-lookup"><span data-stu-id="ab049-116">You should have working knowledge of Node.js.</span></span> <span data-ttu-id="ab049-117">Este início rápido não se destina a ajudá-lo a desenvolver aplicativos Node.js em geral.</span><span class="sxs-lookup"><span data-stu-id="ab049-117">This quickstart is not intended to help you with developing Node.js applications in general.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="ab049-118">Clonar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="ab049-118">Clone the sample application</span></span>

<span data-ttu-id="ab049-119">Abra uma janela de terminal do Git, como git bash, e `cd` para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ab049-119">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

<span data-ttu-id="ab049-120">Execute os comandos a seguir para clonar o repositório de exemplo.</span><span class="sxs-lookup"><span data-stu-id="ab049-120">Run the following commands to clone the sample repository.</span></span> <span data-ttu-id="ab049-121">Esse repositório de exemplo contém o aplicativo [MEAN.js](http://meanjs.org/) padrão.</span><span class="sxs-lookup"><span data-stu-id="ab049-121">This sample repository contains the default [MEAN.js](http://meanjs.org/) application.</span></span> 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-the-application"></a><span data-ttu-id="ab049-122">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="ab049-122">Run the application</span></span>

<span data-ttu-id="ab049-123">Instale os pacotes necessários e inicie o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab049-123">Install the required packages and start the application.</span></span>

```bash
cd mean
npm install
npm start
```

## <a name="log-in-to-azure"></a><span data-ttu-id="ab049-124">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="ab049-124">Log in to Azure</span></span>

<span data-ttu-id="ab049-125">Se você estiver usando uma CLI do Azure instalada, faça logon na sua assinatura do Azure com o comando [az login](/cli/azure/#login) e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="ab049-125">If you are using an installed Azure CLI, log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> <span data-ttu-id="ab049-126">Você poderá ignorar esta etapa se estiver usando o Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="ab049-126">You can skip this step if you're using the Azure Cloud Shell.</span></span>

```azurecli
az login 
``` 
   
## <a name="add-the-azure-cosmos-db-module"></a><span data-ttu-id="ab049-127">Adicione o módulo do BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="ab049-127">Add the Azure Cosmos DB module</span></span>

<span data-ttu-id="ab049-128">Se você estiver usando uma CLI do Azure instalada, verifique se o componente `cosmosdb` já está instalado ao executar o comando `az`.</span><span class="sxs-lookup"><span data-stu-id="ab049-128">If you are using an installed Azure CLI, check to see if the `cosmosdb` component is already installed by running the `az` command.</span></span> <span data-ttu-id="ab049-129">Se `cosmosdb` estiver na lista de comandos básicos, vá para o próximo comando.</span><span class="sxs-lookup"><span data-stu-id="ab049-129">If `cosmosdb` is in the list of base commands, proceed to the next command.</span></span> <span data-ttu-id="ab049-130">Você poderá ignorar esta etapa se estiver usando o Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="ab049-130">You can skip this step if you're using the Azure Cloud Shell.</span></span>

<span data-ttu-id="ab049-131">Se `cosmosdb` não estiver na lista de comandos base, reinstale a [CLI do Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ab049-131">If `cosmosdb` is not in the list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="ab049-132">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ab049-132">Create a resource group</span></span>

<span data-ttu-id="ab049-133">Crie um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) com o [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ab049-133">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ab049-134">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure, como os aplicativos Web, bancos de dados e contas de armazenamento, são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ab049-134">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="ab049-135">O exemplo a seguir cria um grupo de recursos na região da Europa Ocidental.</span><span class="sxs-lookup"><span data-stu-id="ab049-135">The following example creates a resource group in the West Europe region.</span></span> <span data-ttu-id="ab049-136">Escolha um nome exclusivo para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ab049-136">Choose a unique name for the resource group.</span></span>

<span data-ttu-id="ab049-137">Se você estiver usando o Azure Cloud Shell, clique em **Experimente**, siga as instruções na tela para fazer logon e copie o comando para o prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="ab049-137">If you are using Azure Cloud Shell, click **Try It**, follow the onscreen prompts to login, then copy the command into the command prompt.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="ab049-138">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ab049-138">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="ab049-139">Crie uma conta do BD Cosmos do Azure usando o comando [az cosmosdb create](/cli/azure/cosmosdb#create).</span><span class="sxs-lookup"><span data-stu-id="ab049-139">Create an Azure Cosmos DB account with the [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="ab049-140">No comando a seguir, substitua seu próprio nome de conta exclusivo do BD Cosmos do Azure quando vir o espaço reservado `<cosmosdb-name>`.</span><span class="sxs-lookup"><span data-stu-id="ab049-140">In the following command, please substitute your own unique Azure Cosmos DB account name where you see the `<cosmosdb-name>` placeholder.</span></span> <span data-ttu-id="ab049-141">Esse nome exclusivo será usado como parte de seu ponto de extremidade do BD Cosmos do Azure (`https://<cosmosdb-name>.documents.azure.com/`), portanto, o nome precisa ser exclusivo em todas as contas do BD Cosmos do Azure no Azure.</span><span class="sxs-lookup"><span data-stu-id="ab049-141">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so the name needs to be unique across all Azure Cosmos DB accounts in Azure.</span></span> 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="ab049-142">O parâmetro `--kind MongoDB` habilita conexões do cliente MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ab049-142">The `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="ab049-143">Quando a conta do BD Cosmos do Azure é criada, a CLI do Azure mostra informações semelhantes ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ab049-143">When the Azure Cosmos DB account is created, the Azure CLI shows information similar to the following example.</span></span> 

> [!NOTE]
> <span data-ttu-id="ab049-144">Este exemplo usa JSON como o formato de saída da CLI do Azure, que é o padrão.</span><span class="sxs-lookup"><span data-stu-id="ab049-144">This example uses JSON as the Azure CLI output format, which is the default.</span></span> <span data-ttu-id="ab049-145">Para usar outro formato de saída, consulte [Formatos de saída para comandos da CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ab049-145">To use another output format, see [Output formats for Azure CLI 2.0 commands](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span></span>

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-to-the-database"></a><span data-ttu-id="ab049-146">Conectar o aplicativo Node.js ao banco de dados</span><span class="sxs-lookup"><span data-stu-id="ab049-146">Connect your Node.js application to the database</span></span>

<span data-ttu-id="ab049-147">Nesta etapa, você conecta o aplicativo de exemplo MEAN.js ao BD Cosmos do Azure que acabou de ser criado usando uma cadeia de conexão do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ab049-147">In this step, you connect your MEAN.js sample application to an Azure Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

<a name="devconfig"></a>
## <a name="configure-the-connection-string-in-your-nodejs-application"></a><span data-ttu-id="ab049-148">Configurar a cadeia de conexão em seu aplicativo Node.js</span><span class="sxs-lookup"><span data-stu-id="ab049-148">Configure the connection string in your Node.js application</span></span>

<span data-ttu-id="ab049-149">No seu repositório MEAN.js abra `config/env/local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="ab049-149">In your MEAN.js repository, open `config/env/local-development.js`.</span></span>

<span data-ttu-id="ab049-150">Substitua o conteúdo deste arquivo pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="ab049-150">Replace the content of this file with the following code.</span></span> <span data-ttu-id="ab049-151">Substitua também os dois espaços reservados `<cosmosdb-name>` com seu nome de conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ab049-151">Be sure to also replace the two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span></span>

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-the-key"></a><span data-ttu-id="ab049-152">Recuperar a chave</span><span class="sxs-lookup"><span data-stu-id="ab049-152">Retrieve the key</span></span>

<span data-ttu-id="ab049-153">Para se conectar ao BD Cosmos do Azure, você precisa da chave do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ab049-153">In order to connect to an Azure Cosmos DB database, you need the database key.</span></span> <span data-ttu-id="ab049-154">Use o comando [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) para recuperar a chave primária.</span><span class="sxs-lookup"><span data-stu-id="ab049-154">Use the [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command to retrieve the primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

<span data-ttu-id="ab049-155">A CLI do Azure emite informações semelhantes ao seguinte exemplo.</span><span class="sxs-lookup"><span data-stu-id="ab049-155">The Azure CLI outputs information similar to the following example.</span></span> 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

<span data-ttu-id="ab049-156">Copie o valor de `primaryMasterKey`.</span><span class="sxs-lookup"><span data-stu-id="ab049-156">Copy the value of `primaryMasterKey`.</span></span> <span data-ttu-id="ab049-157">Cole isso no `<primary_master_key>` em `local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="ab049-157">Paste this over the  `<primary_master_key>` in `local-development.js`.</span></span>

<span data-ttu-id="ab049-158">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="ab049-158">Save your changes.</span></span>

### <a name="run-the-application-again"></a><span data-ttu-id="ab049-159">Execute o aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="ab049-159">Run the application again.</span></span>

<span data-ttu-id="ab049-160">Execute `npm start` novamente.</span><span class="sxs-lookup"><span data-stu-id="ab049-160">Run `npm start` again.</span></span> 

```bash
npm start
```

<span data-ttu-id="ab049-161">Agora, uma mensagem de console deve informar que o ambiente de desenvolvimento está em execução.</span><span class="sxs-lookup"><span data-stu-id="ab049-161">A console message should now tell you that the development environment is up and running.</span></span> 

<span data-ttu-id="ab049-162">Navegue até `http://localhost:3000` em um navegador.</span><span class="sxs-lookup"><span data-stu-id="ab049-162">Navigate to `http://localhost:3000` in a browser.</span></span> <span data-ttu-id="ab049-163">Clique em **Inscrever-se** no menu superior e tente criar dois usuários fictícios.</span><span class="sxs-lookup"><span data-stu-id="ab049-163">Click **Sign Up** in the top menu and try to create two dummy users.</span></span> 

<span data-ttu-id="ab049-164">O aplicativo de exemplo MEAN.js armazena dados do usuário no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ab049-164">The MEAN.js sample application stores user data in the database.</span></span> <span data-ttu-id="ab049-165">Se você tiver êxito e o MEAN.js entrar automaticamente no usuário criado, então a conexão do BD Cosmos do Azure estará funcionando.</span><span class="sxs-lookup"><span data-stu-id="ab049-165">If you are successful and MEAN.js automatically signs into the created user, then your Azure Cosmos DB connection is working.</span></span> 

![O MEAN.js conecta-se com êxito ao MongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a><span data-ttu-id="ab049-167">Exibir dados no Data Explorer</span><span class="sxs-lookup"><span data-stu-id="ab049-167">View data in Data Explorer</span></span>

<span data-ttu-id="ab049-168">Os dados armazenados pelo BD Cosmos do Azure estão disponíveis para exibir, consultar e executar a lógica de negócios no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab049-168">Data stored by an Azure Cosmos DB is available to view, query, and run business-logic on in the Azure portal.</span></span>

<span data-ttu-id="ab049-169">Para exibir, consultar e trabalhar com os dados de usuário criados na etapa anterior, faça logon no [portal do Azure](https://portal.azure.com) no seu navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="ab049-169">To view, query, and work with the user data created in the previous step, login to the [Azure portal](https://portal.azure.com) in your web browser.</span></span>

<span data-ttu-id="ab049-170">Na caixa de pesquisa superior, digite BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab049-170">In the top Search box, type Azure Cosmos DB.</span></span> <span data-ttu-id="ab049-171">Quando a folha de conta do BD Cosmos abrir, selecione sua conta do BD Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ab049-171">When your Cosmos DB account blade opens, select your Cosmos DB account.</span></span> <span data-ttu-id="ab049-172">No painel de navegação esquerdo, clique em Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="ab049-172">In the left navigation, click Data Explorer.</span></span> <span data-ttu-id="ab049-173">Expanda a coleção no painel Coleções e, em seguida, será possível exibir os documentos na coleção, consultar os dados e até mesmo criar e executar gatilhos, UDFs e procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="ab049-173">Expand your collection in the Collections pane, and then you can view the documents in the collection, query the data, and even create and run stored procedures, triggers, and UDFs.</span></span> 

![Data Explorer no Portal do Azure](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-the-nodejs-application-to-azure"></a><span data-ttu-id="ab049-175">Implantar o aplicativo Node.js no Azure</span><span class="sxs-lookup"><span data-stu-id="ab049-175">Deploy the Node.js application to Azure</span></span>

<span data-ttu-id="ab049-176">Nessa etapa, você implanta seu aplicativo Node.js conectado ao MongoDB no BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab049-176">In this step, you deploy your MongoDB-connected Node.js application to Azure Cosmos DB.</span></span>

<span data-ttu-id="ab049-177">Você talvez tenha notado que o arquivo de configuração alterado anteriormente é voltado para o ambiente de desenvolvimento (`/config/env/local-development.js`).</span><span class="sxs-lookup"><span data-stu-id="ab049-177">You may have noticed that the configuration file that you changed earlier is for the development environment (`/config/env/local-development.js`).</span></span> <span data-ttu-id="ab049-178">Quando você implanta seu aplicativo no Serviço de Aplicativo, ele será executado no ambiente de produção por padrão.</span><span class="sxs-lookup"><span data-stu-id="ab049-178">When you deploy your application to App Service, it will run in the production environment by default.</span></span> <span data-ttu-id="ab049-179">Agora, você precisa fazer a mesma alteração no arquivo de configuração respectivo.</span><span class="sxs-lookup"><span data-stu-id="ab049-179">So now, you need to make the same change to the respective configuration file.</span></span>

<span data-ttu-id="ab049-180">No seu repositório MEAN.js abra `config/env/production.js`.</span><span class="sxs-lookup"><span data-stu-id="ab049-180">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="ab049-181">No objeto `db`, substitua o valor de `uri` conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ab049-181">In the `db` object, replace the value of `uri` as show in the following example.</span></span> <span data-ttu-id="ab049-182">Certifique-se de substituir os espaços reservados como antes.</span><span class="sxs-lookup"><span data-stu-id="ab049-182">Be sure to replace the placeholders as before.</span></span>

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> <span data-ttu-id="ab049-183">A opção `ssl=true` é importante porque o [BD Cosmos do Azure requer SSL](connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="ab049-183">The `ssl=true` option is important because [Azure Cosmos DB requires SSL](connect-mongodb-account.md#connection-string-requirements).</span></span> 
>
>

<span data-ttu-id="ab049-184">No terminal, confirme todas as alterações no Git.</span><span class="sxs-lookup"><span data-stu-id="ab049-184">In the terminal, commit all your changes into Git.</span></span> <span data-ttu-id="ab049-185">É possível copiar ambos os comandos para os executar juntos.</span><span class="sxs-lookup"><span data-stu-id="ab049-185">You can copy both commands to run them together.</span></span>

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a><span data-ttu-id="ab049-186">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="ab049-186">Clean up resources</span></span>

<span data-ttu-id="ab049-187">Se você não continuar usando este aplicativo, exclua todos os recursos criados por esse início rápido no portal do Azure com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ab049-187">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="ab049-188">No menu à esquerda no Portal do Azure, clique em **Grupos de recursos** e depois clique no nome do recurso criado.</span><span class="sxs-lookup"><span data-stu-id="ab049-188">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="ab049-189">Em sua página de grupo de recursos, clique em **Excluir**, digite o nome do recurso para excluir na caixa de texto e depois clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="ab049-189">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab049-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab049-190">Next steps</span></span>

<span data-ttu-id="ab049-191">Neste início rápido, você aprendeu como criar uma conta do BD Cosmos do Azure e como criar uma coleção do MongoDB usando o Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="ab049-191">In this quickstart, you've learned how to create an Azure Cosmos DB account and create a MongoDB collection using the Data Explorer.</span></span> <span data-ttu-id="ab049-192">Agora, é possível migrar os dados do MongoDB para o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab049-192">You can now migrate your MongoDB data to Azure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab049-193">Importar dados do MongoDB no BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="ab049-193">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
