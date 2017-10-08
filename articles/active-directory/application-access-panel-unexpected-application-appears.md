---
title: "aplicativos aaaHow aparecem no painel de acesso Olá | Microsoft Docs"
description: "Solução de problemas que um aplicativo é exibido no painel de acesso de saudação"
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
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a><span data-ttu-id="73b18-103">Como os aplicativos aparecem no painel de acesso Olá</span><span class="sxs-lookup"><span data-stu-id="73b18-103">How applications appear on hello access panel</span></span>

<span data-ttu-id="73b18-104">Olá painel de acesso é um portal baseado na web que permite que um usuário com um trabalho ou escola conta em aplicativos tooview e início baseado em nuvem do Azure Active Directory (AD do Azure) que Olá administrador do AD do Azure tem acesso-los ao.</span><span class="sxs-lookup"><span data-stu-id="73b18-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="73b18-105">Esses aplicativos são configurados em nome de usuário de saudação no portal do Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="73b18-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="73b18-106">Olá administrador pode provisionar Olá toohello usuário do aplicativo diretamente ou tooa grupo que um usuário faz parte do resultando em um aplicativo hello que aparecem no painel de acesso do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="73b18-106">hello admin can provision hello application toohello user directly or tooa group a user is part of resulting in hello application appearing on hello user’s Access Panel.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="73b18-107">Geral emite toocheck primeiro</span><span class="sxs-lookup"><span data-stu-id="73b18-107">General issues toocheck first</span></span>

-   <span data-ttu-id="73b18-108">Se um aplicativo foi removido apenas um usuário ou grupo Olá usuário é membro de, tente toosign e sair novamente no painel de acesso do usuário Olá após toosee de alguns minutos se o aplicativo hello for removido.</span><span class="sxs-lookup"><span data-stu-id="73b18-108">If an application was just removed from a user or group hello user is a member of, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is removed.</span></span>

-   <span data-ttu-id="73b18-109">Se uma licença apenas foi removida de um usuário ou grupo Olá é que um membro deste pode levar algum tempo, dependendo do tamanho de saudação e a complexidade do grupo Olá toobe alterações feita.</span><span class="sxs-lookup"><span data-stu-id="73b18-109">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="73b18-110">Permitir tempo extra antes de entrar no painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="73b18-110">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="73b18-111">Problemas relacionados tooassigning aplicativos toousers</span><span class="sxs-lookup"><span data-stu-id="73b18-111">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="73b18-112">Um usuário pode ver um aplicativo no respectivo painel de acesso porque ele foi anteriormente atribuídos tooit.</span><span class="sxs-lookup"><span data-stu-id="73b18-112">A user may be seeing an application on their Access Panel because they had been previously assigned tooit.</span></span> <span data-ttu-id="73b18-113">Abaixo estão algumas maneiras toocheck:</span><span class="sxs-lookup"><span data-stu-id="73b18-113">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="73b18-114">Verifique se um usuário é atribuído toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="73b18-114">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="73b18-115">Verifique se um usuário está em uma licença relacionados ao aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="73b18-115">Check if a user is under a license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="73b18-116">Verifique se um usuário é atribuído toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="73b18-116">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="73b18-117">toocheck toohello aplicativo, é atribuído a um usuário siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="73b18-117">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="73b18-118">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="73b18-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="73b18-119">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="73b18-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="73b18-120">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="73b18-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="73b18-121">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="73b18-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="73b18-122">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="73b18-122">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="73b18-123">**Pesquisa** para nome de saudação do aplicativo hello em questão.</span><span class="sxs-lookup"><span data-stu-id="73b18-123">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="73b18-124">Clique em **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="73b18-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="73b18-125">Verifique toosee se o usuário é atribuído a toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="73b18-125">Check toosee if your user is assigned toohello application.</span></span>

  * <span data-ttu-id="73b18-126">Se você desejar tooremove Olá usuário do aplicativo hello, **clique linha hello** do usuário hello e selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="73b18-126">If you want tooremove hello user from hello application, **click hello row** of hello user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="73b18-127">Verifique se um usuário está em uma licença relacionados ao aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="73b18-127">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="73b18-128">toocheck um usuário atribuído licenças, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="73b18-128">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="73b18-129">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="73b18-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="73b18-130">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="73b18-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="73b18-131">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="73b18-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="73b18-132">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="73b18-132">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="73b18-133">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="73b18-133">click **All users**.</span></span>

6.  <span data-ttu-id="73b18-134">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="73b18-134">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="73b18-135">Clique em **licenças** toosee quais licenças Olá atualmente atribuída ao usuário.</span><span class="sxs-lookup"><span data-stu-id="73b18-135">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

   * <span data-ttu-id="73b18-136">Se o usuário Olá é atribuído a licença do Office tooan isso habilitar tooappear de aplicativos do Office de terceiros primeiro em Olá painel de acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="73b18-136">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="73b18-137">Problemas relacionados tooassigning aplicativos toogroups</span><span class="sxs-lookup"><span data-stu-id="73b18-137">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="73b18-138">Um usuário pode ver um aplicativo no respectivo painel de acesso porque fazem parte de um grupo que tenha sido atribuído um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="73b18-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="73b18-139">Abaixo estão algumas maneiras toocheck:</span><span class="sxs-lookup"><span data-stu-id="73b18-139">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="73b18-140">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="73b18-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="73b18-141">Verifique se um usuário for um membro de um grupo atribuído a licença tooa</span><span class="sxs-lookup"><span data-stu-id="73b18-141">Check if a user is a member of a group assigned tooa license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="73b18-142">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="73b18-142">Check a user’s group memberships</span></span>

<span data-ttu-id="73b18-143">toocheck a associação do grupo, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="73b18-143">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="73b18-144">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="73b18-144">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="73b18-145">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="73b18-145">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="73b18-146">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="73b18-146">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="73b18-147">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="73b18-147">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="73b18-148">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="73b18-148">click **All users**.</span></span>

6.  <span data-ttu-id="73b18-149">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="73b18-149">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="73b18-150">Clique em **Grupos.**</span><span class="sxs-lookup"><span data-stu-id="73b18-150">click **Groups.**</span></span>

8.  <span data-ttu-id="73b18-151">Verifique toosee se o usuário fizer parte de um aplicativo de toohello grupo atribuído.</span><span class="sxs-lookup"><span data-stu-id="73b18-151">Check toosee if your user is part of a Group assigned toohello application.</span></span>

   * <span data-ttu-id="73b18-152">Se você desejar tooremove Olá usuário do grupo de saudação **clique linha hello** do grupo de saudação e selecione Excluir.</span><span class="sxs-lookup"><span data-stu-id="73b18-152">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a><span data-ttu-id="73b18-153">Verifique se um usuário for um membro de um grupo atribuído a licença tooa</span><span class="sxs-lookup"><span data-stu-id="73b18-153">Check if a user is a member of a group assigned tooa license</span></span>

1.  <span data-ttu-id="73b18-154">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="73b18-154">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="73b18-155">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="73b18-155">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="73b18-156">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="73b18-156">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="73b18-157">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="73b18-157">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="73b18-158">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="73b18-158">click **All users**.</span></span>

6.  <span data-ttu-id="73b18-159">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="73b18-159">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="73b18-160">Clique em **Grupos.**</span><span class="sxs-lookup"><span data-stu-id="73b18-160">click **Groups.**</span></span>

8.  <span data-ttu-id="73b18-161">Clique em linha de saudação de um grupo específico.</span><span class="sxs-lookup"><span data-stu-id="73b18-161">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="73b18-162">Clique em **licenças** toosee qual grupo de licenças Olá atribuiu tooit.</span><span class="sxs-lookup"><span data-stu-id="73b18-162">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

  * <span data-ttu-id="73b18-163">Se o grupo de saudação for atribuído a licença do Office tooan em que isso pode habilitar determinado tooappear de aplicativos do Office de terceiros primeiro Olá painel de acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="73b18-163">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="73b18-164">Se essas etapas de solução de problemas Olá não resolver o problema de saudação</span><span class="sxs-lookup"><span data-stu-id="73b18-164">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="73b18-165">Abra um tíquete de suporte com hello informações a seguir se disponíveis:</span><span class="sxs-lookup"><span data-stu-id="73b18-165">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="73b18-166">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="73b18-166">Correlation error ID</span></span>

-   <span data-ttu-id="73b18-167">UPN (endereço de email do usuário)</span><span class="sxs-lookup"><span data-stu-id="73b18-167">UPN (user email address)</span></span>

-   <span data-ttu-id="73b18-168">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="73b18-168">Tenant ID</span></span>

-   <span data-ttu-id="73b18-169">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="73b18-169">Browser type</span></span>

-   <span data-ttu-id="73b18-170">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="73b18-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="73b18-171">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="73b18-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="73b18-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73b18-172">Next steps</span></span>
[<span data-ttu-id="73b18-173">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73b18-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
