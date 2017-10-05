---
title: "Aplicativo de API do Node.js no Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Saiba como criar um pacote do aplicativo de API RESTful do Node.js e implantá-lo em um aplicativo de API no Serviço de Aplicativo do Azure."
services: app-service\api
documentationcenter: node
author: bradygaster
manager: erikre
editor: 
ms.assetid: a820e400-06af-4852-8627-12b3db4a8e70
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: rachelap
ms.openlocfilehash: 806585edd43b9d2d678bfa41523e4d9d40af8cba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-to-an-api-app-in-azure"></a><span data-ttu-id="1ec8c-103">Criar uma API RESTful do Node. js e implantá-la em um aplicativo de API no Azure</span><span class="sxs-lookup"><span data-stu-id="1ec8c-103">Build a Node.js RESTful API and deploy it to an API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="1ec8c-104">Este guia de início rápido mostra como criar uma API REST escrita com Node.js [Express](http://expressjs.com/), usando uma definição [Swagger](http://swagger.io/) e implantá-la como um [Aplicativo de API](app-service-api-apps-why-best-platform.md) no Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-104">This quickstart shows how to create a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="1ec8c-105">Crie o aplicativo usando as ferramentas de linha de comando, configure os recursos com a [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) e implante o aplicativo usando o Git.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-105">You create the app using command-line tools, configure resources with the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy the app using Git.</span></span>  <span data-ttu-id="1ec8c-106">No fim, você tem uma API REST funcional de exemplo em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ec8c-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1ec8c-107">Prerequisites</span></span>

* [<span data-ttu-id="1ec8c-108">Git</span><span class="sxs-lookup"><span data-stu-id="1ec8c-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="1ec8c-109">Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="1ec8c-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1ec8c-110">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-110">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1ec8c-111">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="1ec8c-112">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1ec8c-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="1ec8c-113">Prepare o seu ambiente</span><span class="sxs-lookup"><span data-stu-id="1ec8c-113">Prepare your environment</span></span>

1. <span data-ttu-id="1ec8c-114">Em uma janela de terminal, execute o seguinte comando para clonar o exemplo em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-114">In a terminal window, run the following command to clone the sample to your local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="1ec8c-115">Altere para o diretório que contém o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-115">Change to the directory that contains the sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="1ec8c-116">Instale o [Swaggerize](https://www.npmjs.com/package/swaggerize-express) em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="1ec8c-117">Swaggerize é uma ferramenta que gera código Node.js para a API REST de uma definição de Swagger.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="1ec8c-118">Como gerar código Node.js</span><span class="sxs-lookup"><span data-stu-id="1ec8c-118">Generate Node.js code</span></span> 

<span data-ttu-id="1ec8c-119">Esta seção do tutorial modela um fluxo de trabalho de desenvolvimento de API em que você cria primeiro os metadados do Swagger e os utiliza para gerar automaticamente o código de servidor para a API.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-119">This section of the tutorial models an API development workflow in which you create Swagger metadata first and use that to scaffold (auto-generate) server code for the API.</span></span> 

<span data-ttu-id="1ec8c-120">Altere o diretório para a pasta *iniciar* e, em seguida, execute `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-120">Change directory to the *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="1ec8c-121">O Swaggerize cria um projeto de Node.js para sua API da definição de Swagger na *api.json*.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-121">Swaggerize creates a Node.js project for your API from the Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="1ec8c-122">Quando Swaggerize solicita um nome de projeto, use *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like to call this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-the-project-code"></a><span data-ttu-id="1ec8c-123">Personalize o código do projeto</span><span class="sxs-lookup"><span data-stu-id="1ec8c-123">Customize the project code</span></span>

1. <span data-ttu-id="1ec8c-124">Copie a pasta *lib* na pasta *ContactList* criada pelo `yo swaggerize` e, em seguida, altere o diretório para *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-124">Copy the *lib* folder into the *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="1ec8c-125">Instale os módulos NPM `jsonpath` e `swaggerize-ui`.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-125">Install the `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="1ec8c-126">Substitua o código no arquivo *handlers/contacts.js* pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ec8c-126">Replace the code in the *handlers/contacts.js* with the following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="1ec8c-127">Esse código usa os dados JSON armazenados no *lib/contacts.json* atendido por *lib/contactRepository.js*.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-127">This code uses the JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="1ec8c-128">O novo código *contacts.js* retorna todos os contatos no repositório como um conteúdo JSON.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-128">The new *contacts.js* code returns all contacts in the repository as a JSON payload.</span></span> 

4. <span data-ttu-id="1ec8c-129">Substitua o código no arquivo **handlers/contacts/{id}.js** pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ec8c-129">Replace the code in the **handlers/contacts/{id}.js** file with the following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="1ec8c-130">Esse código permite que você use uma variável de caminho para retornar apenas o contato com um ID especificado.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-130">This code lets you use a path variable to return only the contact with a given ID.</span></span>

5. <span data-ttu-id="1ec8c-131">Substitua o código em **server.js** pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ec8c-131">Replace the code in **server.js** with the following code:</span></span>

    ```javascript
    'use strict';

    var port = process.env.PORT || 8000; 

    var http = require('http');
    var express = require('express');
    var bodyParser = require('body-parser');
    var swaggerize = require('swaggerize-express');
    var swaggerUi = require('swaggerize-ui'); 
    var path = require('path');
    var fs = require("fs");
    
    fs.existsSync = fs.existsSync || require('path').existsSync;

    var app = express();

    var server = http.createServer(app);

    app.use(bodyParser.json());

    app.use(swaggerize({
        api: path.resolve('./config/swagger.json'),
        handlers: path.resolve('./handlers'),
        docspath: '/swagger' 
    }));

    // change four
    app.use('/docs', swaggerUi({
        docs: '/swagger'  
    }));

    server.listen(port, function () { 
    });
    ```   

    <span data-ttu-id="1ec8c-132">Este código faz pequenas alterações para viabilizar o trabalho com o Serviço de Aplicativo do Azure e expõe uma interface Web interativa para sua API.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-132">This code makes some small changes to let it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-the-api-locally"></a><span data-ttu-id="1ec8c-133">Como testar a API localmente</span><span class="sxs-lookup"><span data-stu-id="1ec8c-133">Test the API locally</span></span>

1. <span data-ttu-id="1ec8c-134">Inicie o aplicativo Node.js</span><span class="sxs-lookup"><span data-stu-id="1ec8c-134">Start up the Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="1ec8c-135">Navegue até http://localhost:8000/contacts para exibir o JSON para toda a lista de contatos.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-135">Browse to http://localhost:8000/contacts to view the JSON for the entire contact list.</span></span>
   
   ```json
    {
        "id": 1,
        "name": "Barney Poland",
        "email": "barney@contoso.com"
    },
    {
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    },
    {
        "id": 3,
        "name": "Lora Riggs",
        "email": "lora@contoso.com"
    }
   ```

3. <span data-ttu-id="1ec8c-136">Navegue até http://localhost:8000/contacts/2 para exibir o contato com um `id` de dois.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-136">Browse to http://localhost:8000/contacts/2 to view the contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="1ec8c-137">Teste a API usando a interface da Web de Swagger em http://localhost:8000/docs.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-137">Test the API using the Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Interface da Web de Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="1ec8c-139"><a id="createapiapp"></a> Como criar um Aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="1ec8c-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="1ec8c-140">Nesta seção, você pode usar a CLI 2.0 do Azure para criar os recursos para hospedar a API no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-140">In this section, you use the Azure CLI 2.0 to create the resources to host the API on Azure App Service.</span></span> 

1.  <span data-ttu-id="1ec8c-141">Faça logon na sua assinatura do Azure com o comando [az login](/cli/azure/#login) e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-141">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="1ec8c-142">Se você tiver várias assinaturas do Azure, altere a assinatura padrão para a desejada.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-142">If you have multiple Azure subscriptions, change the default subscription to the desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-the-api-with-git"></a><span data-ttu-id="1ec8c-143">Como implantar a API com o Git</span><span class="sxs-lookup"><span data-stu-id="1ec8c-143">Deploy the API with Git</span></span>

<span data-ttu-id="1ec8c-144">Implante seu código para o aplicativo de API enviando confirmações de seu repositório Git local para o serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-144">Deploy your code to the API app by pushing commits from your local Git repository to Azure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="1ec8c-145">Inicialize um novo repositório no diretório *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-145">Initialize a new repo in the *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="1ec8c-146">Exclua o diretório *node_modules* criado pelo npm em uma etapa anterior no tutorial do Git.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-146">Exclude the *node_modules* directory created by npm in an earlier step in the tutorial from Git.</span></span> <span data-ttu-id="1ec8c-147">Crie um novo arquivo `.gitignore` no diretório atual e adicione o seguinte texto em uma nova linha, em qualquer lugar no arquivo.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-147">Create a new `.gitignore` file in the current directory and add the following text on a new line anywhere in the file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="1ec8c-148">Confirme se a pasta `node_modules` está sendo ignorada com `git status`.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-148">Confirm the `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="1ec8c-149">Confirme as alterações no conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-149">Commit the changes to the repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push to Azure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-the-api--in-azure"></a><span data-ttu-id="1ec8c-150">Como testar a API no Azure</span><span class="sxs-lookup"><span data-stu-id="1ec8c-150">Test the API  in Azure</span></span>

1. <span data-ttu-id="1ec8c-151">Abra um navegador para http://app_name.azurewebsites.net/contacts.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-151">Open a browser to http://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="1ec8c-152">Você verá o mesmo JSON retornado como quando fez a solicitação localmente anteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-152">You see the same JSON returned as when you made the request locally earlier in the tutorial.</span></span>

   ```json
   {
       "id": 1,
       "name": "Barney Poland",
       "email": "barney@contoso.com"
   },
   {
       "id": 2,
       "name": "Lacy Barrera",
       "email": "lacy@contoso.com"
   },
   {
       "id": 3,
       "name": "Lora Riggs",
       "email": "lora@contoso.com"
   }
   ```

2. <span data-ttu-id="1ec8c-153">Em um navegador, vá para o ponto de extremidade `http://app_name.azurewebsites.net/docs` para experimentar a IU do Swagger enquanto ela é executada no Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-153">In a browser, go to the `http://app_name.azurewebsites.net/docs` endpoint to try out the Swagger UI running on Azure.</span></span>

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="1ec8c-155">Agora, você pode implantar atualizações para a API de exemplo para o Azure enviando confirmações para o repositório Git do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec8c-155">You can now deploy updates to the sample API to Azure simply by pushing commits to the Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="1ec8c-156">Limpar</span><span class="sxs-lookup"><span data-stu-id="1ec8c-156">Clean up</span></span>

<span data-ttu-id="1ec8c-157">Para limpar os recursos criados neste guia de início rápido, execute o seguinte comando da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="1ec8c-157">To clean up the resources created in this quickstart, run the following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="1ec8c-158">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="1ec8c-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="1ec8c-159">Consumo de aplicativos de API de clientes de JavaScript com CORS</span><span class="sxs-lookup"><span data-stu-id="1ec8c-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

