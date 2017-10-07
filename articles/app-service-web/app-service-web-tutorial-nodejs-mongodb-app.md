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
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a>Compilar um aplicativo Web Node.js e MongoDB no Azure

Os aplicativos Web do Azure fornecem um serviço de hospedagem na Web altamente escalonável, com aplicação automática de patches. Este tutorial mostra como toocreate um Node. js aplicativo no Azure da web e conecte-o banco de dados do MongoDB tooa. Quando terminar, você terá um aplicativo MEAN (MongoDB, Express, AngularJS e Node.js) executando em [Serviço de Aplicativo do Azure](app-service-web-overview.md). Para simplificar, o aplicativo de exemplo hello usa Olá [framework do web MEAN.js](http://meanjs.org/).

![Aplicativo MEAN.js em execução no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

O que você aprenderá:

> [!div class="checklist"]
> * Criar um banco de dados MongoDB no Azure
> * Conecte-se um tooMongoDB de aplicativo Node. js
> * Implantar Olá aplicativo tooAzure
> * Atualizar o modelo de dados hello e reimplantar o aplicativo hello
> * Transmitir logs de diagnóstico do Azure
> * Gerenciar o aplicativo hello em Olá portal do Azure

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial:

1. [Instalar o Git](https://git-scm.com/)
1. [Instalar o Node.js e o NPM](https://nodejs.org/)
1. [Instale o Gulp.js](http://gulpjs.com/) (exigido pelo [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))
1. [Instale e execute o MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-mongodb"></a>Testar o MongoDB local

Janela do terminal Olá aberto e `cd` toohello `bin` diretório de instalação do MongoDB. Você pode usar essa janela do terminal toorun todos os comandos de saudação neste tutorial.

Execute `mongo` no servidor tooyour MongoDB local tooconnect terminal hello.

```bash
mongo
```

Se sua conexão tiver êxito, então seu banco de dados MongoDB já está sendo executado. Se não, certifique-se de que seu banco de dados local do MongoDB é iniciado, seguindo as etapas de saudação em [instalar MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/). Geralmente, MongoDB está instalado, mas você ainda precisa toostart-lo executando `mongod`. 

Quando você terminar de teste seu banco de dados do MongoDB, digite `Ctrl+C` em Olá terminal. 

## <a name="create-local-nodejs-app"></a>Criar aplicativo Node.js local

Nesta etapa, você configura Olá local Node. js projeto.

### <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello

Na janela do terminal hello, `cd` tooa diretório de trabalho.  

Execute Olá repositório de exemplo do comando tooclone Olá a seguir. 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

Esse repositório de exemplo contém uma cópia da saudação [MEAN.js repositório](https://github.com/meanjs/mean). É modificada toorun no serviço de aplicativo (para obter mais informações, consulte o repositório de MEAN.js Olá [arquivo Leiame](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).

### <a name="run-hello-application"></a>Executar o aplicativo hello

Execute Olá pacotes de saudação necessário tooinstall comandos a seguir e inicie o aplicativo hello.

```bash
cd meanjs
npm install
npm start
```

Quando o aplicativo hello está totalmente carregado, você verá algo semelhante toohello seguinte mensagem:

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

Navegue toohttp://localhost:3000 em um navegador. Clique em **inscrever** Olá menu superior e criar um usuário de teste. 

Olá MEAN.js aplicativo de exemplo armazena dados de usuário no banco de dados de saudação. Se tiver êxito na criação de um usuário e entrar, seu aplicativo está gravando dados toohello MongoDB banco de dados local.

![MEAN.js se conecta com êxito tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

Selecione **Administração > Gerenciar artigos** tooadd alguns artigos.

toostop Node. js a qualquer momento, pressione `Ctrl+C` em Olá terminal. 

## <a name="create-production-mongodb"></a>Criar MongoDB de produção

Ness etapa, você cria um banco de dados MongoDB no Azure. Quando seu aplicativo é implantado tooAzure, ele usa esse banco de dados de nuvem.

Para o MongoDB, este tutorial usa o [BD Cosmos do Azure](/azure/documentdb/). O BD Cosmos dá suporte a conexões de cliente do MongoDB.

### <a name="log-in-tooazure"></a>Faça logon no tooAzure

Você usará hello Azure CLI 2.0 toocreate Olá recursos necessários toohost seu aplicativo no Azure. Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela.

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Olá exemplo a seguir cria um grupo de recursos na região Europa Ocidental de saudação.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

Saudação de uso [locais de lista do serviço de aplicativo az](/cli/azure/appservice#list-locations) locais disponíveis toolist de comando CLI do Azure. 

### <a name="create-a-cosmos-db-account"></a>Criar uma conta do BD Cosmos

Crie uma conta de banco de dados do Cosmos com hello [cosmosdb az criar](/cli/azure/cosmosdb#create) comando.

Olá a seguir de comando, substitua um nome exclusivo do banco de dados do Cosmos para Olá  *\<cosmosdb_name >* espaço reservado. Esse nome é usado como parte de saudação do ponto de extremidade de banco de dados do Cosmos Olá, `https://<cosmosdb_name>.documents.azure.com/`, portanto, o nome do hello deve toobe exclusivo em todas as contas de banco de dados do Cosmos no Azure. Olá nome deve conter apenas letras minúsculas, números e caracteres de hífen (-) hello e deve ter entre 3 e 50 caracteres.

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

Olá *– tipo MongoDB* parâmetro habilita conexões de cliente do MongoDB.

Quando Olá Cosmos DB conta é criada, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

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

## <a name="connect-app-tooproduction-mongodb"></a>Conecte-se o aplicativo tooproduction MongoDB

Nesta etapa, você pode se conectar o MEAN.js aplicativo toohello Cosmos DB de dados de exemplo que você acabou de criar, usando uma cadeia de caracteres de conexão do MongoDB. 

### <a name="retrieve-hello-database-key"></a>Recuperar a chave de banco de dados de saudação

tooconnect toohello Cosmos banco de dados, você precisa de chave de banco de dados de saudação. Saudação de uso [chaves de lista az cosmosdb](/cli/azure/cosmosdb#list-keys) chave primária do comando tooretrieve hello.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Copie o valor de saudação do `primaryMasterKey`. Você precisará dessas informações na próxima etapa do hello.

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Configurar a cadeia de caracteres de conexão de saudação em seu aplicativo Node. js

Em seu repositório do MEAN.js, abra _config/env/production.js_.

Em Olá `db` do objeto, atualize o valor de saudação do `uri`:

* Substituir saudação dois  *\<cosmosdb_name >* espaços reservados com seu nome de banco de dados do banco de dados do Cosmos.
* Substituir saudação  *\<primary_master_key >* espaço reservado com chave Olá você copiou na etapa anterior hello.

Olá, código a seguir mostra Olá `db` objeto:

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

Olá `ssl=true` opção é necessária porque [Cosmos DB requer SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 

Salve suas alterações.

### <a name="test-hello-application-in-production-mode"></a>Testar o aplicativo hello no modo de produção 

Olá executar scripts de comando toominify e pacote para o ambiente de produção de hello a seguir. Esse processo gera arquivos de saudação necessários ao ambiente de produção de hello.

```bash
gulp prod
```

Olá execução após a cadeia de conexão do comando toouse Olá configurada na _config/env/production.js_.

```bash
NODE_ENV=production node server.js
```

`NODE_ENV=production`Define a variável de ambiente Olá que informa toorun Node. js no ambiente de produção de hello.  `node server.js`Inicia Olá servidor Node.js com `server.js` na raiz do repositório. É dessa forma que o aplicativo Node.js é carregado no Azure. 

Quando o aplicativo hello é carregado, verifique toomake se ele está em execução no ambiente de produção de hello:

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

Navegue toohttp://localhost:8443 em um navegador. Clique em **inscrever** Olá menu superior e criar um usuário de teste. Se você estiver criando um usuário e entrar com êxito, seu aplicativo está gravando dados toohello DB Cosmos banco de dados no Azure. 

Olá terminal, parar Node. js digitando `Ctrl+C`. 

## <a name="deploy-app-tooazure"></a>Implantar o aplicativo tooAzure

Nesta etapa, você deve implantar seu aplicativo de Node. js conectado MongoDB tooAzure do serviço de aplicativo.

### <a name="create-an-app-service-plan"></a>Criar um plano de Serviço de Aplicativo

Criar um plano de serviço de aplicativo com hello [criar plano de serviço de aplicativo az](/cli/azure/appservice/plan#create) comando. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Olá, exemplo a seguir cria um plano de serviço de aplicativo chamado _myAppServicePlan_ usando Olá **livre** preço:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Quando Olá plano de serviço de aplicativo é criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

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

### <a name="create-a-web-app"></a>Criar um aplicativo Web

Criar um aplicativo web no hello `myAppServicePlan` plano de serviço de aplicativo com hello [az webapp criar](/cli/azure/webapp#create) comando. 

Fornece de aplicativo de web Hello você hospedagem espaço toodeploy seu código e fornece uma URL para você Olá tooview aplicativo implantado. Use toocreate Olá web app. 

Olá a seguir de comando, substitua Olá  *\<app_name >* espaço reservado com um nome exclusivo do aplicativo. Esse nome é usado como parte de saudação da saudação padrão URL do aplicativo web de hello, para que o nome do hello deve toobe exclusivo entre todos os aplicativos no serviço de aplicativo do Azure. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Quando o aplicativo da web de saudação tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir: 

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

### <a name="configure-an-environment-variable"></a>Configurar um variável de ambiente

Olá tutorial, você Olá banco de dados conexão cadeia de caracteres codificada em anteriormente _config/env/production.js_. Para manter a prática recomendada de segurança, convém tookeep dados confidenciais fora do seu repositório Git. Para seu aplicativo em execução no Azure, você usará uma variável de ambiente.

No serviço de aplicativo, você definir variáveis de ambiente como _configurações do aplicativo_ usando Olá [az webapp configuração appsettings atualizar](/cli/azure/webapp/config/appsettings#update) comando. 

Olá exemplo a seguir configura um `MONGODB_URI` configuração do aplicativo em seu aplicativo web do Azure. Substituir saudação  *\<app_name >*,  *\<cosmosdb_name >*, e  *\<primary_master_key >* espaços reservados.

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

No código Node.js, você acessa essa configuração de aplicativo com `process.env.MONGODB_URI`, assim como você teria acesso a qualquer variável de ambiente. 

Agora, desfazer suas alterações too_config/env/production.js_ com hello comando a seguir:

```bash
git checkout -- .
```

Abra _config/env/production.js_ novamente. Observe que esse aplicativo de MEAN.js saudação padrão já está configurado toouse Olá `MONGODB_URI` variável de ambiente que você criou.

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a>Configurar a implantação do git local 

Saudação de uso [usuário az webapp implantação definido](/cli/azure/webapp/deployment/user#set) toocreate credenciais para a implantação de comando.

Você pode implantar seu tooAzure de aplicativo do serviço de aplicativo de várias maneiras, incluindo o FTP, Git local, GitHub, Visual Studio Team Services e BitBucket. Para FTP e Git local, é necessário toohave um usuário de implantação configurado no hello server tooauthenticate sua implantação. Este usuário de implantação está no nível de conta e é diferente da sua conta de assinatura do Azure. Você só precisa tooconfigure esse usuário de implantação uma vez.

Olá a seguir de comando, substitua  *\<nome de usuário >* e  *\<senha >* com um novo nome de usuário e senha. nome de usuário Olá deve ser exclusivo. Hello senha deve ter pelo menos oito caracteres, com dois Olá após três elementos: letras, números, símbolos. Se você receber um ` 'Conflict'. Details: 409` erro, o nome de usuário de saudação de alteração. Se receber um erro ` 'Bad Request'. Details: 400`, use uma senha mais forte.

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

Nome de usuário de saudação do registro e a senha para uso em etapas posteriores quando você implanta o aplicativo hello.

Saudação de uso [origem de implantação de aplicativo Web do az-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) comando tooconfigure Git acesso toohello Azure o aplicativo web local. 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

Quando o usuário de implantação Olá é configurado, Olá CLI do Azure mostra Olá URL de implantação para seu aplicativo web do Azure no hello formato a seguir:

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

Copie Olá saída de terminal Olá, pois ela será usada na próxima etapa do hello. 

### <a name="push-tooazure-from-git"></a>TooAzure de envio por push do Git

Adicione um repositório Git local do Azure tooyour remoto. 

```bash
git remote add azure <paste_copied_url_here> 
```

Push toohello toodeploy remoto do Azure seu aplicativo Node. js. Você será solicitado para senha Olá fornecidas anteriormente como parte da criação de saudação do usuário de implantação de saudação. 

```bash
git push azure master
```

Durante a implantação, o Serviço de Aplicativo do Azure comunica seu andamento com o Git.

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

Você pode perceber que executa o processo de implantação de saudação [Gulp](http://gulpjs.com/) depois `npm install`. Serviço de aplicativo não executa tarefas Gulp ou pesado durante a implantação, para que este repositório de exemplo tem dois adicionais arquivos no seu tooenable de diretório raiz-lo: 

- _.Deployment_ -esse arquivo informa ao serviço de aplicativo toorun `bash deploy.sh` como script de implantação personalizada hello.
- _Deploy.sh_ -Olá script de implantação personalizada. Se você revisar o arquivo hello, você verá que ele seja executado `gulp prod` depois `npm install` e `bower install`. 

Você pode usar essa abordagem tooadd tooyour qualquer etapa implantação baseada em Git. Se você reiniciar seu aplicativo Web do Azure em qualquer ponto, o Serviço de Aplicativo não executará novamente essas tarefas de automação.

### <a name="browse-toohello-azure-web-app"></a>Procurar o aplicativo web do Azure de toohello 

Procurar toohello implantado um aplicativo da web usando um navegador da web. 

```bash 
http://<app_name>.azurewebsites.net 
``` 

Clique em **inscrever** Olá menu superior e criar um usuário fictício. 

Se tiver êxito e o aplicativo hello automaticamente entra em toohello criou o usuário e, em seguida, seu aplicativo MEAN.js no Azure tem banco de dados conectividade toohello MongoDB (Cosmos DB). 

![Aplicativo MEAN.js em execução no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Selecione **Administração > Gerenciar artigos** tooadd alguns artigos. 

**Parabéns!** Você está executando um aplicativo Node.js controlado por dados no Serviço de Aplicativo do Azure.

## <a name="update-data-model-and-redeploy"></a>Atualizar o modelo de dados e reimplantar

Nesta etapa, você alterar Olá `article` dados de modelo e publicar seu tooAzure de alteração.

### <a name="update-hello-data-model"></a>Atualizar o modelo de dados Olá

Abra _modules/articles/server/models/article.server.model.js_.

Em `ArticleSchema`, adicione um tipo `String` chamado `comment`. Quando terminar, seu código de esquema deverá ter essa aparência:

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

### <a name="update-hello-articles-code"></a>Atualizar o código de artigos Olá

Atualizar o restante de saudação do seu `articles` código toouse `comment`.

Há cinco arquivos necessários toomodify: controlador de saudação do servidor e modos de exibição de cliente Olá quatro. 

Abra _modules/articles/server/controllers/articles.server.controller.js_.

Em Olá `update` de função, adicione uma atribuição de `article.comment`. Olá, código a seguir mostra Olá concluída `update` função:

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

Abra _modules/articles/client/views/view-article.client.view.html_.

Acima de fechamento Olá `</section>` marca, adicione Olá toodisplay linha a seguir `comment` junto com o restante de saudação do dados de artigo de saudação:

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

Abra _modules/articles/client/views/list-articles.client.view.html_.

Acima de fechamento Olá `</a>` marca, adicione Olá toodisplay linha a seguir `comment` junto com o restante de saudação do dados de artigo de saudação:

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

Abra _modules/articles/client/views/admin/list-articles.client.view.html_.

Olá interna `<div class="list-group">` elemento e acima de fechamento Olá `</a>` marca, adicione Olá toodisplay linha a seguir `comment` junto com o restante de saudação do dados de artigo de saudação:

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

Abra _modules/articles/client/views/admin/form-article.client.view.html_.

Localize Olá `<div class="form-group">` elemento que contém o botão de envio de saudação, que tem esta aparência:

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

Acima essa marca, adicione outro `<div class="form-group">` elemento que permite que as pessoas Editar Olá `comment` campo. Seu novo elemento deve ter esta aparência:

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a>Testar suas alterações localmente

Salve todas as alterações.

Teste suas alterações em modo de produção novamente.

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> Lembre-se de que seu _config/env/production.js_ foi revertido e Olá `MONGODB_URI` variável de ambiente é definida somente em seu aplicativo web do Azure e não no computador local. Se você examinar o arquivo de configuração Olá, você encontrar esse Olá padrões de configuração de produção toouse um banco de dados local do MongoDB. Isso garante seus dados de produção não sejam tocados ao testar suas alterações de código localmente.

Navegue muito`http://localhost:8443` em um navegador e certifique-se de que você está conectado.

Selecione **Administração > Gerenciar artigos**, em seguida, adicionar um artigo selecionando Olá  **+**  botão.

Você verá Olá novo `Comment` caixa de texto agora.

![Comentário adicionado campo tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

Olá terminal, parar Node. js digitando `Ctrl+C`. 

### <a name="publish-changes-tooazure"></a>Publicar alterações tooAzure

Confirmar as alterações no Git, em seguida, push Olá tooAzure de alterações de código.

```bash
git commit -am "added article comment"
git push azure master
```

Uma vez Olá `git push` é concluída, navegue tooyour aplicativo de web do Azure e experimente a nova funcionalidade de saudação.

![Alterações de modelo e o banco de dados publicado tooAzure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

Se você adicionou artigos anteriores, ainda será possível vê-los. Dados existentes no BD Cosmos não são perdidos. Além disso, o esquema de dados de toohello atualizações e deixa os dados existentes intactas.

## <a name="stream-diagnostic-logs"></a>Logs de diagnóstico de fluxo 

Enquanto seu aplicativo Node. js é executado no serviço de aplicativo do Azure, você pode obter Olá console logs canalizado tooyour terminal. Dessa forma, você pode obter Olá mensagens de diagnóstico mesmo toohelp depurar erros de aplicativo.

log toostart streaming use Olá [final de log webapp az](/cli/azure/webapp/log#tail) comando.

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

Depois de iniciado o log de streaming, atualize seu aplicativo web do Azure no hello navegador tooget parte do tráfego da web. Agora, você verá logs do console conectado tooyour terminal.

Para interromper o streaming de log a qualquer momento, digite `Ctrl+C`. 

## <a name="manage-your-azure-web-app"></a>Gerenciar seu aplicativo Web do Azure

Vá toohello [portal do Azure](https://portal.azure.com) toosee Olá web aplicativo que você criou.

No menu à esquerda do hello, clique em **serviços de aplicativos**, clique em nome de saudação do seu aplicativo web do Azure.

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

Por padrão, o portal de saudação mostra seu aplicativo de web **visão geral** página. Esta página fornece uma visão de como está seu aplicativo. Aqui, você também pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir. guias de Olá no lado esquerdo de saudação da página de saudação mostram páginas de configuração diferentes de hello, que você pode abrir.

![Página Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a>Próximas etapas

O que você aprendeu:

> [!div class="checklist"]
> * Criar um banco de dados MongoDB no Azure
> * Conecte-se um tooMongoDB de aplicativo Node. js
> * Implantar Olá aplicativo tooAzure
> * Atualizar o modelo de dados hello e reimplantar o aplicativo hello
> * Logs de fluxo do Azure tooyour terminal
> * Gerenciar o aplicativo hello em Olá portal do Azure

Avançar toolearn tutorial do próximo toohello como toomap um DNS personalizado nome tooyour web app.

> [!div class="nextstepaction"] 
> [Mapear um tooAzure de nome DNS de personalizada existente aplicativos Web](app-service-web-tutorial-custom-domain.md)
