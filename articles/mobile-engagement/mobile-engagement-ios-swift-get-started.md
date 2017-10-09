---
title: aaaGet iniciado com o Azure Mobile Engagement para iOS no Swift | Microsoft Docs
description: "Saiba como toouse Azure Mobile Engagement com análises e notificações por Push para aplicativos do iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a>Introdução ao Azure Mobile Engagement para Aplicativos iOS em Swift
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse do Azure Mobile Engagement toounderstand seu uso do aplicativo e enviar por push o aplicativo do iOS notificações toosegmented usuários tooan.
Neste tutorial, você cria um aplicativo iOS em branco que coleta dados básicos e recebe notificações por push usando o Sistema de Notificação por Push da Apple (APNS).

Este tutorial requer o seguinte hello:

* XCode 8, que pode ser instalado a partir da MAC App Store
* Olá [SDK do Mobile Engagement iOS]
* Certificado de notificação por push (. p12), que pode ser obtido no centro de desenvolvimento da Apple

> [!NOTE]
> Este tutorial usa o Swift versão 3.0. 
> 
> 

A conclusão desse tutorial é um pré-requisito para todos os outros tutoriais do Mobile Engagement para os aplicativos iOS.

> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).
> 
> 

## <a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement
Este tutorial apresenta uma "integração básica", que é Olá mínimo definido toocollect necessários dados e envia uma notificação por push. documentação de integração completa Olá pode ser encontrada no hello [integração do SDK do Mobile Engagement iOS](mobile-engagement-ios-sdk-overview.md)

Vamos criar um aplicativo básico com a integração de saudação do XCode toodemonstrate:

### <a name="create-a-new-ios-project"></a>Crie um novo projeto iOS
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a>Conectar seu back-end do aplicativo tooMobile contrato
1. Baixar Olá [SDK do Mobile Engagement iOS]
2. Extrair hello. gz arquivo tooa pasta no seu computador
3. Projeto Olá clique com botão direito e selecione "Adicionar arquivos muito..."
   
    ![][1]
4. Navegue toohello pasta onde você extraiu hello SDK e selecione Olá `EngagementSDK` pasta e pressione Okey.
   
    ![][2]
5. Olá abrir `Build Phases` guia e na Olá `Link Binary With Libraries` menu Adicionar estruturas de hello, conforme mostrado abaixo:
   
    ![][3]
6. Criar um ponte de cabeçalho toobe toouse capaz de saudação do objetivo C APIs do SDK escolhendo Arquivo > Novo > arquivo > iOS > fonte > arquivo de cabeçalho.
   
    ![][4]
7. Editar saudação ponte cabeçalho arquivo tooexpose Mobile Engagement Objective-C código tooyour código Swift, adicione Olá importa a seguir:
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. Em configurações da compilação, certifique-se de saudação configuração em compilador Swift - geração de código de compilação de cabeçalho de ponte Objective-C tem um cabeçalho de toothis de caminho. Aqui está um exemplo de caminho: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (dependendo do caminho de saudação)**
   
   ![][6]
9. Voltar toohello portal do Azure em seu aplicativo *informações de Conexão* Olá página e copie a cadeia de caracteres de Conexão
   
   ![][5]
10. Agora cole a cadeia de caracteres de conexão de saudação em Olá `didFinishLaunchingWithOptions` delegar
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <a id="monitor"></a>Habilitar monitoramento em tempo real
Em ordem toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela (atividade) toohello Mobile Engagement backend.

1. Olá abrir **ViewController.swift** de arquivo e substitua a classe base Olá de **ViewController** toobe **EngagementViewController**:
   
    `class ViewController : EngagementViewController {`

## <a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitar Notificações por Push e mensagens no aplicativo
Mobile Engagement permite toointeract e alcance com os usuários com notificações por Push e no aplicativo de mensagens no contexto de saudação de campanhas. Esse módulo é chamado alcance no portal do Mobile Engagement hello.
Olá seções a seguir irá configurar seu aplicativo tooreceive-los.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Habilitar seu aplicativo tooreceive silenciosa notificações por Push
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Adicionar Olá alcance biblioteca tooyour projeto
1. Clique com botão direito no projeto
2. Selecione `Add file too...`
3. Navegue toohello pasta onde você extraiu Olá SDK
4. Selecione Olá `EngagementReach` pasta
5. Clique em Adicionar
6. Editar saudação ponte cabeçalhos de alcance do Mobile Engagement Objective-C do cabeçalho arquivo tooexpose e adicione Olá importa a seguir:
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a>Modifique seu Representante do Aplicativo
1. Olá interna `didFinishLaunchingWithOptions` - criar um módulo de alcance e passá-lo tooyour linha de inicialização contrato existente:
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Habilitar seu aplicativo tooreceive notificações por Push do APNS
1. Adicionar Olá toohello linha a seguir `didFinishLaunchingWithOptions` método:
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. Adicionar Olá `didRegisterForRemoteNotificationsWithDeviceToken` método da seguinte maneira:
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. Adicionar Olá `didReceiveRemoteNotification:fetchCompletionHandler:` método da seguinte maneira:
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[SDK do Mobile Engagement iOS]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
