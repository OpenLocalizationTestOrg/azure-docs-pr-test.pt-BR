---
title: 'Azure Active Directory B2C: Como adquirir um token usando um aplicativo do Android | Microsoft Docs'
description: "Este artigo mostra como toocreate um aplicativo do Android que usa AppAuth com identidades de usuário do Azure Active Directory B2C toomanage e autenticar usuários."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a>Azure AD B2C: entrar usando um aplicativo Android

plataforma de identidade do Microsoft Hello usa padrões abertos como OAuth2 e OpenID Connect. Isso permite que desenvolvedores tooleverage qualquer biblioteca desejarem toointegrate com nossos serviços. os desenvolvedores de tooaid usando nossa plataforma com outras bibliotecas, escrevemos algumas instruções passo a passo como esse um toodemonstrate como tooconfigure 3ª parte bibliotecas tooconnect toohello Microsoft plataforma de identidade. A maioria das bibliotecas que implementam [especificação Olá RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) será capaz de tooconnect toohello Microsoft Identity plataforma.

> [!WARNING]
> A Microsoft não fornece correções nem análises para bibliotecas de terceiros. Este exemplo está usando uma biblioteca de terceiros 3º chamada AppAuth foi testada para compatibilidade em cenários básicos com hello Azure AD B2C. Problemas e solicitações de recursos devem ser o projeto de código-fonte aberto da biblioteca toohello direcionado. Para saber mais, confira [este artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).  
>
>

Se você for novo tooOAuth2 ou OpenID Connect muito nesta configuração de exemplo pode não ter tooyou muito sentido. Recomendamos que você examinar um breve [visão geral do protocolo de saudação já tenha sido documentadas aqui](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Obter um diretório AD B2C do Azure

Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário. Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos etc. Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir.

## <a name="create-an-application"></a>Criar um aplicativo

Em seguida, você precisa toocreate um aplicativo no seu diretório do B2C. Isso fornece informações do AD do Azure que precisa toocommunicate com segurança com seu aplicativo. toocreate um aplicativo móvel, siga [estas instruções](active-directory-b2c-app-registration.md). É necessário que você:

* Incluir um **Native Client** no aplicativo hello.
* Saudação de cópia **ID do aplicativo** que é atribuído tooyour aplicativo. Você precisará dessas informações posteriormente.
* Configure um **URI de redirecionamento** de cliente nativo (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Você também precisará dela mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Criar suas políticas

No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md). Esse aplicativo contém uma experiência de identidade: uma combinação de entrada e inscrição. Você precisa toocreate essa política, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Ao criar política hello, certifique-se para:

* Escolha Olá **nome de exibição** como um atributo de inscrição em sua política.
* Escolha Olá **nome de exibição** e **ID de objeto** declarações de aplicativo em cada política. Você pode escolher outras declarações também.
* Saudação de cópia **nome** de cada política depois de criá-lo. Ele deve ter o prefixo Olá `b2c_1_`.  Você precisará nome da política hello mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Depois que você criou as políticas, você está pronto toobuild seu aplicativo.

## <a name="download-hello-sample-code"></a>Baixar o código de exemplo hello

Nós fornecemos um exemplo funcional que usa o AppAuth com o Azure AD B2C [no GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Você pode baixar o código de saudação e executá-lo. Você pode começar rapidamente com seu próprio aplicativo usando sua própria configuração do Azure AD B2C seguindo instruções Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).

exemplo Hello é uma modificação do exemplo hello fornecido pelo [AppAuth](https://openid.github.io/AppAuth-Android/). Visite sua toolearn página mais sobre AppAuth e seus recursos.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Modificando o toouse de aplicativo do Azure AD B2C com AppAuth

> [!NOTE]
> O AppAuth oferece suporte à API Android 16 (Jellybean) e versões superiores. Recomendamos usar a API 23 ou superior.
>

### <a name="configuration"></a>Configuração

Você pode configurar a comunicação com o Azure AD B2C descobrir Olá especificando URI ou especificando o ponto de extremidade de autorização hello e URIs de ponto de extremidade token. Em ambos os casos, você precisará Olá informações a seguir:

* ID do locatário (por exemplo, contoso.onmicrosoft.com)
* Nome da política (por exemplo, B2C\_1\_SignUpIn)

Se você escolher tooautomatically descobrir Olá autorização e token de ponto de extremidade URIs, você precisará toofetch informações de descoberta de saudação URI. descoberta de saudação URI pode ser gerado, substituindo Olá locatário\_ID e hello política\_nome no hello URL a seguir:

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

Você pode adquirir autorização hello e URIs de ponto de extremidade token e criar um objeto AuthorizationServiceConfiguration executando Olá seguinte:

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

Em vez de usar autorização de saudação do tooobtain de descoberta e o ponto de extremidade token URIs, você também pode especificá-los explicitamente, substituindo Olá locatário\_ID e hello política\_nome na URL de saudação abaixo:

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

Execute seu objeto AuthorizationServiceConfiguration de saudação toocreate de código a seguir:

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a>Autorizando

Depois de configurar ou recuperar uma configuração de serviço de autorização, uma solicitação de autorização pode ser criada. Olá toocreate solicitar, você precisará Olá informações a seguir:

* ID do cliente (por exemplo, 00000000-0000-0000-0000-000000000000)
* URI de redirecionamento com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)

Os dois itens devem ter sido salvos quando você estava [registrando seu aplicativo](#create-an-application).

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

Consulte toohello [AppAuth guia](https://openid.github.io/AppAuth-Android/) em como toocomplete Olá restante do processo de saudação. Se você precisar tooquickly começar com um aplicativo de trabalho, check-out [nosso exemplo](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Siga as etapas de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter sua configuração do Azure AD B2C.

Estamos sempre abrir toofeedback e sugestões! Se você tiver dificuldade com este tópico ou ter recomendações para melhorar este conteúdo, Apreciamos seus comentários na parte inferior da saudação da página de saudação. Para solicitações de recurso, adicioná-los muito[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

