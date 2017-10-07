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
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="02789-103">Relatório de local para o SDK do Azure Mobile Engagement para Android</span><span class="sxs-lookup"><span data-stu-id="02789-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="02789-104">Android</span><span class="sxs-lookup"><span data-stu-id="02789-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="02789-105">Este tópico descreve como local de toodo reporting para seu aplicativo do Android.</span><span class="sxs-lookup"><span data-stu-id="02789-105">This topic describes how toodo location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02789-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="02789-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="02789-107">Relatórios de local</span><span class="sxs-lookup"><span data-stu-id="02789-107">Location reporting</span></span>
<span data-ttu-id="02789-108">Se você quiser toobe locais relatado, você precisa tooadd algumas linhas de configuração (entre hello `<application>` e `</application>` marcas).</span><span class="sxs-lookup"><span data-stu-id="02789-108">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="02789-109">Relatórios de local de área lenta</span><span class="sxs-lookup"><span data-stu-id="02789-109">Lazy area location reporting</span></span>
<span data-ttu-id="02789-110">Relatório de local de área lento permite relatório país de hello, região e localidade associado a dispositivos.</span><span class="sxs-lookup"><span data-stu-id="02789-110">Lazy area location reporting enables reporting hello country, region, and locality associated with devices.</span></span> <span data-ttu-id="02789-111">Esse tipo de relatório de local usa apenas os locais de rede (com base na ID da célula ou WIFI).</span><span class="sxs-lookup"><span data-stu-id="02789-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="02789-112">Olá dispositivo é relatada no máximo uma vez por sessão.</span><span class="sxs-lookup"><span data-stu-id="02789-112">hello device area is reported at most once per session.</span></span> <span data-ttu-id="02789-113">Olá GPS nunca é usado e, portanto, esse tipo de relatório local tem baixo impacto na bateria hello.</span><span class="sxs-lookup"><span data-stu-id="02789-113">hello GPS is never used, and thus this type of location report has low impact on hello battery.</span></span>

<span data-ttu-id="02789-114">Relatado áreas são estatísticas de geográfica toocompute usado sobre usuários, sessões, eventos e erros.</span><span class="sxs-lookup"><span data-stu-id="02789-114">Reported areas are used toocompute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="02789-115">Elas também podem ser usadas como critério nas campanhas do Reach.</span><span class="sxs-lookup"><span data-stu-id="02789-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="02789-116">Habilitar o local de área lento reporting por meio da configuração de saudação mencionada anteriormente neste procedimento:</span><span class="sxs-lookup"><span data-stu-id="02789-116">You enable lazy area location reporting by using hello configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="02789-117">Você também precisa toospecify uma permissão de local.</span><span class="sxs-lookup"><span data-stu-id="02789-117">You also need toospecify a location permission.</span></span> <span data-ttu-id="02789-118">Este código usa a permissão ``COARSE`` :</span><span class="sxs-lookup"><span data-stu-id="02789-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="02789-119">Se seu aplicativo exigir, você poderá usar ``ACCESS_FINE_LOCATION`` em vez disso.</span><span class="sxs-lookup"><span data-stu-id="02789-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="02789-120">Relatórios de localização em tempo real</span><span class="sxs-lookup"><span data-stu-id="02789-120">Real-time location reporting</span></span>
<span data-ttu-id="02789-121">Relatórios de local em tempo real permite relatório latitude de saudação e a longitude associado a dispositivos.</span><span class="sxs-lookup"><span data-stu-id="02789-121">Real-time location reporting enables reporting hello latitude and longitude associated with devices.</span></span> <span data-ttu-id="02789-122">Por padrão, esse tipo de relatório de local usa apenas os locais de rede, com base na ID da célula ou WIFI.</span><span class="sxs-lookup"><span data-stu-id="02789-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="02789-123">Olá reporting somente estará ativo quando o aplicativo hello é executado em primeiro plano (por exemplo, durante uma sessão).</span><span class="sxs-lookup"><span data-stu-id="02789-123">hello reporting is only active when hello application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="02789-124">Locais em tempo real são *não* usado toocompute estatísticas.</span><span class="sxs-lookup"><span data-stu-id="02789-124">Real-time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="02789-125">Seu único propósito é o uso de saudação do tooallow de geoinstalação em tempo real \<alcance-público-o isolamento geográfico\> critério de campanhas de alcance.</span><span class="sxs-lookup"><span data-stu-id="02789-125">Their only purpose is tooallow hello use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="02789-126">local em tempo real de tooenable relatórios, adicione uma linha de código toowhere você definir cadeia de caracteres de conexão de contrato Olá na atividade de iniciador hello.</span><span class="sxs-lookup"><span data-stu-id="02789-126">tooenable real-time location reporting, add a line of code toowhere you set hello Engagement connection string in hello launcher activity.</span></span> <span data-ttu-id="02789-127">resultado de saudação semelhante ao seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="02789-127">hello result looks like hello following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="02789-128">Relatórios com base em GPS</span><span class="sxs-lookup"><span data-stu-id="02789-128">GPS based reporting</span></span>
<span data-ttu-id="02789-129">Por padrão, os relatórios de local em tempo real usam apenas locais com base em rede.</span><span class="sxs-lookup"><span data-stu-id="02789-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="02789-130">tooenable Olá dos locais com base em GPS, que são muito mais precisos, usar o objeto de configuração hello:</span><span class="sxs-lookup"><span data-stu-id="02789-130">tooenable hello use of GPS-based locations, which are far more precise, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="02789-131">Você também precisa Olá tooadd permissão a seguir se ausentes:</span><span class="sxs-lookup"><span data-stu-id="02789-131">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="02789-132">Relatório de segundo plano</span><span class="sxs-lookup"><span data-stu-id="02789-132">Background reporting</span></span>
<span data-ttu-id="02789-133">Por padrão, relatórios de local em tempo real só está ativo quando o aplicativo hello é executado em primeiro plano (por exemplo, durante uma sessão).</span><span class="sxs-lookup"><span data-stu-id="02789-133">By default, real-time location reporting is only active when hello application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="02789-134">Olá tooenable relatórios também no plano de fundo, use esse objeto de configuração:</span><span class="sxs-lookup"><span data-stu-id="02789-134">tooenable hello reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="02789-135">Quando o aplicativo hello é executado em segundo plano, somente os locais de rede são relatados, mesmo se você tiver habilitado Olá GPS.</span><span class="sxs-lookup"><span data-stu-id="02789-135">When hello application runs in background, only network-based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="02789-136">Se o usuário Olá reinicializar seu dispositivo, relatório de local do plano de fundo de saudação será interrompido.</span><span class="sxs-lookup"><span data-stu-id="02789-136">If hello user reboots their device, hello background location report is stopped.</span></span> <span data-ttu-id="02789-137">toomake reiniciar automaticamente no momento da inicialização, adicione este código.</span><span class="sxs-lookup"><span data-stu-id="02789-137">toomake it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="02789-138">Você também precisa Olá tooadd permissão a seguir se ausentes:</span><span class="sxs-lookup"><span data-stu-id="02789-138">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="02789-139">Permissões do Android M</span><span class="sxs-lookup"><span data-stu-id="02789-139">Android M permissions</span></span>
<span data-ttu-id="02789-140">A partir do Android M, algumas permissões são gerenciadas em tempo de execução e precisam de aprovação do usuário.</span><span class="sxs-lookup"><span data-stu-id="02789-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="02789-141">Se você selecionar o nível de API do Android 23, permissões de tempo de execução Olá estão desativadas por padrão para novas instalações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="02789-141">If you target Android API level 23, hello runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="02789-142">Caso contrário, elas serão ativadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="02789-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="02789-143">Você pode habilitar/desabilitar essas permissões no menu de configurações de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="02789-143">You can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="02789-144">A desativação de permissões do menu do sistema Olá elimina processos em segundo plano de saudação do aplicativo hello, que é um comportamento do sistema e não tem nenhum impacto na capacidade tooreceive push no plano de fundo.</span><span class="sxs-lookup"><span data-stu-id="02789-144">Turning off permissions from hello system menu kills hello background processes of hello application, which is a system behavior, and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="02789-145">No contexto de saudação do local do Mobile Engagement reporting, permissões de saudação que precisam de aprovação em tempo de execução são:</span><span class="sxs-lookup"><span data-stu-id="02789-145">In hello context of Mobile Engagement location reporting, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="02789-146">Solicite permissões de usuário hello usando uma caixa de diálogo do sistema padrão.</span><span class="sxs-lookup"><span data-stu-id="02789-146">Request permissions from hello user using a standard system dialog.</span></span> <span data-ttu-id="02789-147">Se o usuário Olá aprova, conte- ``EngagementAgent`` tootake alterar em consideração em tempo real.</span><span class="sxs-lookup"><span data-stu-id="02789-147">If hello user approves, tell ``EngagementAgent`` tootake that change into account in real-time.</span></span> <span data-ttu-id="02789-148">Caso contrário, a alteração de Olá é processado próximo tempo Olá usuário inicia Olá aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="02789-148">Otherwise hello change is processed hello next time hello user launches hello application.</span></span>

<span data-ttu-id="02789-149">Aqui está um toouse de exemplo de código em uma atividade de permissões do aplicativo toorequest e resultado Olá forward positivo muito``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="02789-149">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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
