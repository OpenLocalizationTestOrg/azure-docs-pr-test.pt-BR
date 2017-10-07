---
title: aaaHow tooUse Twilio para voz e SMS (Java) | Microsoft Docs
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Exemplos de códigos escritos em Java."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a>Como tooUse Twilio para recursos de SMS no Java e voz
Este guia demonstra como tooperform as tarefas de programação comuns com hello Twilio API de serviço no Azure. cenários de saudação abordados incluem fazer uma chamada telefônica e enviar uma mensagem do serviço SMS (Short Message). Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte Olá [próximas etapas](#NextSteps) seção.

## <a id="WhatIs"></a>O que é Twilio?
Twilio é uma API de serviço web de telefonia que permite que você use seus idiomas de web existente e voz de toobuild habilidades e aplicativos de SMS. O Twilio é um serviço de terceiro (não é um recurso do Azure e não é um produto da Microsoft).

**Voz Twilio** permite que seus aplicativos toomake e receber chamadas telefônicas. **Twilio SMS** permite que seus aplicativos toomake e receber mensagens SMS. **Clientes do Twilio** permite comunicação por voz tooenable usando conexões da Internet existentes, incluindo conexões móveis que seus aplicativos.

## <a id="Pricing"></a>Preços e ofertas especiais da Twilio
A informações sobre os preços do Twilio estão disponíveis em [Preços do Twilio][twilio_pricing]. Os clientes do Azure recebem uma [oferta especial][special_offer]: um crédito de 1.000 mensagens de texto gratuitas ou 1.000 minutos de entrada. toosign para esta oferta ou obter mais informações, visite [http://ahoy.twilio.com/azure][special_offer].

## <a id="Concepts"></a>Conceitos
Olá Twilio API é uma API RESTful que fornece funcionalidade SMS e voz para aplicativos. As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].

Principais aspectos da saudação Twilio API são verbos do Twilio e Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Verbos da Twilio
Olá API faz uso do Twilio verbos; Por exemplo, Olá  **&lt;diga&gt;**  verbo instrui Twilio tooaudibly entregar uma mensagem em uma chamada.

a seguir Olá é uma lista de verbos do Twilio.

* **&lt;Discagem&gt;**: conecta-se o telefone de tooanother Olá chamador.
* **&lt;Coletar&gt;**: coleta dígitos numéricos inseridos no teclado numérico do telefone hello.
* **&lt;Hangup&gt;**: termina uma chamada.
* **&lt;Play&gt;**: reproduz um arquivo de áudio.
* **&lt;Fila&gt;**: Adicionar Olá tooa fila de chamadores.
* **&lt;Pause&gt;**: espera silenciosamente por um número especificado de segundos.
* **&lt;Registro&gt;**: registra a voz do chamador hello e retorna uma URL de um arquivo que contém a gravação da saudação.
* **&lt;Redirecionar&gt;**: transfere o controle de uma chamada ou SMS toohello TwiML em uma URL diferente.
* **&lt;Rejeitar&gt;**: rejeita uma entrada chamar tooyour Twilio número sem cobrança você.
* **&lt;Digamos que&gt;**: converte texto toospeech que é feita em uma chamada.
* **&lt;Sms&gt;**: envia uma mensagem SMS.

### <a id="TwiML"></a>TwiML
TwiML é um conjunto de instruções baseadas em XML com base em verbos do Twilio Olá que informam o Twilio como tooprocess uma chamada ou SMS.

Por exemplo, Olá TwiML a seguir seria converter o texto de saudação **Olá, mundo!** toospeech.

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

Quando a aplicativo chama hello Twilio API, um dos parâmetros de API de saudação é URL Olá retorna Olá TwiML resposta. Para fins de desenvolvimento, você pode usar URLs fornecido Twilio tooprovide Olá TwiML as respostas usadas pelos aplicativos. Você também pode hospedar seus próprio respostas de TwiML URLs tooproduce hello e outra opção é Olá toouse **TwiMLResponse** objeto.

Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml]. Para obter informações adicionais sobre Olá Twilio API, consulte [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Criar uma conta na Twilio
Quando você estiver pronto tooget uma conta do Twilio, inscreva-se em [tente Twilio][try_twilio]. Você pode começar com uma conta gratuita e atualizá-la depois.

Quando você se inscrever para uma conta de Twilio, você receberá uma ID de conta e um token de autenticação. Ambos serão chamadas à API do Twilio toomake necessários. tooprevent não autorizado acessar conta tooyour, mantenha o token de autenticação segura. Sua ID da conta e a autenticação token são visíveis no hello [Twilio Console][twilio_console], no hello campos rotulados **SID da conta** e **TOKEN de autenticação**, respectivamente.

## <a id="create_app"></a>Criar um aplicativo Java
1. Obter Olá JAR do Twilio e adicioná-lo tooyour Java criar o caminho e o seu assembly de implantação WAR. Em [https://github.com/twilio/twilio-java][twilio_java], você pode baixar fontes do GitHub hello e criar seu próprios JAR ou baixar um JAR pré-criado (com ou sem dependências).
2. Verifique se o seu JDK **cacerts** keystore contém o certificado de autoridade de certificação segura Equifax Olá com impressão digital de MD5 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (número de série de saudação é 35:DE:F4:CF e hello SHA1 impressão digital é D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Este é o certificado de autoridade de certificado Olá para Olá [https://api.twilio.com] [ twilio_api_service] service, que é chamado quando você usar as APIs do Twilio. Para obter informações sobre como garantir seu JDK **cacerts** keystore contém o certificado de autoridade de certificação correto hello, consulte [adicionando um certificado toohello repositório de certificados de autoridade de certificação de Java][add_ca_cert].

Instruções detalhadas para usar a biblioteca de clientes do Twilio Olá para Java estão disponíveis em [como tooMake uma chamada telefônica usando o Twilio em um aplicativo Java no Azure][howto_phonecall_java].

## <a id="configure_app"></a>Configurar seu aplicativo tooUse Twilio bibliotecas
Dentro de seu código, você pode adicionar **importar** instruções na parte superior da saudação de seus arquivos de origem para Olá Twilio pacotes ou classes que você deseja toouse em seu aplicativo.

Para arquivos de origem Java:

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

Para arquivos de origem Java Server Page (JSP):

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
Dependendo de quais pacotes Twilio ou classes que você deseja toouse, seu **importar** instruções podem ser diferentes.

## <a id="howto_make_call"></a>Como fazer uma chamada externa
Olá a seguir mostra como uma saída de toomake chamar usando Olá **chamar** classe. Esse código também usa uma saudação do site fornecidos Twilio tooreturn resposta Twilio Markup Language (TwiML). Substitua os valores para Olá **de** e **para** números de telefone e certifique-se de que você verifique Olá **de** número de telefone para o seu código de saudação do Twilio conta toorunning anterior.

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Para obter mais informações sobre parâmetros de saudação passado toohello **Call.creator** método, consulte [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Conforme mencionado, esse código usa uma saudação do site fornecidos Twilio tooreturn TwiML resposta. Em vez disso, você pode usar seu próprio hello tooprovide do site TwiML resposta; Para obter mais informações, consulte [como tooProvide TwiML respostas em um aplicativo Java no Azure](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Como enviar uma mensagem de SMS
Olá a seguir mostra como toosend uma mensagem SMS usando Olá **mensagem** classe. Olá **de** número, **4155992671**, é fornecido por Twilio para contas de avaliação toosend mensagens SMS. Olá **para** número deve ser verificado para seu código de saudação do Twilio conta toorunning anterior.

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

Para obter mais informações sobre parâmetros de saudação passado toohello **Message.creator** método, consulte [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].

## <a id="howto_provide_twiml_responses"></a>Como fornecer respostas TwiML de seu próprio site
Quando o aplicativo inicia toohello uma chamada de API do Twilio, por exemplo por meio de saudação **CallCreator.create** método Twilio enviará a URL de tooa de solicitação que é esperado tooreturn uma resposta TwiML. exemplo Hello acima usa a URL fornecida Twilio de saudação [http://twimlets.com/message][twimlet_message_url]. (Embora TwiML foi projetado para uso pelos serviços da Web, você pode exibir hello TwiML em seu navegador. Por exemplo, clique em [http://twimlets.com/message] [ twimlet_message_url] toosee vazio  **&lt;resposta&gt;**  elemento; como outro exemplo, clique em [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee um  **&lt;resposta&gt;**  elemento que contém um  **&lt;diga &gt;**  elemento.)

Em vez de depender de URL fornecido Twilio de saudação, você pode criar seu próprio site de URL que retorna respostas de HTTP. Você pode criar site hello em qualquer linguagem que retorna respostas HTTP; Este tópico pressupõe que você vai hospedando Olá URL em uma página JSP.

Olá JSP página resultados em uma resposta de TwiML que diz que a seguir **Olá, mundo!** na chamada de saudação.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

Olá JSP página resultados em uma resposta de TwiML que diz que algum texto a seguir tem vários pausa e diz informações sobre a versão da API do Twilio hello e o nome de função do Azure hello.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

Olá **ApiVersion** parâmetro está disponível em solicitações de voz do Twilio (não a solicitações SMS). parâmetros de solicitação disponíveis toosee Olá para voz Twilio e solicitações SMS, consulte <https://www.twilio.com/docs/api/twiml/twilio_request> e <https://www.twilio.com/docs/api/twiml/sms/twilio_request >, respectivamente. Olá **RoleName** variável de ambiente está disponível como parte de uma implantação do Azure. (Se você quiser tooadd variáveis de ambiente personalizado para que eles podem ser retirados do **System.getenv**, consulte a seção de variáveis de ambiente Olá no [diversos parâmetros de configuração de função] [misc_role_config_settings].)

Depois de você tiver sua página JSP configurar tooprovide TwiML respostas, use Olá URL da página JSP Olá Olá URL passada em hello **Call.creator** método. Por exemplo, se você tiver um aplicativo Web chamado tooan MyTwiML implantado hospedado do Azure service e Olá nome de página JSP Olá mytwiml.jsp, Olá URL pode ser passado muito**Call.creator** conforme mostrado na seguinte hello:

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Outra opção para responder com TwiML é por meio de saudação **VoiceResponse** classe, que está disponível no hello **com.twilio.twiml** pacote.

Para obter informações adicionais sobre como usar o Twilio no Azure com Java, consulte [como tooMake uma chamada telefônica usando o Twilio em um aplicativo Java no Azure][howto_phonecall_java].

## <a id="AdditionalServices"></a>Como Usar os Serviços Adicionais do Twilio
Além disso toohello exemplos mostrados aqui, que twilio oferece APIs baseado na web que você pode usar uma funcionalidade adicional Twilio tooleverage do aplicativo do Azure. Para obter detalhes completos, consulte Olá [documentação da API do Twilio][twilio_api_documentation].

## <a id="NextSteps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas sobre Olá Olá Twilio serviço, siga essas toolearn links mais:

* [Diretrizes de segurança do Twilio][twilio_security_guidelines]
* [Código de Exemplo e Procedimentos do Twilio][twilio_howtos]
* [Tutoriais do Guia de início rápido do Twilio][twilio_quickstarts]
* [Twilio no GitHub][twilio_on_github]
* [Fale tooTwilio suporte][twilio_support]

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
