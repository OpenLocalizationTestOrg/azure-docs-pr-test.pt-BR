---
title: "Como fazer uma chamada telefônica do Twilio (PHP) | Microsoft Docs"
description: "Saiba como fazer uma chamada telefônica e enviar uma mensagem SMS com o serviço de API do Twilio no Azure. Exemplos são para o aplicativo PHP."
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
ms.openlocfilehash: f35450ace02727ddf392dbbe857b934a45ee022a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="aeaf4-104">Como fazer uma chamada telefônica usando o Twilio em um aplicativo PHP no Azure</span><span class="sxs-lookup"><span data-stu-id="aeaf4-104">How to Make a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="aeaf4-105">O exemplo a seguir mostra como você pode usar a Twilio para fazer uma chamada de uma página da web PHP hospedada no Azure.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-105">The following example shows you how you can use Twilio to make a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="aeaf4-106">O aplicativo resultante solicitará valores de chamada telefônica ao usuário, conforme mostrado na seguinte captura de tela.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-106">The resulting application will prompt the user for phone call values, as shown in the following screen shot.</span></span>

![Formulário de chamada do Azure usando a Twilio e o PHP][twilio_php]

<span data-ttu-id="aeaf4-108">Você precisará fazer o seguinte para usar o código deste tópico:</span><span class="sxs-lookup"><span data-stu-id="aeaf4-108">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="aeaf4-109">Adquirir uma conta e um token de autenticação da Twilio do seu [Console do Twilio][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="aeaf4-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="aeaf4-110">Para uma introdução ao Twilio, avalie os preços em [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="aeaf4-110">To get started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="aeaf4-111">Você pode se inscrever para uma conta de avaliação em [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="aeaf4-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="aeaf4-112">Obtenha a [biblioteca do Twilio para PHP](https://github.com/twilio/twilio-php) ou a instale como um pacote PEAR.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-112">Obtain the [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="aeaf4-113">Para obter mais informações, veja o [arquivo Leiame](https://github.com/twilio/twilio-php/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="aeaf4-113">For more information, see the [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="aeaf4-114">Instale o SDK do Azure para PHP.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-114">Install the Azure SDK for PHP.</span></span> <span data-ttu-id="aeaf4-115">Para obter uma visão geral do SDK e obter instruções sobre como instalá-lo, consulte [Configurar o SDK do Azure para PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span><span class="sxs-lookup"><span data-stu-id="aeaf4-115">For an overview of the SDK and instructions on installing it, see [Set up the Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="aeaf4-116">Criar um formulário da web para fazer uma chamada</span><span class="sxs-lookup"><span data-stu-id="aeaf4-116">Create a web form for making a call</span></span>
<span data-ttu-id="aeaf4-117">O código HTML a seguir mostra como criar uma página da web (**callform.html**) que recupera dados do usuário para fazer uma chamada:</span><span class="sxs-lookup"><span data-stu-id="aeaf4-117">The following HTML code shows how to build a web page (**callform.html**) that retrieves user data for making a call:</span></span>

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
        <td><input name="callText" size="100" type="text" value="Hello. This is the call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-the-code-to-make-the-call"></a><span data-ttu-id="aeaf4-118">Como criar o código para fazer a chamada</span><span class="sxs-lookup"><span data-stu-id="aeaf4-118">Create the code to make the call</span></span>
<span data-ttu-id="aeaf4-119">O seguinte código mostra como criar **makecall.php**, que é chamada quando o usuário envia o formulário exibido pelo **callform.html**.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-119">The following code shows how to build **makecall.php**, which is called when the user submits the form displayed by **callform.html**.</span></span> <span data-ttu-id="aeaf4-120">O código abaixo cria a mensagem da chamada e gera a chamada.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-120">The code shown below creates the call message and generates the call.</span></span> <span data-ttu-id="aeaf4-121">Além disso, certifique-se de usar sua conta do Twilio e o token de autenticação do [Console do Twilio][twilio_console] em vez dos valores de espaço reservado atribuídos a **$sid** e **$token** no código a seguir.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-121">Also, be sure to use your Twilio account and authentication token from the [Twilio Console][twilio_console] instead of the placeholder values assigned to **$sid** and **$token** in the code below.</span></span>

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

<span data-ttu-id="aeaf4-122">Além de fazer a chamada, o **makecall.php** exibe alguns metadados da chamada, conforme mostrado na imagem abaixo.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-122">In addition to making the call, **makecall.php** displays some call metadata, as is shown in the image below.</span></span> <span data-ttu-id="aeaf4-123">Para obter mais informações sobre chamar metadados, consulte [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span><span class="sxs-lookup"><span data-stu-id="aeaf4-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Resposta de chamada do Azure usando a Twilio e o PHP][twilio_php_response]

## <a name="run-the-application"></a><span data-ttu-id="aeaf4-125">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="aeaf4-125">Run the application</span></span>
<span data-ttu-id="aeaf4-126">A próxima etapa é implantar seu aplicativo a Sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-126">The next step is to deploy your application to Azure Websites.</span></span> <span data-ttu-id="aeaf4-127">Os artigos a seguir contêm as informações para criar um site e implantar seu código com Git, FTP ou WebMatrix (embora nem todas as informações em cada artigo sejam relevantes):</span><span class="sxs-lookup"><span data-stu-id="aeaf4-127">The following articles contain the information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="aeaf4-128">Criar um Site em PHP-MySQL no Azure e implantar usando o Git</span><span class="sxs-lookup"><span data-stu-id="aeaf4-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="aeaf4-129">Criar um site em PHP-MySQL no Azure e Implantar Usando o FTP</span><span class="sxs-lookup"><span data-stu-id="aeaf4-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="aeaf4-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aeaf4-130">Next steps</span></span>
<span data-ttu-id="aeaf4-131">Esse código foi fornecido para mostrar a funcionalidade básica usando a Twilio no PHP no Azure.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-131">This code was provided to show you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="aeaf4-132">Antes de implantar o Azure na produção, convém adicionar mais tratamento de erros ou outros recursos.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-132">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="aeaf4-133">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aeaf4-133">For example:</span></span>

* <span data-ttu-id="aeaf4-134">Em vez de usar um formulário da web, você pode usar os blobs de armazenamento ou o Banco de Dados SQL do Azure para armazenar números de telefone e texto de chamada.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-134">Instead of using a web form, you could use Azure storage blobs or SQL Database to store phone numbers and call text.</span></span> <span data-ttu-id="aeaf4-135">Para obter informações sobre como usar os blobs do armazenamento do Azure no PHP, consulte [Usando o Armazenamento do Azure com aplicativos PHP][howto_blob_storage_php].</span><span class="sxs-lookup"><span data-stu-id="aeaf4-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="aeaf4-136">Para obter informações sobre como usar o Banco de Dados SQL no PHP, consulte [Usando o Banco de Dados SQL com aplicativos PHP][howto_sql_azure_php].</span><span class="sxs-lookup"><span data-stu-id="aeaf4-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="aeaf4-137">O código **makecall.php** usa a URL fornecida pela Twilio ([http://twimlets.com/message][twimlet_message_url]) para fornecer uma resposta em TwiML (linguagem de marcação do Twilio) que informa ao Twilio sobre como proceder com a chamada.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-137">The **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) to provide a Twilio Markup Language (TwiML) response that informs Twilio how to proceed with the call.</span></span> <span data-ttu-id="aeaf4-138">Por exemplo, a TwiML que é retornada pode conter um verbo `<Say>` que resulta no texto que está sendo falado para o destinatário da chamada.</span><span class="sxs-lookup"><span data-stu-id="aeaf4-138">For example, the TwiML that is returned can contain a `<Say>` verb that results in text being spoken to the call recipient.</span></span> <span data-ttu-id="aeaf4-139">Em vez de usar a URL fornecida pela Twilio, você pode criar seu próprio serviço para responder à solicitação da Twilio. Para obter mais informações, consulte [Como usar a Twilio para obter recursos de voz e SMS em PHP][howto_twilio_voice_sms_php].</span><span class="sxs-lookup"><span data-stu-id="aeaf4-139">Instead of using the Twilio-provided URL, you could build your own service to respond to Twilio's request; for more information, see [How to Use Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="aeaf4-140">Mais informações sobre a TwiML podem ser encontradas em [http://www.twilio.com/docs/api/twiml][twiml] e mais informações sobre `<Say>` e outros verbos da Twilio podem ser encontradas em [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="aeaf4-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="aeaf4-141">Leia as diretrizes de segurança da Twilio em [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="aeaf4-141">Read the Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="aeaf4-142">Para obter informações adicionais sobre a Twilio, consulte [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="aeaf4-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="aeaf4-143">Consulte também</span><span class="sxs-lookup"><span data-stu-id="aeaf4-143">See Also</span></span>
* [<span data-ttu-id="aeaf4-144">Como usar o Twilio para obter recursos de voz e SMS no PHP</span><span class="sxs-lookup"><span data-stu-id="aeaf4-144">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

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
