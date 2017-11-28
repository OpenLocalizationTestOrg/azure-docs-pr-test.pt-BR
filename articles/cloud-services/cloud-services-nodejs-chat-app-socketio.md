---
title: Aplicativo Node.js usando Socket.io | Microsoft Docs
description: Saiba como usar socket.io em um aplicativo node.js hospedado no Azure.
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
ms.openlocfilehash: a85d4348a13b79b5b7542362de9956aa3398375a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="843ab-103">Constrói um aplicativo de bate-papo Node.js com Socket.IO em um serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="843ab-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="843ab-104">O Socket.IO fornece comunicação em tempo real entre seu servidor e clientes do node.js.</span><span class="sxs-lookup"><span data-stu-id="843ab-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="843ab-105">Este tutorial explica como hospedar um aplicativo de chat baseado em socket.IO no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="843ab-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="843ab-106">Para mais informações sobre o Socket.IO, consulte <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="843ab-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="843ab-107">Abaixo, uma captura de tela do aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="843ab-107">A screenshot of the completed application is below:</span></span>

![Uma janela do navegador exibindo o serviço hospedado no Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="843ab-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="843ab-109">Prerequisites</span></span>
<span data-ttu-id="843ab-110">Verifique se os seguintes produtos e versões estão instalados para concluir com êxito o exemplo deste artigo:</span><span class="sxs-lookup"><span data-stu-id="843ab-110">Ensure that the following products and versions are installed to successfully complete the example in this article:</span></span>

* <span data-ttu-id="843ab-111">Instalar o [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="843ab-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="843ab-112">Instale o [Node.js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="843ab-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="843ab-113">Instale o [Python versão 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="843ab-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="843ab-114">Criar um projeto de Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="843ab-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="843ab-115">As etapas a seguir criam o projeto de serviço de nuvem que hospedará o aplicativo Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="843ab-115">The following steps create the cloud service project that will host the Socket.IO application.</span></span>

1. <span data-ttu-id="843ab-116">Do **Menu Iniciar** ou na **Tela Iniciar**, procure **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="843ab-116">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="843ab-117">Por fim, clique com botão direito em **Windows PowerShell** e selecione **Executar Como Administrador**.</span><span class="sxs-lookup"><span data-stu-id="843ab-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Ícone PowerShell do Azure][powershell-menu]
2. <span data-ttu-id="843ab-119">Crie um diretório denominado **c:\\node**.</span><span class="sxs-lookup"><span data-stu-id="843ab-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="843ab-120">Altere os diretórios para o diretório **c:\\node**</span><span class="sxs-lookup"><span data-stu-id="843ab-120">Change directories to the **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="843ab-121">Digite os seguintes comandos para criar uma nova solução denominada **chatapp** e uma função de trabalho denominada **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="843ab-121">Enter the following commands to create a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="843ab-122">Você verá a seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="843ab-122">You will see the following response:</span></span>
   
    ![Saída de new-azureservice e add-azurenodeworkerrolecmdlets](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-the-chat-example"></a><span data-ttu-id="843ab-124">Baixar o exemplo de chat</span><span class="sxs-lookup"><span data-stu-id="843ab-124">Download the Chat Example</span></span>
<span data-ttu-id="843ab-125">Para este projeto, usaremos o exemplo de chat do repositório [Socket.IO GitHub].</span><span class="sxs-lookup"><span data-stu-id="843ab-125">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="843ab-126">Execute as seguintes etapas para baixar o exemplo e adicioná-lo ao projeto que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="843ab-126">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="843ab-127">Crie uma cópia local do repositório usando o botão **Clonar** .</span><span class="sxs-lookup"><span data-stu-id="843ab-127">Create a local copy of the repository by using the **Clone** button.</span></span> <span data-ttu-id="843ab-128">Você também pode usar o botão **ZIP** para baixar o projeto.</span><span class="sxs-lookup"><span data-stu-id="843ab-128">You may also use the **ZIP** button to download the project.</span></span>
   
   ![Uma janela do navegador exibindo https://github.com/LearnBoost/socket.io/tree/master/examples/chat, com o ícone de download ZIP realçado][chat-example-view]
2. <span data-ttu-id="843ab-130">Navegue pela estrutura de diretório do repositório local até chegar no diretório **examples\\chat**.</span><span class="sxs-lookup"><span data-stu-id="843ab-130">Navigate the directory structure of the local repository until you arrive at the **examples\\chat** directory.</span></span> <span data-ttu-id="843ab-131">Copie o conteúdo desse diretório para o diretório **C:\\node\\chatapp\\WorkerRole1** criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="843ab-131">Copy the contents of this directory to the **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![Explorer, exibindo o conteúdo do diretório examples\\chat extraído do armazenamento][chat-contents]
   
   <span data-ttu-id="843ab-133">Os itens destacadas na captura de tela acima são os arquivos copiados do diretório **examples\\chat**</span><span class="sxs-lookup"><span data-stu-id="843ab-133">The highlighted items in the screenshot above are the files copied from the **examples\\chat** directory</span></span>
3. <span data-ttu-id="843ab-134">No diretório **C:\\node\\chatapp\\WorkerRole1**, exclua o arquivo **server.js**, em seguida, renomeie o arquivo **app.js** como **server.js**.</span><span class="sxs-lookup"><span data-stu-id="843ab-134">In the **C:\\node\\chatapp\\WorkerRole1** directory, delete the **server.js** file, and then rename the **app.js** file to **server.js**.</span></span> <span data-ttu-id="843ab-135">Isso remove o arquivo **server.js** padrão criado anteriormente com o cmdlet **Add-AzureNodeWorkerRole** e o substitui pelo arquivo do aplicativo no exemplo de chat.</span><span class="sxs-lookup"><span data-stu-id="843ab-135">This removes the default **server.js** file created previously by the **Add-AzureNodeWorkerRole** cmdlet and replaces it with the application file from the chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="843ab-136">Modificar o Server.js e instalar os módulos</span><span class="sxs-lookup"><span data-stu-id="843ab-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="843ab-137">Antes de testar o aplicativo no emulador do Microsoft Azure, é necessário fazer algumas modificações secundárias.</span><span class="sxs-lookup"><span data-stu-id="843ab-137">Before testing the application in the Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="843ab-138">Execute as seguintes etapas para o arquivo server.js:</span><span class="sxs-lookup"><span data-stu-id="843ab-138">Perform the following steps to the server.js file:</span></span>

1. <span data-ttu-id="843ab-139">Abra o arquivo **server.js** no Visual Studio ou em qualquer editor de texto.</span><span class="sxs-lookup"><span data-stu-id="843ab-139">Open the **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="843ab-140">Encontre a seção **Module dependencies** no início do server.js e altere a linha que contém **sio = require('..//..//lib//socket.io')** para **sio = require('socket.io')**, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="843ab-140">Find the **Module dependencies** section at the beginning of server.js and change the line containing **sio = require('..//..//lib//socket.io')** to **sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="843ab-141">Para garantir que o aplicativo escuta na porta correta, abra o server.js no Bloco de notas ou em seu editor favorito, em seguida, altere a linha a seguir, substituindo **3000** por **process.env.port**, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="843ab-141">To ensure the application listens on the correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="843ab-142">Depois de salvar as alterações no **server.js**, use as seguintes etapas para instalar os módulos necessários e testar o aplicativo no emulador do Azure:</span><span class="sxs-lookup"><span data-stu-id="843ab-142">After saving the changes to **server.js**, use the following steps to install required modules, and then test the application in the Azure emulator:</span></span>

1. <span data-ttu-id="843ab-143">Usando o **Azure PowerShell**, altere os diretórios para o diretório **C:\\node\\chatapp\\WorkerRole1** e use o seguinte comando para instalar os módulos necessários para esse aplicativo:</span><span class="sxs-lookup"><span data-stu-id="843ab-143">Using **Azure PowerShell**, change directories to the **C:\\node\\chatapp\\WorkerRole1** directory and use the following command to install the modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="843ab-144">Isso instalará os módulos listados no arquivo package.json.</span><span class="sxs-lookup"><span data-stu-id="843ab-144">This will install the modules listed in the package.json file.</span></span> <span data-ttu-id="843ab-145">Quando o comando for concluído, você verá uma saída semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="843ab-145">After the command completes, you should see output similar to the following:</span></span>
   
   ![A saída do comando npm install][The-output-of-the-npm-install-command]
2. <span data-ttu-id="843ab-147">Como esse exemplo originalmente fazia parte do repositório Socket.IO GitHub e fazia referência direta à biblioteca do Socket.IO pelo caminho relativo, o Socket.IO não era referenciado no arquivo package.json, portanto, precisamos instalá-lo emitindo o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="843ab-147">Since this example was originally a part of the Socket.IO GitHub repository, and directly referenced the Socket.IO library by relative path, Socket.IO was not referenced in the package.json file, so we must install it by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="843ab-148">Testar e implantar</span><span class="sxs-lookup"><span data-stu-id="843ab-148">Test and Deploy</span></span>
1. <span data-ttu-id="843ab-149">Inicie o emulador emitindo o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="843ab-149">Launch the emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="843ab-150">Se você encontrar problemas ao iniciar o emulador, por exemplo: Start-AzureEmulator: ocorreu um erro inesperado.</span><span class="sxs-lookup"><span data-stu-id="843ab-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="843ab-151">Detalhes: encontrado um erro inesperado O objeto de comunicação, System.ServiceModel.Channels.ServiceChannel, não pode ser usado para comunicação porque está no estado Com falha.</span><span class="sxs-lookup"><span data-stu-id="843ab-151">Details: Encountered an unexpected error The communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in the Faulted state.</span></span>
   
      <span data-ttu-id="843ab-152">reinstale o AzureAuthoringTools v 2.7.1 e o AzureComputeEmulator v 2.7 – Verifique se a versão corresponde.</span><span class="sxs-lookup"><span data-stu-id="843ab-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="843ab-153">Abra um navegador e navegue até **http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="843ab-153">Open a browser and navigate to **http://127.0.0.1**.</span></span>
3. <span data-ttu-id="843ab-154">Quando a janela do navegador for aberta, digite um apelido e, em seguida, pressione enter.</span><span class="sxs-lookup"><span data-stu-id="843ab-154">When the browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="843ab-155">Isso permitirá que você poste mensagens usando um apelido específico.</span><span class="sxs-lookup"><span data-stu-id="843ab-155">This will allow you to post messages as a specific nickname.</span></span> <span data-ttu-id="843ab-156">Para testar a funcionalidade de vários usuários, abra janelas adicionais do navegador usando a mesma URL e digite apelidos diferentes.</span><span class="sxs-lookup"><span data-stu-id="843ab-156">To test multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![Duas janelas de navegador exibindo mensagens de chat do Usuário1 e do Usuário2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="843ab-158">Depois de testar o aplicativo, pare o emulador, emitindo o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="843ab-158">After testing the application, stop the emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="843ab-159">Para implantar o aplicativo no Azure, use o cmdlet **Publish-AzureServiceProject** .</span><span class="sxs-lookup"><span data-stu-id="843ab-159">To deploy the application to Azure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="843ab-160">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="843ab-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="843ab-161">Use um nome exclusivo, caso contrário, haverá falha no processo de publicação.</span><span class="sxs-lookup"><span data-stu-id="843ab-161">Be sure to use a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="843ab-162">Depois que a implantação for concluída, o navegador será aberto e navegará para o serviço implantado.</span><span class="sxs-lookup"><span data-stu-id="843ab-162">After the deployment has completed, the browser will open and navigate to the deployed service.</span></span>
   > 
   > <span data-ttu-id="843ab-163">Se você receber um erro informando que o nome da assinatura fornecido não existe no perfil de publicação importado, baixe e importe o perfil de publicação para sua assinatura antes de implantar no Azure.</span><span class="sxs-lookup"><span data-stu-id="843ab-163">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span></span> <span data-ttu-id="843ab-164">Consulte a seção **Implantando o aplicativo no Azure** seção de [Criar e implantar um aplicativo do Node.js em um Serviço de Nuvem do Azure (a página pode estar em inglês)](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="843ab-164">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Uma janela do navegador exibindo o serviço hospedado no Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="843ab-166">Se você receber um erro informando que o nome da assinatura fornecido não existe no perfil de publicação importado, baixe e importe o perfil de publicação para sua assinatura antes de implantar no Azure.</span><span class="sxs-lookup"><span data-stu-id="843ab-166">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span></span> <span data-ttu-id="843ab-167">Consulte a seção **Implantando o aplicativo no Azure** seção de [Criar e implantar um aplicativo do Node.js em um Serviço de Nuvem do Azure (a página pode estar em inglês)](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="843ab-167">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="843ab-168">Seu aplicativo agora está sendo executado no Azure e pode retransmitir mensagens de chat entre diferentes clientes usando o Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="843ab-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="843ab-169">Para simplificar, este exemplo é limitado a chat entre usuários conectados à mesma instância.</span><span class="sxs-lookup"><span data-stu-id="843ab-169">For simplicity, this sample is limited to chatting between users connected to the same instance.</span></span> <span data-ttu-id="843ab-170">Isso significa que se o serviço de nuvem criar duas instâncias de função de trabalho, os usuários só poderão conversar com outros usuários conectados à mesma instância de função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="843ab-170">This means that if the cloud service creates two worker role instances, users will only be able to chat with others connected to the same worker role instance.</span></span> <span data-ttu-id="843ab-171">Para dimensionar o aplicativo para trabalhar com várias instâncias de função, você pode usar uma tecnologia, como o Service Bus para compartilhar o estado do armazenamento do Socket.IO entre instâncias.</span><span class="sxs-lookup"><span data-stu-id="843ab-171">To scale the application to work with multiple role instances, you could use a technology like Service Bus to share the Socket.IO store state across instances.</span></span> <span data-ttu-id="843ab-172">Para obter exemplos, consulte os exemplos de uso dos Tópicos e Filas do Barramento de Serviço em [SDK do Azure para o repositório Node.js GitHub](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="843ab-172">For examples, see the Service Bus Queues and Topics usage samples in the [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="843ab-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="843ab-173">Next steps</span></span>
<span data-ttu-id="843ab-174">Neste tutorial, você aprendeu como criar um aplicativo de chat básico hospedado em um Serviço de Nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="843ab-174">In this tutorial you learned how to create a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="843ab-175">Para saber como hospedar esse aplicativo em um Site do Azure, confira [Criar um aplicativo de chat do Node.js com Socket.IO em um Site da Web do Azure][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="843ab-175">To learn how to host this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="843ab-176">Para obter mais informações, consulte também o [Centro de desenvolvedores do Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="843ab-176">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
<span data-ttu-id="843ab-177">[Socket.IO GitHub]: https://github.com/LearnBoost/socket.io/tree/0.9.14</span><span class="sxs-lookup"><span data-stu-id="843ab-177">[Socket.IO GitHub repository]: https://github.com/LearnBoost/socket.io/tree/0.9.14</span></span>
[Azure Considerations]: #windowsazureconsiderations
[Hosting the Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


