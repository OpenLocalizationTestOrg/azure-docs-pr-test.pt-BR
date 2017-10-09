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
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a>Como tooIntegrate GCM com o Mobile Engagement
> [!IMPORTANT]
> Você deve seguir o procedimento de integração de saudação descrito em hello como tooIntegrate contrato no Android documento antes de seguir este guia.
> 
> Este documento é útil apenas se já integrado Olá alcançar toopush do módulo e o plano Google Play dispositivos. campanhas de alcance toointegrate em seu aplicativo, leia primeiro como tooIntegrate contrato chegar no Android.
> 
> 

## <a name="introduction"></a>Introdução
Integração GCM permite que seu toobe aplicativo enviada por push.

Cargas GCM enviada por push toohello SDK sempre contêm Olá `azme` chave no objeto de dados de saudação. Portanto, se você usar o GCM para outra finalidade em seu aplicativo, é possível filtrar os pushes com base nessa chave.

> [!IMPORTANT]
> Somente os dispositivos que executam Android 2.2 ou acima, com o Google Play instalado e com a conexão em tela de fundo do Google habilitada podem ser enviados por push pelo GCM; no entanto, você pode integrar esse código com segurança em dispositivos sem suporte (ele apenas utiliza intenções).
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a>Criar um projeto do Google Cloud Messaging com uma chave de API
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a>Integração do SDK
### <a name="managing-device-registrations"></a>Gerenciando registros de dispositivo
Cada dispositivo deve enviar um toohello do comando de registro os servidores Google, caso contrário, não pode ser alcançados.

Um dispositivo também pode cancelar o registro de notificações do GCM (dispositivo Olá é cancelado automaticamente se o aplicativo hello for desinstalado).

Se você não usar [Google reproduzir SDK] ou não já envie intenção de registro Olá por conta própria, você pode fazer com que o contrato de registrar o dispositivo Olá automaticamente para você.

tooenable isso, adicione Olá após tooyour `AndroidManifest.xml` arquivo, dentro de saudação `<application/>` marca:

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Comunicar-se o serviço de envio do contrato de toohello do registro id e receber notificações
Na id de registro de saudação ordem toocommunicate de saudação dispositivo toohello envio do contrato de serviço e receber notificações, adicionar Olá após tooyour `AndroidManifest.xml` arquivo, dentro de saudação `<application/>` marca (mesmo se você mesmo gerenciar registros de dispositivo):

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

Certifique-se de ter Olá as seguintes permissões no seu `AndroidManifest.xml` (após Olá `</application>` marca).

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Compromisso de mobilidade de conceder acesso tooyour chave API do GCM
Execute [neste guia](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement acesso tooyour chave API do GCM.

[Google reproduzir SDK]:https://developers.google.com/cloud-messaging/android/start
