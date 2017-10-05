---
title: "O Controle de Acesso Baseado em Função (RBAC) do Azure para controlar os direitos de acesso para criação e gerenciamento de solicitações de suporte | Microsoft Docs"
description: "O Controle de Acesso Baseado em Função (RBAC) do Azure para controlar os direitos de acesso para criação e gerenciamento de solicitações de suporte"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: 20ebd324cbf379980b43d255d468673de2b6d950
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-based-access-control-rbac-to-control-access-rights-to-create-and-manage-support-requests"></a><span data-ttu-id="f5c8e-103">O Controle de Acesso Baseado em Função (RBAC) do Azure para controlar os direitos de acesso para criação e gerenciamento de solicitações de suporte</span><span class="sxs-lookup"><span data-stu-id="f5c8e-103">Azure Role-Based Access Control (RBAC) to control access rights to create and manage support requests</span></span>

<span data-ttu-id="f5c8e-104">O [RBAC (Controle de Acesso Baseado em Função)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) permite gerenciamento de acesso refinado para o Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="f5c8e-105">A criação de solicitação de suporte no portal do Azure [portal.azure.com](https://portal.azure.com) usa o modelo RBAC do Azure para definir quem pode criar e gerenciar solicitações de suporte.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-105">Support request creation in the Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model to define who can create and manage support requests.</span></span>
<span data-ttu-id="f5c8e-106">O acesso é concedido ao atribuir a função RBAC apropriada a usuários, grupos e aplicativos em determinado escopo, que pode ser uma assinatura, um recurso ou um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-106">Access is granted by assigning the appropriate RBAC role to users, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="f5c8e-107">Vejamos um exemplo: como proprietário de um grupo de recursos com permissões de leitura no escopo de assinatura, você pode gerenciar todos os recursos do grupo de recursos, tais como sites, máquinas virtuais e sub-redes.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-107">Let’s take an example: As a resource group owner with read permissions at the subscription scope, you can manage all the resources under the resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="f5c8e-108">No entanto, se tentar criar uma solicitação de suporte relativa ao recurso de máquina virtual, você vai encontrar o seguinte erro</span><span class="sxs-lookup"><span data-stu-id="f5c8e-108">However, when you try to create a support request against the virtual machine resource, you encounter the following error</span></span>

![Erro de assinatura](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="f5c8e-110">No gerenciamento de solicitações de suporte, você precisa de permissão de gravação ou uma função que tenha a ação de suporte Microsoft.Support/* no escopo de assinatura para poder criar e gerenciar solicitações de suporte.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-110">In support request management, you need write permission or a role that has the Support action Microsoft.Support/* at the Subscription scope to be able to create and manage support requests.</span></span>

<span data-ttu-id="f5c8e-111">O seguinte artigo explica como você pode usar o Controle de Acesso Baseado em Função (RBAC) do Azure para criar e gerenciar solicitações de suporte no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-111">The following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) to create and manage support requests in the Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f5c8e-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="f5c8e-112">Getting Started</span></span>

<span data-ttu-id="f5c8e-113">Usando o exemplo acima, será possível criar uma solicitação de suporte para seu recurso se uma função RBAC personalizada na assinatura tiver sido atribuída a você pelo proprietário da assinatura.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-113">Using the example above, you would be able to create a support request for your resource if you were assigned a custom RBAC role on the subscription by the subscription owner.</span></span>
<span data-ttu-id="f5c8e-114">É possível criar [funções RBAC personalizadas](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) usando o Azure PowerShell, a interface de linha de comando (CLI) do Azure e a API REST.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and the REST API.</span></span>

<span data-ttu-id="f5c8e-115">A propriedade actions de uma função personalizada especifica as operações do Azure às quais a função concede acesso.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-115">The actions property of a custom role specifies the Azure operations to which the role grants access.</span></span>
<span data-ttu-id="f5c8e-116">Para criar uma função personalizada para o gerenciamento de solicitações de suporte, a função deve ter a ação Microsoft.Support/*</span><span class="sxs-lookup"><span data-stu-id="f5c8e-116">To create a custom role for support request management, the role must have the action Microsoft.Support/*</span></span>

<span data-ttu-id="f5c8e-117">Aqui está um exemplo de uma função personalizada que você pode usar para criar e gerenciar solicitações de suporte.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-117">Here’s an example of a custom role you can use to create and manage support requests.</span></span>
<span data-ttu-id="f5c8e-118">Chamamos essa função de "Colaborador de Solicitação de Suporte" e é como nos referimos à função personalizada neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-118">We’ve named this role “Support Request Contributor” and that’s how we refer to the custom role in this article.</span></span>

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

<span data-ttu-id="f5c8e-119">Siga as etapas descritas [neste vídeo](https://www.youtube.com/watch?v=-PaBaDmfwKI) para aprender a criar uma função personalizada para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-119">Follow the steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) to learn how to create a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-the-azure-portal"></a><span data-ttu-id="f5c8e-120">Criar e gerenciar solicitações de suporte no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f5c8e-120">Create and manage support requests in the Azure portal</span></span>

<span data-ttu-id="f5c8e-121">Vejamos um exemplo – você é o proprietário da assinatura "Assinatura MSDN do Visual Studio".</span><span class="sxs-lookup"><span data-stu-id="f5c8e-121">Let’s take an example – you are the owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="f5c8e-122">Joe, seu colega, é proprietário de recursos em alguns grupos de recursos dessa assinatura e tem permissão de leitura na assinatura.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-122">Joe is your peer who is a resource owner to some of the resource groups in this subscription and has read permission to the subscription.</span></span>
<span data-ttu-id="f5c8e-123">Você deseja conceder a Joe o acesso necessário à capacidade de criar e gerenciar tíquetes de suporte para os recursos dessa assinatura.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-123">You wish to give access to your peer, Joe, the ability to create and manage support tickets for the resources under this subscription.</span></span>

1. <span data-ttu-id="f5c8e-124">A primeira etapa é ir para a assinatura e ver uma lista de usuários em "Configurações".</span><span class="sxs-lookup"><span data-stu-id="f5c8e-124">The first step is to go to the subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="f5c8e-125">Clique no usuário Joe, que tem acesso de leitura na assinatura, para atribuir uma nova função personalizada para ele.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-125">Click the user Joe who has reader access on the Subscription and let’s assign a new custom role to him.</span></span>

    ![Adicionar função](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="f5c8e-127">Clique em “Adicionar” na folha “Usuários”.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-127">Click "Add" under the "Users" blade.</span></span> <span data-ttu-id="f5c8e-128">Selecione a função personalizada "Colaborador de Solicitação de Suporte" na lista de funções</span><span class="sxs-lookup"><span data-stu-id="f5c8e-128">Select the custom role "Support Request Contributor" from the list of roles</span></span>

    ![Adicione a função colaborador de suporte](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="f5c8e-130">Após selecionar o nome da função, clique em “Adicionar usuários” e insira as credenciais de email de Joe.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-130">After selecting the role name, click "Add users" and enter the Joe's email credentials.</span></span> <span data-ttu-id="f5c8e-131">Clique em “Selecionar”</span><span class="sxs-lookup"><span data-stu-id="f5c8e-131">Click "Select"</span></span>

    ![Adicionar usuários](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="f5c8e-133">Clique em “OK” para continuar</span><span class="sxs-lookup"><span data-stu-id="f5c8e-133">Click "Ok" to proceed</span></span>

    ![Adicionar acesso](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="f5c8e-135">Agora você verá o usuário com a função personalizada "Colaborador de Solicitação de Suporte" recém-adicionada na Assinatura que tem você como proprietário</span><span class="sxs-lookup"><span data-stu-id="f5c8e-135">Now you see the user with the newly added custom role "Support Request Contributor" under the Subscription for which you are the owner</span></span>

    ![Usuário adicionado](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="f5c8e-137">Quando Joe fizer logon no portal, ele verá a assinatura à qual foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-137">When Joe logs in the portal, he sees the subscription to which he was added.</span></span>

7. <span data-ttu-id="f5c8e-138">Joe clica em "Nova solicitação de suporte" na folha "Ajuda e suporte" e pode criar solicitações de suporte para "Visual Studio Ultimate com MSDN"</span><span class="sxs-lookup"><span data-stu-id="f5c8e-138">Joe clicks "New Support request" from the "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Nova solicitação de suporte](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="f5c8e-140">Clique em "Todas as solicitações de suporte" Joe pode ver a lista de solicitações de suporte criado para esta assinatura ![exibição de detalhes do caso](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="f5c8e-140">Clicking "All support requests" Joe can see the list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-the-azure-portal"></a><span data-ttu-id="f5c8e-141">Remover o acesso a solicitação de suporte no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f5c8e-141">Remove support request access in the Azure portal</span></span>

<span data-ttu-id="f5c8e-142">Assim como é possível conceder acesso a um usuário para criar e gerenciar solicitações de suporte, também é possível removê-lo.</span><span class="sxs-lookup"><span data-stu-id="f5c8e-142">Just as it is possible to grant access to a user to create and manage support requests, it's possible to remove access for the user as well.</span></span>
<span data-ttu-id="f5c8e-143">Para remover a capacidade de criar e gerenciar solicitações de suporte, vá para a assinatura, clique em "Configurações" e clique no usuário (nesse caso, Joe).</span><span class="sxs-lookup"><span data-stu-id="f5c8e-143">To remove the ability to create and manage support requests, go to the Subscription, click "Settings" and click the user (in this case, Joe).</span></span>
<span data-ttu-id="f5c8e-144">Clique com o botão direito no nome da função "Colaborador de Solicitação de Suporte" e clique em "Remover"</span><span class="sxs-lookup"><span data-stu-id="f5c8e-144">Right-click the role name, "Support Request Contributor" and click "Remove"</span></span>

![Remover acesso a solicitação de suporte](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="f5c8e-146">Quando Joe faz logon no portal e tenta criar uma solicitação de suporte, ele encontra o seguinte erro</span><span class="sxs-lookup"><span data-stu-id="f5c8e-146">When Joe logs in to the portal and tries to create a support request, he encounters the following error</span></span>

![Erro de assinatura-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="f5c8e-148">Joe não conseguirá ver as solicitações suporte quando clicar em "Todas as solicitações de suporte"</span><span class="sxs-lookup"><span data-stu-id="f5c8e-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![exibição de detalhes do caso-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
