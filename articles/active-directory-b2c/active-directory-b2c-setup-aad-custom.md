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
ms.openlocfilehash: 6c073d70debfdc3560405955d65fa9ccaa7d8b1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="a9941-103">Azure Active Directory B2C: entrar usando contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9941-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="a9941-104">Este artigo mostra como habilitar a entrada para usuários de uma organização específica do Azure AD (Azure Active Directory) por meio do uso de [políticas personalizadas](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a9941-104">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9941-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a9941-105">Prerequisites</span></span>

<span data-ttu-id="a9941-106">Conclua as etapas no artigo [Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a9941-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="a9941-107">As etapas incluem:</span><span class="sxs-lookup"><span data-stu-id="a9941-107">These steps include:</span></span>

1. <span data-ttu-id="a9941-108">Criar um locatário do Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="a9941-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="a9941-109">Criar um aplicativo Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a9941-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="a9941-110">Registrar dois aplicativos do mecanismo de políticas.</span><span class="sxs-lookup"><span data-stu-id="a9941-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="a9941-111">Configurar chaves.</span><span class="sxs-lookup"><span data-stu-id="a9941-111">Setting up keys.</span></span>
5. <span data-ttu-id="a9941-112">Configurar o pacote de início.</span><span class="sxs-lookup"><span data-stu-id="a9941-112">Setting up the starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="a9941-113">Criar um aplicativo Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9941-113">Create an Azure AD app</span></span>

<span data-ttu-id="a9941-114">Para habilitar a entrada para usuários de uma organização específica do Azure AD, você precisa registrar um aplicativo no locatário organizacional do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9941-114">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="a9941-115">Usamos "contoso.com" como o locatário do Azure AD da organização e "fabrikamb2c.onmicrosoft.com" como o locatário do Azure AD B2C nas instruções a seguir.</span><span class="sxs-lookup"><span data-stu-id="a9941-115">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span></span>

1. <span data-ttu-id="a9941-116">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9941-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="a9941-117">Na barra superior, selecione sua conta.</span><span class="sxs-lookup"><span data-stu-id="a9941-117">On the top bar, select your account.</span></span> <span data-ttu-id="a9941-118">Na lista **Diretório**, escolha o locatário do Azure AD organizacional em que deseja registrar seu aplicativo (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="a9941-118">From the **Directory** list, choose the organizational Azure AD tenant where you want to register your application (contoso.com).</span></span>
1. <span data-ttu-id="a9941-119">Selecione **Mais serviços** no painel esquerdo e pesquise por “Registros do aplicativo”.</span><span class="sxs-lookup"><span data-stu-id="a9941-119">Select **More services** in the left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="a9941-120">Selecione **Novo registro de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="a9941-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="a9941-121">Insira um nome para seu aplicativo (por exemplo, `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="a9941-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="a9941-122">Selecione **Aplicativo Web/API** como o tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a9941-122">Select **Web app / API** for the application type.</span></span>
1. <span data-ttu-id="a9941-123">Para a **URL de Logon**, insira a URL a seguir, em que `yourtenant` é substituído pelo nome do seu locatário do Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="a9941-123">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="a9941-124">Salve a ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a9941-124">Save the application ID.</span></span>
1. <span data-ttu-id="a9941-125">Selecione o aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="a9941-125">Select the newly created application.</span></span>
1. <span data-ttu-id="a9941-126">Na folha **Configurações**, selecione **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="a9941-126">Under the **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="a9941-127">Crie uma nova chave e salve-a.</span><span class="sxs-lookup"><span data-stu-id="a9941-127">Create a new key, and save it.</span></span> <span data-ttu-id="a9941-128">Você a usará nas etapas da próxima seção.</span><span class="sxs-lookup"><span data-stu-id="a9941-128">You will use it in the steps in the next section.</span></span>

## <a name="add-the-azure-ad-key-to-azure-ad-b2c"></a><span data-ttu-id="a9941-129">Adicionar a chave do Azure AD ao Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a9941-129">Add the Azure AD key to Azure AD B2C</span></span>

<span data-ttu-id="a9941-130">Você precisa armazenar a chave do aplicativo de contoso.com em seu locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a9941-130">You need to store the contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="a9941-131">Para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="a9941-131">To do this:</span></span>
1. <span data-ttu-id="a9941-132">Vá até seu locatário do Azure AD B2C e abra **Configurações B2C** > **Identity Experience Framework** > **Chaves de Política**.</span><span class="sxs-lookup"><span data-stu-id="a9941-132">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="a9941-133">Selecione **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a9941-133">Select **+Add**.</span></span>
1. <span data-ttu-id="a9941-134">Selecione ou insira estas opções:</span><span class="sxs-lookup"><span data-stu-id="a9941-134">Select or enter these options:</span></span>
   * <span data-ttu-id="a9941-135">Selecione **Manual**.</span><span class="sxs-lookup"><span data-stu-id="a9941-135">Select **Manual**.</span></span>
   * <span data-ttu-id="a9941-136">Para o **Nome**, escolha um nome que corresponda ao nome do locatário do Azure AD (por exemplo, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="a9941-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="a9941-137">O prefixo `B2C_1A_` será adicionado automaticamente ao nome da chave.</span><span class="sxs-lookup"><span data-stu-id="a9941-137">The prefix `B2C_1A_` is added automatically to the name of your key.</span></span>
   * <span data-ttu-id="a9941-138">Cole a chave do aplicativo na caixa de texto **Segredo**.</span><span class="sxs-lookup"><span data-stu-id="a9941-138">Paste your application key in the **Secret** box.</span></span>
   * <span data-ttu-id="a9941-139">Selecione **Assinatura**.</span><span class="sxs-lookup"><span data-stu-id="a9941-139">Select **Signature**.</span></span>
1. <span data-ttu-id="a9941-140">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a9941-140">Select **Create**.</span></span>
1. <span data-ttu-id="a9941-141">Confirme que você criou a chave `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="a9941-141">Confirm that you've created the key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="a9941-142">Adicionar um provedor de declarações à política base</span><span class="sxs-lookup"><span data-stu-id="a9941-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="a9941-143">Se quiser que os usuários entrem usando o Azure AD, você precisará definir o Azure AD como um provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="a9941-143">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span></span> <span data-ttu-id="a9941-144">Em outras palavras, você precisa especificar um ponto de extremidade com o qual o Azure AD B2C se comunicará.</span><span class="sxs-lookup"><span data-stu-id="a9941-144">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="a9941-145">O ponto de extremidade fornecerá um conjunto de declarações que são usadas pelo Azure AD B2C para verificar se um usuário específico foi autenticado.</span><span class="sxs-lookup"><span data-stu-id="a9941-145">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span> 

<span data-ttu-id="a9941-146">Você pode definir o Azure AD como um provedor de declarações adicionando o Azure AD ao nó `<ClaimsProvider>` no arquivo de extensão de sua política:</span><span class="sxs-lookup"><span data-stu-id="a9941-146">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span></span>

1. <span data-ttu-id="a9941-147">Abra o arquivo de extensão (TrustFrameworkExtensions.xml) no diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a9941-147">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="a9941-148">Localize a seção `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="a9941-148">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="a9941-149">Caso ela não exista, adicione-a sob o nó raiz.</span><span class="sxs-lookup"><span data-stu-id="a9941-149">If it does not exist, add it under the root node.</span></span>
1. <span data-ttu-id="a9941-150">Adicione um novo nó `<ClaimsProvider>` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a9941-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

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

1. <span data-ttu-id="a9941-151">Sob o nó `<ClaimsProvider>`, atualize o valor de `<Domain>` para um valor exclusivo que pode ser usado para distinguir de outros provedores de identidade.</span><span class="sxs-lookup"><span data-stu-id="a9941-151">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span></span>
1. <span data-ttu-id="a9941-152">Sob o nó `<ClaimsProvider>`, atualize o valor de `<DisplayName>` para um nome amigável do provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="a9941-152">Under the `<ClaimsProvider>` node, update the value for `<DisplayName>` to a friendly name for the claims provider.</span></span> <span data-ttu-id="a9941-153">Esse valor não é usado atualmente.</span><span class="sxs-lookup"><span data-stu-id="a9941-153">This value is not currently used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="a9941-154">Atualizar o perfil técnico</span><span class="sxs-lookup"><span data-stu-id="a9941-154">Update the technical profile</span></span>

<span data-ttu-id="a9941-155">Para obter um token do ponto de extremidade do Azure AD, você precisa definir os protocolos que o Azure AD B2C deve usar para se comunicar com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9941-155">To get a token from the Azure AD endpoint, you need to define the protocols that Azure AD B2C should use to communicate with Azure AD.</span></span> <span data-ttu-id="a9941-156">Isso é feito no elemento `<TechnicalProfile>` do `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="a9941-156">This is done inside the `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="a9941-157">Atualize a ID do nó `<TechnicalProfile>`.</span><span class="sxs-lookup"><span data-stu-id="a9941-157">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="a9941-158">Essa ID é usada para se referir a esse perfil técnico em outras partes da política.</span><span class="sxs-lookup"><span data-stu-id="a9941-158">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
1. <span data-ttu-id="a9941-159">Atualize o valor de `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="a9941-159">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="a9941-160">Esse valor será exibido no botão de entrada em sua tela de entrada.</span><span class="sxs-lookup"><span data-stu-id="a9941-160">This value will be displayed on the sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="a9941-161">Atualize o valor de `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="a9941-161">Update the value for `<Description>`.</span></span>
1. <span data-ttu-id="a9941-162">O Azure AD usa o protocolo OpenID Connect, portanto, verifique se o valor de `<Protocol>` é `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="a9941-162">Azure AD uses the OpenID Connect protocol, so ensure that the value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="a9941-163">Você precisa atualizar a seção `<Metadata>` no arquivo XML mencionado anteriormente para refletir as definições de configuração do locatário específico do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9941-163">You need to update the `<Metadata>` section in the XML file referred to earlier to reflect the configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="a9941-164">No arquivo XML, atualize os valores de metadados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a9941-164">In the XML file, update the metadata values as follows:</span></span>

1. <span data-ttu-id="a9941-165">Defina `<Item Key="METADATA">` como `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, em que `yourAzureADtenant` é o nome do locatário do Azure AD (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="a9941-165">Set `<Item Key="METADATA">` to `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="a9941-166">Abra o navegador e navegue para a URL `METADATA` que você acabou de atualizar.</span><span class="sxs-lookup"><span data-stu-id="a9941-166">Open your browser and go to the `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="a9941-167">No navegador, procure o objeto “emissor” e copie seu valor.</span><span class="sxs-lookup"><span data-stu-id="a9941-167">In the browser, look for the 'issuer' object and copy its value.</span></span> <span data-ttu-id="a9941-168">Ele deverá ter esta aparência: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="a9941-168">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="a9941-169">Cole o valor de `<Item Key="ProviderName">` no arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="a9941-169">Paste the value for `<Item Key="ProviderName">` in the XML file.</span></span>
1. <span data-ttu-id="a9941-170">Defina `<Item Key="client_id">` como a ID do aplicativo no registro de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a9941-170">Set `<Item Key="client_id">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="a9941-171">Defina `<Item Key="IdTokenAudience">` como a ID do aplicativo no registro de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a9941-171">Set `<Item Key="IdTokenAudience">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="a9941-172">Verifique se `<Item Key="response_types">` está definido como `id_token`.</span><span class="sxs-lookup"><span data-stu-id="a9941-172">Ensure that `<Item Key="response_types">` is set to `id_token`.</span></span>
1. <span data-ttu-id="a9941-173">Verifique se `<Item Key="UsePolicyInRedirectUri">` está definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="a9941-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set to `false`.</span></span>

<span data-ttu-id="a9941-174">Você também precisa vincular o segredo do Azure AD que você registrou no locatário do Azure AD B2C às informações de `<ClaimsProvider>` do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a9941-174">You also need to link the Azure AD secret that you registered in your Azure AD B2C tenant to the Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="a9941-175">Na seção `<CryptographicKeys>` do arquivo XML anterior, atualize o valor de `StorageReferenceId` para a ID de referência do segredo definido (por exemplo, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="a9941-175">In the `<CryptographicKeys>` section in the preceding XML file, update the value for `StorageReferenceId` to the reference ID of the secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="a9941-176">Carregar o arquivo de extensão para verificação</span><span class="sxs-lookup"><span data-stu-id="a9941-176">Upload the extension file for verification</span></span>

<span data-ttu-id="a9941-177">A essa altura, você já terá configurado a política, de forma que o Azure AD B2C saiba como se comunicar com o diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9941-177">By now, you have configured your policy so that Azure AD B2C knows how to communicate with your Azure AD directory.</span></span> <span data-ttu-id="a9941-178">Tente carregar o arquivo de extensão da política apenas para confirmar se ele não apresenta problemas até o momento.</span><span class="sxs-lookup"><span data-stu-id="a9941-178">Try uploading the extension file of your policy just to confirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="a9941-179">Para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="a9941-179">To do so:</span></span>

1. <span data-ttu-id="a9941-180">Abra a folha **Todas as Políticas** no locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a9941-180">Open the **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="a9941-181">Marque a caixa **Substituir a política caso ela exista**.</span><span class="sxs-lookup"><span data-stu-id="a9941-181">Check the **Overwrite the policy if it exists** box.</span></span>
1. <span data-ttu-id="a9941-182">Carregue o arquivo de extensão (TrustFrameworkExtensions.xml) e verifique se ele não falhou na validação.</span><span class="sxs-lookup"><span data-stu-id="a9941-182">Upload the extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail the validation.</span></span>

## <a name="register-the-azure-ad-claims-provider-to-a-user-journey"></a><span data-ttu-id="a9941-183">Registrar o provedor de declarações do Azure AD em um percurso do usuário</span><span class="sxs-lookup"><span data-stu-id="a9941-183">Register the Azure AD claims provider to a user journey</span></span>

<span data-ttu-id="a9941-184">Agora, você precisa adicionar o provedor de identidade do Azure AD a um dos percursos do usuário.</span><span class="sxs-lookup"><span data-stu-id="a9941-184">You now need to add the Azure AD identity provider to one of your user journeys.</span></span> <span data-ttu-id="a9941-185">Neste ponto, o provedor de identidade foi definido, mas não está disponível em nenhuma das telas de inscrição/entrada.</span><span class="sxs-lookup"><span data-stu-id="a9941-185">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="a9941-186">Para disponibilizá-lo, criaremos uma duplicata de um modelo de percurso do usuário existente e, depois, o modificaremos para que ele também tenha o provedor de identidade do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a9941-186">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span></span>

1. <span data-ttu-id="a9941-187">Abra o arquivo base da política (por exemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="a9941-187">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="a9941-188">Localize o elemento `<UserJourneys>` e copie todo o nó `<UserJourney>`, que inclui `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="a9941-188">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="a9941-189">Abra o arquivo de extensão (por exemplo, TrustFrameworkExtensions.xml) e localize o elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="a9941-189">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="a9941-190">Se o elemento não existir, adicione um.</span><span class="sxs-lookup"><span data-stu-id="a9941-190">If the element doesn't exist, add one.</span></span>
1. <span data-ttu-id="a9941-191">Cole todo o nó `<UserJourney>` copiado como um filho do elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="a9941-191">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="a9941-192">Renomeie a ID do novo Percurso do Usuário (por exemplo, renomeie como `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="a9941-192">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-the-button"></a><span data-ttu-id="a9941-193">Exibir o “botão”</span><span class="sxs-lookup"><span data-stu-id="a9941-193">Display the "button"</span></span>

<span data-ttu-id="a9941-194">O elemento `<ClaimsProviderSelection>` é análogo a um botão de provedor de identidade em uma tela de inscrição/conexão.</span><span class="sxs-lookup"><span data-stu-id="a9941-194">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="a9941-195">Se você adicionar um elemento `<ClaimsProviderSelection>` do Azure AD, um novo botão será exibido quando um usuário chegar à página.</span><span class="sxs-lookup"><span data-stu-id="a9941-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="a9941-196">Para adicionar este elemento:</span><span class="sxs-lookup"><span data-stu-id="a9941-196">To add this element:</span></span>

1. <span data-ttu-id="a9941-197">Localize o nó `<OrchestrationStep>` que inclui `Order="1"` no Percurso do Usuário que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="a9941-197">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you just created.</span></span>
1. <span data-ttu-id="a9941-198">Adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a9941-198">Add the following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="a9941-199">Defina `TargetClaimsExchangeId` com um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="a9941-199">Set `TargetClaimsExchangeId` to an appropriate value.</span></span> <span data-ttu-id="a9941-200">Recomendamos seguir a mesma convenção que os outros: *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="a9941-200">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="a9941-201">Vincular o botão a uma ação</span><span class="sxs-lookup"><span data-stu-id="a9941-201">Link the button to an action</span></span>

<span data-ttu-id="a9941-202">Agora que implementou um botão, você precisará vinculá-lo a uma ação.</span><span class="sxs-lookup"><span data-stu-id="a9941-202">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="a9941-203">Nesse caso, a ação destina-se a que o Azure AD B2C se comunique com o Azure AD para receber um token.</span><span class="sxs-lookup"><span data-stu-id="a9941-203">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span></span> <span data-ttu-id="a9941-204">Vincule o botão a uma ação vinculando o perfil técnico ao provedor de declarações do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a9941-204">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="a9941-205">Localize o `<OrchestrationStep>` que inclui `Order="2"` no nó `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="a9941-205">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
1. <span data-ttu-id="a9941-206">Adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a9941-206">Add the following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="a9941-207">Atualize `Id` para o mesmo valor de `TargetClaimsExchangeId` na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="a9941-207">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
1. <span data-ttu-id="a9941-208">Atualize `TechnicalProfileReferenceId` como a ID do perfil técnico você criou anteriormente (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="a9941-208">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="a9941-209">Carregar o arquivo de extensão atualizado</span><span class="sxs-lookup"><span data-stu-id="a9941-209">Upload the updated extension file</span></span>

<span data-ttu-id="a9941-210">Agora você concluiu a modificação do arquivo de extensão.</span><span class="sxs-lookup"><span data-stu-id="a9941-210">You are done modifying the extension file.</span></span> <span data-ttu-id="a9941-211">Salve-o.</span><span class="sxs-lookup"><span data-stu-id="a9941-211">Save it.</span></span> <span data-ttu-id="a9941-212">Em seguida, salve e carregue o arquivo e verifique se todas as validações são bem-sucedidas.</span><span class="sxs-lookup"><span data-stu-id="a9941-212">Then upload the file, and ensure that all validations succeed.</span></span>

### <a name="update-the-rp-file"></a><span data-ttu-id="a9941-213">Atualizar o arquivo RP</span><span class="sxs-lookup"><span data-stu-id="a9941-213">Update the RP file</span></span>

<span data-ttu-id="a9941-214">Agora, você precisa atualizar o arquivo RP (terceira parte confiável) que iniciará o percurso do usuário que você acabou de criar:</span><span class="sxs-lookup"><span data-stu-id="a9941-214">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span></span>

1. <span data-ttu-id="a9941-215">Faça uma cópia de o SignUpOrSignIn.xml em diretório de trabalho e renomeie-o (por exemplo, como SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="a9941-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="a9941-216">Abra o novo arquivo e atualize o atributo `PolicyId` de `<TrustFrameworkPolicy>` com um valor exclusivo (por exemplo, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="a9941-216">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="a9941-217">Esse será o nome da política (por exemplo, B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="a9941-217">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="a9941-218">Modifique o atributo `ReferenceId` em `<DefaultUserJourney>` para que ele corresponda à ID do novo percurso do usuário criado (por exemplo, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="a9941-218">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="a9941-219">Salve as alterações e carregue o arquivo.</span><span class="sxs-lookup"><span data-stu-id="a9941-219">Save your changes, and upload the file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a9941-220">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="a9941-220">Troubleshooting</span></span>

<span data-ttu-id="a9941-221">Teste a política personalizada que você acabou de carregar abrindo sua folha e clicando em **Executar agora**.</span><span class="sxs-lookup"><span data-stu-id="a9941-221">Test the custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="a9941-222">Para diagnosticar problemas, leia sobre [solução de problemas](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a9941-222">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9941-223">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a9941-223">Next steps</span></span>

<span data-ttu-id="a9941-224">Envie seus comentários para [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a9941-224">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
