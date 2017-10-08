---
title: "aaaHow gerenciar contas de usuário no gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como toocreate ou convidar usuários no gerenciamento de API do Azure"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a><span data-ttu-id="2d446-103">Como contas de usuário toomanage no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="2d446-103">How toomanage user accounts in Azure API Management</span></span>
<span data-ttu-id="2d446-104">No gerenciamento de API, os desenvolvedores são usuários Olá Olá APIs que você expõe usando gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="2d446-104">In API Management, developers are hello users of hello APIs that you expose using API Management.</span></span> <span data-ttu-id="2d446-105">Este guia mostra toohow toocreate e convidar os desenvolvedores toouse hello APIs e produtos que você faça toothem disponível com sua instância de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="2d446-105">This guide shows toohow toocreate and invite developers toouse hello APIs and products that you make available toothem with your API Management instance.</span></span> <span data-ttu-id="2d446-106">Para obter informações sobre como gerenciar contas de usuário por meio de programação, consulte Olá [entidade usuário](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentação Olá [API REST de gerenciamento](https://msdn.microsoft.com/library/azure/dn776326.aspx) referência.</span><span class="sxs-lookup"><span data-stu-id="2d446-106">For information on managing user accounts programmatically, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="2d446-107"><a name="create-developer"> </a>Criar um novo desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="2d446-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="2d446-108">toocreate um desenvolvedor de novo, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="2d446-108">toocreate a new developer, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="2d446-109">Isso leva toohello portal do publicador de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="2d446-109">This takes you toohello API Management publisher portal.</span></span> <span data-ttu-id="2d446-110">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="2d446-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal do editor][api-management-management-console]

<span data-ttu-id="2d446-112">Clique em **usuários** de saudação **gerenciamento de API** menu saudação à esquerda e clique **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="2d446-112">Click **Users** from hello **API Management** menu on hello left, and then click **add user**.</span></span>

![Criar desenvolvedor][api-management-create-developer]

<span data-ttu-id="2d446-114">Digite hello **Email**, **senha**, e **nome** para desenvolvedor novo hello e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="2d446-114">Enter hello **Email**, **Password**, and **Name** for hello new developer and click **Save**.</span></span>

![Criar desenvolvedor][api-management-add-new-user]

<span data-ttu-id="2d446-116">Por padrão, são contas de desenvolvedor recém-criado **Active**e associado Olá **desenvolvedores** grupo.</span><span class="sxs-lookup"><span data-stu-id="2d446-116">By default, newly created developer accounts are **Active**, and associated with hello **Developers** group.</span></span>

![Novo desenvolvedor][api-management-new-developer]

<span data-ttu-id="2d446-118">Contas de desenvolvedor que estão em um **active** estado pode ser usado tooaccess todos os APIs Olá para os quais têm assinaturas.</span><span class="sxs-lookup"><span data-stu-id="2d446-118">Developer accounts that are in an **active** state can be used tooaccess all of hello APIs for which they have subscriptions.</span></span> <span data-ttu-id="2d446-119">desenvolvedor de saudação recém-criado tooassociate grupos adicionais, consulte [como os grupos de tooassociate com os desenvolvedores][How tooassociate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="2d446-119">tooassociate hello newly created developer with additional groups, see [How tooassociate groups with developers][How tooassociate groups with developers].</span></span>

## <span data-ttu-id="2d446-120"><a name="invite-developer"> </a>Convidar um desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="2d446-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="2d446-121">tooinvite um desenvolvedor, clique em **usuários** de saudação **gerenciamento de API** menu saudação à esquerda e clique **convidar usuário**.</span><span class="sxs-lookup"><span data-stu-id="2d446-121">tooinvite a developer, click **Users** from hello **API Management** menu on hello left, and then click **Invite User**.</span></span>

![Convidar desenvolvedor][api-management-invite-developer]

<span data-ttu-id="2d446-123">Digite hello nome e endereço de email do desenvolvedor Olá e clique em **convidar**.</span><span class="sxs-lookup"><span data-stu-id="2d446-123">Enter hello name and email address of hello developer, and click **Invite**.</span></span>

![Convidar desenvolvedor][api-management-invite-developer-window]

<span data-ttu-id="2d446-125">Será exibida uma mensagem de confirmação, mas o desenvolvedor Olá recentemente convidado não aparecem na lista de saudação até depois de aceitar o convite de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d446-125">A confirmation message is displayed, but hello newly invited developer does not appear in hello list until after they accept hello invitation.</span></span> 

![Confirmação de convite][api-management-invite-developer-confirmation]

<span data-ttu-id="2d446-127">Quando um desenvolvedor é convidado, é enviado um email toohello developer.</span><span class="sxs-lookup"><span data-stu-id="2d446-127">When a developer is invited, an email is sent toohello developer.</span></span> <span data-ttu-id="2d446-128">O email é gerado utilizando um modelo e pode ser personalizado.</span><span class="sxs-lookup"><span data-stu-id="2d446-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="2d446-129">Para obter mais informações, consulte [Configurar modelos de email][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="2d446-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="2d446-130">Quando Olá convite é aceito, conta Olá fica ativa.</span><span class="sxs-lookup"><span data-stu-id="2d446-130">Once hello invitation is accepted, hello account becomes active.</span></span>

## <span data-ttu-id="2d446-131"><a name="block-developer"> </a> Desativar ou reativar uma conta de desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="2d446-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="2d446-132">Por padrão, as contas de desenvolvedor criadas ou convidadas recentemente têm o estado **Ativa**.</span><span class="sxs-lookup"><span data-stu-id="2d446-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="2d446-133">Clique em toodeactivate uma conta de desenvolvedor, **bloco**.</span><span class="sxs-lookup"><span data-stu-id="2d446-133">toodeactivate a developer account, click **Block**.</span></span> <span data-ttu-id="2d446-134">tooreactivate uma conta de desenvolvedor bloqueado, clique em **ativar**.</span><span class="sxs-lookup"><span data-stu-id="2d446-134">tooreactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="2d446-135">Uma conta de desenvolvedor bloqueados não pode acessar o portal do desenvolvedor hello ou chamar quaisquer APIs.</span><span class="sxs-lookup"><span data-stu-id="2d446-135">A blocked developer account can not access hello developer portal or call any APIs.</span></span> <span data-ttu-id="2d446-136">toodelete uma conta de usuário, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="2d446-136">toodelete a user account, click **Delete**.</span></span>

![Bloquear desenvolvedor][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="2d446-138">Redefinir a senha de um usuário</span><span class="sxs-lookup"><span data-stu-id="2d446-138">Reset a user password</span></span>
<span data-ttu-id="2d446-139">senha de saudação tooreset para uma conta de usuário, clique o nome de saudação da conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d446-139">tooreset hello password for a user account, click hello name of hello account.</span></span>

![Redefinir senha][api-management-view-developer]

<span data-ttu-id="2d446-141">Clique em **Redefinir senha** toosend um tooreset de usuário do link toohello sua senha.</span><span class="sxs-lookup"><span data-stu-id="2d446-141">Click **Reset password** toosend a link toohello user tooreset their password.</span></span>

![Redefinir senha][api-management-reset-password]

<span data-ttu-id="2d446-143">trabalho tooprogrammatically com contas de usuário, consulte Olá [entidade usuário](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentação Olá [API REST de gerenciamento](https://msdn.microsoft.com/library/azure/dn776326.aspx) referência.</span><span class="sxs-lookup"><span data-stu-id="2d446-143">tooprogrammatically work with user accounts, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="2d446-144">tooreset um valor específico do usuário conta senha tooa, você pode usar o hello [atualizar um usuário](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operação e especifique a senha desejada hello.</span><span class="sxs-lookup"><span data-stu-id="2d446-144">tooreset a user account password tooa specific value, you can use hello [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify hello desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="2d446-145">Verificação pendente</span><span class="sxs-lookup"><span data-stu-id="2d446-145">Pending verification</span></span>
![Verificação pendente][api-management-pending-verification]

## <span data-ttu-id="2d446-147"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d446-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="2d446-148">Depois de criar uma conta de desenvolvedor, você pode associá-lo com as funções e inscrevê-lo tooproducts e APIs.</span><span class="sxs-lookup"><span data-stu-id="2d446-148">Once a developer account is created, you can associate it with roles and subscribe it tooproducts and APIs.</span></span> <span data-ttu-id="2d446-149">Para obter mais informações, consulte [como toocreate e use grupos][How toocreate and use groups].</span><span class="sxs-lookup"><span data-stu-id="2d446-149">For more information, see [How toocreate and use groups][How toocreate and use groups].</span></span>

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
