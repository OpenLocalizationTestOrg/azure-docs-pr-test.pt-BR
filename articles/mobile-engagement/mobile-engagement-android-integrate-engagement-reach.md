---
title: "aaaAzure integração do Mobile Engagement Android SDK"
description: "Atualizações e procedimentos mais recentes para o SDK do Android do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a><span data-ttu-id="55e38-103">Como tooIntegrate contrato alcançam no Android</span><span class="sxs-lookup"><span data-stu-id="55e38-103">How tooIntegrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="55e38-104">Você deve seguir o procedimento de integração de saudação descrito em hello como tooIntegrate contrato no Android documento antes de seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="55e38-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="55e38-105">Integração padrão</span><span class="sxs-lookup"><span data-stu-id="55e38-105">Standard integration</span></span>

<span data-ttu-id="55e38-106">Copie os arquivos de recursos de alcance do hello SDK em seu projeto:</span><span class="sxs-lookup"><span data-stu-id="55e38-106">Copy Reach resource files from hello SDK in your project :</span></span>

* <span data-ttu-id="55e38-107">Copiar arquivos de saudação do hello `res/layout` pasta entregues com hello SDK em Olá `res/layout` pasta do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55e38-107">Copy hello files from hello `res/layout` folder delivered with hello SDK into hello `res/layout` folder of your application.</span></span>
* <span data-ttu-id="55e38-108">Copiar arquivos de saudação do hello `res/drawable` pasta entregues com hello SDK em Olá `res/drawable` pasta do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55e38-108">Copy hello files from hello `res/drawable` folder delivered with hello SDK into hello `res/drawable` folder of your application.</span></span>

<span data-ttu-id="55e38-109">Edite seu arquivo `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="55e38-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="55e38-110">Adicionar Olá seção a seguir (entre hello `<application>` e `</application>` marcas):</span><span class="sxs-lookup"><span data-stu-id="55e38-110">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
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
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
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
* <span data-ttu-id="55e38-111">Você precisa de notificações do sistema tooreplay essa permissão que não foram clicou na inicialização (caso contrário, eles serão mantidos no disco, mas não será mais exibidos, você realmente tem tooinclude isso).</span><span class="sxs-lookup"><span data-stu-id="55e38-111">You need this permission tooreplay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have tooinclude this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="55e38-112">Especificar um ícone usado para notificações (tanto no aplicativo e sistema aqueles) copiando e editando Olá seção a seguir (entre hello `<application>` e `</application>` marcas):</span><span class="sxs-lookup"><span data-stu-id="55e38-112">Specify an icon used for notifications (both in app and system ones) by copying and editing hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="55e38-113">Esta seção é **obrigatória** se você planeja usar notificações de sistema durante a criação de campanhas de Alcance.</span><span class="sxs-lookup"><span data-stu-id="55e38-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="55e38-114">O Android impede que as notificações de sistema sem ícones sejam exibidas.</span><span class="sxs-lookup"><span data-stu-id="55e38-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="55e38-115">Portanto, se você omitir essa seção, os usuários finais não será capaz de tooreceive-los.</span><span class="sxs-lookup"><span data-stu-id="55e38-115">So if you omit this section, your end users will not be able tooreceive them.</span></span>
> 
> 

* <span data-ttu-id="55e38-116">Se você criar campanhas com notificações do sistema usando a visão geral, você precisa Olá tooadd as seguintes permissões (após Olá `</application>` marca) se ausentes:</span><span class="sxs-lookup"><span data-stu-id="55e38-116">If you create campaigns with system notifications using big picture, you need tooadd hello following permissions (after hello `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="55e38-117">No Android M e se seu aplicativo direciona o nível de API de 23 do Android ou maior, a permissão do ``WRITE_EXTERNAL_STORAGE`` requer aprovação do usuário.</span><span class="sxs-lookup"><span data-stu-id="55e38-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="55e38-118">Leia [esta seção](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="55e38-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="55e38-119">Para notificações do sistema que você também pode especificar no hello alcançar campanha se dispositivo Olá deve tocar e/ou Vibrar.</span><span class="sxs-lookup"><span data-stu-id="55e38-119">For system notifications you can also specify in hello Reach campaign if hello device should ring and/or vibrate.</span></span> <span data-ttu-id="55e38-120">Para que ele toowork, você tem toomake-se de que você declarou Olá permissão a seguir (após Olá `</application>` marca):</span><span class="sxs-lookup"><span data-stu-id="55e38-120">For it toowork, you have toomake sure you declared hello following permission (after hello `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="55e38-121">Sem essa permissão, Android impede que as notificações do sistema de ser exibida se você tiver marcado anel hello ou hello Vibrar opção no Gerenciador de campanha de alcance hello.</span><span class="sxs-lookup"><span data-stu-id="55e38-121">Without this permission, Android prevents system notifications from being shown if you checked hello ring or hello vibrate option in hello Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="55e38-122">Push nativo</span><span class="sxs-lookup"><span data-stu-id="55e38-122">Native Push</span></span>
<span data-ttu-id="55e38-123">Agora que você configurou o módulo de alcance, é necessário campanhas a tooconfigure push nativo toobe tooreceive capaz de saudação no dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="55e38-123">Now that you configured Reach module, you need tooconfigure native push toobe able tooreceive hello campaigns on hello device.</span></span>

<span data-ttu-id="55e38-124">Oferecemos suporte a dois serviços no Android:</span><span class="sxs-lookup"><span data-stu-id="55e38-124">We support two services on Android:</span></span>

* <span data-ttu-id="55e38-125">Dispositivos do Google Play: Use [Google Cloud Messaging] pelo seguinte Olá [como tooIntegrate GCM com contrato guia](mobile-engagement-android-gcm-integrate.md) guia.</span><span class="sxs-lookup"><span data-stu-id="55e38-125">Google Play devices: Use [Google Cloud Messaging] by following hello [How tooIntegrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="55e38-126">Dispositivos do Amazon: Use [Amazon Device Messaging] pelo seguinte Olá [como tooIntegrate ADM com contrato guia](mobile-engagement-android-adm-integrate.md) guia.</span><span class="sxs-lookup"><span data-stu-id="55e38-126">Amazon devices: Use [Amazon Device Messaging] by following hello [How tooIntegrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="55e38-127">Se você quiser tootarget dispositivos Amazon e Google Play, sua possíveis toohave tudo dentro de 1 AndroidManifest.xml/APK para desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="55e38-127">If you want tootarget both Amazon and Google Play devices, its possible toohave everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="55e38-128">Mas, ao enviar tooAmazon, eles podem rejeitar seu aplicativo se ele encontrar o código do GCM.</span><span class="sxs-lookup"><span data-stu-id="55e38-128">But when submitting tooAmazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="55e38-129">Nesse caso, você deve usar múltiplos APKs.</span><span class="sxs-lookup"><span data-stu-id="55e38-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="55e38-130">**Seu aplicativo está agora pronto tooreceive e exibição alcançar campanhas!**</span><span class="sxs-lookup"><span data-stu-id="55e38-130">**Your application is now ready tooreceive and display reach campaigns!**</span></span>

## <a name="how-toohandle-data-push"></a><span data-ttu-id="55e38-131">Como enviar por push dados toohandle</span><span class="sxs-lookup"><span data-stu-id="55e38-131">How toohandle data push</span></span>
### <a name="integration"></a><span data-ttu-id="55e38-132">Integração</span><span class="sxs-lookup"><span data-stu-id="55e38-132">Integration</span></span>
<span data-ttu-id="55e38-133">Se você quiser toobe seu aplicativo capaz de envios tooreceive alcance dados, você tem toocreate uma subclasse de `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` e referencie a saudação `AndroidManifest.xml` arquivo (entre hello `<application>` e/ou `</application>` marcas):</span><span class="sxs-lookup"><span data-stu-id="55e38-133">If you want your application toobe able tooreceive Reach data pushes, you have toocreate a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in hello `AndroidManifest.xml` file (between hello `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="55e38-134">Em seguida, você pode substituir Olá `onDataPushStringReceived` e `onDataPushBase64Received` retornos de chamada.</span><span class="sxs-lookup"><span data-stu-id="55e38-134">Then you can override hello `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="55e38-135">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="55e38-135">Here is an example:</span></span>

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a><span data-ttu-id="55e38-136">Categoria</span><span class="sxs-lookup"><span data-stu-id="55e38-136">Category</span></span>
<span data-ttu-id="55e38-137">o parâmetro de categoria Olá é opcional quando você criar uma campanha de envio de dados e permite que você toofilter dados envia.</span><span class="sxs-lookup"><span data-stu-id="55e38-137">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="55e38-138">Isso é útil se você tiver vários destinatários de difusão tratamento diferentes tipos de verificações de dados, ou se você quiser toopush diferentes tipos de `Base64` tooidentify de dados e desejar que seu tipo antes da análise-los.</span><span class="sxs-lookup"><span data-stu-id="55e38-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="55e38-139">Parâmetro de retorno dos retornos de chamada</span><span class="sxs-lookup"><span data-stu-id="55e38-139">Callbacks' return parameter</span></span>
<span data-ttu-id="55e38-140">Aqui estão algumas diretrizes tooproperly identificador Olá parâmetro de retorno do `onDataPushStringReceived` e `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="55e38-140">Here are some guidelines tooproperly handle hello return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="55e38-141">Um receptor de difusão deve retornar `null` no retorno de chamada de saudação se ele não sabe como toohandle uma data de envio.</span><span class="sxs-lookup"><span data-stu-id="55e38-141">A broadcast receiver should return `null` in hello callback if it does not know how toohandle a data push.</span></span> <span data-ttu-id="55e38-142">Você deve usar o hello categoria toodetermine se o receptor difusão deve tratar dados por push-Olá ou não.</span><span class="sxs-lookup"><span data-stu-id="55e38-142">You should use hello category toodetermine whether your broadcast receiver should handle hello data push or not.</span></span>
* <span data-ttu-id="55e38-143">Um receptor de difusão Olá deve retornar `true` no retorno de chamada de saudação se ele aceita o envio de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="55e38-143">One of hello broadcast receiver should return `true` in hello callback if it accepts hello data push.</span></span>
* <span data-ttu-id="55e38-144">Um receptor de difusão Olá deve retornar `false` no retorno de chamada de saudação se reconhece os dados por push-Olá, mas descarta por qualquer motivo.</span><span class="sxs-lookup"><span data-stu-id="55e38-144">One of hello broadcast receiver should return `false` in hello callback if it recognizes hello data push, but discards it for whatever reason.</span></span> <span data-ttu-id="55e38-145">Por exemplo, retornar `false` quando os dados recebido de saudação são inválidos.</span><span class="sxs-lookup"><span data-stu-id="55e38-145">For example, return `false` when hello received data is invalid.</span></span>
* <span data-ttu-id="55e38-146">Se uma difusão do receptor retorna `true` enquanto outro um retorna `false` hello a mesma dados por push, o comportamento de saudação é indefinido, você nunca deve fazer isso.</span><span class="sxs-lookup"><span data-stu-id="55e38-146">If one broadcast receiver returns `true` while another one returns `false` for hello same data push, hello behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="55e38-147">tipo de retorno de saudação é usado apenas para estatísticas de alcance hello:</span><span class="sxs-lookup"><span data-stu-id="55e38-147">hello return type is used only for hello Reach statistics:</span></span>

* <span data-ttu-id="55e38-148">`Replied`é incrementado se um dos receptores difusão Olá retornou um `true` ou `false`.</span><span class="sxs-lookup"><span data-stu-id="55e38-148">`Replied` is incremented if one of hello broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="55e38-149">`Actioned`é incrementado apenas se uma saudação difusão receptores retornados `true`.</span><span class="sxs-lookup"><span data-stu-id="55e38-149">`Actioned` is incremented only if one of hello broadcast receivers returned `true`.</span></span>

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="55e38-150">Como campanhas toocustomize</span><span class="sxs-lookup"><span data-stu-id="55e38-150">How toocustomize campaigns</span></span>
<span data-ttu-id="55e38-151">toocustomize campanhas, você pode modificar layouts de saudação fornecidos no hello SDK do Reach.</span><span class="sxs-lookup"><span data-stu-id="55e38-151">toocustomize campaigns, you can modify hello layouts provided in hello Reach SDK.</span></span>

<span data-ttu-id="55e38-152">Você deve manter todos os identificadores de Olá usados em layouts de saudação e manter Olá tipos de exibições de saudação que usam um identificador, especialmente para modos de exibição de texto e imagem.</span><span class="sxs-lookup"><span data-stu-id="55e38-152">You should keep all hello identifiers used in hello layouts and keep hello types of hello views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="55e38-153">Alguns modos de exibição são usado apenas toohide ou mostram as áreas para que seu tipo pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="55e38-153">Some views are just used toohide or show areas so their type may be changed.</span></span> <span data-ttu-id="55e38-154">Verifique o código-fonte Olá se você pretende toochange tipo de saudação de uma exibição em layouts de saudação fornecido.</span><span class="sxs-lookup"><span data-stu-id="55e38-154">Please check hello source code if you intend toochange hello type of a view in hello provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="55e38-155">Notificações</span><span class="sxs-lookup"><span data-stu-id="55e38-155">Notifications</span></span>
<span data-ttu-id="55e38-156">Há dois tipos de notificações: as de sistema e aquelas contidas no aplicativo, que usam arquivos de layout diferentes.</span><span class="sxs-lookup"><span data-stu-id="55e38-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="55e38-157">Notificações de sistema</span><span class="sxs-lookup"><span data-stu-id="55e38-157">System notifications</span></span>
<span data-ttu-id="55e38-158">notificações do sistema toocustomize necessário Olá toouse **categorias**.</span><span class="sxs-lookup"><span data-stu-id="55e38-158">toocustomize system notifications you need toouse hello **categories**.</span></span> <span data-ttu-id="55e38-159">Você pode ir muito[categorias](#categories).</span><span class="sxs-lookup"><span data-stu-id="55e38-159">You can jump too[Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="55e38-160">Notificações no aplicativo</span><span class="sxs-lookup"><span data-stu-id="55e38-160">In-app notifications</span></span>
<span data-ttu-id="55e38-161">Por padrão, uma notificação no aplicativo é uma exibição que é adicionado dinamicamente toohello atual atividade usuário Obrigado toohello Android método de interface `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="55e38-161">By default, an in-app notification is a view that is dynamically added toohello current activity user interface thanks toohello Android method `addContentView()`.</span></span> <span data-ttu-id="55e38-162">Isso é chamado uma sobreposição de notificação.</span><span class="sxs-lookup"><span data-stu-id="55e38-162">This is called a notification overlay.</span></span> <span data-ttu-id="55e38-163">Sobreposições de notificação são ótimas para uma integração rápida porque eles não requerem que você toomodify qualquer layout em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55e38-163">Notification overlays are great for a fast integration because they do not require you toomodify any layout in your application.</span></span>

<span data-ttu-id="55e38-164">aparência de saudação toomodify de seu sobreposições de notificação, simplesmente modifique arquivo hello `engagement_notification_area.xml` tooyour precisa.</span><span class="sxs-lookup"><span data-stu-id="55e38-164">toomodify hello look of your notification overlays, you can simply modify hello file `engagement_notification_area.xml` tooyour needs.</span></span>

> [!NOTE]
> <span data-ttu-id="55e38-165">arquivo Hello `engagement_notification_overlay.xml` é Olá aquele toocreate usado em uma sobreposição de notificação, ele inclui o arquivo hello `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="55e38-165">hello file `engagement_notification_overlay.xml` is hello one that is used toocreate a notification overlay, it includes hello file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="55e38-166">Você também pode personalizá-lo toosuit suas necessidades (como para a área de notificação de saudação em sobreposição de saudação de posicionamento).</span><span class="sxs-lookup"><span data-stu-id="55e38-166">You can also customize it toosuit your needs (such as for positioning hello notification area within hello overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="55e38-167">Incluir um layout de notificação como parte de um layout de atividade</span><span class="sxs-lookup"><span data-stu-id="55e38-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="55e38-168">As sobreposições são ótimas para uma integração rápida, mas podem ser inconvenientes ou ter efeitos colaterais em casos especiais.</span><span class="sxs-lookup"><span data-stu-id="55e38-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="55e38-169">Olá sobreposição sistema pode ser personalizado no nível de atividade, tornando fácil tooprevent efeito colateral de atividades especiais.</span><span class="sxs-lookup"><span data-stu-id="55e38-169">hello overlay system can be customized at an activity level, making it easy tooprevent side effects for special activities.</span></span>

<span data-ttu-id="55e38-170">Você pode decidir tooinclude nosso layout de notificação no seu toohello de Obrigado layout existente Android **incluem** instrução.</span><span class="sxs-lookup"><span data-stu-id="55e38-170">You can decide tooinclude our notification layout in your existing layout thanks toohello Android **include** statement.</span></span> <span data-ttu-id="55e38-171">Olá, a seguir é um exemplo de uma modificação `ListActivity` layout que contêm apenas um `ListView`.</span><span class="sxs-lookup"><span data-stu-id="55e38-171">hello following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="55e38-172">**Antes da integração do Engagement :**</span><span class="sxs-lookup"><span data-stu-id="55e38-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="55e38-173">**Após a integração de Engagement :**</span><span class="sxs-lookup"><span data-stu-id="55e38-173">**After Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

<span data-ttu-id="55e38-174">Neste exemplo adicionamos um contêiner pai, pois layout original Olá usado um modo de exibição de lista como o elemento de nível superior hello.</span><span class="sxs-lookup"><span data-stu-id="55e38-174">In this example we added a parent container since hello original layout used a list view as hello top level element.</span></span> <span data-ttu-id="55e38-175">Também adicionamos `android:layout_weight="1"` tooadd capaz de toobe um modo de exibição abaixo de uma exibição de lista configurado com `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="55e38-175">We also added `android:layout_weight="1"` toobe able tooadd a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="55e38-176">Olá SDK do Reach contrato detecta automaticamente o layout de notificação que hello está incluído nesta atividade e não adicionará uma sobreposição para a atividade.</span><span class="sxs-lookup"><span data-stu-id="55e38-176">hello Engagement Reach SDK automatically detects that hello notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="55e38-177">Se você usar um ListActivity em seu aplicativo, uma sobreposição de alcance visível impedirá você de reagir a itens de tooclicked na exibição de lista hello mais.</span><span class="sxs-lookup"><span data-stu-id="55e38-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting tooclicked items in hello list view anymore.</span></span> <span data-ttu-id="55e38-178">Esse é um problema conhecido.</span><span class="sxs-lookup"><span data-stu-id="55e38-178">This is a known issue.</span></span> <span data-ttu-id="55e38-179">toowork alternativa para esse problema é recomendável tooembed layout de notificação de saudação em seu próprio layout de atividade de lista como no exemplo anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="55e38-179">toowork around this problem we suggest you tooembed hello notification layout in your own list activity layout like in hello previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="55e38-180">Desabilitando a notificação de aplicativo por atividade</span><span class="sxs-lookup"><span data-stu-id="55e38-180">Disabling application notification per activity</span></span>
<span data-ttu-id="55e38-181">Se você não quiser Olá sobreposição toobe adicionado tooyour atividade e se você não incluir o layout de notificação de saudação em seu próprio layout, você pode desabilitar a sobreposição de saudação para esta atividade no hello `AndroidManifest.xml` adicionando um `meta-data` seção como no seguinte Olá exemplo:</span><span class="sxs-lookup"><span data-stu-id="55e38-181">If you don't want hello overlay toobe added tooyour activity, and if you don't include hello notification layout in your own layout, you can disable hello overlay for this activity in hello `AndroidManifest.xml` by adding a `meta-data` section like in hello following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="55e38-182"><a name="categories"></a> Categorias</span><span class="sxs-lookup"><span data-stu-id="55e38-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="55e38-183">Quando você modifica Olá fornecido layouts, você modificar a aparência de saudação de todas as notificações.</span><span class="sxs-lookup"><span data-stu-id="55e38-183">When you modify hello provided layouts, you modify hello look of all your notifications.</span></span> <span data-ttu-id="55e38-184">As categorias permitem que toodefine que vários direcionados parece (possivelmente comportamentos) para notificações.</span><span class="sxs-lookup"><span data-stu-id="55e38-184">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="55e38-185">Uma categoria pode ser especificada quando você cria uma campanha de Reach.</span><span class="sxs-lookup"><span data-stu-id="55e38-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="55e38-186">Tenha em mente que categorias também permitem personalizar anúncios e pesquisas, como está descrito mais adiante neste documento.</span><span class="sxs-lookup"><span data-stu-id="55e38-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="55e38-187">tooregister um manipulador de categoria para as notificações, você precisa tooadd uma chamada quando o aplicativo hello é inicializado.</span><span class="sxs-lookup"><span data-stu-id="55e38-187">tooregister a category handler for your notifications, you need tooadd a call when hello application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55e38-188">Leia o aviso de saudação sobre Olá android: atributo de \<android sdk-contrato processo\> em hello como tooIntegrate contrato no Android tópico antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="55e38-188">Please read hello warning about hello android:process attribute \<android-sdk-engagement-process\> in hello How tooIntegrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="55e38-189">Olá exemplo a seguir supõe que você confirmado aviso anterior hello e usa uma subclasse de `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="55e38-189">hello following example assumes you acknowledged hello previous warning and use a sub-class of `EngagementApplication`:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

<span data-ttu-id="55e38-190">Olá `MyNotifier` objeto é a implementação de saudação do manipulador de categoria de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="55e38-190">hello `MyNotifier` object is hello implementation of hello notification category handler.</span></span> <span data-ttu-id="55e38-191">É qualquer uma implementação de saudação `EngagementNotifier` interface ou classe de implementação do padrão de saudação sub: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="55e38-191">It is either an implementation of hello `EngagementNotifier` interface or a sub class of hello default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="55e38-192">Observe que mesmo Notificador de Olá pode lidar com várias categorias, você pode registrá-los como este:</span><span class="sxs-lookup"><span data-stu-id="55e38-192">Note that hello same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="55e38-193">implementação de categoria do tooreplace saudação padrão, você pode registrar sua implementação como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="55e38-193">tooreplace hello default category implementation, you can register your implementation like in hello following example:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

<span data-ttu-id="55e38-194">Olá categoria usada em um manipulador é passada como um parâmetro na maioria dos métodos que você pode substituir na `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="55e38-194">hello current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="55e38-195">Ela é passada como um parâmetro `String` ou indiretamente em um objeto `EngagementReachContent` que tem um método `getCategory()`.</span><span class="sxs-lookup"><span data-stu-id="55e38-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="55e38-196">Você pode alterar a maior parte do processo de criação de notificação Olá redefinindo métodos em `EngagementDefaultNotifier`, para a personalização avançada se sentir livre tootake uma olhada na documentação técnica Olá e no código-fonte Olá.</span><span class="sxs-lookup"><span data-stu-id="55e38-196">You can change most of hello notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free tootake a look at hello technical documentation and at hello source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="55e38-197">Notificações no aplicativo</span><span class="sxs-lookup"><span data-stu-id="55e38-197">In-app notifications</span></span>
<span data-ttu-id="55e38-198">Se você quiser apenas layouts alternativos toouse para uma categoria específica, você pode implementar isso como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="55e38-198">If you just want toouse alternate layouts for a specific category, you can implement this as in hello following example:</span></span>

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

<span data-ttu-id="55e38-199">**Exemplo de `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="55e38-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="55e38-200">Como você pode ver, Olá identificador da exibição de sobreposição é diferente do padrão de saudação um.</span><span class="sxs-lookup"><span data-stu-id="55e38-200">As you can see, hello overlay view identifier is different than hello standard one.</span></span> <span data-ttu-id="55e38-201">É importante que cada layout use um identificador exclusivo para sobreposições.</span><span class="sxs-lookup"><span data-stu-id="55e38-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="55e38-202">**Exemplo de `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="55e38-202">**Example of `my_notification_area.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

<span data-ttu-id="55e38-203">Como você pode ver, identificador de exibição da área de notificação Olá é diferente do padrão de saudação um.</span><span class="sxs-lookup"><span data-stu-id="55e38-203">As you can see, hello notification area view identifier is different than hello standard one.</span></span> <span data-ttu-id="55e38-204">É importante que cada layout use um identificador exclusivo para áreas de notificação.</span><span class="sxs-lookup"><span data-stu-id="55e38-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="55e38-205">Esse exemplo simples de categoria torna as notificações de aplicativos (ou no aplicativo) exibidas na parte superior de saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="55e38-205">This simple example of category makes application (or in-app) notifications displayed at hello top of hello screen.</span></span> <span data-ttu-id="55e38-206">Não alteramos identificadores padrão de saudação usados na área de notificação de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="55e38-206">We did not change hello standard identifiers used in hello notification area itself.</span></span>

<span data-ttu-id="55e38-207">Se você quiser toochange, você tem Olá tooredefine `EngagementDefaultNotifier.prepareInAppArea` método.</span><span class="sxs-lookup"><span data-stu-id="55e38-207">If you want toochange that, you have tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="55e38-208">É recomendável toolook na documentação técnica Olá e no código-fonte saudação do `EngagementNotifier` e `EngagementDefaultNotifier` se desejar que esse nível de personalização avançada.</span><span class="sxs-lookup"><span data-stu-id="55e38-208">It's recommended toolook at hello technical documentation and at hello source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="55e38-209">Notificações de sistema</span><span class="sxs-lookup"><span data-stu-id="55e38-209">System notifications</span></span>
<span data-ttu-id="55e38-210">Estendendo `EngagementDefaultNotifier`, você pode substituir `onNotificationPrepared` notificação de saudação tooalter que foi preparada pela implementação do padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="55e38-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` tooalter hello notification that was prepared by hello default implementation.</span></span>

<span data-ttu-id="55e38-211">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="55e38-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="55e38-212">Este exemplo faz uma notificação do sistema para um conteúdo que está sendo exibido como um evento em andamento quando a categoria "em andamento" hello é usada.</span><span class="sxs-lookup"><span data-stu-id="55e38-212">This example makes a system notification for a content being displayed as an ongoing event when hello "ongoing" category is used.</span></span>

<span data-ttu-id="55e38-213">Se você quiser Olá toobuild `Notification` do objeto do zero, você pode retornar `false` toohello método e chame `notify` por conta própria Olá `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="55e38-213">If you want toobuild hello `Notification` object from scratch, you can return `false` toohello method and call `notify` yourself on hello `NotificationManager`.</span></span> <span data-ttu-id="55e38-214">Nesse caso é importante que você mantenha um `contentIntent`, um `deleteIntent` e Olá identificador de notificação usado pelo `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="55e38-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and hello notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="55e38-215">Aqui está um exemplo correto de tal implementação:</span><span class="sxs-lookup"><span data-stu-id="55e38-215">Here is a correct example of such an implementation:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="55e38-216">Anúncios exclusivamente de notificação</span><span class="sxs-lookup"><span data-stu-id="55e38-216">Notification only announcements</span></span>
<span data-ttu-id="55e38-217">Olá gerenciamento de saudação clique em uma notificação de anúncio só pode ser personalizado, substituindo `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify Olá preparado `Intent`.</span><span class="sxs-lookup"><span data-stu-id="55e38-217">hello management of hello click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello prepared `Intent`.</span></span> <span data-ttu-id="55e38-218">Usando esse método permite que você tootune sinalizadores de saudação facilmente.</span><span class="sxs-lookup"><span data-stu-id="55e38-218">Using this method allows you tootune hello flags easily.</span></span>

<span data-ttu-id="55e38-219">Por exemplo tooadd Olá `SINGLE_TOP` sinalizador:</span><span class="sxs-lookup"><span data-stu-id="55e38-219">For example tooadd hello `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="55e38-220">Para usuários de contrato herdados, observe que as notificações do sistema sem ação URL agora inicia o aplicativo hello se estava no plano de fundo, para que esse método pode ser chamado com um anúncio sem a URL da ação.</span><span class="sxs-lookup"><span data-stu-id="55e38-220">For legacy Engagement users, please note that system notifications without action URL now launches hello application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="55e38-221">Você deve considerar isso ao personalizar a intenção de saudação.</span><span class="sxs-lookup"><span data-stu-id="55e38-221">You should consider that when customizing hello intent.</span></span>

<span data-ttu-id="55e38-222">Você também pode implementar o `EngagementNotifier.executeNotifAnnouncementAction` do zero.</span><span class="sxs-lookup"><span data-stu-id="55e38-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="55e38-223">Ciclo de vida de notificação</span><span class="sxs-lookup"><span data-stu-id="55e38-223">Notification life cycle</span></span>
<span data-ttu-id="55e38-224">Ao usar a categoria de padrão de saudação, alguns métodos de ciclo de vida são chamados em Olá `EngagementReachInteractiveContent` tooreport estatísticas e atualização Olá campanha o estado do objeto:</span><span class="sxs-lookup"><span data-stu-id="55e38-224">When using hello default category, some life cycle methods are called on hello `EngagementReachInteractiveContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="55e38-225">Quando notificação Olá é exibida no aplicativo ou colocar na barra de status hello, Olá `displayNotification` método é chamado (que relata estatísticas) por `EngagementReachAgent` se `handleNotification` retorna `true`.</span><span class="sxs-lookup"><span data-stu-id="55e38-225">When hello notification is displayed in application or put in hello status bar, hello `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="55e38-226">Se a notificação de saudação é ignorada, Olá `exitNotification` método é chamado, a estatística é relatada e campanhas Avançar agora podem ser processadas.</span><span class="sxs-lookup"><span data-stu-id="55e38-226">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="55e38-227">Se a notificação de saudação é clicada, `actionNotification` é chamado, a estatística é relatada e intenção Olá associado é iniciada.</span><span class="sxs-lookup"><span data-stu-id="55e38-227">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated intent is launched.</span></span>

<span data-ttu-id="55e38-228">Se sua implementação de `EngagementNotifier` bypasses Olá comportamento padrão, você terá que toocall esses métodos de ciclo de vida por si mesmo.</span><span class="sxs-lookup"><span data-stu-id="55e38-228">If your implementation of `EngagementNotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="55e38-229">Olá exemplos a seguir ilustra alguns casos em que o comportamento padrão de saudação é ignorado:</span><span class="sxs-lookup"><span data-stu-id="55e38-229">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="55e38-230">Você não precisa estender `EngagementDefaultNotifier`, por exemplo, você implementou o tratamento de categoria a partir do zero.</span><span class="sxs-lookup"><span data-stu-id="55e38-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="55e38-231">Para notificações do sistema, você substitui Olá `onNotificationPrepared` e você tiver modificado `contentIntent` ou `deleteIntent` em Olá `Notification` objeto.</span><span class="sxs-lookup"><span data-stu-id="55e38-231">For system notifications, you overrode hello `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in hello `Notification` object.</span></span>
* <span data-ttu-id="55e38-232">Para notificações no aplicativo, você substitui `prepareInAppArea`, ser toomap-se de que pelo menos `actionNotification` tooone dos controles U.I.</span><span class="sxs-lookup"><span data-stu-id="55e38-232">For in-app notifications, you overrode `prepareInAppArea`, be sure toomap at least `actionNotification` tooone of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="55e38-233">Se `handleNotification` lançará uma exceção, Olá conteúdo será excluído e `dropContent` é chamado.</span><span class="sxs-lookup"><span data-stu-id="55e38-233">If `handleNotification` throws an exception, hello content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="55e38-234">Isso é informado nas estatísticas e as próximas campanhas agora podem ser processadas.</span><span class="sxs-lookup"><span data-stu-id="55e38-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="55e38-235">Anúncios e pesquisas</span><span class="sxs-lookup"><span data-stu-id="55e38-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="55e38-236">Layouts</span><span class="sxs-lookup"><span data-stu-id="55e38-236">Layouts</span></span>
<span data-ttu-id="55e38-237">Você pode modificar Olá `engagement_text_announcement.xml`, `engagement_web_announcement.xml` e `engagement_poll.xml` toocustomize anúncios de texto, notificações de web e pesquisas de arquivos.</span><span class="sxs-lookup"><span data-stu-id="55e38-237">You can modify hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files toocustomize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="55e38-238">Esses arquivos compartilham dois layouts comuns para a área de título hello e área do botão hello.</span><span class="sxs-lookup"><span data-stu-id="55e38-238">These files share two common layouts for hello title area and hello button area.</span></span> <span data-ttu-id="55e38-239">Olá layout Título Olá é `engagement_content_title.xml` e usa Olá eponymous arquivo drawable para plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="55e38-239">hello layout for hello title is `engagement_content_title.xml` and uses hello eponymous drawable file for hello background.</span></span> <span data-ttu-id="55e38-240">Olá layout para os botões de ação e sair de saudação é `engagement_button_bar.xml` e usa Olá eponymous arquivo drawable para plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="55e38-240">hello layout for hello action and exit buttons is `engagement_button_bar.xml` and uses hello eponymous drawable file for hello background.</span></span>

<span data-ttu-id="55e38-241">Em uma pesquisa, Olá layout de pergunta e as opções são aumentadas dinamicamente usando várias vezes Olá `engagement_question.xml` arquivo de layout para perguntas hello e hello `engagement_choice.xml` arquivo para obter opções de saudação.</span><span class="sxs-lookup"><span data-stu-id="55e38-241">In a poll, hello question layout and their choices are dynamically inflated using several times hello `engagement_question.xml` layout file for hello questions and hello `engagement_choice.xml` file for hello choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="55e38-242">Categorias</span><span class="sxs-lookup"><span data-stu-id="55e38-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="55e38-243">Layouts alternativos</span><span class="sxs-lookup"><span data-stu-id="55e38-243">Alternate layouts</span></span>
<span data-ttu-id="55e38-244">Como as notificações, categoria da campanha Olá pode ser usado toohave de layouts alternativos para suas notificações e pesquisas.</span><span class="sxs-lookup"><span data-stu-id="55e38-244">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="55e38-245">Por exemplo, toocreate uma categoria para um anúncio de texto, você pode estender `EngagementTextAnnouncementActivity` e referencie-Olá `AndroidManifest.xml` arquivo:</span><span class="sxs-lookup"><span data-stu-id="55e38-245">For example, toocreate a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it hello `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="55e38-246">Observe a categoria Olá no intenção de saudação filtro é usado toomake diferença hello atividade de anúncio saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="55e38-246">Note that hello category in hello intent filter is used toomake hello difference with hello default announcement activity.</span></span>

<span data-ttu-id="55e38-247">Olá SDK do Reach usa Olá intenção tooresolve Olá direito a atividade do sistema para uma categoria específica e ele volta na categoria de padrão de saudação se Olá resolução falhou.</span><span class="sxs-lookup"><span data-stu-id="55e38-247">hello Reach SDK uses hello intent system tooresolve hello right activity for a specific category and it falls back on hello default category if hello resolution failed.</span></span>

<span data-ttu-id="55e38-248">Em seguida, você tem tooimplement `MyCustomTextAnnouncementActivity`, se você apenas deseja toochange layout de saudação (mas lembre-Olá mesmo exibir identificadores), você tem apenas classe de saudação toodefine como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="55e38-248">Then you have tooimplement `MyCustomTextAnnouncementActivity`, if you just want toochange hello layout (but keep hello same view identifiers), you just have toodefine hello class like in hello following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

<span data-ttu-id="55e38-249">categoria de padrão de saudação tooreplace de anúncios de texto, basta substituir `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` pela sua implementação.</span><span class="sxs-lookup"><span data-stu-id="55e38-249">tooreplace hello default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="55e38-250">Pesquisas e anúncios da Web podem ser personalizadas de modo semelhante.</span><span class="sxs-lookup"><span data-stu-id="55e38-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="55e38-251">Para notificações de web, você pode estender `EngagementWebAnnouncementActivity` e declarar sua atividade no hello `AndroidManifest.xml` como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="55e38-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="55e38-252">Para pesquisas, você pode estender `EngagementPollActivity` e declarar o hello em `AndroidManifest.xml` como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="55e38-252">For polls you can extend `EngagementPollActivity` and declare your in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="55e38-253">Implementação do zero</span><span class="sxs-lookup"><span data-stu-id="55e38-253">Implementation from scratch</span></span>
<span data-ttu-id="55e38-254">Você pode implementar categorias para suas atividades de anúncio (e pesquisa) sem estender uma saudação `Engagement*Activity` classes fornecidas pela Olá SDK do Reach.</span><span class="sxs-lookup"><span data-stu-id="55e38-254">You can implement categories for your announcement (and poll) activities without extending one of hello `Engagement*Activity` classes provided by hello Reach SDK.</span></span> <span data-ttu-id="55e38-255">Isso é útil por exemplo se você quiser toodefine um layout que não usa Olá mesmo exibições como layouts de saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="55e38-255">This is useful for example if you want toodefine a layout that does not use hello same views as hello standard layouts.</span></span>

<span data-ttu-id="55e38-256">Como personalização avançada de notificação, é recomendável toolook no código-fonte da implementação padrão Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="55e38-256">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

<span data-ttu-id="55e38-257">Aqui estão algumas coisas tookeep em mente: alcance iniciará atividade Olá com um propósito específico (toohello intenção filtro correspondente) além de um parâmetro extra que é o identificador de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="55e38-257">Here are some things tookeep in mind: Reach will launch hello activity with a specific intent (corresponding toohello intent filter) plus an extra parameter which is hello content identifier.</span></span>

<span data-ttu-id="55e38-258">tooretrieve Olá objeto do conteúdo que contêm campos de saudação especificado quando criar hello da campanha no site Olá você pode fazer isso:</span><span class="sxs-lookup"><span data-stu-id="55e38-258">tooretrieve hello content object which contain hello fields you specified when creating hello campaign on hello web site you can do this:</span></span>

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

<span data-ttu-id="55e38-259">Para estatísticas, você pode relatar Olá conteúdo é exibido em Olá `onResume` evento:</span><span class="sxs-lookup"><span data-stu-id="55e38-259">For statistics, you should report hello content is displayed in hello `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="55e38-260">Em seguida, não se esqueça de toocall ou `actionContent(this)` ou `exitContent(this)` no objeto de conteúdo de saudação antes de atividade Olá entra no plano de fundo.</span><span class="sxs-lookup"><span data-stu-id="55e38-260">Then, don't forget toocall either `actionContent(this)` or `exitContent(this)` on hello content object before hello activity goes into background.</span></span>

<span data-ttu-id="55e38-261">Se você não chamar o `actionContent` ou `exitContent`, as estatísticas não serão enviadas (ou seja, nenhuma análise campanha Olá) e mais importante, Olá campanhas próximas não serão notificadas até que o processo de aplicativo hello seja reiniciado.</span><span class="sxs-lookup"><span data-stu-id="55e38-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly, hello next campaigns will not be notified until hello application process is restarted.</span></span>

<span data-ttu-id="55e38-262">Orientação ou outras alterações de configuração pode tomar Olá código complicado toodetermine atividade Olá entra no plano de fundo ou não, Olá torna a implementação padrão se conteúdo de saudação é relatado como encerrado se Olá usuário deixar uma atividade de saudação (seja por pressionar `HOME` ou `BACK`) mas não se altera a orientação de saudação.</span><span class="sxs-lookup"><span data-stu-id="55e38-262">Orientation or other configuration changes can make hello code tricky toodetermine whether hello activity goes into background or not, hello standard implementation makes sure hello content is reported as exited if hello user leaves hello activity (either by pressing `HOME` or `BACK`) but not if hello orientation changes.</span></span>

<span data-ttu-id="55e38-263">Aqui está a parte interessante Olá implementação Olá:</span><span class="sxs-lookup"><span data-stu-id="55e38-263">Here is hello interesting part of hello implementation:</span></span>

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="55e38-264">Como você pode ver, se você chamou `actionContent(this)` depois de terminar a atividade de saudação `exitContent(this)` pode ser chamado com segurança sem causar qualquer impacto.</span><span class="sxs-lookup"><span data-stu-id="55e38-264">As you can see, if you called `actionContent(this)` then finished hello activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
