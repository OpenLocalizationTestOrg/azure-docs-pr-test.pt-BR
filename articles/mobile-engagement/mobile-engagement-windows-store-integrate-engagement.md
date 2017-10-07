---
title: "aaaWindows integração de SDK do contrato de aplicativos Universal"
description: Como tooIntegrate Azure Mobile Engagement com aplicativos universais do Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a>Integração do SDK do Engagement do Windows Universal
> [!div class="op_single_selector"]
> * [Universal do Windows](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Este procedimento descreve hello mais simples maneira tooactivate contrato análise e monitoramento de funções em seu aplicativo Universal do Windows.

Olá, as etapas a seguir é que suficientes relatório de saudação tooactivate dos logs necessário toocompute todas as estatísticas sobre usuários, sessões, atividades, falhas e Technicals. Olá relatório dos logs necessário toocompute outras estatísticas como trabalhos, erros e eventos devem ser feitos manualmente usando Olá contrato de API (consulte [como toouse Olá avançado marcação API em seu aplicativo Windows Universal do Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md) desde Essas estatísticas são depende do aplicativo.

## <a name="supported-versions"></a>Versões com suporte
Olá Mobile Engagement SDK para aplicativos universais do Windows só pode ser integrado em tempo de execução do Windows e o direcionamento de aplicativos de plataforma Universal do Windows:

* Windows 8
* Windows 8.1
* Windows Phone 8,1
* Windows 10 (famílias para dispositivos móveis e desktop)

> [!NOTE]
> Se você tiver como alvo o Windows Phone Silverlight, consulte toohello [procedimento de integração do Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a>Instalar Olá SDK de aplicativos Universal do Mobile Engagement
### <a name="all-platforms"></a>Todas as plataformas
Olá contrato SDK para Windows Universal aplicativo móvel está disponível como um pacote do Nuget chamado *MicrosoftAzure.MobileEngagement*. Você pode instalá-lo de saudação Nuget Package Manager do Visual Studio.

### <a name="windows-8x-and-windows-phone-81"></a>Windows 8.x e Windows Phone 8.1
NuGet implanta automaticamente os recursos SDK Olá Olá `Resources` pasta raiz de saudação de seu projeto de aplicativo.

### <a name="windows-10-universal-windows-platform-applications"></a>Aplicativos da Plataforma do Windows Universal do Windows 10
O NuGet não implantar automaticamente recursos do SDK Olá em seu aplicativo de UWP ainda. Você tem toodo-la manualmente até a implantação de recursos é reintroduzido no NuGet:

1. Abra o Explorador de Arquivos.
2. Navegue toohello local a seguir (**x.x. x** é a versão de saudação do contrato que você está instalando): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x. x**\\content\win81*
3. Saudação de arrastar e soltar **recursos** pasta na raiz da toohello explorer Olá arquivos do projeto no Visual Studio.
4. No Visual Studio, selecione seu projeto e ativar Olá **Mostrar todos os arquivos** ícone sobre Olá **Gerenciador de soluções**.
5. Alguns arquivos não são incluídos no projeto de saudação. tooimport-los de uma vez clique com botão direito em Olá **recursos** pasta, **excluir do projeto** , em seguida, outro direito do mouse em hello **recursos** pasta, **Include no projeto** toore-incluir toda a pasta hello. Todos os arquivos de saudação **recursos** pasta agora estão incluídas no seu projeto.

## <a name="add-hello-capabilities"></a>Adicionar recursos de saudação
Olá contrato SDK precisa de alguns recursos de saudação SDK do Windows em ordem toowork corretamente.

Abra sua `Package.appxmanifest` de arquivo e certifique-se de que Olá recursos a seguir são declarados:

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a>Inicializar Olá contrato SDK
### <a name="engagement-configuration"></a>Configuração do Engagement
configuração do contrato de saudação é centralizada em Olá `Resources\EngagementConfiguration.xml` arquivo do projeto.

Edite esse arquivo toospecify:

* A cadeia de conexão do aplicativo entre as marcas `<connectionString>` and `<\connectionString>`.

Se você quiser toospecify em tempo de execução em vez disso, você pode chamar a seguir Olá método antes da inicialização de agente do hello contrato:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

cadeia de caracteres de conexão de saudação para seu aplicativo é exibida em Olá Portal clássico do Azure.

### <a name="engagement-initialization"></a>Inicialização do Engagement
Quando você cria um novo projeto, um arquivo `App.xaml.cs` é gerado. Essa classe herda de `Application` e contém vários métodos importantes. Ele também será usado tooinitialize Olá SDK do contrato.

Modificar Olá `App.xaml.cs`:

* Adicionar tooyour `using` instruções:
  
      using Microsoft.Azure.Engagement;
* Defina uma inicialização de contrato do método tooshare Olá uma vez para todas as chamadas:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* Chamar `InitEngagement` em Olá `OnLaunched` método:
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* Quando o aplicativo é iniciado usando um esquema personalizado, em seguida, Olá outra linha de comando do aplicativo ou hello `OnActivated` método é chamado. Você também precisa tooinitiate Olá SDK Engagement quando seu aplicativo é ativado. Assim, substituir toodo `OnActivated` método:
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> Altamente Desencorajamos você tooadd Olá contrato inicialização em outro lugar do seu aplicativo.
> 
> 

## <a name="basic-reporting"></a>Relatórios básicos
### <a name="recommended-method-overload-your-page-classes"></a>Método recomendado: sobrecarregar suas classes `Page`
No relatório de saudação tooactivate de ordem de todos os logs de saudação exigido pelo contrato toocompute usuários, sessões, atividades, falhas e estatísticas técnicas, você pode simplesmente fazer todas as suas `Page` subclasses herdam Olá `EngagementPage` classes.

Aqui está um exemplo de como toodo isso para uma página do seu aplicativo. Você pode fazer Olá igual para todas as páginas do seu aplicativo.

#### <a name="c-source-file"></a>Arquivo de código-fonte C#
Modifique o arquivo `.xaml.cs` de paginação:

* Adicionar tooyour `using` instruções:
  
      using Microsoft.Azure.Engagement;
* Substituir `Page` por `EngagementPage`:

**Sem o Engagement:**

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

**Com o Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> Se sua página substitui Olá `OnNavigatedTo` método, ser toocall se `base.OnNavigatedTo(e)`. Caso contrário, a atividade de saudação não será reportada (Olá `EngagementPage` chamadas `StartActivity` dentro de seu `OnNavigatedTo` método).
> 
> 

#### <a name="xaml-file"></a>Arquivo XAML
Modifique o arquivo `.xaml` de paginação:

* Adicione declarações de namespaces tooyour:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* Substituir `Page` por `engagement:EngagementPage`:

**Sem o Engagement:**

        <Page>
            <!-- layout -->
            ...
        </Page>

**Com o Engagement:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a>Substituir o comportamento padrão de saudação
Por padrão, nome de classe de saudação da página de Olá será relatado como nome da atividade hello, com e sem extras. Se a classe Olá usa Olá sufixo "Página", o contrato também removê-la.

Se você quiser um comportamento toooverride saudação padrão para nome hello, basta adicione este código tooyour:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

Se você quiser tooreport algumas informações adicionais com a sua atividade, você pode adicionar esse código tooyour:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Esses métodos são chamados de dentro de saudação `OnNavigatedTo` método da página.

### <a name="alternate-method-call-startactivity-manually"></a>Método alternativo: chame `StartActivity()` manualmente
Se você não pode ou não toooverload seu `Page` classes, em vez disso, você pode iniciar suas atividades chamando `EngagementAgent` métodos diretamente.

É recomendável toocall `StartActivity` dentro de sua `OnNavigatedTo` método da página.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Certifique-se de encerrar a sua sessão corretamente.
> 
> Olá SDK Universal do Windows chama automaticamente Olá `EndActivity` método quando o aplicativo hello está fechado. Assim, é **altamente** recomendado Olá toocall `StartActivity` método sempre que alterar a atividade de saudação do usuário Olá e muito**nunca** chamada hello `EndActivity` método, esse método envia tooEngagement servidor que o aplicativo hello de licença do usuário atual tem, esta será afeta todos os logs de aplicativo.
> 
> 

## <a name="advanced-reporting"></a>Relatórios avançados
Opcionalmente, convém tooreport eventos específicos do aplicativo, erros e trabalhos, toodo assim, use Olá outros métodos encontrados no hello `EngagementAgent` classe. Olá contrato de API permite que toouse todos os recursos avançados do contrato.

Para obter mais informações, consulte [como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo Windows Universal](mobile-engagement-windows-store-use-engagement-api.md).

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
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Modo intermitente
Por padrão, os relatórios de serviço de contrato de saudação logs em tempo real. Se seu aplicativo relatórios logs com muita frequência, é melhor toobuffer Olá logs e tooreport-los todos de uma vez em um base de tempo regulares (Isso é chamado hello "modo de disparo").

toodo assim, chame o método hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Olá argumento for um valor em **milissegundos**. A qualquer momento, se desejar que o log em tempo real do tooreactivate hello, apenas chame método de saudação sem nenhum parâmetro, ou com valor de saudação 0.

Olá modo intermitente ligeiramente aumentar bateria Olá vida mas tem um impacto em Olá contrato Monitor: todas as sessões e trabalhos a duração será arredondado toohello intermitência limite (portanto, sessões e menor do que o limite de disparo Olá pode não estar visível de trabalhos). É recomendável toouse um limite de disparo não mais que 30000 (30 s). Você tem toobe reconhece que salva os logs são itens too300 limitado. Se o envio for muito longo, você poderá perder alguns logs.

> [!WARNING]
> limite de intermitência de saudação não pode ser configurado tooa período anterior de 1s. Se você tentar toodo, portanto, Olá SDK mostrará um rastreamento com o erro hello e será automaticamente redefinir o valor padrão de toohello, ou seja, 0s. Isso vai disparar Olá SDK tooreport Olá logs em tempo real.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

