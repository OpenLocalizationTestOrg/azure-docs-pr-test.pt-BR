---
title: "aaaWindows alcançar integração para o SDK do Universal aplicativos"
description: Como tooIntegrate do Azure Mobile Engagement atingir com aplicativos universais do Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a>Integração do SDK do Reach do Windows Universal
Você deve seguir Olá integração procedimento descrito em Olá [integração do SDK do Windows Universal contrato](mobile-engagement-windows-store-integrate-engagement.md) antes de seguir este guia.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a>Inserir saudação SDK do Reach contrato em seu projeto Universal do Windows
Você não tem nada tooadd. `EngagementReach` já estão em seu projeto.

> [!TIP]
> Você poderá personalizar as imagens localizadas em Olá `Resources` pasta do seu projeto, especialmente Olá marca ícone (esse padrão toohello contrato). Em aplicativos Universal, você também pode mover Olá `Resources` pasta no seu tooshare projeto compartilhado seu conteúdo entre aplicativos, mas você terá Olá tookeep `Resources\EngagementConfiguration.xml` em seu local padrão de arquivo à medida que é dependente de plataforma.
> 
> 

## <a name="enable-hello-windows-notification-service"></a>Habilitar Olá serviço de notificação do Windows
### <a name="windows-8x-and-windows-phone-81-only"></a>Somente Windows 8.x e Windows Phone 8.1
Na saudação de toouse ordem **serviço de notificação do Windows** (conhecido como WNS) em sua `Package.appxmanifest` de arquivo no `Application UI` clique em `All Image Assets` na caixa de bot esquerdo hello. A saudação à direita da caixa de saudação em `Notifications`, alterar `toast capable` de `(not set)` muito`(Yes)`.

### <a name="all-platforms"></a>Todas as plataformas
É necessário toosynchronize seu aplicativo tooyour conta e toohello contrato plataforma Microsoft. Para isso você precisa toocreate uma conta ou logon [Centro de desenvolvimento do windows](https://dev.windows.com). Depois que criar um novo aplicativo e localizar Olá SID e a chave secreta. Em Olá contrato front-end, vá em sua configuração de aplicativo em `native push` e cole as suas credenciais. Depois disso, clique com botão direito no projeto, selecione `store` e `Associate App with hello Store...`. Você precisa apenas o aplicativo de hello tooselect ter criá antes de toosynchronize-lo.

## <a name="initialize-hello-engagement-reach-sdk"></a>Inicializar Olá contrato SDK do Reach
Modificar Olá `App.xaml.cs`:

* Insira `EngagementReach.Instance.Init` logo após `EngagementAgent.Instance.Init` no método `InitEngagement`:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  Olá `EngagementReach.Instance.Init` é executado em um thread dedicado. Você não tem toodo-lo por conta própria.

> [!NOTE]
> Se você estiver usando notificações por push em outro lugar no seu aplicativo, você tem muito[compartilhar seu canal push](#push-channel-sharing) com contrato alcançar.
> 
> 

## <a name="integration"></a>Integração
Contrato fornece exibições intersticiais e as faixas duas maneiras tooadd Olá alcance no aplicativo para notificações e pesquisas em seu aplicativo: Olá sobreposição de integração e integração manual do Olá web modos de exibição. Você não deve combinar ambas as abordagem Olá mesma página.

Escolha Olá entre integração dois Olá podia ser resumida desta forma:

* Você pode escolher Olá sobreposição integração se já herda a suas páginas de saudação agente `EngagementPage`, é simplesmente uma questão de substituição `EngagementPage` por `EngagementPageOverlay` e `xmlns:engagement="using:Microsoft.Azure.Engagement"` por `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` nas suas páginas.
* Você pode optar integração manual do Olá web exibições tooprecisely local Olá alcançar da interface do usuário em suas páginas ou se você não quiser tooadd outro páginas de nível tooyour de herança. 

### <a name="overlay-integration"></a>Integração de sobreposição
sobreposição de contrato Olá dinamicamente adiciona elementos de interface do usuário Olá usados campanhas de alcance toodisplay em sua página. Se Olá sobreposição não é adequado para seu layout considere modos de exibição de web hello integração manual em vez disso.

Em sua alteração de arquivo. XAML `EngagementPage` referência muito`EngagementPageOverlay`

* Adicione declarações de namespaces tooyour:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* Substituir `engagement:EngagementPage` por `engagement:EngagementPageOverlay`:

**Com EngagementPage:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

**Com EngagementPageOverlay:**

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

No seu arquivo .cs, marque a página em `EngagementPageOverlay` em vez de `EngagementPage` e importe `Microsoft.Azure.Engagement.Overlay`.

            using Microsoft.Azure.Engagement.Overlay;

* Substituir `EngagementPage` por `EngagementPageOverlay`:

**Com EngagementPage:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

**Com EngagementPageOverlay:**

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


Olá sobreposição de contrato adiciona um `Grid` elemento na parte superior da página é composto de seu layout e hello dois `WebView` elementos uma saudação banner e Olá outros uma exibição intersticiais hello.

Você pode personalizar elementos de sobreposição de saudação diretamente no hello `EngagementPageOverlay.cs` arquivo.

### <a name="web-views-manual-integration"></a>Integração manual de exibições da Web
Alcance irá procurar as páginas para Olá dois `WebView` elementos responsáveis para exibir a faixa de saudação e exibição intersticiais hello. Olá somente ter toodo é tooadd desses dois `WebView` elementos em algum lugar em suas páginas, aqui está um exemplo:

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


Em Olá Este exemplo `WebView` elementos é toofit ampliada seus contêineres que automaticamente tamanhos-los novamente em caso de alteração de tamanho de rotação ou janela de tela.

> [!WARNING]
> É importante tookeep Olá nomenclatura mesmo `engagement_notification_content` e `engagement_announcement_content` para Olá `WebView` elementos. O Reach os identifica por seu nome. 
> 
> 

## <a name="handle-datapush-optional"></a>Manipular o push de dados (opcional)
Se você quiser envios por push os aplicativo toobe tooreceive capaz de alcançar dados, você tem tooimplement dois eventos de saudação EngagementReach classe:

Em App.xaml.cs no construtor de App() Olá adicione:

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

Você pode ver o retorno de chamada saudação de cada método retorna um valor booleano. Contrato envia um feedback tooits back-end após distribuir dados por push-Olá. Se o retorno de chamada hello retorna false, Olá `exit` comentários será enviado. Caso contrário, ele será `action`. Se nenhum retorno de chamada for definido para eventos de hello, Olá `drop` comentários retornará tooEngagement.

> [!WARNING]
> Contrato não é capaz de tooreceive comentários de múltiplos para um envio de dados. Se você planejar tooset vários manipuladores em um evento, lembre-se de que comentários Olá corresponderá toohello última aquela enviada. Nesse caso, é recomendável tooalways retorna Olá mesmo tooavoid valor ter confuso comentários em Olá front-end.
> 
> 

## <a name="customize-ui-optional"></a>Personalizar a interface do usuário (opcional)
### <a name="first-step"></a>Primeira etapa
Permitir que você alcance de saudação toocustomize da interface do usuário.

toodo assim, você tem toocreate uma subclasse de saudação `EngagementReachHandler` classe.

**Exemplo de código :**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

Em seguida, defina o conteúdo de saudação do hello `EngagementReach.Instance.Handler` campo com seu objeto personalizado no seu `App.xaml.cs` classe dentro Olá `App()` método.

**Exemplo de código :**

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> Por padrão, o Engagement usa a sua própria implementação de `EngagementReachHandler`.
> Você não tem toocreate seus próprios, e se você fizer isso, você não tem toooverride cada método. comportamento padrão de saudação é o objeto base do contrato tooselect hello.
> 
> 

### <a name="web-view"></a>Modo de exibição da Web
Por padrão, o alcance usará recursos de saudação inserido de notificações de Olá Olá DLL toodisplay e páginas.

tooprovide completa possibilidades de personalização só usamos o modo de exibição da web. Se você quiser toocustomize layouts, diretamente substituir arquivos de recursos de saudação `EngagementAnnouncement.html` e `EngagementNotification.html`. Todo o código precisa de contrato `<body></body>` toorun corretamente. Mas você pode adicionar a marca externa `engagement_webview_area`.

No entanto, você pode decidir toouse seus próprios recursos.

Você pode substituir `EngagementReachHandler` métodos em seu toouse de contrato subclasse tootell os layouts, mas levar mecanismo de contrato cuidado tooembedded hello:

**Exemplo de código :**

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


Por padrão, AnnouncementHTML é `ms-appx-web:///Resources/EngagementAnnouncement.html`. Ele representa o arquivo html Olá que cria o conteúdo de saudação de uma mensagem de envio (anúncio de texto, anoucement Web e notificação de sondagem). AnnouncementName é `engagement_announcement_content`. É nome de saudação do design do webview Olá em sua página xaml.

NotfificationHTML é `ms-appx-web:///Resources/EngagementNotification.html`. Ele representa o arquivo html Olá que cria a notificação de saudação de uma mensagem de envio. NotfificationName é `engagement_notification_content`. É nome de saudação do design do webview Olá em sua página xaml.

### <a name="customization"></a>Personalização
Você pode personalizar o modo de exibição da web de notificação e anúncio como desejar se você preservar o objeto Engagement. Lembre-se que objeto webview está descrito três vezes - Olá primeira vez em seu xaml, segundo de tempo em seu arquivo. cs no método de "setwebview()" hello e terceiro tempo no arquivo de html hello.

* O xaml, você descreve Olá layout gráfico webview componente.
* No seu arquivo. cs, você pode definir "setwebview()", na qual você definir a dimensão de saudação do webview dois de saudação (notificação, comunicado). É muito eficiente ao aplicativo hello é redimensionar.
* No arquivo de html do contrato de saudação é descrever Olá webview conteúdo, design e Olá posições de elementos entre si.

### <a name="launch-message"></a>Iniciar mensagem
Quando um usuário clica em um sistema de notificação (uma notificação do sistema), contrato inicia o aplicativo hello, conteúdo de saudação do carregamento de saudação por push as mensagens e exibir página Olá campanha correspondente hello.

Há um atraso entre a inicialização de saudação da exibição de aplicativo e Olá Olá da página de saudação (dependendo da velocidade da saudação da sua rede).

tooindicate toohello o usuário que algo está sendo carregado, você deve fornecer uma informações visuais, como uma barra de progresso ou um indicador de progresso. O Engagement não pode manipular isto por conta própria, mas oferece alguns manipuladores para você.

Adicionar tooimplement Olá retorno de chamada, em App.xaml.cs "App() pública {}":

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

Você pode definir o retorno de chamada de saudação no método "App() pública {}" de seu `App.xaml.cs` arquivos, preferencialmente antes Olá `EngagementReach.Instance.Init()` chamar.

> [!TIP]
> Cada manipulador é chamado pelo Olá Thread de interface do usuário. Você não tem tooworry ao usar uma MessageBox ou algo relacionados à interface do usuário.
> 
> 

## <a id="push-channel-sharing"></a> Enviar o compartilhamento de canal por push
Se você estiver usando notificações por push para outra finalidade em seu aplicativo, em seguida, você tem canal de push Olá toouse recurso de saudação SDK de contrato de compartilhamento. Isso é tooavoid perdido push.

* Você pode fornecer seu próprio push canal toohello contrato alcançar a inicialização. Olá SDK usará em vez de solicitar uma nova.

Olá contrato alcançar inicialização da atualização com o canal de envio no hello `InitEngagement` método da saudação `App.xaml.cs` arquivo:

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* Como alternativa, se você quiser apenas tooconsume Olá por push canal após a inicialização de alcance hello, em seguida, você pode definir um retorno de chamada no canal de push Olá de tooget contrato alcançar depois que ela é criada pelo Olá SDK.

Definir o retorno de chamada em qualquer lugar **depois** Olá inicialização alcance:

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a>Dica de esquema personalizado
Fornecemos o uso de esquema personalizado. Você pode enviar um tipo diferente de URI do contrato toobe de front-end usado em seu aplicativo do compromisso. Um esquema padrão como o `http, ftp, ...` é gerenciados pelo Windows, uma janela será solicitada se não houver aplicativo padrão instalado no dispositivo. Você também pode criar seu próprio esquema personalizado para o aplicativo.

tooset de maneira simples de saudação um esquema personalizado em seu aplicativo é tooopen seu `Package.appxmanifest` vá em `Declarations` painel. Selecione `Protocol` no hello Available Declarations Role caixa e adicioná-lo. Editar saudação `Name` nome de campo com o novo protocolo desejado.

Agora toouse esse protocolo, edite seu `App.xaml.cs` com hello `OnActivated` método e não se esqueça de contrato de tooinitialize aqui também:

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

