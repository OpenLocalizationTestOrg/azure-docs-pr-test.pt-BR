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
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="4aac0-104">Usando o Twilio para voz, VoIP e mensagens SMS no Azure</span><span class="sxs-lookup"><span data-stu-id="4aac0-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="4aac0-105">Este guia demonstra como toobuild aplicativos que se comunicam com Twilio e node.js no Azure.</span><span class="sxs-lookup"><span data-stu-id="4aac0-105">This guide demonstrates how toobuild apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="4aac0-106">O que é o Twilio?</span><span class="sxs-lookup"><span data-stu-id="4aac0-106">What is Twilio?</span></span>
<span data-ttu-id="4aac0-107">Twilio é uma plataforma de API que torna mais fácil para os desenvolvedores toomake e recebe chamadas telefônicas, envia e recebe mensagens de texto e insere a chamada de VoIP em aplicativos móveis baseados em navegador e nativos.</span><span class="sxs-lookup"><span data-stu-id="4aac0-107">Twilio is an API platform that makes it easy for developers toomake and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="4aac0-108">Vamos ver brevemente como isso funciona antes de começar.</span><span class="sxs-lookup"><span data-stu-id="4aac0-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="4aac0-109">Recebendo chamadas e mensagens de texto</span><span class="sxs-lookup"><span data-stu-id="4aac0-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="4aac0-110">Twilio permite que os desenvolvedores muito[números de telefone programável de compra] [ purchase_phone] que pode ser usado tooboth enviar e receber chamadas e mensagens de texto.</span><span class="sxs-lookup"><span data-stu-id="4aac0-110">Twilio allows developers too[purchase programmable phone numbers][purchase_phone] which can be used tooboth send and receive calls and text messages.</span></span> <span data-ttu-id="4aac0-111">Quando um número Twilio recebe uma chamada de entrada ou de texto, Twilio enviará o aplicativo da web HTTP POST ou GET solicitação, solicitando que você para obter instruções sobre como toohandle Olá chamada ou texto.</span><span class="sxs-lookup"><span data-stu-id="4aac0-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how toohandle hello call or text.</span></span> <span data-ttu-id="4aac0-112">O servidor responderá a solicitação HTTP do tooTwilio com [TwiML][twiml], um conjunto simples de marcas XML que contém instruções sobre como toohandle uma chamada ou texto.</span><span class="sxs-lookup"><span data-stu-id="4aac0-112">Your server will respond tooTwilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how toohandle a call or text.</span></span> <span data-ttu-id="4aac0-113">Daqui a pouco, veremos exemplos de TwiML.</span><span class="sxs-lookup"><span data-stu-id="4aac0-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="4aac0-114">Fazendo chamadas e enviando mensagens de texto</span><span class="sxs-lookup"><span data-stu-id="4aac0-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="4aac0-115">Fazendo solicitações HTTP toohello API do serviço web Twilio, os desenvolvedores podem enviar mensagens de texto ou iniciar chamadas telefônicas.</span><span class="sxs-lookup"><span data-stu-id="4aac0-115">By making HTTP requests toohello Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="4aac0-116">Chamadas de saída, o desenvolvedor Olá também deve especificar uma URL que retorna TwiML instruções de como toohandle Olá saída chamar depois que ele está conectado.</span><span class="sxs-lookup"><span data-stu-id="4aac0-116">For outbound calls, hello developer must also specify a URL that returns TwiML instructions for how toohandle hello outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="4aac0-117">Inserindo recursos de VoIP no código da interface do usuário (JavaScript, iOS ou Android)</span><span class="sxs-lookup"><span data-stu-id="4aac0-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="4aac0-118">O Twilio fornece um SDK do lado do cliente que pode transformar qualquer navegador da web da área de trabalho, aplicativo iOS ou aplicativo Android em um telefone VoIP.</span><span class="sxs-lookup"><span data-stu-id="4aac0-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="4aac0-119">Neste artigo, abordaremos como toouse VoIP chamando no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aac0-119">In this article, we will focus on how toouse VoIP calling in hello browser.</span></span> <span data-ttu-id="4aac0-120">Em adição toohello *SDK de JavaScript do Twilio* em execução no navegador hello, um aplicativo do lado do servidor (nosso aplicativo Node. js) deve ser usado tooissue um toohello "token de recurso" cliente JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4aac0-120">In addition toohello *Twilio JavaScript SDK* running in hello browser, a server-side application (our node.js application) must be used tooissue a "capability token" toohello JavaScript client.</span></span> <span data-ttu-id="4aac0-121">Você pode ler mais sobre como usar VoIP com node.js [no blog de desenvolvimento do Twilio Olá][voipnode].</span><span class="sxs-lookup"><span data-stu-id="4aac0-121">You can read more about using VoIP with node.js [on hello Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="4aac0-122">Inscrever-se no Twilio (desconto da Microsoft)</span><span class="sxs-lookup"><span data-stu-id="4aac0-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="4aac0-123">Antes de usar os serviços do Twilio, você deve primeiro [inscrever-se em uma conta][signup].</span><span class="sxs-lookup"><span data-stu-id="4aac0-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="4aac0-124">Os clientes do Microsoft Azure recebem um desconto especial - [ser toosign-se aqui][signup]!</span><span class="sxs-lookup"><span data-stu-id="4aac0-124">Microsoft Azure customers receive a special discount - [be sure toosign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="4aac0-125">Criar e implantar um site do node.js no Azure</span><span class="sxs-lookup"><span data-stu-id="4aac0-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="4aac0-126">Em seguida, você precisará toocreate um site da Web Node. js em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="4aac0-126">Next, you will need toocreate a node.js website running on Azure.</span></span> <span data-ttu-id="4aac0-127">[a documentação oficial Hello para fazer isso está localizada aqui][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="4aac0-127">[hello official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="4aac0-128">Em um nível alto, você fará a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="4aac0-128">At a high level, you will be doing hello following:</span></span>

* <span data-ttu-id="4aac0-129">Inscrever-se para uma conta do Azure, se ainda não tiver uma</span><span class="sxs-lookup"><span data-stu-id="4aac0-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="4aac0-130">Usando toocreate de console de administração do Azure Olá um novo site</span><span class="sxs-lookup"><span data-stu-id="4aac0-130">Using hello Azure admin console toocreate a new website</span></span>
* <span data-ttu-id="4aac0-131">Adicionar o suporte de controle do código-fonte (vamos pressupor que você tenha usado o git)</span><span class="sxs-lookup"><span data-stu-id="4aac0-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="4aac0-132">Criar um arquivo `server.js` com um aplicativo Web Node. js simples</span><span class="sxs-lookup"><span data-stu-id="4aac0-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="4aac0-133">Implantar esse aplicativo simples tooAzure</span><span class="sxs-lookup"><span data-stu-id="4aac0-133">Deploying this simple application tooAzure</span></span>

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a><span data-ttu-id="4aac0-134">Configurar Olá módulo Twilio</span><span class="sxs-lookup"><span data-stu-id="4aac0-134">Configure hello Twilio Module</span></span>
<span data-ttu-id="4aac0-135">Em seguida, começaremos a toowrite um aplicativo simples Node. js que faz uso de saudação Twilio API.</span><span class="sxs-lookup"><span data-stu-id="4aac0-135">Next, we will begin toowrite a simple node.js application which makes use of hello Twilio API.</span></span> <span data-ttu-id="4aac0-136">Antes de começar, é preciso tooconfigure nosso credenciais de conta do Twilio.</span><span class="sxs-lookup"><span data-stu-id="4aac0-136">Before we begin, we need tooconfigure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="4aac0-137">Configurando as credenciais do Twilio nas variáveis de ambiente do sistema</span><span class="sxs-lookup"><span data-stu-id="4aac0-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="4aac0-138">Solicitações de toomake autenticado de ordem no back-end de Twilio hello, precisamos nossos SID da conta e o token de autenticação, a função como saudação de nome de usuário e a senha definida para nossa conta do Twilio.</span><span class="sxs-lookup"><span data-stu-id="4aac0-138">In order toomake authenticated requests against hello Twilio back end, we need our account SID and auth token, which function as hello username and password set for our Twilio account.</span></span> <span data-ttu-id="4aac0-139">Olá tooconfigure de maneira mais segura para uso com o módulo de nó Olá no Azure é por meio de variáveis de ambiente do sistema, que pode ser definido diretamente no console de administração do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aac0-139">hello most secure way tooconfigure these for use with hello node module in Azure is via system environment variables, which you can set directly in hello Azure admin console.</span></span>

<span data-ttu-id="4aac0-140">Selecione seu site node.js e clique hello "Configurar" link.</span><span class="sxs-lookup"><span data-stu-id="4aac0-140">Select your node.js website, and click hello "CONFIGURE" link.</span></span>  <span data-ttu-id="4aac0-141">Se você rolar para baixo um pouco, verá uma área na qual poderá definir propriedades de configuração para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4aac0-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="4aac0-142">Insira suas credenciais de conta do Twilio ([encontrado no seu Console do Twilio][twilio_console]) conforme mostrado - Verifique se tooname-las `TWILIO_ACCOUNT_SID` e `TWILIO_AUTH_TOKEN`, respectivamente:</span><span class="sxs-lookup"><span data-stu-id="4aac0-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure tooname them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Console de administração do Azure][azure-admin-console]

<span data-ttu-id="4aac0-144">Depois de configurar essas variáveis, reinicie o aplicativo no console do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aac0-144">Once you have configured these variables, restart your application in hello Azure console.</span></span>

### <a name="declaring-hello-twilio-module-in-packagejson"></a><span data-ttu-id="4aac0-145">Declarando o módulo do Twilio Olá em Package. JSON</span><span class="sxs-lookup"><span data-stu-id="4aac0-145">Declaring hello Twilio module in package.json</span></span>
<span data-ttu-id="4aac0-146">Em seguida, precisamos toocreate um toomanage Package. JSON nosso dependências de módulo de nó por meio de [npm].</span><span class="sxs-lookup"><span data-stu-id="4aac0-146">Next, we need toocreate a package.json toomanage our node module dependencies via [npm].</span></span> <span data-ttu-id="4aac0-147">No hello mesmo nível como Olá `server.js` arquivo criado na Olá *Azure/node.js* tutorial, crie um arquivo chamado `package.json`.</span><span class="sxs-lookup"><span data-stu-id="4aac0-147">At hello same level as hello `server.js` file you created in hello *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="4aac0-148">Dentro desse arquivo, coloque o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="4aac0-148">Inside this file, place hello following:</span></span>

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

<span data-ttu-id="4aac0-149">Isso declara Olá twilio módulo como uma dependência, bem como Olá populares [Express framework do web] [ express] e mecanismo de modelo EJS hello.</span><span class="sxs-lookup"><span data-stu-id="4aac0-149">This declares hello twilio module as a dependency, as well as hello popular [Express web framework][express] and hello EJS template engine.</span></span>  <span data-ttu-id="4aac0-150">Agora estamos prontos e vamos escrever um código!</span><span class="sxs-lookup"><span data-stu-id="4aac0-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="4aac0-151">Fazer uma chamada de saída</span><span class="sxs-lookup"><span data-stu-id="4aac0-151">Make an Outbound Call</span></span>
<span data-ttu-id="4aac0-152">Vamos criar um formulário simples que colocará um número de tooa de chamada que escolhemos.</span><span class="sxs-lookup"><span data-stu-id="4aac0-152">Let's create a simple form that will place a call tooa number we choose.</span></span> <span data-ttu-id="4aac0-153">Abra o `server.js`e digite Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="4aac0-153">Open up `server.js`, and enter hello following code.</span></span> <span data-ttu-id="4aac0-154">Observe que onde diz "CHANGE_ME" - colocar o nome de saudação do seu site do azure existe:</span><span class="sxs-lookup"><span data-stu-id="4aac0-154">Note where it says "CHANGE_ME" - put hello name of your azure website there:</span></span>

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

<span data-ttu-id="4aac0-155">Em seguida, crie um diretório chamado `views` - dentro desse diretório, crie um arquivo chamado `index.ejs` com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aac0-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with hello following contents:</span></span>

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

<span data-ttu-id="4aac0-156">Agora, implante seu site tooAzure e abrir a página inicial.</span><span class="sxs-lookup"><span data-stu-id="4aac0-156">Now, deploy your website tooAzure and open your home.</span></span> <span data-ttu-id="4aac0-157">Você deve ser capaz de tooenter seu número de telefone no campo de texto de saudação e receber uma chamada de seu número de Twilio!</span><span class="sxs-lookup"><span data-stu-id="4aac0-157">You should be able tooenter your phone number in hello text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="4aac0-158">Enviar uma mensagem SMS</span><span class="sxs-lookup"><span data-stu-id="4aac0-158">Send an SMS Message</span></span>
<span data-ttu-id="4aac0-159">Agora, vamos configurar uma interface de usuário e toosend de lógica de tratamento de forma uma mensagem de texto.</span><span class="sxs-lookup"><span data-stu-id="4aac0-159">Now, let's set up a user interface and form handling logic toosend a text message.</span></span> <span data-ttu-id="4aac0-160">Abra `server.js`e adicione Olá seguinte código após a última chamada de saudação muito`app.post`:</span><span class="sxs-lookup"><span data-stu-id="4aac0-160">Open up `server.js`, and add hello following code after hello last call too`app.post`:</span></span>

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

<span data-ttu-id="4aac0-161">Em `views/index.ejs`, adicione outro formulário em Olá primeiro um toosubmit um número e uma mensagem de texto:</span><span class="sxs-lookup"><span data-stu-id="4aac0-161">In `views/index.ejs`, add another form under hello first one toosubmit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

<span data-ttu-id="4aac0-162">Implante novamente o aplicativo tooAzure e agora você deve ser capaz de toosubmit que formam e enviar uma mensagem de texto a você mesmo (ou qualquer um dos seus amigos mais próximos)!</span><span class="sxs-lookup"><span data-stu-id="4aac0-162">Re-deploy your application tooAzure, and you should now be able toosubmit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="4aac0-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4aac0-163">Next Steps</span></span>
<span data-ttu-id="4aac0-164">Agora, você aprendeu Noções básicas de saudação do uso do Node. js e Twilio toobuild aplicativos que se comunicam.</span><span class="sxs-lookup"><span data-stu-id="4aac0-164">You have now learned hello basics of using node.js and Twilio toobuild apps that communicate.</span></span> <span data-ttu-id="4aac0-165">Mas esses exemplos mal rascunho superfície de saudação do que é possível com Twilio e Node. js.</span><span class="sxs-lookup"><span data-stu-id="4aac0-165">But these examples barely scratch hello surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="4aac0-166">Para obter mais informações usando o Twilio Node. js, confira Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aac0-166">For more information using Twilio with node.js, check out hello following resources:</span></span>

* <span data-ttu-id="4aac0-167">[Documentos oficiais do módulo][docs]</span><span class="sxs-lookup"><span data-stu-id="4aac0-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="4aac0-168">[Tutorial sobre VoIP com aplicativos Node.js][voipnode]</span><span class="sxs-lookup"><span data-stu-id="4aac0-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="4aac0-169">[Votr – um aplicativo de votação SMS em tempo real com node.js e CouchDB (três partes)][votr]</span><span class="sxs-lookup"><span data-stu-id="4aac0-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="4aac0-170">[Programação do par no navegador de saudação com Node. js][pair]</span><span class="sxs-lookup"><span data-stu-id="4aac0-170">[Pair programming in hello browser with node.js][pair]</span></span>

<span data-ttu-id="4aac0-171">Esperamos que você aprecie escrever com o node.js e o Twilio no Azure!</span><span class="sxs-lookup"><span data-stu-id="4aac0-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

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
