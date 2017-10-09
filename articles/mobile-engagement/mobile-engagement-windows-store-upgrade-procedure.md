---
title: "aaaWindows procedimentos de atualização do SDK de aplicativos Universal"
description: "Procedimentos de atualização do SDK do Windows Universal para o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a>Procedimentos de atualização de aplicativos do Windows Universal
Se você já tiver integrado uma versão mais antiga do contrato em seu aplicativo, você tem Olá tooconsider pontos a seguir ao atualizar Olá SDK.

Você pode ter vários procedimentos de toofollow se perdidas várias versões do SDK de saudação. Por exemplo, se você migrar de 0.10.1 too0.11.0 ter toofirst siga hello "de 0.9.0 too0.10.1" procedimento e hello "de 0.10.1 too0.11.0" procedimento.

## <a name="from-330-too340"></a>De 3.3.0 too3.4.0
### <a name="test-logs"></a>Logs de teste
Logs do console produzidos pelo Olá SDK agora podem ser habilitado/desabilitado/filtradas. toocustomize, propriedade de saudação update `EngagementAgent.Instance.TestLogEnabled` tooone do valor de saudação disponível de saudação `EngagementTestLogLevel` enumeração, por exemplo:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a>Recursos
sobreposição de alcance Olá foi aprimorada. Ele faz parte dos recursos de pacote do NuGet do SDK hello.

Durante a atualização toohello nova versão de hello SDK, você pode escolher que se deseja tookeep os arquivos existentes do hello sobreposição de pasta de seus recursos ou não:

* Se sobreposição anterior hello está funcionando para você ou você estiver integrando Olá `WebView` elementos manualmente e em seguida, você pode decidir tookeep os arquivos existentes, continuará a funcionar. 
* Se você quiser tooupdate toohello nova sobreposição, substituir apenas Olá todo `overlay` pasta de seus recursos com hello um novo pacote do SDK de saudação (aplicativos UWP: após a atualização de hello, você pode obter nova pasta de sobreposição de saudação do % USERPROFILE %\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Usando a sobreposição de novo Olá substituirá todas as personalizações feitas na versão anterior do hello.
> 
> 

## <a name="from-320-too330"></a>De 3.2.0 too3.3.0
### <a name="resources"></a>Recursos
Esta etapa aborda apenas os recursos personalizados. Se você tiver personalizado o recursos de Olá fornecidos por Olá SDK (html, imagens, sobreposição), você terá que toobackup-los antes de atualizar e reaplicar a personalização em atualizado recursos.

## <a name="from-310-too320"></a>De 3.1.0 too3.2.0
### <a name="resources"></a>Recursos
Esta etapa aborda apenas os recursos personalizados. Se você tiver personalizado o recursos de Olá fornecidos por Olá SDK (html, imagens, sobreposição), você terá que toobackup-los antes de atualizar e reaplicar a personalização em atualizado recursos.

### <a name="webview-integration"></a>Integração do Modo de exibição da Web
Algumas melhorias toomatch diferentes fatores foram introduzidos nesta versão. Certifique-se de que a integração do webview Olá corresponde seguinte Olá:

Na página XAML ():

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

E no arquivo .cs associado:

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a>De 2.0.0 too3.0.0
### <a name="resources"></a>Recursos
Esta etapa aborda apenas os recursos personalizados. Se você tiver personalizado o recursos de Olá fornecidos por Olá SDK (html, imagens, sobreposição), você terá que toobackup-los antes de atualizar e reaplicar a personalização em atualizado recursos.

## <a name="from-111-too200"></a>De 1.1.1 too2.0.0
Olá a seguir descrevem como toomigrate uma integração SDK da saudação Capptain serviço oferecido pelo Capptain SAS em um aplicativo da plataforma do Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain e o compromisso de mobilidade não são Olá mesmos serviços e procedimento Olá indicado abaixo só destaca como toomigrate Olá aplicativo cliente. Migrando Olá SDK no aplicativo hello não vai migrar seus dados do hello Capptain toohello Mobile Engagement de servidores
> 
> 

Se você estiver migrando de uma versão anterior, consulte Olá Capptain site da web toomigrate too1.1.1 primeiro e aplicar Olá procedimento

### <a name="nuget-package"></a>Pacote NuGet
Substitua **Capptain.WindowsPhone** pelo pacote Nuget **MicrosoftAzure.MobileEngagement**.

### <a name="applying-mobile-engagement"></a>Aplicando o Mobile Engagement
Olá SDK usa o termo Olá `Engagement`. Você precisa tooupdate toomatch seu projeto essa alteração.

É necessário toouninstall seu pacote do nuget Capptain atual. Considere que todas as alterações na pasta de recursos Capptain serão removidas. Se você quiser tookeep esses arquivos, em seguida, faça uma cópia deles.

Depois disso, instale o novo pacote de nuget de contrato do Microsoft Azure Olá no seu projeto. Você pode encontrá-lo diretamente no [site do nuget]. ou aqui no índice. Substitui essa ação, todos os arquivos de recursos usado pelo contrato e adiciona Olá novo contrato DLL tooyour referências de projeto.

Você tem as referências do projeto tooclean excluindo referências Capptain DLL. Se você não fizer isso, versão de saudação do Capptain entrarão em conflito e ocorrerão erros.

Se você tiver personalizado Capptain recursos, copie o conteúdo de arquivos antigos e colá-los em novos arquivos de contrato hello. Observe que os arquivos xaml e o cs toobe atualizado.

Quando essas etapas forem concluídas, você só tem referências antigas de Capptain tooreplace por novas referências de contrato hello.

1. Todos os namespaces Capptain ter toobe atualizado.
   
    Antes da migração:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Após a migração:
   
        using Microsoft.Azure.Engagement;
2. Todas as classes Capptain que contêm "Capptain" devem conter “Engagement".
   
    Antes da migração:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Após a migração:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. Para os arquivos xaml o namespace e atributos Capptain também se alteram.
   
    Antes da migração:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Após a migração:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Alterações na página de sobreposição
   
   > [!IMPORTANT]
   > A sobreposição também será alterada. O novo namespace é `Microsoft.Azure.Engagement.Overlay`. Ele tem toobe usado nos arquivos xaml e o cs. Além disso `CapptainGrid` toobe chamado `EngagementGrid`, `capptain_notification_content` e `capptain_announcement_content` são nomeados `engagement_notification_content` e `engagement_announcement_content`.
   > 
   > 
   
    Para sobreposição:
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    Torna-se:
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. Para Olá a outros recursos como Capptain imagens e arquivos HTML, observe que eles foram renomeado toouse "Contrato".

### <a name="project-declaration"></a>Declaração do projeto
Em Package.appxmanifest `File Type Associations` foi atualizado a partir de:

* capptain\_alcançar\_tooengagement conteúdo\_alcançar\_conteúdo
* capptain\_log\_arquivo tooengagement\_log\_arquivo

### <a name="application-id--sdk-key"></a>ID do aplicativo / chave do SDK
O Engagement usa uma cadeia de conexão. Você não tem toospecify uma ID de aplicativo e uma chave do SDK com o Mobile Engagement, tiver apenas toospecify uma cadeia de caracteres de conexão. Você pode configurá-la em seu arquivo EngagementConfiguration.

configuração do contrato Olá pode ser definida em sua `Resources\EngagementConfiguration.xml` arquivo do projeto.

Edite esse arquivo toospecify:

* A cadeia de conexão do aplicativo entre as marcas `<connectionString>` and `<\connectionString>`.

Se você quiser toospecify em tempo de execução em vez disso, você pode chamar a seguir Olá método antes da inicialização de agente do hello contrato:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

cadeia de caracteres de conexão de saudação para seu aplicativo é exibida em Olá Portal clássico do Azure.

### <a name="items-name-change"></a>Alteração do nome de itens
Todos os itens chamados *capptain* foram nomeados como *engagement*. Da mesma forma para *Capptain* muito*contrato*.

Exemplos de itens do Capptain usados normalmente :

* CapptainConfiguration agora denominado EngagementConfiguration
* CapptainAgent agora denominado EngagementAgent
* CapptainReach agora denominado EngagementReach
* CapptainHttpConfig agora denominado EngagementHttpConfig
* GetCapptainPageName agora denominado GetEngagementPageName

Observe que renomear também afeta métodos substituídos.

