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
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: Adicionar Google+ como um provedor de identidade OAuth2 usando políticas personalizadas

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Este guia mostra como tooenable entrar para usuários da conta do Google + através do uso de saudação do [políticas personalizadas](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Pré-requisitos

Olá concluir as etapas em Olá [guia de Introdução com políticas personalizadas](active-directory-b2c-get-started-custom.md) artigo.

As etapas incluem:

1.  Criar um aplicativo de conta do Google+.
2.  Adicionando Olá Google + conta aplicativo chave tooAzure AD B2C
3.  Adicionar política de tooa do provedor de declarações
4.  Registrando Olá Google + conta declarações provedor tooa usuário jornada
5.  Carregando tooan de política de saudação do Azure AD B2C locatário e testá-lo

## <a name="create-a-google-account-application"></a>Criar um aplicativo de conta do Google+
toouse Google + como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo do Google + e fornecê-lo com os parâmetros de saudação à direita. Você pode registrar um aplicativo do Google+ aqui: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)

1.  Vá toohello [Console de desenvolvedores do Google](https://console.developers.google.com/) e entre com suas credenciais de conta do Google +.
2.  Clique em **Criar projeto**, insira um **Nome de projeto** e clique em **Criar**.

3.  Clique em Olá **menu projetos**.

    ![Conta do Google+ - Selecionar o projeto](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  Clique em Olá  **+**  botão.

    ![Conta do Google+ - Criar novo projeto](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  Insira um **Nome de projeto** e clique em **Criar**.

    ![Conta do Google+ - Novo projeto](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  Aguarde até que o projeto hello está pronto e clique em Olá **menu projetos**.

    ![Conta do Google + - Aguarde até que o novo projeto é toouse pronto](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  Clique no nome do seu projeto.

    ![Conta do Google + - novo projeto de saudação Select](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  Clique em **Manager API** e, em seguida, clique em **credenciais** em Olá barra de navegação esquerda.
9.  Clique em Olá **tela de consentimento de OAuth** guia na parte superior da saudação.

    ![Conta do Google+ - Definir tela de consentimento de OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  Selecione ou especifique um **Endereço de email** válido, forneça um **Nome de produto** e clique em **Salvar**.

    ![Google+ - Credenciais do aplicativo](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  Clique em **Novas credenciais** e escolha **ID do cliente OAuth**.

    ![Google+ - Criar novas credenciais do aplicativo](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  Em **Tipo de aplicativo**, selecione **Aplicativo Web**.

    ![Google+ - Selecione o tipo de aplicativo](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  Forneça um **nome** para seu aplicativo, insira `https://login.microsoftonline.com` em Olá **origens do JavaScript autorizado** campo, e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **autorizados redirecionar URIs**campo. Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com). Olá **{locatário}** valor diferencia maiusculas de minúsculas. Clique em **Criar**.

    ![Google + - Forneça origens de JavaScript autorizadas e URIs de redirecionamento](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  Copie os valores de saudação do **Id do cliente** e **segredo do cliente**. Você precisa ambos tooconfigure Google + como um provedor de identidade no seu locatário. **Segredo do cliente** é uma credencial de segurança importante.

    ![Google + - valores de saudação de cópia de segredo de cliente e a Id do cliente](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a>Adicionar Olá Google + conta aplicativo chave tooAzure AD B2C
Federação com contas do Google + requer um segredo do cliente para o Google + conta tootrust B2C do Azure AD em nome do aplicativo hello. É necessário toostore seu segredo do aplicativo do Google + no locatário do Azure AD B2C:  

1.  Vá locatário tooyour B2C do Azure AD e selecione **B2C configurações** > **Framework de experiência de identidade**
2.  Selecione **chaves política** tooview chaves de saudação disponíveis em seu locatário.
3.  Clique em **+Adicionar**.
4.  Para as **Opções**, use **Manual**.
5.  Para o **Nome**, use `GoogleSecret`.  
    prefixo de saudação `B2C_1A_` podem ser adicionadas automaticamente.
6.  Em Olá **segredo** , digite o segredo do aplicativo Microsoft de https://apps.dev.microsoft.com
7.  Para o **Uso da chave**, use **Assinatura**.
8.  Clique em **Criar**
9.  Confirme que você criou a chave Olá `B2C_1A_GoogleSecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Adicionar um provedor de declarações à política de extensão

Se você quiser usuários toosign no usando a conta do Google +, você precisa toodefine Google + conta como um provedor de declarações. Em outras palavras, você precisa toospecify do Azure AD B2C se comunica com um ponto de extremidade. ponto de extremidade Olá fornece um conjunto de declarações que são usados pelo Azure AD B2C tooverify que um usuário específico autenticado.

Defina a Conta do Google+ como um provedor de declarações adicionando o nó `<ClaimsProvider>` em seu arquivo de política da extensão:

1.  Abra o arquivo de política de extensão de saudação (TrustFrameworkExtensions.xml) do seu diretório de trabalho. Se você precisar de um editor de XML, [experimente o Visual Studio Code](https://code.visualstudio.com/download), um editor de plataforma cruzada leve.
2.  Localize Olá `<ClaimsProviders>` seção
3.  Adicionar Olá seguindo o trecho XML em Olá `ClaimsProviders` elemento e substituir `client_id` valor com sua ID de cliente de aplicativo, conta Google + antes de salvar o arquivo hello.  

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

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Registrar Olá Google + conta declarações provedor tooSign se ou entrar a jornada de usuário

provedor de identidade Olá foi configurado.  No entanto, não está disponível em qualquer uma das telas de entrada-o/entrada hello. Adicionar Olá Google + conta identidade provedor tooyour usuário `SignUpOrSignIn` jornada de usuário. toomake-lo, podemos criar uma duplicata de uma jornada de usuário do modelo existente.  Em seguida, adicionamos Olá Google + conta provedor de identidade:

>[!NOTE]
>
>Se você copiou Olá `<UserJourneys>` elemento de arquivo de base de seu arquivo de extensão da diretiva toohello (TrustFrameworkExtensions.xml), você pode ignorar a seção de toothis.

1.  Abra o arquivo de base de saudação da política (por exemplo, TrustFrameworkBase.xml).
2.  Localize Olá `<UserJourneys>` elemento e cópia Olá todo conteúdo do `<UserJourneys>` nó.
3.  Abra o arquivo de extensão da saudação (por exemplo, TrustFrameworkExtensions.xml) e localize Olá `<UserJourneys>` elemento. Se o elemento de saudação não existir, adicione um.
4.  Cole a todo o conteúdo de saudação `<UserJournesy>` nó que você copiou como um filho do hello `<UserJourneys>` elemento.

### <a name="display-hello-button"></a>Botão de saudação de exibição
Olá `<ClaimsProviderSelections>` elemento define a lista de saudação das opções de seleção de provedor de declarações e sua ordem.  `<ClaimsProviderSelection>`elemento é análogo tooan botão de provedor de identidade em uma página de entrada-o/entrar. Se você adicionar um `<ClaimsProviderSelection>` elemento para a conta do Google +, um novo botão aparece quando um usuário chega na página de saudação. tooadd este elemento:

1.  Localize Olá `<UserJourney>` nó inclui `Id="SignUpOrSignIn"` em jornada saudação do usuário que você copiou.
2.  Localizar Olá `<OrchestrationStep>` nó inclui`Order="1"`
3.  Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Ação de link de saudação botão tooan
Agora que você tem um botão em vigor, é necessário toolink-tooan ação. ação de Hello, nesse caso, é para o Azure AD B2C toocommunicate com tooreceive de conta do Google + um token.

1.  Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.
2.  Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * Certifique-se de saudação `Id` tem Olá mesmo valor de `TargetClaimsExchangeId` em Olá anterior seção
> * Certifique-se de `TechnicalProfileReferenceId` ID está definida toohello perfil técnico que você criou anteriormente (Google-OAUTH).

## <a name="upload-hello-policy-tooyour-tenant"></a>Carregar o locatário de tooyour política Olá
1.  Em Olá [portal do Azure](https://portal.azure.com), alternar para Olá [contexto do seu locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)e abra hello **do Azure AD B2C** folha.
2.  Selecione **Estrutura de Experiência de Identidade**.
3.  Olá abrir **todas as políticas** folha.
4.  Selecione **Carregar Política**.
5.  Verificar **substituir a política de saudação se ela existe** caixa.
6.  **Carregar** TrustFrameworkExtensions.xml e certifique-se de que ele não falha na validação de saudação

## <a name="test-hello-custom-policy-by-using-run-now"></a>Testar a política personalizada do hello usando Executar agora
1.  Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.

    >[!NOTE]
    >
    >    **Executar agora** requer pelo menos um aplicativo toobe pré-registrado no locatário hello. 
    >    toolearn como tooregister aplicativos, consulte hello Azure AD B2C [começar](active-directory-b2c-get-started.md) artigo ou hello [registro do aplicativo](active-directory-b2c-app-registration.md) artigo.


2.  Abra **B2C_1A_signup_signin**, Olá política personalizada do terceira parte confiável (RP) que você carregou. Selecione **Executar Agora**.
3.  Você deve ser capaz de toosign usando a conta do Google +.

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a>[Opcional] Registrar Olá Google + conta declarações provedor tooProfile Editar usuário jornada
Talvez você queira tooadd Olá Google + conta provedor de identidade também tooyour usuário `ProfileEdit` jornada de usuário. toomake disponível, podemos Repita Olá último duas etapas:

### <a name="display-hello-button"></a>Botão de saudação de exibição
1.  Abra o arquivo de extensão de saudação da política (por exemplo, TrustFrameworkExtensions.xml).
2.  Localize Olá `<UserJourney>` nó inclui `Id="ProfileEdit"` em jornada saudação do usuário que você copiou.
3.  Localizar Olá `<OrchestrationStep>` nó inclui`Order="1"`
4.  Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Ação de link de saudação botão tooan
1.  Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.
2.  Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Testar a política personalizada de perfil Editar hello usando Executar agora

1.  Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.
2.  Abra **B2C_1A_ProfileEdit**, Olá política personalizada do terceira parte confiável (RP) que você carregou. Selecione **Executar Agora**.
3.  Você deve ser capaz de toosign usando a conta do Google +.

## <a name="download-hello-complete-policy-files"></a>Baixar arquivos de política completa Olá
Opcional: É recomendável que criar o seu cenário usando seus próprios arquivos de política personalizada após a conclusão Olá guia de Introdução com as políticas personalizadas percorrer em vez de usar esses arquivos de exemplo.  [Arquivos de política de exemplo para referência](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
