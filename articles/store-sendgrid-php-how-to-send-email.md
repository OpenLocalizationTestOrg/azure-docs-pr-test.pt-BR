---
title: "saudação de toouse aaaHow SendGrid serviço de email (PHP) | Microsoft Docs"
description: "Saiba como enviar email com hello SendGrid serviço de email no Azure. Exemplos de código escritos em PHP."
documentationcenter: php
services: 
manager: sendgrid
editor: mollybos
author: thinkingserious
ms.assetid: 51a9928a-4c9e-4b0a-aca8-9a408aeb6f47
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork; matt.bernier@sendgrid.com
ms.openlocfilehash: 0076e56dc185cb8f52e629395e7d2c143cb5cfa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a>Como tooUse Olá SendGrid o serviço de Email do PHP
Este guia demonstra como tooperform as tarefas de programação comuns com hello SendGrid email serviço no Azure. exemplos de saudação são gravados em PHP.
Olá cenários abordados incluem **construindo email**, **enviar email**, e **adicionar anexos**. Para obter mais informações sobre SendGrid e enviar email, consulte Olá [próximas etapas](#next-steps) seção.

## <a name="what-is-hello-sendgrid-email-service"></a>O que é Olá SendGrid serviço de Email?
SendGrid é um [serviço de email baseado em nuvem] que fornece uma [entrega de email transacional], escalabilidade e análise em tempo real confiáveis com APIs flexíveis que facilitam a integração personalizada. Os cenários comuns de uso do SendGrid incluem:

* Enviar automaticamente confirmações toocustomers
* Administração de listas de distribuição para enviar aos clientes mensalmente panfletos eletrônicos e ofertas especiais
* Coleta de métrica em tempo real para, por exemplo, email bloqueado e capacidade de resposta do cliente
* Gerando relatórios toohelp identificar tendências
* Encaminhamento de consultas dos clientes
* Notificações de email de seu aplicativo

Para obter mais informações, consulte [https://sendgrid.com][https://sendgrid.com].

## <a name="create-a-sendgrid-account"></a>Criar uma conta do SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a>Usando SendGrid de seu aplicativo PHP
O uso do SendGrid em um aplicativo PHP Azure não exige configuração ou codificação especial. Como SendGrid é um serviço, ele pode ser acessado em exatamente Olá mesmo modo de um aplicativo em nuvem como ela pode de um aplicativo local.

## <a name="how-to-send-an-email"></a>Como: enviar um email
Você pode enviar emails usando SMTP ou Olá Web API fornecida pelo SendGrid.

### <a name="smtp-api"></a>API do SMTP
email toosend usando Olá SendGrid SMTP API, use *Mailer Swift*, uma biblioteca de componente de envio de emails de aplicativos PHP. Você pode baixar Olá *Mailer Swift* biblioteca de [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (use [criador] tooinstall Mensageiro SWIFT). Enviar email com biblioteca de saudação envolve a criação de instâncias do <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, e <span class="auto-style2">Swift\_mensagem </span> classes, configurando as propriedades apropriadas e, em seguida, chamar o <span class="auto-style2">Swift\_Mailer::send</span> método.

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello receiver is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
     $html = "<html>
           <head></head>
           <body>
               <p>Hi!<br>
                   How are you?<br>
               </p>
           </body>
           </html>";
     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');
     // Email recipients
     $too= array(
           'john@contoso.com'=>'Destination 1 Name',
           'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a>API Web
Usar do PHP [curl função] [ curl function] toosend email usando Olá API da Web do SendGrid.

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $params = array(
          'api_user' => $user,
          'api_key' => $pass,
          'to' => 'john@contoso.com',
          'subject' => 'testing from curl',
          'html' => 'testing body',
          'text' => 'testing body',
          'from' => 'anna@contoso.com',
       );

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

Web API do SendGrid é muito semelhante tooa API REST, mas não é realmente uma API RESTful porque, na maioria das chamadas, ambos OBTÉM e verbos POST podem ser usados intercambiavelmente.

## <a name="how-to-add-an-attachment"></a>Como: adicionar um anexo
### <a name="smtp-api"></a>API do SMTP
Enviar um anexo usando Olá SMTP API envolve uma linha adicional de script de exemplo do código toohello para enviar um email com Swift Mailer.

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello reciever is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
      $html = "<html>
          <head></head>
          <body>
             <p>Hi!<br>
                How are you?<br>
             </p>
          </body>
          </html>";

     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');

     // Email recipients
     $too= array(
          'john@contoso.com'=>'Destination 1 Name',
          'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

linha de código adicional Olá é o seguinte:

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

Esta linha de código chamadas Olá método attach no <span class="auto-style2">Swift\_mensagem</span> de objeto e usa o método estático <span class="auto-style2">fromPath</span> no <span class="auto-style2">Swift\_anexo</span>classe tooget e anexar uma mensagem de tooa do arquivo.

### <a name="web-api"></a>API Web
Enviar um anexo usando Olá API da Web é muito semelhante toosending usando um email Olá API da Web. No entanto, observe que no exemplo hello seguir, a matriz de parâmetros Olá deve conter este elemento:

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

Exemplo:

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $fileName = 'myfile';
     $filePath = dirname(__FILE__);

     $params = array(
         'api_user' => $user,
         'api_key' => $pass,
         'to' =>'john@contoso.com',
         'subject' => 'test of file sends',
         'html' => '<p> hello HTML </p>',
         'text' => 'hello plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Como: usar filtros tooEnable rodapés, acompanhamento e análise
SendGrid fornece a funcionalidade de email adicionais por meio do uso de saudação 'filtros'. Essas são as configurações que podem ser adicionadas tooan a mensagem de email para habilitar a funcionalidade específica, como habilitar o controle de clique, do Google analytics, assinatura de controle, e assim por diante.

Filtros podem ser aplicadas tooa mensagem usando a propriedade de filtros de saudação. Cada filtro é especificado por um hash que possui configurações específicas de filtro. O exemplo a seguir habilita o filtro de rodapé hello e especifica uma mensagem de texto que será anexado toohello inferior saudação da mensagem de email.
Para este exemplo, usaremos a [biblioteca de sendgrid-php].
Use [criador] tooinstall biblioteca:

    php composer.phar require sendgrid/sendgrid 2.1.1

Exemplo:    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // hello list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request tooSendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify hello names of hello recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of hello above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled hello footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // hello subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy hello user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $too= 'john@contoso.com';

     # Create hello body of hello message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of hello email
     # if hello receiver is able tooview html emails then only hello html
     # email will be displayed

     /*
      * Note hello variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment toocall you at -time- EST toodiscuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     toocall you at -time- EST toodiscuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach hello body of hello email
     $email->setFrom($from);
     $email->setHtml($html);
     $email->addTo($to);
     $email->setText($text);

     // Your SendGrid account credentials
     $username = 'sendgridusername@yourdomain.com';
     $password = 'example';

     // Create SendGrid object
     $sendgrid = new SendGrid($username, $password);

     // send message
     $response = $sendgrid->send($email);

     print_r($response);

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas sobre Olá Olá serviço de Email do SendGrid, siga essas toolearn links mais.

* Documentação do SendGrid: <https://sendgrid.com/docs>
* Biblioteca de SendGrid PHP: <https://github.com/sendgrid/sendgrid-php>
* Oferta especial do SendGrid para clientes Azure: <https://sendgrid.com/windowsazure.html>

Para obter mais informações, consulte também Olá [Centro de desenvolvedores PHP](/develop/php/).

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
[serviço de email baseado em nuvem]: https://sendgrid.com/email-solutions
[entrega de email transacional]: https://sendgrid.com/transactional-email
[biblioteca de sendgrid-php]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1
[criador]: https://getcomposer.org/download/
