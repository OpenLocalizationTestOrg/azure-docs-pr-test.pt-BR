---
title: "Integração do SDK do Android do Azure Mobile Engagement"
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
ms.openlocfilehash: 0282abbf44406cac89c13520bc2a4e375817ed1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-gcm-with-mobile-engagement"></a><span data-ttu-id="ca048-103">Como integrar o GCM ao Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ca048-103">How to Integrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ca048-104">Você deve seguir o procedimento de integração descrito no documento Como Integrar o Engagement, antes de seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="ca048-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="ca048-105">Este documento será útil apenas se você já tiver integrado o módulo de Alcance e planeja enviar por push os dispositivos Google Play.</span><span class="sxs-lookup"><span data-stu-id="ca048-105">This document is useful only if you already integrated the Reach module and plan to push Google Play devices.</span></span> <span data-ttu-id="ca048-106">Para integrar campanhas de Alcance em seu aplicativo, leia primeiro Como Integrar o Engagement Reach no Android.</span><span class="sxs-lookup"><span data-stu-id="ca048-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="ca048-107">Introdução</span><span class="sxs-lookup"><span data-stu-id="ca048-107">Introduction</span></span>
<span data-ttu-id="ca048-108">A integração do GCM permite que o seu aplicativo seja enviado por push.</span><span class="sxs-lookup"><span data-stu-id="ca048-108">Integrating GCM allows your application to be pushed.</span></span>

<span data-ttu-id="ca048-109">As cargas do GCM enviadas por push para o SDK sempre contêm a chave `azme` no objeto de dados.</span><span class="sxs-lookup"><span data-stu-id="ca048-109">GCM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="ca048-110">Portanto, se você usar o GCM para outra finalidade em seu aplicativo, é possível filtrar os pushes com base nessa chave.</span><span class="sxs-lookup"><span data-stu-id="ca048-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca048-111">Somente os dispositivos que executam Android 2.2 ou acima, com o Google Play instalado e com a conexão em tela de fundo do Google habilitada podem ser enviados por push pelo GCM; no entanto, você pode integrar esse código com segurança em dispositivos sem suporte (ele apenas utiliza intenções).</span><span class="sxs-lookup"><span data-stu-id="ca048-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="ca048-112">Criar um projeto do Google Cloud Messaging com uma chave de API</span><span class="sxs-lookup"><span data-stu-id="ca048-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="ca048-113">Integração do SDK</span><span class="sxs-lookup"><span data-stu-id="ca048-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="ca048-114">Gerenciando registros de dispositivo</span><span class="sxs-lookup"><span data-stu-id="ca048-114">Managing device registrations</span></span>
<span data-ttu-id="ca048-115">Cada dispositivo deve enviar um comando de registro aos servidores do Google, caso contrário eles não poderão ser alcançados.</span><span class="sxs-lookup"><span data-stu-id="ca048-115">Each device must send a registration command to the Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="ca048-116">Um dispositivo também pode cancelar o registro de notificações do GCM (o registro do dispositivo será cancelado automaticamente se o aplicativo for desinstalado).</span><span class="sxs-lookup"><span data-stu-id="ca048-116">A device can also unregister from GCM notifications (the device is automatically unregistered if the application is uninstalled).</span></span>

<span data-ttu-id="ca048-117">Se você não usa o [SDK do Google Play] ou ainda não enviou a intenção de registro por conta própria, você poderá fazer com que o Engagement registre o dispositivo automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="ca048-117">If you don't use [Google Play SDK] or you don't already send the registration intent yourself, you can make Engagement register the device automatically for you.</span></span>

<span data-ttu-id="ca048-118">Para habilitar isso, adicione o seguinte ao seu arquivo `AndroidManifest.xml` dentro da marca`<application/>`:</span><span class="sxs-lookup"><span data-stu-id="ca048-118">To enable this, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget the \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="ca048-119">Comunicar a ID de registro para o serviço de envio por push do Engagement e receber notificações</span><span class="sxs-lookup"><span data-stu-id="ca048-119">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="ca048-120">Para comunicar a ID de registro do dispositivo para o serviço de envio por push do Engagement e receber notificações, adicione o seguinte ao seu arquivo `AndroidManifest.xml` dentro da marca `<application/>` (mesmo que você gerencie registros de dispositivo por conta própria):</span><span class="sxs-lookup"><span data-stu-id="ca048-120">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you manage device registrations yourself):</span></span>

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

<span data-ttu-id="ca048-121">Certifique-se de ter as seguintes permissões em seu `AndroidManifest.xml` (após a marca `</application>`).</span><span class="sxs-lookup"><span data-stu-id="ca048-121">Ensure you have the following permissions in your `AndroidManifest.xml` (after the `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="ca048-122">Permitir acesso do Mobile Engagement à sua chave de API do GCM</span><span class="sxs-lookup"><span data-stu-id="ca048-122">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="ca048-123">Siga [este guia](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) para permitir acesso do Mobile Engagement à sua chave de API do GCM.</span><span class="sxs-lookup"><span data-stu-id="ca048-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) to grant Mobile Engagement access to your GCM API Key.</span></span>

<span data-ttu-id="ca048-124">[SDK do Google Play]:https://developers.google.com/cloud-messaging/android/start</span><span class="sxs-lookup"><span data-stu-id="ca048-124">[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start</span></span>
