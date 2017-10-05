---
title: Usando o Twilio para voz, VoIP e mensagens SMS no Azure
description: "Saiba como fazer uma chamada telefônica e enviar uma mensagem SMS com o serviço de API do Twilio no Azure. Exemplos de códigos escritos em Node.js."
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
ms.openlocfilehash: 44ec97812130d41d75be98fc8e2d846b7cb5c913
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="75b85-104">Usando o Twilio para voz, VoIP e mensagens SMS no Azure</span><span class="sxs-lookup"><span data-stu-id="75b85-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="75b85-105">Este guia demonstra como compilar aplicativos que se comunicam com o Twilio e o node.js no Azure.</span><span class="sxs-lookup"><span data-stu-id="75b85-105">This guide demonstrates how to build apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="75b85-106">O que é o Twilio?</span><span class="sxs-lookup"><span data-stu-id="75b85-106">What is Twilio?</span></span>
<span data-ttu-id="75b85-107">Twilio é uma plataforma de API que torna mais fácil para os desenvolvedores fazer e receber chamadas telefônicas, enviar e receber mensagens de texto e inserir chamadas VoIP em aplicativos móveis nativos e baseados em navegador.</span><span class="sxs-lookup"><span data-stu-id="75b85-107">Twilio is an API platform that makes it easy for developers to make and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="75b85-108">Vamos ver brevemente como isso funciona antes de começar.</span><span class="sxs-lookup"><span data-stu-id="75b85-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="75b85-109">Recebendo chamadas e mensagens de texto</span><span class="sxs-lookup"><span data-stu-id="75b85-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="75b85-110">O Twilio permite que os desenvolvedores [comprem números de telefone programáveis][purchase_phone] que podem ser usados para enviar e receber chamadas e mensagens de texto.</span><span class="sxs-lookup"><span data-stu-id="75b85-110">Twilio allows developers to [purchase programmable phone numbers][purchase_phone] which can be used to both send and receive calls and text messages.</span></span> <span data-ttu-id="75b85-111">Quando um número do Twilio recebe uma chamada de entrada ou texto, o Twilio envia uma solicitação HTTP POST ou GET ao seu aplicativo Web, solicitando que você forneça instruções sobre como lidar com o texto ou a chamada.</span><span class="sxs-lookup"><span data-stu-id="75b85-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how to handle the call or text.</span></span> <span data-ttu-id="75b85-112">O servidor responderá à solicitação HTTP do Twilio com [TwiML][twiml], um conjunto simples de marcas XML que contém instruções sobre como lidar com uma chamada ou um texto.</span><span class="sxs-lookup"><span data-stu-id="75b85-112">Your server will respond to Twilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how to handle a call or text.</span></span> <span data-ttu-id="75b85-113">Daqui a pouco, veremos exemplos de TwiML.</span><span class="sxs-lookup"><span data-stu-id="75b85-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="75b85-114">Fazendo chamadas e enviando mensagens de texto</span><span class="sxs-lookup"><span data-stu-id="75b85-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="75b85-115">Ao fazer solicitações HTTP para a API do serviço web do Twilio, os desenvolvedores podem enviar mensagens de texto ou iniciar chamadas telefônicas de saída.</span><span class="sxs-lookup"><span data-stu-id="75b85-115">By making HTTP requests to the Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="75b85-116">Para chamadas de saída, o desenvolvedor também deve especificar uma URL que retorne instruções TwiML de como lidar com a chamada de saída depois que ela estiver conectada.</span><span class="sxs-lookup"><span data-stu-id="75b85-116">For outbound calls, the developer must also specify a URL that returns TwiML instructions for how to handle the outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="75b85-117">Inserindo recursos de VoIP no código da interface do usuário (JavaScript, iOS ou Android)</span><span class="sxs-lookup"><span data-stu-id="75b85-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="75b85-118">O Twilio fornece um SDK do lado do cliente que pode transformar qualquer navegador da web da área de trabalho, aplicativo iOS ou aplicativo Android em um telefone VoIP.</span><span class="sxs-lookup"><span data-stu-id="75b85-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="75b85-119">Neste artigo, iremos nos concentrar em como usar as chamadas VoIP no navegador.</span><span class="sxs-lookup"><span data-stu-id="75b85-119">In this article, we will focus on how to use VoIP calling in the browser.</span></span> <span data-ttu-id="75b85-120">Além do *SDK do JavaScript para Twilio* executado no navegador, um aplicativo do lado do servidor (nosso aplicativo node.js) deve ser usado para emitir um "token de funcionalidade" para o cliente JavaScript.</span><span class="sxs-lookup"><span data-stu-id="75b85-120">In addition to the *Twilio JavaScript SDK* running in the browser, a server-side application (our node.js application) must be used to issue a "capability token" to the JavaScript client.</span></span> <span data-ttu-id="75b85-121">Você poderá ler mais sobre como usar VoIP com o node.js [no blog de desenvolvimento do Twilio][voipnode].</span><span class="sxs-lookup"><span data-stu-id="75b85-121">You can read more about using VoIP with node.js [on the Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="75b85-122">Inscrever-se no Twilio (desconto da Microsoft)</span><span class="sxs-lookup"><span data-stu-id="75b85-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="75b85-123">Antes de usar os serviços do Twilio, você deve primeiro [inscrever-se em uma conta][signup].</span><span class="sxs-lookup"><span data-stu-id="75b85-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="75b85-124">Os clientes do Microsoft Azure receberão um desconto especial – [inscreva-se aqui][signup]!</span><span class="sxs-lookup"><span data-stu-id="75b85-124">Microsoft Azure customers receive a special discount - [be sure to sign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="75b85-125">Criar e implantar um site do node.js no Azure</span><span class="sxs-lookup"><span data-stu-id="75b85-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="75b85-126">Em seguida, você precisará criar um site do node.js em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="75b85-126">Next, you will need to create a node.js website running on Azure.</span></span> <span data-ttu-id="75b85-127">[A documentação oficial para esse procedimento está localizada aqui][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="75b85-127">[The official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="75b85-128">Em um nível superior, você fará o seguinte:</span><span class="sxs-lookup"><span data-stu-id="75b85-128">At a high level, you will be doing the following:</span></span>

* <span data-ttu-id="75b85-129">Inscrever-se para uma conta do Azure, se ainda não tiver uma</span><span class="sxs-lookup"><span data-stu-id="75b85-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="75b85-130">Usar o console de administração do Azure para criar um novo site</span><span class="sxs-lookup"><span data-stu-id="75b85-130">Using the Azure admin console to create a new website</span></span>
* <span data-ttu-id="75b85-131">Adicionar o suporte de controle do código-fonte (vamos pressupor que você tenha usado o git)</span><span class="sxs-lookup"><span data-stu-id="75b85-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="75b85-132">Criar um arquivo `server.js` com um aplicativo Web Node. js simples</span><span class="sxs-lookup"><span data-stu-id="75b85-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="75b85-133">Implantar esse aplicativo simples no Azure</span><span class="sxs-lookup"><span data-stu-id="75b85-133">Deploying this simple application to Azure</span></span>

<a id="twiliomodule"/>

## <a name="configure-the-twilio-module"></a><span data-ttu-id="75b85-134">Configurar o módulo Twilio</span><span class="sxs-lookup"><span data-stu-id="75b85-134">Configure the Twilio Module</span></span>
<span data-ttu-id="75b85-135">Em seguida, começaremos a escrever um aplicativo node.js simples, que usa a API do Twilio.</span><span class="sxs-lookup"><span data-stu-id="75b85-135">Next, we will begin to write a simple node.js application which makes use of the Twilio API.</span></span> <span data-ttu-id="75b85-136">Antes de começar, precisamos configurar nossas credenciais de conta do Twilio.</span><span class="sxs-lookup"><span data-stu-id="75b85-136">Before we begin, we need to configure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="75b85-137">Configurando as credenciais do Twilio nas variáveis de ambiente do sistema</span><span class="sxs-lookup"><span data-stu-id="75b85-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="75b85-138">Para fazer solicitações autenticadas no back-end do Twilio, precisamos do nosso SID de conta e do token de autenticação, que funcionam como o nome de usuário e a senha definida para a nossa conta do Twilio.</span><span class="sxs-lookup"><span data-stu-id="75b85-138">In order to make authenticated requests against the Twilio back end, we need our account SID and auth token, which function as the username and password set for our Twilio account.</span></span> <span data-ttu-id="75b85-139">A maneira mais segura de configurá-los para uso com o módulo de nó no Azure é por meio de variáveis de ambiente do sistema, que podem ser definidas diretamente no console de administração do Azure.</span><span class="sxs-lookup"><span data-stu-id="75b85-139">The most secure way to configure these for use with the node module in Azure is via system environment variables, which you can set directly in the Azure admin console.</span></span>

<span data-ttu-id="75b85-140">Selecione o site do node.js e clique no link "CONFIGURAR".</span><span class="sxs-lookup"><span data-stu-id="75b85-140">Select your node.js website, and click the "CONFIGURE" link.</span></span>  <span data-ttu-id="75b85-141">Se você rolar para baixo um pouco, verá uma área na qual poderá definir propriedades de configuração para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="75b85-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="75b85-142">Insira suas credenciais de conta do Twilio ([encontradas no seu painel do Twilio][twilio_console]) conforme mostrado não se esqueça de dar-lhe os nomes `TWILIO_ACCOUNT_SID` e `TWILIO_AUTH_TOKEN`, respectivamente:</span><span class="sxs-lookup"><span data-stu-id="75b85-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure to name them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Console de administração do Azure][azure-admin-console]

<span data-ttu-id="75b85-144">Depois que você tiver configurado essas variáveis, reinicie o aplicativo no console do Azure.</span><span class="sxs-lookup"><span data-stu-id="75b85-144">Once you have configured these variables, restart your application in the Azure console.</span></span>

### <a name="declaring-the-twilio-module-in-packagejson"></a><span data-ttu-id="75b85-145">Declarando o módulo Twilio em package.json</span><span class="sxs-lookup"><span data-stu-id="75b85-145">Declaring the Twilio module in package.json</span></span>
<span data-ttu-id="75b85-146">Em seguida, precisaremos criar um package.json para gerenciar nossas dependências de módulo do nó via [npm].</span><span class="sxs-lookup"><span data-stu-id="75b85-146">Next, we need to create a package.json to manage our node module dependencies via [npm].</span></span> <span data-ttu-id="75b85-147">No mesmo nível que o arquivo `server.js` criado no tutorial do *Azure/node.js*, crie um arquivo denominado `package.json`.</span><span class="sxs-lookup"><span data-stu-id="75b85-147">At the same level as the `server.js` file you created in the *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="75b85-148">Dentro desse arquivo, coloque o seguinte:</span><span class="sxs-lookup"><span data-stu-id="75b85-148">Inside this file, place the following:</span></span>

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

<span data-ttu-id="75b85-149">Isso declara o módulo twilio como uma dependência, bem como a popular [estrutura do Web Express][express] e o mecanismo de modelo EJS.</span><span class="sxs-lookup"><span data-stu-id="75b85-149">This declares the twilio module as a dependency, as well as the popular [Express web framework][express] and the EJS template engine.</span></span>  <span data-ttu-id="75b85-150">Agora estamos prontos e vamos escrever um código!</span><span class="sxs-lookup"><span data-stu-id="75b85-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="75b85-151">Fazer uma chamada de saída</span><span class="sxs-lookup"><span data-stu-id="75b85-151">Make an Outbound Call</span></span>
<span data-ttu-id="75b85-152">Vamos criar um formulário simples que fará uma chamada para um número escolhido.</span><span class="sxs-lookup"><span data-stu-id="75b85-152">Let's create a simple form that will place a call to a number we choose.</span></span> <span data-ttu-id="75b85-153">Abra o `server.js` e insira o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="75b85-153">Open up `server.js`, and enter the following code.</span></span> <span data-ttu-id="75b85-154">Observe onde está escrito "CHANGE_ME" - coloque o nome do seu site do Azure nesse local:</span><span class="sxs-lookup"><span data-stu-id="75b85-154">Note where it says "CHANGE_ME" - put the name of your azure website there:</span></span>

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

// Render an HTML user interface for the application's home page
app.get('/', (request, response) => response.render('index'));

// Handle the form POST to place a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call to this number
    to:request.body.number,

    // Change to a Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" to your app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});

// Generate TwiML to handle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message to the call's receiver
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

<span data-ttu-id="75b85-155">Em seguida, crie um diretório denominado `views` e crie nele um arquivo denominado `index.ejs` com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="75b85-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with the following contents:</span></span>

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
      <input type="submit" value="Call the number above"/>
  </form>
</body>
</html>
```

<span data-ttu-id="75b85-156">Agora, implante o seu site no Azure e abra sua página inicial.</span><span class="sxs-lookup"><span data-stu-id="75b85-156">Now, deploy your website to Azure and open your home.</span></span> <span data-ttu-id="75b85-157">Você deve ser capaz de inserir seu número de telefone no campo de texto e receber uma chamada do seu número do Twilio!</span><span class="sxs-lookup"><span data-stu-id="75b85-157">You should be able to enter your phone number in the text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="75b85-158">Enviar uma mensagem SMS</span><span class="sxs-lookup"><span data-stu-id="75b85-158">Send an SMS Message</span></span>
<span data-ttu-id="75b85-159">Agora, vamos configurar uma interface de usuário e a lógica de manipulação de formulário para enviar uma mensagem de texto.</span><span class="sxs-lookup"><span data-stu-id="75b85-159">Now, let's set up a user interface and form handling logic to send a text message.</span></span> <span data-ttu-id="75b85-160">Abra o `server.js` e adicione o código a seguir após a última chamada para `app.post`:</span><span class="sxs-lookup"><span data-stu-id="75b85-160">Open up `server.js`, and add the following code after the last call to `app.post`:</span></span>

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text to this number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // The body of the text message
      body: request.body.message

  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});
```

<span data-ttu-id="75b85-161">Em `views/index.ejs`, adicione outro formulário sob o primeiro para enviar um número e uma mensagem de texto:</span><span class="sxs-lookup"><span data-stu-id="75b85-161">In `views/index.ejs`, add another form under the first one to submit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message to send" name="message"/>
  <br/>
  <input type="submit" value="Send text to the number above"/>
</form>
```

<span data-ttu-id="75b85-162">Reimplante seu aplicativo no Azure. Agora você deve conseguir enviar o formulário e uma mensagem de texto para você mesmo (ou para qualquer um dos seus amigos mais íntimos)!</span><span class="sxs-lookup"><span data-stu-id="75b85-162">Re-deploy your application to Azure, and you should now be able to submit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="75b85-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="75b85-163">Next Steps</span></span>
<span data-ttu-id="75b85-164">Agora, você aprendeu as noções básicas do uso do node.js e do Twilio para compilar aplicativos que se comunicam.</span><span class="sxs-lookup"><span data-stu-id="75b85-164">You have now learned the basics of using node.js and Twilio to build apps that communicate.</span></span> <span data-ttu-id="75b85-165">Mas esses exemplos pouco abordam o que é possível fazer com o Twilio e o node.js.</span><span class="sxs-lookup"><span data-stu-id="75b85-165">But these examples barely scratch the surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="75b85-166">Para obter mais informações sobre como usar o Twilio com o node.js, verifique os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="75b85-166">For more information using Twilio with node.js, check out the following resources:</span></span>

* <span data-ttu-id="75b85-167">[Documentos oficiais do módulo][docs]</span><span class="sxs-lookup"><span data-stu-id="75b85-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="75b85-168">[Tutorial sobre VoIP com aplicativos Node.js][voipnode]</span><span class="sxs-lookup"><span data-stu-id="75b85-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="75b85-169">[Votr – um aplicativo de votação SMS em tempo real com node.js e CouchDB (três partes)][votr]</span><span class="sxs-lookup"><span data-stu-id="75b85-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="75b85-170">[Programação de par no navegador com node.js][pair]</span><span class="sxs-lookup"><span data-stu-id="75b85-170">[Pair programming in the browser with node.js][pair]</span></span>

<span data-ttu-id="75b85-171">Esperamos que você aprecie escrever com o node.js e o Twilio no Azure!</span><span class="sxs-lookup"><span data-stu-id="75b85-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
<span data-ttu-id="75b85-172">[npm]: http://npmjs.org</span><span class="sxs-lookup"><span data-stu-id="75b85-172">[npm]: http://npmjs.org</span></span>
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
