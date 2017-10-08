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
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a><span data-ttu-id="9fc5b-104">Implantar um tooAzure de aplicativo web do Sails.js do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="9fc5b-104">Deploy a Sails.js web app tooAzure App Service</span></span>
<span data-ttu-id="9fc5b-105">Este tutorial mostra como toodeploy um aplicativo de Sails.js tooAzure do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-105">This tutorial shows you how toodeploy a Sails.js app tooAzure App Service.</span></span> <span data-ttu-id="9fc5b-106">No processo de saudação, você pode obter conhecimentos gerais sobre como tooconfigure seu toorun de aplicativo Node. js no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-106">In hello process, you can glean some general knowledge on how tooconfigure your Node.js app toorun in App Service.</span></span>

<span data-ttu-id="9fc5b-107">Aqui você aprenderá habilidades úteis, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="9fc5b-108">Configure um aplicativo Sails.js executado no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="9fc5b-109">Implante um tooApp aplicativo serviço Olá linha de comando.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-109">Deploy an app tooApp Service from hello command line.</span></span>
* <span data-ttu-id="9fc5b-110">STDOUT e stderr leitura registra tootroubleshoot quaisquer problemas de implantação.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-110">Read stderr and stdout logs tootroubleshoot any deployment issues.</span></span>
* <span data-ttu-id="9fc5b-111">Armazenar variáveis de ambiente fora do controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="9fc5b-112">Acessar as variáveis de ambiente do Azure do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="9fc5b-113">Conecte-se o banco de dados tooa (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-113">Connect tooa database (MongoDB).</span></span>

<span data-ttu-id="9fc5b-114">Você deve ter conhecimento prático de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="9fc5b-115">Este tutorial não é pretendido toohelp com problemas relacionados a toorunning Sail.js em geral.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-115">This tutorial is not intended toohelp you with issues related toorunning Sail.js in general.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="9fc5b-116">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="9fc5b-116">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="9fc5b-117">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-117">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="9fc5b-118">[1.0 de CLI do Azure](app-service-web-nodejs-sails-cli-nodejs.md) – nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de Olá</span><span class="sxs-lookup"><span data-stu-id="9fc5b-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="9fc5b-119">[2.0 do CLI do Azure](app-service-web-nodejs-sails.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="9fc5b-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fc5b-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9fc5b-120">Prerequisites</span></span>
* [<span data-ttu-id="9fc5b-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="9fc5b-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="9fc5b-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="9fc5b-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="9fc5b-123">Git</span><span class="sxs-lookup"><span data-stu-id="9fc5b-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="9fc5b-124">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="9fc5b-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="9fc5b-125">Uma conta do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-125">A Microsoft Azure account.</span></span> <span data-ttu-id="9fc5b-126">Se não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="9fc5b-127">Você pode [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) sem uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="9fc5b-128">Criar um aplicativo de início e explorá-la para a hora de tooan – nenhum cartão de crédito necessários, nenhum investimento.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-128">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="9fc5b-129">Etapa 1: criar e configurar um aplicativo do Sails.js localmente</span><span class="sxs-lookup"><span data-stu-id="9fc5b-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="9fc5b-130">Primeiro, crie rapidamente um aplicativo do Sails.js padrão em seu ambiente de desenvolvimento seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="9fc5b-131">Terminal de linha de comando Olá aberto de sua escolha e `CD` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-131">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span>
2. <span data-ttu-id="9fc5b-132">Crie um novo aplicativo Sails.js e execute-o:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="9fc5b-133">Verifique se que você pode navegar toohello padrão home page em http://localhost:1377.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-133">Make sure you can navigate toohello default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="9fc5b-134">Em seguida, habilitar registro em log para o Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="9fc5b-135">No diretório raiz, crie um arquivo chamado `iisnode.yml` e adicione Olá duas linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-135">In your root directory, create a file called `iisnode.yml` and add hello following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="9fc5b-136">Registro em log está ativado para Olá [iisnode](https://github.com/tjanczuk/iisnode) do serviço de aplicativo do Azure usa toorun Node. js aplicativos de servidor.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-136">Logging is now enabled for hello [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses toorun Node.js apps.</span></span> 
    <span data-ttu-id="9fc5b-137">Para obter mais informações sobre como isso funciona, consulte [como toodebug um Node. js web app no serviço de aplicativo do Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-137">For more information on how this works, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="9fc5b-138">Em seguida, configure as variáveis de ambiente do Azure Olá Sails.js aplicativo toouse.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-138">Next, configure hello Sails.js app toouse Azure environment variables.</span></span> <span data-ttu-id="9fc5b-139">Abra config/env/production.js tooconfigure seu ambiente de produção e defina `port` e `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-139">Open config/env/production.js tooconfigure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="9fc5b-140">Você pode encontrar a documentação para essas configurações na [Documentação do Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="9fc5b-141">Em seguida, codifique Olá Node. js versão que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-141">Next, hardcode hello Node.js version you want toouse.</span></span> <span data-ttu-id="9fc5b-142">Em Package. JSON, adicione o seguinte Olá `engines` propriedade tooset Olá Node. js versão tooone que queremos.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-142">In package.json, add hello following `engines` property tooset hello Node.js version tooone that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="9fc5b-143">Por fim, inicialize um repositório Git e confirme seus arquivos.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="9fc5b-144">Em Olá raiz do aplicativo (onde é Package. JSON), execute Olá Git comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-144">In hello application root (where package.json is), run hello following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="9fc5b-145">Seu código está pronto toobe implantado.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-145">Your code is ready toobe deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="9fc5b-146">Etapa 2: criar um aplicativo do Azure e implantar Sails.js</span><span class="sxs-lookup"><span data-stu-id="9fc5b-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="9fc5b-147">Em seguida, crie Olá recursos do serviço de aplicativo no Azure e implante seu tooit de aplicativo Sails.js.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-147">Next, create hello App Service resource in Azure and deploy your Sails.js app tooit.</span></span>

1. <span data-ttu-id="9fc5b-148">tooAzure de login da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-148">log in tooAzure like so:</span></span>

        az login

    <span data-ttu-id="9fc5b-149">Siga o logon de Olá Olá prompt toocontinue em um navegador com uma conta da Microsoft com sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-149">Follow hello prompt toocontinue hello login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="9fc5b-150">Definir usuário de implantação Olá para serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-150">Set hello deployment user for App Service.</span></span> <span data-ttu-id="9fc5b-151">Mais tarde, você implantará o código usando essas credenciais.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="9fc5b-152">Crie um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) com um nome.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="9fc5b-153">Para este tutorial Node. js, você não precisa realmente tooknow o que é.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-153">For this Node.js tutorial, you don't really need tooknow what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="9fc5b-154">toosee quais possíveis valores que você podem usar para `<location>`, use Olá `az appservice list-locations` comando CLI.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-154">toosee what possible values you can use for `<location>`, use hello `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="9fc5b-155">Criar um novo [Plano do Serviço de Aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) "GRATUITO" com um nome.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="9fc5b-156">Para este tutorial de Node.js, saiba que você não será cobrado por aplicativos Web neste plano.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="9fc5b-157">Crie um novo aplicativo Web com um nome exclusivo no `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="9fc5b-158">Etapa 3: Configurar e implantar seu aplicativo Sails.js</span><span class="sxs-lookup"><span data-stu-id="9fc5b-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="9fc5b-159">Configure a implantação local do Git para seu novo aplicativo web com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-159">Configure local Git deployment for your new web app with hello following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="9fc5b-160">Você obterá uma saída JSON como este, que significa que esse repositório Git remoto do hello é configurado:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-160">You will get a JSON output like this, which means that hello remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="9fc5b-161">Adicionar URL Olá Olá JSON como um Git remoto para seu repositório local (chamado `azure` para manter a simplicidade).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-161">Add hello URL in hello JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="9fc5b-162">Implantar o toohello de código de exemplo `azure` Git remoto.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-162">Deploy your sample code toohello `azure` Git remote.</span></span> <span data-ttu-id="9fc5b-163">Quando solicitado, use as credenciais de implantação de saudação configurados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-163">When prompted, use hello deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="9fc5b-164">Por fim, basta inicie o aplicativo do Azure ao vivo no navegador de saudação:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-164">Finally, just launch your live Azure app in hello browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="9fc5b-165">Agora você deve ver Olá a mesma página de home Sails.js.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-165">You should now see hello same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="9fc5b-166">Solucionar problemas de implantação</span><span class="sxs-lookup"><span data-stu-id="9fc5b-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="9fc5b-167">Se seu aplicativo Sails.js falhar por algum motivo no serviço de aplicativo, localizar Olá stderr logs toohelp solucioná-lo.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-167">If your Sails.js application fails for some reason in App Service, find hello stderr logs toohelp troubleshoot it.</span></span>
<span data-ttu-id="9fc5b-168">Para obter mais informações, consulte [como toodebug um Node. js web app no serviço de aplicativo do Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-168">For more information, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="9fc5b-169">Se o aplicativo hello foi iniciado com êxito, log de stdout Olá deve mostrar mensagem de saudação familiar:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-169">If hello app has started successfully, hello stdout log should show you hello familiar message:</span></span>

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

<span data-ttu-id="9fc5b-170">Você pode controlar a granularidade dos logs de stdout Olá no hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) arquivo.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-170">You can control granularity of hello stdout logs in hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-tooa-database-in-azure"></a><span data-ttu-id="9fc5b-171">Conecte-se o banco de dados tooa no Azure</span><span class="sxs-lookup"><span data-stu-id="9fc5b-171">Connect tooa database in Azure</span></span>
<span data-ttu-id="9fc5b-172">o banco de dados do tooconnect tooa no Azure, você pode criar o banco de dados de saudação de sua escolha no Azure, como banco de dados SQL, MySQL, MongoDB, Cache do Azure (Redis), etc. e usar Olá correspondente [adaptador de armazenamento de dados](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-172">tooconnect tooa database in Azure, you create hello database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use hello corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span></span> <span data-ttu-id="9fc5b-173">Olá etapas nesta seção mostram como tooMongoDB tooconnect usando um [o banco de dados do Azure Cosmos](../documentdb/documentdb-protocol-mongodb.md) banco de dados, o que pode dar suporte a conexões de cliente do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-173">hello steps in this section show you how tooconnect tooMongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="9fc5b-174">[Criar uma conta do BD Cosmos com suporte para protocolo MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="9fc5b-175">[Criar uma coleção e banco de dados do BD Cosmos](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="9fc5b-176">Olá nome da coleção de saudação não importa, mas você precisa de nome de saudação do banco de dados de hello quando você se conectar de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-176">hello name of hello collection doesn't matter, but you need hello name of hello database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="9fc5b-177">[Localizar informações de conexão de saudação para seu banco de dados do banco de dados do Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-177">[Find hello connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="9fc5b-178">Do terminal de linha de comando, instale adaptador do MongoDB hello:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-178">From your command-line terminal, install hello MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="9fc5b-179">Abra config/connections.js e adicione Olá toohello lista de objetos de conexão a seguir:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-179">Open config/connections.js and add hello following connection object toohello list:</span></span>

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
    > <span data-ttu-id="9fc5b-180">Olá `ssl: true` opção é importante porque [Cosmos DB exigir](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-180">hello `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="9fc5b-181">Para cada variável de ambiente (`process.env.*`), você precisa tooset-lo no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-181">For each environment variable (`process.env.*`), you need tooset it in App Service.</span></span> <span data-ttu-id="9fc5b-182">toodo, Olá execução a seguir de comandos de terminal.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-182">toodo this, run hello following commands from your terminal.</span></span> <span data-ttu-id="9fc5b-183">Use informações de conexão de saudação para seu banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-183">Use hello connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="9fc5b-184">Colocar suas configurações nas configurações de aplicativo do Azure mantém dados confidenciais fora do seu controle de origem (Git).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="9fc5b-185">Em seguida, você configurará o desenvolvimento de seu ambiente toouse Olá mesmas informações de conexão.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-185">Next, you will configure your development environment toouse hello same connection information.</span></span>
5. <span data-ttu-id="9fc5b-186">Abra config/local.js e adicione Olá objeto conexões a seguir:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-186">Open config/local.js and add hello following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="9fc5b-187">Essa configuração substitui as configurações de saudação em seu arquivo config/connections.js para o ambiente local hello.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-187">This configuration overrides hello settings in your config/connections.js file for hello local environment.</span></span> <span data-ttu-id="9fc5b-188">Esse arquivo é excluído por. gitignore padrão de saudação em seu projeto, para que ele não será armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-188">This file is excluded by hello default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="9fc5b-189">Agora, você é capaz de tooconnect tooyour Cosmos DB (MongoDB) banco de dados de seu aplicativo web do Azure e do seu ambiente de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-189">Now, you are able tooconnect tooyour Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="9fc5b-190">Abra config/env/production.js tooconfigure seu ambiente de produção e adicione o seguinte Olá `models` objeto:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-190">Open config/env/production.js tooconfigure your production environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="9fc5b-191">Abra config/env/development.js tooconfigure seu ambiente de desenvolvimento e adicione o seguinte Olá `models` objeto:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-191">Open config/env/development.js tooconfigure your development environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="9fc5b-192">`migrate: 'alter'`permite usar toocreate de recursos de migração do banco de dados e atualizar conjuntos de banco de dados ou tabelas facilmente.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-192">`migrate: 'alter'` lets you use database migration features toocreate and update database collections or tables easily.</span></span> <span data-ttu-id="9fc5b-193">No entanto, `migrate: 'safe'` é usado para o seu ambiente do Azure (produção) porque Sails.js não permitem que você toouse `migrate: 'alter'` em um ambiente de produção (consulte [Sails.js documentação](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you toouse `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="9fc5b-194">De saudação terminal, [gerar](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) um Sails.js [plano gráfico API](http://sailsjs.org/documentation/concepts/blueprints) como você normalmente faria, execute `sails lift` criar banco de dados de saudação com Sails.js migração de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-194">From hello terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create hello database with Sails.js database migration.</span></span> <span data-ttu-id="9fc5b-195">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="9fc5b-196">Olá `mywidget` modelo gerado por este comando está vazio, mas podemos usar isso tooshow que há conectividade de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-196">hello `mywidget` model generated by this command is empty, but we can use it tooshow that we have database connectivity.</span></span>
    <span data-ttu-id="9fc5b-197">Quando você executa `sails lift`, ele cria coleções ausente hello e seu aplicativo usa modelos de tabelas para hello.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-197">When you run `sails lift`, it creates hello missing collections and tables for hello models your app uses.</span></span>
9. <span data-ttu-id="9fc5b-198">API de acesso Olá planta acabou de criar no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-198">Access hello blueprint API you just created in hello browser.</span></span> <span data-ttu-id="9fc5b-199">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="9fc5b-200">Olá API deve retornar tooyou voltar de entrada hello criada na janela de navegador hello, que significa que sua coleção será criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-200">hello API should return hello created entry back tooyou in hello browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="9fc5b-201">Agora, enviar por push tooAzure suas alterações e procurar tooyour aplicativo toomake se que ele ainda funciona.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-201">Now, push your changes tooAzure, and browse tooyour app toomake sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="9fc5b-202">Acesso Olá API de especificações técnicas do seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc5b-202">Access hello blueprint API of your Azure web app.</span></span> <span data-ttu-id="9fc5b-203">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9fc5b-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="9fc5b-204">Se Olá API retorna outra nova entrada, seu aplicativo web do Azure está falando tooyour banco de dados do banco de dados do Cosmos (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="9fc5b-204">If hello API returns another new entry, then your Azure web app is talking tooyour Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="9fc5b-205">Mais recursos</span><span class="sxs-lookup"><span data-stu-id="9fc5b-205">More resources</span></span>
* [<span data-ttu-id="9fc5b-206">Get started with Node.js web apps in Azure App Service (Introdução aos aplicativos Web do Node.js no Serviço de Aplicativo do Azure)</span><span class="sxs-lookup"><span data-stu-id="9fc5b-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="9fc5b-207">Usando Módulos no Node.js com aplicativos do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9fc5b-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
