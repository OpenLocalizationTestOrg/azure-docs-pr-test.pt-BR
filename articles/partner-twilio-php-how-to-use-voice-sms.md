---
title: aaaHow tooUse Twilio para voz e SMS (PHP) | Microsoft Docs
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Exemplos de código escritos em PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="00053-104">Como tooUse Twilio para recursos de SMS em PHP e voz</span><span class="sxs-lookup"><span data-stu-id="00053-104">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="00053-105">Este guia demonstra como tooperform as tarefas de programação comuns com hello Twilio API de serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="00053-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="00053-106">cenários de saudação abordados incluem fazer uma chamada telefônica e enviar uma mensagem do serviço SMS (Short Message).</span><span class="sxs-lookup"><span data-stu-id="00053-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="00053-107">Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte Olá [próximas etapas](#NextSteps) seção.</span><span class="sxs-lookup"><span data-stu-id="00053-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="00053-108"><a id="WhatIs"></a>O que é Twilio?</span><span class="sxs-lookup"><span data-stu-id="00053-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="00053-109">Twilio é capacitam Olá futuro das comunicações de negócios, habilitar os desenvolvedores tooembed voice, VoIP e mensagens em aplicativos.</span><span class="sxs-lookup"><span data-stu-id="00053-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="00053-110">Eles virtualizam todos infraestrutura necessária em um ambiente baseado em nuvem, global, expô-lo por meio da plataforma Olá Twilio API de comunicação.</span><span class="sxs-lookup"><span data-stu-id="00053-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="00053-111">Os aplicativos são toobuild simple e escalonável.</span><span class="sxs-lookup"><span data-stu-id="00053-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="00053-112">Aproveite a flexibilidade com pagamento medida que vá preços e se beneficiar da confiabilidade da nuvem.</span><span class="sxs-lookup"><span data-stu-id="00053-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="00053-113">**Voz Twilio** permite que seus aplicativos toomake e receber chamadas telefônicas.</span><span class="sxs-lookup"><span data-stu-id="00053-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="00053-114">**Twilio SMS** permite que seu aplicativo toosend e receber mensagens de texto.</span><span class="sxs-lookup"><span data-stu-id="00053-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span> <span data-ttu-id="00053-115">**Clientes do Twilio** permite chamadas de VoIP toomake de qualquer telefone, tablet ou navegador e dá suporte a WebRTC.</span><span class="sxs-lookup"><span data-stu-id="00053-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="00053-116"><a id="Pricing"></a>Preços e ofertas especiais da Twilio</span><span class="sxs-lookup"><span data-stu-id="00053-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="00053-117">Os clientes do Azure recebem uma [oferta especial](http://www.twilio.com/azure): US$ 10 de cortesia de crédito da Twilio quando atualizam a sua conta da Twilio.</span><span class="sxs-lookup"><span data-stu-id="00053-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="00053-118">Esse crédito Twilio podem ser aplicadas tooany Twilio uso (US $10 crédito equivalente toosending até 1.000 mensagens SMS ou recebimento de too1000 minutos de voz, dependendo do local de saudação do seu destino de número e a mensagem ou chamada telefônica de entrada).</span><span class="sxs-lookup"><span data-stu-id="00053-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="00053-119">Resgate esse crédito da Twilio e faça uma introdução em: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="00053-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="00053-120">Twilio é um serviço flexível.</span><span class="sxs-lookup"><span data-stu-id="00053-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="00053-121">Não há nenhuma taxa de configuração e você pode fechar sua conta a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="00053-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="00053-122">Você pode encontrar mais detalhes em [Preços do Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="00053-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="00053-123"><a id="Concepts"></a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="00053-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="00053-124">Olá Twilio API é uma API RESTful que fornece funcionalidade SMS e voz para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="00053-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="00053-125">As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="00053-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="00053-126">Principais aspectos da saudação Twilio API são verbos do Twilio e Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="00053-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="00053-127"><a id="Verbs"></a>Verbos da Twilio</span><span class="sxs-lookup"><span data-stu-id="00053-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="00053-128">Olá API faz uso do Twilio verbos; Por exemplo, Olá  **&lt;diga&gt;**  verbo instrui Twilio tooaudibly entregar uma mensagem em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="00053-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="00053-129">a seguir Olá é uma lista de verbos do Twilio.</span><span class="sxs-lookup"><span data-stu-id="00053-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="00053-130">Saiba sobre Olá outros verbos e recursos por meio de [documentação de linguagem de marcação do Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="00053-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="00053-131">**&lt;Discagem&gt;**: conecta-se o telefone de tooanother Olá chamador.</span><span class="sxs-lookup"><span data-stu-id="00053-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="00053-132">**&lt;Coletar&gt;**: coleta dígitos numéricos inseridos no teclado numérico do telefone hello.</span><span class="sxs-lookup"><span data-stu-id="00053-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="00053-133">**&lt;Hangup&gt;**: termina uma chamada.</span><span class="sxs-lookup"><span data-stu-id="00053-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="00053-134">**&lt;Play&gt;**: reproduz um arquivo de áudio.</span><span class="sxs-lookup"><span data-stu-id="00053-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="00053-135">**&lt;Pause&gt;**: espera silenciosamente por um número especificado de segundos.</span><span class="sxs-lookup"><span data-stu-id="00053-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="00053-136">**&lt;Registro&gt;**: registra a voz do chamador hello e retorna uma URL de um arquivo que contém a gravação da saudação.</span><span class="sxs-lookup"><span data-stu-id="00053-136">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="00053-137">**&lt;Redirecionar&gt;**: transfere o controle de uma chamada ou SMS toohello TwiML em uma URL diferente.</span><span class="sxs-lookup"><span data-stu-id="00053-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="00053-138">**&lt;Rejeitar&gt;**: rejeita uma entrada chamar tooyour Twilio número sem cobrança você</span><span class="sxs-lookup"><span data-stu-id="00053-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="00053-139">**&lt;Digamos que&gt;**: converte texto toospeech que é feita em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="00053-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="00053-140">**&lt;Sms&gt;**: envia uma mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="00053-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="00053-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="00053-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="00053-142">TwiML é um conjunto de instruções baseadas em XML com base em verbos do Twilio Olá que informam o Twilio como tooprocess uma chamada ou SMS.</span><span class="sxs-lookup"><span data-stu-id="00053-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="00053-143">Por exemplo, Olá TwiML a seguir seria converter o texto de saudação **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="00053-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="00053-144">Quando a aplicativo chama hello Twilio API, um dos parâmetros de API de saudação é URL Olá retorna Olá TwiML resposta.</span><span class="sxs-lookup"><span data-stu-id="00053-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="00053-145">Para fins de desenvolvimento, você pode usar URLs fornecido Twilio tooprovide Olá TwiML as respostas usadas pelos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="00053-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="00053-146">Você também pode hospedar seus próprio respostas de TwiML URLs tooproduce hello e outra opção é Olá toouse **TwiMLResponse** objeto.</span><span class="sxs-lookup"><span data-stu-id="00053-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="00053-147">Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="00053-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="00053-148">Para obter informações adicionais sobre Olá Twilio API, consulte [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="00053-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="00053-149"><a id="CreateAccount"></a>Criar uma conta na Twilio</span><span class="sxs-lookup"><span data-stu-id="00053-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="00053-150">Quando você estiver pronto tooget uma conta do Twilio, inscreva-se em [tente Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="00053-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="00053-151">Você pode começar com uma conta gratuita e atualizá-la depois.</span><span class="sxs-lookup"><span data-stu-id="00053-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="00053-152">Quando você se inscrever para uma conta de Twilio, você receberá uma ID de conta e um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="00053-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="00053-153">Ambos serão chamadas à API do Twilio toomake necessários.</span><span class="sxs-lookup"><span data-stu-id="00053-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="00053-154">tooprevent não autorizado acessar conta tooyour, mantenha o token de autenticação segura.</span><span class="sxs-lookup"><span data-stu-id="00053-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="00053-155">Sua ID da conta e a autenticação token são visíveis no hello [página de conta do Twilio][twilio_account], no hello campos rotulados **SID da conta** e **TOKEN de autenticação**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="00053-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="00053-156"><a id="create_app"></a>Criar um aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="00053-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="00053-157">Um aplicativo PHP que usa o serviço do Twilio hello e está em execução no Azure não é diferente de qualquer outro aplicativo PHP que usa o serviço do Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="00053-157">A PHP application that uses hello Twilio service and is running in Azure is no different than any other PHP application that uses hello Twilio service.</span></span> <span data-ttu-id="00053-158">Enquanto o Twilio serviços são baseados em REST e podem ser chamados de PHP de várias maneiras, este artigo se concentrará em como os serviços de toouse Twilio com [Twilio biblioteca para PHP do GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="00053-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how toouse Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="00053-159">Para obter mais informações sobre como usar a biblioteca do Twilio Olá para PHP, consulte [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="00053-159">For more information about using hello Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="00053-160">Instruções detalhadas para criar e implantar um tooAzure de aplicativo do Twilio/PHP estão disponíveis em [como tooMake uma chamada telefônica usando o Twilio em um aplicativo PHP no Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="00053-160">Detailed instructions for building and deploying a Twilio/PHP application tooAzure are available at [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="00053-161"><a id="configure_app"></a>Configurar seu aplicativo tooUse Twilio bibliotecas</span><span class="sxs-lookup"><span data-stu-id="00053-161"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="00053-162">Você pode configurar sua biblioteca do aplicativo toouse Olá Twilio para PHP de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="00053-162">You can configure your application toouse hello Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="00053-163">Baixar a biblioteca do Twilio Olá para PHP do GitHub ([https://github.com/twilio/twilio-php][twilio_php]) e adicione Olá **serviços** aplicativo tooyour de diretório.</span><span class="sxs-lookup"><span data-stu-id="00053-163">Download hello Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add hello **Services** directory tooyour application.</span></span>
   
    <span data-ttu-id="00053-164">-OU-</span><span class="sxs-lookup"><span data-stu-id="00053-164">-OR-</span></span>
2. <span data-ttu-id="00053-165">Instale a biblioteca do Twilio Olá para PHP como um pacote de PERA.</span><span class="sxs-lookup"><span data-stu-id="00053-165">Install hello Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="00053-166">Ele pode ser instalado com hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="00053-166">It can be installed with hello following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="00053-167">Depois que você instalou a biblioteca do Twilio Olá para PHP, você pode adicionar uma **require_once** instrução na parte superior de saudação do seu PHP arquivos de biblioteca de saudação tooreference:</span><span class="sxs-lookup"><span data-stu-id="00053-167">Once you have installed hello Twilio library for PHP, you can then add a **require_once** statement at hello top of your PHP files tooreference hello library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="00053-168">Para obter mais informações, consulte [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="00053-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="00053-169"><a id="howto_make_call"></a>Como fazer uma chamada externa</span><span class="sxs-lookup"><span data-stu-id="00053-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="00053-170">Olá a seguir mostra como uma saída de toomake chamar usando Olá **Services_Twilio** classe.</span><span class="sxs-lookup"><span data-stu-id="00053-170">hello following shows how toomake an outgoing call using hello **Services_Twilio** class.</span></span> <span data-ttu-id="00053-171">Esse código também usa uma saudação do site fornecidos Twilio tooreturn resposta Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="00053-171">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="00053-172">Substitua os valores para Olá **de** e **para** números de telefone e certifique-se de que você verifique Olá **de** número de telefone para o seu código de saudação do Twilio conta toorunning anterior.</span><span class="sxs-lookup"><span data-stu-id="00053-172">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

<span data-ttu-id="00053-173">Conforme mencionado, esse código usa uma saudação do site fornecidos Twilio tooreturn TwiML resposta.</span><span class="sxs-lookup"><span data-stu-id="00053-173">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="00053-174">Em vez disso, você pode usar seu próprio hello tooprovide do site TwiML resposta; Para obter mais informações, consulte [como tooProvide TwiML respostas do seu próprio Site](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="00053-174">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="00053-175">**Observação**: erros de validação de certificado SSL tootroubleshoot, consulte [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="00053-175">**Note**: tootroubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="00053-176"><a id="howto_send_sms"></a>Como enviar uma mensagem de SMS</span><span class="sxs-lookup"><span data-stu-id="00053-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="00053-177">Olá a seguir mostra como toosend uma mensagem SMS usando Olá **Services_Twilio** classe.</span><span class="sxs-lookup"><span data-stu-id="00053-177">hello following shows how toosend an SMS message using hello **Services_Twilio** class.</span></span> <span data-ttu-id="00053-178">Olá **de** número é fornecido por Twilio para contas de avaliação toosend mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="00053-178">hello **From** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="00053-179">Olá **para** número deve ser verificado para seu código de saudação do Twilio conta toorunning anterior.</span><span class="sxs-lookup"><span data-stu-id="00053-179">hello **To** number must be verified for your Twilio account prior toorunning hello code.</span></span>

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <span data-ttu-id="00053-180"><a id="howto_provide_twiml_responses"></a>Como fornecer respostas TwiML de seu próprio site</span><span class="sxs-lookup"><span data-stu-id="00053-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="00053-181">Quando o aplicativo inicia toohello uma chamada de API do Twilio, Twilio enviará a URL de tooa de solicitação que é esperado tooreturn uma resposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="00053-181">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="00053-182">exemplo Hello acima usa a URL fornecida Twilio de saudação [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="00053-182">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="00053-183">(Embora TwiML foi projetado para uso por Twilio, você pode exibir hello-lo em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="00053-183">(While TwiML is designed for use by Twilio, you can view hello it in your browser.</span></span> <span data-ttu-id="00053-184">Por exemplo, clique em [http://twimlets.com/message] [ twimlet_message_url] toosee vazio `<Response>` elemento; como outro exemplo, clique em [http://twimlets.com/message? Mensagem % 5B0 %5D = Olá % 20World] [ twimlet_message_url_hello_world] toosee um `<Response>` elemento que contém um `<Say>` elemento.)</span><span class="sxs-lookup"><span data-stu-id="00053-184">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="00053-185">Em vez de depender de URL fornecido Twilio de saudação, você pode criar seu próprio site que retorna respostas de HTTP.</span><span class="sxs-lookup"><span data-stu-id="00053-185">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="00053-186">Você pode criar site hello em qualquer linguagem que retorna respostas XML; Este tópico pressupõe que você vai usar saudação do PHP toocreate TwiML.</span><span class="sxs-lookup"><span data-stu-id="00053-186">You can create hello site in any language that returns XML responses; this topic assumes you'll be using PHP toocreate hello TwiML.</span></span>

<span data-ttu-id="00053-187">Olá PHP página resultados em uma resposta de TwiML que diz que a seguir **Hello World** na chamada de saudação.</span><span class="sxs-lookup"><span data-stu-id="00053-187">hello following PHP page results in a TwiML response that says **Hello World** on hello call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="00053-188">Como você pode ver do exemplo hello acima, Olá TwiML resposta é simplesmente um documento XML.</span><span class="sxs-lookup"><span data-stu-id="00053-188">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="00053-189">biblioteca do Twilio Olá para PHP contém classes que irá gerar TwiML para você.</span><span class="sxs-lookup"><span data-stu-id="00053-189">hello Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="00053-190">exemplo Hello abaixo produz resposta equivalente hello como mostrado acima, mas usa Olá **serviços\_Twilio\_Twiml** classe na biblioteca do Twilio Olá para PHP:</span><span class="sxs-lookup"><span data-stu-id="00053-190">hello example below produces hello equivalent response as shown above, but uses hello **Services\_Twilio\_Twiml** class in hello Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="00053-191">Para obter mais informações sobre TwiML, consulte [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="00053-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="00053-192">Uma vez que a página PHP configurar respostas de TwiML tooprovide, usar Olá URL da página PHP hello como Olá URL passada em Olá `Services_Twilio->account->calls->create` método.</span><span class="sxs-lookup"><span data-stu-id="00053-192">Once you have your PHP page set up tooprovide TwiML responses, use hello URL of hello PHP page as hello URL passed into hello  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="00053-193">Por exemplo, se você tiver um aplicativo Web chamado **MyTwiML** tooan implantado Azure o serviço hospedado e Olá nome da página PHP Olá é **mytwiml.php**, Olá URL pode ser passada muito **Services_ Twilio -> contas -> chamadas -> criar** conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="00053-193">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, and hello name of hello PHP page is **mytwiml.php**, hello URL can be passed too **Services_Twilio->account->calls->create**  as shown in hello following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

<span data-ttu-id="00053-194">Para obter informações adicionais sobre como usar o Twilio no Azure com o PHP, consulte [como tooMake uma chamada telefônica usando o Twilio em um aplicativo PHP no Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="00053-194">For additional information about using Twilio in Azure with PHP, see [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="00053-195"><a id="AdditionalServices"></a>Como Usar os Serviços Adicionais do Twilio</span><span class="sxs-lookup"><span data-stu-id="00053-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="00053-196">Além disso toohello exemplos mostrados aqui, que twilio oferece APIs baseado na web que você pode usar uma funcionalidade adicional Twilio tooleverage do aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="00053-196">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="00053-197">Para obter detalhes completos, consulte Olá [documentação da API do Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="00053-197">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="00053-198"><a id="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="00053-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="00053-199">Agora que você aprendeu as Noções básicas sobre Olá Olá Twilio serviço, siga essas toolearn links mais:</span><span class="sxs-lookup"><span data-stu-id="00053-199">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="00053-200">[Diretrizes de segurança do Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="00053-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="00053-201">[Código de Exemplo e Procedimentos do Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="00053-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="00053-202">[Tutoriais do Guia de início rápido do Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="00053-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="00053-203">[Twilio no GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="00053-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="00053-204">[Fale tooTwilio suporte][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="00053-204">[Talk tooTwilio Support][twilio_support]</span></span>

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
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
