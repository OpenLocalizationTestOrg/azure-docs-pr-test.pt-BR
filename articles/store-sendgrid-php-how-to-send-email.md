---
title: "Como usar o serviço de email SendGrid (PHP) | Microsoft Docs"
description: "Saiba como enviar email com o serviço de email SendGrid no Azure. Exemplos de código escritos em PHP."
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
ms.openlocfilehash: 523b986f66a2e48685e9707903194856f0dcf4a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-sendgrid-email-service-from-php"></a><span data-ttu-id="b722a-104">Como usar serviço de email SendGrid do PHP</span><span class="sxs-lookup"><span data-stu-id="b722a-104">How to Use the SendGrid Email Service from PHP</span></span>
<span data-ttu-id="b722a-105">Este guia demonstra como executar tarefas comuns de programação com o serviço de email SendGrid no Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="b722a-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="b722a-106">As amostras são escritas em PHP.</span><span class="sxs-lookup"><span data-stu-id="b722a-106">The samples are written in PHP.</span></span>
<span data-ttu-id="b722a-107">Os cenários abordados incluem **escrever email**, **enviar email**, and **adicionar anexos**.</span><span class="sxs-lookup"><span data-stu-id="b722a-107">The scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span></span> <span data-ttu-id="b722a-108">Para obter mais informações sobre o SendGrid e o envio de e-mails, consulte a seção [Próximas etapas](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="b722a-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="b722a-109">O que é o serviço de email SendGrid?</span><span class="sxs-lookup"><span data-stu-id="b722a-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="b722a-110">SendGrid é um [serviço de email baseado em nuvem] que fornece uma [entrega de email transacional], escalabilidade e análise em tempo real confiáveis com APIs flexíveis que facilitam a integração personalizada.</span><span class="sxs-lookup"><span data-stu-id="b722a-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="b722a-111">Os cenários comuns de uso do SendGrid incluem:</span><span class="sxs-lookup"><span data-stu-id="b722a-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="b722a-112">Envio automático de recibos para os clientes</span><span class="sxs-lookup"><span data-stu-id="b722a-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="b722a-113">Administração de listas de distribuição para enviar aos clientes mensalmente panfletos eletrônicos e ofertas especiais</span><span class="sxs-lookup"><span data-stu-id="b722a-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="b722a-114">Coleta de métrica em tempo real para, por exemplo, email bloqueado e capacidade de resposta do cliente</span><span class="sxs-lookup"><span data-stu-id="b722a-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="b722a-115">Geração de relatórios para ajudar a identificar as tendências</span><span class="sxs-lookup"><span data-stu-id="b722a-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="b722a-116">Encaminhamento de consultas dos clientes</span><span class="sxs-lookup"><span data-stu-id="b722a-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="b722a-117">Notificações de email de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b722a-117">Email notifications from your application</span></span>

<span data-ttu-id="b722a-118">Para obter mais informações, consulte [https://sendgrid.com][https://sendgrid.com].</span><span class="sxs-lookup"><span data-stu-id="b722a-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="b722a-119">Criar uma conta do SendGrid</span><span class="sxs-lookup"><span data-stu-id="b722a-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a><span data-ttu-id="b722a-120">Usando SendGrid de seu aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="b722a-120">Using SendGrid from your PHP Application</span></span>
<span data-ttu-id="b722a-121">O uso do SendGrid em um aplicativo PHP Azure não exige configuração ou codificação especial.</span><span class="sxs-lookup"><span data-stu-id="b722a-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span></span> <span data-ttu-id="b722a-122">Como o SendGrid é um serviço, ele pode ser acessado exatamente da mesma maneira de um aplicativo em nuvem ou de um aplicativo local.</span><span class="sxs-lookup"><span data-stu-id="b722a-122">Because SendGrid is a service, it can be accessed in exactly the same way from a cloud application as it can from an on-premises application.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="b722a-123">Como: enviar um email</span><span class="sxs-lookup"><span data-stu-id="b722a-123">How to: Send an Email</span></span>
<span data-ttu-id="b722a-124">É possível enviar emails usando o SMTP ou a API Web fornecida pelo SendGrid.</span><span class="sxs-lookup"><span data-stu-id="b722a-124">You can send email using either SMTP or the Web API provided by SendGrid.</span></span>

### <a name="smtp-api"></a><span data-ttu-id="b722a-125">API do SMTP</span><span class="sxs-lookup"><span data-stu-id="b722a-125">SMTP API</span></span>
<span data-ttu-id="b722a-126">Para enviar email usando a API do SMTP do SendGrid, use o *Swift Mailer*, uma biblioteca baseada em componente para envio de emails de aplicativos PHP.</span><span class="sxs-lookup"><span data-stu-id="b722a-126">To send email using the SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span></span> <span data-ttu-id="b722a-127">Você pode baixar a biblioteca do *Swift Mailer* em [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use o [Compositor] para instalar o Swift Mailer).</span><span class="sxs-lookup"><span data-stu-id="b722a-127">You can download the *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] to install Swift Mailer).</span></span> <span data-ttu-id="b722a-128">O envio de email pela biblioteca envolve a criação de instâncias do <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span> e classes do <span class="auto-style2">Swift\_Message</span>, a definição das propriedades adequadas e a chamada do método <span class="auto-style2">Swift\_Mailer::send</span>.</span><span class="sxs-lookup"><span data-stu-id="b722a-128">Sending email with the library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create the body of the message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of the email
      * If the receiver is able to view html emails then only the html
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
     $from = array('someone@example.com' => 'Name To Appear');
     // Email recipients
     $to = array(
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

     // attach the body of the email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out to '.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a><span data-ttu-id="b722a-129">API Web</span><span class="sxs-lookup"><span data-stu-id="b722a-129">Web API</span></span>
<span data-ttu-id="b722a-130">Use a [função de curl][curl function] do PHP para enviar email usando a API Web do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="b722a-130">Use PHP's [curl function][curl function] to send email using the SendGrid Web API.</span></span>

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

     // Tell curl to use HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is the body of the POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not to return headers, but do return the response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

<span data-ttu-id="b722a-131">A API Web do SendGrid é muito semelhante a uma API REST, embora ela não seja realmente uma API RESTful já que, na maioria das chamadas, ambos os verbos GET e POST podem ser usados de maneira alternada.</span><span class="sxs-lookup"><span data-stu-id="b722a-131">SendGrid's Web API is very similar to a REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span></span>

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="b722a-132">Como: adicionar um anexo</span><span class="sxs-lookup"><span data-stu-id="b722a-132">How to: Add an Attachment</span></span>
### <a name="smtp-api"></a><span data-ttu-id="b722a-133">API do SMTP</span><span class="sxs-lookup"><span data-stu-id="b722a-133">SMTP API</span></span>
<span data-ttu-id="b722a-134">O envio de um anexo usando a API do SMTP envolve uma linha adicional de código para o script de exemplo para enviar um email com Swift Mailer.</span><span class="sxs-lookup"><span data-stu-id="b722a-134">Sending an attachment using the SMTP API involves one additional line of code to the example script for sending an email with Swift Mailer.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create the body of the message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of the email
      * If the reciever is able to view html emails then only the html
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
     $from = array('someone@example.com' => 'Name To Appear');

     // Email recipients
     $to = array(
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

     // attach the body of the email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out to '.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

<span data-ttu-id="b722a-135">A linha de código adicional é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="b722a-135">The additional line of code is as follows:</span></span>

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

<span data-ttu-id="b722a-136">Essa linha de código chama o método anexar no objeto <span class="auto-style2">Swift\_Message</span> e usa o método estático <span class="auto-style2">fromPath</span> na classe <span class="auto-style2">Swift\_Attachment</span> para obter e anexar um arquivo a uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="b722a-136">This line of code calls the attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class to get and attach a file to a message.</span></span>

### <a name="web-api"></a><span data-ttu-id="b722a-137">API Web</span><span class="sxs-lookup"><span data-stu-id="b722a-137">Web API</span></span>
<span data-ttu-id="b722a-138">O envio de um anexo usando a API Web é muito semelhante ao envio de um email usando a API Web.</span><span class="sxs-lookup"><span data-stu-id="b722a-138">Sending an attachment using the Web API is very similar to sending an email using the Web API.</span></span> <span data-ttu-id="b722a-139">No entanto, observe que, no exemplo a seguir,a matriz de parâmetros deve conter este elemento:</span><span class="sxs-lookup"><span data-stu-id="b722a-139">However, note that in the example that follows, the parameter array must contain this element:</span></span>

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

<span data-ttu-id="b722a-140">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="b722a-140">Example:</span></span>

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
         'html' => '<p> the HTML </p>',
         'text' => 'the plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl to use HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is the body of the POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not to return headers, but do return the response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="b722a-141">Como: usar filtros para habilitar rodapés, rastreamento e análise</span><span class="sxs-lookup"><span data-stu-id="b722a-141">How to: Use Filters to Enable Footers, Tracking, and Analytics</span></span>
<span data-ttu-id="b722a-142">O SendGrid fornece a funcionalidade adicional de email por meio do uso de ‘filtros’.</span><span class="sxs-lookup"><span data-stu-id="b722a-142">SendGrid provides additional email functionality through the use of 'filters'.</span></span> <span data-ttu-id="b722a-143">Essas são as configurações que podem ser adicionadas a uma mensagem de email para habilitar uma funcionalidade específica, como habilitar rastreamento de cliques, Google analytics, rastreamento de assinatura e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="b722a-143">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span>

<span data-ttu-id="b722a-144">Os filtros podem ser aplicados a uma mensagem pela propriedade filtros.</span><span class="sxs-lookup"><span data-stu-id="b722a-144">Filters can be applied to a message by using the filters property.</span></span> <span data-ttu-id="b722a-145">Cada filtro é especificado por um hash que possui configurações específicas de filtro.</span><span class="sxs-lookup"><span data-stu-id="b722a-145">Each filter is specified by a hash containing filter-specific settings.</span></span> <span data-ttu-id="b722a-146">O exemplo a seguir ativa o filtro do rodapé e especifica uma mensagem de texto que será anexada na parte inferior da mensagem de email:</span><span class="sxs-lookup"><span data-stu-id="b722a-146">The following example enables the footer filter and specifies a text message that will be appended to the bottom of the email message.</span></span>
<span data-ttu-id="b722a-147">Para este exemplo, usaremos a [biblioteca de sendgrid-php].</span><span class="sxs-lookup"><span data-stu-id="b722a-147">For this example we will use [sendgrid-php library].</span></span>
<span data-ttu-id="b722a-148">Use o [Compositor] para instalar a biblioteca:</span><span class="sxs-lookup"><span data-stu-id="b722a-148">Use [Composer] to install library:</span></span>

    php composer.phar require sendgrid/sendgrid 2.1.1

<span data-ttu-id="b722a-149">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="b722a-149">Example:</span></span>    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // The list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request to SendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify the names of the recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of the above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled the footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // The subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy the user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $to = 'john@contoso.com';

     # Create the body of the message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of the email
     # if the receiver is able to view html emails then only the html
     # email will be displayed

     /*
      * Note the variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment to call you at -time- EST to discuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     to call you at -time- EST to discuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach the body of the email
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

## <a name="next-steps"></a><span data-ttu-id="b722a-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b722a-150">Next Steps</span></span>
<span data-ttu-id="b722a-151">Agora que você já conhece as noções básicas do serviço de email SendGrid, siga estes links para saber mais.</span><span class="sxs-lookup"><span data-stu-id="b722a-151">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="b722a-152">Documentação do SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="b722a-152">SendGrid documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="b722a-153">Biblioteca de SendGrid PHP: <https://github.com/sendgrid/sendgrid-php></span><span class="sxs-lookup"><span data-stu-id="b722a-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span></span>
* <span data-ttu-id="b722a-154">Oferta especial do SendGrid para clientes Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="b722a-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

<span data-ttu-id="b722a-155">Para saber mais, veja também a [Central de desenvolvedores do PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="b722a-155">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
<span data-ttu-id="b722a-156">[serviço de email baseado em nuvem]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="b722a-156">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="b722a-157">[entrega de email transacional]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="b722a-157">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
<span data-ttu-id="b722a-158">[biblioteca de sendgrid-php]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1</span><span class="sxs-lookup"><span data-stu-id="b722a-158">[sendgrid-php library]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1</span></span>
<span data-ttu-id="b722a-159">[Compositor]: https://getcomposer.org/download/</span><span class="sxs-lookup"><span data-stu-id="b722a-159">[Composer]: https://getcomposer.org/download/</span></span>
