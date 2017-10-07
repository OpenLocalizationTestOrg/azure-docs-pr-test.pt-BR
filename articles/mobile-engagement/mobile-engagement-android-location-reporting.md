---
title: "aaaLocation relatórios para o Android SDK do Azure Mobile Engagement"
description: Descreve como local de tooconfigure reporting para Android SDK do Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a>Relatório de local para o SDK do Azure Mobile Engagement para Android
> [!div class="op_single_selector"]
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Este tópico descreve como local de toodo reporting para seu aplicativo do Android.

## <a name="prerequisites"></a>Pré-requisitos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a>Relatórios de local
Se você quiser toobe locais relatado, você precisa tooadd algumas linhas de configuração (entre hello `<application>` e `</application>` marcas).

### <a name="lazy-area-location-reporting"></a>Relatórios de local de área lenta
Relatório de local de área lento permite relatório país de hello, região e localidade associado a dispositivos. Esse tipo de relatório de local usa apenas os locais de rede (com base na ID da célula ou WIFI). Olá dispositivo é relatada no máximo uma vez por sessão. Olá GPS nunca é usado e, portanto, esse tipo de relatório local tem baixo impacto na bateria hello.

Relatado áreas são estatísticas de geográfica toocompute usado sobre usuários, sessões, eventos e erros. Elas também podem ser usadas como critério nas campanhas do Reach.

Habilitar o local de área lento reporting por meio da configuração de saudação mencionada anteriormente neste procedimento:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Você também precisa toospecify uma permissão de local. Este código usa a permissão ``COARSE`` :

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Se seu aplicativo exigir, você poderá usar ``ACCESS_FINE_LOCATION`` em vez disso.

### <a name="real-time-location-reporting"></a>Relatórios de localização em tempo real
Relatórios de local em tempo real permite relatório latitude de saudação e a longitude associado a dispositivos. Por padrão, esse tipo de relatório de local usa apenas os locais de rede, com base na ID da célula ou WIFI. Olá reporting somente estará ativo quando o aplicativo hello é executado em primeiro plano (por exemplo, durante uma sessão).

Locais em tempo real são *não* usado toocompute estatísticas. Seu único propósito é o uso de saudação do tooallow de geoinstalação em tempo real \<alcance-público-o isolamento geográfico\> critério de campanhas de alcance.

local em tempo real de tooenable relatórios, adicione uma linha de código toowhere você definir cadeia de caracteres de conexão de contrato Olá na atividade de iniciador hello. resultado de saudação semelhante ao seguinte hello:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a>Relatórios com base em GPS
Por padrão, os relatórios de local em tempo real usam apenas locais com base em rede. tooenable Olá dos locais com base em GPS, que são muito mais precisos, usar o objeto de configuração hello:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Você também precisa Olá tooadd permissão a seguir se ausentes:

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Relatório de segundo plano
Por padrão, relatórios de local em tempo real só está ativo quando o aplicativo hello é executado em primeiro plano (por exemplo, durante uma sessão). Olá tooenable relatórios também no plano de fundo, use esse objeto de configuração:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Quando o aplicativo hello é executado em segundo plano, somente os locais de rede são relatados, mesmo se você tiver habilitado Olá GPS.
> 
> 

Se o usuário Olá reinicializar seu dispositivo, relatório de local do plano de fundo de saudação será interrompido. toomake reiniciar automaticamente no momento da inicialização, adicione este código.

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

Você também precisa Olá tooadd permissão a seguir se ausentes:

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a>Permissões do Android M
A partir do Android M, algumas permissões são gerenciadas em tempo de execução e precisam de aprovação do usuário.

Se você selecionar o nível de API do Android 23, permissões de tempo de execução Olá estão desativadas por padrão para novas instalações do aplicativo. Caso contrário, elas serão ativadas por padrão.

Você pode habilitar/desabilitar essas permissões no menu de configurações de dispositivo de saudação. A desativação de permissões do menu do sistema Olá elimina processos em segundo plano de saudação do aplicativo hello, que é um comportamento do sistema e não tem nenhum impacto na capacidade tooreceive push no plano de fundo.

No contexto de saudação do local do Mobile Engagement reporting, permissões de saudação que precisam de aprovação em tempo de execução são:

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

Solicite permissões de usuário hello usando uma caixa de diálogo do sistema padrão. Se o usuário Olá aprova, conte- ``EngagementAgent`` tootake alterar em consideração em tempo real. Caso contrário, a alteração de Olá é processado próximo tempo Olá usuário inicia Olá aplicativo hello.

Aqui está um toouse de exemplo de código em uma atividade de permissões do aplicativo toorequest e resultado Olá forward positivo muito``EngagementAgent``:

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
