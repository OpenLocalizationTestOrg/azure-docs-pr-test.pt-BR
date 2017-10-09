---
title: "aaaWindows integração do SDK do contrato Phone Silverlight"
description: Como tooIntegrate Azure Mobile Engagement com aplicativos do Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a>Integração do SDK do Windows Phone Silverlight para o Engagement
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Este procedimento descreve hello mais simples maneira tooactivate do Azure Mobile Engagement análise e monitoramento de funções em seu aplicativo do Windows Phone Silverlight.

Olá, as etapas a seguir é que suficientes relatório de saudação tooactivate dos logs necessário toocompute todas as estatísticas sobre usuários, sessões, atividades, falhas e Technicals. Olá relatório dos logs necessário toocompute outras estatísticas como trabalhos, erros e eventos devem ser feitos manualmente usando Olá contrato de API (consulte [como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo do Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) abaixo) desde que essas estatísticas são dependentes do aplicativo.

## <a name="supported-versions"></a>Versões com suporte
Olá Mobile Engagement SDK para Windows Silverlight somente pode ser integrado em aplicativos voltados para:

* Windows Phone 8.0
* Windows Phone 8.1 Silverlight

> [!NOTE]
> Se você tiver como alvo o Windows Phone 8.1 (não Silverlight), consulte toohello [procedimento de integração Universal do Windows](mobile-engagement-windows-store-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a>Instalar Olá Silverlight SDK do Mobile Engagement
Olá Mobile Engagement SDK para Windows Silverlight está disponível como um pacote do Nuget chamado *MicrosoftAzure.MobileEngagement*. Você pode instalá-lo de saudação Nuget Package Manager do Visual Studio. 

## <a name="add-hello-capabilities"></a>Adicionar recursos de saudação
Olá contrato SDK precisa de alguns recursos de saudação do Windows Phone Silverlight SDK em ordem toowork corretamente.

Abra o `WMAppManifest.xml` de arquivos e certifique-se de que Olá recursos a seguir são declarados no hello `Capabilities` painel:

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a>Inicializar Olá contrato SDK
### <a name="engagement-configuration"></a>Configuração do Engagement
configuração do contrato de saudação é centralizada em Olá `Resources\EngagementConfiguration.xml` arquivo do projeto.

Edite esse arquivo toospecify:

* A cadeia de conexão do aplicativo entre as marcas `<connectionString>` and `<\connectionString>`.

Se você quiser toospecify em tempo de execução em vez disso, você pode chamar a seguir Olá método antes da inicialização de agente do hello contrato:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

cadeia de caracteres de conexão de saudação para seu aplicativo é exibida em Olá Portal clássico do Azure.

### <a name="engagement-initialization"></a>Inicialização do Engagement
Quando você cria um novo projeto, um arquivo `App.xaml.cs` é gerado. Essa classe herda de `Application` e contém vários métodos importantes. Ele também será usado tooinitialize Olá SDK do contrato.

Modificar Olá `App.xaml.cs`:

* Adicionar tooyour `using` instruções:
  
      using Microsoft.Azure.Engagement;
* Inserir `EngagementAgent.Instance.Init` em Olá `Application_Launching` método:
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* Inserir `EngagementAgent.Instance.OnActivated` em Olá `Application_Activated` método:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> Altamente Desencorajamos você tooadd Olá contrato inicialização em outro lugar do seu aplicativo. No entanto, lembre-se que Olá `EngagementAgent.Instance.Init` método é executado em um thread dedicado e não Olá thread de interface do usuário.
> 
> 

## <a name="basic-reporting"></a>Relatórios básicos
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a>Método recomendado: sobrecarregar suas classes `PhoneApplicationPage`
No relatório de saudação tooactivate de ordem de todos os logs de saudação exigido pelo contrato toocompute usuários, sessões, atividades, falhas e estatísticas técnicas, você pode simplesmente fazer todas as suas `PhoneApplicationPage` subclasses herdam Olá `EngagementPage` classes.

Aqui está um exemplo de como toodo isso para uma página do seu aplicativo. Você pode fazer Olá igual para todas as páginas do seu aplicativo.

#### <a name="c-source-file"></a>Arquivo de código-fonte C#
Modifique o arquivo `.xaml.cs` de paginação :

* Adicionar tooyour `using` instruções:
  
      using Microsoft.Azure.Engagement;
* Substituir `PhoneApplicationPage` por `EngagementPage` :

**Sem o Engagement:**

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

**Com o Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> Se sua página herda de saudação `OnNavigatedTo` método, seja cuidadoso toolet Olá `base.OnNavigatedTo(e)` chamar. Caso contrário, a atividade de saudação não será reportada. Na verdade, Olá `EngagementPage` está chamando `StartActivity` dentro Olá `OnNavigatedTo` método.
> 
> 

#### <a name="xaml-file"></a>Arquivo XAML
Modifique o arquivo `.xaml` de paginação :

* Adicione declarações de namespaces tooyour:
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* Substituir `phone:PhoneApplicationPage` por `engagement:EngagementPage` :

**Sem o Engagement:**

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

**Com o Engagement:**

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a>Substituir o comportamento padrão de saudação
Por padrão, nome de classe de saudação da página de Olá será relatado como nome da atividade hello, com e sem extras. Se a classe Olá usa Olá sufixo "Página", o contrato também removê-la.

Se você quiser comportamento do toooverride saudação padrão para nome hello, basta adicione este código tooyour:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

Se você quiser tooreport informações extras com sua atividade, você pode adicionar esse código tooyour:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

Esses métodos são chamados de dentro de saudação `OnNavigatedTo` método da página.

### <a name="alternate-method-call-startactivity-manually"></a>Método alternativo: chame `StartActivity()` manualmente
Se você não pode ou não toooverload seu `PhoneApplicationPage` classes, em vez disso, você pode iniciar suas atividades chamando `EngagementAgent` métodos diretamente.

Recomendamos chamar `StartActivity` dentro do método `OnNavigatedTo` da sua PhoneApplicationPage.

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> Certifique-se de encerrar a sua sessão corretamente.
> 
> Olá SDK chama automaticamente Olá `EndActivity` método quando o aplicativo hello está fechado. Portanto, é **altamente** recomendado Olá toocall `StartActivity` sempre que alterar a atividade de saudação do usuário Olá e muito**nunca** chamada hello `EndActivity` método. Esse método envia um servidor de contrato de toohello mensagens que o usuário atual Olá saiu aplicativo hello e isso afeta todos os logs de aplicativo.
> 
> 

## <a name="advanced-reporting"></a>Relatórios avançados
Opcionalmente, convém tooreport eventos específicos do aplicativo, erros e trabalhos, toodo assim, use Olá outros métodos encontrados no hello `EngagementAgent` classe. Olá contrato de API permite que toouse todos os recursos avançados do contrato.

Para obter mais informações, consulte [como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo do Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).

## <a name="advanced-configuration"></a>Configuração avançada
### <a name="disable-automatic-crash-reporting"></a>Desabilitar o relatório de falhas automático
Você pode desabilitar o recurso de contrato de relatório de falha automático do hello. Então, quando uma exceção não tratada ocorrer, o Engagement não fará nada.

> [!WARNING]
> Se você planejar toodisable esse recurso, lembre-se de que, quando uma falha sem tratamento ocorrerá em seu aplicativo, contrato não enviará falha Olá **AND** não fechará sessão hello e trabalhos.
> 
> 

Falha automático de toodisable reporting, apenas personalizar a configuração dependendo da maneira Olá você declarado:

#### <a name="from-engagementconfigurationxml-file"></a>No arquivo `EngagementConfiguration.xml`
Definir o relatório de falhas muito`false` entre `<reportCrash>` e `</reportCrash>` marcas.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>No objeto `EngagementConfiguration` em tempo de execução
Definir toofalse de falha de relatório usando o objeto EngagementConfiguration.

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Modo intermitente
Por padrão, os relatórios de serviço de contrato de saudação logs em tempo real. Se seu aplicativo relatórios logs com muita frequência, é melhor toobuffer Olá logs e tooreport-los todos de uma vez em um base de tempo regulares (Isso é chamado hello "modo de disparo").

toodo assim, chame o método hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Olá argumento for um valor em **milissegundos**. A qualquer momento, se desejar que o log em tempo real do tooreactivate hello, apenas chame método de saudação sem nenhum parâmetro, ou com valor de saudação 0.

Olá modo intermitente ligeiramente aumentar bateria Olá vida mas tem um impacto em Olá contrato Monitor: todas as sessões e trabalhos a duração será arredondado toohello intermitência limite (portanto, sessões e menor do que o limite de disparo Olá pode não estar visível de trabalhos). É recomendável toouse um limite de disparo não mais que 30000 (30 s). Você tem toobe reconhece que salva os logs são itens too300 limitado. Se o envio for muito longo, você poderá perder alguns logs.

> [!WARNING]
> Olá limite de disparo não pode ser configurado tooa período menor que um segundo. Se você tentar toodo, portanto, Olá SDK mostrará um rastreamento com o erro hello e será automaticamente redefinir valor padrão de toohello, isto é, zero segundos. Isso vai disparar Olá SDK tooreport Olá logs em tempo real.
> 
> 

