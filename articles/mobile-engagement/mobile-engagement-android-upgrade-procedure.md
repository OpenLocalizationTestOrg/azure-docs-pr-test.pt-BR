---
title: "aaaAzure integração do Mobile Engagement Android SDK"
description: "Atualizações e procedimentos mais recentes para o SDK do Android do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>Procedimentos de atualização
Se você já tiver integrado uma versão mais antiga do nosso SDK em seu aplicativo, você tem Olá tooconsider pontos a seguir ao atualizar Olá SDK.

Você pode ter vários procedimentos de toofollow se perdidas várias versões do SDK de saudação. Por exemplo, se você migrar de 1.4.0 too1.6.0 ter toofirst siga hello "de 1.4.0 too1.5.0" procedimento e hello "de 1.5.0 too1.6.0" procedimento.

Qualquer versão de hello atualizar, você tem Olá tooreplace `mobile-engagement-VERSION.jar` com hello uma nova.

## <a name="from-420-too421"></a>De 4.2.0 too4.2.1
Esta etapa, na verdade, pode ser feita em qualquer versão do SDK do hello, é um aprimoramento de segurança ao integrar o alcance de atividades.

Agora você deve adicionar `exported="false"` tooall alcance atividades.

As atividades de Alcance deverão ter esta aparência no `AndroidManifest.xml`:

            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

## <a name="from-400-too410"></a>De 4.0.0 too4.1.0
Olá SDK agora identificador novo modelo de permissão do Android M.

Se você usar os recursos de localização ou notificações de visão geral, leia [esta seção](mobile-engagement-android-integrate-engagement.md#android-m-permissions).

Além disso toohello novo modelo de permissão, podemos agora oferecem suporte à configuração recursos de local em tempo de execução.
Estamos ainda compatíveis com os parâmetros de manifesto da saudação para local, mas agora está obsoleta. configuração de tempo de execução toouse, a seguir remove Olá seções de sua ``AndroidManifest.xml``:

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

e ler [isso atualizado procedimento](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse configuração de tempo de execução em vez disso.

## <a name="from-300-too400"></a>De 3.0.0 too4.0.0
### <a name="native-push"></a>Push nativo
Envio por push nativo (GCM/ADM) agora também é usado para em notificações de aplicativo para que você deve configurar credenciais de push nativo Olá para qualquer tipo de campanha de push.

Caso ainda não o tenha feito, siga [este procedimento](mobile-engagement-android-integrate-engagement-reach.md#native-push).

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Integração de Reach foi modificada em ``AndroidManifest.xml``.

Substitua:

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

Por

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>
    <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
      <intent-filter>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
      </intent-filter>
    </receiver>

Possivelmente, agora existe uma tela de carregamento quando você clica em um anúncio (com texto/conteúdo da web) ou uma pesquisa.
Você tem tooadd isso para esses toowork campanhas em 4.0.0:

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a>Recursos
Inserir saudação novo `res/layout/engagement_loading.xml` o arquivo no seu projeto.

## <a name="from-240-too300"></a>De 2.4.0 too3.0.0
Olá a seguir descrevem como toomigrate uma integração SDK da saudação Capptain serviço oferecido pelo Capptain SAS em um aplicativo da plataforma do Azure Mobile Engagement. Se você estiver migrando de uma versão anterior, consulte Olá Capptain site da web toomigrate too2.4.0 primeiro e depois aplicar Olá procedimento a seguir.

> [!IMPORTANT]
> Capptain Mobile Engagement não Olá mesmos serviços e são Olá procedimento indicado abaixo destaca somente como toomigrate Olá aplicativo cliente. Migrando Olá SDK no aplicativo hello não vai migrar seus dados do hello Capptain toohello Mobile Engagement de servidores.
> 
> 

### <a name="jar-file"></a>Arquivo JAR
Substitua `capptain.jar` por `mobile-engagement-VERSION.jar` em sua pasta `libs`.

### <a name="resource-files"></a>Arquivos de recurso
Cada arquivo de recurso que fornecemos (antecedidos `capptain_`) toobe substituiu por Olá novos (prefixadas com `engagement_`).

Se você personalizou os arquivos, você tem toore-aplicar a personalização nos novos arquivos de hello, **todos os identificadores de saudação em arquivos de recurso Olá também foram renomeados**.

### <a name="application-id"></a>ID do aplicativo
Agora o contrato usa um identificadores conexão cadeia de caracteres tooconfigure Olá SDK como identificador de aplicativo hello.

Você tem toouse `EngagementAgent.init` método em sua atividade de iniciador como este:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

cadeia de caracteres de conexão de saudação para seu aplicativo é exibida no Portal do Azure.

Remova qualquer chamada muito`CapptainAgent.configure` como `EngagementAgent.init` substitui esse método.

Olá `appId` não podem ser configuradas usando `AndroidManifest.xml`.

Remova esta seção de seu `AndroidManifest.xml` se você tiver:

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a>API Java
Cada chamada tooany classe Java do nosso SDK tem toobe renomeado; Por exemplo, `CapptainAgent.getInstance(this)` devem ser renomeados `EngagementAgent.getInstance(this)`, `extends CapptainActivity` devem ser renomeados `extends EngagementActivity` etc...

Se foram integradas com arquivos de preferência de agente padrão, o nome de arquivo hello padrão agora é `engagement.agent` e chave de saudação `engagement:agent`.

Ao criar notificações de web, Olá Javascript associador agora é `engagementReachContent`.

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Muitas alterações aconteceu existe, serviço de saudação não é mais compartilhado e muitos destinatários não podem ser exportadas mais.

declaração de serviço Olá agora é mais simples; Remover filtro intenção hello e todos os metadados dentro dele e adicionar `exportable=false`.

Além disso, tudo o que é o contrato de toouse renomeado.

Agora, ele deverá ficar parecido com:

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

Quando você quiser tooenable logs de teste, Olá metadados agora foi movido toohello marca de aplicativo e foi renomeado:

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

Todos os outros metadados apenas tem sido renomeados, aqui está a lista completa de saudação (claro renomear apenas Olá que você usar):

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

Controle do Google Play e SmartAd foi removida do SDK você que tooremove isso sem substituição:

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

atividades de alcance Olá agora são declaradas como este:

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

Se você tiver atividades personalizadas de alcance, você precisa apenas toochange Olá ações intencionais toomatch `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` ou `com.microsoft.azure.engagement.reach.intent.action.POLL`.

Olá receptores de transmissão foram renomeados, além de adicionarmos agora `exported=false`. Aqui está a lista completa Olá de receptores de saudação com nova especificação de Olá, (claro renomear apenas Olá que você usar):

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

Receptor de rastreamento tiver sido removido, para que você tenha tooremove nesta seção:

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

Observação a declaração de saudação da sua implementação de saudação difusão receptor **EngagementMessageReceiver** foi alterado em Olá `AndroidManifest.xml`. Isso ocorre porque toosend Olá API e remover XMPP arbitrário mensagens de entidades XMPP arbitrárias e Olá toosend API e receber mensagens entre os dispositivos foram removidos. Assim, você também tem Olá toodelete seguir retornos de chamada do seu **EngagementMessageReceiver** implementação:

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

e

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

exclua todas as chamadas em **EngagementAgent** para :

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

e

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a>ProGuard
Configuração ProGuard pode ser afetada pela rebranding Olá regras agora estão procurando como:

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

