---
title: "saudação de toouse aaaHow SendGrid serviço de email (Java) | Microsoft Docs"
description: "Saiba como enviar email com hello SendGrid serviço de email no Azure. Exemplos de códigos escritos em Java."
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
ms.openlocfilehash: 542ce0003e94fc8f5551487d5a3cd6f75d27e8cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java"></a><span data-ttu-id="198f6-104">Como tooSend Email usando o SendGrid do Java</span><span class="sxs-lookup"><span data-stu-id="198f6-104">How tooSend Email Using SendGrid from Java</span></span>
<span data-ttu-id="198f6-105">Este guia demonstra como tooperform as tarefas de programação comuns com o SendGrid email serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="198f6-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="198f6-106">exemplos de saudação são escritos em Java.</span><span class="sxs-lookup"><span data-stu-id="198f6-106">hello samples are written in Java.</span></span> <span data-ttu-id="198f6-107">Olá cenários abordados incluem **construindo email**, **enviar email**, **adicionar anexos**, **usando filtros**e **Atualizando propriedades**.</span><span class="sxs-lookup"><span data-stu-id="198f6-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="198f6-108">Para obter mais informações sobre SendGrid e enviar email, consulte Olá [próximas etapas](#next-steps) seção.</span><span class="sxs-lookup"><span data-stu-id="198f6-108">For more information on SendGrid and sending email, see hello [Next steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="198f6-109">O que é Olá SendGrid serviço de Email?</span><span class="sxs-lookup"><span data-stu-id="198f6-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="198f6-110">SendGrid é um [serviço de email baseado em nuvem] que fornece uma [entrega de email transacional], escalabilidade e análise em tempo real confiáveis com APIs flexíveis que facilitam a integração personalizada.</span><span class="sxs-lookup"><span data-stu-id="198f6-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="198f6-111">Os cenários comuns de uso do SendGrid incluem:</span><span class="sxs-lookup"><span data-stu-id="198f6-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="198f6-112">Enviar automaticamente confirmações toocustomers</span><span class="sxs-lookup"><span data-stu-id="198f6-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="198f6-113">Administração de listas de distribuição para enviar aos clientes mensalmente panfletos eletrônicos e ofertas especiais</span><span class="sxs-lookup"><span data-stu-id="198f6-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="198f6-114">Coleta de métrica em tempo real para, por exemplo, email bloqueado e capacidade de resposta do cliente</span><span class="sxs-lookup"><span data-stu-id="198f6-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="198f6-115">Gerando relatórios toohelp identificar tendências</span><span class="sxs-lookup"><span data-stu-id="198f6-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="198f6-116">Encaminhamento de consultas dos clientes</span><span class="sxs-lookup"><span data-stu-id="198f6-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="198f6-117">Notificações de email de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="198f6-117">Email notifications from your application</span></span>

<span data-ttu-id="198f6-118">Para obter mais informações, consulte <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="198f6-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="198f6-119">Criar uma conta do SendGrid</span><span class="sxs-lookup"><span data-stu-id="198f6-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a><span data-ttu-id="198f6-120">Como: usar Olá javax.mail bibliotecas</span><span class="sxs-lookup"><span data-stu-id="198f6-120">How to: Use hello javax.mail libraries</span></span>
<span data-ttu-id="198f6-121">Obter bibliotecas de javax.mail hello, por exemplo, de <http://www.oracle.com/technetwork/java/javamail> e importá-los em seu código.</span><span class="sxs-lookup"><span data-stu-id="198f6-121">Obtain hello javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="198f6-122">Em um nível alto, hello processo para usar o email do hello javax.mail biblioteca toosend usando SMTP é toodo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="198f6-122">At a high-level, hello process for using hello javax.mail library toosend email using SMTP is toodo hello following:</span></span>

1. <span data-ttu-id="198f6-123">Especifica valores de SMTP hello, incluindo o servidor de SMTP hello, que é smtp.sendgrid.net para SendGrid.</span><span class="sxs-lookup"><span data-stu-id="198f6-123">Specify hello SMTP values, including hello SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

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

1. <span data-ttu-id="198f6-124">Estender Olá *javax.mail.Authenticator* classe e na implementação do *getPasswordAuthentication* método, retornar o nome de usuário do SendGrid e a senha.</span><span class="sxs-lookup"><span data-stu-id="198f6-124">Extend hello *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="198f6-125">Criar uma sessão de email autenticada por meio de um objeto *javax.mail.Session* .</span><span class="sxs-lookup"><span data-stu-id="198f6-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="198f6-126">Criar sua mensagem e atribuir valores de conteúdo, **Para**, **De** e **Assunto**.</span><span class="sxs-lookup"><span data-stu-id="198f6-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="198f6-127">Isso é mostrado no hello [como: criar um Email](#how-to-create-an-email) seção.</span><span class="sxs-lookup"><span data-stu-id="198f6-127">This is shown in hello [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="198f6-128">Enviar mensagem de saudação por meio de um *javax.mail.Transport* objeto.</span><span class="sxs-lookup"><span data-stu-id="198f6-128">Send hello message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="198f6-129">Isso é mostrado no hello [como: enviar um Email] [como: enviar um Email] seção.</span><span class="sxs-lookup"><span data-stu-id="198f6-129">This is shown in hello [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="198f6-130">Como criar um email</span><span class="sxs-lookup"><span data-stu-id="198f6-130">How to: Create an email</span></span>
<span data-ttu-id="198f6-131">Veja a seguir Hello como toospecify valores para um email.</span><span class="sxs-lookup"><span data-stu-id="198f6-131">hello following shows how toospecify values for an email.</span></span>

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

## <a name="how-to-send-an-email"></a><span data-ttu-id="198f6-132">Como: enviar um email</span><span class="sxs-lookup"><span data-stu-id="198f6-132">How to: Send an email</span></span>
<span data-ttu-id="198f6-133">Olá a seguir mostra como toosend um email.</span><span class="sxs-lookup"><span data-stu-id="198f6-133">hello following shows how toosend an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="198f6-134">Como: adicionar um anexo</span><span class="sxs-lookup"><span data-stu-id="198f6-134">How to: Add an attachment</span></span>
<span data-ttu-id="198f6-135">Olá código a seguir mostra como tooadd um anexo.</span><span class="sxs-lookup"><span data-stu-id="198f6-135">hello following code shows you how tooadd an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify hello local file tooattach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses hello local file name as hello attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="198f6-136">Como: Use os filtros tooenable rodapés, acompanhamento e análise</span><span class="sxs-lookup"><span data-stu-id="198f6-136">How to: Use filters tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="198f6-137">SendGrid fornece a funcionalidade de email adicionais por meio do uso de saudação do *filtros*.</span><span class="sxs-lookup"><span data-stu-id="198f6-137">SendGrid provides additional email functionality through hello use of *filters*.</span></span> <span data-ttu-id="198f6-138">Essas são as configurações que podem ser adicionadas tooan a mensagem de email para habilitar a funcionalidade específica, como habilitar o controle de clique, do Google analytics, assinatura de controle, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="198f6-138">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="198f6-139">Para obter uma lista completa de filtros, consulte [Configurações de filtro][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="198f6-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="198f6-140">Veja a seguir Hello como tooinsert um rodapé de filtro que resulta em texto HTML que aparece na parte inferior de saudação do email hello está sendo enviado.</span><span class="sxs-lookup"><span data-stu-id="198f6-140">hello following shows how tooinsert a footer filter that results in HTML text appearing at hello bottom of hello email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="198f6-141">Outro exemplo de um filtro é o acompanhamento de cliques.</span><span class="sxs-lookup"><span data-stu-id="198f6-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="198f6-142">Digamos que seu texto de email contém um hiperlink, como hello seguinte e você quiser tootrack Olá clique taxa:</span><span class="sxs-lookup"><span data-stu-id="198f6-142">Let’s say that your email text contains a hyperlink, such as hello following, and you want tootrack hello click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="198f6-143">Olá tooenable clique em controle de alterações, use Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="198f6-143">tooenable hello click tracking, use hello following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="198f6-144">Como atualizar as propriedades do email</span><span class="sxs-lookup"><span data-stu-id="198f6-144">How to: Update email properties</span></span>
<span data-ttu-id="198f6-145">Algumas propriedades de email podem ser substituídas usando  **definir*propriedade** * ou ser acrescentados usando  **adicionar*propriedade** *.</span><span class="sxs-lookup"><span data-stu-id="198f6-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="198f6-146">Por exemplo, toospecify **ReplyTo** endereços, use a seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="198f6-146">For example, toospecify **ReplyTo** addresses, use hello following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="198f6-147">tooadd um **Cc** seguinte de saudação do destinatário, use:</span><span class="sxs-lookup"><span data-stu-id="198f6-147">tooadd a **Cc** recipient, use hello following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="198f6-148">Como: usar serviços adicionais do SendGrid</span><span class="sxs-lookup"><span data-stu-id="198f6-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="198f6-149">SendGrid oferece APIs baseado na web que você pode usar uma funcionalidade adicional tooleverage SendGrid de seu aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="198f6-149">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="198f6-150">Para obter detalhes completos, consulte Olá [documentação da API do SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="198f6-150">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="198f6-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="198f6-151">Next steps</span></span>
<span data-ttu-id="198f6-152">Agora que você aprendeu as Noções básicas sobre Olá Olá serviço de Email do SendGrid, siga essas toolearn links mais.</span><span class="sxs-lookup"><span data-stu-id="198f6-152">Now that you’ve learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="198f6-153">Exemplo que demonstra como usar o SendGrid em uma implantação do Azure: [como toosend de email usando o SendGrid do Java em uma implantação do Azure](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="198f6-153">Sample that demonstrates using SendGrid in an Azure deployment: [How toosend email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="198f6-154">SDK do Java do SendGrid: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="198f6-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="198f6-155">Documentação da API do SendGrid: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="198f6-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="198f6-156">Oferta especial do SendGrid para clientes Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="198f6-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
[serviço de email baseado em nuvem]: https://sendgrid.com/email-solutions
[entrega de email transacional]: https://sendgrid.com/transactional-email
