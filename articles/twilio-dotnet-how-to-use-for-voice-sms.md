---
title: aaaHow tooUse Twilio para voz e SMS (.NET) | Microsoft Docs
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Amostras de código gravadas no .NET."
services: 
documentationcenter: .net
author: devinrader
manager: twilio
editor: 
ms.assetid: 74d4f3c9-f1cb-4968-b744-36b32cd0e834
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/24/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f568da87ef15e9f540fee9674de31e983d4acb6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a>Como toouse Twilio para recursos SMS do Azure e voz
Este guia demonstra como tooperform as tarefas de programação comuns com hello Twilio API de serviço no Azure. cenários de saudação abordados incluem fazer uma chamada telefônica e enviar uma mensagem do serviço SMS (Short Message). Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte Olá [próximas etapas](#NextSteps) seção.

## <a id="WhatIs"></a>O que é Twilio?
Twilio é capacitam Olá futuro das comunicações de negócios, habilitar os desenvolvedores tooembed voice, VoIP e mensagens em aplicativos. Eles virtualizam todos infraestrutura necessária em um ambiente baseado em nuvem, global, expô-lo por meio da plataforma Olá Twilio API de comunicação. Os aplicativos são toobuild simple e escalonável. Aproveite a flexibilidade com preço pré-pago e se beneficie da confiabilidade da nuvem.

**Voz Twilio** permite que seus aplicativos toomake e receber chamadas telefônicas. **Twilio SMS** permite que seus aplicativos toosend e receber mensagens SMS. **Clientes do Twilio** permite chamadas de VoIP toomake de qualquer telefone, tablet ou navegador e dá suporte a WebRTC.

## <a id="Pricing"></a>Preços e ofertas especiais da Twilio
Os clientes do Azure recebem uma [oferta especial](http://www.twilio.com/azure): US$ 10 de cortesia de crédito da Twilio quando atualizam a sua conta da Twilio. Esse crédito Twilio podem ser aplicadas tooany Twilio uso (US $10 crédito equivalente toosending até 1.000 mensagens SMS ou recebimento de too1000 minutos de voz, dependendo do local de saudação do seu destino de número e a mensagem ou chamada telefônica de entrada). Resgate esse crédito da Twilio e faça uma introdução em [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio é um serviço flexível. Não há nenhuma taxa de configuração e você pode fechar sua conta a qualquer momento. Você pode encontrar mais detalhes em [Preços da Twilio](http://www.twilio.com/voice/pricing).

## <a id="Concepts"></a>Conceitos
Olá Twilio API é uma API RESTful que fornece funcionalidade SMS e voz para aplicativos. As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].

Principais aspectos da saudação Twilio API são verbos do Twilio e Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Verbos da Twilio
Olá API faz uso do Twilio verbos; Por exemplo, Olá  **&lt;diga&gt;**  verbo instrui Twilio tooaudibly entregar uma mensagem em uma chamada.

a seguir Olá é uma lista de verbos do Twilio.  Saiba sobre Olá outros verbos e recursos por meio de [documentação de linguagem de marcação do Twilio](http://www.twilio.com/docs/api/twiml).

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

## <a id="create_app"></a>Criar um aplicativo Azure
Um aplicativo do Azure que hospeda um aplicativo Twilio habilitado não é diferente de qualquer outro aplicativo do Azure. Adicionar a biblioteca do .NET do Twilio hello e configurar Olá função toouse Olá Twilio .NET bibliotecas.
Para obter informações sobre como criar um projeto inicial do Azure, consulte [Creating an Azure project with Visual Studio][vs_project] (Criando um projeto do Azure com o Visual Studio).

## <a id="configure_app"></a>Configurar seu aplicativo toouse Twilio bibliotecas
Twilio fornece um conjunto de bibliotecas do auxiliar de .NET que envolvem vários aspectos do Twilio tooprovide maneiras simples e fácil toointeract com hello API REST do Twilio e clientes do Twilio toogenerate TwiML respostas.

Twilio fornece cinco bibliotecas para desenvolvedores .NET:
Biblioteca|Descrição
---|---
Twilio.API|Olá Twilio biblioteca principal que encapsula Olá API REST do Twilio em uma biblioteca .NET amigável. Essa biblioteca está disponível para o .NET, Silverlight e Windows Phone 7.
Twilio.TwiML|Fornece uma marcação de TwiML toogenerate .NET forma amigável.
Twilio.MVC|Para os desenvolvedores que usam o ASP.NET MVC, esta biblioteca inclui um TwilioController, o TwiML ActionResult e o atributo de validação de solicitação.
Twilio.WebMatrix|Para os desenvolvedores usando a ferramenta de desenvolvimento do WebMatrix gratuita da Microsoft, esta biblioteca contém auxiliares de sintaxe do Razor para várias ações de Twilio.
Twilio.Client.Capability|Contém o gerador de token de recurso Olá para uso com hello Twilio SDK de JavaScript do cliente.

Observe que todas as bibliotecas requerem o .NET 3.5, Silverlight 4 ou Windows Phone 7 ou posterior.

exemplos de saudação fornecidos neste guia usam biblioteca de Twilio.API hello.

Olá bibliotecas podem ser [instalados usando a extensão do Gerenciador de pacote de NuGet de saudação](http://www.twilio.com/docs/csharp/install) disponíveis para o Visual Studio 2010 para cima too2015.  Olá código-fonte está hospedado em [GitHub][twilio_github_repo], que inclui um Wiki que contém a documentação completa do uso de bibliotecas de saudação.

Por padrão, o Microsoft Visual Studio 2010 instala a versão 1.2 do NuGet. Instalar bibliotecas do Twilio Olá requer a versão 1.6 do NuGet ou superior. Para obter mais informações sobre como instalar ou atualizar o NuGet, consulte [http://nuget.org/][nuget].

> [!NOTE]
> tooinstall Olá última versão do NuGet, você deve primeiro desinstalar Olá versão carregado usando Olá Gerenciador de extensões do Visual Studio. toodo, portanto, você deve executar o Visual Studio como administrador. Caso contrário, o botão de desinstalação hello está desabilitado.
>
>

### <a id="use_nuget"></a>tooadd Olá Twilio bibliotecas tooyour projeto do Visual Studio:
1. Abra sua solução no Visual Studio.
2. Clique com o botão direito do mouse em **Referências**.
3. Clique em **Gerenciar Pacotes NuGet...**
4. Clique em **Online**.
5. Na caixa online de pesquisa de hello, digite *twilio*.
6. Clique em **instalar** no pacote do Twilio hello.

## <a id="howto_make_call"></a>Como fazer uma chamada externa
Olá a seguir mostra como uma saída de toomake chamar usando Olá **CallResource** classe. Esse código também usa uma saudação do site fornecidos Twilio tooreturn resposta Twilio Markup Language (TwiML). Substitua os valores para Olá **para** e **de** números de telefone e certifique-se de que você verifique Olá **de** número de telefone para sua conta do Twilio antes de executar código hello.

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set hello call From, To, and URL values toouse for hello call.
    // This sample uses hello sandbox number provided by
    // Twilio toomake hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

Para obter mais informações sobre parâmetros de saudação passado toohello **CallResource.Create** método, consulte [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Conforme mencionado, esse código usa uma saudação do site fornecidos Twilio tooreturn TwiML resposta. Em vez disso, você pode usar seu próprio hello tooprovide do site TwiML resposta. Para obter mais informações, consulte [Como fornecer respostas do TwiML de seu próprio site](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Como enviar uma mensagem de SMS
Olá seguinte captura de tela mostra como toosend uma mensagem SMS usando Olá **MessageResource** classe. Olá **de** número é fornecido por Twilio para contas de avaliação toosend mensagens SMS. Olá **para** número deve ser verificado para sua conta do Twilio antes de executar código hello.

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    try
    {
        // Send an SMS message.
        var message = MessageResource.Create(
            to: new PhoneNumber("+12069419717"),
            from: new PhoneNumber("+14155992671"),
            body: "This is my SMS message.");
    }
    catch (TwilioException ex)
    {
        // An exception occurred making hello REST call
        Console.WriteLine(ex.Message);
    }

## <a id="howto_provide_twiml_responses"></a>Como fornecer respostas TwiML de seu próprio site
Quando o aplicativo inicia toohello uma chamada de API do Twilio - por exemplo, por meio de saudação **CallResource.Create** método - Twilio envia sua solicitação URL de tooan que é esperado tooreturn uma resposta TwiML. exemplo Hello [como: fazer uma chamada de saída](#howto_make_call) usa Olá URL fornecida Twilio [http://twimlets.com/message] [ twimlet_message_url] tooreturn resposta de saudação.

> [!NOTE]
> Enquanto TwiML é projetado para uso pelos serviços da web, você pode exibir hello TwiML em seu navegador. Por exemplo, clique em [http://twimlets.com/message] [ twimlet_message_url] toosee vazio &lt;resposta&gt; elemento; como outro exemplo, clique em [http://twimlets.com/message ? Mensagem % 5B0 %5D = Olá % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee um &lt;resposta&gt; elemento que contém um &lt;diga&gt; elemento.
>
>

Em vez de depender de URL fornecido Twilio de saudação, você pode criar seu próprio site de URL que retorna respostas de HTTP. Você pode criar o site de saudação em qualquer linguagem que retorna respostas de HTTP. Este tópico pressupõe que você vai hospedando Olá URL de um manipulador genérico do ASP.NET.

Olá seguindo o manipulador ASP.NET monta uma resposta de TwiML diz **Hello World** na chamada de saudação.

    using System.Text;
    using System.Web;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {
            public void ProcessRequest(HttpContext context)
            {
                const string twiMLResponse =
                    "<Response><Say>Hello World.</Say></Response>";
                
                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.ContentEncoding = Encoding.UTF8;
                context.Response.Write(twiMLResponse);
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }
    
Como você pode ver do exemplo hello acima, Olá TwiML resposta é simplesmente um documento XML. biblioteca de Twilio.TwiML Olá contém classes que irá gerar TwiML para você. Olá exemplo a seguir produz resposta equivalente hello como mostrado acima, mas usa Olá **VoiceResponse** classe.

    using System.Web;
    using Twilio.TwiML;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {

            public void ProcessRequest(HttpContext context)
            {
                var twiml = new VoiceResponse();
                twiml.Say("Hello World.");

                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.Write(twiml.ToString());
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }

Para obter mais informações sobre TwiML, consulte [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).

Depois que você configurar respostas de TwiML de tooprovide uma forma, você pode passar essa URL toohello **CallResource.Create** método. Por exemplo, se você tiver um aplicativo web chamado tooan MyTwiML implantado o serviço de nuvem do Azure e nome de saudação do seu manipulador ASP.NET é mytwiml.ashx, Olá URL pode ser passado muito**CallResource.Create** conforme Olá código a seguir exemplo:

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

Para obter informações adicionais sobre como usar o Twilio no Azure com o ASP.NET, consulte [como toomake um telefone de chamada usando o Twilio em uma função web no Azure][howto_phonecall_dotnet].

[!INCLUDE [twilio-additional-services-and-next-steps](../includes/twilio-additional-services-and-next-steps.md)]

[howto_phonecall_dotnet]: partner-twilio-cloud-services-dotnet-phone-call-web-role.md

[twimlet_message_url]: http://twimlets.com/message

[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls

[vs_project]:http://msdn.microsoft.com/library/windowsazure/ee405487.aspx
[nuget]:http://nuget.org/
[twilio_github_repo]:https://github.com/twilio/twilio-csharp

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
