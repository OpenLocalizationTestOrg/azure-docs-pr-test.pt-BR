---
title: aaaProblems entrar tooa aplicativo Microsoft | Microsoft Docs
description: Solucionar problemas enfrentados ao entrar toofirst terceiros Microsoft Applications usando o Azure AD (como o Office 365)
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a><span data-ttu-id="bfb4d-103">Problemas para entrar no tooa aplicativos Microsoft</span><span class="sxs-lookup"><span data-stu-id="bfb4d-103">Problems signing in tooa Microsoft application</span></span>

<span data-ttu-id="bfb4d-104">Os aplicativos Microsoft (como o Office 365 Exchange, SharePoint, Yammer, etc.) são atribuídos e gerenciados de forma um pouco diferente dos aplicativos SaaS de terceiros ou outros aplicativos que você integra com o Azure AD para o logon único.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="bfb4d-105">Há três maneiras principais que um usuário pode obter acesso tooa Microsoft publicou o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-105">There are three main ways that a user can get access tooa Microsoft-published application.</span></span>

-   <span data-ttu-id="bfb4d-106">Para aplicativos em Olá Office 365 ou outros pacotes pagas, os usuários terão acesso por meio de **atribuição de licença** ou diretamente tootheir conta de usuário, ou por meio de um grupo usando nosso recurso de atribuição de licença baseada em grupo.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-106">For applications in hello Office 365 or other paid suites, users are granted access through **license assignment** either directly tootheir user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="bfb4d-107">Para aplicativos que Microsoft ou uma terceira parte confiável publica livremente para qualquer pessoa toouse, os usuários podem receber acesso por meio de **consentimento do usuário**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-107">For applications that Microsoft or a Third Party publishes freely for anyone toouse, users may be granted access through **user consent**.</span></span> <span data-ttu-id="bfb4d-108">This0 significa que eles entrar no aplicativo toohello com sua conta do Azure AD ou de estudante e permitir que ele toohave acesso toosome limitada de conjunto de dados em sua conta.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-108">This0 means that they sign in toohello application with their Azure AD Work or School account and allow it toohave access toosome limited set of data on their account.</span></span>

-   <span data-ttu-id="bfb4d-109">Para aplicativos que Microsoft ou uma parte do 3º publica livremente para qualquer pessoa toouse, os usuários também podem ser concedidos acesso por meio de **consentimento do administrador**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-109">For applications that Microsoft or a 3rd Party publishes freely for anyone toouse, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="bfb4d-110">Isso significa que um administrador determinou aplicativo hello pode ser usado por todas as pessoas na organização hello, para que poderem entrar no aplicativo de toohello com uma conta de Administrador Global e conceder acesso tooeveryone na organização hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-110">This means that an administrator has determined hello application may be used by everyone in hello organization, so they sign in toohello application with a Global Administrator account and grant access tooeveryone in hello organization.</span></span>

<span data-ttu-id="bfb4d-111">tootroubleshoot seu problema, começam com hello [áreas de problemas gerais com acesso de aplicativo tooconsider](#general-problem-areas-with-application-access-to-consider) e, em seguida, ler Olá [passo a passo: etapas tootroubleshoot access do Microsoft Application](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget detalhes hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-111">tootroubleshoot your issue, start with hello [General Problem Areas with Application Access tooconsider](#general-problem-areas-with-application-access-to-consider) and then read hello [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget into hello details.</span></span>

## <a name="general-problem-areas-with-application-access-tooconsider"></a><span data-ttu-id="bfb4d-112">Áreas de problemas gerais com tooconsider de acesso do aplicativo</span><span class="sxs-lookup"><span data-stu-id="bfb4d-112">General Problem Areas with Application Access tooconsider</span></span>

<span data-ttu-id="bfb4d-113">Abaixo está uma lista de saudação áreas de problema geral que você pode analisar se você tiver uma ideia de onde toostart, mas é recomendável que você leia Olá passo a passo tooget ir rapidamente: [passo a passo: etapas tootroubleshoot access do Microsoft Application](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="bfb4d-113">Below is a list of hello general problem areas that you can drill into if you have an idea of where toostart, but we recommend you read hello walkthrough tooget going quickly: [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="bfb4d-114">Problemas com a conta do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="bfb4d-114">Problems with hello user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="bfb4d-115">Problemas com grupos</span><span class="sxs-lookup"><span data-stu-id="bfb4d-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="bfb4d-116">Problemas com políticas de acesso condicional</span><span class="sxs-lookup"><span data-stu-id="bfb4d-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="bfb4d-117">Problemas com consentimento do aplicativo</span><span class="sxs-lookup"><span data-stu-id="bfb4d-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a><span data-ttu-id="bfb4d-118">Etapas tootroubleshoot access do Microsoft Application</span><span class="sxs-lookup"><span data-stu-id="bfb4d-118">Steps tootroubleshoot Microsoft Application access</span></span>

<span data-ttu-id="bfb4d-119">Abaixo estão algumas pessoas problemas comuns encontrar quando os usuários não podem entrar no tooa aplicativos Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-119">Below are some common issues folks run into when their users cannot sign in tooa Microsoft application.</span></span>

-   <span data-ttu-id="bfb4d-120">Geral emite toocheck primeiro</span><span class="sxs-lookup"><span data-stu-id="bfb4d-120">General issues toocheck first</span></span>

  * <span data-ttu-id="bfb4d-121">Verifique se o usuário hello está entrando toohello **corrigir URL** e não é uma URL de aplicativo local.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-121">Make sure hello user is signing in toohello **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="bfb4d-122">Certifique-se de conta de usuário Olá **não bloqueada.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-122">Make sure hello user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="bfb4d-123">Verifique se Olá **conta de usuário existe** no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-123">Make sure hello **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="bfb4d-124">Verificar se existe uma conta de usuário no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfb4d-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="bfb4d-125">Certifique-se de conta de usuário Olá **habilitado** para entradas. [Verificar o status da conta do usuário](#problems-with-the-users-account)</span><span class="sxs-lookup"><span data-stu-id="bfb4d-125">Make sure hello user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)</span></span>

  * <span data-ttu-id="bfb4d-126">Tornar-se de que usuário Olá **senha não está expirada ou esquecida.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-126">Make sure hello user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="bfb4d-127">[Redefinir uma senha do usuário](#reset-a-users-password) ou [Habilitar a redefinição de senha por autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="bfb4d-127">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="bfb4d-128">Certifique-se de que a **Autenticação Multifator** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-128">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="bfb4d-129">[Verificar o status de autenticação multifator do usuário](#check-a-users-multi-factor-authentication-status) ou [Verificar informações de contato de autenticação do usuário](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="bfb4d-129">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="bfb4d-130">Certifique-se de que uma **Política de Acesso Condicional** ou política de **Proteção de Identidade** não está bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-130">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="bfb4d-131">[Verificar uma política específica de acesso condicional ](#problems-with-conditional-access-policies) ou [Verificar uma política específica de acesso condicional do aplicativo](#check-a-specific-applications-conditional-access-policy) ou [Desabilitar uma política específica de acesso condicional ](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="bfb4d-131">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="bfb4d-132">Certifique-se de que um usuário **informações de contato de autenticação** está ativo toodate tooallow autenticação multifator ou o acesso condicional políticas toobe imposta.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-132">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span> <span data-ttu-id="bfb4d-133">[Verificar o status de autenticação multifator do usuário](#check-a-users-multi-factor-authentication-status) ou [Verificar informações de contato de autenticação do usuário](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="bfb4d-133">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="bfb4d-134">Para **Microsoft** **aplicativos que exigem uma licença** (como o Office365), aqui estão alguns problemas específicos toocheck depois de verificar problemas gerais de saudação acima:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-134">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues toocheck once you have ruled out hello general issues above:</span></span>

   * <span data-ttu-id="bfb4d-135">Verifique se o usuário hello ou tem um **licença atribuída.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-135">Ensure hello user or has a **license assigned.**</span></span> <span data-ttu-id="bfb4d-136">[Verificar as licenças atribuídas de um usuário](#check-a-users-assigned-licenses) ou [Verificar licenças atribuídas de um grupo](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="bfb4d-136">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="bfb4d-137">Se a licença de saudação é **atribuído tooa** **grupo estático**, certifique-se de que Olá **usuário é um membro** desse grupo.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-137">If hello license is **assigned tooa** **static group**, ensure that hello **user is a member** of that group.</span></span> [<span data-ttu-id="bfb4d-138">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-138">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="bfb4d-139">Se a licença de saudação é **atribuído tooa** **grupo dinâmico**, certifique-se de que Olá **regra dinâmica de grupo está definida corretamente**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-139">If hello license is **assigned tooa** **dynamic group**, ensure that hello **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="bfb4d-140">Verificar os critérios de associação do grupo dinâmico</span><span class="sxs-lookup"><span data-stu-id="bfb4d-140">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="bfb4d-141">Se a licença de saudação é **atribuído tooa** **grupo dinâmico**, certifique-se de que esse grupo dinâmico Olá tem **concluir o processamento** sua associação e que hello **usuário é um membro** (Isso pode levar algum tempo).</span><span class="sxs-lookup"><span data-stu-id="bfb4d-141">If hello license is **assigned tooa** **dynamic group**, ensure that hello dynamic group has **finished processing** its membership and that hello **user is a member** (this can take some time).</span></span> [<span data-ttu-id="bfb4d-142">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="bfb4d-143">Depois que você certifique-se de saudação licença será atribuída, certifique-se de licença Olá é **não expirado**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-143">Once you make sure hello license is assigned, make sure hello license is **not expired**.</span></span>

   *  <span data-ttu-id="bfb4d-144">Certifique-se de licença Olá é **para o aplicativo hello** estão acessando.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-144">Make sure hello license is **for hello application** they are accessing.</span></span>

-   <span data-ttu-id="bfb4d-145">Para **Microsoft** **aplicativos que não requerem uma licença**, aqui estão algumas outra coisas toocheck:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-145">For **Microsoft** **applications that don’t require a license**, here are some other things toocheck:</span></span>

   * <span data-ttu-id="bfb4d-146">Se o aplicativo hello está solicitando **permissões em nível de usuário** (por exemplo "acesso a caixa de correio do usuário"), certifique-se de que o usuário Olá entrou no aplicativo toohello e executou um **operação consentimento de nível de usuário**  toolet Olá aplicativo acessar seus dados.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-146">If hello application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that hello user has signed in toohello application and has performed a **user-level consent operation** toolet hello application access her data.</span></span>

   * <span data-ttu-id="bfb4d-147">Se o aplicativo hello está solicitando **permissões de administrador** (por exemplo "acesso a caixas de correio de todos os usuários"), certifique-se de que um Administrador Global executou um **operação consentimento de nível de administrador nome de todos os usuários** na organização hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-147">If hello application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in hello organization.</span></span>

## <a name="problems-with-hello-users-account"></a><span data-ttu-id="bfb4d-148">Problemas com a conta do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="bfb4d-148">Problems with hello user’s account</span></span>

<span data-ttu-id="bfb4d-149">Acesso de aplicativo pode ser bloqueado devido a problema tooa com um usuário que é atribuído o aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-149">Application access can be blocked due tooa problem with a user that is assigned toohello application.</span></span> <span data-ttu-id="bfb4d-150">Veja abaixo algumas maneiras de solucionar problemas dos usuários e suas configurações de conta:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-150">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="bfb4d-151">Verificar se existe uma conta de usuário no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfb4d-151">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="bfb4d-152">Verificar o status da conta do usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-152">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="bfb4d-153">Redefinir a senha de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-153">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="bfb4d-154">Habilitar a redefinição de senha por autoatendimento</span><span class="sxs-lookup"><span data-stu-id="bfb4d-154">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="bfb4d-155">Verificar o status da Autenticação Multifator de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-155">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="bfb4d-156">Verificar as informações de contato de autenticação de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-156">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="bfb4d-157">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-157">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="bfb4d-158">Verificar as licenças atribuídas de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-158">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="bfb4d-159">Atribuir uma licença a um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-159">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="bfb4d-160">Verificar se existe uma conta de usuário no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfb4d-160">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="bfb4d-161">toocheck se uma conta de usuário estiver presente, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-161">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-162">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-162">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-163">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-163">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-164">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-164">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-165">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-165">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-166">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-166">click **All users**.</span></span>

6.  <span data-ttu-id="bfb4d-167">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-167">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bfb4d-168">Verifique as propriedades de saudação do hello usuário objeto toobe-se de que elas são conforme o esperado e nenhum dado está ausente.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-168">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="bfb4d-169">Verificar o status da conta do usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-169">Check a user’s account status</span></span>

<span data-ttu-id="bfb4d-170">toocheck um usuário status da conta, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-170">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-171">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-171">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-172">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-172">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-173">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-173">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-174">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-174">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-175">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-175">click **All users**.</span></span>

6.  <span data-ttu-id="bfb4d-176">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-176">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bfb4d-177">Clique em **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-177">click **Profile**.</span></span>

8.  <span data-ttu-id="bfb4d-178">Em **configurações** Certifique-se de que **bloco entrar** está definido muito**não**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-178">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="bfb4d-179">Redefinir a senha de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-179">Reset a user’s password</span></span>

<span data-ttu-id="bfb4d-180">tooreset a senha do usuário, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-180">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-181">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-181">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-182">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-182">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-183">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-183">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-184">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-184">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-185">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-185">click **All users**.</span></span>

6.  <span data-ttu-id="bfb4d-186">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-186">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bfb4d-187">Clique em Olá **Redefinir senha** botão na parte superior de saudação da folha de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-187">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="bfb4d-188">Clique em hello **Redefinir senha** botão Olá **Redefinir senha** folha que aparece.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-188">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="bfb4d-189">Saudação de cópia **senha temporária** ou **insira uma nova senha** para usuário hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-189">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="bfb4d-190">Se comunicar esse novo usuário toohello senha, eles toochange necessária essa senha durante o próximo entrar tooAzure do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-190">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="bfb4d-191">Habilitar a redefinição de senha por autoatendimento</span><span class="sxs-lookup"><span data-stu-id="bfb4d-191">Enable self-service password reset</span></span>

<span data-ttu-id="bfb4d-192">senha de autoatendimento tooenable redefinir, execute as etapas de implantação de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-192">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="bfb4d-193">Habilitar os usuários tooreset suas senhas do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="bfb4d-193">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="bfb4d-194">Habilitar os usuários tooreset ou alterar suas senhas do Active Directory local</span><span class="sxs-lookup"><span data-stu-id="bfb4d-194">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="bfb4d-195">Verificar o status da Autenticação Multifator de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-195">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="bfb4d-196">toocheck um usuário do multi-factor status de autenticação seguem Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-196">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-197">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-197">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-198">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-198">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-199">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-199">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-200">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-200">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-201">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-201">click **All users**.</span></span>

6.  <span data-ttu-id="bfb4d-202">Clique em Olá **multi-Factor Authentication** botão na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-202">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="bfb4d-203">Uma vez Olá **Portal de administração do multi-Factor Authentication** cargas, certifique-se você estiver usando Olá **usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-203">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="bfb4d-204">Localize usuário Olá Olá lista de usuários por pesquisa, filtragem ou classificação.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-204">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="bfb4d-205">Usuário Olá selecione da lista de saudação de usuários e **habilitar**, **desabilitar**, ou **impor** autenticação multifator conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-205">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="bfb4d-206">**Observação**: se um usuário estiver em um **imposto** de estado, você pode defini-las muito**desabilitado** temporariamente toolet-los de volta para sua conta.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-206">**Note**: If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="bfb4d-207">Quando eles forem novamente, você pode alterar seu estado muito**habilitado** novamente toorequire-los entre suas informações de contato durante o próximo registro de toore.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-207">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="bfb4d-208">Como alternativa, você pode seguir etapas Olá Olá [Verifique informações de contato de autenticação do usuário](#check-a-users-authentication-contact-info) tooverify ou defina esses dados para eles.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-208">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="bfb4d-209">Verificar as informações de contato de autenticação de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-209">Check a user’s authentication contact info</span></span>

<span data-ttu-id="bfb4d-210">toocheck autenticação do usuário entre em contato com informações usadas para autenticação multifator, acesso condicional, proteção de identidade e de redefinição de senha, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-210">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-211">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-211">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-212">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-212">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-213">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-213">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-214">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-214">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-215">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-215">click **All users**.</span></span>

6.  <span data-ttu-id="bfb4d-216">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-216">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bfb4d-217">Clique em **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-217">click **Profile**.</span></span>

8.  <span data-ttu-id="bfb4d-218">Role para baixo demais**informações de contato de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-218">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="bfb4d-219">**Revisão** dados saudação registrado para o usuário hello e atualização conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-219">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="bfb4d-220">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-220">Check a user’s group memberships</span></span>

<span data-ttu-id="bfb4d-221">toocheck um usuário as associações de grupo, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-221">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-222">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-222">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-223">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-223">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-224">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-224">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-225">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-225">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-226">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-226">click **All users**.</span></span>

6.  <span data-ttu-id="bfb4d-227">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-227">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bfb4d-228">Clique em **grupos** toosee que agrupa usuário Olá é membro.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-228">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="bfb4d-229">Verificar as licenças atribuídas de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-229">Check a user’s assigned licenses</span></span>

<span data-ttu-id="bfb4d-230">toocheck um usuário atribuído licenças, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-230">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-231">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-231">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-232">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-232">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-233">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-233">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-234">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-234">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-235">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-235">click **All users**.</span></span>

6.  <span data-ttu-id="bfb4d-236">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-236">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bfb4d-237">Clique em **licenças** toosee quais licenças Olá atualmente atribuída ao usuário.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-237">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="bfb4d-238">Atribuir uma licença a um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-238">Assign a user a license</span></span> 

<span data-ttu-id="bfb4d-239">tooassign um usuário de tooa de licença, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-239">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-240">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-240">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-241">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-241">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-242">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-242">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-243">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-243">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-244">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-244">click **All users**.</span></span>

6.  <span data-ttu-id="bfb4d-245">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-245">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bfb4d-246">Clique em **licenças** toosee quais licenças Olá atualmente atribuída ao usuário.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-246">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="bfb4d-247">Clique em Olá **atribuir** botão.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-247">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="bfb4d-248">Selecione **um ou mais produtos** da lista de saudação de produtos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-248">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="bfb4d-249">**Opcional** clique Olá **opções atribuição** item toogranularly atribuir produtos.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-249">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="bfb4d-250">Clique em **OK** quando isso for concluído.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-250">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="bfb4d-251">Clique em Olá **atribuir** botão tooassign usuário de toothis essas licenças.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-251">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="bfb4d-252">Problemas com grupos</span><span class="sxs-lookup"><span data-stu-id="bfb4d-252">Problems with groups</span></span>

<span data-ttu-id="bfb4d-253">Acesso de aplicativo pode ser bloqueado devido a problema tooa com um grupo que é atribuído o aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-253">Application access can be blocked due tooa problem with a group that is assigned toohello application.</span></span> <span data-ttu-id="bfb4d-254">Abaixo são apresentadas algumas maneiras para solucionar problemas com grupos e associações de grupo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-254">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="bfb4d-255">Verificar associações de um grupo</span><span class="sxs-lookup"><span data-stu-id="bfb4d-255">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="bfb4d-256">Verificar os critérios de associação do grupo dinâmico</span><span class="sxs-lookup"><span data-stu-id="bfb4d-256">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="bfb4d-257">Verificar as licenças atribuídas de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-257">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="bfb4d-258">Reprocessar licenças do um grupo</span><span class="sxs-lookup"><span data-stu-id="bfb4d-258">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="bfb4d-259">Atribuir uma licença a um grupo</span><span class="sxs-lookup"><span data-stu-id="bfb4d-259">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="bfb4d-260">Verificar associações de um grupo</span><span class="sxs-lookup"><span data-stu-id="bfb4d-260">Check a group’s membership</span></span>

<span data-ttu-id="bfb4d-261">toocheck a associação do grupo, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-261">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-262">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-262">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-263">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-263">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-264">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-264">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-265">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-265">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-266">clique em **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-266">click **All groups**.</span></span>

6.  <span data-ttu-id="bfb4d-267">**Pesquisa** para grupo de saudação que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-267">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bfb4d-268">Clique em **membros** tooreview lista de saudação de usuários atribuídos toothis grupo.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-268">click **Members** tooreview hello list of users assigned toothis group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="bfb4d-269">Verificar os critérios de associação do grupo dinâmico</span><span class="sxs-lookup"><span data-stu-id="bfb4d-269">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="bfb4d-270">toocheck critérios de associação do grupo dinâmico, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-270">toocheck a dynamic group’s membership criteria, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-271">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-271">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-272">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-272">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-273">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-273">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-274">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-274">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-275">clique em **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-275">click **All groups**.</span></span>

6.  <span data-ttu-id="bfb4d-276">**Pesquisa** para grupo de saudação que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-276">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bfb4d-277">clique em **Regras de associação dinâmica.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-277">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="bfb4d-278">Saudação de revisão **simples** ou **avançados** definida para esse grupo de regras e certifique-se de que esse usuário Olá deseja toobe um membro desse grupo atenda a esses critérios.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-278">Review hello **simple** or **advanced** rule defined for this group and ensure that hello user you want toobe a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="bfb4d-279">Verificar as licenças atribuídas de um usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-279">Check a group’s assigned licenses</span></span>

<span data-ttu-id="bfb4d-280">toocheck um grupo atribuído licenças, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-280">toocheck a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-281">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-281">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-282">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-282">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-283">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-283">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-284">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-284">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-285">clique em **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-285">click **All groups**.</span></span>

6.  <span data-ttu-id="bfb4d-286">**Pesquisa** para grupo de saudação que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-286">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bfb4d-287">Clique em **licenças** toosee qual grupo de licenças Olá atualmente tem atribuída.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-287">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="bfb4d-288">Reprocessar licenças do um grupo</span><span class="sxs-lookup"><span data-stu-id="bfb4d-288">Reprocess a group’s licenses</span></span>

<span data-ttu-id="bfb4d-289">tooreprocess um grupo atribuído licenças, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-289">tooreprocess a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-290">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-290">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-291">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-291">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-292">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-292">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-293">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-293">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-294">clique em **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-294">click **All groups**.</span></span>

6.  <span data-ttu-id="bfb4d-295">**Pesquisa** para grupo de saudação que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-295">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bfb4d-296">Clique em **licenças** toosee qual grupo de licenças Olá atualmente tem atribuída.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-296">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="bfb4d-297">Clique em Olá **reprocessar** tooensure botão que Olá membros do grupo de toothis licenças atribuídas estão atualizados.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-297">click hello **Reprocess** button tooensure that hello licenses assigned toothis group’s members are up-to-date.</span></span> <span data-ttu-id="bfb4d-298">Isso pode levar algum tempo, dependendo do tamanho de saudação e a complexidade do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-298">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="bfb4d-299">toodo isso mais rapidamente, considere temporariamente atribuir uma licença toohello usuário diretamente.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-299">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="bfb4d-300">[Atribua uma licença a um usuário](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="bfb4d-300">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="bfb4d-301">Atribuir uma licença a um grupo</span><span class="sxs-lookup"><span data-stu-id="bfb4d-301">Assign a group a license</span></span>

<span data-ttu-id="bfb4d-302">tooassign um grupo de tooa de licença, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-302">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="bfb4d-303">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-303">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-304">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-304">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-305">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-305">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-306">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-306">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-307">clique em **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-307">click **All groups**.</span></span>

6.  <span data-ttu-id="bfb4d-308">**Pesquisa** para grupo de saudação que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-308">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bfb4d-309">Clique em **licenças** toosee qual grupo de licenças Olá atualmente tem atribuída.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-309">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="bfb4d-310">Clique em Olá **atribuir** botão.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-310">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="bfb4d-311">Selecione **um ou mais produtos** da lista de saudação de produtos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-311">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="bfb4d-312">**Opcional** clique Olá **opções atribuição** item toogranularly atribuir produtos.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-312">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="bfb4d-313">Clique em **OK** quando isso for concluído.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-313">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="bfb4d-314">Clique em Olá **atribuir** botão tooassign grupo de toothis essas licenças.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-314">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="bfb4d-315">Isso pode levar algum tempo, dependendo do tamanho de saudação e a complexidade do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-315">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="bfb4d-316">toodo isso mais rapidamente, considere temporariamente atribuir uma licença toohello usuário diretamente.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-316">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="bfb4d-317">[Atribua uma licença a um usuário](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="bfb4d-317">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="bfb4d-318">Problemas com políticas de acesso condicional</span><span class="sxs-lookup"><span data-stu-id="bfb4d-318">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="bfb4d-319">Verificar uma política específica de acesso condicional</span><span class="sxs-lookup"><span data-stu-id="bfb4d-319">Check a specific conditional access policy</span></span>

<span data-ttu-id="bfb4d-320">toocheck ou validar uma política de acesso condicional:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-320">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="bfb4d-321">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-321">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-322">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-322">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-323">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-323">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-324">Clique em **aplicativos empresariais** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-324">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-325">Clique em Olá **acesso condicional** item de navegação.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-325">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="bfb4d-326">Clique em diretiva de saudação que lhe interessam inspecionar.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-326">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="bfb4d-327">Analise se não há condições, atribuições ou outras configurações específicas que podem estar bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-327">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="bfb4d-328">Você poderá desabilitar tootemporarily este tooensure de política está afetando sinal ins toodo não hello, conjunto **habilitar política** alternar muito**não** e clique em Olá **salvar** botão .</span><span class="sxs-lookup"><span data-stu-id="bfb4d-328">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="bfb4d-329">Verificar uma política específica de acesso condicional do aplicativo</span><span class="sxs-lookup"><span data-stu-id="bfb4d-329">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="bfb4d-330">toocheck ou validar a política de acesso condicional configurada atualmente de um único aplicativo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-330">toocheck or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="bfb4d-331">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-331">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-332">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-332">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-333">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-333">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-334">Clique em **aplicativos empresariais** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-334">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-335">clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-335">click **All applications**.</span></span>

6.  <span data-ttu-id="bfb4d-336">Pesquisa para o aplicativo hello está interessado, ou Olá usuário está tentando toosign no aplicativo tooby exibir a id de aplicativo ou nome.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-336">Search for hello application you are interested in, or hello user is attempting toosign in tooby application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="bfb4d-337">Se você não vir o aplicativo hello que você está procurando, clique em Olá **filtro** botão e expandir o escopo de saudação da lista de saudação muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-337">If you don’t see hello application you are looking for, click hello **Filter** button and expand hello scope of hello list too**All applications**.</span></span> <span data-ttu-id="bfb4d-338">Se você quiser toosee mais colunas, clique em Olá **colunas** botão detalhes adicionais de tooadd para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-338">If you want toosee more columns, click hello **Columns** button tooadd additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="bfb4d-339">Clique em Olá **acesso condicional** item de navegação.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-339">click hello **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="bfb4d-340">Clique em diretiva de saudação que lhe interessam inspecionar.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-340">click hello policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="bfb4d-341">Analise se não há condições, atribuições ou outras configurações específicas que podem estar bloqueando o acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-341">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="bfb4d-342">Você poderá desabilitar tootemporarily este tooensure de política está afetando sinal ins toodo não hello, conjunto **habilitar política** alternar muito**não** e clique em Olá **salvar** botão .</span><span class="sxs-lookup"><span data-stu-id="bfb4d-342">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="bfb4d-343">Desabilitar uma política específica de acesso condicional</span><span class="sxs-lookup"><span data-stu-id="bfb4d-343">Disable a specific conditional access policy</span></span>

<span data-ttu-id="bfb4d-344">toocheck ou validar uma política de acesso condicional:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-344">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="bfb4d-345">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bfb4d-345">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfb4d-346">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-346">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bfb4d-347">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-347">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfb4d-348">Clique em **aplicativos empresariais** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-348">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bfb4d-349">Clique em Olá **acesso condicional** item de navegação.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-349">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="bfb4d-350">Clique em diretiva de saudação que lhe interessam inspecionar.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-350">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="bfb4d-351">Desabilitar política Olá por configuração Olá **habilitar política** alternar muito**não** e clique em Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-351">Disable hello policy by setting hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="bfb4d-352">Problemas com consentimento do aplicativo</span><span class="sxs-lookup"><span data-stu-id="bfb4d-352">Problems with application consent</span></span>

<span data-ttu-id="bfb4d-353">Acesso de aplicativo pode ser bloqueado porque não houve Olá permissões adequadas consentimento operação.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-353">Application access can be blocked because hello proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="bfb4d-354">Abaixo, são apresentadas algumas maneiras de solucionar problemas e resolver questões relacionados ao consentimento do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="bfb4d-354">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="bfb4d-355">Executar uma operação de consentimento de nível de usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-355">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="bfb4d-356">Executar operação de consentimento de nível de administrador para qualquer aplicativo</span><span class="sxs-lookup"><span data-stu-id="bfb4d-356">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="bfb4d-357">Executar consentimento de nível de administrador para um aplicativo de locatário único</span><span class="sxs-lookup"><span data-stu-id="bfb4d-357">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="bfb4d-358">Executar consentimento de nível de administrador para um aplicativo multilocatário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-358">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="bfb4d-359">Executar uma operação de consentimento de nível de usuário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-359">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="bfb4d-360">Para qualquer aplicativo habilitado para abrir conexão de ID que solicita permissões, navegar a tela de entrada do aplicativo toohello executa um aplicativo de toohello de nível de consentimento do usuário para o usuário conectado hello.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-360">For any Open ID Connect-enabled application that requests permissions, navigating toohello application’s sign in screen performs a user level consent toohello application for hello signed-in user.</span></span>

-   <span data-ttu-id="bfb4d-361">Se você desejar toodo isso programaticamente, consulte [solicita o consentimento do usuário individual](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="bfb4d-361">If you wish toodo this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="bfb4d-362">Executar operação de consentimento de nível de administrador para qualquer aplicativo</span><span class="sxs-lookup"><span data-stu-id="bfb4d-362">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="bfb4d-363">Para **somente os aplicativos desenvolvidos usando o modelo de aplicativo hello V1**, você pode forçar essa toooccur de nível de consentimento do administrador adicionando "**? prompt = admin\_consentimento**" toohello final de um entrada do aplicativo na URL.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-363">For **only applications developed using hello V1 application model**, you can force this administrator level consent toooccur by adding “**?prompt=admin\_consent**” toohello end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="bfb4d-364">Para **qualquer aplicativo desenvolvido usando o modelo de aplicativo hello V2**, você pode impor esse toooccur consentimento de nível de administrador, seguindo as instruções de saudação em Olá **solicitar permissões de saudação de um diretório administrador** seção [usando o ponto de extremidade de autorização do Olá administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="bfb4d-364">For **any application developed using hello V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="bfb4d-365">Executar consentimento de nível de administrador para um aplicativo de locatário único</span><span class="sxs-lookup"><span data-stu-id="bfb4d-365">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="bfb4d-366">Para **único locatário aplicativos** que solicitar permissões (como aqueles que você está desenvolvendo ou possuir em sua organização), você pode executar uma **consentimento de nível administrativo** operação em nome de todos os os usuários fazer logon como um Administrador Global e clicando em Olá **conceder permissões** botão na parte superior de saudação do hello **registro de aplicativos -&gt; todos os aplicativos -&gt; selecionar um aplicativo - &gt; Permissões necessárias** folha.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-366">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on hello **Grant permissions** button at hello top of hello **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="bfb4d-367">Para **qualquer aplicativo desenvolvido usando Olá V1 ou V2 modelo de aplicativo**, você pode impor esse toooccur consentimento de nível de administrador, seguindo as instruções de saudação em Olá **solicitar permissões de saudação de um administrador de diretório** seção [usando o ponto de extremidade de autorização do Olá administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="bfb4d-367">For **any application developed using hello V1 or V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="bfb4d-368">Executar consentimento de nível de administrador para um aplicativo multilocatário</span><span class="sxs-lookup"><span data-stu-id="bfb4d-368">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="bfb4d-369">Para **Aplicativos de multilocatário** que solicitar permissões (como um aplicativo de terceiros ou desenvolvido pela Microsoft), você pode executar uma operação de **consentimento de nível administrativo**.</span><span class="sxs-lookup"><span data-stu-id="bfb4d-369">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="bfb4d-370">Entrar como um Administrador Global e clicando em Olá **conceder permissões** botão sob Olá **aplicativos corporativos -&gt; todos os aplicativos -&gt; selecionar um aplicativo -&gt; Permissões** folha (disponível em breve).</span><span class="sxs-lookup"><span data-stu-id="bfb4d-370">Sign in as a Global Administrator and clicking on hello **Grant permissions** button under hello **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="bfb4d-371">Você também pode impor esse toooccur consentimento de nível de administrador seguindo as instruções de saudação em hello **solicitar permissões de saudação de um administrador de diretório** seção [usando o ponto de extremidade de autorização do Olá administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="bfb4d-371">You can also enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfb4d-372">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bfb4d-372">Next steps</span></span>
[<span data-ttu-id="bfb4d-373">Usando o ponto de extremidade de autorização do Olá administrador</span><span class="sxs-lookup"><span data-stu-id="bfb4d-373">Using hello admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

