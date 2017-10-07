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
# <a name="how-toosend-email-using-sendgrid-with-azure"></a><span data-ttu-id="3048a-104">Como tooSend Email usando o SendGrid com o Azure</span><span class="sxs-lookup"><span data-stu-id="3048a-104">How tooSend Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="3048a-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3048a-105">Overview</span></span>
<span data-ttu-id="3048a-106">Este guia demonstra como tooperform as tarefas de programação comuns com o SendGrid email serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="3048a-106">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="3048a-107">exemplos de saudação são escritos em C\# e oferece suporte ao .NET Standard 1.3.</span><span class="sxs-lookup"><span data-stu-id="3048a-107">hello samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="3048a-108">cenários de saudação abordados incluem a construção de email, enviar email, adicionar anexos e permitindo que várias mensagens e configurações de controle.</span><span class="sxs-lookup"><span data-stu-id="3048a-108">hello scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="3048a-109">Para obter mais informações sobre SendGrid e enviar email, consulte Olá [próximas etapas] [ Next steps] seção.</span><span class="sxs-lookup"><span data-stu-id="3048a-109">For more information on SendGrid and sending email, see hello [Next steps][Next steps] section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="3048a-110">O que é Olá SendGrid serviço de Email?</span><span class="sxs-lookup"><span data-stu-id="3048a-110">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="3048a-111">SendGrid é um [serviço de email baseado em nuvem] que fornece uma [entrega de email transacional], escalabilidade e análise em tempo real confiáveis com APIs flexíveis que facilitam a integração personalizada.</span><span class="sxs-lookup"><span data-stu-id="3048a-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="3048a-112">Os casos de uso comuns do SendGrid incluem:</span><span class="sxs-lookup"><span data-stu-id="3048a-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="3048a-113">Enviar automaticamente confirmações ou toocustomers de confirmações de compra.</span><span class="sxs-lookup"><span data-stu-id="3048a-113">Automatically sending receipts or purchase confirmations toocustomers.</span></span>
* <span data-ttu-id="3048a-114">Administração de listas de distribuição para envio mensal de panfletos eletrônicos e ofertas.</span><span class="sxs-lookup"><span data-stu-id="3048a-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="3048a-115">Coleta de métricas em tempo real para, por exemplo, email bloqueado e engajamento do cliente.</span><span class="sxs-lookup"><span data-stu-id="3048a-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="3048a-116">Encaminhamento de consultas dos clientes.</span><span class="sxs-lookup"><span data-stu-id="3048a-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="3048a-117">Processamento de emails de entrada.</span><span class="sxs-lookup"><span data-stu-id="3048a-117">Processing incoming emails.</span></span>

<span data-ttu-id="3048a-118">Para obter mais informações, visite [https://sendgrid.com](https://sendgrid.com) ou o repositório GitHub da [biblioteca C#][sendgrid-csharp] do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="3048a-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="3048a-119">Criar uma conta do SendGrid</span><span class="sxs-lookup"><span data-stu-id="3048a-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a><span data-ttu-id="3048a-120">Saudação de referência biblioteca de classes do SendGrid .NET</span><span class="sxs-lookup"><span data-stu-id="3048a-120">Reference hello SendGrid .NET Class Library</span></span>
<span data-ttu-id="3048a-121">Olá [pacote NuGet do SendGrid](https://www.nuget.org/packages/Sendgrid) é Olá mais fácil maneira tooget Olá API do SendGrid e tooconfigure seu aplicativo com todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="3048a-121">hello [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is hello easiest way tooget hello SendGrid API and tooconfigure your application with all dependencies.</span></span> <span data-ttu-id="3048a-122">NuGet é um extensão incluído com o Microsoft Visual Studio 2015 e superior que torna fácil bibliotecas tooinstall e atualização e ferramentas do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3048a-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy tooinstall and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="3048a-123">tooinstall NuGet se você estiver executando uma versão do Visual Studio anterior ao Visual Studio 2015, visite [http://www.nuget.org](http://www.nuget.org)e clique em Olá **instalar NuGet** botão.</span><span class="sxs-lookup"><span data-stu-id="3048a-123">tooinstall NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click hello **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="3048a-124">Olá tooinstall pacote NuGet do SendGrid em seu aplicativo, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3048a-124">tooinstall hello SendGrid NuGet package in your application, do hello following:</span></span>

1. <span data-ttu-id="3048a-125">Clique em **Novo projeto** e selecione um **Modelo**.</span><span class="sxs-lookup"><span data-stu-id="3048a-125">Click on **New Project** and select a **Template**.</span></span>

   ![Criar um novo projeto][create-new-project]
2. <span data-ttu-id="3048a-127">No **Gerenciador de Soluções**, clique com botão direito em **Referências**, em seguida, clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3048a-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![pacote NuGet do SendGrid][SendGrid-NuGet-package]
3. <span data-ttu-id="3048a-129">Procurar **SendGrid** e selecione hello **SendGrid** item na lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="3048a-129">Search for **SendGrid** and select hello **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="3048a-130">Selecione versão estável mais recente de saudação do pacote do Nuget Olá Olá versão suspensa toobe capaz de toowork com o modelo de objeto hello e APIs demonstrado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="3048a-130">Select hello latest stable version of hello Nuget package from hello version dropdown toobe able toowork with hello object model and APIs demonstrated in this article.</span></span>

   ![Pacote SendGrid][sendgrid-package]
5. <span data-ttu-id="3048a-132">Clique em **instalar** toocomplete Olá instalação e, em seguida, feche esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3048a-132">Click **Install** toocomplete hello installation, and then close this dialog.</span></span>

<span data-ttu-id="3048a-133">A biblioteca de classes do .NET do SendGrid se chama **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="3048a-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="3048a-134">Ele contém Olá namespaces a seguir:</span><span class="sxs-lookup"><span data-stu-id="3048a-134">It contains hello following namespaces:</span></span>

* <span data-ttu-id="3048a-135">**SendGrid** para comunicação com a API do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="3048a-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="3048a-136">**SendGrid.Helpers.Mail** para auxiliar métodos tooeasily criar objetos SendGridMessage que especificam como toosend emails.</span><span class="sxs-lookup"><span data-stu-id="3048a-136">**SendGrid.Helpers.Mail** for helper methods tooeasily create SendGridMessage objects that specify how toosend emails.</span></span>

<span data-ttu-id="3048a-137">Adicione Olá código namespace declarações toohello parte superior de qualquer arquivo c# no qual você deseja que o serviço de email do SendGrid do tooprogrammatically acesso Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="3048a-137">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access hello SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="3048a-138">Como: criar um email</span><span class="sxs-lookup"><span data-stu-id="3048a-138">How to: Create an Email</span></span>
<span data-ttu-id="3048a-139">Saudação de uso **SendGridMessage** toocreate uma mensagem de email do objeto.</span><span class="sxs-lookup"><span data-stu-id="3048a-139">Use hello **SendGridMessage** object toocreate an email message.</span></span> <span data-ttu-id="3048a-140">Depois que o objeto de mensagem de saudação é criado, você pode definir propriedades e métodos, incluindo o remetente do email hello, destinatário de email Olá e assunto hello e corpo do email hello.</span><span class="sxs-lookup"><span data-stu-id="3048a-140">Once hello message object is created, you can set properties and methods, including hello email sender, hello email recipient, and hello subject and body of hello email.</span></span>

<span data-ttu-id="3048a-141">Olá exemplo a seguir demonstra como toocreate um objeto totalmente populado email:</span><span class="sxs-lookup"><span data-stu-id="3048a-141">hello following example demonstrates how toocreate a fully populated email object:</span></span>

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

<span data-ttu-id="3048a-142">Para obter mais informações sobre todas as propriedades e métodos com suporte do tipo **SendGrid**, consulte [sendgrid-csharp][sendgrid-csharp] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="3048a-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="3048a-143">Como: enviar um email</span><span class="sxs-lookup"><span data-stu-id="3048a-143">How to: Send an Email</span></span>
<span data-ttu-id="3048a-144">Depois de criar uma mensagem de email, você poderá enviá-la usando a API do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="3048a-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="3048a-145">Como alternativa, você poderá usar a [biblioteca incorporada do .NET][NET-library].</span><span class="sxs-lookup"><span data-stu-id="3048a-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="3048a-146">O envio de email requer que você forneça sua chave de API do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="3048a-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="3048a-147">Se você precisar obter detalhes sobre como tooconfigure chaves de API, visite chaves de API do SendGrid [documentação][documentation].</span><span class="sxs-lookup"><span data-stu-id="3048a-147">If you need details about how tooconfigure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="3048a-148">Você pode armazenar essas credenciais por meio de seu Portal do Azure clicando em configurações do aplicativo e adicionar pares de chave/valor de saudação em configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3048a-148">You may store these credentials via your Azure Portal by clicking Application settings and adding hello key/value pairs under App settings.</span></span>

 ![Configurações do aplicativo do Azure][azure_app_settings]

 <span data-ttu-id="3048a-150">Em seguida, você pode acessá-las da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="3048a-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="3048a-151">Olá exemplos a seguir mostra como toosend uma mensagem usando Olá API da Web.</span><span class="sxs-lookup"><span data-stu-id="3048a-151">hello following examples show how toosend a message using hello Web API.</span></span>

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

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="3048a-152">Como: adicionar um anexo</span><span class="sxs-lookup"><span data-stu-id="3048a-152">How to: Add an attachment</span></span>
<span data-ttu-id="3048a-153">Anexos podem ser adicionados a mensagem tooa por chamada hello **AddAttachment** método e minimamente especificando o nome do arquivo hello e codificado na Base64 conteúdo você deseja tooattach.</span><span class="sxs-lookup"><span data-stu-id="3048a-153">Attachments can be added tooa message by calling hello **AddAttachment** method and minimally specifying hello file name and Base64 encoded content you want tooattach.</span></span> <span data-ttu-id="3048a-154">Você pode incluir vários anexos de chamar este método depois de cada arquivo que você deseja tooattach ou usando Olá **AddAttachments** método.</span><span class="sxs-lookup"><span data-stu-id="3048a-154">You can include multiple attachments by calling this method once for each file you wish tooattach or by using hello **AddAttachments** method.</span></span> <span data-ttu-id="3048a-155">saudação de exemplo a seguir demonstra como adicionar uma mensagem de tooa anexo:</span><span class="sxs-lookup"><span data-stu-id="3048a-155">hello following example demonstrates adding an attachment tooa message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="3048a-156">Como: Use rodapés de tooenable de configurações de email, acompanhamento e análise</span><span class="sxs-lookup"><span data-stu-id="3048a-156">How to: Use mail settings tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="3048a-157">SendGrid fornece a funcionalidade de email adicionais por meio do uso de saudação de configurações de email e controle.</span><span class="sxs-lookup"><span data-stu-id="3048a-157">SendGrid provides additional email functionality through hello use of mail settings and tracking settings.</span></span> <span data-ttu-id="3048a-158">Essas configurações podem ser adicionadas tooan email mensagem tooenable funcionalidade específica, como controle de clique, do Google analytics, controle de assinatura e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="3048a-158">These settings can be added tooan email message tooenable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="3048a-159">Para obter uma lista completa de aplicativos, consulte Olá [configurações documentação][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="3048a-159">For a full list of apps, see hello [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="3048a-160">Aplicativos podem ser aplicados muito**SendGrid** usando os métodos implementados como parte da saudação de mensagens de email **SendGridMessage** classe.</span><span class="sxs-lookup"><span data-stu-id="3048a-160">Apps can be applied too**SendGrid** email messages using methods implemented as part of hello **SendGridMessage** class.</span></span> <span data-ttu-id="3048a-161">Olá exemplos a seguir demonstram o rodapé hello e clique em filtros de rastreamento:</span><span class="sxs-lookup"><span data-stu-id="3048a-161">hello following examples demonstrate hello footer and click tracking filters:</span></span>

<span data-ttu-id="3048a-162">Olá exemplos a seguir demonstram o rodapé hello e clique em filtros de rastreamento:</span><span class="sxs-lookup"><span data-stu-id="3048a-162">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="3048a-163">Configurações de rodapé</span><span class="sxs-lookup"><span data-stu-id="3048a-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="3048a-164">Rastreamento de cliques</span><span class="sxs-lookup"><span data-stu-id="3048a-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="3048a-165">Como: usar serviços adicionais do SendGrid</span><span class="sxs-lookup"><span data-stu-id="3048a-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="3048a-166">SendGrid oferece várias APIs e webhooks, que você pode usar a funcionalidade adicional tooleverage dentro de seu aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="3048a-166">SendGrid offers several APIs and webhooks that you can use tooleverage additional functionality within your Azure application.</span></span> <span data-ttu-id="3048a-167">Para obter mais detalhes, consulte Olá [referência de API do SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="3048a-167">For more details, see hello [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="3048a-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3048a-168">Next steps</span></span>
<span data-ttu-id="3048a-169">Agora que você aprendeu as Noções básicas sobre Olá Olá serviço de Email do SendGrid, siga essas toolearn links mais.</span><span class="sxs-lookup"><span data-stu-id="3048a-169">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="3048a-170">Repositório da biblioteca C\# do SendGrid: [sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="3048a-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="3048a-171">Documentação da API do SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="3048a-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

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

