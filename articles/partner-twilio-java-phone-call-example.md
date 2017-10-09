---
title: aaaHow tooMake um telefonema do Twilio (Java) | Microsoft Docs
description: "Saiba como toomake um telefone chamar a partir de uma página da web usando o Twilio em um aplicativo Java no Azure."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 0381789e-e775-41a0-a784-294275192b1d
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 04fe5a78d431a79790dee3ca75c2b004aea4345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="ce59d-103">Como tooMake uma chamada telefônica usando o Twilio em um aplicativo Java no Azure</span><span class="sxs-lookup"><span data-stu-id="ce59d-103">How tooMake a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="ce59d-104">Olá exemplo a seguir mostra como você pode usar Twilio toomake uma chamada de uma página da web hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="ce59d-104">hello following example shows you how you can use Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="ce59d-105">aplicativo resultante Hello solicitará usuário Olá valores de chamada telefônica, conforme mostrado na seguinte captura de tela de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce59d-105">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Formulário de chamada do Azure usando a Twilio e o Java][twilio_java]

<span data-ttu-id="ce59d-107">Você precisará toodo Olá seguinte código Olá toouse neste tópico:</span><span class="sxs-lookup"><span data-stu-id="ce59d-107">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="ce59d-108">Obter uma conta e um token de autenticação da Twilio.</span><span class="sxs-lookup"><span data-stu-id="ce59d-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="ce59d-109">tooget iniciado com Twilio, avaliar preços em [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="ce59d-109">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="ce59d-110">Você pode se inscrever em [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="ce59d-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="ce59d-111">Para obter informações sobre Olá API fornecida pelo Twilio, consulte [http://www.twilio.com/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="ce59d-111">For information about hello API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="ce59d-112">Obter Olá Twilio JAR.</span><span class="sxs-lookup"><span data-stu-id="ce59d-112">Obtain hello Twilio JAR.</span></span> <span data-ttu-id="ce59d-113">Em [https://github.com/twilio/twilio-java][twilio_java_github], você pode baixar fontes do GitHub hello e criar seu próprios JAR ou baixar um JAR pré-criado (com ou sem dependências).</span><span class="sxs-lookup"><span data-stu-id="ce59d-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="ce59d-114">código de saudação neste tópico foi escrito usando Olá pré-criadas JAR TwilioJava 3.3.8 com dependências.</span><span class="sxs-lookup"><span data-stu-id="ce59d-114">hello code in this topic was written using hello pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="ce59d-115">Adicione Olá JAR tooyour caminho de compilação de Java.</span><span class="sxs-lookup"><span data-stu-id="ce59d-115">Add hello JAR tooyour Java build path.</span></span>
4. <span data-ttu-id="ce59d-116">Se você estiver usando o Eclipse toocreate este aplicativo Java, incluem hello JAR Twilio em seu arquivo de implantação de aplicativo (WAR) usando o recurso de assembly de implantação do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ce59d-116">If you are using Eclipse toocreate this Java application, include hello Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="ce59d-117">Se você não estiver usando este aplicativo Java toocreate do Eclipse, certifique-se de saudação Twilio JAR estiver incluída em Olá mesma função do Azure como o caminho de classe Java toohello de aplicativo e adicionado de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce59d-117">If you are not using Eclipse toocreate this Java application, ensure hello Twilio JAR is included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>
5. <span data-ttu-id="ce59d-118">Certifique-se de que sua chave cacerts contém o certificado de autoridade de certificação segura Equifax Olá com impressão digital de MD5 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Olá serial number 35:DE:F4:CF e impressão digital de saudação SHA1 D2:32:09:AD:23:D 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="ce59d-118">Ensure your cacerts keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="ce59d-119">Este é o certificado de autoridade de certificado Olá para Olá [https://api.twilio.com] [ twilio_api_service] service, que é chamado quando você usar as APIs do Twilio.</span><span class="sxs-lookup"><span data-stu-id="ce59d-119">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="ce59d-120">Para obter informações sobre como adicionar um repositório de cacert do JDK esta autoridade de certificação certificado tooyour, consulte [adicionando um toohello certificado repositório de certificados de autoridade de certificação de Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="ce59d-120">For information about adding this CA certificate tooyour JDK's cacert store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="ce59d-121">Além disso, a familiaridade com informações de saudação em [criando um Olá Olá mundo aplicativo usando o Kit de ferramentas do Azure para Eclipse][azure_java_eclipse_hello_world], ou com outras técnicas para hospedar aplicativos do Java no Azure se você não estiver usando o Eclipse, é altamente recomendável.</span><span class="sxs-lookup"><span data-stu-id="ce59d-121">Additionally, familiarity with hello information at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="ce59d-122">Criar um formulário da web para fazer uma chamada</span><span class="sxs-lookup"><span data-stu-id="ce59d-122">Create a web form for making a call</span></span>
<span data-ttu-id="ce59d-123">saudação de código a seguir mostra como toocreate uma web formam tooretrieve dados de usuário para fazer uma chamada.</span><span class="sxs-lookup"><span data-stu-id="ce59d-123">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="ce59d-124">Para o objetivo deste exemplo, um novo projeto Web dinâmico, chamado **TwilioCloud**, foi criado e **callform.jsp** foi adicionado como um arquivo JSP.</span><span class="sxs-lookup"><span data-stu-id="ce59d-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Automated call form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Make this call</b>.</p>
     <br/>
      <form action="makecall.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="callTo" value="" />
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="callFrom" value="" />
           </td>
         </tr>
         <tr>
           <td>Call message:</td>
           <td><input type="text" size=400 name="callText" value="Hello. This is hello call text. Good bye." />
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Make this call" />
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="ce59d-125">Crie uma chamada de Olá Olá código toomake</span><span class="sxs-lookup"><span data-stu-id="ce59d-125">Create hello code toomake hello call</span></span>
<span data-ttu-id="ce59d-126">Olá código a seguir, que é chamado quando o usuário Olá conclui formulário Olá exibido pelo callform.jsp, cria a mensagem de saudação do chamada e gera chamada hello.</span><span class="sxs-lookup"><span data-stu-id="ce59d-126">hello following code, which is called when hello user completes hello form displayed by callform.jsp, creates hello call message and generates hello call.</span></span> <span data-ttu-id="ce59d-127">Para fins deste exemplo, é chamado de arquivo JSP de saudação **makecall.jsp** e foi adicionado toohello **TwilioCloud** projeto.</span><span class="sxs-lookup"><span data-stu-id="ce59d-127">For purposes of this example, hello JSP file is named **makecall.jsp** and was added toohello **TwilioCloud** project.</span></span> <span data-ttu-id="ce59d-128">(Use sua conta do Twilio e autenticação de token em vez de valores de espaço reservado de saudação atribuídos muito**accountSID** e **authToken** no código de saudação abaixo.)</span><span class="sxs-lookup"><span data-stu-id="ce59d-128">(Use your Twilio account and authentication token instead of hello placeholder values assigned too**accountSID** and **authToken** in hello code below.)</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    import="java.util.*"
    import="com.twilio.*"
    import="com.twilio.sdk.*"
    import="com.twilio.sdk.resource.factory.*"
    import="com.twilio.sdk.resource.instance.*"
    pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Call processing happens here</title>
    </head>
    <body>
        <b>This is my make call page.</b><p/>
     <%
    try 
    {
         // Use your account SID and authentication token instead
         // of hello placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of hello Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve hello account, used later tooretrieve hello CallFactory.
         Account account = client.getAccount();

         // Display hello client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display hello API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve hello values entered by hello user.
         String callTo = request.getParameter("callTo");  
         // hello Outgoing Caller ID, used for hello From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in hello user's text with '%20', 
         // toomake hello text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using hello Twilio message and hello user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display hello message URL.
         out.println("<p>");
         out.println("hello URL is " + Url);
         out.println("</p>");

         // Place hello call From, tooand URL values into a hash map. 
         HashMap<String, String> params = new HashMap<String, String>();
         params.put("From", callFrom);
         params.put("To", callTo);
         params.put("Url", Url);

         CallFactory callFactory = account.getCallFactory();
         Call call = callFactory.create(params);
         out.println("<p>Call status: " + call.getStatus()  + "</p>"); 
    } 
    catch (TwilioRestException e) 
    {
        out.println("<p>TwilioRestException encountered: " + e.getMessage() + "</p>");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    catch (Exception e) 
    {
        out.println("<p>Exception encountered: " + e.getMessage() + "");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    %>
    </body>
    </html>

<span data-ttu-id="ce59d-129">Além disso toomaking Olá chamada, makecall.jsp exibe o ponto de extremidade do hello Twilio, a versão da API e status de chamada hello.</span><span class="sxs-lookup"><span data-stu-id="ce59d-129">In addition toomaking hello call, makecall.jsp displays hello Twilio endpoint, API version, and hello call status.</span></span> <span data-ttu-id="ce59d-130">Um exemplo é hello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce59d-130">An example is hello following screen shot:</span></span>

![Resposta de chamada do Azure usando a Twilio e o Java][twilio_java_response]

## <a name="run-hello-application"></a><span data-ttu-id="ce59d-132">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="ce59d-132">Run hello application</span></span>
<span data-ttu-id="ce59d-133">A seguir são Olá toorun etapas de alto nível do aplicativo; detalhes sobre essas etapas podem ser encontradas em [criando um Olá Olá mundo aplicativo usando o Kit de ferramentas do Azure para Eclipse][azure_java_eclipse_hello_world].</span><span class="sxs-lookup"><span data-stu-id="ce59d-133">Following are hello high-level steps toorun your application; details for these steps can be found at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="ce59d-134">Exportar sua toohello TwilioCloud WAR Azure **approot** pasta.</span><span class="sxs-lookup"><span data-stu-id="ce59d-134">Export your TwilioCloud WAR toohello Azure **approot** folder.</span></span> 
2. <span data-ttu-id="ce59d-135">Modificar **startup.cmd** toounzip sua TwilioCloud WAR.</span><span class="sxs-lookup"><span data-stu-id="ce59d-135">Modify **startup.cmd** toounzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="ce59d-136">Compile o aplicativo para o emulador de computação hello.</span><span class="sxs-lookup"><span data-stu-id="ce59d-136">Compile your application for hello compute emulator.</span></span>
4. <span data-ttu-id="ce59d-137">Inicie a implantação no emulador de computação hello.</span><span class="sxs-lookup"><span data-stu-id="ce59d-137">Start your deployment in hello compute emulator.</span></span>
5. <span data-ttu-id="ce59d-138">Abra um navegador e execute o **http://localhost:8080/TwilioCloud/callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="ce59d-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="ce59d-139">Insira valores no formulário de saudação, clique em **fazer essa chamada**e, em seguida, veja os resultados de saudação em makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="ce59d-139">Enter values in hello form, click **Make this call**, and then see hello results in makecall.jsp.</span></span>

<span data-ttu-id="ce59d-140">Quando você estiver pronto toodeploy tooAzure, recompile para nuvem toohello de implantação, implantar tooAzure e executar http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp no navegador de saudação (substitua o valor de *your_hosted_name*).</span><span class="sxs-lookup"><span data-stu-id="ce59d-140">When you are ready toodeploy tooAzure, recompile for deployment toohello cloud, deploy tooAzure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in hello browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce59d-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce59d-141">Next steps</span></span>
<span data-ttu-id="ce59d-142">Este código foi fornecido tooshow você funcionalidade básica usando o Twilio em Java no Azure.</span><span class="sxs-lookup"><span data-stu-id="ce59d-142">This code was provided tooshow you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="ce59d-143">Antes de implantar tooAzure em produção, talvez você queira tooadd mais tratamento de erros ou outros recursos.</span><span class="sxs-lookup"><span data-stu-id="ce59d-143">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="ce59d-144">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ce59d-144">For example:</span></span>

* <span data-ttu-id="ce59d-145">Em vez de usar um formulário da web, você poderia usar blobs de armazenamento do Azure ou números de telefone de toostore do banco de dados SQL e chamar o texto.</span><span class="sxs-lookup"><span data-stu-id="ce59d-145">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="ce59d-146">Para obter informações sobre o uso de blobs de armazenamento do Azure em Java, consulte [como tooUse Olá serviço de armazenamento de Blob do Java][howto_blob_storage_java].</span><span class="sxs-lookup"><span data-stu-id="ce59d-146">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="ce59d-147">Para obter informações sobre como usar o banco de dados SQL em Java, consulte [usando de banco de dados SQL em Java][howto_sql_azure_java].</span><span class="sxs-lookup"><span data-stu-id="ce59d-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="ce59d-148">Você pode usar **RoleEnvironment.getConfigurationSettings** tooretrieve Olá ID da conta do Twilio e autenticação de token da implantação definições de configuração, em vez de codificar valores de saudação em makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="ce59d-148">You could use **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in makecall.jsp.</span></span> <span data-ttu-id="ce59d-149">Para obter informações sobre Olá **RoleEnvironment** de classe, consulte [hello usando biblioteca de tempo de execução de serviço do Azure no JSP] [ azure_runtime_jsp] e documentação de pacote de tempo de execução de serviço do Azure Olá em [http://dl.windowsazure.com/javadoc][azure_javadoc].</span><span class="sxs-lookup"><span data-stu-id="ce59d-149">For information about hello **RoleEnvironment** class, see [Using hello Azure Service Runtime Library in JSP][azure_runtime_jsp] and hello Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="ce59d-150">código de makecall.jsp Olá atribui uma URL fornecida Twilio, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variável.</span><span class="sxs-lookup"><span data-stu-id="ce59d-150">hello makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable.</span></span> <span data-ttu-id="ce59d-151">Essa URL fornece uma resposta do Twilio Markup Language (TwiML) que informa o Twilio como tooproceed com hello chamar.</span><span class="sxs-lookup"><span data-stu-id="ce59d-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="ce59d-152">Por exemplo, Olá TwiML retornado pode conter um ** &lt;diga&gt; ** verbo que resulta em texto que está sendo falado toohello chamada destinatário.</span><span class="sxs-lookup"><span data-stu-id="ce59d-152">For example, hello TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="ce59d-153">Em vez de usar a URL fornecida pelo Twilio de saudação, você pode criar solicitação do tooTwilio toorespond seu próprio serviço; Para obter mais informações, consulte [como tooUse Twilio para recursos de SMS no Java e voz][howto_twilio_voice_sms_java].</span><span class="sxs-lookup"><span data-stu-id="ce59d-153">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="ce59d-154">Para obter mais informações sobre TwiML podem ser encontradas em [http://www.twilio.com/docs/api/twiml][twiml]e mais informações sobre ** &lt;diga&gt; ** e outros verbos Twilio podem ser encontrados em [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="ce59d-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="ce59d-155">Leia as diretrizes de segurança Olá Twilio em [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="ce59d-155">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="ce59d-156">Para obter informações adicionais sobre a Twilio, consulte [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="ce59d-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="ce59d-157">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ce59d-157">See Also</span></span>
* <span data-ttu-id="ce59d-158">[Como tooUse Twilio para recursos de SMS no Java e voz][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="ce59d-158">[How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="ce59d-159">[Adicionando um certificado toohello repositório de certificados de autoridade de certificação de Java][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="ce59d-159">[Adding a Certificate toohello Java CA Certificate Store][add_ca_cert]</span></span>

[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/api
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_java_github]: http://github.com/twilio/twilio-java
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[azure_java_eclipse_hello_world]: http://msdn.microsoft.com/library/windowsazure/hh690944.aspx
[howto_twilio_voice_sms_java]: partner-twilio-java-how-to-use-voice-sms.md
[howto_blob_storage_java]: http://www.windowsazure.com/develop/java/how-to-guides/blob-storage/
[howto_sql_azure_java]: http://msdn.microsoft.com/library/windowsazure/hh749029.aspx
[azure_runtime_jsp]: http://msdn.microsoft.com/library/windowsazure/hh690948.aspx
[azure_javadoc]: http://dl.windowsazure.com/javadoc
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[twilio_java]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaCallForm.jpg
[twilio_java_response]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaMakeCall.jpg
