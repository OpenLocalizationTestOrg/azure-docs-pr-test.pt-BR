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
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a>Constrói um aplicativo de bate-papo Node.js com Socket.IO em um serviço de nuvem do Azure
O Socket.IO fornece comunicação em tempo real entre seu servidor e clientes do node.js. Este tutorial explica como hospedar um aplicativo de chat baseado em socket.IO no Microsoft Azure. Para mais informações sobre o Socket.IO, consulte <http://socket.io/>.

É uma captura de tela do aplicativo hello concluída abaixo:

![Uma janela do navegador exibindo o serviço de saudação hospedado no Azure][completed-app]  

## <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que Olá produtos a seguir e as versões estiverem instalados toosuccessfully exemplo hello concluída neste artigo:

* Instalar o [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)
* Instale o [Node.js](https://nodejs.org/download/)
* Instale o [Python versão 2.7.10](https://www.python.org/)

## <a name="create-a-cloud-service-project"></a>Criar um projeto de Serviço de Nuvem
Olá, etapas a seguir criam projeto de serviço de nuvem Olá que hospedará o aplicativo de Socket.IO hello.

1. De saudação **Menu Iniciar** ou **tela inicial**, procure **do Windows PowerShell**. Por fim, clique com botão direito em **Windows PowerShell** e selecione **Executar Como Administrador**.
   
    ![Ícone PowerShell do Azure][powershell-menu]
2. Crie um diretório denominado **c:\\node**. 
   
        PS C:\> md node
3. Altere os diretórios toohello **c:\\nó** diretório
   
        PS C:\> cd node
4. Digite hello comandos toocreate uma nova solução chamada a seguir **chatapp** e uma função de trabalho chamado **WorkerRole1**:
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    Você verá Olá resposta a seguir:
   
    ![saída de saudação do hello new-azureservice e azurenodeworkerrolecmdlets adicionar](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a>Baixar Olá exemplo Chat
Para este projeto, nós usaremos o exemplo de chat hello de saudação [repositório Socket.IO GitHub]. Executar Olá etapas toodownload Olá exemplo a seguir e adicione-o projeto toohello que você criou anteriormente.

1. Criar uma cópia local do repositório de saudação usando Olá **Clone** botão. Você também pode usar o hello **ZIP** projeto de saudação do botão toodownload.
   
   ![Uma janela do navegador exibindo https://github.com/LearnBoost/socket.io/tree/master/examples/chat, com o ícone de download do ZIP Olá realçado][chat-example-view]
2. Navegue estrutura de diretório de saudação do repositório local Olá até chegar na Olá **exemplos\\bate-papo** directory. Copiar conteúdo de saudação do toothe diretório **c:\\nó\\chatapp\\WorkerRole1** diretório criado anteriormente.
   
   ![Pesquisador de objetos, exibindo conteúdo de saudação do exemplos Olá\\directory bate-papo extraído do arquivo hello][chat-contents]
   
   itens realçados na captura de tela de saudação acima Hello são arquivos de saudação copiados da saudação **exemplos\\bate-papo** diretório
3. Em Olá **c:\\nó\\chatapp\\WorkerRole1** diretório, Olá delete **server.js** arquivo e, em seguida, renomeie Olá **app.js**arquivo muito**server.js**. Isso remove o padrão de saudação **server.js** arquivo criado anteriormente pela Olá **Add-AzureNodeWorkerRole** cmdlet e substitui-lo com o aplicativo hello arquivo hello exemplo bate-papo.

### <a name="modify-serverjs-and-install-modules"></a>Modificar o Server.js e instalar os módulos
Antes de aplicativo hello teste em Olá emulador do Azure, é necessário fazer algumas modificações secundárias. Execute Olá seguir etapas toothe server.js arquivo:

1. Olá abrir **server.js** arquivo no Visual Studio ou qualquer editor de texto.
2. Localize Olá **as dependências do módulo** seção no início de saudação do Server. js e alterar Olá linha contendo **sio = require('.. //.. lib//Socket.IO')** muito**sio = require('socket.io')** conforme mostrado abaixo:
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. aplicativo de hello tooensure ouve a porta correta hello, abra server.js no bloco de notas ou seu editor favorito e, em seguida, altere a linha a seguir, substituindo **3000** com **process.env.port** conforme mostrado abaixo:
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

Depois de salvar as alterações de saudação muito**server.js**, use Olá etapas a seguir para instalar os módulos necessários e, em seguida, testar o aplicativo hello no emulador do Azure:

1. Usando **Azure PowerShell**, altere os diretórios toohello **c:\\nó\\chatapp\\WorkerRole1** directory e uso Olá Olá de tooinstall de comando a seguir módulos necessários para este aplicativo:
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   Isso irá instalar módulos Olá listados no arquivo de Package. JSON hello. Após a conclusão do comando hello, você deve ver o seguinte de toothe semelhante de saída:
   
   ![comando de instalação de saída de saudação do npm Olá][The-output-of-the-npm-install-command]
2. Como este exemplo foi originalmente a parte da saudação repositório Socket.IO GitHub e referenciado diretamente a biblioteca de Socket.IO Olá pelo caminho relativo, Socket.IO não foi referenciado no arquivo de Package. JSON hello, portanto, deverá instalá-lo, emitindo o comando a seguir de saudação:
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a>Testar e implantar
1. Inicie o emulador Olá emitindo o comando a seguir de saudação:
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > Se você encontrar problemas ao iniciar o emulador, por exemplo: Start-AzureEmulator: ocorreu um erro inesperado.  Detalhes: Encontrado um objeto de comunicação de saudação do erro inesperado, ServiceChannel, não é usado para comunicação porque está no estado com falha de saudação.
   
      reinstale o AzureAuthoringTools v 2.7.1 e o AzureComputeEmulator v 2.7 – Verifique se a versão corresponde.
   >
   >


2. Abra um navegador e navegue muito**http://127.0.0.1**.
3. Quando abre a janela do navegador hello, insira um apelido e, em seguida, pressione enter.
   Isso permitirá que você toopost mensagens como um apelido específico. funcionalidade de multiusuário tootest, abra janelas adicionais do navegador usando a mesma URL e insira apelidos diferentes.
   
   ![Duas janelas de navegador exibindo mensagens de chat do Usuário1 e do Usuário2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. Após a aplicação de saudação do teste, pare emulador Olá emitindo o comando a seguir:
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. tooAzure de aplicativo hello toodeploy, use o **AzureServiceProject publicar** cmdlet. Por exemplo:
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > Ser um nome exclusivo de toouse-se de que, caso contrário, Olá publicar processo falhará. Após a implantação de hello, navegador Olá será aberto e navegue serviço toohello implantado.
   > 
   > Se você receber um erro indicando que Olá fornecidos nome de assinatura não existe no hello importado perfil de publicação, você deve baixar e importar o perfil de publicação Olá para sua assinatura antes de implantar tooAzure. Consulte Olá **Implantando Olá aplicativo tooAzure** seção [compilar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 
   
   ![Uma janela do navegador exibindo o serviço de saudação hospedado no Azure][completed-app]
   
   > [!NOTE]
   > Se você receber um erro indicando que Olá fornecidos nome de assinatura não existe no hello importado perfil de publicação, você deve baixar e importar o perfil de publicação Olá para sua assinatura antes de implantar tooAzure. Consulte Olá **Implantando Olá aplicativo tooAzure** seção [compilar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 

Seu aplicativo agora está sendo executado no Azure e pode retransmitir mensagens de chat entre diferentes clientes usando o Socket.IO.

> [!NOTE]
> Para simplificar, este exemplo é limitado toochatting entre toohello de usuários conectados mesma instância. Isso significa que se o serviço de nuvem Olá cria duas instâncias de função de trabalho, os usuários só poderão toochat com outros usuários conectados toohello mesma instância de função de trabalho. tooscale Olá aplicativo toowork com várias instâncias de função, você pode usar uma tecnologia como armazenar estado de barramento de serviço tooshare Olá Socket.IO entre instâncias. Para obter exemplos, consulte exemplos do uso de tópicos e filas do barramento de serviço do hello em Olá [SDK do Azure para o repositório GitHub Node. js](https://github.com/WindowsAzure/azure-sdk-for-node).
> 
> 

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como toocreate um aplicativo de chat básica hospedados em um serviço de nuvem do Azure. toolearn como toohost esse aplicativo em um site do Azure, consulte [criar um Site do Azure de um aplicativo de Chat do Node. js com Socket.IO][chatwebsite].

Para obter mais informações, consulte também Olá [Node. js Developer Center](/develop/nodejs/).

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


