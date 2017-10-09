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
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="70758-103">Como tooSend Email usando o SendGrid do Java em uma implantação do Azure</span><span class="sxs-lookup"><span data-stu-id="70758-103">How tooSend Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="70758-104">Olá exemplo a seguir mostra como você pode usar o SendGrid toosend emails de uma página da web hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="70758-104">hello following example shows you how you can use SendGrid toosend emails from a web page hosted in Azure.</span></span> <span data-ttu-id="70758-105">aplicativo resultante Hello solicitará usuário Olá valores de email, conforme mostrado na seguinte captura de tela de saudação.</span><span class="sxs-lookup"><span data-stu-id="70758-105">hello resulting application will prompt hello user for email values, as shown in hello following screen shot.</span></span>

![Formulário de email][emailform]

<span data-ttu-id="70758-107">Olá resultante email terá aparência semelhante toohello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="70758-107">hello resulting email will look similar toohello following screen shot.</span></span>

![Mensagem de email][emailsent]

<span data-ttu-id="70758-109">Você precisará toodo Olá seguinte código Olá toouse neste tópico:</span><span class="sxs-lookup"><span data-stu-id="70758-109">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="70758-110">Obter Olá JARs javax.mail, por exemplo, de <http://www.oracle.com/technetwork/java/javamail/index.html>.</span><span class="sxs-lookup"><span data-stu-id="70758-110">Obtain hello javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="70758-111">Adicione Olá JARs tooyour caminho de compilação de Java.</span><span class="sxs-lookup"><span data-stu-id="70758-111">Add hello JARs tooyour Java build path.</span></span>
3. <span data-ttu-id="70758-112">Se você estiver usando o Eclipse toocreate este aplicativo Java, você pode incluir bibliotecas do SendGrid Olá em seu arquivo de implantação de aplicativo (WAR) usando o recurso de assembly de implantação do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="70758-112">If you are using Eclipse toocreate this Java application, you can include hello SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="70758-113">Se você não estiver usando o Eclipse toocreate este aplicativo Java, certifique-se de bibliotecas Olá estão incluídas no hello mesma função do Azure como o caminho de classe Java toohello de aplicativo e adicionado de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70758-113">If you are not using Eclipse toocreate this Java application, ensure hello libraries are included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>

<span data-ttu-id="70758-114">Você também deve ter seu próprio nome de usuário do SendGrid e a senha, o email do toobe toosend capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="70758-114">You must also have your own SendGrid username and password, toobe able toosend hello email.</span></span> <span data-ttu-id="70758-115">tooget iniciado com SendGrid, consulte [como toosend de email usando o SendGrid do Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="70758-115">tooget started with SendGrid, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="70758-116">Além disso, a familiaridade com informações de saudação em [criando um aplicativo Hello World para Azure no Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), ou com outras técnicas para hospedar aplicativos do Java no Azure, se você não estiver usando o Eclipse, é altamente recomendável.</span><span class="sxs-lookup"><span data-stu-id="70758-116">Additionally, familiarity with hello information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="70758-117">Criar um formulário da web para enviar email</span><span class="sxs-lookup"><span data-stu-id="70758-117">Create a web form for sending email</span></span>
<span data-ttu-id="70758-118">saudação de código a seguir mostra como toocreate uma web formam tooretrieve dados do usuário para enviar email.</span><span class="sxs-lookup"><span data-stu-id="70758-118">hello following code shows how toocreate a web form tooretrieve user data for sending email.</span></span> <span data-ttu-id="70758-119">Para fins deste conteúdo, é chamado de arquivo JSP de saudação **emailform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="70758-119">For purposes of this content, hello JSP file is named **emailform.jsp**.</span></span>

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

## <a name="create-hello-code-toosend-hello-email"></a><span data-ttu-id="70758-120">Criar hello código toosend Olá email</span><span class="sxs-lookup"><span data-stu-id="70758-120">Create hello code toosend hello email</span></span>
<span data-ttu-id="70758-121">Olá código a seguir, que é chamado quando você concluir o formulário de saudação em emailform.jsp, cria a mensagem de saudação do email e a envia.</span><span class="sxs-lookup"><span data-stu-id="70758-121">hello following code, which is called when you complete hello form in emailform.jsp, creates hello email message and sends it.</span></span> <span data-ttu-id="70758-122">Para fins deste conteúdo, é chamado de arquivo JSP de saudação **sendemail.jsp**.</span><span class="sxs-lookup"><span data-stu-id="70758-122">For purposes of this content, hello JSP file is named **sendemail.jsp**.</span></span>

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

<span data-ttu-id="70758-123">Além disso toosending Olá email, emailform.jsp fornece um resultado para usuário Olá; um exemplo é hello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="70758-123">In addition toosending hello email, emailform.jsp provides a result for hello user; an example is hello following screen shot:</span></span>

![Resultado de envio de email][emailresult]

## <a name="next-steps"></a><span data-ttu-id="70758-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70758-125">Next steps</span></span>
<span data-ttu-id="70758-126">Implantar o emulador de computação do aplicativo toohello e dentro de um navegador executar emailform.jsp, insira valores no formulário de saudação, clique em **enviar este email**e, em seguida, consulte resulta em sendemail.jsp.</span><span class="sxs-lookup"><span data-stu-id="70758-126">Deploy your application toohello compute emulator and within a browser run emailform.jsp, enter values in hello form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="70758-127">Este código foi fornecido tooshow você como toouse SendGrid em Java no Azure.</span><span class="sxs-lookup"><span data-stu-id="70758-127">This code was provided tooshow you how toouse SendGrid in Java on Azure.</span></span> <span data-ttu-id="70758-128">Antes de implantar tooAzure em produção, talvez você queira tooadd mais tratamento de erros ou outros recursos.</span><span class="sxs-lookup"><span data-stu-id="70758-128">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="70758-129">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="70758-129">For example:</span></span> 

* <span data-ttu-id="70758-130">Você pode usar os blobs de armazenamento do Azure ou endereços de email do banco de dados SQL toostore e mensagens de email, em vez de usar um formulário da web.</span><span class="sxs-lookup"><span data-stu-id="70758-130">You could use Azure storage blobs or SQL Database toostore email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="70758-131">Para obter informações sobre o uso de blobs de armazenamento do Azure em Java, consulte [como tooUse Olá serviço de armazenamento de Blob do Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span><span class="sxs-lookup"><span data-stu-id="70758-131">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="70758-132">Para obter informações sobre como usar o Banco de Dados SQL no Java, consulte [Usando o Banco de Dados SQL no Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span><span class="sxs-lookup"><span data-stu-id="70758-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="70758-133">Você pode usar `RoleEnvironment.getConfigurationSettings` tooretrieve Olá SendGrid nome de usuário e senha de definições de configuração da implantação, em vez de usar Olá web formulário tooretrieve esses valores.</span><span class="sxs-lookup"><span data-stu-id="70758-133">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid username and password from your deployment's configuration settings, instead of using hello web form tooretrieve those values.</span></span> <span data-ttu-id="70758-134">Para obter informações sobre Olá `RoleEnvironment` de classe, consulte [hello usando biblioteca de tempo de execução de serviço do Azure no JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) e documentação de pacote de tempo de execução de serviço do Azure Olá em <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="70758-134">For information about hello `RoleEnvironment` class, see [Using hello Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and hello Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="70758-135">Para obter mais informações sobre como usar o SendGrid em Java, consulte [como toosend de email usando o SendGrid do Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="70758-135">For more information about using SendGrid in Java, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
