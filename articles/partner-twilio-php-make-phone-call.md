---
title: aaaHow toomake um telefonema do Twilio (PHP) | Microsoft Docs
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Exemplos são para o aplicativo PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 44e35adc-be06-4700-beee-8c9e2c20c540
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: e6fecc345bf9ae787d14d533bd8d96b175c2453b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="e0417-104">Como tooMake uma chamada telefônica usando o Twilio em um aplicativo PHP no Azure</span><span class="sxs-lookup"><span data-stu-id="e0417-104">How tooMake a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="e0417-105">Olá exemplo a seguir mostra como você pode usar Twilio toomake uma chamada de uma página da web PHP hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="e0417-105">hello following example shows you how you can use Twilio toomake a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="e0417-106">aplicativo resultante Hello solicitará usuário Olá valores de chamada telefônica, conforme mostrado na seguinte captura de tela de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0417-106">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Formulário de chamada do Azure usando a Twilio e o PHP][twilio_php]

<span data-ttu-id="e0417-108">Você precisará toodo Olá seguinte código Olá toouse neste tópico:</span><span class="sxs-lookup"><span data-stu-id="e0417-108">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="e0417-109">Adquirir uma conta e um token de autenticação da Twilio do seu [Console do Twilio][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="e0417-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="e0417-110">tooget iniciado com Twilio, avaliar preços em [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="e0417-110">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="e0417-111">Você pode se inscrever para uma conta de avaliação em [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="e0417-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="e0417-112">Obter Olá [Twilio biblioteca para PHP](https://github.com/twilio/twilio-php) ou instalá-lo como um pacote de PERA.</span><span class="sxs-lookup"><span data-stu-id="e0417-112">Obtain hello [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="e0417-113">Para obter mais informações, consulte Olá [arquivo Leiame](https://github.com/twilio/twilio-php/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="e0417-113">For more information, see hello [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="e0417-114">Instale hello Azure SDK para PHP.</span><span class="sxs-lookup"><span data-stu-id="e0417-114">Install hello Azure SDK for PHP.</span></span> <span data-ttu-id="e0417-115">Para obter uma visão geral de saudação SDK e instruções sobre como instalá-lo, consulte [configurar hello Azure SDK para PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span><span class="sxs-lookup"><span data-stu-id="e0417-115">For an overview of hello SDK and instructions on installing it, see [Set up hello Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="e0417-116">Criar um formulário da web para fazer uma chamada</span><span class="sxs-lookup"><span data-stu-id="e0417-116">Create a web form for making a call</span></span>
<span data-ttu-id="e0417-117">Olá HTML a seguir de código mostra como toobuild uma página da web (**callform.html**) que recupera dados de usuário para fazer uma chamada:</span><span class="sxs-lookup"><span data-stu-id="e0417-117">hello following HTML code shows how toobuild a web page (**callform.html**) that retrieves user data for making a call:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
  <title>Automated call form</title>
</head>
<body>
  <h1>Automated Call Form</h1>
  <p>Fill in all fields and click <b>Make this call</b>.</p>
  <form action="makecall.php" method="post">
    <table>
      <tr>
        <td>To:</td>
        <td><input name="callTo" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>From:</td>
        <td><input name="callFrom" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>Call message:</td>
        <td><input name="callText" size="100" type="text" value="Hello. This is hello call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="e0417-118">Crie uma chamada de Olá Olá código toomake</span><span class="sxs-lookup"><span data-stu-id="e0417-118">Create hello code toomake hello call</span></span>
<span data-ttu-id="e0417-119">Olá mostrado no código a seguir como toobuild **makecall.php**, que é chamado quando o usuário Olá envia o formulário de saudação exibido pelo **callform.html**.</span><span class="sxs-lookup"><span data-stu-id="e0417-119">hello following code shows how toobuild **makecall.php**, which is called when hello user submits hello form displayed by **callform.html**.</span></span> <span data-ttu-id="e0417-120">código Olá mostrado a seguir cria a mensagem de saudação do chamada e gera chamada hello.</span><span class="sxs-lookup"><span data-stu-id="e0417-120">hello code shown below creates hello call message and generates hello call.</span></span> <span data-ttu-id="e0417-121">Além disso, ser toouse-se de que sua conta do Twilio e autenticação de token de saudação [Twilio Console] [ twilio_console] em vez de valores de espaço reservado de saudação atribuídos muito**$sid** e **$token** no código de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="e0417-121">Also, be sure toouse your Twilio account and authentication token from hello [Twilio Console][twilio_console] instead of hello placeholder values assigned too**$sid** and **$token** in hello code below.</span></span>

```html
<html>
<head><title>Making call...</title></head>
<body>
<p>Your call is being made.</p>

<?php
require_once 'path/to/vendor/autoload.php';

$sid   = "your_account_sid";
$token = "your_authentication_token";

$from_number = $_POST['callFrom']; // Calls must be made from a registered Twilio number.
$to_number   = $_POST['callTo'];
$message     = $_POST['callText'];

$client = new Twilio\Rest\Client($sid, $token);

$call = $client->calls->create(
            $to_number,
            $from_number,
            array('url' => http://twimlets.com/message?Message=' . urlencode($message))
        );

echo "Call status: " . $call->status . "<br />";
echo "URI resource: " . $call->uri . "<br />";
?>
</body>
</html>
```

<span data-ttu-id="e0417-122">Além disso, toomaking Olá chamada **makecall.php** exibe alguns metadados de chamada, conforme é mostrado na imagem de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="e0417-122">In addition toomaking hello call, **makecall.php** displays some call metadata, as is shown in hello image below.</span></span> <span data-ttu-id="e0417-123">Para obter mais informações sobre chamar metadados, consulte [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span><span class="sxs-lookup"><span data-stu-id="e0417-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Resposta de chamada do Azure usando a Twilio e o PHP][twilio_php_response]

## <a name="run-hello-application"></a><span data-ttu-id="e0417-125">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="e0417-125">Run hello application</span></span>
<span data-ttu-id="e0417-126">próxima etapa do Hello é toodeploy tooAzure seu aplicativo sites.</span><span class="sxs-lookup"><span data-stu-id="e0417-126">hello next step is toodeploy your application tooAzure Websites.</span></span> <span data-ttu-id="e0417-127">Hello artigos a seguir contêm informações de saudação para criar um site e implantar seu código com o Git, FTP ou o WebMatrix (embora nem todas as informações de cada artigo são relevantes):</span><span class="sxs-lookup"><span data-stu-id="e0417-127">hello following articles contain hello information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="e0417-128">Criar um Site em PHP-MySQL no Azure e implantar usando o Git</span><span class="sxs-lookup"><span data-stu-id="e0417-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="e0417-129">Criar um site em PHP-MySQL no Azure e Implantar Usando o FTP</span><span class="sxs-lookup"><span data-stu-id="e0417-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="e0417-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0417-130">Next steps</span></span>
<span data-ttu-id="e0417-131">Este código foi fornecido tooshow você funcionalidade básica usando o Twilio em PHP no Azure.</span><span class="sxs-lookup"><span data-stu-id="e0417-131">This code was provided tooshow you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="e0417-132">Antes de implantar tooAzure em produção, talvez você queira tooadd mais tratamento de erros ou outros recursos.</span><span class="sxs-lookup"><span data-stu-id="e0417-132">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="e0417-133">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0417-133">For example:</span></span>

* <span data-ttu-id="e0417-134">Em vez de usar um formulário da web, você poderia usar blobs de armazenamento do Azure ou números de telefone de toostore do banco de dados SQL e chamar o texto.</span><span class="sxs-lookup"><span data-stu-id="e0417-134">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="e0417-135">Para obter informações sobre como usar os blobs do armazenamento do Azure no PHP, consulte [Usando o Armazenamento do Azure com aplicativos PHP][howto_blob_storage_php].</span><span class="sxs-lookup"><span data-stu-id="e0417-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="e0417-136">Para obter informações sobre como usar o Banco de Dados SQL no PHP, consulte [Usando o Banco de Dados SQL com aplicativos PHP][howto_sql_azure_php].</span><span class="sxs-lookup"><span data-stu-id="e0417-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="e0417-137">Olá **makecall.php** código usa a URL fornecida pelo Twilio ([http://twimlets.com/message][twimlet_message_url]) tooprovide uma resposta do Twilio Markup Language (TwiML) que informa como o Twilio tooproceed com chamada de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0417-137">hello **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) tooprovide a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="e0417-138">Por exemplo, Olá TwiML retornado pode conter um `<Say>` verbo que resulta em texto que está sendo falado toohello chamada destinatário.</span><span class="sxs-lookup"><span data-stu-id="e0417-138">For example, hello TwiML that is returned can contain a `<Say>` verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="e0417-139">Em vez de usar a URL fornecida pelo Twilio de saudação, você pode criar solicitação do tooTwilio toorespond seu próprio serviço; Para obter mais informações, consulte [como tooUse Twilio para recursos de SMS em PHP e voz][howto_twilio_voice_sms_php].</span><span class="sxs-lookup"><span data-stu-id="e0417-139">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="e0417-140">Mais informações sobre a TwiML podem ser encontradas em [http://www.twilio.com/docs/api/twiml][twiml] e mais informações sobre `<Say>` e outros verbos da Twilio podem ser encontradas em [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="e0417-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="e0417-141">Leia as diretrizes de segurança Olá Twilio em [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="e0417-141">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="e0417-142">Para obter informações adicionais sobre a Twilio, consulte [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="e0417-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="e0417-143">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e0417-143">See Also</span></span>
* [<span data-ttu-id="e0417-144">Como tooUse Twilio para recursos de SMS em PHP e voz</span><span class="sxs-lookup"><span data-stu-id="e0417-144">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/docs/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[build_php_azure_app]: http://azurephp.interoperabilitybridges.com/articles/build-and-deploy-a-windows-azure-php-application
[howto_twilio_voice_sms_php]: partner-twilio-php-how-to-use-voice-sms.md
[howto_blob_storage_php]: http://azure.microsoft.com/documentation/articles/storage-php-how-to-use-blobs/
[howto_sql_azure_php]: http://azure.microsoft.com/documentation/articles/sql-database-php-how-to-use/
[twilio_call_properties]: https://www.twilio.com/docs/api/rest/call#instance-properties
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_php]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPCallForm.jpg
[twilio_php_response]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPMakeCall.jpg
[website-git]: ./web-sites/web-sites-php-mysql-deploy-use-git.md
[website-ftp]: ./web-sites/web-sites-php-mysql-deploy-use-ftp.md
[twilio_php_github]: https://github.com/twilio/twilio-php
