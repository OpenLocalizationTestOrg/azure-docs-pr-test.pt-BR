---
title: "Azure Active Directory B2C: como modificar a inscrição em políticas personalizadas e configurar um provedor autodeclarado"
description: "Um passo a passo sobre como adicionar declarações toosign backup e configurar a entrada do usuário Olá"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: tbd
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/29/2017
ms.author: joroja
ms.openlocfilehash: c31d737263fef3e771bdf451b809b0ca522c8fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a><span data-ttu-id="f96d2-103">B2C de diretório ativo do Azure: Modificar tooadd novas declarações de inscrição e configure a entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="f96d2-103">Azure Active Directory B2C: Modify sign up tooadd new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="f96d2-104">Neste artigo, você adicionará uma novo fornecida pelo usuário (uma declaração) de entrada tooyour inscrição usuário jornada.</span><span class="sxs-lookup"><span data-stu-id="f96d2-104">In this article, you will add a new user provided entry (a claim) tooyour signup user journey.</span></span>  <span data-ttu-id="f96d2-105">Você configurará entrada hello como uma lista suspensa e definir se é necessário.</span><span class="sxs-lookup"><span data-stu-id="f96d2-105">You will configure hello entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="f96d2-106">Editado por Sipi tootrigger teste entrega.</span><span class="sxs-lookup"><span data-stu-id="f96d2-106">Edited by Sipi tootrigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f96d2-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f96d2-107">Prerequisites</span></span>

* <span data-ttu-id="f96d2-108">Olá concluído as etapas no artigo de saudação [guia de Introdução com as políticas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="f96d2-108">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="f96d2-109">Teste toosignup jornada de usuário de inscrição/signin Olá uma nova conta local antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="f96d2-109">Test hello signup/signin user journey toosignup a new local account before proceeding.</span></span>


<span data-ttu-id="f96d2-110">A coleta de dados inicial de seus usuários é obtida por meio de inscrição/entrada.</span><span class="sxs-lookup"><span data-stu-id="f96d2-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="f96d2-111">Declarações adicionais podem ser obtidas posteriormente por meio de percursos do usuário de edição de perfil.</span><span class="sxs-lookup"><span data-stu-id="f96d2-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="f96d2-112">Sempre que o Azure AD B2C reúne informações diretamente do usuário Olá interativamente, Olá identidade experiência Framework usa seu `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="f96d2-112">Anytime Azure AD B2C gathers information directly from hello user interactively, hello Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="f96d2-113">Olá estas etapas se aplicam a qualquer momento, esse provedor é usado.</span><span class="sxs-lookup"><span data-stu-id="f96d2-113">hello steps below apply anytime this provider is used.</span></span>


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a><span data-ttu-id="f96d2-114">Definir Olá declaração, seu nome de exibição e Olá tipo de entrada do usuário</span><span class="sxs-lookup"><span data-stu-id="f96d2-114">Define hello claim, its display name and hello user input type</span></span>
<span data-ttu-id="f96d2-115">Permite solicitar Olá usuário seu cidade.</span><span class="sxs-lookup"><span data-stu-id="f96d2-115">Lets ask hello user for their city.</span></span>  <span data-ttu-id="f96d2-116">Adicionar Olá após o elemento toohello `<ClaimsSchema>` elemento no arquivo de política de TrustFrameWorkExtensions hello:</span><span class="sxs-lookup"><span data-stu-id="f96d2-116">Add hello following element toohello `<ClaimsSchema>` element in hello TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="f96d2-117">Há opções adicionais que você pode fazer aqui toocustomize Olá de declaração.</span><span class="sxs-lookup"><span data-stu-id="f96d2-117">There are additional choices you can make here toocustomize hello claim.</span></span>  <span data-ttu-id="f96d2-118">Para um esquema completo, consulte toohello **guia de referência técnica do identidade experiência Framework**.</span><span class="sxs-lookup"><span data-stu-id="f96d2-118">For a full schema, refer toohello **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="f96d2-119">Este guia será publicado em breve na seção de referência de saudação.</span><span class="sxs-lookup"><span data-stu-id="f96d2-119">This guide will be published soon in hello reference section.</span></span>

* <span data-ttu-id="f96d2-120">`<DisplayName>`é uma cadeia de caracteres que define voltadas para o usuário Olá *rótulo*</span><span class="sxs-lookup"><span data-stu-id="f96d2-120">`<DisplayName>` is a string that defines hello user-facing *label*</span></span>

* <span data-ttu-id="f96d2-121">`<UserHelpText>`Ajuda o usuário a saudação entender o que é necessário</span><span class="sxs-lookup"><span data-stu-id="f96d2-121">`<UserHelpText>` helps hello user understand what is required</span></span>

* <span data-ttu-id="f96d2-122">`<UserInputType>`Olá seguintes quatro opções realçou abaixo:</span><span class="sxs-lookup"><span data-stu-id="f96d2-122">`<UserInputType>` has hello following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="f96d2-123">`RadioSingleSelectduration` – Impõe uma única seleção.</span><span class="sxs-lookup"><span data-stu-id="f96d2-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>RadioSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

    * <span data-ttu-id="f96d2-124">`DropdownSingleSelect`-Permite a seleção de saudação do único valor válido.</span><span class="sxs-lookup"><span data-stu-id="f96d2-124">`DropdownSingleSelect` - Allows hello selection of only valid value.</span></span>

![Captura de tela da opção de lista suspensa](./media/active-directory-b2c-configure-signup-self-asserted-custom/dropdown-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```


* <span data-ttu-id="f96d2-126">`CheckboxMultiSelect`Permite a seleção de saudação de um ou mais valores.</span><span class="sxs-lookup"><span data-stu-id="f96d2-126">`CheckboxMultiSelect` Allows for hello selection of one or more values.</span></span>

![Captura de tela de opção com seleção múltipla](./media/active-directory-b2c-configure-signup-self-asserted-custom/multiselect-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>Receive updates from which cities?</DisplayName>
  <DataType>string</DataType>
  <UserInputType>CheckboxMultiSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a><span data-ttu-id="f96d2-128">Adicionar Olá declaração toohello sign up/entrar jornada de usuário</span><span class="sxs-lookup"><span data-stu-id="f96d2-128">Add hello claim toohello sign up/sign in user journey</span></span>

1. <span data-ttu-id="f96d2-129">Adicione a declaração hello como um `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (encontrado no arquivo de política de TrustFrameworkBase Olá).</span><span class="sxs-lookup"><span data-stu-id="f96d2-129">Add hello claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in hello TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="f96d2-130">Observe que este TechnicalProfile usa Olá SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="f96d2-130">Note this TechnicalProfile uses hello SelfAssertedAttributeProvider.</span></span>

  ```xml
  <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
    <DisplayName>Email signup</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
      <Item Key="IpAddressClaimReferenceId">IpAddress</Item>
      <Item Key="ContentDefinitionReferenceId">api.localaccountsignup</Item>
      <Item Key="language.button_continue">Create</Item>
    </Metadata>
    <CryptographicKeys>
      <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
    </CryptographicKeys>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" />
    </InputClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
      <OutputClaim ClaimTypeReferenceId="newPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="reenterPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" />
      <OutputClaim ClaimTypeReferenceId="newUser" />
      <!-- Optional claims, toobe collected from hello user -->
      <OutputClaim ClaimTypeReferenceId="givenName" />
      <OutputClaim ClaimTypeReferenceId="surName" />
      <OutputClaim ClaimTypeReferenceId="city"/>
    </OutputClaims>
    <ValidationTechnicalProfiles>
      <ValidationTechnicalProfile ReferenceId="AAD-UserWriteUsingLogonEmail" />
    </ValidationTechnicalProfiles>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

2. <span data-ttu-id="f96d2-131">Adicionar Olá declaração toohello UserWriteUsingLogonEmail AAD como uma `<PersistedClaim ClaimTypeReferenceId="city" />` diretório do AAD toowrite Olá declaração toohello após coletá-lo do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="f96d2-131">Add hello claim toohello AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello claim toohello AAD directory after collecting it from hello user.</span></span> <span data-ttu-id="f96d2-132">Você pode ignorar esta etapa se você preferir não toopersist Olá declaração no diretório Olá para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="f96d2-132">You may skip this step if you prefer not toopersist hello claim in hello directory for future use.</span></span>

  ```xml
  <!-- Technical profiles for local accounts -->
  <TechnicalProfile Id="AAD-UserWriteUsingLogonEmail">
    <Metadata>
      <Item Key="Operation">Write</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">true</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" Required="true" />
    </InputClaims>
    <PersistedClaims>
      <!-- Required claims -->
      <PersistedClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" />
      <PersistedClaim ClaimTypeReferenceId="newPassword" PartnerClaimType="password" />
      <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />
      <PersistedClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration" />
      <!-- Optional claims. -->
      <PersistedClaim ClaimTypeReferenceId="givenName" />
      <PersistedClaim ClaimTypeReferenceId="surname" />
      <PersistedClaim ClaimTypeReferenceId="city" />
    </PersistedClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

3. <span data-ttu-id="f96d2-133">Adicionar Olá declaração toohello TechnicalProfile que lê do diretório hello quando um usuário fizer logon como um`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="f96d2-133">Add hello claim toohello TechnicalProfile that reads from hello directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for hello provided user ID.</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames" Required="true" />
    </InputClaims>
    <OutputClaims>
      <!-- Required claims -->
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <!-- Optional claims -->
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="displayName" />
      <OutputClaim ClaimTypeReferenceId="otherMails" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
  </TechnicalProfile>
  ```

4. <span data-ttu-id="f96d2-134">Adicionar Olá `<OutputClaim ClaimTypeReferenceId="city" />` arquivo de política RP toohello SignUporSignIn.xml para esta declaração é enviada toohello aplicativo no token Olá após uma viagem de usuário bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="f96d2-134">Add hello `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP policy file SignUporSignIn.xml so this claim is sent toohello application in hello token after a successful user journey.</span></span>

  ```xml
  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="city" />
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
  ```

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="f96d2-135">Testar a política personalizada do hello usando "Executar agora"</span><span class="sxs-lookup"><span data-stu-id="f96d2-135">Test hello custom policy using "Run Now"</span></span>

1. <span data-ttu-id="f96d2-136">Olá abrir **folha do Azure AD B2C** e navegue muito**identidade experiência Framework > políticas personalizadas**.</span><span class="sxs-lookup"><span data-stu-id="f96d2-136">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="f96d2-137">Selecione Olá política personalizada que você carregou e, em seguida, clique em Olá **executar agora** botão.</span><span class="sxs-lookup"><span data-stu-id="f96d2-137">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="f96d2-138">Você deve ser capaz de toosign usando um endereço de email.</span><span class="sxs-lookup"><span data-stu-id="f96d2-138">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="f96d2-139">tela de inscrição Hello no modo de teste deve ser toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="f96d2-139">hello signup screen in test mode should look similar toothis:</span></span>

![Captura de tela da opção de inscrição modificada](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="f96d2-141">Olá token tooyour back aplicativo agora incluirá Olá `city` conforme mostrado abaixo de declaração</span><span class="sxs-lookup"><span data-stu-id="f96d2-141">hello token back tooyour application will now include hello `city` claim as shown below</span></span>
```json
{
  "exp": 1493596822,
  "nbf": 1493593222,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "9c2a3a9e-ac65-4e46-a12d-9557b63033a9",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustf_signup_signin",
  "nonce": "defaultNonce",
  "iat": 1493593222,
  "auth_time": 1493593222,
  "email": "joe@outlook.com",
  "given_name": "Joe",
  "family_name": "Ras",
  "city": "Bellevue",
  "name": "unknown"
}
```

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="f96d2-142">Opcional: Remoção da verificação de email do percurso de inscrição</span><span class="sxs-lookup"><span data-stu-id="f96d2-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="f96d2-143">verificação de email tooskip, autor da política Olá pode escolher tooremove `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="f96d2-143">tooskip email verification, hello policy author can choose tooremove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="f96d2-144">Olá endereço de email serão necessárias, mas não verificado, a menos que "Necessário" = true é removido.</span><span class="sxs-lookup"><span data-stu-id="f96d2-144">hello email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="f96d2-145">Considere cuidadosamente se esta opção é adequada para seus casos de uso!</span><span class="sxs-lookup"><span data-stu-id="f96d2-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="f96d2-146">Verificar email é habilitado por padrão no hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` no arquivo de política de TrustFrameworkBase Olá no pacote de inicializador de saudação:</span><span class="sxs-lookup"><span data-stu-id="f96d2-146">Verified email is enabled by default in hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in hello TrustFrameworkBase policy file in hello starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="f96d2-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f96d2-147">Next steps</span></span>

<span data-ttu-id="f96d2-148">Adicione Olá novos declaração toohello fluxos para logons de conta social alterando Olá TechnicalProfiles listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="f96d2-148">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed below.</span></span> <span data-ttu-id="f96d2-149">Esses são usados por conta social/federado logons toowrite e ler dados do usuário hello usando alternativeSecurityId Olá Olá localizador.</span><span class="sxs-lookup"><span data-stu-id="f96d2-149">These are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
