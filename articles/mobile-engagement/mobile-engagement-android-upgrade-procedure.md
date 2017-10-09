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
# <a name="upgrade-procedures"></a><span data-ttu-id="cc822-103">Procedimentos de atualização</span><span class="sxs-lookup"><span data-stu-id="cc822-103">Upgrade procedures</span></span>
<span data-ttu-id="cc822-104">Se você já tiver integrado uma versão mais antiga do nosso SDK em seu aplicativo, você tem Olá tooconsider pontos a seguir ao atualizar Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="cc822-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="cc822-105">Você pode ter vários procedimentos de toofollow se perdidas várias versões do SDK de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc822-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="cc822-106">Por exemplo, se você migrar de 1.4.0 too1.6.0 ter toofirst siga hello "de 1.4.0 too1.5.0" procedimento e hello "de 1.5.0 too1.6.0" procedimento.</span><span class="sxs-lookup"><span data-stu-id="cc822-106">For example if you migrate from 1.4.0 too1.6.0 you have toofirst follow hello "from 1.4.0 too1.5.0" procedure then hello "from 1.5.0 too1.6.0" procedure.</span></span>

<span data-ttu-id="cc822-107">Qualquer versão de hello atualizar, você tem Olá tooreplace `mobile-engagement-VERSION.jar` com hello uma nova.</span><span class="sxs-lookup"><span data-stu-id="cc822-107">Whatever hello version you upgrade from, you have tooreplace hello `mobile-engagement-VERSION.jar` with hello new one.</span></span>

## <a name="from-420-too421"></a><span data-ttu-id="cc822-108">De 4.2.0 too4.2.1</span><span class="sxs-lookup"><span data-stu-id="cc822-108">From 4.2.0 too4.2.1</span></span>
<span data-ttu-id="cc822-109">Esta etapa, na verdade, pode ser feita em qualquer versão do SDK do hello, é um aprimoramento de segurança ao integrar o alcance de atividades.</span><span class="sxs-lookup"><span data-stu-id="cc822-109">This step can actually be done on any version of hello SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="cc822-110">Agora você deve adicionar `exported="false"` tooall alcance atividades.</span><span class="sxs-lookup"><span data-stu-id="cc822-110">You should now add `exported="false"` tooall Reach activities.</span></span>

<span data-ttu-id="cc822-111">As atividades de Alcance deverão ter esta aparência no `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="cc822-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-too410"></a><span data-ttu-id="cc822-112">De 4.0.0 too4.1.0</span><span class="sxs-lookup"><span data-stu-id="cc822-112">From 4.0.0 too4.1.0</span></span>
<span data-ttu-id="cc822-113">Olá SDK agora identificador novo modelo de permissão do Android M.</span><span class="sxs-lookup"><span data-stu-id="cc822-113">hello SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="cc822-114">Se você usar os recursos de localização ou notificações de visão geral, leia [esta seção](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="cc822-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="cc822-115">Além disso toohello novo modelo de permissão, podemos agora oferecem suporte à configuração recursos de local em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="cc822-115">In addition toohello new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="cc822-116">Estamos ainda compatíveis com os parâmetros de manifesto da saudação para local, mas agora está obsoleta.</span><span class="sxs-lookup"><span data-stu-id="cc822-116">We are still compatible with hello manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="cc822-117">configuração de tempo de execução toouse, a seguir remove Olá seções de sua ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="cc822-117">toouse runtime configuration, remove hello following sections from your ``AndroidManifest.xml``:</span></span>

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

<span data-ttu-id="cc822-118">e ler [isso atualizado procedimento](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse configuração de tempo de execução em vez disso.</span><span class="sxs-lookup"><span data-stu-id="cc822-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse runtime configuration instead.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="cc822-119">De 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="cc822-119">From 3.0.0 too4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="cc822-120">Push nativo</span><span class="sxs-lookup"><span data-stu-id="cc822-120">Native push</span></span>
<span data-ttu-id="cc822-121">Envio por push nativo (GCM/ADM) agora também é usado para em notificações de aplicativo para que você deve configurar credenciais de push nativo Olá para qualquer tipo de campanha de push.</span><span class="sxs-lookup"><span data-stu-id="cc822-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="cc822-122">Caso ainda não o tenha feito, siga [este procedimento](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="cc822-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="cc822-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="cc822-123">AndroidManifest.xml</span></span>
<span data-ttu-id="cc822-124">Integração de Reach foi modificada em ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="cc822-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="cc822-125">Substitua:</span><span class="sxs-lookup"><span data-stu-id="cc822-125">Replace this:</span></span>

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

<span data-ttu-id="cc822-126">Por</span><span class="sxs-lookup"><span data-stu-id="cc822-126">By</span></span>

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

<span data-ttu-id="cc822-127">Possivelmente, agora existe uma tela de carregamento quando você clica em um anúncio (com texto/conteúdo da web) ou uma pesquisa.</span><span class="sxs-lookup"><span data-stu-id="cc822-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="cc822-128">Você tem tooadd isso para esses toowork campanhas em 4.0.0:</span><span class="sxs-lookup"><span data-stu-id="cc822-128">You have tooadd this for those campaigns toowork in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="cc822-129">Recursos</span><span class="sxs-lookup"><span data-stu-id="cc822-129">Resources</span></span>
<span data-ttu-id="cc822-130">Inserir saudação novo `res/layout/engagement_loading.xml` o arquivo no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="cc822-130">Embed hello new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-too300"></a><span data-ttu-id="cc822-131">De 2.4.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="cc822-131">From 2.4.0 too3.0.0</span></span>
<span data-ttu-id="cc822-132">Olá a seguir descrevem como toomigrate uma integração SDK da saudação Capptain serviço oferecido pelo Capptain SAS em um aplicativo da plataforma do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="cc822-132">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="cc822-133">Se você estiver migrando de uma versão anterior, consulte Olá Capptain site da web toomigrate too2.4.0 primeiro e depois aplicar Olá procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="cc822-133">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too2.4.0 first and then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc822-134">Capptain Mobile Engagement não Olá mesmos serviços e são Olá procedimento indicado abaixo destaca somente como toomigrate Olá aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="cc822-134">Capptain and Mobile Engagement are not hello same services, and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="cc822-135">Migrando Olá SDK no aplicativo hello não vai migrar seus dados do hello Capptain toohello Mobile Engagement de servidores.</span><span class="sxs-lookup"><span data-stu-id="cc822-135">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="cc822-136">Arquivo JAR</span><span class="sxs-lookup"><span data-stu-id="cc822-136">JAR file</span></span>
<span data-ttu-id="cc822-137">Substitua `capptain.jar` por `mobile-engagement-VERSION.jar` em sua pasta `libs`.</span><span class="sxs-lookup"><span data-stu-id="cc822-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="cc822-138">Arquivos de recurso</span><span class="sxs-lookup"><span data-stu-id="cc822-138">Resource files</span></span>
<span data-ttu-id="cc822-139">Cada arquivo de recurso que fornecemos (antecedidos `capptain_`) toobe substituiu por Olá novos (prefixadas com `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="cc822-139">Every resource file that we provided (prefixed by `capptain_`) has toobe replaced by hello new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="cc822-140">Se você personalizou os arquivos, você tem toore-aplicar a personalização nos novos arquivos de hello, **todos os identificadores de saudação em arquivos de recurso Olá também foram renomeados**.</span><span class="sxs-lookup"><span data-stu-id="cc822-140">If you customized those files, you have toore-apply your customization on hello new files, **all hello identifiers in hello resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="cc822-141">ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="cc822-141">Application ID</span></span>
<span data-ttu-id="cc822-142">Agora o contrato usa um identificadores conexão cadeia de caracteres tooconfigure Olá SDK como identificador de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cc822-142">Now Engagement uses a connection string tooconfigure hello SDK identifiers such as hello application identifier.</span></span>

<span data-ttu-id="cc822-143">Você tem toouse `EngagementAgent.init` método em sua atividade de iniciador como este:</span><span class="sxs-lookup"><span data-stu-id="cc822-143">You have toouse `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="cc822-144">cadeia de caracteres de conexão de saudação para seu aplicativo é exibida no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc822-144">hello connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="cc822-145">Remova qualquer chamada muito`CapptainAgent.configure` como `EngagementAgent.init` substitui esse método.</span><span class="sxs-lookup"><span data-stu-id="cc822-145">Please remove any call too`CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="cc822-146">Olá `appId` não podem ser configuradas usando `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="cc822-146">hello `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="cc822-147">Remova esta seção de seu `AndroidManifest.xml` se você tiver:</span><span class="sxs-lookup"><span data-stu-id="cc822-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="cc822-148">API Java</span><span class="sxs-lookup"><span data-stu-id="cc822-148">Java API</span></span>
<span data-ttu-id="cc822-149">Cada chamada tooany classe Java do nosso SDK tem toobe renomeado; Por exemplo, `CapptainAgent.getInstance(this)` devem ser renomeados `EngagementAgent.getInstance(this)`, `extends CapptainActivity` devem ser renomeados `extends EngagementActivity` etc...</span><span class="sxs-lookup"><span data-stu-id="cc822-149">Every call tooany Java class of our SDK has toobe renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="cc822-150">Se foram integradas com arquivos de preferência de agente padrão, o nome de arquivo hello padrão agora é `engagement.agent` e chave de saudação `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="cc822-150">If you were integrated with default agent preference files, hello default file name is now `engagement.agent` and hello key is `engagement:agent`.</span></span>

<span data-ttu-id="cc822-151">Ao criar notificações de web, Olá Javascript associador agora é `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="cc822-151">When creating web announcements, hello Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="cc822-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="cc822-152">AndroidManifest.xml</span></span>
<span data-ttu-id="cc822-153">Muitas alterações aconteceu existe, serviço de saudação não é mais compartilhado e muitos destinatários não podem ser exportadas mais.</span><span class="sxs-lookup"><span data-stu-id="cc822-153">A lot of changes happened there, hello service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="cc822-154">declaração de serviço Olá agora é mais simples; Remover filtro intenção hello e todos os metadados dentro dele e adicionar `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="cc822-154">hello service declaration is now simpler; remove hello intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="cc822-155">Além disso, tudo o que é o contrato de toouse renomeado.</span><span class="sxs-lookup"><span data-stu-id="cc822-155">Plus everything is renamed toouse engagement.</span></span>

<span data-ttu-id="cc822-156">Agora, ele deverá ficar parecido com:</span><span class="sxs-lookup"><span data-stu-id="cc822-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="cc822-157">Quando você quiser tooenable logs de teste, Olá metadados agora foi movido toohello marca de aplicativo e foi renomeado:</span><span class="sxs-lookup"><span data-stu-id="cc822-157">When you want tooenable test logs, hello meta-data has now been moved toohello application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="cc822-158">Todos os outros metadados apenas tem sido renomeados, aqui está a lista completa de saudação (claro renomear apenas Olá que você usar):</span><span class="sxs-lookup"><span data-stu-id="cc822-158">All other meta-data have just been renamed, here is hello full list (of course rename only hello ones you use):</span></span>

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

<span data-ttu-id="cc822-159">Controle do Google Play e SmartAd foi removida do SDK você que tooremove isso sem substituição:</span><span class="sxs-lookup"><span data-stu-id="cc822-159">Google Play and SmartAd tracking has been removed from SDK you just have tooremove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="cc822-160">atividades de alcance Olá agora são declaradas como este:</span><span class="sxs-lookup"><span data-stu-id="cc822-160">hello Reach activities are now declared like this:</span></span>

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

<span data-ttu-id="cc822-161">Se você tiver atividades personalizadas de alcance, você precisa apenas toochange Olá ações intencionais toomatch `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` ou `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="cc822-161">If you have custom Reach activities, you need only toochange hello intent actions toomatch either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="cc822-162">Olá receptores de transmissão foram renomeados, além de adicionarmos agora `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="cc822-162">hello broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="cc822-163">Aqui está a lista completa Olá de receptores de saudação com nova especificação de Olá, (claro renomear apenas Olá que você usar):</span><span class="sxs-lookup"><span data-stu-id="cc822-163">Here is hello full list of hello receivers with hello new specification, (of course rename only hello ones you use):</span></span>

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

<span data-ttu-id="cc822-164">Receptor de rastreamento tiver sido removido, para que você tenha tooremove nesta seção:</span><span class="sxs-lookup"><span data-stu-id="cc822-164">Tracking receiver has been removed, so you have tooremove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="cc822-165">Observação a declaração de saudação da sua implementação de saudação difusão receptor **EngagementMessageReceiver** foi alterado em Olá `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="cc822-165">Note that hello declaration of your implementation of hello broadcast receiver **EngagementMessageReceiver** has changed in hello `AndroidManifest.xml`.</span></span> <span data-ttu-id="cc822-166">Isso ocorre porque toosend Olá API e remover XMPP arbitrário mensagens de entidades XMPP arbitrárias e Olá toosend API e receber mensagens entre os dispositivos foram removidos.</span><span class="sxs-lookup"><span data-stu-id="cc822-166">This is because hello API toosend and remove arbitrary XMPP messages from arbitrary XMPP entities and hello API toosend and receive messages between devices have been removed.</span></span> <span data-ttu-id="cc822-167">Assim, você também tem Olá toodelete seguir retornos de chamada do seu **EngagementMessageReceiver** implementação:</span><span class="sxs-lookup"><span data-stu-id="cc822-167">Thus, you have also toodelete hello following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="cc822-168">e</span><span class="sxs-lookup"><span data-stu-id="cc822-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="cc822-169">exclua todas as chamadas em **EngagementAgent** para :</span><span class="sxs-lookup"><span data-stu-id="cc822-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="cc822-170">e</span><span class="sxs-lookup"><span data-stu-id="cc822-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="cc822-171">ProGuard</span><span class="sxs-lookup"><span data-stu-id="cc822-171">Proguard</span></span>
<span data-ttu-id="cc822-172">Configuração ProGuard pode ser afetada pela rebranding Olá regras agora estão procurando como:</span><span class="sxs-lookup"><span data-stu-id="cc822-172">Proguard configuration can be impacted by rebranding, hello rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

