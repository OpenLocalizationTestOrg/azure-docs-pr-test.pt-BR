---
title: "aaaAdd tooan entrar iOS aplicativo usando Olá o ponto de extremidade do AD do Azure v 2.0 | Microsoft Docs"
description: "Como toobuild um aplicativo iOS que entra em usuários com ambas as conta pessoal da Microsoft e contas corporativa ou escolar usando bibliotecas de terceiros."
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Adicionar aplicativo do iOS tooan entrar usando uma biblioteca de terceiros com a API do Graph usando o ponto de extremidade do hello v 2.0
plataforma de identidade do Microsoft Hello usa padrões abertos como OAuth2 e OpenID Connect. Os desenvolvedores podem usar qualquer biblioteca quiserem toointegrate com nossos serviços. os desenvolvedores de toohelp usar nossa plataforma com outras bibliotecas, escrevemos algumas instruções passo a passo como esse um toodemonstrate como plataforma de identidade da Microsoft tooconnect toohello tooconfigure bibliotecas de terceiros. A maioria das bibliotecas que implementam [especificação Olá RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) pode se conectar a plataforma de identidade do Microsoft toohello.

Com o aplicativo hello que cria este passo a passo, os usuários podem entrar tootheir organização e, em seguida, procure outras pessoas em sua organização usando Olá API do Graph.

Se você for novo tooOAuth2 ou OpenID Connect, muito dessa configuração de exemplo pode não fazer sentido tooyou. Recomendamos ler o artigo [Protocolos v 2.0 – Fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols-oauth-code.md) para saber mais.

> [!NOTE]
> Alguns recursos de nossa plataforma que têm uma expressão em Olá OAuth2 ou padrões de OpenID Connect, como acesso condicional e gerenciamento de política do Intune, exigem você toouse nosso código-fonte aberto bibliotecas de identidade do Microsoft Azure.
> 
> 

o ponto de extremidade do Hello v 2.0 não oferece suporte a todos os recursos e cenários de Active Directory do Azure.

> [!NOTE]
> toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-code-from-github"></a>Baixar o código do GitHub
código de saudação para este tutorial é mantido [no GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).  toofollow ao longo, você pode [baixar o esqueleto do aplicativo hello como. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou esqueleto de saudação do clone:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

Você também pode baixar o exemplo hello e começar imediatamente:

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a>Registrar um aplicativo
Criar um novo aplicativo no hello [portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou siga Olá etapas detalhadas em [como tooregister um aplicativo com o ponto de extremidade do hello v 2.0](active-directory-v2-app-registration.md).  Não se esqueça de:

* Saudação de cópia **Id do aplicativo** que é atribuído tooyour aplicativo porque você precisará dele em breve.
* Adicionar Olá **Mobile** plataforma para seu aplicativo.
* Saudação de cópia **URI de redirecionamento** do portal de saudação. Você deve usar o valor padrão Olá `urn:ietf:wg:oauth:2.0:oob`.

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a>Baixar Olá terceiros NXOAuth2 biblioteca e criar um espaço de trabalho
Para este passo a passo, você usará Olá OAuth2Client do GitHub, que é uma biblioteca de OAuth2 para Mac OS X e iOS (Cocoa e Cocoa touch). Essa biblioteca baseia-se em 10 de rascunho da especificação de OAuth2 hello. Ele implementa um perfil de aplicativo nativo hello e dá suporte ao ponto de extremidade de autorização de saudação do usuário hello. Essas são todas as coisas Olá toointegrate com a plataforma de identidade Microsoft hello, será necessário.

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a>Adicionar projeto de tooyour biblioteca hello usando CocoaPods
O CocoaPods é um gerenciador de dependência para projetos do Xcode. Gerencia automaticamente as etapas de instalação anterior hello.

```
$ vi Podfile
```
1. Adicione Olá toothis podfile a seguir:
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. Carregar Olá podfile usando CocoaPods. Isso criará um novo espaço de trabalho Xcode que será carregado.
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a>Explorar a estrutura de saudação do projeto de saudação
Olá estrutura a seguir é definido para o nosso projeto de esqueleto hello:

* Um modo de exibição mestre com uma pesquisa UPN
* Uma exibição de detalhes para dados saudação sobre o usuário selecionado Olá
* Um modo de exibição de logon em que um usuário pode fazer logon no gráfico de saudação do toohello aplicativo tooquery

Podemos moverá os arquivos de toovarious na autenticação de esqueleto tooadd hello. Outras partes do código de saudação, como o código do visual hello, não relacionados tooidentity, mas são fornecidos para você.

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a>Configurar Olá settings.plst arquivo na biblioteca de saudação
* No projeto de início rápido do hello, abra Olá `settings.plist` arquivo. Substitua valores de saudação de elementos Olá Olá seção tooreflect Olá os valores que você usou no portal do Azure de saudação. Seu código fará referência a esses valores sempre que ele usa Olá biblioteca de autenticação do Active Directory.
  * Olá `clientId` é Olá ID do cliente do aplicativo que você copiou do portal de saudação.
  * Olá `redirectUri` é URL de redirecionamento Olá portal Olá fornecido.

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a>Configurar Olá NXOAuth2Client biblioteca no seu LoginViewController
a biblioteca de NXOAuth2Client Olá requer alguns tooget valores configurado. Depois de concluir essa tarefa, você pode usar Olá adquiridos toocall token Olá API do Graph. Porque `LoginView` será chamado a qualquer momento precisamos tooauthenticate, faz sentido tooput valores de configuração no arquivo toothat.

* Vamos adicionar alguns valores toohello `LoginViewController.m` contexto de saudação do arquivo tooset para autenticação e autorização. Detalhes sobre os valores hello execute código hello.
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

Vamos examinar os detalhes sobre o código de saudação.

primeira cadeia de caracteres de saudação é para `scopes`.  Olá `User.Read` valor permite que você tooread perfil básico do hello de saudação usuário conectado.

Você pode aprender mais sobre todos os escopos disponíveis de saudação em [escopos de permissão do Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Para `authURL`, `loginURL`, `bhh`, e `tokenURL`, você deve usar valores hello fornecidos anteriormente. Se você usar o software livre de saudação bibliotecas de identidade do Microsoft Azure, é suspenso esses dados para você por meio de nosso ponto de extremidade de metadados. Fizemos o difícil trabalho Olá de extrair esses valores para você.

Olá `keychain` valor é o contêiner Olá Olá NXOAuth2Client biblioteca usará toocreate toostore um conjunto de chaves seus tokens. Se você deseja que tooget-logon único (SSO) em vários aplicativos, você pode especificar Olá mesmo conjunto de chaves em cada um dos seus aplicativos e solicitar o uso de saudação desse conjunto de chaves em seus direitos Xcode. Isso é explicado em Olá documentação da Apple.

rest Olá desses valores são necessários toouse Olá biblioteca e crie locais de contexto de toohello toocarry valores.

### <a name="create-a-url-cache"></a>Criar um cache de URL
Dentro de `(void)viewDidLoad()`, sempre que é chamado após a exibição Olá é carregada, o código a seguir hello primes um cache para o nosso uso.

Adicione Olá código a seguir:

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a>Criar um Modo de Exibição da Web para conexão
Uma exibição da Web pode solicitar ao usuário Olá fatores adicionais como mensagem de texto SMS (se configurado) ou retornar o usuário de toohello de mensagens de erro. Aqui você configurará Olá WebView e depois hello de gravação retornos de chamada do código toohandle Olá que ocorrerão em Olá WebView dos serviços de identidade hello.

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a>Autenticação de toohandle Olá WebView métodos de substituição
Olá tootell WebView o que acontece quando um usuário precisa toosign em como discutido anteriormente, você pode colar Olá código a seguir.

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a>Gravar código toohandle Olá resultado da solicitação de OAuth2 Olá
Olá código a seguir tratará redirectURL Olá que retorna da saudação WebView. Se a autenticação não foi bem-sucedida, o código de saudação tentará novamente. Enquanto isso, biblioteca Olá fornecerá erro Olá que você pode ver no console de saudação ou tratar de forma assíncrona.

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a>Configurar Olá contexto OAuth (chamada de repositório de conta)
Aqui você pode chamar `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` no repositório de conta compartilhada Olá para cada serviço que você deseja que o aplicativo de saudação toobe tooaccess capaz de. tipo de conta de saudação é uma cadeia de caracteres que é usada como um identificador para um determinado serviço. Porque você está acessando Olá API do Graph, o código de saudação refere-se tooit como `"myGraphService"`. Depois, configure um observador que informará quando algo for alterado com o token de saudação. Depois de obter token hello, retornar Olá usuário back toohello `masterView`.

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a>Configurar Olá toosearch do modo de exibição mestre e exibir os usuários Olá Olá API do Graph
Um aplicativo Master-View-Controller (MVC) que exibe o saudação retornada dados na grade de saudação está além do escopo de saudação deste passo a passo e tutoriais online muitos explicam como toobuild um. Todo esse código está no arquivo esqueleto hello. No entanto, você precisa toodeal com alguns itens neste aplicativo MVC:

* Quando um usuário digita algo no campo de pesquisa de saudação de interceptação
* Forneça um objeto de dados back toohello MasterView para que ele pode exibir resultados de saudação na grade de saudação

Faremos isso a seguir.

### <a name="add-a-check-toosee-if-youre-logged-in"></a>Adicionar um toosee de seleção se você está conectado
aplicativo Hello faz pouco se Olá usuário não está conectado, portanto é inteligente toocheck se já houver um token no cache de saudação. Se não, você pode redirecionar toohello LoginView para Olá usuário toosign no. Se você se lembra, Olá melhor maneira toodo ações quando uma exibição é carregado é Olá toouse `viewDidLoad()` método Apple fornece.

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-hello-table-view-when-data-is-received"></a>Saudação de atualização quando dados são recebidos de exibição de tabela
Quando Olá Graph API retorna dados, você precisa toodisplay dados de saudação. Para simplificar, aqui está a todas as tabelas de Olá Olá código tooupdate. Apenas você pode colar valores corretos da saudação em seu código de texto clichê MVC.

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a>Forneça uma saudação toocall de maneira API do Graph quando alguém digita no campo de pesquisa de saudação
Quando um usuário digita uma pesquisa na caixa hello, você precisa tooshove que toohello API do Graph. Olá `GraphAPICaller` classe, que você criará no hello código a seguir, separa a funcionalidade de pesquisa de saudação de apresentação de saudação. Por enquanto, vamos escrever código Olá feeds quaisquer caracteres de pesquisa toohello API do Graph. Podemos fazer isso ao fornecer um método chamado `lookupInGraph`, que usa a cadeia de caracteres de saudação que desejamos toosearch para.

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a>Gravar uma saudação de tooaccess classe auxiliar da Graph API
Esse é o núcleo de saudação do nosso aplicativo. Enquanto o restante de saudação estava inserindo código em saudação padrão MVC padrão da Apple, aqui você escrever gráfico de saudação do código tooquery como tipos de usuário hello e, em seguida, retornar os dados. Aqui está o código de saudação e uma explicação detalhada segue.

### <a name="create-a-new-objective-c-header-file"></a>Criar um novo arquivo de cabeçalho em Objective-C
Arquivo de saudação do nome `GraphAPICaller.h`e adicione Olá código a seguir.

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

Aqui, você vê que um método especificado usa uma cadeia de caracteres e retorna um completionBlock. Este completionBlock, como você pode esperar, atualizará Olá tabela fornecendo um objeto populados dados em tempo real conforme Olá pesquisas de usuário.

### <a name="create-a-new-objective-c-file"></a>Criar um novo arquivo Objective-C
Arquivo de saudação do nome `GraphAPICaller.m`e adicione o seguinte método de saudação.

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


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

```

Vamos analisar esse método em detalhes.

núcleo de saudação do código está em Olá `NXOAuth2Request`, método que usa parâmetros de saudação que já tenha definido no arquivo de settings.plist hello.

Olá primeira etapa é chamada de API do Graph tooconstruct saudação à direita. Como você está chamando `/users`, você pode especificar que, acrescentando-o recurso da API do Graph toohello junto com a versão de saudação. Faz sentido tooput em um arquivo externo porque eles podem alterar como Olá API evolui.

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

Em seguida, você precisa toospecify parâmetros também fornecerá toohello chamada de API do Graph. É *muito importante* que você não colocar parâmetros Olá no ponto de extremidade de recurso Olá porque que é limpo para todos os caracteres de URI não conformes em tempo de execução. Todo o código de consulta deve ser fornecido em parâmetros de saudação.

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

Observe que isso chama um método `convertParamsToDictionary` que você ainda não escreveu. Vamos fazer isso agora no final de saudação do arquivo hello:

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
Em seguida, vamos usar Olá `NXOAuth2Request` dados do método tooget fazer do hello API no formato JSON.

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

Por fim, vamos ver como você retornar Olá dados toohello MasterViewController. dados de saudação retorna como serializada e precisa toobe desserializado e carregados em um objeto que Olá MainViewController pode consumir. Para essa finalidade, esqueleto Olá tem um `User.m/h` arquivo que cria um objeto de usuário. Preencha esse objeto de usuário com as informações do gráfico de saudação.

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-hello-sample"></a>Executar o exemplo hello
Se você tiver usado esqueleto hello ou seguido junto com instruções passo a passo de saudação que seu aplicativo seja executado. Iniciar o simulador hello e clique em **entrar** aplicativo hello de toouse.

## <a name="get-security-updates-for-our-product"></a>Obter atualizações de segurança para nosso produto
Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando Olá [TechCenter de segurança](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.

