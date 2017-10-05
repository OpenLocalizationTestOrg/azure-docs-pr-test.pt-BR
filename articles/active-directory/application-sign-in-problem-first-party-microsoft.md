---
title: Problemas ao entrar em um aplicativo Microsoft | Microsoft Docs
description: "Solucionar problemas comuns enfrentados ao entrar em aplicativos primários da Microsoft usando o Azure AD (como o Office 365)"
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
ms.openlocfilehash: 5638434270ee82d2b9737ea8eed8b5a8c62f7121
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
## <a name="problems-signing-in-to-a-microsoft-application"></a><span data-ttu-id="2993c-103">Problemas ao entrar em um aplicativo Microsoft</span><span class="sxs-lookup"><span data-stu-id="2993c-103">Problems signing in to a Microsoft application</span></span>

<span data-ttu-id="2993c-104">Os aplicativos Microsoft (como o Office 365 Exchange, SharePoint, Yammer, etc.) são atribuídos e gerenciados de forma um pouco diferente dos aplicativos SaaS de terceiros ou outros aplicativos que você integra com o Azure AD para o logon único.</span><span class="sxs-lookup"><span data-stu-id="2993c-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="2993c-105">Há três principais maneiras que um usuário pode obter acesso a um aplicativo publicado Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2993c-105">There are three main ways that a user can get access to a Microsoft-published application.</span></span>

-   <span data-ttu-id="2993c-106">Para aplicativos no Office 365 ou em outros conjuntos de aplicativos pagos, os usuários têm acesso através de **atribuição de licença** diretamente à sua conta de usuário ou através de um grupo que usa nosso recurso de atribuição de licenças baseada em grupo.</span><span class="sxs-lookup"><span data-stu-id="2993c-106">For applications in the Office 365 or other paid suites, users are granted access through **license assignment** either directly to their user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="2993c-107">Para aplicativos que a Microsoft ou terceiros publicam livremente para uso de qualquer pessoa, os usuários podem ter o acesso concedido através do **consentimento do usuário**.</span><span class="sxs-lookup"><span data-stu-id="2993c-107">For applications that Microsoft or a Third Party publishes freely for anyone to use, users may be granted access through **user consent**.</span></span> <span data-ttu-id="2993c-108">Isso significa que o usuário se conecte ao aplicativo usando a conta de Estudante ou do Azure AD Work e permite acesso a um conjunto limitado de dados em sua conta.</span><span class="sxs-lookup"><span data-stu-id="2993c-108">This0 means that they sign in to the application with their Azure AD Work or School account and allow it to have access to some limited set of data on their account.</span></span>

-   <span data-ttu-id="2993c-109">Para aplicativos que a Microsoft ou terceiros publicam livremente para uso de qualquer pessoa, os usuários também podem ter o acesso concedido através do **consentimento do administrador**.</span><span class="sxs-lookup"><span data-stu-id="2993c-109">For applications that Microsoft or a 3rd Party publishes freely for anyone to use, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="2993c-110">Isso significa que um administrador determinou que o aplicativo pode ser usado por todos na organização, portanto, entram no aplicativo com uma conta de Administrador Global e concedem acesso a todos na organização.</span><span class="sxs-lookup"><span data-stu-id="2993c-110">This means that an administrator has determined the application may be used by everyone in the organization, so they sign in to the application with a Global Administrator account and grant access to everyone in the organization.</span></span>

<span data-ttu-id="2993c-111">Para solucionar o problema, inicie com as [Áreas com Problemas Gerais com o Acesso do Aplicativo a considerar](#general-problem-areas-with-application-access-to-consider) e leia o [Passo a passo: Etapas para solucionar problemas de acesso ao aplicativo Microsoft](#walkthrough-steps-to-troubleshoot-microsoft-application-access) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="2993c-111">To troubleshoot your issue, start with the [General Problem Areas with Application Access to consider](#general-problem-areas-with-application-access-to-consider) and then read the [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) to get into the details.</span></span>

## <a name="general-problem-areas-with-application-access-to-consider"></a><span data-ttu-id="2993c-112">Áreas com Problemas Gerais com o Acesso do Aplicativo a considerar</span><span class="sxs-lookup"><span data-stu-id="2993c-112">General Problem Areas with Application Access to consider</span></span>

<span data-ttu-id="2993c-113">Abaixo segue uma lista das áreas com problemas gerais que você pode analisar se tiver uma ideia de onde iniciar, mas é recomendável que leia o passo a passo para começar rapidamente: [Passo a passo: Etapas para solucionar problemas de acesso ao aplicativo Microsoft](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="2993c-113">Below is a list of the general problem areas that you can drill into if you have an idea of where to start, but we recommend you read the walkthrough to get going quickly: [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="2993c-114">Problemas com a conta do usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-114">Problems with the user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="2993c-115">Problemas com grupos</span><span class="sxs-lookup"><span data-stu-id="2993c-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="2993c-116">Problemas com políticas de acesso condicional</span><span class="sxs-lookup"><span data-stu-id="2993c-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="2993c-117">Problemas com consentimento do aplicativo</span><span class="sxs-lookup"><span data-stu-id="2993c-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-to-troubleshoot-microsoft-application-access"></a><span data-ttu-id="2993c-118">Solucionar problemas de acesso do aplicativo Microsoft</span><span class="sxs-lookup"><span data-stu-id="2993c-118">Steps to troubleshoot Microsoft Application access</span></span>

<span data-ttu-id="2993c-119">A seguir, são apresentados alguns problemas comuns que as pessoas se deparam quando seus usuários não podem entram em um aplicativo Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2993c-119">Below are some common issues folks run into when their users cannot sign in to a Microsoft application.</span></span>

-   <span data-ttu-id="2993c-120">Problemas gerais a serem primeiramente verificados</span><span class="sxs-lookup"><span data-stu-id="2993c-120">General issues to check first</span></span>

  * <span data-ttu-id="2993c-121">Certifique-se de que o usuário está entrando na **URL correta** e não em uma URL de aplicativo local.</span><span class="sxs-lookup"><span data-stu-id="2993c-121">Make sure the user is signing in to the **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="2993c-122">Certifique-se de que a conta do usuário **não está bloqueada.**</span><span class="sxs-lookup"><span data-stu-id="2993c-122">Make sure the user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="2993c-123">Certifique-se de que a**conta do usuário existe** no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2993c-123">Make sure the **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="2993c-124">Verificar se uma conta de usuário existe no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2993c-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="2993c-125">Certifique-se de que a conta do usuário está **habilitada** para entrar.</span><span class="sxs-lookup"><span data-stu-id="2993c-125">Make sure the user’s account is **enabled** for sign ins.</span></span> [<span data-ttu-id="2993c-126">Verificar o status da conta do usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-126">Check a user’s account status</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="2993c-127">Certifique-se de que a **senha do usuário não está expirada ou esquecida.**</span><span class="sxs-lookup"><span data-stu-id="2993c-127">Make sure the user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="2993c-128">[Redefinir uma senha do usuário](#reset-a-users-password) ou [Habilitar a redefinição de senha por autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="2993c-128">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="2993c-129">Certifique-se de que a **Autenticação Multifator** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="2993c-129">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="2993c-130">[Verificar o status de autenticação multifator do usuário](#check-a-users-multi-factor-authentication-status) ou [Verificar informações de contato de autenticação do usuário](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="2993c-130">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="2993c-131">Certifique-se de que uma **Política de Acesso Condicional** ou política de **Proteção de Identidade** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="2993c-131">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="2993c-132">[Verificar uma política específica de acesso condicional ](#problems-with-conditional-access-policies) ou [Verificar uma política específica de acesso condicional do aplicativo](#check-a-specific-applications-conditional-access-policy) ou [Desabilitar uma política específica de acesso condicional ](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="2993c-132">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="2993c-133">Certifique-se de que as **informações de contato de autenticação** de um usuário estão atualizadas para permitir que as políticas de Acesso Condicional ou Autenticação Multifator sejam impostas.</span><span class="sxs-lookup"><span data-stu-id="2993c-133">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span> <span data-ttu-id="2993c-134">[Verificar o status de autenticação multifator do usuário](#check-a-users-multi-factor-authentication-status) ou [Verificar informações de contato de autenticação do usuário](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="2993c-134">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="2993c-135">Para aplicativos **Microsoft** **que exigem uma licença** (como o Office365), aqui estão alguns problemas específicos para verificar após ter excluído os problemas gerais acima:</span><span class="sxs-lookup"><span data-stu-id="2993c-135">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues to check once you have ruled out the general issues above:</span></span>

   * <span data-ttu-id="2993c-136">Verifique se o usuário ou tem um **licença atribuída.**</span><span class="sxs-lookup"><span data-stu-id="2993c-136">Ensure the user or has a **license assigned.**</span></span> <span data-ttu-id="2993c-137">[Verificar as licenças atribuídas de um usuário](#check-a-users-assigned-licenses) ou [Verificar licenças atribuídas de um grupo](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="2993c-137">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="2993c-138">Se a licença estiver **atribuída a um** **grupo estático**, certifique-se de que o **usuário é um membro** desse grupo.</span><span class="sxs-lookup"><span data-stu-id="2993c-138">If the license is **assigned to a** **static group**, ensure that the **user is a member** of that group.</span></span> [<span data-ttu-id="2993c-139">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-139">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="2993c-140">Se a licença estiver **atribuída a um** **grupo dinâmico**, certifique-se de que o **regra de grupo dinâmico está definida corretamente**.</span><span class="sxs-lookup"><span data-stu-id="2993c-140">If the license is **assigned to a** **dynamic group**, ensure that the **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="2993c-141">Verificar os critérios de associação do grupo dinâmico</span><span class="sxs-lookup"><span data-stu-id="2993c-141">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="2993c-142">Se a licença estiver **atribuída a um** **grupo dinâmico**, verifique se o grupo dinâmico **terminou de processar** sua associação e se o **usuário é um membro** (isso pode demorar algum tempo).</span><span class="sxs-lookup"><span data-stu-id="2993c-142">If the license is **assigned to a** **dynamic group**, ensure that the dynamic group has **finished processing** its membership and that the **user is a member** (this can take some time).</span></span> [<span data-ttu-id="2993c-143">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-143">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="2993c-144">Após certificar-se de que a licença está atribuída, certifique-se de que a licença **não expirou**.</span><span class="sxs-lookup"><span data-stu-id="2993c-144">Once you make sure the license is assigned, make sure the license is **not expired**.</span></span>

   *  <span data-ttu-id="2993c-145">Certifique-se de que a licença é **para o aplicativo** que será acessado.</span><span class="sxs-lookup"><span data-stu-id="2993c-145">Make sure the license is **for the application** they are accessing.</span></span>

-   <span data-ttu-id="2993c-146">Para aplicativos **Microsoft** **que não exigem uma licença**, a seguir são apresentadas algumas outras opções a verificar:</span><span class="sxs-lookup"><span data-stu-id="2993c-146">For **Microsoft** **applications that don’t require a license**, here are some other things to check:</span></span>

   * <span data-ttu-id="2993c-147">Se o aplicativo estiver solicitando **permissões em nível de usuário** (por exemplo "Acesso à caixa de correio do usuário"), certifique-se de que o usuário entrou no aplicativo e executou uma **operação de consentimento de nível de usuário** para permitir que o aplicativo acesse seus dados.</span><span class="sxs-lookup"><span data-stu-id="2993c-147">If the application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that the user has signed in to the application and has performed a **user-level consent operation** to let the application access her data.</span></span>

   * <span data-ttu-id="2993c-148">Se o aplicativo estriver solicitando **permissões de administrador** (por exemplo "Acesso a caixas de correio de todos os usuários"), certifique-se de que um Administrador Global executou uma **operação de consentimento de nível de administrador em nome de todos os usuários** na organização.</span><span class="sxs-lookup"><span data-stu-id="2993c-148">If the application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in the organization.</span></span>

## <a name="problems-with-the-users-account"></a><span data-ttu-id="2993c-149">Problemas com a conta do usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-149">Problems with the user’s account</span></span>

<span data-ttu-id="2993c-150">O acesso do aplicativo pode ser bloqueado devido a um problema com um usuário atribuído ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2993c-150">Application access can be blocked due to a problem with a user that is assigned to the application.</span></span> <span data-ttu-id="2993c-151">Abaixo são apresentadas algumas maneiras para solucionar problemas e resolver problemas com usuários e suas configurações de conta:</span><span class="sxs-lookup"><span data-stu-id="2993c-151">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="2993c-152">Verificar se existe uma conta de usuário no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2993c-152">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="2993c-153">Verificar o status da conta do usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-153">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="2993c-154">Redefinir a senha de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-154">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="2993c-155">Habilitar a redefinição de senha por autoatendimento</span><span class="sxs-lookup"><span data-stu-id="2993c-155">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="2993c-156">Verificar o status da Autenticação Multifator de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-156">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="2993c-157">Verificar as informações de contato de autenticação de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-157">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="2993c-158">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-158">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="2993c-159">Verificar as licenças atribuídas de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-159">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="2993c-160">Atribuir uma licença a um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-160">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="2993c-161">Verificar se existe uma conta de usuário no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2993c-161">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="2993c-162">Para verificar se há uma conta de usuário presente, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-162">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-163">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-163">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-164">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-164">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-165">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-165">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-166">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-166">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-167">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2993c-167">click **All users**.</span></span>

6.  <span data-ttu-id="2993c-168">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-168">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="2993c-169">Verifique as propriedades do objeto do usuário para ter certeza de que elas estejam definidas conforme o esperado e de que nenhum dado esteja faltando.</span><span class="sxs-lookup"><span data-stu-id="2993c-169">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="2993c-170">Verificar o status da conta do usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-170">Check a user’s account status</span></span>

<span data-ttu-id="2993c-171">Para verificar o status da conta de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-171">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-172">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-172">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-173">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-173">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-174">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-174">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-175">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-175">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-176">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2993c-176">click **All users**.</span></span>

6.  <span data-ttu-id="2993c-177">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-177">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="2993c-178">Clique em **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="2993c-178">click **Profile**.</span></span>

8.  <span data-ttu-id="2993c-179">Em **Configurações** verifique se **Bloquear entrada** está definido como **Não**.</span><span class="sxs-lookup"><span data-stu-id="2993c-179">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="2993c-180">Redefinir a senha de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-180">Reset a user’s password</span></span>

<span data-ttu-id="2993c-181">Para redefinir a senha de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-181">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-182">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-183">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-184">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-185">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-186">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2993c-186">click **All users**.</span></span>

6.  <span data-ttu-id="2993c-187">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-187">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="2993c-188">Clique no botão **Redefinir senha** na parte superior da folha do usuário.</span><span class="sxs-lookup"><span data-stu-id="2993c-188">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="2993c-189">Clique no botão **Redefinir senha** na folha **Redefinir senha** que aparece.</span><span class="sxs-lookup"><span data-stu-id="2993c-189">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="2993c-190">Copie a **senha temporária** ou **insira uma nova senha** para o usuário.</span><span class="sxs-lookup"><span data-stu-id="2993c-190">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="2993c-191">Informe essa nova senha para o usuário, e que ele precisa alterar essa senha durante o próximo logon no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2993c-191">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="2993c-192">Habilitar a redefinição de senha por autoatendimento</span><span class="sxs-lookup"><span data-stu-id="2993c-192">Enable self-service password reset</span></span>

<span data-ttu-id="2993c-193">Para habilitar a redefinição de senhas por autoatendimento, execute as etapas de implantação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-193">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="2993c-194">Permitir que os usuários redefinam suas senhas do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2993c-194">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="2993c-195">Permitir que os usuários redefinam ou alterem suas senhas locais do Active Directory</span><span class="sxs-lookup"><span data-stu-id="2993c-195">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="2993c-196">Verificar o status da Autenticação Multifator de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-196">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="2993c-197">Para verificar o status da Autenticação Multifator de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-197">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-198">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-199">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-200">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-201">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-201">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-202">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2993c-202">click **All users**.</span></span>

6.  <span data-ttu-id="2993c-203">Clique no botão **Autenticação Multifator** na parte inferior da folha.</span><span class="sxs-lookup"><span data-stu-id="2993c-203">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="2993c-204">Após o carregamento do **Portal de Administração da Autenticação Multifator**, verifique se você está na guia **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="2993c-204">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="2993c-205">Encontre o usuário na lista de usuários pesquisando, filtrando ou classificando.</span><span class="sxs-lookup"><span data-stu-id="2993c-205">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="2993c-206">Selecione o usuário na lista de usuários e **Habilite**, **Desabilite** ou **Imponha** a autenticação multifator conforme o desejado.</span><span class="sxs-lookup"><span data-stu-id="2993c-206">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="2993c-207">**Observação**: Se um usuário estiver em estado **Imposto** defina-o temporariamente como **Desabilitado** para permitir que volte à sua conta.</span><span class="sxs-lookup"><span data-stu-id="2993c-207">**Note**: If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="2993c-208">Quando ele puder entrar novamente, altere novamente o estado para **Habilitado** para exigir o novo registro de suas informações de contato durante o próximo logon.</span><span class="sxs-lookup"><span data-stu-id="2993c-208">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="2993c-209">Como alternativa, execute as etapas em [Verificar as informações de contato de autenticação do usuário](#check-a-users-authentication-contact-info) para verificar ou definir esses dados para eles.</span><span class="sxs-lookup"><span data-stu-id="2993c-209">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="2993c-210">Verificar as informações de contato de autenticação de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-210">Check a user’s authentication contact info</span></span>

<span data-ttu-id="2993c-211">Para verificar as informações de contato de autenticação do usuário usadas para Autenticação Multifator, Acesso Condicional, Proteção de Identidade e Redefinição de Senha, execute as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-211">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-212">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-212">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-213">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-213">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-214">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-214">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-215">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-215">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-216">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2993c-216">click **All users**.</span></span>

6.  <span data-ttu-id="2993c-217">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-217">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="2993c-218">Clique em **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="2993c-218">click **Profile**.</span></span>

8.  <span data-ttu-id="2993c-219">Role a tela para baixo até **Informações de contato de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="2993c-219">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="2993c-220">**Revise** os dados registrados para o usuário e a atualização conforme o necessário.</span><span class="sxs-lookup"><span data-stu-id="2993c-220">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="2993c-221">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-221">Check a user’s group memberships</span></span>

<span data-ttu-id="2993c-222">Para verificar as associações de grupo de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-222">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-223">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-223">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-224">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-224">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-225">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-225">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-226">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-226">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-227">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2993c-227">click **All users**.</span></span>

6.  <span data-ttu-id="2993c-228">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-228">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="2993c-229">Clique em **Grupos** para ver de quais grupos o usuário é membro.</span><span class="sxs-lookup"><span data-stu-id="2993c-229">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="2993c-230">Verificar as licenças atribuídas de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-230">Check a user’s assigned licenses</span></span>

<span data-ttu-id="2993c-231">Para verificar as licenças atribuídas de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-231">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-232">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-232">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-233">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-233">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-234">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-234">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-235">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-235">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-236">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2993c-236">click **All users**.</span></span>

6.  <span data-ttu-id="2993c-237">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-237">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="2993c-238">clique em **Licenças** para ver quais licenças o usuário atribuiu atualmente.</span><span class="sxs-lookup"><span data-stu-id="2993c-238">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="2993c-239">Atribuir uma licença a um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-239">Assign a user a license</span></span> 

<span data-ttu-id="2993c-240">Para atribuir uma licença a um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-240">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-241">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-242">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-243">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-244">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-244">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-245">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2993c-245">click **All users**.</span></span>

6.  <span data-ttu-id="2993c-246">**Pesquise** pelo usuário no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-246">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="2993c-247">clique em **Licenças** para ver quais licenças o usuário atribuiu atualmente.</span><span class="sxs-lookup"><span data-stu-id="2993c-247">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="2993c-248">clique no botão **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="2993c-248">click the **Assign** button.</span></span>

9.  <span data-ttu-id="2993c-249">Selecione **um ou mais produtos** da lista de produtos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2993c-249">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="2993c-250">**Opcional** clique no item **opções de atribuição** para atribuir produtos granularmente.</span><span class="sxs-lookup"><span data-stu-id="2993c-250">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="2993c-251">Clique em **OK** quando isso for concluído.</span><span class="sxs-lookup"><span data-stu-id="2993c-251">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="2993c-252">Clique no botão **Atribuir** para atribuir essas licenças para esse usuário.</span><span class="sxs-lookup"><span data-stu-id="2993c-252">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="2993c-253">Problemas com grupos</span><span class="sxs-lookup"><span data-stu-id="2993c-253">Problems with groups</span></span>

<span data-ttu-id="2993c-254">O acesso a aplicativos pode ser bloqueado devido a um problema com um grupo atribuído ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2993c-254">Application access can be blocked due to a problem with a group that is assigned to the application.</span></span> <span data-ttu-id="2993c-255">Abaixo são apresentadas algumas maneiras para solucionar problemas com grupos e associações de grupo:</span><span class="sxs-lookup"><span data-stu-id="2993c-255">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="2993c-256">Verificar associações de um grupo</span><span class="sxs-lookup"><span data-stu-id="2993c-256">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="2993c-257">Verificar os critérios de associação do grupo dinâmico</span><span class="sxs-lookup"><span data-stu-id="2993c-257">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="2993c-258">Verificar as licenças atribuídas de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-258">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="2993c-259">Reprocessar licenças do um grupo</span><span class="sxs-lookup"><span data-stu-id="2993c-259">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="2993c-260">Atribuir uma licença a um grupo</span><span class="sxs-lookup"><span data-stu-id="2993c-260">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="2993c-261">Verificar associações de um grupo</span><span class="sxs-lookup"><span data-stu-id="2993c-261">Check a group’s membership</span></span>

<span data-ttu-id="2993c-262">Para verificar as associações de um grupo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-262">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-263">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-263">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-264">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-264">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-265">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-265">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-266">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-266">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-267">clique em **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="2993c-267">click **All groups**.</span></span>

6.  <span data-ttu-id="2993c-268">**Pesquise** pelo grupo no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-268">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="2993c-269">clique em **Membros** para examinar a lista de usuários atribuídos a esse grupo.</span><span class="sxs-lookup"><span data-stu-id="2993c-269">click **Members** to review the list of users assigned to this group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="2993c-270">Verificar os critérios de associação do grupo dinâmico</span><span class="sxs-lookup"><span data-stu-id="2993c-270">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="2993c-271">Para verificar as associações de grupo dinâmico, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-271">To check a dynamic group’s membership criteria, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-272">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-272">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-273">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-273">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-274">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-274">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-275">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-275">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-276">clique em **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="2993c-276">click **All groups**.</span></span>

6.  <span data-ttu-id="2993c-277">**Pesquise** pelo grupo no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-277">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="2993c-278">clique em **Regras de associação dinâmica.**</span><span class="sxs-lookup"><span data-stu-id="2993c-278">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="2993c-279">Analise a regra **simples** ou **avançada** definida para esse grupo e certifique-se de que o usuário que pretende ser membro deste grupo atende as esses critérios.</span><span class="sxs-lookup"><span data-stu-id="2993c-279">Review the **simple** or **advanced** rule defined for this group and ensure that the user you want to be a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="2993c-280">Verificar as licenças atribuídas de um usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-280">Check a group’s assigned licenses</span></span>

<span data-ttu-id="2993c-281">Para verificar as licenças atribuídas de um usuário, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-281">To check a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-282">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-282">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-283">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-283">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-284">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-284">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-285">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-285">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-286">clique em **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="2993c-286">click **All groups**.</span></span>

6.  <span data-ttu-id="2993c-287">**Pesquise** pelo grupo no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-287">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="2993c-288">clique em **Licenças** para ver quais licenças o grupo atribuiu atualmente.</span><span class="sxs-lookup"><span data-stu-id="2993c-288">click **Licenses** to see which licenses the group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="2993c-289">Reprocessar licenças do um grupo</span><span class="sxs-lookup"><span data-stu-id="2993c-289">Reprocess a group’s licenses</span></span>

<span data-ttu-id="2993c-290">Para reprocessar as licenças atribuídas de um usuário, execute as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-290">To reprocess a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-291">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-292">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-293">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-294">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-294">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-295">clique em **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="2993c-295">click **All groups**.</span></span>

6.  <span data-ttu-id="2993c-296">**Pesquise** pelo grupo no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-296">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="2993c-297">clique em **Licenças** para ver quais licenças o grupo atribuiu atualmente.</span><span class="sxs-lookup"><span data-stu-id="2993c-297">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="2993c-298">clique no botão **Reprocessar** para garantir que as licenças atribuídas a membros desse grupo sejam atualizadas.</span><span class="sxs-lookup"><span data-stu-id="2993c-298">click the **Reprocess** button to ensure that the licenses assigned to this group’s members are up-to-date.</span></span> <span data-ttu-id="2993c-299">Isso pode levar algum tempo, dependendo do tamanho e da complexidade do grupo.</span><span class="sxs-lookup"><span data-stu-id="2993c-299">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="2993c-300">Para fazer isso mais rápido, considere atribuir temporariamente uma licença diretamente ao usuário.</span><span class="sxs-lookup"><span data-stu-id="2993c-300">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="2993c-301">[Atribua uma licença a um usuário](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="2993c-301">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="2993c-302">Atribuir uma licença a um grupo</span><span class="sxs-lookup"><span data-stu-id="2993c-302">Assign a group a license</span></span>

<span data-ttu-id="2993c-303">Para atribuir uma licença a um grupo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2993c-303">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="2993c-304">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-304">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-305">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-305">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-306">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-306">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-307">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-307">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-308">clique em **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="2993c-308">click **All groups**.</span></span>

6.  <span data-ttu-id="2993c-309">**Pesquise** pelo grupo no qual você está interessado e **clique na linha** para selecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-309">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="2993c-310">clique em **Licenças** para ver quais licenças o grupo atribuiu atualmente.</span><span class="sxs-lookup"><span data-stu-id="2993c-310">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="2993c-311">clique no botão **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="2993c-311">click the **Assign** button.</span></span>

9.  <span data-ttu-id="2993c-312">Selecione **um ou mais produtos** da lista de produtos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2993c-312">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="2993c-313">**Opcional** clique no item **opções de atribuição** para atribuir produtos granularmente.</span><span class="sxs-lookup"><span data-stu-id="2993c-313">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="2993c-314">Clique em **OK** quando isso for concluído.</span><span class="sxs-lookup"><span data-stu-id="2993c-314">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="2993c-315">Clique no botão **Atribuir** para atribuir essas licenças para esse grupo.</span><span class="sxs-lookup"><span data-stu-id="2993c-315">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="2993c-316">Isso pode levar algum tempo, dependendo do tamanho e da complexidade do grupo.</span><span class="sxs-lookup"><span data-stu-id="2993c-316">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="2993c-317">Para fazer isso mais rápido, considere atribuir temporariamente uma licença diretamente ao usuário.</span><span class="sxs-lookup"><span data-stu-id="2993c-317">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="2993c-318">[Atribua uma licença a um usuário](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="2993c-318">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="2993c-319">Problemas com políticas de acesso condicional</span><span class="sxs-lookup"><span data-stu-id="2993c-319">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="2993c-320">Verificar uma política específica de acesso condicional</span><span class="sxs-lookup"><span data-stu-id="2993c-320">Check a specific conditional access policy</span></span>

<span data-ttu-id="2993c-321">Para verificar ou validar uma política de acesso condicional única:</span><span class="sxs-lookup"><span data-stu-id="2993c-321">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="2993c-322">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-322">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-323">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-323">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-324">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-324">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-325">clique em **Aplicativos empresariais** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-325">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-326">clique no item de navegação **Acesso condicional**.</span><span class="sxs-lookup"><span data-stu-id="2993c-326">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="2993c-327">clique na política que você pretende inspecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-327">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="2993c-328">Analise se não há condições, atribuições ou outras configurações específicas que podem estar bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="2993c-328">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="2993c-329">Talvez você queira desabilitar temporariamente essa política para garantir que ela não está afetando entradas.</span><span class="sxs-lookup"><span data-stu-id="2993c-329">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="2993c-330">Para fazer isso, defina a alternância **Habilitar política** para **Não** e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2993c-330">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="2993c-331">Verificar uma política específica de acesso condicional do aplicativo</span><span class="sxs-lookup"><span data-stu-id="2993c-331">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="2993c-332">Para verificar ou validar uma política de acesso condicional configurada atualmente de aplicativo único:</span><span class="sxs-lookup"><span data-stu-id="2993c-332">To check or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="2993c-333">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-333">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-334">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-334">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-335">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-335">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-336">clique em **Aplicativos empresariais** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-336">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-337">clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2993c-337">click **All applications**.</span></span>

6.  <span data-ttu-id="2993c-338">Procure o aplicativo de seu interesse, o usuário que está tentando entrar pelo nome de exibição do aplicativo ou ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2993c-338">Search for the application you are interested in, or the user is attempting to sign in to by application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="2993c-339">Se você não encontrar o aplicativo que está procurando, clique no botão **Filtrar** e expanda o escopo da lista para **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2993c-339">If you don’t see the application you are looking for, click the **Filter** button and expand the scope of the list to **All applications**.</span></span> <span data-ttu-id="2993c-340">Se você quiser ver mais colunas, clique no botão **Colunas** para adicionar detalhes complementares a seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2993c-340">If you want to see more columns, click the **Columns** button to add additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="2993c-341">clique no item de navegação **Acesso condicional**.</span><span class="sxs-lookup"><span data-stu-id="2993c-341">click the **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="2993c-342">clique na política que você pretende inspecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-342">click the policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="2993c-343">Analise se não há condições, atribuições ou outras configurações específicas que podem estar bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="2993c-343">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="2993c-344">Talvez você queira desabilitar temporariamente essa política para garantir que ela não está afetando entradas.</span><span class="sxs-lookup"><span data-stu-id="2993c-344">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="2993c-345">Para fazer isso, defina a alternância **Habilitar política** para **Não** e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2993c-345">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="2993c-346">Desabilitar uma política específica de acesso condicional</span><span class="sxs-lookup"><span data-stu-id="2993c-346">Disable a specific conditional access policy</span></span>

<span data-ttu-id="2993c-347">Para verificar ou validar uma política de acesso condicional única:</span><span class="sxs-lookup"><span data-stu-id="2993c-347">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="2993c-348">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2993c-348">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2993c-349">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="2993c-349">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2993c-350">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2993c-350">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2993c-351">clique em **Aplicativos empresariais** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="2993c-351">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="2993c-352">clique no item de navegação **Acesso condicional**.</span><span class="sxs-lookup"><span data-stu-id="2993c-352">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="2993c-353">clique na política que você pretende inspecionar.</span><span class="sxs-lookup"><span data-stu-id="2993c-353">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="2993c-354">Desabilite a política, configurando a alternância **Habilitar política** para **Não** e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2993c-354">Disable the policy by setting the **Enable policy** toggle to **No** and click the **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="2993c-355">Problemas com consentimento do aplicativo</span><span class="sxs-lookup"><span data-stu-id="2993c-355">Problems with application consent</span></span>

<span data-ttu-id="2993c-356">O acesso do aplicativo pode ser bloqueado porque a operação de consentimento de permissões apropriadas não ocorreu.</span><span class="sxs-lookup"><span data-stu-id="2993c-356">Application access can be blocked because the proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="2993c-357">Abaixo, são apresentadas algumas maneiras de solucionar problemas e resolver questões relacionados ao consentimento do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="2993c-357">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="2993c-358">Executar uma operação de consentimento de nível de usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-358">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="2993c-359">Executar operação de consentimento de nível de administrador para qualquer aplicativo</span><span class="sxs-lookup"><span data-stu-id="2993c-359">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="2993c-360">Executar consentimento de nível de administrador para um aplicativo de locatário único</span><span class="sxs-lookup"><span data-stu-id="2993c-360">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="2993c-361">Executar consentimento de nível de administrador para um aplicativo multilocatário</span><span class="sxs-lookup"><span data-stu-id="2993c-361">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="2993c-362">Executar uma operação de consentimento de nível de usuário</span><span class="sxs-lookup"><span data-stu-id="2993c-362">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="2993c-363">Para qualquer aplicativo habilitado para Open ID Connect que solicita permissões, navegar até a tela de entrada do aplicativo executa um consentimento de nível de usuário para o aplicativo do usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="2993c-363">For any Open ID Connect-enabled application that requests permissions, navigating to the application’s sign in screen performs a user level consent to the application for the signed-in user.</span></span>

-   <span data-ttu-id="2993c-364">Se você quiser fazer isso programaticamente, consulte [Solicitando consentimento do usuário individual](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="2993c-364">If you wish to do this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="2993c-365">Executar operação de consentimento de nível de administrador para qualquer aplicativo</span><span class="sxs-lookup"><span data-stu-id="2993c-365">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="2993c-366">Somente **para aplicativos desenvolvidos usando o modelo de aplicativo V1**, você pode forçar que esse consentimento de nível de administrador ocorra, adicionando “**?prompt=admin\_consent**” ao final da URL de entrada do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2993c-366">For **only applications developed using the V1 application model**, you can force this administrator level consent to occur by adding “**?prompt=admin\_consent**” to the end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="2993c-367">Para **qualquer aplicativo desenvolvido usando o modelo de aplicativo V2**, você pode impor que esse consentimento de nível de administrador ocorra, seguindo as instruções na seção **Solicitar permissões de um administrador de diretório** de [Usando o ponto de extremidade de consentimento do administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="2993c-367">For **any application developed using the V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="2993c-368">Executar consentimento de nível de administrador para um aplicativo de locatário único</span><span class="sxs-lookup"><span data-stu-id="2993c-368">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="2993c-369">Para **aplicativos de locatário único** que solicitam permissões (como os em desenvolvimento ou próprios da organização), é possível executar uma operação de **consentimento de nível administrativo** em nome de todos os usuários, entrando como um Administrador Global e clicando no botão **Conceder permissões** na parte superior da folha **Registro de Aplicativo -&gt; Todos os Aplicativos -&gt; Selecionar um Aplicativo -&gt; Permissões Necessárias**.</span><span class="sxs-lookup"><span data-stu-id="2993c-369">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on the **Grant permissions** button at the top of the **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="2993c-370">Para **qualquer aplicativo desenvolvido usando o modelo de aplicativo V1 ou V2**, você pode impor que esse consentimento de nível de administrador ocorra, seguindo as instruções na seção **Solicitar permissões de um administrador de diretório** de [Usando o ponto de extremidade de consentimento do administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="2993c-370">For **any application developed using the V1 or V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="2993c-371">Executar consentimento de nível de administrador para um aplicativo multilocatário</span><span class="sxs-lookup"><span data-stu-id="2993c-371">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="2993c-372">Para **Aplicativos de multilocatário** que solicitar permissões (como um aplicativo de terceiros ou desenvolvido pela Microsoft), você pode executar uma operação de **consentimento de nível administrativo**.</span><span class="sxs-lookup"><span data-stu-id="2993c-372">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="2993c-373">Entre como um Administrador Global e clique no botão **Conceder permissões** na folha **Aplicativos Empresariais -&gt; Todos os Aplicativos -&gt; Selecionar um Aplicativo -&gt; Permissões** (disponível em breve).</span><span class="sxs-lookup"><span data-stu-id="2993c-373">Sign in as a Global Administrator and clicking on the **Grant permissions** button under the **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="2993c-374">É possível impor que esse consentimento de nível de administrador ocorra, seguindo as instruções na seção **Solicitar permissões de um administrador de diretório** de [Usando o ponto de extremidade de consentimento do administrado](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="2993c-374">You can also enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2993c-375">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2993c-375">Next steps</span></span>
[<span data-ttu-id="2993c-376">Usando o ponto de extremidade de consentimento do administrador</span><span class="sxs-lookup"><span data-stu-id="2993c-376">Using the admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

