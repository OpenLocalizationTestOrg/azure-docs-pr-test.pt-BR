---
title: "aaaWindows Phone Silverlight alcançar SDK integração"
description: Como tooIntegrate do Azure Mobile Engagement atingir com aplicativos do Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a>Integração do SDK do Windows Phone Silverlight para o Reach
Você deve seguir Olá integração procedimento descrito em Olá [integração do SDK do Windows Phone Silverlight contrato](mobile-engagement-windows-phone-integrate-engagement.md) antes de seguir este guia.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a>Inserir saudação SDK do Reach contrato em seu projeto do Windows Phone Silverlight
Você não tem nada tooadd. `EngagementReach` já estão em seu projeto.

> [!TIP]
> Você poderá personalizar as imagens localizadas em Olá `Resources` pasta do seu projeto, especialmente Olá marca ícone (esse padrão toohello contrato).
> 
> 

## <a name="add-hello-capabilities"></a>Adicionar recursos de saudação
Olá SDK do Reach contrato precisa de alguns recursos adicionais.

Abra sua `WMAppManifest.xml` de arquivo e certifique-se de que Olá recursos a seguir são declarados:

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

Olá primeiro um é usado pela exibição de saudação de tooallow Olá MPNS serviço de notificação do sistema. Olá, um segundo é usado tooembed uma tarefa de navegador em Olá SDK.

Editar saudação `WMAppManifest.xml` de arquivos e adicionar dentro Olá `<Capabilities />` marca:

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a>Habilitar Olá Microsoft Push Notification Service
Na saudação de toouse ordem **Microsoft Push Notification Service** (conhecido como MPNS) seu `WMAppManifest.xml` arquivo deve ter uma `<App />` marca com um `Publisher` atributo definido toohello nome do seu projeto.

## <a name="initialize-hello-engagement-reach-sdk"></a>Inicializar Olá contrato SDK do Reach
### <a name="engagement-configuration"></a>Configuração do Engagement
configuração do contrato de saudação é centralizada em Olá `Resources\EngagementConfiguration.xml` arquivo do projeto.

Edite essa configuração do arquivo toospecify alcance:

* *Opcional*, indique se o push nativo da saudação (MPNS) está ativado ou não entre `<enableNativePush>` e `</enableNativePush>` marcas, (`true` por padrão).
* *Opcional*, indicar o nome de saudação do canal de envio de saudação entre `<channelName>` e `</channelName>` marcas, forneça Olá mesmo que seu aplicativo pode usar ou deixe-o vazio no momento.

Se você quiser toospecify em tempo de execução em vez disso, você pode chamar a seguir Olá método antes da inicialização de agente do hello contrato:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> Você pode especificar o nome de saudação do canal de push MPNS saudação do seu aplicativo. Por padrão, o contrato cria um nome com base no appId hello. Você não têm necessidade toospecify Olá nome por conta própria, exceto se você estiver planejando canal de push Olá toouse fora do contrato.
> 
> 

### <a name="engagement-initialization"></a>Inicialização do Engagement
Modificar Olá `App.xaml.cs`:

* Adicionar tooyour `using` instruções:
  
      using Microsoft.Azure.Engagement;
* Insira `EngagementReach.Instance.Init` logo após `EngagementAgent.Instance.Init` e `Application_Launching` :
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* Inserir `EngagementReach.Instance.OnActivated` em Olá `Application_Activated` método:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> Olá `EngagementReach.Instance.Init` é executado em um thread dedicado. Você não tem toodo-lo por conta própria.
> 
> 

## <a name="app-store-submission-considerations"></a>Considerações de envio de armazenamento de aplicativo
Microsoft impõe algumas regras ao usar notificações por push de saudação:

De saudação Microsoft [políticas de aplicativo] documentação, seção 2.9:

1) Você deve pedir notificações por push do hello usuário tooaccept tooreceive. Em seguida, em suas configurações, adicione notificações de push uma maneira toodisable hello.

Olá EngagementReach fornece dois métodos toomanage Olá aceitar-em/Recusar, `EnableNativePush()` e `DisableNativePush()`. Por exemplo, pode criar uma opção nas configurações de saudação com uma alternância toodisable ou habilitar MPNS.

Você também pode decidir toodeactivate MPNS por meio da configuração de contrato Olá\<windows phone-sdk-alcance-configuração\>.

> 2.9.1) aplicativo hello primeiro deve descrever Olá notificações toobe fornecido e **obter permissão expressa e do usuário da saudação (opt-in)**, e **deve fornecer um mecanismo pelo qual Olá usuário pode recusar recebimento notificações por push**. Todas as notificações fornecidas usando Olá Microsoft Push Notification Service deve ser consistentes com hello descrição fornecida toohello usuário e deve estar em conformidade com todos os aplicável [políticas de aplicativo] [ Content Policies]e [requisitos adicionais para tipos específicos de aplicativo].
> 
> 

2) Você não deve usar muitas notificações por push. O Engagement manipulará notificações para você.

> 2.9.2) aplicativo hello e seu uso da saudação Microsoft Push Notification Service não excessivamente use capacidade de rede ou de largura de banda de saudação Microsoft Push Notification Service, ou caso contrário indevidamente sobrecarregam um Windows Phone ou outro dispositivo da Microsoft ou o serviço com excessiva por push de notificações, conforme determinado pela Microsoft a seu critério e não deve danificar ou interferir com redes Microsoft ou servidores ou servidores de terceiros ou redes conectadas toohello Microsoft Push Notification Service.
> 
> 

3) Não confie em informações de criticals toosend MPNS. Contrato usa MPNS, portanto, esta regra também se aplica para campanhas Olá criadas dentro de saudação contrato front-end.

> 2.9.3) Olá Microsoft Push Notification Service não pode ser usado toosend notificações que são de missão crítica ou não poderia afetar assuntos de vida ou morte, incluindo, sem dispositivo médico da limitação notificações críticas tooa relacionados ou condição. MICROSOFT expressamente se isenta de qualquer garantia que Olá uso de hello MICROSOFT PUSH notificação serviço ou entrega de MICROSOFT PUSH notificação serviço notificações serão ser ININTERRUPTAS, livre de erro, ou caso contrário garantido tooOCCUR ON A real-time base.
> 
> 

**Não podemos garantir que seu aplicativo passará o processo de validação Olá se você não respeitam essas recomendações.**

## <a name="handle-data-push-optional"></a>Manipular o push de dados (opcional)
Se você quiser envios por push os aplicativo toobe tooreceive capaz de alcançar dados, você tem tooimplement dois eventos de saudação EngagementReach classe:

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

Em seguida, defina o conteúdo de saudação do hello `EngagementReach.Instance.Handler` campo com seu objeto personalizado no seu `App.xaml.cs` classe dentro Olá `Application_Launching` método.

**Exemplo de código :**

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> Por padrão, o Engagement usa a sua própria implementação de `EngagementReachHandler`. Você não tem toocreate seus próprios, e se você fizer isso, você não tem toooverride cada método. comportamento padrão de saudação é o objeto base do contrato tooselect hello.
> 
> 

### <a name="layouts"></a>Layouts
Por padrão, o alcance usará recursos de saudação inserido de notificações de Olá Olá DLL toodisplay e páginas.

No entanto, você pode decidir toouse tooreflect seus próprios recursos sua marca nesses componentes.

Você pode substituir `EngagementReachHandler` métodos no seu toouse de contrato subclasse tootell seus layouts:

**Exemplo de código :**

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> Olá `CreateNotification` método pode retornar nulo. notificação de saudação não será exibida e campanha de alcance hello será descartada.
> 
> 

toosimplify sua implementação de layout, nós também fornecemos nossa própria xaml que pode servir como base para seu código. Eles estão localizados no arquivo de projeto SDK hello (/ src alcance /).

> [!WARNING]
> fontes de saudação que fornecemos são Olá exata que mesmo que usamos. Portanto toomodify-los diretamente, não esqueça toochange Olá namespace e Olá nome.
> 
> 

### <a name="notification-position"></a>Posição de notificação
Por padrão, uma notificação no aplicativo é exibida no lado Olá inferior esquerdo do aplicativo hello. Você pode alterar esse comportamento, substituindo Olá `GetNotificationPosition` método hello `EngagementReachHandler` objeto.

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

No momento, você pode escolher entre hello `BOTTOM` (padrão) e `TOP` posições.

### <a name="launch-message"></a>Iniciar mensagem
Quando um usuário clica em um sistema de notificação (uma notificação do sistema), inicia contrato Olá aplicativo, conteúdo de saudação do carregamento de saudação por push as mensagens e exibir página Olá Olá correspondente campanha.

Há um atraso entre a inicialização de saudação da exibição de aplicativo e Olá Olá da página de saudação (dependendo da velocidade da saudação da sua rede).

tooindicate toohello o usuário que algo está sendo carregado, você deve fornecer uma informações visuais, como uma barra de progresso ou um indicador de progresso. O Engagement não pode manipular isto por conta própria, mas oferece alguns manipuladores para você.

tooimplement Olá retorno de chamada, execute:

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

Você pode definir o retorno de chamada de saudação seu `Application_Launching` método de sua `App.xaml.cs` arquivos, preferencialmente antes Olá `EngagementReach.Instance.Init()` chamar.

> [!TIP]
> Cada manipulador é chamado pelo Olá Thread de interface do usuário. Você não tem tooworry ao usar uma MessageBox ou algo relacionados à interface do usuário.
> 
> 

[políticas de aplicativo]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[requisitos adicionais para tipos específicos de aplicativo]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

