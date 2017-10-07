---
title: "toocontrol de controle de acesso baseado em função (RBAC) aaaAzure toocreate de direitos de acesso e gerenciar solicitações de suporte | Microsoft Docs"
description: "Toocontrol de controle de acesso baseado em função (RBAC) do Azure toocreate direitos de acesso e gerenciar solicitações de suporte"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a><span data-ttu-id="d667b-103">Toocontrol de controle de acesso baseado em função (RBAC) do Azure toocreate direitos de acesso e gerenciar solicitações de suporte</span><span class="sxs-lookup"><span data-stu-id="d667b-103">Azure Role-Based Access Control (RBAC) toocontrol access rights toocreate and manage support requests</span></span>

<span data-ttu-id="d667b-104">O [RBAC (Controle de Acesso Baseado em Função)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) permite gerenciamento de acesso refinado para o Azure.</span><span class="sxs-lookup"><span data-stu-id="d667b-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="d667b-105">Suporte à criação de solicitação no hello portal do Azure, [portal.azure.com](https://portal.azure.com), usa toodefine de modelo RBAC do Azure que pode criar e gerenciar solicitações de suporte.</span><span class="sxs-lookup"><span data-stu-id="d667b-105">Support request creation in hello Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model toodefine who can create and manage support requests.</span></span>
<span data-ttu-id="d667b-106">Acesso atribuindo Olá apropriado RBAC função toousers, grupos e aplicativos em um determinado escopo, pode ser uma assinatura, o grupo de recursos ou um recurso.</span><span class="sxs-lookup"><span data-stu-id="d667b-106">Access is granted by assigning hello appropriate RBAC role toousers, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="d667b-107">Vejamos um exemplo: como proprietário do grupo de recursos com permissões de leitura no escopo de assinatura hello, você pode gerenciar todos os recursos de saudação no grupo de recursos de saudação, como sites, máquinas virtuais e sub-redes.</span><span class="sxs-lookup"><span data-stu-id="d667b-107">Let’s take an example: As a resource group owner with read permissions at hello subscription scope, you can manage all hello resources under hello resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="d667b-108">No entanto, quando você tenta toocreate uma solicitação de suporte no recurso de máquina virtual hello, encontrar hello erro a seguir</span><span class="sxs-lookup"><span data-stu-id="d667b-108">However, when you try toocreate a support request against hello virtual machine resource, you encounter hello following error</span></span>

![Erro de assinatura](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="d667b-110">Gerenciamento de solicitação de suporte, você precisa de permissão de gravação ou uma função que tenha Olá suporte ação Microsoft.Support/* no hello assinatura escopo toobe capaz de toocreate e gerenciar solicitações de suporte.</span><span class="sxs-lookup"><span data-stu-id="d667b-110">In support request management, you need write permission or a role that has hello Support action Microsoft.Support/* at hello Subscription scope toobe able toocreate and manage support requests.</span></span>

<span data-ttu-id="d667b-111">Olá artigo a seguir explica como você pode usar toocreate de controle de acesso baseado em função (RBAC) personalizado do Azure e gerenciar solicitações de suporte em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d667b-111">hello following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) toocreate and manage support requests in hello Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d667b-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="d667b-112">Getting Started</span></span>

<span data-ttu-id="d667b-113">Usando o exemplo hello acima, você seria capaz de toocreate uma solicitação de suporte para o recurso se você foram atribuídos a uma função RBAC personalizada na assinatura de saudação pelo proprietário da assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="d667b-113">Using hello example above, you would be able toocreate a support request for your resource if you were assigned a custom RBAC role on hello subscription by hello subscription owner.</span></span>
<span data-ttu-id="d667b-114">[Funções personalizadas de RBAC](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) podem ser criados usando o PowerShell do Azure, Azure Interface de linha de comando (CLI) e Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="d667b-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and hello REST API.</span></span>

<span data-ttu-id="d667b-115">propriedade de ações de saudação de uma função personalizada especifica hello Azure operações toowhich Olá função concede acesso.</span><span class="sxs-lookup"><span data-stu-id="d667b-115">hello actions property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span>
<span data-ttu-id="d667b-116">toocreate uma função personalizada para o gerenciamento de solicitação de suporte, uma função de saudação deve ter ação Olá Microsoft.Support/*</span><span class="sxs-lookup"><span data-stu-id="d667b-116">toocreate a custom role for support request management, hello role must have hello action Microsoft.Support/*</span></span>

<span data-ttu-id="d667b-117">Aqui está um exemplo de uma função personalizada, você pode usar toocreate e gerenciar solicitações de suporte.</span><span class="sxs-lookup"><span data-stu-id="d667b-117">Here’s an example of a custom role you can use toocreate and manage support requests.</span></span>
<span data-ttu-id="d667b-118">Chamamos essa função "Colaborador de solicitação de suporte" e isso é como fazemos referência a função personalizada toohello neste artigo.</span><span class="sxs-lookup"><span data-stu-id="d667b-118">We’ve named this role “Support Request Contributor” and that’s how we refer toohello custom role in this article.</span></span>

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

<span data-ttu-id="d667b-119">Siga etapas Olá descritas em [este vídeo](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn como toocreate uma função personalizada para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="d667b-119">Follow hello steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn how toocreate a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a><span data-ttu-id="d667b-120">Criar e gerenciar solicitações de suporte em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d667b-120">Create and manage support requests in hello Azure portal</span></span>

<span data-ttu-id="d667b-121">Vejamos um exemplo – você é proprietário de saudação de assinatura "Visual Studio assinatura do MSDN."</span><span class="sxs-lookup"><span data-stu-id="d667b-121">Let’s take an example – you are hello owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="d667b-122">Se o ponto a ponto que é um toosome de proprietário do recurso Olá de grupos de recursos na assinatura e tem a assinatura de toohello de permissão de leitura.</span><span class="sxs-lookup"><span data-stu-id="d667b-122">Joe is your peer who is a resource owner toosome of hello resource groups in this subscription and has read permission toohello subscription.</span></span>
<span data-ttu-id="d667b-123">Você deseja toogive acesso tooyour ponto a ponto, Joe, Olá capacidade toocreate e gerenciar tíquetes de suporte para recursos de saudação sob essa assinatura.</span><span class="sxs-lookup"><span data-stu-id="d667b-123">You wish toogive access tooyour peer, Joe, hello ability toocreate and manage support tickets for hello resources under this subscription.</span></span>

1. <span data-ttu-id="d667b-124">Olá primeira etapa é toogo toohello assinatura e em "Configurações" você ver uma lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d667b-124">hello first step is toogo toohello subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="d667b-125">Clique em usuário Olá Joe quem tem acesso de leitor em Olá assinatura e permite atribuir um novo toohim de função personalizada.</span><span class="sxs-lookup"><span data-stu-id="d667b-125">Click hello user Joe who has reader access on hello Subscription and let’s assign a new custom role toohim.</span></span>

    ![Adicionar função](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="d667b-127">Na folha de "Usuários" Olá, clique em "Adicionar".</span><span class="sxs-lookup"><span data-stu-id="d667b-127">Click "Add" under hello "Users" blade.</span></span> <span data-ttu-id="d667b-128">Função personalizada de hello "Colaborador de solicitação de suporte" Selecione na lista de saudação de funções</span><span class="sxs-lookup"><span data-stu-id="d667b-128">Select hello custom role "Support Request Contributor" from hello list of roles</span></span>

    ![Adicione a função colaborador de suporte](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="d667b-130">Depois de selecionar o nome da função hello, clique em "Adicionar usuários" e insira as credenciais de email de Joe hello.</span><span class="sxs-lookup"><span data-stu-id="d667b-130">After selecting hello role name, click "Add users" and enter hello Joe's email credentials.</span></span> <span data-ttu-id="d667b-131">Clique em “Selecionar”</span><span class="sxs-lookup"><span data-stu-id="d667b-131">Click "Select"</span></span>

    ![Adicionar usuários](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="d667b-133">Clique em "Okey" tooproceed</span><span class="sxs-lookup"><span data-stu-id="d667b-133">Click "Ok" tooproceed</span></span>

    ![Adicionar acesso](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="d667b-135">Agora você verá que o usuário Olá com função personalizada recém-adicionado hello "Suporte de solicitação Colaborador" na assinatura Olá para o qual você é proprietário de saudação</span><span class="sxs-lookup"><span data-stu-id="d667b-135">Now you see hello user with hello newly added custom role "Support Request Contributor" under hello Subscription for which you are hello owner</span></span>

    ![Usuário adicionado](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="d667b-137">Quando Joe faz logon no portal de hello, ele vê Olá assinatura toowhich que ele foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="d667b-137">When Joe logs in hello portal, he sees hello subscription toowhich he was added.</span></span>

7. <span data-ttu-id="d667b-138">José clica em "Nova solicitação de suporte" da folha de "Ajuda e suporte" hello e pode criar solicitações de suporte para "Visual Studio Ultimate com MSDN"</span><span class="sxs-lookup"><span data-stu-id="d667b-138">Joe clicks "New Support request" from hello "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Nova solicitação de suporte](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="d667b-140">Clique em "Todas as solicitações de suporte" Joe pode ver Olá lista solicitações de suporte criado para esta assinatura ![exibição de detalhes do caso](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="d667b-140">Clicking "All support requests" Joe can see hello list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-hello-azure-portal"></a><span data-ttu-id="d667b-141">Remover o acesso de solicitação de suporte em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d667b-141">Remove support request access in hello Azure portal</span></span>

<span data-ttu-id="d667b-142">Assim como é possível toogrant acesso tooa usuário toocreate e gerenciar solicitações de suporte, é possível tooremove acesso usuário de saudação também.</span><span class="sxs-lookup"><span data-stu-id="d667b-142">Just as it is possible toogrant access tooa user toocreate and manage support requests, it's possible tooremove access for hello user as well.</span></span>
<span data-ttu-id="d667b-143">tooremove Olá toocreate de capacidade e gerenciar solicitações de suporte, vá toohello assinatura, clique em "Configurações" e clique em Olá usuário (nesse caso, Pedro).</span><span class="sxs-lookup"><span data-stu-id="d667b-143">tooremove hello ability toocreate and manage support requests, go toohello Subscription, click "Settings" and click hello user (in this case, Joe).</span></span>
<span data-ttu-id="d667b-144">Clique em nome da função hello, "Colaborador de solicitação de suporte" e clique em "Remover"</span><span class="sxs-lookup"><span data-stu-id="d667b-144">Right-click hello role name, "Support Request Contributor" and click "Remove"</span></span>

![Remover acesso a solicitação de suporte](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="d667b-146">Quando Joe fizer logon no portal de toohello e tenta toocreate uma solicitação de suporte, ele encontra Olá erro a seguir</span><span class="sxs-lookup"><span data-stu-id="d667b-146">When Joe logs in toohello portal and tries toocreate a support request, he encounters hello following error</span></span>

![Erro de assinatura-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="d667b-148">Joe não conseguirá ver as solicitações suporte quando clicar em "Todas as solicitações de suporte"</span><span class="sxs-lookup"><span data-stu-id="d667b-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![exibição de detalhes do caso-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
