---
title: "notificações de aaaConfigure e email modelos no gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como tooconfigure notificações e email modelos no gerenciamento de API do Azure."
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
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="e815d-103">Como notificações tooconfigure e email modelos no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="e815d-103">How tooconfigure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="e815d-104">Gerenciamento de API permite Olá tooconfigure notificações sobre eventos específicos e modelos de email de saudação tooconfigure que são usada toocommunicate com administradores hello e desenvolvedores de uma instância de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="e815d-104">API Management provides hello ability tooconfigure notifications for specific events, and tooconfigure hello email templates that are used toocommunicate with hello administrators and developers of an API Management instance.</span></span> <span data-ttu-id="e815d-105">Este tópico mostra como as notificações tooconfigure Olá eventos disponíveis e fornece uma visão geral de como configurar modelos de email de saudação usados para esses eventos.</span><span class="sxs-lookup"><span data-stu-id="e815d-105">This topic shows how tooconfigure notifications for hello available events, and provides an overview of configuring hello email templates used for these events.</span></span>

## <span data-ttu-id="e815d-106"><a name="publisher-notifications"> </a>Configurar notificações do editor</span><span class="sxs-lookup"><span data-stu-id="e815d-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="e815d-107">notificações de tooconfigure, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="e815d-107">tooconfigure notifications, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="e815d-108">Isso leva toohello portal do publicador de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="e815d-108">This takes you toohello API Management publisher portal.</span></span>

![Portal do editor][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="e815d-110">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="e815d-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="e815d-111">Clique em **notificações** de saudação **gerenciamento de API** menu Olá deixado tooview notificações disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="e815d-111">Click **Notifications** from hello **API Management** menu on hello left tooview hello available notifications.</span></span>

![Notificações do editor][api-management-publisher-notifications]

<span data-ttu-id="e815d-113">Olá lista de eventos a seguir pode ser configurada para notificações.</span><span class="sxs-lookup"><span data-stu-id="e815d-113">hello following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="e815d-114">**Solicitações de assinatura (que exige aprovação)** - Olá destinatários de email especificado e os usuários receberão notificações por email sobre solicitações de assinatura para exigir a aprovação de produtos de API.</span><span class="sxs-lookup"><span data-stu-id="e815d-114">**Subscription requests (requiring approval)** - hello specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="e815d-115">**Novas assinaturas** - Olá destinatários de email especificado e os usuários receberão notificações por email sobre novas assinaturas de produto de API.</span><span class="sxs-lookup"><span data-stu-id="e815d-115">**New subscriptions** - hello specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="e815d-116">**Solicitações de galeria de aplicativos** - Olá destinatários de email especificado e os usuários receberão notificações por email quando novos aplicativos forem enviados toohello Galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e815d-116">**Application gallery requests** - hello specified email recipients and users will receive email notifications when new applications are submitted toohello application gallery.</span></span>
* <span data-ttu-id="e815d-117">**Cco** - Olá destinatários de email especificado e os usuários receberão o email com cópia oculta do toodevelopers de todos os emails enviados.</span><span class="sxs-lookup"><span data-stu-id="e815d-117">**BCC** - hello specified email recipients and users will receive email blind carbon copies of all emails sent toodevelopers.</span></span>
* <span data-ttu-id="e815d-118">**Novo problema ou comentário** - Olá destinatários de email especificado e os usuários receberão notificações por email quando um novo problema ou comentário é enviado no portal do desenvolvedor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e815d-118">**New issue or comment** - hello specified email recipients and users will receive email notifications when a new issue or comment is submitted on hello developer portal.</span></span>
* <span data-ttu-id="e815d-119">**Mensagem de fechar conta** - Olá destinatários de email especificado e os usuários receberão notificações por email quando uma conta é fechada.</span><span class="sxs-lookup"><span data-stu-id="e815d-119">**Close account message** - hello specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="e815d-120">**Próximo limite de cota de assinatura** - Olá destinatários de email a seguir e os usuários receberão notificações por email quando o uso de assinatura obtém toousage fechar cota.</span><span class="sxs-lookup"><span data-stu-id="e815d-120">**Approaching subscription quota limit** - hello following email recipients and users will receive email notifications when subscription usage gets close toousage quota.</span></span>

<span data-ttu-id="e815d-121">Para cada evento, você pode especificar os destinatários de email usando a caixa de texto de endereço de email de saudação ou você pode selecionar os usuários de uma lista.</span><span class="sxs-lookup"><span data-stu-id="e815d-121">For each event, you can specify email recipients using hello email address text box or you can select users from a list.</span></span>

<span data-ttu-id="e815d-122">endereços de email do toospecify Olá toobe notificado, digite-os na caixa de texto de endereço de email de saudação.</span><span class="sxs-lookup"><span data-stu-id="e815d-122">toospecify hello email addresses toobe notified, enter them in hello email address text box.</span></span> <span data-ttu-id="e815d-123">Se tiver diversos endereços de email, separe-os por vírgula.</span><span class="sxs-lookup"><span data-stu-id="e815d-123">If you have multiple email addresses, separate them using commas.</span></span>

![Destinatários da notificação][api-management-email-addresses]

<span data-ttu-id="e815d-125">toospecify Olá usuários toobe notificado, clique em **Adicionar destinatário**, Olá caixa ao lado de saudação usuários toobe notificado de seleção e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="e815d-125">toospecify hello users toobe notified, click **add recipient**, check hello box beside hello users toobe notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="e815d-126">Somente os administradores são exibidos na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="e815d-126">Only administrators are displayed in hello list.</span></span>


<span data-ttu-id="e815d-127">Depois de configurar os destinatários de notificações de saudação, clique em **salvar** tooapply Olá atualizado destinatários de notificação.</span><span class="sxs-lookup"><span data-stu-id="e815d-127">After configuring hello notification recipients, click **Save** tooapply hello updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="e815d-128">Se você sair Olá **publicador notificações** portal do publicador Olá guia alerta se há alterações não salvas.</span><span class="sxs-lookup"><span data-stu-id="e815d-128">If you navigate away from hello **Publisher Notifications** tab hello publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="e815d-129"><a name="email-templates"> </a>Configurar modelos de email</span><span class="sxs-lookup"><span data-stu-id="e815d-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="e815d-130">Gerenciamento de API fornece modelos de email para Olá mensagens de email que são enviadas em curso de saudação de administrar e usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="e815d-130">API Management provides email templates for hello email messages that are sent in hello course of administering and using hello service.</span></span> <span data-ttu-id="e815d-131">Olá, modelos de email a seguir é fornecido.</span><span class="sxs-lookup"><span data-stu-id="e815d-131">hello following email templates are provided.</span></span>

* <span data-ttu-id="e815d-132">Envio à galeria de aplicativos aprovado</span><span class="sxs-lookup"><span data-stu-id="e815d-132">Application gallery submission approved</span></span>
* <span data-ttu-id="e815d-133">Carta de despedida do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="e815d-133">Developer farewell letter</span></span>
* <span data-ttu-id="e815d-134">Notificação de limite de cota se aproximando</span><span class="sxs-lookup"><span data-stu-id="e815d-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="e815d-135">Convidar usuário</span><span class="sxs-lookup"><span data-stu-id="e815d-135">Invite user</span></span>
* <span data-ttu-id="e815d-136">Novo comentário adicionado tooan problema</span><span class="sxs-lookup"><span data-stu-id="e815d-136">New comment added tooan issue</span></span>
* <span data-ttu-id="e815d-137">Novo problema recebido</span><span class="sxs-lookup"><span data-stu-id="e815d-137">New issue received</span></span>
* <span data-ttu-id="e815d-138">Nova assinatura ativada</span><span class="sxs-lookup"><span data-stu-id="e815d-138">New subscription activated</span></span>
* <span data-ttu-id="e815d-139">Confirmação de renovação de assinatura</span><span class="sxs-lookup"><span data-stu-id="e815d-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="e815d-140">Solicitação de assinatura negada</span><span class="sxs-lookup"><span data-stu-id="e815d-140">Subscription request declines</span></span>
* <span data-ttu-id="e815d-141">Solicitação de assinatura recebida</span><span class="sxs-lookup"><span data-stu-id="e815d-141">Subscription request received</span></span>

<span data-ttu-id="e815d-142">Esses modelos podem ser modificados da forma desejada.</span><span class="sxs-lookup"><span data-stu-id="e815d-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="e815d-143">tooview e configurar modelos de email de saudação para sua instância de gerenciamento de API, clique em **notificações** de saudação **gerenciamento de API** menu saudação à esquerda e selecione Olá **modelos de Email**  guia.</span><span class="sxs-lookup"><span data-stu-id="e815d-143">tooview and configure hello email templates for your API Management instance, click **Notifications** from hello **API Management** menu on hello left, and select hello **Email Templates** tab.</span></span>

![Modelos de email][api-management-email-templates]

<span data-ttu-id="e815d-145">tooview ou modificar um modelo específico, selecione-o da saudação **modelos** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="e815d-145">tooview or modify a specific template, select it from hello **Templates** drop-down list.</span></span>

![Lista de modelos de email][api-management-email-templates-list]

<span data-ttu-id="e815d-147">Cada modelo de email tem um assunto em texto sem formatação e uma definição de corpo em formato HTML.</span><span class="sxs-lookup"><span data-stu-id="e815d-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="e815d-148">Cada item pode ser personalizado da forma desejada.</span><span class="sxs-lookup"><span data-stu-id="e815d-148">Each item can be customized as desired.</span></span>

![Editor de modelos de email][api-management-email-template]

<span data-ttu-id="e815d-150">Olá **parâmetros** lista contém uma lista de parâmetros, que, quando inserido em Olá assunto ou corpo, será o valor substituído Olá designado quando Olá email é enviado.</span><span class="sxs-lookup"><span data-stu-id="e815d-150">hello **Parameters** list contains a list of parameters, which when inserted into hello subject or body, will be replaced hello designated value when hello email is sent.</span></span> <span data-ttu-id="e815d-151">tooinsert um parâmetro, coloque o cursor de saudação em que você deseja Olá parâmetro toogo e clique em Olá seta toohello esquerda do nome de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="e815d-151">tooinsert a parameter, place hello cursor where you wish hello parameter toogo, and click hello arrow toohello left of hello parameter name.</span></span>

<span data-ttu-id="e815d-152">Clique em **visualização** ou **enviar um teste** toosee como email hello serão pesquisar ou enviar um email de teste.</span><span class="sxs-lookup"><span data-stu-id="e815d-152">Click **Preview** or **Send a test** toosee how hello email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="e815d-153">parâmetros de saudação não são substituídos por valores reais quando visualizar ou enviar um teste.</span><span class="sxs-lookup"><span data-stu-id="e815d-153">hello parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="e815d-154">modelo de email do toohello toosave Olá alterações, clique em **salvar**, ou clique em alterações de saudação toocancel **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="e815d-154">toosave hello changes toohello email template, click **Save**, or toocancel hello changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
