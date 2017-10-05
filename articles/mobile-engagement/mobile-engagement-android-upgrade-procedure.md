---
title: "Integração do SDK do Android do Azure Mobile Engagement"
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
ms.openlocfilehash: 1f047f93fa8bc852b28c86e91d0c007a94fb4299
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="b9815-103">Procedimentos de atualização</span><span class="sxs-lookup"><span data-stu-id="b9815-103">Upgrade procedures</span></span>
<span data-ttu-id="b9815-104">Se você já tiver integrado uma versão anterior do SDK no seu aplicativo, você deve considerar os seguintes pontos ao atualizar o SDK.</span><span class="sxs-lookup"><span data-stu-id="b9815-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="b9815-105">Você precisará seguir vários procedimentos se perdeu várias versões do SDK.</span><span class="sxs-lookup"><span data-stu-id="b9815-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="b9815-106">Por exemplo, se você migrar do 1.4.0 para 1.6.0 você tem que primeiro seguir o procedimento "de 1.4.0 a 1.5.0” e depois o procedimento "de 1.5.0 a 1.6.0".</span><span class="sxs-lookup"><span data-stu-id="b9815-106">For example if you migrate from 1.4.0 to 1.6.0 you have to first follow the "from 1.4.0 to 1.5.0" procedure then the "from 1.5.0 to 1.6.0" procedure.</span></span>

<span data-ttu-id="b9815-107">Seja qual for a versão de atualização, você precisa substituir o `mobile-engagement-VERSION.jar` pelo novo.</span><span class="sxs-lookup"><span data-stu-id="b9815-107">Whatever the version you upgrade from, you have to replace the `mobile-engagement-VERSION.jar` with the new one.</span></span>

## <a name="from-420-to-421"></a><span data-ttu-id="b9815-108">De 4.2.0 a 4.2.1</span><span class="sxs-lookup"><span data-stu-id="b9815-108">From 4.2.0 to 4.2.1</span></span>
<span data-ttu-id="b9815-109">De fato, esta etapa pode ser realizada em qualquer versão do SDK; é uma melhoria de segurança quando as atividades de Alcance são integradas.</span><span class="sxs-lookup"><span data-stu-id="b9815-109">This step can actually be done on any version of the SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="b9815-110">Agora você deverá adicionar `exported="false"` a todas as atividades de Alcance.</span><span class="sxs-lookup"><span data-stu-id="b9815-110">You should now add `exported="false"` to all Reach activities.</span></span>

<span data-ttu-id="b9815-111">As atividades de Alcance deverão ter esta aparência no `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="b9815-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-to-410"></a><span data-ttu-id="b9815-112">De 4.0.0 a 4.1.0</span><span class="sxs-lookup"><span data-stu-id="b9815-112">From 4.0.0 to 4.1.0</span></span>
<span data-ttu-id="b9815-113">O SDK agora manipula o novo modelo de permissão para Android M.</span><span class="sxs-lookup"><span data-stu-id="b9815-113">The SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="b9815-114">Se você usar os recursos de localização ou notificações de visão geral, leia [esta seção](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="b9815-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="b9815-115">Além do novo modelo de permissão, podemos agora dar suporte a recursos locais de configuração em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="b9815-115">In addition to the new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="b9815-116">Ainda somos compatíveis com os parâmetros de manifesto para o localização, mas agora foi preterido.</span><span class="sxs-lookup"><span data-stu-id="b9815-116">We are still compatible with the manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="b9815-117">Para usar a configuração de tempo de execução, remova as seções a seguir do seu ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="b9815-117">To use runtime configuration, remove the following sections from your ``AndroidManifest.xml``:</span></span>

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

<span data-ttu-id="b9815-118">e leia [este procedimento atualizado](mobile-engagement-android-integrate-engagement.md#location-reporting) para usar em vez disso, a configuração de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="b9815-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) to use runtime configuration instead.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="b9815-119">De 3.0.0 a 4.0.0</span><span class="sxs-lookup"><span data-stu-id="b9815-119">From 3.0.0 to 4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="b9815-120">Push nativo</span><span class="sxs-lookup"><span data-stu-id="b9815-120">Native push</span></span>
<span data-ttu-id="b9815-121">O push nativo (GCM/ADM) agora também é usado nas notificações de aplicativo para que você deve configurar as credenciais por push nativo para qualquer tipo de campanha de envio.</span><span class="sxs-lookup"><span data-stu-id="b9815-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="b9815-122">Caso ainda não o tenha feito, siga [este procedimento](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="b9815-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="b9815-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="b9815-123">AndroidManifest.xml</span></span>
<span data-ttu-id="b9815-124">Integração de Reach foi modificada em ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="b9815-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="b9815-125">Substitua:</span><span class="sxs-lookup"><span data-stu-id="b9815-125">Replace this:</span></span>

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

<span data-ttu-id="b9815-126">Por</span><span class="sxs-lookup"><span data-stu-id="b9815-126">By</span></span>

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

<span data-ttu-id="b9815-127">Possivelmente, agora existe uma tela de carregamento quando você clica em um anúncio (com texto/conteúdo da web) ou uma pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b9815-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="b9815-128">Você deve adicioná-lo para as campanhas funcionarem em 4.0.0:</span><span class="sxs-lookup"><span data-stu-id="b9815-128">You have to add this for those campaigns to work in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="b9815-129">Recursos</span><span class="sxs-lookup"><span data-stu-id="b9815-129">Resources</span></span>
<span data-ttu-id="b9815-130">Insira o novo arquivo `res/layout/engagement_loading.xml` no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="b9815-130">Embed the new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-to-300"></a><span data-ttu-id="b9815-131">De 2.4.0 a 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b9815-131">From 2.4.0 to 3.0.0</span></span>
<span data-ttu-id="b9815-132">O seguinte descreve como migrar uma integração do SDK do serviço Capptain oferecido pelo Capptain SAS em um aplicativo acionado pelo Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b9815-132">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="b9815-133">Se você estiver migrando de uma versão anterior, consulte o site do Capptain para migrar primeiro para a 2.4.0 e depois aplicar o procedimento a seguir</span><span class="sxs-lookup"><span data-stu-id="b9815-133">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 2.4.0 first and then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9815-134">O Capptain e o Mobile Engagement não são os mesmos serviços e o procedimento fornecido abaixo destaca apenas como migrar o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="b9815-134">Capptain and Mobile Engagement are not the same services, and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="b9815-135">Migrar o SDK no aplicativo NÃO migrará os dados dos servidores Capptain para os servidores do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b9815-135">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="b9815-136">Arquivo JAR</span><span class="sxs-lookup"><span data-stu-id="b9815-136">JAR file</span></span>
<span data-ttu-id="b9815-137">Substitua `capptain.jar` por `mobile-engagement-VERSION.jar` em sua pasta `libs`.</span><span class="sxs-lookup"><span data-stu-id="b9815-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="b9815-138">Arquivos de recurso</span><span class="sxs-lookup"><span data-stu-id="b9815-138">Resource files</span></span>
<span data-ttu-id="b9815-139">Cada arquivo de recursos que fornecemos (antecedidos por `capptain_`) precisa ser substituído por novos (prefixados com `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="b9815-139">Every resource file that we provided (prefixed by `capptain_`) has to be replaced by the new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="b9815-140">Se você personalizou os arquivos, precisará reaplicar sua personalização nos novos arquivos, **todos os identificadores nos arquivos de recursos também foram renomeados**.</span><span class="sxs-lookup"><span data-stu-id="b9815-140">If you customized those files, you have to re-apply your customization on the new files, **all the identifiers in the resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="b9815-141">ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b9815-141">Application ID</span></span>
<span data-ttu-id="b9815-142">Agora o Engagement usa uma cadeia de conexão para configurar os identificadores SDK, como o identificador do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9815-142">Now Engagement uses a connection string to configure the SDK identifiers such as the application identifier.</span></span>

<span data-ttu-id="b9815-143">Você precisa usar um método `EngagementAgent.init` em sua atividade de inicializador como este:</span><span class="sxs-lookup"><span data-stu-id="b9815-143">You have to use `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="b9815-144">A cadeia de conexão para o seu aplicativo é exibida no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9815-144">The connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="b9815-145">Remova todas as chamadas para `CapptainAgent.configure` já que o `EngagementAgent.init` substitui esse método.</span><span class="sxs-lookup"><span data-stu-id="b9815-145">Please remove any call to `CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="b9815-146">O `appId` não pode ser configurado usando `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="b9815-146">The `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="b9815-147">Remova esta seção de seu `AndroidManifest.xml` se você tiver:</span><span class="sxs-lookup"><span data-stu-id="b9815-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="b9815-148">API Java</span><span class="sxs-lookup"><span data-stu-id="b9815-148">Java API</span></span>
<span data-ttu-id="b9815-149">Cada chamada a qualquer classe Java do nosso SDK precisa ser renomeada; por exemplo, `CapptainAgent.getInstance(this)` deve ser renomeado para `EngagementAgent.getInstance(this)`, `extends CapptainActivity` deve ser renomeado para `extends EngagementActivity`, etc...</span><span class="sxs-lookup"><span data-stu-id="b9815-149">Every call to any Java class of our SDK has to be renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="b9815-150">Se elas tiverem sido integradas com arquivos de preferência do agente padrão, o nome de arquivo padrão é agora `engagement.agent` e a chave é `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="b9815-150">If you were integrated with default agent preference files, the default file name is now `engagement.agent` and the key is `engagement:agent`.</span></span>

<span data-ttu-id="b9815-151">Ao criar anúncios da Web, o associador de Javascript é agora `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="b9815-151">When creating web announcements, the Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="b9815-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="b9815-152">AndroidManifest.xml</span></span>
<span data-ttu-id="b9815-153">Ocorreram muitas alterações, o serviço não está mais compartilhado e muitos destinatários não são mais exportáveis.</span><span class="sxs-lookup"><span data-stu-id="b9815-153">A lot of changes happened there, the service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="b9815-154">Agora, a declaração de serviço é mais simples: remova o filtro intencional e todos os metadados de dentro dele e adicione `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="b9815-154">The service declaration is now simpler; remove the intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="b9815-155">Além disso, tudo é renomeado para usar o Engagement.</span><span class="sxs-lookup"><span data-stu-id="b9815-155">Plus everything is renamed to use engagement.</span></span>

<span data-ttu-id="b9815-156">Agora, ele deverá ficar parecido com:</span><span class="sxs-lookup"><span data-stu-id="b9815-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="b9815-157">Quando você desejar habilitar logs de teste, agora os metadados foram movidos para a marca de aplicativo e renomeados:</span><span class="sxs-lookup"><span data-stu-id="b9815-157">When you want to enable test logs, the meta-data has now been moved to the application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="b9815-158">Todos os outros metadados têm sido apenas renomeados, aqui está a lista completa (renomeie apenas aqueles que for usar):</span><span class="sxs-lookup"><span data-stu-id="b9815-158">All other meta-data have just been renamed, here is the full list (of course rename only the ones you use):</span></span>

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

<span data-ttu-id="b9815-159">O acompanhamento do Google Play e do SmartAd foi removido do SDK, você só precisa removê-lo sem substituição:</span><span class="sxs-lookup"><span data-stu-id="b9815-159">Google Play and SmartAd tracking has been removed from SDK you just have to remove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="b9815-160">As atividades do Reach agora são declaradas conforme segue:</span><span class="sxs-lookup"><span data-stu-id="b9815-160">The Reach activities are now declared like this:</span></span>

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

<span data-ttu-id="b9815-161">Se tiver atividades do Reach personalizadas, você só precisa alterar as ações intencionais para corresponder a `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` ou `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="b9815-161">If you have custom Reach activities, you need only to change the intent actions to match either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="b9815-162">Os receptores de transmissão foram renomeados e agora adicionamos `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="b9815-162">The broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="b9815-163">Aqui está a lista completa de destinatários com a nova especificação (renomeie apenas aqueles que for usar):</span><span class="sxs-lookup"><span data-stu-id="b9815-163">Here is the full list of the receivers with the new specification, (of course rename only the ones you use):</span></span>

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

<span data-ttu-id="b9815-164">O receptor de acompanhamento foi removido, você precisará remover esta seção:</span><span class="sxs-lookup"><span data-stu-id="b9815-164">Tracking receiver has been removed, so you have to remove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="b9815-165">Observe que a declaração de sua implementação do receptor de difusão **EngagementMessageReceiver** mudou no `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="b9815-165">Note that the declaration of your implementation of the broadcast receiver **EngagementMessageReceiver** has changed in the `AndroidManifest.xml`.</span></span> <span data-ttu-id="b9815-166">Isso ocorre porque a API envia e remove mensagens XMPP arbitrárias de entidades XMPP arbitrárias e a API envia e recebe mensagens entre dispositivos que foram removidos.</span><span class="sxs-lookup"><span data-stu-id="b9815-166">This is because the API to send and remove arbitrary XMPP messages from arbitrary XMPP entities and the API to send and receive messages between devices have been removed.</span></span> <span data-ttu-id="b9815-167">Portanto, você também precisa excluir os seguintes retornos de chamada de sua implementação **EngagementMessageReceiver** :</span><span class="sxs-lookup"><span data-stu-id="b9815-167">Thus, you have also to delete the following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="b9815-168">e</span><span class="sxs-lookup"><span data-stu-id="b9815-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="b9815-169">exclua todas as chamadas em **EngagementAgent** para :</span><span class="sxs-lookup"><span data-stu-id="b9815-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="b9815-170">e</span><span class="sxs-lookup"><span data-stu-id="b9815-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="b9815-171">ProGuard</span><span class="sxs-lookup"><span data-stu-id="b9815-171">Proguard</span></span>
<span data-ttu-id="b9815-172">A configuração ProGuard pode ser afetada por mudanças de marca, as regras agora estão assim:</span><span class="sxs-lookup"><span data-stu-id="b9815-172">Proguard configuration can be impacted by rebranding, the rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

