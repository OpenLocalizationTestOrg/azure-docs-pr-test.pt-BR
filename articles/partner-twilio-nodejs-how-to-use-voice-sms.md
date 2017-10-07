---
title: aaaUsing Twilio de voz, VoIP e mensagens SMS no Azure
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Exemplos de códigos escritos em Node.js."
services: 
documentationcenter: nodejs
author: devinrader
manager: wpickett
editor: 
ms.assetid: f558cbbd-13d2-416f-b9b1-33a99c426af9
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/25/2014
ms.author: wpickett
ms.openlocfilehash: 6c44d60e217fcdf51e69fd2a8197f979afbb507a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a>Usando o Twilio para voz, VoIP e mensagens SMS no Azure
Este guia demonstra como toobuild aplicativos que se comunicam com Twilio e node.js no Azure.

<a id="whatis"/>

## <a name="what-is-twilio"></a>O que é o Twilio?
Twilio é uma plataforma de API que torna mais fácil para os desenvolvedores toomake e recebe chamadas telefônicas, envia e recebe mensagens de texto e insere a chamada de VoIP em aplicativos móveis baseados em navegador e nativos. Vamos ver brevemente como isso funciona antes de começar.

### <a name="receiving-calls-and-text-messages"></a>Recebendo chamadas e mensagens de texto
Twilio permite que os desenvolvedores muito[números de telefone programável de compra] [ purchase_phone] que pode ser usado tooboth enviar e receber chamadas e mensagens de texto. Quando um número Twilio recebe uma chamada de entrada ou de texto, Twilio enviará o aplicativo da web HTTP POST ou GET solicitação, solicitando que você para obter instruções sobre como toohandle Olá chamada ou texto. O servidor responderá a solicitação HTTP do tooTwilio com [TwiML][twiml], um conjunto simples de marcas XML que contém instruções sobre como toohandle uma chamada ou texto. Daqui a pouco, veremos exemplos de TwiML.

### <a name="making-calls-and-sending-text-messages"></a>Fazendo chamadas e enviando mensagens de texto
Fazendo solicitações HTTP toohello API do serviço web Twilio, os desenvolvedores podem enviar mensagens de texto ou iniciar chamadas telefônicas. Chamadas de saída, o desenvolvedor Olá também deve especificar uma URL que retorna TwiML instruções de como toohandle Olá saída chamar depois que ele está conectado.

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a>Inserindo recursos de VoIP no código da interface do usuário (JavaScript, iOS ou Android)
O Twilio fornece um SDK do lado do cliente que pode transformar qualquer navegador da web da área de trabalho, aplicativo iOS ou aplicativo Android em um telefone VoIP. Neste artigo, abordaremos como toouse VoIP chamando no navegador de saudação. Em adição toohello *SDK de JavaScript do Twilio* em execução no navegador hello, um aplicativo do lado do servidor (nosso aplicativo Node. js) deve ser usado tooissue um toohello "token de recurso" cliente JavaScript. Você pode ler mais sobre como usar VoIP com node.js [no blog de desenvolvimento do Twilio Olá][voipnode].

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a>Inscrever-se no Twilio (desconto da Microsoft)
Antes de usar os serviços do Twilio, você deve primeiro [inscrever-se em uma conta][signup]. Os clientes do Microsoft Azure recebem um desconto especial - [ser toosign-se aqui][signup]!

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a>Criar e implantar um site do node.js no Azure
Em seguida, você precisará toocreate um site da Web Node. js em execução no Azure. [a documentação oficial Hello para fazer isso está localizada aqui][azure_new_site]. Em um nível alto, você fará a seguir hello:

* Inscrever-se para uma conta do Azure, se ainda não tiver uma
* Usando toocreate de console de administração do Azure Olá um novo site
* Adicionar o suporte de controle do código-fonte (vamos pressupor que você tenha usado o git)
* Criar um arquivo `server.js` com um aplicativo Web Node. js simples
* Implantar esse aplicativo simples tooAzure

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a>Configurar Olá módulo Twilio
Em seguida, começaremos a toowrite um aplicativo simples Node. js que faz uso de saudação Twilio API. Antes de começar, é preciso tooconfigure nosso credenciais de conta do Twilio.

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a>Configurando as credenciais do Twilio nas variáveis de ambiente do sistema
Solicitações de toomake autenticado de ordem no back-end de Twilio hello, precisamos nossos SID da conta e o token de autenticação, a função como saudação de nome de usuário e a senha definida para nossa conta do Twilio. Olá tooconfigure de maneira mais segura para uso com o módulo de nó Olá no Azure é por meio de variáveis de ambiente do sistema, que pode ser definido diretamente no console de administração do Azure de saudação.

Selecione seu site node.js e clique hello "Configurar" link.  Se você rolar para baixo um pouco, verá uma área na qual poderá definir propriedades de configuração para o seu aplicativo.  Insira suas credenciais de conta do Twilio ([encontrado no seu Console do Twilio][twilio_console]) conforme mostrado - Verifique se tooname-las `TWILIO_ACCOUNT_SID` e `TWILIO_AUTH_TOKEN`, respectivamente:

![Console de administração do Azure][azure-admin-console]

Depois de configurar essas variáveis, reinicie o aplicativo no console do Azure de saudação.

### <a name="declaring-hello-twilio-module-in-packagejson"></a>Declarando o módulo do Twilio Olá em Package. JSON
Em seguida, precisamos toocreate um toomanage Package. JSON nosso dependências de módulo de nó por meio de [npm]. No hello mesmo nível como Olá `server.js` arquivo criado na Olá *Azure/node.js* tutorial, crie um arquivo chamado `package.json`.  Dentro desse arquivo, coloque o seguinte hello:

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node server"
  },
  "dependencies": {
    "body-parser": "^1.16.1",
    "ejs": "^2.5.5",
    "errorhandler": "^1.5.0",
    "express": "^4.14.1",
    "morgan": "^1.8.1",
    "twilio": "^2.11.1"
  }
}
```

Isso declara Olá twilio módulo como uma dependência, bem como Olá populares [Express framework do web] [ express] e mecanismo de modelo EJS hello.  Agora estamos prontos e vamos escrever um código!

<a id="makecall"/>

## <a name="make-an-outbound-call"></a>Fazer uma chamada de saída
Vamos criar um formulário simples que colocará um número de tooa de chamada que escolhemos. Abra o `server.js`e digite Olá código a seguir. Observe que onde diz "CHANGE_ME" - colocar o nome de saudação do seu site do azure existe:

```javascript
// Module dependencies
const express = require('express');
const path = require('path');
const http = require('http');
const twilio = require('twilio');
const logger = require('morgan');
const bodyParser = require('body-parser');
const errorHandler = require('errorhandler');
const accountSid = process.env.TWILIO_ACCOUNT_SID;
const authToken = process.env.TWILIO_AUTH_TOKEN;
// Create Express web application
const app = express();

// Express configuration
app.set('port', process.env.PORT || 3000);
app.set('views', __dirname + '/views');
app.set('view engine', 'ejs');
app.use(logger('tiny'));
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
app.use(express.static(path.join(__dirname, 'public')));

if (app.get('env') !== 'production') {
  app.use(errorHandler());
}

// Render an HTML user interface for hello application's home page
app.get('/', (request, response) => response.render('index'));

// Handle hello form POST tooplace a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call toothis number
    to:request.body.number,

    // Change tooa Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" tooyour app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});

// Generate TwiML toohandle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message toohello call's receiver
  twiml.say('hello - thanks for checking out Twilio and Azure', {
      voice:'woman'
  });

  response.set('Content-Type', 'text/xml');
  response.send(twiml.toString());
});

// Start server
app.listen(app.get('port'), function(){
  console.log(`Express server listening on port ${app.get('port')}`);
});
```

Em seguida, crie um diretório chamado `views` - dentro desse diretório, crie um arquivo chamado `index.ejs` com hello conteúdo a seguir:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Twilio Test</title>
  <style>
    input { height:20px; width:300px; font-size:18px; margin:5px; padding:5px; }
  </style>
</head>
<body>
  <h1>Twilio Test</h1>
  <form action="/call" method="POST">
      <input placeholder="Enter a phone number" name="number"/>
      <br/>
      <input type="submit" value="Call hello number above"/>
  </form>
</body>
</html>
```

Agora, implante seu site tooAzure e abrir a página inicial. Você deve ser capaz de tooenter seu número de telefone no campo de texto de saudação e receber uma chamada de seu número de Twilio!

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a>Enviar uma mensagem SMS
Agora, vamos configurar uma interface de usuário e toosend de lógica de tratamento de forma uma mensagem de texto. Abra `server.js`e adicione Olá seguinte código após a última chamada de saudação muito`app.post`:

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text toothis number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // hello body of hello text message
      body: request.body.message

  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});
```

Em `views/index.ejs`, adicione outro formulário em Olá primeiro um toosubmit um número e uma mensagem de texto:

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

Implante novamente o aplicativo tooAzure e agora você deve ser capaz de toosubmit que formam e enviar uma mensagem de texto a você mesmo (ou qualquer um dos seus amigos mais próximos)!

<a id="nextsteps"/>

## <a name="next-steps"></a>Próximas etapas
Agora, você aprendeu Noções básicas de saudação do uso do Node. js e Twilio toobuild aplicativos que se comunicam. Mas esses exemplos mal rascunho superfície de saudação do que é possível com Twilio e Node. js. Para obter mais informações usando o Twilio Node. js, confira Olá recursos a seguir:

* [Documentos oficiais do módulo][docs]
* [Tutorial sobre VoIP com aplicativos Node.js][voipnode]
* [Votr – um aplicativo de votação SMS em tempo real com node.js e CouchDB (três partes)][votr]
* [Programação do par no navegador de saudação com Node. js][pair]

Esperamos que você aprecie escrever com o node.js e o Twilio no Azure!

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
[npm]: http://npmjs.org
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
