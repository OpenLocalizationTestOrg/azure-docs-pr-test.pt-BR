---
title: "Como usar o serviço de email SendGrid (.NET) | Microsoft Docs"
description: "Saiba como enviar email com o serviço de email SendGrid no Azure. Exemplos de código escritos em c# e usam a API .NET."
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
ms.openlocfilehash: b3a48b3c838763b022a18e55817ec7455fe94c85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-send-email-using-sendgrid-with-azure"></a><span data-ttu-id="015d0-104">Como enviar emails usando o SendGrid com o Azure</span><span class="sxs-lookup"><span data-stu-id="015d0-104">How to Send Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="015d0-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="015d0-105">Overview</span></span>
<span data-ttu-id="015d0-106">Este guia demonstra como executar tarefas comuns de programação com o serviço de email SendGrid no Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="015d0-106">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="015d0-107">Os exemplos são escritos em C\# e dão suporte a .NET Standard 1.3.</span><span class="sxs-lookup"><span data-stu-id="015d0-107">The samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="015d0-108">Os cenários abordados incluem a criação e o envio de emails, a adição de anexos e a habilitação de várias configurações de email e acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="015d0-108">The scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="015d0-109">Para obter mais informações sobre o SendGrid e o envio de emails, consulte a seção [Próximas etapas][Next steps].</span><span class="sxs-lookup"><span data-stu-id="015d0-109">For more information on SendGrid and sending email, see the [Next steps][Next steps] section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="015d0-110">O que é o serviço de email SendGrid?</span><span class="sxs-lookup"><span data-stu-id="015d0-110">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="015d0-111">SendGrid é um [serviço de email baseado em nuvem] que fornece uma [entrega de email transacional], escalabilidade e análise em tempo real confiáveis com APIs flexíveis que facilitam a integração personalizada.</span><span class="sxs-lookup"><span data-stu-id="015d0-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="015d0-112">Os casos de uso comuns do SendGrid incluem:</span><span class="sxs-lookup"><span data-stu-id="015d0-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="015d0-113">Envio automático de recibos ou confirmações de compra para os clientes.</span><span class="sxs-lookup"><span data-stu-id="015d0-113">Automatically sending receipts or purchase confirmations to customers.</span></span>
* <span data-ttu-id="015d0-114">Administração de listas de distribuição para envio mensal de panfletos eletrônicos e ofertas.</span><span class="sxs-lookup"><span data-stu-id="015d0-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="015d0-115">Coleta de métricas em tempo real para, por exemplo, email bloqueado e engajamento do cliente.</span><span class="sxs-lookup"><span data-stu-id="015d0-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="015d0-116">Encaminhamento de consultas dos clientes.</span><span class="sxs-lookup"><span data-stu-id="015d0-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="015d0-117">Processamento de emails de entrada.</span><span class="sxs-lookup"><span data-stu-id="015d0-117">Processing incoming emails.</span></span>

<span data-ttu-id="015d0-118">Para obter mais informações, visite [https://sendgrid.com](https://sendgrid.com) ou o repositório GitHub da [biblioteca C#][sendgrid-csharp] do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="015d0-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="015d0-119">Criar uma conta do SendGrid</span><span class="sxs-lookup"><span data-stu-id="015d0-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-net-class-library"></a><span data-ttu-id="015d0-120">Referência à biblioteca de classes do .NET do SendGrid</span><span class="sxs-lookup"><span data-stu-id="015d0-120">Reference the SendGrid .NET Class Library</span></span>
<span data-ttu-id="015d0-121">O [pacote NuGet do SendGrid](https://www.nuget.org/packages/Sendgrid) é a maneira mais fácil de obter a API do SendGrid e para configurar seu aplicativo com todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="015d0-121">The [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is the easiest way to get the SendGrid API and to configure your application with all dependencies.</span></span> <span data-ttu-id="015d0-122">O NuGet é uma extensão do Visual Studio incluída no Microsoft Visual Studio 2015 e nas versões posteriores que facilita a instalação e a atualização de bibliotecas e ferramentas.</span><span class="sxs-lookup"><span data-stu-id="015d0-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy to install and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="015d0-123">Para instalar o NuGet se você estiver executando uma versão do Visual Studio anterior ao Visual Studio 2015, visite [http://www.nuget.org](http://www.nuget.org)e clique no botão **Instalar NuGet** .</span><span class="sxs-lookup"><span data-stu-id="015d0-123">To install NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click the **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="015d0-124">Para instalar o pacote NuGet do SendGrid no seu aplicativo, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="015d0-124">To install the SendGrid NuGet package in your application, do the following:</span></span>

1. <span data-ttu-id="015d0-125">Clique em **Novo projeto** e selecione um **Modelo**.</span><span class="sxs-lookup"><span data-stu-id="015d0-125">Click on **New Project** and select a **Template**.</span></span>

   ![Criar um novo projeto][create-new-project]
2. <span data-ttu-id="015d0-127">No **Gerenciador de Soluções**, clique com botão direito em **Referências**, em seguida, clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="015d0-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![pacote NuGet do SendGrid][SendGrid-NuGet-package]
3. <span data-ttu-id="015d0-129">Procure **SendGrid** e selecione o item **SendGrid** na lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="015d0-129">Search for **SendGrid** and select the **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="015d0-130">Selecione a versão estável mais recente do pacote NuGet no menu suspenso da versão para poder trabalhar com o modelo de objeto e as APIs demonstradas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="015d0-130">Select the latest stable version of the Nuget package from the version dropdown to be able to work with the object model and APIs demonstrated in this article.</span></span>

   ![Pacote SendGrid][sendgrid-package]
5. <span data-ttu-id="015d0-132">Clique em **Instalar** para concluir a instalação e, em seguida, feche essa caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="015d0-132">Click **Install** to complete the installation, and then close this dialog.</span></span>

<span data-ttu-id="015d0-133">A biblioteca de classes do .NET do SendGrid se chama **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="015d0-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="015d0-134">Ela contém os seguintes namespaces:</span><span class="sxs-lookup"><span data-stu-id="015d0-134">It contains the following namespaces:</span></span>

* <span data-ttu-id="015d0-135">**SendGrid** para comunicação com a API do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="015d0-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="015d0-136">**SendGrid.Helpers.Mail** para que os métodos auxiliares criem facilmente objetos SendGridMessage, que especificam como enviar emails.</span><span class="sxs-lookup"><span data-stu-id="015d0-136">**SendGrid.Helpers.Mail** for helper methods to easily create SendGridMessage objects that specify how to send emails.</span></span>

<span data-ttu-id="015d0-137">Adicione as declarações de namespace de código a seguir à parte superior de qualquer arquivo C# em que queira acessar o serviço de email SendGrid de forma programática.</span><span class="sxs-lookup"><span data-stu-id="015d0-137">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access the SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="015d0-138">Como: criar um email</span><span class="sxs-lookup"><span data-stu-id="015d0-138">How to: Create an Email</span></span>
<span data-ttu-id="015d0-139">Use o objeto **SendGridMessage** para criar uma mensagem de email.</span><span class="sxs-lookup"><span data-stu-id="015d0-139">Use the **SendGridMessage** object to create an email message.</span></span> <span data-ttu-id="015d0-140">Quando o objeto de mensagem for criado, você poderá definir as propriedades e os métodos, incluindo o remetente do email, o destinatário do email e o assunto e o corpo do email.</span><span class="sxs-lookup"><span data-stu-id="015d0-140">Once the message object is created, you can set properties and methods, including the email sender, the email recipient, and the subject and body of the email.</span></span>

<span data-ttu-id="015d0-141">O exemplo a seguir demonstra como criar um objeto de email totalmente preenchido:</span><span class="sxs-lookup"><span data-stu-id="015d0-141">The following example demonstrates how to create a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing the SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="015d0-142">Para obter mais informações sobre todas as propriedades e métodos com suporte do tipo **SendGrid**, consulte [sendgrid-csharp][sendgrid-csharp] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="015d0-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="015d0-143">Como: enviar um email</span><span class="sxs-lookup"><span data-stu-id="015d0-143">How to: Send an Email</span></span>
<span data-ttu-id="015d0-144">Depois de criar uma mensagem de email, você poderá enviá-la usando a API do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="015d0-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="015d0-145">Como alternativa, você poderá usar a [biblioteca incorporada do .NET][NET-library].</span><span class="sxs-lookup"><span data-stu-id="015d0-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="015d0-146">O envio de email requer que você forneça sua chave de API do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="015d0-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="015d0-147">Se precisar de detalhes sobre como configurar as chaves de API, veja a [documentação][documentation] das Chaves de API do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="015d0-147">If you need details about how to configure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="015d0-148">Você pode armazenar essas credenciais por meio do Portal do Azure ao clicar nas configurações do Aplicativo e adicionar os pares chave/valor em "Configurações do aplicativo".</span><span class="sxs-lookup"><span data-stu-id="015d0-148">You may store these credentials via your Azure Portal by clicking Application settings and adding the key/value pairs under App settings.</span></span>

 ![Configurações do aplicativo do Azure][azure_app_settings]

 <span data-ttu-id="015d0-150">Em seguida, você pode acessá-las da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="015d0-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="015d0-151">Os exemplos a seguir mostram como enviar umamensagem usando a API da Web.</span><span class="sxs-lookup"><span data-stu-id="015d0-151">The following examples show how to send a message using the Web API.</span></span>

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
                    Subject = "Hello World from the SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="015d0-152">Como: adicionar um anexo</span><span class="sxs-lookup"><span data-stu-id="015d0-152">How to: Add an attachment</span></span>
<span data-ttu-id="015d0-153">É possível adicionar anexos a uma mensagem chamando o método **AddAttachment** e especificando minimamente o nome do arquivo e o conteúdo codificado Base64 que você deseja anexar.</span><span class="sxs-lookup"><span data-stu-id="015d0-153">Attachments can be added to a message by calling the **AddAttachment** method and minimally specifying the file name and Base64 encoded content you want to attach.</span></span> <span data-ttu-id="015d0-154">Você pode incluir vários anexos chamando esse método uma vez para cada arquivo que você quiser anexar ou usando o método **AddAttachments**.</span><span class="sxs-lookup"><span data-stu-id="015d0-154">You can include multiple attachments by calling this method once for each file you wish to attach or by using the **AddAttachments** method.</span></span> <span data-ttu-id="015d0-155">O exemplo a seguir demonstra como adicionar um anexo a uma mensagem:</span><span class="sxs-lookup"><span data-stu-id="015d0-155">The following example demonstrates adding an attachment to a message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="015d0-156">Como: usar configurações de email para habilitar rodapés, acompanhamento e análise</span><span class="sxs-lookup"><span data-stu-id="015d0-156">How to: Use mail settings to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="015d0-157">O SendGrid fornece a funcionalidade adicional de email por meio do uso das configurações de email e de acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="015d0-157">SendGrid provides additional email functionality through the use of mail settings and tracking settings.</span></span> <span data-ttu-id="015d0-158">Essas configurações podem ser adicionadas a uma mensagem de email para habilitar uma funcionalidade específica, como o Acompanhamento de Cliques, Google Analytics, Acompanhamento de Assinatura e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="015d0-158">These settings can be added to an email message to enable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="015d0-159">Para obter uma lista completa de aplicativos, consulte a [Documentação de Configurações][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="015d0-159">For a full list of apps, see the [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="015d0-160">Os aplicativos podem ser aplicados nas mensagens de email do **SendGrid** usando os métodos implementados como parte da classe **SendGridMessage**.</span><span class="sxs-lookup"><span data-stu-id="015d0-160">Apps can be applied to **SendGrid** email messages using methods implemented as part of the **SendGridMessage** class.</span></span> <span data-ttu-id="015d0-161">Os exemplos a seguir demonstram os filtros de rodapé e de acompanhamento de cliques:</span><span class="sxs-lookup"><span data-stu-id="015d0-161">The following examples demonstrate the footer and click tracking filters:</span></span>

<span data-ttu-id="015d0-162">Os exemplos a seguir demonstram os filtros de rodapé e de acompanhamento de cliques:</span><span class="sxs-lookup"><span data-stu-id="015d0-162">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="015d0-163">Configurações de rodapé</span><span class="sxs-lookup"><span data-stu-id="015d0-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="015d0-164">Rastreamento de cliques</span><span class="sxs-lookup"><span data-stu-id="015d0-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="015d0-165">Como: usar serviços adicionais do SendGrid</span><span class="sxs-lookup"><span data-stu-id="015d0-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="015d0-166">O SendGrid oferece várias APIs e webhooks que você pode usar para aproveitar a funcionalidade adicional em seu aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="015d0-166">SendGrid offers several APIs and webhooks that you can use to leverage additional functionality within your Azure application.</span></span> <span data-ttu-id="015d0-167">Para obter mais detalhes, consulte a [Referência de API do SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="015d0-167">For more details, see the [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="015d0-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="015d0-168">Next steps</span></span>
<span data-ttu-id="015d0-169">Agora que você já conhece as noções básicas do serviço de email SendGrid, siga estes links para saber mais.</span><span class="sxs-lookup"><span data-stu-id="015d0-169">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="015d0-170">Repositório da biblioteca C\# do SendGrid: [sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="015d0-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="015d0-171">Documentação da API do SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="015d0-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is the SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference the SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters to Enable Footers, Tracking, and Analytics]: #usefilters
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

<span data-ttu-id="015d0-172">[serviço de email baseado em nuvem]: https://sendgrid.com/solutions</span><span class="sxs-lookup"><span data-stu-id="015d0-172">[cloud-based email service]: https://sendgrid.com/solutions</span></span>
<span data-ttu-id="015d0-173">[entrega de email transacional]: https://sendgrid.com/use-cases/transactional-email</span><span class="sxs-lookup"><span data-stu-id="015d0-173">[transactional email delivery]: https://sendgrid.com/use-cases/transactional-email</span></span>

