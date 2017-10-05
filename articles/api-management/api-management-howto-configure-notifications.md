---
title: "Configurar notificações e modelos de email no Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como configurar notificações e modelos de email no Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 3d8b74e32059cfc1a4c3a8fc7d3bd04676ee80c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="9ee0f-103">Como configurar notificações e modelos de email no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="9ee0f-103">How to configure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="9ee0f-104">O Gerenciamento de API possibilita configurar notificações de eventos específicos e modelos dos emails que são usados para se comunicar com os administradores e desenvolvedores de uma instância do Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span></span> <span data-ttu-id="9ee0f-105">Este tópico mostra como configurar notificações de eventos disponíveis e fornece uma visão geral da configuração dos modelos dos emails usados desses eventos.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-105">This topic shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span></span>

## <span data-ttu-id="9ee0f-106"><a name="publisher-notifications"> </a>Configurar notificações do editor</span><span class="sxs-lookup"><span data-stu-id="9ee0f-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="9ee0f-107">Para configurar notificações, clique no **portal do Editor** no Portal do Azure para seu serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-107">To configure notifications, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="9ee0f-108">Isso levará você ao portal do editor de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-108">This takes you to the API Management publisher portal.</span></span>

![Portal do editor][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="9ee0f-110">Se ainda não criou uma instância de serviço de Gerenciamento de API, confira [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9ee0f-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="9ee0f-111">Clique em **Notificações** no menu **Gerenciamento de API** à esquerda para ver as notificações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-111">Click **Notifications** from the **API Management** menu on the left to view the available notifications.</span></span>

![Notificações do editor][api-management-publisher-notifications]

<span data-ttu-id="9ee0f-113">Os eventos na lista a seguir podem ser configurados para enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-113">The following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="9ee0f-114">**Solicitações de assinatura (que precisam de aprovação)** - Os usuários e destinatários de email especificados receberão notificações por email sobre solicitações de assinaturas de produtos de API que precisarem de aprovação.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-114">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="9ee0f-115">**Novas assinaturas** - Os usuários e destinatários de email especificados receberão notificações por email sobre novas assinaturas de produtos de API.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-115">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="9ee0f-116">**Solicitações da galeria de aplicativos** - Os usuários e destinatários de email especificados receberão notificações por email quando novos aplicativos forem enviados à galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-116">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span></span>
* <span data-ttu-id="9ee0f-117">**CCO** - Os usuários e destinatários de email especificados receberão cópias ocultas de todos os emails enviados a desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-117">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span></span>
* <span data-ttu-id="9ee0f-118">**Novo problema ou comentário** - Os usuários e destinatários de email especificados receberão notificações por email quando um novo problema ou comentário for enviado no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-118">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span></span>
* <span data-ttu-id="9ee0f-119">**Mensagem de conta encerrada** - Os usuários e destinatários de email especificados receberão notificações por email quando uma conta for encerrada.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-119">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="9ee0f-120">**Limite de cota de assinatura se aproximando** - Os usuários e destinatários de email a seguir receberão notificações por email quando o uso de assinaturas estiver se aproximando da cota.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-120">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span></span>

<span data-ttu-id="9ee0f-121">Para cada evento, você pode especificar destinatários de email usando a caixa de texto de endereço de email ou selecionando os usuários em uma lista.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-121">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span></span>

<span data-ttu-id="9ee0f-122">Para especificar os endereços de email a serem notificados, insira-os na caixa de texto de endereço de email.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-122">To specify the email addresses to be notified, enter them in the email address text box.</span></span> <span data-ttu-id="9ee0f-123">Se tiver diversos endereços de email, separe-os por vírgula.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-123">If you have multiple email addresses, separate them using commas.</span></span>

![Destinatários da notificação][api-management-email-addresses]

<span data-ttu-id="9ee0f-125">Para especificar os usuários a serem notificados, clique em **adicionar destinatário**, marque as caixas de seleção ao lado dos usuários a serem notificados e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-125">To specify the users to be notified, click **add recipient**, check the box beside the users to be notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="9ee0f-126">Somente os administradores são exibidos na lista.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-126">Only administrators are displayed in the list.</span></span>


<span data-ttu-id="9ee0f-127">Após configurar os destinatários da notificação, clique em **Salvar** para aplicar a atualização dos destinatários da notificação.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-127">After configuring the notification recipients, click **Save** to apply the updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="9ee0f-128">Se você navegar para fora da guia **Notificações do editor** , o Portal do editor o alertará se houver alterações não salvas.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-128">If you navigate away from the **Publisher Notifications** tab the publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="9ee0f-129"><a name="email-templates"> </a>Configurar modelos de email</span><span class="sxs-lookup"><span data-stu-id="9ee0f-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="9ee0f-130">O Gerenciamento de API fornece modelos de email para mensagens de email que são enviadas no decorrer da administração e da utilização do serviço.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-130">API Management provides email templates for the email messages that are sent in the course of administering and using the service.</span></span> <span data-ttu-id="9ee0f-131">Os seguintes modelos de email são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-131">The following email templates are provided.</span></span>

* <span data-ttu-id="9ee0f-132">Envio à galeria de aplicativos aprovado</span><span class="sxs-lookup"><span data-stu-id="9ee0f-132">Application gallery submission approved</span></span>
* <span data-ttu-id="9ee0f-133">Carta de despedida do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="9ee0f-133">Developer farewell letter</span></span>
* <span data-ttu-id="9ee0f-134">Notificação de limite de cota se aproximando</span><span class="sxs-lookup"><span data-stu-id="9ee0f-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="9ee0f-135">Convidar usuário</span><span class="sxs-lookup"><span data-stu-id="9ee0f-135">Invite user</span></span>
* <span data-ttu-id="9ee0f-136">Novo comentário adicionado a um problema</span><span class="sxs-lookup"><span data-stu-id="9ee0f-136">New comment added to an issue</span></span>
* <span data-ttu-id="9ee0f-137">Novo problema recebido</span><span class="sxs-lookup"><span data-stu-id="9ee0f-137">New issue received</span></span>
* <span data-ttu-id="9ee0f-138">Nova assinatura ativada</span><span class="sxs-lookup"><span data-stu-id="9ee0f-138">New subscription activated</span></span>
* <span data-ttu-id="9ee0f-139">Confirmação de renovação de assinatura</span><span class="sxs-lookup"><span data-stu-id="9ee0f-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="9ee0f-140">Solicitação de assinatura negada</span><span class="sxs-lookup"><span data-stu-id="9ee0f-140">Subscription request declines</span></span>
* <span data-ttu-id="9ee0f-141">Solicitação de assinatura recebida</span><span class="sxs-lookup"><span data-stu-id="9ee0f-141">Subscription request received</span></span>

<span data-ttu-id="9ee0f-142">Esses modelos podem ser modificados da forma desejada.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="9ee0f-143">Para ver e configurar os modelos de email para sua instância do Gerenciamento de API, clique em **Notificações** no menu **Gerenciamento de API** à esquerda e selecione a guia **Modelos de email**.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-143">To view and configure the email templates for your API Management instance, click **Notifications** from the **API Management** menu on the left, and select the **Email Templates** tab.</span></span>

![Modelos de email][api-management-email-templates]

<span data-ttu-id="9ee0f-145">Para ver ou modificar um modelo específico, selecione-o na lista suspensa **Modelos** .</span><span class="sxs-lookup"><span data-stu-id="9ee0f-145">To view or modify a specific template, select it from the **Templates** drop-down list.</span></span>

![Lista de modelos de email][api-management-email-templates-list]

<span data-ttu-id="9ee0f-147">Cada modelo de email tem um assunto em texto sem formatação e uma definição de corpo em formato HTML.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="9ee0f-148">Cada item pode ser personalizado da forma desejada.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-148">Each item can be customized as desired.</span></span>

![Editor de modelos de email][api-management-email-template]

<span data-ttu-id="9ee0f-150">A lista **Parâmetros** contém parâmetros que, quando inseridos no assunto ou corpo, serão substituídos pelo valor designado quando o email for enviado.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-150">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span></span> <span data-ttu-id="9ee0f-151">Para inserir um parâmetro, posicione o cursor onde quiser que ele seja colocado e clique na seta à esquerda do nome do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-151">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span></span>

<span data-ttu-id="9ee0f-152">Clique em **Visualização** ou **Enviar um teste** para ver como o email ficará ou enviar um email de teste.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-152">Click **Preview** or **Send a test** to see how the email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="9ee0f-153">Os parâmetros não são substituídos por valores reais ao visualizar ou enviar um teste.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-153">The parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="9ee0f-154">Para salvar as alterações feitas no modelo de email, clique em **Salvar** ou, para cancelar as alterações, clique em **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="9ee0f-154">To save the changes to the email template, click **Save**, or to cancel the changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
