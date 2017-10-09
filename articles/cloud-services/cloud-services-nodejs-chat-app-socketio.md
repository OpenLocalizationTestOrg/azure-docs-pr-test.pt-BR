---
title: aplicativo de aaaNode.js usando Socket.io | Microsoft Docs
description: Saiba como socket.io toouse em um aplicativo Node. js hospedado no Azure.
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="dc3ff-103">Constrói um aplicativo de bate-papo Node.js com Socket.IO em um serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="dc3ff-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="dc3ff-104">O Socket.IO fornece comunicação em tempo real entre seu servidor e clientes do node.js.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="dc3ff-105">Este tutorial explica como hospedar um aplicativo de chat baseado em socket.IO no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="dc3ff-106">Para mais informações sobre o Socket.IO, consulte <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="dc3ff-107">É uma captura de tela do aplicativo hello concluída abaixo:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-107">A screenshot of hello completed application is below:</span></span>

![Uma janela do navegador exibindo o serviço de saudação hospedado no Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="dc3ff-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dc3ff-109">Prerequisites</span></span>
<span data-ttu-id="dc3ff-110">Certifique-se de que Olá produtos a seguir e as versões estiverem instalados toosuccessfully exemplo hello concluída neste artigo:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-110">Ensure that hello following products and versions are installed toosuccessfully complete hello example in this article:</span></span>

* <span data-ttu-id="dc3ff-111">Instalar o [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="dc3ff-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="dc3ff-112">Instale o [Node.js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="dc3ff-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="dc3ff-113">Instale o [Python versão 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="dc3ff-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="dc3ff-114">Criar um projeto de Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="dc3ff-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="dc3ff-115">Olá, etapas a seguir criam projeto de serviço de nuvem Olá que hospedará o aplicativo de Socket.IO hello.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-115">hello following steps create hello cloud service project that will host hello Socket.IO application.</span></span>

1. <span data-ttu-id="dc3ff-116">De saudação **Menu Iniciar** ou **tela inicial**, procure **do Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-116">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="dc3ff-117">Por fim, clique com botão direito em **Windows PowerShell** e selecione **Executar Como Administrador**.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Ícone PowerShell do Azure][powershell-menu]
2. <span data-ttu-id="dc3ff-119">Crie um diretório denominado **c:\\node**.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="dc3ff-120">Altere os diretórios toohello **c:\\nó** diretório</span><span class="sxs-lookup"><span data-stu-id="dc3ff-120">Change directories toohello **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="dc3ff-121">Digite hello comandos toocreate uma nova solução chamada a seguir **chatapp** e uma função de trabalho chamado **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-121">Enter hello following commands toocreate a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="dc3ff-122">Você verá Olá resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-122">You will see hello following response:</span></span>
   
    ![saída de saudação do hello new-azureservice e azurenodeworkerrolecmdlets adicionar](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a><span data-ttu-id="dc3ff-124">Baixar Olá exemplo Chat</span><span class="sxs-lookup"><span data-stu-id="dc3ff-124">Download hello Chat Example</span></span>
<span data-ttu-id="dc3ff-125">Para este projeto, nós usaremos o exemplo de chat hello de saudação [repositório Socket.IO GitHub].</span><span class="sxs-lookup"><span data-stu-id="dc3ff-125">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="dc3ff-126">Executar Olá etapas toodownload Olá exemplo a seguir e adicione-o projeto toohello que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-126">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="dc3ff-127">Criar uma cópia local do repositório de saudação usando Olá **Clone** botão.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-127">Create a local copy of hello repository by using hello **Clone** button.</span></span> <span data-ttu-id="dc3ff-128">Você também pode usar o hello **ZIP** projeto de saudação do botão toodownload.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-128">You may also use hello **ZIP** button toodownload hello project.</span></span>
   
   ![Uma janela do navegador exibindo https://github.com/LearnBoost/socket.io/tree/master/examples/chat, com o ícone de download do ZIP Olá realçado][chat-example-view]
2. <span data-ttu-id="dc3ff-130">Navegue estrutura de diretório de saudação do repositório local Olá até chegar na Olá **exemplos\\bate-papo** directory.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-130">Navigate hello directory structure of hello local repository until you arrive at hello **examples\\chat** directory.</span></span> <span data-ttu-id="dc3ff-131">Copiar conteúdo de saudação do toothe diretório **c:\\nó\\chatapp\\WorkerRole1** diretório criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-131">Copy hello contents of this directory toothe **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![Pesquisador de objetos, exibindo conteúdo de saudação do exemplos Olá\\directory bate-papo extraído do arquivo hello][chat-contents]
   
   <span data-ttu-id="dc3ff-133">itens realçados na captura de tela de saudação acima Hello são arquivos de saudação copiados da saudação **exemplos\\bate-papo** diretório</span><span class="sxs-lookup"><span data-stu-id="dc3ff-133">hello highlighted items in hello screenshot above are hello files copied from hello **examples\\chat** directory</span></span>
3. <span data-ttu-id="dc3ff-134">Em Olá **c:\\nó\\chatapp\\WorkerRole1** diretório, Olá delete **server.js** arquivo e, em seguida, renomeie Olá **app.js**arquivo muito**server.js**.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-134">In hello **C:\\node\\chatapp\\WorkerRole1** directory, delete hello **server.js** file, and then rename hello **app.js** file too**server.js**.</span></span> <span data-ttu-id="dc3ff-135">Isso remove o padrão de saudação **server.js** arquivo criado anteriormente pela Olá **Add-AzureNodeWorkerRole** cmdlet e substitui-lo com o aplicativo hello arquivo hello exemplo bate-papo.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-135">This removes hello default **server.js** file created previously by hello **Add-AzureNodeWorkerRole** cmdlet and replaces it with hello application file from hello chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="dc3ff-136">Modificar o Server.js e instalar os módulos</span><span class="sxs-lookup"><span data-stu-id="dc3ff-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="dc3ff-137">Antes de aplicativo hello teste em Olá emulador do Azure, é necessário fazer algumas modificações secundárias.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-137">Before testing hello application in hello Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="dc3ff-138">Execute Olá seguir etapas toothe server.js arquivo:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-138">Perform hello following steps toothe server.js file:</span></span>

1. <span data-ttu-id="dc3ff-139">Olá abrir **server.js** arquivo no Visual Studio ou qualquer editor de texto.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-139">Open hello **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="dc3ff-140">Localize Olá **as dependências do módulo** seção no início de saudação do Server. js e alterar Olá linha contendo **sio = require('.. //.. lib//Socket.IO')** muito**sio = require('socket.io')** conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-140">Find hello **Module dependencies** section at hello beginning of server.js and change hello line containing **sio = require('..//..//lib//socket.io')** too**sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="dc3ff-141">aplicativo de hello tooensure ouve a porta correta hello, abra server.js no bloco de notas ou seu editor favorito e, em seguida, altere a linha a seguir, substituindo **3000** com **process.env.port** conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-141">tooensure hello application listens on hello correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="dc3ff-142">Depois de salvar as alterações de saudação muito**server.js**, use Olá etapas a seguir para instalar os módulos necessários e, em seguida, testar o aplicativo hello no emulador do Azure:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-142">After saving hello changes too**server.js**, use hello following steps to install required modules, and then test hello application in the Azure emulator:</span></span>

1. <span data-ttu-id="dc3ff-143">Usando **Azure PowerShell**, altere os diretórios toohello **c:\\nó\\chatapp\\WorkerRole1** directory e uso Olá Olá de tooinstall de comando a seguir módulos necessários para este aplicativo:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-143">Using **Azure PowerShell**, change directories toohello **C:\\node\\chatapp\\WorkerRole1** directory and use hello following command tooinstall hello modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="dc3ff-144">Isso irá instalar módulos Olá listados no arquivo de Package. JSON hello.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-144">This will install hello modules listed in hello package.json file.</span></span> <span data-ttu-id="dc3ff-145">Após a conclusão do comando hello, você deve ver o seguinte de toothe semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-145">After hello command completes, you should see output similar toothe following:</span></span>
   
   ![comando de instalação de saída de saudação do npm Olá][The-output-of-the-npm-install-command]
2. <span data-ttu-id="dc3ff-147">Como este exemplo foi originalmente a parte da saudação repositório Socket.IO GitHub e referenciado diretamente a biblioteca de Socket.IO Olá pelo caminho relativo, Socket.IO não foi referenciado no arquivo de Package. JSON hello, portanto, deverá instalá-lo, emitindo o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-147">Since this example was originally a part of hello Socket.IO GitHub repository, and directly referenced hello Socket.IO library by relative path, Socket.IO was not referenced in hello package.json file, so we must install it by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="dc3ff-148">Testar e implantar</span><span class="sxs-lookup"><span data-stu-id="dc3ff-148">Test and Deploy</span></span>
1. <span data-ttu-id="dc3ff-149">Inicie o emulador Olá emitindo o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-149">Launch hello emulator by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="dc3ff-150">Se você encontrar problemas ao iniciar o emulador, por exemplo: Start-AzureEmulator: ocorreu um erro inesperado.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="dc3ff-151">Detalhes: Encontrado um objeto de comunicação de saudação do erro inesperado, ServiceChannel, não é usado para comunicação porque está no estado com falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-151">Details: Encountered an unexpected error hello communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in hello Faulted state.</span></span>
   
      <span data-ttu-id="dc3ff-152">reinstale o AzureAuthoringTools v 2.7.1 e o AzureComputeEmulator v 2.7 – Verifique se a versão corresponde.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="dc3ff-153">Abra um navegador e navegue muito**http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-153">Open a browser and navigate too**http://127.0.0.1**.</span></span>
3. <span data-ttu-id="dc3ff-154">Quando abre a janela do navegador hello, insira um apelido e, em seguida, pressione enter.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-154">When hello browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="dc3ff-155">Isso permitirá que você toopost mensagens como um apelido específico.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-155">This will allow you toopost messages as a specific nickname.</span></span> <span data-ttu-id="dc3ff-156">funcionalidade de multiusuário tootest, abra janelas adicionais do navegador usando a mesma URL e insira apelidos diferentes.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-156">tootest multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![Duas janelas de navegador exibindo mensagens de chat do Usuário1 e do Usuário2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="dc3ff-158">Após a aplicação de saudação do teste, pare emulador Olá emitindo o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-158">After testing hello application, stop hello emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="dc3ff-159">tooAzure de aplicativo hello toodeploy, use o **AzureServiceProject publicar** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-159">toodeploy hello application tooAzure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="dc3ff-160">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dc3ff-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="dc3ff-161">Ser um nome exclusivo de toouse-se de que, caso contrário, Olá publicar processo falhará.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-161">Be sure toouse a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="dc3ff-162">Após a implantação de hello, navegador Olá será aberto e navegue serviço toohello implantado.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-162">After hello deployment has completed, hello browser will open and navigate toohello deployed service.</span></span>
   > 
   > <span data-ttu-id="dc3ff-163">Se você receber um erro indicando que Olá fornecidos nome de assinatura não existe no hello importado perfil de publicação, você deve baixar e importar o perfil de publicação Olá para sua assinatura antes de implantar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-163">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="dc3ff-164">Consulte Olá **Implantando Olá aplicativo tooAzure** seção [compilar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="dc3ff-164">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Uma janela do navegador exibindo o serviço de saudação hospedado no Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="dc3ff-166">Se você receber um erro indicando que Olá fornecidos nome de assinatura não existe no hello importado perfil de publicação, você deve baixar e importar o perfil de publicação Olá para sua assinatura antes de implantar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-166">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="dc3ff-167">Consulte Olá **Implantando Olá aplicativo tooAzure** seção [compilar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="dc3ff-167">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="dc3ff-168">Seu aplicativo agora está sendo executado no Azure e pode retransmitir mensagens de chat entre diferentes clientes usando o Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="dc3ff-169">Para simplificar, este exemplo é limitado toochatting entre toohello de usuários conectados mesma instância.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-169">For simplicity, this sample is limited toochatting between users connected toohello same instance.</span></span> <span data-ttu-id="dc3ff-170">Isso significa que se o serviço de nuvem Olá cria duas instâncias de função de trabalho, os usuários só poderão toochat com outros usuários conectados toohello mesma instância de função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-170">This means that if hello cloud service creates two worker role instances, users will only be able toochat with others connected toohello same worker role instance.</span></span> <span data-ttu-id="dc3ff-171">tooscale Olá aplicativo toowork com várias instâncias de função, você pode usar uma tecnologia como armazenar estado de barramento de serviço tooshare Olá Socket.IO entre instâncias.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-171">tooscale hello application toowork with multiple role instances, you could use a technology like Service Bus tooshare hello Socket.IO store state across instances.</span></span> <span data-ttu-id="dc3ff-172">Para obter exemplos, consulte exemplos do uso de tópicos e filas do barramento de serviço do hello em Olá [SDK do Azure para o repositório GitHub Node. js](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="dc3ff-172">For examples, see hello Service Bus Queues and Topics usage samples in hello [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="dc3ff-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc3ff-173">Next steps</span></span>
<span data-ttu-id="dc3ff-174">Neste tutorial, você aprendeu como toocreate um aplicativo de chat básica hospedados em um serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc3ff-174">In this tutorial you learned how toocreate a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="dc3ff-175">toolearn como toohost esse aplicativo em um site do Azure, consulte [criar um Site do Azure de um aplicativo de Chat do Node. js com Socket.IO][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="dc3ff-175">toolearn how toohost this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="dc3ff-176">Para obter mais informações, consulte também Olá [Node. js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="dc3ff-176">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[repositório Socket.IO GitHub]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


