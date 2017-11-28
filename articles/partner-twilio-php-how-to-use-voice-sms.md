---
title: Como usar o Twilio para voz e SMS (PHP) | Microsoft Docs
description: "Saiba como fazer uma chamada telefônica e enviar uma mensagem SMS com o serviço de API do Twilio no Azure. Exemplos de código escritos em PHP."
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
ms.openlocfilehash: bd50eac7390e8639f77894689388e6926cdb619c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="a11a9-104">Como usar o Twilio para obter recursos de voz e SMS no PHP</span><span class="sxs-lookup"><span data-stu-id="a11a9-104">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="a11a9-105">Este guia demonstra como executar tarefas comuns de programação com o serviço de API do Twilio no Azure.</span><span class="sxs-lookup"><span data-stu-id="a11a9-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="a11a9-106">Os cenários abrangidos incluem fazer uma chamada telefônica e enviar uma mensagem serviço de mensagem curta (SMS).</span><span class="sxs-lookup"><span data-stu-id="a11a9-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="a11a9-107">Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte a seção [Próximas etapas](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="a11a9-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="a11a9-108"><a id="WhatIs"></a>O que é Twilio?</span><span class="sxs-lookup"><span data-stu-id="a11a9-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="a11a9-109">Twilio é alimentar o futuro das comunicações de negócios, que permite aos desenvolvedores incorporar voz, VoIP e mensagens em aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a11a9-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="a11a9-110">Eles virtualizam toda a infra-estrutura necessária em um ambiente baseado em nuvem, global, expondo-as por meio da plataforma de comunicações API Twilio.</span><span class="sxs-lookup"><span data-stu-id="a11a9-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="a11a9-111">Os aplicativos são simples de criar e dimensionável.</span><span class="sxs-lookup"><span data-stu-id="a11a9-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="a11a9-112">Aproveite a flexibilidade com pagamento medida que vá preços e se beneficiar da confiabilidade da nuvem.</span><span class="sxs-lookup"><span data-stu-id="a11a9-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="a11a9-113">**Twilio Voice** permite que seus aplicativos façam e recebam chamadas telefônicas.</span><span class="sxs-lookup"><span data-stu-id="a11a9-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="a11a9-114">**SMS da Twilio** permite que seu aplicativo envie e receba mensagens de texto.</span><span class="sxs-lookup"><span data-stu-id="a11a9-114">**Twilio SMS** enables your application to send and receive text messages.</span></span> <span data-ttu-id="a11a9-115">**Cliente de Twilio** permite que você faça chamadas VoIP de qualquer telefone, tablet ou navegador e oferece suporte a WebRTC.</span><span class="sxs-lookup"><span data-stu-id="a11a9-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="a11a9-116"><a id="Pricing"></a>Preços e ofertas especiais da Twilio</span><span class="sxs-lookup"><span data-stu-id="a11a9-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="a11a9-117">Os clientes do Azure recebem uma [oferta especial](http://www.twilio.com/azure): US$ 10 de cortesia de crédito da Twilio quando atualizam a sua conta da Twilio.</span><span class="sxs-lookup"><span data-stu-id="a11a9-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="a11a9-118">Esse crédito de Twilio pode ser aplicado a qualquer uso de Twilio (equivalente a até 1.000 mensagens SMS de envio ou recebimento de até 1000 minutos de voz entrados, dependendo da localização do seu destino de chamada e mensagem ou número de telefone de crédito de US $10).</span><span class="sxs-lookup"><span data-stu-id="a11a9-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="a11a9-119">Resgate esse crédito da Twilio e faça uma introdução em: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="a11a9-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="a11a9-120">Twilio é um serviço flexível.</span><span class="sxs-lookup"><span data-stu-id="a11a9-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="a11a9-121">Não há nenhuma taxa de configuração e você pode fechar sua conta a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="a11a9-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="a11a9-122">Você pode encontrar mais detalhes em [Preços do Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="a11a9-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="a11a9-123"><a id="Concepts"></a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="a11a9-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="a11a9-124">A API do Twilio é uma API RESTful que fornece os recursos de voz e SMS para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a11a9-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="a11a9-125">As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="a11a9-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="a11a9-126">Os principais aspectos da API do Twilio são os verbos Twilio e a TwiML (Linguagem de Marcação do Twilio).</span><span class="sxs-lookup"><span data-stu-id="a11a9-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="a11a9-127"><a id="Verbs"></a>Verbos da Twilio</span><span class="sxs-lookup"><span data-stu-id="a11a9-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="a11a9-128">A API usa os verbos do Twilio; por exemplo, o verbo **&lt;Say&gt;** instrui o Twilio a fornecer de forma audível uma mensagem em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="a11a9-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="a11a9-129">A seguir está uma lista de verbos do Twilio.</span><span class="sxs-lookup"><span data-stu-id="a11a9-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="a11a9-130">Saiba mais sobre os outros verbos e recursos na [Documentação da linguagem de marcação da Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="a11a9-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="a11a9-131">**&lt;Dial&gt;**: conecta o chamador com outro telefone.</span><span class="sxs-lookup"><span data-stu-id="a11a9-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="a11a9-132">**&lt;Gather&gt;**: coleta os dígitos numéricos inseridos no teclado numérico de telefone.</span><span class="sxs-lookup"><span data-stu-id="a11a9-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="a11a9-133">**&lt;Hangup&gt;**: termina uma chamada.</span><span class="sxs-lookup"><span data-stu-id="a11a9-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="a11a9-134">**&lt;Play&gt;**: reproduz um arquivo de áudio.</span><span class="sxs-lookup"><span data-stu-id="a11a9-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="a11a9-135">**&lt;Pause&gt;**: espera silenciosamente por um número especificado de segundos.</span><span class="sxs-lookup"><span data-stu-id="a11a9-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="a11a9-136">**&lt;Record&gt;**: grava a voz do chamador e retorna uma URL de um arquivo que contém a gravação.</span><span class="sxs-lookup"><span data-stu-id="a11a9-136">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="a11a9-137">**&lt;Redirect&gt;**: transfere o controle de uma chamada ou SMS para TwiML em um URL diferente.</span><span class="sxs-lookup"><span data-stu-id="a11a9-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="a11a9-138">**&lt;Reject&gt;**: rejeita uma chamada recebida para o número do Twilio sem cobrar você</span><span class="sxs-lookup"><span data-stu-id="a11a9-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="a11a9-139">**&lt;Say&gt;**: converte o texto em fala que é executada em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="a11a9-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="a11a9-140">**&lt;Sms&gt;**: envia uma mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="a11a9-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="a11a9-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="a11a9-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="a11a9-142">TwiML é um conjunto de instruções em XML com base nos verbos do Twilio que informam o Twilio como processar uma chamada ou SMS.</span><span class="sxs-lookup"><span data-stu-id="a11a9-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="a11a9-143">Por exemplo, o seguinte TwiML converteria a mensagem **Olá, mundo** em fala.</span><span class="sxs-lookup"><span data-stu-id="a11a9-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="a11a9-144">Quando o aplicativo chama a API Twilio, um dos parâmetros a API é a URL que retorna a resposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="a11a9-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="a11a9-145">Para fins de desenvolvimento, você pode usar URLs fornecidos Twilio para fornecer as respostas de TwiML usadas por seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a11a9-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="a11a9-146">Você também pode hospedar seus próprio URLs para produzir as respostas TwiML e outra opção é usar o **TwiMLResponse** objeto.</span><span class="sxs-lookup"><span data-stu-id="a11a9-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="a11a9-147">Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="a11a9-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="a11a9-148">Para obter mais informações sobre a API do Twilio, consulte [API do Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="a11a9-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="a11a9-149"><a id="CreateAccount"></a>Criar uma conta na Twilio</span><span class="sxs-lookup"><span data-stu-id="a11a9-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="a11a9-150">Quando estiver pronto para obter uma conta do Twilio, inscreva-se em [Experimentar o Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="a11a9-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="a11a9-151">Você pode começar com uma conta gratuita e atualizá-la depois.</span><span class="sxs-lookup"><span data-stu-id="a11a9-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="a11a9-152">Quando você se inscrever para uma conta de Twilio, você receberá uma ID de conta e um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="a11a9-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="a11a9-153">Eles serão necessários para fazer chamadas de API do Twilio.</span><span class="sxs-lookup"><span data-stu-id="a11a9-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="a11a9-154">Para evitar o acesso não autorizado em sua conta, mantenha o token da autenticação seguro.</span><span class="sxs-lookup"><span data-stu-id="a11a9-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="a11a9-155">A ID de sua conta e o token de autenticação estão visíveis na [página da conta do Twilio][twilio_account], nos campos rotulados **ACCOUNT SID** e **AUTH TOKEN**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="a11a9-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="a11a9-156"><a id="create_app"></a>Criar um aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="a11a9-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="a11a9-157">Um aplicativo PHP que usa o serviço do Twilio e está em execução no Azure não é diferente de qualquer outro aplicativo PHP que usa o serviço do Twilio.</span><span class="sxs-lookup"><span data-stu-id="a11a9-157">A PHP application that uses the Twilio service and is running in Azure is no different than any other PHP application that uses the Twilio service.</span></span> <span data-ttu-id="a11a9-158">Enquanto Twilio serviços são baseados em REST e podem ser chamados de PHP de várias maneiras, este artigo abordará como usar os serviços do Twilio com [Twilio biblioteca para PHP do GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="a11a9-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how to use Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="a11a9-159">Para obter mais informações sobre como usar a biblioteca do Twilio para PHP, consulte [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="a11a9-159">For more information about using the Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="a11a9-160">Instruções detalhadas para criar e implantar um aplicativo PHP/Twilio para o Azure estão disponíveis em [como fazer uma chamada telefônica usando o Twilio em um aplicativo PHP no Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="a11a9-160">Detailed instructions for building and deploying a Twilio/PHP application to Azure are available at [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="a11a9-161"><a id="configure_app"></a>Configurar seu aplicativo para usar bibliotecas Twilio</span><span class="sxs-lookup"><span data-stu-id="a11a9-161"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="a11a9-162">Você pode configurar seu aplicativo para usar a biblioteca do Twilio para PHP de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="a11a9-162">You can configure your application to use the Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="a11a9-163">Baixar a biblioteca do Twilio para PHP do GitHub ([https://github.com/twilio/twilio-php][twilio_php]) e adicione o **serviços** diretório para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a11a9-163">Download the Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add the **Services** directory to your application.</span></span>
   
    <span data-ttu-id="a11a9-164">-OU-</span><span class="sxs-lookup"><span data-stu-id="a11a9-164">-OR-</span></span>
2. <span data-ttu-id="a11a9-165">Instalar a biblioteca da Twilio para PHP como um pacote PEAR.</span><span class="sxs-lookup"><span data-stu-id="a11a9-165">Install the Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="a11a9-166">Ela pode ser instalada com os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a11a9-166">It can be installed with the following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="a11a9-167">Depois de instalar a biblioteca da Twilio para PHP, você pode adicionar uma instrução **require_once** na parte superior dos arquivos PHP para fazer referência à biblioteca:</span><span class="sxs-lookup"><span data-stu-id="a11a9-167">Once you have installed the Twilio library for PHP, you can then add a **require_once** statement at the top of your PHP files to reference the library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="a11a9-168">Para obter mais informações, consulte [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="a11a9-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="a11a9-169"><a id="howto_make_call"></a>Como fazer uma chamada externa</span><span class="sxs-lookup"><span data-stu-id="a11a9-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="a11a9-170">Abaixo é mostrado como fazer uma chamada externa usando a classe **Services_Twilio**.</span><span class="sxs-lookup"><span data-stu-id="a11a9-170">The following shows how to make an outgoing call using the **Services_Twilio** class.</span></span> <span data-ttu-id="a11a9-171">Esse código também usa um site fornecido pelo Twilio para retornar a resposta TwiML (Linguagem de Marcação do Twilio).</span><span class="sxs-lookup"><span data-stu-id="a11a9-171">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="a11a9-172">Substitua os valores dos números telefônico **De** e **Para** e certifique-se de verificar o número telefônico **De** para sua conta do Twilio antes de executar o código.</span><span class="sxs-lookup"><span data-stu-id="a11a9-172">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // The number of the phone initiating the the call.
    $from_number = "NNNNNNNNNNN";

    // The number of the phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use the Twilio-provided site for the TwiML response.
    $url = "http://twimlets.com/message";

    // The phone message text.
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make the call.
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

<span data-ttu-id="a11a9-173">Como mencionado, esse código utiliza um site fornecido pelo Twilio para retornar a resposta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="a11a9-173">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="a11a9-174">Em vez disso, você pode usar seu próprio site para fornecer a resposta TwiML. Para obter mais informações, consulte [Como fornecer respostas TwiML em seu próprio site](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="a11a9-174">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="a11a9-175">**Observação**: para solucionar erros de validação de certificado SSL, consulte [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="a11a9-175">**Note**: To troubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="a11a9-176"><a id="howto_send_sms"></a>Como enviar uma mensagem de SMS</span><span class="sxs-lookup"><span data-stu-id="a11a9-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="a11a9-177">Abaixo é mostrado como enviar uma mensagem SMS usando a classe **Services_Twilio**.</span><span class="sxs-lookup"><span data-stu-id="a11a9-177">The following shows how to send an SMS message using the **Services_Twilio** class.</span></span> <span data-ttu-id="a11a9-178">O **de** número é fornecido por Twilio para contas de avaliação para enviar mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="a11a9-178">The **From** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="a11a9-179">O número **Para** deve ser verificado para sua conta de Twilio antes de executar o código.</span><span class="sxs-lookup"><span data-stu-id="a11a9-179">The **To** number must be verified for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send the SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <span data-ttu-id="a11a9-180"><a id="howto_provide_twiml_responses"></a>Como fornecer respostas TwiML de seu próprio site</span><span class="sxs-lookup"><span data-stu-id="a11a9-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="a11a9-181">Quando o aplicativo inicia uma chamada para a API do Twilio, o Twilio enviará a solicitação a uma URL que deve retornar uma resposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="a11a9-181">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="a11a9-182">O exemplo acima usa a URL fornecida pelo Twilio [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="a11a9-182">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="a11a9-183">(Embora o TwiML tenha sido criado para uso do Twilio, você pode exibi-lo em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="a11a9-183">(While TwiML is designed for use by Twilio, you can view the it in your browser.</span></span> <span data-ttu-id="a11a9-184">Por exemplo, clique em [http://twimlets.com/message][twimlet_message_url] para ver um elemento `<Response>` vazio. Como outro exemplo, clique em [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] para ver um elemento `<Response>` que contém um elemento `<Say>`.)</span><span class="sxs-lookup"><span data-stu-id="a11a9-184">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="a11a9-185">Em vez de contar com a URL fornecida pela Twilio, você pode criar seu próprio site que retorne respostas HTTP.</span><span class="sxs-lookup"><span data-stu-id="a11a9-185">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="a11a9-186">Você pode criar o site em qualquer linguagem que retorna respostas XML; este tópico pressupõe que você usará PHP para criar o TwiML.</span><span class="sxs-lookup"><span data-stu-id="a11a9-186">You can create the site in any language that returns XML responses; this topic assumes you'll be using PHP to create the TwiML.</span></span>

<span data-ttu-id="a11a9-187">A página PHP seguinte resulta em uma resposta de TwiML que diz **Hello World** na chamada.</span><span class="sxs-lookup"><span data-stu-id="a11a9-187">The following PHP page results in a TwiML response that says **Hello World** on the call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="a11a9-188">Como você pode ver no exemplo acima, a resposta de TwiML é simplesmente um documento XML.</span><span class="sxs-lookup"><span data-stu-id="a11a9-188">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="a11a9-189">A biblioteca da Twilio para PHP contém classes que geram TwiML para você.</span><span class="sxs-lookup"><span data-stu-id="a11a9-189">The Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="a11a9-190">O exemplo a seguir produz a resposta equivalente conforme mostrado acima, mas usa a classe **Services\_Twilio\_Twiml** na biblioteca da Twilio para PHP:</span><span class="sxs-lookup"><span data-stu-id="a11a9-190">The example below produces the equivalent response as shown above, but uses the **Services\_Twilio\_Twiml** class in the Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="a11a9-191">Para obter mais informações sobre TwiML, consulte [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="a11a9-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="a11a9-192">Uma vez que a página PHP estiver configurada para fornecer respostas TwiML, use a URL da página PHP como a URL passada para o método `Services_Twilio->account->calls->create`.</span><span class="sxs-lookup"><span data-stu-id="a11a9-192">Once you have your PHP page set up to provide TwiML responses, use the URL of the PHP page as the URL passed into the  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="a11a9-193">Por exemplo, se você tiver um aplicativo Web chamado **MyTwiML** implantado em um serviço hospedado do Azure e o nome da página PHP é **mytwiml.php**, a URL poderá ser passada para **Services_Twilio->account->calls->create** conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a11a9-193">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, and the name of the PHP page is **mytwiml.php**, the URL can be passed to  **Services_Twilio->account->calls->create**  as shown in the following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // The phone message text.
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

<span data-ttu-id="a11a9-194">Para obter informações adicionais sobre como usar o Twilio no Azure com o PHP, consulte [como fazer uma chamada telefônica usando o Twilio em um aplicativo PHP no Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="a11a9-194">For additional information about using Twilio in Azure with PHP, see [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="a11a9-195"><a id="AdditionalServices"></a>Como Usar os Serviços Adicionais do Twilio</span><span class="sxs-lookup"><span data-stu-id="a11a9-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="a11a9-196">Além dos exemplos mostrados aqui, o Twilio oferece APIs baseadas na Web que podem ser usadas para aproveitar a funcionalidade adicional do Twilio do aplicativo Azure.</span><span class="sxs-lookup"><span data-stu-id="a11a9-196">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="a11a9-197">Para obter detalhes completos, consulte a [Documentação da API do Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="a11a9-197">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="a11a9-198"><a id="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a11a9-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="a11a9-199">Agora que você já conhece os princípios do serviço Twilio, acesse estes links para saber mais:</span><span class="sxs-lookup"><span data-stu-id="a11a9-199">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="a11a9-200">[Diretrizes de segurança do Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="a11a9-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="a11a9-201">[Código de Exemplo e Procedimentos do Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="a11a9-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="a11a9-202">[Tutoriais do Guia de início rápido do Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="a11a9-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="a11a9-203">[Twilio no GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="a11a9-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="a11a9-204">[Fale com o suporte do Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="a11a9-204">[Talk to Twilio Support][twilio_support]</span></span>

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
