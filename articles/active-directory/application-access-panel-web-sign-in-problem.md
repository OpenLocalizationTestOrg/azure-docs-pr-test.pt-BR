---
title: aaaProblem entrando no site do painel de acesso toohello | Microsoft Docs
description: "Problemas de tootroubleshoot de diretrizes que podem ocorrer durante a tentativa de toosign em toouse Olá painel de acesso"
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
ms.reviwer: japere
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a><span data-ttu-id="36eb6-103">Problema ao entrar no site do painel de acesso toohello</span><span class="sxs-lookup"><span data-stu-id="36eb6-103">Problem signing in toohello access panel website</span></span>

<span data-ttu-id="36eb6-104">Olá painel de acesso é um portal baseado na web que permite que um usuário que tem um trabalho ou escola conta em aplicativos tooview e inicie baseado em nuvem do Azure Active Directory (AD do Azure) administrador Olá AD do Azure-los concedeu acesso ao.</span><span class="sxs-lookup"><span data-stu-id="36eb6-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="36eb6-105">Um usuário com as edições do AD do Azure também pode usar grupos de autoatendimento e recursos de gerenciamento de aplicativo por meio do painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="36eb6-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="36eb6-106">Olá painel de acesso é separado do hello portal do Azure e não exige que os usuários toohave uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="36eb6-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="36eb6-107">Os usuários podem entrar no toohello painel de acesso se tiverem uma conta corporativa ou de estudante no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="36eb6-107">Users can sign in toohello Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="36eb6-108">Os usuários podem ser autenticados diretamente no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36eb6-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="36eb6-109">Os usuários podem ser autenticados usando os Serviços de Federação do Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="36eb6-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="36eb6-110">Os usuários podem ser autenticados pelo Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36eb6-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="36eb6-111">Se um usuário possui uma assinatura do Azure ou Office 365 e estiver usando Olá portal do Azure ou um aplicativo do Office 365, eles serão capaz toouse Olá painel de acesso diretamente sem a necessidade de toosign em novamente.</span><span class="sxs-lookup"><span data-stu-id="36eb6-111">If a user has a subscription for Azure or Office 365 and has been using hello Azure portal or an Office 365 application, they'll be able toouse hello Access Panel seamlessly without needing toosign in again.</span></span> <span data-ttu-id="36eb6-112">Os usuários que não estão autenticados ser solicitada toosign no usando Olá username e password para suas contas no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="36eb6-112">Users who are not authenticated be prompted toosign in by using hello username and password for their account in Azure AD.</span></span> <span data-ttu-id="36eb6-113">Se a organização Olá configurou a federação, digitar o nome de usuário de saudação é suficiente.</span><span class="sxs-lookup"><span data-stu-id="36eb6-113">If hello organization has configured federation, typing hello username is sufficient.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="36eb6-114">Geral emite toocheck primeiro</span><span class="sxs-lookup"><span data-stu-id="36eb6-114">General issues toocheck first</span></span> 

-   <span data-ttu-id="36eb6-115">Verifique se o usuário hello está entrando toohello **corrigir URL**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="36eb6-115">Make sure hello user is signing in toohello **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="36eb6-116">Certifique-se de navegador do usuário Olá adicionou Olá URL tooits **sites confiáveis**</span><span class="sxs-lookup"><span data-stu-id="36eb6-116">Make sure hello user’s browser has added hello URL tooits **trusted sites**</span></span>

-   <span data-ttu-id="36eb6-117">Certifique-se de conta de usuário Olá **habilitado** para entradas.</span><span class="sxs-lookup"><span data-stu-id="36eb6-117">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="36eb6-118">Certifique-se de conta de usuário Olá **não bloqueada.**</span><span class="sxs-lookup"><span data-stu-id="36eb6-118">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="36eb6-119">Tornar-se de que usuário Olá **senha não está expirada ou esquecida.**</span><span class="sxs-lookup"><span data-stu-id="36eb6-119">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="36eb6-120">Verifique se a **Autenticação Multifator** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="36eb6-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="36eb6-121">Verifique se uma **Política de acesso condicional** ou política de **Proteção de Identidade** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="36eb6-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="36eb6-122">Certifique-se de que um usuário **informações de contato de autenticação** está ativo toodate tooallow autenticação multifator ou o acesso condicional políticas toobe imposta.</span><span class="sxs-lookup"><span data-stu-id="36eb6-122">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="36eb6-123">Verifique se tooalso tente eliminar os cookies do seu navegador e tentar toosign em novamente.</span><span class="sxs-lookup"><span data-stu-id="36eb6-123">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="36eb6-124">Atende aos requisitos de navegador de saudação painel de acesso</span><span class="sxs-lookup"><span data-stu-id="36eb6-124">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="36eb6-125">Olá painel de acesso requer um navegador que ofereça suporte ao JavaScript e CSS habilitou.</span><span class="sxs-lookup"><span data-stu-id="36eb6-125">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="36eb6-126">toouse baseado em senha-logon único (SSO) no hello painel de acesso, Olá extensão do painel de acesso deve ser instalado no navegador do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-126">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="36eb6-127">Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.</span><span class="sxs-lookup"><span data-stu-id="36eb6-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="36eb6-128">Para SSO baseado em senha, navegadores de saudação do usuário podem ser:</span><span class="sxs-lookup"><span data-stu-id="36eb6-128">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="36eb6-129">Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior</span><span class="sxs-lookup"><span data-stu-id="36eb6-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="36eb6-130">Edge no Windows 10 Anniversary Edition ou posterior</span><span class="sxs-lookup"><span data-stu-id="36eb6-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="36eb6-131">Chrome – No Windows 7 ou posterior e no MacOS X ou posterior</span><span class="sxs-lookup"><span data-stu-id="36eb6-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="36eb6-132">Firefox 26.0 ou posterior, no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior</span><span class="sxs-lookup"><span data-stu-id="36eb6-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-hello-users-account"></a><span data-ttu-id="36eb6-133">Problemas com a conta do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="36eb6-133">Problems with hello user’s account</span></span>

<span data-ttu-id="36eb6-134">Acesso toohello painel de acesso pode ser bloqueada devido a problema tooa com a conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="36eb6-134">Access toohello Access Panel can be blocked due tooa problem with hello user’s account.</span></span> <span data-ttu-id="36eb6-135">Veja abaixo algumas maneiras de solucionar problemas dos usuários e suas configurações de conta:</span><span class="sxs-lookup"><span data-stu-id="36eb6-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="36eb6-136">Verificar se existe uma conta de usuário no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36eb6-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="36eb6-137">Verificar o status da conta do usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="36eb6-138">Redefinir a senha de um usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="36eb6-139">Habilitar a redefinição de senha por autoatendimento</span><span class="sxs-lookup"><span data-stu-id="36eb6-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="36eb6-140">Verificar o status da Autenticação Multifator de um usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="36eb6-141">Verificar as informações de contato de autenticação de um usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="36eb6-142">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="36eb6-143">Verificar as licenças atribuídas de um usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="36eb6-144">Atribuir uma licença a um usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="36eb6-145">Verificar se existe uma conta de usuário no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36eb6-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="36eb6-146">toocheck se uma conta de usuário estiver presente, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="36eb6-146">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="36eb6-147">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="36eb6-147">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="36eb6-148">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-148">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36eb6-149">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="36eb6-149">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36eb6-150">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-150">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="36eb6-151">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="36eb6-151">click **All users**.</span></span>

6.  <span data-ttu-id="36eb6-152">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="36eb6-152">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="36eb6-153">Verifique as propriedades de saudação do hello usuário objeto toobe-se de que elas são conforme o esperado e nenhum dado está ausente.</span><span class="sxs-lookup"><span data-stu-id="36eb6-153">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="36eb6-154">Verificar o status da conta do usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-154">Check a user’s account status</span></span>

<span data-ttu-id="36eb6-155">toocheck um usuário status da conta, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="36eb6-155">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="36eb6-156">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="36eb6-156">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="36eb6-157">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-157">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36eb6-158">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="36eb6-158">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36eb6-159">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-159">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="36eb6-160">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="36eb6-160">click **All users**.</span></span>

6.  <span data-ttu-id="36eb6-161">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="36eb6-161">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="36eb6-162">Clique em **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="36eb6-162">click **Profile**.</span></span>

8.  <span data-ttu-id="36eb6-163">Em **configurações** Certifique-se de que **bloco entrar** está definido muito**não**.</span><span class="sxs-lookup"><span data-stu-id="36eb6-163">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="36eb6-164">Redefinir a senha de um usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-164">Reset a user’s password</span></span>

<span data-ttu-id="36eb6-165">tooreset a senha do usuário, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="36eb6-165">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="36eb6-166">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="36eb6-166">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="36eb6-167">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-167">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36eb6-168">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="36eb6-168">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36eb6-169">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-169">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="36eb6-170">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="36eb6-170">click **All users**.</span></span>

6.  <span data-ttu-id="36eb6-171">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="36eb6-171">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="36eb6-172">Clique em Olá **Redefinir senha** botão na parte superior de saudação da folha de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-172">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="36eb6-173">Clique em hello **Redefinir senha** botão Olá **Redefinir senha** folha que aparece.</span><span class="sxs-lookup"><span data-stu-id="36eb6-173">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="36eb6-174">Saudação de cópia **senha temporária** ou **insira uma nova senha** para usuário hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-174">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="36eb6-175">Se comunicar esse novo usuário toohello senha, eles toochange necessária essa senha durante o próximo entrar tooAzure do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36eb6-175">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="36eb6-176">Habilitar a redefinição de senha por autoatendimento</span><span class="sxs-lookup"><span data-stu-id="36eb6-176">Enable self-service password reset</span></span>

<span data-ttu-id="36eb6-177">senha de autoatendimento tooenable redefinir, execute as etapas de implantação de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="36eb6-177">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="36eb6-178">Habilitar os usuários tooreset suas senhas do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="36eb6-178">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="36eb6-179">Habilitar os usuários tooreset ou alterar suas senhas do Active Directory local</span><span class="sxs-lookup"><span data-stu-id="36eb6-179">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="36eb6-180">Verificar o status da Autenticação Multifator de um usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="36eb6-181">toocheck um usuário do multi-factor status de autenticação seguem Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="36eb6-181">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="36eb6-182">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="36eb6-182">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="36eb6-183">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-183">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36eb6-184">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="36eb6-184">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36eb6-185">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-185">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="36eb6-186">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="36eb6-186">click **All users**.</span></span>

6.  <span data-ttu-id="36eb6-187">Clique em Olá **multi-Factor Authentication** botão na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="36eb6-187">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="36eb6-188">Uma vez Olá **Portal de administração do multi-Factor Authentication** cargas, certifique-se você estiver usando Olá **usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="36eb6-188">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="36eb6-189">Localize usuário Olá Olá lista de usuários por pesquisa, filtragem ou classificação.</span><span class="sxs-lookup"><span data-stu-id="36eb6-189">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="36eb6-190">Usuário Olá selecione da lista de saudação de usuários e **habilitar**, **desabilitar**, ou **impor** autenticação multifator conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="36eb6-190">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="36eb6-191">Se um usuário estiver em um **imposto** de estado, você pode defini-las muito**desabilitado** temporariamente toolet-los de volta para sua conta.</span><span class="sxs-lookup"><span data-stu-id="36eb6-191">If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="36eb6-192">Quando eles forem novamente, você pode alterar seu estado muito**habilitado** novamente toorequire-los entre suas informações de contato durante o próximo registro de toore.</span><span class="sxs-lookup"><span data-stu-id="36eb6-192">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="36eb6-193">Como alternativa, você pode seguir etapas Olá Olá [Verifique informações de contato de autenticação do usuário](#check-a-users-authentication-contact-info) tooverify ou defina esses dados para eles.</span><span class="sxs-lookup"><span data-stu-id="36eb6-193">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="36eb6-194">Verificar as informações de contato de autenticação de um usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="36eb6-195">toocheck autenticação do usuário entre em contato com informações usadas para autenticação multifator, acesso condicional, proteção de identidade e de redefinição de senha, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="36eb6-195">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="36eb6-196">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="36eb6-196">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="36eb6-197">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-197">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36eb6-198">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="36eb6-198">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36eb6-199">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-199">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="36eb6-200">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="36eb6-200">click **All users**.</span></span>

6.  <span data-ttu-id="36eb6-201">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="36eb6-201">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="36eb6-202">Clique em **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="36eb6-202">click **Profile**.</span></span>

8.  <span data-ttu-id="36eb6-203">Role para baixo demais**informações de contato de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="36eb6-203">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="36eb6-204">**Revisão** dados saudação registrado para o usuário hello e atualização conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="36eb6-204">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="36eb6-205">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-205">Check a user’s group memberships</span></span>

<span data-ttu-id="36eb6-206">toocheck um usuário as associações de grupo, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="36eb6-206">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="36eb6-207">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="36eb6-207">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="36eb6-208">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-208">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36eb6-209">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="36eb6-209">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36eb6-210">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-210">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="36eb6-211">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="36eb6-211">click **All users**.</span></span>

6.  <span data-ttu-id="36eb6-212">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="36eb6-212">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="36eb6-213">Clique em **grupos** toosee que agrupa usuário Olá é membro.</span><span class="sxs-lookup"><span data-stu-id="36eb6-213">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="36eb6-214">Verificar as licenças atribuídas de um usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="36eb6-215">toocheck um usuário atribuído licenças, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="36eb6-215">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="36eb6-216">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="36eb6-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="36eb6-217">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36eb6-218">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="36eb6-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36eb6-219">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-219">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="36eb6-220">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="36eb6-220">click **All users**.</span></span>

6.  <span data-ttu-id="36eb6-221">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="36eb6-221">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="36eb6-222">Clique em **licenças** toosee quais licenças Olá atualmente atribuída ao usuário.</span><span class="sxs-lookup"><span data-stu-id="36eb6-222">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="36eb6-223">Atribuir uma licença a um usuário</span><span class="sxs-lookup"><span data-stu-id="36eb6-223">Assign a user a license</span></span> 

<span data-ttu-id="36eb6-224">tooassign um usuário de tooa de licença, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="36eb6-224">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="36eb6-225">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="36eb6-225">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="36eb6-226">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-226">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36eb6-227">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="36eb6-227">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36eb6-228">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="36eb6-228">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="36eb6-229">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="36eb6-229">click **All users**.</span></span>

6.  <span data-ttu-id="36eb6-230">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="36eb6-230">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="36eb6-231">Clique em **licenças** toosee quais licenças Olá atualmente atribuída ao usuário.</span><span class="sxs-lookup"><span data-stu-id="36eb6-231">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="36eb6-232">Clique em Olá **atribuir** botão.</span><span class="sxs-lookup"><span data-stu-id="36eb6-232">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="36eb6-233">Selecione **um ou mais produtos** da lista de saudação de produtos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="36eb6-233">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="36eb6-234">**Opcional** clique Olá **opções atribuição** item toogranularly atribuir produtos.</span><span class="sxs-lookup"><span data-stu-id="36eb6-234">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="36eb6-235">Clique em **OK** quando isso for concluído.</span><span class="sxs-lookup"><span data-stu-id="36eb6-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="36eb6-236">Clique em Olá **atribuir** botão tooassign usuário de toothis essas licenças.</span><span class="sxs-lookup"><span data-stu-id="36eb6-236">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="36eb6-237">Se essas etapas de solução de problemas não resolver o problema de saudação</span><span class="sxs-lookup"><span data-stu-id="36eb6-237">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="36eb6-238">Abra um tíquete de suporte com hello informações a seguir se disponíveis:</span><span class="sxs-lookup"><span data-stu-id="36eb6-238">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="36eb6-239">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="36eb6-239">Correlation error ID</span></span>

-   <span data-ttu-id="36eb6-240">UPN (endereço de email do usuário)</span><span class="sxs-lookup"><span data-stu-id="36eb6-240">UPN (user email address)</span></span>

-   <span data-ttu-id="36eb6-241">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="36eb6-241">Tenant ID</span></span>

-   <span data-ttu-id="36eb6-242">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="36eb6-242">Browser type</span></span>

-   <span data-ttu-id="36eb6-243">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="36eb6-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="36eb6-244">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="36eb6-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="36eb6-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="36eb6-245">Next steps</span></span>
[<span data-ttu-id="36eb6-246">Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="36eb6-246">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
