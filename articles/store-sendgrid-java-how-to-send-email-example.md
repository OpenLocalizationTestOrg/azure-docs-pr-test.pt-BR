---
title: aaastore-sendgrid-Java-How-to-Send-email-example
description: "Como toosend de email usando o SendGrid do Java em uma implantação do Azure"
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: af096a73-6985-4350-92e4-ce1722c8d72f
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: vibhork;dominic.may@sendgrid.com;elmer.thomas@sendgrid.com
ms.openlocfilehash: 51fde1fc71467f8252532b30d2f87856ec25067b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a>Como tooSend Email usando o SendGrid do Java em uma implantação do Azure
Olá exemplo a seguir mostra como você pode usar o SendGrid toosend emails de uma página da web hospedado no Azure. aplicativo resultante Hello solicitará usuário Olá valores de email, conforme mostrado na seguinte captura de tela de saudação.

![Formulário de email][emailform]

Olá resultante email terá aparência semelhante toohello captura de tela a seguir.

![Mensagem de email][emailsent]

Você precisará toodo Olá seguinte código Olá toouse neste tópico:

1. Obter Olá JARs javax.mail, por exemplo, de <http://www.oracle.com/technetwork/java/javamail/index.html>.
2. Adicione Olá JARs tooyour caminho de compilação de Java.
3. Se você estiver usando o Eclipse toocreate este aplicativo Java, você pode incluir bibliotecas do SendGrid Olá em seu arquivo de implantação de aplicativo (WAR) usando o recurso de assembly de implantação do Eclipse. Se você não estiver usando o Eclipse toocreate este aplicativo Java, certifique-se de bibliotecas Olá estão incluídas no hello mesma função do Azure como o caminho de classe Java toohello de aplicativo e adicionado de seu aplicativo.

Você também deve ter seu próprio nome de usuário do SendGrid e a senha, o email do toobe toosend capaz de saudação. tooget iniciado com SendGrid, consulte [como toosend de email usando o SendGrid do Java](store-sendgrid-java-how-to-send-email.md).

Além disso, a familiaridade com informações de saudação em [criando um aplicativo Hello World para Azure no Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), ou com outras técnicas para hospedar aplicativos do Java no Azure, se você não estiver usando o Eclipse, é altamente recomendável.

## <a name="create-a-web-form-for-sending-email"></a>Criar um formulário da web para enviar email
saudação de código a seguir mostra como toocreate uma web formam tooretrieve dados do usuário para enviar email. Para fins deste conteúdo, é chamado de arquivo JSP de saudação **emailform.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Send this email</b>.</p>
     <br/>
      <form action="sendemail.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="emailTo">
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="emailFrom">
           </td>
         </tr>
         <tr>
           <td>Subject:</td>
           <td><input type="text" size=100 name="emailSubject" value="My email subject">
           </td>
         </tr>
         <tr>
           <td>Text:</td>
           <td><input type="text" size=400 name="emailText" value="Hello,<p>This is my message.</p>Thank you." />
           </td>
         </tr>
         <tr>
           <td>SendGrid user name:</td>
           <td><input type="text" name="sendGridUser">
           </td>
         </tr>
         <tr>
           <td>SendGrid password:</td>
           <td><input type="password" name="sendGridPassword">
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Send this email">
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toosend-hello-email"></a>Criar hello código toosend Olá email
Olá código a seguir, que é chamado quando você concluir o formulário de saudação em emailform.jsp, cria a mensagem de saudação do email e a envia. Para fins deste conteúdo, é chamado de arquivo JSP de saudação **sendemail.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" import="javax.activation.*, javax.mail.*, javax.mail.internet.*, java.util.Date, java.util.Properties" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email processing happens here</title>
    </head>
    <body>
        <b>This is my send mail page.</b><p/>
     <%

     final String sendGridUser = request.getParameter("sendGridUser");
     final String sendGridPassword = request.getParameter("sendGridPassword");

     class SMTPAuthenticator extends Authenticator
     {
       public PasswordAuthentication getPasswordAuthentication()
       {
            String username = sendGridUser;
            String password = sendGridPassword;

            return new PasswordAuthentication(username, password);   
       }
     }
     try
     {

         // hello SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display hello email fields entered by hello user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create hello authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create hello mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information toostdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create hello message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify hello email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment hello following if you want tooadd a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment hello following if you want tooenable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect hello transport object.
         transport.connect();
         // Send hello message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close hello connection.
         transport.close();

        out.println("<p>Email processing completed.</p>");

     }
     catch (Exception e)
     {
         out.println("<p>Exception encountered: " + 
                            e.getMessage()     +
                            "</p>");   
     }
    %>

    </body>
    </html>

Além disso toosending Olá email, emailform.jsp fornece um resultado para usuário Olá; um exemplo é hello captura de tela a seguir:

![Resultado de envio de email][emailresult]

## <a name="next-steps"></a>Próximas etapas
Implantar o emulador de computação do aplicativo toohello e dentro de um navegador executar emailform.jsp, insira valores no formulário de saudação, clique em **enviar este email**e, em seguida, consulte resulta em sendemail.jsp.

Este código foi fornecido tooshow você como toouse SendGrid em Java no Azure. Antes de implantar tooAzure em produção, talvez você queira tooadd mais tratamento de erros ou outros recursos. Por exemplo: 

* Você pode usar os blobs de armazenamento do Azure ou endereços de email do banco de dados SQL toostore e mensagens de email, em vez de usar um formulário da web. Para obter informações sobre o uso de blobs de armazenamento do Azure em Java, consulte [como tooUse Olá serviço de armazenamento de Blob do Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/). Para obter informações sobre como usar o Banco de Dados SQL no Java, consulte [Usando o Banco de Dados SQL no Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).
* Você pode usar `RoleEnvironment.getConfigurationSettings` tooretrieve Olá SendGrid nome de usuário e senha de definições de configuração da implantação, em vez de usar Olá web formulário tooretrieve esses valores. Para obter informações sobre Olá `RoleEnvironment` de classe, consulte [hello usando biblioteca de tempo de execução de serviço do Azure no JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) e documentação de pacote de tempo de execução de serviço do Azure Olá em <http://dl.windowsazure.com/javadoc>.
* Para obter mais informações sobre como usar o SendGrid em Java, consulte [como toosend de email usando o SendGrid do Java](store-sendgrid-java-how-to-send-email.md).

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
