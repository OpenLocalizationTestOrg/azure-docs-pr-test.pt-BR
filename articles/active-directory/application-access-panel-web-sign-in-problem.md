---
title: Problema ao entrar no site do painel de acesso | Microsoft Docs
description: "Orientação para solução de problemas que você pode encontrar ao tentar entrar e usar o Painel de Acesso"
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
ms.openlocfilehash: 28d91237adf745e591b02322de7881c8122827ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-signing-in-to-the-access-panel-website"></a><span data-ttu-id="68826-103">Problema ao entrar no site do painel de acesso</span><span class="sxs-lookup"><span data-stu-id="68826-103">Problem signing in to the access panel website</span></span>

<span data-ttu-id="68826-104">O Painel de Acesso é um portal baseado na Web que permite a um usuário que tenha uma conta corporativa ou de estudante no Azure Active Directory (Azure AD) exibir e iniciar aplicativos baseados em nuvem para os quais o administrador do Azure AD concedeu acesso.</span><span class="sxs-lookup"><span data-stu-id="68826-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="68826-105">Um usuário com as edições do Azure AD também pode usar os recursos de gerenciamento de grupo de autoatendimento e aplicativo por meio do Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="68826-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="68826-106">O Painel de Acesso é separado do Portal do Azure e não exige que os usuários tenham uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="68826-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="68826-107">Os usuários podem entrar no Painel de Acesso se eles tiverem uma conta corporativa ou de estudante no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68826-107">Users can sign in to the Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="68826-108">Os usuários podem ser autenticados diretamente no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68826-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="68826-109">Os usuários podem ser autenticados usando os Serviços de Federação do Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="68826-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="68826-110">Os usuários podem ser autenticados pelo Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68826-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="68826-111">Se um usuário tiver uma assinatura do Azure ou Office 365 e estiver usando o Portal do Azure ou um aplicativo do Office 365, ele poderá usar o Painel de Acesso sem precisar entrar novamente.</span><span class="sxs-lookup"><span data-stu-id="68826-111">If a user has a subscription for Azure or Office 365 and has been using the Azure portal or an Office 365 application, they'll be able to use the Access Panel seamlessly without needing to sign in again.</span></span> <span data-ttu-id="68826-112">Usuários não autenticados recebem uma solicitação para entrar usando o nome de usuário e a senha de sua conta no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68826-112">Users who are not authenticated be prompted to sign in by using the username and password for their account in Azure AD.</span></span> <span data-ttu-id="68826-113">Se a organização tiver configurado a federação, digitar o nome do usuário será suficiente.</span><span class="sxs-lookup"><span data-stu-id="68826-113">If the organization has configured federation, typing the username is sufficient.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="68826-114">Problemas gerais para verificar primeiro</span><span class="sxs-lookup"><span data-stu-id="68826-114">General issues to check first</span></span> 

-   <span data-ttu-id="68826-115">Verifique se o usuário está entrando com a **URL correta**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="68826-115">Make sure the user is signing in to the **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="68826-116">Verifique se o navegador do usuário adicionou a URL aos seus **sites confiáveis**</span><span class="sxs-lookup"><span data-stu-id="68826-116">Make sure the user’s browser has added the URL to its **trusted sites**</span></span>

-   <span data-ttu-id="68826-117">Verifique se a conta do usuário está **habilitada** para entradas.</span><span class="sxs-lookup"><span data-stu-id="68826-117">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="68826-118">Verifique se a conta do usuário **não está bloqueada.**</span><span class="sxs-lookup"><span data-stu-id="68826-118">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="68826-119">Verifique se a **senha do usuário não expirou ou foi esquecida.**</span><span class="sxs-lookup"><span data-stu-id="68826-119">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="68826-120">Verifique se a **Autenticação Multifator** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="68826-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="68826-121">Verifique se uma **Política de acesso condicional** ou política de **Proteção de Identidade** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="68826-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="68826-122">Verifique se as **informações de contato de autenticação** de um usuário estão atualizadas para permitir a aplicação da Autenticação Multifator ou de políticas de Acesso Condicional.</span><span class="sxs-lookup"><span data-stu-id="68826-122">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="68826-123">Tente também eliminar os cookies do navegador e tente entrar novamente.</span><span class="sxs-lookup"><span data-stu-id="68826-123">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="68826-124">Atender aos requisitos de navegador para o Painel de Acesso</span><span class="sxs-lookup"><span data-stu-id="68826-124">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="68826-125">O Painel de Acesso exige um navegador com suporte para JavaScript e CSS habilitado.</span><span class="sxs-lookup"><span data-stu-id="68826-125">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="68826-126">Para usar o SSO (logon único) baseado em senha no Painel de Acesso, a extensão do Painel de Acesso deve estar instalada no navegador do usuário.</span><span class="sxs-lookup"><span data-stu-id="68826-126">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="68826-127">Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.</span><span class="sxs-lookup"><span data-stu-id="68826-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="68826-128">Para SSO baseado em senha, os navegadores do usuário final podem ser:</span><span class="sxs-lookup"><span data-stu-id="68826-128">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="68826-129">Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior</span><span class="sxs-lookup"><span data-stu-id="68826-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="68826-130">Edge no Windows 10 Anniversary Edition ou posterior</span><span class="sxs-lookup"><span data-stu-id="68826-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="68826-131">Chrome – No Windows 7 ou posterior e no MacOS X ou posterior</span><span class="sxs-lookup"><span data-stu-id="68826-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="68826-132">Firefox 26.0 ou posterior, no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior</span><span class="sxs-lookup"><span data-stu-id="68826-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-the-users-account"></a><span data-ttu-id="68826-133">Problemas com a conta do usuário</span><span class="sxs-lookup"><span data-stu-id="68826-133">Problems with the user’s account</span></span>

<span data-ttu-id="68826-134">O acesso ao Painel de Acesso pode ser bloqueado devido a um problema com a conta do usuário.</span><span class="sxs-lookup"><span data-stu-id="68826-134">Access to the Access Panel can be blocked due to a problem with the user’s account.</span></span> <span data-ttu-id="68826-135">Veja abaixo algumas maneiras de solucionar problemas dos usuários e suas configurações de conta:</span><span class="sxs-lookup"><span data-stu-id="68826-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="68826-136">Verificar se existe uma conta de usuário no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68826-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="68826-137">Verificar o status da conta do usuário</span><span class="sxs-lookup"><span data-stu-id="68826-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="68826-138">Redefinir a senha de um usuário</span><span class="sxs-lookup"><span data-stu-id="68826-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="68826-139">Habilitar a redefinição de senha por autoatendimento</span><span class="sxs-lookup"><span data-stu-id="68826-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="68826-140">Verificar o status da Autenticação Multifator de um usuário</span><span class="sxs-lookup"><span data-stu-id="68826-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="68826-141">Verificar as informações de contato de autenticação de um usuário</span><span class="sxs-lookup"><span data-stu-id="68826-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="68826-142">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="68826-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="68826-143">Verificar as licenças atribuídas de um usuário</span><span class="sxs-lookup"><span data-stu-id="68826-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="68826-144">Atribuir uma licença a um usuário</span><span class="sxs-lookup"><span data-stu-id="68826-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="68826-145">Verificar se existe uma conta de usuário no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68826-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="68826-146">Para verificar se há uma conta de usuário presente, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="68826-146">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="68826-147">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="68826-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="68826-148">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="68826-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="68826-149">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68826-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="68826-150">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="68826-150">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="68826-151">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="68826-151">click **All users**.</span></span>

6.  <span data-ttu-id="68826-152">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="68826-152">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="68826-153">Verifique as propriedades do objeto do usuário para ter certeza de que elas estejam definidas conforme o esperado e de que nenhum dado esteja faltando.</span><span class="sxs-lookup"><span data-stu-id="68826-153">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="68826-154">Verificar o status da conta do usuário</span><span class="sxs-lookup"><span data-stu-id="68826-154">Check a user’s account status</span></span>

<span data-ttu-id="68826-155">Para verificar o status da conta de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="68826-155">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="68826-156">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="68826-156">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="68826-157">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="68826-157">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="68826-158">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68826-158">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="68826-159">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="68826-159">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="68826-160">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="68826-160">click **All users**.</span></span>

6.  <span data-ttu-id="68826-161">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="68826-161">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="68826-162">Clique em **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="68826-162">click **Profile**.</span></span>

8.  <span data-ttu-id="68826-163">Em **Configurações** verifique se **Bloquear entrada** está definido como **Não**.</span><span class="sxs-lookup"><span data-stu-id="68826-163">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="68826-164">Redefinir a senha de um usuário</span><span class="sxs-lookup"><span data-stu-id="68826-164">Reset a user’s password</span></span>

<span data-ttu-id="68826-165">Para redefinir a senha de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="68826-165">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="68826-166">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="68826-166">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="68826-167">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="68826-167">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="68826-168">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68826-168">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="68826-169">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="68826-169">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="68826-170">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="68826-170">click **All users**.</span></span>

6.  <span data-ttu-id="68826-171">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="68826-171">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="68826-172">Clique no botão **Redefinir senha** na parte superior da folha do usuário.</span><span class="sxs-lookup"><span data-stu-id="68826-172">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="68826-173">Clique no botão **Redefinir senha** na folha **Redefinir senha** que aparece.</span><span class="sxs-lookup"><span data-stu-id="68826-173">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="68826-174">Copie a **senha temporária** ou **insira uma nova senha** para o usuário.</span><span class="sxs-lookup"><span data-stu-id="68826-174">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="68826-175">Informe essa nova senha para o usuário, e que ele precisa alterar essa senha durante o próximo logon no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68826-175">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="68826-176">Habilitar a redefinição de senha por autoatendimento</span><span class="sxs-lookup"><span data-stu-id="68826-176">Enable self-service password reset</span></span>

<span data-ttu-id="68826-177">Para habilitar a redefinição de senhas por autoatendimento, execute as etapas de implantação abaixo:</span><span class="sxs-lookup"><span data-stu-id="68826-177">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="68826-178">Permitir que os usuários redefinam suas senhas do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68826-178">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="68826-179">Permitir que os usuários redefinam ou alterem suas senhas locais do Active Directory</span><span class="sxs-lookup"><span data-stu-id="68826-179">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="68826-180">Verificar o status da Autenticação Multifator de um usuário</span><span class="sxs-lookup"><span data-stu-id="68826-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="68826-181">Para verificar o status da Autenticação Multifator de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="68826-181">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="68826-182">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="68826-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="68826-183">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="68826-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="68826-184">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68826-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="68826-185">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="68826-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="68826-186">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="68826-186">click **All users**.</span></span>

6.  <span data-ttu-id="68826-187">Clique no botão **Autenticação Multifator** na parte inferior da folha.</span><span class="sxs-lookup"><span data-stu-id="68826-187">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="68826-188">Após o carregamento do **Portal de Administração da Autenticação Multifator**, verifique se você está na guia **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="68826-188">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="68826-189">Encontre o usuário na lista de usuários pesquisando, filtrando ou classificando.</span><span class="sxs-lookup"><span data-stu-id="68826-189">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="68826-190">Selecione o usuário na lista de usuários e **Habilite**, **Desabilite** ou **Imponha** a autenticação multifator conforme o desejado.</span><span class="sxs-lookup"><span data-stu-id="68826-190">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="68826-191">Se um usuário estiver em um estado **Imposto**, defina-o temporariamente como **Desabilitado** para deixá-lo entrar novamente na conta.</span><span class="sxs-lookup"><span data-stu-id="68826-191">If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="68826-192">Quando ele puder entrar novamente, altere novamente o estado para **Habilitado** para exigir o novo registro de suas informações de contato durante o próximo logon.</span><span class="sxs-lookup"><span data-stu-id="68826-192">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="68826-193">Como alternativa, execute as etapas em [Verificar as informações de contato de autenticação do usuário](#check-a-users-authentication-contact-info) para verificar ou definir esses dados para eles.</span><span class="sxs-lookup"><span data-stu-id="68826-193">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="68826-194">Verificar as informações de contato de autenticação de um usuário</span><span class="sxs-lookup"><span data-stu-id="68826-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="68826-195">Para verificar as informações de contato de autenticação do usuário usadas para Autenticação Multifator, Acesso Condicional, Proteção de Identidade e Redefinição de Senha, execute as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="68826-195">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="68826-196">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="68826-196">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="68826-197">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="68826-197">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="68826-198">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68826-198">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="68826-199">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="68826-199">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="68826-200">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="68826-200">click **All users**.</span></span>

6.  <span data-ttu-id="68826-201">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="68826-201">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="68826-202">Clique em **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="68826-202">click **Profile**.</span></span>

8.  <span data-ttu-id="68826-203">Role a tela para baixo até **Informações de contato de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="68826-203">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="68826-204">**Revise** os dados registrados para o usuário e a atualização conforme o necessário.</span><span class="sxs-lookup"><span data-stu-id="68826-204">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="68826-205">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="68826-205">Check a user’s group memberships</span></span>

<span data-ttu-id="68826-206">Para verificar as associações de grupo de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="68826-206">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="68826-207">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="68826-207">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="68826-208">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="68826-208">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="68826-209">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68826-209">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="68826-210">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="68826-210">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="68826-211">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="68826-211">click **All users**.</span></span>

6.  <span data-ttu-id="68826-212">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="68826-212">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="68826-213">Clique em **Grupos** para ver de quais grupos o usuário é membro.</span><span class="sxs-lookup"><span data-stu-id="68826-213">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="68826-214">Verificar as licenças atribuídas de um usuário</span><span class="sxs-lookup"><span data-stu-id="68826-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="68826-215">Para verificar as licenças atribuídas de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="68826-215">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="68826-216">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="68826-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="68826-217">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="68826-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="68826-218">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68826-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="68826-219">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="68826-219">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="68826-220">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="68826-220">click **All users**.</span></span>

6.  <span data-ttu-id="68826-221">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="68826-221">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="68826-222">clique em **Licenças** para ver quais licenças o usuário atribuiu atualmente.</span><span class="sxs-lookup"><span data-stu-id="68826-222">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="68826-223">Atribuir uma licença a um usuário</span><span class="sxs-lookup"><span data-stu-id="68826-223">Assign a user a license</span></span> 

<span data-ttu-id="68826-224">Para atribuir uma licença a um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="68826-224">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="68826-225">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="68826-225">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="68826-226">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="68826-226">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="68826-227">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68826-227">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="68826-228">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="68826-228">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="68826-229">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="68826-229">click **All users**.</span></span>

6.  <span data-ttu-id="68826-230">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="68826-230">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="68826-231">clique em **Licenças** para ver quais licenças o usuário atribuiu atualmente.</span><span class="sxs-lookup"><span data-stu-id="68826-231">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="68826-232">clique no botão **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="68826-232">click the **Assign** button.</span></span>

9.  <span data-ttu-id="68826-233">Selecione **um ou mais produtos** da lista de produtos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="68826-233">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="68826-234">**Opcional** clique no item **opções de atribuição** para atribuir produtos granularmente.</span><span class="sxs-lookup"><span data-stu-id="68826-234">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="68826-235">Clique em **OK** quando isso for concluído.</span><span class="sxs-lookup"><span data-stu-id="68826-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="68826-236">Clique no botão **Atribuir** para atribuir essas licenças para esse usuário.</span><span class="sxs-lookup"><span data-stu-id="68826-236">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="68826-237">Se essas etapas de solução de problemas não resolverem o problema</span><span class="sxs-lookup"><span data-stu-id="68826-237">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="68826-238">Abra um tíquete de suporte com as informações a seguir, se estiverem disponíveis:</span><span class="sxs-lookup"><span data-stu-id="68826-238">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="68826-239">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="68826-239">Correlation error ID</span></span>

-   <span data-ttu-id="68826-240">UPN (endereço de email do usuário)</span><span class="sxs-lookup"><span data-stu-id="68826-240">UPN (user email address)</span></span>

-   <span data-ttu-id="68826-241">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="68826-241">Tenant ID</span></span>

-   <span data-ttu-id="68826-242">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="68826-242">Browser type</span></span>

-   <span data-ttu-id="68826-243">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="68826-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="68826-244">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="68826-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="68826-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="68826-245">Next steps</span></span>
[<span data-ttu-id="68826-246">Fornecer logon único para seus aplicativos com Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="68826-246">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
