---
title: "aaaDeploy um tooAzure de aplicativo de web do serviço de aplicativo Sails.js | Microsoft Docs"
description: "Saiba como toodeploy um aplicativo do serviço de aplicativo do Azure do Node. js. Este tutorial mostra como aplicativo da web de toodeploy um Sails.js."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a>Implantar um tooAzure de aplicativo web do Sails.js do serviço de aplicativo
Este tutorial mostra como toodeploy um aplicativo de Sails.js tooAzure do serviço de aplicativo. No processo de saudação, você pode obter conhecimentos gerais sobre como tooconfigure seu toorun de aplicativo Node. js no serviço de aplicativo.

Aqui você aprenderá habilidades úteis, por exemplo:

* Configure um aplicativo Sails.js executado no Serviço de Aplicativo.
* Implante um tooApp aplicativo serviço Olá linha de comando.
* STDOUT e stderr leitura registra tootroubleshoot quaisquer problemas de implantação.
* Armazenar variáveis de ambiente fora do controle do código-fonte.
* Acessar as variáveis de ambiente do Azure do seu aplicativo.
* Conecte-se o banco de dados tooa (MongoDB).

Você deve ter conhecimento prático de Sails.js. Este tutorial não é pretendido toohelp com problemas relacionados a toorunning Sail.js em geral.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete

Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](app-service-web-nodejs-sails-cli-nodejs.md) – nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de Olá
- [2.0 do CLI do Azure](app-service-web-nodejs-sails.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação

## <a name="prerequisites"></a>Pré-requisitos
* [Node.js](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git](http://www.git-scm.com/downloads)
* [CLI 2.0 do Azure](/cli/azure/install-az-cli2)
* Uma conta do Microsoft Azure. Se não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> Você pode [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) sem uma conta do Azure. Criar um aplicativo de início e explorá-la para a hora de tooan – nenhum cartão de crédito necessários, nenhum investimento.
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>Etapa 1: criar e configurar um aplicativo do Sails.js localmente
Primeiro, crie rapidamente um aplicativo do Sails.js padrão em seu ambiente de desenvolvimento seguindo estas etapas:

1. Terminal de linha de comando Olá aberto de sua escolha e `CD` tooa diretório de trabalho.
2. Crie um novo aplicativo Sails.js e execute-o:

        sails new <app_name>
        cd <app_name>
        sails lift

    Verifique se que você pode navegar toohello padrão home page em http://localhost:1377.

1. Em seguida, habilitar registro em log para o Azure. No diretório raiz, crie um arquivo chamado `iisnode.yml` e adicione Olá duas linhas a seguir:

        loggingEnabled: true
        logDirectory: iisnode

    Registro em log está ativado para Olá [iisnode](https://github.com/tjanczuk/iisnode) do serviço de aplicativo do Azure usa toorun Node. js aplicativos de servidor. 
    Para obter mais informações sobre como isso funciona, consulte [como toodebug um Node. js web app no serviço de aplicativo do Azure](web-sites-nodejs-debug.md).

2. Em seguida, configure as variáveis de ambiente do Azure Olá Sails.js aplicativo toouse. Abra config/env/production.js tooconfigure seu ambiente de produção e defina `port` e `hookTimeout`:

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    Você pode encontrar a documentação para essas configurações na [Documentação do Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).

4. Em seguida, codifique Olá Node. js versão que você deseja toouse. Em Package. JSON, adicione o seguinte Olá `engines` propriedade tooset Olá Node. js versão tooone que queremos.

        "engines": {
            "node": "6.9.1"
        },

5. Por fim, inicialize um repositório Git e confirme seus arquivos. Em Olá raiz do aplicativo (onde é Package. JSON), execute Olá Git comandos a seguir:

        git init
        git add .
        git commit -m "<your commit message>"

Seu código está pronto toobe implantado. 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>Etapa 2: criar um aplicativo do Azure e implantar Sails.js

Em seguida, crie Olá recursos do serviço de aplicativo no Azure e implante seu tooit de aplicativo Sails.js.

1. tooAzure de login da seguinte forma:

        az login

    Siga o logon de Olá Olá prompt toocontinue em um navegador com uma conta da Microsoft com sua assinatura do Azure.

3. Definir usuário de implantação Olá para serviço de aplicativo. Mais tarde, você implantará o código usando essas credenciais.
   
        az appservice web deployment user set --user-name <username> --password <password>

3. Crie um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) com um nome. Para este tutorial Node. js, você não precisa realmente tooknow o que é.

        az group create --location "<location>" --name my-sailsjs-app-group

    toosee quais possíveis valores que você podem usar para `<location>`, use Olá `az appservice list-locations` comando CLI.

3. Criar um novo [Plano do Serviço de Aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) "GRATUITO" com um nome. Para este tutorial de Node.js, saiba que você não será cobrado por aplicativos Web neste plano.

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. Crie um novo aplicativo Web com um nome exclusivo no `<app_name>`.

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>Etapa 3: Configurar e implantar seu aplicativo Sails.js

1. Configure a implantação local do Git para seu novo aplicativo web com hello comando a seguir:

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    Você obterá uma saída JSON como este, que significa que esse repositório Git remoto do hello é configurado:

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. Adicionar URL Olá Olá JSON como um Git remoto para seu repositório local (chamado `azure` para manter a simplicidade).

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. Implantar o toohello de código de exemplo `azure` Git remoto. Quando solicitado, use as credenciais de implantação de saudação configurados anteriormente.

        git push azure master

7. Por fim, basta inicie o aplicativo do Azure ao vivo no navegador de saudação:

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    Agora você deve ver Olá a mesma página de home Sails.js.

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>Solucionar problemas de implantação
Se seu aplicativo Sails.js falhar por algum motivo no serviço de aplicativo, localizar Olá stderr logs toohelp solucioná-lo.
Para obter mais informações, consulte [como toodebug um Node. js web app no serviço de aplicativo do Azure](web-sites-nodejs-debug.md).
Se o aplicativo hello foi iniciado com êxito, log de stdout Olá deve mostrar mensagem de saudação familiar:

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

Você pode controlar a granularidade dos logs de stdout Olá no hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) arquivo.

## <a name="connect-tooa-database-in-azure"></a>Conecte-se o banco de dados tooa no Azure
o banco de dados do tooconnect tooa no Azure, você pode criar o banco de dados de saudação de sua escolha no Azure, como banco de dados SQL, MySQL, MongoDB, Cache do Azure (Redis), etc. e usar Olá correspondente [adaptador de armazenamento de dados](https://github.com/balderdashy/sails#compatibility) tooconnect tooit. Olá etapas nesta seção mostram como tooMongoDB tooconnect usando um [o banco de dados do Azure Cosmos](../documentdb/documentdb-protocol-mongodb.md) banco de dados, o que pode dar suporte a conexões de cliente do MongoDB.

1. [Criar uma conta do BD Cosmos com suporte para protocolo MongoDB](../documentdb/documentdb-create-mongodb-account.md).
2. [Criar uma coleção e banco de dados do BD Cosmos](../documentdb/documentdb-create-collection.md). Olá nome da coleção de saudação não importa, mas você precisa de nome de saudação do banco de dados de hello quando você se conectar de Sails.js.
3. [Localizar informações de conexão de saudação para seu banco de dados do banco de dados do Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).
2. Do terminal de linha de comando, instale adaptador do MongoDB hello:

        npm install sails-mongo --save

3. Abra config/connections.js e adicione Olá toohello lista de objetos de conexão a seguir:

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > Olá `ssl: true` opção é importante porque [Cosmos DB exigir](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 
    >
    >

4. Para cada variável de ambiente (`process.env.*`), você precisa tooset-lo no serviço de aplicativo. toodo, Olá execução a seguir de comandos de terminal. Use informações de conexão de saudação para seu banco de dados do Cosmos.

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    Colocar suas configurações nas configurações de aplicativo do Azure mantém dados confidenciais fora do seu controle de origem (Git). Em seguida, você configurará o desenvolvimento de seu ambiente toouse Olá mesmas informações de conexão.
5. Abra config/local.js e adicione Olá objeto conexões a seguir:

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    Essa configuração substitui as configurações de saudação em seu arquivo config/connections.js para o ambiente local hello. Esse arquivo é excluído por. gitignore padrão de saudação em seu projeto, para que ele não será armazenado no Git. Agora, você é capaz de tooconnect tooyour Cosmos DB (MongoDB) banco de dados de seu aplicativo web do Azure e do seu ambiente de desenvolvimento local.
6. Abra config/env/production.js tooconfigure seu ambiente de produção e adicione o seguinte Olá `models` objeto:

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. Abra config/env/development.js tooconfigure seu ambiente de desenvolvimento e adicione o seguinte Olá `models` objeto:

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`permite usar toocreate de recursos de migração do banco de dados e atualizar conjuntos de banco de dados ou tabelas facilmente. No entanto, `migrate: 'safe'` é usado para o seu ambiente do Azure (produção) porque Sails.js não permitem que você toouse `migrate: 'alter'` em um ambiente de produção (consulte [Sails.js documentação](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).
8. De saudação terminal, [gerar](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) um Sails.js [plano gráfico API](http://sailsjs.org/documentation/concepts/blueprints) como você normalmente faria, execute `sails lift` criar banco de dados de saudação com Sails.js migração de banco de dados. Por exemplo:

         sails generate api mywidget
         sails lift

    Olá `mywidget` modelo gerado por este comando está vazio, mas podemos usar isso tooshow que há conectividade de banco de dados.
    Quando você executa `sails lift`, ele cria coleções ausente hello e seu aplicativo usa modelos de tabelas para hello.
9. API de acesso Olá planta acabou de criar no navegador de saudação. Por exemplo:

        http://localhost:1337/mywidget/create

    Olá API deve retornar tooyou voltar de entrada hello criada na janela de navegador hello, que significa que sua coleção será criada com êxito.

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. Agora, enviar por push tooAzure suas alterações e procurar tooyour aplicativo toomake se que ele ainda funciona.

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. Acesso Olá API de especificações técnicas do seu aplicativo web do Azure. Por exemplo:

         http://<appname>.azurewebsites.net/mywidget/create

     Se Olá API retorna outra nova entrada, seu aplicativo web do Azure está falando tooyour banco de dados do banco de dados do Cosmos (MongoDB).

## <a name="more-resources"></a>Mais recursos
* [Get started with Node.js web apps in Azure App Service (Introdução aos aplicativos Web do Node.js no Serviço de Aplicativo do Azure)](app-service-web-get-started-nodejs.md)
* [Usando Módulos no Node.js com aplicativos do Microsoft Azure](../nodejs-use-node-modules-azure-apps.md)
