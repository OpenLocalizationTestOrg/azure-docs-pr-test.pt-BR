---
title: "Azure Active Directory B2C: Adicionar MSA (Conta da Microsoft) como um provedor de identidade usando Políticas personalizadas"
description: Exemplo usando Microsoft como provedor de identidade usando o protocolo OIDC (OpenID Connect)
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
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: Adicionar MSA (Conta da Microsoft) como um provedor de identidade usando políticas personalizadas

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Este artigo mostra como tooenable entrar para usuários de conta da Microsoft (MSA) através do uso de saudação do [políticas personalizadas](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Pré-requisitos
Olá concluir as etapas em Olá [guia de Introdução com políticas personalizadas](active-directory-b2c-get-started-custom.md) artigo.

As etapas incluem:

1.  Criar um aplicativo de conta da Microsoft.
2.  Adicionando tooAzure de chave aplicativo AD B2C de conta de Microsoft hello
3.  Adicionar política de tooa do provedor de declarações
4.  Registrando jornada de usuário tooa do provedor de declarações de Account da Microsoft hello
5.  Carregando tooan de política de saudação do Azure AD B2C locatário e testá-lo

## <a name="create-a-microsoft-account-application"></a>Criar um aplicativo de conta da Microsoft
toouse Microsoft conta como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo de conta da Microsoft e fornecê-lo com os parâmetros de saudação à direita. Você precisa de uma conta da Microsoft. Se você não tiver uma, visite [https://www.live.com/](https://www.live.com/).

1.  Vá toohello [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e entre com suas credenciais de conta da Microsoft.
2.  Clique em **Adicionar um aplicativo**.

    ![Conta da Microsoft – Adicionar um aplicativo](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  Forneça um **Nome** para seu aplicativo, **Email de contato**, desmarque **Deixe-nos ajudar você a começar** e clique em **Criar**.

    ![Conta da Microsoft - Registrar seu aplicativo](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  Copie o valor de saudação do **Id do aplicativo**. Precisar tooconfigure conta da Microsoft como um provedor de identidade em seu locatário.

    ![Conta da Microsoft - copiar o valor de saudação do Id do aplicativo](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  Clique em **Adicionar plataforma**

    ![Conta da Microsoft - Adicionar plataforma](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  Na lista de plataforma hello, escolha **Web**.

    ![Conta da Microsoft - na lista de plataformas de saudação escolher Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  Digite `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **URIs de redirecionamento** campo. Substitua **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com).

    ![Conta da Microsoft – Definir URLs de redirecionamento](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  Clique em **gerar nova senha** em Olá **segredos do aplicativo** seção. Cópia Olá nova senha exibida na tela. Precisar tooconfigure conta da Microsoft como um provedor de identidade em seu locatário. A senha é uma credencial de segurança importante.

    ![Conta da Microsoft - Gerar nova senha](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Conta da Microsoft - nova senha de saudação de cópia](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  Caixa de saudação de seleção que diz **suporte do SDK do Live** em Olá **opções avançadas de** seção. Clique em **Salvar**.

    ![Conta da Microsoft - Suporte ao SDK do Live](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a>Adicionar tooAzure de chave aplicativo AD B2C de conta de Microsoft hello
Federação com contas da Microsoft requer um segredo do cliente para tootrust de conta do Microsoft Azure AD B2C em nome do aplicativo hello. É necessário toostore seu secert de aplicativo de conta Microsoft no Azure AD B2C locatário:   

1.  Vá locatário tooyour B2C do Azure AD e selecione **B2C configurações** > **Framework de experiência de identidade**
2.  Selecione **chaves política** tooview chaves de saudação disponíveis em seu locatário.
3.  Clique em **+Adicionar**.
4.  Para as **Opções**, use **Manual**.
5.  Para o **Nome**, use `MSASecret`.  
    prefixo de saudação `B2C_1A_` podem ser adicionadas automaticamente.
6.  Em Olá **segredo** , digite o segredo do aplicativo Microsoft de https://apps.dev.microsoft.com
7.  Para o **Uso da chave**, use **Assinatura**.
8.  Clique em **Criar**
9.  Confirme que você criou a chave Olá `B2C_1A_MSASecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Adicionar um provedor de declarações à política de extensão
Se você quiser usuários toosign no usando Account da Microsoft, você precisa toodefine Account da Microsoft como um provedor de declarações. Em outras palavras, você precisa toospecify do Azure AD B2C se comunica com um ponto de extremidade. ponto de extremidade Olá fornece um conjunto de declarações que são usados pelo Azure AD B2C tooverify que um usuário específico autenticado.

Defina a Conta da Microsoft como um provedor de declarações adicionando o nó `<ClaimsProvider>` em seu arquivo de política da extensão:

1.  Abra o arquivo de política de extensão de saudação (TrustFrameworkExtensions.xml) do seu diretório de trabalho. Se você precisar de um editor de XML, [experimente o Visual Studio Code](https://code.visualstudio.com/download), um editor de plataforma cruzada leve.
2.  Localize Olá `<ClaimsProviders>` seção
3.  Adicione o seguinte trecho XML em Olá `ClaimsProviders` elemento:

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  Substitua o valor `client_id` pela Id de cliente do aplicativo da Conta da Microsoft

5.  Salve o arquivo hello.

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Registrar tooSign de provedor de declarações Olá Account da Microsoft se ou entrar jornada de usuário

Neste ponto, o provedor de identidade Olá foi configurado, mas não está disponível em qualquer uma das telas de entrada-o/entrada hello. Agora você precisa tooadd Olá Account Microsoft identidade provedor tooyour usuário `SignUpOrSignIn` jornada de usuário. toomake-lo, podemos criar uma duplicata de uma jornada de usuário do modelo existente.  Em seguida, adicionamos provedor de identidade Olá Account da Microsoft:

> [!NOTE]
>
>Se você tiver copiado anteriormente Olá `<UserJourneys>` elemento de arquivo de base de seu arquivo de extensão de toohello política `TrustFrameworkExtensions.xml`, você pode ignorar a seção de toothis.

1.  Abra o arquivo de base de saudação da política (por exemplo, TrustFrameworkBase.xml).
2.  Localize Olá `<UserJourneys>` elemento e cópia Olá todo conteúdo do `<UserJourneys>` nó.
3.  Abra o arquivo de extensão da saudação (por exemplo, TrustFrameworkExtensions.xml) e localize Olá `<UserJourneys>` elemento. Se o elemento de saudação não existir, adicione um.
4.  Cole a todo o conteúdo de saudação `<UserJournesy>` nó que você copiou como um filho do hello `<UserJourneys>` elemento.

### <a name="display-hello-button"></a>Botão de saudação de exibição
Olá `<ClaimsProviderSelections>` elemento define a lista de saudação das opções de seleção de provedor de declarações e sua ordem.  `<ClaimsProviderSelection>`elemento é análogo tooan botão de provedor de identidade em uma página de entrada-o/entrar. Se você adicionar um `<ClaimsProviderSelection>` elemento para a conta da Microsoft, um novo botão aparece quando um usuário chega na página de saudação. tooadd este elemento:

1.  Localize Olá `<UserJourney>` nó inclui `Id="SignUpOrSignIn"` em jornada saudação do usuário que você copiou.
2.  Localizar Olá `<OrchestrationStep>` nó inclui`Order="1"`
3.  Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Ação de link de saudação botão tooan
Agora que você tem um botão em vigor, é necessário toolink-tooan ação. ação Hello, nesse caso, é para o Azure AD B2C toocommunicate com Account Microsoft tooreceive um token. Ação do botão tooan de saudação do link vinculando perfil técnico Olá para o seu provedor de declarações de Account da Microsoft:

1.  Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.
2.  Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * Certifique-se de saudação `Id` tem Olá mesmo valor de `TargetClaimsExchangeId` em Olá anterior seção
>   * Certifique-se de `TechnicalProfileReferenceId` ID está definida toohello perfil técnico que você criou anteriormente (MSA-OIDC).

## <a name="upload-hello-policy-tooyour-tenant"></a>Carregar o locatário de tooyour política Olá
1.  Em Olá [portal do Azure](https://portal.azure.com), alternar para Olá [contexto do seu locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)e abra hello **do Azure AD B2C** folha.
2.  Selecione **Estrutura de Experiência de Identidade**.
3.  Olá abrir **todas as políticas** folha.
4.  Selecione **Carregar Política**.
5.  Verificar **substituir a política de saudação se ela existe** caixa.
6.  **Carregar** TrustFrameworkExtensions.xml e certifique-se de que ele não falha na validação de saudação

## <a name="test-hello-custom-policy-by-using-run-now"></a>Testar a política personalizada do hello usando Executar agora

1.  Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.
> [!NOTE]
>
>**Executar agora** requer pelo menos um aplicativo toobe pré-registrado no locatário hello. toolearn como tooregister aplicativos, consulte hello Azure AD B2C [começar](active-directory-b2c-get-started.md) artigo ou hello [registro do aplicativo](active-directory-b2c-app-registration.md) artigo.
2.  Abra **B2C_1A_signup_signin**, Olá política personalizada do terceira parte confiável (RP) que você carregou. Selecione **Executar Agora**.
3.  Você deve ser capaz de toosign usando a conta da Microsoft.

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a>[Opcional] Registrar a jornada do hello Microsoft Account declarações provedor tooProfile Editar usuário
Você pode querer provedor de identidade tooadd Olá Account da Microsoft também tooyour usuário `ProfileEdit` jornada de usuário. toomake disponível, podemos Repita Olá último duas etapas:

### <a name="display-hello-button"></a>Botão de saudação de exibição
1.  Abra o arquivo de extensão de saudação da política (por exemplo, TrustFrameworkExtensions.xml).
2.  Localize Olá `<UserJourney>` nó inclui `Id="ProfileEdit"` em jornada saudação do usuário que você copiou.
3.  Localizar Olá `<OrchestrationStep>` nó inclui`Order="1"`
4.  Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Ação de link de saudação botão tooan
1.  Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.
2.  Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Testar a política personalizada de perfil Editar hello usando Executar agora
1.  Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.
2.  Abra **B2C_1A_ProfileEdit**, Olá política personalizada do terceira parte confiável (RP) que você carregou. Selecione **Executar Agora**.
3.  Você deve ser capaz de toosign usando a conta da Microsoft.

## <a name="download-hello-complete-policy-files"></a>Baixar arquivos de política completa Olá
Opcional: É recomendável que criar o seu cenário usando seus próprios arquivos de política personalizada após a conclusão Olá guia de Introdução com as políticas personalizadas percorrer em vez de usar esses arquivos de exemplo.  [Arquivos de política de exemplo para referência](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
