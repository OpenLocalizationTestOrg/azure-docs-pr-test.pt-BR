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
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a>Azure Active Directory B2C: entrar usando contas do Azure AD

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Este artigo mostra como tooenable entrar para usuários de uma organização específica do Azure Active Directory (AD do Azure) através do uso de saudação do [políticas personalizadas](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Pré-requisitos

Olá concluir as etapas em Olá [guia de Introdução com políticas personalizadas](active-directory-b2c-get-started-custom.md) artigo.

As etapas incluem:

1. Criar um locatário do Azure Active Directory B2C (Azure AD B2C).
2. Criar um aplicativo Azure AD B2C.
3. Registrar dois aplicativos do mecanismo de políticas.
4. Configurar chaves.
5. Configurar o pacote de inicializador de saudação.

## <a name="create-an-azure-ad-app"></a>Criar um aplicativo Azure AD

tooenable entrar para usuários de uma determinada organização do AD do Azure, você precisa tooregister um aplicativo no locatário Olá organizacional do AD do Azure.

>[!NOTE]
> Podemos usar "contoso.com" para locatário Olá organizacional do AD do Azure e "fabrikamb2c.onmicrosoft.com" como locatário hello Azure AD B2C em Olá instruções a seguir.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
1. Na barra superior do hello, selecione sua conta. De saudação **diretório** , escolha locatário Olá organizacional do AD do Azure onde deseja tooregister seu aplicativo (contoso.com).
1. Selecione **mais serviços** no painel esquerdo do hello e procure "Registros de aplicativo".
1. Selecione **Novo registro de aplicativo**.
1. Insira um nome para seu aplicativo (por exemplo, `Azure AD B2C App`).
1. Selecione **aplicativo Web / API** para o tipo de aplicativo hello.
1. Para **URL de logon**, digite Olá seguindo a URL, onde `yourtenant` é substituído pelo nome de saudação do seu locatário do Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. Salvar o ID do aplicativo hello.
1. Selecione o aplicativo hello recém-criado.
1. Em Olá **configurações** folha, selecione **chaves**.
1. Crie uma nova chave e salve-a. Você o usará em etapas Olá Olá próxima seção.

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a>Adicionar tooAzure de chave de saudação do AD do Azure AD B2C

É necessário a chave de aplicativo toostore Olá contoso.com em seu locatário do Azure AD B2C. toodo isso:
1. Go locatário tooyour B2C do Azure AD e selecione **B2C configurações** > **identidade experiência Framework** > **chaves política**.
1. Selecione **+Adicionar**.
1. Selecione ou insira estas opções:
   * Selecione **Manual**.
   * Para o **Nome**, escolha um nome que corresponda ao nome do locatário do Azure AD (por exemplo, `ContosoAppSecret`).  prefixo de saudação `B2C_1A_` é adicionado automaticamente toohello nome da chave.
   * Cole a chave de aplicativo hello **segredo** caixa.
   * Selecione **Assinatura**.
1. Selecione **Criar**.
1. Confirme que você criou a chave Olá `B2C_1A_ContosoAppSecret`.


## <a name="add-a-claims-provider-in-your-base-policy"></a>Adicionar um provedor de declarações à política base

Se você quiser usuários toosign no usando o AD do Azure, você precisa toodefine AD do Azure como um provedor de declarações. Em outras palavras, você precisa toospecify um ponto de extremidade do Azure AD B2C se comunicará. ponto de extremidade Olá fornecem um conjunto de declarações que são usados pelo Azure AD B2C tooverify que um usuário específico autenticado. 

Você pode definir o AD do Azure como um provedor de declarações adicionando toohello do AD do Azure `<ClaimsProvider>` nó no arquivo de extensão de saudação da política:

1. Abra o arquivo de extensão da saudação (TrustFrameworkExtensions.xml) do seu diretório de trabalho.
1. Localize Olá `<ClaimsProviders>` seção. Se não existir, adicione-o nó raiz de saudação.
1. Adicione um novo nó `<ClaimsProvider>` da seguinte maneira:

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

1. Em Olá `<ClaimsProvider>` nó, o valor de saudação de atualização para `<Domain>` tooa valor exclusivo que pode ser usado toodistinguish-lo de outros provedores de identidade.
1. Em Olá `<ClaimsProvider>` nó, o valor de saudação de atualização para `<DisplayName>` tooa nome amigável do hello provedor de declarações. Esse valor não é usado atualmente.

### <a name="update-hello-technical-profile"></a>Atualizar perfil técnica Olá

tooget um token do ponto de extremidade do hello AD do Azure, você precisa de protocolos de saudação toodefine que o Azure AD B2C deve usar toocommunicate com o Azure AD. Isso é feito dentro Olá `<TechnicalProfile>` elemento `<ClaimsProvider>`.
1. Atualizar a ID de saudação do hello `<TechnicalProfile>` nó. Essa ID é usada toorefer toothis perfil técnico de outras partes da política de saudação.
1. Atualizar o valor Olá para `<DisplayName>`. Esse valor será exibido no botão logon Olá em sua tela de entrada.
1. Atualizar o valor Olá para `<Description>`.
1. AD do Azure usa o protocolo de saudação OpenID Connect, para garantir que esse valor Olá para `<Protocol>` é `"OpenIdConnect"`.

Você precisa Olá tooupdate `<Metadata>` seção no arquivo XML de saudação chamado definições de configuração do tooearlier tooreflect Olá para o determinado locatário do AD do Azure. No arquivo XML de hello, atualize valores de metadados de saudação da seguinte maneira:

1. Definir `<Item Key="METADATA">` muito`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, onde `yourAzureADtenant` é o nome do locatário do AD do Azure (contoso.com).
1. Abra seu navegador e acesse toohello `METADATA` URL que você acabou de ser atualizado.
1. No navegador hello, procure o objeto de 'emissor' hello e copie seu valor. Deve se parecer com o seguinte Olá: `https://sts.windows.net/{tenantId}/`.
1. Cole o valor de saudação para `<Item Key="ProviderName">` no arquivo XML de saudação.
1. Definir `<Item Key="client_id">` toohello ID do aplicativo de registro do aplicativo hello.
1. Definir `<Item Key="IdTokenAudience">` toohello ID do aplicativo de registro do aplicativo hello.
1. Certifique-se de que `<Item Key="response_types">` está definido muito`id_token`.
1. Certifique-se de que `<Item Key="UsePolicyInRedirectUri">` está definido muito`false`.

Você também precisa toolink segredo de saudação do AD do Azure que você registrou no seu toohello de locatário do Azure AD B2C do Azure AD `<ClaimsProvider>` informações:

* Em Olá `<CryptographicKeys>` seção Olá precede o arquivo XML, atualize o valor Olá para `StorageReferenceId` toohello ID de referência de segredo Olá definido (por exemplo, `ContosoAppSecret`).

### <a name="upload-hello-extension-file-for-verification"></a>Carregue o arquivo de extensão de saudação para verificação

Agora, você configurou sua política de modo que o Azure AD B2C Saiba como toocommunicate com seu diretório do AD do Azure. Tente carregar o arquivo de extensão de saudação do seu tooconfirm apenas de política que ele não tem quaisquer problemas até o momento. toodo para:

1. Olá abrir **todas as políticas** folha em seu locatário do Azure AD B2C.
1. Verificar Olá **substituir a política de saudação se ela existe** caixa.
1. Carregar arquivo de extensão da saudação (TrustFrameworkExtensions.xml) e certifique-se de que ele não falha na validação de saudação.

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a>Registrar a jornada de usuário tooa do provedor de declarações de AD do Azure Olá

Agora, você precisa tooadd Olá AD do Azure identidade provedor tooone de jornadas seu usuário. Neste ponto, o provedor de identidade Olá foi configurado, mas não está disponível em qualquer uma das telas de entrada-o/entrada hello. toomake-las disponíveis, criaremos uma duplicata de uma jornada de usuário do modelo existente e, em seguida, modificá-lo para que ele também tem o provedor de identidade de saudação do AD do Azure:

1. Abra o arquivo de base de saudação da política (por exemplo, TrustFrameworkBase.xml).
1. Localize Olá `<UserJourneys>` Olá de elemento e copie todo `<UserJourney>` nó inclui `Id="SignUpOrSignIn"`.
1. Abra o arquivo de extensão da saudação (por exemplo, TrustFrameworkExtensions.xml) e localize Olá `<UserJourneys>` elemento. Se o elemento de saudação não existir, adicione um.
1. Saudação de colar toda `<UserJourney>` nó que você copiou como um filho do hello `<UserJourneys>` elemento.
1. Renomear a ID de saudação do jornada de usuário nova hello (por exemplo, renomear como `SignUpOrSignUsingContoso`).

### <a name="display-hello-button"></a>Saudação de exibição "button"

Olá `<ClaimsProviderSelection>` elemento é análogo tooan botão de provedor de identidade em uma tela de entrada-o/entrar. Se você adicionar um `<ClaimsProviderSelection>` elemento do AD do Azure, um novo botão aparece quando um usuário chega na página de saudação. tooadd este elemento:

1. Localize Olá `<OrchestrationStep>` nó inclui `Order="1"` em jornada saudação do usuário que você acabou de criar.
1. Adicione Olá seguinte:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. Definir `TargetClaimsExchangeId` valor apropriado tooan. É recomendável seguir Olá a mesma convenção de outras pessoas:  *\[ClaimProviderName\]Exchange*.

### <a name="link-hello-button-tooan-action"></a>Ação de link de saudação botão tooan

Agora que você tem um botão em vigor, é necessário toolink-tooan ação. ação Hello, nesse caso, é para o Azure AD B2C toocommunicate com AD do Azure tooreceive um token. Ação de link Olá botão tooan vinculando perfil técnico Olá para o seu provedor de declarações do AD do Azure:

1. Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.
1. Adicione Olá seguinte:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. Atualização `Id` toohello mesmo valor de `TargetClaimsExchangeId` em Olá anterior seção.
1. Atualização `TechnicalProfileReferenceId` toohello ID da saudação técnica perfil que você criou anteriormente (ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Carregar arquivo de extensão atualizada Olá

Você concluiu a modificar arquivo de extensão de saudação. Salve-o. Em seguida, carregar o arquivo hello e certifique-se de que todas as validações de êxito.

### <a name="update-hello-rp-file"></a>Atualizar o arquivo do RP Olá

Você agora precisa tooupdate Olá terceira parte confiável (RP) arquivo irá iniciar a jornada saudação do usuário que você acabou de criar:

1. Faça uma cópia do SignUpOrSignIn.xml no diretório de trabalho e renomeá-lo (por exemplo, renomeá-lo de tooSignUpOrSignInWithAAD.xml).
1. Olá novo Olá abrir arquivo e atualização `PolicyId` atributo `<TrustFrameworkPolicy>` com um valor exclusivo (por exemplo, SignUpOrSignInWithAAD). <br> Esse será o nome hello da política (por exemplo, B2C\_1A\_SignUpOrSignInWithAAD).
1. Modificar Olá `ReferenceId` atributo `<DefaultUserJourney>` toomatch Olá ID de jornada de usuário nova Olá que você criou (SignUpOrSignUsingContoso).
1. Salve suas alterações e carregar o arquivo hello.

## <a name="troubleshooting"></a>Solucionar problemas

Testar política personalizada do hello carregado abrindo sua folha e clicando em **executar agora**. problemas de toodiagnose, leia sobre [de solução de problemas](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Próximas etapas

Fornecer comentários muito[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
