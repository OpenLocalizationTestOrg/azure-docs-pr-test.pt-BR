---
title: "aaaSending tooiOS de notificações por push com Hubs de notificação do Azure | Microsoft Docs"
description: "Neste tutorial, você aprenderá como o aplicativo do iOS tooan notificações de envio toouse toosend de Hubs de notificação do Azure."
services: notification-hubs
documentationcenter: ios
keywords: "notificação por push, notificações por push, notificações por push do ios"
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a>TooiOS envio de notificações por push com Hubs de notificação do Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Visão geral
> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).
> 
> 

Este tutorial mostra como o aplicativo do iOS tooan notificações de envio toouse toosend de Hubs de notificação do Azure. Você criará um aplicativo iOS em branco que recebe notificações por push usando Olá [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html). 

Quando você terminar, você será capaz de toouse sua toobroadcast de hub de notificação por push notificações tooall Olá a dispositivos que executam seu aplicativo.

## <a name="before-you-begin"></a>Antes de começar
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Olá concluída de código para este tutorial pode ser encontrado [no GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted). 

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial requer o seguinte hello:

* [serviços móveis iOS SDK versão 1.2.4]
* Versão mais recente do [Xcode]
* Um dispositivo compatível com o iOS 8 (ou versão posterior)
* [Programa de Desenvolvedores de iOS](https://developer.apple.com/programs/) 
  
  > [!NOTE]
  > Devido aos requisitos de configuração para notificações por push, você deve implantar e testar notificações por push em um dispositivo físico iOS (iPhone ou iPad) em vez da saudação simulador de iOS.
  > 
  > 

A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre os Hubs de Notificação para aplicativos do iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a>Configurar o Hub de Notificação para notificações por push do iOS
Esta seção orienta você pela criação de um novo hub de notificação e configurar a autenticação com APNS usando Olá **. p12** certificado de push que você criou. Se você quiser toouse um hub de notificação que você já tiver criado, você poderá ignorar toostep 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p>Clique Olá <b>Notification Services</b> botão Olá <b>configurações</b> folha, selecione <b>Apple (APNS)</b>. Clique em <b>carregar certificado</b> e selecione hello <b>. p12</b> arquivo que você exportou anteriormente. Verifique se que você também especificar a senha correta da saudação.</p>

<p>Certifique-se de que tooselect <b>Sandbox</b> modo como isso é para o desenvolvimento. Somente use Olá <b>produção</b> se você quiser toosend toousers de notificações de envio que compraram o aplicativo da loja de saudação.</p>
</li>
</ol>
&emsp;&emsp;&emsp;&emsp;![Configurar APNS no Portal do Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)

&emsp;&emsp;&emsp;&emsp;![Configurar certificação do APNS no Portal do Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

O hub de notificação agora está configurado toowork com APNS e ter Olá tooregister de cadeias de caracteres de conexão de seu aplicativo e enviar notificações por push.

## <a name="connect-your-ios-app-toonotification-hubs"></a>Conectar seu aplicativo de iOS tooNotification Hubs
1. No Xcode, crie um novo projeto de iOS e selecione Olá **único aplicativo de exibição** modelo.
   
    ![Xcode - aplicativo de modo de exibição único][8]
    
2. Ao definir opções de saudação para seu novo projeto, certifique-se de toouse Olá mesmo **nome do produto** e **identificador de organização** que você usou quando você configurado anteriormente ID do pacote Olá Olá desenvolvedor Apple Portal.
   
    ![Xcode - opções de projeto][11]
    
3. Em **destinos**, clique em seu nome de projeto Olá **configurações da compilação** guia e expanda **a identidade de assinatura de código**e, em seguida, em **depurar**, defina sua identidade de assinatura de código. Ativar/desativar **níveis** de **básica** muito**todos os**e defina **perfil de provisionamento de** toohello provisionamento de perfil que você criou anteriormente .
   
    Se você não vir Olá provisionamento novo perfil que você criou no Xcode, tente atualizar perfis Olá para sua identidade de assinatura. Clique em **Xcode** na barra de menus do hello, clique em **preferências**, clique em Olá **conta** , clique em Olá **exibir detalhes** , clique em seu assinatura de identidade e, em seguida, clique botão de atualização de saudação no canto inferior direito de saudação.
   
    ![Xcode - perfil de provisionamento][9]
4. Baixar Olá [serviços móveis iOS SDK versão 1.2.4] e descompacte o arquivo hello. No Xcode, clique com o botão direito e clique em Olá **adicionar arquivos ao** Olá de tooadd opção **WindowsAzureMessaging.framework** projeto de Xcode tooyour pasta. Selecione **Copiar itens se necessário** e depois clique em **Adicionar**.
   
   > [!NOTE]
   > hubs de notificação Olá SDK não suporta atualmente bitcode no Xcode 7.  Você deve definir **habilitar Bitcode** muito**não** em Olá **opções de compilação** para seu projeto.
   > 
   > 
   
    ![Descompactar o SDK do Azure][10]
5. Adicione um novo projeto de tooyour de arquivo de cabeçalho chamado `HubInfo.h`. Esse arquivo manterá constantes Olá para o hub de notificação.  Adicionar Olá definições a seguir e substitua os espaços reservados literal de cadeia de caracteres hello com seu *nome do hub* e hello *DefaultListenSharedAccessSignature* que você anotou anteriormente.
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. Abra seu `AppDelegate.h` adicionar de arquivo hello diretivas de importação a seguir:
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. No seu `AppDelegate.m file`, adicionar Olá Olá código a seguir `didFinishLaunchingWithOptions` método com base na sua versão do iOS. Esse código registra seu identificador de dispositivo nas APNs:
   
    Para iOS 8:
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    Para too8 anteriores do iOS versões:
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. Em Olá mesmo arquivo, adicione Olá métodos a seguir. Esse código conecta-se usando as informações de conexão de saudação especificado em HubInfo.h de hub de notificação toohello. Ele oferece hub de notificação de token toohello Olá dispositivo, em seguida, para que hello hub de notificação pode enviar notificações:
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. Em Olá mesmo arquivo, adicione Olá toodisplay do método a seguir um **UIAlert** se notificação de saudação for recebida, enquanto o aplicativo hello está ativo:

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. Compilar e executar o aplicativo hello em seu tooverify de dispositivo que não há nenhuma falha.

## <a name="send-test-push-notifications"></a>Enviar notificações por push de teste
Você pode testar a receber notificações em seu aplicativo por meio do envio de notificações por push em Olá [Portal do Azure] via Olá **solução de problemas** seção na folha de hub hello (use Olá *deenviodeteste* opção).

![Portal do Azure - Testar Enviar][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a>(Opcional) Enviar notificações por push do aplicativo hello
> [!IMPORTANT]
> Este exemplo de envio de notificações do aplicativo de cliente de saudação é fornecido para fins de aprendizado. Uma vez que isso exigirá Olá `DefaultFullSharedAccessSignature` toobe presente no aplicativo de cliente hello, ele expõe o risco de toohello do hub de notificação que um usuário pode obter acesso não autorizado de toosend notificações tooyour clientes.
> 
> 

Se você quiser notificações por push de toosend de dentro de um aplicativo, esta seção fornece um exemplo de como toodo Olá isso usando a interface REST.

1. No Xcode, abra `Main.storyboard` e adicione Olá seguindo os componentes de interface do usuário da saudação objeto biblioteca tooallow Olá usuário toosend notificações por push no aplicativo hello:
   
   * Um rótulo sem texto de rótulo. Ele será usado tooreport erros no envio de notificações. Olá **linhas** propriedade deve ser definida muito**0** para que ele será dimensionado automaticamente toohello restrita direita e as margens esquerdas e superior de saudação do modo de exibição de saudação.
   * Um campo de texto com **espaço reservado** texto definido muito**Inserir mensagem de notificação**. Restringir o campo Olá logo abaixo rótulo Olá conforme mostrado abaixo. Defina Olá View Controller como representante de loja hello.
   * Um botão chamado **enviar notificação** restrita abaixo de campo de texto de saudação e no Centro de saudação horizontal.
     
     exibição de saudação se assemelhar ao seguinte:
     
     ![Designer do Xcode][32]
2. [Adicionar saídas](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) de campo de rótulo e o texto de saudação conectado seu modo de exibição e atualizar seu `interface` definição toosupport `UITextFieldDelegate` e `NSXMLParserDelegate`. Adicione declarações de propriedade três Olá mostradas abaixo toohelp suporte chamando Olá API REST e analisar a resposta de saudação.
   
    O arquivo ViewController.h deve ser semelhante ao seguinte:
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. Abra `HubInfo.h` e adicione Olá constantes que serão usadas para enviar o hub de tooyour notificações a seguir. Substitua o literal de cadeia de espaço reservado de saudação com seu real *DefaultFullSharedAccessSignature* cadeia de caracteres de conexão.
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. Adicione o seguinte Olá `#import` instruções tooyour `ViewController.h` arquivo.
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. No `ViewController.m` adicionar Olá implementação de interface toohello de código a seguir. Esse código analisará a cadeia de conexão *DefaultFullSharedAccessSignature* . Conforme mencionado em Olá [referência da API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), essas informações analisadas serão toogenerate usado um token SaS para Olá **autorização** cabeçalho de solicitação.
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. Em `ViewController.m`, Olá atualização `viewDidLoad` método tooparse Olá conexão cadeia de caracteres quando a exibição Olá carrega. Também adicionar métodos de utilitário hello, mostrados abaixo, a implementação de interface toohello.  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. Em `ViewController.m`, adicionar Olá após código toohello interface implementação toogenerate Olá autorização token SaS que será fornecido em hello **autorização** cabeçalho, como mencionado na Olá [API REST Referência](http://msdn.microsoft.com/library/azure/dn495627.aspx).
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. CTRL + arrastar de Olá **enviar notificação** botão muito`ViewController.m` tooadd uma ação chamada **SendNotificationMessage** para Olá **toque para baixo** eventos. Método de atualização com hello notificação de saudação do código toosend usando Olá API REST a seguir.
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. Em `ViewController.m`, adicionar Olá Delegar método toosupport teclado Olá para o campo de texto de saudação de fechamento a seguir. CTRL + arrastar Olá texto campo toohello View Controller do ícone de no Olá Olá de designer tooset interface exibir controlador como representante de loja hello.
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. Em `ViewController.m`, adicione a seguinte Olá delegar a resposta de análise Olá métodos toosupport usando `NSXMLParser`.
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. Criar projeto hello e verifique se não há nenhum erro.

> [!NOTE]
> Se você encontrar um erro de compilação em Xcode7 sobre o suporte de bitcode, você deve alterar Olá **configurações da compilação** > **Bitcode habilitar (ENABLE_BITCODE)** muito**não** no Xcode. Olá SDK de Hubs de notificação atualmente não dá suporte para bitcode. 
> 
> 

Você encontrará todas as cargas de notificações possíveis Olá Olá Apple [Local e o guia de programação de notificação por Push].

## <a name="checking-if-your-app-can-receive-push-notifications"></a>Como verificar se o aplicativo pode receber notificações por push
notificações de push tootest no iOS, você deve implantar o dispositivo de e / s físicas Olá aplicativo tooa. Você não pode enviar notificações de envio por push da Apple usando Olá simulador de iOS.

1. Execute o aplicativo hello e verifique que o registro for bem-sucedido e, em seguida, pressione **Okey**.
   
    ![Teste de registro de notificação por push de aplicativo do iOS][33]
2. Você pode enviar uma notificação por push de teste do hello [Portal do Azure], conforme descrito acima. Se você adicionou o código para enviar notificações por push no aplicativo hello, toque em tooenter de campo de texto de saudação uma mensagem de notificação. Pressione Olá **enviar** botão no teclado hello ou Olá **enviar notificação** botão na mensagem de notificação de saudação do hello exibição toosend.
   
    ![Teste de envio de notificação por push de aplicativo do iOS][34]
3. Olá push notificação é enviada tooall dispositivos registrado tooreceive notificações de saudação do hello Hub de notificação específica.
   
    ![Teste de recebimento de notificação por push de aplicativo do iOS][35]

## <a name="next-steps"></a>Próximas etapas
Neste exemplo simples, você transmitida tooall de notificações por push seus dispositivos iOS registrados. Sugerimos como uma próxima etapa do aprendizado continuar toohello [notificação Hubs notificar os usuários do Azure para iOS com o back-end .NET] tutorial, que irá orientá-lo na criação de um envio por push do back-end toosend notificações usando marcas. 

Se você quiser toosegment os usuários, grupos de interesse, você poderá mover além no toohello [toosend de Hubs de notificação de uso últimas notícias] tutorial. 

Para obter informações gerais sobre os Hubs de Notificação, confira [Diretrizes dos Hubs de Notificação].

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[serviços móveis iOS SDK versão 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Diretrizes dos Hubs de Notificação]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[notificação Hubs notificar os usuários do Azure para iOS com o back-end .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[toosend de Hubs de notificação de uso últimas notícias]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[Local e o guia de programação de notificação por Push]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Portal do Azure]: https://portal.azure.com
