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
# <a name="how-toosend-email-using-sendgrid-from-java"></a>Como tooSend Email usando o SendGrid do Java
Este guia demonstra como tooperform as tarefas de programação comuns com o SendGrid email serviço no Azure. exemplos de saudação são escritos em Java. Olá cenários abordados incluem **construindo email**, **enviar email**, **adicionar anexos**, **usando filtros**e **Atualizando propriedades**. Para obter mais informações sobre SendGrid e enviar email, consulte Olá [próximas etapas](#next-steps) seção.

## <a name="what-is-hello-sendgrid-email-service"></a>O que é Olá SendGrid serviço de Email?
SendGrid é um [serviço de email baseado em nuvem] que fornece uma [entrega de email transacional], escalabilidade e análise em tempo real confiáveis com APIs flexíveis que facilitam a integração personalizada. Os cenários comuns de uso do SendGrid incluem:

* Enviar automaticamente confirmações toocustomers
* Administração de listas de distribuição para enviar aos clientes mensalmente panfletos eletrônicos e ofertas especiais
* Coleta de métrica em tempo real para, por exemplo, email bloqueado e capacidade de resposta do cliente
* Gerando relatórios toohelp identificar tendências
* Encaminhamento de consultas dos clientes
* Notificações de email de seu aplicativo

Para obter mais informações, consulte <http://sendgrid.com>.

## <a name="create-a-sendgrid-account"></a>Criar uma conta do SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a>Como: usar Olá javax.mail bibliotecas
Obter bibliotecas de javax.mail hello, por exemplo, de <http://www.oracle.com/technetwork/java/javamail> e importá-los em seu código. Em um nível alto, hello processo para usar o email do hello javax.mail biblioteca toosend usando SMTP é toodo Olá seguinte:

1. Especifica valores de SMTP hello, incluindo o servidor de SMTP hello, que é smtp.sendgrid.net para SendGrid.

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

1. Estender Olá *javax.mail.Authenticator* classe e na implementação do *getPasswordAuthentication* método, retornar o nome de usuário do SendGrid e a senha.  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. Criar uma sessão de email autenticada por meio de um objeto *javax.mail.Session* .  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. Criar sua mensagem e atribuir valores de conteúdo, **Para**, **De** e **Assunto**. Isso é mostrado no hello [como: criar um Email](#how-to-create-an-email) seção.
4. Enviar mensagem de saudação por meio de um *javax.mail.Transport* objeto. Isso é mostrado no hello [como: enviar um Email] [como: enviar um Email] seção.

## <a name="how-to-create-an-email"></a>Como criar um email
Veja a seguir Hello como toospecify valores para um email.

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

## <a name="how-to-send-an-email"></a>Como: enviar um email
Olá a seguir mostra como toosend um email.

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>Como: adicionar um anexo
Olá código a seguir mostra como tooadd um anexo.

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Como: Use os filtros tooenable rodapés, acompanhamento e análise
SendGrid fornece a funcionalidade de email adicionais por meio do uso de saudação do *filtros*. Essas são as configurações que podem ser adicionadas tooan a mensagem de email para habilitar a funcionalidade específica, como habilitar o controle de clique, do Google analytics, assinatura de controle, e assim por diante. Para obter uma lista completa de filtros, consulte [Configurações de filtro][Filter Settings].

* Veja a seguir Hello como tooinsert um rodapé de filtro que resulta em texto HTML que aparece na parte inferior de saudação do email hello está sendo enviado.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* Outro exemplo de um filtro é o acompanhamento de cliques. Digamos que seu texto de email contém um hiperlink, como hello seguinte e você quiser tootrack Olá clique taxa:

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* Olá tooenable clique em controle de alterações, use Olá código a seguir:

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>Como atualizar as propriedades do email
Algumas propriedades de email podem ser substituídas usando  **definir*propriedade** * ou ser acrescentados usando  **adicionar*propriedade** *.

Por exemplo, toospecify **ReplyTo** endereços, use a seguinte hello:

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

tooadd um **Cc** seguinte de saudação do destinatário, use:

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>Como: usar serviços adicionais do SendGrid
SendGrid oferece APIs baseado na web que você pode usar uma funcionalidade adicional tooleverage SendGrid de seu aplicativo do Azure. Para obter detalhes completos, consulte Olá [documentação da API do SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas sobre Olá Olá serviço de Email do SendGrid, siga essas toolearn links mais.

* Exemplo que demonstra como usar o SendGrid em uma implantação do Azure: [como toosend de email usando o SendGrid do Java em uma implantação do Azure](store-sendgrid-java-how-to-send-email-example.md)
* SDK do Java do SendGrid: <https://sendgrid.com/docs/Code_Examples/java.html>
* Documentação da API do SendGrid: <https://sendgrid.com/docs/API_Reference/index.html>
* Oferta especial do SendGrid para clientes Azure: <https://sendgrid.com/windowsazure.html>

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
