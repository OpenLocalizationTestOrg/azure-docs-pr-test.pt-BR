---
title: aaaIntegrate AD do Azure em um aplicativo do iOS | Microsoft Docs
description: Como toobuild um aplicativo iOS que se integra ao AD do Azure para entrar e chamadas de AD do Azure APIs protegidas usando OAuth.
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a>Integrar o Azure AD em um aplicativo iOS
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Experimentar a visualização de saudação do nosso novo [portal do desenvolvedor](https://identity.microsoft.com/Docs/iOS) que ajuda a colocar em funcionamento com o Azure Active Directory em apenas alguns minutos!  portal do desenvolvedor Olá o guiará pelo processo de saudação do registro de um aplicativo e a integração do AD do Azure em seu código.  Quando terminar, você terá um aplicativo simples que pode autenticar os usuários em seu locatário e um back-end que pode aceitar tokens e executar a validação. 
> 
> 

Azure Active Directory (AD do Azure) fornece Olá biblioteca de autenticação do Active Directory ou ADAL, para os clientes do iOS que precisam tooaccess protegido recursos. ADAL simplifica o processo de saudação que seu aplicativo usa tooobtain tokens de acesso. toodemonstrate fácil é, este artigo é criar um aplicativo de lista de tarefas do objetivo C que:

* Obtém acesso tokens para chamar a API do Azure AD Graph Olá usando Olá [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Pesquisa um diretório para usuários com um determinado alias.

aplicativo de trabalho concluída hello de toobuild, você precisa:

1. Registrar seu aplicativo no Azure AD.
2. Instalar e configurar a ADAL.
3. Use ADAL tooget tokens do AD do Azure.

tooget iniciado, [baixar o esqueleto do aplicativo hello](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) ou [baixar exemplo hello concluída](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip). Você também precisará de um locatário do Azure AD no qual possa criar usuários e registrar um aplicativo. Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).


> [!TIP]
> Experimentar a visualização de saudação do nosso novo [portal do desenvolvedor](https://identity.microsoft.com/Docs/iOS) que ajuda a colocar em funcionamento com o Azure AD em apenas alguns minutos. portal do desenvolvedor Olá o guiará pelo processo de saudação do registro de um aplicativo e a integração do AD do Azure em seu código. Quando terminar, você terá um aplicativo simples que pode autenticar os usuários em seu locatário e um back-end que pode aceitar tokens e executar a validação. 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a>1. Determine qual é seu URI de redirecionamento para iOS
toosecurely iniciar seus aplicativos em determinados cenários SSO, você deve criar um *URI de redirecionamento* em um formato específico. Um redirecionamento de URI é usado tooensure que Olá tokens retorno toohello aplicativo correto que solicitado para eles.


Olá iOS formato um redirecionamento de URI é:

```
<app-scheme>://<bundle-id>
```

* **app-scheme** – isso é registrado no projeto XCode. É como os outros aplicativos podem chamar você. Você pode encontrar isso em Info.plist -> tipos de URL -> identificador de URL. Você deve criar um se você ainda não tiver um ou mais configurados.
* **id do pacote** -isso é hello identificador de pacote encontrado em "identity" cancelar suas configurações de projeto no XCode.

Um exemplo para este código de Início Rápido é: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***

## <a name="2-register-hello-directorysearcher-application"></a>2. Registrar o aplicativo de DirectorySearcher hello
tooset backup de seus tokens de tooget do aplicativo, primeiro é necessário tooregistê-lo no AD do Azure locatário e conceda a ela Olá tooaccess de permissão do Azure AD Graph API:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior do hello, clique em sua conta. Em Olá **diretório** , escolha o locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.
3. Clique em **mais serviços** Olá painel de navegação esquerda e, em seguida, selecione **Active Directory do Azure**.
4. Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.
5. Siga Olá solicita toocreate um novo **aplicativo cliente nativo**.
  * Olá **nome** da saudação aplicativo descreve os usuários de tooend do aplicativo.
  * Olá **Uri de redirecionamento** é uma combinação de esquema e a cadeia de caracteres que o AD do Azure usa tooreturn respostas de token.  Insira um valor que é tooyour específico de aplicativo e se baseia em informações de URI de redirecionamento anteriores hello.
6. Depois de concluir o registro de hello, Azure AD atribui seu aplicativo a uma ID exclusiva do aplicativo.  Você precisará desse valor nas seções de Avançar hello, portanto copiá-lo do guia do aplicativo hello.
7. De saudação **configurações** página, selecione **permissões necessárias** e, em seguida, selecione **adicionar**. Selecione **Microsoft Graph** como Olá API e, em seguida, adicione Olá **ler dados do diretório** permissão em **permissões delegadas**.  Isso configura a saudação de tooquery seu aplicativo do Azure AD Graph API para os usuários.

## <a name="3-install-and-configure-adal"></a>3. Instalar e configurar a ADAL
Agora que você tem um aplicativo no AD do Azure, você pode instalar a ADAL e escrever seu código relacionado à identidade.  Para obter toocommunicate ADAL com o AD do Azure, você precisa tooprovide-lo com algumas informações sobre o registro do seu aplicativo.

1. Comece adicionando toohello ADAL DirectorySearcher projeto usando CocoaPods.

    ```
    $ vi Podfile
    ```
2. Adicione Olá toothis podfile a seguir:

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. Carregar agora Olá podfile usando CocoaPods. Esta etapa cria um novo espaço de trabalho do XCode que você carrega.

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. No projeto de início rápido do hello, abrir o arquivo de plist Olá `settings.plist`.  Substitua valores de saudação de elementos Olá Olá seção tooreflect Olá os valores que você inseriu na Olá portal do Azure. Seu código faz referência a esses valores sempre que ele usar a ADAL.
  * Olá `tenant` é o domínio de saudação do seu locatário do AD do Azure, por exemplo, contoso.onmicrosoft.com.
  * Olá `clientId` é Olá ID do cliente do aplicativo que você copiou do portal de saudação.
  * Olá `redirectUri` é a URL de redirecionamento de saudação registrado no portal de saudação.

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a>4.    Usar o ADAL tooget tokens do AD do Azure
Olá princípio básico de ADAL é que sempre que seu aplicativo precisa de um token de acesso, ele simplesmente chama um completionBlock `+(void) getToken : `, e ADAL Olá rest.  

1. Em Olá `QuickStart` projeto, abra `GraphAPICaller.m` e localize Olá `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comentário superior hello.  Isso é onde você pode passa Olá ADAL coordenadas por meio de um CompletionBlock, toocommunicate com o AD do Azure e informe como toocache tokens.

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. Agora precisamos toouse toosearch esse token para usuários no gráfico de saudação. Localize Olá `// TODO: implement SearchUsersList` comentário. Esse método torna um tooquery de toohello do Azure AD Graph API de solicitação GET para usuários cujo UPN começa com hello dado o termo de pesquisa.  tooquery hello Azure AD Graph API, você precisa tooinclude um access_token no hello `Authorization` cabeçalho de solicitação de saudação. É aí que a ADAL entra em cena.

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

                             [Users addObject:s];
                         }

                         completionBlock(Users, nil);
                     }
                     else
                     {
                         completionBlock(nil, error);
                     }

                }];
             }
         }];

    }

    ```


3. Quando o aplicativo solicita um token chamando `getToken(...)`, ADAL tentativas tooreturn um token sem solicitar credenciais de usuário hello.  Se ADAL determina que o usuário Olá precisa toosign em tooget um token, ele será exibir uma caixa de diálogo para entrar, coletar credenciais de saudação do usuário e, em seguida, retorna um token após a autenticação bem-sucedida.  Se a ADAL não é capaz de tooreturn um token por qualquer motivo, ele gerará um `AdalException`.

> [!Note] 
> Olá `AuthenticationResult` objeto contém um `tokenCacheStoreItem` objeto que pode ser usado toocollect Olá informações que seu aplicativo pode precisar. Em Olá QuickStart, `tokenCacheStoreItem` é toodetermine usado se a autenticação já foi concluída.
>
>

## <a name="5-build-and-run-hello-application"></a>5. Compilar e executar o aplicativo hello
Parabéns! Agora você tem um aplicativo do iOS funcional que pode autenticar os usuários, com segurança chamar APIs da Web usando o OAuth 2.0 e obter informações básicas sobre o usuário hello.  Se você ainda não fez isso, agora é Olá tempo toopopulate seu locatário com alguns usuários.  Inicie o aplicativo do Guia de início rápido e entre com um desses usuários.  Procure por outros usuários com base em seus UPNs.  Feche o aplicativo hello e, em seguida, inicie-o novamente.  Observe que a sessão do usuário Olá permanece intacta.

ADAL torna fácil tooincorporate todos esses recursos comuns de identidade em seu aplicativo.  Cuida de todo o trabalho sujo Olá para você, como gerenciamento de cache, suporte de protocolo OAuth, apresentar Olá usuário toosign uma interface do usuário no e atualizar tokens expirados.  Tudo o que você realmente precisa de tooknow é uma única chamada de API, `getToken`.

Para referência, o exemplo hello concluída (sem os valores de configuração) é fornecido em [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).  

## <a name="next-steps"></a>Próximas etapas
Agora você pode mover tooadditional cenários.  Você pode desejar tootry:

* [Proteger uma API Web Node.js com o Azure AD](active-directory-devquickstarts-webapi-nodejs.md)
* Saiba [como tooenable SSO entre aplicativos no iOS usando o ADAL](active-directory-sso-ios.md)  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

