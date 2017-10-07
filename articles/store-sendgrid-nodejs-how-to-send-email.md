---
title: "saudação de toouse aaaHow SendGrid serviço de email (Node. js) | Microsoft Docs"
description: "Saiba como enviar email com hello SendGrid serviço de email no Azure. Exemplos escritos usando Olá Node. js API de código."
services: 
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: 
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: fd617b6aaa656e7b5dd51c51ebb0db1e848450f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="3e773-104">Como tooSend Email usando o SendGrid do Node. js</span><span class="sxs-lookup"><span data-stu-id="3e773-104">How tooSend Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="3e773-105">Este guia demonstra como tooperform as tarefas de programação comuns com o SendGrid email serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="3e773-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="3e773-106">exemplos de saudação são gravados usando Olá API Node. js.</span><span class="sxs-lookup"><span data-stu-id="3e773-106">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="3e773-107">Olá cenários abordados incluem **construindo email**, **enviar email**, **adicionar anexos**, **usando filtros**e **Atualizando propriedades**.</span><span class="sxs-lookup"><span data-stu-id="3e773-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="3e773-108">Para obter mais informações sobre SendGrid e enviar email, consulte Olá [próximas etapas](#next-steps) seção.</span><span class="sxs-lookup"><span data-stu-id="3e773-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="3e773-109">O que é Olá SendGrid serviço de Email?</span><span class="sxs-lookup"><span data-stu-id="3e773-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="3e773-110">SendGrid é um [serviço de email baseado em nuvem] que fornece uma [entrega de email transacional], escalabilidade e análise em tempo real confiáveis com APIs flexíveis que facilitam a integração personalizada.</span><span class="sxs-lookup"><span data-stu-id="3e773-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="3e773-111">Os cenários comuns de uso do SendGrid incluem:</span><span class="sxs-lookup"><span data-stu-id="3e773-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="3e773-112">Enviar automaticamente confirmações toocustomers</span><span class="sxs-lookup"><span data-stu-id="3e773-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="3e773-113">Administração de listas de distribuição para enviar aos clientes mensalmente panfletos eletrônicos e ofertas especiais</span><span class="sxs-lookup"><span data-stu-id="3e773-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="3e773-114">Coleta de métrica em tempo real para, por exemplo, email bloqueado e capacidade de resposta do cliente</span><span class="sxs-lookup"><span data-stu-id="3e773-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="3e773-115">Gerando relatórios toohelp identificar tendências</span><span class="sxs-lookup"><span data-stu-id="3e773-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="3e773-116">Encaminhamento de consultas dos clientes</span><span class="sxs-lookup"><span data-stu-id="3e773-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="3e773-117">Notificações de email de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="3e773-117">Email notifications from your application</span></span>

<span data-ttu-id="3e773-118">Para obter mais informações, consulte [https://sendgrid.com](https://sendgrid.com).</span><span class="sxs-lookup"><span data-stu-id="3e773-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="3e773-119">Criar uma conta do SendGrid</span><span class="sxs-lookup"><span data-stu-id="3e773-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a><span data-ttu-id="3e773-120">Saudação de referência módulo de Node.js do SendGrid</span><span class="sxs-lookup"><span data-stu-id="3e773-120">Reference hello SendGrid Node.js Module</span></span>
<span data-ttu-id="3e773-121">módulo do SendGrid Olá para Node. js pode ser instalado por meio do Gerenciador de pacotes de nó de saudação (npm) usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="3e773-121">hello SendGrid module for Node.js can be installed through hello node package manager (npm) by using hello following command:</span></span>

    npm install sendgrid

<span data-ttu-id="3e773-122">Após a instalação, você pode exigir o módulo Olá em seu aplicativo usando Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e773-122">After installation, you can require hello module in your application by using hello following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="3e773-123">módulo do SendGrid Olá exporta Olá **SendGrid** e **Email** funções.</span><span class="sxs-lookup"><span data-stu-id="3e773-123">hello SendGrid module exports hello **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="3e773-124">**SendGrid** é responsável por enviar email por meio da API da Web, enquanto **Email** encapsula uma mensagem de email.</span><span class="sxs-lookup"><span data-stu-id="3e773-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="3e773-125">Como: criar um email</span><span class="sxs-lookup"><span data-stu-id="3e773-125">How to: Create an Email</span></span>
<span data-ttu-id="3e773-126">Criando uma mensagem de email usando o módulo de SendGrid Olá envolve criar primeiro uma mensagem de email usando a função de Email hello e, em seguida, enviá-lo usando a função do SendGrid hello.</span><span class="sxs-lookup"><span data-stu-id="3e773-126">Creating an email message using hello SendGrid module involves first creating an email message using hello Email function, and then sending it using hello SendGrid function.</span></span> <span data-ttu-id="3e773-127">a seguir Olá é um exemplo de como criar uma nova mensagem usando a função de Email hello:</span><span class="sxs-lookup"><span data-stu-id="3e773-127">hello following is an example of creating a new message using hello Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="3e773-128">Você também pode especificar uma mensagem de HTML para clientes que dão suporte a ele definindo a propriedade de html hello.</span><span class="sxs-lookup"><span data-stu-id="3e773-128">You can also specify an HTML message for clients that support it by setting hello html property.</span></span> <span data-ttu-id="3e773-129">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3e773-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="3e773-130">Definir as propriedades de texto e html Olá fornece normal fallback para conteúdo de texto para clientes que não oferece suporte a mensagens em HTML.</span><span class="sxs-lookup"><span data-stu-id="3e773-130">Setting both hello text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="3e773-131">Para obter mais informações sobre todas as propriedades com suporte pelo Olá função Email, consulte [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="3e773-131">For more information on all properties supported by hello Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="3e773-132">Como: enviar um email</span><span class="sxs-lookup"><span data-stu-id="3e773-132">How to: Send an Email</span></span>
<span data-ttu-id="3e773-133">Depois de criar uma mensagem de email usando Olá função de Email, você pode enviar usando Olá Web API fornecida pelo SendGrid.</span><span class="sxs-lookup"><span data-stu-id="3e773-133">After creating an email message using hello Email function, you can send it using hello Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="3e773-134">API Web</span><span class="sxs-lookup"><span data-stu-id="3e773-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="3e773-135">Enquanto Olá acima exemplos mostram passagem em uma função de retorno de chamada e de objeto de email, você também diretamente pode chamar a função de envio de saudação especificando diretamente as propriedades de email.</span><span class="sxs-lookup"><span data-stu-id="3e773-135">While hello above examples show passing in an email object and callback function, you can also directly invoke hello send function by directly specifying email properties.</span></span> <span data-ttu-id="3e773-136">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3e773-136">For example:</span></span>  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="3e773-137">Como: adicionar um anexo</span><span class="sxs-lookup"><span data-stu-id="3e773-137">How to: Add an Attachment</span></span>
<span data-ttu-id="3e773-138">Anexos podem ser adicionados a mensagem tooa, especificando nomes de arquivo hello e caminhos Olá **arquivos** propriedade.</span><span class="sxs-lookup"><span data-stu-id="3e773-138">Attachments can be added tooa message by specifying hello file name(s) and path(s) in hello **files** property.</span></span> <span data-ttu-id="3e773-139">saudação de exemplo a seguir demonstra enviando um anexo:</span><span class="sxs-lookup"><span data-stu-id="3e773-139">hello following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used toospecify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="3e773-140">Ao usar o hello **arquivos** propriedade, o arquivo hello deve ser acessível por meio de [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span><span class="sxs-lookup"><span data-stu-id="3e773-140">When using hello **files** property, hello file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="3e773-141">Se o arquivo hello desejar tooattach estiver hospedado no armazenamento do Azure, como em um contêiner de Blob, é necessário primeiro copiar armazenamento de toolocal arquivo hello ou tooan unidade do Azure antes de ser enviado como um anexo usando Olá **arquivos** propriedade.</span><span class="sxs-lookup"><span data-stu-id="3e773-141">If hello file you wish tooattach is hosted in Azure Storage, such as in a Blob container, you must first copy hello file toolocal storage or tooan Azure drive before it can be sent as an attachment using hello **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a><span data-ttu-id="3e773-142">Como: usar filtros tooEnable rodapés e controle</span><span class="sxs-lookup"><span data-stu-id="3e773-142">How to: Use Filters tooEnable Footers and Tracking</span></span>
<span data-ttu-id="3e773-143">SendGrid fornece a funcionalidade de email adicionais por meio do uso de saudação de filtros.</span><span class="sxs-lookup"><span data-stu-id="3e773-143">SendGrid provides additional email functionality through hello use of filters.</span></span> <span data-ttu-id="3e773-144">Essas são as configurações que podem ser adicionadas tooan a mensagem de email para habilitar a funcionalidade específica, como habilitar o controle de clique, do Google analytics, assinatura de controle, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="3e773-144">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="3e773-145">Para obter uma lista completa de filtros, consulte [Configurações de filtro][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="3e773-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="3e773-146">Os filtros podem ser aplicadas tooa mensagem usando Olá **filtros** propriedade.</span><span class="sxs-lookup"><span data-stu-id="3e773-146">Filters can be applied tooa message by using hello **filters** property.</span></span>
<span data-ttu-id="3e773-147">Cada filtro é especificado por um hash que possui configurações específicas de filtro.</span><span class="sxs-lookup"><span data-stu-id="3e773-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="3e773-148">Olá exemplos a seguir demonstram o rodapé hello e clique em filtros de rastreamento:</span><span class="sxs-lookup"><span data-stu-id="3e773-148">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="3e773-149">Rodapé</span><span class="sxs-lookup"><span data-stu-id="3e773-149">Footer</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a><span data-ttu-id="3e773-150">Acompanhamento de cliques</span><span class="sxs-lookup"><span data-stu-id="3e773-150">Click Tracking</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a><span data-ttu-id="3e773-151">Como atualizar as propriedades do e-mail</span><span class="sxs-lookup"><span data-stu-id="3e773-151">How to: Update Email Properties</span></span>
<span data-ttu-id="3e773-152">Algumas propriedades de email podem ser substituídas usando  **definir*propriedade** * ou ser acrescentados usando  **adicionar*propriedade** *.</span><span class="sxs-lookup"><span data-stu-id="3e773-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="3e773-153">Por exemplo, você pode adicionar destinatários adicionais ao usar</span><span class="sxs-lookup"><span data-stu-id="3e773-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="3e773-154">ou definir um filtro usando</span><span class="sxs-lookup"><span data-stu-id="3e773-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="3e773-155">Para obter mais informações, consulte [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="3e773-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="3e773-156">Como: usar serviços adicionais do SendGrid</span><span class="sxs-lookup"><span data-stu-id="3e773-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="3e773-157">SendGrid oferece APIs baseado na web que você pode usar uma funcionalidade adicional tooleverage SendGrid de seu aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e773-157">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="3e773-158">Para obter detalhes completos, consulte Olá [documentação da API do SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="3e773-158">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e773-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3e773-159">Next Steps</span></span>
<span data-ttu-id="3e773-160">Agora que você aprendeu as Noções básicas sobre Olá Olá serviço de Email do SendGrid, siga essas toolearn links mais.</span><span class="sxs-lookup"><span data-stu-id="3e773-160">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="3e773-161">Repositório de módulo de Node.js do SendGrid: [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="3e773-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="3e773-162">Documentação da API do SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="3e773-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="3e773-163">Oferta especial de SendGrid para clientes Azure: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="3e773-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[serviço de email baseado em nuvem]: https://sendgrid.com/email-solutions
[entrega de email transacional]: https://sendgrid.com/transactional-email
