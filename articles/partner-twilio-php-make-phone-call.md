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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a>Como tooMake uma chamada telefônica usando o Twilio em um aplicativo PHP no Azure
Olá exemplo a seguir mostra como você pode usar Twilio toomake uma chamada de uma página da web PHP hospedado no Azure. aplicativo resultante Hello solicitará usuário Olá valores de chamada telefônica, conforme mostrado na seguinte captura de tela de saudação.

![Formulário de chamada do Azure usando a Twilio e o PHP][twilio_php]

Você precisará toodo Olá seguinte código Olá toouse neste tópico:

1. Adquirir uma conta e um token de autenticação da Twilio do seu [Console do Twilio][twilio_console]. tooget iniciado com Twilio, avaliar preços em [http://www.twilio.com/pricing][twilio_pricing]. Você pode se inscrever para uma conta de avaliação em [https://www.twilio.com/try-twilio][try_twilio].
2. Obter Olá [Twilio biblioteca para PHP](https://github.com/twilio/twilio-php) ou instalá-lo como um pacote de PERA. Para obter mais informações, consulte Olá [arquivo Leiame](https://github.com/twilio/twilio-php/blob/master/README.md).
3. Instale hello Azure SDK para PHP. Para obter uma visão geral de saudação SDK e instruções sobre como instalá-lo, consulte [configurar hello Azure SDK para PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)

## <a name="create-a-web-form-for-making-a-call"></a>Criar um formulário da web para fazer uma chamada
Olá HTML a seguir de código mostra como toobuild uma página da web (**callform.html**) que recupera dados de usuário para fazer uma chamada:

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

## <a name="create-hello-code-toomake-hello-call"></a>Crie uma chamada de Olá Olá código toomake
Olá mostrado no código a seguir como toobuild **makecall.php**, que é chamado quando o usuário Olá envia o formulário de saudação exibido pelo **callform.html**. código Olá mostrado a seguir cria a mensagem de saudação do chamada e gera chamada hello. Além disso, ser toouse-se de que sua conta do Twilio e autenticação de token de saudação [Twilio Console] [ twilio_console] em vez de valores de espaço reservado de saudação atribuídos muito**$sid** e **$token** no código de saudação abaixo.

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

Além disso, toomaking Olá chamada **makecall.php** exibe alguns metadados de chamada, conforme é mostrado na imagem de saudação abaixo. Para obter mais informações sobre chamar metadados, consulte [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].

![Resposta de chamada do Azure usando a Twilio e o PHP][twilio_php_response]

## <a name="run-hello-application"></a>Executar o aplicativo hello
próxima etapa do Hello é toodeploy tooAzure seu aplicativo sites. Hello artigos a seguir contêm informações de saudação para criar um site e implantar seu código com o Git, FTP ou o WebMatrix (embora nem todas as informações de cada artigo são relevantes):

* [Criar um Site em PHP-MySQL no Azure e implantar usando o Git](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [Criar um site em PHP-MySQL no Azure e Implantar Usando o FTP](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a>Próximas etapas
Este código foi fornecido tooshow você funcionalidade básica usando o Twilio em PHP no Azure. Antes de implantar tooAzure em produção, talvez você queira tooadd mais tratamento de erros ou outros recursos. Por exemplo:

* Em vez de usar um formulário da web, você poderia usar blobs de armazenamento do Azure ou números de telefone de toostore do banco de dados SQL e chamar o texto. Para obter informações sobre como usar os blobs do armazenamento do Azure no PHP, consulte [Usando o Armazenamento do Azure com aplicativos PHP][howto_blob_storage_php]. Para obter informações sobre como usar o Banco de Dados SQL no PHP, consulte [Usando o Banco de Dados SQL com aplicativos PHP][howto_sql_azure_php].
* Olá **makecall.php** código usa a URL fornecida pelo Twilio ([http://twimlets.com/message][twimlet_message_url]) tooprovide uma resposta do Twilio Markup Language (TwiML) que informa como o Twilio tooproceed com chamada de saudação. Por exemplo, Olá TwiML retornado pode conter um `<Say>` verbo que resulta em texto que está sendo falado toohello chamada destinatário. Em vez de usar a URL fornecida pelo Twilio de saudação, você pode criar solicitação do tooTwilio toorespond seu próprio serviço; Para obter mais informações, consulte [como tooUse Twilio para recursos de SMS em PHP e voz][howto_twilio_voice_sms_php]. Mais informações sobre a TwiML podem ser encontradas em [http://www.twilio.com/docs/api/twiml][twiml] e mais informações sobre `<Say>` e outros verbos da Twilio podem ser encontradas em [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Leia as diretrizes de segurança Olá Twilio em [https://www.twilio.com/docs/security][twilio_docs_security].

Para obter informações adicionais sobre a Twilio, consulte [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Consulte também
* [Como tooUse Twilio para recursos de SMS em PHP e voz](partner-twilio-php-how-to-use-voice-sms.md)

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
