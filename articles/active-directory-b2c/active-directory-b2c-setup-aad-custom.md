---
title: "Azure Active Directory B2C: adicionar um provedor do Azure AD usando políticas personalizadas | Microsoft Docs"
description: "Saiba mais sobre as políticas personalizadas do Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="aa8d9-103">Azure Active Directory B2C: entrar usando contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa8d9-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="aa8d9-104">Este artigo mostra como tooenable entrar para usuários de uma organização específica do Azure Active Directory (AD do Azure) através do uso de saudação do [políticas personalizadas](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-104">This article shows you how tooenable sign-in for users from a specific Azure Active Directory (Azure AD) organization through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa8d9-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aa8d9-105">Prerequisites</span></span>

<span data-ttu-id="aa8d9-106">Olá concluir as etapas em Olá [guia de Introdução com políticas personalizadas](active-directory-b2c-get-started-custom.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="aa8d9-107">As etapas incluem:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-107">These steps include:</span></span>

1. <span data-ttu-id="aa8d9-108">Criar um locatário do Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="aa8d9-109">Criar um aplicativo Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="aa8d9-110">Registrar dois aplicativos do mecanismo de políticas.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="aa8d9-111">Configurar chaves.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-111">Setting up keys.</span></span>
5. <span data-ttu-id="aa8d9-112">Configurar o pacote de inicializador de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-112">Setting up hello starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="aa8d9-113">Criar um aplicativo Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa8d9-113">Create an Azure AD app</span></span>

<span data-ttu-id="aa8d9-114">tooenable entrar para usuários de uma determinada organização do AD do Azure, você precisa tooregister um aplicativo no locatário Olá organizacional do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-114">tooenable sign-in for users from a specific Azure AD organization, you need tooregister an application within hello organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="aa8d9-115">Podemos usar "contoso.com" para locatário Olá organizacional do AD do Azure e "fabrikamb2c.onmicrosoft.com" como locatário hello Azure AD B2C em Olá instruções a seguir.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-115">We use "contoso.com" for hello organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as hello Azure AD B2C tenant in hello following instructions.</span></span>

1. <span data-ttu-id="aa8d9-116">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="aa8d9-117">Na barra superior do hello, selecione sua conta.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-117">On hello top bar, select your account.</span></span> <span data-ttu-id="aa8d9-118">De saudação **diretório** , escolha locatário Olá organizacional do AD do Azure onde deseja tooregister seu aplicativo (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-118">From hello **Directory** list, choose hello organizational Azure AD tenant where you want tooregister your application (contoso.com).</span></span>
1. <span data-ttu-id="aa8d9-119">Selecione **mais serviços** no painel esquerdo do hello e procure "Registros de aplicativo".</span><span class="sxs-lookup"><span data-stu-id="aa8d9-119">Select **More services** in hello left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="aa8d9-120">Selecione **Novo registro de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="aa8d9-121">Insira um nome para seu aplicativo (por exemplo, `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="aa8d9-122">Selecione **aplicativo Web / API** para o tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-122">Select **Web app / API** for hello application type.</span></span>
1. <span data-ttu-id="aa8d9-123">Para **URL de logon**, digite Olá seguindo a URL, onde `yourtenant` é substituído pelo nome de saudação do seu locatário do Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="aa8d9-123">For **Sign-on URL**, enter hello following URL, where `yourtenant` is replaced by hello name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="aa8d9-124">Salvar o ID do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-124">Save hello application ID.</span></span>
1. <span data-ttu-id="aa8d9-125">Selecione o aplicativo hello recém-criado.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-125">Select hello newly created application.</span></span>
1. <span data-ttu-id="aa8d9-126">Em Olá **configurações** folha, selecione **chaves**.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-126">Under hello **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="aa8d9-127">Crie uma nova chave e salve-a.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-127">Create a new key, and save it.</span></span> <span data-ttu-id="aa8d9-128">Você o usará em etapas Olá Olá próxima seção.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-128">You will use it in hello steps in hello next section.</span></span>

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a><span data-ttu-id="aa8d9-129">Adicionar tooAzure de chave de saudação do AD do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="aa8d9-129">Add hello Azure AD key tooAzure AD B2C</span></span>

<span data-ttu-id="aa8d9-130">É necessário a chave de aplicativo toostore Olá contoso.com em seu locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-130">You need toostore hello contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="aa8d9-131">toodo isso:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-131">toodo this:</span></span>
1. <span data-ttu-id="aa8d9-132">Go locatário tooyour B2C do Azure AD e selecione **B2C configurações** > **identidade experiência Framework** > **chaves política**.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-132">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="aa8d9-133">Selecione **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-133">Select **+Add**.</span></span>
1. <span data-ttu-id="aa8d9-134">Selecione ou insira estas opções:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-134">Select or enter these options:</span></span>
   * <span data-ttu-id="aa8d9-135">Selecione **Manual**.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-135">Select **Manual**.</span></span>
   * <span data-ttu-id="aa8d9-136">Para o **Nome**, escolha um nome que corresponda ao nome do locatário do Azure AD (por exemplo, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="aa8d9-137">prefixo de saudação `B2C_1A_` é adicionado automaticamente toohello nome da chave.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-137">hello prefix `B2C_1A_` is added automatically toohello name of your key.</span></span>
   * <span data-ttu-id="aa8d9-138">Cole a chave de aplicativo hello **segredo** caixa.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-138">Paste your application key in hello **Secret** box.</span></span>
   * <span data-ttu-id="aa8d9-139">Selecione **Assinatura**.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-139">Select **Signature**.</span></span>
1. <span data-ttu-id="aa8d9-140">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-140">Select **Create**.</span></span>
1. <span data-ttu-id="aa8d9-141">Confirme que você criou a chave Olá `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-141">Confirm that you've created hello key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="aa8d9-142">Adicionar um provedor de declarações à política base</span><span class="sxs-lookup"><span data-stu-id="aa8d9-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="aa8d9-143">Se você quiser usuários toosign no usando o AD do Azure, você precisa toodefine AD do Azure como um provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-143">If you want users toosign in by using Azure AD, you need toodefine Azure AD as a claims provider.</span></span> <span data-ttu-id="aa8d9-144">Em outras palavras, você precisa toospecify um ponto de extremidade do Azure AD B2C se comunicará.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-144">In other words, you need toospecify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="aa8d9-145">ponto de extremidade Olá fornecem um conjunto de declarações que são usados pelo Azure AD B2C tooverify que um usuário específico autenticado.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-145">hello endpoint will provide a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span> 

<span data-ttu-id="aa8d9-146">Você pode definir o AD do Azure como um provedor de declarações adicionando toohello do AD do Azure `<ClaimsProvider>` nó no arquivo de extensão de saudação da política:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-146">You can define Azure AD as a claims provider by adding Azure AD toohello `<ClaimsProvider>` node in hello extension file of your policy:</span></span>

1. <span data-ttu-id="aa8d9-147">Abra o arquivo de extensão da saudação (TrustFrameworkExtensions.xml) do seu diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-147">Open hello extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="aa8d9-148">Localize Olá `<ClaimsProviders>` seção.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-148">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="aa8d9-149">Se não existir, adicione-o nó raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-149">If it does not exist, add it under hello root node.</span></span>
1. <span data-ttu-id="aa8d9-150">Adicione um novo nó `<ClaimsProvider>` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
                </OutputClaims>
                <OutputClaimsTransformations>
                    <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
                    <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
                    <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
                    <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
                </OutputClaimsTransformations>
                <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
            </TechnicalProfile>
        </TechnicalProfiles>
    </ClaimsProvider>
    ```

1. <span data-ttu-id="aa8d9-151">Em Olá `<ClaimsProvider>` nó, o valor de saudação de atualização para `<Domain>` tooa valor exclusivo que pode ser usado toodistinguish-lo de outros provedores de identidade.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-151">Under hello `<ClaimsProvider>` node, update hello value for `<Domain>` tooa unique value that can be used toodistinguish it from other identity providers.</span></span>
1. <span data-ttu-id="aa8d9-152">Em Olá `<ClaimsProvider>` nó, o valor de saudação de atualização para `<DisplayName>` tooa nome amigável do hello provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-152">Under hello `<ClaimsProvider>` node, update hello value for `<DisplayName>` tooa friendly name for hello claims provider.</span></span> <span data-ttu-id="aa8d9-153">Esse valor não é usado atualmente.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-153">This value is not currently used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="aa8d9-154">Atualizar perfil técnica Olá</span><span class="sxs-lookup"><span data-stu-id="aa8d9-154">Update hello technical profile</span></span>

<span data-ttu-id="aa8d9-155">tooget um token do ponto de extremidade do hello AD do Azure, você precisa de protocolos de saudação toodefine que o Azure AD B2C deve usar toocommunicate com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-155">tooget a token from hello Azure AD endpoint, you need toodefine hello protocols that Azure AD B2C should use toocommunicate with Azure AD.</span></span> <span data-ttu-id="aa8d9-156">Isso é feito dentro Olá `<TechnicalProfile>` elemento `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-156">This is done inside hello `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="aa8d9-157">Atualizar a ID de saudação do hello `<TechnicalProfile>` nó.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-157">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="aa8d9-158">Essa ID é usada toorefer toothis perfil técnico de outras partes da política de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-158">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
1. <span data-ttu-id="aa8d9-159">Atualizar o valor Olá para `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-159">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="aa8d9-160">Esse valor será exibido no botão logon Olá em sua tela de entrada.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-160">This value will be displayed on hello sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="aa8d9-161">Atualizar o valor Olá para `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-161">Update hello value for `<Description>`.</span></span>
1. <span data-ttu-id="aa8d9-162">AD do Azure usa o protocolo de saudação OpenID Connect, para garantir que esse valor Olá para `<Protocol>` é `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-162">Azure AD uses hello OpenID Connect protocol, so ensure that hello value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="aa8d9-163">Você precisa Olá tooupdate `<Metadata>` seção no arquivo XML de saudação chamado definições de configuração do tooearlier tooreflect Olá para o determinado locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-163">You need tooupdate hello `<Metadata>` section in hello XML file referred tooearlier tooreflect hello configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="aa8d9-164">No arquivo XML de hello, atualize valores de metadados de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-164">In hello XML file, update hello metadata values as follows:</span></span>

1. <span data-ttu-id="aa8d9-165">Definir `<Item Key="METADATA">` muito`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, onde `yourAzureADtenant` é o nome do locatário do AD do Azure (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-165">Set `<Item Key="METADATA">` too`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="aa8d9-166">Abra seu navegador e acesse toohello `METADATA` URL que você acabou de ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-166">Open your browser and go toohello `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="aa8d9-167">No navegador hello, procure o objeto de 'emissor' hello e copie seu valor.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-167">In hello browser, look for hello 'issuer' object and copy its value.</span></span> <span data-ttu-id="aa8d9-168">Deve se parecer com o seguinte Olá: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-168">It should look like hello following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="aa8d9-169">Cole o valor de saudação para `<Item Key="ProviderName">` no arquivo XML de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-169">Paste hello value for `<Item Key="ProviderName">` in hello XML file.</span></span>
1. <span data-ttu-id="aa8d9-170">Definir `<Item Key="client_id">` toohello ID do aplicativo de registro do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-170">Set `<Item Key="client_id">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="aa8d9-171">Definir `<Item Key="IdTokenAudience">` toohello ID do aplicativo de registro do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-171">Set `<Item Key="IdTokenAudience">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="aa8d9-172">Certifique-se de que `<Item Key="response_types">` está definido muito`id_token`.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-172">Ensure that `<Item Key="response_types">` is set too`id_token`.</span></span>
1. <span data-ttu-id="aa8d9-173">Certifique-se de que `<Item Key="UsePolicyInRedirectUri">` está definido muito`false`.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set too`false`.</span></span>

<span data-ttu-id="aa8d9-174">Você também precisa toolink segredo de saudação do AD do Azure que você registrou no seu toohello de locatário do Azure AD B2C do Azure AD `<ClaimsProvider>` informações:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-174">You also need toolink hello Azure AD secret that you registered in your Azure AD B2C tenant toohello Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="aa8d9-175">Em Olá `<CryptographicKeys>` seção Olá precede o arquivo XML, atualize o valor Olá para `StorageReferenceId` toohello ID de referência de segredo Olá definido (por exemplo, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-175">In hello `<CryptographicKeys>` section in hello preceding XML file, update hello value for `StorageReferenceId` toohello reference ID of hello secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="aa8d9-176">Carregue o arquivo de extensão de saudação para verificação</span><span class="sxs-lookup"><span data-stu-id="aa8d9-176">Upload hello extension file for verification</span></span>

<span data-ttu-id="aa8d9-177">Agora, você configurou sua política de modo que o Azure AD B2C Saiba como toocommunicate com seu diretório do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-177">By now, you have configured your policy so that Azure AD B2C knows how toocommunicate with your Azure AD directory.</span></span> <span data-ttu-id="aa8d9-178">Tente carregar o arquivo de extensão de saudação do seu tooconfirm apenas de política que ele não tem quaisquer problemas até o momento.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-178">Try uploading hello extension file of your policy just tooconfirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="aa8d9-179">toodo para:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-179">toodo so:</span></span>

1. <span data-ttu-id="aa8d9-180">Olá abrir **todas as políticas** folha em seu locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-180">Open hello **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="aa8d9-181">Verificar Olá **substituir a política de saudação se ela existe** caixa.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-181">Check hello **Overwrite hello policy if it exists** box.</span></span>
1. <span data-ttu-id="aa8d9-182">Carregar arquivo de extensão da saudação (TrustFrameworkExtensions.xml) e certifique-se de que ele não falha na validação de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-182">Upload hello extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail hello validation.</span></span>

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a><span data-ttu-id="aa8d9-183">Registrar a jornada de usuário tooa do provedor de declarações de AD do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="aa8d9-183">Register hello Azure AD claims provider tooa user journey</span></span>

<span data-ttu-id="aa8d9-184">Agora, você precisa tooadd Olá AD do Azure identidade provedor tooone de jornadas seu usuário.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-184">You now need tooadd hello Azure AD identity provider tooone of your user journeys.</span></span> <span data-ttu-id="aa8d9-185">Neste ponto, o provedor de identidade Olá foi configurado, mas não está disponível em qualquer uma das telas de entrada-o/entrada hello.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-185">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="aa8d9-186">toomake-las disponíveis, criaremos uma duplicata de uma jornada de usuário do modelo existente e, em seguida, modificá-lo para que ele também tem o provedor de identidade de saudação do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-186">toomake it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has hello Azure AD identity provider:</span></span>

1. <span data-ttu-id="aa8d9-187">Abra o arquivo de base de saudação da política (por exemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-187">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="aa8d9-188">Localize Olá `<UserJourneys>` Olá de elemento e copie todo `<UserJourney>` nó inclui `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-188">Find hello `<UserJourneys>` element and copy hello entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="aa8d9-189">Abra o arquivo de extensão da saudação (por exemplo, TrustFrameworkExtensions.xml) e localize Olá `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-189">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="aa8d9-190">Se o elemento de saudação não existir, adicione um.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-190">If hello element doesn't exist, add one.</span></span>
1. <span data-ttu-id="aa8d9-191">Saudação de colar toda `<UserJourney>` nó que você copiou como um filho do hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-191">Paste hello entire `<UserJourney>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="aa8d9-192">Renomear a ID de saudação do jornada de usuário nova hello (por exemplo, renomear como `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-192">Rename hello ID of hello new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="aa8d9-193">Saudação de exibição "button"</span><span class="sxs-lookup"><span data-stu-id="aa8d9-193">Display hello "button"</span></span>

<span data-ttu-id="aa8d9-194">Olá `<ClaimsProviderSelection>` elemento é análogo tooan botão de provedor de identidade em uma tela de entrada-o/entrar.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-194">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="aa8d9-195">Se você adicionar um `<ClaimsProviderSelection>` elemento do AD do Azure, um novo botão aparece quando um usuário chega na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="aa8d9-196">tooadd este elemento:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-196">tooadd this element:</span></span>

1. <span data-ttu-id="aa8d9-197">Localize Olá `<OrchestrationStep>` nó inclui `Order="1"` em jornada saudação do usuário que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-197">Find hello `<OrchestrationStep>` node that includes `Order="1"` in hello user journey that you just created.</span></span>
1. <span data-ttu-id="aa8d9-198">Adicione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-198">Add hello following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="aa8d9-199">Definir `TargetClaimsExchangeId` valor apropriado tooan.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-199">Set `TargetClaimsExchangeId` tooan appropriate value.</span></span> <span data-ttu-id="aa8d9-200">É recomendável seguir Olá a mesma convenção de outras pessoas:  *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-200">We recommend following hello same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="aa8d9-201">Ação de link de saudação botão tooan</span><span class="sxs-lookup"><span data-stu-id="aa8d9-201">Link hello button tooan action</span></span>

<span data-ttu-id="aa8d9-202">Agora que você tem um botão em vigor, é necessário toolink-tooan ação.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-202">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="aa8d9-203">ação Hello, nesse caso, é para o Azure AD B2C toocommunicate com AD do Azure tooreceive um token.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-203">hello action, in this case, is for Azure AD B2C toocommunicate with Azure AD tooreceive a token.</span></span> <span data-ttu-id="aa8d9-204">Ação de link Olá botão tooan vinculando perfil técnico Olá para o seu provedor de declarações do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-204">Link hello button tooan action by linking hello technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="aa8d9-205">Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-205">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
1. <span data-ttu-id="aa8d9-206">Adicione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-206">Add hello following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="aa8d9-207">Atualização `Id` toohello mesmo valor de `TargetClaimsExchangeId` em Olá anterior seção.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-207">Update `Id` toohello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
1. <span data-ttu-id="aa8d9-208">Atualização `TechnicalProfileReferenceId` toohello ID da saudação técnica perfil que você criou anteriormente (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-208">Update `TechnicalProfileReferenceId` toohello ID of hello technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="aa8d9-209">Carregar arquivo de extensão atualizada Olá</span><span class="sxs-lookup"><span data-stu-id="aa8d9-209">Upload hello updated extension file</span></span>

<span data-ttu-id="aa8d9-210">Você concluiu a modificar arquivo de extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-210">You are done modifying hello extension file.</span></span> <span data-ttu-id="aa8d9-211">Salve-o.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-211">Save it.</span></span> <span data-ttu-id="aa8d9-212">Em seguida, carregar o arquivo hello e certifique-se de que todas as validações de êxito.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-212">Then upload hello file, and ensure that all validations succeed.</span></span>

### <a name="update-hello-rp-file"></a><span data-ttu-id="aa8d9-213">Atualizar o arquivo do RP Olá</span><span class="sxs-lookup"><span data-stu-id="aa8d9-213">Update hello RP file</span></span>

<span data-ttu-id="aa8d9-214">Você agora precisa tooupdate Olá terceira parte confiável (RP) arquivo irá iniciar a jornada saudação do usuário que você acabou de criar:</span><span class="sxs-lookup"><span data-stu-id="aa8d9-214">You now need tooupdate hello relying party (RP) file that will initiate hello user journey that you just created:</span></span>

1. <span data-ttu-id="aa8d9-215">Faça uma cópia do SignUpOrSignIn.xml no diretório de trabalho e renomeá-lo (por exemplo, renomeá-lo de tooSignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it tooSignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="aa8d9-216">Olá novo Olá abrir arquivo e atualização `PolicyId` atributo `<TrustFrameworkPolicy>` com um valor exclusivo (por exemplo, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-216">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="aa8d9-217">Esse será o nome hello da política (por exemplo, B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-217">This will be hello name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="aa8d9-218">Modificar Olá `ReferenceId` atributo `<DefaultUserJourney>` toomatch Olá ID de jornada de usuário nova Olá que você criou (SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-218">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello ID of hello new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="aa8d9-219">Salve suas alterações e carregar o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-219">Save your changes, and upload hello file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="aa8d9-220">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="aa8d9-220">Troubleshooting</span></span>

<span data-ttu-id="aa8d9-221">Testar política personalizada do hello carregado abrindo sua folha e clicando em **executar agora**.</span><span class="sxs-lookup"><span data-stu-id="aa8d9-221">Test hello custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="aa8d9-222">problemas de toodiagnose, leia sobre [de solução de problemas](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-222">toodiagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa8d9-223">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aa8d9-223">Next steps</span></span>

<span data-ttu-id="aa8d9-224">Fornecer comentários muito[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="aa8d9-224">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
