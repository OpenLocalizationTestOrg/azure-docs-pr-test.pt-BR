---
title: Adquirindo um token usando um aplicativo iOS - Azure AD B2C | Microsoft Docs
description: "Este artigo mostra como toocreate um aplicativo iOS que usa AppAuth com identidades de usuário do Azure Active Directory B2C toomanage e autenticar usuários."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a>Azure AD B2C: entrar usando um aplicativo iOS

plataforma de identidade do Microsoft Hello usa padrões abertos como OAuth2 e OpenID Connect. Usar um protocolo padrão aberto oferece mais opções de desenvolvedor, ao selecionar um toointegrate de biblioteca com os nossos serviços. Fornecemos este passo a passo e outros como ele tooaid desenvolvedores a gravar aplicativos que se conectam a plataforma do Microsoft Identity toohello. A maioria das bibliotecas que implementam [especificação Olá RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) são capazes de tooconnect toohello Microsoft Identity plataforma.

> [!WARNING]
> A Microsoft não fornece correções para bibliotecas de terceiros e não as analisou. Este exemplo está usando uma biblioteca de terceiros chamada AppAuth foi testada para compatibilidade em cenários básicos com hello Azure AD B2C. Problemas e solicitações de recursos devem ser o projeto de código-fonte aberto da biblioteca toohello direcionado. Para obter mais informações, consulte [este artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).
>
>

Se você for novo tooOAuth2 ou OpenID Connect, muito dessa configuração de exemplo pode não ter tooyou muito sentido. Recomendamos que você examinar um breve [visão geral do protocolo de saudação já tenha sido documentadas aqui](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Obter um diretório AD B2C do Azure
Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário. Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos e muito mais. Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir.

## <a name="create-an-application"></a>Criar um aplicativo
Em seguida, você precisa toocreate um aplicativo no seu diretório do B2C. o registro do aplicativo Hello fornece informações do AD do Azure que precisa toocommunicate com segurança com seu aplicativo. toocreate um aplicativo móvel, siga [estas instruções](active-directory-b2c-app-registration.md). É necessário que você:

* Incluir um **Native client** no aplicativo hello.
* Saudação de cópia **ID do aplicativo** que é atribuído tooyour aplicativo. Você precisará desse GUID posteriormente.
* Configure um **URI de redirecionamento** com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Você precisará desse URI posteriormente.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Criar suas políticas
No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md). Esse aplicativo contém uma experiência de identidade: uma combinação de entrada e inscrição. Crie essa política conforme descrito no [artigo de referência da política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Ao criar política hello, certifique-se para:

* Em **inscrição atributos**, selecione o atributo de saudação **nome de exibição**.  É possível selecionar outros atributos também.
* Em **declarações de aplicativo**, selecione Olá declarações **nome de exibição** e **ID de objeto do usuário**. É possível selecionar outras declarações também.
* Saudação de cópia **nome** de cada política depois de criá-lo. O nome da política é prefixado com `b2c_1_` quando você salvar a política Olá.  É necessário o nome da política hello mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Depois que você criou as políticas, você está pronto toobuild seu aplicativo.

## <a name="download-hello-sample-code"></a>Baixar o código de exemplo hello
Nós fornecemos um exemplo funcional que usa o AppAuth com o Azure AD B2C [no GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Você pode baixar o código de saudação e executá-lo. toouse seus próprios B2C do AD do Azure locatário, siga as instruções de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).

Este exemplo foi criado, seguindo as instruções do Leiame Olá Olá [iOS AppAuth projeto no GitHub](https://github.com/openid/AppAuth-iOS). Para obter mais detalhes sobre como exemplo hello e biblioteca Olá funcionam, referência Olá AppAuth README no GitHub.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Modificando o toouse de aplicativo do Azure AD B2C com AppAuth

> [!NOTE]
> O AppAuth dá suporte a iOS 7 e versões superiores.  No entanto, é necessário logons de social toosupport no Google, SFSafariViewController que requer iOS 9 ou superior.
>

### <a name="configuration"></a>Configuração

Você pode configurar a comunicação com o Azure AD B2C especificando o ponto de extremidade de autorização hello e URIs de ponto de extremidade token.  toogenerate esses URIs, você precisa Olá informações a seguir:
* ID do locatário (por exemplo, contoso.onmicrosoft.com)
* Nome da política (por exemplo, B2C\_1\_SignUpIn)

ponto de extremidade token URI pode ser gerado, substituindo Olá Olá locatário\_ID e hello política\_nome no hello URL a seguir:

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

ponto de extremidade de autorização URI pode ser gerado, substituindo Olá Olá locatário\_ID e hello política\_nome no hello URL a seguir:

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

Execute seu objeto AuthorizationServiceConfiguration de saudação toocreate de código a seguir:

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a>Autorizando

Depois de configurar ou recuperar uma configuração de serviço de autorização, uma solicitação de autorização pode ser criada. Olá toocreate solicitar, você precisa Olá informações a seguir:  
* ID do cliente (por exemplo, 00000000-0000-0000-0000-000000000000)
* URI de redirecionamento com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)

Os dois itens devem ter sido salvos quando você estava [registrando seu aplicativo](#create-an-application).

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

tooset o seu aplicativo toohandle Olá redirecionamento toohello URI com esquema personalizado Olá, é necessário tooupdate lista de saudação do 'Esquemas de URL' no seu Info. plist:
* Abra Info.pList.
* Passe o mouse sobre uma linha como 'Código de tipo de sistema operacional do pacote' e clique em Olá \+ símbolo.
* Renomear Olá nova linha 'URL tipos'.
* Clique em Olá seta toohello esquerda da árvore de saudação tooopen 'Tipos de URL'.
* Clique em Olá seta toohello esquerda da árvore de saudação tooopen 'Item 0'.
* Renomeie o primeiro item sob Item too'URL 0 esquemas.
* Clique em Olá seta toohello esquerda da árvore de saudação tooopen 'Esquemas de URL'.
* Na coluna de 'Value' hello, há esquerda de toohello um campo em branco do 'Item 0' abaixo 'Esquemas de URL'.  Defina o esquema exclusivo do aplicativo do hello valor tooyour.  valor de saudação deve corresponder esquema Olá usada no redirectURL ao criar objeto de OIDAuthorizationRequest hello.  Em nosso exemplo, usamos o esquema de saudação 'com.onmicrosoft.fabrikamb2c.exampleapp'.

Consulte toohello [AppAuth guia](https://openid.github.io/AppAuth-iOS/) em como toocomplete Olá restante do processo de saudação. Se você precisar tooquickly começar com um aplicativo de trabalho, check-out [nosso exemplo](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Siga as etapas de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter sua configuração do Azure AD B2C.

Estamos sempre abrir toofeedback e sugestões! Se você tiver dificuldade com este tópico ou ter recomendações para melhorar este conteúdo, Apreciamos seus comentários na parte inferior da saudação da página de saudação. Para solicitações de recurso, adicioná-los muito[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
