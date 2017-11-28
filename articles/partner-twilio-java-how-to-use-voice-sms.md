---
title: aaaHow tooUse Twilio para voz e SMS (Java) | Microsoft Docs
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Exemplos de códigos escritos em Java."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="09063-104">Como tooUse Twilio para recursos de SMS no Java e voz</span><span class="sxs-lookup"><span data-stu-id="09063-104">How tooUse Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="09063-105">Este guia demonstra como tooperform as tarefas de programação comuns com hello Twilio API de serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="09063-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="09063-106">cenários de saudação abordados incluem fazer uma chamada telefônica e enviar uma mensagem do serviço SMS (Short Message).</span><span class="sxs-lookup"><span data-stu-id="09063-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="09063-107">Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte Olá [próximas etapas](#NextSteps) seção.</span><span class="sxs-lookup"><span data-stu-id="09063-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="09063-108"><a id="WhatIs"></a>O que é Twilio?</span><span class="sxs-lookup"><span data-stu-id="09063-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="09063-109">Twilio é uma API de serviço web de telefonia que permite que você use seus idiomas de web existente e voz de toobuild habilidades e aplicativos de SMS.</span><span class="sxs-lookup"><span data-stu-id="09063-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="09063-110">O Twilio é um serviço de terceiro (não é um recurso do Azure e não é um produto da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="09063-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="09063-111">**Voz Twilio** permite que seus aplicativos toomake e receber chamadas telefônicas.</span><span class="sxs-lookup"><span data-stu-id="09063-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="09063-112">**Twilio SMS** permite que seus aplicativos toomake e receber mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="09063-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="09063-113">**Clientes do Twilio** permite comunicação por voz tooenable usando conexões da Internet existentes, incluindo conexões móveis que seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="09063-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="09063-114"><a id="Pricing"></a>Preços e ofertas especiais da Twilio</span><span class="sxs-lookup"><span data-stu-id="09063-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="09063-115">A informações sobre os preços do Twilio estão disponíveis em [Preços do Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="09063-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="09063-116">Os clientes do Azure recebem uma [oferta especial][special_offer]: um crédito de 1.000 mensagens de texto gratuitas ou 1.000 minutos de entrada.</span><span class="sxs-lookup"><span data-stu-id="09063-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="09063-117">toosign para esta oferta ou obter mais informações, visite [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="09063-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="09063-118"><a id="Concepts"></a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="09063-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="09063-119">Olá Twilio API é uma API RESTful que fornece funcionalidade SMS e voz para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="09063-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="09063-120">As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="09063-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="09063-121">Principais aspectos da saudação Twilio API são verbos do Twilio e Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="09063-121">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="09063-122"><a id="Verbs"></a>Verbos da Twilio</span><span class="sxs-lookup"><span data-stu-id="09063-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="09063-123">Olá API faz uso do Twilio verbos; Por exemplo, Olá  **&lt;diga&gt;**  verbo instrui Twilio tooaudibly entregar uma mensagem em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="09063-123">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="09063-124">a seguir Olá é uma lista de verbos do Twilio.</span><span class="sxs-lookup"><span data-stu-id="09063-124">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="09063-125">**&lt;Discagem&gt;**: conecta-se o telefone de tooanother Olá chamador.</span><span class="sxs-lookup"><span data-stu-id="09063-125">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="09063-126">**&lt;Coletar&gt;**: coleta dígitos numéricos inseridos no teclado numérico do telefone hello.</span><span class="sxs-lookup"><span data-stu-id="09063-126">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="09063-127">**&lt;Hangup&gt;**: termina uma chamada.</span><span class="sxs-lookup"><span data-stu-id="09063-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="09063-128">**&lt;Play&gt;**: reproduz um arquivo de áudio.</span><span class="sxs-lookup"><span data-stu-id="09063-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="09063-129">**&lt;Fila&gt;**: Adicionar Olá tooa fila de chamadores.</span><span class="sxs-lookup"><span data-stu-id="09063-129">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="09063-130">**&lt;Pause&gt;**: espera silenciosamente por um número especificado de segundos.</span><span class="sxs-lookup"><span data-stu-id="09063-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="09063-131">**&lt;Registro&gt;**: registra a voz do chamador hello e retorna uma URL de um arquivo que contém a gravação da saudação.</span><span class="sxs-lookup"><span data-stu-id="09063-131">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="09063-132">**&lt;Redirecionar&gt;**: transfere o controle de uma chamada ou SMS toohello TwiML em uma URL diferente.</span><span class="sxs-lookup"><span data-stu-id="09063-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="09063-133">**&lt;Rejeitar&gt;**: rejeita uma entrada chamar tooyour Twilio número sem cobrança você.</span><span class="sxs-lookup"><span data-stu-id="09063-133">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="09063-134">**&lt;Digamos que&gt;**: converte texto toospeech que é feita em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="09063-134">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="09063-135">**&lt;Sms&gt;**: envia uma mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="09063-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="09063-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="09063-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="09063-137">TwiML é um conjunto de instruções baseadas em XML com base em verbos do Twilio Olá que informam o Twilio como tooprocess uma chamada ou SMS.</span><span class="sxs-lookup"><span data-stu-id="09063-137">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="09063-138">Por exemplo, Olá TwiML a seguir seria converter o texto de saudação **Olá, mundo!**</span><span class="sxs-lookup"><span data-stu-id="09063-138">As an example, hello following TwiML would convert hello text **Hello World!**</span></span> <span data-ttu-id="09063-139">toospeech.</span><span class="sxs-lookup"><span data-stu-id="09063-139">toospeech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="09063-140">Quando a aplicativo chama hello Twilio API, um dos parâmetros de API de saudação é URL Olá retorna Olá TwiML resposta.</span><span class="sxs-lookup"><span data-stu-id="09063-140">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="09063-141">Para fins de desenvolvimento, você pode usar URLs fornecido Twilio tooprovide Olá TwiML as respostas usadas pelos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="09063-141">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="09063-142">Você também pode hospedar seus próprio respostas de TwiML URLs tooproduce hello e outra opção é Olá toouse **TwiMLResponse** objeto.</span><span class="sxs-lookup"><span data-stu-id="09063-142">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="09063-143">Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="09063-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="09063-144">Para obter informações adicionais sobre Olá Twilio API, consulte [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="09063-144">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="09063-145"><a id="CreateAccount"></a>Criar uma conta na Twilio</span><span class="sxs-lookup"><span data-stu-id="09063-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="09063-146">Quando você estiver pronto tooget uma conta do Twilio, inscreva-se em [tente Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="09063-146">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="09063-147">Você pode começar com uma conta gratuita e atualizá-la depois.</span><span class="sxs-lookup"><span data-stu-id="09063-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="09063-148">Quando você se inscrever para uma conta de Twilio, você receberá uma ID de conta e um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="09063-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="09063-149">Ambos serão chamadas à API do Twilio toomake necessários.</span><span class="sxs-lookup"><span data-stu-id="09063-149">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="09063-150">tooprevent não autorizado acessar conta tooyour, mantenha o token de autenticação segura.</span><span class="sxs-lookup"><span data-stu-id="09063-150">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="09063-151">Sua ID da conta e a autenticação token são visíveis no hello [Twilio Console][twilio_console], no hello campos rotulados **SID da conta** e **TOKEN de autenticação**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="09063-151">Your account ID and authentication token are viewable at hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="09063-152"><a id="create_app"></a>Criar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="09063-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="09063-153">Obter Olá JAR do Twilio e adicioná-lo tooyour Java criar o caminho e o seu assembly de implantação WAR.</span><span class="sxs-lookup"><span data-stu-id="09063-153">Obtain hello Twilio JAR and add it tooyour Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="09063-154">Em [https://github.com/twilio/twilio-java][twilio_java], você pode baixar fontes do GitHub hello e criar seu próprios JAR ou baixar um JAR pré-criado (com ou sem dependências).</span><span class="sxs-lookup"><span data-stu-id="09063-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="09063-155">Verifique se o seu JDK **cacerts** keystore contém o certificado de autoridade de certificação segura Equifax Olá com impressão digital de MD5 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (número de série de saudação é 35:DE:F4:CF e hello SHA1 impressão digital é D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="09063-155">Ensure your JDK's **cacerts** keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="09063-156">Este é o certificado de autoridade de certificado Olá para Olá [https://api.twilio.com] [ twilio_api_service] service, que é chamado quando você usar as APIs do Twilio.</span><span class="sxs-lookup"><span data-stu-id="09063-156">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="09063-157">Para obter informações sobre como garantir seu JDK **cacerts** keystore contém o certificado de autoridade de certificação correto hello, consulte [adicionando um certificado toohello repositório de certificados de autoridade de certificação de Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="09063-157">For information about ensuring your JDK's **cacerts** keystore contains hello correct CA certificate, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="09063-158">Instruções detalhadas para usar a biblioteca de clientes do Twilio Olá para Java estão disponíveis em [como tooMake uma chamada telefônica usando o Twilio em um aplicativo Java no Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="09063-158">Detailed instructions for using hello Twilio client library for Java are available at [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="09063-159"><a id="configure_app"></a>Configurar seu aplicativo tooUse Twilio bibliotecas</span><span class="sxs-lookup"><span data-stu-id="09063-159"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="09063-160">Dentro de seu código, você pode adicionar **importar** instruções na parte superior da saudação de seus arquivos de origem para Olá Twilio pacotes ou classes que você deseja toouse em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="09063-160">Within your code, you can add **import** statements at hello top of your source files for hello Twilio packages or classes you want toouse in your application.</span></span>

<span data-ttu-id="09063-161">Para arquivos de origem Java:</span><span class="sxs-lookup"><span data-stu-id="09063-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="09063-162">Para arquivos de origem Java Server Page (JSP):</span><span class="sxs-lookup"><span data-stu-id="09063-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="09063-163">Dependendo de quais pacotes Twilio ou classes que você deseja toouse, seu **importar** instruções podem ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="09063-163">Depending on which Twilio packages or classes you want toouse, your **import** statements may be different.</span></span>

## <span data-ttu-id="09063-164"><a id="howto_make_call"></a>Como fazer uma chamada externa</span><span class="sxs-lookup"><span data-stu-id="09063-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="09063-165">Olá a seguir mostra como uma saída de toomake chamar usando Olá **chamar** classe.</span><span class="sxs-lookup"><span data-stu-id="09063-165">hello following shows how toomake an outgoing call using hello **Call** class.</span></span> <span data-ttu-id="09063-166">Esse código também usa uma saudação do site fornecidos Twilio tooreturn resposta Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="09063-166">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="09063-167">Substitua os valores para Olá **de** e **para** números de telefone e certifique-se de que você verifique Olá **de** número de telefone para o seu código de saudação do Twilio conta toorunning anterior.</span><span class="sxs-lookup"><span data-stu-id="09063-167">Substitute your values for hello **from** and **to** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account prior toorunning hello code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="09063-168">Para obter mais informações sobre parâmetros de saudação passado toohello **Call.creator** método, consulte [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="09063-168">For more information about hello parameters passed in toohello **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="09063-169">Conforme mencionado, esse código usa uma saudação do site fornecidos Twilio tooreturn TwiML resposta.</span><span class="sxs-lookup"><span data-stu-id="09063-169">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="09063-170">Em vez disso, você pode usar seu próprio hello tooprovide do site TwiML resposta; Para obter mais informações, consulte [como tooProvide TwiML respostas em um aplicativo Java no Azure](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="09063-170">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="09063-171"><a id="howto_send_sms"></a>Como enviar uma mensagem de SMS</span><span class="sxs-lookup"><span data-stu-id="09063-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="09063-172">Olá a seguir mostra como toosend uma mensagem SMS usando Olá **mensagem** classe.</span><span class="sxs-lookup"><span data-stu-id="09063-172">hello following shows how toosend an SMS message using hello **Message** class.</span></span> <span data-ttu-id="09063-173">Olá **de** número, **4155992671**, é fornecido por Twilio para contas de avaliação toosend mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="09063-173">hello **from** number, **4155992671**, is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="09063-174">Olá **para** número deve ser verificado para seu código de saudação do Twilio conta toorunning anterior.</span><span class="sxs-lookup"><span data-stu-id="09063-174">hello **to** number must be verified for your Twilio account prior toorunning hello code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="09063-175">Para obter mais informações sobre parâmetros de saudação passado toohello **Message.creator** método, consulte [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="09063-175">For more information about hello parameters passed in toohello **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="09063-176"><a id="howto_provide_twiml_responses"></a>Como fornecer respostas TwiML de seu próprio site</span><span class="sxs-lookup"><span data-stu-id="09063-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="09063-177">Quando o aplicativo inicia toohello uma chamada de API do Twilio, por exemplo por meio de saudação **CallCreator.create** método Twilio enviará a URL de tooa de solicitação que é esperado tooreturn uma resposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="09063-177">When your application initiates a call toohello Twilio API, for example via hello **CallCreator.create** method, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="09063-178">exemplo Hello acima usa a URL fornecida Twilio de saudação [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="09063-178">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="09063-179">(Embora TwiML foi projetado para uso pelos serviços da Web, você pode exibir hello TwiML em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="09063-179">(While TwiML is designed for use by Web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="09063-180">Por exemplo, clique em [http://twimlets.com/message] [ twimlet_message_url] toosee vazio  **&lt;resposta&gt;**  elemento; como outro exemplo, clique em [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee um  **&lt;resposta&gt;**  elemento que contém um  **&lt;diga &gt;**  elemento.)</span><span class="sxs-lookup"><span data-stu-id="09063-180">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] toosee a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="09063-181">Em vez de depender de URL fornecido Twilio de saudação, você pode criar seu próprio site de URL que retorna respostas de HTTP.</span><span class="sxs-lookup"><span data-stu-id="09063-181">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="09063-182">Você pode criar site hello em qualquer linguagem que retorna respostas HTTP; Este tópico pressupõe que você vai hospedando Olá URL em uma página JSP.</span><span class="sxs-lookup"><span data-stu-id="09063-182">You can create hello site in any language that returns HTTP responses; this topic assumes you'll be hosting hello URL in a JSP page.</span></span>

<span data-ttu-id="09063-183">Olá JSP página resultados em uma resposta de TwiML que diz que a seguir **Olá, mundo!**</span><span class="sxs-lookup"><span data-stu-id="09063-183">hello following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="09063-184">na chamada de saudação.</span><span class="sxs-lookup"><span data-stu-id="09063-184">on hello call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="09063-185">Olá JSP página resultados em uma resposta de TwiML que diz que algum texto a seguir tem vários pausa e diz informações sobre a versão da API do Twilio hello e o nome de função do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="09063-185">hello following JSP page results in a TwiML response that says some text, has several pauses, and says information about hello Twilio API version and hello Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="09063-186">Olá **ApiVersion** parâmetro está disponível em solicitações de voz do Twilio (não a solicitações SMS).</span><span class="sxs-lookup"><span data-stu-id="09063-186">hello **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="09063-187">parâmetros de solicitação disponíveis toosee Olá para voz Twilio e solicitações SMS, consulte <https://www.twilio.com/docs/api/twiml/twilio_request> e <https://www.twilio.com/docs/api/twiml/sms/twilio_request >, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="09063-187">toosee hello available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="09063-188">Olá **RoleName** variável de ambiente está disponível como parte de uma implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="09063-188">hello **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="09063-189">(Se você quiser tooadd variáveis de ambiente personalizado para que eles podem ser retirados do **System.getenv**, consulte a seção de variáveis de ambiente Olá no [diversos parâmetros de configuração de função] [misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="09063-189">(If you want tooadd custom environment variables so they could be picked up from **System.getenv**, see hello environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="09063-190">Depois de você tiver sua página JSP configurar tooprovide TwiML respostas, use Olá URL da página JSP Olá Olá URL passada em hello **Call.creator** método.</span><span class="sxs-lookup"><span data-stu-id="09063-190">Once you have your JSP page set up tooprovide TwiML responses, use hello URL of hello JSP page as hello URL passed into hello **Call.creator** method.</span></span> <span data-ttu-id="09063-191">Por exemplo, se você tiver um aplicativo Web chamado tooan MyTwiML implantado hospedado do Azure service e Olá nome de página JSP Olá mytwiml.jsp, Olá URL pode ser passado muito**Call.creator** conforme mostrado na seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="09063-191">For example, if you have a Web application named MyTwiML deployed tooan Azure hosted service, and hello name of hello JSP page is mytwiml.jsp, hello URL can be passed too**Call.creator** as shown in hello following:</span></span>

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="09063-192">Outra opção para responder com TwiML é por meio de saudação **VoiceResponse** classe, que está disponível no hello **com.twilio.twiml** pacote.</span><span class="sxs-lookup"><span data-stu-id="09063-192">Another option for responding with TwiML is via hello **VoiceResponse** class, which is available in hello **com.twilio.twiml** package.</span></span>

<span data-ttu-id="09063-193">Para obter informações adicionais sobre como usar o Twilio no Azure com Java, consulte [como tooMake uma chamada telefônica usando o Twilio em um aplicativo Java no Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="09063-193">For additional information about using Twilio in Azure with Java, see [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="09063-194"><a id="AdditionalServices"></a>Como Usar os Serviços Adicionais do Twilio</span><span class="sxs-lookup"><span data-stu-id="09063-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="09063-195">Além disso toohello exemplos mostrados aqui, que twilio oferece APIs baseado na web que você pode usar uma funcionalidade adicional Twilio tooleverage do aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="09063-195">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="09063-196">Para obter detalhes completos, consulte Olá [documentação da API do Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="09063-196">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="09063-197"><a id="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09063-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="09063-198">Agora que você aprendeu as Noções básicas sobre Olá Olá Twilio serviço, siga essas toolearn links mais:</span><span class="sxs-lookup"><span data-stu-id="09063-198">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="09063-199">[Diretrizes de segurança do Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="09063-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="09063-200">[Código de Exemplo e Procedimentos do Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="09063-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="09063-201">[Tutoriais do Guia de início rápido do Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="09063-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="09063-202">[Twilio no GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="09063-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="09063-203">[Fale tooTwilio suporte][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="09063-203">[Talk tooTwilio Support][twilio_support]</span></span>

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
