---
title: "aaaAzure AD Node. js Introdução | Microsoft Docs"
description: "Como toobuild uma API da web REST Node. js que se integra com o Azure AD para autenticação."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a>Introdução às APIs Web para o Node.js
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

*Passport* é middleware de autenticação para o Node.js. Flexível e modular, Passport atualizam pode ser descartado em tooany expressas ou Restify o aplicativo web. Um conjunto abrangente de estratégias dão suporte à autenticação usando um nome de usuário e senha, Facebook, Twitter e mais. Desenvolvemos uma estratégia para o Microsoft Azure Active Directory (Azure AD). Podemos instalar este módulo e adicionar Olá Microsoft Azure Active Directory `passport-azure-ad` plug-in.

toodo isso, você precisa:

1. Registrar um aplicativo com o Azure AD.
2. Configurar seu aplicativo toouse Passport `passport-azure-ad` plug-in.
3. Configure um cliente aplicativo toocall Olá tooDo lista API da web.

código de saudação para este tutorial é mantido [no GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).

> [!NOTE]
> Este artigo não aborda como tooimplement entrar, inscrição, ou criar o perfil de gerenciamento com o Azure AD B2C. Ele se concentra em APIs da web chamado depois que o usuário Olá já está autenticado.  É recomendável que você inicie com [como toointegrate com documentos do Active Directory do Azure](active-directory-how-to-integrate.md) toolearn sobre noções básicas de saudação do Active Directory do Azure.
>
>

Assim, já lançamos o código-fonte para este exemplo em execução no GitHub sob uma licença do MIT, Olá todos os se sentir tooclone livre (ou melhor ainda, bifurcação) e fornecer comentários e efetuar pull das solicitações.

## <a name="about-nodejs-modules"></a>Sobre os módulos do Node.js
Usaremos módulos do Node.js neste passo a passo. Os módulos são pacotes carregáveis do JavaScript que fornecem funcionalidade específica para seu aplicativo. Geralmente instalar módulos, usando a saudação Node. js, uma ferramenta de linha de comando NPM no diretório de instalação de NPM hello. No entanto, alguns módulos, como o módulo HTTP do hello, estão incluídos no pacote de Node. js de núcleo de saudação.

Módulos instalados são salvos em Olá **node_modules** diretório raiz de saudação do seu diretório de instalação do Node. js. Cada módulo no hello **node_modules** directory mantém seu próprio **node_modules** diretório que contém todos os módulos que ele depende. Além disso, cada módulo requerido tem um diretório **node_modules**. Esta estrutura de diretório recursiva representa a cadeia de dependência de saudação.

Essa estrutura de cadeia de dependência resulta em um espaço de aplicativo maior. Mas ela também garante que todas as dependências são atendidas e versão do módulos Olá Olá é usado no desenvolvimento também é usado na produção. Isso torna o comportamento do aplicativo de produção de hello mais previsível e evita os problemas de controle de versão que podem afetar os usuários.

## <a name="step-1-register-an-azure-ad-tenant"></a>Etapa 1: registrar um locatário do Azure AD
toouse exemplo, é necessário um locatário do Active Directory do Azure. Se você não tiver certeza de que um locatário é ou como tooget, consulte [como tooget um AD do Azure locatário](active-directory-howto-tenant.md).

## <a name="step-2-create-an-application"></a>Etapa 2: criar um aplicativo
Em seguida, você cria um aplicativo em seu diretório que dá o AD do Azure informações que precisa toosecurely se comunicar com seu aplicativo.  Aplicativo de cliente hello e a API da web são representados por um único **ID do aplicativo** nesse caso, porque eles compõem um aplicativo lógico.  toocreate um aplicativo, siga [estas instruções](active-directory-how-applications-are-added.md). Se você estiver criando um aplicativo de linha de negócios, [estas instruções adicionais podem ser úteis](../active-directory-applications-guiding-developers-for-lob-applications.md).

toocreate um aplicativo:

1. Entrar toohello [portal do Azure](https://portal.azure.com).

2. No menu superior do hello, selecione sua conta. Em seguida, em Olá **diretório** , escolha o locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.

3. No menu Olá Olá esquerda, selecione **mais serviços**e, em seguida, selecione **Active Directory do Azure**.

4. Selecione **Registros do aplicativo**e, em seguida, selecione **Adicionar**.

5. Siga Olá prompts toocreate um **aplicativo Web e/ou WebAPI**.

      * Olá **nome** da saudação aplicativo descreve os usuários de tooend do aplicativo.

      * Olá **URL de logon** é Olá a URL base do seu aplicativo.  Olá URL do código de exemplo hello padrão é `https://localhost:8080`.

6. Depois de se registrar, o Azure AD atribui uma ID de aplicativo única ao seu aplicativo. Você precisa desse valor nas seções de Avançar Olá, portanto copie-o da página de aplicativo hello.

7. De saudação **configurações** -> **propriedades** página para seu aplicativo, Olá URI da ID do aplicativo de atualização. Olá **URI da ID do aplicativo** é um identificador exclusivo para seu aplicativo. convenção de saudação é toouse `https://<tenant-domain>/<app-name>`, por exemplo: `https://contoso.onmicrosoft.com/my-first-aad-app`.

8. Criar um **chave** para seu aplicativo de saudação **configurações** página e, em seguida, copie-o em algum lugar. Você precisará dela em breve.

## <a name="step-3-download-nodejs-for-your-platform"></a>Etapa 3: baixar o Node.js para a sua plataforma
toosuccessfully usar este exemplo, você deve ter uma instalação em funcionamento do Node. js.

Instale o Node.js a partir de [http://nodejs.org](http://nodejs.org).

## <a name="step-4-install-mongodb-on-your-platform"></a>Etapa 4: instalar o MongoDB na sua plataforma
toosuccessfully usar este exemplo, você deve ter uma instalação em funcionamento do MongoDB. Use o MongoDB toomake Olá REST API persistente em instâncias de servidor.

Instalar o MongoDB a partir de [http://mongodb.org](http://www.mongodb.org).

> [!NOTE]
> Este passo a passo pressupõe que você use Olá instalação e o servidor de pontos de extremidade padrão para o MongoDB, que em tempo de saudação da redação deste artigo é mongodb://localhost.
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a>Etapa 5: Instalar os módulos de Restify de saudação em sua API da web
Estamos usando Restify toobuild nossa API REST. O Restify é uma estrutura de aplicativo do Node.js mínima e flexível, derivada do Express. Tem um conjunto robusto de recursos para a criação de APIs REST sobre o Connect.

### <a name="install-restify"></a>Instalar Restify
1. Olá linha de comando, altere diretórios toohello **doWindows Azure** directory. Se hello **doWindows Azure** diretório não existe, criá-lo.

        `cd azuread - or- mkdir azuread; cd azuread`

2. Digite hello comando a seguir:

    `npm install restify`

    Este comando instala o Restify.

#### <a name="did-you-get-an-error"></a>Você obteve um erro?
Ao usar o NPM em alguns sistemas operacionais, você poderá receber uma mensagem de erro que diz: **Erro: EPERM, chmod '/usr/local/bin/..'** e uma sugestão que você tente conta de saudação em execução como administrador. Se isso ocorrer, use Olá sudo comando toorun NPM em um nível de privilégio mais alto.

#### <a name="did-you-get-an-error-regarding-dtrace"></a>Ocorreu um erro com relação ao DTRACE?
Você poderá ver um erro assim ao instalar o Restify:

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
O Restify fornece um mecanismo poderoso para rastreamento de chamadas REST usando o DTrace. No entanto, muitos sistemas operacionais não possuem o DTrace. Você pode ignorar com segurança esses erros.

saída de Hello desse comando deve ser semelhante toohello saída a seguir:

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


## <a name="step-6-install-passportjs-in-your-web-api"></a>Etapa 6: instalar o Passport.js na sua API da Web
[Passport](http://passportjs.org/) é middleware de autenticação para o Node.js. Flexível e modular, Passport atualizam pode ser descartado em tooany expressas ou Restify o aplicativo web. Um conjunto abrangente de estratégias dão suporte à autenticação usando um nome de usuário e senha, Facebook, Twitter e mais.

Desenvolvemos uma estratégia para o Active Directory do Azure. Podemos instalar este módulo e adicionar plug-in da estratégia de Active Directory do Azure de saudação.

1. Olá linha de comando, altere diretórios toohello **doWindows Azure** directory.

2. tooinstall passport.js, digite Olá comando a seguir:

    `npm install passport`

    saída de saudação do comando Olá deve ser a seguir toohello semelhante:

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a>Etapa 7: Adicionar API da web do AD de Azure Passport tooyour
Em seguida, adicionamos estratégia de OAuth hello usando `passport-azure-ad`, um conjunto de estratégias que se conectam tooPassport do Active Directory do Azure. Usaremos essa estratégia para tokens de portador neste exemplo de API Rest.

> [!NOTE]
> Embora o OAuth2 forneça uma estrutura na qual qualquer tipo de token conhecido possa ser emitido, somente determinados tipos de token são comumente usados. Tokens de portador são tokens de hello mais comumente usada para proteger os pontos de extremidade. Eles são o tipo de hello mais amplamente emitido de token em OAuth2. Muitas implementações supõem que os tokens de portador são Olá únicos tipos de tokens emitidos.
>
>

Olá linha de comando, altere diretórios toohello **doWindows Azure** directory.

Digite o seguinte Olá comando Olá tooinstall Passport.js `passport-azure-ad module`:

`npm install passport-azure-ad`

saída de saudação do comando Olá deve ser semelhante toohello saída a seguir:


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a>Etapa 8: Adicionar MongoDB módulos tooyour web API
Usamos o MongoDB como nosso repositório de dados. Por esse motivo, é preciso tooinstall Olá amplamente usada plug-in Modelos de toomanage Mongoose chamados e esquemas. Também precisamos de driver de banco de dados tooinstall Olá para o MongoDB (que também é chamado MongoDB).

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a>Etapa 9: instalar módulos adicionais
Em seguida, podemos instalar Olá restantes módulos necessários.

1. Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá.

    `cd azuread`

2. Digite hello tooinstall comandos a seguir esses módulos em seu **node_modules** diretório:

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a>Etapa 10: criar um server.js com as suas dependências
arquivo de server.js de saudação fornece a maioria da funcionalidade de saudação para nosso servidor de API da web. Vamos adicionar mais nosso toothis do arquivo de código. Para fins de produção, recomendamos que você refatorar funcionalidade Olá em arquivos menores, como controladores e rotas separadas. Nesta demonstração, usaremos o server.js para essa funcionalidade.

1. Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá.

    `cd azuread`

2. Criar um `server.js` de arquivo em seu editor favorito e adicione Olá informações a seguir:

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. Salve o arquivo hello. Retornaremos tooit em breve.

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a>Etapa 11: Criar um toostore do arquivo de configuração de suas configurações do AD do Azure
Arquivo de código passa parâmetros de configuração de saudação de seu tooPassport.js portal do Active Directory do Azure. Quando você adicionou o portal de toohello Olá web API na primeira parte Olá Olá passo a passo, você criou esses valores de configuração. Explicamos que tooput em valores desses parâmetros Olá depois de copiar o código de saudação.

1. Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá.

    `cd azuread`

2. Criar um `config.js` de arquivo em seu editor favorito e adicione Olá informações a seguir:

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. Salve o arquivo hello.

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a>Etapa 12: Adicionar o arquivo de configuração de valores tooyour Server. js
É preciso tooread esses valores no arquivo. config Olá que você criou em nosso aplicativo. toodo isso, adicionamos arquivo. config de saudação como um recurso necessário em nosso aplicativo. Em seguida, vamos definir variáveis de Olá Olá variáveis globais toomatch no documento de config.js hello.

1. Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá.

    `cd azuread`

2. Abra o `server.js` do arquivo em seu editor favorito e adicione Olá informações a seguir:

    ```Javascript
    var config = require('./config');
    ```
3. Em seguida, adicione uma nova seção muito`server.js` com hello código a seguir:

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. Salve o arquivo hello.

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Etapa 13: Adicionar Olá MongoDB modelo e informações de esquema usando Mongoose
Agora todos os essa preparação vai toostart pagar como podemos combinar esses três arquivos em um serviço de API REST.

Para este passo a passo, usamos MongoDB toostore nosso tarefas, conforme descrito na etapa 4.

Em Olá `config.js` que criamos na etapa 11, chamamos nosso banco de dados de arquivo `tasklist`, pois esse era o que colocar no final de saudação do nosso **mogoose_auth_local** URL de conexão. Você não precisa toocreate banco de dados com antecedência no MongoDB. Em vez disso, MongoDB cria isso para que possamos em Olá primeiro execução de nosso aplicativo de servidor (supondo que o banco de dados Olá ainda não existe).

Agora que dissemos servidor Olá qual banco de dados do MongoDB gostaríamos toouse, precisamos toowrite alguns adicionais toocreate Olá modelo e código de esquema para tarefas do servidor.

### <a name="discussion-of-hello-model"></a>Descrição do modelo de saudação
Nosso modelo de esquema é simples. Você pode expandi-lo conforme necessário.

NOME: o nome de saudação da saudação pessoa designada toohello tarefa. Uma **cadeia de caracteres**.

TAREFA: Olá própria tarefa. Uma **cadeia de caracteres**.

Data de saudação de data: tarefa Olá é devida. UM VALOR **DATETIME**.

CONCLUÍDA: Se Olá tarefa tiver sido concluída ou não. UM VALOR **BOOLEANO**.

### <a name="creating-hello-schema-in-hello-code"></a>Criando esquema Olá em código de saudação
1. Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá.

    `cd azuread`

2. Abra seu `server.js` arquivo em seu editor favorito e adicione Olá informações abaixo da entrada de configuração de saudação a seguir:

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
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
Como você pode ver no código hello, criamos nossa esquema primeiro. Em seguida, podemos criar um objeto de modelo que usamos toostore nossos dados durante a saudação código quando definimos nosso **rotas**.

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a>Etapa 14: adicionar nossas rotas a nosso servidor de API REST da tarefa
Agora que temos uma toowork de modelo de banco de dados com, vamos adicionar rotas Olá estamos use contínuo para nosso servidor de API REST.

### <a name="about-routes-in-restify"></a>Sobre rotas no Restify
Rotas funcionam em Restify Olá mesma maneira como eles em Olá Express de pilha. Definir rotas usando Olá URI que você espera Olá toocall de aplicativos de cliente. Normalmente, você define suas rotas em um arquivo separado. Para nossos objetivos, colocamos nossas rotas no arquivo de server.js hello. Recomendamos que você as coloque no seu próprio arquivo para uso em produção.

Um padrão típico para uma rota do Restify é:

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


Este é o padrão de saudação em seu nível mais básico. O Restify (e o Express) fornece uma funcionalidade muito mais aprofundada, como a definição de tipos de aplicativos e o roteamento complexo entre diferentes pontos de extremidade. Para nossos propósitos, estamos mantendo essas rotas simples.

### <a name="add-default-routes-tooour-server"></a>Adicionar servidor de tooour rotas padrão
Agora adicionar Olá básica CRUD rotas de criar, recuperar, atualizar e excluir.

1. Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá:

    `cd azuread`

2. Olá abrir `server.js` arquivo em seu editor favorito e adicione Olá informações abaixo Olá banco de dados as entradas anteriores feitas a seguir:

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a>Adicionar tratamento de erros em nossas APIs
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a>Etapa 15: criar seu servidor
Definimos nosso banco de dados e nossas rotas estão em vigor. Olá última coisa toodo é adicionar a instância do servidor de saudação que gerencia nossas chamadas.

Restify (e Express), você pode fazer muita de personalização para um servidor de API REST, mas, novamente, vamos configuração mais básica do toouse Olá para nossas finalidades.

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a>Etapa 16: Adicionar o servidor de toohello de rotas de saudação (sem autenticação agora)
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a>Etapa 17: Executar o servidor de saudação (antes de adicionar suporte OAuth)
Teste o seu servidor antes de adicionarmos a autenticação.

Olá tootest de maneira mais fácil o servidor está usando ondulação em uma linha de comando. Antes de fazermos isso, precisamos de um utilitário que nos permite saída tooparse como JSON.

1. Instale Olá, ferramenta JSON (Olá todos os exemplos a seguir usam esta ferramenta) a seguir:

    `$npm install -g jsontool`

    Isso instala a ferramenta JSON de saudação globalmente. Agora que nós já realizado que, vamos executar com o servidor de saudação:

2. Primeiro, verifique se a instância do MongoDB está em execução:

    `$sudo mongod`

3. Em seguida, altere o diretório toohello e iniciar curling:

    `$ cd azuread` `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. Então, podemos adicionar uma tarefa deste modo:

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

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
    E podemos pode listar tarefas para Brandon deste modo:

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Se tudo isso funciona, estamos servidor de API REST de toohello tooadd pronto OAuth.

Você tem um servidor de API REST com o MongoDB!

## <a name="step-18-add-authentication-tooour-rest-api-server"></a>Etapa 18: Adicionar o servidor de API REST de tooour de autenticação
Agora que temos uma API REST em execução, vamos começar ativando-a com o Azure AD.

Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá.

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Use Olá OIDCBearerStrategy que está incluído no ad de azure passport
Até agora, criamos um servidor típico TODO do REST sem nenhum tipo de autorização. Aqui é onde começamos a juntar as peças.

1. Primeiro, precisamos tooindicate que desejamos toouse Passport. Coloque isso logo após a configuração do servidor:

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > Quando você escreve APIs, recomendamos que você sempre vincular Olá dados toosomething exclusivo do token Olá Olá usuário não pode falsificar. Quando esse servidor armazena itens de tarefas, armazena-as com base na ID de objeto de saudação do usuário Olá no token de saudação (chamado por meio de token.oid), que são colocados no campo de "proprietário" hello. Isso garante que somente o usuário possa acessar seus TODOs. Não há nenhuma exposição no Olá API de "proprietário", para que um usuário externo pode solicitar Olá TODOs outros mesmo quando eles são autenticados.                    

2. Avançar vamos usar a estratégia de portador de saudação que vem com `passport-azure-ad`. Examine o código de saudação por enquanto e explicaremos rest Olá em breve. Coloque isto depois do que você colou acima:

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

O Passport usa um padrão semelhante para todas as estratégias (Twitter, Facebook e assim por diante) que todos os gravadores de estratégia seguem. Passamos a ele uma função que tem um token e uma pronto como parâmetros de saudação observando estratégia hello, consulte. estratégia de saudação vem toous novamente depois que ele faz seu trabalho. Depois que ele faz, armazenamos Olá usuário e token de saudação stash para que não seja necessário tooask para ele novamente.

> [!IMPORTANT]
> código anterior Olá usa qualquer usuário que ocorre em tooauthenticate tooour server. Isso é conhecido como registro automático. Em servidores de produção, não convém permitir que qualquer pessoa entre sem primeiro passar por um processo de registro em que você decida. Normalmente, este é o padrão de saudação que consulte em aplicativos de consumidor, que permitem que você tooregister com o Facebook, mas, em seguida, solicitar que você toofill informações adicionais. Se isso não era um programa de linha de comando, podemos foi ter extrair email saudação do objeto de token de saudação que é retornado e, em seguida, terá Olá usuário toofill informações adicionais. Como esse é um servidor de teste, basta adicioná-los banco de dados do toohello na memória.
>
>

### <a name="protect-some-endpoints"></a>Proteger alguns pontos de extremidade
Proteger os pontos de extremidade, especificando Olá `passport.authenticate()` chamada com protocolo hello que você deseja toouse.

toomake nosso código do servidor fazer algo mais interessante, vamos Editar rota de saudação.

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a>Etapa 19: executar o aplicativo de servidor novamente e certificar-se de que rejeitará você
Vamos usar `curl` novamente toosee se agora temos OAuth2 proteção contra os pontos de extremidade. Fazemos isso antes de executar qualquer um dos nossos SDKs de cliente para esse ponto de extremidade. Hello cabeçalhos que são retornados devem ser suficientes tootell conosco se vamos caminho certo hello.

1. Primeiro, verifique se a instância do MongoDB está em execução:

    `$sudo mongod`

2. Em seguida, altere o diretório toohello e iniciar curling.

      `$ cd azuread` `$ node server.js`

3. Tente uma POSTAGEM básica.

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

Um 401 é resposta Olá que você está procurando aqui. Essa resposta indica que camada Olá Passport está tentando tooredirect toohello autorizado ponto de extremidade que é exatamente o que você deseja.

## <a name="next-steps"></a>Próximas etapas
Você já fez tudo o que podia com esse servidor sem usar um cliente compatível com o OAuth2. Você precisará toogo por meio de uma passo a passo adicional.

Você aprendeu como tooimplement uma API REST usando Restify e OAuth2. Você também tem mais do que suficiente tookeep código desenvolver seu serviço e aprender como toobuild neste exemplo.

Se você estiver interessado em próximas etapas de saudação em sua jornada ADAL, aqui estão alguns clientes ADAL com suporte, é recomendável que você continuar trabalhando com.

Clonar a máquina do desenvolvedor tooyour e configure conforme descrito no passo a passo de saudação.

[ADAL para iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[ADAL para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
