---
title: "Integração do SDK do Android do Azure Mobile Engagement"
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
ms.openlocfilehash: 35bd92e52b7a02f58620a03156902f9f91be57ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-on-android"></a><span data-ttu-id="f9024-103">Como integrar o Engagement ao Android</span><span class="sxs-lookup"><span data-stu-id="f9024-103">How to Integrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9024-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="f9024-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="f9024-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="f9024-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="f9024-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f9024-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="f9024-107">Android</span><span class="sxs-lookup"><span data-stu-id="f9024-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="f9024-108">Este procedimento descreve a maneira mais simples de ativar as funções de Análise e Monitoramento do Engagement em seu aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="f9024-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9024-109">O nível mínimo de API do Android SDK deve ser 10 ou superior (Android 2.3.3 ou superior).</span><span class="sxs-lookup"><span data-stu-id="f9024-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="f9024-110">As etapas a seguir são suficientes para ativar o relatório de logs necessário para calcular todas as estatísticas referentes a Usuários, Sessões, Atividades, Falhas e Suporte Técnico.</span><span class="sxs-lookup"><span data-stu-id="f9024-110">The following steps are enough to activates the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="f9024-111">O relatório de logs necessários para calcular outras estatísticas, como Trabalhos, Erros e Eventos deve ser feito manualmente usando a API do Engagement (consulte [Como usar a marcação avançada de API do Mobile Engagement em seu Android](mobile-engagement-android-use-engagement-api.md) já que essas estatísticas são dependentes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9024-111">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="f9024-112">Incorpore o SDK e serviço do Engagement em seu projeto Android</span><span class="sxs-lookup"><span data-stu-id="f9024-112">Embed the Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="f9024-113">Baixe o Android SDK [aqui](https://aka.ms/vq9mfn) Obtenha `mobile-engagement-VERSION.jar` e coloque-as na pasta `libs` do seu projeto Android (crie a pasta de bibliotecas se ela ainda não existir).</span><span class="sxs-lookup"><span data-stu-id="f9024-113">Download the Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into the `libs` folder of your Android project (create the libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9024-114">Se você compilar seu pacote de aplicativo com o ProGuard, você precisa manter algumas classes.</span><span class="sxs-lookup"><span data-stu-id="f9024-114">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="f9024-115">Você pode usar o seguinte trecho de código de configuração:</span><span class="sxs-lookup"><span data-stu-id="f9024-115">You can use the following configuration snippet:</span></span>
> 
> <span data-ttu-id="f9024-116">-manter classe pública * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="f9024-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="f9024-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="f9024-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="f9024-118">Especifique a cadeia de conexão do Engagement chamando o método a seguir na atividade de inicializador:</span><span class="sxs-lookup"><span data-stu-id="f9024-118">Specify your Engagement connection string by calling the following method in the launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f9024-119">A cadeia de conexão para o seu aplicativo é exibida no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9024-119">The connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="f9024-120">Se estiver faltando, adicione as seguintes permissões do Android (antes da marca `<application>`):</span><span class="sxs-lookup"><span data-stu-id="f9024-120">If missing, add the following Android permissions (before the `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="f9024-121">Adicione a seção a seguir (entre as marcas `<application>` e `</application>`):</span><span class="sxs-lookup"><span data-stu-id="f9024-121">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="f9024-122">Substitua `<Your application name>` pelo nome do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9024-122">Change `<Your application name>` by the name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="f9024-123">A chave `android:label` permite que você escolha o nome do serviço do Engagement como ele aparecerá para os usuários finais na tela "Serviços em execução" dos seus respectivos telefones.</span><span class="sxs-lookup"><span data-stu-id="f9024-123">The `android:label` attribute allows you to choose the name of the Engagement service as it will appear to the end-users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="f9024-124">É recomendável definir esse atributo para `"<Your application name>Service"` (por exemplo, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="f9024-124">It is recommended to set this attribute to `"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="f9024-125">Especificar o atributo `android:process` garante que o serviço do Engagement será executado em seu próprio processo (executando o Engagement no mesmo processo que seu aplicativo fará o thread/interface de usuário principal potencialmente menos responsivos).</span><span class="sxs-lookup"><span data-stu-id="f9024-125">Specifying the `android:process` attribute ensures that the Engagement service will run in its own process (running Engagement in the same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="f9024-126">Qualquer código que você colocar em `Application.onCreate()` e outros retornos de chamada do aplicativo serão executados para todos os processos de seu aplicativo, incluindo o serviço Engagement.</span><span class="sxs-lookup"><span data-stu-id="f9024-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="f9024-127">Ele pode ter efeitos colaterais indesejados (como alocações desnecessárias e threads no processo do Engagement, serviços ou receptores de difusão duplicados).</span><span class="sxs-lookup"><span data-stu-id="f9024-127">It may have unwanted side effects (like unneeded memory allocations and threads in the Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="f9024-128">Se você substituir `Application.onCreate()`, recomenda-se adicionar o seguinte trecho de código no início da sua função `Application.onCreate()`:</span><span class="sxs-lookup"><span data-stu-id="f9024-128">If you override `Application.onCreate()`, it's recommended to add the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="f9024-129">Você pode fazer a mesma coisa para `Application.onTerminate()`, `Application.onLowMemory()` e `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="f9024-129">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="f9024-130">Você também pode estender `EngagementApplication` em vez de ampliar `Application`: o retorno de chamada `Application.onCreate()` faz a verificação do processo e chama `Application.onApplicationProcessCreate()` somente se o processo atual não for aquele que hospeda o serviço do Engagement. As mesmas regras se aplicam para os outros retornos de chamada.</span><span class="sxs-lookup"><span data-stu-id="f9024-130">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="f9024-131">Relatórios básicos</span><span class="sxs-lookup"><span data-stu-id="f9024-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="f9024-132">Método recomendado: sobrecarregar suas classes `Activity`</span><span class="sxs-lookup"><span data-stu-id="f9024-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="f9024-133">Para ativar o relatório de todos os logs exigidos pelo Engagement para calcular os Usuários, Sessões, Atividades, Falhas e Estatísticas técnicas, você só precisa fazer com que todas as suas subclasses `*Activity` herdem classes `Engagement*Activity` correspondentes (por exemplo, se sua atividade herdada estende `ListActivity`, faça com que ela estenda `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="f9024-133">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you just have to make all your `*Activity` sub-classes inherit from the corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="f9024-134">**Sem o Engagement :**</span><span class="sxs-lookup"><span data-stu-id="f9024-134">**Without Engagement :**</span></span>

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

<span data-ttu-id="f9024-135">**Com o Engagement :**</span><span class="sxs-lookup"><span data-stu-id="f9024-135">**With Engagement :**</span></span>

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
> <span data-ttu-id="f9024-136">Ao usar `EngagementListActivity` ou `EngagementExpandableListActivity`, certifique-se de que qualquer chamada para `requestWindowFeature(...);` seja feita antes da chamada para `super.onCreate(...);`, caso contrário, ocorrerá uma falha.</span><span class="sxs-lookup"><span data-stu-id="f9024-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="f9024-137">Você pode encontrar essas classes na pasta `src` e copiá-las para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="f9024-137">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="f9024-138">As classes também estão no **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="f9024-138">The classes are also in the **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="f9024-139">Método alternativo: chame `startActivity()` e `endActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="f9024-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="f9024-140">Se você não pode ou não quer sobrecarregar as suas classes `Activity`, é possível iniciar suas atividades chamando diretamente os métodos de `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="f9024-140">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9024-141">O SDK do Android nunca chama o método `endActivity()`, mesmo quando o aplicativo é fechado (no Android, aplicativos nunca são, na verdade, fechados).</span><span class="sxs-lookup"><span data-stu-id="f9024-141">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="f9024-142">Dessa forma, é *ALTAMENTE* recomendável chamar o método `startActivity()` no retorno de chamada `onResume` de *TODAS* as suas atividades, e o método `endActivity()` no retorno de chamada `onPause()` de *TODAS* as suas atividades.</span><span class="sxs-lookup"><span data-stu-id="f9024-142">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="f9024-143">Essa é a única maneira de certificar-se de que as sessões não serão perdidas.</span><span class="sxs-lookup"><span data-stu-id="f9024-143">This is the only way to be sure that sessions will not be leaked.</span></span> <span data-ttu-id="f9024-144">Se ocorrer perda de uma sessão, o serviço Engagement nunca se desconectará do back-end do Engagement (desde que o serviço permaneça conectado enquanto houver uma sessão pendente).</span><span class="sxs-lookup"><span data-stu-id="f9024-144">If a session is leaked, the Engagement service will never disconnect from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="f9024-145">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="f9024-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="f9024-146">Este exemplo é muito semelhante à classe `EngagementActivity` e suas variantes, cujo código-fonte é fornecido na pasta `src`.</span><span class="sxs-lookup"><span data-stu-id="f9024-146">This example very similiar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="f9024-147">Teste</span><span class="sxs-lookup"><span data-stu-id="f9024-147">Test</span></span>
<span data-ttu-id="f9024-148">Agora, verifique se a integração ao executar seu aplicativo móvel em um dispositivo ou emulador e verifique se ele registra uma sessão na guia Monitor.</span><span class="sxs-lookup"><span data-stu-id="f9024-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on the Monitor tab.</span></span>

<span data-ttu-id="f9024-149">As seções a seguir são opcionais.</span><span class="sxs-lookup"><span data-stu-id="f9024-149">The next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="f9024-150">Relatórios de local</span><span class="sxs-lookup"><span data-stu-id="f9024-150">Location reporting</span></span>
<span data-ttu-id="f9024-151">Se quiser que locais sejam informados, você precisa adicionar algumas linhas de configuração (entre as marcas `<application>` e `</application>`).</span><span class="sxs-lookup"><span data-stu-id="f9024-151">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="f9024-152">Relatórios de local de área lenta</span><span class="sxs-lookup"><span data-stu-id="f9024-152">Lazy area location reporting</span></span>
<span data-ttu-id="f9024-153">O relatório de local de área lenta permite relatar o país, a região e a localidade associados aos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f9024-153">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="f9024-154">Esse tipo de relatório de local usa apenas os locais de rede (com base na ID da célula ou WIFI).</span><span class="sxs-lookup"><span data-stu-id="f9024-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="f9024-155">A área de dispositivo é relatada no máximo uma vez por sessão.</span><span class="sxs-lookup"><span data-stu-id="f9024-155">The device area is reported at most once per session.</span></span> <span data-ttu-id="f9024-156">O GPS nunca é usado e, portanto, esse tipo de relatório de local tem pouco impacto (ou quase nenhum) sobre a bateria.</span><span class="sxs-lookup"><span data-stu-id="f9024-156">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="f9024-157">As áreas relatadas são usadas para computar as estatísticas geográficas sobre usuários, sessões, eventos e erros.</span><span class="sxs-lookup"><span data-stu-id="f9024-157">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="f9024-158">Elas também podem ser usadas como critério nas campanhas do Reach.</span><span class="sxs-lookup"><span data-stu-id="f9024-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="f9024-159">Para habilitar o relatório de localização de área simples, você pode fazer isso usando a configuração mencionada anteriormente neste procedimento:</span><span class="sxs-lookup"><span data-stu-id="f9024-159">To enable lazy area location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f9024-160">Você também precisa adicionar a permissão a seguir, se estiver ausente:</span><span class="sxs-lookup"><span data-stu-id="f9024-160">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="f9024-161">Ou pode continuar usando ``ACCESS_FINE_LOCATION`` se você já usa em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9024-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="f9024-162">Relatórios de local em tempo real</span><span class="sxs-lookup"><span data-stu-id="f9024-162">Real time location reporting</span></span>
<span data-ttu-id="f9024-163">Os relatórios de local em tempo real permitem relatar a latitude e a longitude associados aos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f9024-163">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="f9024-164">Por padrão, esse tipo de relatório local usa apenas os locais de rede (com base na ID da célula ou WIFI) e o relatório estará disponível apenas quando o aplicativo for executado em primeiro plano (ou seja, durante uma sessão).</span><span class="sxs-lookup"><span data-stu-id="f9024-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="f9024-165">Os locais em tempo real *NÃO* são usados para calcular estatísticas.</span><span class="sxs-lookup"><span data-stu-id="f9024-165">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="f9024-166">Sua única finalidade é permitir o uso do critério de isolamento geográfico em tempo real \<Reach-Audience-geofencing\> em campanhas de alcance.</span><span class="sxs-lookup"><span data-stu-id="f9024-166">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="f9024-167">Para habilitar o relatório local em tempo real, você pode fazer isso usando a configuração mencionada anteriormente neste procedimento:</span><span class="sxs-lookup"><span data-stu-id="f9024-167">To enable real time location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f9024-168">Você também precisa adicionar a permissão a seguir, se estiver ausente:</span><span class="sxs-lookup"><span data-stu-id="f9024-168">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="f9024-169">Ou pode continuar usando ``ACCESS_FINE_LOCATION`` se você já usa em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9024-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="f9024-170">Relatórios com base em GPS</span><span class="sxs-lookup"><span data-stu-id="f9024-170">GPS based reporting</span></span>
<span data-ttu-id="f9024-171">Por padrão, os relatórios de local em tempo real usam apenas locais com base em rede.</span><span class="sxs-lookup"><span data-stu-id="f9024-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="f9024-172">Para habilitar o uso do GPS com base em locais (que são muito mais precisos), use o objeto de configuração:</span><span class="sxs-lookup"><span data-stu-id="f9024-172">To enable the use of GPS based locations (which are far more precise), use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f9024-173">Você também precisa adicionar a permissão a seguir, se estiver ausente:</span><span class="sxs-lookup"><span data-stu-id="f9024-173">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="f9024-174">Relatório de segundo plano</span><span class="sxs-lookup"><span data-stu-id="f9024-174">Background reporting</span></span>
<span data-ttu-id="f9024-175">Por padrão, os relatórios de local em tempo real ficam ativos apenas quando o aplicativo é executado em primeiro plano (ou seja, durante uma sessão).</span><span class="sxs-lookup"><span data-stu-id="f9024-175">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="f9024-176">Para habilitar o relatório também em segundo plano, use o objeto de configuração:</span><span class="sxs-lookup"><span data-stu-id="f9024-176">To enable the reporting also in background, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="f9024-177">Quando o aplicativo é executado em segundo plano, somente locais baseados em rede são relatados, mesmo se você tiver habilitado o GPS.</span><span class="sxs-lookup"><span data-stu-id="f9024-177">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="f9024-178">O relatório de local de segundo plano será interrompido se o usuário reiniciar o dispositivo; você pode adicionar isso para fazê-lo reiniciar automaticamente no momento de inicialização:</span><span class="sxs-lookup"><span data-stu-id="f9024-178">The background location report will be stopped if the user reboots its device, you can add this to make it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="f9024-179">Você também precisa adicionar a permissão a seguir, se estiver ausente:</span><span class="sxs-lookup"><span data-stu-id="f9024-179">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="f9024-180">Permissões do Android M</span><span class="sxs-lookup"><span data-stu-id="f9024-180">Android M permissions</span></span>
<span data-ttu-id="f9024-181">A partir do Android M, algumas permissões são gerenciadas em tempo de execução e precisam de aprovação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f9024-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="f9024-182">As permissões de tempo de execução serão desativadas por padrão para novas instalações do aplicativo se você selecionar o nível 23 da API do Android.</span><span class="sxs-lookup"><span data-stu-id="f9024-182">The runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="f9024-183">Caso contrário, elas serão ativadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="f9024-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="f9024-184">O usuário pode habilitar/desabilitar essas permissões no menu de configurações do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f9024-184">The user can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="f9024-185">A desativação de permissões no menu do sistema interrompe os processos em segundo plano do aplicativo; esse é um comportamento do sistema e não tem nenhum impacto na capacidade de receber push em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="f9024-185">Turning off permissions from system menu kills background processes of the application, this is a system behavior and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="f9024-186">No contexto do Mobile Engagement, as permissões que exigem aprovação em tempo de execução são:</span><span class="sxs-lookup"><span data-stu-id="f9024-186">In the context of Mobile Engagement, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="f9024-187">`WRITE_EXTERNAL_STORAGE` (somente para direcionamento de nível 23 da API do Android para essa)</span><span class="sxs-lookup"><span data-stu-id="f9024-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="f9024-188">O armazenamento externo é usado apenas para o recurso Acessar visão global.</span><span class="sxs-lookup"><span data-stu-id="f9024-188">The external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="f9024-189">Se você acha que pedir essa permissão aos usuários é incômodo, é possível removê-la se a usou somente para o Mobile Engagement, mas isso desabilitará o recurso de visão global.</span><span class="sxs-lookup"><span data-stu-id="f9024-189">If you find asking users this permission to be disruptive, you can remove it if you used it only for Mobile Engagement but at the cost of disabling big picture feature.</span></span>

<span data-ttu-id="f9024-190">Para os recursos de localização, você deve solicitar permissões para usuário usando uma caixa de diálogo padrão do sistema.</span><span class="sxs-lookup"><span data-stu-id="f9024-190">For the location features, you should request permissions to user using a standard system dialog.</span></span> <span data-ttu-id="f9024-191">Se o usuário aprovar, é necessário pedir a ``EngagementAgent`` para levar em conta essa alteração em tempo real (caso contrário, a alteração será processada na próxima vez que o usuário iniciar o aplicativo).</span><span class="sxs-lookup"><span data-stu-id="f9024-191">If the user approves, you need to tell ``EngagementAgent`` to take that change into account in real time (otherwise the change will be processed the next time the user launches the application).</span></span>

<span data-ttu-id="f9024-192">Aqui está um exemplo de código para usar em uma atividade do seu aplicativo para solicitar permissões e encaminhar o resultado se for positivo para ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="f9024-192">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this won't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want to keep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="f9024-193">Relatórios avançados</span><span class="sxs-lookup"><span data-stu-id="f9024-193">Advanced reporting</span></span>
<span data-ttu-id="f9024-194">Opcionalmente, se deseja relatar trabalhos, erros e eventos específicos do aplicativo, você precisa usar a API do Engagement por meio dos métodos da classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="f9024-194">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="f9024-195">Um objeto dessa classe pode ser recuperado chamando o método estático `EngagementAgent.getInstance()` .</span><span class="sxs-lookup"><span data-stu-id="f9024-195">An object of this class can be retreived by calling the `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="f9024-196">A API do Engagement permite usar todos os recursos avançados do Engagement e é detalhada em Como usar a API do Engagement em Android (além da documentação técnica da classe `EngagementAgent` ).</span><span class="sxs-lookup"><span data-stu-id="f9024-196">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on Android (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="f9024-197">Configuração avançada (em Androidmanifest.xml)</span><span class="sxs-lookup"><span data-stu-id="f9024-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="f9024-198">Bloqueios de ativação</span><span class="sxs-lookup"><span data-stu-id="f9024-198">Wake locks</span></span>
<span data-ttu-id="f9024-199">Se quiser ter certeza de que as estatísticas são enviadas em tempo real ao usar Wifi ou quando a tela estiver desligada, adicione a seguinte permissão opcional:</span><span class="sxs-lookup"><span data-stu-id="f9024-199">If you want to be sure that statistics are sent in real time when using Wifi or when the screen is off, add the following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="f9024-200">Relatório de falha</span><span class="sxs-lookup"><span data-stu-id="f9024-200">Crash report</span></span>
<span data-ttu-id="f9024-201">Se você deseja desabilitar relatórios de falha, adicione (entre as marcas `<application>` e `</application>`):</span><span class="sxs-lookup"><span data-stu-id="f9024-201">If you want to disable crash reports, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="f9024-202">Limite de intermitência</span><span class="sxs-lookup"><span data-stu-id="f9024-202">Burst threshold</span></span>
<span data-ttu-id="f9024-203">Por padrão, o serviço Engagement reporta logs em tempo real.</span><span class="sxs-lookup"><span data-stu-id="f9024-203">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="f9024-204">Se seu aplicativo reporta logs com muita frequência, é melhor armazenar os logs em buffer e relatá-los todos de uma vez em uma base de tempo normal (isso é chamado de "modo de intermitência").</span><span class="sxs-lookup"><span data-stu-id="f9024-204">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the "burst mode").</span></span> <span data-ttu-id="f9024-205">Para fazer isso, adicione (entre as marcas `<application>` e `</application>`):</span><span class="sxs-lookup"><span data-stu-id="f9024-205">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="f9024-206">O modo de intermitência aumenta ligeiramente a vida útil da bateria, mas tem um impacto no Monitor do Engagement: a duração de todas as sessões e trabalhos será arredondada para o limite de intermitência (portanto, as sessões e trabalhos mais curtos do que o limite de intermitência podem não estar visíveis).</span><span class="sxs-lookup"><span data-stu-id="f9024-206">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="f9024-207">É recomendável usar um limite de intermitência não maior que 30.000 (30s).</span><span class="sxs-lookup"><span data-stu-id="f9024-207">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="f9024-208">Tempo limite da sessão</span><span class="sxs-lookup"><span data-stu-id="f9024-208">Session timeout</span></span>
<span data-ttu-id="f9024-209">Por padrão, uma sessão é encerrada 10s após o término de sua última atividade (que geralmente ocorre pressionando a tecla Página Inicial ou Voltar, definindo o telefone como ocioso ou indo diretamente para outro aplicativo).</span><span class="sxs-lookup"><span data-stu-id="f9024-209">By default, a session is ended 10s after the end of its last activity (which usually occurs by pressing the Home or Back key, by setting the phone idle or by jumping into another application).</span></span> <span data-ttu-id="f9024-210">Isso é para evitar uma divisão de sessão cada vez que o usuário sair e retornar para o aplicativo rapidamente (o que pode acontecer quando ele pegar uma imagem, verificar uma notificação, etc.).</span><span class="sxs-lookup"><span data-stu-id="f9024-210">This is to avoid a session split each time the user exit and return to the application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="f9024-211">Convém modificar esse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="f9024-211">You may want to modify this parameter.</span></span> <span data-ttu-id="f9024-212">Para fazer isso, adicione (entre as marcas `<application>` e `</application>`):</span><span class="sxs-lookup"><span data-stu-id="f9024-212">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="f9024-213">Desabilitar o relatório de log</span><span class="sxs-lookup"><span data-stu-id="f9024-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="f9024-214">Usando uma chamada de método</span><span class="sxs-lookup"><span data-stu-id="f9024-214">Using a method call</span></span>
<span data-ttu-id="f9024-215">Se desejar que o Engagement pare de enviar logs, você pode chamar:</span><span class="sxs-lookup"><span data-stu-id="f9024-215">If you want Engagement to stop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="f9024-216">Essa chamada é persistente: ela utiliza um arquivo de preferências compartilhado.</span><span class="sxs-lookup"><span data-stu-id="f9024-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="f9024-217">Se o Engagement está ativo quando você chama essa função, pode levar um minuto para parar o serviço.</span><span class="sxs-lookup"><span data-stu-id="f9024-217">If Engagement is active when you call this function, it may take 1 minute for the service to stop.</span></span> <span data-ttu-id="f9024-218">No entanto, ele nem sequer abrirá o serviço na próxima vez que você iniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9024-218">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="f9024-219">Você pode habilitar o log de relatórios novamente chamando a mesma função com `true`.</span><span class="sxs-lookup"><span data-stu-id="f9024-219">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="f9024-220">Integração em seu próprio `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="f9024-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="f9024-221">Em vez de chamar essa função, você também pode integrar esta configuração diretamente em seu arquivo existente `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="f9024-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="f9024-222">Você pode configurar o Engagement para usar o arquivo de preferências (com o modo desejado) no arquivo `AndroidManifest.xml` com `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="f9024-222">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="f9024-223">A chave `engagement:agent:settings:name` é usada para definir o nome do arquivo de preferências compartilhado.</span><span class="sxs-lookup"><span data-stu-id="f9024-223">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="f9024-224">A chave `engagement:agent:settings:mode` é usada para definir o modo do arquivo de preferências compartilhado. Você deve usar o mesmo modo que em seu `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="f9024-224">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file, you should use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="f9024-225">O modo deve ser passado como um número: se você estiver usando uma combinação de sinalizadores constantes em seu código, verifique o valor total.</span><span class="sxs-lookup"><span data-stu-id="f9024-225">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="f9024-226">O Engagement sempre usa a chave booliana `engagement:key` dentro do arquivo de preferências para gerenciar esta configuração.</span><span class="sxs-lookup"><span data-stu-id="f9024-226">Engagement always use the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="f9024-227">O exemplo a seguir de `AndroidManifest.xml` mostra os valores padrão:</span><span class="sxs-lookup"><span data-stu-id="f9024-227">The following example of `AndroidManifest.xml` shows the default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="f9024-228">Em seguida, você pode adicionar um `CheckBoxPreference` em seu layout de preferência como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f9024-228">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
