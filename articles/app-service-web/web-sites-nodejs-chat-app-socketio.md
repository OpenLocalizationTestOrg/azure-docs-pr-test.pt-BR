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
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>Criar um aplicativo de chat do Node.js com Socket.IO no Serviço de Aplicativo do Azure
Socket.IO fornece uma comunicação em tempo real entre o seu servidor node.js e clientes usando WebSockets. Ele também dá suporte a transportes de fallback tooother (por exemplo, a sondagem longa) que funcionam com navegadores mais antigos. Este tutorial orientará hospedando um aplicativo de bate-papo Socket.IO com base em como um aplicativo web do Azure e mostram como tooscale hello usando o aplicativo [Cache Redis do Azure]. Para mais informações sobre o Socket.IO, consulte <http://socket.io/>.

> [!NOTE]
> Olá procedimentos nessa tarefa aplicam-se muito[aplicativo de serviço Web aplicativos]; para serviços de nuvem, consulte [criar um aplicativo de Chat do Node. js com Socket.IO em um serviço de nuvem do Azure].
> 
> 

## <a name="download-hello-chat-example"></a>Baixe o exemplo de chat hello
Para este projeto, nós usaremos o exemplo de chat hello de saudação [repositório Socket.IO GitHub]. Executar Olá etapas toodownload Olá exemplo a seguir e adicione-o projeto toohello que você criou anteriormente.

1. Baixar um [ZIP ou GZ arquivado versão] do projeto de Socket.IO hello (versão 1.3.5 foi usado para este documento)
2. Extrair Olá Olá arquivamento e cópia **exemplos\\bate-papo** novo local do diretório tooa. Por exemplo, **\\node\\chat**.

## <a name="modify-appjs-and-install-modules"></a>Modificar o app.js e instalar os módulos
1. Renomear Olá **js** arquivo muito**app.js**. Isso permite que toodetect do Azure que se trata de um aplicativo Node. js.
2. Olá abrir **app.js** em um editor de texto. Alteração Olá linha contendo `var io = require('../..')(server);` conforme mostrado abaixo:
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. Olá abrir **Package. JSON** de arquivos e adicionar um toosocket.io de referência em `dependencies`, conforme mostrado abaixo:
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. Saudação de linha de comando, alterar toohello  **\\nó\\bate-papo** directory e uso tooinstall Olá módulos npm exigidos por este aplicativo:
   
        npm install
   
    Isso irá instalar os módulos de saudação em uma subpasta chamada **node_modules**.

## <a name="create-an-azure-web-app"></a>Criar um aplicativo Web do Azure
Siga essas etapas toocreate um aplicativo web do Azure, habilitar a publicação de Git e, em seguida, habilitar o suporte de WebSocket do aplicativo web de saudação.

> [!NOTE]
> toocomplete neste tutorial, você precisa de uma conta do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Avaliação gratuita do Azure</a>.
> 
> 

1. Instalar hello Azure Interface de linha de comando (CLI do Azure) e conecte-se tooyour assinatura do Azure. Consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md).
2. Se esse for o primeiro tempo configurando um repositório no Azure, você precisa ter credenciais de logon de toocreate. Em Olá CLI do Azure, digite Olá comando a seguir:
   
        azure site deployment user set [username] [password]
3. Alterar toohello  **\\node\chat** directory e uso a seguir Olá comando toocreate um novo aplicativo web do Azure e um repositório Git local. Esse comando também cria um repositório remoto do Git chamado 'azure'.
   
        azure site create mysitename --git
   
    Você deve substituir 'mysitename' por um nome exclusivo para seu aplicativo Web.
4. Confirme Olá existente arquivos toohello repositório local usando Olá comandos a seguir:
   
        git add .
        git commit -m "Initial commit"
5. Enviar por push de repositório de aplicativos Web do Azure Olá arquivos toohello com hello comando a seguir:
   
        git push azure master
   
    Quando solicitado, insira suas credenciais da etapa 2. Você receberá mensagens de status, como os módulos são importados no servidor de saudação. Depois que esse processo for concluído, o aplicativo hello será hospedado em seu aplicativo web do Azure.
   
   > [!NOTE]
   > Durante a instalação do módulo, você pode observar erros que ' hello... projeto importado não foi encontrado '. Isso podem ser ignorados.
   > 
   > 
6. Socket.IO usa o WebSocket, que não é habilitado por padrão no Azure. soquetes da web de tooenable, use Olá comando a seguir:
   
        azure site set -w
   
    Se solicitado, insira o nome de saudação do aplicativo web de saudação.
   
   > [!NOTE]
   > Olá será de comando 'site do azure set -w' funcionam somente com a versão 0.7.4 ou posterior do hello Interface de linha de comando do Azure. Você também pode habilitar o suporte para WebSocket usando Olá [Portal do Azure](https://portal.azure.com).
   > 
   > usando o WebSocket tooenable Olá Portal do Azure, clique em aplicativo web de saudação da folha de aplicativos Web de saudação do **todas as configurações** > **configurações do aplicativo**. Em **Web Sockets**, clique em **Ativado**. Em seguida, clique em **Salvar**.
   > 
   > 
7. tooview Olá web app no seguinte de saudação do Azure, use comando toolaunch seu navegador da web e navegue toohello hospedado web app:
   
        azure site browse

Seu aplicativo agora está sendo executado no Azure e pode retransmitir mensagens de chat entre diferentes clientes usando o Socket.IO.

## <a name="scale-out"></a>Expansão
Aplicativos Socket.IO podem ser expandidos usando um **adaptador** toodistribute mensagens e eventos entre várias instâncias do aplicativo. Embora haja várias adaptadores disponíveis, Olá [redis socket.io] adaptador pode ser usado com o recurso de Cache Redis do Azure Olá facilmente.

> [!NOTE]
> Um requisito adicional para expandir uma solução Socket.IO é dar suporte a sessões complexas. As sessões complexas são habilitadas por padrão para Aplicativos Web do Azure por meio do Request Routing do Azure. Para obter mais informações, consulte [Afinidade da instância nos Sites do Azure].
> 
> 

### <a name="create-a-redis-cache"></a>Criar um cache Redis
Execute as etapas de saudação em [criar um cache no Cache Redis do Azure] toocreate um novo cache.

> [!NOTE]
> Salvar Olá **nome de Host** e **chave primária** para seu cache, como eles serão necessários no hello próximas etapas.
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a>Adicionar redis hello e módulos socket.io redis
1. De uma linha de comando, altere toohello  **\\nó\\bate-papo** saudação de diretório e usar comandos a seguir.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > Olá versões especificadas neste comando são Olá usados ao testar este artigo.
   > 
   > 
2. Modificar Olá **app.js** linhas seguintes do arquivo tooadd Olá imediatamente após`var io = require('socket.io')(server);`
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    Substituir **redishostname** e **rediskey** com nome de host de saudação e a chave para o cache Redis.
   
    Isso criará uma publicação e assinar toohello cliente Redis cache criado anteriormente. clientes Hello são usados com hello adaptador tooconfigure cache Redis do Socket.IO toouse Olá para transmitir mensagens e eventos entre instâncias do seu aplicativo
   
   > [!NOTE]
   > Durante a saudação **redis socket.io** adaptador pode se comunicar diretamente tooRedis, versão atual do hello não dá suporte à autenticação de saudação exigida pelo cache Redis do Azure. Para a conexão inicial Olá é criado usando Olá **redis** módulo, o cliente de hello, em seguida, é passada toohello **redis socket.io** adaptador.
   > 
   > Enquanto o Cache Redis do Azure dá suporte a conexões seguras usando a porta 6380, módulos de saudação usados neste exemplo não dão suporte a conexões seguras a partir de 14/7/2014. Olá acima código usa saudação padrão, porta não segura de 6379.
   > 
   > 
3. Salvar Olá modificado **app.js**

### <a name="commit-changes-and-redeploy"></a>Confirme as alterações e implantar novamente
De saudação de linha de comando no hello  **\\nó\\bate-papo** diretório, use Olá comandos toocommit alterações a seguir e reimplantar o aplicativo hello.

    git add .
    git commit -m "implementing scale out"
    git push azure master

Depois que alterações Olá foram empurrados para servidor toohello, você pode dimensionar seu site em várias instâncias usando o comando a seguir de saudação.

    azure site scale instances --instances #

Onde  **#**  é Olá número de instâncias toocreate.

Você pode conectar o aplicativo da web de tooyour de tooverify vários navegadores ou computadores que são enviadas corretamente tooall clientes.

## <a name="troubleshooting"></a>Solucionar problemas
### <a name="connection-limits"></a>Limites de conexão
Os aplicativos Web do Azure está disponível em várias SKUs, que determinam o site do hello recursos tooyour disponíveis. Isso inclui o número de saudação do WebSocket de conexões permitidas. Para obter mais informações, consulte Olá [página de preços de aplicativos Web].

### <a name="messages-arent-being-sent-using-websockets"></a>As mensagens não estão sendo enviadas usando o WebSockets
Se navegadores clientes mantenham voltando toolong sondagem em vez de usar o WebSocket, pode ser devido a um dos seguintes hello.

* **Tente limitar Olá transporte toojust WebSockets**
  
    A fim de toouse Socket.IO WebSockets como transporte de mensagens de saudação, cliente e servidor de saudação devem oferecer suporte a WebSockets. Se um ou Olá outros não, Socket.IO negociará outro transporte, como sondagem longa. a lista de transportes usados por Socket.IO padrão Olá é ` websocket, htmlfile, xhr-polling, jsonp-polling`. Você pode forçar o uso de tooonly WebSockets adicionando Olá toohello de código a seguir **app.js** arquivo após Olá linha contendo `, nicknames = {};`.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > Observe que navegadores mais antigos que não oferecem suporte a WebSockets não será capaz de tooconnect toohello site enquanto Olá acima código está ativa, pois ela restringe a comunicação tooWebSockets somente.
  > 
  > 
* **Usar o SSL**
  
    WebSockets depende de alguns menor cabeçalhos HTTP usados, como Olá **atualização** cabeçalho. Alguns dispositivos de rede intermediários, como os proxies da web, podem remover esses cabeçalhos. tooavoid esse problema, você pode estabelecer uma conexão de WebSocket Olá sobre SSL.
  
    Uma maneira fácil tooaccomplish isso é tooconfigure Socket.IO muito`match origin protocol`. Isso instrui igual Olá HTTP/HTTPS de origem de solicitação para página da web de Olá Olá de comunicação Socket.IO toosecure WebSocket. Se o navegador usa uma URL HTTPS toovisit seu site, comunicações subsequentes do WebSocket por meio de Socket.IO serão protegidas por SSL.
  
    toomodify tooenable esse exemplo nessa configuração, adicione Olá toohello de código a seguir **app.js** arquivo após Olá linha contendo `, nicknames = {};`.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **Verificar as configurações do web.config**
  
    Aplicativos web do Azure que hospedam aplicativos Node. js usam Olá **Web. config** arquivo tooroute entrada solicitações toohello Node. js aplicativo. Para toofunction WebSockets corretamente com aplicativos Node. js, Olá **Web. config** deve conter a seguinte entrada de saudação.
  
        <webSocket enabled="false"/>
  
    Isso desabilita o módulo de WebSockets do IIS hello, que inclui sua própria implementação do WebSocket e está em conflito com módulos específicos de WebSocket Node. js como Socket.IO. Se essa linha não está presente ou está definida muito`true`, isso pode ser o motivo de saudação que transporte de WebSocket Olá não está funcionando para seu aplicativo.
  
    Normalmente, os aplicativos Node.js não incluem um arquivo **web.config** , por tanto os Sites do Azure gerarão automaticamente um para os aplicativos Node.js assim que estiverem implantados. Como esse arquivo é gerado automaticamente no servidor de saudação, você deve usar Olá FTP ou FTPS URL para seu site tooview esse arquivo. Você pode encontrar hello FTP e FTPS URLs para seu site no portal clássico Olá selecionando seu aplicativo web e, em seguida, Olá **painel** link. Olá URLs são exibidas no hello **visão rápida** seção.
  
  > [!NOTE]
  > Olá **Web. config** arquivo é gerado apenas por sites do Azure se seu aplicativo não fornecer um. Se você fornecer um **Web. config** arquivo na raiz de saudação do seu projeto de aplicativo, ele será usado por aplicativos Web do Azure.
  > 
  > 
  
    Se a entrada hello não está presente ou estiver definida como valor de tooa de `true`, em seguida, você deve criar um **Web. config** Olá raiz do seu aplicativo Node. js e especifique um valor de `false`.  Para referência, Olá abaixo é um padrão **Web. config** para um aplicativo que usa **app.js** como ponto de entrada hello.
  
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
  
    Se seu aplicativo usa um ponto de entrada diferente de **app.js**, você deve substituir todas as ocorrências de **app.js** com hello corrigir o ponto de entrada. Por exemplo, substituir o **app.js** por **server.js**.

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo], onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como toocreate um aplicativo de chat hospedados em um aplicativo web do Azure. Você também pode hospedar o aplicativo como um serviço de nuvem do Azure. Para obter etapas sobre como tooaccomplish isso, consulte [criar um aplicativo de Chat do Node. js com Socket.IO em um serviço de nuvem do Azure].

Para obter mais informações, consulte também Olá [Node. js Developer Center].

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente].

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
