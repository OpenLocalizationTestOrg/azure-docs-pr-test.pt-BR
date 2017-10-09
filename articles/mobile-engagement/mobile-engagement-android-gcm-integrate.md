---
title: "aaaAzure integração do Mobile Engagement Android SDK"
description: "Atualizações e procedimentos mais recentes para o SDK do Android do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a><span data-ttu-id="632b3-103">Como tooIntegrate GCM com o Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="632b3-103">How tooIntegrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="632b3-104">Você deve seguir o procedimento de integração de saudação descrito em hello como tooIntegrate contrato no Android documento antes de seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="632b3-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="632b3-105">Este documento é útil apenas se já integrado Olá alcançar toopush do módulo e o plano Google Play dispositivos.</span><span class="sxs-lookup"><span data-stu-id="632b3-105">This document is useful only if you already integrated hello Reach module and plan toopush Google Play devices.</span></span> <span data-ttu-id="632b3-106">campanhas de alcance toointegrate em seu aplicativo, leia primeiro como tooIntegrate contrato chegar no Android.</span><span class="sxs-lookup"><span data-stu-id="632b3-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="632b3-107">Introdução</span><span class="sxs-lookup"><span data-stu-id="632b3-107">Introduction</span></span>
<span data-ttu-id="632b3-108">Integração GCM permite que seu toobe aplicativo enviada por push.</span><span class="sxs-lookup"><span data-stu-id="632b3-108">Integrating GCM allows your application toobe pushed.</span></span>

<span data-ttu-id="632b3-109">Cargas GCM enviada por push toohello SDK sempre contêm Olá `azme` chave no objeto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="632b3-109">GCM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="632b3-110">Portanto, se você usar o GCM para outra finalidade em seu aplicativo, é possível filtrar os pushes com base nessa chave.</span><span class="sxs-lookup"><span data-stu-id="632b3-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="632b3-111">Somente os dispositivos que executam Android 2.2 ou acima, com o Google Play instalado e com a conexão em tela de fundo do Google habilitada podem ser enviados por push pelo GCM; no entanto, você pode integrar esse código com segurança em dispositivos sem suporte (ele apenas utiliza intenções).</span><span class="sxs-lookup"><span data-stu-id="632b3-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="632b3-112">Criar um projeto do Google Cloud Messaging com uma chave de API</span><span class="sxs-lookup"><span data-stu-id="632b3-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="632b3-113">Integração do SDK</span><span class="sxs-lookup"><span data-stu-id="632b3-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="632b3-114">Gerenciando registros de dispositivo</span><span class="sxs-lookup"><span data-stu-id="632b3-114">Managing device registrations</span></span>
<span data-ttu-id="632b3-115">Cada dispositivo deve enviar um toohello do comando de registro os servidores Google, caso contrário, não pode ser alcançados.</span><span class="sxs-lookup"><span data-stu-id="632b3-115">Each device must send a registration command toohello Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="632b3-116">Um dispositivo também pode cancelar o registro de notificações do GCM (dispositivo Olá é cancelado automaticamente se o aplicativo hello for desinstalado).</span><span class="sxs-lookup"><span data-stu-id="632b3-116">A device can also unregister from GCM notifications (hello device is automatically unregistered if hello application is uninstalled).</span></span>

<span data-ttu-id="632b3-117">Se você não usar [Google reproduzir SDK] ou não já envie intenção de registro Olá por conta própria, você pode fazer com que o contrato de registrar o dispositivo Olá automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="632b3-117">If you don't use [Google Play SDK] or you don't already send hello registration intent yourself, you can make Engagement register hello device automatically for you.</span></span>

<span data-ttu-id="632b3-118">tooenable isso, adicione Olá após tooyour `AndroidManifest.xml` arquivo, dentro de saudação `<application/>` marca:</span><span class="sxs-lookup"><span data-stu-id="632b3-118">tooenable this, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="632b3-119">Comunicar-se o serviço de envio do contrato de toohello do registro id e receber notificações</span><span class="sxs-lookup"><span data-stu-id="632b3-119">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="632b3-120">Na id de registro de saudação ordem toocommunicate de saudação dispositivo toohello envio do contrato de serviço e receber notificações, adicionar Olá após tooyour `AndroidManifest.xml` arquivo, dentro de saudação `<application/>` marca (mesmo se você mesmo gerenciar registros de dispositivo):</span><span class="sxs-lookup"><span data-stu-id="632b3-120">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you manage device registrations yourself):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

<span data-ttu-id="632b3-121">Certifique-se de ter Olá as seguintes permissões no seu `AndroidManifest.xml` (após Olá `</application>` marca).</span><span class="sxs-lookup"><span data-stu-id="632b3-121">Ensure you have hello following permissions in your `AndroidManifest.xml` (after hello `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="632b3-122">Compromisso de mobilidade de conceder acesso tooyour chave API do GCM</span><span class="sxs-lookup"><span data-stu-id="632b3-122">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="632b3-123">Execute [neste guia](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement acesso tooyour chave API do GCM.</span><span class="sxs-lookup"><span data-stu-id="632b3-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement access tooyour GCM API Key.</span></span>

[Google reproduzir SDK]:https://developers.google.com/cloud-messaging/android/start
