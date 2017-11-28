---
title: "aaaCreate um aplicativo de chat Node. js com Socket.IO no serviço de aplicativo do Azure"
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
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="59110-103">Criar um aplicativo de chat do Node.js com Socket.IO no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="59110-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="59110-104">Socket.IO fornece uma comunicação em tempo real entre o seu servidor node.js e clientes usando WebSockets.</span><span class="sxs-lookup"><span data-stu-id="59110-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="59110-105">Ele também dá suporte a transportes de fallback tooother (por exemplo, a sondagem longa) que funcionam com navegadores mais antigos.</span><span class="sxs-lookup"><span data-stu-id="59110-105">It also supports fallback tooother transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="59110-106">Este tutorial orientará hospedando um aplicativo de bate-papo Socket.IO com base em como um aplicativo web do Azure e mostram como tooscale hello usando o aplicativo [Cache Redis do Azure].</span><span class="sxs-lookup"><span data-stu-id="59110-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how tooscale hello application using [Azure Redis Cache].</span></span> <span data-ttu-id="59110-107">Para mais informações sobre o Socket.IO, consulte <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="59110-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="59110-108">Olá procedimentos nessa tarefa aplicam-se muito[aplicativo de serviço Web aplicativos]; para serviços de nuvem, consulte [criar um aplicativo de Chat do Node. js com Socket.IO em um serviço de nuvem do Azure].</span><span class="sxs-lookup"><span data-stu-id="59110-108">hello procedures in this task apply too[App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-hello-chat-example"></a><span data-ttu-id="59110-109">Baixe o exemplo de chat hello</span><span class="sxs-lookup"><span data-stu-id="59110-109">Download hello chat example</span></span>
<span data-ttu-id="59110-110">Para este projeto, nós usaremos o exemplo de chat hello de saudação [repositório Socket.IO GitHub].</span><span class="sxs-lookup"><span data-stu-id="59110-110">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="59110-111">Executar Olá etapas toodownload Olá exemplo a seguir e adicione-o projeto toohello que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="59110-111">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="59110-112">Baixar um [ZIP ou GZ arquivado versão] do projeto de Socket.IO hello (versão 1.3.5 foi usado para este documento)</span><span class="sxs-lookup"><span data-stu-id="59110-112">Download a [ZIP or GZ archived release] of hello Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="59110-113">Extrair Olá Olá arquivamento e cópia **exemplos\\bate-papo** novo local do diretório tooa.</span><span class="sxs-lookup"><span data-stu-id="59110-113">Extract hello archive and copy hello **examples\\chat** directory tooa new location.</span></span> <span data-ttu-id="59110-114">Por exemplo, **\\node\\chat**.</span><span class="sxs-lookup"><span data-stu-id="59110-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="59110-115">Modificar o app.js e instalar os módulos</span><span class="sxs-lookup"><span data-stu-id="59110-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="59110-116">Renomear Olá **js** arquivo muito**app.js**.</span><span class="sxs-lookup"><span data-stu-id="59110-116">Rename hello **index.js** file too**app.js**.</span></span> <span data-ttu-id="59110-117">Isso permite que toodetect do Azure que se trata de um aplicativo Node. js.</span><span class="sxs-lookup"><span data-stu-id="59110-117">This allows Azure toodetect that this is a Node.js application.</span></span>
2. <span data-ttu-id="59110-118">Olá abrir **app.js** em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="59110-118">Open hello **app.js** file in a text editor.</span></span> <span data-ttu-id="59110-119">Alteração Olá linha contendo `var io = require('../..')(server);` conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="59110-119">Change hello line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="59110-120">Olá abrir **Package. JSON** de arquivos e adicionar um toosocket.io de referência em `dependencies`, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="59110-120">Open hello **package.json** file and add a reference toosocket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="59110-121">Saudação de linha de comando, alterar toohello  **\\nó\\bate-papo** directory e uso tooinstall Olá módulos npm exigidos por este aplicativo:</span><span class="sxs-lookup"><span data-stu-id="59110-121">From hello command-line, change toohello **\\node\\chat** directory and use npm tooinstall hello modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="59110-122">Isso irá instalar os módulos de saudação em uma subpasta chamada **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="59110-122">This will install hello modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="59110-123">Criar um aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="59110-123">Create an Azure Web App</span></span>
<span data-ttu-id="59110-124">Siga essas etapas toocreate um aplicativo web do Azure, habilitar a publicação de Git e, em seguida, habilitar o suporte de WebSocket do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="59110-124">Follow these steps toocreate an Azure web app, enable Git publishing, and then enable WebSocket support for hello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="59110-125">toocomplete neste tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="59110-125">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="59110-126">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="59110-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="59110-127">Para obter detalhes, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Avaliação gratuita do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="59110-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="59110-128">Instalar hello Azure Interface de linha de comando (CLI do Azure) e conecte-se tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="59110-128">Install hello Azure Command-Line Interface (Azure CLI) and connect tooyour Azure subscription.</span></span> <span data-ttu-id="59110-129">Consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="59110-129">See [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="59110-130">Se esse for o primeiro tempo configurando um repositório no Azure, você precisa ter credenciais de logon de toocreate.</span><span class="sxs-lookup"><span data-stu-id="59110-130">If this is your first time setting up a repository in Azure, you need toocreate login credentials.</span></span> <span data-ttu-id="59110-131">Em Olá CLI do Azure, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="59110-131">From hello Azure CLI, enter hello following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="59110-132">Alterar toohello  **\\node\chat** directory e uso a seguir Olá comando toocreate um novo aplicativo web do Azure e um repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="59110-132">Change toohello **\\node\chat** directory and use hello following command toocreate a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="59110-133">Esse comando também cria um repositório remoto do Git chamado 'azure'.</span><span class="sxs-lookup"><span data-stu-id="59110-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="59110-134">Você deve substituir 'mysitename' por um nome exclusivo para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="59110-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="59110-135">Confirme Olá existente arquivos toohello repositório local usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="59110-135">Commit hello existing files toohello local repository by using hello following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="59110-136">Enviar por push de repositório de aplicativos Web do Azure Olá arquivos toohello com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="59110-136">Push hello files toohello Azure Web Apps repository with hello following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="59110-137">Quando solicitado, insira suas credenciais da etapa 2.</span><span class="sxs-lookup"><span data-stu-id="59110-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="59110-138">Você receberá mensagens de status, como os módulos são importados no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="59110-138">You will receive status messages as modules are imported on hello server.</span></span> <span data-ttu-id="59110-139">Depois que esse processo for concluído, o aplicativo hello será hospedado em seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="59110-139">Once this process has completed, hello application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="59110-140">Durante a instalação do módulo, você pode observar erros que ' hello... projeto importado não foi encontrado '.</span><span class="sxs-lookup"><span data-stu-id="59110-140">During module installation, you may notice errors that 'hello imported project ... was not found'.</span></span> <span data-ttu-id="59110-141">Isso podem ser ignorados.</span><span class="sxs-lookup"><span data-stu-id="59110-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="59110-142">Socket.IO usa o WebSocket, que não é habilitado por padrão no Azure.</span><span class="sxs-lookup"><span data-stu-id="59110-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="59110-143">soquetes da web de tooenable, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="59110-143">tooenable web sockets, use hello following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="59110-144">Se solicitado, insira o nome de saudação do aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="59110-144">If prompted, enter hello name of hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="59110-145">Olá será de comando 'site do azure set -w' funcionam somente com a versão 0.7.4 ou posterior do hello Interface de linha de comando do Azure.</span><span class="sxs-lookup"><span data-stu-id="59110-145">hello 'azure site set -w' command will work only with version 0.7.4 or higher of hello Azure Command-Line Interface.</span></span> <span data-ttu-id="59110-146">Você também pode habilitar o suporte para WebSocket usando Olá [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="59110-146">You can also enable WebSocket support using hello [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="59110-147">usando o WebSocket tooenable Olá Portal do Azure, clique em aplicativo web de saudação da folha de aplicativos Web de saudação do **todas as configurações** > **configurações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="59110-147">tooenable WebSockets using hello Azure Portal, click hello web app from hello Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="59110-148">Em **Web Sockets**, clique em **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="59110-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="59110-149">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="59110-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="59110-150">tooview Olá web app no seguinte de saudação do Azure, use comando toolaunch seu navegador da web e navegue toohello hospedado web app:</span><span class="sxs-lookup"><span data-stu-id="59110-150">tooview hello web app on Azure, use hello following command toolaunch your web browser and navigate toohello hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="59110-151">Seu aplicativo agora está sendo executado no Azure e pode retransmitir mensagens de chat entre diferentes clientes usando o Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="59110-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="59110-152">Expansão</span><span class="sxs-lookup"><span data-stu-id="59110-152">Scale out</span></span>
<span data-ttu-id="59110-153">Aplicativos Socket.IO podem ser expandidos usando um **adaptador** toodistribute mensagens e eventos entre várias instâncias do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59110-153">Socket.IO applications can be scaled out by using an **adapter** toodistribute messages and events between multiple application instances.</span></span> <span data-ttu-id="59110-154">Embora haja várias adaptadores disponíveis, Olá [redis socket.io] adaptador pode ser usado com o recurso de Cache Redis do Azure Olá facilmente.</span><span class="sxs-lookup"><span data-stu-id="59110-154">While there are several adapters available, hello [socket.io-redis] adapter can be easily used with hello Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="59110-155">Um requisito adicional para expandir uma solução Socket.IO é dar suporte a sessões complexas.</span><span class="sxs-lookup"><span data-stu-id="59110-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="59110-156">As sessões complexas são habilitadas por padrão para Aplicativos Web do Azure por meio do Request Routing do Azure.</span><span class="sxs-lookup"><span data-stu-id="59110-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="59110-157">Para obter mais informações, consulte [Afinidade da instância nos Sites do Azure].</span><span class="sxs-lookup"><span data-stu-id="59110-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="59110-158">Criar um cache Redis</span><span class="sxs-lookup"><span data-stu-id="59110-158">Create a Redis cache</span></span>
<span data-ttu-id="59110-159">Execute as etapas de saudação em [criar um cache no Cache Redis do Azure] toocreate um novo cache.</span><span class="sxs-lookup"><span data-stu-id="59110-159">Perform hello steps in [Create a cache in Azure Redis Cache] toocreate a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="59110-160">Salvar Olá **nome de Host** e **chave primária** para seu cache, como eles serão necessários no hello próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="59110-160">Save hello **Host name** and **Primary key** for your cache, as these will be needed in hello next steps.</span></span>
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a><span data-ttu-id="59110-161">Adicionar redis hello e módulos socket.io redis</span><span class="sxs-lookup"><span data-stu-id="59110-161">Add hello redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="59110-162">De uma linha de comando, altere toohello  **\\nó\\bate-papo** saudação de diretório e usar comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="59110-162">From a command-line, change toohello **\\node\\chat** directory and use hello following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="59110-163">Olá versões especificadas neste comando são Olá usados ao testar este artigo.</span><span class="sxs-lookup"><span data-stu-id="59110-163">hello versions specified in this command are hello versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="59110-164">Modificar Olá **app.js** linhas seguintes do arquivo tooadd Olá imediatamente após`var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="59110-164">Modify hello **app.js** file tooadd hello following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="59110-165">Substituir **redishostname** e **rediskey** com nome de host de saudação e a chave para o cache Redis.</span><span class="sxs-lookup"><span data-stu-id="59110-165">Replace **redishostname** and **rediskey** with hello host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="59110-166">Isso criará uma publicação e assinar toohello cliente Redis cache criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="59110-166">This will create a publish and subscribe client toohello Redis cache created previously.</span></span> <span data-ttu-id="59110-167">clientes Hello são usados com hello adaptador tooconfigure cache Redis do Socket.IO toouse Olá para transmitir mensagens e eventos entre instâncias do seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="59110-167">hello clients are then used with hello adapter tooconfigure Socket.IO toouse hello Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="59110-168">Durante a saudação **redis socket.io** adaptador pode se comunicar diretamente tooRedis, versão atual do hello não dá suporte à autenticação de saudação exigida pelo cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="59110-168">While hello **socket.io-redis** adapter can communicate directly tooRedis, hello current version does not support hello authentication required by Azure Redis cache.</span></span> <span data-ttu-id="59110-169">Para a conexão inicial Olá é criado usando Olá **redis** módulo, o cliente de hello, em seguida, é passada toohello **redis socket.io** adaptador.</span><span class="sxs-lookup"><span data-stu-id="59110-169">So hello initial connection is created using hello **redis** module, then hello client is passed toohello **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="59110-170">Enquanto o Cache Redis do Azure dá suporte a conexões seguras usando a porta 6380, módulos de saudação usados neste exemplo não dão suporte a conexões seguras a partir de 14/7/2014.</span><span class="sxs-lookup"><span data-stu-id="59110-170">While Azure Redis Cache supports secure connections using port 6380, hello modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="59110-171">Olá acima código usa saudação padrão, porta não segura de 6379.</span><span class="sxs-lookup"><span data-stu-id="59110-171">hello above code uses hello default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="59110-172">Salvar Olá modificado **app.js**</span><span class="sxs-lookup"><span data-stu-id="59110-172">Save hello modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="59110-173">Confirme as alterações e implantar novamente</span><span class="sxs-lookup"><span data-stu-id="59110-173">Commit changes and redeploy</span></span>
<span data-ttu-id="59110-174">De saudação de linha de comando no hello  **\\nó\\bate-papo** diretório, use Olá comandos toocommit alterações a seguir e reimplantar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="59110-174">From hello command-line in hello **\\node\\chat** directory, use hello following commands toocommit changes and redeploy hello application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="59110-175">Depois que alterações Olá foram empurrados para servidor toohello, você pode dimensionar seu site em várias instâncias usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="59110-175">Once hello changes have been pushed toohello server, you can scale your site across multiple instances by using hello following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="59110-176">Onde  **#**  é Olá número de instâncias toocreate.</span><span class="sxs-lookup"><span data-stu-id="59110-176">Where **#** is hello number of instances toocreate.</span></span>

<span data-ttu-id="59110-177">Você pode conectar o aplicativo da web de tooyour de tooverify vários navegadores ou computadores que são enviadas corretamente tooall clientes.</span><span class="sxs-lookup"><span data-stu-id="59110-177">You can connect tooyour web app from multiple browsers or computers tooverify that messages are correctly sent tooall clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="59110-178">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="59110-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="59110-179">Limites de conexão</span><span class="sxs-lookup"><span data-stu-id="59110-179">Connection limits</span></span>
<span data-ttu-id="59110-180">Os aplicativos Web do Azure está disponível em várias SKUs, que determinam o site do hello recursos tooyour disponíveis.</span><span class="sxs-lookup"><span data-stu-id="59110-180">Azure Web Apps is available in multiple SKUs, which determine hello resources available tooyour site.</span></span> <span data-ttu-id="59110-181">Isso inclui o número de saudação do WebSocket de conexões permitidas.</span><span class="sxs-lookup"><span data-stu-id="59110-181">This includes hello number of allowed WebSocket connections.</span></span> <span data-ttu-id="59110-182">Para obter mais informações, consulte Olá [página de preços de aplicativos Web].</span><span class="sxs-lookup"><span data-stu-id="59110-182">For more information, see hello [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="59110-183">As mensagens não estão sendo enviadas usando o WebSockets</span><span class="sxs-lookup"><span data-stu-id="59110-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="59110-184">Se navegadores clientes mantenham voltando toolong sondagem em vez de usar o WebSocket, pode ser devido a um dos seguintes hello.</span><span class="sxs-lookup"><span data-stu-id="59110-184">If client browsers keep falling back toolong polling instead of using WebSockets, it may be because of one of hello following.</span></span>

* <span data-ttu-id="59110-185">**Tente limitar Olá transporte toojust WebSockets**</span><span class="sxs-lookup"><span data-stu-id="59110-185">**Try limiting hello transport toojust WebSockets**</span></span>
  
    <span data-ttu-id="59110-186">A fim de toouse Socket.IO WebSockets como transporte de mensagens de saudação, cliente e servidor de saudação devem oferecer suporte a WebSockets.</span><span class="sxs-lookup"><span data-stu-id="59110-186">In order for Socket.IO toouse WebSockets as hello messaging transport, both hello server and client must support WebSockets.</span></span> <span data-ttu-id="59110-187">Se um ou Olá outros não, Socket.IO negociará outro transporte, como sondagem longa.</span><span class="sxs-lookup"><span data-stu-id="59110-187">If one or hello other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="59110-188">a lista de transportes usados por Socket.IO padrão Olá é ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="59110-188">hello default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="59110-189">Você pode forçar o uso de tooonly WebSockets adicionando Olá toohello de código a seguir **app.js** arquivo após Olá linha contendo `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="59110-189">You can force it tooonly use WebSockets by adding hello following code toohello **app.js** file, after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="59110-190">Observe que navegadores mais antigos que não oferecem suporte a WebSockets não será capaz de tooconnect toohello site enquanto Olá acima código está ativa, pois ela restringe a comunicação tooWebSockets somente.</span><span class="sxs-lookup"><span data-stu-id="59110-190">Note that older browsers that do not support WebSockets will not be able tooconnect toohello site while hello above code is active, as it restricts communication tooWebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="59110-191">**Usar o SSL**</span><span class="sxs-lookup"><span data-stu-id="59110-191">**Use SSL**</span></span>
  
    <span data-ttu-id="59110-192">WebSockets depende de alguns menor cabeçalhos HTTP usados, como Olá **atualização** cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="59110-192">WebSockets relies on some lesser used HTTP headers, such as hello **Upgrade** header.</span></span> <span data-ttu-id="59110-193">Alguns dispositivos de rede intermediários, como os proxies da web, podem remover esses cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="59110-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="59110-194">tooavoid esse problema, você pode estabelecer uma conexão de WebSocket Olá sobre SSL.</span><span class="sxs-lookup"><span data-stu-id="59110-194">tooavoid this problem, you can establish hello WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="59110-195">Uma maneira fácil tooaccomplish isso é tooconfigure Socket.IO muito`match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="59110-195">An easy way tooaccomplish this is tooconfigure Socket.IO too`match origin protocol`.</span></span> <span data-ttu-id="59110-196">Isso instrui igual Olá HTTP/HTTPS de origem de solicitação para página da web de Olá Olá de comunicação Socket.IO toosecure WebSocket.</span><span class="sxs-lookup"><span data-stu-id="59110-196">This instructs Socket.IO toosecure WebSockets communication hello same as hello originating HTTP/HTTPS request for hello web page.</span></span> <span data-ttu-id="59110-197">Se o navegador usa uma URL HTTPS toovisit seu site, comunicações subsequentes do WebSocket por meio de Socket.IO serão protegidas por SSL.</span><span class="sxs-lookup"><span data-stu-id="59110-197">If a browser uses an HTTPS URL toovisit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="59110-198">toomodify tooenable esse exemplo nessa configuração, adicione Olá toohello de código a seguir **app.js** arquivo após Olá linha contendo `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="59110-198">toomodify this example tooenable this configuration, add hello following code toohello **app.js** file after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="59110-199">**Verificar as configurações do web.config**</span><span class="sxs-lookup"><span data-stu-id="59110-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="59110-200">Aplicativos web do Azure que hospedam aplicativos Node. js usam Olá **Web. config** arquivo tooroute entrada solicitações toohello Node. js aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59110-200">Azure web apps that host Node.js applications use hello **web.config** file tooroute incoming requests toohello Node.js application.</span></span> <span data-ttu-id="59110-201">Para toofunction WebSockets corretamente com aplicativos Node. js, Olá **Web. config** deve conter a seguinte entrada de saudação.</span><span class="sxs-lookup"><span data-stu-id="59110-201">For WebSockets toofunction correctly with Node.js applications, hello **web.config** must contain hello following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="59110-202">Isso desabilita o módulo de WebSockets do IIS hello, que inclui sua própria implementação do WebSocket e está em conflito com módulos específicos de WebSocket Node. js como Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="59110-202">This disables hello IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="59110-203">Se essa linha não está presente ou está definida muito`true`, isso pode ser o motivo de saudação que transporte de WebSocket Olá não está funcionando para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59110-203">If this line is not present, or is set too`true`, this may be hello reason that hello WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="59110-204">Normalmente, os aplicativos Node.js não incluem um arquivo **web.config** , por tanto os Sites do Azure gerarão automaticamente um para os aplicativos Node.js assim que estiverem implantados.</span><span class="sxs-lookup"><span data-stu-id="59110-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="59110-205">Como esse arquivo é gerado automaticamente no servidor de saudação, você deve usar Olá FTP ou FTPS URL para seu site tooview esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="59110-205">Since this file is automatically generated on hello server, you must use hello FTP or FTPS URL for your website tooview this file.</span></span> <span data-ttu-id="59110-206">Você pode encontrar hello FTP e FTPS URLs para seu site no portal clássico Olá selecionando seu aplicativo web e, em seguida, Olá **painel** link.</span><span class="sxs-lookup"><span data-stu-id="59110-206">You can find hello FTP and FTPS URLs for your site in hello classic portal by selecting your web app, and then hello **Dashboard** link.</span></span> <span data-ttu-id="59110-207">Olá URLs são exibidas no hello **visão rápida** seção.</span><span class="sxs-lookup"><span data-stu-id="59110-207">hello URLs are displayed in hello **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="59110-208">Olá **Web. config** arquivo é gerado apenas por sites do Azure se seu aplicativo não fornecer um.</span><span class="sxs-lookup"><span data-stu-id="59110-208">hello **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="59110-209">Se você fornecer um **Web. config** arquivo na raiz de saudação do seu projeto de aplicativo, ele será usado por aplicativos Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="59110-209">If you provide a **web.config** file in hello root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="59110-210">Se a entrada hello não está presente ou estiver definida como valor de tooa de `true`, em seguida, você deve criar um **Web. config** Olá raiz do seu aplicativo Node. js e especifique um valor de `false`.</span><span class="sxs-lookup"><span data-stu-id="59110-210">If hello entry is not present, or is set tooa value of `true`, then you should create a **web.config** in hello root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="59110-211">Para referência, Olá abaixo é um padrão **Web. config** para um aplicativo que usa **app.js** como ponto de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="59110-211">For reference, hello below is a default **web.config** for an application that uses **app.js** as hello entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="59110-212">Se seu aplicativo usa um ponto de entrada diferente de **app.js**, você deve substituir todas as ocorrências de **app.js** com hello corrigir o ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="59110-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with hello correct entry point.</span></span> <span data-ttu-id="59110-213">Por exemplo, substituir o **app.js** por **server.js**.</span><span class="sxs-lookup"><span data-stu-id="59110-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="59110-214">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo], onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="59110-214">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="59110-215">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="59110-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="59110-216">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="59110-216">Next steps</span></span>
<span data-ttu-id="59110-217">Neste tutorial, você aprendeu como toocreate um aplicativo de chat hospedados em um aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="59110-217">In this tutorial you learned how toocreate a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="59110-218">Você também pode hospedar o aplicativo como um serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="59110-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="59110-219">Para obter etapas sobre como tooaccomplish isso, consulte [criar um aplicativo de Chat do Node. js com Socket.IO em um serviço de nuvem do Azure].</span><span class="sxs-lookup"><span data-stu-id="59110-219">For steps on how tooaccomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="59110-220">Para obter mais informações, consulte também Olá [Node. js Developer Center].</span><span class="sxs-lookup"><span data-stu-id="59110-220">For more information, see also hello [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="59110-221">O que mudou</span><span class="sxs-lookup"><span data-stu-id="59110-221">What's changed</span></span>
* <span data-ttu-id="59110-222">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente].</span><span class="sxs-lookup"><span data-stu-id="59110-222">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

[Cache Redis do Azure]: /documentation/services/redis-cache/
[aplicativo de serviço Web aplicativos]: http://go.microsoft.com/fwlink/?LinkId=529714
[página de preços de aplicativos Web]: http://go.microsoft.com/fwlink/?LinkId=511643
[criar um aplicativo de Chat do Node. js com Socket.IO em um serviço de nuvem do Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente]: http://go.microsoft.com/fwlink/?LinkId=529714
[Node. js Developer Center]: /develop/nodejs/
[tente do serviço de aplicativo]: https://azure.microsoft.com/try/app-service/
[Afinidade da instância nos Sites do Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[criar um cache no Cache Redis do Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[redis socket.io]: https://github.com/socketio/socket.io-redis
[repositório Socket.IO GitHub]: https://github.com/socketio/socket.io
[ZIP ou GZ arquivado versão]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
