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
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a><span data-ttu-id="71f1d-103">Adicionar aplicativo de xamarin de tooyour de notificações por push</span><span class="sxs-lookup"><span data-stu-id="71f1d-103">Add push notifications tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="71f1d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="71f1d-104">Overview</span></span>
<span data-ttu-id="71f1d-105">Neste tutorial, você adiciona toohello de notificações por push [início rápido do xamarin](app-service-mobile-windows-store-dotnet-get-started.md) de projeto para que uma notificação por push seja enviada toohello dispositivo toda vez que um registro é inserido.</span><span class="sxs-lookup"><span data-stu-id="71f1d-105">In this tutorial, you add push notifications toohello [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="71f1d-106">Se você não usar Olá baixar o projeto de servidor de início rápido, será necessário Olá o pacote de extensão de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="71f1d-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="71f1d-107">Consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="71f1d-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71f1d-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="71f1d-108">Prerequisites</span></span>
<span data-ttu-id="71f1d-109">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="71f1d-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="71f1d-110">Uma conta ativa do Google.</span><span class="sxs-lookup"><span data-stu-id="71f1d-110">An active Google account.</span></span> <span data-ttu-id="71f1d-111">Você pode se inscrever em uma conta do Google em [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="71f1d-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="71f1d-112">[Componente do cliente Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="71f1d-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="71f1d-113"><a name="configure-hub"></a>Configurar um novo Hub de Notificações</span><span class="sxs-lookup"><span data-stu-id="71f1d-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="71f1d-114"><a id="register"></a>Habilitar mensagens de nuvem Firebase</span><span class="sxs-lookup"><span data-stu-id="71f1d-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a><span data-ttu-id="71f1d-115">Configurar solicitações de envio por push toosend do Azure</span><span class="sxs-lookup"><span data-stu-id="71f1d-115">Configure Azure toosend push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="71f1d-116"><a id="update-server"></a>Olá servidor projeto toosend push notificações de atualização</span><span class="sxs-lookup"><span data-stu-id="71f1d-116"><a id="update-server"></a>Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="71f1d-117"><a id="configure-app"></a>Configurar o projeto de cliente Olá para notificações por push</span><span class="sxs-lookup"><span data-stu-id="71f1d-117"><a id="configure-app"></a>Configure hello client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="71f1d-118"><a id="add-push"></a>Adicionar aplicativo de tooyour de código de notificações por push</span><span class="sxs-lookup"><span data-stu-id="71f1d-118"><a id="add-push"></a>Add push notifications code tooyour app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="71f1d-119"><a name="test"></a>Testar notificações por push no seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="71f1d-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="71f1d-120">Você pode testar o aplicativo hello usando um dispositivo virtual no emulador de saudação.</span><span class="sxs-lookup"><span data-stu-id="71f1d-120">You can test hello app by using a virtual device in hello emulator.</span></span> <span data-ttu-id="71f1d-121">Há etapas de configuração adicionais exigidas durante a execução em um emulador.</span><span class="sxs-lookup"><span data-stu-id="71f1d-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="71f1d-122">Certifique-se de que você está implantando tooor depuração em um dispositivo virtual que tem a APIs do Google definido como destino hello, conforme mostrado abaixo no Gerenciador de dispositivo Virtual Android (AVD) hello.</span><span class="sxs-lookup"><span data-stu-id="71f1d-122">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="71f1d-123">Adicionar um dispositivo Android do Google conta toohello clicando **aplicativos** > **configurações** > **adicionar conta**, em seguida, siga os prompts de saudação.</span><span class="sxs-lookup"><span data-stu-id="71f1d-123">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="71f1d-124">Executar aplicativo de lista de tarefas pendentes hello como antes e inserir um novo item de tarefas.</span><span class="sxs-lookup"><span data-stu-id="71f1d-124">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="71f1d-125">Neste momento, um ícone de notificação é exibido na área de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="71f1d-125">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="71f1d-126">Você pode abrir Olá notificação gaveta tooview Olá texto completo da notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="71f1d-126">You can open hello notification drawer tooview hello full text of hello notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
