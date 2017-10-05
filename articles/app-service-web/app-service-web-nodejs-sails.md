---
title: "Implantar um aplicativo Web do Sails.js no Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Saiba como implantar um aplicativo do Node.js no Serviço de Aplicativo do Azure. Este tutorial mostra como implantar um aplicativo Web Sails.js."
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
ms.openlocfilehash: e36fc5f5273f98c3cca91973db9910f32443ec7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a><span data-ttu-id="e805c-104">Implantar um aplicativo Web Sails.js no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="e805c-104">Deploy a Sails.js web app to Azure App Service</span></span>
<span data-ttu-id="e805c-105">Este tutorial mostra como implantar um aplicativo Sails.js no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="e805c-105">This tutorial shows you how to deploy a Sails.js app to Azure App Service.</span></span> <span data-ttu-id="e805c-106">No processo, você pode reunir algum conhecimento geral sobre como configurar seu aplicativo Node.js para a execução no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e805c-106">In the process, you can glean some general knowledge on how to configure your Node.js app to run in App Service.</span></span>

<span data-ttu-id="e805c-107">Aqui você aprenderá habilidades úteis, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e805c-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="e805c-108">Configure um aplicativo Sails.js executado no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e805c-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="e805c-109">Implante um aplicativo para o Serviço de Aplicativo da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="e805c-109">Deploy an app to App Service from the command line.</span></span>
* <span data-ttu-id="e805c-110">Ler os logs de stderr e stdout para solucionar problemas de implantação.</span><span class="sxs-lookup"><span data-stu-id="e805c-110">Read stderr and stdout logs to troubleshoot any deployment issues.</span></span>
* <span data-ttu-id="e805c-111">Armazenar variáveis de ambiente fora do controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="e805c-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="e805c-112">Acessar as variáveis de ambiente do Azure do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e805c-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="e805c-113">Conectar-se a um banco de dados (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="e805c-113">Connect to a database (MongoDB).</span></span>

<span data-ttu-id="e805c-114">Você deve ter conhecimento prático de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="e805c-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="e805c-115">Este tutorial não se destina a ajudá-lo com problemas relacionados à execução do Sail.js em geral.</span><span class="sxs-lookup"><span data-stu-id="e805c-115">This tutorial is not intended to help you with issues related to running Sail.js in general.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="e805c-116">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="e805c-116">CLI versions to complete the task</span></span>

<span data-ttu-id="e805c-117">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="e805c-117">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="e805c-118">[CLI do Azure 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="e805c-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="e805c-119">[CLI 2.0 do Azure](app-service-web-nodejs-sails.md) – nossa última geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="e805c-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e805c-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e805c-120">Prerequisites</span></span>
* [<span data-ttu-id="e805c-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="e805c-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="e805c-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="e805c-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="e805c-123">Git</span><span class="sxs-lookup"><span data-stu-id="e805c-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="e805c-124">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="e805c-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="e805c-125">Uma conta do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e805c-125">A Microsoft Azure account.</span></span> <span data-ttu-id="e805c-126">Se não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e805c-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="e805c-127">Você pode [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) sem uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e805c-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="e805c-128">Crie um aplicativo inicial e brinque com ele por até uma hora: não é necessário cartão de crédito ou compromissos.</span><span class="sxs-lookup"><span data-stu-id="e805c-128">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="e805c-129">Etapa 1: criar e configurar um aplicativo do Sails.js localmente</span><span class="sxs-lookup"><span data-stu-id="e805c-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="e805c-130">Primeiro, crie rapidamente um aplicativo do Sails.js padrão em seu ambiente de desenvolvimento seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e805c-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="e805c-131">Abra o terminal de linha de comando de sua escolha e `CD` para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e805c-131">Open the command-line terminal of your choice and `CD` to a working directory.</span></span>
2. <span data-ttu-id="e805c-132">Crie um novo aplicativo Sails.js e execute-o:</span><span class="sxs-lookup"><span data-stu-id="e805c-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="e805c-133">Verifique se você pode navegar para a home page padrão em http://localhost:1377.</span><span class="sxs-lookup"><span data-stu-id="e805c-133">Make sure you can navigate to the default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="e805c-134">Em seguida, habilitar registro em log para o Azure.</span><span class="sxs-lookup"><span data-stu-id="e805c-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="e805c-135">No diretório raiz, crie um arquivo chamado `iisnode.yml` e adicione as duas linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e805c-135">In your root directory, create a file called `iisnode.yml` and add the following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="e805c-136">O registro em log está habilitado para o servidor [iisnode](https://github.com/tjanczuk/iisnode) que o Serviço de Aplicativo do Azure usa para executar aplicativos Node.js.</span><span class="sxs-lookup"><span data-stu-id="e805c-136">Logging is now enabled for the [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses to run Node.js apps.</span></span> 
    <span data-ttu-id="e805c-137">Para obter mais informações sobre como isso funciona, consulte [Como depurar um aplicativo Web Node.js no Serviço de Aplicativo do Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="e805c-137">For more information on how this works, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="e805c-138">Em seguida, configure o aplicativo Sails.js para usar variáveis de ambiente do Azure.</span><span class="sxs-lookup"><span data-stu-id="e805c-138">Next, configure the Sails.js app to use Azure environment variables.</span></span> <span data-ttu-id="e805c-139">Abra config/env/production.js para configurar seu ambiente de produção e definir `port` e `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="e805c-139">Open config/env/production.js to configure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="e805c-140">Você pode encontrar a documentação para essas configurações na [Documentação do Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="e805c-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="e805c-141">Em seguida, codifique a versão do Node.js que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="e805c-141">Next, hardcode the Node.js version you want to use.</span></span> <span data-ttu-id="e805c-142">Em package.json, adicione a seguinte propriedade `engines` para definir a versão do Node.js como desejado.</span><span class="sxs-lookup"><span data-stu-id="e805c-142">In package.json, add the following `engines` property to set the Node.js version to one that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="e805c-143">Por fim, inicialize um repositório Git e confirme seus arquivos.</span><span class="sxs-lookup"><span data-stu-id="e805c-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="e805c-144">Na raiz do aplicativo (na qual package.json está), execute os seguintes comandos do Git:</span><span class="sxs-lookup"><span data-stu-id="e805c-144">In the application root (where package.json is), run the following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="e805c-145">Seu código está pronto para ser implantado.</span><span class="sxs-lookup"><span data-stu-id="e805c-145">Your code is ready to be deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="e805c-146">Etapa 2: criar um aplicativo do Azure e implantar Sails.js</span><span class="sxs-lookup"><span data-stu-id="e805c-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="e805c-147">Em seguida, crie o recurso de Serviço de Aplicativo no Azure e implante seu aplicativo Sails.js nele.</span><span class="sxs-lookup"><span data-stu-id="e805c-147">Next, create the App Service resource in Azure and deploy your Sails.js app to it.</span></span>

1. <span data-ttu-id="e805c-148">Faça logon no Azure da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="e805c-148">log in to Azure like so:</span></span>

        az login

    <span data-ttu-id="e805c-149">Siga o prompt para continuar o logon em um navegador com uma conta da Microsoft que tenha sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e805c-149">Follow the prompt to continue the login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="e805c-150">Defina o usuário de implantação para o Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e805c-150">Set the deployment user for App Service.</span></span> <span data-ttu-id="e805c-151">Mais tarde, você implantará o código usando essas credenciais.</span><span class="sxs-lookup"><span data-stu-id="e805c-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="e805c-152">Crie um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) com um nome.</span><span class="sxs-lookup"><span data-stu-id="e805c-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="e805c-153">Para este tutorial de Node.js, você não precisa realmente saber o que isso é.</span><span class="sxs-lookup"><span data-stu-id="e805c-153">For this Node.js tutorial, you don't really need to know what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="e805c-154">Para ver quais possíveis valores você pode usar para `<location>`, use o comando `az appservice list-locations` da CLI.</span><span class="sxs-lookup"><span data-stu-id="e805c-154">To see what possible values you can use for `<location>`, use the `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="e805c-155">Criar um novo [Plano do Serviço de Aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) "GRATUITO" com um nome.</span><span class="sxs-lookup"><span data-stu-id="e805c-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="e805c-156">Para este tutorial de Node.js, saiba que você não será cobrado por aplicativos Web neste plano.</span><span class="sxs-lookup"><span data-stu-id="e805c-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="e805c-157">Crie um novo aplicativo Web com um nome exclusivo no `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="e805c-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="e805c-158">Etapa 3: Configurar e implantar seu aplicativo Sails.js</span><span class="sxs-lookup"><span data-stu-id="e805c-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="e805c-159">Configure a implantação Git local para o novo aplicativo Web com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="e805c-159">Configure local Git deployment for your new web app with the following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="e805c-160">Você receberá uma saída JSON como esta, o que significa que o repositório Git remoto está configurado:</span><span class="sxs-lookup"><span data-stu-id="e805c-160">You will get a JSON output like this, which means that the remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="e805c-161">Adicione a URL no JSON como um Git remoto para seu repositório local (chamado de `azure` para manter a simplicidade).</span><span class="sxs-lookup"><span data-stu-id="e805c-161">Add the URL in the JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="e805c-162">Implante o código de exemplo no Git remoto do `azure`.</span><span class="sxs-lookup"><span data-stu-id="e805c-162">Deploy your sample code to the `azure` Git remote.</span></span> <span data-ttu-id="e805c-163">Quando solicitado, use as credenciais de implantação que você configurou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e805c-163">When prompted, use the deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="e805c-164">Por fim, apenas abra seu aplicativo do Azure ativo no navegador:</span><span class="sxs-lookup"><span data-stu-id="e805c-164">Finally, just launch your live Azure app in the browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="e805c-165">Agora você deve ver a mesma home page do Sails.js.</span><span class="sxs-lookup"><span data-stu-id="e805c-165">You should now see the same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="e805c-166">Solucionar problemas de implantação</span><span class="sxs-lookup"><span data-stu-id="e805c-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="e805c-167">Se seu aplicativo Sails.js falhar por algum motivo no Serviço de Aplicativo, encontre os logs de stderr para ajudar na solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="e805c-167">If your Sails.js application fails for some reason in App Service, find the stderr logs to help troubleshoot it.</span></span>
<span data-ttu-id="e805c-168">Para obter mais informações, consulte [Como depurar um aplicativo Web Node.js no Serviço de Aplicativo do Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="e805c-168">For more information, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="e805c-169">Se o aplicativo tiver sido iniciado com êxito, o log de stdout deverá mostrar a você a mensagem familiar:</span><span class="sxs-lookup"><span data-stu-id="e805c-169">If the app has started successfully, the stdout log should show you the familiar message:</span></span>

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
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="e805c-170">Você pode controlar a granularidade dos logs do stdout no arquivo [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) .</span><span class="sxs-lookup"><span data-stu-id="e805c-170">You can control granularity of the stdout logs in the [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-to-a-database-in-azure"></a><span data-ttu-id="e805c-171">Conectar-se a um banco de dados no Azure</span><span class="sxs-lookup"><span data-stu-id="e805c-171">Connect to a database in Azure</span></span>
<span data-ttu-id="e805c-172">Para se conectar a um banco de dados no Azure, crie o banco de dados de sua escolha no Azure, como Banco de Dados SQL, MySQL, MongoDB, Cache (Redis) do Azure, dentre outros, e use o [adaptador de repositório de dados](https://github.com/balderdashy/sails#compatibility) correspondente para se conectar a ele.</span><span class="sxs-lookup"><span data-stu-id="e805c-172">To connect to a database in Azure, you create the database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use the corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) to connect to it.</span></span> <span data-ttu-id="e805c-173">As etapas nesta seção mostram como se conectar ao MongoDB usando um [BD Cosmos do Azure](../documentdb/documentdb-protocol-mongodb.md), que pode dar suporte a conexões de cliente do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e805c-173">The steps in this section show you how to connect to MongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="e805c-174">[Criar uma conta do BD Cosmos com suporte para protocolo MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="e805c-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="e805c-175">[Criar uma coleção e banco de dados do BD Cosmos](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="e805c-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="e805c-176">O nome da coleção não importa, mas você precisará do nome do banco de dados quando você se conectar de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="e805c-176">The name of the collection doesn't matter, but you need the name of the database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="e805c-177">[Localizar as informações de conexão para seu BD Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="e805c-177">[Find the connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="e805c-178">No seu terminal de linha de comando, instale o adaptador do MongoDB:</span><span class="sxs-lookup"><span data-stu-id="e805c-178">From your command-line terminal, install the MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="e805c-179">Abra config/connections.js e adicione o seguinte objeto de conexão à lista:</span><span class="sxs-lookup"><span data-stu-id="e805c-179">Open config/connections.js and add the following connection object to the list:</span></span>

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
    > <span data-ttu-id="e805c-180">A opção `ssl: true` é importante porque o [BD Cosmos a requer](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="e805c-180">The `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="e805c-181">Para cada variável de ambiente (`process.env.*`), você precisa defini-la no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e805c-181">For each environment variable (`process.env.*`), you need to set it in App Service.</span></span> <span data-ttu-id="e805c-182">Para isso, execute os comandos a seguir no seu terminal.</span><span class="sxs-lookup"><span data-stu-id="e805c-182">To do this, run the following commands from your terminal.</span></span> <span data-ttu-id="e805c-183">Use as informações de conexão para seu BD Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e805c-183">Use the connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="e805c-184">Colocar suas configurações nas configurações de aplicativo do Azure mantém dados confidenciais fora do seu controle de origem (Git).</span><span class="sxs-lookup"><span data-stu-id="e805c-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="e805c-185">Em seguida, você configurará seu ambiente de desenvolvimento para usar as mesmas informações de conexão.</span><span class="sxs-lookup"><span data-stu-id="e805c-185">Next, you will configure your development environment to use the same connection information.</span></span>
5. <span data-ttu-id="e805c-186">Abra config/local.js e adicione o seguinte objeto de conexão:</span><span class="sxs-lookup"><span data-stu-id="e805c-186">Open config/local.js and add the following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="e805c-187">Essa configuração substitui as configurações no arquivo config/connections.js para o ambiente local.</span><span class="sxs-lookup"><span data-stu-id="e805c-187">This configuration overrides the settings in your config/connections.js file for the local environment.</span></span> <span data-ttu-id="e805c-188">Esse arquivo é excluído pelo .gitignore padrão em seu projeto, portanto não será armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="e805c-188">This file is excluded by the default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="e805c-189">Agora, você será capaz de se conectar ao BD Cosmos (MongoDB) tanto de seu aplicativo Web do Azure quanto do ambiente de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="e805c-189">Now, you are able to connect to your Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="e805c-190">Abra config/env/production.js para configurar seu ambiente de produção e adicione o seguinte objeto `models` :</span><span class="sxs-lookup"><span data-stu-id="e805c-190">Open config/env/production.js to configure your production environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="e805c-191">Abra config/env/development.js para configurar seu ambiente de desenvolvimento e adicione o seguinte objeto `models` :</span><span class="sxs-lookup"><span data-stu-id="e805c-191">Open config/env/development.js to configure your development environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="e805c-192">`migrate: 'alter'` permite que você use os recursos de migração do banco de dados para criar e atualizar facilmente suas coleções ou tabelas de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e805c-192">`migrate: 'alter'` lets you use database migration features to create and update database collections or tables easily.</span></span> <span data-ttu-id="e805c-193">No entanto, o `migrate: 'safe'` é usado para seu ambiente (produção) do Azure, pois Sails.js não permite o uso de `migrate: 'alter'` em um ambiente de produção (confira a [Documentação do Sails.js](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="e805c-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you to use `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="e805c-194">No terminal, [gere](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) um [API de plano gráfico](http://sailsjs.org/documentation/concepts/blueprints) do Sails.js, como você faria normalmente, e execute `sails lift` para criar o banco de dados com a migração de banco de dados do Sails.js.</span><span class="sxs-lookup"><span data-stu-id="e805c-194">From the terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create the database with Sails.js database migration.</span></span> <span data-ttu-id="e805c-195">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e805c-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="e805c-196">O modelo `mywidget` gerado por este comando está vazio, mas podemos usar isso para mostrar que temos conectividade com o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e805c-196">The `mywidget` model generated by this command is empty, but we can use it to show that we have database connectivity.</span></span>
    <span data-ttu-id="e805c-197">Quando você executa o `sails lift`, ele cria as coleções e tabelas ausentes para os modelos usados por seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e805c-197">When you run `sails lift`, it creates the missing collections and tables for the models your app uses.</span></span>
9. <span data-ttu-id="e805c-198">Acesse a API de plano gráfico que você acabou de criar no navegador.</span><span class="sxs-lookup"><span data-stu-id="e805c-198">Access the blueprint API you just created in the browser.</span></span> <span data-ttu-id="e805c-199">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e805c-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="e805c-200">A API deve retornar a entrada criada para você na janela do navegador, o que significa que a sua coleção foi criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="e805c-200">The API should return the created entry back to you in the browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="e805c-201">Agora, envie por push suas alterações para o Azure e navegue até seu aplicativo para verificar se ele ainda funciona.</span><span class="sxs-lookup"><span data-stu-id="e805c-201">Now, push your changes to Azure, and browse to your app to make sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="e805c-202">Acesse a API de plano gráfico de seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="e805c-202">Access the blueprint API of your Azure web app.</span></span> <span data-ttu-id="e805c-203">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e805c-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="e805c-204">Se a API retornar outra entrada nova, seu aplicativo Web do Azure estará falando com seu BD Cosmos (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="e805c-204">If the API returns another new entry, then your Azure web app is talking to your Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="e805c-205">Mais recursos</span><span class="sxs-lookup"><span data-stu-id="e805c-205">More resources</span></span>
* [<span data-ttu-id="e805c-206">Get started with Node.js web apps in Azure App Service (Introdução aos aplicativos Web do Node.js no Serviço de Aplicativo do Azure)</span><span class="sxs-lookup"><span data-stu-id="e805c-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="e805c-207">Usando Módulos no Node.js com aplicativos do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e805c-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
