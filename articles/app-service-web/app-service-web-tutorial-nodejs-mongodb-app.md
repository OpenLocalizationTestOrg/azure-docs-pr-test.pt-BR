---
title: Compilar um aplicativo Web Node.js e MongoDB no Azure | Microsoft Docs
description: "Saiba como fazer com que um aplicativo Node.js funcione no Azure, com conexão a um BD Cosmos com uma cadeia de conexão MongoDB."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3b309382be8cdf8d48b396207fd482a5dc5ed934
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="4cd17-103">Compilar um aplicativo Web Node.js e MongoDB no Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="4cd17-104">Os aplicativos Web do Azure fornecem um serviço de hospedagem na Web altamente escalonável, com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="4cd17-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="4cd17-105">Este tutorial mostra como criar um aplicativo Web Node.js no Azure e conectá-lo a um banco de dados MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4cd17-105">This tutorial shows how to create a Node.js web app in Azure and connect it to a MongoDB database.</span></span> <span data-ttu-id="4cd17-106">Quando terminar, você terá um aplicativo MEAN (MongoDB, Express, AngularJS e Node.js) executando em [Serviço de Aplicativo do Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4cd17-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="4cd17-107">Para simplificar, o aplicativo de exemplo usa a [estrutura Web MEAN.js](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="4cd17-107">For simplicity, the sample application uses the [MEAN.js web framework](http://meanjs.org/).</span></span>

![Aplicativo MEAN.js em execução no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="4cd17-109">O que você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="4cd17-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4cd17-110">Criar um banco de dados MongoDB no Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="4cd17-111">Conectar um aplicativo Node.js ao MongoDB</span><span class="sxs-lookup"><span data-stu-id="4cd17-111">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="4cd17-112">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-112">Deploy the app to Azure</span></span>
> * <span data-ttu-id="4cd17-113">Atualizar o modelo de dados e reimplantar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="4cd17-113">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="4cd17-114">Transmitir logs de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="4cd17-115">Gerenciar o aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-115">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4cd17-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4cd17-116">Prerequisites</span></span>

<span data-ttu-id="4cd17-117">Para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="4cd17-117">To complete this tutorial:</span></span>

1. [<span data-ttu-id="4cd17-118">Instalar o Git</span><span class="sxs-lookup"><span data-stu-id="4cd17-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="4cd17-119">Instalar o Node.js e o NPM</span><span class="sxs-lookup"><span data-stu-id="4cd17-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="4cd17-120">[Instale o Gulp.js](http://gulpjs.com/) (exigido pelo [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span><span class="sxs-lookup"><span data-stu-id="4cd17-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="4cd17-121">Instale e execute o MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="4cd17-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4cd17-122">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4cd17-122">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4cd17-123">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="4cd17-123">Run `az --version` to find the version.</span></span> <span data-ttu-id="4cd17-124">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4cd17-124">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="4cd17-125">Testar o MongoDB local</span><span class="sxs-lookup"><span data-stu-id="4cd17-125">Test local MongoDB</span></span>

<span data-ttu-id="4cd17-126">Abra a janela do terminal e `cd` para o `bin` diretório da instalação do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4cd17-126">Open the terminal window and `cd` to the `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="4cd17-127">Você pode usar essa janela do terminal para executar todos os comandos deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="4cd17-127">You can use this terminal window to run all the commands in this tutorial.</span></span>

<span data-ttu-id="4cd17-128">Execute `mongo` no terminal para se conectar ao servidor do MongoDB local.</span><span class="sxs-lookup"><span data-stu-id="4cd17-128">Run `mongo` in the terminal to connect to your local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="4cd17-129">Se sua conexão tiver êxito, então seu banco de dados MongoDB já está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="4cd17-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="4cd17-130">Caso contrário, certifique-se de que seu banco de dados MongoDB local foi iniciado seguindo as etapas em [Instale o MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="4cd17-130">If not, make sure that your local MongoDB database is started by following the steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="4cd17-131">Com frequência, o MongoDB está instalado, mas você ainda precisa iniciá-lo executando `mongod`.</span><span class="sxs-lookup"><span data-stu-id="4cd17-131">Often, MongoDB is installed, but you still need to start it by running `mongod`.</span></span> 

<span data-ttu-id="4cd17-132">Ao terminar o teste do seu banco de dados MongoDB, digite `Ctrl+C` no terminal.</span><span class="sxs-lookup"><span data-stu-id="4cd17-132">When you're done testing your MongoDB database, type `Ctrl+C` in the terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="4cd17-133">Criar aplicativo Node.js local</span><span class="sxs-lookup"><span data-stu-id="4cd17-133">Create local Node.js app</span></span>

<span data-ttu-id="4cd17-134">Nessa etapa, você configura o projeto Node.js local.</span><span class="sxs-lookup"><span data-stu-id="4cd17-134">In this step, you set up the local Node.js project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="4cd17-135">Clonar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="4cd17-135">Clone the sample application</span></span>

<span data-ttu-id="4cd17-136">Na janela do terminal, `cd` para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="4cd17-136">In the terminal window, `cd` to a working directory.</span></span>  

<span data-ttu-id="4cd17-137">Execute o comando a seguir para clonar o repositório de exemplo.</span><span class="sxs-lookup"><span data-stu-id="4cd17-137">Run the following command to clone the sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="4cd17-138">Esse repositório de exemplo contém uma cópia do [repositório do MEAN.js](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="4cd17-138">This sample repository contains a copy of the [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="4cd17-139">Ele é modificado para ser executado no Serviço de Aplicativo (para obter mais informações, consulte o [arquivo LEIAME](https://github.com/Azure-Samples/meanjs/blob/master/README.md) do repositório do MEAN.js).</span><span class="sxs-lookup"><span data-stu-id="4cd17-139">It is modified to run on App Service (for more information, see the MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-the-application"></a><span data-ttu-id="4cd17-140">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="4cd17-140">Run the application</span></span>

<span data-ttu-id="4cd17-141">Execute os seguintes comandos para instalar os pacotes necessários e iniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4cd17-141">Run the following commands to install the required packages and start the application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="4cd17-142">Quando o aplicativo estiver totalmente carregado, você verá algo semelhante à seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="4cd17-142">When the app is fully loaded, you see something similar to the following message:</span></span>

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

<span data-ttu-id="4cd17-143">Navegue até http://localhost:3000 em um navegador.</span><span class="sxs-lookup"><span data-stu-id="4cd17-143">Navigate to http://localhost:3000 in a browser.</span></span> <span data-ttu-id="4cd17-144">Clique em **Criar Conta** no menu superior e crie um usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="4cd17-144">Click **Sign Up** in the top menu and create a test user.</span></span> 

<span data-ttu-id="4cd17-145">O aplicativo de exemplo MEAN.js armazena dados do usuário no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4cd17-145">The MEAN.js sample application stores user data in the database.</span></span> <span data-ttu-id="4cd17-146">Se tiver êxito na criação de um usuário e ao entrar, seu aplicativo estará gravando dados no banco de dados local MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4cd17-146">If you are successful at creating a user and signing in, then your app is writing data to the local MongoDB database.</span></span>

![O MEAN.js conecta-se com êxito ao MongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="4cd17-148">Selecione **Admin > Gerenciar Artigos** para adicionar alguns artigos.</span><span class="sxs-lookup"><span data-stu-id="4cd17-148">Select **Admin > Manage Articles** to add some articles.</span></span>

<span data-ttu-id="4cd17-149">Para parar o Node.js a qualquer momento, pressione `Ctrl+C` no terminal.</span><span class="sxs-lookup"><span data-stu-id="4cd17-149">To stop Node.js at any time, press `Ctrl+C` in the terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="4cd17-150">Criar MongoDB de produção</span><span class="sxs-lookup"><span data-stu-id="4cd17-150">Create production MongoDB</span></span>

<span data-ttu-id="4cd17-151">Ness etapa, você cria um banco de dados MongoDB no Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="4cd17-152">Quando seu aplicativo é implantado no Azure, ele usa esse banco de dados na nuvem.</span><span class="sxs-lookup"><span data-stu-id="4cd17-152">When your app is deployed to Azure, it uses this cloud database.</span></span>

<span data-ttu-id="4cd17-153">Para o MongoDB, este tutorial usa o [BD Cosmos do Azure](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="4cd17-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="4cd17-154">O BD Cosmos dá suporte a conexões de cliente do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4cd17-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="4cd17-155">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-155">Log in to Azure</span></span>

<span data-ttu-id="4cd17-156">Você usará a CLI do Azure 2.0 para criar os recursos necessários para hospedar seu aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-156">You'll use the Azure CLI 2.0 to create the resources needed to host your app in Azure.</span></span> <span data-ttu-id="4cd17-157">Faça logon na sua assinatura do Azure com o comando [az login](/cli/azure/#login) e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="4cd17-157">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="4cd17-158">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="4cd17-158">Create a resource group</span></span>

<span data-ttu-id="4cd17-159">Crie um grupo de recursos com o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4cd17-159">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="4cd17-160">O exemplo a seguir cria um grupo de recursos na região da Europa Ocidental.</span><span class="sxs-lookup"><span data-stu-id="4cd17-160">The following example creates a resource group in the West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="4cd17-161">Use o comando CLI do Azure [az appservice list-locations](/cli/azure/appservice#list-locations) para listar os locais disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4cd17-161">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="4cd17-162">Criar uma conta do BD Cosmos</span><span class="sxs-lookup"><span data-stu-id="4cd17-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="4cd17-163">Crie uma conta do BD Cosmos usando o comando [az cosmosdb create](/cli/azure/cosmosdb#create).</span><span class="sxs-lookup"><span data-stu-id="4cd17-163">Create a Cosmos DB account with the [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="4cd17-164">No comando a seguir, substitua um nome do Cosmos DB exclusivo quando vir o espaço reservado *\<cosmosdb_name>*.</span><span class="sxs-lookup"><span data-stu-id="4cd17-164">In the following command, substitute a unique Cosmos DB name for the *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="4cd17-165">Esse nome exclusivo é usado como parte do seu ponto de extremidade do Cosmos DB, `https://<cosmosdb_name>.documents.azure.com/`, portanto, o nome precisa ser exclusivo em todas as contas do Cosmos DB no Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-165">This name is used as the part of the Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so the name needs to be unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="4cd17-166">O nome deve conter somente letras minúsculas, números e o caractere hífen (-), e deve ter entre 3 e 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="4cd17-166">The name must contain only lowercase letters, numbers, and the hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="4cd17-167">O parâmetro *--kind MongoDB* habilita conexões do cliente MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4cd17-167">The *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="4cd17-168">Quando a conta do BD Cosmos é criada, a CLI do Azure mostra informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cd17-168">When the Cosmos DB account is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-to-production-mongodb"></a><span data-ttu-id="4cd17-169">Conectar o aplicativo ao MongoDB de produção</span><span class="sxs-lookup"><span data-stu-id="4cd17-169">Connect app to production MongoDB</span></span>

<span data-ttu-id="4cd17-170">Nesta etapa, você conecta o aplicativo de exemplo MEAN.js ao BD Cosmos que acabou de ser criado usando uma cadeia de conexão do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4cd17-170">In this step, you connect your MEAN.js sample application to the Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-the-database-key"></a><span data-ttu-id="4cd17-171">Recuperar a chave do banco de dados</span><span class="sxs-lookup"><span data-stu-id="4cd17-171">Retrieve the database key</span></span>

<span data-ttu-id="4cd17-172">Para se conectar ao BD Cosmos, você precisa da chave do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4cd17-172">To connect to the Cosmos DB database, you need the database key.</span></span> <span data-ttu-id="4cd17-173">Use o comando [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) para recuperar a chave primária.</span><span class="sxs-lookup"><span data-stu-id="4cd17-173">Use the [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command to retrieve the primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="4cd17-174">A CLI do Azure apresenta as informações semelhantes ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="4cd17-174">The Azure CLI shows information similar to the following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Copie o valor de `primaryMasterKey`. <span data-ttu-id="4cd17-176">Essas informações serão necessárias na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="4cd17-176">You need this information in the next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-the-connection-string-in-your-nodejs-application"></a><span data-ttu-id="4cd17-177">Configurar a cadeia de conexão em seu aplicativo Node.js</span><span class="sxs-lookup"><span data-stu-id="4cd17-177">Configure the connection string in your Node.js application</span></span>

<span data-ttu-id="4cd17-178">Em seu repositório do MEAN.js, abra _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="4cd17-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="4cd17-179">No objeto `db`, atualize o valor de `uri`:</span><span class="sxs-lookup"><span data-stu-id="4cd17-179">In the `db` object, update the value of `uri`:</span></span>

* <span data-ttu-id="4cd17-180">Substitua os dois espaços reservados  *\<cosmosdb_name >* com seu nome do banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4cd17-180">Replace the two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="4cd17-181">Substitua o espaço reservado  *\<primary_master_key >* pela chave que você copiou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="4cd17-181">Replace the *\<primary_master_key>* placeholder with the key you copied in the previous step.</span></span>

<span data-ttu-id="4cd17-182">O código a seguir mostra o objeto `db`:</span><span class="sxs-lookup"><span data-stu-id="4cd17-182">The following code shows the `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="4cd17-183">A opção `ssl=true` é necessária porque o [Cosmos DB requer SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="4cd17-183">The `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="4cd17-184">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="4cd17-184">Save your changes.</span></span>

### <a name="test-the-application-in-production-mode"></a><span data-ttu-id="4cd17-185">Testar o aplicativo em modo de produção</span><span class="sxs-lookup"><span data-stu-id="4cd17-185">Test the application in production mode</span></span> 

<span data-ttu-id="4cd17-186">Execute o seguinte comando para reduzir e agrupar scripts para o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4cd17-186">Run the following command to minify and bundle scripts for the production environment.</span></span> <span data-ttu-id="4cd17-187">Esse processo gera os arquivos necessários para o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4cd17-187">This process generates the files needed by the production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="4cd17-188">Execute o seguinte comando para usar a cadeia de conexão configurada em _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="4cd17-188">Run the following command to use the connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="4cd17-189">`NODE_ENV=production` define a variável de ambiente que informa o Node. js a ser executado no ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4cd17-189">`NODE_ENV=production` sets the environment variable that tells Node.js to run in the production environment.</span></span>  <span data-ttu-id="4cd17-190">`node server.js` inicia o servidor Node.js com `server.js` na raiz do repositório.</span><span class="sxs-lookup"><span data-stu-id="4cd17-190">`node server.js` starts the Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="4cd17-191">É dessa forma que o aplicativo Node.js é carregado no Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="4cd17-192">Quando o aplicativo for carregado, verifique se ele está sendo executado no ambiente de produção:</span><span class="sxs-lookup"><span data-stu-id="4cd17-192">When the app is loaded, check to make sure that it's running in the production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="4cd17-193">Navegue até http://localhost:8443 em um navegador.</span><span class="sxs-lookup"><span data-stu-id="4cd17-193">Navigate to http://localhost:8443 in a browser.</span></span> <span data-ttu-id="4cd17-194">Clique em **Criar Conta** no menu superior e crie um usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="4cd17-194">Click **Sign Up** in the top menu and create a test user.</span></span> <span data-ttu-id="4cd17-195">Se tiver êxito na criação de um usuário e ao entrar, seu aplicativo estará gravando dados no banco de dados do Cosmos DB no Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-195">If you are successful creating a user and signing in, then your app is writing data to the Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="4cd17-196">No terminal, pare o Node.js digitando `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="4cd17-196">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-to-azure"></a><span data-ttu-id="4cd17-197">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-197">Deploy app to Azure</span></span>

<span data-ttu-id="4cd17-198">Nessa etapa, você implanta seu aplicativo Node.js conectado ao MongoDB no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-198">In this step, you deploy your MongoDB-connected Node.js application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="4cd17-199">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="4cd17-199">Create an App Service plan</span></span>

<span data-ttu-id="4cd17-200">Criar um plano do Serviço de Aplicativo com o comando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="4cd17-200">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="4cd17-201">O exemplo a seguir cria um Plano do Serviço de Aplicativo chamado _myAppServicePlan_ usando o tipo de preço **GRATUITO**:</span><span class="sxs-lookup"><span data-stu-id="4cd17-201">The following example creates an App Service plan named _myAppServicePlan_ using the **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="4cd17-202">Quando o Plano do Serviço de Aplicativo é criado, a CLI do Azure mostra informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cd17-202">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a><span data-ttu-id="4cd17-203">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="4cd17-203">Create a web app</span></span>

<span data-ttu-id="4cd17-204">Crie um aplicativo Web no `myAppServicePlan` plano do Serviço de Aplicativo com o comando [az webapp create](/cli/azure/webapp#create).</span><span class="sxs-lookup"><span data-stu-id="4cd17-204">Create a web app in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="4cd17-205">O aplicativo Web fornece um espaço de hospedagem para implantar seu código e fornecer uma URL para exibir o aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="4cd17-205">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="4cd17-206">Use para criar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="4cd17-206">Use  to create the web app.</span></span> 

<span data-ttu-id="4cd17-207">No seguinte comando, substitua o espaço reservado *\<app_name>* por um nome de aplicativo exclusivo.</span><span class="sxs-lookup"><span data-stu-id="4cd17-207">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="4cd17-208">Esse nome é usado como parte da URL padrão para o aplicativo Web, portanto, o nome precisa ser exclusivo em todos os aplicativos no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-208">This name is used as the part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="4cd17-209">Quando o aplicativo Web tiver sido criado, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cd17-209">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-an-environment-variable"></a><span data-ttu-id="4cd17-210">Configurar um variável de ambiente</span><span class="sxs-lookup"><span data-stu-id="4cd17-210">Configure an environment variable</span></span>

<span data-ttu-id="4cd17-211">Anteriormente no tutorial, você codificou a cadeia de conexão de banco de dados em _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="4cd17-211">Earlier in the tutorial, you hardcoded the database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="4cd17-212">De acordo com as melhores práticas de segurança, você deseja manter esses dados confidenciais fora do seu repositório Git.</span><span class="sxs-lookup"><span data-stu-id="4cd17-212">In keeping with security best practice, you want to keep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="4cd17-213">Para seu aplicativo em execução no Azure, você usará uma variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="4cd17-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="4cd17-214">No Serviço de Aplicativo, defina as variáveis de ambiente como _configurações do aplicativo_ usando o comando [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update).</span><span class="sxs-lookup"><span data-stu-id="4cd17-214">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="4cd17-215">O exemplo a seguir permite definir uma configuração de aplicativo `MONGODB_URI` no seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-215">The following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="4cd17-216">Substitua os espaços reservados  *\<app_name >*,  *\<cosmosdb_name >* e  *\<primary_master_key >*.</span><span class="sxs-lookup"><span data-stu-id="4cd17-216">Replace the *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="4cd17-217">No código Node.js, você acessa essa configuração de aplicativo com `process.env.MONGODB_URI`, assim como você teria acesso a qualquer variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="4cd17-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="4cd17-218">Agora, desfaça as alterações em _config/env/production.js_ com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4cd17-218">Now, undo your changes to _config/env/production.js_ with the following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="4cd17-219">Abra _config/env/production.js_ novamente.</span><span class="sxs-lookup"><span data-stu-id="4cd17-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="4cd17-220">Observe que o aplicativo MEAN.js padrão já está configurado para usar a variável de ambiente `MONGODB_URI` que você criou.</span><span class="sxs-lookup"><span data-stu-id="4cd17-220">Note that the default MEAN.js app is already configured to use the `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="4cd17-221">Configurar a implantação do git local</span><span class="sxs-lookup"><span data-stu-id="4cd17-221">Configure local git deployment</span></span> 

<span data-ttu-id="4cd17-222">Use o comando [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) para criar credenciais de implantação.</span><span class="sxs-lookup"><span data-stu-id="4cd17-222">Use the [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command to create credentials for deployment.</span></span>

<span data-ttu-id="4cd17-223">É possível implantar seu aplicativo no Serviço de Aplicativo do Azure de várias maneiras, incluindo FTP, Git local, GitHub, Visual Studio Team Services e BitBucket.</span><span class="sxs-lookup"><span data-stu-id="4cd17-223">You can deploy your application to Azure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="4cd17-224">Para o FTP e o Git local, é necessário ter um usuário de implantação configurado no servidor para autenticar sua implantação.</span><span class="sxs-lookup"><span data-stu-id="4cd17-224">For FTP and local Git, it is necessary to have a deployment user configured on the server to authenticate your deployment.</span></span> <span data-ttu-id="4cd17-225">Este usuário de implantação está no nível de conta e é diferente da sua conta de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="4cd17-226">É necessário configurar esse usuário de implantação somente uma vez.</span><span class="sxs-lookup"><span data-stu-id="4cd17-226">You only need to configure this deployment user once.</span></span>

<span data-ttu-id="4cd17-227">No comando a seguir, substitua *\<nome-de-usuário>* e *\<senha >* por um novo nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="4cd17-227">In the following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="4cd17-228">O nome do usuário deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="4cd17-228">The user name must be unique.</span></span> <span data-ttu-id="4cd17-229">A senha deve ter pelo menos oito caracteres, com dois destes três elementos: letras, números, símbolos.</span><span class="sxs-lookup"><span data-stu-id="4cd17-229">The password must be at least eight characters long, with two of the following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="4cd17-230">Se receber um erro ` 'Conflict'. Details: 409`, altere o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="4cd17-230">If you get a ` 'Conflict'. Details: 409` error, change the username.</span></span> <span data-ttu-id="4cd17-231">Se receber um erro ` 'Bad Request'. Details: 400`, use uma senha mais forte.</span><span class="sxs-lookup"><span data-stu-id="4cd17-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="4cd17-232">Registre o nome de usuário e senha para uso em etapas posteriores quando você implantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4cd17-232">Record the user name and password for use in later steps when you deploy the app.</span></span>

<span data-ttu-id="4cd17-233">Use o comando [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) para configurar o acesso do Git local ao aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-233">Use the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command to configure local Git access to the Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="4cd17-234">Quando o usuário de implantação é configurado, a CLI do Azure mostra a URL de implantação ao seu aplicativo Web Azure no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="4cd17-234">When the deployment user is configured, the Azure CLI shows the deployment URL for your Azure web app in the following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="4cd17-235">Copie a saída do terminal, pois ela será usada na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="4cd17-235">Copy the output from the terminal, as it will be used in the next step.</span></span> 

### <a name="push-to-azure-from-git"></a><span data-ttu-id="4cd17-236">Enviar do Git para o Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-236">Push to Azure from Git</span></span>

<span data-ttu-id="4cd17-237">Adicione um Azure remoto ao seu repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="4cd17-237">Add an Azure remote to your local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="4cd17-238">Envie para o Azure remoto para implantar seu aplicativo Node.js.</span><span class="sxs-lookup"><span data-stu-id="4cd17-238">Push to the Azure remote to deploy your Node.js application.</span></span> <span data-ttu-id="4cd17-239">Será solicitada a senha que você forneceu anteriormente como parte da criação do usuário de implantação.</span><span class="sxs-lookup"><span data-stu-id="4cd17-239">You will be prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="4cd17-240">Durante a implantação, o Serviço de Aplicativo do Azure comunica seu andamento com o Git.</span><span class="sxs-lookup"><span data-stu-id="4cd17-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="4cd17-241">É possível notar que o processo de implantação executa [Gulp](http://gulpjs.com/) após `npm install`.</span><span class="sxs-lookup"><span data-stu-id="4cd17-241">You may notice that the deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="4cd17-242">O Serviço de Aplicativo não executa tarefas Gulp ou Grunt durante a implantação, portanto, esse repositório de exemplo possui dois arquivos adicionais em seu diretório raiz para habilitá-lo:</span><span class="sxs-lookup"><span data-stu-id="4cd17-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory to enable it:</span></span> 

- <span data-ttu-id="4cd17-243">_.deployment_ – este arquivo instrui o Serviço de Aplicativo a executar `bash deploy.sh` como o script de implantação personalizado.</span><span class="sxs-lookup"><span data-stu-id="4cd17-243">_.deployment_ - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
- <span data-ttu-id="4cd17-244">_deploy.sh_ – o script de implantação personalizado.</span><span class="sxs-lookup"><span data-stu-id="4cd17-244">_deploy.sh_ - The custom deployment script.</span></span> <span data-ttu-id="4cd17-245">Se você revisar o arquivo, verá que ele executa `gulp prod` após `npm install` e `bower install`.</span><span class="sxs-lookup"><span data-stu-id="4cd17-245">If you review the file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="4cd17-246">É possível usar essa abordagem para adicionar qualquer etapa à implantação com base em Git.</span><span class="sxs-lookup"><span data-stu-id="4cd17-246">You can use this approach to add any step to your Git-based deployment.</span></span> <span data-ttu-id="4cd17-247">Se você reiniciar seu aplicativo Web do Azure em qualquer ponto, o Serviço de Aplicativo não executará novamente essas tarefas de automação.</span><span class="sxs-lookup"><span data-stu-id="4cd17-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="4cd17-248">Navegar até o aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-248">Browse to the Azure web app</span></span> 

<span data-ttu-id="4cd17-249">Navegue até o aplicativo Web implantado usando o navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="4cd17-249">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="4cd17-250">Clique em **Criar Conta** no menu superior e crie um usuário fictício.</span><span class="sxs-lookup"><span data-stu-id="4cd17-250">Click **Sign Up** in the top menu and create a dummy user.</span></span> 

<span data-ttu-id="4cd17-251">Se você tiver êxito e o aplicativo entrar automaticamente no usuário criado, isso significa que seu aplicativo MEAN.js no Azure tem conectividade com o banco de dados MongoDB (Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="4cd17-251">If you are successful and the app automatically signs in to the created user, then your MEAN.js app in Azure has connectivity to the MongoDB (Cosmos DB) database.</span></span> 

![Aplicativo MEAN.js em execução no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="4cd17-253">Selecione **Admin > Gerenciar Artigos** para adicionar alguns artigos.</span><span class="sxs-lookup"><span data-stu-id="4cd17-253">Select **Admin > Manage Articles** to add some articles.</span></span> 

<span data-ttu-id="4cd17-254">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="4cd17-254">**Congratulations!**</span></span> <span data-ttu-id="4cd17-255">Você está executando um aplicativo Node.js controlado por dados no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="4cd17-256">Atualizar o modelo de dados e reimplantar</span><span class="sxs-lookup"><span data-stu-id="4cd17-256">Update data model and redeploy</span></span>

<span data-ttu-id="4cd17-257">Nessa etapa, você altera o modelo de dados `article` e publica suas alterações no Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-257">In this step, you change the `article` data model and publish your change to Azure.</span></span>

### <a name="update-the-data-model"></a><span data-ttu-id="4cd17-258">Atualizar o modelo de dados</span><span class="sxs-lookup"><span data-stu-id="4cd17-258">Update the data model</span></span>

<span data-ttu-id="4cd17-259">Abra _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="4cd17-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="4cd17-260">Em `ArticleSchema`, adicione um tipo `String` chamado `comment`.</span><span class="sxs-lookup"><span data-stu-id="4cd17-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="4cd17-261">Quando terminar, seu código de esquema deverá ter essa aparência:</span><span class="sxs-lookup"><span data-stu-id="4cd17-261">When you're done, your schema code should look like this:</span></span>

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-the-articles-code"></a><span data-ttu-id="4cd17-262">Atualizar o código dos artigos</span><span class="sxs-lookup"><span data-stu-id="4cd17-262">Update the articles code</span></span>

<span data-ttu-id="4cd17-263">Atualize o resto do seu código `articles` para usar `comment`.</span><span class="sxs-lookup"><span data-stu-id="4cd17-263">Update the rest of your `articles` code to use `comment`.</span></span>

<span data-ttu-id="4cd17-264">Há cinco arquivos que você precisa modificar: o controlador de servidor e as quatro exibições do cliente.</span><span class="sxs-lookup"><span data-stu-id="4cd17-264">There are five files you need to modify: the server controller and the four client views.</span></span> 

<span data-ttu-id="4cd17-265">Abra _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="4cd17-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="4cd17-266">Na função `update` adicione uma atribuição para `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="4cd17-266">In the `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="4cd17-267">O código a seguir mostra a função `update` completa:</span><span class="sxs-lookup"><span data-stu-id="4cd17-267">The following code shows the completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="4cd17-268">Abra _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="4cd17-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="4cd17-269">Logo acima da marca de fechamento `</section>`, adicione a seguinte linha para exibir `comment` juntamente com o resto dos dados do artigo:</span><span class="sxs-lookup"><span data-stu-id="4cd17-269">Just above the closing `</section>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="4cd17-270">Abra _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="4cd17-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="4cd17-271">Logo acima da marca de fechamento `</a>`, adicione a seguinte linha para exibir `comment` juntamente com o resto dos dados do artigo:</span><span class="sxs-lookup"><span data-stu-id="4cd17-271">Just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="4cd17-272">Abra _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="4cd17-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="4cd17-273">Dentro do elemento `<div class="list-group">` e logo acima da marcação de fechamento `</a>`, adicione a seguinte linha para exibir `comment` juntamente com o resto dos dados do artigo:</span><span class="sxs-lookup"><span data-stu-id="4cd17-273">Inside the `<div class="list-group">` element and just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="4cd17-274">Abra _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="4cd17-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="4cd17-275">Localize o elemento `<div class="form-group">` que contém o botão enviar, que se parece com este:</span><span class="sxs-lookup"><span data-stu-id="4cd17-275">Find the `<div class="form-group">` element that contains the submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="4cd17-276">Logo acima dessa marcação, adicione outro elemento `<div class="form-group">` que permite editar o campo `comment`.</span><span class="sxs-lookup"><span data-stu-id="4cd17-276">Just above this tag, add another `<div class="form-group">` element that lets people edit the `comment` field.</span></span> <span data-ttu-id="4cd17-277">Seu novo elemento deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="4cd17-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="4cd17-278">Testar suas alterações localmente</span><span class="sxs-lookup"><span data-stu-id="4cd17-278">Test your changes locally</span></span>

<span data-ttu-id="4cd17-279">Salve todas as alterações.</span><span class="sxs-lookup"><span data-stu-id="4cd17-279">Save all your changes.</span></span>

<span data-ttu-id="4cd17-280">Teste suas alterações em modo de produção novamente.</span><span class="sxs-lookup"><span data-stu-id="4cd17-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="4cd17-281">Lembre-se de que _config/env/production.js_ foi revertido e a variável de ambiente `MONGODB_URI` está definida apenas no seu aplicativo Web do Azure e não no computador local.</span><span class="sxs-lookup"><span data-stu-id="4cd17-281">Remember that your _config/env/production.js_ has been reverted, and the `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="4cd17-282">Se analisar o arquivo de configuração, você verá que a configuração de produção é definida por padrão para usar um banco de dados MongoDB local.</span><span class="sxs-lookup"><span data-stu-id="4cd17-282">If you look at the config file, you find that the production configuration defaults to use a local MongoDB database.</span></span> <span data-ttu-id="4cd17-283">Isso garante seus dados de produção não sejam tocados ao testar suas alterações de código localmente.</span><span class="sxs-lookup"><span data-stu-id="4cd17-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="4cd17-284">Navegue até `http://localhost:8443` em um navegador e certifique-se de que está conectado.</span><span class="sxs-lookup"><span data-stu-id="4cd17-284">Navigate to `http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="4cd17-285">Clique em **Admin > Gerenciar Artigos** e, em seguida, adicione um artigo selecionando o botão **+**.</span><span class="sxs-lookup"><span data-stu-id="4cd17-285">Select **Admin > Manage Articles**, then add an article by selecting the **+** button.</span></span>

<span data-ttu-id="4cd17-286">Agora, você verá a nova caixa de texto `Comment`.</span><span class="sxs-lookup"><span data-stu-id="4cd17-286">You see the new `Comment` textbox now.</span></span>

![Campo de comentário adicionado para Artigos](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="4cd17-288">No terminal, pare o Node.js digitando `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="4cd17-288">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-to-azure"></a><span data-ttu-id="4cd17-289">Publicar alterações no Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-289">Publish changes to Azure</span></span>

<span data-ttu-id="4cd17-290">Confirme suas alterações no Git, em seguida, envie as alterações do código para o Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-290">Commit your changes in Git, then push the code changes to Azure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="4cd17-291">Quando `git push` estiver completo, navegue até seu aplicativo Web do Azure e tente a nova funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="4cd17-291">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality.</span></span>

![Alterações de banco de dados e modelos publicadas no Azure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="4cd17-293">Se você adicionou artigos anteriores, ainda será possível vê-los.</span><span class="sxs-lookup"><span data-stu-id="4cd17-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="4cd17-294">Dados existentes no BD Cosmos não são perdidos.</span><span class="sxs-lookup"><span data-stu-id="4cd17-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="4cd17-295">Também, suas atualizações para o esquema de dados e deixa seus dados existentes intactos.</span><span class="sxs-lookup"><span data-stu-id="4cd17-295">Also, your updates to the data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="4cd17-296">Logs de diagnóstico de fluxo</span><span class="sxs-lookup"><span data-stu-id="4cd17-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="4cd17-297">Enquanto o aplicativo Node.js é executado no Serviço de Aplicativo do Azure, você pode obter logs do console transferidos para o seu terminal.</span><span class="sxs-lookup"><span data-stu-id="4cd17-297">While your Node.js application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="4cd17-298">Dessa forma, é possível obter as mesmas mensagens de diagnóstico para ajudá-lo a depurar erros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4cd17-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="4cd17-299">Para iniciar o streaming de log, use o comando [az webapp log tail](/cli/azure/webapp/log#tail).</span><span class="sxs-lookup"><span data-stu-id="4cd17-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="4cd17-300">Uma vez iniciado o streaming de log, atualize seu aplicativo Web do Azure no navegador para obter algum tráfego da Web.</span><span class="sxs-lookup"><span data-stu-id="4cd17-300">Once log streaming has started, refresh your Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="4cd17-301">Agora, será possível ver os logs do console transferidos para o seu terminal.</span><span class="sxs-lookup"><span data-stu-id="4cd17-301">You now see console logs piped to your terminal.</span></span>

<span data-ttu-id="4cd17-302">Para interromper o streaming de log a qualquer momento, digite `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="4cd17-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="4cd17-303">Gerenciar seu aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-303">Manage your Azure web app</span></span>

<span data-ttu-id="4cd17-304">Vá para o [portal do Azure](https://portal.azure.com) para ver o aplicativo Web que você criou.</span><span class="sxs-lookup"><span data-stu-id="4cd17-304">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="4cd17-305">No menu à esquerda, clique em **Serviço de Aplicativos** e, em seguida, clique no nome do seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd17-305">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Navegação do portal para o aplicativo Web do Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="4cd17-307">Por padrão, o portal mostra a página **Visão geral** do seu aplicativo Web .</span><span class="sxs-lookup"><span data-stu-id="4cd17-307">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="4cd17-308">Esta página fornece uma visão de como está seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4cd17-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="4cd17-309">Aqui, você também pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="4cd17-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="4cd17-310">As guias no lado esquerdo da página mostram as páginas de configuração diferentes que você pode abrir.</span><span class="sxs-lookup"><span data-stu-id="4cd17-310">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Página Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="4cd17-312">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4cd17-312">Next steps</span></span>

<span data-ttu-id="4cd17-313">O que você aprendeu:</span><span class="sxs-lookup"><span data-stu-id="4cd17-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4cd17-314">Criar um banco de dados MongoDB no Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="4cd17-315">Conectar um aplicativo Node.js ao MongoDB</span><span class="sxs-lookup"><span data-stu-id="4cd17-315">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="4cd17-316">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-316">Deploy the app to Azure</span></span>
> * <span data-ttu-id="4cd17-317">Atualizar o modelo de dados e reimplantar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="4cd17-317">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="4cd17-318">Transmitir logs do Azure para seu terminal</span><span class="sxs-lookup"><span data-stu-id="4cd17-318">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="4cd17-319">Gerenciar o aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-319">Manage the app in the Azure portal</span></span>

<span data-ttu-id="4cd17-320">Vá para o próximo tutorial para saber como mapear um nome DNS personalizado para o seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="4cd17-320">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="4cd17-321">Mapear um nome DNS personalizado existente para aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="4cd17-321">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
