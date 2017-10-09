---
title: aaaHow tooUse Twilio para voz e SMS (PHP) | Microsoft Docs
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Exemplos de código escritos em PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a>Como tooUse Twilio para recursos de SMS em PHP e voz
Este guia demonstra como tooperform as tarefas de programação comuns com hello Twilio API de serviço no Azure. cenários de saudação abordados incluem fazer uma chamada telefônica e enviar uma mensagem do serviço SMS (Short Message). Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte Olá [próximas etapas](#NextSteps) seção.

## <a id="WhatIs"></a>O que é Twilio?
Twilio é capacitam Olá futuro das comunicações de negócios, habilitar os desenvolvedores tooembed voice, VoIP e mensagens em aplicativos. Eles virtualizam todos infraestrutura necessária em um ambiente baseado em nuvem, global, expô-lo por meio da plataforma Olá Twilio API de comunicação. Os aplicativos são toobuild simple e escalonável. Aproveite a flexibilidade com pagamento medida que vá preços e se beneficiar da confiabilidade da nuvem.

**Voz Twilio** permite que seus aplicativos toomake e receber chamadas telefônicas. **Twilio SMS** permite que seu aplicativo toosend e receber mensagens de texto. **Clientes do Twilio** permite chamadas de VoIP toomake de qualquer telefone, tablet ou navegador e dá suporte a WebRTC.

## <a id="Pricing"></a>Preços e ofertas especiais da Twilio
Os clientes do Azure recebem uma [oferta especial](http://www.twilio.com/azure): US$ 10 de cortesia de crédito da Twilio quando atualizam a sua conta da Twilio. Esse crédito Twilio podem ser aplicadas tooany Twilio uso (US $10 crédito equivalente toosending até 1.000 mensagens SMS ou recebimento de too1000 minutos de voz, dependendo do local de saudação do seu destino de número e a mensagem ou chamada telefônica de entrada). Resgate esse crédito da Twilio e faça uma introdução em: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio é um serviço flexível. Não há nenhuma taxa de configuração e você pode fechar sua conta a qualquer momento. Você pode encontrar mais detalhes em [Preços do Twilio][twilio_pricing].

## <a id="Concepts"></a>Conceitos
Olá Twilio API é uma API RESTful que fornece funcionalidade SMS e voz para aplicativos. As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].

Principais aspectos da saudação Twilio API são verbos do Twilio e Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Verbos da Twilio
Olá API faz uso do Twilio verbos; Por exemplo, Olá  **&lt;diga&gt;**  verbo instrui Twilio tooaudibly entregar uma mensagem em uma chamada.

a seguir Olá é uma lista de verbos do Twilio. Saiba sobre Olá outros verbos e recursos por meio de [documentação de linguagem de marcação do Twilio](http://www.twilio.com/docs/api/twiml).

* **&lt;Discagem&gt;**: conecta-se o telefone de tooanother Olá chamador.
* **&lt;Coletar&gt;**: coleta dígitos numéricos inseridos no teclado numérico do telefone hello.
* **&lt;Hangup&gt;**: termina uma chamada.
* **&lt;Play&gt;**: reproduz um arquivo de áudio.
* **&lt;Pause&gt;**: espera silenciosamente por um número especificado de segundos.
* **&lt;Registro&gt;**: registra a voz do chamador hello e retorna uma URL de um arquivo que contém a gravação da saudação.
* **&lt;Redirecionar&gt;**: transfere o controle de uma chamada ou SMS toohello TwiML em uma URL diferente.
* **&lt;Rejeitar&gt;**: rejeita uma entrada chamar tooyour Twilio número sem cobrança você
* **&lt;Digamos que&gt;**: converte texto toospeech que é feita em uma chamada.
* **&lt;Sms&gt;**: envia uma mensagem SMS.

### <a id="TwiML"></a>TwiML
TwiML é um conjunto de instruções baseadas em XML com base em verbos do Twilio Olá que informam o Twilio como tooprocess uma chamada ou SMS.

Por exemplo, Olá TwiML a seguir seria converter o texto de saudação **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Quando a aplicativo chama hello Twilio API, um dos parâmetros de API de saudação é URL Olá retorna Olá TwiML resposta. Para fins de desenvolvimento, você pode usar URLs fornecido Twilio tooprovide Olá TwiML as respostas usadas pelos aplicativos. Você também pode hospedar seus próprio respostas de TwiML URLs tooproduce hello e outra opção é Olá toouse **TwiMLResponse** objeto.

Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml]. Para obter informações adicionais sobre Olá Twilio API, consulte [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Criar uma conta na Twilio
Quando você estiver pronto tooget uma conta do Twilio, inscreva-se em [tente Twilio][try_twilio]. Você pode começar com uma conta gratuita e atualizá-la depois.

Quando você se inscrever para uma conta de Twilio, você receberá uma ID de conta e um token de autenticação. Ambos serão chamadas à API do Twilio toomake necessários. tooprevent não autorizado acessar conta tooyour, mantenha o token de autenticação segura. Sua ID da conta e a autenticação token são visíveis no hello [página de conta do Twilio][twilio_account], no hello campos rotulados **SID da conta** e **TOKEN de autenticação**, respectivamente.

## <a id="create_app"></a>Criar um aplicativo PHP
Um aplicativo PHP que usa o serviço do Twilio hello e está em execução no Azure não é diferente de qualquer outro aplicativo PHP que usa o serviço do Twilio hello. Enquanto o Twilio serviços são baseados em REST e podem ser chamados de PHP de várias maneiras, este artigo se concentrará em como os serviços de toouse Twilio com [Twilio biblioteca para PHP do GitHub][twilio_php]. Para obter mais informações sobre como usar a biblioteca do Twilio Olá para PHP, consulte [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].

Instruções detalhadas para criar e implantar um tooAzure de aplicativo do Twilio/PHP estão disponíveis em [como tooMake uma chamada telefônica usando o Twilio em um aplicativo PHP no Azure][howto_phonecall_php].

## <a id="configure_app"></a>Configurar seu aplicativo tooUse Twilio bibliotecas
Você pode configurar sua biblioteca do aplicativo toouse Olá Twilio para PHP de duas maneiras:

1. Baixar a biblioteca do Twilio Olá para PHP do GitHub ([https://github.com/twilio/twilio-php][twilio_php]) e adicione Olá **serviços** aplicativo tooyour de diretório.
   
    -OU-
2. Instale a biblioteca do Twilio Olá para PHP como um pacote de PERA. Ele pode ser instalado com hello comandos a seguir:
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

Depois que você instalou a biblioteca do Twilio Olá para PHP, você pode adicionar uma **require_once** instrução na parte superior de saudação do seu PHP arquivos de biblioteca de saudação tooreference:

        require_once 'Services/Twilio.php';

Para obter mais informações, consulte [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Como fazer uma chamada externa
Olá a seguir mostra como uma saída de toomake chamar usando Olá **Services_Twilio** classe. Esse código também usa uma saudação do site fornecidos Twilio tooreturn resposta Twilio Markup Language (TwiML). Substitua os valores para Olá **de** e **para** números de telefone e certifique-se de que você verifique Olá **de** número de telefone para o seu código de saudação do Twilio conta toorunning anterior.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Conforme mencionado, esse código usa uma saudação do site fornecidos Twilio tooreturn TwiML resposta. Em vez disso, você pode usar seu próprio hello tooprovide do site TwiML resposta; Para obter mais informações, consulte [como tooProvide TwiML respostas do seu próprio Site](#howto_provide_twiml_responses).

* **Observação**: erros de validação de certificado SSL tootroubleshoot, consulte [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation] 

## <a id="howto_send_sms"></a>Como enviar uma mensagem de SMS
Olá a seguir mostra como toosend uma mensagem SMS usando Olá **Services_Twilio** classe. Olá **de** número é fornecido por Twilio para contas de avaliação toosend mensagens SMS. Olá **para** número deve ser verificado para seu código de saudação do Twilio conta toorunning anterior.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <a id="howto_provide_twiml_responses"></a>Como fornecer respostas TwiML de seu próprio site
Quando o aplicativo inicia toohello uma chamada de API do Twilio, Twilio enviará a URL de tooa de solicitação que é esperado tooreturn uma resposta TwiML. exemplo Hello acima usa a URL fornecida Twilio de saudação [http://twimlets.com/message][twimlet_message_url]. (Embora TwiML foi projetado para uso por Twilio, você pode exibir hello-lo em seu navegador. Por exemplo, clique em [http://twimlets.com/message] [ twimlet_message_url] toosee vazio `<Response>` elemento; como outro exemplo, clique em [http://twimlets.com/message? Mensagem % 5B0 %5D = Olá % 20World] [ twimlet_message_url_hello_world] toosee um `<Response>` elemento que contém um `<Say>` elemento.)

Em vez de depender de URL fornecido Twilio de saudação, você pode criar seu próprio site que retorna respostas de HTTP. Você pode criar site hello em qualquer linguagem que retorna respostas XML; Este tópico pressupõe que você vai usar saudação do PHP toocreate TwiML.

Olá PHP página resultados em uma resposta de TwiML que diz que a seguir **Hello World** na chamada de saudação.

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

Como você pode ver do exemplo hello acima, Olá TwiML resposta é simplesmente um documento XML. biblioteca do Twilio Olá para PHP contém classes que irá gerar TwiML para você. exemplo Hello abaixo produz resposta equivalente hello como mostrado acima, mas usa Olá **serviços\_Twilio\_Twiml** classe na biblioteca do Twilio Olá para PHP:

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

Para obter mais informações sobre TwiML, consulte [https://www.twilio.com/docs/api/twiml][twiml_reference]. 

Uma vez que a página PHP configurar respostas de TwiML tooprovide, usar Olá URL da página PHP hello como Olá URL passada em Olá `Services_Twilio->account->calls->create` método. Por exemplo, se você tiver um aplicativo Web chamado **MyTwiML** tooan implantado Azure o serviço hospedado e Olá nome da página PHP Olá é **mytwiml.php**, Olá URL pode ser passada muito **Services_ Twilio -> contas -> chamadas -> criar** conforme mostrado no exemplo a seguir de saudação:

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Para obter informações adicionais sobre como usar o Twilio no Azure com o PHP, consulte [como tooMake uma chamada telefônica usando o Twilio em um aplicativo PHP no Azure][howto_phonecall_php].

## <a id="AdditionalServices"></a>Como Usar os Serviços Adicionais do Twilio
Além disso toohello exemplos mostrados aqui, que twilio oferece APIs baseado na web que você pode usar uma funcionalidade adicional Twilio tooleverage do aplicativo do Azure. Para obter detalhes completos, consulte Olá [documentação da API do Twilio][twilio_api_documentation].

## <a id="NextSteps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas sobre Olá Olá Twilio serviço, siga essas toolearn links mais:

* [Diretrizes de segurança do Twilio][twilio_security_guidelines]
* [Código de Exemplo e Procedimentos do Twilio][twilio_howtos]
* [Tutoriais do Guia de início rápido do Twilio][twilio_quickstarts] 
* [Twilio no GitHub][twilio_on_github]
* [Fale tooTwilio suporte][twilio_support]

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
