---
title: "saudação de toouse aaaHow SendGrid serviço de email (.NET) | Microsoft Docs"
description: "Saiba como enviar email com hello SendGrid serviço de email no Azure. Exemplos de código escritos em c# e use Olá API .NET."
services: app-service-web
documentationcenter: .net
author: thinkingserious
manager: erikre
editor: 
ms.assetid: 21bf4028-9046-476b-9799-3d3082a0f84c
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2017
ms.author: dx@sendgrid.com
ms.openlocfilehash: b3d77bb67898b991c7293e6b9086b263f6bcb755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-with-azure"></a>Como tooSend Email usando o SendGrid com o Azure
## <a name="overview"></a>Visão geral
Este guia demonstra como tooperform as tarefas de programação comuns com o SendGrid email serviço no Azure. exemplos de saudação são escritos em C\# e oferece suporte ao .NET Standard 1.3. cenários de saudação abordados incluem a construção de email, enviar email, adicionar anexos e permitindo que várias mensagens e configurações de controle. Para obter mais informações sobre SendGrid e enviar email, consulte Olá [próximas etapas] [ Next steps] seção.

## <a name="what-is-hello-sendgrid-email-service"></a>O que é Olá SendGrid serviço de Email?
SendGrid é um [serviço de email baseado em nuvem] que fornece uma [entrega de email transacional], escalabilidade e análise em tempo real confiáveis com APIs flexíveis que facilitam a integração personalizada. Os casos de uso comuns do SendGrid incluem:

* Enviar automaticamente confirmações ou toocustomers de confirmações de compra.
* Administração de listas de distribuição para envio mensal de panfletos eletrônicos e ofertas.
* Coleta de métricas em tempo real para, por exemplo, email bloqueado e engajamento do cliente.
* Encaminhamento de consultas dos clientes.
* Processamento de emails de entrada.

Para obter mais informações, visite [https://sendgrid.com](https://sendgrid.com) ou o repositório GitHub da [biblioteca C#][sendgrid-csharp] do SendGrid.

## <a name="create-a-sendgrid-account"></a>Criar uma conta do SendGrid
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a>Saudação de referência biblioteca de classes do SendGrid .NET
Olá [pacote NuGet do SendGrid](https://www.nuget.org/packages/Sendgrid) é Olá mais fácil maneira tooget Olá API do SendGrid e tooconfigure seu aplicativo com todas as dependências. NuGet é um extensão incluído com o Microsoft Visual Studio 2015 e superior que torna fácil bibliotecas tooinstall e atualização e ferramentas do Visual Studio.

> [!NOTE]
> tooinstall NuGet se você estiver executando uma versão do Visual Studio anterior ao Visual Studio 2015, visite [http://www.nuget.org](http://www.nuget.org)e clique em Olá **instalar NuGet** botão.
>
>

Olá tooinstall pacote NuGet do SendGrid em seu aplicativo, Olá a seguir:

1. Clique em **Novo projeto** e selecione um **Modelo**.

   ![Criar um novo projeto][create-new-project]
2. No **Gerenciador de Soluções**, clique com botão direito em **Referências**, em seguida, clique em **Gerenciar Pacotes NuGet**.

   ![pacote NuGet do SendGrid][SendGrid-NuGet-package]
3. Procurar **SendGrid** e selecione hello **SendGrid** item na lista de resultados.
4. Selecione versão estável mais recente de saudação do pacote do Nuget Olá Olá versão suspensa toobe capaz de toowork com o modelo de objeto hello e APIs demonstrado neste artigo.

   ![Pacote SendGrid][sendgrid-package]
5. Clique em **instalar** toocomplete Olá instalação e, em seguida, feche esta caixa de diálogo.

A biblioteca de classes do .NET do SendGrid se chama **SendGrid**. Ele contém Olá namespaces a seguir:

* **SendGrid** para comunicação com a API do SendGrid.
* **SendGrid.Helpers.Mail** para auxiliar métodos tooeasily criar objetos SendGridMessage que especificam como toosend emails.

Adicione Olá código namespace declarações toohello parte superior de qualquer arquivo c# no qual você deseja que o serviço de email do SendGrid do tooprogrammatically acesso Olá a seguir.

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a>Como: criar um email
Saudação de uso **SendGridMessage** toocreate uma mensagem de email do objeto. Depois que o objeto de mensagem de saudação é criado, você pode definir propriedades e métodos, incluindo o remetente do email hello, destinatário de email Olá e assunto hello e corpo do email hello.

Olá exemplo a seguir demonstra como toocreate um objeto totalmente populado email:

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing hello SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

Para obter mais informações sobre todas as propriedades e métodos com suporte do tipo **SendGrid**, consulte [sendgrid-csharp][sendgrid-csharp] no GitHub.

## <a name="how-to-send-an-email"></a>Como: enviar um email
Depois de criar uma mensagem de email, você poderá enviá-la usando a API do SendGrid. Como alternativa, você poderá usar a [biblioteca incorporada do .NET][NET-library].

O envio de email requer que você forneça sua chave de API do SendGrid. Se você precisar obter detalhes sobre como tooconfigure chaves de API, visite chaves de API do SendGrid [documentação][documentation].

Você pode armazenar essas credenciais por meio de seu Portal do Azure clicando em configurações do aplicativo e adicionar pares de chave/valor de saudação em configurações do aplicativo.

 ![Configurações do aplicativo do Azure][azure_app_settings]

 Em seguida, você pode acessá-las da seguinte forma:

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

Olá exemplos a seguir mostra como toosend uma mensagem usando Olá API da Web.

    using System;
    using System.Threading.Tasks;
    using SendGrid;
    using SendGrid.Helpers.Mail;

    namespace Example
    {
        internal class Example
        {
            private static void Main()
            {
                Execute().Wait();
            }

            static async Task Execute()
            {
                var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
                var client = new SendGridClient(apiKey);
                var msg = new SendGridMessage()
                {
                    From = new EmailAddress("test@example.com", "DX Team"),
                    Subject = "Hello World from hello SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a>Como: adicionar um anexo
Anexos podem ser adicionados a mensagem tooa por chamada hello **AddAttachment** método e minimamente especificando o nome do arquivo hello e codificado na Base64 conteúdo você deseja tooattach. Você pode incluir vários anexos de chamar este método depois de cada arquivo que você deseja tooattach ou usando Olá **AddAttachments** método. saudação de exemplo a seguir demonstra como adicionar uma mensagem de tooa anexo:

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a>Como: Use rodapés de tooenable de configurações de email, acompanhamento e análise
SendGrid fornece a funcionalidade de email adicionais por meio do uso de saudação de configurações de email e controle. Essas configurações podem ser adicionadas tooan email mensagem tooenable funcionalidade específica, como controle de clique, do Google analytics, controle de assinatura e assim por diante. Para obter uma lista completa de aplicativos, consulte Olá [configurações documentação][settings-documentation].

Aplicativos podem ser aplicados muito**SendGrid** usando os métodos implementados como parte da saudação de mensagens de email **SendGridMessage** classe. Olá exemplos a seguir demonstram o rodapé hello e clique em filtros de rastreamento:

Olá exemplos a seguir demonstram o rodapé hello e clique em filtros de rastreamento:

### <a name="footer-settings"></a>Configurações de rodapé
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a>Rastreamento de cliques
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a>Como: usar serviços adicionais do SendGrid
SendGrid oferece várias APIs e webhooks, que você pode usar a funcionalidade adicional tooleverage dentro de seu aplicativo do Azure. Para obter mais detalhes, consulte Olá [referência de API do SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas sobre Olá Olá serviço de Email do SendGrid, siga essas toolearn links mais.

* Repositório da biblioteca C\# do SendGrid: [sendgrid-csharp][sendgrid-csharp]
* Documentação da API do SendGrid: <https://sendgrid.com/docs>

[Next steps]: #next-steps
[What is hello SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference hello SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters tooEnable Footers, Tracking, and Analytics]: #usefilters
[How to: Use Additional SendGrid Services]: #useservices

[create-new-project]: ./media/sendgrid-dotnet-how-to-send-email/new-project.png
[SendGrid-NuGet-package]: ./media/sendgrid-dotnet-how-to-send-email/reference.png
[sendgrid-package]: ./media/sendgrid-dotnet-how-to-send-email/sendgrid-package.png
[azure_app_settings]: ./media/sendgrid-dotnet-how-to-send-email/azure-app-settings.png
[sendgrid-csharp]: https://github.com/sendgrid/sendgrid-csharp
[SMTP vs. Web API]: https://sendgrid.com/docs/Integrate/index.html
[App Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/api_v3.html
[NET-library]: https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html#-Using-NETs-Builtin-SMTP-Library
[documentation]: https://sendgrid.com/docs/Classroom/Send/api_keys.html
[settings-documentation]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html

[serviço de email baseado em nuvem]: https://sendgrid.com/solutions
[entrega de email transacional]: https://sendgrid.com/use-cases/transactional-email

