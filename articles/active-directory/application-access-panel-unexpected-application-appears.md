---
title: Como aplicativos aparecem no painel de acesso | Microsoft Docs
description: "Solucionar problemas relacionados a por que um aplicativo está aparecendo no Painel de Acesso"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewr: japere
ms.openlocfilehash: f8ccf2cf66b49940bc7f2b9f4764020efc04838e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-applications-appear-on-the-access-panel"></a><span data-ttu-id="3284a-103">Como aplicativos aparecem no painel de acesso</span><span class="sxs-lookup"><span data-stu-id="3284a-103">How applications appear on the access panel</span></span>

<span data-ttu-id="3284a-104">O Painel de Acesso é um portal baseado na Web que permite a um usuário com uma conta corporativa ou de estudante no Azure AD (Azure Active Directory) exibir e iniciar aplicativos baseados em nuvem aos quais o administrador do Azure AD concedeu acesso.</span><span class="sxs-lookup"><span data-stu-id="3284a-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="3284a-105">Esses aplicativos são configurados em nome do usuário no portal do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3284a-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="3284a-106">O administrador pode provisionar o aplicativo diretamente para o usuário ou para um grupo de que o usuário faz parte, o que faz com que o aplicativo apareça no Painel de Acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="3284a-106">The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="3284a-107">Problemas gerais a serem verificados primeiro</span><span class="sxs-lookup"><span data-stu-id="3284a-107">General issues to check first</span></span>

-   <span data-ttu-id="3284a-108">Se um aplicativo tiver acabado de ser removido de um usuário ou de um grupo de que o usuário faz parte, tente entrar e sair novamente do Painel de Acesso do usuário após alguns minutos para ver se o aplicativo foi removido.</span><span class="sxs-lookup"><span data-stu-id="3284a-108">If an application was just removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.</span></span>

-   <span data-ttu-id="3284a-109">Se uma licença tiver acabado de ser removida de um usuário ou de um grupo de que o usuário faz parte, isso poderá levar um longo período, dependendo do tamanho e da complexidade do grupo.</span><span class="sxs-lookup"><span data-stu-id="3284a-109">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="3284a-110">Espere mais algum tempo antes de entrar no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3284a-110">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="3284a-111">Problemas relacionados à atribuição de aplicativos para usuários</span><span class="sxs-lookup"><span data-stu-id="3284a-111">Problems related to assigning applications to users</span></span>

<span data-ttu-id="3284a-112">Um usuário pode estar vendo um aplicativo em seu Painel de Acesso por ter sido atribuído a ele anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3284a-112">A user may be seeing an application on their Access Panel because they had been previously assigned to it.</span></span> <span data-ttu-id="3284a-113">Abaixo, são descritas algumas formas de verificar:</span><span class="sxs-lookup"><span data-stu-id="3284a-113">Below are some ways to check:</span></span>

-   [<span data-ttu-id="3284a-114">Verificar se um usuário está atribuído ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="3284a-114">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="3284a-115">Verificar se um usuário está sob uma licença relacionada ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="3284a-115">Check if a user is under a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="3284a-116">Verificar se um usuário está atribuído ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="3284a-116">Check if a user is assigned to the application</span></span>

<span data-ttu-id="3284a-117">Para verificar se um usuário está atribuído ao aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="3284a-117">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="3284a-118">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3284a-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3284a-119">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="3284a-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3284a-120">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3284a-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3284a-121">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3284a-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3284a-122">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3284a-122">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="3284a-123">**Pesquise** pelo nome do aplicativo em questão.</span><span class="sxs-lookup"><span data-stu-id="3284a-123">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="3284a-124">Clique em **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3284a-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="3284a-125">Verifique se o usuário está atribuído ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3284a-125">Check to see if your user is assigned to the application.</span></span>

  * <span data-ttu-id="3284a-126">Se quiser remover o usuário do aplicativo, **clique na linha** do usuário e selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="3284a-126">If you want to remove the user from the application, **click the row** of the user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="3284a-127">Verificar se um usuário está sob uma licença relacionada ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="3284a-127">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="3284a-128">Para verificar as licenças atribuídas de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="3284a-128">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="3284a-129">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3284a-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3284a-130">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="3284a-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3284a-131">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3284a-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3284a-132">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="3284a-132">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="3284a-133">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3284a-133">click **All users**.</span></span>

6.  <span data-ttu-id="3284a-134">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="3284a-134">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="3284a-135">Clique em **Licenças** para ver quais licenças estão atribuídas ao usuário.</span><span class="sxs-lookup"><span data-stu-id="3284a-135">click **Licenses** to see which licenses the user currently has assigned.</span></span>

   * <span data-ttu-id="3284a-136">Se o usuário estiver atribuído a uma licença do Office, isso permitirá que aplicativos internos do Office apareçam no Painel de Acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="3284a-136">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="3284a-137">Problemas relacionados à atribuição de aplicativos a grupos</span><span class="sxs-lookup"><span data-stu-id="3284a-137">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="3284a-138">Um usuário pode estar vendo um aplicativo em seu Painel de Acesso por fazer parte de um grupo ao qual o aplicativo foi atribuído.</span><span class="sxs-lookup"><span data-stu-id="3284a-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="3284a-139">Abaixo, são descritas algumas formas de verificar:</span><span class="sxs-lookup"><span data-stu-id="3284a-139">Below are some ways to check:</span></span>

-   [<span data-ttu-id="3284a-140">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="3284a-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="3284a-141">Verificar se um usuário é membro de um grupo atribuído a uma licença</span><span class="sxs-lookup"><span data-stu-id="3284a-141">Check if a user is a member of a group assigned to a license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="3284a-142">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="3284a-142">Check a user’s group memberships</span></span>

<span data-ttu-id="3284a-143">Para verificar as associações de um grupo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="3284a-143">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="3284a-144">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3284a-144">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3284a-145">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="3284a-145">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3284a-146">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3284a-146">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3284a-147">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="3284a-147">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="3284a-148">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3284a-148">click **All users**.</span></span>

6.  <span data-ttu-id="3284a-149">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="3284a-149">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="3284a-150">Clique em **Grupos.**</span><span class="sxs-lookup"><span data-stu-id="3284a-150">click **Groups.**</span></span>

8.  <span data-ttu-id="3284a-151">Verifique se o usuário faz parte de um Grupo atribuído ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3284a-151">Check to see if your user is part of a Group assigned to the application.</span></span>

   * <span data-ttu-id="3284a-152">Se quiser remover o usuário do grupo, **clique na linha** do grupo e selecione excluir.</span><span class="sxs-lookup"><span data-stu-id="3284a-152">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-to-a-license"></a><span data-ttu-id="3284a-153">Verificar se um usuário é membro de um grupo atribuído a uma licença</span><span class="sxs-lookup"><span data-stu-id="3284a-153">Check if a user is a member of a group assigned to a license</span></span>

1.  <span data-ttu-id="3284a-154">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3284a-154">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3284a-155">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="3284a-155">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3284a-156">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3284a-156">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3284a-157">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="3284a-157">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="3284a-158">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3284a-158">click **All users**.</span></span>

6.  <span data-ttu-id="3284a-159">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="3284a-159">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="3284a-160">Clique em **Grupos.**</span><span class="sxs-lookup"><span data-stu-id="3284a-160">click **Groups.**</span></span>

8.  <span data-ttu-id="3284a-161">Clique na linha de um grupo específico.</span><span class="sxs-lookup"><span data-stu-id="3284a-161">click the row of a specific group.</span></span>

9.  <span data-ttu-id="3284a-162">Clique em **Licenças** para ver quais licenças o grupo atribuiu a ele.</span><span class="sxs-lookup"><span data-stu-id="3284a-162">click **Licenses** to see which licenses the group has assigned to it.</span></span>

  * <span data-ttu-id="3284a-163">Se o grupo for atribuído a uma licença do Office, isso poderá permitir que determinados aplicativos internos do Office apareçam no Painel de Acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="3284a-163">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="3284a-164">Se essas etapas de solução de problemas não resolverem o problema</span><span class="sxs-lookup"><span data-stu-id="3284a-164">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="3284a-165">Abra um tíquete de suporte com as informações a seguir, se estiverem disponíveis:</span><span class="sxs-lookup"><span data-stu-id="3284a-165">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="3284a-166">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="3284a-166">Correlation error ID</span></span>

-   <span data-ttu-id="3284a-167">UPN (endereço de email do usuário)</span><span class="sxs-lookup"><span data-stu-id="3284a-167">UPN (user email address)</span></span>

-   <span data-ttu-id="3284a-168">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="3284a-168">Tenant ID</span></span>

-   <span data-ttu-id="3284a-169">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="3284a-169">Browser type</span></span>

-   <span data-ttu-id="3284a-170">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="3284a-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="3284a-171">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="3284a-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="3284a-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3284a-172">Next steps</span></span>
[<span data-ttu-id="3284a-173">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3284a-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
