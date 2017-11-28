---
title: "Azure Active Directory B2C: adicionando um provedor SAML do Salesforce usando políticas personalizadas | Microsoft Docs"
description: "Saiba mais sobre como criar e gerenciar políticas personalizadas do Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: 269cbd80fb6e861fa8588025eec70b6c6e2890d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="ffb3d-103">Azure Active Directory B2C: entrar usando contas do Salesforce via SAML</span><span class="sxs-lookup"><span data-stu-id="ffb3d-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="ffb3d-104">Este artigo mostra como usar [políticas personalizadas](active-directory-b2c-overview-custom.md) para configurar a entrada de usuários de uma organização específica do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-104">This article shows you how to use [custom policies](active-directory-b2c-overview-custom.md) to set up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffb3d-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ffb3d-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="ffb3d-106">Configuração do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ffb3d-106">Azure AD B2C setup</span></span>

<span data-ttu-id="ffb3d-107">Não deixe de concluir todas as etapas que mostram como [começar a usar as políticas personalizadas](active-directory-b2c-get-started-custom.md) no Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-107">Ensure that you have completed all of the steps that show you how to [get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="ffb3d-108">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-108">These include:</span></span>

* <span data-ttu-id="ffb3d-109">Criar um locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="ffb3d-110">Criar um aplicativo Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="ffb3d-111">Registrar dois aplicativos de mecanismo de políticas.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="ffb3d-112">Configurar chaves.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-112">Set up keys.</span></span>
* <span data-ttu-id="ffb3d-113">Configurar o pacote inicial.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-113">Set up the starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="ffb3d-114">Configuração do Salesforce</span><span class="sxs-lookup"><span data-stu-id="ffb3d-114">Salesforce setup</span></span>

<span data-ttu-id="ffb3d-115">Neste artigo, presumimos que você já tenha feito o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-115">In this article, we assume that you have already done the following:</span></span>

* <span data-ttu-id="ffb3d-116">Inscreveu-se em uma conta do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="ffb3d-117">Você pode se inscrever em uma [conta gratuita do Developer Edition](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="ffb3d-118">[Configurou Meu Domínio](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) para sua organização do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="ffb3d-119">Configurar o Salesforce para que os usuários possam estabelecer a federação</span><span class="sxs-lookup"><span data-stu-id="ffb3d-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="ffb3d-120">Para ajudar o Azure AD B2C a se comunicar com o Salesforce, você precisa obter a URL de metadados do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-120">To help Azure AD B2C communicate with Salesforce, you need to get the Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="ffb3d-121">Configurar o Salesforce como um provedor de identidade</span><span class="sxs-lookup"><span data-stu-id="ffb3d-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="ffb3d-122">Neste artigo, presumimos que você esteja usando o [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="ffb3d-123">[Entre no Salesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-123">[Sign in to Salesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="ffb3d-124">No menu à esquerda, em **Configurações**, expanda **Identidade** e clique em **Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-124">On the left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="ffb3d-125">Clique em **Habilitar Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="ffb3d-126">Em **Selecione um certificado**, selecione o certificado que você quer que o Salesforce use para se comunicar com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-126">Under **Select the certificate**, select the certificate you want Salesforce to use to communicate with Azure AD B2C.</span></span> <span data-ttu-id="ffb3d-127">(Você pode usar o certificado padrão.) Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-127">(You can use the default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="ffb3d-128">Criar um aplicativo conectado no Salesforce</span><span class="sxs-lookup"><span data-stu-id="ffb3d-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="ffb3d-129">Na página **Provedor de Identidade**, vá até **Provedores de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-129">On the **Identity Provider** page, go to **Service Providers**.</span></span>
2. <span data-ttu-id="ffb3d-130">Clique em **Os Provedores de Serviço agora são criados por meio de Aplicativos Conectados. Clique aqui.**</span><span class="sxs-lookup"><span data-stu-id="ffb3d-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="ffb3d-131">Em **Informações Básicas**, forneça os valores necessários para seu aplicativo conectado.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-131">Under **Basic Information**,  enter the required values for your connected app.</span></span>
4. <span data-ttu-id="ffb3d-132">Em **Configurações do Aplicativo Web**, marque a caixa de seleção **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-132">Under **Web App Settings**, select the **Enable SAML** check box.</span></span>
5. <span data-ttu-id="ffb3d-133">No campo **ID da Entidade**, digite a URL a seguir.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-133">In the **Entity ID** field, enter the following URL.</span></span> <span data-ttu-id="ffb3d-134">Certifique-se substituir o valor de `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-134">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="ffb3d-135">No campo **URL ACS**, digite a URL a seguir.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-135">In the **ACS URL** field, enter the following URL.</span></span> <span data-ttu-id="ffb3d-136">Certifique-se substituir o valor de `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-136">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="ffb3d-137">Deixe os valores padrão para todas as outras configurações.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-137">Leave the default values for all other settings.</span></span>
8. <span data-ttu-id="ffb3d-138">Role até a parte inferior da lista e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-138">Scroll to the bottom of the list, and then click **Save**.</span></span>

### <a name="get-the-metadata-url"></a><span data-ttu-id="ffb3d-139">Obter a URL de metadados</span><span class="sxs-lookup"><span data-stu-id="ffb3d-139">Get the metadata URL</span></span>

1. <span data-ttu-id="ffb3d-140">Na página de visão geral de seu aplicativo conectado, clique em **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-140">On the overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="ffb3d-141">Copie o valor de **Ponto de Extremidade de Descoberta de Metadados** e salve-o.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-141">Copy the value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="ffb3d-142">Você o usará posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-to-federate"></a><span data-ttu-id="ffb3d-143">Configurar os usuários do Salesforce para federação</span><span class="sxs-lookup"><span data-stu-id="ffb3d-143">Set up Salesforce users to federate</span></span>

1. <span data-ttu-id="ffb3d-144">Na página **Gerenciar** de seu aplicativo conectado, vá até **Perfis**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-144">On the **Manage** page of your connected app, go to **Profiles**.</span></span>
2. <span data-ttu-id="ffb3d-145">Clique em **Gerenciar Perfis**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="ffb3d-146">Selecione os perfis (ou grupos de usuários) que você deseja federar com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-146">Select the profiles (or groups of users) that you want to federate with Azure AD B2C.</span></span> <span data-ttu-id="ffb3d-147">Como administrador do sistema, marque a caixa de seleção **Administrador do Sistema** para que você possa estabelecer a federação usando sua conta do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-147">As a system administrator, select the **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="ffb3d-148">Gerar um certificado de autenticação para o Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ffb3d-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="ffb3d-149">Solicitações enviadas para o Salesforce precisam ser assinadas pelo Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-149">Requests sent to Salesforce need to be signed by Azure AD B2C.</span></span> <span data-ttu-id="ffb3d-150">Para gerar um certificado de autenticação, abra o Azure PowerShell e, em seguida, execute os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-150">To generate a signing certificate, open Azure PowerShell, and then run the following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="ffb3d-151">Não deixe de atualizar o nome do locatário e a senha nas primeiras duas linhas.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-151">Make sure that you update the tenant name and password in the top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-the-saml-signing-certificate-to-azure-ad-b2c"></a><span data-ttu-id="ffb3d-152">Adicionar o certificado de autenticação SAML ao Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ffb3d-152">Add the SAML signing certificate to Azure AD B2C</span></span>

<span data-ttu-id="ffb3d-153">Carregue o certificado de autenticação para seu locatário do Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-153">Upload the signing certificate to your Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="ffb3d-154">Vá até seu locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-154">Go to your Azure AD B2C tenant.</span></span> <span data-ttu-id="ffb3d-155">Clique em **Configurações** > **Estrutura de Experiência de Identidade** > **Chaves da Política**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="ffb3d-156">Clique em **+Adicionar** e, em seguida:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="ffb3d-157">Clique em **Opções** > **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="ffb3d-158">Insira um **Nome** (por exemplo, SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="ffb3d-159">O prefixo *B2C_1A_* será adicionado automaticamente ao nome da chave.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-159">The prefix *B2C_1A_* is automatically added to the name of your key.</span></span>
    3. <span data-ttu-id="ffb3d-160">Para selecionar seu certificado, selecione **carregar o controle de arquivo**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-160">To select your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="ffb3d-161">Insira a senha do certificado que você definiu no script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-161">Enter the certificate's password that you set in the PowerShell script.</span></span>
3. <span data-ttu-id="ffb3d-162">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-162">Click **Create**.</span></span>
4. <span data-ttu-id="ffb3d-163">Verifique se você criou uma chave (por exemplo, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="ffb3d-164">Anote o nome completo (incluindo *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-164">Take note of the full name (including *B2C_1A_*).</span></span> <span data-ttu-id="ffb3d-165">Você fará referência a essa chave posteriormente na política.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-165">You will refer to this key later in the policy.</span></span>

## <a name="create-the-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="ffb3d-166">Criar o provedor de declarações SAML do Salesforce em sua política base</span><span class="sxs-lookup"><span data-stu-id="ffb3d-166">Create the Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="ffb3d-167">Você precisa definir o Salesforce como um provedor de declarações para que os usuários possam entrar usando o Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-167">You need to define Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="ffb3d-168">Em outras palavras, você precisa especificar o ponto de extremidade com o qual o Azure AD B2C se comunicará.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-168">In other words, you need to specify the endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="ffb3d-169">O ponto de extremidade *fornecerá* um conjunto de *declarações* usadas pelo Azure AD B2C para verificar se um usuário específico foi autenticado.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-169">The endpoint will *provide* a set of *claims* that Azure AD B2C uses to verify that a specific user has authenticated.</span></span> <span data-ttu-id="ffb3d-170">Faça isso adicionando um `<ClaimsProvider>` ao Salesforce no arquivo de extensão da política:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-170">To do this, add a `<ClaimsProvider>` for Salesforce in the extension file of your policy:</span></span>

1. <span data-ttu-id="ffb3d-171">No diretório de trabalho, abra o arquivo de extensão (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-171">In your working directory, open the extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="ffb3d-172">Localize a seção `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-172">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="ffb3d-173">Caso ela não exista, crie-a sob o nó raiz.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-173">If it does not exist, create it under the root node.</span></span>
3. <span data-ttu-id="ffb3d-174">Adicione um novo `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-174">Add a new `<ClaimsProvider>`:</span></span>

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
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

<span data-ttu-id="ffb3d-175">Sob o nó `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-175">Under the `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="ffb3d-176">Altere o valor de `<Domain>` para um valor exclusivo para distinguir `<ClaimsProvider>` de outros provedores de identidade.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-176">Change the value for `<Domain>` to a unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="ffb3d-177">Atualize o valor de `<DisplayName>` para um nome de exibição do provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-177">Update the value for `<DisplayName>` to a display name for the claims provider.</span></span> <span data-ttu-id="ffb3d-178">Atualmente, esse valor não é usado.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-178">Currently, this value is not used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="ffb3d-179">Atualizar o perfil técnico</span><span class="sxs-lookup"><span data-stu-id="ffb3d-179">Update the technical profile</span></span>

<span data-ttu-id="ffb3d-180">Para obter um token SAML do Salesforce, defina os protocolos que o Azure AD B2C usará para se comunicar com o Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-180">To get a SAML token from Salesforce, define the protocols that Azure AD B2C will use to communicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ffb3d-181">Faça isso no elemento `<TechnicalProfile>` de `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-181">Do this in the `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="ffb3d-182">Atualize a ID do nó `<TechnicalProfile>`.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-182">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="ffb3d-183">Essa ID é usada para se referir a esse perfil técnico em outras partes da política.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-183">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
2. <span data-ttu-id="ffb3d-184">Atualize o valor de `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-184">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="ffb3d-185">Esse valor é exibido no botão de entrada em sua página de entrada.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-185">This value is displayed on the sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="ffb3d-186">Atualize o valor de `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-186">Update the value for `<Description>`.</span></span>
4. <span data-ttu-id="ffb3d-187">O Salesforce usa o protocolo SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-187">Salesforce uses the SAML 2.0 protocol.</span></span> <span data-ttu-id="ffb3d-188">Certifique-se de que o valor de `<Protocol>` seja **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-188">Ensure that the value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="ffb3d-189">Atualize a seção `<Metadata>` no XML anterior para refletir as configurações de sua conta específica do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-189">Update the `<Metadata>` section in the preceding XML to reflect the settings for your specific Salesforce account.</span></span> <span data-ttu-id="ffb3d-190">No XML, atualize os valores dos metadados:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-190">In the XML, update the metadata values:</span></span>

1. <span data-ttu-id="ffb3d-191">Atualize o valor de `<Item Key="PartnerEntity">` com a URL de metadados do Salesforce que você copiou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-191">Update the value of `<Item Key="PartnerEntity">` with the Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="ffb3d-192">Ela tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-192">It has the following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="ffb3d-193">Na seção `<CryptographicKeys>`, atualize o valor de ambas as instâncias de `StorageReferenceId` para o nome da chave de seu certificado de autenticação (por exemplo, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-193">In the `<CryptographicKeys>` section, update the value for both instances of `StorageReferenceId` to the name of the key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="ffb3d-194">Carregar o arquivo de extensão para verificação</span><span class="sxs-lookup"><span data-stu-id="ffb3d-194">Upload the extension file for verification</span></span>

<span data-ttu-id="ffb3d-195">Agora, a política agora está configurada para que o Azure AD B2C saiba como se comunicar com o Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-195">Your policy is now configured so that Azure AD B2C knows how to communicate with Salesforce.</span></span> <span data-ttu-id="ffb3d-196">Tente carregar o arquivo de extensão da política para confirmar se ele não apresenta problemas até o momento.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-196">Try uploading the extension file of your policy, to verify that there aren't any issues so far.</span></span> <span data-ttu-id="ffb3d-197">Para carregar o arquivo de extensão da política:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-197">To upload the extension file of your policy:</span></span>

1. <span data-ttu-id="ffb3d-198">Acesse a folha **Todas as Políticas** no locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-198">In your Azure AD B2C tenant, go to the **All Policies** blade.</span></span>
2. <span data-ttu-id="ffb3d-199">Marque a caixa de seleção **Substituir a política caso ela exista**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-199">Select the **Overwrite the policy if it exists** check box.</span></span>
3. <span data-ttu-id="ffb3d-200">Carregue o arquivo de extensões (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-200">Upload the extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="ffb3d-201">Certifique-se de que ele não falhe na validação.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-the-salesforce-saml-claims-provider-to-a-user-journey"></a><span data-ttu-id="ffb3d-202">Registrar o provedor de declarações SAML do Salesforce em um percurso do usuário</span><span class="sxs-lookup"><span data-stu-id="ffb3d-202">Register the Salesforce SAML claims provider to a user journey</span></span>

<span data-ttu-id="ffb3d-203">Em seguida, adicione o provedor de identidade SAML do Salesforce a um dos percursos do usuário.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-203">Next, add the Salesforce SAML identity provider to one of your user journeys.</span></span> <span data-ttu-id="ffb3d-204">Neste ponto, o provedor de identidade foi definido, mas não está disponível em nenhuma das páginas de inscrição/entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-204">At this point, the identity provider has been set up, but it’s not available on any of the user sign-up or sign-in pages.</span></span> <span data-ttu-id="ffb3d-205">Para adicionar o provedor de identidade a uma página de entrada, crie primeiro uma duplicata de um Percurso do Usuário do modelo existente.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-205">To add the identity provider to a sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="ffb3d-206">Em seguida, modifique o modelo para que ele também tenha o provedor de identidade do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-206">Then, modify the template so that it also has the Azure AD identity provider.</span></span>

1. <span data-ttu-id="ffb3d-207">Abra o arquivo base da política (por exemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-207">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="ffb3d-208">Localize o elemento `<UserJourneys>` e copie todo o valor de `<UserJourney>`, incluindo Id=“SignUpOrSignIn”.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-208">Find the `<UserJourneys>` element, and then copy the entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="ffb3d-209">Abra o arquivo de extensão (por exemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-209">Open the extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="ffb3d-210">Localize o elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-210">Find the `<UserJourneys>` element.</span></span> <span data-ttu-id="ffb3d-211">Se o elemento não existir, crie um.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-211">If the element doesn't exist, create one.</span></span>
4. <span data-ttu-id="ffb3d-212">Cole todo o `<UserJourney>` copiado como um filho do elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-212">Paste the entire copied `<UserJourney>` as a child of the `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="ffb3d-213">Renomeie a ID do novo `<UserJourney>` (por exemplo, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-213">Rename the ID of the new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-the-identity-provider-button"></a><span data-ttu-id="ffb3d-214">Exibir o botão do provedor de identidade</span><span class="sxs-lookup"><span data-stu-id="ffb3d-214">Display the identity provider button</span></span>

<span data-ttu-id="ffb3d-215">O elemento `<ClaimsProviderSelection>` é análogo a um botão de provedor de identidade em uma página de inscrição/entrada.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-215">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="ffb3d-216">Ao adicionar um elemento `<ClaimsProviderSelection>` ao Salesforce, um novo botão aparecerá quando um usuário chegar na página.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes to this page.</span></span> <span data-ttu-id="ffb3d-217">Para exibir o botão do provedor de identidade:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-217">To display the identity provider button:</span></span>

1. <span data-ttu-id="ffb3d-218">No `<UserJourney>` criado, localize o `<OrchestrationStep>` com `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-218">In the `<UserJourney>` that you created, find the `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="ffb3d-219">Adicione o XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-219">Add the following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="ffb3d-220">Defina `TargetClaimsExchangeId` como um valor lógico.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-220">Set `TargetClaimsExchangeId` to a logical value.</span></span> <span data-ttu-id="ffb3d-221">Recomendamos seguir a mesma convenção que os outros (por exemplo, *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-221">We recommend following the same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-the-identity-provider-button-to-an-action"></a><span data-ttu-id="ffb3d-222">Vincular o botão do provedor de identidade a uma ação</span><span class="sxs-lookup"><span data-stu-id="ffb3d-222">Link the identity provider button to an action</span></span>

<span data-ttu-id="ffb3d-223">Agora que você implementou um botão do provedor de identidade, vincule-o a uma ação.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-223">Now that you have an identity provider button in place, link it to an action.</span></span> <span data-ttu-id="ffb3d-224">Nesse caso, a ação destina-se a que o Azure AD B2C se comunique com o Salesforce para receber um token SAML.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-224">In this case, the action is for Azure AD B2C to communicate with Salesforce to receive a SAML token.</span></span> <span data-ttu-id="ffb3d-225">Faça isso vinculando o perfil técnico ao provedor de declarações SAML do Salesforce:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-225">You can do this by linking the technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="ffb3d-226">No nó `<UserJourney>`, localize o `<OrchestrationStep>` com `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-226">In the `<UserJourney>` node, find the `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="ffb3d-227">Adicione o XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-227">Add the following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="ffb3d-228">Atualize `Id` com o mesmo valor que você usou anteriormente para `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-228">Update `Id` to the same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="ffb3d-229">Atualize `TechnicalProfileReferenceId` para o `Id` do perfil técnico você criou anteriormente (por exemplo, ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-229">Update `TechnicalProfileReferenceId` to the `Id` of the technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="ffb3d-230">Carregar o arquivo de extensão atualizado</span><span class="sxs-lookup"><span data-stu-id="ffb3d-230">Upload the updated extension file</span></span>

<span data-ttu-id="ffb3d-231">Agora você concluiu a modificação do arquivo de extensão.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-231">You are done modifying the extension file.</span></span> <span data-ttu-id="ffb3d-232">Salve e carregue esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-232">Save and upload this file.</span></span> <span data-ttu-id="ffb3d-233">Certifique-se de que todas as validações tenham êxito.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-233">Ensure that all validations succeed.</span></span>

### <a name="update-the-relying-party-file"></a><span data-ttu-id="ffb3d-234">Atualizar o arquivo de terceira parte confiável</span><span class="sxs-lookup"><span data-stu-id="ffb3d-234">Update the relying party file</span></span>

<span data-ttu-id="ffb3d-235">Em seguida, atualize o arquivo de RP (terceira parte confiável) que iniciará o percurso do usuário que você criou:</span><span class="sxs-lookup"><span data-stu-id="ffb3d-235">Next, update the relying party (RP) file that initiates the user journey that you created:</span></span>

1. <span data-ttu-id="ffb3d-236">Faça uma cópia de SignUpOrSignIn.xml em seu diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="ffb3d-237">Em seguida, renomeie-a (por exemplo, SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="ffb3d-238">Abra o novo arquivo e atualize o atributo `PolicyId` de `<TrustFrameworkPolicy>` com um valor exclusivo.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-238">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="ffb3d-239">Esse é o nome da política (por exemplo, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-239">This is the name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="ffb3d-240">Modifique o atributo `ReferenceId` em `<DefaultUserJourney>` para que ele corresponda a `Id` do novo percurso do usuário criado (por exemplo, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-240">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="ffb3d-241">Salve as alterações e, em seguida, carregue o arquivo.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-241">Save your changes, and then upload the file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="ffb3d-242">Testar e solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="ffb3d-242">Test and troubleshoot</span></span>

<span data-ttu-id="ffb3d-243">Para testar a política personalizada que você acabou de carregar, no portal do Azure, vá até a folha de política e, em seguida, clique em **Executar agora**.</span><span class="sxs-lookup"><span data-stu-id="ffb3d-243">To test the custom policy that you just uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span></span> <span data-ttu-id="ffb3d-244">Se ela falhar, consulte [Solucionar problemas com políticas personalizadas](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffb3d-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ffb3d-245">Next steps</span></span>

<span data-ttu-id="ffb3d-246">Envie seus comentários para [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ffb3d-246">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
