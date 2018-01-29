---
title: "Azure Active Directory B2C: adicionar o Twitter como um provedor de identidade OAuth1 usando políticas personalizadas"
description: Usar o Twitter como provedor de identidade usando o protocolo OAuth1
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: mtillman
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 10/23/2017
ms.author: yoelh
ms.openlocfilehash: 629e0bbaa7c62ef5d381085588c6a99c203c41cb
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="azure-active-directory-b2c-add-twitter-as-an-oauth1-identity-provider-by-using-custom-policies"></a>Azure Active Directory B2C: adicionar o Twitter como um provedor de identidade OAuth1 usando políticas personalizadas
[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Este artigo mostra como habilitar a entrada para usuários de uma conta do Twitter usando [políticas personalizadas](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Pré-requisitos
Conclua as etapas no artigo [Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md).

## <a name="step-1-create-a-twitter-account-application"></a>Etapa 1: Criar um aplicativo de conta do Twitter
Para usar o Twitter como um provedor de identidade no Azure AD B2C (Azure Active Directory B2C), você deve criar um aplicativo do Twitter e fornecer a ele os parâmetros certos. Você pode registrar um aplicativo do Twitter indo até a [página de inscrição do Twitter](https://twitter.com/signup).

1. Vá até o site de [Desenvolvedores do Twitter](https://apps.twitter.com/), entre com suas credenciais da conta do Twitter e selecione **Criar Novo Aplicativo**.

    ![Conta do Twitter – criar novo aplicativo](media/active-directory-b2c-custom-setup-twitter-idp/adb2c-ief-setup-twitter-idp-new-app1.png)

2. Na janela **Criar um aplicativo**, faça o seguinte:
 
    a. Digite o **Nome** e uma **Descrição** para o novo aplicativo. 

    b. Na caixa **Site**, cole **https://login.microsoftonline.com**. 

    c. Na caixa **URL de Retorno de Chamada**, cole **https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/oauth2/authresp**. Substitua {*tenant*} por seu nome de locatário (por exemplo, contosob2c.onmicrosoft.com). Certifique-se de que você está usando o esquema HTTPS. 

    d. Na parte inferior da página, leia e aceite os termos e, em seguida, selecione **Criar seu aplicativo Twitter**.

    ![Conta do Twitter – adicionar um novo aplicativo](media/active-directory-b2c-custom-setup-twitter-idp/adb2c-ief-setup-twitter-idp-new-app2.png)

3. Na janela **Demonstração do B2C**, selecione **Configurações**, marque a caixa de seleção **Permitir que este aplicativo seja usado para entrar com o Twitter** e selecione **Atualizar Configurações**.

4. Selecione **Chaves e Tokens de Acesso** e observe os valores de **Chave de Consumidor (Chave de API)** e **Segredo do Consumidor (Segredo de API)**.

    ![Conta do Twitter – definir propriedades do aplicativo](media/active-directory-b2c-custom-setup-twitter-idp/adb2c-ief-setup-twitter-idp-new-app3.png)

    >[!NOTE]
    >O segredo do consumidor é uma credencial de segurança importante. Não compartilhe esse segredo com ninguém nem o distribua com seu aplicativo.

## <a name="step-2-add-your-twitter-account-application-key-to-azure-ad-b2c"></a>Etapa 2: Adicionar a chave de aplicativo da conta do Twitter ao Azure AD B2C
A federação com contas do Twitter exige um segredo do consumidor para a conta do Twitter confiar no Azure AD B2C em nome do aplicativo. Para armazenar o segredo do consumidor do aplicativo do Twitter no seu locatário do Azure AD B2C, faça o seguinte: 

1. No seu locatário do Azure AD B2C, selecione **Configurações de B2C** > **Estrutura de Experiência de Identidade**.

2. Para exibir as chaves disponíveis no seu locatário, selecione **Chaves de Política**.

3. Selecione **Adicionar**.

4. Na caixa **Opções**, selecione **Manual**.

5. Na caixa **Nome**, selecione **TwitterSecret**.  
    O prefixo *B2C_1A_* pode ser adicionado automaticamente.

6. Na caixa **Segredo**, insira o segredo de aplicativo da Microsoft do [Portal de Registro de Aplicativo](https://apps.dev.microsoft.com).

7. Para o **Uso da chave**, use **Criptografia**.

8. Selecione **Criar**.

9. Confirme que você criou a chave `B2C_1A_TwitterSecret`.

## <a name="step-3-add-a-claims-provider-in-your-extension-policy"></a>Etapa 3: adicionar um provedor de declarações à sua política de extensão

Se quiser que os usuários entrem usando a conta do Twitter, você precisará definir o Twitter como um provedor de declarações. Em outras palavras, você deve especificar pontos de extremidade com os quais o Azure AD B2C se comunique. Os pontos de extremidade fornecem um conjunto de declarações que são usadas pelo Azure AD B2C para verificar se um usuário específico foi autenticado.

Defina o Twitter como um provedor de declarações adicionando o nó `<ClaimsProvider>` em seu arquivo de política da extensão:

1. No diretório de trabalho, abra o arquivo de política de extensão *TrustFrameworkExtensions.xml*. 

2. Pesquise a seção `<ClaimsProviders>`.

3. No nó `<ClaimsProviders>`, adicione o seguinte trecho de código XML:  

    ```xml
    <ClaimsProvider>
        <Domain>twitter.com</Domain>
        <DisplayName>Twitter</DisplayName>
        <TechnicalProfiles>
        <TechnicalProfile Id="Twitter-OAUTH1">
            <DisplayName>Twitter</DisplayName>
            <Protocol Name="OAuth1" />
            <Metadata>
            <Item Key="ProviderName">Twitter</Item>
            <Item Key="authorization_endpoint">https://api.twitter.com/oauth/authenticate</Item>
            <Item Key="access_token_endpoint">https://api.twitter.com/oauth/access_token</Item>
            <Item Key="request_token_endpoint">https://api.twitter.com/oauth/request_token</Item>
            <Item Key="ClaimsEndpoint">https://api.twitter.com/1.1/account/verify_credentials.json?include_email=true</Item>
            <Item Key="ClaimsResponseFormat">json</Item>
            <Item Key="client_id">Your Twitter application consumer key</Item>
            </Metadata>
            <CryptographicKeys>
            <Key Id="client_secret" StorageReferenceId="B2C_1A_TwitterSecret" />
            </CryptographicKeys>
            <InputClaims />
            <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="user_id" />
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="screen_name" />
            <OutputClaim ClaimTypeReferenceId="email" />
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="twitter.com" />
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
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

4. Substitua o valor *client_id* pela chave do consumidor do aplicativo da conta do Twitter.

5. Salve o arquivo.

## <a name="step-4-register-the-twitter-account-claims-provider-to-your-sign-up-or-sign-in-user-journey"></a>Etapa 4: Registrar o provedor de declarações da conta do Twitter para um percurso do usuário de inscrição ou entrada
Você configurou o provedor de identidade. No entanto, ele ainda não está disponível em nenhuma das janelas de inscrição ou entrada. Agora você deve adicionar o provedor de identidade da conta do Twitter ao percurso de usuário `SignUpOrSignIn` do usuário.

### <a name="step-41-make-a-copy-of-the-user-journey"></a>Etapa 4.1: Fazer uma cópia do percurso do usuário
Para disponibilizar o percurso do usuário, você cria uma duplicata de um modelo de percurso do usuário existente e, em seguida, adiciona o provedor de identidade do Twitter:

>[!NOTE]
>Se você tiver copiado o elemento `<UserJourneys>` do arquivo de base da sua política para o arquivo de extensão *TrustFrameworkExtensions.xml*, poderá ir para a seção seguinte.

1. Abra o arquivo base da política (por exemplo, TrustFrameworkBase.xml).

2. Pesquise o elemento `<UserJourneys>`, selecione todo o conteúdo do nó `<UserJourney>` e selecione **Recortar** para mover o texto selecionado para a área de transferência.

3. Abra o arquivo de extensão (por exemplo, TrustFrameworkExtensions.xml) e, em seguida, pesquise o elemento `<UserJourneys>`. Se o elemento não existir, adicione-o.

4. Cole o conteúdo inteiro do nó `<UserJourney>`, que você moveu para a área de transferência na etapa 2, no elemento `<UserJourneys>`.

### <a name="step-42-display-the-button"></a>Etapa 4.2: Exibir o “botão”
O elemento `<ClaimsProviderSelections>` define a lista de opções de seleção de provedor de declarações e sua ordem. O nó `<ClaimsProviderSelection>` é análogo a um botão de provedor de identidade em uma página de inscrição ou entrada. Se você adicionar um nó `<ClaimsProviderSelection>` à conta do Twitter, um novo botão será exibido quando um usuário chegar à página. Para adicionar esse elemento, faça o seguinte:

1. Pesquise o nó `<UserJourney>` que contém `Id="SignUpOrSignIn"` no percurso do usuário copiado.

2. Localize o nó `<OrchestrationStep>` que contém `Order="1"`.

3. No elemento `<ClaimsProviderSelections>`, adicione o seguinte trecho de código XML:

    ```xml
    <ClaimsProviderSelection TargetClaimsExchangeId="TwitterExchange" />
    ```

### <a name="step-43-link-the-button-to-an-action"></a>Etapa 4.3: Vincular o botão a uma ação
Agora que implementou um botão, você deve vinculá-lo a uma ação. Nesse caso, a ação é para o Azure AD B2C se comunicar com a conta do Twitter para receber um token. Vincule o botão a uma ação vinculando o perfil técnico ao provedor de declarações da conta do Twitter:

1. Pesquise o nó `<OrchestrationStep>` que contém `Order="2"` no nó `<UserJourney>`.
2. No elemento `<ClaimsExchanges>`, adicione o seguinte trecho de código XML:

    ```xml
    <ClaimsExchange Id="TwitterExchange" TechnicalProfileReferenceId="Twitter-OAUTH1" />
    ```

    >[!NOTE]
    >* Certifique-se de que o `Id` tenha o mesmo valor de `TargetClaimsExchangeId` na seção anterior.
    >* Verifique se a ID `TechnicalProfileReferenceId` está definida para o perfil técnico criado anteriormente (Twitter-OAUTH1).

## <a name="step-5-upload-the-policy-to-your-tenant"></a>Etapa 5: Carregar a política para o seu locatário
1. No [Portal do Azure](https://portal.azure.com), mude para o [contexto do locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) e, em seguida, selecione **Azure AD B2C**.

2. Selecione **Estrutura de Experiência de Identidade**.

3. Selecione **Todas as Políticas**.

4. Selecione **Carregar Política**.

5. Marque a caixa de seleção **Substituir a política caso ela exista**.

6. Carregue os arquivos *TrustFrameworkBase.xml* e *TrustFrameworkExtensions.xml* e certifique-se de que eles passem na validação.

## <a name="step-6-test-the-custom-policy-by-using-run-now"></a>Etapa 6: Testar a política personalizada usando Executar Agora

1. Selecione **Configurações do Azure AD B2C** e selecione **Estrutura de Experiência de Identidade**.

    >[!NOTE]
    >Executar Agora exige que pelo menos um aplicativo esteja previamente registrado no locatário. Para saber como registrar aplicativos, confira os artigos [Introdução](active-directory-b2c-get-started.md) ou [Registro do aplicativo](active-directory-b2c-app-registration.md) do Azure AD B2C.

2. Abra **B2C_1A_signup_signin**, a política personalizada da RP (terceira parte confiável) carregada e selecione **Executar agora**.  
    Agora você deve conseguir entrar usando a conta do Twitter.

## <a name="step-7-optional-register-the-twitter-account-claims-provider-to-the-profile-edit-user-journey"></a>Etapa 7: (Opcional) Registrar o provedor de declarações da conta do Twitter para o percurso de usuário de edição de perfil
Você também deve adicionar o provedor de identidade da conta do Twitter ao percurso do usuário `ProfileEdit`. Para disponibilizar o percurso do usuário, repita a “Etapa 4”. Neste momento, selecione o nó `<UserJourney>` que contém `Id="ProfileEdit"`. Salve, carregue e teste sua política.


## <a name="optional-download-the-complete-policy-files"></a>(Opcional) Baixar os arquivos da política completa
Depois de concluir o passo a passo [Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md), recomendamos que você crie o cenário usando seus próprios arquivos de política personalizados. Fornecemos os [Arquivos de política de exemplo](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-twitter-app) como referência.
