---
title: "funções de controle de acesso baseado em função personalizadas aaaCreate e atribuir toointernal e usuários externos no Azure | Microsoft Docs"
description: "Atribuir funções RBAC personalizadas criadas usando o PowerShell e a CLI para usuários internos e externos"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="b3e83-103">Introdução ao controle de acesso baseado em função do Azure</span><span class="sxs-lookup"><span data-stu-id="b3e83-103">Intro on role-based access control</span></span>

<span data-ttu-id="b3e83-104">Controle de acesso baseado em função é um recurso de somente portal do Azure permitindo proprietários de saudação de uma assinatura tooassign funções granulares tooother que podem gerenciar escopos de recurso específico em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="b3e83-104">Role-based access control is an Azure portal only feature allowing hello owners of a subscription tooassign granular roles tooother users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="b3e83-105">RBAC permite melhor gerenciamento de segurança para organizações de grandes porte em SMBs trabalhando com parceiros externos, fornecedores ou freelancers que precisam acessar os recursos de toospecific em seu ambiente, mas não necessariamente toda a infraestrutura de toohello ou qualquer escopos relacionados à cobrança.</span><span class="sxs-lookup"><span data-stu-id="b3e83-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access toospecific resources in your environment but not necessarily toohello entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="b3e83-106">RBAC permite flexibilidade de saudação do proprietário de uma assinatura do Azure gerenciada por conta de administrador da saudação (função de administrador de serviço em um nível de assinatura) e tem várias toowork usuários convidados em Olá mesma assinatura mas sem qualquer administrativas direitos para ele.</span><span class="sxs-lookup"><span data-stu-id="b3e83-106">RBAC allows hello flexibility of owning one Azure subscription managed by hello administrator account (service administrator role at a subscription level) and have multiple users invited toowork under hello same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="b3e83-107">De uma perspectiva de cobrança e gerenciamento, o recurso RBAC Olá prova toobe uma opção tempo e gerenciamento eficiente para o uso do Azure em vários cenários.</span><span class="sxs-lookup"><span data-stu-id="b3e83-107">From a management and billing perspective, hello RBAC feature proves toobe a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3e83-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b3e83-108">Prerequisites</span></span>
<span data-ttu-id="b3e83-109">Usando o RBAC no ambiente do Azure de saudação requer:</span><span class="sxs-lookup"><span data-stu-id="b3e83-109">Using RBAC in hello Azure environment requires:</span></span>

* <span data-ttu-id="b3e83-110">Assinatura do Azure com um autônomo atribuído toohello usuário como o proprietário (função de assinatura)</span><span class="sxs-lookup"><span data-stu-id="b3e83-110">Having a standalone Azure subscription assigned toohello user as owner (subscription role)</span></span>
* <span data-ttu-id="b3e83-111">Ter função de proprietário de saudação do hello assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="b3e83-111">Have hello Owner role of hello Azure subscription</span></span>
* <span data-ttu-id="b3e83-112">Ter acesso toohello [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b3e83-112">Have access toohello [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="b3e83-113">Certifique-se Olá toohave seguintes provedores de recursos registrado para a assinatura de usuário Olá: **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="b3e83-113">Make sure toohave hello following Resource Providers registered for hello user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="b3e83-114">Para obter mais informações sobre como tooregister Olá provedores de recursos, consulte [provedores do Gerenciador de recursos, regiões, as versões de API e esquemas](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="b3e83-114">For more information on how tooregister hello resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b3e83-115">Assinaturas do Office 365 ou licenças do Active Directory do Azure (por exemplo: acessar tooAzure do Active Directory) provisionado de saudação O365 portal não qualidade usando o RBAC.</span><span class="sxs-lookup"><span data-stu-id="b3e83-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access tooAzure Active Directory) provisioned from hello O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="b3e83-116">Como o RBAC pode ser usado</span><span class="sxs-lookup"><span data-stu-id="b3e83-116">How can RBAC be used</span></span>
<span data-ttu-id="b3e83-117">O RBAC pode ser aplicado em três escopos diferentes no Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e83-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="b3e83-118">De saudação maior escopo toohello um menor, eles são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="b3e83-118">From hello highest scope toohello lowest one, they are as follows:</span></span>

* <span data-ttu-id="b3e83-119">Assinatura (mais alto)</span><span class="sxs-lookup"><span data-stu-id="b3e83-119">Subscription (highest)</span></span>
* <span data-ttu-id="b3e83-120">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b3e83-120">Resource group</span></span>
* <span data-ttu-id="b3e83-121">Escopo do recurso (hello mais baixo nível de acesso oferta tooan escopo de recursos do Azure individuais de permissões de destino)</span><span class="sxs-lookup"><span data-stu-id="b3e83-121">Resource scope (hello lowest access level offering targeted permissions tooan individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a><span data-ttu-id="b3e83-122">Atribuir funções RBAC no escopo de assinatura Olá</span><span class="sxs-lookup"><span data-stu-id="b3e83-122">Assign RBAC roles at hello subscription scope</span></span>
<span data-ttu-id="b3e83-123">Há dois exemplos comuns de momentos em que o RBAC é usado (entre outros):</span><span class="sxs-lookup"><span data-stu-id="b3e83-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="b3e83-124">Ter usuários externos de organizações de saudação (que não faz parte do Azure Active Directory do usuário do administrador de saudação) convidado toomanage certos recursos ou a assinatura inteira Olá</span><span class="sxs-lookup"><span data-stu-id="b3e83-124">Having external users from hello organizations (not part of hello admin user's Azure Active Directory tenant) invited toomanage certain resources or hello whole subscription</span></span>
* <span data-ttu-id="b3e83-125">Trabalhando com os usuários dentro da organização de saudação (elas fazem parte de locatário do Azure Active Directory do usuário Olá), mas parte de equipes diferentes ou grupos que precisam de acesso granular ou toohello assinatura inteira ou grupos de recursos toocertain ou recurso escopos em Olá ambiente</span><span class="sxs-lookup"><span data-stu-id="b3e83-125">Working with users inside hello organization (they are part of hello user's Azure Active Directory tenant) but part of different teams or groups which need granular access either toohello whole subscription or toocertain resource groups or resource scopes in hello environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="b3e83-126">Conceder acesso no nível da assinatura para um usuário fora do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b3e83-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="b3e83-127">Funções RBAC podem ser concedidas somente pelo **proprietários** de assinatura de saudação, portanto, o usuário de administrador Olá deve estar conectado com um nome de usuário que tem essa função previamente atribuída ou criou Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e83-127">RBAC roles can be granted only by **Owners** of hello subscription therefore hello admin user must be logged with a username which has this role pre-assigned or has created hello Azure subscription.</span></span>

<span data-ttu-id="b3e83-128">De Olá portal do Azure, depois que você entrar como administrador, selecione "Assinaturas" e escolha Olá desejado um.</span><span class="sxs-lookup"><span data-stu-id="b3e83-128">From hello Azure portal, after you sign-in as admin, select “Subscriptions” and chose hello desired one.</span></span>
<span data-ttu-id="b3e83-129">![folha de assinatura no portal do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) por padrão, se o usuário administrador Olá adquiriu Olá assinatura do Azure, usuário Olá aparecerão como **administrador da conta**, esta sendo a função de saudação de assinatura.</span><span class="sxs-lookup"><span data-stu-id="b3e83-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if hello admin user has purchased hello Azure subscription, hello user will show up as **Account Admin**, this being hello subscription role.</span></span> <span data-ttu-id="b3e83-130">Para obter mais detalhes sobre funções de assinatura do Azure hello, consulte [adicionar ou alterar funções de administrador do Azure que gerenciam a assinatura de saudação ou serviços](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="b3e83-130">For more details on hello Azure subscription roles, see [Add or change Azure administrator roles that manage hello subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="b3e83-131">Neste exemplo, Olá usuário "alflanigan@outlook.com" é hello **proprietário** de hello "Avaliação gratuita" assinatura no hello AAD locatário "Padrão de locatário do Azure".</span><span class="sxs-lookup"><span data-stu-id="b3e83-131">In this example, hello user "alflanigan@outlook.com" is hello **Owner** of hello "Free Trial" subscription in hello AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="b3e83-132">Como esse usuário é o criador de saudação do hello assinatura do Azure com a saudação inicial Account da Microsoft "Outlook" (Microsoft Account = Outlook, etc. ao vivo) Olá nome de domínio padrão para todos os outros usuários adicionados neste locatário será **"@alflaniganuoutlook.onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="b3e83-132">Since this user is hello creator of hello Azure subscription with hello initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) hello default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="b3e83-133">Por design, sintaxe de saudação do novo domínio de saudação é formado por reunir Olá nome de usuário e nome de domínio do usuário de saudação que criou o locatário hello e adicionar extensão de saudação **". c o m"**.</span><span class="sxs-lookup"><span data-stu-id="b3e83-133">By design, hello syntax of hello new domain is formed by putting together hello username and domain name of hello user who created hello tenant and adding hello extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="b3e83-134">Além disso, os usuários podem entrar com um nome de domínio personalizado no locatário Olá depois de adicionar e verificando-lo para o novo locatário de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3e83-134">Furthermore, users can sign-in with a custom domain name in hello tenant after adding and verifying it for hello new tenant.</span></span> <span data-ttu-id="b3e83-135">Para obter mais detalhes sobre como tooverify um nome de domínio personalizado em um locatário do Active Directory do Azure, consulte [adicionar um diretório de tooyour de nome de domínio personalizado](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="b3e83-135">For more details on how tooverify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name tooyour directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="b3e83-136">Neste exemplo, hello "padrão do Azure" diretório locatário contém somente os usuários com o nome de domínio hello "@alflanigan.onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="b3e83-136">In this example, hello "Default tenant Azure" directory contains only users with hello domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="b3e83-137">Depois de selecionar a assinatura hello, usuário de administrador Olá deve clicar em **controle de acesso (IAM)** e **adicionar uma nova função**.</span><span class="sxs-lookup"><span data-stu-id="b3e83-137">After selecting hello subscription, hello admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![recurso IAM de controle de acesso no portal do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![adicionar novo usuário no recurso IAM de controle de acesso no portal do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="b3e83-140">Olá próxima etapa é tooselect Olá função toobe atribuído e usuário Olá quem será atribuída à função RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="b3e83-140">hello next step is tooselect hello role toobe assigned and hello user whom hello RBAC role will be assigned to.</span></span> <span data-ttu-id="b3e83-141">Em Olá **função** usuário de administrador de saudação de menu suspenso vê apenas Olá RBAC funções internas que estão disponíveis no Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e83-141">In hello **Role** dropdown menu hello admin user sees only hello built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="b3e83-142">Para obter explicações mais detalhadas sobre cada função e seus escopos atribuíveis, consulte [Funções internas para o Controle de Acesso Baseado em Função do Azure](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="b3e83-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="b3e83-143">o usuário administrador Hello, deverá tooadd endereço de email de saudação do usuário externo hello.</span><span class="sxs-lookup"><span data-stu-id="b3e83-143">hello admin user then needs tooadd hello email address of hello external user.</span></span> <span data-ttu-id="b3e83-144">Olá esperado é de comportamento para Olá usuário externo toonot aparecem Olá existente de locatário.</span><span class="sxs-lookup"><span data-stu-id="b3e83-144">hello expected behavior is for hello external user toonot show up in hello existing tenant.</span></span> <span data-ttu-id="b3e83-145">Depois que o usuário externo Olá foi convidado, ele ficará visível em **assinaturas > controle de acesso (IAM)** com todos os usuários atuais Olá que estão atualmente atribuídos a uma função de RBAC no escopo de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3e83-145">After hello external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all hello current users which are currently assigned an RBAC role at hello Subscription scope.</span></span>





![Adicionar função RBAC toonew permissões](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![lista de funções de RBAC no nível de assinatura](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="b3e83-148">usuário Hello "chessercarlton@gmail.com" foi convidado toobe um **proprietário** para Olá assinatura "Avaliação gratuita".</span><span class="sxs-lookup"><span data-stu-id="b3e83-148">hello user "chessercarlton@gmail.com" has been invited toobe an **Owner** for hello “Free Trial” subscription.</span></span> <span data-ttu-id="b3e83-149">Depois de enviar o convite hello, usuário externo Olá receberá um email de confirmação com um link de ativação.</span><span class="sxs-lookup"><span data-stu-id="b3e83-149">After sending hello invitation, hello external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="b3e83-150">![convite por email para a função RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="b3e83-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="b3e83-151">Sendo organização toohello externo, Olá novo usuário não tem os atributos existentes no diretório de "Padrão de locatário do Azure" hello.</span><span class="sxs-lookup"><span data-stu-id="b3e83-151">Being external toohello organization, hello new user does not have any existing attributes in hello "Default tenant Azure" directory.</span></span> <span data-ttu-id="b3e83-152">Elas serão criadas depois que o usuário externo Olá tenha dado consentimento toobe registrada no diretório de saudação que é associado à assinatura Olá que ele foi atribuído uma função.</span><span class="sxs-lookup"><span data-stu-id="b3e83-152">They will be created after hello external user has given consent toobe recorded in hello directory which is associated with hello subscription which he has been assigned a role to.</span></span>





![mensagem de convite de email para a função de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="b3e83-154">usuário externo Olá mostra no hello locatário do Active Directory do Azure de agora em diante como usuário externo e isso pode ser exibido em Olá portal do Azure e no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="b3e83-154">hello external user shows in hello Azure Active Directory tenant from now on as external user and this can be viewed both in hello Azure portal and in hello classic portal.</span></span>





![folha dos usuários no azure active-directory, portal do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![folha dos usuários no azure active-directory, portal clássico do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="b3e83-157">Em Olá **usuários** em ambos os usuários externos de saudação portais do modo de exibição pode ser reconhecido por:</span><span class="sxs-lookup"><span data-stu-id="b3e83-157">In hello **Users** view in both portals hello external users can be recognized by:</span></span>

* <span data-ttu-id="b3e83-158">tipo de ícone diferentes Olá no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b3e83-158">hello different icon type in hello Azure portal</span></span>
* <span data-ttu-id="b3e83-159">Olá diferente de fornecimento de ponto no portal clássico Olá</span><span class="sxs-lookup"><span data-stu-id="b3e83-159">hello different sourcing point in hello classic portal</span></span>

<span data-ttu-id="b3e83-160">No entanto, concedendo **proprietário** ou **Colaborador** acesso tooan usuário externo no hello **assinatura** escopo, não permite que o diretório do usuário do administrador toohello acesso Olá, a menos que Olá **Administrador Global** permite.</span><span class="sxs-lookup"><span data-stu-id="b3e83-160">However, granting **Owner** or **Contributor** access tooan external user at hello **Subscription** scope, does not allow hello access toohello admin user's directory, unless hello **Global Admin** allows it.</span></span> <span data-ttu-id="b3e83-161">Em Propriedades do usuário hello, Olá **usuário tipo** que tem dois parâmetros comuns, **membro** e **convidado** pode ser identificado.</span><span class="sxs-lookup"><span data-stu-id="b3e83-161">In hello user proprieties,  hello **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="b3e83-162">Um membro é um usuário que está registrado no diretório Olá enquanto um convidado é um diretório de toohello usuário convidado de uma fonte externa.</span><span class="sxs-lookup"><span data-stu-id="b3e83-162">A member is a user which is registered in hello directory while a guest is a user invited toohello directory from an external source.</span></span> <span data-ttu-id="b3e83-163">Para obter mais informações, consulte [Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="b3e83-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="b3e83-164">Certifique-se de que depois de inserir as credenciais de saudação no portal de hello, usuário externo Olá seleciona diretório correto de saudação toosign no.</span><span class="sxs-lookup"><span data-stu-id="b3e83-164">Make sure that after entering hello credentials in hello portal, hello external user selects hello correct directory toosign-in to.</span></span> <span data-ttu-id="b3e83-165">Olá mesmo usuário pode ter acesso toomultiple diretórios e pode selecionar qualquer uma delas clicando Olá nome de usuário no lado superior direito de saudação em Olá portal do Azure e escolha diretório apropriado Olá na lista suspensa hello.</span><span class="sxs-lookup"><span data-stu-id="b3e83-165">hello same user can have access toomultiple directories and can select either one of  them by clicking hello username in hello top right-hand side in hello Azure portal and then choose hello appropriate directory from hello dropdown list.</span></span>

<span data-ttu-id="b3e83-166">Ao ser convidados no diretório Olá, usuário externo Olá pode gerenciar todos os recursos de saudação assinatura do Azure, mas não é possível acessar o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3e83-166">While being a guest in hello directory, hello external user can manage all resources for hello Azure subscription, but can't access hello directory.</span></span>





![acessar o portal do Azure do active directory tooazure restrito](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="b3e83-168">O Azure Active Directory e uma assinatura do Azure não têm uma relação de pai-filho como outros recursos do Azure (por exemplo: máquinas virtuais, redes virtuais, aplicativos Web, armazenamento etc.) têm com uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e83-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="b3e83-169">Todos os hello último é criada, gerenciada e cobrado em uma assinatura do Azure, enquanto uma assinatura do Azure é usado toomanage Olá acesso tooan directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e83-169">All hello latter is created, managed and billed under an Azure subscription while an Azure subscription is used toomanage hello access tooan Azure directory.</span></span> <span data-ttu-id="b3e83-170">Para obter mais detalhes, consulte [assinatura como um Azure está relacionada tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="b3e83-170">For more details, see [How an Azure subscription is related tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="b3e83-171">De todas as funções internas de RBAC de hello, **proprietário** e **Colaborador** oferecem acesso de gerenciamento completo tooall recursos ambiente hello, Olá diferença sendo que não é possível criar um colaborador e excluir novo Funções RBAC.</span><span class="sxs-lookup"><span data-stu-id="b3e83-171">From all hello built-in RBAC roles, **Owner** and **Contributor** offer full management access tooall resources in hello environment, hello difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="b3e83-172">Olá outras funções internas, como **colaborador da máquina Virtual** oferecem acesso de gerenciamento completo apenas os recursos de toohello indicados pelo nome do hello, independentemente de saudação **grupo de recursos** estão sendo criados em.</span><span class="sxs-lookup"><span data-stu-id="b3e83-172">hello other built-in roles like **Virtual Machine Contributor** offer full management access only toohello resources indicated by hello name, regardless of hello **Resource Group** they are being created into.</span></span>

<span data-ttu-id="b3e83-173">Atribuindo Olá RBAC função interna de **colaborador da máquina Virtual** em um nível de assinatura, significa que essa função de Olá Olá atribuídos pelo usuário:</span><span class="sxs-lookup"><span data-stu-id="b3e83-173">Assigning hello built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that hello user assigned hello role:</span></span>

* <span data-ttu-id="b3e83-174">Pode exibir todas as máquinas virtuais independentemente suas implantação data e hello grupos de recursos fazem parte do</span><span class="sxs-lookup"><span data-stu-id="b3e83-174">Can view all virtual machines regardless their deployment date and hello resource groups they are part of</span></span>
* <span data-ttu-id="b3e83-175">Tem gerenciamento completo acessar toohello as máquinas virtuais na assinatura Olá</span><span class="sxs-lookup"><span data-stu-id="b3e83-175">Has full management access toohello virtual machines in hello subscription</span></span>
* <span data-ttu-id="b3e83-176">Não é possível exibir outros tipos de recursos na assinatura Olá</span><span class="sxs-lookup"><span data-stu-id="b3e83-176">Can't view any other resource types in hello subscription</span></span>
* <span data-ttu-id="b3e83-177">Não é possível operar nenhuma alteração de uma perspectiva de cobrança</span><span class="sxs-lookup"><span data-stu-id="b3e83-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="b3e83-178">RBAC sendo um recurso somente do portal do Azure, ele não concede o portal clássico do acesso toohello.</span><span class="sxs-lookup"><span data-stu-id="b3e83-178">RBAC being an Azure portal only feature, it doesn't grant access toohello classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a><span data-ttu-id="b3e83-179">Atribuir um usuário externo interno do RBAC função tooan</span><span class="sxs-lookup"><span data-stu-id="b3e83-179">Assign a built-in RBAC role tooan external user</span></span>
<span data-ttu-id="b3e83-180">Para um cenário diferente nesse teste, Olá usuário externo "alflanigan@gmail.com" é adicionado como um **colaborador da máquina Virtual**.</span><span class="sxs-lookup"><span data-stu-id="b3e83-180">For a different scenario in this test, hello external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![função interna de colaborador de máquina virtual](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="b3e83-182">comportamento de saudação normal para este usuário externo com essa função interna é toosee e gerenciar somente as máquinas virtuais e seu adjacentes Gerenciador de recursos somente recursos necessário durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="b3e83-182">hello normal behavior for this external user with this built-in role is toosee and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="b3e83-183">Por design, essas funções limitadas oferecem acesso apenas tootheir correspondente de recursos criados no hello portal do Azure, independentemente alguns ainda podem ser implantados no portal clássico Olá também (por exemplo: máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="b3e83-183">By design, these limited roles offer access only tootheir correspondent resources created in hello Azure portal, regardless some can still be deployed in hello classic portal as well (for example: virtual machines).</span></span>





![visão geral da função de colaborador de máquina virtual no portal do azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a><span data-ttu-id="b3e83-185">Conceda acesso em um nível de assinatura para um usuário no hello mesmo diretório</span><span class="sxs-lookup"><span data-stu-id="b3e83-185">Grant access at a subscription level for a user in hello same directory</span></span>
<span data-ttu-id="b3e83-186">fluxo do processo de saudação é um usuário externo, da função RBAC do Olá administrador perspectiva concessão hello, bem como sendo concedida a função de toohello de acesso de usuário de saudação do tooadding idêntico.</span><span class="sxs-lookup"><span data-stu-id="b3e83-186">hello process flow is identical tooadding an external user, both from hello admin perspective granting hello RBAC role as well as hello user being granted access toohello role.</span></span> <span data-ttu-id="b3e83-187">diferença de Olá aqui é que o usuário Olá convidado não receberão qualquer convites de email como todos os escopos de recurso Olá em assinatura Olá estarão disponíveis no painel de saudação depois de entrar.</span><span class="sxs-lookup"><span data-stu-id="b3e83-187">hello difference here is that hello invited user will not receive any email invitations as all hello resource scopes within hello subscription will be available in hello dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a><span data-ttu-id="b3e83-188">Atribuir funções RBAC no escopo do grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="b3e83-188">Assign RBAC roles at hello resource group scope</span></span>
<span data-ttu-id="b3e83-189">Atribuir uma função RBAC em um **grupo de recursos** escopo tem um processo idêntico para atribuição de função hello no nível de assinatura de saudação para ambos os tipos de usuários - externos ou internos (parte do hello mesmo diretório).</span><span class="sxs-lookup"><span data-stu-id="b3e83-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning hello role at hello subscription level, for both types of users - either external or internal (part of hello same directory).</span></span> <span data-ttu-id="b3e83-190">Olá usuários que recebem a função RBAC Olá é toosee em seu ambiente somente o grupo de recursos de saudação eles tiverem recebido acesso de saudação **grupos de recursos** ícone Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e83-190">hello users which are assigned hello RBAC role is toosee in their environment only hello resource group they have been assigned access from hello **Resource Groups** icon in hello Azure portal.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-scope"></a><span data-ttu-id="b3e83-191">Atribuir funções RBAC no escopo do recurso Olá</span><span class="sxs-lookup"><span data-stu-id="b3e83-191">Assign RBAC roles at hello resource scope</span></span>
<span data-ttu-id="b3e83-192">Atribuir uma função RBAC em um escopo de recursos no Azure tem um processo idêntico para atribuição de função hello no nível de assinatura de saudação ou no nível do grupo de recursos de hello, seguinte Olá mesmo fluxo de trabalho para os dois cenários.</span><span class="sxs-lookup"><span data-stu-id="b3e83-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning hello role at hello subscription level or at hello resource group level, following hello same workflow for both scenarios.</span></span> <span data-ttu-id="b3e83-193">Novamente, usuários Olá que recebem a função RBAC Olá podem ver apenas os itens de saudação que eles tiverem recebido acesso para qualquer Olá em **todos os recursos** guia ou diretamente em seu painel.</span><span class="sxs-lookup"><span data-stu-id="b3e83-193">Again, hello users which are assigned hello RBAC role can see only hello items that they have been assigned access to, either in hello **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="b3e83-194">É um aspecto importante para RBAC no escopo do grupo de recursos ou o escopo do recurso para o diretório correto do hello usuários toomake toohello se toosign-in.</span><span class="sxs-lookup"><span data-stu-id="b3e83-194">An important aspect for RBAC both at resource group scope or resource scope is for hello users toomake sure toosign-in toohello correct directory.</span></span>





![logon do diretório no portal do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="b3e83-196">Atribuir funções de RBAC a um grupo do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b3e83-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="b3e83-197">Todos os cenários de saudação usando o RBAC em três escopos diferentes Olá na oferta do Azure privilégio de saudação de gerenciar, implantar e administrar vários recursos como um usuário atribuído sem Olá necessário do gerenciamento de uma assinatura pessoal.</span><span class="sxs-lookup"><span data-stu-id="b3e83-197">All hello scenarios using RBAC at hello three different scopes in Azure offer hello privilege of managing, deploying and administering various resources as an assigned user without hello need of managing a personal subscription.</span></span> <span data-ttu-id="b3e83-198">Função RBAC Olá independentemente é atribuída a uma assinatura, o grupo de recursos ou o escopo do recurso, todos os recursos de saudação criados mais adiante por usuários Olá atribuído são cobrados em Olá uma assinatura do Azure em que usuários de saudação têm acesso a.</span><span class="sxs-lookup"><span data-stu-id="b3e83-198">Regardless hello RBAC role is assigned for a subscription, resource group or resource scope, all hello resources created further on by hello assigned users are billed under hello one Azure subscription where hello users have access to.</span></span> <span data-ttu-id="b3e83-199">Dessa forma, hello usuários com permissões de administrador para essa assinatura do Azure inteira de cobrança tem uma visão geral completa consumo hello, independentemente de quem está gerenciando recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3e83-199">This way, hello users who have billing administrator permissions for that entire Azure subscription has a complete overview on hello consumption, regardless who is managing hello resources.</span></span>

<span data-ttu-id="b3e83-200">Para organizações maiores, funções RBAC podem ser aplicadas no hello mesma forma para grupos do Active Directory do Azure considerando perspectiva Olá usuário Olá administrador quer acesso granular de saudação toogrant para equipes ou departamentos inteiros, não individualmente para cada usuário, assim considerá-lo como muito tempo e o gerenciamento eficiente opção.</span><span class="sxs-lookup"><span data-stu-id="b3e83-200">For larger organizations, RBAC roles can be applied in hello same way for Azure Active Directory groups considering hello perspective that hello admin user wants toogrant hello granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="b3e83-201">tooillustrate neste exemplo, a saudação **Colaborador** função foi adicionada tooone dos grupos de saudação locatário Olá no nível de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3e83-201">tooillustrate this example, hello **Contributor** role has been added tooone of hello groups in hello tenant at hello subscription level.</span></span>





![adicionar função de RBAC a grupos do AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="b3e83-203">Esses grupos são grupos de segurança provisionados e gerenciados somente dentro do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b3e83-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a><span data-ttu-id="b3e83-204">Criar um suporte de tooopen função RBAC personalizado solicitações usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3e83-204">Create a custom RBAC role tooopen support requests using PowerShell</span></span>
<span data-ttu-id="b3e83-205">funções RBAC internas Olá que estão disponíveis no Azure Verifique determinados níveis de permissão com base nos recursos disponíveis Olá ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="b3e83-205">hello built-in RBAC roles which are available in Azure ensure certain permission levels based on hello available resources in hello environment.</span></span> <span data-ttu-id="b3e83-206">No entanto, se nenhuma dessas funções atenderem às necessidades do usuário do administrador Olá, há acesso toolimit de opção de saudação ainda mais com a criação de funções RBAC personalizadas.</span><span class="sxs-lookup"><span data-stu-id="b3e83-206">However, if none of these roles suit hello admin user's needs, there is hello option toolimit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="b3e83-207">Criar funções personalizadas de RBAC requer tootake uma função interna, editá-lo e, em seguida, importá-lo novamente no ambiente de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3e83-207">Creating custom RBAC roles requires tootake one built-in role, edit it and then import it back in hello environment.</span></span> <span data-ttu-id="b3e83-208">download de saudação e o carregamento da função hello são gerenciados usando o PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="b3e83-208">hello download and upload of hello role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="b3e83-209">É importante toounderstand Olá pré-requisitos de criação de uma função personalizada que podem conceder acesso granular no nível de assinatura hello e também permitir flexibilidade de Olá Olá convidado usuário de abrir solicitações de suporte.</span><span class="sxs-lookup"><span data-stu-id="b3e83-209">It is important toounderstand hello prerequisites of creating a custom role which can grant granular access at hello subscription level and also allow hello invited user hello flexibility of opening support requests.</span></span>

<span data-ttu-id="b3e83-210">Para essa função interna do exemplo hello **leitor** que permite aos usuários acesso tooview todos os recursos de saudação escopos mas não tooedit-los ou criar novos foi personalizada a opção de saudação de usuário tooallow Olá de abertura de solicitações de suporte.</span><span class="sxs-lookup"><span data-stu-id="b3e83-210">For this example hello built-in role **Reader** which allows users access tooview all hello resource scopes but not tooedit them or create new ones has been customized tooallow hello user hello option of opening support requests.</span></span>

<span data-ttu-id="b3e83-211">Olá a primeira ação de exportação Olá **leitor** função necessidades toobe concluída no PowerShell é executado com permissões elevadas como administrador.</span><span class="sxs-lookup"><span data-stu-id="b3e83-211">hello first action of exporting hello **Reader** role needs toobe completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Captura de tela do PowerShell para a função do RBAC de Leitor](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="b3e83-213">Você precisa tooextract modelo JSON Olá da função hello.</span><span class="sxs-lookup"><span data-stu-id="b3e83-213">Then you need tooextract hello JSON template of hello role.</span></span>





![Modelo JSON para a função do RBAC de Leitor personalizada](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="b3e83-215">Uma função RBAC típica é composta por três seções principais, **Actions**, **NotActions** e **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="b3e83-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="b3e83-216">Em Olá **ação** seção são listadas todas Olá operações permitidas para essa função.</span><span class="sxs-lookup"><span data-stu-id="b3e83-216">In hello **Action** section are listed all hello permitted operations for this role.</span></span> <span data-ttu-id="b3e83-217">É importante toounderstand que cada ação é atribuída de um provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="b3e83-217">It's important toounderstand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="b3e83-218">Nesse caso, para a criação de saudação de tíquetes de suporte **verificação** provedor de recursos deve ser listado.</span><span class="sxs-lookup"><span data-stu-id="b3e83-218">In this case, for creating support tickets hello **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="b3e83-219">toosee capaz de toobe todos Olá provedores de recursos disponíveis e registrados em sua assinatura, você pode usar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3e83-219">toobe able toosee all hello resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="b3e83-220">Além disso, você pode verificar Olá todos Olá disponível PowerShell cmdlets toomanage Olá provedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="b3e83-220">Additionally, you can check for hello all hello available PowerShell cmdlets toomanage hello resource providers.</span></span>
    <span data-ttu-id="b3e83-221">![Captura de tela do PowerShell para gerenciamento do provedor de recursos](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="b3e83-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="b3e83-222">toorestrict todos Olá ações para uma função específica do RBAC, recurso provedores são listados na seção Olá **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="b3e83-222">toorestrict all hello actions for a particular RBAC role, resource providers are listed under hello section **NotActions**.</span></span>
<span data-ttu-id="b3e83-223">Por último, é obrigatório para que essa função RBAC Olá contém assinatura explícita de saudação IDs onde ele é usado.</span><span class="sxs-lookup"><span data-stu-id="b3e83-223">Last, it's mandatory that hello RBAC role contains hello explicit subscription IDs where it is used.</span></span> <span data-ttu-id="b3e83-224">Olá IDs de assinatura são listados na Olá **AssignableScopes**, caso contrário, você não poderá ser tooimport função de saudação em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b3e83-224">hello subscription IDs are listed under hello **AssignableScopes**, otherwise you will not be allowed tooimport hello role in your subscription.</span></span>

<span data-ttu-id="b3e83-225">Depois de criar e personalizar a função RBAC hello, ele precisa toobe ambiente de saudação back importados.</span><span class="sxs-lookup"><span data-stu-id="b3e83-225">After creating and customizing hello RBAC role, it needs toobe imported back hello environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="b3e83-226">Neste exemplo, nome de saudação personalizado para essa função RBAC é "leitor suporte tíquetes nível de acesso" permitindo Olá usuário tooview tudo na assinatura hello e também tooopen solicitações de suporte.</span><span class="sxs-lookup"><span data-stu-id="b3e83-226">In this example, hello custom name for this RBAC role is "Reader support tickets access level" allowing hello user tooview everything in hello subscription and also tooopen support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="b3e83-227">Olá apenas duas funções RBAC internas, permitindo que a ação de saudação de abertura de solicitações de suporte são **proprietário** e **Colaborador**.</span><span class="sxs-lookup"><span data-stu-id="b3e83-227">hello only two built-in RBAC roles allowing hello action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="b3e83-228">Um toobe tooopen capaz de suporte para solicitações de usuário, ele deve receber uma função RBAC somente no escopo de assinatura de hello, porque todas as solicitações de suporte são criadas com base em uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e83-228">For a user toobe able tooopen support requests, he must be assigned an RBAC role only at hello subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="b3e83-229">Essa nova função personalizada foi atribuída a usuário tooan Olá mesmo diretório.</span><span class="sxs-lookup"><span data-stu-id="b3e83-229">This new custom role has been assigned tooan user from hello same directory.</span></span>





![captura de tela de função personalizada de RBAC importada Olá portal do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![captura de tela da atribuição personalizado importado toouser função RBAC em Olá mesmo diretório](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![captura de tela de permissões para a função de RBAC personalizada importada](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="b3e83-233">exemplo Hello foi ainda mais detalhadas tooemphasize Olá limites dessa função RBAC personalizado da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b3e83-233">hello example has been further detailed tooemphasize hello limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="b3e83-234">Pode criar novas solicitações de suporte</span><span class="sxs-lookup"><span data-stu-id="b3e83-234">Can create new support requests</span></span>
* <span data-ttu-id="b3e83-235">Não pode criar novos escopos de recursos (por exemplo: máquina virtual)</span><span class="sxs-lookup"><span data-stu-id="b3e83-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="b3e83-236">Não pode criar novos grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="b3e83-236">Can't create new resource groups</span></span>





![captura de tela de função personalizada de RBAC criando solicitações de suporte](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![captura de tela de função RBAC personalizada não é possível toocreate VMs](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![captura de tela de função RBAC personalizada não é possível toocreate RGs novo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a><span data-ttu-id="b3e83-240">Criar um suporte de tooopen função RBAC personalizado solicitações usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b3e83-240">Create a custom RBAC role tooopen support requests using Azure CLI</span></span>
<span data-ttu-id="b3e83-241">Em execução em um Mac e sem a necessidade de acesso tooPowerShell, CLI do Azure é Olá maneira toogo.</span><span class="sxs-lookup"><span data-stu-id="b3e83-241">Running on a Mac and without having access tooPowerShell, Azure CLI is hello way toogo.</span></span>

<span data-ttu-id="b3e83-242">Olá etapas toocreate uma função personalizada são Olá iguais, com exceção de único Olá que usam a CLI função hello não pode ser baixada em um modelo JSON, mas podem ser exibidas no hello CLI.</span><span class="sxs-lookup"><span data-stu-id="b3e83-242">hello steps toocreate a custom role are hello same, with hello sole exception that using CLI hello role can't be downloaded in a JSON template, but it can be viewed in hello CLI.</span></span>

<span data-ttu-id="b3e83-243">Para este exemplo eu tiver selecionado a função interna de saudação do **Backup leitor**.</span><span class="sxs-lookup"><span data-stu-id="b3e83-243">For this example I have chosen hello built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Captura de tela da CLI da função de leitor de backup mostrada](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="b3e83-245">Editar função hello no Visual Studio depois de copiar as propriedades de saudação em um modelo JSON, Olá **verificação** provedor de recursos foi adicionado no hello **ações** seções para que este usuário pode abrir solicitações de suporte enquanto continua toobe um leitor para o Cofre de backup hello.</span><span class="sxs-lookup"><span data-stu-id="b3e83-245">Editing hello role in Visual Studio after copying hello proprieties in a JSON template, hello **Microsoft.Support** resource provider has been added in hello **Actions** sections so that this user can open support requests while continuing toobe a reader for hello backup vaults.</span></span> <span data-ttu-id="b3e83-246">Novamente é ID de assinatura necessário tooadd Olá onde essa função será usada no hello **AssignableScopes** seção.</span><span class="sxs-lookup"><span data-stu-id="b3e83-246">Again it is necessary tooadd hello subscription ID where this role will be used in hello **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Captura de tela da CLI da importação da função de RBAC personalizada](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="b3e83-248">nova função de saudação agora está disponível no hello portal do Azure e o processo de atribuição de saudação é Olá mesmo como nos exemplos anteriores hello.</span><span class="sxs-lookup"><span data-stu-id="b3e83-248">hello new role is now available in hello Azure portal and hello assignation process is hello same as in hello previous examples.</span></span>





![Captura de tela do portal do Azure da função RBAC personalizada criada usando a CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="b3e83-250">A partir de saudação 2017 de compilação mais recente, Olá Shell de nuvem do Azure está disponível.</span><span class="sxs-lookup"><span data-stu-id="b3e83-250">As of hello latest Build 2017, hello Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="b3e83-251">Shell de nuvem do Azure é um complemento tooIDE e hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e83-251">Azure Cloud Shell is a complement tooIDE and hello Azure Portal.</span></span> <span data-ttu-id="b3e83-252">Com esse serviço, você obtém um shell baseado em navegador que é autenticado e hospedado no Azure e pode ser usado no lugar da CLI instalada em seu computador.</span><span class="sxs-lookup"><span data-stu-id="b3e83-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
