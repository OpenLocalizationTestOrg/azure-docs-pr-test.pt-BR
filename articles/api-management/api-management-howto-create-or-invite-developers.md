---
title: "Como gerenciar contas de usuário no Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como criar ou convidar usuários no Gerenciamento de API do Azure"
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
ms.openlocfilehash: d3a50f6d22cbf1797f580078bc0d2cc9cefe5064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a><span data-ttu-id="283a3-103">Como gerenciar contas de usuário no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="283a3-103">How to manage user accounts in Azure API Management</span></span>
<span data-ttu-id="283a3-104">No Gerenciamento de API, os desenvolvedores são os usuários das APIs que você expõe utilizando o Gerenciamento d API.</span><span class="sxs-lookup"><span data-stu-id="283a3-104">In API Management, developers are the users of the APIs that you expose using API Management.</span></span> <span data-ttu-id="283a3-105">Este guia mostra como criar e convidar desenvolvedores a utilizarem as APIs e os produtos que você disponibilizar para eles com sua instância do Gerenciamento da API.</span><span class="sxs-lookup"><span data-stu-id="283a3-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span></span> <span data-ttu-id="283a3-106">Para saber mais sobre como gerenciar contas de usuário por meio de programação, confira a documentação sobre [Entidade de usuário](https://msdn.microsoft.com/library/azure/dn776330.aspx) na referência [REST de Gerenciamento de API](https://msdn.microsoft.com/library/azure/dn776326.aspx).</span><span class="sxs-lookup"><span data-stu-id="283a3-106">For information on managing user accounts programmatically, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="283a3-107"><a name="create-developer"> </a>Criar um novo desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="283a3-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="283a3-108">Para criar um novo desenvolvedor, clique no **portal do Editor** no Portal do Azure para seu serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="283a3-108">To create a new developer, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="283a3-109">Isso levará você ao portal do editor de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="283a3-109">This takes you to the API Management publisher portal.</span></span> <span data-ttu-id="283a3-110">Se ainda não criou uma instância de serviço de Gerenciamento de API, confira [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="283a3-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal do editor][api-management-management-console]

<span data-ttu-id="283a3-112">Clique em **Usuários** no menu **Gerenciamento de API** à esquerda e depois clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="283a3-112">Click **Users** from the **API Management** menu on the left, and then click **add user**.</span></span>

![Criar desenvolvedor][api-management-create-developer]

<span data-ttu-id="283a3-114">Insira o **Email**, a **Senha** e o **Nome** do novo desenvolvedor e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="283a3-114">Enter the **Email**, **Password**, and **Name** for the new developer and click **Save**.</span></span>

![Criar desenvolvedor][api-management-add-new-user]

<span data-ttu-id="283a3-116">Por padrão, as contas de desenvolvedor criadas recentemente têm o estado **Ativa** e são associadas ao grupo **Desenvolvedores**.</span><span class="sxs-lookup"><span data-stu-id="283a3-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span></span>

![Novo desenvolvedor][api-management-new-developer]

<span data-ttu-id="283a3-118">As contas de desenvolvedor que estão com estado **ativa** podem ser utilizadas para acessar todas as APIs nas quais estão inscritas.</span><span class="sxs-lookup"><span data-stu-id="283a3-118">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span></span> <span data-ttu-id="283a3-119">Para associar um desenvolvedor recém-criado a grupos adicionais, consulte [Como associar grupos a desenvolvedores][How to associate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="283a3-119">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="283a3-120"><a name="invite-developer"> </a>Convidar um desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="283a3-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="283a3-121">Para convidar um desenvolvedor, clique em **Usuários** no menu **Gerenciamento de API** à esquerda e depois clique em **Convidar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="283a3-121">To invite a developer, click **Users** from the **API Management** menu on the left, and then click **Invite User**.</span></span>

![Convidar desenvolvedor][api-management-invite-developer]

<span data-ttu-id="283a3-123">Insira o nome e o endereço de email do desenvolvedor e clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="283a3-123">Enter the name and email address of the developer, and click **Invite**.</span></span>

![Convidar desenvolvedor][api-management-invite-developer-window]

<span data-ttu-id="283a3-125">Uma mensagem de confirmação é exibida, mas o desenvolvedor recém-convidado não aparecerá na lista até que ele aceite o convite.</span><span class="sxs-lookup"><span data-stu-id="283a3-125">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span></span> 

![Confirmação de convite][api-management-invite-developer-confirmation]

<span data-ttu-id="283a3-127">Quando um desenvolvedor é convidado, um email é enviado a ele.</span><span class="sxs-lookup"><span data-stu-id="283a3-127">When a developer is invited, an email is sent to the developer.</span></span> <span data-ttu-id="283a3-128">O email é gerado utilizando um modelo e pode ser personalizado.</span><span class="sxs-lookup"><span data-stu-id="283a3-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="283a3-129">Para obter mais informações, consulte [Configurar modelos de email][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="283a3-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="283a3-130">Após o convite ser aceito, a conta se torna ativa.</span><span class="sxs-lookup"><span data-stu-id="283a3-130">Once the invitation is accepted, the account becomes active.</span></span>

## <span data-ttu-id="283a3-131"><a name="block-developer"> </a> Desativar ou reativar uma conta de desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="283a3-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="283a3-132">Por padrão, as contas de desenvolvedor criadas ou convidadas recentemente têm o estado **Ativa**.</span><span class="sxs-lookup"><span data-stu-id="283a3-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="283a3-133">Para desativar uma conta de desenvolvedor, clique em **Bloquear**.</span><span class="sxs-lookup"><span data-stu-id="283a3-133">To deactivate a developer account, click **Block**.</span></span> <span data-ttu-id="283a3-134">Para reativar uma conta de desenvolvedor bloqueada, clique em **Ativar**.</span><span class="sxs-lookup"><span data-stu-id="283a3-134">To reactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="283a3-135">Uma conta de desenvolvedor bloqueada não pode acessar o portal do desenvolvedor ou chamar quaisquer APIs.</span><span class="sxs-lookup"><span data-stu-id="283a3-135">A blocked developer account can not access the developer portal or call any APIs.</span></span> <span data-ttu-id="283a3-136">Para excluir uma conta de usuário, clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="283a3-136">To delete a user account, click **Delete**.</span></span>

![Bloquear desenvolvedor][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="283a3-138">Redefinir a senha de um usuário</span><span class="sxs-lookup"><span data-stu-id="283a3-138">Reset a user password</span></span>
<span data-ttu-id="283a3-139">Para redefinir a senha de uma conta de usuário, clique no nome da conta.</span><span class="sxs-lookup"><span data-stu-id="283a3-139">To reset the password for a user account, click the name of the account.</span></span>

![Redefinir senha][api-management-view-developer]

<span data-ttu-id="283a3-141">Clique em **Redefinir senha** para enviar um link para o usuário a fim de redefinir sua senha.</span><span class="sxs-lookup"><span data-stu-id="283a3-141">Click **Reset password** to send a link to the user to reset their password.</span></span>

![Redefinir senha][api-management-reset-password]

<span data-ttu-id="283a3-143">Para trabalhar de forma programática com contas de usuário, confira a documentação sobre [Entidade de usuário](https://msdn.microsoft.com/library/azure/dn776330.aspx) na referência [REST de Gerenciamento de API](https://msdn.microsoft.com/library/azure/dn776326.aspx).</span><span class="sxs-lookup"><span data-stu-id="283a3-143">To programmatically work with user accounts, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="283a3-144">Para redefinir uma senha de conta de usuário para um valor específico, você pode usar a operação [Atualizar um usuário](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) e especificar a senha desejada.</span><span class="sxs-lookup"><span data-stu-id="283a3-144">To reset a user account password to a specific value, you can use the [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify the desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="283a3-145">Verificação pendente</span><span class="sxs-lookup"><span data-stu-id="283a3-145">Pending verification</span></span>
![Verificação pendente][api-management-pending-verification]

## <span data-ttu-id="283a3-147"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="283a3-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="283a3-148">Após criar uma conta de desenvolvedor, você pode associá-la a funções e inscrevê-la em produtos e APIs.</span><span class="sxs-lookup"><span data-stu-id="283a3-148">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span></span> <span data-ttu-id="283a3-149">Para obter mais informações, confira [Como criar e utilizar grupos][How to create and use groups].</span><span class="sxs-lookup"><span data-stu-id="283a3-149">For more information, see [How to create and use groups][How to create and use groups].</span></span>

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
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
