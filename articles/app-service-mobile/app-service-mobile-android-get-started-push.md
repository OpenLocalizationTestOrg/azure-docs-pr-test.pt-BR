---
title: "aaaAdd push notificações tooyour aplicativo Android com aplicativos móveis | Microsoft Docs"
description: "Saiba como aplicativo Android do tooyour notificações por push de toouse toosend de aplicativos móveis."
services: app-service\mobile
documentationcenter: android
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: dcfb8463b395904b4bd0bf9bde2f71f259894066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-android-app"></a>Adicionar notificações de push tooyour aplicativo Android
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Visão geral
Neste tutorial, você adiciona toohello de notificações por push [início rápido do Android] projeto para que uma notificação por push seja enviada toohello dispositivo toda vez que um registro é inserido.

Se você não usar Olá baixar o projeto de servidor de início rápido, precisa Olá pacote de extensão de notificação por push. Para obter mais informações, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Pré-requisitos
Você precisa Olá seguinte:

* Uma IDE, dependendo do back-end do projeto:

  * [Android Studio](https://developer.android.com/sdk/index.html), se esse aplicativo tiver um back-end do Node.js.
  * [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) ou posterior, se esse aplicativo tiver um back-end do Microsoft .NET.
* Android 2.3 ou posterior, Google Repository revisão 27 ou posterior e Google Play Services 9.0.2 ou posterior para o Firebase Cloud Messaging.
* Olá completa [início rápido do Android].

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Criar um projeto que ofereça suporte ao Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a>Configurar um hub de notificação
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Configurar notificações por push de toosend do Azure
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a>Habilitar notificações por push para o projeto do servidor de saudação
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a>Adicionar aplicativo de tooyour de notificações por push
Nesta seção, você deve atualizar as notificações de push do cliente aplicativo Android toohandle.

### <a name="verify-android-sdk-version"></a>Verificar a versão do SDK do Android
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

A próxima etapa é tooinstall serviços do Google Play. Google Cloud Messaging tem alguns requisitos de nível de API mínimos para desenvolvimento e teste, quais Olá **minSdkVersion** propriedade no manifesto de saudação deve estar de acordo com.

Se você estiver testando com um dispositivo mais antigo, consulte [definir o Google reproduzir SDK dos serviços] toodetermine baixa como você pode definir esse valor e defini-lo apropriadamente.

### <a name="add-google-play-services-toohello-project"></a>Adicionar projeto de toohello de serviços do Google Play
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a>Incluir código
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a>Aplicativo de teste de saudação contra Olá publicado serviço móvel
Você pode testar o aplicativo hello anexando diretamente um telefone Android com um cabo USB, ou usando um dispositivo virtual no emulador de saudação.

## <a name="next-steps"></a>Próximas etapas
Agora que você concluiu este tutorial, considere a possibilidade de continuar tooone de saudação tutoriais a seguir:

* [Adicionar aplicativo do Android autenticação tooyour](app-service-mobile-android-get-started-users.md).
  Saiba como guia de início rápido tooadd autenticação toohello todolist projeto Android usando um provedor de identidade com suporte.
* [Habilitar a sincronização offline para o aplicativo móvel Android](app-service-mobile-android-get-started-offline-data.md).
  Saiba como o tooadd offline dão suporte ao aplicativo tooyour usando um back-end de aplicativos móveis. Com a sincronização offline, os usuários podem interagir com um aplicativo móvel &mdash; exibindo, adicionando ou modificando dados &mdash; mesmo quando não há nenhuma conexão de rede.

<!-- URLs -->
[início rápido do Android]: app-service-mobile-android-get-started.md

[definir o Google reproduzir SDK dos serviços]:https://developers.google.com/android/guides/setup
