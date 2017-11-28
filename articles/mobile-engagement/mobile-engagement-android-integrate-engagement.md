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
# <a name="how-toointegrate-engagement-on-android"></a><span data-ttu-id="b415e-103">Como tooIntegrate contrato no Android</span><span class="sxs-lookup"><span data-stu-id="b415e-103">How tooIntegrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b415e-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="b415e-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="b415e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="b415e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="b415e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="b415e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="b415e-107">Android</span><span class="sxs-lookup"><span data-stu-id="b415e-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="b415e-108">Este procedimento descreve hello mais simples maneira tooactivate contrato análise e monitoramento de funções em seu aplicativo do Android.</span><span class="sxs-lookup"><span data-stu-id="b415e-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b415e-109">O nível mínimo de API do Android SDK deve ser 10 ou superior (Android 2.3.3 ou superior).</span><span class="sxs-lookup"><span data-stu-id="b415e-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="b415e-110">Olá, as etapas a seguir é que suficientes relatório de saudação tooactivates dos logs necessário toocompute todas as estatísticas sobre usuários, sessões, atividades, falhas e Technicals.</span><span class="sxs-lookup"><span data-stu-id="b415e-110">hello following steps are enough tooactivates hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="b415e-111">Olá relatório dos logs necessário toocompute outras estatísticas como trabalhos, erros e eventos devem ser feitos manualmente usando Olá contrato de API (consulte [como toouse Olá avançado Mobile Engagement marcação API em seu Android](mobile-engagement-android-use-engagement-api.md) desde que eles as estatísticas são depende do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b415e-111">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="b415e-112">Inserir hello contrato SDK e serviço em seu projeto Android</span><span class="sxs-lookup"><span data-stu-id="b415e-112">Embed hello Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="b415e-113">Olá de download do SDK do Android [aqui](https://aka.ms/vq9mfn) obter `mobile-engagement-VERSION.jar` e colocá-los em Olá `libs` pasta do seu projeto Android (criar pasta de bibliotecas de saudação se ele ainda não existir).</span><span class="sxs-lookup"><span data-stu-id="b415e-113">Download hello Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into hello `libs` folder of your Android project (create hello libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b415e-114">Se você criar seu pacote de aplicativo com ProGuard, será necessário tookeep algumas classes.</span><span class="sxs-lookup"><span data-stu-id="b415e-114">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="b415e-115">Você pode usar o hello trecho de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="b415e-115">You can use hello following configuration snippet:</span></span>
> 
> <span data-ttu-id="b415e-116">-manter classe pública * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="b415e-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="b415e-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="b415e-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="b415e-118">Especifique a cadeia de caracteres de conexão do contrato, Olá chamada seguinte método na atividade de iniciador hello:</span><span class="sxs-lookup"><span data-stu-id="b415e-118">Specify your Engagement connection string by calling hello following method in hello launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="b415e-119">cadeia de caracteres de conexão de saudação para seu aplicativo é exibida no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b415e-119">hello connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="b415e-120">Se não, adicionar Olá as seguintes permissões Android (antes Olá `<application>` marca):</span><span class="sxs-lookup"><span data-stu-id="b415e-120">If missing, add hello following Android permissions (before hello `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="b415e-121">Adicionar Olá seção a seguir (entre hello `<application>` e `</application>` marcas):</span><span class="sxs-lookup"><span data-stu-id="b415e-121">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="b415e-122">Alterar `<Your application name>` por nome de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b415e-122">Change `<Your application name>` by hello name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="b415e-123">Olá `android:label` atributo permite que você toochoose Olá nome da saudação serviço contrato como ele será exibido toohello os usuários finais na tela de "Serviços em execução" hello do seu telefone.</span><span class="sxs-lookup"><span data-stu-id="b415e-123">hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it will appear toohello end-users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="b415e-124">É recomendável tooset esse atributo muito`"<Your application name>Service"` (por exemplo, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="b415e-124">It is recommended tooset this attribute too`"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="b415e-125">Olá especificando `android:process` atributo garante que o serviço de contrato Olá será executado em seu próprio processo (executando o contrato Olá mesmo processo que seu aplicativo fizer o thread principal de interfaces de usuário responsivo potencialmente menor).</span><span class="sxs-lookup"><span data-stu-id="b415e-125">Specifying hello `android:process` attribute ensures that hello Engagement service will run in its own process (running Engagement in hello same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="b415e-126">Qualquer código que você coloca em `Application.onCreate()` e outras chamadas de retorno do aplicativo serão executadas para processos de todos os seus aplicativos, incluindo o serviço de contrato de saudação.</span><span class="sxs-lookup"><span data-stu-id="b415e-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="b415e-127">Ele pode ter efeitos colaterais indesejáveis (como as alocações de memória desnecessários e threads no processo do contrato hello, duplicados receptores de difusão ou serviços).</span><span class="sxs-lookup"><span data-stu-id="b415e-127">It may have unwanted side effects (like unneeded memory allocations and threads in hello Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="b415e-128">Se você substituir `Application.onCreate()`, é recomendado tooadd Olá seguindo o trecho de código no início de saudação do seu `Application.onCreate()` função:</span><span class="sxs-lookup"><span data-stu-id="b415e-128">If you override `Application.onCreate()`, it's recommended tooadd hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="b415e-129">Você pode fazer Olá para a mesma coisa `Application.onTerminate()`, `Application.onLowMemory()` e `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="b415e-129">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="b415e-130">Você também pode estender `EngagementApplication` em vez de estender `Application`: Olá retorno de chamada `Application.onCreate()` Olá seleção de processo e chamadas `Application.onApplicationProcessCreate()` somente se processo atual Olá for não Olá uma saudação contrato serviço de hospedagem, hello mesmas regras se aplicam para Olá outras chamadas de retorno.</span><span class="sxs-lookup"><span data-stu-id="b415e-130">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="b415e-131">Relatórios básicos</span><span class="sxs-lookup"><span data-stu-id="b415e-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="b415e-132">Método recomendado: sobrecarregar suas classes `Activity`</span><span class="sxs-lookup"><span data-stu-id="b415e-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="b415e-133">No relatório de saudação tooactivate de ordem de todos os logs de saudação exigido pelo contrato toocompute usuários, sessões, atividades, falhas e estatísticas técnicas, você tem apenas toomake todos os seus `*Activity` subclasses herdam Olá correspondente `Engagement*Activity` classes (por exemplo, se a sua atividade herdada estende `ListActivity`, verifique se estende `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="b415e-133">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you just have toomake all your `*Activity` sub-classes inherit from hello corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="b415e-134">**Sem o Engagement :**</span><span class="sxs-lookup"><span data-stu-id="b415e-134">**Without Engagement :**</span></span>

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

<span data-ttu-id="b415e-135">**Com o Engagement :**</span><span class="sxs-lookup"><span data-stu-id="b415e-135">**With Engagement :**</span></span>

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
> <span data-ttu-id="b415e-136">Ao usar `EngagementListActivity` ou `EngagementExpandableListActivity`, certifique-se de que qualquer chamada muito`requestWindowFeature(...);` é feita antes da chamada de saudação muito`super.onCreate(...);`, caso contrário, ocorrerá uma falha.</span><span class="sxs-lookup"><span data-stu-id="b415e-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="b415e-137">Você pode encontrar essas classes no hello `src` pasta e pode copiá-los em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="b415e-137">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="b415e-138">classes de saudação também estão em hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="b415e-138">hello classes are also in hello **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="b415e-139">Método alternativo: chame `startActivity()` e `endActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="b415e-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="b415e-140">Se você não pode ou não toooverload seu `Activity` classes, em vez disso, você pode começar e terminar suas atividades chamando `EngagementAgent`do métodos diretamente.</span><span class="sxs-lookup"><span data-stu-id="b415e-140">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b415e-141">Olá Android SDK nunca chama Olá `endActivity()` método, mesmo quando o aplicativo hello é fechado (no Android, aplicativos são, na verdade, nunca fechados).</span><span class="sxs-lookup"><span data-stu-id="b415e-141">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="b415e-142">Portanto, é *altamente* recomendado Olá toocall `startActivity()` método hello `onResume` retorno de chamada de *todos os* suas atividades e Olá `endActivity()` método hello `onPause()` retorno de chamada de *todas as* suas atividades.</span><span class="sxs-lookup"><span data-stu-id="b415e-142">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="b415e-143">Isso é Olá somente modo toobe-se de que as sessões não serão perdas.</span><span class="sxs-lookup"><span data-stu-id="b415e-143">This is hello only way toobe sure that sessions will not be leaked.</span></span> <span data-ttu-id="b415e-144">Se uma sessão é vazada, Olá serviço contrato nunca se desconectará do back-end de contrato de saudação (como serviço Olá permanece conectado enquanto uma sessão estiver pendente).</span><span class="sxs-lookup"><span data-stu-id="b415e-144">If a session is leaked, hello Engagement service will never disconnect from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="b415e-145">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="b415e-145">Here is an example:</span></span>

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

<span data-ttu-id="b415e-146">Este toohello muito semelhantes de exemplo `EngagementActivity` classe e suas variantes, cujo código-fonte é fornecido no hello `src` pasta.</span><span class="sxs-lookup"><span data-stu-id="b415e-146">This example very similiar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="b415e-147">Teste</span><span class="sxs-lookup"><span data-stu-id="b415e-147">Test</span></span>
<span data-ttu-id="b415e-148">Agora, verifique se a integração executando seu aplicativo móvel em um dispositivo ou emulador e verificar que ele registra uma sessão no guia do Monitor de saudação.</span><span class="sxs-lookup"><span data-stu-id="b415e-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on hello Monitor tab.</span></span>

<span data-ttu-id="b415e-149">próximas seções de saudação são opcionais.</span><span class="sxs-lookup"><span data-stu-id="b415e-149">hello next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="b415e-150">Relatórios de local</span><span class="sxs-lookup"><span data-stu-id="b415e-150">Location reporting</span></span>
<span data-ttu-id="b415e-151">Se você quiser toobe locais relatado, você precisa tooadd algumas linhas de configuração (entre hello `<application>` e `</application>` marcas).</span><span class="sxs-lookup"><span data-stu-id="b415e-151">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="b415e-152">Relatórios de local de área lenta</span><span class="sxs-lookup"><span data-stu-id="b415e-152">Lazy area location reporting</span></span>
<span data-ttu-id="b415e-153">Relatório de local de área lento permite país de saudação tooreport, região e localidade associados toodevices.</span><span class="sxs-lookup"><span data-stu-id="b415e-153">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="b415e-154">Esse tipo de relatório de local usa apenas os locais de rede (com base na ID da célula ou WIFI).</span><span class="sxs-lookup"><span data-stu-id="b415e-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="b415e-155">Olá dispositivo é relatada no máximo uma vez por sessão.</span><span class="sxs-lookup"><span data-stu-id="b415e-155">hello device area is reported at most once per session.</span></span> <span data-ttu-id="b415e-156">Olá GPS nunca é usado e, portanto, esse tipo de relatório local tem poucos (não toosay nenhuma) impacto na bateria hello.</span><span class="sxs-lookup"><span data-stu-id="b415e-156">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="b415e-157">Relatado áreas são estatísticas de geográfica toocompute usado sobre usuários, sessões, eventos e erros.</span><span class="sxs-lookup"><span data-stu-id="b415e-157">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="b415e-158">Elas também podem ser usadas como critério nas campanhas do Reach.</span><span class="sxs-lookup"><span data-stu-id="b415e-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="b415e-159">local de área lento tooenable reporting, você pode fazer isso usando a configuração de saudação mencionada anteriormente neste procedimento:</span><span class="sxs-lookup"><span data-stu-id="b415e-159">tooenable lazy area location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="b415e-160">Você também precisa Olá tooadd permissão a seguir se ausentes:</span><span class="sxs-lookup"><span data-stu-id="b415e-160">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="b415e-161">Ou pode continuar usando ``ACCESS_FINE_LOCATION`` se você já usa em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b415e-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="b415e-162">Relatórios de local em tempo real</span><span class="sxs-lookup"><span data-stu-id="b415e-162">Real time location reporting</span></span>
<span data-ttu-id="b415e-163">Relatório de local em tempo real permite latitude de saudação do tooreport e a longitude associada toodevices.</span><span class="sxs-lookup"><span data-stu-id="b415e-163">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="b415e-164">Por padrão, esse tipo de relatório local usa apenas os locais de rede (com base na ID de célula ou Wi-Fi) e reporting Olá somente estará ativo quando o aplicativo hello é executado em primeiro plano (ou seja, durante uma sessão).</span><span class="sxs-lookup"><span data-stu-id="b415e-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="b415e-165">Locais de tempo real são *não* usado toocompute estatísticas.</span><span class="sxs-lookup"><span data-stu-id="b415e-165">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="b415e-166">Seu único propósito é o uso de saudação do tooallow de geoinstalação em tempo real \<alcance-público-o isolamento geográfico\> critério de campanhas de alcance.</span><span class="sxs-lookup"><span data-stu-id="b415e-166">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="b415e-167">local em tempo real tooenable reporting, você pode fazer isso usando a configuração de saudação mencionada anteriormente neste procedimento:</span><span class="sxs-lookup"><span data-stu-id="b415e-167">tooenable real time location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="b415e-168">Você também precisa Olá tooadd permissão a seguir se ausentes:</span><span class="sxs-lookup"><span data-stu-id="b415e-168">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="b415e-169">Ou pode continuar usando ``ACCESS_FINE_LOCATION`` se você já usa em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b415e-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="b415e-170">Relatórios com base em GPS</span><span class="sxs-lookup"><span data-stu-id="b415e-170">GPS based reporting</span></span>
<span data-ttu-id="b415e-171">Por padrão, os relatórios de local em tempo real usam apenas locais com base em rede.</span><span class="sxs-lookup"><span data-stu-id="b415e-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="b415e-172">uso de saudação do tooenable de GPS baseada em locais (que são muito mais precisas), use o objeto de configuração de saudação:</span><span class="sxs-lookup"><span data-stu-id="b415e-172">tooenable hello use of GPS based locations (which are far more precise), use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="b415e-173">Você também precisa Olá tooadd permissão a seguir se ausentes:</span><span class="sxs-lookup"><span data-stu-id="b415e-173">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="b415e-174">Relatório de segundo plano</span><span class="sxs-lookup"><span data-stu-id="b415e-174">Background reporting</span></span>
<span data-ttu-id="b415e-175">Por padrão, relatórios de local em tempo real só está ativo quando o aplicativo hello é executado em primeiro plano (ou seja, durante uma sessão).</span><span class="sxs-lookup"><span data-stu-id="b415e-175">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="b415e-176">tooenable Olá reporting também no plano de fundo, use o objeto de configuração Olá:</span><span class="sxs-lookup"><span data-stu-id="b415e-176">tooenable hello reporting also in background, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="b415e-177">Quando o aplicativo hello é executado em segundo plano, locais de rede com base somente são relatados, mesmo se você tiver habilitado Olá GPS.</span><span class="sxs-lookup"><span data-stu-id="b415e-177">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="b415e-178">relatório de local do plano de fundo de saudação será interrompido se o usuário Olá reinicializar seu dispositivo, você pode adicionar esse toomake reiniciar automaticamente durante a inicialização:</span><span class="sxs-lookup"><span data-stu-id="b415e-178">hello background location report will be stopped if hello user reboots its device, you can add this toomake it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="b415e-179">Você também precisa Olá tooadd permissão a seguir se ausentes:</span><span class="sxs-lookup"><span data-stu-id="b415e-179">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="b415e-180">Permissões do Android M</span><span class="sxs-lookup"><span data-stu-id="b415e-180">Android M permissions</span></span>
<span data-ttu-id="b415e-181">A partir do Android M, algumas permissões são gerenciadas em tempo de execução e precisam de aprovação do usuário.</span><span class="sxs-lookup"><span data-stu-id="b415e-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="b415e-182">permissões de tempo de execução de saudação serão desligadas por padrão para novas instalações do aplicativo se você selecionar o nível de API do Android 23.</span><span class="sxs-lookup"><span data-stu-id="b415e-182">hello runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="b415e-183">Caso contrário, elas serão ativadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="b415e-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="b415e-184">usuário Olá pode habilitar/desabilitar essas permissões no menu de configurações de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b415e-184">hello user can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="b415e-185">A desativação de permissões no menu de sistema interrompe processos em segundo plano do aplicativo hello, este é um comportamento do sistema e não tem nenhum impacto na capacidade tooreceive push no plano de fundo.</span><span class="sxs-lookup"><span data-stu-id="b415e-185">Turning off permissions from system menu kills background processes of hello application, this is a system behavior and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="b415e-186">No contexto de saudação do Mobile Engagement, permissões de saudação que precisam de aprovação em tempo de execução são:</span><span class="sxs-lookup"><span data-stu-id="b415e-186">In hello context of Mobile Engagement, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="b415e-187">`WRITE_EXTERNAL_STORAGE` (somente para direcionamento de nível 23 da API do Android para essa)</span><span class="sxs-lookup"><span data-stu-id="b415e-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="b415e-188">armazenamento externo de saudação é usado apenas para o recurso de visão geral de alcance.</span><span class="sxs-lookup"><span data-stu-id="b415e-188">hello external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="b415e-189">Se você encontrar pedir que os usuários neste toobe permissão interrupções, você poderá removê-lo se usado somente para o Mobile Engagement, mas ao custo de saudação de desabilitar o recurso de visão geral.</span><span class="sxs-lookup"><span data-stu-id="b415e-189">If you find asking users this permission toobe disruptive, you can remove it if you used it only for Mobile Engagement but at hello cost of disabling big picture feature.</span></span>

<span data-ttu-id="b415e-190">Para recursos de local de Olá, você deve solicitar permissões toouser usando uma caixa de diálogo do sistema padrão.</span><span class="sxs-lookup"><span data-stu-id="b415e-190">For hello location features, you should request permissions toouser using a standard system dialog.</span></span> <span data-ttu-id="b415e-191">Se o usuário Olá aprova, será necessário tootell ``EngagementAgent`` tootake alterar em consideração em tempo real (alteração de saudação caso contrário será processado próximo tempo Olá usuário inicia Olá aplicativo hello).</span><span class="sxs-lookup"><span data-stu-id="b415e-191">If hello user approves, you need tootell ``EngagementAgent`` tootake that change into account in real time (otherwise hello change will be processed hello next time hello user launches hello application).</span></span>

<span data-ttu-id="b415e-192">Aqui está um toouse de exemplo de código em uma atividade de permissões do aplicativo toorequest e resultado Olá forward positivo muito``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="b415e-192">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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

## <a name="advanced-reporting"></a><span data-ttu-id="b415e-193">Relatórios avançados</span><span class="sxs-lookup"><span data-stu-id="b415e-193">Advanced reporting</span></span>
<span data-ttu-id="b415e-194">Opcionalmente, se você quiser trabalhos, erros e eventos específicos do aplicativo tooreport, você precisa toouse Olá contrato de API por meio de métodos de saudação do hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="b415e-194">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="b415e-195">Um objeto desta classe pode ser recuperados pela chamada hello `EngagementAgent.getInstance()` método estático.</span><span class="sxs-lookup"><span data-stu-id="b415e-195">An object of this class can be retreived by calling hello `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="b415e-196">Olá contrato API permite que toouse todos os recursos avançados do contrato e é detalhado no hello como tooUse a API de contrato no Android (bem como na documentação técnica Olá Olá `EngagementAgent` classe).</span><span class="sxs-lookup"><span data-stu-id="b415e-196">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on Android (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="b415e-197">Configuração avançada (em Androidmanifest.xml)</span><span class="sxs-lookup"><span data-stu-id="b415e-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="b415e-198">Bloqueios de ativação</span><span class="sxs-lookup"><span data-stu-id="b415e-198">Wake locks</span></span>
<span data-ttu-id="b415e-199">Se você quiser toobe-se de que as estatísticas são enviadas em tempo real, ao usar o Wi-Fi ou tela hello está desativado, adicione Olá permissão opcional a seguir:</span><span class="sxs-lookup"><span data-stu-id="b415e-199">If you want toobe sure that statistics are sent in real time when using Wifi or when hello screen is off, add hello following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="b415e-200">Relatório de falha</span><span class="sxs-lookup"><span data-stu-id="b415e-200">Crash report</span></span>
<span data-ttu-id="b415e-201">Se você deseja obter relatórios de falha de toodisable, adicione (entre hello `<application>` e `</application>` marcas):</span><span class="sxs-lookup"><span data-stu-id="b415e-201">If you want toodisable crash reports, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="b415e-202">Limite de intermitência</span><span class="sxs-lookup"><span data-stu-id="b415e-202">Burst threshold</span></span>
<span data-ttu-id="b415e-203">Por padrão, os relatórios de serviço de contrato de saudação logs em tempo real.</span><span class="sxs-lookup"><span data-stu-id="b415e-203">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="b415e-204">Se seu aplicativo relatórios logs com muita frequência, é melhor toobuffer Olá logs e tooreport-los todos de uma vez em um base de tempo regulares (Isso é chamado hello "modo de disparo").</span><span class="sxs-lookup"><span data-stu-id="b415e-204">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello "burst mode").</span></span> <span data-ttu-id="b415e-205">toodo assim, adicione (entre hello `<application>` e `</application>` marcas):</span><span class="sxs-lookup"><span data-stu-id="b415e-205">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="b415e-206">Olá modo intermitente ligeiramente aumentar bateria Olá vida mas tem um impacto em Olá contrato Monitor: todas as sessões e trabalhos a duração será arredondado toohello intermitência limite (portanto, sessões e menor do que o limite de disparo Olá pode não estar visível de trabalhos).</span><span class="sxs-lookup"><span data-stu-id="b415e-206">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="b415e-207">É recomendável toouse um limite de disparo não mais que 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="b415e-207">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="b415e-208">Tempo limite da sessão</span><span class="sxs-lookup"><span data-stu-id="b415e-208">Session timeout</span></span>
<span data-ttu-id="b415e-209">Por padrão, uma sessão é encerrada por 10 após o término de saudação de sua última atividade (que normalmente ocorre por pressionando Olá Home ou faça a chave, por definição Olá telefone ocioso ou pulando em outro aplicativo).</span><span class="sxs-lookup"><span data-stu-id="b415e-209">By default, a session is ended 10s after hello end of its last activity (which usually occurs by pressing hello Home or Back key, by setting hello phone idle or by jumping into another application).</span></span> <span data-ttu-id="b415e-210">Isso é tooavoid uma divisão de sessão cada usuário em tempo de saudação sair e retornar o aplicativo toohello rapidamente (o que pode acontecer quando ele escolher uma imagem, verifique a notificação, etc.).</span><span class="sxs-lookup"><span data-stu-id="b415e-210">This is tooavoid a session split each time hello user exit and return toohello application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="b415e-211">Talvez você queira toomodify esse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b415e-211">You may want toomodify this parameter.</span></span> <span data-ttu-id="b415e-212">toodo assim, adicione (entre hello `<application>` e `</application>` marcas):</span><span class="sxs-lookup"><span data-stu-id="b415e-212">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="b415e-213">Desabilitar o relatório de log</span><span class="sxs-lookup"><span data-stu-id="b415e-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="b415e-214">Usando uma chamada de método</span><span class="sxs-lookup"><span data-stu-id="b415e-214">Using a method call</span></span>
<span data-ttu-id="b415e-215">Se você quiser toostop contrato envio de logs, você pode chamar:</span><span class="sxs-lookup"><span data-stu-id="b415e-215">If you want Engagement toostop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="b415e-216">Essa chamada é persistente: ela utiliza um arquivo de preferências compartilhado.</span><span class="sxs-lookup"><span data-stu-id="b415e-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="b415e-217">Se o contrato está ativo, quando você chamar essa função, pode levar 1 minuto para Olá toostop de serviço.</span><span class="sxs-lookup"><span data-stu-id="b415e-217">If Engagement is active when you call this function, it may take 1 minute for hello service toostop.</span></span> <span data-ttu-id="b415e-218">No entanto, não é possível abrir serviço Olá Olá todos próxima vez que você iniciar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b415e-218">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="b415e-219">Você pode habilitar o log de relatórios novamente chamando Olá a mesma função com `true`.</span><span class="sxs-lookup"><span data-stu-id="b415e-219">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="b415e-220">Integração em seu próprio `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="b415e-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="b415e-221">Em vez de chamar essa função, você também pode integrar esta configuração diretamente em seu arquivo existente `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="b415e-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="b415e-222">Você pode configurar contrato toouse suas preferências de arquivo (com modo desejado de saudação) Olá `AndroidManifest.xml` arquivo com `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="b415e-222">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="b415e-223">Olá `engagement:agent:settings:name` chave é usado toodefine Olá nome do arquivo de preferências compartilhadas Olá.</span><span class="sxs-lookup"><span data-stu-id="b415e-223">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="b415e-224">Olá `engagement:agent:settings:mode` chave toodefine usado o modo de saudação do arquivo de preferências compartilhadas hello, você deverá usar Olá mesmo modo que no seu `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="b415e-224">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file, you should use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="b415e-225">Olá modo deve ser passado como um número: se você estiver usando uma combinação de sinalizadores constantes em seu código, verifique o valor total de saudação.</span><span class="sxs-lookup"><span data-stu-id="b415e-225">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="b415e-226">Contrato sempre usar Olá `engagement:key` booliano chave no arquivo de preferências de saudação para gerenciar essa configuração.</span><span class="sxs-lookup"><span data-stu-id="b415e-226">Engagement always use hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="b415e-227">Olá seguindo o exemplo de `AndroidManifest.xml` mostra Olá valores padrão:</span><span class="sxs-lookup"><span data-stu-id="b415e-227">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="b415e-228">Em seguida, você pode adicionar um `CheckBoxPreference` em seu layout de preferência como Olá seguindo um:</span><span class="sxs-lookup"><span data-stu-id="b415e-228">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
