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
ms.openlocfilehash: e0aaf710d230f7667fff32b50ddb64104509d740
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="901ed-103">Azure Active Directory B2C: Adicionar Google+ como um provedor de identidade OAuth2 usando políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="901ed-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="901ed-104">Este guia mostra como habilitar a entrada para usuários da conta do Google+ por meio de [políticas personalizadas](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="901ed-104">This guide shows you how to enable sign-in for users from Google+ account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="901ed-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="901ed-105">Prerequisites</span></span>

<span data-ttu-id="901ed-106">Conclua as etapas no artigo [Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="901ed-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="901ed-107">As etapas incluem:</span><span class="sxs-lookup"><span data-stu-id="901ed-107">These steps include:</span></span>

1.  <span data-ttu-id="901ed-108">Criar um aplicativo de conta do Google+.</span><span class="sxs-lookup"><span data-stu-id="901ed-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="901ed-109">Adicionar a chave de aplicativo da conta do Google+ ao Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="901ed-109">Adding the Google+ account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="901ed-110">Adicionar o provedor de declarações a uma política</span><span class="sxs-lookup"><span data-stu-id="901ed-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="901ed-111">Registrar o provedor de declarações da conta do Google+ a um percurso do usuário</span><span class="sxs-lookup"><span data-stu-id="901ed-111">Registering the Google+ account claims provider to a user journey</span></span>
5.  <span data-ttu-id="901ed-112">Carregar a política para um locatário do Azure AD B2C e testá-la</span><span class="sxs-lookup"><span data-stu-id="901ed-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="901ed-113">Criar um aplicativo de conta do Google+</span><span class="sxs-lookup"><span data-stu-id="901ed-113">Create a Google+ account application</span></span>
<span data-ttu-id="901ed-114">Para usar o Google+ como um provedor de identidade no Azure AD (Azure Active Directory B2C), você precisará criar um aplicativo do Google+ e fornecer a ele os parâmetros certos.</span><span class="sxs-lookup"><span data-stu-id="901ed-114">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="901ed-115">Você pode registrar um aplicativo do Google+ aqui: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span><span class="sxs-lookup"><span data-stu-id="901ed-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="901ed-116">Acesse o [Console de Desenvolvedores do Google](https://console.developers.google.com/) e entre com suas credenciais de conta do Google+.</span><span class="sxs-lookup"><span data-stu-id="901ed-116">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="901ed-117">Clique em **Criar projeto**, insira um **Nome de projeto** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="901ed-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="901ed-118">Clique no **menu Projetos**.</span><span class="sxs-lookup"><span data-stu-id="901ed-118">Click on the **Projects menu**.</span></span>

    ![Conta do Google+ - Selecionar o projeto](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="901ed-120">Clique no botão **+**.</span><span class="sxs-lookup"><span data-stu-id="901ed-120">Click on the **+** button.</span></span>

    ![Conta do Google+ - Criar novo projeto](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="901ed-122">Insira um **Nome de projeto** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="901ed-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Conta do Google+ - Novo projeto](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="901ed-124">Aguarde até que o projeto esteja pronto e clique no **menu Projetos**.</span><span class="sxs-lookup"><span data-stu-id="901ed-124">Wait until the project is ready and click on the **Projects menu**.</span></span>

    ![Conta do Google+ - Aguarde até que o novo projeto esteja pronto para uso](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="901ed-126">Clique no nome do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="901ed-126">Click on your project name.</span></span>

    ![Conta do Google+ - Selecionar o novo projeto](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="901ed-128">Clique em **Gerenciador de API** e em **Credenciais** no painel de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="901ed-128">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
9.  <span data-ttu-id="901ed-129">Clique na guia **OAuth consent screen (Tela de consentimento do OAuth)** na parte superior.</span><span class="sxs-lookup"><span data-stu-id="901ed-129">Click the **OAuth consent screen** tab at the top.</span></span>

    ![Conta do Google+ - Definir tela de consentimento de OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="901ed-131">Selecione ou especifique um **Endereço de email** válido, forneça um **Nome de produto** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="901ed-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google+ - Credenciais do aplicativo](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="901ed-133">Clique em **Novas credenciais** e escolha **ID do cliente OAuth**.</span><span class="sxs-lookup"><span data-stu-id="901ed-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google+ - Criar novas credenciais do aplicativo](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="901ed-135">Em **Tipo de aplicativo**, selecione **Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="901ed-135">Under **Application type**, select **Web application**.</span></span>

    ![Google+ - Selecione o tipo de aplicativo](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="901ed-137">Forneça um **Nome** para seu aplicativo, insira `https://login.microsoftonline.com` no campo **Origens de JavaScript autorizadas** e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` no campo **URIs de redirecionamento autorizados**.</span><span class="sxs-lookup"><span data-stu-id="901ed-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="901ed-138">Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="901ed-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="901ed-139">O valor **{tenant}** diferencia letras maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="901ed-139">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="901ed-140">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="901ed-140">Click **Create**.</span></span>

    ![Google + - Forneça origens de JavaScript autorizadas e URIs de redirecionamento](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="901ed-142">Copie os valores de **ID do cliente** e **Segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="901ed-142">Copy the values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="901ed-143">Você precisa de ambos para configurar o Google+ como um provedor de identidade no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="901ed-143">You need both to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="901ed-144">**Segredo do cliente** é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="901ed-144">**Client secret** is an important security credential.</span></span>

    ![Google+ - Copie os valores de Id do cliente e Segredo do cliente](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-the-google-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="901ed-146">Adicionar a chave de aplicativo da conta do Google+ ao Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="901ed-146">Add the Google+ account application key to Azure AD B2C</span></span>
<span data-ttu-id="901ed-147">A federação com contas do Google+ exige um segredo do cliente para a conta do Google+ para confiar no Azure AD B2C em nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="901ed-147">Federation with Google+ accounts requires a client secret for Google+ account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="901ed-148">Você precisa armazenar seu segredo de aplicativo doa Google+ no locatário do Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="901ed-148">You need to store your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="901ed-149">Vá até seu locatário do Azure AD B2C e selecione **Configurações de B2C** > **Identity Experience Framework**</span><span class="sxs-lookup"><span data-stu-id="901ed-149">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="901ed-150">Selecione **Chaves de Política** para exibir as chaves disponíveis no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="901ed-150">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="901ed-151">Clique em **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="901ed-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="901ed-152">Para as **Opções**, use **Manual**.</span><span class="sxs-lookup"><span data-stu-id="901ed-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="901ed-153">Para o **Nome**, use `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="901ed-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="901ed-154">O prefixo `B2C_1A_` pode ser adicionado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="901ed-154">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="901ed-155">Na caixa **Segredo**, insira o segredo de aplicativo da Microsoft de https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="901ed-155">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="901ed-156">Para o **Uso da chave**, use **Assinatura**.</span><span class="sxs-lookup"><span data-stu-id="901ed-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="901ed-157">Clique em **Criar**</span><span class="sxs-lookup"><span data-stu-id="901ed-157">Click **Create**</span></span>
9.  <span data-ttu-id="901ed-158">Confirme que você criou a chave `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="901ed-158">Confirm that you've created the key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="901ed-159">Adicionar um provedor de declarações à política de extensão</span><span class="sxs-lookup"><span data-stu-id="901ed-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="901ed-160">Se quiser que os usuários entrem usando a conta do Google+, você precisará definir a conta do Google+ como um provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="901ed-160">If you want users to sign in by using Google+ account, you need to define Google+ account as a claims provider.</span></span> <span data-ttu-id="901ed-161">Em outras palavras, você precisa especificar um ponto de extremidade com o qual o Azure AD B2C se comunica.</span><span class="sxs-lookup"><span data-stu-id="901ed-161">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="901ed-162">O ponto de extremidade fornece um conjunto de declarações que são usadas pelo Azure AD B2C para verificar se um usuário específico foi autenticado.</span><span class="sxs-lookup"><span data-stu-id="901ed-162">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="901ed-163">Defina a Conta do Google+ como um provedor de declarações adicionando o nó `<ClaimsProvider>` em seu arquivo de política da extensão:</span><span class="sxs-lookup"><span data-stu-id="901ed-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="901ed-164">Abra o arquivo de política de extensão (TrustFrameworkExtensions.xml) de seu diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="901ed-164">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="901ed-165">Se você precisar de um editor de XML, [experimente o Visual Studio Code](https://code.visualstudio.com/download), um editor de plataforma cruzada leve.</span><span class="sxs-lookup"><span data-stu-id="901ed-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="901ed-166">Localize a seção `<ClaimsProviders>`</span><span class="sxs-lookup"><span data-stu-id="901ed-166">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="901ed-167">Adicione o seguinte trecho XML sob o elemento `ClaimsProviders` e substitua o valor `client_id` por sua ID de cliente de aplicativo da conta do Google + antes de salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="901ed-167">Add the following XML snippet under the `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving the file.</span></span>  

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
            <!--In case of authorization code used error, we don't want the user to select his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-the-google-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="901ed-168">Registrar o provedor de declarações da conta do Google+ para um percurso do usuário de Inscrição ou Entrada</span><span class="sxs-lookup"><span data-stu-id="901ed-168">Register the Google+ account claims provider to Sign up or Sign in user journey</span></span>

<span data-ttu-id="901ed-169">O provedor de identidade foi configurado.</span><span class="sxs-lookup"><span data-stu-id="901ed-169">The identity provider has been set up.</span></span>  <span data-ttu-id="901ed-170">No entanto, ele não está disponível em qualquer uma das telas de inscrição/entrada.</span><span class="sxs-lookup"><span data-stu-id="901ed-170">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="901ed-171">Adicione o provedor de identidade da conta do Google+ ao percurso de usuário `SignUpOrSignIn` do usuário.</span><span class="sxs-lookup"><span data-stu-id="901ed-171">Add the Google+ account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="901ed-172">Para disponibilizá-lo, criamos uma duplicata de um percurso de usuário do modelo existente.</span><span class="sxs-lookup"><span data-stu-id="901ed-172">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="901ed-173">Em seguida, adicionamos o provedor de identidade da conta do Google+:</span><span class="sxs-lookup"><span data-stu-id="901ed-173">Then we add the Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="901ed-174">Se você copiou o elemento `<UserJourneys>` do arquivo de base de sua política para o arquivo de extensão (TrustFrameworkExtensions.xml), pule para esta seção.</span><span class="sxs-lookup"><span data-stu-id="901ed-174">If you copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml), you can skip to this section.</span></span>

1.  <span data-ttu-id="901ed-175">Abra o arquivo base da política (por exemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="901ed-175">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="901ed-176">Localize o elemento `<UserJourneys>` e copie todo o conteúdo do nó `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="901ed-176">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="901ed-177">Abra o arquivo de extensão (por exemplo, TrustFrameworkExtensions.xml) e localize o elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="901ed-177">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="901ed-178">Se o elemento não existir, adicione um.</span><span class="sxs-lookup"><span data-stu-id="901ed-178">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="901ed-179">Cole todo o conteúdo do nó `<UserJournesy>` copiado como um filho do elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="901ed-179">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="901ed-180">Exibir o botão</span><span class="sxs-lookup"><span data-stu-id="901ed-180">Display the button</span></span>
<span data-ttu-id="901ed-181">O elemento `<ClaimsProviderSelections>` define a lista de opções de seleção de provedor de declarações e sua ordem.</span><span class="sxs-lookup"><span data-stu-id="901ed-181">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="901ed-182">O elemento `<ClaimsProviderSelection>` é análogo a um botão de provedor de identidade em uma página de inscrição/entrada.</span><span class="sxs-lookup"><span data-stu-id="901ed-182">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="901ed-183">Se você adicionar um elemento `<ClaimsProviderSelection>` para a conta do Google+, um novo botão será exibido quando um usuário chegar à página.</span><span class="sxs-lookup"><span data-stu-id="901ed-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="901ed-184">Para adicionar este elemento:</span><span class="sxs-lookup"><span data-stu-id="901ed-184">To add this element:</span></span>

1.  <span data-ttu-id="901ed-185">Localize o nó `<UserJourney>` que inclui `Id="SignUpOrSignIn"` no percurso do usuário que você acabou de copiar.</span><span class="sxs-lookup"><span data-stu-id="901ed-185">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="901ed-186">Localize o nó `<OrchestrationStep>` que inclui `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="901ed-186">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="901ed-187">Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="901ed-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="901ed-188">Vincular o botão a uma ação</span><span class="sxs-lookup"><span data-stu-id="901ed-188">Link the button to an action</span></span>
<span data-ttu-id="901ed-189">Agora que implementou um botão, você precisará vinculá-lo a uma ação.</span><span class="sxs-lookup"><span data-stu-id="901ed-189">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="901ed-190">Nesse caso, a ação destina-se a que o Azure AD B2C se comunique com a conta do Google+ para receber um token.</span><span class="sxs-lookup"><span data-stu-id="901ed-190">The action, in this case, is for Azure AD B2C to communicate with Google+ account to receive a token.</span></span>

1.  <span data-ttu-id="901ed-191">Localize o `<OrchestrationStep>` que inclui `Order="2"` no nó `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="901ed-191">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="901ed-192">Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="901ed-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="901ed-193">Certifique-se de que o `Id` tenha o mesmo valor de `TargetClaimsExchangeId` na seção anterior</span><span class="sxs-lookup"><span data-stu-id="901ed-193">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
> * <span data-ttu-id="901ed-194">Certifique-se de que a ID `TechnicalProfileReferenceId` esteja definida como o perfil técnico criado anteriormente (Google-OAUTH).</span><span class="sxs-lookup"><span data-stu-id="901ed-194">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="901ed-195">Carregar a política ao seu locatário</span><span class="sxs-lookup"><span data-stu-id="901ed-195">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="901ed-196">No [Portal do Azure](https://portal.azure.com), alterne para o [contexto do seu locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) e abra a folha do **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="901ed-196">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="901ed-197">Selecione **Estrutura de Experiência de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="901ed-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="901ed-198">Abra a folha **Todas as Políticas**.</span><span class="sxs-lookup"><span data-stu-id="901ed-198">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="901ed-199">Selecione **Carregar Política**.</span><span class="sxs-lookup"><span data-stu-id="901ed-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="901ed-200">Marque a caixa **Substituir a política caso ela exista**.</span><span class="sxs-lookup"><span data-stu-id="901ed-200">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="901ed-201">**Carregue** TrustFrameworkExtensions.xml e verifique se ele não falhou na validação</span><span class="sxs-lookup"><span data-stu-id="901ed-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="901ed-202">Testar a política personalizada usando a opção Executar Agora</span><span class="sxs-lookup"><span data-stu-id="901ed-202">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="901ed-203">Abra as **Configurações do Azure AD B2C** e acesse a **Estrutura de Experiência de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="901ed-203">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="901ed-204">A **Executar Agora** exige que pelo menos um aplicativo esteja previamente registrado no locatário.</span><span class="sxs-lookup"><span data-stu-id="901ed-204">**Run now** requires at least one application to be preregistered on the tenant.</span></span> 
    >    <span data-ttu-id="901ed-205">Para saber como registrar aplicativos, confira os artigos [Introdução](active-directory-b2c-get-started.md) ou [Registro do aplicativo](active-directory-b2c-app-registration.md) do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="901ed-205">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="901ed-206">Abra a **B2C_1A_signup_signin**, a política personalizada da RP (terceira parte confiável) que você carregou.</span><span class="sxs-lookup"><span data-stu-id="901ed-206">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="901ed-207">Selecione **Executar Agora**.</span><span class="sxs-lookup"><span data-stu-id="901ed-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="901ed-208">Você deve conseguir entrar usando a conta do Google+.</span><span class="sxs-lookup"><span data-stu-id="901ed-208">You should be able to sign in using Google+ account.</span></span>

## <a name="optional-register-the-google-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="901ed-209">[Opcional] Registrar o provedor de declarações da conta do Google+ ao percurso de usuário de Edição de Perfil</span><span class="sxs-lookup"><span data-stu-id="901ed-209">[Optional] Register the Google+ account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="901ed-210">Convém adicionar também o provedor de identidade da conta do Google+ ao percurso de usuário `ProfileEdit` do usuário.</span><span class="sxs-lookup"><span data-stu-id="901ed-210">You may want to add the Google+ account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="901ed-211">Para disponibilizá-lo, repetimos as duas últimas etapas:</span><span class="sxs-lookup"><span data-stu-id="901ed-211">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="901ed-212">Exibir o botão</span><span class="sxs-lookup"><span data-stu-id="901ed-212">Display the button</span></span>
1.  <span data-ttu-id="901ed-213">Abra o arquivo de extensão de sua política (por exemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="901ed-213">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="901ed-214">Localize o nó `<UserJourney>` que inclui `Id="ProfileEdit"` no percurso do usuário que você acabou de copiar.</span><span class="sxs-lookup"><span data-stu-id="901ed-214">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="901ed-215">Localize o nó `<OrchestrationStep>` que inclui `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="901ed-215">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="901ed-216">Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="901ed-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="901ed-217">Vincular o botão a uma ação</span><span class="sxs-lookup"><span data-stu-id="901ed-217">Link the button to an action</span></span>
1.  <span data-ttu-id="901ed-218">Localize o `<OrchestrationStep>` que inclui `Order="2"` no nó `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="901ed-218">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="901ed-219">Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="901ed-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="901ed-220">Testar a política personalizada de Edição de Perfil usando Executar Agora</span><span class="sxs-lookup"><span data-stu-id="901ed-220">Test the custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="901ed-221">Abra as **Configurações do Azure AD B2C** e acesse a **Estrutura de Experiência de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="901ed-221">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="901ed-222">Abra **B2C_1A_signup_signin**, a política personalizada da RP (terceira parte confiável) que você carregou.</span><span class="sxs-lookup"><span data-stu-id="901ed-222">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="901ed-223">Selecione **Executar Agora**.</span><span class="sxs-lookup"><span data-stu-id="901ed-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="901ed-224">Você deve conseguir entrar usando a conta do Google+.</span><span class="sxs-lookup"><span data-stu-id="901ed-224">You should be able to sign in using Google+ account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="901ed-225">Baixar os arquivos da política completa</span><span class="sxs-lookup"><span data-stu-id="901ed-225">Download the complete policy files</span></span>
<span data-ttu-id="901ed-226">Opcional: recomendamos a criação de seu cenário usando seus próprios arquivos de política personalizada após a conclusão do passo a passo Introdução às políticas personalizadas em vez de usar esses arquivos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="901ed-226">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="901ed-227">Arquivos de política de exemplo para referência</span><span class="sxs-lookup"><span data-stu-id="901ed-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
