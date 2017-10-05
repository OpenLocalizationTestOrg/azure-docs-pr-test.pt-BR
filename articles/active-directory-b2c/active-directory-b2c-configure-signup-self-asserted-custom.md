---
title: "Azure Active Directory B2C: como modificar a inscrição em políticas personalizadas e configurar um provedor autodeclarado"
description: "Um passo a passo sobre como adicionar declarações para inscrição e configurar a entrada do usuário"
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
ms.openlocfilehash: 64b9d904d7d070052e125b479f4719d208c9ff85
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-to-add-new-claims-and-configure-user-input"></a><span data-ttu-id="fa126-103">Azure Active Directory B2C: como modificar a inscrição para adicionar novas declarações e configurar a entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="fa126-103">Azure Active Directory B2C: Modify sign up to add new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="fa126-104">Neste artigo, você adicionará uma nova entrada de usuário fornecido (uma declaração) para seu percurso do usuário para inscrição.</span><span class="sxs-lookup"><span data-stu-id="fa126-104">In this article, you will add a new user provided entry (a claim) to your signup user journey.</span></span>  <span data-ttu-id="fa126-105">Você configurará a entrada como uma lista suspensa e a definirá se for necessário.</span><span class="sxs-lookup"><span data-stu-id="fa126-105">You will configure the entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="fa126-106">Editado por Sipi para disparar a entrega de teste.</span><span class="sxs-lookup"><span data-stu-id="fa126-106">Edited by Sipi to trigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa126-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fa126-107">Prerequisites</span></span>

* <span data-ttu-id="fa126-108">Conclua as etapas no artigo [Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="fa126-108">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="fa126-109">Teste o percurso do usuário para entrada/inscrição para fazer uma inscrição e uma conta local nova antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="fa126-109">Test the signup/signin user journey to signup a new local account before proceeding.</span></span>


<span data-ttu-id="fa126-110">A coleta de dados inicial de seus usuários é obtida por meio de inscrição/entrada.</span><span class="sxs-lookup"><span data-stu-id="fa126-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="fa126-111">Declarações adicionais podem ser obtidas posteriormente por meio de percursos do usuário de edição de perfil.</span><span class="sxs-lookup"><span data-stu-id="fa126-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="fa126-112">Toda vez que o Azure AD B2C reúne informações diretamente do usuário de forma interativa, o Identity Experience Framework usa seu `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="fa126-112">Anytime Azure AD B2C gathers information directly from the user interactively, the Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="fa126-113">As etapas a seguir se aplicam sempre que esse provedor é usado.</span><span class="sxs-lookup"><span data-stu-id="fa126-113">The steps below apply anytime this provider is used.</span></span>


## <a name="define-the-claim-its-display-name-and-the-user-input-type"></a><span data-ttu-id="fa126-114">Definir a declaração, seu nome de exibição e o tipo de entrada do usuário</span><span class="sxs-lookup"><span data-stu-id="fa126-114">Define the claim, its display name and the user input type</span></span>
<span data-ttu-id="fa126-115">Permite perguntar ao usuário sobre a cidade dele.</span><span class="sxs-lookup"><span data-stu-id="fa126-115">Lets ask the user for their city.</span></span>  <span data-ttu-id="fa126-116">Adicione o seguinte elemento para o elemento `<ClaimsSchema>` no arquivo de política de TrustFrameWorkExtensions:</span><span class="sxs-lookup"><span data-stu-id="fa126-116">Add the following element to the `<ClaimsSchema>` element in the TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="fa126-117">Existem outras opções que você pode fazer aqui para personalizar a declaração.</span><span class="sxs-lookup"><span data-stu-id="fa126-117">There are additional choices you can make here to customize the claim.</span></span>  <span data-ttu-id="fa126-118">Para um esquema completo, consulte o **Guia de Referência Técnica do Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="fa126-118">For a full schema, refer to the **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="fa126-119">Este guia será publicado em breve na seção de referência.</span><span class="sxs-lookup"><span data-stu-id="fa126-119">This guide will be published soon in the reference section.</span></span>

* <span data-ttu-id="fa126-120">`<DisplayName>` é uma cadeia de caracteres que define o *rótulo* voltado para o usuário</span><span class="sxs-lookup"><span data-stu-id="fa126-120">`<DisplayName>` is a string that defines the user-facing *label*</span></span>

* <span data-ttu-id="fa126-121">`<UserHelpText>` ajuda o usuário a entender o que é necessário</span><span class="sxs-lookup"><span data-stu-id="fa126-121">`<UserHelpText>` helps the user understand what is required</span></span>

* <span data-ttu-id="fa126-122">`<UserInputType>` tem as quatro opções a seguir destacadas abaixo:</span><span class="sxs-lookup"><span data-stu-id="fa126-122">`<UserInputType>` has the following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="fa126-123">`RadioSingleSelectduration` – Impõe uma única seleção.</span><span class="sxs-lookup"><span data-stu-id="fa126-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
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

    * <span data-ttu-id="fa126-124">`DropdownSingleSelect` – Permite a seleção de um único valor válido.</span><span class="sxs-lookup"><span data-stu-id="fa126-124">`DropdownSingleSelect` - Allows the selection of only valid value.</span></span>

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


* <span data-ttu-id="fa126-126">`CheckboxMultiSelect` Permite a seleção de um ou mais valores.</span><span class="sxs-lookup"><span data-stu-id="fa126-126">`CheckboxMultiSelect` Allows for the selection of one or more values.</span></span>

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

## <a name="add-the-claim-to-the-sign-upsign-in-user-journey"></a><span data-ttu-id="fa126-128">Adicione a declaração ao percurso do usuário de entrada/inscrição</span><span class="sxs-lookup"><span data-stu-id="fa126-128">Add the claim to the sign up/sign in user journey</span></span>

1. <span data-ttu-id="fa126-129">Adicione a declaração como um `<OutputClaim ClaimTypeReferenceId="city"/>` ao TechnicalProfile `LocalAccountSignUpWithLogonEmail` (encontrado no arquivo de política de TrustFrameworkBase).</span><span class="sxs-lookup"><span data-stu-id="fa126-129">Add the claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` to the TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in the TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="fa126-130">Observe que este TechnicalProfile usa o SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="fa126-130">Note this TechnicalProfile uses the SelfAssertedAttributeProvider.</span></span>

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
      <!-- Optional claims, to be collected from the user -->
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

2. <span data-ttu-id="fa126-131">Adicione a declaração para o AAD-UserWriteUsingLogonEmail como um `<PersistedClaim ClaimTypeReferenceId="city" />` para gravar a declaração para o diretório do AAD depois de coletar do usuário.</span><span class="sxs-lookup"><span data-stu-id="fa126-131">Add the claim to the AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` to write the claim to the AAD directory after collecting it from the user.</span></span> <span data-ttu-id="fa126-132">Você pode ignorar esta etapa se você preferir não manter a declaração no diretório para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="fa126-132">You may skip this step if you prefer not to persist the claim in the directory for future use.</span></span>

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

3. <span data-ttu-id="fa126-133">Adicione a declaração do TechnicalProfile, que lê do diretório quando um usuário faz logon como um `<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="fa126-133">Add the claim to the TechnicalProfile that reads from the directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for the provided user ID.</Item>
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

4. <span data-ttu-id="fa126-134">Adicione `<OutputClaim ClaimTypeReferenceId="city" />` ao arquivo de política RP SignUporSignIn.xml para que essa declaração seja enviada para o aplicativo no token após um percurso do usuário bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="fa126-134">Add the `<OutputClaim ClaimTypeReferenceId="city" />` to the RP policy file SignUporSignIn.xml so this claim is sent to the application in the token after a successful user journey.</span></span>

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

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="fa126-135">Testar a política personalizada usando a opção “Executar Agora”</span><span class="sxs-lookup"><span data-stu-id="fa126-135">Test the custom policy using "Run Now"</span></span>

1. <span data-ttu-id="fa126-136">Abra a **Folha B2C do Azure AD** e navegue até **Identity Experience Framework > Políticas personalizadas**.</span><span class="sxs-lookup"><span data-stu-id="fa126-136">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="fa126-137">Selecione a política personalizada carregada e clique no botão **Executar agora**.</span><span class="sxs-lookup"><span data-stu-id="fa126-137">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="fa126-138">Você deverá conseguir se inscrever usando um endereço de email.</span><span class="sxs-lookup"><span data-stu-id="fa126-138">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="fa126-139">A tela de inscrição no modo de teste deve ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="fa126-139">The signup screen in test mode should look similar to this:</span></span>

![Captura de tela da opção de inscrição modificada](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="fa126-141">O token de volta para seu aplicativo incluirá a declaração `city` conforme mostrado abaixo</span><span class="sxs-lookup"><span data-stu-id="fa126-141">The token back to your application will now include the `city` claim as shown below</span></span>
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

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="fa126-142">Opcional: Remoção da verificação de email do percurso de inscrição</span><span class="sxs-lookup"><span data-stu-id="fa126-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="fa126-143">Para ignorar a verificação de email, o autor da política pode optar por remover `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="fa126-143">To skip email verification, the policy author can choose to remove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="fa126-144">O endereço de email será necessário, mas não verificado, a menos que "Required" = true seja removido.</span><span class="sxs-lookup"><span data-stu-id="fa126-144">The email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="fa126-145">Considere cuidadosamente se esta opção é adequada para seus casos de uso!</span><span class="sxs-lookup"><span data-stu-id="fa126-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="fa126-146">Verificar email está habilitado por padrão no `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` no arquivo de política TrustFrameworkBase no pacote starter:</span><span class="sxs-lookup"><span data-stu-id="fa126-146">Verified email is enabled by default in the `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in the TrustFrameworkBase policy file in the starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="fa126-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fa126-147">Next steps</span></span>

<span data-ttu-id="fa126-148">Adicione a nova declaração aos fluxos para logons de conta social alterando os TechnicalProfiles listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="fa126-148">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed below.</span></span> <span data-ttu-id="fa126-149">Eles são usados por logons de conta social/federados para gravar e ler os dados do usuário usando o alternativeSecurityId como o localizador.</span><span class="sxs-lookup"><span data-stu-id="fa126-149">These are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
