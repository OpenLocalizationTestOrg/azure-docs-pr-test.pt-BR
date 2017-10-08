---
title: aaaSecure uma API da web do Active Directory do Azure v 2.0 usando Node. js | Microsoft Docs
description: Saiba como toobuild um Node. js web API que aceita tokens de uma conta pessoal da Microsoft e de contas corporativa ou escolar.
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a>Proteger uma API Web usando Node.js
> [!NOTE]
> Nem todos os recursos e cenários de Active Directory do Azure funcionam com o ponto de extremidade do hello v 2.0. toodetermine se você deve usar o ponto de extremidade do hello v 2.0 ou ponto de extremidade Olá v 1.0, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
> 
> 

Quando você usa o ponto de extremidade do hello Azure Active Directory (AD do Azure) v 2.0, você pode usar [OAuth 2.0](active-directory-v2-protocols.md) tokens de acesso tooprotect sua API da web. Com os tokens de acesso OAuth 2.0, os usuários que têm uma conta da Microsoft pessoal e contas corporativas ou de estudante podem acessar sua API Web com segurança.

*Passport* é middleware de autenticação para o Node.js. Flexível e modular, o Passport pode ser colocado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify. No Passport, um conjunto abrangente de estratégias dão suporte à autenticação com o uso de um nome de usuário e uma senha, Facebook, Twitter e outras opções. Desenvolvemos uma estratégia para o Azure AD. Neste artigo, mostramos como tooinstall Olá módulo e, em seguida, adicionar Olá AD do Azure `passport-azure-ad` plug-in.

## <a name="download"></a>Baixar
código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs). tutorial de saudação toofollow, você pode [baixar esqueleto de saudação do aplicativo como um arquivo. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), ou esqueleto de saudação do clone:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

Você também pode obter aplicativo hello concluída final Olá deste tutorial.

## <a name="1-register-an-app"></a>1: registrar um aplicativo
Criar um novo aplicativo no [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou execute [essas etapas detalhadas](active-directory-v2-app-registration.md) tooregister um aplicativo. Verifique se você:

* Saudação de cópia **Id do aplicativo** atribuído tooyour aplicativo. Ela será necessária para este tutorial.
* Adicionar Olá **Mobile** plataforma para seu aplicativo.
* Saudação de cópia **URI de redirecionamento** do portal de saudação. Você deve usar o valor do URI de padrão de saudação `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-install-nodejs"></a>2: instalar o Node.js
exemplo de hello toouse para este tutorial, você deve [instalar Node. js](http://nodejs.org).

## <a name="3-install-mongodb"></a>3: instalar o MongoDB
toosuccessfully usar este exemplo, você deve [instalar MongoDB](http://www.mongodb.org). Neste exemplo, você usar MongoDB toomake API REST persistente em instâncias de servidor.

> [!NOTE]
> Neste artigo, vamos supor que você use Olá instalação e o servidor de pontos de extremidade padrão para o MongoDB: mongodb://localhost.
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a>4: instalar Olá restify módulos na sua API da web
Usamos Resitfy toobuild nossa API REST. O Restify é uma estrutura de aplicativo do Node.js mínima e flexível, derivada do Express. Restify tem um conjunto robusto de recursos que você pode usar toobuild APIs REST sobre conectar.

### <a name="install-restify"></a>Instalar o Restify
1.  Em um prompt de comando, altere o diretório de saudação muito**azuread**:

    `cd azuread`

    Se hello **doWindows Azure** diretório não existe, criá-lo:

    `mkdir azuread`

2.  Instale o Restify:

    `npm install restify`

    saída de Hello desse comando deve ter esta aparência:

    ```
    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a>Você obteve um erro?
Em alguns sistemas operacionais, quando você usa Olá `npm` de comando, você verá esta mensagem: `Error: EPERM, chmod '/usr/local/bin/..'`. Erro de saudação é seguido por uma solicitação que você tente conta de saudação em execução como administrador. Se isso ocorrer, use o comando Olá `sudo` toorun `npm` em um nível de privilégio mais alto.

#### <a name="did-you-get-an-error-related-toodtrace"></a>Você obteve um erro relacionado tooDTrace?
Quando você instala o restify, pode ver esta mensagem:

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

Restify tem um tootrace poderoso mecanismo chamadas REST usando DTrace. No entanto, o DTrace não está disponível em muitos sistemas operacionais. Você pode ignorar essa mensagem de erro com segurança.


## <a name="5-install-passportjs-in-your-web-api"></a>5: instalar o Passport.js na sua API Web
1.  No prompt de comando hello, altere o diretório de saudação muito**azuread**.

2.  Instale o Passport.js:

    `npm install passport`

    saída de saudação do comando Olá deve ter esta aparência:

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a>6: Adicionar de API da web do ad de azure passport tooyour
Em seguida, adicione a estratégia de OAuth Olá, usando o passport-doWindows Azure. `passport-azuread` é um pacote de estratégias que conectam o Azure AD ao Passport. Usaremos essa estratégia para tokens de portador neste exemplo de API Rest.

> [!NOTE]
> Embora o OAuth 2.0 forneça uma estrutura na qual qualquer tipo de token conhecido possa ser emitido, determinados tipos de token são comumente usados. Os tokens de portador são pontos de extremidade de tooprotect usadas com frequência. Tokens de portador são tipo de hello mais amplamente emitido de token do OAuth 2.0. Muitas implementações do OAuth 2.0 supõem que os tokens de portador são Olá único tipo de token emitido.
> 
> 

1.  Em um prompt de comando, altere o diretório de saudação muito**azuread**.

    `cd azuread`

2.  Instalar Olá Passport.js `passport-azure-ad` módulo:

    `npm install passport-azure-ad`

    saída de saudação do comando Olá deve ter esta aparência:

    ```
    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a>7: Adicionar MongoDB módulos tooyour web API
Neste exemplo, usamos o MongoDB como nosso armazenamento de dados. 

1.  Instalar Mongoose, amplamente utilizado plug-in, toomanage modelos e esquemas: 

    `npm install mongoose`

2.  Instale o driver de banco de dados de saudação para o MongoDB, que também é chamado MongoDB:

    `npm install mongodb`

## <a name="8-install-additional-modules"></a>8: instalar módulos adicionais
Instale Olá restantes módulos necessários.

1.  Em um prompt de comando, altere o diretório de saudação muito**azuread**:

    `cd azuread`

2.  Digite hello comandos a seguir. comandos de saudação instalam Olá módulos no diretório node_modules a seguir:

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a>9: criar um arquivo Server.js para suas dependências
Um arquivo Server.js mantém maioria de saudação da funcionalidade de saudação do seu servidor de API da web. Adicione mais seu toothis do arquivo de código. Para fins de produção, você pode refatorar funcionalidade Olá em arquivos menores, como para controladores e rotas separadas. Neste artigo, usaremos Server.js para essa finalidade.

1.  Em um prompt de comando, altere o diretório de saudação muito**azuread**:

    `cd azuread`

2.  Usando um editor de sua escolha, crie um arquivo Server.js. Adicione Olá arquivo toohello de informações a seguir:

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  Salve o arquivo hello. Você retornará tooit em breve.

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a>10: criar um toostore do arquivo de configuração suas configurações do AD do Azure
Arquivo de código passa parâmetros de configuração de saudação de seu tooPassport.js portal do AD do Azure. Você criou esses valores de configuração quando você adicionou o portal de toohello Olá web API no início de saudação do artigo hello. Depois de copiar código Olá, vamos explicar quais tooput em valores hello desses parâmetros.

1.  Em um prompt de comando, altere o diretório de saudação muito**azuread**:

    `cd azuread`

2.  Em um editor, crie um arquivo Config.js. Adicione Olá informações a seguir:

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a>Valores necessários

*   **IdentityMetadata**: isso é onde `passport-azure-ad` procura os dados de configuração para o provedor de identidade (IDP) do hello e Olá chaves toovalidate Olá JSON Web Tokens (JWTs). Se você estiver usando o AD do Azure, não convém toochange isso.

*   **público-alvo**: O URI de redirecionamento do portal de saudação.

> [!NOTE]
> Reverta suas chaves em intervalos frequentes. Certifique-se de que você sempre efetuar pull de URL de "openid_keys" Olá, e que o aplicativo hello possa acessar Olá da Internet.
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a>11: Adicionar Olá configuração tooyour Server.js arquivo
Seu aplicativo precisa tooread valores de saudação do arquivo de configuração de saudação que você acabou de criar. Adicione o arquivo. config de saudação como um recurso necessário em seu aplicativo. Definir Olá toothose de variáveis globais que estão em Config.js.

1.  No prompt de comando hello, altere o diretório de saudação muito**azuread**:

    `cd azuread`

2.  Em um editor, abra o Server.js. Adicione Olá informações a seguir:

    ```Javascript
    var config = require('./config');
    ```

3.  Adicione um novo tooServer.js de seção:

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>12: Adicionar Olá MongoDB modelo e informações de esquema usando Mongoose
Em seguida, conecte esses três arquivos em um serviço de API REST.

Neste artigo, usamos o MongoDB toostore nosso tarefas. Abordaremos isso na *etapa 4*.

No arquivo de Config.js Olá criado na etapa 11, o banco de dados é chamado *tasklist*. Isso é o que é colocado no final da saudação da sua URL de conexão mongoose_auth_local. Você não precisa toocreate banco de dados com antecedência no MongoDB. Olá banco de dados é criado no hello primeiro execução do seu aplicativo de servidor (supondo que o banco de dados de saudação ainda não existir).

Você informou servidor Olá que toouse de banco de dados do MongoDB. Em seguida, você precisa toowrite alguns adicionais toocreate Olá modelo e código de esquema para tarefas do servidor.

### <a name="hello-model"></a>modelo de saudação
modelo de esquema Olá é muito básico. Você pode expandi-lo se necessário. 

modelo de esquema Olá tem estes valores:

*   **NAME**. Olá pessoa toohello atribuído a tarefa. Esse é um valor do tipo **string**.
*   **TASK**. nome de saudação da tarefa de saudação. Esse é um valor do tipo **string**.
*   **DATE**. Data de saudação tarefa hello está vencida. Esse é um valor do tipo **datetime**.
*   **COMPLETED**. Se a tarefa de saudação é concluída. Esse é um valor do tipo **Boolean**.

### <a name="create-hello-schema-in-hello-code"></a>Criar esquema Olá no código de saudação
1.  Em um prompt de comando, altere o diretório de saudação muito**azuread**:

    `cd azuread`

2.  No editor, abra o Server.js. Abaixo da entrada de configuração hello, adicione Olá informações a seguir:

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

Esse código conecta toohello MongoDB server. Ele também retorna um objeto de esquema.

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a>Usando o esquema de hello, criar seu modelo no código de saudação
Abaixo Olá precede o código, adicione Olá código a seguir:

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

Como você pode ver no código hello, primeiro crie o esquema. Em seguida, você cria um objeto do modelo. Usar toostore de objeto de modelo Olá seus dados durante a saudação de código ao definir sua **rotas**.

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a>13: adicionar as rotas ao servidor de API REST da tarefa
Agora que você tem um toowork de modelo de banco de dados com o, adicione rotas Olá que você usará para seu servidor de API REST.

### <a name="about-routes-in-restify"></a>Sobre rotas no Restify
Rotas de restify trabalho exatamente hello mesma forma, quando você usar Olá pilha Express. Definir rotas usando Olá URI que você espera Olá toocall de aplicativos de cliente. Normalmente, você define suas rotas em um arquivo separado. Neste tutorial, colocamos nossa rotas no Server.js. Para uso em produção, recomendamos que você coloque as rotas no próprio arquivo delas.

Eis um padrão típico para uma rota de Restify:

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


Este é o padrão de saudação no nível mais básico de saudação. Restify (e Express) fornecem muito mais funcionalidades, como tipos de aplicativo hello capacidade toodefine e roteamento complexas entre diferentes pontos de extremidade.

#### <a name="add-default-routes-tooyour-server"></a>Adicionar servidor de tooyour rotas padrão
Adicionar rotas CRUD básicas Olá: **criar**, **recuperar**, **atualizar**, e **excluir**.

1.  Em um prompt de comando, altere o diretório de saudação muito**azuread**:

    `cd azuread`

2.  Em um editor, abra o Server.js. Abaixo Olá entradas do banco de dados que você fez anteriormente, adicionar Olá informações a seguir:

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();
    _task.save(function(err) {
    if (err) {
    req.log.warn(err, 'createTask: unable toosave');
    next(err);
    } else {
    res.send(201, _task);
    }
    });
    return next();
    }
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable toodelete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in hello database. Add one!");
    }
    if (!owner) {
    log.warn(err, "You did not pass an owner when listing tasks.");
    } else {
    res.json(data);
    }
    });
    return next();
    }
    ```

### <a name="add-error-handling-for-hello-routes"></a>Adicionar o tratamento de erros para rotas de saudação
Adicione alguns tratamento de erros para que possa se comunicar toohello back cliente sobre o problema de saudação encontrado.

Adicione Olá código abaixo o código de saudação, que você já escreveu a seguir:

```Javascript
///--- Errors for communicating something more information back toohello client.
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="14-create-your-server"></a>14: criar seu servidor
Olá toodo de última coisa é tooadd sua instância de servidor. instância do servidor de saudação gerencia suas chamadas.

O Restify (e Express) têm personalização profunda que pode ser usada com um servidor de API REST. Neste tutorial, usamos a configuração mais básica do hello.

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a>15: adicionar rotas hello (sem autenticação, por enquanto)
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a>16: executar o servidor de saudação
É uma boa ideia tootest seu servidor antes de adicionar a autenticação.

Olá tootest de maneira mais fácil o servidor está usando ondulação no prompt de comando. toodo isso, é necessário um utilitário simples que você pode usar a saída de tooparse como JSON. 

1.  Instale a ferramenta JSON de saudação que usamos em Olá exemplos a seguir:

    `$npm install -g jsontool`

    Isso instala a ferramenta JSON de saudação globalmente.

2.  Verifique se a instância do MongoDB está em execução.

    `$sudo mongod`

3.  Altere o diretório de saudação muito**doWindows Azure**, e, em seguida, execute ondulação:

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  tooadd uma tarefa:

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    Olá resposta deve ser:

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  Listar tarefas para Brandon:

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Se todos esses comandos são executados sem erros, você está pronto tooadd servidor de API REST de toohello de OAuth.

*Agora você tem um servidor de API REST com o MongoDB!*

## <a name="17-add-authentication-tooyour-rest-api-server"></a>17: Adicionar servidor de API REST de tooyour de autenticação
Agora que você tem uma API REST em execução, configurá-lo toouse-lo com o Azure AD.

Em um prompt de comando, altere o diretório de saudação muito**azuread**:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a>Usar oidcbearerstrategy Olá incluído com o ad de azure passport
Até agora, você criou um servidor típico TODO do REST sem nenhum tipo de autorização. Agora, adicione autenticação.

Primeiro, indique que você deseja toouse Passport. Coloque isso logo após a sua configuração anterior do servidor:

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> Quando você escreve APIs, é uma boa ideia tooalways link Olá que dados toosomething exclusivo do token Olá Olá usuário não pode falsificar. Quando esse servidor armazena itens de tarefas, armazena-as com base na ID de assinatura de usuário Olá no token de saudação (chamado por meio de token.sub). Você pode colocar Olá token.sub no campo de "proprietário" hello. Isso garante que somente este usuário pode acessar TODOs do usuário hello. Ninguém pode acessar TODOs Olá que foram inseridos. Não há nenhuma exposição em hello API para "proprietário". Um usuário externo pode solicitar TODOs de outros usuários, mesmo quando eles estão autenticados.
> 
> 

Em seguida, use a estratégia de portador de conectar-se do Open ID Olá que vem com `passport-azure-ad`. Coloque isto depois do que você colou anteriormente:

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

O Passport usa um padrão semelhante para todas as suas estratégias (Twitter, Facebook e assim por diante). Todos os gravadores de estratégia aderem toohello padrão. Passe a estratégia de saudação um `function()` que usa um token e `done` como parâmetros. estratégia de saudação é retornada depois que ele faz seu trabalho. Usuário de saudação do repositório e token de saudação stash para que você não precise tooask para ele novamente.

> [!IMPORTANT]
> Olá código anterior usa qualquer usuário que pode autenticar o servidor de tooyour. Isso é conhecido como registro automático. Em um servidor de produção, você não quer toolet qualquer pessoa sem ter que primeiro eles passam por um processo de registro que você escolher. Normalmente, este é o padrão de saudação que consulte em aplicativos de consumidor. aplicativo Hello pode permitir tooregister com o Facebook, mas, em seguida, ele solicitará que você tooenter obter informações adicionais. Se não houver um programa de linha de comando para este tutorial, é possível extrair o email de saudação do objeto de token de saudação que é retornado. Em seguida, você pode solicitar informações adicionais do hello usuário tooenter. Como esse é um servidor de teste, você adicionar usuário Olá diretamente toohello memória no banco de dados.
> 
> 

### <a name="protect-endpoints"></a>Proteger pontos de extremidade
Proteger os pontos de extremidade, especificando Olá **passport.authenticate()** chamada com protocolo hello que você deseja toouse.

Você pode editar sua rota em seu código de servidor para uma opção mais avançada:

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a>18: executar o aplicativo para servidores novamente
Use curl novamente toosee se você tiver o OAuth 2.0 proteção contra seus pontos de extremidade. Faça isso antes de executar qualquer um dos seus SDKs de cliente para esse ponto de extremidade. cabeçalhos de saudação retornados devem informar se a autenticação está funcionando corretamente.

1.  Verifique se a instância do MongoDB está em execução:

    `$sudo mongod`

2.  Alterar toohello **doWindows Azure** diretório e, em seguida, use ondulação:

    `$ cd azuread`

    `$ node server.js`

3.  Tente uma POSTAGEM básica:

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

Uma resposta 401 indica camada Olá Passport está tentando tooredirect toohello autorizar o ponto de extremidade, que é exatamente o que você deseja.

*Agora você tem um serviço de API REST que usa OAuth 2.0!*

Você já fez tudo o que podia com esse servidor sem usar um cliente compatível com o OAuth 2.0. Para fazer isso, você precisará tooreview um tutorial adicional.

## <a name="next-steps"></a>Próximas etapas
Para referência, o exemplo hello concluída (sem os valores de configuração) é fornecido como [um arquivo. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip). Você também pode cloná-la no GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

Agora, você pode mover toomore tópicos avançados. Talvez você queira tootry [proteger um aplicativo de web Node.js usando o ponto de extremidade do hello v 2.0](active-directory-v2-devquickstarts-node-web.md).

Estes são alguns recursos adicionais:

* [Guia do desenvolvedor do Azure AD v2.0](active-directory-appmodel-v2-overview.md)
* [Marcação “azure-active-directory” do Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Obter atualizações de segurança para nossos produtos
Recomendamos que você toosign backup toobe notificado quando ocorrerem incidentes de segurança. Em Olá [notificações de segurança técnica da Microsoft](https://technet.microsoft.com/security/dd252948) página, assinar tooSecurity comunicados de alertas.

