---
title: Como usar o Twilio para voz e SMS (Java) | Microsoft Docs
description: "Saiba como fazer uma chamada telefônica e enviar uma mensagem SMS com o serviço de API do Twilio no Azure. Exemplos de códigos escritos em Java."
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
ms.openlocfilehash: 5a1b2ffa160a31b639605242b651dc8d14e7a01b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="26f2a-104">Como usar a Twilio para obter recursos de voz e SMS no Java</span><span class="sxs-lookup"><span data-stu-id="26f2a-104">How to Use Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="26f2a-105">Este guia demonstra como executar tarefas comuns de programação com o serviço de API do Twilio no Azure.</span><span class="sxs-lookup"><span data-stu-id="26f2a-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="26f2a-106">Os cenários abrangidos incluem fazer uma chamada telefônica e enviar uma mensagem serviço de mensagem curta (SMS).</span><span class="sxs-lookup"><span data-stu-id="26f2a-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="26f2a-107">Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte a seção [Próximas etapas](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="26f2a-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="26f2a-108"><a id="WhatIs"></a>O que é Twilio?</span><span class="sxs-lookup"><span data-stu-id="26f2a-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="26f2a-109">Twilio é uma API do serviço Web de telefonia que permite usar os idiomas e as habilidades existentes de Web para criar aplicativos de voz e SMS.</span><span class="sxs-lookup"><span data-stu-id="26f2a-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="26f2a-110">O Twilio é um serviço de terceiro (não é um recurso do Azure e não é um produto da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="26f2a-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="26f2a-111">**Twilio Voice** permite que seus aplicativos façam e recebam chamadas telefônicas.</span><span class="sxs-lookup"><span data-stu-id="26f2a-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="26f2a-112">**Twilio SMS** permite que seus aplicativos façam e recebam mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="26f2a-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="26f2a-113">**Twilio Cliente** permite que seus aplicativos habilitem a comunicação de voz usando as conexões existentes com a Internet, incluindo conexões para celular.</span><span class="sxs-lookup"><span data-stu-id="26f2a-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="26f2a-114"><a id="Pricing"></a>Preços e ofertas especiais da Twilio</span><span class="sxs-lookup"><span data-stu-id="26f2a-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="26f2a-115">A informações sobre os preços do Twilio estão disponíveis em [Preços do Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="26f2a-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="26f2a-116">Os clientes do Azure recebem uma [oferta especial][special_offer]: um crédito de 1.000 mensagens de texto gratuitas ou 1.000 minutos de entrada.</span><span class="sxs-lookup"><span data-stu-id="26f2a-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="26f2a-117">Para se inscrever nessa oferta ou obter mais informações, visite [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="26f2a-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="26f2a-118"><a id="Concepts"></a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="26f2a-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="26f2a-119">A API do Twilio é uma API RESTful que fornece os recursos de voz e SMS para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="26f2a-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="26f2a-120">As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="26f2a-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="26f2a-121">Os principais aspectos da API do Twilio são os verbos Twilio e a TwiML (Linguagem de Marcação do Twilio).</span><span class="sxs-lookup"><span data-stu-id="26f2a-121">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="26f2a-122"><a id="Verbs"></a>Verbos da Twilio</span><span class="sxs-lookup"><span data-stu-id="26f2a-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="26f2a-123">A API usa os verbos do Twilio; por exemplo, o verbo **&lt;Say&gt;** instrui o Twilio a fornecer de forma audível uma mensagem em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="26f2a-123">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="26f2a-124">A seguir está uma lista de verbos do Twilio.</span><span class="sxs-lookup"><span data-stu-id="26f2a-124">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="26f2a-125">**&lt;Dial&gt;**: conecta o chamador com outro telefone.</span><span class="sxs-lookup"><span data-stu-id="26f2a-125">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="26f2a-126">**&lt;Gather&gt;**: coleta os dígitos numéricos inseridos no teclado numérico de telefone.</span><span class="sxs-lookup"><span data-stu-id="26f2a-126">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="26f2a-127">**&lt;Hangup&gt;**: termina uma chamada.</span><span class="sxs-lookup"><span data-stu-id="26f2a-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="26f2a-128">**&lt;Play&gt;**: reproduz um arquivo de áudio.</span><span class="sxs-lookup"><span data-stu-id="26f2a-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="26f2a-129">**&lt;Fila&gt;**: adicionar a chamada a uma fila de chamadores.</span><span class="sxs-lookup"><span data-stu-id="26f2a-129">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="26f2a-130">**&lt;Pause&gt;**: espera silenciosamente por um número especificado de segundos.</span><span class="sxs-lookup"><span data-stu-id="26f2a-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="26f2a-131">**&lt;Record&gt;**: grava a voz do chamador e retorna uma URL de um arquivo que contém a gravação.</span><span class="sxs-lookup"><span data-stu-id="26f2a-131">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="26f2a-132">**&lt;Redirect&gt;**: transfere o controle de uma chamada ou SMS para TwiML em um URL diferente.</span><span class="sxs-lookup"><span data-stu-id="26f2a-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="26f2a-133">**&lt;Reject&gt;**: rejeita uma chamada recebida para o número do Twilio sem cobrar você.</span><span class="sxs-lookup"><span data-stu-id="26f2a-133">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="26f2a-134">**&lt;Say&gt;**: converte o texto em fala que é executada em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="26f2a-134">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="26f2a-135">**&lt;Sms&gt;**: envia uma mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="26f2a-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="26f2a-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="26f2a-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="26f2a-137">TwiML é um conjunto de instruções em XML com base nos verbos do Twilio que informam o Twilio como processar uma chamada ou SMS.</span><span class="sxs-lookup"><span data-stu-id="26f2a-137">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="26f2a-138">Por exemplo, o TwiML a seguir converteria o texto **Olá, mundo!**</span><span class="sxs-lookup"><span data-stu-id="26f2a-138">As an example, the following TwiML would convert the text **Hello World!**</span></span> <span data-ttu-id="26f2a-139">em fala.</span><span class="sxs-lookup"><span data-stu-id="26f2a-139">to speech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="26f2a-140">Quando o aplicativo chama a API Twilio, um dos parâmetros a API é a URL que retorna a resposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="26f2a-140">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="26f2a-141">Para fins de desenvolvimento, você pode usar URLs fornecidos Twilio para fornecer as respostas de TwiML usadas por seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="26f2a-141">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="26f2a-142">Você também pode hospedar seus próprio URLs para produzir as respostas TwiML e outra opção é usar o **TwiMLResponse** objeto.</span><span class="sxs-lookup"><span data-stu-id="26f2a-142">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="26f2a-143">Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="26f2a-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="26f2a-144">Para obter mais informações sobre a API do Twilio, consulte [API do Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="26f2a-144">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="26f2a-145"><a id="CreateAccount"></a>Criar uma conta na Twilio</span><span class="sxs-lookup"><span data-stu-id="26f2a-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="26f2a-146">Quando estiver pronto para obter uma conta do Twilio, inscreva-se em [Experimentar o Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="26f2a-146">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="26f2a-147">Você pode começar com uma conta gratuita e atualizá-la depois.</span><span class="sxs-lookup"><span data-stu-id="26f2a-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="26f2a-148">Quando você se inscrever para uma conta de Twilio, você receberá uma ID de conta e um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="26f2a-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="26f2a-149">Eles serão necessários para fazer chamadas de API do Twilio.</span><span class="sxs-lookup"><span data-stu-id="26f2a-149">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="26f2a-150">Para evitar o acesso não autorizado em sua conta, mantenha o token da autenticação seguro.</span><span class="sxs-lookup"><span data-stu-id="26f2a-150">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="26f2a-151">A ID de sua conta e o token de autenticação estão visíveis no [Console do Twilio][twilio_console], nos campos rotulados **ACCOUNT SID** e **AUTH TOKEN**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="26f2a-151">Your account ID and authentication token are viewable at the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="26f2a-152"><a id="create_app"></a>Criar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="26f2a-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="26f2a-153">Obtenha o JAR do Twilio e adicione-o ao seu caminho de compilação do Java e seu assembly de implantação WAR.</span><span class="sxs-lookup"><span data-stu-id="26f2a-153">Obtain the Twilio JAR and add it to your Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="26f2a-154">Em [https://github.com/twilio/twilio-java][twilio_java], você pode baixar as fontes GitHub e criar seu próprio JAR ou baixar um JAR predefinido (com ou sem dependências).</span><span class="sxs-lookup"><span data-stu-id="26f2a-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="26f2a-155">Certifique-se de que o armazenamento de chaves **cacerts** do JDK contém o certificado de Autoridade de Certificação Segura Equifax com impressão digital MD5 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (o número de série é 35:DE:F4:CF e a impressão digital SHA1 é D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="26f2a-155">Ensure your JDK's **cacerts** keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="26f2a-156">Esse é o certificado de AC (autoridade de certificação) do serviço [https://api.twilio.com][twilio_api_service], que é chamado quando você usa APIs da Twilio.</span><span class="sxs-lookup"><span data-stu-id="26f2a-156">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="26f2a-157">Para obter informações sobre como assegurar que o armazenamento de chaves **cacerts** do seu JDK contenha o certificado de autoridade de certificação correto, consulte [Adicionando um certificado ao repositório de certificados de autoridade de certificação do Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="26f2a-157">For information about ensuring your JDK's **cacerts** keystore contains the correct CA certificate, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="26f2a-158">Instruções detalhadas para usar a biblioteca de cliente do Twilio para Java estão disponíveis em [Como fazer uma chamada telefônica usando Twilio em um aplicativo Java no Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="26f2a-158">Detailed instructions for using the Twilio client library for Java are available at [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="26f2a-159"><a id="configure_app"></a>Configurar seu aplicativo para usar bibliotecas Twilio</span><span class="sxs-lookup"><span data-stu-id="26f2a-159"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="26f2a-160">Dentro de seu código, você pode adicionar instruções de **importação** na parte superior dos seus arquivos de origem dos pacotes ou classes do Twilio que você deseja usar em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26f2a-160">Within your code, you can add **import** statements at the top of your source files for the Twilio packages or classes you want to use in your application.</span></span>

<span data-ttu-id="26f2a-161">Para arquivos de origem Java:</span><span class="sxs-lookup"><span data-stu-id="26f2a-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="26f2a-162">Para arquivos de origem Java Server Page (JSP):</span><span class="sxs-lookup"><span data-stu-id="26f2a-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="26f2a-163">Dependendo dos pacotes ou classes do Twilio que você deseja usar, as instruções de **importação** podem ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="26f2a-163">Depending on which Twilio packages or classes you want to use, your **import** statements may be different.</span></span>

## <span data-ttu-id="26f2a-164"><a id="howto_make_call"></a>Como fazer uma chamada externa</span><span class="sxs-lookup"><span data-stu-id="26f2a-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="26f2a-165">Abaixo é mostrado como fazer uma chamada externa usando a classe **Call**.</span><span class="sxs-lookup"><span data-stu-id="26f2a-165">The following shows how to make an outgoing call using the **Call** class.</span></span> <span data-ttu-id="26f2a-166">Esse código também usa um site fornecido pelo Twilio para retornar a resposta TwiML (Linguagem de Marcação do Twilio).</span><span class="sxs-lookup"><span data-stu-id="26f2a-166">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="26f2a-167">Substitua os valores dos números telefônicos **de** e **para** e certifique-se de verificar o número telefônico **de** da sua conta do Twilio antes de executar o código.</span><span class="sxs-lookup"><span data-stu-id="26f2a-167">Substitute your values for the **from** and **to** phone numbers, and ensure that you verify the **from** phone number for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare To and From numbers
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="26f2a-168">Para obter mais informações sobre os parâmetros passados para o método **Call.creator**, consulte [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="26f2a-168">For more information about the parameters passed in to the **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="26f2a-169">Como mencionado, esse código utiliza um site fornecido pelo Twilio para retornar a resposta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="26f2a-169">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="26f2a-170">Em vez disso, você pode usar seu próprio site para fornecer a resposta de TwiML; para obter mais informações, consulte [Como fornecer respostas de TwiML em um aplicativo Java no Azure](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="26f2a-170">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="26f2a-171"><a id="howto_send_sms"></a>Como enviar uma mensagem de SMS</span><span class="sxs-lookup"><span data-stu-id="26f2a-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="26f2a-172">O conteúdo abaixo mostra como enviar uma mensagem SMS usando a classe **Message**.</span><span class="sxs-lookup"><span data-stu-id="26f2a-172">The following shows how to send an SMS message using the **Message** class.</span></span> <span data-ttu-id="26f2a-173">O número **de**, **4155992671**, é fornecido pelo Twilio para contas de avaliação para envio de mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="26f2a-173">The **from** number, **4155992671**, is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="26f2a-174">O número **para** deve ser verificado para sua conta de Twilio antes da execução do código.</span><span class="sxs-lookup"><span data-stu-id="26f2a-174">The **to** number must be verified for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare To and From numbers and the Body of the SMS message
    PhoneNumber to = new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, To and Body values
    // then send the SMS message by calling the create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="26f2a-175">Para obter mais informações sobre os parâmetros passados para o método **Message.creator**, consulte [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="26f2a-175">For more information about the parameters passed in to the **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="26f2a-176"><a id="howto_provide_twiml_responses"></a>Como fornecer respostas TwiML de seu próprio site</span><span class="sxs-lookup"><span data-stu-id="26f2a-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="26f2a-177">Quando o aplicativo iniciar uma chamada para a API do Twilio, por exemplo, por meio do método **CallCreator.create**, o Twilio enviará a solicitação para uma URL que deverá retornar uma resposta em TwiML.</span><span class="sxs-lookup"><span data-stu-id="26f2a-177">When your application initiates a call to the Twilio API, for example via the **CallCreator.create** method, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="26f2a-178">O exemplo acima usa a URL fornecida pelo Twilio [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="26f2a-178">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="26f2a-179">(O TwiML destina-se ao uso pelos serviços Web, mas você pode exibir o TwiML no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="26f2a-179">(While TwiML is designed for use by Web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="26f2a-180">Por exemplo, clique em [http://twimlets.com/message][twimlet_message_url] para ver um elemento **&lt;Response&gt;** vazio; como outro exemplo, clique em [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] para ver um elemento **&lt;Response&gt;** que contém um elemento **&lt;Say&gt;**.)</span><span class="sxs-lookup"><span data-stu-id="26f2a-180">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] to see a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="26f2a-181">Em vez de contar com a URL fornecida pela Twilio, você pode criar seu próprio site URL que retorna respostas HTTP.</span><span class="sxs-lookup"><span data-stu-id="26f2a-181">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="26f2a-182">Você pode criar o site em qualquer linguagem que retorna respostas HTTP; este tópico pressupõe que você hospedará a URL em uma página JSP.</span><span class="sxs-lookup"><span data-stu-id="26f2a-182">You can create the site in any language that returns HTTP responses; this topic assumes you'll be hosting the URL in a JSP page.</span></span>

<span data-ttu-id="26f2a-183">A página JSP seguinte resulta em uma resposta em TwiML que diz **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="26f2a-183">The following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="26f2a-184">na chamada.</span><span class="sxs-lookup"><span data-stu-id="26f2a-184">on the call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="26f2a-185">A página JSP seguinte resulta em uma resposta de TwiML que diz algum texto, tem várias pausas e diz informações sobre a versão de API do Twilio e o nome da função do Azure.</span><span class="sxs-lookup"><span data-stu-id="26f2a-185">The following JSP page results in a TwiML response that says some text, has several pauses, and says information about the Twilio API version and the Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>The Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>The Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="26f2a-186">O parâmetro **ApiVersion** está disponível nas solicitações de voz do Twilio (não nas solicitações de SMS).</span><span class="sxs-lookup"><span data-stu-id="26f2a-186">The **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="26f2a-187">Para ver os parâmetros de solicitação disponíveis para solicitações de SMS e voz do Twilio, consulte <https://www.twilio.com/docs/api/twiml/twilio_request> e <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="26f2a-187">To see the available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="26f2a-188">A variável de ambiente **RoleName** está disponível como parte de uma implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="26f2a-188">The **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="26f2a-189">(Se você deseja adicionar variáveis de ambiente personalizadas para que elas possam ser detectadas de **System.getenv**, consulte a seção variáveis de ambiente em [Diversos parâmetros de configuração de função][misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="26f2a-189">(If you want to add custom environment variables so they could be picked up from **System.getenv**, see the environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="26f2a-190">Após você definir a página JSP para fornecer respostas TwiML, use a URL da página JSP conforme a URL passada para o método **Call.creator**.</span><span class="sxs-lookup"><span data-stu-id="26f2a-190">Once you have your JSP page set up to provide TwiML responses, use the URL of the JSP page as the URL passed into the **Call.creator** method.</span></span> <span data-ttu-id="26f2a-191">Por exemplo, se você tiver um aplicativo Web chamado MyTwiML implantado em um serviço hospedado do Azure e o nome da página JSP for mytwiml.jsp, a URL poderá ser passada para **Call.creator** conforme mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="26f2a-191">For example, if you have a Web application named MyTwiML deployed to an Azure hosted service, and the name of the JSP page is mytwiml.jsp, the URL can be passed to **Call.creator** as shown in the following:</span></span>

```java
    // Declare To and From numbers and the URL of your JSP page
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="26f2a-192">Outra opção para responder com TwiML é por meio da classe **VoiceResponse**, que está disponível no pacote **com.twilio.twiml**.</span><span class="sxs-lookup"><span data-stu-id="26f2a-192">Another option for responding with TwiML is via the **VoiceResponse** class, which is available in the **com.twilio.twiml** package.</span></span>

<span data-ttu-id="26f2a-193">Para obter informações adicionais sobre como usar Twilio no Azure com Java, consulte [Como fazer uma chamada telefônica usando Twilio em um aplicativo Java no Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="26f2a-193">For additional information about using Twilio in Azure with Java, see [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="26f2a-194"><a id="AdditionalServices"></a>Como Usar os Serviços Adicionais do Twilio</span><span class="sxs-lookup"><span data-stu-id="26f2a-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="26f2a-195">Além dos exemplos mostrados aqui, o Twilio oferece APIs baseadas na Web que podem ser usadas para aproveitar a funcionalidade adicional do Twilio do aplicativo Azure.</span><span class="sxs-lookup"><span data-stu-id="26f2a-195">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="26f2a-196">Para obter detalhes completos, consulte a [Documentação da API do Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="26f2a-196">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="26f2a-197"><a id="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26f2a-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="26f2a-198">Agora que você já conhece os princípios do serviço Twilio, acesse estes links para saber mais:</span><span class="sxs-lookup"><span data-stu-id="26f2a-198">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="26f2a-199">[Diretrizes de segurança do Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="26f2a-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="26f2a-200">[Código de Exemplo e Procedimentos do Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="26f2a-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="26f2a-201">[Tutoriais do Guia de início rápido do Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="26f2a-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="26f2a-202">[Twilio no GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="26f2a-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="26f2a-203">[Fale com o suporte do Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="26f2a-203">[Talk to Twilio Support][twilio_support]</span></span>

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
