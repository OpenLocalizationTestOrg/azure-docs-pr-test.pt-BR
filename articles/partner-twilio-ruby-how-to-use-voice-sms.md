---
title: aaaHow tooUse Twilio para voz e SMS (Ruby) | Microsoft Docs
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Exemplos de códigos escritos em Ruby."
services: 
documentationcenter: ruby
author: devinrader
manager: twilio
editor: 
ms.assetid: 60e512f6-fa47-47c0-aedc-f19bb72a1158
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 11/25/2014
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: aca5ccb4663ff03c9c1f39c848469415f06dfb45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a>Como tooUse Twilio para recursos de SMS em Ruby e voz
Este guia demonstra como tooperform as tarefas de programação comuns com hello Twilio API de serviço no Azure. cenários de saudação abordados incluem fazer uma chamada telefônica e enviar uma mensagem do serviço SMS (Short Message). Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte Olá [próximas etapas](#NextSteps) seção.

## <a id="WhatIs"></a>O que é Twilio?
Twilio é uma API de serviço web de telefonia que permite que você use seus idiomas de web existente e voz de toobuild habilidades e aplicativos de SMS. O Twilio é um serviço de terceiro (não é um recurso do Azure e não é um produto da Microsoft).

**Voz Twilio** permite que seus aplicativos toomake e receber chamadas telefônicas. **Twilio SMS** permite que seus aplicativos toomake e receber mensagens SMS. **Clientes do Twilio** permite comunicação por voz tooenable usando conexões da Internet existentes, incluindo conexões móveis que seus aplicativos.

## <a id="Pricing"></a>Preços e ofertas especiais da Twilio
A informações sobre os preços do Twilio estão disponíveis em [Preços do Twilio][twilio_pricing]. Os clientes do Azure recebem uma [oferta especial][special_offer]: um crédito de 1.000 mensagens de texto gratuitas ou 1.000 minutos de entrada. toosign para esta oferta ou obter mais informações, visite [http://ahoy.twilio.com/azure][special_offer].  

## <a id="Concepts"></a>Conceitos
Olá Twilio API é uma API RESTful que fornece funcionalidade SMS e voz para aplicativos. As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].

### <a id="TwiML"></a>TwiML
TwiML é um conjunto de instruções baseadas em XML que informam o Twilio como tooprocess uma chamada ou SMS.

Por exemplo, Olá TwiML a seguir seria converter o texto de saudação **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Todos os documentos do TwiML têm `<Response>` como seu elemento raiz. A partir daí, você deve usar comportamento de saudação do Twilio verbos toodefine do seu aplicativo.

### <a id="Verbs"></a>Verbos do TwiML
Twilio verbos são marcas XML que informam o Twilio muito**fazer**. Por exemplo, Olá  **&lt;diga&gt;**  verbo instrui Twilio tooaudibly entregar uma mensagem em uma chamada. 

a seguir Olá é uma lista de verbos do Twilio.

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

Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml]. Para obter informações adicionais sobre Olá Twilio API, consulte [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Criar uma conta na Twilio
Quando você estiver pronto tooget uma conta do Twilio, inscreva-se em [tente Twilio][try_twilio]. Você pode começar com uma conta gratuita e atualizá-la depois.

Ao se inscrever em uma conta do Twilio, você receberá um número de telefone gratuito para o seu aplicativo. Você também receberá uma SID de conta e um token de autenticação. Ambos serão chamadas à API do Twilio toomake necessários. tooprevent não autorizado acessar conta tooyour, mantenha o token de autenticação segura. O SID da conta e o token de autenticação são visíveis no hello [página de conta do Twilio][twilio_account], no hello campos rotulados **SID da conta** e **TOKEN de autenticação** , respectivamente.

### <a id="VerifyPhoneNumbers"></a>Verificar números telefônicos
O número de toohello adição que você receber do Twilio, você também pode verificar números que você controle (ou seja, seu telefone celular ou home número de telefone) para uso em seus aplicativos. 

Para obter informações sobre como tooverify um número de telefone, consulte [gerenciar números][verify_phone].

## <a id="create_app"></a>Criar um Aplicativo em Ruby
Um aplicativo Ruby que usa o serviço do Twilio hello e está em execução no Azure não é diferente de qualquer outro aplicativo Ruby que usa o serviço do Twilio hello. Enquanto Twilio serviços são RESTful e podem ser chamados de Ruby de várias maneiras, este artigo se concentrará em como os serviços de toouse Twilio com [biblioteca auxiliar da Twilio para Ruby][twilio_ruby].

Primeiro, [configuração de uma nova VM do Linux Azure] [ azure_vm_setup] tooact como um host para seu novo aplicativo web Ruby. Ignore as etapas de saudação que envolvem a criação de saudação de um aplicativo de trilhos, apenas Olá configuração VM. Certifique-se de criar um ponto de extremidade com uma porta externa 80 e uma porta interna 5000.

Nos exemplos de saudação abaixo, vamos usar [Sinatra][sinatra], uma estrutura muito simples da web para Ruby. Mas você pode usar biblioteca auxiliar da saudação Twilio para Ruby com qualquer outra estrutura de web, inclusive Ruby nos trilhos.

Use SSH na sua nova VM e crie um diretório para o seu novo aplicativo. Dentro desse diretório, crie um arquivo chamado hello Gemfile e cópia de código a seguir nele:

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

Na linha de comando Olá executar `bundle install`. Isso irá instalar dependências de saudação acima. Em seguida, crie um arquivo chamado `web.rb`. Isso será onde reside o código de saudação para seu aplicativo web. Cole Olá código a seguir nele:

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

Agora você deve ser o comando de Olá Olá capaz de executar `ruby web.rb -p 5000`. Isso vai girar um servidor Web pequeno na porta 5000. Você deve ser capaz de toobrowse toothis aplicativo em seu navegador visitando o URL Olá você configuração para sua VM do Azure. Depois que você pode acessar seu aplicativo web no navegador hello, você está pronto toostart compilar um aplicativo Twilio.

## <a id="configure_app"></a>Configurar seu aplicativo tooUse Twilio
Você pode configurar sua biblioteca de Twilio web app toouse Olá atualizando seu `Gemfile` tooinclude esta linha:

    gem 'twilio-ruby'

Na linha de comando hello, execute `bundle install`. Agora, abra `web.rb` e esta linha na parte superior do hello, incluindo:

    require 'twilio-ruby'

Você está agora todos os conjunto de biblioteca auxiliar da toouse Olá Twilio para Ruby em seu aplicativo web.

## <a id="howto_make_call"></a>Como fazer uma chamada externa
Olá a seguir mostra como chamar toomake uma saída. Conceitos principais incluem o uso de biblioteca auxiliar da saudação Twilio para Ruby toomake chamadas à API REST e TwiML de renderização. Substitua os valores para Olá **de** e **para** números de telefone e certifique-se de que você verifique Olá **de** número de telefone para o seu código de saudação do Twilio conta toorunning anterior.

Adicione esta função muito`web.md`:

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # hello number of hello phone receiving call.
    too= "NNNNNNNNNNN";

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create hello call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make hello call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

Se você abrir o `http://yourdomain.cloudapp.net/make_call` em um navegador, que irá disparar Olá chamada toohello Twilio API toomake Olá telefonema. Olá dois primeiros parâmetros `client.account.calls.create` são bem auto-explicativo: Olá número Olá chamada é `from` e Olá número Olá chamada é `to`. 

Olá terceiro parâmetro (`url`) é URL Olá que Twilio solicitações tooget instruções sobre qual toodo quando chamada hello está conectada. Nesse caso, configuração de uma URL (`http://yourdomain.cloudapp.net`) que retorna um documento TwiML simples e usa Olá `<Say>` toodo verbo Olá alguns texto em fala e fale "Hello macaco" toohello receptor da chamada.

## <a id="howto_recieve_sms"></a>Como receber uma mensagem SMS
No exemplo anterior de saudação é iniciada uma **saída** chamada telefônica. Esse tempo, vamos usar o número de telefone de saudação Twilio nos forneceu durante a inscrição tooprocess um **entrada** mensagem SMS.

Primeiro, logon tooyour [Twilio painel][twilio_account]. Clique em "Números" na navegação superior hello e em seguida, clique em Olá número Twilio que foram fornecidos. Você verá dois URLs que podem ser configurados. Um URL de solicitação da voz e de SMS. Esses são URLs Olá Twilio chamadas sempre que uma chamada é feita ou um SMS é enviado tooyour número. Olá URLs também são conhecidos como "ganchos web".

Gostaríamos tooprocess recebimento de mensagens SMS, vamos atualizar Olá URL muito`http://yourdomain.cloudapp.net/sms_url`. Vá em frente e clique em Salvar alterações final Olá Olá página. Agora, voltando no `web.rb` programa vamos toohandle nosso aplicativo isso:

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

Depois de fazer a alteração de saudação, verifique toore-start-se de que seu aplicativo web. Agora, retire o seu telefone e enviar um SMS tooyour número Twilio. Imediatamente, você deve obter uma resposta SMS que diz "Ei, agradecemos ping Olá! O Twilio e o Azure são demais!".

## <a id="additional_services"></a>Como Usar os Serviços Adicionais do Twilio
Além disso toohello exemplos mostrados aqui, que twilio oferece APIs baseado na web que você pode usar uma funcionalidade adicional Twilio tooleverage do aplicativo do Azure. Para obter detalhes completos, consulte Olá [documentação da API do Twilio][twilio_api_documentation].

### <a id="NextSteps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas sobre Olá Olá Twilio serviço, siga essas toolearn links mais:

* [Diretrizes de segurança do Twilio][twilio_security_guidelines]
* [Código de Exemplo e Procedimentos do Twilio][twilio_howtos]
* [Tutoriais do Guia de início rápido do Twilio][twilio_quickstarts] 
* [Twilio no GitHub][twilio_on_github]
* [Fale tooTwilio suporte][twilio_support]

[twilio_ruby]: https://www.twilio.com/docs/ruby/install





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
[sinatra]: http://www.sinatrarb.com/
[azure_vm_setup]: http://www.windowsazure.com/develop/ruby/tutorials/web-app-with-linux-vm/
