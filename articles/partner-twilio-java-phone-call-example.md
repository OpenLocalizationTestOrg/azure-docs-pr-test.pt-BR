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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a>Como tooMake uma chamada telefônica usando o Twilio em um aplicativo Java no Azure
Olá exemplo a seguir mostra como você pode usar Twilio toomake uma chamada de uma página da web hospedado no Azure. aplicativo resultante Hello solicitará usuário Olá valores de chamada telefônica, conforme mostrado na seguinte captura de tela de saudação.

![Formulário de chamada do Azure usando a Twilio e o Java][twilio_java]

Você precisará toodo Olá seguinte código Olá toouse neste tópico:

1. Obter uma conta e um token de autenticação da Twilio. tooget iniciado com Twilio, avaliar preços em [http://www.twilio.com/pricing][twilio_pricing]. Você pode se inscrever em [https://www.twilio.com/try-twilio][try_twilio]. Para obter informações sobre Olá API fornecida pelo Twilio, consulte [http://www.twilio.com/api][twilio_api].
2. Obter Olá Twilio JAR. Em [https://github.com/twilio/twilio-java][twilio_java_github], você pode baixar fontes do GitHub hello e criar seu próprios JAR ou baixar um JAR pré-criado (com ou sem dependências).
   código de saudação neste tópico foi escrito usando Olá pré-criadas JAR TwilioJava 3.3.8 com dependências.
3. Adicione Olá JAR tooyour caminho de compilação de Java.
4. Se você estiver usando o Eclipse toocreate este aplicativo Java, incluem hello JAR Twilio em seu arquivo de implantação de aplicativo (WAR) usando o recurso de assembly de implantação do Eclipse. Se você não estiver usando este aplicativo Java toocreate do Eclipse, certifique-se de saudação Twilio JAR estiver incluída em Olá mesma função do Azure como o caminho de classe Java toohello de aplicativo e adicionado de seu aplicativo.
5. Certifique-se de que sua chave cacerts contém o certificado de autoridade de certificação segura Equifax Olá com impressão digital de MD5 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Olá serial number 35:DE:F4:CF e impressão digital de saudação SHA1 D2:32:09:AD:23:D 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Este é o certificado de autoridade de certificado Olá para Olá [https://api.twilio.com] [ twilio_api_service] service, que é chamado quando você usar as APIs do Twilio. Para obter informações sobre como adicionar um repositório de cacert do JDK esta autoridade de certificação certificado tooyour, consulte [adicionando um toohello certificado repositório de certificados de autoridade de certificação de Java][add_ca_cert].

Além disso, a familiaridade com informações de saudação em [criando um Olá Olá mundo aplicativo usando o Kit de ferramentas do Azure para Eclipse][azure_java_eclipse_hello_world], ou com outras técnicas para hospedar aplicativos do Java no Azure se você não estiver usando o Eclipse, é altamente recomendável.

## <a name="create-a-web-form-for-making-a-call"></a>Criar um formulário da web para fazer uma chamada
saudação de código a seguir mostra como toocreate uma web formam tooretrieve dados de usuário para fazer uma chamada. Para o objetivo deste exemplo, um novo projeto Web dinâmico, chamado **TwilioCloud**, foi criado e **callform.jsp** foi adicionado como um arquivo JSP.

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

## <a name="create-hello-code-toomake-hello-call"></a>Crie uma chamada de Olá Olá código toomake
Olá código a seguir, que é chamado quando o usuário Olá conclui formulário Olá exibido pelo callform.jsp, cria a mensagem de saudação do chamada e gera chamada hello. Para fins deste exemplo, é chamado de arquivo JSP de saudação **makecall.jsp** e foi adicionado toohello **TwilioCloud** projeto. (Use sua conta do Twilio e autenticação de token em vez de valores de espaço reservado de saudação atribuídos muito**accountSID** e **authToken** no código de saudação abaixo.)

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

Além disso toomaking Olá chamada, makecall.jsp exibe o ponto de extremidade do hello Twilio, a versão da API e status de chamada hello. Um exemplo é hello captura de tela a seguir:

![Resposta de chamada do Azure usando a Twilio e o Java][twilio_java_response]

## <a name="run-hello-application"></a>Executar o aplicativo hello
A seguir são Olá toorun etapas de alto nível do aplicativo; detalhes sobre essas etapas podem ser encontradas em [criando um Olá Olá mundo aplicativo usando o Kit de ferramentas do Azure para Eclipse][azure_java_eclipse_hello_world].

1. Exportar sua toohello TwilioCloud WAR Azure **approot** pasta. 
2. Modificar **startup.cmd** toounzip sua TwilioCloud WAR.
3. Compile o aplicativo para o emulador de computação hello.
4. Inicie a implantação no emulador de computação hello.
5. Abra um navegador e execute o **http://localhost:8080/TwilioCloud/callform.jsp**.
6. Insira valores no formulário de saudação, clique em **fazer essa chamada**e, em seguida, veja os resultados de saudação em makecall.jsp.

Quando você estiver pronto toodeploy tooAzure, recompile para nuvem toohello de implantação, implantar tooAzure e executar http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp no navegador de saudação (substitua o valor de *your_hosted_name*).

## <a name="next-steps"></a>Próximas etapas
Este código foi fornecido tooshow você funcionalidade básica usando o Twilio em Java no Azure. Antes de implantar tooAzure em produção, talvez você queira tooadd mais tratamento de erros ou outros recursos. Por exemplo:

* Em vez de usar um formulário da web, você poderia usar blobs de armazenamento do Azure ou números de telefone de toostore do banco de dados SQL e chamar o texto. Para obter informações sobre o uso de blobs de armazenamento do Azure em Java, consulte [como tooUse Olá serviço de armazenamento de Blob do Java][howto_blob_storage_java]. Para obter informações sobre como usar o banco de dados SQL em Java, consulte [usando de banco de dados SQL em Java][howto_sql_azure_java].
* Você pode usar **RoleEnvironment.getConfigurationSettings** tooretrieve Olá ID da conta do Twilio e autenticação de token da implantação definições de configuração, em vez de codificar valores de saudação em makecall.jsp. Para obter informações sobre Olá **RoleEnvironment** de classe, consulte [hello usando biblioteca de tempo de execução de serviço do Azure no JSP] [ azure_runtime_jsp] e documentação de pacote de tempo de execução de serviço do Azure Olá em [http://dl.windowsazure.com/javadoc][azure_javadoc].
* código de makecall.jsp Olá atribui uma URL fornecida Twilio, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variável. Essa URL fornece uma resposta do Twilio Markup Language (TwiML) que informa o Twilio como tooproceed com hello chamar. Por exemplo, Olá TwiML retornado pode conter um ** &lt;diga&gt; ** verbo que resulta em texto que está sendo falado toohello chamada destinatário. Em vez de usar a URL fornecida pelo Twilio de saudação, você pode criar solicitação do tooTwilio toorespond seu próprio serviço; Para obter mais informações, consulte [como tooUse Twilio para recursos de SMS no Java e voz][howto_twilio_voice_sms_java]. Para obter mais informações sobre TwiML podem ser encontradas em [http://www.twilio.com/docs/api/twiml][twiml]e mais informações sobre ** &lt;diga&gt; ** e outros verbos Twilio podem ser encontrados em [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Leia as diretrizes de segurança Olá Twilio em [https://www.twilio.com/docs/security][twilio_docs_security].

Para obter informações adicionais sobre a Twilio, consulte [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Consulte também
* [Como tooUse Twilio para recursos de SMS no Java e voz][howto_twilio_voice_sms_java]
* [Adicionando um certificado toohello repositório de certificados de autoridade de certificação de Java][add_ca_cert]

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
