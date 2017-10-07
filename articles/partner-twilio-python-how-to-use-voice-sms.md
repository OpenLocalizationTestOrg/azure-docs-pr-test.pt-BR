---
title: aaaHow tooUse Twilio para voz e SMS (Python) | Microsoft Docs
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Exemplos de códigos escritos em Python."
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a>Como tooUse Twilio para recursos de SMS em Python e voz
Este guia demonstra como tooperform as tarefas de programação comuns com hello Twilio API de serviço no Azure. cenários de saudação abordados incluem fazer uma chamada telefônica e enviar uma mensagem do serviço SMS (Short Message). Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte Olá [próximas etapas](#NextSteps) seção.

## <a id="WhatIs"></a>O que é Twilio?
Twilio é capacitam Olá futuro das comunicações de negócios, habilitar os desenvolvedores tooembed voice, VoIP e mensagens em aplicativos. Eles virtualizam todos infraestrutura necessária em um ambiente baseado em nuvem, global, expô-lo por meio da plataforma Olá Twilio API de comunicação. Os aplicativos são toobuild simple e escalonável. Aproveite a flexibilidade com pagamento medida que vá preços e se beneficiar da confiabilidade da nuvem.

**Voz Twilio** permite que seus aplicativos toomake e receber chamadas telefônicas.
**Twilio SMS** permite que seu aplicativo toosend e receber mensagens de texto.
**Clientes do Twilio** permite chamadas de VoIP toomake de qualquer telefone, tablet ou navegador e dá suporte a WebRTC.

## <a id="Pricing"></a>Preços e ofertas especiais da Twilio
Os clientes do Azure recebem uma [oferta especial][special_offer] de US$ 10 de crédito do Twilio quando você atualiza sua conta do Twilio. Esse crédito Twilio podem ser aplicadas tooany Twilio uso (US $10 crédito equivalente toosending até 1.000 mensagens SMS ou recebimento de too1000 minutos de voz, dependendo do local de saudação do seu destino de número e a mensagem ou chamada telefônica de entrada). Resgate esse [crédito do Twilio][special_offer] e comece a usar.

Twilio é um serviço flexível. Não há nenhuma taxa de configuração e você pode fechar sua conta a qualquer momento. Você pode encontrar mais detalhes em [Preços do Twilio][twilio_pricing].

## <a id="Concepts"></a>Conceitos
Olá Twilio API é uma API RESTful que fornece funcionalidade SMS e voz para aplicativos. As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].

Principais aspectos da saudação Twilio API são verbos do Twilio e Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Verbos da Twilio
Olá API faz uso do Twilio verbos; Por exemplo, Olá  **&lt;diga&gt;**  verbo instrui Twilio tooaudibly entregar uma mensagem em uma chamada.

a seguir Olá é uma lista de verbos do Twilio. Saiba sobre Olá outros verbos e recursos por meio de [documentação de linguagem de marcação do Twilio][twiml].

* **&lt;Discagem&gt;**: conecta-se o telefone de tooanother Olá chamador.
* **&lt;Coletar&gt;**: coleta dígitos numéricos inseridos no teclado numérico do telefone hello.
* **&lt;Hangup&gt;**: termina uma chamada.
* **&lt;Pause&gt;**: espera silenciosamente por um número especificado de segundos.
* **&lt;Play&gt;**: reproduz um arquivo de áudio.
* **&lt;Fila&gt;**: Adicionar Olá tooa fila de chamadores.
* **&lt;Registro&gt;**: registros de voz de saudação do chamador hello e retorna uma URL de um arquivo que contém a gravação da saudação.
* **&lt;Redirecionar&gt;**: transfere o controle de uma chamada ou SMS toohello TwiML em uma URL diferente.
* **&lt;Rejeitar&gt;**: rejeita uma entrada chamar tooyour Twilio número sem cobrança você.
* **&lt;Digamos que&gt;**: converte texto toospeech que é feita em uma chamada.
* **&lt;Sms&gt;**: envia uma mensagem SMS.

### <a id="TwiML"></a>TwiML
TwiML é um conjunto de instruções baseadas em XML com base em verbos do Twilio Olá que informam o Twilio como tooprocess uma chamada ou SMS.

Por exemplo, Olá TwiML a seguir seria converter o texto de saudação **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

Quando a aplicativo chama hello Twilio API, um dos parâmetros de API de saudação é URL Olá retorna Olá TwiML resposta. Para fins de desenvolvimento, você pode usar URLs fornecido Twilio tooprovide Olá TwiML as respostas usadas pelos aplicativos. Você também pode hospedar seus próprio respostas de TwiML URLs tooproduce hello e outra opção é toouse Olá `TwiMLResponse` objeto.

Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml]. Para obter informações adicionais sobre Olá Twilio API, consulte [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Criar uma conta na Twilio
Quando você estiver pronto tooget uma conta do Twilio, inscreva-se em [tente Twilio][try_twilio]. Você pode começar com uma conta gratuita e atualizá-la depois.

Ao se inscrever em uma conta do Twilio, você receberá uma SID de conta e um token de autenticação. Ambos serão chamadas à API do Twilio toomake necessários. tooprevent não autorizado acessar conta tooyour, mantenha o token de autenticação segura. O SID da conta e o token de autenticação são visíveis no hello [Twilio Console][twilio_console], no hello campos rotulados **SID de conta** e **TOKEN de autenticação**, respectivamente.

## <a id="create_app"></a>Criar um Aplicativo Python
Um aplicativo do Python que usa o serviço do Twilio hello e está em execução no Azure não é diferente de qualquer outro aplicativo do Python que usa o serviço do Twilio hello. Enquanto o Twilio serviços são baseados em REST e podem ser chamados do Python de várias maneiras, este artigo se concentrará em como os serviços de toouse Twilio com [Twilio biblioteca para Python do GitHub][twilio_python]. Para obter mais informações sobre como usar a biblioteca do Twilio Olá para Python, consulte [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].

Primeiro, [configuração de uma nova VM Linux do Azure] [azure_vm_setup] tooact como um host para o novo aplicativo web Python. Depois de hello Máquina Virtual está em execução, será necessário tooexpose seu aplicativo em uma porta pública conforme descrito abaixo.

### <a name="add-an-incoming-rule"></a>Adicionar Uma Regra de Entrada
  1. Vá toohello [grupo de segurança de rede] [azure_nsg] página.
  2. Olá selecione grupo de segurança de rede que corresponda com sua máquina Virtual.
  3. Adicione uma **regra de saída** para a **porta 80**. Ser tooallow-se de entrada de qualquer endereço.

### <a name="set-hello-dns-name-label"></a>Saudação de conjunto de rótulo do nome DNS
  1. Vá toohello [Olá endereços de IP público] [azure_ips] página.
  2. Selecione Olá IP público que correspends com sua máquina Virtual.
  3. Saudação de conjunto **rótulo do nome DNS** em Olá **configuração** seção. No caso de Olá deste exemplo terá aparência semelhante a esta *o rótulo de domínio*. centralus.cloudapp.azure.com

Depois que você é capaz de tooconnect por meio do SSH toohello Máquina Virtual que você pode instalar Olá Framework do Web de sua escolha (Olá dois mais conhecidas do Python que está sendo [bulbo](http://flask.pocoo.org/) e [Django](https://www.djangoproject.com)). Você pode instalar qualquer um deles apenas executando Olá `pip install` comando.

Tenha em mente que configuramos o tráfego de tooallow de máquina Virtual Olá apenas na porta 80. Portanto, certifique-se de que tooconfigure Olá aplicativo toouse essa porta.

## <a id="configure_app"></a>Configurar seu aplicativo tooUse Twilio bibliotecas
Você pode configurar sua biblioteca do aplicativo toouse Olá Twilio para Python de duas maneiras:

* Instale biblioteca do Twilio Olá para Python como um pacote de Pip. Ele pode ser instalado com hello comandos a seguir:
   
        $ pip install twilio

    -OU-

* Baixar a biblioteca do Twilio Olá para Python do GitHub ([https://github.com/twilio/twilio-python][twilio_python]) e instalá-lo assim:

        $ python setup.py install

Depois que você instalou a biblioteca do Twilio Olá para Python, você pode, em seguida, `import` -lo em seus arquivos de Python:

        import twilio

Para obter mais informações, consulte [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Como fazer uma chamada externa
Olá a seguir mostra como chamar toomake uma saída. Esse código também usa uma saudação do site fornecidos Twilio tooreturn resposta Twilio Markup Language (TwiML). Substitua os valores para Olá **from_number** e **to_number** números de telefone e certifique-se de que você verificou Olá **from_number** número de telefone para sua conta do Twilio antes da execução de código hello.

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

Conforme mencionado, esse código usa uma saudação do site fornecidos Twilio tooreturn TwiML resposta. Em vez disso, você pode usar seu próprio hello tooprovide do site TwiML resposta; Para obter mais informações, consulte [como tooProvide TwiML respostas do seu próprio Site](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Como enviar uma mensagem de SMS
Olá a seguir mostra como toosend uma mensagem SMS usando Olá `TwilioRestClient` classe. Olá **from_number** número é fornecido por Twilio para contas de avaliação toosend mensagens SMS. Olá **to_number** número deve ser verificado para sua conta do Twilio antes de executar código hello.

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <a id="howto_provide_twiml_responses"></a>Como fornecer respostas TwiML de seu próprio site
Quando o aplicativo inicia toohello uma chamada de API do Twilio, Twilio enviará a URL de tooa de solicitação que é esperado tooreturn uma resposta TwiML. exemplo Hello acima usa a URL fornecida Twilio de saudação [http://twimlets.com/message][twimlet_message_url]. (Embora o TwiML tenha sido criado para uso do Twilio, você pode exibi-lo em seu navegador. Por exemplo, clique em [http://twimlets.com/message] [ twimlet_message_url] toosee vazio `<Response>` elemento; como outro exemplo, clique em [http://twimlets.com/message? Mensagem % 5B0 %5D = Olá % 20World] [ twimlet_message_url_hello_world] toosee um `<Response>` elemento que contém um `<Say>` elemento.)

Em vez de depender de URL fornecido Twilio de saudação, você pode criar seu próprio site que retorna respostas de HTTP. Você pode criar site hello em qualquer linguagem que retorna respostas XML; Este tópico pressupõe que você usará saudação do Python toocreate TwiML.

Olá exemplos a seguir produzirá uma resposta de TwiML diz **Hello World** na chamada de saudação.

Com o Flash:

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

Com o Django:

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

Como você pode ver do exemplo hello acima, Olá TwiML resposta é simplesmente um documento XML. biblioteca do Twilio Olá para Python contém classes que irá gerar TwiML para você. Olá exemplo a seguir produz resposta equivalente hello como mostrado acima, mas usa Olá `twiml` módulo na biblioteca do Twilio de saudação do Python:

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

Para obter mais informações sobre TwiML, consulte [https://www.twilio.com/docs/api/twiml][twiml_reference].

Uma vez que seu aplicativo Python configurar tooprovide TwiML respostas, use Olá URL do aplicativo hello como Olá URL passada em hello `client.calls.create` método. Por exemplo, se você tiver um aplicativo Web chamado **MyTwiML** tooan implantado Azure o serviço hospedado, você pode usar a url como webhook, conforme mostrado no exemplo a seguir de saudação:

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <a id="AdditionalServices"></a>Como Usar os Serviços Adicionais do Twilio
Além disso toohello exemplos mostrados aqui, que twilio oferece APIs baseado na web que você pode usar uma funcionalidade adicional Twilio tooleverage do aplicativo do Azure. Para obter detalhes completos, consulte Olá [documentação da API do Twilio][twilio_api].

## <a id="NextSteps"></a>Próximas etapas
Agora que você aprendeu os fundamentos de saudação do hello Twilio serviço, siga essas toolearn links mais:

* [Diretrizes de segurança do Twilio][twilio_security_guidelines]
* [Código de Exemplo e Guias de Procedimentos do Twilio][twilio_howtos]
* [Tutoriais do Guia de início rápido do Twilio][twilio_quickstarts]
* [Twilio no GitHub][twilio_on_github]
* [Fale tooTwilio suporte][twilio_support]

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
