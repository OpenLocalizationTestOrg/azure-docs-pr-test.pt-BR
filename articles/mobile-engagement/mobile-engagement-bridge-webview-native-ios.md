---
title: iOS aaaBridge WebView com o SDK do iOS nativo do Mobile Engagement
description: "Descreve como toocreate uma ponte entre a exibição da Web que executa o Javascript e hello nativo do Mobile Engagement iOS SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: e1d6ff6f-cd67-4131-96eb-c3d6318de752
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 089ed8484722cb5ba624e5dce0e670ab56de514d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a>Faça a ponte entre o iOS WebView com SDK do Mobile Engagement iOS
> [!div class="op_single_selector"]
> * [Ponte do Android](mobile-engagement-bridge-webview-native-android.md)
> * [Ponte do iOS](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Alguns aplicativos móveis são criados como um aplicativo híbrido onde aplicativo hello em si é desenvolvido usando desenvolvimento iOS nativo Objective-C, mas algumas ou todas as telas de saudação são renderizadas dentro de um exibição da Web do iOS. Você ainda pode consumir o SDK do iOS do Mobile Engagement em tais aplicativos e este tutorial descreve como toogo sobre como fazer isso. 

Há dois tooachieve de abordagens isso Embora ambos sejam documentadas:

* A primeira é descrita neste [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) e envolve registrar um `UIWebViewDelegate` no modo de exibição da Web e pegar e cancelar imediatamente uma alteração de local feita no Javascript. 
* Segundo uma baseada nessa [WWDC 2013 sessão](https://developer.apple.com/videos/play/wwdc2013/615), uma abordagem que é mais fácil do que Olá primeiro e que vamos seguir este guia. Observe que essa abordagem funciona apenas no iOS7 e posterior. 

Siga as etapas de saudação abaixo para iOS Olá ponte exemplo:

1. Em primeiro lugar, você precisa tooensure que passaram por meio de nosso [tutorial de Introdução](mobile-engagement-ios-get-started.md) toointegrate Olá iOS SDK do Mobile Engagement em seu aplicativo híbrido. Opcionalmente, você também pode habilitar teste log da seguinte maneira para que você pode ver os métodos SDK Olá como podemos dispará-los do webview Olá. 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. Agora, verifique se seu aplicativo híbrido tem uma tela com WebView. Você pode adicionar toohello `Main.storyboard` do aplicativo hello. 
3. Associar este webview com seu **ViewController** clicando e arrastando Olá webview da saudação exibição controlador cena toohello `ViewController.h` Editar tela, colocando-o abaixo Olá `@interface` linha. 
4. Quando você fizer isso, uma caixa de diálogo será exibida solicitando um nome. Forneça nome hello como **webView**. O `ViewController.h` arquivo deve ser semelhante Olá seguinte:
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. Atualizaremos Olá `ViewController.m` arquivo mais tarde, mas primeiro vamos criar arquivo de saudação da ponte que cria um wrapper sobre alguns iOS Mobile Engagement comumente usados métodos do SDK. Criar um novo arquivo de cabeçalho chamado **EngagementJsExports.h** que usa Olá `JSExport` mecanismo descrito em Olá mencionados acima [sessão](https://developer.apple.com/videos/play/wwdc2013/615) métodos do tooexpose Olá iOS nativo. 
   
        #import <Foundation/Foundation.h>
        #import <JavaScriptCore/JavascriptCore.h>
   
        @protocol EngagementJsExports <JSExport>
   
        + (void) sendEngagementEvent:(NSString*) name :(NSString*)extras;
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras;
        + (void) endEngagementJob:(NSString*) name;
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras;
        + (void) sendEngagementAppInfo:(NSString*) appInfo;
   
        @end
   
        @interface EngagementJs : NSObject <EngagementJsExports>
   
        @end
6. Em seguida, vamos criar a segunda parte Olá do arquivo de saudação da ponte. Crie um arquivo chamado **EngagementJsExports.m** que conterá a implementação de saudação criando Olá wrappers reais chamando métodos do SDK Olá Mobile Engagement iOS. Observe também que podemos estiver analisando Olá `extras` sendo passados do hello webview javascript e colocá-lo para um `NSMutableDictionary` toobe objeto passado com hello método do SDK do contrato chamadas.  
   
        #import <UIKit/UIKit.h>
        #import "EngagementAgent.h"
        #import "EngagementJsExports.h"
   
        @implementation EngagementJs
   
        +(void) sendEngagementEvent:(NSString*)name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendEvent:name extras:extrasInput];
        }
   
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] startJob:name extras:extrasInput];
        }
   
        + (void) endEngagementJob:(NSString*) name {
           [[EngagementAgent shared] endJob:name];
        }
   
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendError:name extras:extrasInput];
        }
   
        + (void) sendEngagementAppInfo:(NSString*) appInfo {
           NSMutableDictionary* appInfoInput = [self ParseExtras:appInfo];
           [[EngagementAgent shared] sendAppInfo:appInfoInput];
        }
   
        + (NSMutableDictionary*) ParseExtras:(NSString*) input {
           NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
           NSError* error = nil;
           NSMutableDictionary* extras = [NSJSONSerialization JSONObjectWithData:data options:0 error:&error];
   
           return extras;
        }
   
        @end
7. Agora podemos voltar toohello **ViewController.m** e atualizá-lo com hello código a seguir: 
   
        #import <JavaScriptCore/JavaScriptCore.h>
        #import "ViewController.h"
        #import "EngagementJsExports.h"
   
        @interface ViewController ()
   
        @end
   
        @implementation ViewController
   
        - (void)viewDidLoad
        {
           self.webView.delegate = self;
           [super viewDidLoad];
           [self loadWebView];
        }
   
        - (void)loadWebView {
           NSBundle* mainBundle = [NSBundle mainBundle];
           NSURL* htmlPage = [mainBundle URLForResource:@"LocalPage" withExtension:@"html"];
   
           NSURLRequest* urlReq = [NSURLRequest requestWithURL:htmlPage];
           [self.webView loadRequest:urlReq];
        }
   
        - (void)webViewDidFinishLoad:(UIWebView*)wv
        {
           JSContext* context = [wv valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
   
           context[@"EngagementJs"] = [EngagementJs class];
        }
   
        - (void)webView:(UIWebView*)wv didFailLoadWithError:(NSError*)error
        {
           NSLog(@"Error for WEBVIEW: %@", [error description]);
        }
   
        - (void)didReceiveMemoryWarning {
           [super didReceiveMemoryWarning];
           // Dispose of any resources that can be recreated.
        }
   
        @end
8. Pontos a seguir Olá Observação sobre Olá **ViewController.m** arquivo:
   
   * Em Olá `loadWebView` método, estamos carregando um arquivo HTML local chamado **LocalPage.html** cujo código analisaremos lado. 
   * Em Olá `webViewDidFinishLoad` método, são captando Olá `JsContext` e associando nossa classe wrapper ele. Isso permitirá que chamar métodos SDK usando o identificador de saudação de nosso wrapper **EngagementJs** do webView hello. 
9. Crie um arquivo chamado **LocalPage.html** com hello código a seguir:
   
        <!doctype html>
        <html>
           <head>
               <style type='text/css'>
                   html { font-family:Helvetica; color:#222; }
                   h1 { color:steelblue; font-size:22px; margin-top:16px; }
                   h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
               </style>
   
               <script type="text/javascript">
   
               window.onerror = function(err)
               {
                   alert('window.onerror: ' + err);
               }
   
               function send(inputId)
               {
                   var input = document.getElementById(inputId);
                   if(input)
                   {
                       var value = input.value;
                       // Example of how extras info can be passed with hello Engagement logs
                       var extras = '{"CustomerId":"MS290011"}';
                   }
   
                   if(value && value.length > 0)
                   {
                       switch(inputId)
                       {
                           case "event":
                           EngagementJs.sendEngagementEvent(value, extras);
                           break;
   
                           case "job":
                           EngagementJs.startEngagementJob(value, extras);
                           window.setTimeout(
                           function(){
                               EngagementJs.endEngagementJob(value);
                           }, 10000 );
                           break;
   
                           case "error":
                           EngagementJs.sendEngagementError(value, extras);
                           break;
   
                           case "appInfo":
                           var appInfo = '{"customer_name":"' + value + '"}';
                           EngagementJs.sendEngagementAppInfo(appInfo);
                           break;
                       }
                   }
               }
               </script>
   
           </head>
           <body>
               <h1>Bridge Tester</h1>
   
               <div id='engagement'>
   
                   <br/>
                   <h2>Event</h2>
                   <input type="text" id="event" size="35">
                   <button onclick="send('event')">Send</button>
   
                   <br/>
                   <h2>Job</h2>
                   <input type="text" id="job" size="35">
                   <button onclick="send('job')">Send</button>
   
                   <br/>
                   <h2>Error</h2>
                   <input type="text" id="error" size="35">
                   <button onclick="send('error')">Send</button
   
                   <br/>
                   <h2>AppInfo</h2>
                   <input type="text" id="appInfo" size="35">
                   <button onclick="send('appInfo')">Send</button>
   
               </div>
           </body>
        </html>
10. Pontos a seguir Olá Observação sobre o arquivo HTML Olá acima:
    
    * Ele contém um conjunto de caixas de entrada, onde você pode fornecer dados toobe utilizado como nomes de seu evento, o trabalho, o erro, o AppInfo. Quando você clica em Olá botão Avançar tooit, é feita uma chamada toohello Javascript que eventualmente chama métodos de saudação da saudação ponte arquivo toopass toohello essa chamada do SDK do Mobile Engagement iOS. 
    * Nós são marcação em alguns eventos de toohello informações estáticas sobre extra, trabalhos e até mesmo erros toodemonstrate como isso pode ser feito. Essas informações extras é enviada como um JSON de cadeia de caracteres que, se você olhar no hello `EngagementJsExports.m` de arquivo, é analisado e passadas junto com eventos, trabalhos, erros de envio. 
    * Um trabalho do Mobile Engagement é iniciado com o nome hello você especificar na caixa de entrada hello, executado por 10 segundos e desligar. 
    * Um compromisso de mobilidade appinfo ou uma marca é passada com 'customer_name' como chave estática hello e o valor de saudação que você inseriu na entrada hello como valor Olá para marca de saudação. 
11. Saudação de execução de aplicativo e você verá a seguir hello. Agora, fornecer algum nome de um evento de teste como Olá a seguir e clique em **enviar** tooit Avançar. 
    
     ![][1]
12. Agora, se você for toohello **Monitor** guia do aplicativo e veja em **eventos -> detalhes**, você verá esse evento aparecer junto com hello estático app-info que estamos enviando. 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
