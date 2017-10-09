---
title: "Azure Active Directory B2C: Adicionar MSA (Conta da Microsoft) como um provedor de identidade usando Políticas personalizadas"
description: Exemplo usando Microsoft como provedor de identidade usando o protocolo OIDC (OpenID Connect)
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="1b2bd-103">Azure Active Directory B2C: Adicionar MSA (Conta da Microsoft) como um provedor de identidade usando políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="1b2bd-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="1b2bd-104">Este artigo mostra como tooenable entrar para usuários de conta da Microsoft (MSA) através do uso de saudação do [políticas personalizadas](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="1b2bd-104">This article shows you how tooenable sign-in for users from Microsoft account (MSA) through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b2bd-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1b2bd-105">Prerequisites</span></span>
<span data-ttu-id="1b2bd-106">Olá concluir as etapas em Olá [guia de Introdução com políticas personalizadas](active-directory-b2c-get-started-custom.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="1b2bd-107">As etapas incluem:</span><span class="sxs-lookup"><span data-stu-id="1b2bd-107">These steps include:</span></span>

1.  <span data-ttu-id="1b2bd-108">Criar um aplicativo de conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="1b2bd-109">Adicionando tooAzure de chave aplicativo AD B2C de conta de Microsoft hello</span><span class="sxs-lookup"><span data-stu-id="1b2bd-109">Adding hello Microsoft account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="1b2bd-110">Adicionar política de tooa do provedor de declarações</span><span class="sxs-lookup"><span data-stu-id="1b2bd-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="1b2bd-111">Registrando jornada de usuário tooa do provedor de declarações de Account da Microsoft hello</span><span class="sxs-lookup"><span data-stu-id="1b2bd-111">Registering hello Microsoft Account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="1b2bd-112">Carregando tooan de política de saudação do Azure AD B2C locatário e testá-lo</span><span class="sxs-lookup"><span data-stu-id="1b2bd-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="1b2bd-113">Criar um aplicativo de conta da Microsoft</span><span class="sxs-lookup"><span data-stu-id="1b2bd-113">Create a Microsoft account application</span></span>
<span data-ttu-id="1b2bd-114">toouse Microsoft conta como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo de conta da Microsoft e fornecê-lo com os parâmetros de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-114">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="1b2bd-115">Você precisa de uma conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-115">You need a Microsoft account.</span></span> <span data-ttu-id="1b2bd-116">Se você não tiver uma, visite [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="1b2bd-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="1b2bd-117">Vá toohello [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e entre com suas credenciais de conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-117">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="1b2bd-118">Clique em **Adicionar um aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-118">Click **Add an app**.</span></span>

    ![Conta da Microsoft – Adicionar um aplicativo](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="1b2bd-120">Forneça um **Nome** para seu aplicativo, **Email de contato**, desmarque **Deixe-nos ajudar você a começar** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Conta da Microsoft - Registrar seu aplicativo](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="1b2bd-122">Copie o valor de saudação do **Id do aplicativo**. Precisar tooconfigure conta da Microsoft como um provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-122">Copy hello value of **Application Id**. You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>

    ![Conta da Microsoft - copiar o valor de saudação do Id do aplicativo](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="1b2bd-124">Clique em **Adicionar plataforma**</span><span class="sxs-lookup"><span data-stu-id="1b2bd-124">Click on **Add platform**</span></span>

    ![Conta da Microsoft - Adicionar plataforma](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="1b2bd-126">Na lista de plataforma hello, escolha **Web**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-126">From hello platform list, choose **Web**.</span></span>

    ![Conta da Microsoft - na lista de plataformas de saudação escolher Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="1b2bd-128">Digite `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **URIs de redirecionamento** campo.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="1b2bd-129">Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="1b2bd-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Conta da Microsoft – Definir URLs de redirecionamento](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="1b2bd-131">Clique em **gerar nova senha** em Olá **segredos do aplicativo** seção.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-131">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="1b2bd-132">Cópia Olá nova senha exibida na tela.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-132">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="1b2bd-133">Precisar tooconfigure conta da Microsoft como um provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-133">You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="1b2bd-134">A senha é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-134">This password is an important security credential.</span></span>

    ![Conta da Microsoft - Gerar nova senha](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Conta da Microsoft - nova senha de saudação de cópia](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="1b2bd-137">Caixa de saudação de seleção que diz **suporte do SDK do Live** em Olá **opções avançadas de** seção.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-137">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="1b2bd-138">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-138">Click **Save**.</span></span>

    ![Conta da Microsoft - Suporte ao SDK do Live](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="1b2bd-140">Adicionar tooAzure de chave aplicativo AD B2C de conta de Microsoft hello</span><span class="sxs-lookup"><span data-stu-id="1b2bd-140">Add hello Microsoft account application key tooAzure AD B2C</span></span>
<span data-ttu-id="1b2bd-141">Federação com contas da Microsoft requer um segredo do cliente para tootrust de conta do Microsoft Azure AD B2C em nome do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-141">Federation with Microsoft accounts requires a client secret for Microsoft account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="1b2bd-142">É necessário toostore seu secert de aplicativo de conta Microsoft no Azure AD B2C locatário:</span><span class="sxs-lookup"><span data-stu-id="1b2bd-142">You need toostore your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="1b2bd-143">Vá locatário tooyour B2C do Azure AD e selecione **B2C configurações** > **Framework de experiência de identidade**</span><span class="sxs-lookup"><span data-stu-id="1b2bd-143">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="1b2bd-144">Selecione **chaves política** tooview chaves de saudação disponíveis em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-144">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="1b2bd-145">Clique em **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="1b2bd-146">Para as **Opções**, use **Manual**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="1b2bd-147">Para o **Nome**, use `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="1b2bd-148">prefixo de saudação `B2C_1A_` podem ser adicionadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-148">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="1b2bd-149">Em Olá **segredo** , digite o segredo do aplicativo Microsoft de https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1b2bd-149">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="1b2bd-150">Para o **Uso da chave**, use **Assinatura**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="1b2bd-151">Clique em **Criar**</span><span class="sxs-lookup"><span data-stu-id="1b2bd-151">Click **Create**</span></span>
9.  <span data-ttu-id="1b2bd-152">Confirme que você criou a chave Olá `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-152">Confirm that you've created hello key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="1b2bd-153">Adicionar um provedor de declarações à política de extensão</span><span class="sxs-lookup"><span data-stu-id="1b2bd-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="1b2bd-154">Se você quiser usuários toosign no usando Account da Microsoft, você precisa toodefine Account da Microsoft como um provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-154">If you want users toosign in by using Microsoft Account, you need toodefine Microsoft Account as a claims provider.</span></span> <span data-ttu-id="1b2bd-155">Em outras palavras, você precisa toospecify do Azure AD B2C se comunica com um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-155">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="1b2bd-156">ponto de extremidade Olá fornece um conjunto de declarações que são usados pelo Azure AD B2C tooverify que um usuário específico autenticado.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-156">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="1b2bd-157">Defina a Conta da Microsoft como um provedor de declarações adicionando o nó `<ClaimsProvider>` em seu arquivo de política da extensão:</span><span class="sxs-lookup"><span data-stu-id="1b2bd-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="1b2bd-158">Abra o arquivo de política de extensão de saudação (TrustFrameworkExtensions.xml) do seu diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-158">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="1b2bd-159">Se você precisar de um editor de XML, [experimente o Visual Studio Code](https://code.visualstudio.com/download), um editor de plataforma cruzada leve.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="1b2bd-160">Localize Olá `<ClaimsProviders>` seção</span><span class="sxs-lookup"><span data-stu-id="1b2bd-160">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="1b2bd-161">Adicione o seguinte trecho XML em Olá `ClaimsProviders` elemento:</span><span class="sxs-lookup"><span data-stu-id="1b2bd-161">Add following XML snippet under hello `ClaimsProviders` element:</span></span>

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  <span data-ttu-id="1b2bd-162">Substitua o valor `client_id` pela Id de cliente do aplicativo da Conta da Microsoft</span><span class="sxs-lookup"><span data-stu-id="1b2bd-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="1b2bd-163">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-163">Save hello file.</span></span>

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="1b2bd-164">Registrar tooSign de provedor de declarações Olá Account da Microsoft se ou entrar jornada de usuário</span><span class="sxs-lookup"><span data-stu-id="1b2bd-164">Register hello Microsoft Account claims provider tooSign up or Sign-in user journey</span></span>

<span data-ttu-id="1b2bd-165">Neste ponto, o provedor de identidade Olá foi configurado, mas não está disponível em qualquer uma das telas de entrada-o/entrada hello.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-165">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="1b2bd-166">Agora você precisa tooadd Olá Account Microsoft identidade provedor tooyour usuário `SignUpOrSignIn` jornada de usuário.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-166">Now you need tooadd hello Microsoft Account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="1b2bd-167">toomake-lo, podemos criar uma duplicata de uma jornada de usuário do modelo existente.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-167">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="1b2bd-168">Em seguida, adicionamos provedor de identidade Olá Account da Microsoft:</span><span class="sxs-lookup"><span data-stu-id="1b2bd-168">Then we add hello Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="1b2bd-169">Se você tiver copiado anteriormente Olá `<UserJourneys>` elemento de arquivo de base de seu arquivo de extensão de toohello política `TrustFrameworkExtensions.xml`, você pode ignorar a seção de toothis.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-169">If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file `TrustFrameworkExtensions.xml`, you can skip toothis section.</span></span>

1.  <span data-ttu-id="1b2bd-170">Abra o arquivo de base de saudação da política (por exemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="1b2bd-170">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="1b2bd-171">Localize Olá `<UserJourneys>` elemento e cópia Olá todo conteúdo do `<UserJourneys>` nó.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-171">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="1b2bd-172">Abra o arquivo de extensão da saudação (por exemplo, TrustFrameworkExtensions.xml) e localize Olá `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-172">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="1b2bd-173">Se o elemento de saudação não existir, adicione um.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-173">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="1b2bd-174">Cole a todo o conteúdo de saudação `<UserJournesy>` nó que você copiou como um filho do hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-174">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="1b2bd-175">Botão de saudação de exibição</span><span class="sxs-lookup"><span data-stu-id="1b2bd-175">Display hello button</span></span>
<span data-ttu-id="1b2bd-176">Olá `<ClaimsProviderSelections>` elemento define a lista de saudação das opções de seleção de provedor de declarações e sua ordem.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-176">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="1b2bd-177">`<ClaimsProviderSelection>`elemento é análogo tooan botão de provedor de identidade em uma página de entrada-o/entrar.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-177">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="1b2bd-178">Se você adicionar um `<ClaimsProviderSelection>` elemento para a conta da Microsoft, um novo botão aparece quando um usuário chega na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="1b2bd-179">tooadd este elemento:</span><span class="sxs-lookup"><span data-stu-id="1b2bd-179">tooadd this element:</span></span>

1.  <span data-ttu-id="1b2bd-180">Localize Olá `<UserJourney>` nó inclui `Id="SignUpOrSignIn"` em jornada saudação do usuário que você copiou.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-180">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="1b2bd-181">Localizar Olá `<OrchestrationStep>` nó inclui`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="1b2bd-181">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="1b2bd-182">Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="1b2bd-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="1b2bd-183">Ação de link de saudação botão tooan</span><span class="sxs-lookup"><span data-stu-id="1b2bd-183">Link hello button tooan action</span></span>
<span data-ttu-id="1b2bd-184">Agora que você tem um botão em vigor, é necessário toolink-tooan ação.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-184">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="1b2bd-185">ação Hello, nesse caso, é para o Azure AD B2C toocommunicate com Account Microsoft tooreceive um token.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-185">hello action, in this case, is for Azure AD B2C toocommunicate with Microsoft Account tooreceive a token.</span></span> <span data-ttu-id="1b2bd-186">Ação do botão tooan de saudação do link vinculando perfil técnico Olá para o seu provedor de declarações de Account da Microsoft:</span><span class="sxs-lookup"><span data-stu-id="1b2bd-186">Link hello button tooan action by linking hello technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="1b2bd-187">Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-187">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="1b2bd-188">Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="1b2bd-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="1b2bd-189">Certifique-se de saudação `Id` tem Olá mesmo valor de `TargetClaimsExchangeId` em Olá anterior seção</span><span class="sxs-lookup"><span data-stu-id="1b2bd-189">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
>   * <span data-ttu-id="1b2bd-190">Certifique-se de `TechnicalProfileReferenceId` ID está definida toohello perfil técnico que você criou anteriormente (MSA-OIDC).</span><span class="sxs-lookup"><span data-stu-id="1b2bd-190">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="1b2bd-191">Carregar o locatário de tooyour política Olá</span><span class="sxs-lookup"><span data-stu-id="1b2bd-191">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="1b2bd-192">Em Olá [portal do Azure](https://portal.azure.com), alternar para Olá [contexto do seu locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)e abra hello **do Azure AD B2C** folha.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-192">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="1b2bd-193">Selecione **Estrutura de Experiência de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="1b2bd-194">Olá abrir **todas as políticas** folha.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-194">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="1b2bd-195">Selecione **Carregar Política**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="1b2bd-196">Verificar **substituir a política de saudação se ela existe** caixa.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-196">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="1b2bd-197">**Carregar** TrustFrameworkExtensions.xml e certifique-se de que ele não falha na validação de saudação</span><span class="sxs-lookup"><span data-stu-id="1b2bd-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="1b2bd-198">Testar a política personalizada do hello usando Executar agora</span><span class="sxs-lookup"><span data-stu-id="1b2bd-198">Test hello custom policy by using Run Now</span></span>

1.  <span data-ttu-id="1b2bd-199">Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-199">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="1b2bd-200">**Executar agora** requer pelo menos um aplicativo toobe pré-registrado no locatário hello.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-200">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> <span data-ttu-id="1b2bd-201">toolearn como tooregister aplicativos, consulte hello Azure AD B2C [começar](active-directory-b2c-get-started.md) artigo ou hello [registro do aplicativo](active-directory-b2c-app-registration.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-201">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="1b2bd-202">Abra **B2C_1A_signup_signin**, Olá política personalizada do terceira parte confiável (RP) que você carregou.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-202">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="1b2bd-203">Selecione **Executar Agora**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="1b2bd-204">Você deve ser capaz de toosign usando a conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-204">You should be able toosign in using Microsoft account.</span></span>

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="1b2bd-205">[Opcional] Registrar a jornada do hello Microsoft Account declarações provedor tooProfile Editar usuário</span><span class="sxs-lookup"><span data-stu-id="1b2bd-205">[Optional] Register hello Microsoft Account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="1b2bd-206">Você pode querer provedor de identidade tooadd Olá Account da Microsoft também tooyour usuário `ProfileEdit` jornada de usuário.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-206">You may want tooadd hello Microsoft Account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="1b2bd-207">toomake disponível, podemos Repita Olá último duas etapas:</span><span class="sxs-lookup"><span data-stu-id="1b2bd-207">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="1b2bd-208">Botão de saudação de exibição</span><span class="sxs-lookup"><span data-stu-id="1b2bd-208">Display hello button</span></span>
1.  <span data-ttu-id="1b2bd-209">Abra o arquivo de extensão de saudação da política (por exemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="1b2bd-209">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="1b2bd-210">Localize Olá `<UserJourney>` nó inclui `Id="ProfileEdit"` em jornada saudação do usuário que você copiou.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-210">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="1b2bd-211">Localizar Olá `<OrchestrationStep>` nó inclui`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="1b2bd-211">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="1b2bd-212">Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="1b2bd-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="1b2bd-213">Ação de link de saudação botão tooan</span><span class="sxs-lookup"><span data-stu-id="1b2bd-213">Link hello button tooan action</span></span>
1.  <span data-ttu-id="1b2bd-214">Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-214">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="1b2bd-215">Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="1b2bd-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="1b2bd-216">Testar a política personalizada de perfil Editar hello usando Executar agora</span><span class="sxs-lookup"><span data-stu-id="1b2bd-216">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="1b2bd-217">Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-217">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="1b2bd-218">Abra **B2C_1A_ProfileEdit**, Olá política personalizada do terceira parte confiável (RP) que você carregou.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-218">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="1b2bd-219">Selecione **Executar Agora**.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="1b2bd-220">Você deve ser capaz de toosign usando a conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-220">You should be able toosign in using Microsoft account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="1b2bd-221">Baixar arquivos de política completa Olá</span><span class="sxs-lookup"><span data-stu-id="1b2bd-221">Download hello complete policy files</span></span>
<span data-ttu-id="1b2bd-222">Opcional: É recomendável que criar o seu cenário usando seus próprios arquivos de política personalizada após a conclusão Olá guia de Introdução com as políticas personalizadas percorrer em vez de usar esses arquivos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="1b2bd-222">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="1b2bd-223">Arquivos de política de exemplo para referência</span><span class="sxs-lookup"><span data-stu-id="1b2bd-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
