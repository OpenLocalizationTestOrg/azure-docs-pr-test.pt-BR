---
title: aaaGet iniciado com o Windows Universal aplicativos do Azure Mobile Engagement
description: "Saiba como toouse do Azure Mobile Engagement com notificações de análise e enviar por push para aplicativos Universal do Windows."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a>Introdução ao Azure Mobile Engagement para aplicativos universais do Windows
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse do Azure Mobile Engagement toounderstand seu uso do aplicativo e enviar por push usuários de toosegmented de notificações de um aplicativo Universal do Windows.
Este tutorial demonstra Olá cenário difusão simples usando o Mobile Engagement. Você cria um Aplicativo Windows Universal em branco que coleta os dados básicos de uso do aplicativo e recebe notificações por push usando o Serviço de Notificação do Windows (WNS).

> [!NOTE]
> serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes. Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

## <a name="prerequisites"></a>Pré-requisitos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a>Configurar o Mobile Engagement para seu aplicativo Windows Universal
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement
Este tutorial apresenta uma "integração básica," hello mínimo definido toocollect necessários dados e envia uma notificação por push. documentação de integração completa Olá pode ser encontrada no hello [integração do SDK do Mobile Engagement Windows Universal](mobile-engagement-windows-store-sdk-overview.md).

Você pode criar um aplicativo básico com a integração do Visual Studio toodemonstrate hello.

### <a name="create-a-windows-universal-app-project"></a>Criar um projeto de Aplicativo Windows Universal
Olá etapas a seguir pressupõem uso de saudação do Visual Studio 2015 que etapas Olá são semelhantes em versões anteriores do Visual Studio.

1. Inicie o Visual Studio e em Olá **início** tela, selecione **novo projeto**.
2. No pop-up hello, selecione **Windows** -> **Universal** -> **(Universal do Windows) do aplicativo em branco**. Preencha o aplicativo hello **nome** e **nome da solução**e, em seguida, clique em **Okey**.

    ![][1]

Você criou um projeto de aplicativo Universal do Windows na qual você integrar lado Olá SDK do Azure Mobile Engagement.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Conectar seu back-end do aplicativo tooMobile contrato
1. Instalar Olá [MicrosoftAzure.MobileEngagement] pacote Nuget em seu projeto. Se você estiver direcionando plataformas Windows e Windows Phone, você precisa toodo isso para os dois projetos. Para o Windows 8. x e Windows Phone 8.1, Olá mesmo Nuget pacote casas Olá correto específico da plataforma binários em cada projeto.
2. Abra **Package. appxmanifest** e certifique-se de que Olá funcionalidade a seguir é adicionada existe:

        Internet (Client)

    ![][2]
3. Copiar a cadeia de caracteres de conexão de saudação que você copiou anteriormente para seu aplicativo do Mobile Engagement agora e colá-lo em Olá `Resources\EngagementConfiguration.xml` arquivo entre hello `<connectionString>` e `</connectionString>` marcas:

    ![][3]

    > [!TIP]
    > Se seu aplicativo for destinado para as plataformas Windows e Windows Phone, você ainda deverá criar dois Aplicativos do Mobile Engagement - um para cada plataforma com suporte. Ter dois aplicativos garante que você pode criar segmentação correta do público-alvo hello e pode enviar notificações de destino corretamente para cada plataforma.

    > [!IMPORTANT]
    > NuGet não copiar recursos do SDK Olá automaticamente em seu aplicativo de UWP do Windows 10. Você tem toodo-o manualmente após a etapas Olá que aparecem (Leiame. txt) quando o pacote do Nuget hello está instalado.  

1. Em Olá `App.xaml.cs` arquivo:

    a. Adicionar Olá `using` instrução:

            using Microsoft.Azure.Engagement;

    b. Adicione um método que inicializa Olá contrato:

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    c. Inicializar Olá SDK no hello **OnLaunched** método:

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    c. Inserir o seguinte Olá em hello **OnActivated** método e adicione o método hello se ele não ainda estiver presente:

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <a id="monitor"></a>Habilitar monitoramento em tempo real
toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela (atividade) toohello Mobile Engagement backend.

1. Em Olá **MainPage.xaml.cs**, adicione o seguinte Olá `using` instrução:

    usando Microsoft.Azure.Engagement.Overlay;
2. Alterar a classe base de saudação do **MainPage** de **página** muito**EngagementPageOverlay**:

        class MainPage : EngagementPageOverlay
3. Em Olá `MainPage.xaml` arquivo:

    a. Adicione declarações de namespaces tooyour:

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    b. Substituir saudação **página** no nome da marca XML Olá com **contrato: EngagementPageOverlay**

> [!IMPORTANT]
> Se sua página substitui Olá `OnNavigatedTo` método, ser toocall se `base.OnNavigatedTo(e)`. Caso contrário, a atividade de saudação não é informada `EngagementPage` chamadas `StartActivity` dentro de seu `OnNavigatedTo` método). Isso é especialmente importante em um projeto do Windows Phone onde saudação padrão modelo tem um `OnNavigatedTo` método.
>
> Para **aplicativos universais do Windows 10**, usar o método hello recomendado em hello "recomendado método: sobrecarregar suas classes de página" seção [avançado relatar Olá SDK de contrato de aplicativos Universal do Windows](mobile-engagement-windows-store-advanced-reporting.md) , em vez da saudação mencionados acima.

## <a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo
Mobile Engagement permite toointeract e alcançar os usuários com as notificações por push e no aplicativo mensagens no contexto de saudação de campanhas. Esse módulo é chamado alcance no portal do Mobile Engagement hello.
Olá seções a seguir configurar seu aplicativo tooreceive-los.

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a>Habilitar seu aplicativo tooreceive notificações por Push do WNS
1. Em Olá `Package.appxmanifest` no arquivo, em Olá **aplicativo** guia em **notificações**, defina **compatíveis com notificação do sistema:** muito**Sim**

    ![][5]

### <a name="initialize-hello-reach-sdk"></a>Inicializar Olá SDK do REACH
Em `App.xaml.cs`, chame **EngagementReach.Instance.Init(e);** em Olá **InitEngagement** função logo após a inicialização do agente de saudação:

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

Você está pronto toosend uma notificação do sistema. Em seguida, verificamos se você realizou corretamente essa integração básica.

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a>Conceder acesso tooMobile contrato toosend notificações
1. Abra [Centro de Desenvolvimento da Windows Store] no navegador da Web, faça logon e crie uma conta, se necessário.
2. Clique em **painel** na parte superior de saudação à direita de canto e, em seguida, clique em **criar um novo aplicativo** Olá esquerdo no menu do painel.

    ![][9]
3. Crie seu aplicativo ao reservar o nome dele.

    ![][10]
4. Depois que o aplicativo hello foi criado, navegar muito**serviços -> notificações por Push** no menu esquerdo hello.

    ![][11]
5. Em Olá seção notificações de Push, clique em Olá **site de serviços do Live** link.

    ![][12]
6. Você navegar toohello seção de credenciais de Push. Verifique se você está no hello **configurações do aplicativo** seção e, em seguida, copie o **SID do pacote** e **segredo do cliente**

    ![][13]
7. Navegue toohello **configurações** de seu portal do Mobile Engagement e clique em Olá **Push nativo** seção Olá esquerda. Em seguida, clique em Olá **editar** tooenter botão seu **identificador de segurança (SID) do pacote** e sua **chave secreta** conforme mostrado:

    ![][6]
8. Por fim, certifique-se de que você associou o aplicativo do Visual Studio com este aplicativo criado no repositório de aplicativo hello. Clique em **Associar Aplicativo à Loja** no Visual Studio.

    ![][7]

## <a id="send"></a>Enviar um aplicativo de tooyour de notificação
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Se o aplicativo hello está em execução, você verá uma notificação no aplicativo. Caso contrário, se aplicativo hello estiver fechado, você verá uma notificação do sistema.
Se você vir uma notificação no aplicativo, mas não uma notificação do sistema, e você estiver executando o aplicativo hello no modo de depuração no Visual Studio, em seguida, tente **eventos de ciclo de vida -> Suspender** no hello tooensure de barra de ferramentas que o aplicativo hello é suspensa. Se você clicou o botão de início Olá durante a depuração de aplicativo hello no Visual Studio, em seguida, ele não sempre obter suspenso e enquanto você receber a notificação de saudação como no aplicativo, ele não aparece como uma notificação do sistema.  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Centro de Desenvolvimento da Windows Store]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
