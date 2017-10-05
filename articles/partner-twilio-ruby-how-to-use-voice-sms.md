---
title: Como Usar o Twilio para Voz e SMS (Ruby) | Microsoft Docs
description: "Saiba como fazer uma chamada telefônica e enviar uma mensagem SMS com o serviço de API do Twilio no Azure. Exemplos de códigos escritos em Ruby."
services: 
documentationcenter: ruby
author: devinrader
manager: twilio
editor: 
ms.assetid: 60e512f6-fa47-47c0-aedc-f19bb72a1158
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 11/25/2014
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 69e50e7fe0e1f302e96c309878b8dea6869dff4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="b9180-104">Como usar o Twilio para recursos de voz e SMS no Ruby</span><span class="sxs-lookup"><span data-stu-id="b9180-104">How to Use Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="b9180-105">Este guia demonstra como executar tarefas comuns de programação com o serviço de API do Twilio no Azure.</span><span class="sxs-lookup"><span data-stu-id="b9180-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="b9180-106">Os cenários abrangidos incluem fazer uma chamada telefônica e enviar uma mensagem serviço de mensagem curta (SMS).</span><span class="sxs-lookup"><span data-stu-id="b9180-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="b9180-107">Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte a seção [Próximas etapas](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="b9180-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="b9180-108"><a id="WhatIs"></a>O que é Twilio?</span><span class="sxs-lookup"><span data-stu-id="b9180-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="b9180-109">Twilio é uma API do serviço Web de telefonia que permite usar os idiomas e as habilidades existentes de Web para criar aplicativos de voz e SMS.</span><span class="sxs-lookup"><span data-stu-id="b9180-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="b9180-110">O Twilio é um serviço de terceiro (não é um recurso do Azure e não é um produto da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="b9180-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="b9180-111">**Twilio Voice** permite que seus aplicativos façam e recebam chamadas telefônicas.</span><span class="sxs-lookup"><span data-stu-id="b9180-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="b9180-112">**Twilio SMS** permite que seus aplicativos façam e recebam mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="b9180-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="b9180-113">**Twilio Cliente** permite que seus aplicativos habilitem a comunicação de voz usando as conexões existentes com a Internet, incluindo conexões para celular.</span><span class="sxs-lookup"><span data-stu-id="b9180-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="b9180-114"><a id="Pricing"></a>Preços e ofertas especiais da Twilio</span><span class="sxs-lookup"><span data-stu-id="b9180-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="b9180-115">A informações sobre os preços do Twilio estão disponíveis em [Preços do Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="b9180-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="b9180-116">Os clientes do Azure recebem uma [oferta especial][special_offer]: um crédito de 1.000 mensagens de texto gratuitas ou 1.000 minutos de entrada.</span><span class="sxs-lookup"><span data-stu-id="b9180-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="b9180-117">Para se inscrever nessa oferta ou obter mais informações, visite [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="b9180-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="b9180-118"><a id="Concepts"></a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="b9180-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="b9180-119">A API do Twilio é uma API RESTful que fornece os recursos de voz e SMS para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b9180-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="b9180-120">As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="b9180-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="b9180-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="b9180-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="b9180-122">TwiML é um conjunto de instruções em XML que informam o Twilio como processar uma chamada ou SMS.</span><span class="sxs-lookup"><span data-stu-id="b9180-122">TwiML is a set of XML-based instructions that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="b9180-123">Por exemplo, o seguinte TwiML converteria a mensagem **Olá, mundo** em fala.</span><span class="sxs-lookup"><span data-stu-id="b9180-123">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="b9180-124">Todos os documentos do TwiML têm `<Response>` como seu elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="b9180-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="b9180-125">Por meio disso, você usará os verbos do Twilio para definir o comportamento do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9180-125">From there, you use Twilio Verbs to define the behavior of your application.</span></span>

### <span data-ttu-id="b9180-126"><a id="Verbs"></a>Verbos do TwiML</span><span class="sxs-lookup"><span data-stu-id="b9180-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="b9180-127">Os verbos do Twilio são marcas XML que dizem ao Twilio o que **fazer**.</span><span class="sxs-lookup"><span data-stu-id="b9180-127">Twilio Verbs are XML tags that tell Twilio what to **do**.</span></span> <span data-ttu-id="b9180-128">Por exemplo, o verbo **&lt;Dizer&gt;** instrui o Twilio para entregar de forma audível uma mensagem em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="b9180-128">For example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span> 

<span data-ttu-id="b9180-129">A seguir está uma lista de verbos do Twilio.</span><span class="sxs-lookup"><span data-stu-id="b9180-129">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="b9180-130">**&lt;Dial&gt;**: conecta o chamador com outro telefone.</span><span class="sxs-lookup"><span data-stu-id="b9180-130">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="b9180-131">**&lt;Gather&gt;**: coleta os dígitos numéricos inseridos no teclado numérico de telefone.</span><span class="sxs-lookup"><span data-stu-id="b9180-131">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="b9180-132">**&lt;Hangup&gt;**: termina uma chamada.</span><span class="sxs-lookup"><span data-stu-id="b9180-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="b9180-133">**&lt;Play&gt;**: reproduz um arquivo de áudio.</span><span class="sxs-lookup"><span data-stu-id="b9180-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="b9180-134">**&lt;Pause&gt;**: espera silenciosamente por um número especificado de segundos.</span><span class="sxs-lookup"><span data-stu-id="b9180-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="b9180-135">**&lt;Record&gt;**: grava a voz do chamador e retorna uma URL de um arquivo que contém a gravação.</span><span class="sxs-lookup"><span data-stu-id="b9180-135">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="b9180-136">**&lt;Redirect&gt;**: transfere o controle de uma chamada ou SMS para TwiML em um URL diferente.</span><span class="sxs-lookup"><span data-stu-id="b9180-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="b9180-137">**&lt;Reject&gt;**: rejeita uma chamada recebida para o número do Twilio sem cobrar você</span><span class="sxs-lookup"><span data-stu-id="b9180-137">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="b9180-138">**&lt;Say&gt;**: converte o texto em fala que é executada em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="b9180-138">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="b9180-139">**&lt;Sms&gt;**: envia uma mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="b9180-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="b9180-140">Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="b9180-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="b9180-141">Para obter mais informações sobre a API do Twilio, consulte [API do Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="b9180-141">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="b9180-142"><a id="CreateAccount"></a>Criar uma conta na Twilio</span><span class="sxs-lookup"><span data-stu-id="b9180-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="b9180-143">Quando estiver pronto para obter uma conta do Twilio, inscreva-se em [Experimentar o Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="b9180-143">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="b9180-144">Você pode começar com uma conta gratuita e atualizá-la depois.</span><span class="sxs-lookup"><span data-stu-id="b9180-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="b9180-145">Ao se inscrever em uma conta do Twilio, você receberá um número de telefone gratuito para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9180-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="b9180-146">Você também receberá uma SID de conta e um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="b9180-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="b9180-147">Eles serão necessários para fazer chamadas de API do Twilio.</span><span class="sxs-lookup"><span data-stu-id="b9180-147">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="b9180-148">Para evitar o acesso não autorizado em sua conta, mantenha o token da autenticação seguro.</span><span class="sxs-lookup"><span data-stu-id="b9180-148">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="b9180-149">A ID de sua conta e o token de autenticação estão visíveis na [página da conta do Twilio][twilio_account], nos campos rotulados **ACCOUNT SID** e **AUTH TOKEN**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="b9180-149">Your account SID and auth token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="b9180-150"><a id="VerifyPhoneNumbers"></a>Verificar números telefônicos</span><span class="sxs-lookup"><span data-stu-id="b9180-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="b9180-151">Além do número fornecido pelo Twilio, você também pode verificar os números que controla (isto é, seu número do telefone celular ou residencial) para uso em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b9180-151">In addition to the number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="b9180-152">Para obter informações sobre como verificar um número de telefone, consulte [Gerenciar Números][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="b9180-152">For information on how to verify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="b9180-153"><a id="create_app"></a>Criar um Aplicativo em Ruby</span><span class="sxs-lookup"><span data-stu-id="b9180-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="b9180-154">Um aplicativo Ruby que usa o serviço do Twilio e está em execução no Azure não é diferente de nenhum outro aplicativo Ruby que usa o serviço do Twilio.</span><span class="sxs-lookup"><span data-stu-id="b9180-154">A Ruby application that uses the Twilio service and is running in Azure is no different than any other Ruby application that uses the Twilio service.</span></span> <span data-ttu-id="b9180-155">Embora os serviços do Twilio sejam RESTful e possam ser chamados do Ruby de várias maneiras, este artigo se concentra em como usar esses serviços com a [biblioteca auxiliar do Twilio para Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="b9180-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how to use Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="b9180-156">Primeiro, [configure uma nova VM Linux do Azure][azure_vm_setup] para agir como um host para o novo aplicativo Web do Ruby.</span><span class="sxs-lookup"><span data-stu-id="b9180-156">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Ruby web application.</span></span> <span data-ttu-id="b9180-157">Ignore as etapas que envolvem a criação de um aplicativo do Rails, apenas configure a VM.</span><span class="sxs-lookup"><span data-stu-id="b9180-157">Ignore the steps involving the creation of a Rails app, just set-up the VM.</span></span> <span data-ttu-id="b9180-158">Certifique-se de criar um ponto de extremidade com uma porta externa 80 e uma porta interna 5000.</span><span class="sxs-lookup"><span data-stu-id="b9180-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="b9180-159">Nos exemplos a seguir, usaremos o [Sinatra][sinatra], uma estrutura da web muito simples para Ruby.</span><span class="sxs-lookup"><span data-stu-id="b9180-159">In the examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="b9180-160">Mas você certamente pode usar a biblioteca do auxiliar do Twilio para Ruby com qualquer outra estrutura da web, incluindo o Ruby on Rails.</span><span class="sxs-lookup"><span data-stu-id="b9180-160">But you can certainly use the Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="b9180-161">Use SSH na sua nova VM e crie um diretório para o seu novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9180-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="b9180-162">Dentro desse diretório, crie um arquivo denominado Gemfile e copie o código a seguir dentro dele:</span><span class="sxs-lookup"><span data-stu-id="b9180-162">Inside that directory, create a file called Gemfile and copy the following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="b9180-163">Na linha de comando, execute `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="b9180-163">On the command line run `bundle install`.</span></span> <span data-ttu-id="b9180-164">Isso instalará as dependências acima.</span><span class="sxs-lookup"><span data-stu-id="b9180-164">This will install the dependencies above.</span></span> <span data-ttu-id="b9180-165">Em seguida, crie um arquivo chamado `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="b9180-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="b9180-166">Ele será a localização do código do seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="b9180-166">This will be where the code for your web app lives.</span></span> <span data-ttu-id="b9180-167">Cole o código a seguir dentro dele:</span><span class="sxs-lookup"><span data-stu-id="b9180-167">Paste the following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="b9180-168">A esta altura você deve ser capaz de executar o comando `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="b9180-168">At this point you should be able the run the command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="b9180-169">Isso vai girar um servidor Web pequeno na porta 5000.</span><span class="sxs-lookup"><span data-stu-id="b9180-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="b9180-170">Você poderá acessar esse aplicativo em seu navegador, visitando a URL configurada para sua VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9180-170">You should be able to browse to this app in your browser by visiting the URL you set-up for your Azure VM.</span></span> <span data-ttu-id="b9180-171">Depois que conseguir acessar seu aplicativo web no navegador, você estará pronto para iniciar a compilação de um aplicativo do Twilio.</span><span class="sxs-lookup"><span data-stu-id="b9180-171">Once you can reach your web app in the browser, you're ready to start building a Twilio app.</span></span>

## <span data-ttu-id="b9180-172"><a id="configure_app"></a>Configurar seu aplicativo para usar o Twilio</span><span class="sxs-lookup"><span data-stu-id="b9180-172"><a id="configure_app"></a>Configure Your Application to Use Twilio</span></span>
<span data-ttu-id="b9180-173">Você pode configurar seu aplicativo web para usar a biblioteca Twilio atualizando o `Gemfile` para incluir esta linha:</span><span class="sxs-lookup"><span data-stu-id="b9180-173">You can configure your web app to use the Twilio library by updating your `Gemfile` to include this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="b9180-174">Na linha de comando, execute `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="b9180-174">On the command line, run `bundle install`.</span></span> <span data-ttu-id="b9180-175">Agora, abra `web.rb` e inclua esta linha na parte superior:</span><span class="sxs-lookup"><span data-stu-id="b9180-175">Now open `web.rb` and including this line at the top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="b9180-176">Você está configurado para usar a biblioteca do auxiliar do Twilio para Ruby em seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="b9180-176">You're now all set to use the Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="b9180-177"><a id="howto_make_call"></a>Como fazer uma chamada externa</span><span class="sxs-lookup"><span data-stu-id="b9180-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="b9180-178">A seguir você verá como fazer uma chamada de saída.</span><span class="sxs-lookup"><span data-stu-id="b9180-178">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="b9180-179">Os conceitos principais incluem usar a biblioteca do auxiliar do Twilio para o Ruby para fazer chamadas de API REST e renderizar o TwiML.</span><span class="sxs-lookup"><span data-stu-id="b9180-179">Key concepts include using the Twilio helper library for Ruby to make REST API calls and rendering TwiML.</span></span> <span data-ttu-id="b9180-180">Substitua os valores para os números de telefone **De** e **Para** e verifique o número de telefone **De** da sua conta do Twilio antes de executar o código.</span><span class="sxs-lookup"><span data-stu-id="b9180-180">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

<span data-ttu-id="b9180-181">Adicione esta função a `web.md`:</span><span class="sxs-lookup"><span data-stu-id="b9180-181">Add this function to `web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # The number of the phone receiving call.
    to = "NNNNNNNNNNN";

    # Use the Twilio-provided site for the TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create the call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make the call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="b9180-182">Se você reabrir `http://yourdomain.cloudapp.net/make_call` em um navegador, isso disparará a chamada de API do Twilio para fazer a chamada telefônica.</span><span class="sxs-lookup"><span data-stu-id="b9180-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger the call to the Twilio API to make the phone call.</span></span> <span data-ttu-id="b9180-183">Os dois primeiros parâmetros em `client.account.calls.create` são auto-explicativos: o número da chamada é `from` e o número de chamada é `to`.</span><span class="sxs-lookup"><span data-stu-id="b9180-183">The first two parameters in `client.account.calls.create` are fairly self-explanatory: the number the call is `from` and the number the call is `to`.</span></span> 

<span data-ttu-id="b9180-184">O terceiro parâmetro (`url`) é a URL solicitada pelo Twilio para obter instruções sobre o que fazer quando a chamada estiver conectada.</span><span class="sxs-lookup"><span data-stu-id="b9180-184">The third parameter (`url`) is the URL that Twilio requests to get instructions on what to do once the call is connected.</span></span> <span data-ttu-id="b9180-185">Nesse caso, configuramos uma URL (`http://yourdomain.cloudapp.net`) que retorna um documento simples de TwiML e usa o verbo `<Say>` para fazer uma conversão de texto em fala e dizer "Olá" à pessoa que estiver recebendo a chamada.</span><span class="sxs-lookup"><span data-stu-id="b9180-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses the `<Say>` verb to do some text-to-speech and say "Hello Monkey" to the person recieving the call.</span></span>

## <span data-ttu-id="b9180-186"><a id="howto_recieve_sms"></a>Como receber uma mensagem SMS</span><span class="sxs-lookup"><span data-stu-id="b9180-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="b9180-187">No exemplo anterior, iniciamos uma chamada telefônica de **saída** .</span><span class="sxs-lookup"><span data-stu-id="b9180-187">In the previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="b9180-188">Agora, vamos usar o número de telefone que o Twilio nos forneceu durante a inscrição para processar uma mensagem SMS de **entrada** .</span><span class="sxs-lookup"><span data-stu-id="b9180-188">This time, let's use the phone number that Twilio gave us during sign-up to process an **incoming** SMS message.</span></span>

<span data-ttu-id="b9180-189">Primeiro, faça logon no seu [painel do Twilio][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="b9180-189">First, log-in to your [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="b9180-190">Clique em "Número" no navegador superior e clique no número do Twilio fornecido.</span><span class="sxs-lookup"><span data-stu-id="b9180-190">Click on "Numbers" in the top nav and then click on the Twilio number you were provided.</span></span> <span data-ttu-id="b9180-191">Você verá dois URLs que podem ser configurados.</span><span class="sxs-lookup"><span data-stu-id="b9180-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="b9180-192">Um URL de solicitação da voz e de SMS.</span><span class="sxs-lookup"><span data-stu-id="b9180-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="b9180-193">Estes são os URLs que o Twilio chama sempre que uma chamada telefônica é feita ou um SMS é enviado ao seu número.</span><span class="sxs-lookup"><span data-stu-id="b9180-193">These are the URLs that Twilio calls whenever a phone call is made or an SMS is sent to your number.</span></span> <span data-ttu-id="b9180-194">As URLs também são conhecidas como "ganchos da web".</span><span class="sxs-lookup"><span data-stu-id="b9180-194">The URLs are also known as "web hooks".</span></span>

<span data-ttu-id="b9180-195">Gostaríamos de processar mensagens SMS de entrada, portanto, vamos atualizar a URL para `http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="b9180-195">We would like to process incoming SMS messages, so let's update the URL to `http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="b9180-196">Prossiga e clique em Salvar alterações na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="b9180-196">Go ahead and click Save Changes at the bottom of the page.</span></span> <span data-ttu-id="b9180-197">Agora, de volta em `web.rb` vamos programar o aplicativo para lidar com isso:</span><span class="sxs-lookup"><span data-stu-id="b9180-197">Now, back in `web.rb` let's program our application to handle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for the ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="b9180-198">Após fazer a alteração, certifique-se de reiniciar o aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="b9180-198">After making the change, make sure to re-start your web app.</span></span> <span data-ttu-id="b9180-199">Agora, remova o telefone e envie um SMS ao número do Twilio.</span><span class="sxs-lookup"><span data-stu-id="b9180-199">Now, take out your phone and send an SMS to your Twilio number.</span></span> <span data-ttu-id="b9180-200">Você deve obter imediatamente uma resposta de SMS que informa "Oi, obrigado pelo ping!</span><span class="sxs-lookup"><span data-stu-id="b9180-200">You should promptly get an SMS response that says "Hey, thanks for the ping!</span></span> <span data-ttu-id="b9180-201">O Twilio e o Azure são demais!".</span><span class="sxs-lookup"><span data-stu-id="b9180-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="b9180-202"><a id="additional_services"></a>Como Usar os Serviços Adicionais do Twilio</span><span class="sxs-lookup"><span data-stu-id="b9180-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="b9180-203">Além dos exemplos mostrados aqui, o Twilio oferece APIs baseadas na Web que podem ser usadas para aproveitar a funcionalidade adicional do Twilio do aplicativo Azure.</span><span class="sxs-lookup"><span data-stu-id="b9180-203">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="b9180-204">Para obter detalhes completos, consulte a [Documentação da API do Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="b9180-204">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="b9180-205"><a id="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9180-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="b9180-206">Agora que você já conhece os princípios do serviço Twilio, acesse estes links para saber mais:</span><span class="sxs-lookup"><span data-stu-id="b9180-206">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="b9180-207">[Diretrizes de segurança do Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="b9180-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="b9180-208">[Código de Exemplo e Procedimentos do Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="b9180-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="b9180-209">[Tutoriais do Guia de início rápido do Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="b9180-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="b9180-210">[Twilio no GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="b9180-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="b9180-211">[Fale com o suporte do Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="b9180-211">[Talk to Twilio Support][twilio_support]</span></span>

[twilio_ruby]: https://www.twilio.com/docs/ruby/install





[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
[sinatra]: http://www.sinatrarb.com/
[azure_vm_setup]: http://www.windowsazure.com/develop/ruby/tutorials/web-app-with-linux-vm/
