---
title: "Azure Active Directory B2C: adicionando um provedor SAML do Salesforce usando políticas personalizadas | Microsoft Docs"
description: "Saiba mais sobre como toocreate e gerenciar políticas personalizadas do Azure Active Directory B2C."
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
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="2a59a-103">Azure Active Directory B2C: entrar usando contas do Salesforce via SAML</span><span class="sxs-lookup"><span data-stu-id="2a59a-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="2a59a-104">Este artigo mostra como toouse [políticas personalizadas](active-directory-b2c-overview-custom.md) tooset a entrada de usuários de uma organização de vendas específica.</span><span class="sxs-lookup"><span data-stu-id="2a59a-104">This article shows you how toouse [custom policies](active-directory-b2c-overview-custom.md) tooset up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a59a-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2a59a-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="2a59a-106">Configuração do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="2a59a-106">Azure AD B2C setup</span></span>

<span data-ttu-id="2a59a-107">Certifique-se de que você concluiu todas as etapas de saudação que mostram como muito[Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md) no Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="2a59a-107">Ensure that you have completed all of hello steps that show you how too[get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="2a59a-108">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="2a59a-108">These include:</span></span>

* <span data-ttu-id="2a59a-109">Criar um locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2a59a-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="2a59a-110">Criar um aplicativo Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2a59a-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="2a59a-111">Registrar dois aplicativos de mecanismo de políticas.</span><span class="sxs-lookup"><span data-stu-id="2a59a-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="2a59a-112">Configurar chaves.</span><span class="sxs-lookup"><span data-stu-id="2a59a-112">Set up keys.</span></span>
* <span data-ttu-id="2a59a-113">Configure o pacote de inicializador de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a59a-113">Set up hello starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="2a59a-114">Configuração do Salesforce</span><span class="sxs-lookup"><span data-stu-id="2a59a-114">Salesforce setup</span></span>

<span data-ttu-id="2a59a-115">Neste artigo, vamos supor que você já tenha feito o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="2a59a-115">In this article, we assume that you have already done hello following:</span></span>

* <span data-ttu-id="2a59a-116">Inscreveu-se em uma conta do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2a59a-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="2a59a-117">Você pode se inscrever em uma [conta gratuita do Developer Edition](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="2a59a-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="2a59a-118">[Configurou Meu Domínio](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) para sua organização do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2a59a-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="2a59a-119">Configurar o Salesforce para que os usuários possam estabelecer a federação</span><span class="sxs-lookup"><span data-stu-id="2a59a-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="2a59a-120">toohelp do Azure AD B2C se comunicar com a equipe de vendas, é necessário o URL de metadados de Salesforce tooget hello.</span><span class="sxs-lookup"><span data-stu-id="2a59a-120">toohelp Azure AD B2C communicate with Salesforce, you need tooget hello Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="2a59a-121">Configurar o Salesforce como um provedor de identidade</span><span class="sxs-lookup"><span data-stu-id="2a59a-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="2a59a-122">Neste artigo, presumimos que você esteja usando o [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="2a59a-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="2a59a-123">[Entrar tooSalesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="2a59a-123">[Sign in tooSalesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="2a59a-124">Na saudação esquerda menu em **configurações**, expanda **identidade**e, em seguida, clique em **provedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-124">On hello left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="2a59a-125">Clique em **Habilitar Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="2a59a-126">Em **certificado Olá selecione**, selecione Olá certificado Salesforce toouse toocommunicate com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2a59a-126">Under **Select hello certificate**, select hello certificate you want Salesforce toouse toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="2a59a-127">(Você pode usar o certificado padrão de hello.) Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-127">(You can use hello default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="2a59a-128">Criar um aplicativo conectado no Salesforce</span><span class="sxs-lookup"><span data-stu-id="2a59a-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="2a59a-129">Em Olá **provedor de identidade** página, ir muito**provedores de serviço**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-129">On hello **Identity Provider** page, go too**Service Providers**.</span></span>
2. <span data-ttu-id="2a59a-130">Clique em **Os Provedores de Serviço agora são criados por meio de Aplicativos Conectados. Clique aqui.**</span><span class="sxs-lookup"><span data-stu-id="2a59a-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="2a59a-131">Em **informações básicas**, insira valores hello necessários para seu aplicativo conectado.</span><span class="sxs-lookup"><span data-stu-id="2a59a-131">Under **Basic Information**,  enter hello required values for your connected app.</span></span>
4. <span data-ttu-id="2a59a-132">Em **configurações do aplicativo Web**, selecione Olá **habilitar SAML** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="2a59a-132">Under **Web App Settings**, select hello **Enable SAML** check box.</span></span>
5. <span data-ttu-id="2a59a-133">Em Olá **ID da entidade** digite Olá URL a seguir.</span><span class="sxs-lookup"><span data-stu-id="2a59a-133">In hello **Entity ID** field, enter hello following URL.</span></span> <span data-ttu-id="2a59a-134">Certifique-se de que você substitua o valor de saudação para `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="2a59a-134">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="2a59a-135">Em Olá **URL do ACS** digite Olá URL a seguir.</span><span class="sxs-lookup"><span data-stu-id="2a59a-135">In hello **ACS URL** field, enter hello following URL.</span></span> <span data-ttu-id="2a59a-136">Certifique-se de que você substitua o valor de saudação para `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="2a59a-136">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="2a59a-137">Deixe valores padrão de saudação para todas as outras configurações.</span><span class="sxs-lookup"><span data-stu-id="2a59a-137">Leave hello default values for all other settings.</span></span>
8. <span data-ttu-id="2a59a-138">Role toohello inferior da lista de saudação e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-138">Scroll toohello bottom of hello list, and then click **Save**.</span></span>

### <a name="get-hello-metadata-url"></a><span data-ttu-id="2a59a-139">Obter URL de metadados de saudação</span><span class="sxs-lookup"><span data-stu-id="2a59a-139">Get hello metadata URL</span></span>

1. <span data-ttu-id="2a59a-140">Na página de visão geral de saudação do seu aplicativo conectado, clique em **gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-140">On hello overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="2a59a-141">Copiar valor Olá **ponto de extremidade de descoberta de metadados**e, em seguida, salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="2a59a-141">Copy hello value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="2a59a-142">Você o usará posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2a59a-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-toofederate"></a><span data-ttu-id="2a59a-143">Configurar toofederate de usuários do Salesforce</span><span class="sxs-lookup"><span data-stu-id="2a59a-143">Set up Salesforce users toofederate</span></span>

1. <span data-ttu-id="2a59a-144">Em Olá **gerenciar** página do aplicativo conectado, vá muito**perfis**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-144">On hello **Manage** page of your connected app, go too**Profiles**.</span></span>
2. <span data-ttu-id="2a59a-145">Clique em **Gerenciar Perfis**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="2a59a-146">Selecione perfis hello (ou grupos de usuários) que você deseja toofederate com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2a59a-146">Select hello profiles (or groups of users) that you want toofederate with Azure AD B2C.</span></span> <span data-ttu-id="2a59a-147">Como um administrador do sistema, selecione Olá **administrador do sistema** caixa de seleção para que você pode federar usando sua conta do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2a59a-147">As a system administrator, select hello **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="2a59a-148">Gerar um certificado de autenticação para o Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="2a59a-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="2a59a-149">Solicitações enviadas tooSalesforce necessidade toobe assinado pelo Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2a59a-149">Requests sent tooSalesforce need toobe signed by Azure AD B2C.</span></span> <span data-ttu-id="2a59a-150">toogenerate um certificado de assinatura, abra o Azure PowerShell e execute Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="2a59a-150">toogenerate a signing certificate, open Azure PowerShell, and then run hello following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="2a59a-151">Certifique-se de que você atualize o nome do locatário hello e a senha em duas linhas de saudação superior.</span><span class="sxs-lookup"><span data-stu-id="2a59a-151">Make sure that you update hello tenant name and password in hello top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a><span data-ttu-id="2a59a-152">Adicionar certificado tooAzure assinatura Olá SAML AD B2C</span><span class="sxs-lookup"><span data-stu-id="2a59a-152">Add hello SAML signing certificate tooAzure AD B2C</span></span>

<span data-ttu-id="2a59a-153">Carregar Olá locatário de tooyour do Azure AD B2C do certificado de assinatura:</span><span class="sxs-lookup"><span data-stu-id="2a59a-153">Upload hello signing certificate tooyour Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="2a59a-154">Vá locatário tooyour B2C do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a59a-154">Go tooyour Azure AD B2C tenant.</span></span> <span data-ttu-id="2a59a-155">Clique em **Configurações** > **Estrutura de Experiência de Identidade** > **Chaves da Política**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="2a59a-156">Clique em **+Adicionar** e, em seguida:</span><span class="sxs-lookup"><span data-stu-id="2a59a-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="2a59a-157">Clique em **Opções** > **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="2a59a-158">Insira um **Nome** (por exemplo, SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="2a59a-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="2a59a-159">prefixo de saudação *B2C_1A_* é adicionado automaticamente toohello nome da chave.</span><span class="sxs-lookup"><span data-stu-id="2a59a-159">hello prefix *B2C_1A_* is automatically added toohello name of your key.</span></span>
    3. <span data-ttu-id="2a59a-160">tooselect seu certificado, selecione **carregar o controle de arquivo**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-160">tooselect your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="2a59a-161">Insira a senha do certificado Olá definida no script do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="2a59a-161">Enter hello certificate's password that you set in hello PowerShell script.</span></span>
3. <span data-ttu-id="2a59a-162">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-162">Click **Create**.</span></span>
4. <span data-ttu-id="2a59a-163">Verifique se você criou uma chave (por exemplo, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="2a59a-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="2a59a-164">Anote o nome completo da saudação (incluindo *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="2a59a-164">Take note of hello full name (including *B2C_1A_*).</span></span> <span data-ttu-id="2a59a-165">Você fará referência chave toothis posteriormente na política de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a59a-165">You will refer toothis key later in hello policy.</span></span>

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="2a59a-166">Criar hello Salesforce SAML provedor de declarações em sua política de base</span><span class="sxs-lookup"><span data-stu-id="2a59a-166">Create hello Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="2a59a-167">É necessário toodefine Salesforce como um provedor de declarações para que os usuários possam se conectar usando a equipe de vendas.</span><span class="sxs-lookup"><span data-stu-id="2a59a-167">You need toodefine Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="2a59a-168">Em outras palavras, você precisa toospecify Olá ponto de extremidade do Azure AD B2C se comunicará.</span><span class="sxs-lookup"><span data-stu-id="2a59a-168">In other words, you need toospecify hello endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="2a59a-169">ponto de extremidade Olá será *fornecer* um conjunto de *declarações* B2C do Azure AD usa tooverify que um usuário específico autenticado.</span><span class="sxs-lookup"><span data-stu-id="2a59a-169">hello endpoint will *provide* a set of *claims* that Azure AD B2C uses tooverify that a specific user has authenticated.</span></span> <span data-ttu-id="2a59a-170">toodo isso, adicione um `<ClaimsProvider>` para a equipe de vendas no arquivo de extensão de saudação da política:</span><span class="sxs-lookup"><span data-stu-id="2a59a-170">toodo this, add a `<ClaimsProvider>` for Salesforce in hello extension file of your policy:</span></span>

1. <span data-ttu-id="2a59a-171">No diretório de trabalho, abra o arquivo de extensão da saudação (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="2a59a-171">In your working directory, open hello extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="2a59a-172">Localize Olá `<ClaimsProviders>` seção.</span><span class="sxs-lookup"><span data-stu-id="2a59a-172">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="2a59a-173">Se não existir, criá-lo sob o nó raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a59a-173">If it does not exist, create it under hello root node.</span></span>
3. <span data-ttu-id="2a59a-174">Adicione um novo `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="2a59a-174">Add a new `<ClaimsProvider>`:</span></span>

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

<span data-ttu-id="2a59a-175">Em Olá `<ClaimsProvider>` nó:</span><span class="sxs-lookup"><span data-stu-id="2a59a-175">Under hello `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="2a59a-176">Alterar valor Olá `<Domain>` tooa valor exclusivo que diferencia `<ClaimsProvider>` de outros provedores de identidade.</span><span class="sxs-lookup"><span data-stu-id="2a59a-176">Change hello value for `<Domain>` tooa unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="2a59a-177">Atualizar valor Olá `<DisplayName>` tooa nome para exibição para Olá provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="2a59a-177">Update hello value for `<DisplayName>` tooa display name for hello claims provider.</span></span> <span data-ttu-id="2a59a-178">Atualmente, esse valor não é usado.</span><span class="sxs-lookup"><span data-stu-id="2a59a-178">Currently, this value is not used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="2a59a-179">Atualizar perfil técnica Olá</span><span class="sxs-lookup"><span data-stu-id="2a59a-179">Update hello technical profile</span></span>

<span data-ttu-id="2a59a-180">tooget um token SAML do Salesforce, definir protocolos de saudação do Azure AD B2C usará toocommunicate com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="2a59a-180">tooget a SAML token from Salesforce, define hello protocols that Azure AD B2C will use toocommunicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="2a59a-181">Fazer isso no hello `<TechnicalProfile>` elemento `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="2a59a-181">Do this in hello `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="2a59a-182">Atualizar a ID de saudação do hello `<TechnicalProfile>` nó.</span><span class="sxs-lookup"><span data-stu-id="2a59a-182">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="2a59a-183">Essa ID é usada toorefer toothis perfil técnico de outras partes da política de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a59a-183">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
2. <span data-ttu-id="2a59a-184">Atualizar o valor Olá para `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="2a59a-184">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="2a59a-185">Esse valor é exibido no botão logon Olá na página de entrada.</span><span class="sxs-lookup"><span data-stu-id="2a59a-185">This value is displayed on hello sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="2a59a-186">Atualizar o valor Olá para `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="2a59a-186">Update hello value for `<Description>`.</span></span>
4. <span data-ttu-id="2a59a-187">A equipe de vendas usa o protocolo de saudação SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="2a59a-187">Salesforce uses hello SAML 2.0 protocol.</span></span> <span data-ttu-id="2a59a-188">Verifique se esse valor Olá para `<Protocol>` é **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-188">Ensure that hello value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="2a59a-189">Saudação de atualização `<Metadata>` seção Olá anterior configurações de saudação do XML tooreflect para sua conta do Salesforce específica.</span><span class="sxs-lookup"><span data-stu-id="2a59a-189">Update hello `<Metadata>` section in hello preceding XML tooreflect hello settings for your specific Salesforce account.</span></span> <span data-ttu-id="2a59a-190">Olá XML, atualize os valores de metadados hello:</span><span class="sxs-lookup"><span data-stu-id="2a59a-190">In hello XML, update hello metadata values:</span></span>

1. <span data-ttu-id="2a59a-191">Atualizar o valor de saudação do `<Item Key="PartnerEntity">` com URL de metadados de Salesforce Olá copiados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a59a-191">Update hello value of `<Item Key="PartnerEntity">` with hello Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="2a59a-192">Ele tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a59a-192">It has hello following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="2a59a-193">Em Olá `<CryptographicKeys>` seção atualização Olá valor para ambas as instâncias de `StorageReferenceId` toohello nome da chave de saudação do seu certificado de autenticação (por exemplo, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="2a59a-193">In hello `<CryptographicKeys>` section, update hello value for both instances of `StorageReferenceId` toohello name of hello key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="2a59a-194">Carregue o arquivo de extensão de saudação para verificação</span><span class="sxs-lookup"><span data-stu-id="2a59a-194">Upload hello extension file for verification</span></span>

<span data-ttu-id="2a59a-195">A política agora está configurada para que o Azure AD B2C sabe como toocommunicate com a equipe de vendas.</span><span class="sxs-lookup"><span data-stu-id="2a59a-195">Your policy is now configured so that Azure AD B2C knows how toocommunicate with Salesforce.</span></span> <span data-ttu-id="2a59a-196">Tente carregar o arquivo de extensão de saudação de sua política, tooverify que não existem problemas até o momento.</span><span class="sxs-lookup"><span data-stu-id="2a59a-196">Try uploading hello extension file of your policy, tooverify that there aren't any issues so far.</span></span> <span data-ttu-id="2a59a-197">arquivo de extensão tooupload Olá da política:</span><span class="sxs-lookup"><span data-stu-id="2a59a-197">tooupload hello extension file of your policy:</span></span>

1. <span data-ttu-id="2a59a-198">No seu locatário do Azure AD B2C, acesse toohello **todas as políticas** folha.</span><span class="sxs-lookup"><span data-stu-id="2a59a-198">In your Azure AD B2C tenant, go toohello **All Policies** blade.</span></span>
2. <span data-ttu-id="2a59a-199">Selecione Olá **substituir a política de saudação se ela existe** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="2a59a-199">Select hello **Overwrite hello policy if it exists** check box.</span></span>
3. <span data-ttu-id="2a59a-200">Carregar arquivo de extensão da saudação (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="2a59a-200">Upload hello extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="2a59a-201">Certifique-se de que ele não falhe na validação.</span><span class="sxs-lookup"><span data-stu-id="2a59a-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a><span data-ttu-id="2a59a-202">Registrar Olá jornada de usuário do Salesforce SAML declarações provedor tooa</span><span class="sxs-lookup"><span data-stu-id="2a59a-202">Register hello Salesforce SAML claims provider tooa user journey</span></span>

<span data-ttu-id="2a59a-203">Em seguida, adicione Olá tooone de provedor de identidade Salesforce SAML de seu Jornadas de usuário.</span><span class="sxs-lookup"><span data-stu-id="2a59a-203">Next, add hello Salesforce SAML identity provider tooone of your user journeys.</span></span> <span data-ttu-id="2a59a-204">Neste ponto, o provedor de identidade Olá foi configurado, mas não está disponível em qualquer uma das páginas de inscrição ou entrada de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="2a59a-204">At this point, hello identity provider has been set up, but it’s not available on any of hello user sign-up or sign-in pages.</span></span> <span data-ttu-id="2a59a-205">tooadd Olá identidade provedor tooa página de entrada, primeiro, crie uma duplicata de uma jornada de usuário do modelo existente.</span><span class="sxs-lookup"><span data-stu-id="2a59a-205">tooadd hello identity provider tooa sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="2a59a-206">Em seguida, modificar o modelo de saudação para que ele também tem o provedor de identidade do AD do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2a59a-206">Then, modify hello template so that it also has hello Azure AD identity provider.</span></span>

1. <span data-ttu-id="2a59a-207">Abra o arquivo de base de saudação da política (por exemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="2a59a-207">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="2a59a-208">Localize Olá `<UserJourneys>` elemento e, em seguida, hello de cópia inteira `<UserJourney>` valor, incluindo a Id = "SignUpOrSignIn".</span><span class="sxs-lookup"><span data-stu-id="2a59a-208">Find hello `<UserJourneys>` element, and then copy hello entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="2a59a-209">Abra o arquivo de extensão da saudação (por exemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="2a59a-209">Open hello extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="2a59a-210">Localize Olá `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="2a59a-210">Find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="2a59a-211">Se o elemento de saudação não existir, crie um.</span><span class="sxs-lookup"><span data-stu-id="2a59a-211">If hello element doesn't exist, create one.</span></span>
4. <span data-ttu-id="2a59a-212">Saudação de colar todo copiada `<UserJourney>` como um filho do hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="2a59a-212">Paste hello entire copied `<UserJourney>` as a child of hello `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="2a59a-213">Renomear a ID de saudação do hello novo `<UserJourney>` (por exemplo, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="2a59a-213">Rename hello ID of hello new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-hello-identity-provider-button"></a><span data-ttu-id="2a59a-214">Botão de provedor de identidade de saudação de exibição</span><span class="sxs-lookup"><span data-stu-id="2a59a-214">Display hello identity provider button</span></span>

<span data-ttu-id="2a59a-215">Olá `<ClaimsProviderSelection>` elemento é análogo tooan botão de provedor de identidade em uma página de inscrição ou entrar.</span><span class="sxs-lookup"><span data-stu-id="2a59a-215">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="2a59a-216">Adicionando um `<ClaimsProviderSelection>` elemento para a equipe de vendas, um novo botão aparece quando um usuário sai toothis página.</span><span class="sxs-lookup"><span data-stu-id="2a59a-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes toothis page.</span></span> <span data-ttu-id="2a59a-217">botão de provedor de identidade de saudação toodisplay:</span><span class="sxs-lookup"><span data-stu-id="2a59a-217">toodisplay hello identity provider button:</span></span>

1. <span data-ttu-id="2a59a-218">Em Olá `<UserJourney>` que você criou, localize Olá `<OrchestrationStep>` com `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="2a59a-218">In hello `<UserJourney>` that you created, find hello `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="2a59a-219">Adicione Olá XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a59a-219">Add hello following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="2a59a-220">Definir `TargetClaimsExchangeId` valor lógico tooa.</span><span class="sxs-lookup"><span data-stu-id="2a59a-220">Set `TargetClaimsExchangeId` tooa logical value.</span></span> <span data-ttu-id="2a59a-221">É recomendável seguir Olá a mesma convenção de outros usuários (por exemplo,  *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="2a59a-221">We recommend following hello same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-hello-identity-provider-button-tooan-action"></a><span data-ttu-id="2a59a-222">Provedor de identidade do link Olá botão tooan ação</span><span class="sxs-lookup"><span data-stu-id="2a59a-222">Link hello identity provider button tooan action</span></span>

<span data-ttu-id="2a59a-223">Agora que você tem um botão de provedor de identidade em vigor, vincule-tooan ação.</span><span class="sxs-lookup"><span data-stu-id="2a59a-223">Now that you have an identity provider button in place, link it tooan action.</span></span> <span data-ttu-id="2a59a-224">Nesse caso, a ação de saudação é para o Azure AD B2C toocommunicate com a equipe de vendas tooreceive um token SAML.</span><span class="sxs-lookup"><span data-stu-id="2a59a-224">In this case, hello action is for Azure AD B2C toocommunicate with Salesforce tooreceive a SAML token.</span></span> <span data-ttu-id="2a59a-225">Você pode fazer isso por meio da vinculação perfil técnico Olá para o Salesforce SAML provedor de declarações:</span><span class="sxs-lookup"><span data-stu-id="2a59a-225">You can do this by linking hello technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="2a59a-226">Em Olá `<UserJourney>` nó, localizar Olá `<OrchestrationStep>` com `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="2a59a-226">In hello `<UserJourney>` node, find hello `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="2a59a-227">Adicione Olá XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a59a-227">Add hello following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="2a59a-228">Atualização `Id` toohello mesmo valor que você usou anteriormente para `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="2a59a-228">Update `Id` toohello same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="2a59a-229">Atualização `TechnicalProfileReferenceId` toohello `Id` de saudação técnica perfil você criou anteriormente (por exemplo, ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="2a59a-229">Update `TechnicalProfileReferenceId` toohello `Id` of hello technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="2a59a-230">Carregar arquivo de extensão atualizada Olá</span><span class="sxs-lookup"><span data-stu-id="2a59a-230">Upload hello updated extension file</span></span>

<span data-ttu-id="2a59a-231">Você concluiu a modificar arquivo de extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a59a-231">You are done modifying hello extension file.</span></span> <span data-ttu-id="2a59a-232">Salve e carregue esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="2a59a-232">Save and upload this file.</span></span> <span data-ttu-id="2a59a-233">Certifique-se de que todas as validações tenham êxito.</span><span class="sxs-lookup"><span data-stu-id="2a59a-233">Ensure that all validations succeed.</span></span>

### <a name="update-hello-relying-party-file"></a><span data-ttu-id="2a59a-234">Atualizar o arquivo de parte confiável Olá</span><span class="sxs-lookup"><span data-stu-id="2a59a-234">Update hello relying party file</span></span>

<span data-ttu-id="2a59a-235">Em seguida, atualize Olá terceira parte confiável (RP) arquivo inicia jornada saudação do usuário que você criou:</span><span class="sxs-lookup"><span data-stu-id="2a59a-235">Next, update hello relying party (RP) file that initiates hello user journey that you created:</span></span>

1. <span data-ttu-id="2a59a-236">Faça uma cópia de SignUpOrSignIn.xml em seu diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2a59a-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="2a59a-237">Em seguida, renomeie-a (por exemplo, SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="2a59a-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="2a59a-238">Olá novo Olá abrir arquivo e atualização `PolicyId` atributo `<TrustFrameworkPolicy>` com um valor exclusivo.</span><span class="sxs-lookup"><span data-stu-id="2a59a-238">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="2a59a-239">Este é o nome de saudação da política (por exemplo, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="2a59a-239">This is hello name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="2a59a-240">Modificar Olá `ReferenceId` atributo `<DefaultUserJourney>` toomatch Olá `Id` de jornada usuário novo Olá que você criou (por exemplo, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="2a59a-240">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello `Id` of hello new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="2a59a-241">Salve suas alterações e, em seguida, carregue o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="2a59a-241">Save your changes, and then upload hello file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="2a59a-242">Testar e solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="2a59a-242">Test and troubleshoot</span></span>

<span data-ttu-id="2a59a-243">tootest Olá política personalizada que você acaba de carregar, em Olá portal do Azure, vá toohello folha de política e, em seguida, clique em **executar agora**.</span><span class="sxs-lookup"><span data-stu-id="2a59a-243">tootest hello custom policy that you just uploaded, in hello Azure portal, go toohello policy blade, and then click **Run now**.</span></span> <span data-ttu-id="2a59a-244">Se ela falhar, consulte [Solucionar problemas com políticas personalizadas](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2a59a-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a59a-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a59a-245">Next steps</span></span>

<span data-ttu-id="2a59a-246">Fornecer comentários muito[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2a59a-246">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
