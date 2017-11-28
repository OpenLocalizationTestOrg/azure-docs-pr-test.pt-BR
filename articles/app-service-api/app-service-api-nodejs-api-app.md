---
title: "aplicativo aaaNode.js API no serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como toocreate uma API RESTful do Node.js e implante-o aplicativo tooan API no serviço de aplicativo do Azure."
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
ms.openlocfilehash: 3b3229c1453b6ca4d06bef26f476e92afda4e244
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a><span data-ttu-id="96310-103">Criar uma API RESTful Node. js e implantá-lo tooan API do aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="96310-103">Build a Node.js RESTful API and deploy it tooan API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="96310-104">Este guia de início rápido mostra como toocreate uma API REST, escrito com Node.js [Express](http://expressjs.com/)usando um [Swagger](http://swagger.io/) definição e implantá-lo como um [aplicativo de API](app-service-api-apps-why-best-platform.md) no Azure.</span><span class="sxs-lookup"><span data-stu-id="96310-104">This quickstart shows how toocreate a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="96310-105">Criar aplicativo hello usando as ferramentas de linha de comando, configure recursos com hello [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)e implantar o aplicativo hello usando o Git.</span><span class="sxs-lookup"><span data-stu-id="96310-105">You create hello app using command-line tools, configure resources with hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy hello app using Git.</span></span>  <span data-ttu-id="96310-106">No fim, você tem uma API REST funcional de exemplo em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="96310-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96310-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="96310-107">Prerequisites</span></span>

* [<span data-ttu-id="96310-108">Git</span><span class="sxs-lookup"><span data-stu-id="96310-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="96310-109">Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="96310-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="96310-110">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="96310-110">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="96310-111">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="96310-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="96310-112">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="96310-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="96310-113">Prepare o seu ambiente</span><span class="sxs-lookup"><span data-stu-id="96310-113">Prepare your environment</span></span>

1. <span data-ttu-id="96310-114">Em uma janela de terminal, execute Olá máquina local do tooyour de exemplo de saudação do comando tooclone a seguir.</span><span class="sxs-lookup"><span data-stu-id="96310-114">In a terminal window, run hello following command tooclone hello sample tooyour local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="96310-115">Altere o diretório de toohello que contém o código de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="96310-115">Change toohello directory that contains hello sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="96310-116">Instale o [Swaggerize](https://www.npmjs.com/package/swaggerize-express) em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="96310-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="96310-117">Swaggerize é uma ferramenta que gera código Node.js para a API REST de uma definição de Swagger.</span><span class="sxs-lookup"><span data-stu-id="96310-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="96310-118">Como gerar código Node.js</span><span class="sxs-lookup"><span data-stu-id="96310-118">Generate Node.js code</span></span> 

<span data-ttu-id="96310-119">Esta seção do tutorial de saudação modela um fluxo de trabalho de desenvolvimento de API em que você cria os metadados do Swagger primeiro e usa esse tooscaffold (gerar automaticamente) código do servidor de saudação API.</span><span class="sxs-lookup"><span data-stu-id="96310-119">This section of hello tutorial models an API development workflow in which you create Swagger metadata first and use that tooscaffold (auto-generate) server code for hello API.</span></span> 

<span data-ttu-id="96310-120">Altere o diretório toohello *iniciar* pasta, em seguida, execute `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="96310-120">Change directory toohello *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="96310-121">Swaggerize cria um projeto de Node. js para sua API da definição de Swagger de saudação em *api.json*.</span><span class="sxs-lookup"><span data-stu-id="96310-121">Swaggerize creates a Node.js project for your API from hello Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="96310-122">Quando Swaggerize solicita um nome de projeto, use *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="96310-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a><span data-ttu-id="96310-123">Personalizar o código do projeto Olá</span><span class="sxs-lookup"><span data-stu-id="96310-123">Customize hello project code</span></span>

1. <span data-ttu-id="96310-124">Saudação de cópia *lib* pasta em Olá *ContactList* pasta criada pelo `yo swaggerize`, em seguida, altere o diretório para *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="96310-124">Copy hello *lib* folder into hello *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="96310-125">Instalar Olá `jsonpath` e `swaggerize-ui` módulos NPM.</span><span class="sxs-lookup"><span data-stu-id="96310-125">Install hello `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="96310-126">Substitua o código Olá Olá *handlers/contacts.js* com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="96310-126">Replace hello code in hello *handlers/contacts.js* with hello following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="96310-127">Esse código utiliza os dados JSON de saudação armazenados *lib/contacts.json* servidas por *lib/contactRepository.js*.</span><span class="sxs-lookup"><span data-stu-id="96310-127">This code uses hello JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="96310-128">Olá novo *contacts.js* código retorna todos os contatos no repositório de saudação como uma carga JSON.</span><span class="sxs-lookup"><span data-stu-id="96310-128">hello new *contacts.js* code returns all contacts in hello repository as a JSON payload.</span></span> 

4. <span data-ttu-id="96310-129">Substitua o código Olá Olá **handlers/contacts/{id}.js** arquivo com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="96310-129">Replace hello code in hello **handlers/contacts/{id}.js** file with hello following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="96310-130">Esse código permite que você use um caminho tooreturn variável apenas Olá contato com uma ID especificada.</span><span class="sxs-lookup"><span data-stu-id="96310-130">This code lets you use a path variable tooreturn only hello contact with a given ID.</span></span>

5. <span data-ttu-id="96310-131">Substitua Olá código em **server.js** com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="96310-131">Replace hello code in **server.js** with hello following code:</span></span>

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

    <span data-ttu-id="96310-132">Este código faz toolet algumas pequenas alterações que ele funciona com o serviço de aplicativo do Azure e expõe uma interface web interativos para sua API.</span><span class="sxs-lookup"><span data-stu-id="96310-132">This code makes some small changes toolet it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-hello-api-locally"></a><span data-ttu-id="96310-133">Localmente o hello teste-API</span><span class="sxs-lookup"><span data-stu-id="96310-133">Test hello API locally</span></span>

1. <span data-ttu-id="96310-134">Iniciar o aplicativo de Node. js Olá</span><span class="sxs-lookup"><span data-stu-id="96310-134">Start up hello Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="96310-135">Procurar toohttp://localhost:8000 / contata tooview Olá JSON para a lista de contatos inteira hello.</span><span class="sxs-lookup"><span data-stu-id="96310-135">Browse toohttp://localhost:8000/contacts tooview hello JSON for hello entire contact list.</span></span>
   
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

3. <span data-ttu-id="96310-136">Procurar contato da saudação tooview toohttp://localhost:8000 contatos/2 com um `id` de dois.</span><span class="sxs-lookup"><span data-stu-id="96310-136">Browse toohttp://localhost:8000/contacts/2 tooview hello contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="96310-137">API de saudação do teste usando a interface Olá Swagger da web no http://localhost:8000/documentos.</span><span class="sxs-lookup"><span data-stu-id="96310-137">Test hello API using hello Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Interface da Web de Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="96310-139"><a id="createapiapp"></a> Como criar um Aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="96310-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="96310-140">Nesta seção, você pode usar hello Azure CLI 2.0 toocreate Olá recursos toohost Olá API no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="96310-140">In this section, you use hello Azure CLI 2.0 toocreate hello resources toohost hello API on Azure App Service.</span></span> 

1.  <span data-ttu-id="96310-141">Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="96310-141">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="96310-142">Se você tiver várias assinaturas do Azure, alteração saudação padrão assinatura toohello desejado um.</span><span class="sxs-lookup"><span data-stu-id="96310-142">If you have multiple Azure subscriptions, change hello default subscription toohello desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a><span data-ttu-id="96310-143">Implantar a API de saudação com Git</span><span class="sxs-lookup"><span data-stu-id="96310-143">Deploy hello API with Git</span></span>

<span data-ttu-id="96310-144">Implante seu aplicativo de API do código toohello enviando confirmações de seu local tooAzure de repositório do Git do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="96310-144">Deploy your code toohello API app by pushing commits from your local Git repository tooAzure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="96310-145">Inicializar um novo repositório no hello *ContactList* directory.</span><span class="sxs-lookup"><span data-stu-id="96310-145">Initialize a new repo in hello *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="96310-146">Excluir Olá *node_modules* diretório criado pelo npm em uma etapa anterior no tutorial de saudação do Git.</span><span class="sxs-lookup"><span data-stu-id="96310-146">Exclude hello *node_modules* directory created by npm in an earlier step in hello tutorial from Git.</span></span> <span data-ttu-id="96310-147">Criar um novo `.gitignore` no diretório atual hello e adicionar Olá texto a seguir em uma nova linha em qualquer lugar no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="96310-147">Create a new `.gitignore` file in hello current directory and add hello following text on a new line anywhere in hello file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="96310-148">Confirmar Olá `node_modules` pasta está sendo ignorada com `git status`.</span><span class="sxs-lookup"><span data-stu-id="96310-148">Confirm hello `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="96310-149">Confirme Olá alterações toohello repositório.</span><span class="sxs-lookup"><span data-stu-id="96310-149">Commit hello changes toohello repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a><span data-ttu-id="96310-150">Saudação de teste API no Azure</span><span class="sxs-lookup"><span data-stu-id="96310-150">Test hello API  in Azure</span></span>

1. <span data-ttu-id="96310-151">Abra um navegador toohttp://app_name.azurewebsites.net/contacts.</span><span class="sxs-lookup"><span data-stu-id="96310-151">Open a browser toohttp://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="96310-152">Você verá Olá que mesmo JSON retornado como quando você fez a solicitação de saudação localmente anteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="96310-152">You see hello same JSON returned as when you made hello request locally earlier in hello tutorial.</span></span>

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

2. <span data-ttu-id="96310-153">Em um navegador, vá toohello `http://app_name.azurewebsites.net/docs` tootry de ponto de extremidade out Olá Swagger da interface do usuário em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="96310-153">In a browser, go toohello `http://app_name.azurewebsites.net/docs` endpoint tootry out hello Swagger UI running on Azure.</span></span>

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="96310-155">Agora você pode implantar atualizações toohello exemplo API tooAzure enviando confirmações toohello Azure Git repositório.</span><span class="sxs-lookup"><span data-stu-id="96310-155">You can now deploy updates toohello sample API tooAzure simply by pushing commits toohello Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="96310-156">Limpar</span><span class="sxs-lookup"><span data-stu-id="96310-156">Clean up</span></span>

<span data-ttu-id="96310-157">tooclean recursos Olá criado neste guia de início rápido, execute Olá após o comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="96310-157">tooclean up hello resources created in this quickstart, run hello following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="96310-158">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="96310-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="96310-159">Consumo de aplicativos de API de clientes de JavaScript com CORS</span><span class="sxs-lookup"><span data-stu-id="96310-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

