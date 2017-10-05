---
title: "Como usar o serviço de email SendGrid (Java) | Microsoft Docs"
description: "Saiba como enviar email com o serviço de email SendGrid no Azure. Exemplos de códigos escritos em Java."
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: cc75c43e-ede9-492b-98c2-9147fcb92c21
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork
ms.openlocfilehash: 85a0e302626ca14ac039ee6f662f372ddbeb62c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java"></a><span data-ttu-id="89606-104">Como enviar emails usando o SendGrid com Java</span><span class="sxs-lookup"><span data-stu-id="89606-104">How to Send Email Using SendGrid from Java</span></span>
<span data-ttu-id="89606-105">Este guia demonstra como executar tarefas comuns de programação com o serviço de email SendGrid no Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="89606-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="89606-106">As amostras são gravadas em Java.</span><span class="sxs-lookup"><span data-stu-id="89606-106">The samples are written in Java.</span></span> <span data-ttu-id="89606-107">Os cenários abordados incluem a **construção de emails**, o **envio de emails**, a **adição de anexos**, o **uso de filtros** e a **atualização de propriedades**.</span><span class="sxs-lookup"><span data-stu-id="89606-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="89606-108">Para obter mais informações sobre o SendGrid e o envio de emails, consulte a seção [Próximas etapas](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="89606-108">For more information on SendGrid and sending email, see the [Next steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="89606-109">O que é o serviço de email SendGrid?</span><span class="sxs-lookup"><span data-stu-id="89606-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="89606-110">SendGrid é um [serviço de email baseado em nuvem] que fornece uma [entrega de email transacional], escalabilidade e análise em tempo real confiáveis com APIs flexíveis que facilitam a integração personalizada.</span><span class="sxs-lookup"><span data-stu-id="89606-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="89606-111">Os cenários comuns de uso do SendGrid incluem:</span><span class="sxs-lookup"><span data-stu-id="89606-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="89606-112">Envio automático de recibos para os clientes</span><span class="sxs-lookup"><span data-stu-id="89606-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="89606-113">Administração de listas de distribuição para enviar aos clientes mensalmente panfletos eletrônicos e ofertas especiais</span><span class="sxs-lookup"><span data-stu-id="89606-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="89606-114">Coleta de métrica em tempo real para, por exemplo, email bloqueado e capacidade de resposta do cliente</span><span class="sxs-lookup"><span data-stu-id="89606-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="89606-115">Geração de relatórios para ajudar a identificar as tendências</span><span class="sxs-lookup"><span data-stu-id="89606-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="89606-116">Encaminhamento de consultas dos clientes</span><span class="sxs-lookup"><span data-stu-id="89606-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="89606-117">Notificações de email de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="89606-117">Email notifications from your application</span></span>

<span data-ttu-id="89606-118">Para obter mais informações, consulte <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="89606-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="89606-119">Criar uma conta do SendGrid</span><span class="sxs-lookup"><span data-stu-id="89606-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-the-javaxmail-libraries"></a><span data-ttu-id="89606-120">Como usar as bibliotecas javax.mail</span><span class="sxs-lookup"><span data-stu-id="89606-120">How to: Use the javax.mail libraries</span></span>
<span data-ttu-id="89606-121">Obtenha as bibliotecas javax.mail, por exemplo, em <http://www.oracle.com/technetwork/java/javamail> e importe-as para o seu código.</span><span class="sxs-lookup"><span data-stu-id="89606-121">Obtain the javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="89606-122">Em um alto nível, o processo de usar a biblioteca javax.mail para enviar emails usando SMTP é fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="89606-122">At a high-level, the process for using the javax.mail library to send email using SMTP is to do the following:</span></span>

1. <span data-ttu-id="89606-123">Especificar os valores de SMTP, incluindo o servidor SMTP, que, para SendGrid, é smtp.sendgrid.net.</span><span class="sxs-lookup"><span data-stu-id="89606-123">Specify the SMTP values, including the SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

```
        import java.util.Properties;
        import javax.activation.*;
        import javax.mail.*;
        import javax.mail.internet.*;

        public class MyEmailer {
           private static final String SMTP_HOST_NAME = "smtp.sendgrid.net";
           private static final String SMTP_AUTH_USER = "your_sendgrid_username";
           private static final String SMTP_AUTH_PWD = "your_sendgrid_password";

           public static void main(String[] args) throws Exception{
               new MyEmailer().SendMail();
           }

           public void SendMail() throws Exception
           {
              Properties properties = new Properties();
                 properties.put("mail.transport.protocol", "smtp");
                 properties.put("mail.smtp.host", SMTP_HOST_NAME);
                 properties.put("mail.smtp.port", 587);
                 properties.put("mail.smtp.auth", "true");
                 // …
```

1. <span data-ttu-id="89606-124">Estenda a classe *javax.mail.Authenticator* e, na implementação do método *getPasswordAuthentication*, retorne seu nome de usuário e sua senha do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="89606-124">Extend the *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="89606-125">Criar uma sessão de email autenticada por meio de um objeto *javax.mail.Session* .</span><span class="sxs-lookup"><span data-stu-id="89606-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="89606-126">Criar sua mensagem e atribuir valores de conteúdo, **Para**, **De** e **Assunto**.</span><span class="sxs-lookup"><span data-stu-id="89606-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="89606-127">Isso é mostrado na seção [Como criar um email](#how-to-create-an-email).</span><span class="sxs-lookup"><span data-stu-id="89606-127">This is shown in the [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="89606-128">Enviar a mensagem por meio de um objeto *javax.mail.Transport* .</span><span class="sxs-lookup"><span data-stu-id="89606-128">Send the message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="89606-129">Isso é mostrado na seção [Como enviar um email] [Como enviar um email].</span><span class="sxs-lookup"><span data-stu-id="89606-129">This is shown in the [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="89606-130">Como criar um email</span><span class="sxs-lookup"><span data-stu-id="89606-130">How to: Create an email</span></span>
<span data-ttu-id="89606-131">O código a seguir mostra como especificar valores para um email.</span><span class="sxs-lookup"><span data-stu-id="89606-131">The following shows how to specify values for an email.</span></span>

    MimeMessage message = new MimeMessage(mailSession);
    Multipart multipart = new MimeMultipart("alternative");
    BodyPart part1 = new MimeBodyPart();
    part1.setText("Hello, Your Contoso order has shipped. Thank you, John");
    BodyPart part2 = new MimeBodyPart();
    part2.setContent(
        "<p>Hello,</p>
        <p>Your Contoso order has <b>shipped</b>.</p>
        <p>Thank you,<br>John</br></p>",
        "text/html");
    multipart.addBodyPart(part1);
    multipart.addBodyPart(part2);
    message.setFrom(new InternetAddress("john@contoso.com"));
    message.addRecipient(Message.RecipientType.TO,
       new InternetAddress("someone@example.com"));
    message.setSubject("Your recent order");
    message.setContent(multipart);

## <a name="how-to-send-an-email"></a><span data-ttu-id="89606-132">Como: enviar um email</span><span class="sxs-lookup"><span data-stu-id="89606-132">How to: Send an email</span></span>
<span data-ttu-id="89606-133">O código a seguir mostra como enviar um email.</span><span class="sxs-lookup"><span data-stu-id="89606-133">The following shows how to send an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect the transport object.
    transport.connect();
    // Send the message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close the connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="89606-134">Como: adicionar um anexo</span><span class="sxs-lookup"><span data-stu-id="89606-134">How to: Add an attachment</span></span>
<span data-ttu-id="89606-135">O código a seguir mostra como adicionar um anexo.</span><span class="sxs-lookup"><span data-stu-id="89606-135">The following code shows you how to add an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify the local file to attach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses the local file name as the attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="89606-136">Como: usar filtros para habilitar rodapés, rastreamento e análise</span><span class="sxs-lookup"><span data-stu-id="89606-136">How to: Use filters to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="89606-137">O SendGrid fornece a funcionalidade adicional de email por meio do uso de *filtros*.</span><span class="sxs-lookup"><span data-stu-id="89606-137">SendGrid provides additional email functionality through the use of *filters*.</span></span> <span data-ttu-id="89606-138">Essas são as configurações que podem ser adicionadas a uma mensagem de email para habilitar uma funcionalidade específica, como habilitar rastreamento de cliques, Google analytics, rastreamento de assinatura e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="89606-138">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="89606-139">Para obter uma lista completa de filtros, consulte [Configurações de filtro][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="89606-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="89606-140">O código a seguir mostra como inserir um filtro de rodapés que faça com que o texto HTML exibido na parte inferior do email seja enviado.</span><span class="sxs-lookup"><span data-stu-id="89606-140">The following shows how to insert a footer filter that results in HTML text appearing at the bottom of the email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="89606-141">Outro exemplo de um filtro é o acompanhamento de cliques.</span><span class="sxs-lookup"><span data-stu-id="89606-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="89606-142">Digamos que o texto do email contém um hiperlink, como o seguinte, e você deseja acompanhar a taxa de cliques:</span><span class="sxs-lookup"><span data-stu-id="89606-142">Let’s say that your email text contains a hyperlink, such as the following, and you want to track the click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is the body of the message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="89606-143">Para habilitar o acompanhamento de cliques, use o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="89606-143">To enable the click tracking, use the following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="89606-144">Como atualizar as propriedades do email</span><span class="sxs-lookup"><span data-stu-id="89606-144">How to: Update email properties</span></span>
<span data-ttu-id="89606-145">Algumas propriedades de email podem ser substituídas usando  **definir*propriedade** * ou ser acrescentados usando  **adicionar*propriedade** *.</span><span class="sxs-lookup"><span data-stu-id="89606-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="89606-146">Por exemplo, para especificar endereços para **ReplyTo** , use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="89606-146">For example, to specify **ReplyTo** addresses, use the following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="89606-147">Para adicionar um destinatário a **Cc** , use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="89606-147">To add a **Cc** recipient, use the following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="89606-148">Como: usar serviços adicionais do SendGrid</span><span class="sxs-lookup"><span data-stu-id="89606-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="89606-149">O SendGrid oferece APIs baseadas na Web que podem ser usadas para aproveitar a funcionalidade adicional do SendGrid do aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="89606-149">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="89606-150">Para obter detalhes completos, consulte a [Documentação da API do SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="89606-150">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="89606-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="89606-151">Next steps</span></span>
<span data-ttu-id="89606-152">Agora que você já conhece as noções básicas do serviço de email SendGrid, siga estes links para saber mais.</span><span class="sxs-lookup"><span data-stu-id="89606-152">Now that you’ve learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="89606-153">Exemplo que demonstra o uso do SendGrid em uma implantação do Azure: [Como enviar email usando o SendGrid do Java em uma implantação do Azure](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="89606-153">Sample that demonstrates using SendGrid in an Azure deployment: [How to send email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="89606-154">SDK do Java do SendGrid: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="89606-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="89606-155">Documentação da API do SendGrid: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="89606-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="89606-156">Oferta especial do SendGrid para clientes Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="89606-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
<span data-ttu-id="89606-157">[serviço de email baseado em nuvem]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="89606-157">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="89606-158">[entrega de email transacional]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="89606-158">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
