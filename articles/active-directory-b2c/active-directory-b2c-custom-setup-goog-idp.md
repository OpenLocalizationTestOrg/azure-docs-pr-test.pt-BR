---
title: "Azure Active Directory B2C: Adicionar Google+ como um provedor de identidade OAuth2 usando políticas personalizadas"
description: Exemplo de como usar o Google + como provedor de identidade usando o protocolo OAuth2
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
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="c1ba5-103">Azure Active Directory B2C: Adicionar Google+ como um provedor de identidade OAuth2 usando políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="c1ba5-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="c1ba5-104">Este guia mostra como tooenable entrar para usuários da conta do Google + através do uso de saudação do [políticas personalizadas](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c1ba5-104">This guide shows you how tooenable sign-in for users from Google+ account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1ba5-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c1ba5-105">Prerequisites</span></span>

<span data-ttu-id="c1ba5-106">Olá concluir as etapas em Olá [guia de Introdução com políticas personalizadas](active-directory-b2c-get-started-custom.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="c1ba5-107">As etapas incluem:</span><span class="sxs-lookup"><span data-stu-id="c1ba5-107">These steps include:</span></span>

1.  <span data-ttu-id="c1ba5-108">Criar um aplicativo de conta do Google+.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="c1ba5-109">Adicionando Olá Google + conta aplicativo chave tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c1ba5-109">Adding hello Google+ account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="c1ba5-110">Adicionar política de tooa do provedor de declarações</span><span class="sxs-lookup"><span data-stu-id="c1ba5-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="c1ba5-111">Registrando Olá Google + conta declarações provedor tooa usuário jornada</span><span class="sxs-lookup"><span data-stu-id="c1ba5-111">Registering hello Google+ account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="c1ba5-112">Carregando tooan de política de saudação do Azure AD B2C locatário e testá-lo</span><span class="sxs-lookup"><span data-stu-id="c1ba5-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="c1ba5-113">Criar um aplicativo de conta do Google+</span><span class="sxs-lookup"><span data-stu-id="c1ba5-113">Create a Google+ account application</span></span>
<span data-ttu-id="c1ba5-114">toouse Google + como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo do Google + e fornecê-lo com os parâmetros de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-114">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="c1ba5-115">Você pode registrar um aplicativo do Google+ aqui: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span><span class="sxs-lookup"><span data-stu-id="c1ba5-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="c1ba5-116">Vá toohello [Console de desenvolvedores do Google](https://console.developers.google.com/) e entre com suas credenciais de conta do Google +.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-116">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="c1ba5-117">Clique em **Criar projeto**, insira um **Nome de projeto** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="c1ba5-118">Clique em Olá **menu projetos**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-118">Click on hello **Projects menu**.</span></span>

    ![Conta do Google+ - Selecionar o projeto](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="c1ba5-120">Clique em Olá  **+**  botão.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-120">Click on hello **+** button.</span></span>

    ![Conta do Google+ - Criar novo projeto](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="c1ba5-122">Insira um **Nome de projeto** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Conta do Google+ - Novo projeto](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="c1ba5-124">Aguarde até que o projeto hello está pronto e clique em Olá **menu projetos**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-124">Wait until hello project is ready and click on hello **Projects menu**.</span></span>

    ![Conta do Google + - Aguarde até que o novo projeto é toouse pronto](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="c1ba5-126">Clique no nome do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-126">Click on your project name.</span></span>

    ![Conta do Google + - novo projeto de saudação Select](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="c1ba5-128">Clique em **Manager API** e, em seguida, clique em **credenciais** em Olá barra de navegação esquerda.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-128">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
9.  <span data-ttu-id="c1ba5-129">Clique em Olá **tela de consentimento de OAuth** guia na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-129">Click hello **OAuth consent screen** tab at hello top.</span></span>

    ![Conta do Google+ - Definir tela de consentimento de OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="c1ba5-131">Selecione ou especifique um **Endereço de email** válido, forneça um **Nome de produto** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google+ - Credenciais do aplicativo](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="c1ba5-133">Clique em **Novas credenciais** e escolha **ID do cliente OAuth**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google+ - Criar novas credenciais do aplicativo](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="c1ba5-135">Em **Tipo de aplicativo**, selecione **Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-135">Under **Application type**, select **Web application**.</span></span>

    ![Google+ - Selecione o tipo de aplicativo](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="c1ba5-137">Forneça um **nome** para seu aplicativo, insira `https://login.microsoftonline.com` em Olá **origens do JavaScript autorizado** campo, e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **autorizados redirecionar URIs**campo.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="c1ba5-138">Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="c1ba5-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="c1ba5-139">Olá **{locatário}** valor diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-139">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="c1ba5-140">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-140">Click **Create**.</span></span>

    ![Google + - Forneça origens de JavaScript autorizadas e URIs de redirecionamento](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="c1ba5-142">Copie os valores de saudação do **Id do cliente** e **segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-142">Copy hello values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="c1ba5-143">Você precisa ambos tooconfigure Google + como um provedor de identidade no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-143">You need both tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="c1ba5-144">**Segredo do cliente** é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-144">**Client secret** is an important security credential.</span></span>

    ![Google + - valores de saudação de cópia de segredo de cliente e a Id do cliente](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="c1ba5-146">Adicionar Olá Google + conta aplicativo chave tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c1ba5-146">Add hello Google+ account application key tooAzure AD B2C</span></span>
<span data-ttu-id="c1ba5-147">Federação com contas do Google + requer um segredo do cliente para o Google + conta tootrust B2C do Azure AD em nome do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-147">Federation with Google+ accounts requires a client secret for Google+ account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="c1ba5-148">É necessário toostore seu segredo do aplicativo do Google + no locatário do Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="c1ba5-148">You need toostore your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="c1ba5-149">Vá locatário tooyour B2C do Azure AD e selecione **B2C configurações** > **Framework de experiência de identidade**</span><span class="sxs-lookup"><span data-stu-id="c1ba5-149">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="c1ba5-150">Selecione **chaves política** tooview chaves de saudação disponíveis em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-150">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="c1ba5-151">Clique em **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="c1ba5-152">Para as **Opções**, use **Manual**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="c1ba5-153">Para o **Nome**, use `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="c1ba5-154">prefixo de saudação `B2C_1A_` podem ser adicionadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-154">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="c1ba5-155">Em Olá **segredo** , digite o segredo do aplicativo Microsoft de https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="c1ba5-155">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="c1ba5-156">Para o **Uso da chave**, use **Assinatura**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="c1ba5-157">Clique em **Criar**</span><span class="sxs-lookup"><span data-stu-id="c1ba5-157">Click **Create**</span></span>
9.  <span data-ttu-id="c1ba5-158">Confirme que você criou a chave Olá `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-158">Confirm that you've created hello key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="c1ba5-159">Adicionar um provedor de declarações à política de extensão</span><span class="sxs-lookup"><span data-stu-id="c1ba5-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="c1ba5-160">Se você quiser usuários toosign no usando a conta do Google +, você precisa toodefine Google + conta como um provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-160">If you want users toosign in by using Google+ account, you need toodefine Google+ account as a claims provider.</span></span> <span data-ttu-id="c1ba5-161">Em outras palavras, você precisa toospecify do Azure AD B2C se comunica com um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-161">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="c1ba5-162">ponto de extremidade Olá fornece um conjunto de declarações que são usados pelo Azure AD B2C tooverify que um usuário específico autenticado.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-162">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="c1ba5-163">Defina a Conta do Google+ como um provedor de declarações adicionando o nó `<ClaimsProvider>` em seu arquivo de política da extensão:</span><span class="sxs-lookup"><span data-stu-id="c1ba5-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="c1ba5-164">Abra o arquivo de política de extensão de saudação (TrustFrameworkExtensions.xml) do seu diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-164">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="c1ba5-165">Se você precisar de um editor de XML, [experimente o Visual Studio Code](https://code.visualstudio.com/download), um editor de plataforma cruzada leve.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="c1ba5-166">Localize Olá `<ClaimsProviders>` seção</span><span class="sxs-lookup"><span data-stu-id="c1ba5-166">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="c1ba5-167">Adicionar Olá seguindo o trecho XML em Olá `ClaimsProviders` elemento e substituir `client_id` valor com sua ID de cliente de aplicativo, conta Google + antes de salvar o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-167">Add hello following XML snippet under hello `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving hello file.</span></span>  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="c1ba5-168">Registrar Olá Google + conta declarações provedor tooSign se ou entrar a jornada de usuário</span><span class="sxs-lookup"><span data-stu-id="c1ba5-168">Register hello Google+ account claims provider tooSign up or Sign in user journey</span></span>

<span data-ttu-id="c1ba5-169">provedor de identidade Olá foi configurado.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-169">hello identity provider has been set up.</span></span>  <span data-ttu-id="c1ba5-170">No entanto, não está disponível em qualquer uma das telas de entrada-o/entrada hello.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-170">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="c1ba5-171">Adicionar Olá Google + conta identidade provedor tooyour usuário `SignUpOrSignIn` jornada de usuário.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-171">Add hello Google+ account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="c1ba5-172">toomake-lo, podemos criar uma duplicata de uma jornada de usuário do modelo existente.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-172">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="c1ba5-173">Em seguida, adicionamos Olá Google + conta provedor de identidade:</span><span class="sxs-lookup"><span data-stu-id="c1ba5-173">Then we add hello Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="c1ba5-174">Se você copiou Olá `<UserJourneys>` elemento de arquivo de base de seu arquivo de extensão da diretiva toohello (TrustFrameworkExtensions.xml), você pode ignorar a seção de toothis.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-174">If you copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml), you can skip toothis section.</span></span>

1.  <span data-ttu-id="c1ba5-175">Abra o arquivo de base de saudação da política (por exemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="c1ba5-175">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="c1ba5-176">Localize Olá `<UserJourneys>` elemento e cópia Olá todo conteúdo do `<UserJourneys>` nó.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-176">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="c1ba5-177">Abra o arquivo de extensão da saudação (por exemplo, TrustFrameworkExtensions.xml) e localize Olá `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-177">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="c1ba5-178">Se o elemento de saudação não existir, adicione um.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-178">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="c1ba5-179">Cole a todo o conteúdo de saudação `<UserJournesy>` nó que você copiou como um filho do hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-179">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="c1ba5-180">Botão de saudação de exibição</span><span class="sxs-lookup"><span data-stu-id="c1ba5-180">Display hello button</span></span>
<span data-ttu-id="c1ba5-181">Olá `<ClaimsProviderSelections>` elemento define a lista de saudação das opções de seleção de provedor de declarações e sua ordem.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-181">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="c1ba5-182">`<ClaimsProviderSelection>`elemento é análogo tooan botão de provedor de identidade em uma página de entrada-o/entrar.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-182">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="c1ba5-183">Se você adicionar um `<ClaimsProviderSelection>` elemento para a conta do Google +, um novo botão aparece quando um usuário chega na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="c1ba5-184">tooadd este elemento:</span><span class="sxs-lookup"><span data-stu-id="c1ba5-184">tooadd this element:</span></span>

1.  <span data-ttu-id="c1ba5-185">Localize Olá `<UserJourney>` nó inclui `Id="SignUpOrSignIn"` em jornada saudação do usuário que você copiou.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-185">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="c1ba5-186">Localizar Olá `<OrchestrationStep>` nó inclui`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="c1ba5-186">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="c1ba5-187">Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="c1ba5-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="c1ba5-188">Ação de link de saudação botão tooan</span><span class="sxs-lookup"><span data-stu-id="c1ba5-188">Link hello button tooan action</span></span>
<span data-ttu-id="c1ba5-189">Agora que você tem um botão em vigor, é necessário toolink-tooan ação.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-189">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="c1ba5-190">ação de Hello, nesse caso, é para o Azure AD B2C toocommunicate com tooreceive de conta do Google + um token.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-190">hello action, in this case, is for Azure AD B2C toocommunicate with Google+ account tooreceive a token.</span></span>

1.  <span data-ttu-id="c1ba5-191">Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-191">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="c1ba5-192">Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="c1ba5-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="c1ba5-193">Certifique-se de saudação `Id` tem Olá mesmo valor de `TargetClaimsExchangeId` em Olá anterior seção</span><span class="sxs-lookup"><span data-stu-id="c1ba5-193">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
> * <span data-ttu-id="c1ba5-194">Certifique-se de `TechnicalProfileReferenceId` ID está definida toohello perfil técnico que você criou anteriormente (Google-OAUTH).</span><span class="sxs-lookup"><span data-stu-id="c1ba5-194">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="c1ba5-195">Carregar o locatário de tooyour política Olá</span><span class="sxs-lookup"><span data-stu-id="c1ba5-195">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="c1ba5-196">Em Olá [portal do Azure](https://portal.azure.com), alternar para Olá [contexto do seu locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)e abra hello **do Azure AD B2C** folha.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-196">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="c1ba5-197">Selecione **Estrutura de Experiência de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="c1ba5-198">Olá abrir **todas as políticas** folha.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-198">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="c1ba5-199">Selecione **Carregar Política**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="c1ba5-200">Verificar **substituir a política de saudação se ela existe** caixa.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-200">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="c1ba5-201">**Carregar** TrustFrameworkExtensions.xml e certifique-se de que ele não falha na validação de saudação</span><span class="sxs-lookup"><span data-stu-id="c1ba5-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="c1ba5-202">Testar a política personalizada do hello usando Executar agora</span><span class="sxs-lookup"><span data-stu-id="c1ba5-202">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="c1ba5-203">Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-203">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="c1ba5-204">**Executar agora** requer pelo menos um aplicativo toobe pré-registrado no locatário hello.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-204">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> 
    >    <span data-ttu-id="c1ba5-205">toolearn como tooregister aplicativos, consulte hello Azure AD B2C [começar](active-directory-b2c-get-started.md) artigo ou hello [registro do aplicativo](active-directory-b2c-app-registration.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-205">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="c1ba5-206">Abra **B2C_1A_signup_signin**, Olá política personalizada do terceira parte confiável (RP) que você carregou.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-206">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="c1ba5-207">Selecione **Executar Agora**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="c1ba5-208">Você deve ser capaz de toosign usando a conta do Google +.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-208">You should be able toosign in using Google+ account.</span></span>

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="c1ba5-209">[Opcional] Registrar Olá Google + conta declarações provedor tooProfile Editar usuário jornada</span><span class="sxs-lookup"><span data-stu-id="c1ba5-209">[Optional] Register hello Google+ account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="c1ba5-210">Talvez você queira tooadd Olá Google + conta provedor de identidade também tooyour usuário `ProfileEdit` jornada de usuário.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-210">You may want tooadd hello Google+ account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="c1ba5-211">toomake disponível, podemos Repita Olá último duas etapas:</span><span class="sxs-lookup"><span data-stu-id="c1ba5-211">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="c1ba5-212">Botão de saudação de exibição</span><span class="sxs-lookup"><span data-stu-id="c1ba5-212">Display hello button</span></span>
1.  <span data-ttu-id="c1ba5-213">Abra o arquivo de extensão de saudação da política (por exemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="c1ba5-213">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="c1ba5-214">Localize Olá `<UserJourney>` nó inclui `Id="ProfileEdit"` em jornada saudação do usuário que você copiou.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-214">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="c1ba5-215">Localizar Olá `<OrchestrationStep>` nó inclui`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="c1ba5-215">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="c1ba5-216">Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="c1ba5-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="c1ba5-217">Ação de link de saudação botão tooan</span><span class="sxs-lookup"><span data-stu-id="c1ba5-217">Link hello button tooan action</span></span>
1.  <span data-ttu-id="c1ba5-218">Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-218">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="c1ba5-219">Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="c1ba5-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="c1ba5-220">Testar a política personalizada de perfil Editar hello usando Executar agora</span><span class="sxs-lookup"><span data-stu-id="c1ba5-220">Test hello custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="c1ba5-221">Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-221">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="c1ba5-222">Abra **B2C_1A_ProfileEdit**, Olá política personalizada do terceira parte confiável (RP) que você carregou.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-222">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="c1ba5-223">Selecione **Executar Agora**.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="c1ba5-224">Você deve ser capaz de toosign usando a conta do Google +.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-224">You should be able toosign in using Google+ account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="c1ba5-225">Baixar arquivos de política completa Olá</span><span class="sxs-lookup"><span data-stu-id="c1ba5-225">Download hello complete policy files</span></span>
<span data-ttu-id="c1ba5-226">Opcional: É recomendável que criar o seu cenário usando seus próprios arquivos de política personalizada após a conclusão Olá guia de Introdução com as políticas personalizadas percorrer em vez de usar esses arquivos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c1ba5-226">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="c1ba5-227">Arquivos de política de exemplo para referência</span><span class="sxs-lookup"><span data-stu-id="c1ba5-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
