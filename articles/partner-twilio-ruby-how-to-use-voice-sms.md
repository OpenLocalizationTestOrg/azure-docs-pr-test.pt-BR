---
title: aaaHow tooUse Twilio para voz e SMS (Ruby) | Microsoft Docs
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Exemplos de códigos escritos em Ruby."
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
ms.openlocfilehash: aca5ccb4663ff03c9c1f39c848469415f06dfb45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="a8e6c-104">Como tooUse Twilio para recursos de SMS em Ruby e voz</span><span class="sxs-lookup"><span data-stu-id="a8e6c-104">How tooUse Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="a8e6c-105">Este guia demonstra como tooperform as tarefas de programação comuns com hello Twilio API de serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="a8e6c-106">cenários de saudação abordados incluem fazer uma chamada telefônica e enviar uma mensagem do serviço SMS (Short Message).</span><span class="sxs-lookup"><span data-stu-id="a8e6c-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="a8e6c-107">Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte Olá [próximas etapas](#NextSteps) seção.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="a8e6c-108"><a id="WhatIs"></a>O que é Twilio?</span><span class="sxs-lookup"><span data-stu-id="a8e6c-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="a8e6c-109">Twilio é uma API de serviço web de telefonia que permite que você use seus idiomas de web existente e voz de toobuild habilidades e aplicativos de SMS.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="a8e6c-110">O Twilio é um serviço de terceiro (não é um recurso do Azure e não é um produto da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="a8e6c-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="a8e6c-111">**Voz Twilio** permite que seus aplicativos toomake e receber chamadas telefônicas.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="a8e6c-112">**Twilio SMS** permite que seus aplicativos toomake e receber mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="a8e6c-113">**Clientes do Twilio** permite comunicação por voz tooenable usando conexões da Internet existentes, incluindo conexões móveis que seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="a8e6c-114"><a id="Pricing"></a>Preços e ofertas especiais da Twilio</span><span class="sxs-lookup"><span data-stu-id="a8e6c-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="a8e6c-115">A informações sobre os preços do Twilio estão disponíveis em [Preços do Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="a8e6c-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="a8e6c-116">Os clientes do Azure recebem uma [oferta especial][special_offer]: um crédito de 1.000 mensagens de texto gratuitas ou 1.000 minutos de entrada.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="a8e6c-117">toosign para esta oferta ou obter mais informações, visite [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="a8e6c-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="a8e6c-118"><a id="Concepts"></a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="a8e6c-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="a8e6c-119">Olá Twilio API é uma API RESTful que fornece funcionalidade SMS e voz para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="a8e6c-120">As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="a8e6c-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="a8e6c-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="a8e6c-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="a8e6c-122">TwiML é um conjunto de instruções baseadas em XML que informam o Twilio como tooprocess uma chamada ou SMS.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-122">TwiML is a set of XML-based instructions that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="a8e6c-123">Por exemplo, Olá TwiML a seguir seria converter o texto de saudação **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-123">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="a8e6c-124">Todos os documentos do TwiML têm `<Response>` como seu elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="a8e6c-125">A partir daí, você deve usar comportamento de saudação do Twilio verbos toodefine do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-125">From there, you use Twilio Verbs toodefine hello behavior of your application.</span></span>

### <span data-ttu-id="a8e6c-126"><a id="Verbs"></a>Verbos do TwiML</span><span class="sxs-lookup"><span data-stu-id="a8e6c-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="a8e6c-127">Twilio verbos são marcas XML que informam o Twilio muito**fazer**.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-127">Twilio Verbs are XML tags that tell Twilio what too**do**.</span></span> <span data-ttu-id="a8e6c-128">Por exemplo, Olá  **&lt;diga&gt;**  verbo instrui Twilio tooaudibly entregar uma mensagem em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-128">For example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span> 

<span data-ttu-id="a8e6c-129">a seguir Olá é uma lista de verbos do Twilio.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-129">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="a8e6c-130">**&lt;Discagem&gt;**: conecta-se o telefone de tooanother Olá chamador.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-130">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="a8e6c-131">**&lt;Coletar&gt;**: coleta dígitos numéricos inseridos no teclado numérico do telefone hello.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-131">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="a8e6c-132">**&lt;Hangup&gt;**: termina uma chamada.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="a8e6c-133">**&lt;Play&gt;**: reproduz um arquivo de áudio.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="a8e6c-134">**&lt;Pause&gt;**: espera silenciosamente por um número especificado de segundos.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="a8e6c-135">**&lt;Registro&gt;**: registra a voz do chamador hello e retorna uma URL de um arquivo que contém a gravação da saudação.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-135">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="a8e6c-136">**&lt;Redirecionar&gt;**: transfere o controle de uma chamada ou SMS toohello TwiML em uma URL diferente.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="a8e6c-137">**&lt;Rejeitar&gt;**: rejeita uma entrada chamar tooyour Twilio número sem cobrança você</span><span class="sxs-lookup"><span data-stu-id="a8e6c-137">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="a8e6c-138">**&lt;Digamos que&gt;**: converte texto toospeech que é feita em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-138">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="a8e6c-139">**&lt;Sms&gt;**: envia uma mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="a8e6c-140">Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="a8e6c-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="a8e6c-141">Para obter informações adicionais sobre Olá Twilio API, consulte [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="a8e6c-141">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="a8e6c-142"><a id="CreateAccount"></a>Criar uma conta na Twilio</span><span class="sxs-lookup"><span data-stu-id="a8e6c-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="a8e6c-143">Quando você estiver pronto tooget uma conta do Twilio, inscreva-se em [tente Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="a8e6c-143">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="a8e6c-144">Você pode começar com uma conta gratuita e atualizá-la depois.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="a8e6c-145">Ao se inscrever em uma conta do Twilio, você receberá um número de telefone gratuito para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="a8e6c-146">Você também receberá uma SID de conta e um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="a8e6c-147">Ambos serão chamadas à API do Twilio toomake necessários.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-147">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="a8e6c-148">tooprevent não autorizado acessar conta tooyour, mantenha o token de autenticação segura.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-148">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="a8e6c-149">O SID da conta e o token de autenticação são visíveis no hello [página de conta do Twilio][twilio_account], no hello campos rotulados **SID da conta** e **TOKEN de autenticação** , respectivamente.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-149">Your account SID and auth token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="a8e6c-150"><a id="VerifyPhoneNumbers"></a>Verificar números telefônicos</span><span class="sxs-lookup"><span data-stu-id="a8e6c-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="a8e6c-151">O número de toohello adição que você receber do Twilio, você também pode verificar números que você controle (ou seja, seu telefone celular ou home número de telefone) para uso em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-151">In addition toohello number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="a8e6c-152">Para obter informações sobre como tooverify um número de telefone, consulte [gerenciar números][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="a8e6c-152">For information on how tooverify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="a8e6c-153"><a id="create_app"></a>Criar um Aplicativo em Ruby</span><span class="sxs-lookup"><span data-stu-id="a8e6c-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="a8e6c-154">Um aplicativo Ruby que usa o serviço do Twilio hello e está em execução no Azure não é diferente de qualquer outro aplicativo Ruby que usa o serviço do Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-154">A Ruby application that uses hello Twilio service and is running in Azure is no different than any other Ruby application that uses hello Twilio service.</span></span> <span data-ttu-id="a8e6c-155">Enquanto Twilio serviços são RESTful e podem ser chamados de Ruby de várias maneiras, este artigo se concentrará em como os serviços de toouse Twilio com [biblioteca auxiliar da Twilio para Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="a8e6c-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how toouse Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="a8e6c-156">Primeiro, [configuração de uma nova VM do Linux Azure] [ azure_vm_setup] tooact como um host para seu novo aplicativo web Ruby.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-156">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Ruby web application.</span></span> <span data-ttu-id="a8e6c-157">Ignore as etapas de saudação que envolvem a criação de saudação de um aplicativo de trilhos, apenas Olá configuração VM.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-157">Ignore hello steps involving hello creation of a Rails app, just set-up hello VM.</span></span> <span data-ttu-id="a8e6c-158">Certifique-se de criar um ponto de extremidade com uma porta externa 80 e uma porta interna 5000.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="a8e6c-159">Nos exemplos de saudação abaixo, vamos usar [Sinatra][sinatra], uma estrutura muito simples da web para Ruby.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-159">In hello examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="a8e6c-160">Mas você pode usar biblioteca auxiliar da saudação Twilio para Ruby com qualquer outra estrutura de web, inclusive Ruby nos trilhos.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-160">But you can certainly use hello Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="a8e6c-161">Use SSH na sua nova VM e crie um diretório para o seu novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="a8e6c-162">Dentro desse diretório, crie um arquivo chamado hello Gemfile e cópia de código a seguir nele:</span><span class="sxs-lookup"><span data-stu-id="a8e6c-162">Inside that directory, create a file called Gemfile and copy hello following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="a8e6c-163">Na linha de comando Olá executar `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-163">On hello command line run `bundle install`.</span></span> <span data-ttu-id="a8e6c-164">Isso irá instalar dependências de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-164">This will install hello dependencies above.</span></span> <span data-ttu-id="a8e6c-165">Em seguida, crie um arquivo chamado `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="a8e6c-166">Isso será onde reside o código de saudação para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-166">This will be where hello code for your web app lives.</span></span> <span data-ttu-id="a8e6c-167">Cole Olá código a seguir nele:</span><span class="sxs-lookup"><span data-stu-id="a8e6c-167">Paste hello following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="a8e6c-168">Agora você deve ser o comando de Olá Olá capaz de executar `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-168">At this point you should be able hello run hello command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="a8e6c-169">Isso vai girar um servidor Web pequeno na porta 5000.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="a8e6c-170">Você deve ser capaz de toobrowse toothis aplicativo em seu navegador visitando o URL Olá você configuração para sua VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-170">You should be able toobrowse toothis app in your browser by visiting hello URL you set-up for your Azure VM.</span></span> <span data-ttu-id="a8e6c-171">Depois que você pode acessar seu aplicativo web no navegador hello, você está pronto toostart compilar um aplicativo Twilio.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-171">Once you can reach your web app in hello browser, you're ready toostart building a Twilio app.</span></span>

## <span data-ttu-id="a8e6c-172"><a id="configure_app"></a>Configurar seu aplicativo tooUse Twilio</span><span class="sxs-lookup"><span data-stu-id="a8e6c-172"><a id="configure_app"></a>Configure Your Application tooUse Twilio</span></span>
<span data-ttu-id="a8e6c-173">Você pode configurar sua biblioteca de Twilio web app toouse Olá atualizando seu `Gemfile` tooinclude esta linha:</span><span class="sxs-lookup"><span data-stu-id="a8e6c-173">You can configure your web app toouse hello Twilio library by updating your `Gemfile` tooinclude this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="a8e6c-174">Na linha de comando hello, execute `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-174">On hello command line, run `bundle install`.</span></span> <span data-ttu-id="a8e6c-175">Agora, abra `web.rb` e esta linha na parte superior do hello, incluindo:</span><span class="sxs-lookup"><span data-stu-id="a8e6c-175">Now open `web.rb` and including this line at hello top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="a8e6c-176">Você está agora todos os conjunto de biblioteca auxiliar da toouse Olá Twilio para Ruby em seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-176">You're now all set toouse hello Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="a8e6c-177"><a id="howto_make_call"></a>Como fazer uma chamada externa</span><span class="sxs-lookup"><span data-stu-id="a8e6c-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="a8e6c-178">Olá a seguir mostra como chamar toomake uma saída.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-178">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="a8e6c-179">Conceitos principais incluem o uso de biblioteca auxiliar da saudação Twilio para Ruby toomake chamadas à API REST e TwiML de renderização.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-179">Key concepts include using hello Twilio helper library for Ruby toomake REST API calls and rendering TwiML.</span></span> <span data-ttu-id="a8e6c-180">Substitua os valores para Olá **de** e **para** números de telefone e certifique-se de que você verifique Olá **de** número de telefone para o seu código de saudação do Twilio conta toorunning anterior.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-180">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

<span data-ttu-id="a8e6c-181">Adicione esta função muito`web.md`:</span><span class="sxs-lookup"><span data-stu-id="a8e6c-181">Add this function too`web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # hello number of hello phone receiving call.
    too= "NNNNNNNNNNN";

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create hello call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make hello call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="a8e6c-182">Se você abrir o `http://yourdomain.cloudapp.net/make_call` em um navegador, que irá disparar Olá chamada toohello Twilio API toomake Olá telefonema.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger hello call toohello Twilio API toomake hello phone call.</span></span> <span data-ttu-id="a8e6c-183">Olá dois primeiros parâmetros `client.account.calls.create` são bem auto-explicativo: Olá número Olá chamada é `from` e Olá número Olá chamada é `to`.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-183">hello first two parameters in `client.account.calls.create` are fairly self-explanatory: hello number hello call is `from` and hello number hello call is `to`.</span></span> 

<span data-ttu-id="a8e6c-184">Olá terceiro parâmetro (`url`) é URL Olá que Twilio solicitações tooget instruções sobre qual toodo quando chamada hello está conectada.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-184">hello third parameter (`url`) is hello URL that Twilio requests tooget instructions on what toodo once hello call is connected.</span></span> <span data-ttu-id="a8e6c-185">Nesse caso, configuração de uma URL (`http://yourdomain.cloudapp.net`) que retorna um documento TwiML simples e usa Olá `<Say>` toodo verbo Olá alguns texto em fala e fale "Hello macaco" toohello receptor da chamada.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses hello `<Say>` verb toodo some text-to-speech and say "Hello Monkey" toohello person recieving hello call.</span></span>

## <span data-ttu-id="a8e6c-186"><a id="howto_recieve_sms"></a>Como receber uma mensagem SMS</span><span class="sxs-lookup"><span data-stu-id="a8e6c-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="a8e6c-187">No exemplo anterior de saudação é iniciada uma **saída** chamada telefônica.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-187">In hello previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="a8e6c-188">Esse tempo, vamos usar o número de telefone de saudação Twilio nos forneceu durante a inscrição tooprocess um **entrada** mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-188">This time, let's use hello phone number that Twilio gave us during sign-up tooprocess an **incoming** SMS message.</span></span>

<span data-ttu-id="a8e6c-189">Primeiro, logon tooyour [Twilio painel][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="a8e6c-189">First, log-in tooyour [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="a8e6c-190">Clique em "Números" na navegação superior hello e em seguida, clique em Olá número Twilio que foram fornecidos.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-190">Click on "Numbers" in hello top nav and then click on hello Twilio number you were provided.</span></span> <span data-ttu-id="a8e6c-191">Você verá dois URLs que podem ser configurados.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="a8e6c-192">Um URL de solicitação da voz e de SMS.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="a8e6c-193">Esses são URLs Olá Twilio chamadas sempre que uma chamada é feita ou um SMS é enviado tooyour número.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-193">These are hello URLs that Twilio calls whenever a phone call is made or an SMS is sent tooyour number.</span></span> <span data-ttu-id="a8e6c-194">Olá URLs também são conhecidos como "ganchos web".</span><span class="sxs-lookup"><span data-stu-id="a8e6c-194">hello URLs are also known as "web hooks".</span></span>

<span data-ttu-id="a8e6c-195">Gostaríamos tooprocess recebimento de mensagens SMS, vamos atualizar Olá URL muito`http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-195">We would like tooprocess incoming SMS messages, so let's update hello URL too`http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="a8e6c-196">Vá em frente e clique em Salvar alterações final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-196">Go ahead and click Save Changes at hello bottom of hello page.</span></span> <span data-ttu-id="a8e6c-197">Agora, voltando no `web.rb` programa vamos toohandle nosso aplicativo isso:</span><span class="sxs-lookup"><span data-stu-id="a8e6c-197">Now, back in `web.rb` let's program our application toohandle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="a8e6c-198">Depois de fazer a alteração de saudação, verifique toore-start-se de que seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-198">After making hello change, make sure toore-start your web app.</span></span> <span data-ttu-id="a8e6c-199">Agora, retire o seu telefone e enviar um SMS tooyour número Twilio.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-199">Now, take out your phone and send an SMS tooyour Twilio number.</span></span> <span data-ttu-id="a8e6c-200">Imediatamente, você deve obter uma resposta SMS que diz "Ei, agradecemos ping Olá!</span><span class="sxs-lookup"><span data-stu-id="a8e6c-200">You should promptly get an SMS response that says "Hey, thanks for hello ping!</span></span> <span data-ttu-id="a8e6c-201">O Twilio e o Azure são demais!".</span><span class="sxs-lookup"><span data-stu-id="a8e6c-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="a8e6c-202"><a id="additional_services"></a>Como Usar os Serviços Adicionais do Twilio</span><span class="sxs-lookup"><span data-stu-id="a8e6c-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="a8e6c-203">Além disso toohello exemplos mostrados aqui, que twilio oferece APIs baseado na web que você pode usar uma funcionalidade adicional Twilio tooleverage do aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e6c-203">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="a8e6c-204">Para obter detalhes completos, consulte Olá [documentação da API do Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="a8e6c-204">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="a8e6c-205"><a id="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8e6c-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="a8e6c-206">Agora que você aprendeu as Noções básicas sobre Olá Olá Twilio serviço, siga essas toolearn links mais:</span><span class="sxs-lookup"><span data-stu-id="a8e6c-206">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="a8e6c-207">[Diretrizes de segurança do Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="a8e6c-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="a8e6c-208">[Código de Exemplo e Procedimentos do Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="a8e6c-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="a8e6c-209">[Tutoriais do Guia de início rápido do Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="a8e6c-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="a8e6c-210">[Twilio no GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="a8e6c-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="a8e6c-211">[Fale tooTwilio suporte][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="a8e6c-211">[Talk tooTwilio Support][twilio_support]</span></span>

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
