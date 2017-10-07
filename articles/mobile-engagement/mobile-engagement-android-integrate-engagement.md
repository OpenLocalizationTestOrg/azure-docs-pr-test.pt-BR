---
title: "aaaAzure integração do Mobile Engagement Android SDK"
description: "Atualizações e procedimentos mais recentes para o SDK do Android do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a>Como tooIntegrate contrato no Android
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Este procedimento descreve hello mais simples maneira tooactivate contrato análise e monitoramento de funções em seu aplicativo do Android.

> [!IMPORTANT]
> O nível mínimo de API do Android SDK deve ser 10 ou superior (Android 2.3.3 ou superior).
> 
> 

Olá, as etapas a seguir é que suficientes relatório de saudação tooactivates dos logs necessário toocompute todas as estatísticas sobre usuários, sessões, atividades, falhas e Technicals. Olá relatório dos logs necessário toocompute outras estatísticas como trabalhos, erros e eventos devem ser feitos manualmente usando Olá contrato de API (consulte [como toouse Olá avançado Mobile Engagement marcação API em seu Android](mobile-engagement-android-use-engagement-api.md) desde que eles as estatísticas são depende do aplicativo.

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a>Inserir hello contrato SDK e serviço em seu projeto Android
Olá de download do SDK do Android [aqui](https://aka.ms/vq9mfn) obter `mobile-engagement-VERSION.jar` e colocá-los em Olá `libs` pasta do seu projeto Android (criar pasta de bibliotecas de saudação se ele ainda não existir).

> [!IMPORTANT]
> Se você criar seu pacote de aplicativo com ProGuard, será necessário tookeep algumas classes. Você pode usar o hello trecho de configuração a seguir:
> 
> -manter classe pública * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
> 
> <methods>; }
> 
> 

Especifique a cadeia de caracteres de conexão do contrato, Olá chamada seguinte método na atividade de iniciador hello:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

cadeia de caracteres de conexão de saudação para seu aplicativo é exibida no Portal do Azure.

* Se não, adicionar Olá as seguintes permissões Android (antes Olá `<application>` marca):
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* Adicionar Olá seção a seguir (entre hello `<application>` e `</application>` marcas):
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* Alterar `<Your application name>` por nome de saudação do seu aplicativo.

> [!TIP]
> Olá `android:label` atributo permite que você toochoose Olá nome da saudação serviço contrato como ele será exibido toohello os usuários finais na tela de "Serviços em execução" hello do seu telefone. É recomendável tooset esse atributo muito`"<Your application name>Service"` (por exemplo, `"AcmeFunGameService"`).
> 
> 

Olá especificando `android:process` atributo garante que o serviço de contrato Olá será executado em seu próprio processo (executando o contrato Olá mesmo processo que seu aplicativo fizer o thread principal de interfaces de usuário responsivo potencialmente menor).

> [!NOTE]
> Qualquer código que você coloca em `Application.onCreate()` e outras chamadas de retorno do aplicativo serão executadas para processos de todos os seus aplicativos, incluindo o serviço de contrato de saudação. Ele pode ter efeitos colaterais indesejáveis (como as alocações de memória desnecessários e threads no processo do contrato hello, duplicados receptores de difusão ou serviços).
> 
> 

Se você substituir `Application.onCreate()`, é recomendado tooadd Olá seguindo o trecho de código no início de saudação do seu `Application.onCreate()` função:

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

Você pode fazer Olá para a mesma coisa `Application.onTerminate()`, `Application.onLowMemory()` e `Application.onConfigurationChanged(...)`.

Você também pode estender `EngagementApplication` em vez de estender `Application`: Olá retorno de chamada `Application.onCreate()` Olá seleção de processo e chamadas `Application.onApplicationProcessCreate()` somente se processo atual Olá for não Olá uma saudação contrato serviço de hospedagem, hello mesmas regras se aplicam para Olá outras chamadas de retorno.

## <a name="basic-reporting"></a>Relatórios básicos
### <a name="recommended-method-overload-your-activity-classes"></a>Método recomendado: sobrecarregar suas classes `Activity`
No relatório de saudação tooactivate de ordem de todos os logs de saudação exigido pelo contrato toocompute usuários, sessões, atividades, falhas e estatísticas técnicas, você tem apenas toomake todos os seus `*Activity` subclasses herdam Olá correspondente `Engagement*Activity` classes (por exemplo, se a sua atividade herdada estende `ListActivity`, verifique se estende `EngagementListActivity`).

**Sem o Engagement :**

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

**Com o Engagement :**

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> Ao usar `EngagementListActivity` ou `EngagementExpandableListActivity`, certifique-se de que qualquer chamada muito`requestWindowFeature(...);` é feita antes da chamada de saudação muito`super.onCreate(...);`, caso contrário, ocorrerá uma falha.
> 
> 

Você pode encontrar essas classes no hello `src` pasta e pode copiá-los em seu projeto. classes de saudação também estão em hello **JavaDoc**.

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Método alternativo: chame `startActivity()` e `endActivity()` manualmente
Se você não pode ou não toooverload seu `Activity` classes, em vez disso, você pode começar e terminar suas atividades chamando `EngagementAgent`do métodos diretamente.

> [!IMPORTANT]
> Olá Android SDK nunca chama Olá `endActivity()` método, mesmo quando o aplicativo hello é fechado (no Android, aplicativos são, na verdade, nunca fechados). Portanto, é *altamente* recomendado Olá toocall `startActivity()` método hello `onResume` retorno de chamada de *todos os* suas atividades e Olá `endActivity()` método hello `onPause()` retorno de chamada de *todas as* suas atividades. Isso é Olá somente modo toobe-se de que as sessões não serão perdas. Se uma sessão é vazada, Olá serviço contrato nunca se desconectará do back-end de contrato de saudação (como serviço Olá permanece conectado enquanto uma sessão estiver pendente).
> 
> 

Aqui está um exemplo:

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

Este toohello muito semelhantes de exemplo `EngagementActivity` classe e suas variantes, cujo código-fonte é fornecido no hello `src` pasta.

## <a name="test"></a>Teste
Agora, verifique se a integração executando seu aplicativo móvel em um dispositivo ou emulador e verificar que ele registra uma sessão no guia do Monitor de saudação.

próximas seções de saudação são opcionais.

## <a name="location-reporting"></a>Relatórios de local
Se você quiser toobe locais relatado, você precisa tooadd algumas linhas de configuração (entre hello `<application>` e `</application>` marcas).

### <a name="lazy-area-location-reporting"></a>Relatórios de local de área lenta
Relatório de local de área lento permite país de saudação tooreport, região e localidade associados toodevices. Esse tipo de relatório de local usa apenas os locais de rede (com base na ID da célula ou WIFI). Olá dispositivo é relatada no máximo uma vez por sessão. Olá GPS nunca é usado e, portanto, esse tipo de relatório local tem poucos (não toosay nenhuma) impacto na bateria hello.

Relatado áreas são estatísticas de geográfica toocompute usado sobre usuários, sessões, eventos e erros. Elas também podem ser usadas como critério nas campanhas do Reach.

local de área lento tooenable reporting, você pode fazer isso usando a configuração de saudação mencionada anteriormente neste procedimento:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Você também precisa Olá tooadd permissão a seguir se ausentes:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Ou pode continuar usando ``ACCESS_FINE_LOCATION`` se você já usa em seu aplicativo.

### <a name="real-time-location-reporting"></a>Relatórios de local em tempo real
Relatório de local em tempo real permite latitude de saudação do tooreport e a longitude associada toodevices. Por padrão, esse tipo de relatório local usa apenas os locais de rede (com base na ID de célula ou Wi-Fi) e reporting Olá somente estará ativo quando o aplicativo hello é executado em primeiro plano (ou seja, durante uma sessão).

Locais de tempo real são *não* usado toocompute estatísticas. Seu único propósito é o uso de saudação do tooallow de geoinstalação em tempo real \<alcance-público-o isolamento geográfico\> critério de campanhas de alcance.

local em tempo real tooenable reporting, você pode fazer isso usando a configuração de saudação mencionada anteriormente neste procedimento:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Você também precisa Olá tooadd permissão a seguir se ausentes:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Ou pode continuar usando ``ACCESS_FINE_LOCATION`` se você já usa em seu aplicativo.

#### <a name="gps-based-reporting"></a>Relatórios com base em GPS
Por padrão, os relatórios de local em tempo real usam apenas locais com base em rede. uso de saudação do tooenable de GPS baseada em locais (que são muito mais precisas), use o objeto de configuração de saudação:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Você também precisa Olá tooadd permissão a seguir se ausentes:

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Relatório de segundo plano
Por padrão, relatórios de local em tempo real só está ativo quando o aplicativo hello é executado em primeiro plano (ou seja, durante uma sessão). tooenable Olá reporting também no plano de fundo, use o objeto de configuração Olá:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Quando o aplicativo hello é executado em segundo plano, locais de rede com base somente são relatados, mesmo se você tiver habilitado Olá GPS.
> 
> 

relatório de local do plano de fundo de saudação será interrompido se o usuário Olá reinicializar seu dispositivo, você pode adicionar esse toomake reiniciar automaticamente durante a inicialização:

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

Você também precisa Olá tooadd permissão a seguir se ausentes:

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a>Permissões do Android M
A partir do Android M, algumas permissões são gerenciadas em tempo de execução e precisam de aprovação do usuário.

permissões de tempo de execução de saudação serão desligadas por padrão para novas instalações do aplicativo se você selecionar o nível de API do Android 23. Caso contrário, elas serão ativadas por padrão.

usuário Olá pode habilitar/desabilitar essas permissões no menu de configurações de dispositivo de saudação. A desativação de permissões no menu de sistema interrompe processos em segundo plano do aplicativo hello, este é um comportamento do sistema e não tem nenhum impacto na capacidade tooreceive push no plano de fundo.

No contexto de saudação do Mobile Engagement, permissões de saudação que precisam de aprovação em tempo de execução são:

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* `WRITE_EXTERNAL_STORAGE` (somente para direcionamento de nível 23 da API do Android para essa)

armazenamento externo de saudação é usado apenas para o recurso de visão geral de alcance. Se você encontrar pedir que os usuários neste toobe permissão interrupções, você poderá removê-lo se usado somente para o Mobile Engagement, mas ao custo de saudação de desabilitar o recurso de visão geral.

Para recursos de local de Olá, você deve solicitar permissões toouser usando uma caixa de diálogo do sistema padrão. Se o usuário Olá aprova, será necessário tootell ``EngagementAgent`` tootake alterar em consideração em tempo real (alteração de saudação caso contrário será processado próximo tempo Olá usuário inicia Olá aplicativo hello).

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
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a>Relatórios avançados
Opcionalmente, se você quiser trabalhos, erros e eventos específicos do aplicativo tooreport, você precisa toouse Olá contrato de API por meio de métodos de saudação do hello `EngagementAgent` classe. Um objeto desta classe pode ser recuperados pela chamada hello `EngagementAgent.getInstance()` método estático.

Olá contrato API permite que toouse todos os recursos avançados do contrato e é detalhado no hello como tooUse a API de contrato no Android (bem como na documentação técnica Olá Olá `EngagementAgent` classe).

## <a name="advanced-configuration-in-androidmanifestxml"></a>Configuração avançada (em Androidmanifest.xml)
### <a name="wake-locks"></a>Bloqueios de ativação
Se você quiser toobe-se de que as estatísticas são enviadas em tempo real, ao usar o Wi-Fi ou tela hello está desativado, adicione Olá permissão opcional a seguir:

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a>Relatório de falha
Se você deseja obter relatórios de falha de toodisable, adicione (entre hello `<application>` e `</application>` marcas):

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Limite de intermitência
Por padrão, os relatórios de serviço de contrato de saudação logs em tempo real. Se seu aplicativo relatórios logs com muita frequência, é melhor toobuffer Olá logs e tooreport-los todos de uma vez em um base de tempo regulares (Isso é chamado hello "modo de disparo"). toodo assim, adicione (entre hello `<application>` e `</application>` marcas):

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Olá modo intermitente ligeiramente aumentar bateria Olá vida mas tem um impacto em Olá contrato Monitor: todas as sessões e trabalhos a duração será arredondado toohello intermitência limite (portanto, sessões e menor do que o limite de disparo Olá pode não estar visível de trabalhos). É recomendável toouse um limite de disparo não mais que 30000 (30 s).

### <a name="session-timeout"></a>Tempo limite da sessão
Por padrão, uma sessão é encerrada por 10 após o término de saudação de sua última atividade (que normalmente ocorre por pressionando Olá Home ou faça a chave, por definição Olá telefone ocioso ou pulando em outro aplicativo). Isso é tooavoid uma divisão de sessão cada usuário em tempo de saudação sair e retornar o aplicativo toohello rapidamente (o que pode acontecer quando ele escolher uma imagem, verifique a notificação, etc.). Talvez você queira toomodify esse parâmetro. toodo assim, adicione (entre hello `<application>` e `</application>` marcas):

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Desabilitar o relatório de log
### <a name="using-a-method-call"></a>Usando uma chamada de método
Se você quiser toostop contrato envio de logs, você pode chamar:

            EngagementAgent.getInstance(context).setEnabled(false);

Essa chamada é persistente: ela utiliza um arquivo de preferências compartilhado.

Se o contrato está ativo, quando você chamar essa função, pode levar 1 minuto para Olá toostop de serviço. No entanto, não é possível abrir serviço Olá Olá todos próxima vez que você iniciar o aplicativo hello.

Você pode habilitar o log de relatórios novamente chamando Olá a mesma função com `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Integração em seu próprio `PreferenceActivity`
Em vez de chamar essa função, você também pode integrar esta configuração diretamente em seu arquivo existente `PreferenceActivity`.

Você pode configurar contrato toouse suas preferências de arquivo (com modo desejado de saudação) Olá `AndroidManifest.xml` arquivo com `application meta-data`:

* Olá `engagement:agent:settings:name` chave é usado toodefine Olá nome do arquivo de preferências compartilhadas Olá.
* Olá `engagement:agent:settings:mode` chave toodefine usado o modo de saudação do arquivo de preferências compartilhadas hello, você deverá usar Olá mesmo modo que no seu `PreferenceActivity`. Olá modo deve ser passado como um número: se você estiver usando uma combinação de sinalizadores constantes em seu código, verifique o valor total de saudação.

Contrato sempre usar Olá `engagement:key` booliano chave no arquivo de preferências de saudação para gerenciar essa configuração.

Olá seguindo o exemplo de `AndroidManifest.xml` mostra Olá valores padrão:

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

Em seguida, você pode adicionar um `CheckBoxPreference` em seu layout de preferência como Olá seguindo um:

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
