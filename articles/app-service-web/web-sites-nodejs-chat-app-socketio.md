---
title: "Criar um aplicativo de chat do Node.js com Socket.IO no Serviço de Aplicativo do Azure"
description: Um tutorial que demonstra como usar o socket.io em um aplicativo Web node.js hospedado no Azure.
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: e1aa539e1134884261ea7464bfda6d14815618d4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="dce95-103">Criar um aplicativo de chat do Node.js com Socket.IO no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="dce95-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="dce95-104">Socket.IO fornece uma comunicação em tempo real entre o seu servidor node.js e clientes usando WebSockets.</span><span class="sxs-lookup"><span data-stu-id="dce95-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="dce95-105">Ele também dá suporte a fallback para outros transportes (como sondagem longa) que funcionam com navegadores mais antigos.</span><span class="sxs-lookup"><span data-stu-id="dce95-105">It also supports fallback to other transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="dce95-106">Este tutorial explicará a você passo a passo como hospedar um aplicativo de chat baseado em Socket.IO como um aplicativo Web do Azure e como dimensionar o aplicativo usando o [Cache Redis do Azure].</span><span class="sxs-lookup"><span data-stu-id="dce95-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how to scale the application using [Azure Redis Cache].</span></span> <span data-ttu-id="dce95-107">Para mais informações sobre o Socket.IO, consulte <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="dce95-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="dce95-108">Os procedimentos nesta tarefa aplicam-se a [Aplicativos Web do Serviço de Aplicativo]. Para Serviços de Nuvem, consulte [Criar um aplicativo de chat do Node.js com Socket.IO em um serviço de nuvem do Azure].</span><span class="sxs-lookup"><span data-stu-id="dce95-108">The procedures in this task apply to [App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-the-chat-example"></a><span data-ttu-id="dce95-109">Baixar o exemplo de chat</span><span class="sxs-lookup"><span data-stu-id="dce95-109">Download the chat example</span></span>
<span data-ttu-id="dce95-110">Para este projeto, usaremos o exemplo de chat do [repositório Socket.IOGitHub].</span><span class="sxs-lookup"><span data-stu-id="dce95-110">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="dce95-111">Execute as seguintes etapas para baixar o exemplo e adicioná-lo ao projeto que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="dce95-111">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="dce95-112">Baixar uma [versão arquivada ZIP ou GZ] do projeto Socket.IO (a versão 1.3.5 foi usada para este documento)</span><span class="sxs-lookup"><span data-stu-id="dce95-112">Download a [ZIP or GZ archived release] of the Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="dce95-113">Extrair o arquivo e copiar o diretório **examples\\chat** para um novo local.</span><span class="sxs-lookup"><span data-stu-id="dce95-113">Extract the archive and copy the **examples\\chat** directory to a new location.</span></span> <span data-ttu-id="dce95-114">Por exemplo, **\\node\\chat**.</span><span class="sxs-lookup"><span data-stu-id="dce95-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="dce95-115">Modificar o app.js e instalar os módulos</span><span class="sxs-lookup"><span data-stu-id="dce95-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="dce95-116">Renomeie o arquivo **index.js** para o **app.js**.</span><span class="sxs-lookup"><span data-stu-id="dce95-116">Rename the **index.js** file to **app.js**.</span></span> <span data-ttu-id="dce95-117">Isso permite que o Azure detecte que este é um aplicativo Node.js.</span><span class="sxs-lookup"><span data-stu-id="dce95-117">This allows Azure to detect that this is a Node.js application.</span></span>
2. <span data-ttu-id="dce95-118">Abra o arquivo **app.js** em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="dce95-118">Open the **app.js** file in a text editor.</span></span> <span data-ttu-id="dce95-119">Altere a linha que contém `var io = require('../..')(server);` , conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="dce95-119">Change the line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="dce95-120">Abra o arquivo **package.json** e adicione uma referência ao socket.io em `dependencies`, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="dce95-120">Open the **package.json** file and add a reference to socket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="dce95-121">Na linha de comando, altere para o diretório **\\node\\chat** e use npm para instalar os módulos necessários para esse aplicativo:</span><span class="sxs-lookup"><span data-stu-id="dce95-121">From the command-line, change to the **\\node\\chat** directory and use npm to install the modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="dce95-122">Isso instalará os módulos em uma subpasta chamada **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="dce95-122">This will install the modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="dce95-123">Criar um aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="dce95-123">Create an Azure Web App</span></span>
<span data-ttu-id="dce95-124">Siga estas etapas para criar um aplicativo Web do Azure e habilitar a publicação Git e, em seguida, habilitar o suporte dado ao site pelo WebSocket.</span><span class="sxs-lookup"><span data-stu-id="dce95-124">Follow these steps to create an Azure web app, enable Git publishing, and then enable WebSocket support for the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="dce95-125">Para concluir este tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce95-125">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="dce95-126">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="dce95-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="dce95-127">Para obter detalhes, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Avaliação Gratuita do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="dce95-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="dce95-128">Instalar a interface de linha de comando do Azure (CLI do Azure) e conecte-se à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce95-128">Install the Azure Command-Line Interface (Azure CLI) and connect to your Azure subscription.</span></span> <span data-ttu-id="dce95-129">Consulte [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="dce95-129">See [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="dce95-130">Se for a primeira vez que você configura um repositório no Azure, você precisa criar suas credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="dce95-130">If this is your first time setting up a repository in Azure, you need to create login credentials.</span></span> <span data-ttu-id="dce95-131">Na CLI do Azure, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="dce95-131">From the Azure CLI, enter the following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="dce95-132">Alterne para o diretório **\\node\chat** e use o comando a seguir para criar um novo aplicativo Web do Azure e um repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="dce95-132">Change to the **\\node\chat** directory and use the following command to create a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="dce95-133">Esse comando também cria um repositório remoto do Git chamado 'azure'.</span><span class="sxs-lookup"><span data-stu-id="dce95-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="dce95-134">Você deve substituir 'mysitename' por um nome exclusivo para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="dce95-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="dce95-135">Confirme os arquivos existentes no local repositório usando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="dce95-135">Commit the existing files to the local repository by using the following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="dce95-136">Envie por push os arquivos para o repositório de aplicativos Web do Azure com o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="dce95-136">Push the files to the Azure Web Apps repository with the following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="dce95-137">Quando solicitado, insira suas credenciais da etapa 2.</span><span class="sxs-lookup"><span data-stu-id="dce95-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="dce95-138">Você receberá mensagens de status que módulos são importados no servidor.</span><span class="sxs-lookup"><span data-stu-id="dce95-138">You will receive status messages as modules are imported on the server.</span></span> <span data-ttu-id="dce95-139">Quando esse processo for concluído, o aplicativo será hospedado em seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce95-139">Once this process has completed, the application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dce95-140">Durante a instalação do módulo, você poderá observar erros que '... O projeto importado não foi encontrado '.</span><span class="sxs-lookup"><span data-stu-id="dce95-140">During module installation, you may notice errors that 'The imported project ... was not found'.</span></span> <span data-ttu-id="dce95-141">Isso podem ser ignorados.</span><span class="sxs-lookup"><span data-stu-id="dce95-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="dce95-142">Socket.IO usa o WebSocket, que não é habilitado por padrão no Azure.</span><span class="sxs-lookup"><span data-stu-id="dce95-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="dce95-143">Para habilitar os websockets, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="dce95-143">To enable web sockets, use the following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="dce95-144">Se solicitado, digite o nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="dce95-144">If prompted, enter the name of the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dce95-145">O comando 'azure site set -w' funcionará somente com a versão 0.7.4 ou superior da Interface de Linha de Comando do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce95-145">The 'azure site set -w' command will work only with version 0.7.4 or higher of the Azure Command-Line Interface.</span></span> <span data-ttu-id="dce95-146">Você também pode habilitar o suporte ao WebSocket usando o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dce95-146">You can also enable WebSocket support using the [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="dce95-147">Para habilitar WebSockets usando o Portal do Azure, clique no aplicativo Web na folha de aplicativos Web, clique em **Todas as configurações** > **Configurações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="dce95-147">To enable WebSockets using the Azure Portal, click the web app from the Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="dce95-148">Em **Web Sockets**, clique em **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="dce95-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="dce95-149">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="dce95-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="dce95-150">Para exibir o aplicativo Web no Azure, use o comando a seguir para iniciar seu navegador da Web e navegue até o aplicativo Web hospedado:</span><span class="sxs-lookup"><span data-stu-id="dce95-150">To view the web app on Azure, use the following command to launch your web browser and navigate to the hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="dce95-151">Seu aplicativo agora está sendo executado no Azure e pode retransmitir mensagens de chat entre diferentes clientes usando o Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="dce95-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="dce95-152">Expansão</span><span class="sxs-lookup"><span data-stu-id="dce95-152">Scale out</span></span>
<span data-ttu-id="dce95-153">Os aplicativos Socket.IO podem ser expandidos usando um **adaptador** para distribuir as mensagens e eventos entre várias instâncias do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dce95-153">Socket.IO applications can be scaled out by using an **adapter** to distribute messages and events between multiple application instances.</span></span> <span data-ttu-id="dce95-154">Embora haja vários adaptadores disponíveis, o adaptador [socket.io-redis] pode ser facilmente usado com o recurso Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce95-154">While there are several adapters available, the [socket.io-redis] adapter can be easily used with the Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="dce95-155">Um requisito adicional para expandir uma solução Socket.IO é dar suporte a sessões complexas.</span><span class="sxs-lookup"><span data-stu-id="dce95-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="dce95-156">As sessões complexas são habilitadas por padrão para Aplicativos Web do Azure por meio do Request Routing do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce95-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="dce95-157">Para obter mais informações, consulte [Afinidade da instância nos Sites do Azure].</span><span class="sxs-lookup"><span data-stu-id="dce95-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="dce95-158">Criar um cache Redis</span><span class="sxs-lookup"><span data-stu-id="dce95-158">Create a Redis cache</span></span>
<span data-ttu-id="dce95-159">Executar as etapas no [Criar um cache no Cache Redis do Azure] para criar um novo cache.</span><span class="sxs-lookup"><span data-stu-id="dce95-159">Perform the steps in [Create a cache in Azure Redis Cache] to create a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="dce95-160">Salve o **Nome do Host** e **Chave primária** para seu cache, pois serão necessários nas próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="dce95-160">Save the **Host name** and **Primary key** for your cache, as these will be needed in the next steps.</span></span>
> 
> 

### <a name="add-the-redis-and-socketio-redis-modules"></a><span data-ttu-id="dce95-161">Adicionar os módulos redis e socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="dce95-161">Add the redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="dce95-162">Na linha de comando, altere para o diretório **\\node\\chat** e use o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="dce95-162">From a command-line, change to the **\\node\\chat** directory and use the following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="dce95-163">As versões especificadas neste comando são as versões usadas ao testar este artigo.</span><span class="sxs-lookup"><span data-stu-id="dce95-163">The versions specified in this command are the versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="dce95-164">Modificar o arquivo **app.js** para adicionar as seguintes linhas imediatamente após `var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="dce95-164">Modify the **app.js** file to add the following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="dce95-165">Substituir **redishostname** e **rediskey** com o nome e a chave do host para seu cache Redis.</span><span class="sxs-lookup"><span data-stu-id="dce95-165">Replace **redishostname** and **rediskey** with the host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="dce95-166">Isso criará um cliente público e assinado no cache Redis criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="dce95-166">This will create a publish and subscribe client to the Redis cache created previously.</span></span> <span data-ttu-id="dce95-167">Os clientes são usados com o adaptador para configurar o Socket.IO para usar o cache Redis para passar mensagens e eventos entre instâncias do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dce95-167">The clients are then used with the adapter to configure Socket.IO to use the Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dce95-168">Embora o adaptador **socket.io-redis** possa se comunicar diretamente com o Redis, a versão atual não dá suporte à autenticação requerida pelo Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce95-168">While the **socket.io-redis** adapter can communicate directly to Redis, the current version does not support the authentication required by Azure Redis cache.</span></span> <span data-ttu-id="dce95-169">Então a conexão inicial é criada usando o módulo **redis** e o cliente é passado ao adaptador **socket.io-redis**.</span><span class="sxs-lookup"><span data-stu-id="dce95-169">So the initial connection is created using the **redis** module, then the client is passed to the **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="dce95-170">Embora o Cache Redis do Azure dê suporte a conexões seguras usando a porta 6380, os módulos usados neste exemplo não dão suporte a conexões seguras a partir de 14/7/2014.</span><span class="sxs-lookup"><span data-stu-id="dce95-170">While Azure Redis Cache supports secure connections using port 6380, the modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="dce95-171">O código acima usa o padrão, a porta não segura 6379.</span><span class="sxs-lookup"><span data-stu-id="dce95-171">The above code uses the default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="dce95-172">Salvar o **app.js** modificado</span><span class="sxs-lookup"><span data-stu-id="dce95-172">Save the modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="dce95-173">Confirme as alterações e implantar novamente</span><span class="sxs-lookup"><span data-stu-id="dce95-173">Commit changes and redeploy</span></span>
<span data-ttu-id="dce95-174">Da linha de comando no diretório **\\node\\chat**, use os seguintes comandos para confirmar as alterações e implantar novamente o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dce95-174">From the command-line in the **\\node\\chat** directory, use the following commands to commit changes and redeploy the application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="dce95-175">Assim que as alterações tenham sido enviadas por push ao servidor, você pode dimensionar seu site através de várias instâncias usando o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="dce95-175">Once the changes have been pushed to the server, you can scale your site across multiple instances by using the following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="dce95-176">Em que **#** é o número de instâncias a ser criado.</span><span class="sxs-lookup"><span data-stu-id="dce95-176">Where **#** is the number of instances to create.</span></span>

<span data-ttu-id="dce95-177">Você pode conectar seu aplicativo Web por meio de vários navegadores ou computadores para verificar que as mensagens sejam enviadas corretamente a todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="dce95-177">You can connect to your web app from multiple browsers or computers to verify that messages are correctly sent to all clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="dce95-178">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="dce95-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="dce95-179">Limites de conexão</span><span class="sxs-lookup"><span data-stu-id="dce95-179">Connection limits</span></span>
<span data-ttu-id="dce95-180">Os aplicativos Web do Azure estão disponíveis em vários SKUs, que determinam os recursos disponíveis no seu site.</span><span class="sxs-lookup"><span data-stu-id="dce95-180">Azure Web Apps is available in multiple SKUs, which determine the resources available to your site.</span></span> <span data-ttu-id="dce95-181">Isso inclui o número de conexões permitidas do WebSocket.</span><span class="sxs-lookup"><span data-stu-id="dce95-181">This includes the number of allowed WebSocket connections.</span></span> <span data-ttu-id="dce95-182">Para obter mais informações, consulte a [Página de preços de aplicativos Web].</span><span class="sxs-lookup"><span data-stu-id="dce95-182">For more information, see the [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="dce95-183">As mensagens não estão sendo enviadas usando o WebSockets</span><span class="sxs-lookup"><span data-stu-id="dce95-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="dce95-184">Se os navegadores do cliente continuam para sondagens compridas em vez de usar o WebSockets, pode ser devido ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="dce95-184">If client browsers keep falling back to long polling instead of using WebSockets, it may be because of one of the following.</span></span>

* <span data-ttu-id="dce95-185">**Tente limitar o transporte para apenas WebSockets**</span><span class="sxs-lookup"><span data-stu-id="dce95-185">**Try limiting the transport to just WebSockets**</span></span>
  
    <span data-ttu-id="dce95-186">Para que o Socket.IO use o WebSockets como o transporte de mensagens, o servidor e o cliente devem oferecer suporte ao WebSockets.</span><span class="sxs-lookup"><span data-stu-id="dce95-186">In order for Socket.IO to use WebSockets as the messaging transport, both the server and client must support WebSockets.</span></span> <span data-ttu-id="dce95-187">Se um deles não fizer isso, o Socket.IO negociará outro transporte, como a sondagem comprida.</span><span class="sxs-lookup"><span data-stu-id="dce95-187">If one or the other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="dce95-188">A lista padrão de transportes usados pelo Socket.IO é ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="dce95-188">The default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="dce95-189">Você pode forçá-la para usar apenas WebSockets adicionando o seguinte código ao arquivo **app.js**, após a linha que contenha `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="dce95-189">You can force it to only use WebSockets by adding the following code to the **app.js** file, after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="dce95-190">Observe que os navegadores antigos que não deem suporte a WebSockets não serão capazes de conectar-se ao site enquanto o código acima estiver ativo, porque ele restringe a comunicação apenas aos WebSockets.</span><span class="sxs-lookup"><span data-stu-id="dce95-190">Note that older browsers that do not support WebSockets will not be able to connect to the site while the above code is active, as it restricts communication to WebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="dce95-191">**Usar o SSL**</span><span class="sxs-lookup"><span data-stu-id="dce95-191">**Use SSL**</span></span>
  
    <span data-ttu-id="dce95-192">O WebSockets depende de alguns cabeçalhos HTTP menos usados, como o cabeçalho **Atualizar** .</span><span class="sxs-lookup"><span data-stu-id="dce95-192">WebSockets relies on some lesser used HTTP headers, such as the **Upgrade** header.</span></span> <span data-ttu-id="dce95-193">Alguns dispositivos de rede intermediários, como os proxies da web, podem remover esses cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="dce95-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="dce95-194">Para evitar esse problema, você pode estabelecer a conexão WebSocket em vez da SSL.</span><span class="sxs-lookup"><span data-stu-id="dce95-194">To avoid this problem, you can establish the WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="dce95-195">Uma maneira fácil de conseguir isso é configurar o Socket.IO para `match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="dce95-195">An easy way to accomplish this is to configure Socket.IO to `match origin protocol`.</span></span> <span data-ttu-id="dce95-196">Isso instrui ao Socket.IO para proteger a comunicação de WebSockets da mesma maneira que a solicitação HTTP/HTTPS originadora para a página web.</span><span class="sxs-lookup"><span data-stu-id="dce95-196">This instructs Socket.IO to secure WebSockets communication the same as the originating HTTP/HTTPS request for the web page.</span></span> <span data-ttu-id="dce95-197">Se um navegador usar uma URL HTTPS para visitar seu site, as comunicações WebSocket subsequentes através do Socket.IO serão protegidas sobre o SSL.</span><span class="sxs-lookup"><span data-stu-id="dce95-197">If a browser uses an HTTPS URL to visit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="dce95-198">Para modificar este exemplo para habilitar essa configuração, adicione o seguinte código ao arquivo **app.js** após a linha que contém `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="dce95-198">To modify this example to enable this configuration, add the following code to the **app.js** file after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="dce95-199">**Verificar as configurações do web.config**</span><span class="sxs-lookup"><span data-stu-id="dce95-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="dce95-200">Os aplicativos Web do Azure que hospedam aplicativos Node.js usam o arquivo **web.config** para rotear as solicitações de entrada para o aplicativo Node.js.</span><span class="sxs-lookup"><span data-stu-id="dce95-200">Azure web apps that host Node.js applications use the **web.config** file to route incoming requests to the Node.js application.</span></span> <span data-ttu-id="dce95-201">Para que o WebSockets funcione corretamente com os aplicativos Note.js, o **web.config** deve conter a seguinte entrada.</span><span class="sxs-lookup"><span data-stu-id="dce95-201">For WebSockets to function correctly with Node.js applications, the **web.config** must contain the following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="dce95-202">Isso desabilita o módulo IIS do WebSockets, que inclui sua própria implementação do WebSockets e está em conflito com módulos WebSockets específicos de Node.js, como Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="dce95-202">This disables the IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="dce95-203">Se essa linha não estiver presente ou estiver definida como `true`, isso pode ser o motivo pelo qual o transporte de WebSocket não está funcionando para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dce95-203">If this line is not present, or is set to `true`, this may be the reason that the WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="dce95-204">Normalmente, os aplicativos Node.js não incluem um arquivo **web.config** , por tanto os Sites do Azure gerarão automaticamente um para os aplicativos Node.js assim que estiverem implantados.</span><span class="sxs-lookup"><span data-stu-id="dce95-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="dce95-205">Como este arquivo é gerado automaticamente no servidor, você deve usar a URL FTP ou FTPS para seu site para visualizar esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="dce95-205">Since this file is automatically generated on the server, you must use the FTP or FTPS URL for your website to view this file.</span></span> <span data-ttu-id="dce95-206">Você pode encontrar as URLs de FTP e FTPS para seu site no portal clássico selecionando seu aplicativo Web e o link **Painel** .</span><span class="sxs-lookup"><span data-stu-id="dce95-206">You can find the FTP and FTPS URLs for your site in the classic portal by selecting your web app, and then the **Dashboard** link.</span></span> <span data-ttu-id="dce95-207">As URLs são exibidas na seção **visão rápida** .</span><span class="sxs-lookup"><span data-stu-id="dce95-207">The URLs are displayed in the **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="dce95-208">O arquivo **web.config** será gerado pelos sites do Azure apenas se seu aplicativo não fornecer um.</span><span class="sxs-lookup"><span data-stu-id="dce95-208">The **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="dce95-209">Se você fornecer um arquivo **web.config** na raiz do projeto do seu aplicativo, esse arquivo será usado por aplicativos Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce95-209">If you provide a **web.config** file in the root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="dce95-210">Se a entrada não estiver presente, ou for configurada para um valor `true`, então você deve criar um **web.config** na raiz do seu aplicativo Node.js e especificar um valor `false`.</span><span class="sxs-lookup"><span data-stu-id="dce95-210">If the entry is not present, or is set to a value of `true`, then you should create a **web.config** in the root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="dce95-211">Para referência, abaixo se encontra um **web.config** padrão para um aplicativo que usa o **app.js** como o ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="dce95-211">For reference, the below is a default **web.config** for an application that uses **app.js** as the entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used to run node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that the server.js file is a node.js web app to be handled by the iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether the incoming URL matches a physical file in the /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped to the node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using the following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes to restart the server
                * node_env: will be propagated to node as NODE_ENV environment variable
                * debuggingEnabled - controls whether the built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="dce95-212">Se seu aplicativo usar um ponto de entrada diferente de **app.js**, você deve substituir todas as ocorrências do **app.js** pelo ponto de entrada correto.</span><span class="sxs-lookup"><span data-stu-id="dce95-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with the correct entry point.</span></span> <span data-ttu-id="dce95-213">Por exemplo, substituir o **app.js** por **server.js**.</span><span class="sxs-lookup"><span data-stu-id="dce95-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="dce95-214">Se você deseja começar a usar o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, vá até [Experimentar o Serviço de Aplicativo], em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dce95-214">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="dce95-215">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="dce95-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="dce95-216">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dce95-216">Next steps</span></span>
<span data-ttu-id="dce95-217">Neste tutorial, você aprendeu como criar um aplicativo de chat hospedado em um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce95-217">In this tutorial you learned how to create a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="dce95-218">Você também pode hospedar o aplicativo como um serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce95-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="dce95-219">Para obter etapas sobre como fazer isso, consulte [Criar um aplicativo de chat do Node.js com Socket.IO em um serviço de nuvem do Azure]</span><span class="sxs-lookup"><span data-stu-id="dce95-219">For steps on how to accomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="dce95-220">Para obter mais informações, consulte também o [Centro de desenvolvedores do Node.js].</span><span class="sxs-lookup"><span data-stu-id="dce95-220">For more information, see also the [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="dce95-221">O que mudou</span><span class="sxs-lookup"><span data-stu-id="dce95-221">What's changed</span></span>
* <span data-ttu-id="dce95-222">Para obter um guia sobre a alteração dos Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes].</span><span class="sxs-lookup"><span data-stu-id="dce95-222">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

<span data-ttu-id="dce95-223">[Cache Redis do Azure]: /documentation/services/redis-cache/</span><span class="sxs-lookup"><span data-stu-id="dce95-223">[Azure Redis Cache]: /documentation/services/redis-cache/</span></span>
<span data-ttu-id="dce95-224">[Aplicativos Web do Serviço de Aplicativo]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="dce95-224">[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="dce95-225">[Página de preços de aplicativos Web]: http://go.microsoft.com/fwlink/?LinkId=511643</span><span class="sxs-lookup"><span data-stu-id="dce95-225">[Web Apps Pricing page]: http://go.microsoft.com/fwlink/?LinkId=511643</span></span>
<span data-ttu-id="dce95-226">[Criar um aplicativo de chat do Node.js com Socket.IO em um serviço de nuvem do Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="dce95-226">[Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span></span>
[Install and Configure the Azure CLI]: ../cli-install-nodejs.md
<span data-ttu-id="dce95-227">[Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="dce95-227">[Azure App Service and Its Impact on Existing Azure Services]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="dce95-228">[Centro de desenvolvedores do Node.js]: /develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="dce95-228">[Node.js Developer Center]: /develop/nodejs/</span></span>
<span data-ttu-id="dce95-229">[Experimentar o Serviço de Aplicativo]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="dce95-229">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>
<span data-ttu-id="dce95-230">[Afinidade da instância nos Sites do Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span><span class="sxs-lookup"><span data-stu-id="dce95-230">[Instance Affinity in Azure Web Sites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span></span>
<span data-ttu-id="dce95-231">[Criar um cache no Cache Redis do Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span><span class="sxs-lookup"><span data-stu-id="dce95-231">[Create a cache in Azure Redis Cache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span></span>

<span data-ttu-id="dce95-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="dce95-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span></span>
<span data-ttu-id="dce95-233">[repositório Socket.IOGitHub]: https://github.com/socketio/socket.io</span><span class="sxs-lookup"><span data-stu-id="dce95-233">[Socket.IO GitHub repository]: https://github.com/socketio/socket.io</span></span>
<span data-ttu-id="dce95-234">[versão arquivada ZIP ou GZ]: https://github.com/socketio/socket.io/releases</span><span class="sxs-lookup"><span data-stu-id="dce95-234">[ZIP or GZ archived release]: https://github.com/socketio/socket.io/releases</span></span>

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
