---
title: "aaaAzure integração do Mobile Engagement Android SDK"
description: "Atualizações e procedimentos mais recentes para o SDK do Android do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a>Como tooIntegrate ADM com contrato
> [!IMPORTANT]
> Você deve seguir o procedimento de integração de saudação descrito em hello como tooIntegrate contrato no Android documento antes de seguir este guia.
> 
> Este documento é útil apenas se você já Olá alcance módulo e o plano toopush Amazon dispositivos integrado. campanhas de alcance toointegrate em seu aplicativo, leia primeiro como tooIntegrate contrato chegar no Android.
> 
> 

## <a name="introduction"></a>Introdução
Integração ADM permite que seu toobe aplicativo enviada por push ao direcionar dispositivos com Android da Amazon.

Cargas ADM enviadas toohello SDK sempre contêm Olá `azme` chave no objeto de dados de saudação. Portanto, se você usar o ADM para outra finalidade em seu aplicativo, é possível filtrar os pushes com base nessa chave.

> [!IMPORTANT]
> Somente dispositivos Amazon Kindle executando Android 4.0.3 ou acima têm suporte pelo Amazon Device Messaging; no entanto, você pode integrar esse código com segurança em outros dispositivos.
> 
> 

## <a name="sign-up-tooadm"></a>Inscreva-se tooADM
Se ainda não tiver feito, você deve habilitar o ADM em sua conta da Amazon.

procedimento de saudação é detalhado no: [ <https://developer.amazon.com/sdk/adm/credentials.html>].

Após concluir o procedimento hello, você obtém:

* OAuth credenciais (uma ID de cliente e um segredo do cliente) para o contrato toobe capaz de toopush seus dispositivos.
* Uma chave de API que deve ser integrada ao seu aplicativo.

## <a name="sdk-integration"></a>Integração do SDK
### <a name="managing-device-registrations"></a>Gerenciando registros de dispositivo
Cada dispositivo deve enviar um toohello do comando de registro de servidores ADM, caso contrário, não pode ser alcançados.

Se você já usa Olá [biblioteca de cliente ADM]e já tiver [integrado ADM] poderá ir diretamente tooandroid-sdk-adm-receber.

Se você não tiver integrado ADM ainda, contrato tem um tooenable de forma mais simples-lo em seu aplicativo:

Edite seu arquivo `AndroidManifest.xml`:

* Adicione Olá Amazon namespace, Olá arquivo deve começar como este:
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* Olá interna `<application/>` marca, adicionar nesta seção:
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* Depois de adicionar a marca do amazon hello, você pode ter um erro de compilação se o destino de compilação de projeto está abaixo Android 2.1. Você tem toouse um **Android 2.1 +** destino de compilação (não se preocupe, você ainda pode ter um `minSdkVersion` definido too4).
* Integrar Olá ADM chave de API como um ativo seguindo [esse procedimento].

Siga as instruções de saudação de próximas seções de saudação.

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Comunicar-se o serviço de envio do contrato de toohello do registro id e receber notificações
Na id de registro de saudação ordem toocommunicate de saudação dispositivo toohello envio do contrato de serviço e receber notificações, adicionar Olá após tooyour `AndroidManifest.xml` arquivo, dentro de saudação `<application/>` marca (mesmo se você usar ADM sem compromisso):

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

Certifique-se de ter Olá as seguintes permissões no seu `AndroidManifest.xml` (antes da saudação `</application>` marca).

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a>Conceda as credenciais do Engagement OAuth
Envie suas credenciais OAuth (ID do Cliente e Segredo do Cliente) no Portal do Engagement.

[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[biblioteca de cliente ADM]:https://developer.amazon.com/sdk/adm/setup.html
[integrado ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[esse procedimento]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
