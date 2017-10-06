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
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a>Criar uma API RESTful Node. js e implantá-lo tooan API do aplicativo no Azure
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Este guia de início rápido mostra como toocreate uma API REST, escrito com Node.js [Express](http://expressjs.com/)usando um [Swagger](http://swagger.io/) definição e implantá-lo como um [aplicativo de API](app-service-api-apps-why-best-platform.md) no Azure. Criar aplicativo hello usando as ferramentas de linha de comando, configure recursos com hello [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)e implantar o aplicativo hello usando o Git.  No fim, você tem uma API REST funcional de exemplo em execução no Azure.

## <a name="prerequisites"></a>Pré-requisitos

* [Git](https://git-scm.com/)
* [Node.js e NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-your-environment"></a>Prepare o seu ambiente

1. Em uma janela de terminal, execute Olá máquina local do tooyour de exemplo de saudação do comando tooclone a seguir.

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. Altere o diretório de toohello que contém o código de exemplo hello.

    ```bash
    cd app-service-api-node-contact-list
    ```

3. Instale o [Swaggerize](https://www.npmjs.com/package/swaggerize-express) em seu computador local. Swaggerize é uma ferramenta que gera código Node.js para a API REST de uma definição de Swagger.

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a>Como gerar código Node.js 

Esta seção do tutorial de saudação modela um fluxo de trabalho de desenvolvimento de API em que você cria os metadados do Swagger primeiro e usa esse tooscaffold (gerar automaticamente) código do servidor de saudação API. 

Altere o diretório toohello *iniciar* pasta, em seguida, execute `yo swaggerize`. Swaggerize cria um projeto de Node. js para sua API da definição de Swagger de saudação em *api.json*.

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

Quando Swaggerize solicita um nome de projeto, use *ContactList*.
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a>Personalizar o código do projeto Olá

1. Saudação de cópia *lib* pasta em Olá *ContactList* pasta criada pelo `yo swaggerize`, em seguida, altere o diretório para *ContactList*.

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. Instalar Olá `jsonpath` e `swaggerize-ui` módulos NPM. 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. Substitua o código Olá Olá *handlers/contacts.js* com hello código a seguir: 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    Esse código utiliza os dados JSON de saudação armazenados *lib/contacts.json* servidas por *lib/contactRepository.js*. Olá novo *contacts.js* código retorna todos os contatos no repositório de saudação como uma carga JSON. 

4. Substitua o código Olá Olá **handlers/contacts/{id}.js** arquivo com hello código a seguir:

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    Esse código permite que você use um caminho tooreturn variável apenas Olá contato com uma ID especificada.

5. Substitua Olá código em **server.js** com hello código a seguir:

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

    Este código faz toolet algumas pequenas alterações que ele funciona com o serviço de aplicativo do Azure e expõe uma interface web interativos para sua API.

### <a name="test-hello-api-locally"></a>Localmente o hello teste-API

1. Iniciar o aplicativo de Node. js Olá
    ```bash
    npm start
    ```
    
2. Procurar toohttp://localhost:8000 / contata tooview Olá JSON para a lista de contatos inteira hello.
   
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

3. Procurar contato da saudação tooview toohttp://localhost:8000 contatos/2 com um `id` de dois.
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. API de saudação do teste usando a interface Olá Swagger da web no http://localhost:8000/documentos.
   
    ![Interface da Web de Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <a id="createapiapp"></a> Como criar um Aplicativo de API

Nesta seção, você pode usar hello Azure CLI 2.0 toocreate Olá recursos toohost Olá API no serviço de aplicativo do Azure. 

1.  Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela.

    ```azurecli-interactive
    az login
    ```

2. Se você tiver várias assinaturas do Azure, alteração saudação padrão assinatura toohello desejado um.

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a>Implantar a API de saudação com Git

Implante seu aplicativo de API do código toohello enviando confirmações de seu local tooAzure de repositório do Git do serviço de aplicativo.

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. Inicializar um novo repositório no hello *ContactList* directory. 

    ```bash
    git init .
    ```

3. Excluir Olá *node_modules* diretório criado pelo npm em uma etapa anterior no tutorial de saudação do Git. Criar um novo `.gitignore` no diretório atual hello e adicionar Olá texto a seguir em uma nova linha em qualquer lugar no arquivo hello.

    ```
    node_modules/
    ```
    Confirmar Olá `node_modules` pasta está sendo ignorada com `git status`.

4. Confirme Olá alterações toohello repositório.
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a>Saudação de teste API no Azure

1. Abra um navegador toohttp://app_name.azurewebsites.net/contacts. Você verá Olá que mesmo JSON retornado como quando você fez a solicitação de saudação localmente anteriormente no tutorial de saudação.

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

2. Em um navegador, vá toohello `http://app_name.azurewebsites.net/docs` tootry de ponto de extremidade out Olá Swagger da interface do usuário em execução no Azure.

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    Agora você pode implantar atualizações toohello exemplo API tooAzure enviando confirmações toohello Azure Git repositório.

## <a name="clean-up"></a>Limpar

tooclean recursos Olá criado neste guia de início rápido, execute Olá após o comando CLI do Azure:

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a>Próxima etapa 
> [!div class="nextstepaction"]
> [Consumo de aplicativos de API de clientes de JavaScript com CORS](app-service-api-cors-consume-javascript.md)

