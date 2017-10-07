---
title: "aaaWindows Universal avançado relatórios com o contrato de MobileApps"
description: Como tooIntegrate Azure Mobile Engagement com aplicativos universais do Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a>Relatórios avançados com hello SDK de contrato de aplicativos Universal do Windows
> [!div class="op_single_selector"]
> * [Universal do Windows](mobile-engagement-windows-store-advanced-reporting.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

Este tópico descreve cenários de relatório adicionais em seu aplicativo universal do Windows. Esses cenários incluem opções que você pode escolher tooapply toohello aplicativo criado no hello [Introdução](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.

## <a name="prerequisites"></a>Pré-requisitos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

Antes de iniciar este tutorial, você deve completar Olá [Introdução](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, o que é deliberadamente simples e direto. Este tutorial aborda as opções adicionais que você pode escolher.

## <a name="specifying-engagement-configuration-at-runtime"></a>Como especificar a configuração do Engagement em tempo de execução
configuração do contrato de saudação é centralizada em Olá `Resources\EngagementConfiguration.xml` arquivo do projeto, que é onde ele foi especificado na Olá [Introdução](mobile-engagement-windows-store-dotnet-get-started.md) tópico.

Mas você também pode especificá-lo em tempo de execução: você pode chamar hello seguinte método antes da inicialização de agente de contrato hello:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a>Método recomendado: sobrecarregar suas classes `Page`
tooactivate Olá relatórios de todos os logs de saudação exigidos pelo contrato toocompute usuários, sessões, atividades, falhas e estatísticas técnicas, faça todas as suas `Page` subclasses herdam a saudação `EngagementPage` classes.

Este é um exemplo de uma página de seu aplicativo. Você pode fazer Olá igual para todas as páginas do seu aplicativo.

### <a name="c-source-file"></a>Arquivo de código-fonte C#
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
> Se sua página substitui Olá `OnNavigatedTo` método, ser toocall se `base.OnNavigatedTo(e)`. Caso contrário, a atividade de saudação não é informada (Olá `EngagementPage` chamadas `StartActivity` dentro de seu `OnNavigatedTo` método).
> 
> 

### <a name="xaml-file"></a>Arquivo XAML
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

### <a name="override-hello-default-behaviour"></a>Substituir o comportamento padrão de saudação
Por padrão, nome de classe de saudação da página de Olá será relatado como nome da atividade hello, com e sem extras. Se a classe Olá usa Olá sufixo "Página", contrato remove.

comportamento do toooverride saudação padrão para nome hello, adicione este código:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

tooreport informações extras com sua atividade, adicione este código:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Esses métodos são chamados de dentro de saudação `OnNavigatedTo` método da página.

### <a name="alternate-method-call-startactivity-manually"></a>Método alternativo: chame `StartActivity()` manualmente
Se você não pode ou não toooverload seu `Page` classes, em vez disso, você pode iniciar suas atividades chamando `EngagementAgent` métodos diretamente.

Recomendamos chamar `StartActivity` dentro de seu método `OnNavigatedTo` da sua Página.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Certifique-se de encerrar a sua sessão corretamente.
> 
> Olá SDK Universal do Windows chama automaticamente Olá `EndActivity` método quando o aplicativo hello está fechado. Portanto, é **altamente** recomendado Olá toocall `StartActivity` sempre que alterar a atividade de saudação do usuário Olá e muito**nunca** chamada hello `EndActivity` método. Este método notifica o servidor de contrato de saudação que usuário Olá atual tiver saído aplicativo hello, que afeta todos os logs de aplicativo.
> 
> 

## <a name="advanced-reporting"></a>Relatórios avançados
Opcionalmente, convém eventos específicos de aplicativos de tooreport, erros e trabalhos, toodo assim, use Olá outros métodos encontrados no hello `EngagementAgent` classe. Olá contrato de API permite o uso de recursos avançados do contrato de todos os.

Para obter mais informações, consulte [como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo Windows Universal](mobile-engagement-windows-store-use-engagement-api.md).

