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
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a>B2C de diretório ativo do Azure: Modificar tooadd novas declarações de inscrição e configure a entrada do usuário.

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Neste artigo, você adicionará uma novo fornecida pelo usuário (uma declaração) de entrada tooyour inscrição usuário jornada.  Você configurará entrada hello como uma lista suspensa e definir se é necessário.

Editado por Sipi tootrigger teste entrega.

## <a name="prerequisites"></a>Pré-requisitos

* Olá concluído as etapas no artigo de saudação [guia de Introdução com as políticas personalizadas](active-directory-b2c-get-started-custom.md).  Teste toosignup jornada de usuário de inscrição/signin Olá uma nova conta local antes de continuar.


A coleta de dados inicial de seus usuários é obtida por meio de inscrição/entrada.  Declarações adicionais podem ser obtidas posteriormente por meio de percursos do usuário de edição de perfil. Sempre que o Azure AD B2C reúne informações diretamente do usuário Olá interativamente, Olá identidade experiência Framework usa seu `selfasserted provider`. Olá estas etapas se aplicam a qualquer momento, esse provedor é usado.


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a>Definir Olá declaração, seu nome de exibição e Olá tipo de entrada do usuário
Permite solicitar Olá usuário seu cidade.  Adicionar Olá após o elemento toohello `<ClaimsSchema>` elemento no arquivo de política de TrustFrameWorkExtensions hello:

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
Há opções adicionais que você pode fazer aqui toocustomize Olá de declaração.  Para um esquema completo, consulte toohello **guia de referência técnica do identidade experiência Framework**.  Este guia será publicado em breve na seção de referência de saudação.

* `<DisplayName>`é uma cadeia de caracteres que define voltadas para o usuário Olá *rótulo*

* `<UserHelpText>`Ajuda o usuário a saudação entender o que é necessário

* `<UserInputType>`Olá seguintes quatro opções realçou abaixo:
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * `RadioSingleSelectduration` – Impõe uma única seleção.
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

    * `DropdownSingleSelect`-Permite a seleção de saudação do único valor válido.

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


* `CheckboxMultiSelect`Permite a seleção de saudação de um ou mais valores.

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

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a>Adicionar Olá declaração toohello sign up/entrar jornada de usuário

1. Adicione a declaração hello como um `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (encontrado no arquivo de política de TrustFrameworkBase Olá).  Observe que este TechnicalProfile usa Olá SelfAssertedAttributeProvider.

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

2. Adicionar Olá declaração toohello UserWriteUsingLogonEmail AAD como uma `<PersistedClaim ClaimTypeReferenceId="city" />` diretório do AAD toowrite Olá declaração toohello após coletá-lo do usuário hello. Você pode ignorar esta etapa se você preferir não toopersist Olá declaração no diretório Olá para uso futuro.

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

3. Adicionar Olá declaração toohello TechnicalProfile que lê do diretório hello quando um usuário fizer logon como um`<OutputClaim ClaimTypeReferenceId="city" />`

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

4. Adicionar Olá `<OutputClaim ClaimTypeReferenceId="city" />` arquivo de política RP toohello SignUporSignIn.xml para esta declaração é enviada toohello aplicativo no token Olá após uma viagem de usuário bem-sucedida.

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

## <a name="test-hello-custom-policy-using-run-now"></a>Testar a política personalizada do hello usando "Executar agora"

1. Olá abrir **folha do Azure AD B2C** e navegue muito**identidade experiência Framework > políticas personalizadas**.
2. Selecione Olá política personalizada que você carregou e, em seguida, clique em Olá **executar agora** botão.
3. Você deve ser capaz de toosign usando um endereço de email.

tela de inscrição Hello no modo de teste deve ser toothis semelhante:

![Captura de tela da opção de inscrição modificada](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  Olá token tooyour back aplicativo agora incluirá Olá `city` conforme mostrado abaixo de declaração
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

## <a name="optional-remove-email-verification-from-signup-journey"></a>Opcional: Remoção da verificação de email do percurso de inscrição

verificação de email tooskip, autor da política Olá pode escolher tooremove `PartnerClaimType="Verified.Email"`. Olá endereço de email serão necessárias, mas não verificado, a menos que "Necessário" = true é removido.  Considere cuidadosamente se esta opção é adequada para seus casos de uso!

Verificar email é habilitado por padrão no hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` no arquivo de política de TrustFrameworkBase Olá no pacote de inicializador de saudação:
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a>Próximas etapas

Adicione Olá novos declaração toohello fluxos para logons de conta social alterando Olá TechnicalProfiles listados abaixo. Esses são usados por conta social/federado logons toowrite e ler dados do usuário hello usando alternativeSecurityId Olá Olá localizador.
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
