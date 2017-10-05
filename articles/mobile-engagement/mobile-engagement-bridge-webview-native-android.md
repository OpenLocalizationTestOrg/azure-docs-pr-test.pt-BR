---
title: Ponte Android WebView com o SDK do Mobile Engagement Android
description: Descreve como criar uma ponte entre o WebView que executa Javascript e o SDK do Mobile Engagement iOS nativo
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: cf272f3f-2b09-41b1-b190-944cdca8bba2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4fc7b3c81747ec80974a99084eeb1acc311f11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="22656-103">Ponte Android WebView com o SDK do Mobile Engagement Android</span><span class="sxs-lookup"><span data-stu-id="22656-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22656-104">Ponte do Android</span><span class="sxs-lookup"><span data-stu-id="22656-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="22656-105">Ponte do iOS</span><span class="sxs-lookup"><span data-stu-id="22656-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="22656-106">Alguns aplicativos móveis são projetados como um aplicativo híbrido onde o aplicativo foi desenvolvido usando desenvolvimento Android nativo, mas algumas ou todas as telas são renderizadas em uma exibição do Android WebView.</span><span class="sxs-lookup"><span data-stu-id="22656-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native Android development but some or even all of the screens are rendered within an Android WebView.</span></span> <span data-ttu-id="22656-107">Você ainda pode consumir o SDK do Mobile Engagement Android em tais aplicativos e este tutorial descreve como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="22656-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how to go about doing this.</span></span> <span data-ttu-id="22656-108">O exemplo de código abaixo baseia-se nesta documentação do Android [aqui](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="22656-108">The sample code below is based on the Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="22656-109">Ela descreve como essa abordagem documentada poderia ser usada para implementar o mesmo para métodos mais usados pelo SDK do Mobile Engagement Android de forma que uma Webview de um aplicativo híbrido também possa iniciar solicitações para controlar eventos, trabalhos, erros, informações do aplicativo enquanto os canaliza pelo nosso SDK do Android.</span><span class="sxs-lookup"><span data-stu-id="22656-109">It describes how this documented approach could be used to implement the same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests to track events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="22656-110">Em primeiro lugar, você precisa concluir nosso [Tutorial de introdução](mobile-engagement-android-get-started.md) para integrar o SDK do Mobile Engagement Android ao aplicativo híbrido.</span><span class="sxs-lookup"><span data-stu-id="22656-110">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) to integrate the Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="22656-111">Depois de fazer isso, seu método `OnCreate` será semelhante ao seguinte.</span><span class="sxs-lookup"><span data-stu-id="22656-111">Once you do that, your `OnCreate` method will look like the following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="22656-112">Agora, verifique se seu aplicativo híbrido tem uma tela com WebView.</span><span class="sxs-lookup"><span data-stu-id="22656-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="22656-113">O código para ele será semelhante ao que se segue, em que estamos carregando um arquivo HTML local **Sample.html** no Webview no método `onCreate` da sua tela.</span><span class="sxs-lookup"><span data-stu-id="22656-113">The code for it will be similar to the following where we are loading a local HTML file **Sample.html** in the Webview in the `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="22656-114">Agora crie um arquivo de ponte chamado **WebAppInterface** que cria um wrapper sobre alguns métodos comumente usados do SDK do Mobile Engagement Android usando a abordagem `@JavascriptInterface` descrita na [Documentação do Android](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="22656-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using the `@JavascriptInterface` approach described in the [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate the interface and set the context */
            WebAppInterface(Context c) {
                mContext = c;
            }
   
            @JavascriptInterface
            public void sendEngagementEvent(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendEvent(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void startEngagementJob(String name, String extras ){
                EngagementAgent.getInstance(mContext).startJob(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void endEngagementJob(String name){
                EngagementAgent.getInstance(mContext).endJob(name);
            }
   
            @JavascriptInterface
            public void sendEngagementError(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendError(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void sendEngagementAppInfo(String appInfo){
                EngagementAgent.getInstance(mContext).sendAppInfo(ParseExtras(appInfo));
            }
   
            public Bundle ParseExtras(String input) {
                Bundle extras = new Bundle();
   
                try {
                    JSONObject jObject = new JSONObject(input);
                    extras.putString(jObject.names().getString(0),
                            jObject.get(jObject.names().getString(0)).toString());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return extras;
            }
        }  
4. <span data-ttu-id="22656-115">Após criar o arquivo de ponte acima, precisamos garantir que ele esteja associado ao nosso Webview.</span><span class="sxs-lookup"><span data-stu-id="22656-115">Once we have created the above bridge file, we need to ensure that it is associated with our Webview.</span></span> <span data-ttu-id="22656-116">Para que isso aconteça, você precisa editar o método `SetWebview` para que ele se pareça com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="22656-116">For this to happen, you need to edit your `SetWebview` method so that it looks like the following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="22656-117">No trecho acima, chamamos `addJavascriptInterface` para associar a nossa classe de ponte ao nosso Webview e também criamos um identificador chamado **EngagementJs** para chamar os métodos do arquivo de ponte.</span><span class="sxs-lookup"><span data-stu-id="22656-117">In the above snippet, we called `addJavascriptInterface` to associate our bridge class with our Webview and also created a handle called **EngagementJs** to call the methods from the bridge file.</span></span> 
6. <span data-ttu-id="22656-118">Agora, crie o arquivo a seguir chamado **Sample.html** em seu projeto em uma pasta chamada **ativos** que é carregada no Webview e onde poderemos chamar os métodos a partir do arquivo de ponte.</span><span class="sxs-lookup"><span data-stu-id="22656-118">Now create the following file called **Sample.html** in your project in a folder called **assets** which is loaded into the Webview and where we will call the methods from the bridge file.</span></span>
   
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
                      log('window.onerror: ' + err);
                    }
   
                    send = function(inputId)
                    {
                        var input = document.getElementById(inputId);
                        if(input)
                        {
                            var value = input.value;
                            // Example of how extras info can be passed with the Engagement logs
                            var extras = '{"CustomerId":"MS290011"}';
   
                            if(value && value.length > 0)
                            {
                                switch(inputId)
                                {
                                    case "event":
                                    EngagementJs.sendEngagementEvent(value, extras);
                                    break;
   
                                    case "job":
                                    EngagementJs.startEngagementJob(value, extras);
                                    window.setTimeout( function()
                                    {
                                      EngagementJs.endEngagementJob(value);
                                    }, 10000 );
                                    break;
   
                                    case "error":
                                    EngagementJs.sendEngagementError(value, extras);
                                    break;
   
                                    case "appInfo":
                                    EngagementJs.sendEngagementAppInfo({"customer_name":value});
                                    break;
                                }
                            }
                        }
                    }
                </script>
            </head>
            <body>
                <h1>Bridge Tester</h1>
                <div id='engagement'>
                    <h2>Event</h2>
                    <input type="text" id="event" size="35">
                    <button onclick="send('event')">Send</button>
   
                    <h2>Job</h2>
                    <input type="text" id="job" size="35">
                    <button onclick="send('job')">Send</button>
   
                    <h2>Error</h2>
                    <input type="text" id="error" size="35">
                    <button onclick="send('error')">Send</button>
   
                    <h2>AppInfo</h2>
                    <input type="text" id="appInfo" size="35">
                    <button onclick="send('appInfo')">Send</button>
                </div>
            </body>
        </html>
7. <span data-ttu-id="22656-119">Observe os seguintes pontos sobre o arquivo HTML acima:</span><span class="sxs-lookup"><span data-stu-id="22656-119">Note the following points about the HTML file above:</span></span>
   
   * <span data-ttu-id="22656-120">Ele contém um conjunto de caixas de entrada onde você pode fornecer dados a serem usados como nomes de Evento, Erro, Trabalho, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="22656-120">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="22656-121">Quando você clica no botão ao lado dele, é feita uma chamada para o Javascript que eventualmente chama os métodos do arquivo de ponte para passar essa chamada para o SDK do Mobile Engagement Android.</span><span class="sxs-lookup"><span data-stu-id="22656-121">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="22656-122">Estamos marcando algumas informações estáticas adicionais nos eventos, nos trabalhos e até mesmo nos erros para demonstrar como isso pode ser feito.</span><span class="sxs-lookup"><span data-stu-id="22656-122">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="22656-123">Essa informação adicional é enviada como uma cadeia de caracteres JSON que, se você olhar o arquivo `WebAppInterface`, é analisada, colocada em um Android `Bundle` e passada juntamente com envios de Eventos, Trabalhos, Erros.</span><span class="sxs-lookup"><span data-stu-id="22656-123">This extra info is sent as a JSON string which, if you look in the `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="22656-124">O Trabalho do Mobile Engagement é inicializado com o nome que você especifica na caixa de entrada, executado por 10 segundos e, em seguida, desligado.</span><span class="sxs-lookup"><span data-stu-id="22656-124">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="22656-125">Um appinfo ou marca do Mobile Engagement é passada com “customer_name” como a chave estática e com o valor que você inseriu na entrada como o valor da marca.</span><span class="sxs-lookup"><span data-stu-id="22656-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
8. <span data-ttu-id="22656-126">Execute o aplicativo e você verá o seguinte:</span><span class="sxs-lookup"><span data-stu-id="22656-126">Run the app and you will see the following.</span></span> <span data-ttu-id="22656-127">Agora, forneça um nome para um evento de teste conforme mostrado a seguir e clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="22656-127">Now provide some name for a test event like the following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="22656-128">Agora, se você acessar a guia **Monitor** do aplicativo e procurar em **Eventos -> Detalhes**, verá esse evento aparecer junto ao app-info estático que estamos enviando.</span><span class="sxs-lookup"><span data-stu-id="22656-128">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
