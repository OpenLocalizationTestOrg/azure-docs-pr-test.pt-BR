---
title: "aaaAdd push notificações tooyour xamarin aplicativo | Microsoft Docs"
description: "Saiba como toouse do serviço de aplicativo do Azure e Hubs de notificação do Azure toosend aplicativo por push notificações tooyour xamarin"
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a>Adicionar aplicativo de xamarin de tooyour de notificações por push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Visão geral
Neste tutorial, você adiciona toohello de notificações por push [início rápido do xamarin](app-service-mobile-windows-store-dotnet-get-started.md) de projeto para que uma notificação por push seja enviada toohello dispositivo toda vez que um registro é inserido.

Se você não usar Olá baixar o projeto de servidor de início rápido, será necessário Olá o pacote de extensão de notificação por push. Consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial requer o seguinte hello:

* Uma conta ativa do Google. Você pode se inscrever em uma conta do Google em [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).
* [Componente do cliente Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/).

## <a name="configure-hub"></a>Configurar um novo Hub de Notificações
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Habilitar mensagens de nuvem Firebase
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a>Configurar solicitações de envio por push toosend do Azure
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a id="update-server"></a>Olá servidor projeto toosend push notificações de atualização
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a id="configure-app"></a>Configurar o projeto de cliente Olá para notificações por push
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <a id="add-push"></a>Adicionar aplicativo de tooyour de código de notificações por push
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <a name="test"></a>Testar notificações por push no seu aplicativo
Você pode testar o aplicativo hello usando um dispositivo virtual no emulador de saudação. Há etapas de configuração adicionais exigidas durante a execução em um emulador.

1. Certifique-se de que você está implantando tooor depuração em um dispositivo virtual que tem a APIs do Google definido como destino hello, conforme mostrado abaixo no Gerenciador de dispositivo Virtual Android (AVD) hello.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. Adicionar um dispositivo Android do Google conta toohello clicando **aplicativos** > **configurações** > **adicionar conta**, em seguida, siga os prompts de saudação.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. Executar aplicativo de lista de tarefas pendentes hello como antes e inserir um novo item de tarefas. Neste momento, um ícone de notificação é exibido na área de notificação de saudação. Você pode abrir Olá notificação gaveta tooview Olá texto completo da notificação de saudação.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
