---
title: 'Azure AD B2C: proteger uma API Web usando o Node.js | Microsoft Docs'
description: "Como a API da web do toobuild um Node. js que aceita tokens de um locatário B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a>Azure AD B2C: proteger uma API Web usando o Node .js
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

Com o Active Directory B2C do Azure (AD do Azure), você pode proteger uma API Web usando tokens de acesso do OAuth 2.0. Esses tokens permitem que seus aplicativos cliente que usam a API do Azure AD B2C tooauthenticate toohello. Este artigo mostra como toocreate uma "lista de tarefas" API que permite aos usuários tooadd e lista de tarefas. Olá web API é protegida usando o Azure AD B2C e só permite que os usuários autenticados toomanage sua lista de tarefas pendentes.

> [!NOTE]
> Este exemplo foi escrito toobe conectado tooby usando nosso [aplicativo de exemplo do iOS B2C](active-directory-b2c-devquickstarts-ios.md). Olá passo a passo atual primeiro e depois junto com o exemplo.
>
>

**Passport** é middleware de autenticação para o Node.js. Flexível e modular, o Passport pode ser instalado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify. Um conjunto abrangente de estratégias que dão suporte à autenticação usando um nome de usuário e uma senha, o Facebook, o Twitter e muito mais. Desenvolvemos uma estratégia para o Azure AD (Active Directory do Azure). Instalar este módulo e, em seguida, adicionar Olá AD do Azure `passport-azure-ad` plug-in.

toodo neste exemplo, você precisa:

1. Registrar um aplicativo com o Azure AD.
2. Configurar seu aplicativo toouse Passport `azure-ad-passport` plug-in.
3. Configure um cliente aplicativo toocall hello "lista de tarefas" API da web.

## <a name="get-an-azure-ad-b2c-directory"></a>Obter um diretório AD B2C do Azure
Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.  Um diretório é um contêiner para todos os usuários, aplicativos, grupos e muito mais.  Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir.

## <a name="create-an-application"></a>Criar um aplicativo
Em seguida, você precisa toocreate um aplicativo em seu diretório do B2C que fornece algumas informações que precisa toosecurely de AD do Azure se comunicar com seu aplicativo. Nesse caso, a saudação aplicativo de cliente e a API da web são representados por um único **ID do aplicativo**, pois elas formam um aplicativo lógico. toocreate um aplicativo, siga [estas instruções](active-directory-b2c-app-registration.md). É necessário que você:

* Incluir um **web do aplicativo de web api** no aplicativo hello
* Digite `http://localhost/TodoListService` como uma **URL de Resposta**. É saudação padrão URL para este exemplo de código.
* Crie um **Segredo de aplicativo** para seu aplicativo e copie-o. Você precisa destes dados mais tarde. Observe que esse valor precisa toobe [XML escapado](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de você usá-lo.
* Saudação de cópia **ID do aplicativo** que é atribuído tooyour aplicativo. Você precisa destes dados mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Criar suas políticas
No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md). O aplicativo contém duas experiências de identidade: inscrever-se e entrar. Você precisa de uma política de toocreate de cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).  Ao criar as três políticas, não deixe de:

* Escolha Olá **nome de exibição** e outros atributos de inscrição em sua política de inscrição.
* Escolha Olá **nome de exibição** e **ID de objeto** declarações de aplicativo em cada política.  Você pode escolher outras declarações também.
* Cópia para baixo Olá **nome** de cada política depois de criá-lo. Ele deve ter o prefixo Olá `b2c_1_`.  Mais tarde, você precisará desses nomes de política.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Depois de ter criado as três políticas, você está pronto toobuild seu aplicativo.

toolearn sobre como as diretivas funcionam no Azure AD B2C, começam com hello [.NET web aplicativo tutorial de Introdução](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="download-hello-code"></a>Baixar o código de saudação
Olá código para este tutorial [é mantida no GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS). exemplo de hello toobuild que você vá, você pode [baixar um projeto de esqueleto como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip). Também é possível clonar o esqueleto do hello:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

aplicativo Hello concluída também é [disponível como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) ou em Olá `complete` ramificação da saudação mesmo repositório.

## <a name="download-nodejs-for-your-platform"></a>Baixar o Node.js para sua plataforma
toosuccessfully usar este exemplo, você precisa de uma instalação de trabalho do Node. js.

Instale o Node.js de [nodejs.org](http://nodejs.org).

## <a name="install-mongodb-for-your-platform"></a>Instalar o MongoDB para sua plataforma
toosuccessfully usar este exemplo, você precisa de uma instalação de trabalho do MongoDB. Podemos usar o MongoDB toomake API REST persistente em instâncias de servidor.

Instale o MongoDB de [mongodb.org](http://www.mongodb.org).

> [!NOTE]
> Este passo a passo pressupõe que você use Olá instalação e o servidor de pontos de extremidade padrão para o MongoDB, que em tempo de saudação da redação deste artigo é `mongodb://localhost`.
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a>Instalar módulos de Restify Olá em sua API da web
Usamos Restify toobuild a API REST. O Restify é uma estrutura de aplicativo do Node.js mínima e flexível, derivada do Express. Tem um conjunto robusto de recursos para a criação de APIs REST sobre o Connect.

### <a name="install-restify"></a>Instalar Restify
Olá linha de comando, altere seu diretório muito`azuread`. Se hello `azuread` diretório não existe, criá-lo.

`cd azuread` ou `mkdir azuread;`

Digite hello comando a seguir:

`npm install restify`

Este comando instala o Restify.

#### <a name="did-you-get-an-error"></a>Você obteve um erro?
Em alguns sistemas operacionais, quando você usa `npm`, você pode receber o erro Olá `Error: EPERM, chmod '/usr/local/bin/..'` e uma solicitação que você execute conta hello como um administrador. Se ocorrer esse problema, use Olá `sudo` toorun comando `npm` em um nível de privilégio mais alto.

#### <a name="did-you-get-a-dtrace-error"></a>Você recebeu um erro DTrace?
Você pode ver algo como este texto ao instalar o Restify:

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
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

O Restify fornece um mecanismo poderoso para rastreamento de chamadas REST usando o DTrace. No entanto, muitos sistemas operacionais não têm o DTrace disponível. Você pode ignorar com segurança esses erros.

saída de saudação do comando de saudação deve aparecer texto toothis semelhante:

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
    └── bunyan@0.22.0 (mv@0.0.5)

## <a name="install-passport-in-your-web-api"></a>Instalar o Passport.js na API Web
Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá.

Instale o Passport usando Olá comando a seguir:

`npm install passport`

saída de saudação do comando Olá deve ser texto toothis semelhante:

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a>Adicionar passport azuread tooyour web API
Em seguida, adicione a estratégia de OAuth hello usando `passport-azuread`, um conjunto de estratégias que se conectam do AD do Azure com o Passport. Use essa estratégia para tokens de portador no exemplo de API REST hello.

> [!NOTE]
> Embora o OAuth2 forneça uma estrutura na qual qualquer tipo de token conhecido pode ser emitido, somente determinados tipos de token passaram a ser amplamente usados. tokens de saudação para proteger pontos de extremidade são tokens de portador. Esses tipos de tokens são hello mais amplamente emitido em OAuth2. Muitas implementações supõem que os tokens de portador são Olá único tipo de token emitido.
>
>

Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá.

Instalar Olá Passport `passport-azure-ad` módulo usando Olá comando a seguir:

`npm install passport-azure-ad`

saída de saudação do comando Olá deve ser texto toothis semelhante:

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a>Adicionar de API da web do MongoDB módulos tooyour
Este exemplo usa o MongoDB como repositório de dados. Para isso, instale o Mongoose, um plug-in amplamente utilizado para gerenciar modelos e esquemas.

* `npm install mongoose`

## <a name="install-additional-modules"></a>Instalar módulos adicionais
Em seguida, instale Olá restantes módulos necessários.

Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:

`cd azuread`

Instalar módulos Olá no seu `node_modules` diretório:

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a>Criar um arquivo server.js com suas dependências
Olá `server.js` arquivo fornece a maioria de saudação da funcionalidade de saudação para seu servidor de API da Web.

Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:

`cd azuread`

Crie um arquivo `server.js` em um editor. Adicione Olá informações a seguir:

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

Salve o arquivo hello. Você pode retornar tooit mais tarde.

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a>Criar um toostore de arquivo config.js suas configurações do AD do Azure
Esse arquivo de código passa parâmetros de configuração de saudação do seu Portal do AD do Azure toohello `Passport.js` arquivo. Você criou esses valores de configuração quando você adicionou o portal de toohello Olá web API a primeira parte Olá passo a passo hello. Explicamos que tooput em valores desses parâmetros Olá depois de copiar o código de saudação.

Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:

`cd azuread`

Crie um arquivo `config.js` em um editor. Adicione Olá informações a seguir:

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a>Valores necessários
`clientID`: Olá ID do cliente do seu aplicativo de API da Web.

`IdentityMetadata`: Esse é o local onde `passport-azure-ad` procura os dados de configuração para o provedor de identidade hello. Ele também procura tokens da web JSON de saudação do hello chaves toovalidate.

`audience`: Olá identificador de recurso uniforme (URI) do portal de saudação que identifica seu aplicativo de chamada.

`tenantName`: o nome do locatário (por exemplo, **contoso.onmicrosoft.com**).

`policyName`: Olá política que deseja que os tokens de saudação toovalidate as novidades no servidor tooyour. Esta política deve ser Olá política mesmo que você usa no aplicativo de cliente hello para entrar.

> [!NOTE]
> Por enquanto, use Olá mesmo políticas pela instalação de cliente e servidor. Se você já tiver concluído uma apresentação e criar essas políticas, você não precisa toodo novamente. Como concluir o passo a passo Olá, você não deve necessário tooset novas políticas para orientações de cliente no site de saudação.
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a>Adicionar o arquivo de configuração de server.js tooyour
tooread valores Olá Olá `config.js` arquivo criado, adicione Olá `.config` arquivo como um recurso necessário em seu aplicativo e depois defina Olá variáveis globais toothose no hello `config.js` documento.

Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:

`cd azuread`

Olá abrir `server.js` arquivo em um editor. Adicione Olá informações a seguir:

```Javascript
var config = require('./config');
```
Adicionar uma nova seção muito`server.js` que inclui a saudação de código a seguir:

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

Em seguida, vamos adicionar alguns espaços reservados para os usuários de saudação que recebemos de nossos aplicativos de chamada.

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

Vamos prosseguir e criar nosso logger também.

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Adicionar informações de modelo e o esquema do MongoDB hello usando Mongoose
Olá preparação anterior paga como trazer esses três arquivos juntos em um serviço de API REST.

Para este passo a passo, use MongoDB toostore suas tarefas, conforme discutido anteriormente.

Em Olá `config.js` arquivo, você chamou o seu banco de dados **tasklist**. Esse nome também é o que é colocado no final de saudação do hello `mongoose_auth_local` URL de conexão. Você não precisa toocreate banco de dados com antecedência no MongoDB. Ele cria o banco de dados de saudação para você na primeira execução de saudação do seu aplicativo de servidor.

Depois que você informa o servidor de saudação que toouse de banco de dados do MongoDB, você precisa toowrite alguns adicionais toocreate Olá modelo e código de esquema para suas tarefas de servidor.

### <a name="expand-hello-model"></a>Expanda o modelo de saudação
Esse modelo de esquema é simples. Você pode expandi-lo conforme necessário.

`owner`: Que é atribuído a tarefa toohello. Este objeto é uma **cadeia de caracteres**.  

`Text`: tarefa Olá em si. Este objeto é uma **cadeia de caracteres**.

`date`: date de hello tarefa hello está vencida. Este objeto é um **datetime**.

`completed`: Se Olá tarefa foi concluída. Este objeto é um **Booliano**.

### <a name="create-hello-schema-in-hello-code"></a>Criar esquema Olá no código de saudação
Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:

`cd azuread`

Olá abrir `server.js` arquivo em um editor. Adicione Olá informações abaixo da entrada de configuração de saudação a seguir:

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
Criar esquema Olá primeiro e, em seguida, você cria um objeto de modelo que você usar toostore seus dados durante a saudação de código ao definir sua **rotas**.

## <a name="add-routes-for-your-rest-api-task-server"></a>Adicionar rotas para o servidor de tarefa da API REST
Agora que você tem um toowork de modelo de banco de dados com, adicione rotas Olá usado para o seu servidor de API REST.

### <a name="about-routes-in-restify"></a>Sobre rotas no Restify
Rotas funcionam em Restify em Olá mesma forma como funcionam quando eles usam a pilha do hello Express. Definir rotas usando Olá URI que você espera Olá toocall de aplicativos de cliente.

Um padrão típico para uma rota do Restify é:

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

O Restify e o Express fornecem funcionalidade muito mais aprofundada, como a definição de tipos de aplicativos e o roteamento complexo entre diferentes pontos de extremidade. Para fins de saudação deste tutorial, podemos manter essas rotas simples.

#### <a name="add-default-routes-tooyour-server"></a>Adicionar servidor de tooyour rotas padrão
Agora que você adicionar Olá básica CRUD rotas **criar** e **lista** para nossa API REST. Outras rotas podem ser encontradas no hello `complete` ramificação do exemplo hello.

Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:

`cd azuread`

Olá abrir `server.js` arquivo em um editor. Abaixo de entradas de banco de dados de saudação feitas acima adicionar Olá informações a seguir:

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a>Adicionar o tratamento de erros para rotas de saudação
Adicione alguns tratamentos de erro para que você possa comunicar os problemas encontrados back toohello cliente de forma que ele possa entender.

Adicione Olá código a seguir:

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a>Criar seu servidor
Agora você definiu o banco de dados e incluiu as rotas. Olá última coisa para você toodo é instância de servidor de saudação tooadd que gerencia suas chamadas.

Restify e Express fornecem personalização profunda para um servidor de API REST, mas podemos usar a configuração mais básica do hello aqui.

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a>Adicionar servidor de toohello rotas hello (sem autenticação)
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a>Adicionar servidor de API REST de tooyour de autenticação
Agora que tem um servidor de API REST em execução, você pode torná-lo útil no Azure AD.

Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Use Olá OIDCBearerStrategy que está incluído no ad de azure passport
> [!TIP]
> Quando você escreve APIs, você deve sempre vincular Olá dados toosomething exclusivo do token Olá Olá usuário não pode falsificar. Quando o servidor de saudação armazena itens de tarefas, ele faz então com base em Olá **oid** do usuário Olá no token de saudação (chamado por meio de token.oid), que vai no campo proprietário"Olá". Esse valor garante que somente o usuário possa acessar seus próprios itens de Tarefas Pendentes. Não há nenhuma exposição no Olá API de "proprietário", para que um usuário externo pode solicitar outros itens de tarefas, mesmo quando eles são autenticados.
>
>

Em seguida, usar a estratégia de portador de saudação que vem com `passport-azure-ad`.

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

Passport usa Olá mesmo padrão para todas as suas estratégias. Você o passa como um `function()` que tem `token` e `done` como parâmetros. estratégia de saudação volta tooyou depois que ela fez todo seu trabalho. Você deve armazenar usuário hello e salvar o token Olá para que você não precisa tooask para ele novamente.

> [!IMPORTANT]
> código de saudação acima usa qualquer usuário que acontece tooauthenticate tooyour server. Este processo é conhecido como registro automático. Em servidores de produção, não deixe em qualquer API de saudação de acesso de usuários, sem ter que primeiro-los passar por um processo de registro. Esse processo é geralmente padrão Olá que consulte em aplicativos cliente que permitem que você tooregister usando o Facebook, mas, em seguida, solicitar que você toofill informações adicionais. Se este programa não um programa de linha de comando, podemos foi ter extrair email saudação do objeto de token de saudação que é retornado e, em seguida, terá os usuários toofill informações adicionais. Como esse é um exemplo, adicioná-los banco de dados do tooan na memória.
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a>Execute o tooverify do aplicativo de servidor que ele rejeita você
Você pode usar `curl` toosee se você já OAuth2 proteção contra seus pontos de extremidade. Olá cabeçalhos retornados devem ser suficientes tootell que estão no caminho de saudação à direita.

Verifique se a instância do MongoDB está em execução.

    $sudo mongodb

Alterar diretório toohello e servidor de saudação de execução:

    $ cd azuread
    $ node server.js

Em uma nova janela de terminal, execute `curl`

Tente uma POSTAGEM básica:

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

Um erro 401 é resposta Olá desejado. Ele indica a camada Olá Passport está tentando tooredirect toohello autorizar o ponto de extremidade.

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a>Agora você tem um serviço de API REST que usa OAuth2
Você implementou uma API REST usando Restify e OAuth! Agora você tem código suficiente para que você possa continuar toodevelop seu serviço e compilar este exemplo. Você  fez tudo o que podia com esse servidor sem usar um cliente compatível com OAuth2. Para a próxima etapa, use uma passo a passo adicional como nosso [conectar-se a API da web do tooa usando iOS com B2C](active-directory-b2c-devquickstarts-ios.md) passo a passo.

## <a name="next-steps"></a>Próximas etapas
Agora você pode mover tópicos toomore avançada, como:

[Conecte-se a API da web do tooa usando iOS com B2C](active-directory-b2c-devquickstarts-ios.md)
