---
title: "aaaHow tooUse SDK do iOS para aplicativos móveis do Azure"
description: "Como tooUse SDK do iOS para aplicativos móveis do Azure"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a>Como tooUse iOS biblioteca de cliente para aplicativos móveis do Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Este guia ensina usando hello mais recente de cenários comuns de tooperform [os aplicativos móveis do Azure SDK do iOS][1]. Se você for novo tooAzure os aplicativos móveis, primeiro conclua [início rápido do Azure Mobile aplicativos] toocreate um back-end, crie uma tabela e baixar um projeto do Xcode iOS pré-criado. Este guia, vamos nos concentrar no SDK do iOS saudação do cliente. toolearn mais sobre Olá SDK do lado do servidor de back-end do hello, consulte HOWTOs de SDK do servidor de saudação.

## <a name="reference-documentation"></a>Documentação de referência
Olá documentação de referência do SDK do cliente de iOS hello está localizada aqui: [os aplicativos móveis do Azure iOS cliente referência][2].

## <a name="supported-platforms"></a>Plataformas com suporte
SDK do iOS Olá suporta projetos Objective-C, Swift 2.2 projetos e Swift 2.3 projetos para o iOS versão 8.0 ou posterior.

autenticação de "server-fluxo" Hello usa WebView para Olá apresentado da interface do usuário.  Se o dispositivo de Olá não for capaz de toopresent uma UI WebView, em seguida, outro método de autenticação é necessário que está fora do escopo Olá produto hello.  
Esse SDK, portanto, não é adequado para relógios ou dispositivos similarmente restritos.

## <a name="Setup"></a>Configuração e Pré-requisitos
Este guia pressupõe que você tenha criado um back-end com uma tabela. Este guia pressupõe que dessa tabela Olá tem o mesmo esquema como tabelas Olá esses tutoriais. Este guia também pressupõe que em seu código, você referencia `MicrosoftAzureMobile.framework` e importa `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.

## <a name="create-client"></a>Como: criar o cliente
tooaccess um back-end de aplicativos do Azure Mobile no seu projeto, criar um `MSClient`. Substituir `AppUrl` com a URL do aplicativo hello. Você pode deixar `gatewayURLString` e `applicationKey` vazios. Se você configurar um gateway para autenticação, popular `gatewayURLString` com hello gateway URL.

**Objective-C**:

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

**Swift**:

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <a name="table-reference"></a>Como criar uma referência de tabela
tooaccess ou atualização de dados, crie uma tabela de back-end do toohello de referência. Substituir `TodoItem` com nome de saudação da tabela

**Objective-C**:

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

**Swift**:

```
let table = client.tableWithName("TodoItem")
```


## <a name="querying"></a>Como consultar dados
toocreate uma consulta de banco de dados, Olá consulta `MSTable` objeto. Olá consulta a seguir obtém todos os itens de saudação `TodoItem` e logs Olá texto de cada item.

**Objective-C**:

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="filtering"></a>Como filtrar dados retornados
resultados de toofilter, há muitas opções disponíveis.

toofilter usando um predicado, use um `NSPredicate` e `readWithPredicate`. seguinte Olá filtra dados retornados toofind incompletas apenas itens de tarefas.

**Objective-C**:

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="query-object"></a>Como usar o MSQuery
tooperform criar uma consulta complexa (incluindo classificação e paginação), um `MSQuery` de objeto, diretamente ou por meio de um predicado:

**Objective-C**:

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

**Swift**:

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

`MSQuery` permite que você controle vários comportamentos de consulta.

* Especificar a ordem dos resultados
* Limitar quais campos tooreturn
* Limitar quantos registros tooreturn
* Especificar contagem total na resposta
* Especificar parâmetros de cadeia de consulta personalizada na solicitação
* Aplicar funções adicionais

Executar um `MSQuery` consulta chamando `readWithCompletion` no objeto de saudação.

## <a name="sorting"></a>Como classificar dados com MSQuery
resultados de toosort, vamos examinar um exemplo. toosort por 'text' campo em ordem crescente e decrescente 'completa', invocar `MSQuery` da seguinte forma:

**Objective-C**:

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <a name="selecting"></a><a name="parameters"></a>Como limitar campos e expandir os parâmetros de cadeia de caracteres de consulta com MSQuery
toolimit toobe de campos retornado em uma consulta, especificar nomes de saudação de campos de saudação no hello **selectFields** propriedade. Este exemplo retorna somente o texto de saudação e campos concluídos:

**Objective-C**:

```
query.selectFields = @[@"text", @"complete"];
```

**Swift**:

```
query.selectFields = ["text", "complete"]
```

parâmetros de cadeia de caracteres de consulta adicionais tooinclude no servidor de saudação solicitar (por exemplo, porque usa um script do lado do servidor personalizado), popular `query.parameters` da seguinte forma:

**Objective-C**:

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

**Swift**:

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <a name="paging"></a>Como: Configurar o tamanho de página
Com aplicativos móveis do Azure, controles de tamanho de página Olá Olá número de registros que são extraídas por vez de tabelas de back-end de saudação. Uma chamada muito`pull` dados seriam do lote, em seguida, os dados, com base no tamanho de página, até que não haja nenhum toopull registros mais.

É possível tooconfigure um tamanho de página usando **MSPullSettings** conforme mostrado abaixo. tamanho de página saudação padrão é 50, e o exemplo hello abaixo altera too3.

Você pode configurar um tamanho de página diferente por motivos de desempenho. Se você tiver um grande número de registros de dados pequeno, um tamanho de página de alta reduz o número de saudação de ida e volta do servidor.

Essa configuração controla apenas o tamanho de página Olá no lado do cliente de saudação. Se o cliente Olá solicita um tamanho de página maior que oferece suporte a aplicativos móveis de saudação back-end, o tamanho da página de saudação é controlada no back-end do Olá Olá máximo é toosupport configurado.

Essa configuração também é hello *número* de registros de dados, não Olá *tamanho em bytes*.

Se você aumentar o tamanho de página do cliente hello, você também deve aumentar o tamanho de página Olá no servidor de saudação. Consulte ["como: ajustar o tamanho da paginação tabela hello"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para Olá etapas toodo isso.

**Objective-C**:

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


**Swift**:

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <a name="inserting"></a>Como inserir dados
criar uma nova linha de tabela, de tooinsert um `NSDictionary` e invocar `table insert`. Se [esquema dinâmico] é habilitado, hello Azure do serviço de aplicativo móvel back-end automaticamente gera novas colunas com base em Olá `NSDictionary`.

Se `id` não for fornecido, Olá back-end gera automaticamente uma nova ID exclusiva. Fornecer sua própria `id` toouse seus próprios valores personalizados, nomes de usuário ou endereços de email como ID. Fornecer sua própria identificação pode facilitar junções e lógicas de banco de dados comerciais.

Olá `result` contém Olá novo item que foi inserida. Dependendo de sua lógica de servidor, pode ter adicionais em comparação comparados os dados modificados toowhat foi passado ou toohello server.

**Objective-C**:

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <a name="modifying"></a>Como modificar dados
tooupdate uma linha existente, modifique um item e a chamada `update`:

**Objective-C**:

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

Como alternativa, fornece Olá ID da linha e campo Olá atualizado:

**Objective-C**:

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

No mínimo, Olá `id` atributo deve ser definido ao fazer atualizações.

## <a name="deleting"></a>Como excluir dados
toodelete um item, invocar `delete` com item hello:

**Objective-C**:

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Swift**:

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

Como alternativa, exclua fornecendo uma ID de linha:

**Objective-C**:

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Swift**:

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

No mínimo, Olá `id` atributo deve ser definido quando fazer exclui.

## <a name="customapi"></a>Como chamar uma API personalizada
Com uma API personalizada, você pode expor qualquer funcionalidade de back-end. Operação de tabela tooa toomap não é necessário. Não só você obter mais controle sobre o sistema de mensagens, você pode até mesmo conjunto de cabeçalhos de leitura/e alterar o formato do corpo de resposta de saudação. toolearn como toocreate uma API personalizada no back-end hello, ler [APIs personalizadas](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)

toocall uma API personalizada, chame `MSClient.invokeAPI`. saudação de solicitação e resposta de conteúdo são tratados como JSON. toouse outros tipos de mídia, [use Olá outra sobrecarga do `invokeAPI` ] [ 5].  toomake um `GET` solicitação em vez de um `POST` solicitação, o parâmetro de conjunto de `HTTPMethod` muito`"GET"` e parâmetro `body` muito`nil` (como solicitações GET não ter corpos de mensagens.) Se sua API personalizada dá suporte a outros verbos HTTP, altere o `HTTPMethod` adequadamente.

**Objective-C**:

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

**Swift**:

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <a name="templates"></a>Como: notificações de plataforma cruzada do registro por push modelos toosend
modelos de tooregister passar modelos com seu **client.push registerDeviceToken** método no seu aplicativo cliente.

**Objective-C**:

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

**Swift**:

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

Os modelos são do tipo NSDictionary e podem conter vários modelos em Olá formato a seguir:

**Objective-C**:

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

**Swift**:

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

Todas as marcas são eliminadas da solicitação de saudação de segurança.  tooadd marcas tooinstallations ou modelos dentro de instalações, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure][4].  notificações de toosend usando esses modelos registrados, trabalhar com [APIs de Hubs de notificação][3].

## <a name="errors"></a>Como tratar erros
Quando você chama um back-end móvel do serviço de aplicativo do Azure, o bloco de conclusão de saudação contém um `NSError` parâmetro. Quando ocorre um erro, esse parâmetro é não nulo. No seu código, você deve verificar esse parâmetro e tratar o erro Olá conforme necessário, como demonstrado no hello anterior trechos de código.

arquivo Hello [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] define constantes Olá `MSErrorResponseKey`, `MSErrorRequestKey`, e `MSErrorServerItemKey`. tooget mais dados relacionados ao erro toohello:

**Objective-C**:

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

**Swift**:

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

Além disso, o arquivo hello define constantes para cada código de erro:

**Objective-C**:

```
if (error.code == MSErrorPreconditionFailed) {
```

**Swift**:

```
if (error.code == MSErrorPreconditionFailed) {
```

## <a name="adal"></a>Como: autenticar usuários com hello biblioteca de autenticação do Active Directory
Você pode usar usuários do hello biblioteca de autenticação do Active Directory (ADAL) toosign em seu aplicativo usando o Active Directory do Azure. Autenticação de fluxo de cliente usando um provedor de identidade SDK é preferível toousing Olá `loginWithProvider:completion:` método.  Autenticação de fluxo de cliente fornece uma aparência mais nativa do UX e permite uma maior personalização.

1. Configurar seu back-end do aplicativo móvel para entrar no AAD pela seguinte Olá [como tooconfigure aplicativo de serviço de logon do Active Directory] [ 7] tutorial. Torne-se toocomplete Olá opcional de registro de um aplicativo cliente nativo. Para iOS, é recomendável que direcionam Olá URI tem formato Olá `<app-scheme>://<bundle-id>`. Para obter mais informações, consulte Olá [quickstart iOS ADAL][8].
2. Instale o ADAL usando o Cocoapods. Editar a saudação de tooinclude Podfile definição a seguir, substituindo **seu projeto** com nome de saudação do seu projeto Xcode:

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   e hello Pod:

        pod 'ADALiOS'
3. Usando Olá Terminal, execute `pod install` do diretório Olá contendo seu projeto e abra Olá gerado Xcode espaço de trabalho (não o projeto de saudação).
4. Adicione Olá aplicativo tooyour de código a seguir, de acordo com a linguagem de toohello que você está usando. Em cada um, faça estas substituições:

   * Substituir **aqui de autoridade de inserção** com o nome de saudação do locatário Olá no qual você provisionou o seu aplicativo. O formato deve ser https://login.microsoftonline.com/contoso.onmicrosoft.com. Esse valor pode ser copiado de guia de saudação do domínio no Active Directory do Azure no hello [portal clássico do Azure].
   * Substituir **inserir recursos-ID aqui** com a ID de cliente Olá para o back-end do aplicativo móvel. Você pode obter a ID do cliente de saudação **avançado** guia **configurações do Active Directory do Azure** no portal de saudação.
   * Substituir **aqui INSERT-CLIENT-ID** com a ID de cliente Olá você copiou do aplicativo cliente nativo de saudação.
   * Substituir **INSERT-REDIRECT-URI-aqui** com seu site */.auth/login/done* ponto de extremidade, usando o esquema do hello HTTPS. Esse valor deve ser semelhante muito*https://contoso.azurewebsites.net/.auth/login/done*.

**Objective-C**:

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


**Swift**:

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <a name="facebook-sdk"></a>Como: autenticar usuários com hello Facebook SDK para iOS
Você pode usar o hello Facebook SDK para iOS toosign usuários em seu aplicativo usando o Facebook.  Usando a autenticação de um fluxo de cliente é preferível toousing Olá `loginWithProvider:completion:` método.  autenticação de fluxo de cliente Olá fornece uma aparência UX mais nativa e permite a personalização adicional.

1. Configure seu back-end do aplicativo móvel para entrar no Facebook seguindo o [como tooconfigure aplicativo de serviço de logon do Facebook] [ 9] tutorial.
2. Instalar Olá Facebook SDK para iOS pela seguinte Olá [Facebook SDK para iOS - Introdução] [ 10] documentação. Em vez de criar um aplicativo, você pode adicionar um registro existente de tooyour Olá de plataforma iOS.
3. Documentação do Facebook inclui um código Objective-C em Olá representante do aplicativo. Se você estiver usando **Swift**, você pode usar o hello traduções para appdelegate. SWIFT a seguir:

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. Em adição tooadding `FBSDKCoreKit.framework` tooyour de projeto, também adicionar uma referência muito`FBSDKLoginKit.framework` em Olá mesma maneira.
5. Adicione Olá aplicativo tooyour de código a seguir, de acordo com a linguagem de toohello que você está usando.

**Objective-C**:

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

**Swift**:

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <a name="twitter-fabric"></a>Instruções: autenticar usuários com a Twitter Fabric para iOS
Você pode usar a malha para usuários do iOS toosign em seu aplicativo usando o Twitter. Autenticação de cliente de fluxo é preferível toousing Olá `loginWithProvider:completion:` método, como ele fornece uma aparência UX mais nativa e permite a personalização adicional.

1. Para configurar seu back-end do aplicativo móvel para entrar no Twitter, Olá após [como tooconfigure de serviço de aplicativo para o logon do Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.
2. Adicionar projeto de tooyour de malha, Olá seguir [malha para iOS - Introdução] documentação e a configuração TwitterKit.

   > [!NOTE]
   > Por padrão, o Fabric cria um aplicativo do Twitter para você. Você pode evitar a criação de um aplicativo registrando Olá chave do consumidor e o segredo do consumidor criado anteriormente usando o hello trechos de código a seguir.    Como alternativa, você pode substituir Olá chave do consumidor e valores de segredo do consumidor que você forneça valores tooApp serviço com hello consulte Olá [painel da malha]. Se você escolher essa opção, ser se tooset Olá retorno de chamada URL tooa valor de espaço reservado, como `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.
   >
   >

    Se você escolher toouse segredos Olá criado anteriormente, adicione Olá código tooyour representante do aplicativo a seguir:

    **Objective-C**:

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    **Swift**:

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. Adicione Olá aplicativo tooyour de código a seguir, de acordo com a linguagem de toohello que você está usando.

**Objective-C**:

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

**Swift**:

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <a name="google-sdk"></a>Como: autenticar usuários com hello Google entrar SDK para iOS
Você pode usar o hello Google entrar SDK para iOS toosign usuários em seu aplicativo usando uma conta do Google.  Google recentemente anunciado alterações tootheir OAuth as políticas de segurança.  Essas alterações de política requerem Olá uso do SDK do Google no hello futuras.

1. Configurar seu back-end do aplicativo móvel para entrar no Google pelo seguinte Olá [como tooconfigure de serviço de aplicativo para o logon do Google](app-service-mobile-how-to-configure-google-authentication.md) tutorial.
2. Instalar Olá Google SDK para iOS pela seguinte Olá [Sign-In Google para iOS - iniciar a integração de](https://developers.google.com/identity/sign-in/ios/start-integrating) documentação. Você pode ignorar a seção de "Autenticar com um servidor back-end" hello.
3. Adicionar saudação do tooyour representante a seguir `signIn:didSignInForUser:withError:` método, de acordo com o idioma toohello que você está usando.

**Objective-C**:

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

**Swift**:

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. Certifique-se de também adicionar Olá seguir muito`application:didFinishLaunchingWithOptions:` em seu aplicativo delegar, substituindo "SERVER_CLIENT_ID" com hello mesma ID que você usou tooconfigure do serviço de aplicativo na etapa 1.

**Objective-C**:

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 **Swift**:

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. Adicionar Olá após o aplicativo de tooyour de código em um UIViewController que implementa Olá `GIDSignInUIDelegate` protocolo, de acordo com a linguagem de toohello que você está usando.  Você saiu antes que está sendo assinado novamente, e embora não seja necessário tooenter suas credenciais novamente, você verá uma caixa de diálogo de consentimento.  Chame esse método quando o token de sessão Olá expirou.

   **Objective-C**:

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   **Swift**:

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[início rápido do Azure Mobile aplicativos]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[esquema dinâmico]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[painel da malha]: https://www.fabric.io/home
[malha para iOS - Introdução]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
