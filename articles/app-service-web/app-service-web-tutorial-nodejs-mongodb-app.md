---
title: aaaBuild um aplicativo web Node. js e MongoDB no Azure | Microsoft Docs
description: "Saiba como tooget um aplicativo Node. js trabalhando no Azure, com conexão tooa Cosmos banco de dados do banco de dados com uma cadeia de caracteres de conexão do MongoDB."
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
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="5ee33-103">Compilar um aplicativo Web Node.js e MongoDB no Azure</span><span class="sxs-lookup"><span data-stu-id="5ee33-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="5ee33-104">Os aplicativos Web do Azure fornecem um serviço de hospedagem na Web altamente escalonável, com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="5ee33-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="5ee33-105">Este tutorial mostra como toocreate um Node. js aplicativo no Azure da web e conecte-o banco de dados do MongoDB tooa.</span><span class="sxs-lookup"><span data-stu-id="5ee33-105">This tutorial shows how toocreate a Node.js web app in Azure and connect it tooa MongoDB database.</span></span> <span data-ttu-id="5ee33-106">Quando terminar, você terá um aplicativo MEAN (MongoDB, Express, AngularJS e Node.js) executando em [Serviço de Aplicativo do Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ee33-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="5ee33-107">Para simplificar, o aplicativo de exemplo hello usa Olá [framework do web MEAN.js](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="5ee33-107">For simplicity, hello sample application uses hello [MEAN.js web framework](http://meanjs.org/).</span></span>

![Aplicativo MEAN.js em execução no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="5ee33-109">O que você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="5ee33-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5ee33-110">Criar um banco de dados MongoDB no Azure</span><span class="sxs-lookup"><span data-stu-id="5ee33-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="5ee33-111">Conecte-se um tooMongoDB de aplicativo Node. js</span><span class="sxs-lookup"><span data-stu-id="5ee33-111">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="5ee33-112">Implantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="5ee33-112">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="5ee33-113">Atualizar o modelo de dados hello e reimplantar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="5ee33-113">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="5ee33-114">Transmitir logs de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee33-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="5ee33-115">Gerenciar o aplicativo hello em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee33-115">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ee33-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5ee33-116">Prerequisites</span></span>

<span data-ttu-id="5ee33-117">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="5ee33-117">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="5ee33-118">Instalar o Git</span><span class="sxs-lookup"><span data-stu-id="5ee33-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="5ee33-119">Instalar o Node.js e o NPM</span><span class="sxs-lookup"><span data-stu-id="5ee33-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="5ee33-120">[Instale o Gulp.js](http://gulpjs.com/) (exigido pelo [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span><span class="sxs-lookup"><span data-stu-id="5ee33-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="5ee33-121">Instale e execute o MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="5ee33-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5ee33-122">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5ee33-122">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5ee33-123">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee33-123">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5ee33-124">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5ee33-124">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="5ee33-125">Testar o MongoDB local</span><span class="sxs-lookup"><span data-stu-id="5ee33-125">Test local MongoDB</span></span>

<span data-ttu-id="5ee33-126">Janela do terminal Olá aberto e `cd` toohello `bin` diretório de instalação do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5ee33-126">Open hello terminal window and `cd` toohello `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="5ee33-127">Você pode usar essa janela do terminal toorun todos os comandos de saudação neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5ee33-127">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

<span data-ttu-id="5ee33-128">Execute `mongo` no servidor tooyour MongoDB local tooconnect terminal hello.</span><span class="sxs-lookup"><span data-stu-id="5ee33-128">Run `mongo` in hello terminal tooconnect tooyour local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="5ee33-129">Se sua conexão tiver êxito, então seu banco de dados MongoDB já está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="5ee33-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="5ee33-130">Se não, certifique-se de que seu banco de dados local do MongoDB é iniciado, seguindo as etapas de saudação em [instalar MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="5ee33-130">If not, make sure that your local MongoDB database is started by following hello steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="5ee33-131">Geralmente, MongoDB está instalado, mas você ainda precisa toostart-lo executando `mongod`.</span><span class="sxs-lookup"><span data-stu-id="5ee33-131">Often, MongoDB is installed, but you still need toostart it by running `mongod`.</span></span> 

<span data-ttu-id="5ee33-132">Quando você terminar de teste seu banco de dados do MongoDB, digite `Ctrl+C` em Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="5ee33-132">When you're done testing your MongoDB database, type `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="5ee33-133">Criar aplicativo Node.js local</span><span class="sxs-lookup"><span data-stu-id="5ee33-133">Create local Node.js app</span></span>

<span data-ttu-id="5ee33-134">Nesta etapa, você configura Olá local Node. js projeto.</span><span class="sxs-lookup"><span data-stu-id="5ee33-134">In this step, you set up hello local Node.js project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="5ee33-135">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="5ee33-135">Clone hello sample application</span></span>

<span data-ttu-id="5ee33-136">Na janela do terminal hello, `cd` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5ee33-136">In hello terminal window, `cd` tooa working directory.</span></span>  

<span data-ttu-id="5ee33-137">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="5ee33-137">Run hello following command tooclone hello sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="5ee33-138">Esse repositório de exemplo contém uma cópia da saudação [MEAN.js repositório](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="5ee33-138">This sample repository contains a copy of hello [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="5ee33-139">É modificada toorun no serviço de aplicativo (para obter mais informações, consulte o repositório de MEAN.js Olá [arquivo Leiame](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="5ee33-139">It is modified toorun on App Service (for more information, see hello MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-hello-application"></a><span data-ttu-id="5ee33-140">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="5ee33-140">Run hello application</span></span>

<span data-ttu-id="5ee33-141">Execute Olá pacotes de saudação necessário tooinstall comandos a seguir e inicie o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5ee33-141">Run hello following commands tooinstall hello required packages and start hello application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="5ee33-142">Quando o aplicativo hello está totalmente carregado, você verá algo semelhante toohello seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="5ee33-142">When hello app is fully loaded, you see something similar toohello following message:</span></span>

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

<span data-ttu-id="5ee33-143">Navegue toohttp://localhost:3000 em um navegador.</span><span class="sxs-lookup"><span data-stu-id="5ee33-143">Navigate toohttp://localhost:3000 in a browser.</span></span> <span data-ttu-id="5ee33-144">Clique em **inscrever** Olá menu superior e criar um usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="5ee33-144">Click **Sign Up** in hello top menu and create a test user.</span></span> 

<span data-ttu-id="5ee33-145">Olá MEAN.js aplicativo de exemplo armazena dados de usuário no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee33-145">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="5ee33-146">Se tiver êxito na criação de um usuário e entrar, seu aplicativo está gravando dados toohello MongoDB banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="5ee33-146">If you are successful at creating a user and signing in, then your app is writing data toohello local MongoDB database.</span></span>

![MEAN.js se conecta com êxito tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="5ee33-148">Selecione **Administração > Gerenciar artigos** tooadd alguns artigos.</span><span class="sxs-lookup"><span data-stu-id="5ee33-148">Select **Admin > Manage Articles** tooadd some articles.</span></span>

<span data-ttu-id="5ee33-149">toostop Node. js a qualquer momento, pressione `Ctrl+C` em Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="5ee33-149">toostop Node.js at any time, press `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="5ee33-150">Criar MongoDB de produção</span><span class="sxs-lookup"><span data-stu-id="5ee33-150">Create production MongoDB</span></span>

<span data-ttu-id="5ee33-151">Ness etapa, você cria um banco de dados MongoDB no Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee33-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="5ee33-152">Quando seu aplicativo é implantado tooAzure, ele usa esse banco de dados de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5ee33-152">When your app is deployed tooAzure, it uses this cloud database.</span></span>

<span data-ttu-id="5ee33-153">Para o MongoDB, este tutorial usa o [BD Cosmos do Azure](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="5ee33-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="5ee33-154">O BD Cosmos dá suporte a conexões de cliente do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5ee33-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="5ee33-155">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="5ee33-155">Log in tooAzure</span></span>

<span data-ttu-id="5ee33-156">Você usará hello Azure CLI 2.0 toocreate Olá recursos necessários toohost seu aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee33-156">You'll use hello Azure CLI 2.0 toocreate hello resources needed toohost your app in Azure.</span></span> <span data-ttu-id="5ee33-157">Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="5ee33-157">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="5ee33-158">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5ee33-158">Create a resource group</span></span>

<span data-ttu-id="5ee33-159">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="5ee33-159">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="5ee33-160">Olá exemplo a seguir cria um grupo de recursos na região Europa Ocidental de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee33-160">hello following example creates a resource group in hello West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="5ee33-161">Saudação de uso [locais de lista do serviço de aplicativo az](/cli/azure/appservice#list-locations) locais disponíveis toolist de comando CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee33-161">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="5ee33-162">Criar uma conta do BD Cosmos</span><span class="sxs-lookup"><span data-stu-id="5ee33-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="5ee33-163">Crie uma conta de banco de dados do Cosmos com hello [cosmosdb az criar](/cli/azure/cosmosdb#create) comando.</span><span class="sxs-lookup"><span data-stu-id="5ee33-163">Create a Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="5ee33-164">Olá a seguir de comando, substitua um nome exclusivo do banco de dados do Cosmos para Olá  *\<cosmosdb_name >* espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="5ee33-164">In hello following command, substitute a unique Cosmos DB name for hello *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="5ee33-165">Esse nome é usado como parte de saudação do ponto de extremidade de banco de dados do Cosmos Olá, `https://<cosmosdb_name>.documents.azure.com/`, portanto, o nome do hello deve toobe exclusivo em todas as contas de banco de dados do Cosmos no Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee33-165">This name is used as hello part of hello Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so hello name needs toobe unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="5ee33-166">Olá nome deve conter apenas letras minúsculas, números e caracteres de hífen (-) hello e deve ter entre 3 e 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="5ee33-166">hello name must contain only lowercase letters, numbers, and hello hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="5ee33-167">Olá *– tipo MongoDB* parâmetro habilita conexões de cliente do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5ee33-167">hello *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="5ee33-168">Quando Olá Cosmos DB conta é criada, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee33-168">When hello Cosmos DB account is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="connect-app-tooproduction-mongodb"></a><span data-ttu-id="5ee33-169">Conecte-se o aplicativo tooproduction MongoDB</span><span class="sxs-lookup"><span data-stu-id="5ee33-169">Connect app tooproduction MongoDB</span></span>

<span data-ttu-id="5ee33-170">Nesta etapa, você pode se conectar o MEAN.js aplicativo toohello Cosmos DB de dados de exemplo que você acabou de criar, usando uma cadeia de caracteres de conexão do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5ee33-170">In this step, you connect your MEAN.js sample application toohello Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-hello-database-key"></a><span data-ttu-id="5ee33-171">Recuperar a chave de banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="5ee33-171">Retrieve hello database key</span></span>

<span data-ttu-id="5ee33-172">tooconnect toohello Cosmos banco de dados, você precisa de chave de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee33-172">tooconnect toohello Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="5ee33-173">Saudação de uso [chaves de lista az cosmosdb](/cli/azure/cosmosdb#list-keys) chave primária do comando tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="5ee33-173">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="5ee33-174">Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee33-174">hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Copie o valor de saudação do `primaryMasterKey`. <span data-ttu-id="5ee33-176">Você precisará dessas informações na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="5ee33-176">You need this information in hello next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="5ee33-177">Configurar a cadeia de caracteres de conexão de saudação em seu aplicativo Node. js</span><span class="sxs-lookup"><span data-stu-id="5ee33-177">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="5ee33-178">Em seu repositório do MEAN.js, abra _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="5ee33-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="5ee33-179">Em Olá `db` do objeto, atualize o valor de saudação do `uri`:</span><span class="sxs-lookup"><span data-stu-id="5ee33-179">In hello `db` object, update hello value of `uri`:</span></span>

* <span data-ttu-id="5ee33-180">Substituir saudação dois  *\<cosmosdb_name >* espaços reservados com seu nome de banco de dados do banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5ee33-180">Replace hello two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="5ee33-181">Substituir saudação  *\<primary_master_key >* espaço reservado com chave Olá você copiou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="5ee33-181">Replace hello *\<primary_master_key>* placeholder with hello key you copied in hello previous step.</span></span>

<span data-ttu-id="5ee33-182">Olá, código a seguir mostra Olá `db` objeto:</span><span class="sxs-lookup"><span data-stu-id="5ee33-182">hello following code shows hello `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="5ee33-183">Olá `ssl=true` opção é necessária porque [Cosmos DB requer SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="5ee33-183">hello `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="5ee33-184">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="5ee33-184">Save your changes.</span></span>

### <a name="test-hello-application-in-production-mode"></a><span data-ttu-id="5ee33-185">Testar o aplicativo hello no modo de produção</span><span class="sxs-lookup"><span data-stu-id="5ee33-185">Test hello application in production mode</span></span> 

<span data-ttu-id="5ee33-186">Olá executar scripts de comando toominify e pacote para o ambiente de produção de hello a seguir.</span><span class="sxs-lookup"><span data-stu-id="5ee33-186">Run hello following command toominify and bundle scripts for hello production environment.</span></span> <span data-ttu-id="5ee33-187">Esse processo gera arquivos de saudação necessários ao ambiente de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="5ee33-187">This process generates hello files needed by hello production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="5ee33-188">Olá execução após a cadeia de conexão do comando toouse Olá configurada na _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="5ee33-188">Run hello following command toouse hello connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="5ee33-189">`NODE_ENV=production`Define a variável de ambiente Olá que informa toorun Node. js no ambiente de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="5ee33-189">`NODE_ENV=production` sets hello environment variable that tells Node.js toorun in hello production environment.</span></span>  <span data-ttu-id="5ee33-190">`node server.js`Inicia Olá servidor Node.js com `server.js` na raiz do repositório.</span><span class="sxs-lookup"><span data-stu-id="5ee33-190">`node server.js` starts hello Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="5ee33-191">É dessa forma que o aplicativo Node.js é carregado no Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee33-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="5ee33-192">Quando o aplicativo hello é carregado, verifique toomake se ele está em execução no ambiente de produção de hello:</span><span class="sxs-lookup"><span data-stu-id="5ee33-192">When hello app is loaded, check toomake sure that it's running in hello production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="5ee33-193">Navegue toohttp://localhost:8443 em um navegador.</span><span class="sxs-lookup"><span data-stu-id="5ee33-193">Navigate toohttp://localhost:8443 in a browser.</span></span> <span data-ttu-id="5ee33-194">Clique em **inscrever** Olá menu superior e criar um usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="5ee33-194">Click **Sign Up** in hello top menu and create a test user.</span></span> <span data-ttu-id="5ee33-195">Se você estiver criando um usuário e entrar com êxito, seu aplicativo está gravando dados toohello DB Cosmos banco de dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee33-195">If you are successful creating a user and signing in, then your app is writing data toohello Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="5ee33-196">Olá terminal, parar Node. js digitando `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="5ee33-196">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-tooazure"></a><span data-ttu-id="5ee33-197">Implantar o aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="5ee33-197">Deploy app tooAzure</span></span>

<span data-ttu-id="5ee33-198">Nesta etapa, você deve implantar seu aplicativo de Node. js conectado MongoDB tooAzure do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5ee33-198">In this step, you deploy your MongoDB-connected Node.js application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="5ee33-199">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="5ee33-199">Create an App Service plan</span></span>

<span data-ttu-id="5ee33-200">Criar um plano de serviço de aplicativo com hello [criar plano de serviço de aplicativo az](/cli/azure/appservice/plan#create) comando.</span><span class="sxs-lookup"><span data-stu-id="5ee33-200">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="5ee33-201">Olá, exemplo a seguir cria um plano de serviço de aplicativo chamado _myAppServicePlan_ usando Olá **livre** preço:</span><span class="sxs-lookup"><span data-stu-id="5ee33-201">hello following example creates an App Service plan named _myAppServicePlan_ using hello **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="5ee33-202">Quando Olá plano de serviço de aplicativo é criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee33-202">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="5ee33-203">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="5ee33-203">Create a web app</span></span>

<span data-ttu-id="5ee33-204">Criar um aplicativo web no hello `myAppServicePlan` plano de serviço de aplicativo com hello [az webapp criar](/cli/azure/webapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="5ee33-204">Create a web app in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="5ee33-205">Fornece de aplicativo de web Hello você hospedagem espaço toodeploy seu código e fornece uma URL para você Olá tooview aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="5ee33-205">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="5ee33-206">Use toocreate Olá web app.</span><span class="sxs-lookup"><span data-stu-id="5ee33-206">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="5ee33-207">Olá a seguir de comando, substitua Olá  *\<app_name >* espaço reservado com um nome exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5ee33-207">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="5ee33-208">Esse nome é usado como parte de saudação da saudação padrão URL do aplicativo web de hello, para que o nome do hello deve toobe exclusivo entre todos os aplicativos no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee33-208">This name is used as hello part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="5ee33-209">Quando o aplicativo da web de saudação tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee33-209">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-an-environment-variable"></a><span data-ttu-id="5ee33-210">Configurar um variável de ambiente</span><span class="sxs-lookup"><span data-stu-id="5ee33-210">Configure an environment variable</span></span>

<span data-ttu-id="5ee33-211">Olá tutorial, você Olá banco de dados conexão cadeia de caracteres codificada em anteriormente _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="5ee33-211">Earlier in hello tutorial, you hardcoded hello database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="5ee33-212">Para manter a prática recomendada de segurança, convém tookeep dados confidenciais fora do seu repositório Git.</span><span class="sxs-lookup"><span data-stu-id="5ee33-212">In keeping with security best practice, you want tookeep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="5ee33-213">Para seu aplicativo em execução no Azure, você usará uma variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="5ee33-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="5ee33-214">No serviço de aplicativo, você definir variáveis de ambiente como _configurações do aplicativo_ usando Olá [az webapp configuração appsettings atualizar](/cli/azure/webapp/config/appsettings#update) comando.</span><span class="sxs-lookup"><span data-stu-id="5ee33-214">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="5ee33-215">Olá exemplo a seguir configura um `MONGODB_URI` configuração do aplicativo em seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee33-215">hello following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="5ee33-216">Substituir saudação  *\<app_name >*,  *\<cosmosdb_name >*, e  *\<primary_master_key >* espaços reservados.</span><span class="sxs-lookup"><span data-stu-id="5ee33-216">Replace hello *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="5ee33-217">No código Node.js, você acessa essa configuração de aplicativo com `process.env.MONGODB_URI`, assim como você teria acesso a qualquer variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="5ee33-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="5ee33-218">Agora, desfazer suas alterações too_config/env/production.js_ com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee33-218">Now, undo your changes too_config/env/production.js_ with hello following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="5ee33-219">Abra _config/env/production.js_ novamente.</span><span class="sxs-lookup"><span data-stu-id="5ee33-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="5ee33-220">Observe que esse aplicativo de MEAN.js saudação padrão já está configurado toouse Olá `MONGODB_URI` variável de ambiente que você criou.</span><span class="sxs-lookup"><span data-stu-id="5ee33-220">Note that hello default MEAN.js app is already configured toouse hello `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="5ee33-221">Configurar a implantação do git local</span><span class="sxs-lookup"><span data-stu-id="5ee33-221">Configure local git deployment</span></span> 

<span data-ttu-id="5ee33-222">Saudação de uso [usuário az webapp implantação definido](/cli/azure/webapp/deployment/user#set) toocreate credenciais para a implantação de comando.</span><span class="sxs-lookup"><span data-stu-id="5ee33-222">Use hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command toocreate credentials for deployment.</span></span>

<span data-ttu-id="5ee33-223">Você pode implantar seu tooAzure de aplicativo do serviço de aplicativo de várias maneiras, incluindo o FTP, Git local, GitHub, Visual Studio Team Services e BitBucket.</span><span class="sxs-lookup"><span data-stu-id="5ee33-223">You can deploy your application tooAzure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="5ee33-224">Para FTP e Git local, é necessário toohave um usuário de implantação configurado no hello server tooauthenticate sua implantação.</span><span class="sxs-lookup"><span data-stu-id="5ee33-224">For FTP and local Git, it is necessary toohave a deployment user configured on hello server tooauthenticate your deployment.</span></span> <span data-ttu-id="5ee33-225">Este usuário de implantação está no nível de conta e é diferente da sua conta de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee33-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="5ee33-226">Você só precisa tooconfigure esse usuário de implantação uma vez.</span><span class="sxs-lookup"><span data-stu-id="5ee33-226">You only need tooconfigure this deployment user once.</span></span>

<span data-ttu-id="5ee33-227">Olá a seguir de comando, substitua  *\<nome de usuário >* e  *\<senha >* com um novo nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="5ee33-227">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="5ee33-228">nome de usuário Olá deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5ee33-228">hello user name must be unique.</span></span> <span data-ttu-id="5ee33-229">Hello senha deve ter pelo menos oito caracteres, com dois Olá após três elementos: letras, números, símbolos.</span><span class="sxs-lookup"><span data-stu-id="5ee33-229">hello password must be at least eight characters long, with two of hello following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="5ee33-230">Se você receber um ` 'Conflict'. Details: 409` erro, o nome de usuário de saudação de alteração.</span><span class="sxs-lookup"><span data-stu-id="5ee33-230">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="5ee33-231">Se receber um erro ` 'Bad Request'. Details: 400`, use uma senha mais forte.</span><span class="sxs-lookup"><span data-stu-id="5ee33-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="5ee33-232">Nome de usuário de saudação do registro e a senha para uso em etapas posteriores quando você implanta o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5ee33-232">Record hello user name and password for use in later steps when you deploy hello app.</span></span>

<span data-ttu-id="5ee33-233">Saudação de uso [origem de implantação de aplicativo Web do az-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) comando tooconfigure Git acesso toohello Azure o aplicativo web local.</span><span class="sxs-lookup"><span data-stu-id="5ee33-233">Use hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command tooconfigure local Git access toohello Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="5ee33-234">Quando o usuário de implantação Olá é configurado, Olá CLI do Azure mostra Olá URL de implantação para seu aplicativo web do Azure no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee33-234">When hello deployment user is configured, hello Azure CLI shows hello deployment URL for your Azure web app in hello following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="5ee33-235">Copie Olá saída de terminal Olá, pois ela será usada na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="5ee33-235">Copy hello output from hello terminal, as it will be used in hello next step.</span></span> 

### <a name="push-tooazure-from-git"></a><span data-ttu-id="5ee33-236">TooAzure de envio por push do Git</span><span class="sxs-lookup"><span data-stu-id="5ee33-236">Push tooAzure from Git</span></span>

<span data-ttu-id="5ee33-237">Adicione um repositório Git local do Azure tooyour remoto.</span><span class="sxs-lookup"><span data-stu-id="5ee33-237">Add an Azure remote tooyour local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="5ee33-238">Push toohello toodeploy remoto do Azure seu aplicativo Node. js.</span><span class="sxs-lookup"><span data-stu-id="5ee33-238">Push toohello Azure remote toodeploy your Node.js application.</span></span> <span data-ttu-id="5ee33-239">Você será solicitado para senha Olá fornecidas anteriormente como parte da criação de saudação do usuário de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee33-239">You will be prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="5ee33-240">Durante a implantação, o Serviço de Aplicativo do Azure comunica seu andamento com o Git.</span><span class="sxs-lookup"><span data-stu-id="5ee33-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="5ee33-241">Você pode perceber que executa o processo de implantação de saudação [Gulp](http://gulpjs.com/) depois `npm install`.</span><span class="sxs-lookup"><span data-stu-id="5ee33-241">You may notice that hello deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="5ee33-242">Serviço de aplicativo não executa tarefas Gulp ou pesado durante a implantação, para que este repositório de exemplo tem dois adicionais arquivos no seu tooenable de diretório raiz-lo:</span><span class="sxs-lookup"><span data-stu-id="5ee33-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory tooenable it:</span></span> 

- <span data-ttu-id="5ee33-243">_.Deployment_ -esse arquivo informa ao serviço de aplicativo toorun `bash deploy.sh` como script de implantação personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="5ee33-243">_.deployment_ - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
- <span data-ttu-id="5ee33-244">_Deploy.sh_ -Olá script de implantação personalizada.</span><span class="sxs-lookup"><span data-stu-id="5ee33-244">_deploy.sh_ - hello custom deployment script.</span></span> <span data-ttu-id="5ee33-245">Se você revisar o arquivo hello, você verá que ele seja executado `gulp prod` depois `npm install` e `bower install`.</span><span class="sxs-lookup"><span data-stu-id="5ee33-245">If you review hello file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="5ee33-246">Você pode usar essa abordagem tooadd tooyour qualquer etapa implantação baseada em Git.</span><span class="sxs-lookup"><span data-stu-id="5ee33-246">You can use this approach tooadd any step tooyour Git-based deployment.</span></span> <span data-ttu-id="5ee33-247">Se você reiniciar seu aplicativo Web do Azure em qualquer ponto, o Serviço de Aplicativo não executará novamente essas tarefas de automação.</span><span class="sxs-lookup"><span data-stu-id="5ee33-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="5ee33-248">Procurar o aplicativo web do Azure de toohello</span><span class="sxs-lookup"><span data-stu-id="5ee33-248">Browse toohello Azure web app</span></span> 

<span data-ttu-id="5ee33-249">Procurar toohello implantado um aplicativo da web usando um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="5ee33-249">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="5ee33-250">Clique em **inscrever** Olá menu superior e criar um usuário fictício.</span><span class="sxs-lookup"><span data-stu-id="5ee33-250">Click **Sign Up** in hello top menu and create a dummy user.</span></span> 

<span data-ttu-id="5ee33-251">Se tiver êxito e o aplicativo hello automaticamente entra em toohello criou o usuário e, em seguida, seu aplicativo MEAN.js no Azure tem banco de dados conectividade toohello MongoDB (Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="5ee33-251">If you are successful and hello app automatically signs in toohello created user, then your MEAN.js app in Azure has connectivity toohello MongoDB (Cosmos DB) database.</span></span> 

![Aplicativo MEAN.js em execução no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="5ee33-253">Selecione **Administração > Gerenciar artigos** tooadd alguns artigos.</span><span class="sxs-lookup"><span data-stu-id="5ee33-253">Select **Admin > Manage Articles** tooadd some articles.</span></span> 

<span data-ttu-id="5ee33-254">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="5ee33-254">**Congratulations!**</span></span> <span data-ttu-id="5ee33-255">Você está executando um aplicativo Node.js controlado por dados no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee33-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="5ee33-256">Atualizar o modelo de dados e reimplantar</span><span class="sxs-lookup"><span data-stu-id="5ee33-256">Update data model and redeploy</span></span>

<span data-ttu-id="5ee33-257">Nesta etapa, você alterar Olá `article` dados de modelo e publicar seu tooAzure de alteração.</span><span class="sxs-lookup"><span data-stu-id="5ee33-257">In this step, you change hello `article` data model and publish your change tooAzure.</span></span>

### <a name="update-hello-data-model"></a><span data-ttu-id="5ee33-258">Atualizar o modelo de dados Olá</span><span class="sxs-lookup"><span data-stu-id="5ee33-258">Update hello data model</span></span>

<span data-ttu-id="5ee33-259">Abra _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="5ee33-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="5ee33-260">Em `ArticleSchema`, adicione um tipo `String` chamado `comment`.</span><span class="sxs-lookup"><span data-stu-id="5ee33-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="5ee33-261">Quando terminar, seu código de esquema deverá ter essa aparência:</span><span class="sxs-lookup"><span data-stu-id="5ee33-261">When you're done, your schema code should look like this:</span></span>

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

### <a name="update-hello-articles-code"></a><span data-ttu-id="5ee33-262">Atualizar o código de artigos Olá</span><span class="sxs-lookup"><span data-stu-id="5ee33-262">Update hello articles code</span></span>

<span data-ttu-id="5ee33-263">Atualizar o restante de saudação do seu `articles` código toouse `comment`.</span><span class="sxs-lookup"><span data-stu-id="5ee33-263">Update hello rest of your `articles` code toouse `comment`.</span></span>

<span data-ttu-id="5ee33-264">Há cinco arquivos necessários toomodify: controlador de saudação do servidor e modos de exibição de cliente Olá quatro.</span><span class="sxs-lookup"><span data-stu-id="5ee33-264">There are five files you need toomodify: hello server controller and hello four client views.</span></span> 

<span data-ttu-id="5ee33-265">Abra _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="5ee33-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="5ee33-266">Em Olá `update` de função, adicione uma atribuição de `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="5ee33-266">In hello `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="5ee33-267">Olá, código a seguir mostra Olá concluída `update` função:</span><span class="sxs-lookup"><span data-stu-id="5ee33-267">hello following code shows hello completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="5ee33-268">Abra _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="5ee33-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="5ee33-269">Acima de fechamento Olá `</section>` marca, adicione Olá toodisplay linha a seguir `comment` junto com o restante de saudação do dados de artigo de saudação:</span><span class="sxs-lookup"><span data-stu-id="5ee33-269">Just above hello closing `</section>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="5ee33-270">Abra _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="5ee33-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="5ee33-271">Acima de fechamento Olá `</a>` marca, adicione Olá toodisplay linha a seguir `comment` junto com o restante de saudação do dados de artigo de saudação:</span><span class="sxs-lookup"><span data-stu-id="5ee33-271">Just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="5ee33-272">Abra _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="5ee33-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="5ee33-273">Olá interna `<div class="list-group">` elemento e acima de fechamento Olá `</a>` marca, adicione Olá toodisplay linha a seguir `comment` junto com o restante de saudação do dados de artigo de saudação:</span><span class="sxs-lookup"><span data-stu-id="5ee33-273">Inside hello `<div class="list-group">` element and just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="5ee33-274">Abra _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="5ee33-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="5ee33-275">Localize Olá `<div class="form-group">` elemento que contém o botão de envio de saudação, que tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="5ee33-275">Find hello `<div class="form-group">` element that contains hello submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="5ee33-276">Acima essa marca, adicione outro `<div class="form-group">` elemento que permite que as pessoas Editar Olá `comment` campo.</span><span class="sxs-lookup"><span data-stu-id="5ee33-276">Just above this tag, add another `<div class="form-group">` element that lets people edit hello `comment` field.</span></span> <span data-ttu-id="5ee33-277">Seu novo elemento deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="5ee33-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="5ee33-278">Testar suas alterações localmente</span><span class="sxs-lookup"><span data-stu-id="5ee33-278">Test your changes locally</span></span>

<span data-ttu-id="5ee33-279">Salve todas as alterações.</span><span class="sxs-lookup"><span data-stu-id="5ee33-279">Save all your changes.</span></span>

<span data-ttu-id="5ee33-280">Teste suas alterações em modo de produção novamente.</span><span class="sxs-lookup"><span data-stu-id="5ee33-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="5ee33-281">Lembre-se de que seu _config/env/production.js_ foi revertido e Olá `MONGODB_URI` variável de ambiente é definida somente em seu aplicativo web do Azure e não no computador local.</span><span class="sxs-lookup"><span data-stu-id="5ee33-281">Remember that your _config/env/production.js_ has been reverted, and hello `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="5ee33-282">Se você examinar o arquivo de configuração Olá, você encontrar esse Olá padrões de configuração de produção toouse um banco de dados local do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5ee33-282">If you look at hello config file, you find that hello production configuration defaults toouse a local MongoDB database.</span></span> <span data-ttu-id="5ee33-283">Isso garante seus dados de produção não sejam tocados ao testar suas alterações de código localmente.</span><span class="sxs-lookup"><span data-stu-id="5ee33-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="5ee33-284">Navegue muito`http://localhost:8443` em um navegador e certifique-se de que você está conectado.</span><span class="sxs-lookup"><span data-stu-id="5ee33-284">Navigate too`http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="5ee33-285">Selecione **Administração > Gerenciar artigos**, em seguida, adicionar um artigo selecionando Olá  **+**  botão.</span><span class="sxs-lookup"><span data-stu-id="5ee33-285">Select **Admin > Manage Articles**, then add an article by selecting hello **+** button.</span></span>

<span data-ttu-id="5ee33-286">Você verá Olá novo `Comment` caixa de texto agora.</span><span class="sxs-lookup"><span data-stu-id="5ee33-286">You see hello new `Comment` textbox now.</span></span>

![Comentário adicionado campo tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="5ee33-288">Olá terminal, parar Node. js digitando `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="5ee33-288">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-tooazure"></a><span data-ttu-id="5ee33-289">Publicar alterações tooAzure</span><span class="sxs-lookup"><span data-stu-id="5ee33-289">Publish changes tooAzure</span></span>

<span data-ttu-id="5ee33-290">Confirmar as alterações no Git, em seguida, push Olá tooAzure de alterações de código.</span><span class="sxs-lookup"><span data-stu-id="5ee33-290">Commit your changes in Git, then push hello code changes tooAzure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="5ee33-291">Uma vez Olá `git push` é concluída, navegue tooyour aplicativo de web do Azure e experimente a nova funcionalidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee33-291">Once hello `git push` is complete, navigate tooyour Azure web app and try out hello new functionality.</span></span>

![Alterações de modelo e o banco de dados publicado tooAzure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="5ee33-293">Se você adicionou artigos anteriores, ainda será possível vê-los.</span><span class="sxs-lookup"><span data-stu-id="5ee33-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="5ee33-294">Dados existentes no BD Cosmos não são perdidos.</span><span class="sxs-lookup"><span data-stu-id="5ee33-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="5ee33-295">Além disso, o esquema de dados de toohello atualizações e deixa os dados existentes intactas.</span><span class="sxs-lookup"><span data-stu-id="5ee33-295">Also, your updates toohello data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="5ee33-296">Logs de diagnóstico de fluxo</span><span class="sxs-lookup"><span data-stu-id="5ee33-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="5ee33-297">Enquanto seu aplicativo Node. js é executado no serviço de aplicativo do Azure, você pode obter Olá console logs canalizado tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="5ee33-297">While your Node.js application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="5ee33-298">Dessa forma, você pode obter Olá mensagens de diagnóstico mesmo toohelp depurar erros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5ee33-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="5ee33-299">log toostart streaming use Olá [final de log webapp az](/cli/azure/webapp/log#tail) comando.</span><span class="sxs-lookup"><span data-stu-id="5ee33-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="5ee33-300">Depois de iniciado o log de streaming, atualize seu aplicativo web do Azure no hello navegador tooget parte do tráfego da web.</span><span class="sxs-lookup"><span data-stu-id="5ee33-300">Once log streaming has started, refresh your Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="5ee33-301">Agora, você verá logs do console conectado tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="5ee33-301">You now see console logs piped tooyour terminal.</span></span>

<span data-ttu-id="5ee33-302">Para interromper o streaming de log a qualquer momento, digite `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="5ee33-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="5ee33-303">Gerenciar seu aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee33-303">Manage your Azure web app</span></span>

<span data-ttu-id="5ee33-304">Vá toohello [portal do Azure](https://portal.azure.com) toosee Olá web aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="5ee33-304">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="5ee33-305">No menu à esquerda do hello, clique em **serviços de aplicativos**, clique em nome de saudação do seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee33-305">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="5ee33-307">Por padrão, o portal de saudação mostra seu aplicativo de web **visão geral** página.</span><span class="sxs-lookup"><span data-stu-id="5ee33-307">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="5ee33-308">Esta página fornece uma visão de como está seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5ee33-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="5ee33-309">Aqui, você também pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir.</span><span class="sxs-lookup"><span data-stu-id="5ee33-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="5ee33-310">guias de Olá no lado esquerdo de saudação da página de saudação mostram páginas de configuração diferentes de hello, que você pode abrir.</span><span class="sxs-lookup"><span data-stu-id="5ee33-310">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Página Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="5ee33-312">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5ee33-312">Next steps</span></span>

<span data-ttu-id="5ee33-313">O que você aprendeu:</span><span class="sxs-lookup"><span data-stu-id="5ee33-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5ee33-314">Criar um banco de dados MongoDB no Azure</span><span class="sxs-lookup"><span data-stu-id="5ee33-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="5ee33-315">Conecte-se um tooMongoDB de aplicativo Node. js</span><span class="sxs-lookup"><span data-stu-id="5ee33-315">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="5ee33-316">Implantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="5ee33-316">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="5ee33-317">Atualizar o modelo de dados hello e reimplantar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="5ee33-317">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="5ee33-318">Logs de fluxo do Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="5ee33-318">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="5ee33-319">Gerenciar o aplicativo hello em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee33-319">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="5ee33-320">Avançar toolearn tutorial do próximo toohello como toomap um DNS personalizado nome tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="5ee33-320">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="5ee33-321">Mapear um tooAzure de nome DNS de personalizada existente aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="5ee33-321">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
