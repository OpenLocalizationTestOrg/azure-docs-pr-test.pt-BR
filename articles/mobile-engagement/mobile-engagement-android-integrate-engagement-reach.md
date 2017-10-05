---
title: "Integração do SDK do Android do Azure Mobile Engagement"
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
ms.openlocfilehash: 26ba47b19f3a503693d60d344ad39b9eba74fe99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-reach-on-android"></a><span data-ttu-id="c42b0-103">Como integrar o Engagement Reach ao Android</span><span class="sxs-lookup"><span data-stu-id="c42b0-103">How to Integrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c42b0-104">Você deve seguir o procedimento de integração descrito no documento Como Integrar o Engagement, antes de seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="c42b0-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="c42b0-105">Integração padrão</span><span class="sxs-lookup"><span data-stu-id="c42b0-105">Standard integration</span></span>

<span data-ttu-id="c42b0-106">Copie os arquivos de recursos do Reach por meio do SDK para seu projeto:</span><span class="sxs-lookup"><span data-stu-id="c42b0-106">Copy Reach resource files from the SDK in your project :</span></span>

* <span data-ttu-id="c42b0-107">Copie os arquivos da pasta `res/layout` fornecida com o SDK para a pasta `res/layout` do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c42b0-107">Copy the files from the `res/layout` folder delivered with the SDK into the `res/layout` folder of your application.</span></span>
* <span data-ttu-id="c42b0-108">Copie os arquivos da pasta `res/drawable` fornecida com o SDK para a pasta `res/drawable` do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c42b0-108">Copy the files from the `res/drawable` folder delivered with the SDK into the `res/drawable` folder of your application.</span></span>

<span data-ttu-id="c42b0-109">Edite seu arquivo `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="c42b0-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="c42b0-110">Adicione a seção a seguir (entre as marcas `<application>` e `</application>`):</span><span class="sxs-lookup"><span data-stu-id="c42b0-110">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
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
* <span data-ttu-id="c42b0-111">Você precisa dessa permissão para exibir novamente as notificações de sistema que não foram clicadas na inicialização (caso contrário, elas serão mantidas em disco mas não serão mais exibidas; você realmente precisa incluir isso).</span><span class="sxs-lookup"><span data-stu-id="c42b0-111">You need this permission to replay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have to include this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="c42b0-112">Especifique um ícone usado para notificações (de aplicativo e de sistema), copiando e editando a seção a seguir (entre as marcas `<application>` e `</application>`):</span><span class="sxs-lookup"><span data-stu-id="c42b0-112">Specify an icon used for notifications (both in app and system ones) by copying and editing the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="c42b0-113">Esta seção é **obrigatória** se você planeja usar notificações de sistema durante a criação de campanhas de Alcance.</span><span class="sxs-lookup"><span data-stu-id="c42b0-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="c42b0-114">O Android impede que as notificações de sistema sem ícones sejam exibidas.</span><span class="sxs-lookup"><span data-stu-id="c42b0-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="c42b0-115">Portanto, se você omitir esta seção, os usuários finais não poderão recebê-las.</span><span class="sxs-lookup"><span data-stu-id="c42b0-115">So if you omit this section, your end users will not be able to receive them.</span></span>
> 
> 

* <span data-ttu-id="c42b0-116">Se você criar campanhas com notificações de sistema usando a visão global, você precisa adicionar as seguintes permissões (após a marca `</application>` ) se estiverem faltando:</span><span class="sxs-lookup"><span data-stu-id="c42b0-116">If you create campaigns with system notifications using big picture, you need to add the following permissions (after the `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="c42b0-117">No Android M e se seu aplicativo direciona o nível de API de 23 do Android ou maior, a permissão do ``WRITE_EXTERNAL_STORAGE`` requer aprovação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c42b0-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="c42b0-118">Leia [esta seção](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="c42b0-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="c42b0-119">Para notificações de sistema, você também pode especificar na campanha do Reach se o dispositivo deve tocar e/ou vibrar.</span><span class="sxs-lookup"><span data-stu-id="c42b0-119">For system notifications you can also specify in the Reach campaign if the device should ring and/or vibrate.</span></span> <span data-ttu-id="c42b0-120">Para que isso funcione, você deve certificar-se de ter declarado a permissão a seguir (após a marca `</application>` ):</span><span class="sxs-lookup"><span data-stu-id="c42b0-120">For it to work, you have to make sure you declared the following permission (after the `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="c42b0-121">Sem essa permissão, o Android impede que as notificações de sistema seja mostradas se você marcou a opção para tocar ou vibrar Gerenciador de Campanha do Reach.</span><span class="sxs-lookup"><span data-stu-id="c42b0-121">Without this permission, Android prevents system notifications from being shown if you checked the ring or the vibrate option in the Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="c42b0-122">Push nativo</span><span class="sxs-lookup"><span data-stu-id="c42b0-122">Native Push</span></span>
<span data-ttu-id="c42b0-123">Agora que você configurou o módulo Reach, você precisa fazer a configuração nativa por push para poder receber as campanhas no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c42b0-123">Now that you configured Reach module, you need to configure native push to be able to receive the campaigns on the device.</span></span>

<span data-ttu-id="c42b0-124">Oferecemos suporte a dois serviços no Android:</span><span class="sxs-lookup"><span data-stu-id="c42b0-124">We support two services on Android:</span></span>

* <span data-ttu-id="c42b0-125">Dispositivos Google Play: Use o [Google Cloud Messaging] seguindo a guia [Como integrar o GCM com a guia do Engagement](mobile-engagement-android-gcm-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="c42b0-125">Google Play devices: Use [Google Cloud Messaging] by following the [How to Integrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="c42b0-126">Dispositivos Amazon: Use o [Amazon Device Messaging] seguindo a guia [Como integrar o ADM com a guia do Engagement](mobile-engagement-android-adm-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="c42b0-126">Amazon devices: Use [Amazon Device Messaging] by following the [How to Integrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="c42b0-127">Se você deseja ter como alvo tanto dispositivos Amazon quanto Google Play, é possível ter tudo dentro de 1 AndroidManifest.xml/APK (Android Application Package) para desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="c42b0-127">If you want to target both Amazon and Google Play devices, its possible to have everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="c42b0-128">Mas, ao enviar para a Amazon, eles podem rejeitar seu aplicativo se encontrarem código do GCM (Google Cloud Messaging).</span><span class="sxs-lookup"><span data-stu-id="c42b0-128">But when submitting to Amazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="c42b0-129">Nesse caso, você deve usar múltiplos APKs.</span><span class="sxs-lookup"><span data-stu-id="c42b0-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="c42b0-130">**Seu aplicativo agora está pronto para receber e exibir as campanhas de alcance!**</span><span class="sxs-lookup"><span data-stu-id="c42b0-130">**Your application is now ready to receive and display reach campaigns!**</span></span>

## <a name="how-to-handle-data-push"></a><span data-ttu-id="c42b0-131">Como lidar com o envio de dados</span><span class="sxs-lookup"><span data-stu-id="c42b0-131">How to handle data push</span></span>
### <a name="integration"></a><span data-ttu-id="c42b0-132">Integração</span><span class="sxs-lookup"><span data-stu-id="c42b0-132">Integration</span></span>
<span data-ttu-id="c42b0-133">Se desejar que seu aplicativo seja capaz de receber push de dados d Reach, você precisa criar uma subclasse de `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` e fazer referência a ela no arquivo `AndroidManifest.xml` (entre as marcas `<application>` e/ou `</application>`):</span><span class="sxs-lookup"><span data-stu-id="c42b0-133">If you want your application to be able to receive Reach data pushes, you have to create a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in the `AndroidManifest.xml` file (between the `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="c42b0-134">Em seguida, você pode substituir os retornos de chamada `onDataPushStringReceived` e `onDataPushBase64Received`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-134">Then you can override the `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="c42b0-135">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="c42b0-135">Here is an example:</span></span>

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

### <a name="category"></a><span data-ttu-id="c42b0-136">Categoria</span><span class="sxs-lookup"><span data-stu-id="c42b0-136">Category</span></span>
<span data-ttu-id="c42b0-137">O parâmetro de categoria é opcional quando você criar uma campanha de envio de dados e permitir que você filtre o envio de dados.</span><span class="sxs-lookup"><span data-stu-id="c42b0-137">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="c42b0-138">Isso é útil se você tiver vários receptores de difusão lidando com tipos diferentes de push de dados, ou se você deseja enviar por push diferentes tipos de dados `Base64` e deseja identificar o tipo dos mesmos antes de analisá-los.</span><span class="sxs-lookup"><span data-stu-id="c42b0-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="c42b0-139">Parâmetro de retorno dos retornos de chamada</span><span class="sxs-lookup"><span data-stu-id="c42b0-139">Callbacks' return parameter</span></span>
<span data-ttu-id="c42b0-140">Aqui estão algumas diretrizes para lidar corretamente com o parâmetro de retorno de `onDataPushStringReceived` e `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="c42b0-140">Here are some guidelines to properly handle the return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="c42b0-141">Um receptor de difusão deve retornar `null` no retorno de chamada se ele não souber como lidar com um push de dados.</span><span class="sxs-lookup"><span data-stu-id="c42b0-141">A broadcast receiver should return `null` in the callback if it does not know how to handle a data push.</span></span> <span data-ttu-id="c42b0-142">Você deve usar a categoria para determinar se seu receptor de difusão deve lidar com o push de dados ou não.</span><span class="sxs-lookup"><span data-stu-id="c42b0-142">You should use the category to determine whether your broadcast receiver should handle the data push or not.</span></span>
* <span data-ttu-id="c42b0-143">Um receptor de difusão deve retornar `true` no retorno de chamada se ele aceita o push de dados.</span><span class="sxs-lookup"><span data-stu-id="c42b0-143">One of the broadcast receiver should return `true` in the callback if it accepts the data push.</span></span>
* <span data-ttu-id="c42b0-144">Um receptor de difusão deve retornar `false` no retorno de chamada se reconhece o push de dados, mas descarta por qualquer motivo.</span><span class="sxs-lookup"><span data-stu-id="c42b0-144">One of the broadcast receiver should return `false` in the callback if it recognizes the data push, but discards it for whatever reason.</span></span> <span data-ttu-id="c42b0-145">Por exemplo, retornar `false` quando os dados recebidos são inválidos.</span><span class="sxs-lookup"><span data-stu-id="c42b0-145">For example, return `false` when the received data is invalid.</span></span>
* <span data-ttu-id="c42b0-146">Se um receptor de difusão retorna `true` enquanto outro retorna `false` para o mesmo push de dados, o comportamento será indefinido; portanto, você nunca deve fazer isso.</span><span class="sxs-lookup"><span data-stu-id="c42b0-146">If one broadcast receiver returns `true` while another one returns `false` for the same data push, the behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="c42b0-147">O tipo de retorno é usado apenas para as estatísticas do Reach:</span><span class="sxs-lookup"><span data-stu-id="c42b0-147">The return type is used only for the Reach statistics:</span></span>

* <span data-ttu-id="c42b0-148">`Replied` será incrementado se um dos receptores de difusão tiver retornado um `true` ou `false`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-148">`Replied` is incremented if one of the broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="c42b0-149">`Actioned` será incrementado apenas se um dos receptores de difusão tiver retornado `true`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-149">`Actioned` is incremented only if one of the broadcast receivers returned `true`.</span></span>

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="c42b0-150">Como personalizar campanhas</span><span class="sxs-lookup"><span data-stu-id="c42b0-150">How to customize campaigns</span></span>
<span data-ttu-id="c42b0-151">Para personalizar campanhas, você pode modificar os layouts fornecidos no SDK do Reach.</span><span class="sxs-lookup"><span data-stu-id="c42b0-151">To customize campaigns, you can modify the layouts provided in the Reach SDK.</span></span>

<span data-ttu-id="c42b0-152">Você deve manter todos os identificadores usados nos layouts e manter os tipos de modos de exibição que usam um identificador, especialmente para modos de exibição de texto e modos de exibição de imagem.</span><span class="sxs-lookup"><span data-stu-id="c42b0-152">You should keep all the identifiers used in the layouts and keep the types of the views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="c42b0-153">Alguns modos de exibição são usados apenas para ocultar ou exibir determinadas áreas, para que seu tipo possa ser alterado.</span><span class="sxs-lookup"><span data-stu-id="c42b0-153">Some views are just used to hide or show areas so their type may be changed.</span></span> <span data-ttu-id="c42b0-154">Se você pretende alterar o tipo de uma exibição nos layouts fornecidos, verifique o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="c42b0-154">Please check the source code if you intend to change the type of a view in the provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="c42b0-155">Notificações</span><span class="sxs-lookup"><span data-stu-id="c42b0-155">Notifications</span></span>
<span data-ttu-id="c42b0-156">Há dois tipos de notificações: as de sistema e aquelas contidas no aplicativo, que usam arquivos de layout diferentes.</span><span class="sxs-lookup"><span data-stu-id="c42b0-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="c42b0-157">Notificações de sistema</span><span class="sxs-lookup"><span data-stu-id="c42b0-157">System notifications</span></span>
<span data-ttu-id="c42b0-158">Para personalizar as notificações de sistema, você precisa usar as **categorias**.</span><span class="sxs-lookup"><span data-stu-id="c42b0-158">To customize system notifications you need to use the **categories**.</span></span> <span data-ttu-id="c42b0-159">Você pode ir para [Categorias](#categories).</span><span class="sxs-lookup"><span data-stu-id="c42b0-159">You can jump to [Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="c42b0-160">Notificações no aplicativo</span><span class="sxs-lookup"><span data-stu-id="c42b0-160">In-app notifications</span></span>
<span data-ttu-id="c42b0-161">Por padrão, uma notificação no aplicativo é um modo de exibição que é adicionado dinamicamente à interface do usuário da atividade atual graças ao método Android `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-161">By default, an in-app notification is a view that is dynamically added to the current activity user interface thanks to the Android method `addContentView()`.</span></span> <span data-ttu-id="c42b0-162">Isso é chamado uma sobreposição de notificação.</span><span class="sxs-lookup"><span data-stu-id="c42b0-162">This is called a notification overlay.</span></span> <span data-ttu-id="c42b0-163">Sobreposições de notificação são ótimas para uma integração rápida, porque elas não exigem que você modifique nenhum layout em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c42b0-163">Notification overlays are great for a fast integration because they do not require you to modify any layout in your application.</span></span>

<span data-ttu-id="c42b0-164">Para modificar a aparência de suas sobreposições de notificação, você pode simplesmente modificar o arquivo `engagement_notification_area.xml` segundo as suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="c42b0-164">To modify the look of your notification overlays, you can simply modify the file `engagement_notification_area.xml` to your needs.</span></span>

> [!NOTE]
> <span data-ttu-id="c42b0-165">O arquivo `engagement_notification_overlay.xml` é aquele usado para criar uma sobreposição de notificação, e ele inclui o arquivo `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-165">The file `engagement_notification_overlay.xml` is the one that is used to create a notification overlay, it includes the file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="c42b0-166">Você também pode personalizá-lo para adequar-se às suas necessidades (como para posicionar a área de notificação dentro da sobreposição).</span><span class="sxs-lookup"><span data-stu-id="c42b0-166">You can also customize it to suit your needs (such as for positioning the notification area within the overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="c42b0-167">Incluir um layout de notificação como parte de um layout de atividade</span><span class="sxs-lookup"><span data-stu-id="c42b0-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="c42b0-168">As sobreposições são ótimas para uma integração rápida, mas podem ser inconvenientes ou ter efeitos colaterais em casos especiais.</span><span class="sxs-lookup"><span data-stu-id="c42b0-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="c42b0-169">O sistema de sobreposição pode ser personalizado em nível de atividade, tornando fácil evitar efeitos colaterais para atividades especiais.</span><span class="sxs-lookup"><span data-stu-id="c42b0-169">The overlay system can be customized at an activity level, making it easy to prevent side effects for special activities.</span></span>

<span data-ttu-id="c42b0-170">Você pode optar por incluir o layout de notificação ao seu layout existente graças à instrução **include** do Android.</span><span class="sxs-lookup"><span data-stu-id="c42b0-170">You can decide to include our notification layout in your existing layout thanks to the Android **include** statement.</span></span> <span data-ttu-id="c42b0-171">A seguir, temos um exemplo de um layout `ListActivity` modificado que contém apenas um `ListView`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-171">The following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="c42b0-172">**Antes da integração do Engagement :**</span><span class="sxs-lookup"><span data-stu-id="c42b0-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="c42b0-173">**Após a integração de Engagement :**</span><span class="sxs-lookup"><span data-stu-id="c42b0-173">**After Engagement integration :**</span></span>

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

<span data-ttu-id="c42b0-174">Neste exemplo, adicionamos um contêiner pai porque o layout original usou um modo de exibição de lista como o elemento de nível mais alto.</span><span class="sxs-lookup"><span data-stu-id="c42b0-174">In this example we added a parent container since the original layout used a list view as the top level element.</span></span> <span data-ttu-id="c42b0-175">Também adicionamos `android:layout_weight="1"` para podermos adicionar um modo de exibição embaixo de um modo de exibição de lista configurado com `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-175">We also added `android:layout_weight="1"` to be able to add a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="c42b0-176">O SDK do Engagement Reach detecta automaticamente que o layout de notificação está incluído nesta atividade e não adicionará uma sobreposição para tal atividade.</span><span class="sxs-lookup"><span data-stu-id="c42b0-176">The Engagement Reach SDK automatically detects that the notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="c42b0-177">Se você usar um ListActivity em seu aplicativo, uma sobreposição de Reach visível impedirá que você continue a reagir a itens clicados na exibição de lista.</span><span class="sxs-lookup"><span data-stu-id="c42b0-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting to clicked items in the list view anymore.</span></span> <span data-ttu-id="c42b0-178">Esse é um problema conhecido.</span><span class="sxs-lookup"><span data-stu-id="c42b0-178">This is a known issue.</span></span> <span data-ttu-id="c42b0-179">Para contornar esse problema, sugerimos que você incorpore o layout de notificação em seu próprio layout de atividade de lista, como no exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="c42b0-179">To work around this problem we suggest you to embed the notification layout in your own list activity layout like in the previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="c42b0-180">Desabilitando a notificação de aplicativo por atividade</span><span class="sxs-lookup"><span data-stu-id="c42b0-180">Disabling application notification per activity</span></span>
<span data-ttu-id="c42b0-181">Se você não desejar que a sobreposição seja adicionada à sua atividade e se não incluir o layout de notificação em seu próprio layout, você pode desabilitar a sobreposição para essa atividade no `AndroidManifest.xml` pela adição de uma seção `meta-data`, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c42b0-181">If you don't want the overlay to be added to your activity, and if you don't include the notification layout in your own layout, you can disable the overlay for this activity in the `AndroidManifest.xml` by adding a `meta-data` section like in the following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="c42b0-182"><a name="categories"></a> Categorias</span><span class="sxs-lookup"><span data-stu-id="c42b0-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="c42b0-183">Quando você modifica os layouts fornecidos, pode modificar também a aparência de todas as notificações.</span><span class="sxs-lookup"><span data-stu-id="c42b0-183">When you modify the provided layouts, you modify the look of all your notifications.</span></span> <span data-ttu-id="c42b0-184">As categorias permitem que você defina várias aparências direcionadas (possíveis comportamentos) para as notificações.</span><span class="sxs-lookup"><span data-stu-id="c42b0-184">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="c42b0-185">Uma categoria pode ser especificada quando você cria uma campanha de Reach.</span><span class="sxs-lookup"><span data-stu-id="c42b0-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="c42b0-186">Tenha em mente que categorias também permitem personalizar anúncios e pesquisas, como está descrito mais adiante neste documento.</span><span class="sxs-lookup"><span data-stu-id="c42b0-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="c42b0-187">Para registrar um manipulador de categorias para suas notificações, você precisa adicionar uma chamada quando o aplicativo é inicializado.</span><span class="sxs-lookup"><span data-stu-id="c42b0-187">To register a category handler for your notifications, you need to add a call when the application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c42b0-188">Leia o aviso sobre o atributo android: process \<android-sdk-engagement-process\> no tópico Como integrar contratos Android antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="c42b0-188">Please read the warning about the android:process attribute \<android-sdk-engagement-process\> in the How to Integrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="c42b0-189">O exemplo a seguir pressupõe que você confirmou o recebimento do aviso anterior e utilizará uma subclasse de `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="c42b0-189">The following example assumes you acknowledged the previous warning and use a sub-class of `EngagementApplication`:</span></span>

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

<span data-ttu-id="c42b0-190">O objeto `MyNotifier` é a implementação do manipulador de categorias de notificação.</span><span class="sxs-lookup"><span data-stu-id="c42b0-190">The `MyNotifier` object is the implementation of the notification category handler.</span></span> <span data-ttu-id="c42b0-191">Trata-se de uma implementação da interface `EngagementNotifier` ou então de uma subclasse da implementação padrão: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-191">It is either an implementation of the `EngagementNotifier` interface or a sub class of the default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="c42b0-192">Observe que o mesmo notificador pode manipular várias categorias e você pode registrá-las assim:</span><span class="sxs-lookup"><span data-stu-id="c42b0-192">Note that the same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="c42b0-193">Para substituir a implementação padrão de categoria, você pode registrar sua implementação como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c42b0-193">To replace the default category implementation, you can register your implementation like in the following example:</span></span>

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

<span data-ttu-id="c42b0-194">A categoria atual usada em um manipulador é passada como um parâmetro na maioria dos métodos que você pode substituir em `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-194">The current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="c42b0-195">Ela é passada como um parâmetro `String` ou indiretamente em um objeto `EngagementReachContent` que tem um método `getCategory()`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="c42b0-196">Você pode alterar a maior parte do processo de criação de notificação redefinindo métodos em `EngagementDefaultNotifier`. Para uma personalização mais avançada, fique à vontade para dar uma olhada na documentação técnica e no código-fonte.</span><span class="sxs-lookup"><span data-stu-id="c42b0-196">You can change most of the notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free to take a look at the technical documentation and at the source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="c42b0-197">Notificações no aplicativo</span><span class="sxs-lookup"><span data-stu-id="c42b0-197">In-app notifications</span></span>
<span data-ttu-id="c42b0-198">Se você quiser apenas usar layouts alternativos para uma categoria específica, você pode implementar isso como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c42b0-198">If you just want to use alternate layouts for a specific category, you can implement this as in the following example:</span></span>

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

<span data-ttu-id="c42b0-199">**Exemplo de `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="c42b0-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="c42b0-200">Como você pode ver, o identificador de exibição de sobreposição é diferente do padrão.</span><span class="sxs-lookup"><span data-stu-id="c42b0-200">As you can see, the overlay view identifier is different than the standard one.</span></span> <span data-ttu-id="c42b0-201">É importante que cada layout use um identificador exclusivo para sobreposições.</span><span class="sxs-lookup"><span data-stu-id="c42b0-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="c42b0-202">**Exemplo de `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="c42b0-202">**Example of `my_notification_area.xml` :**</span></span>

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

<span data-ttu-id="c42b0-203">Como você pode ver, o identificador de exibição da área de notificação é diferente do padrão.</span><span class="sxs-lookup"><span data-stu-id="c42b0-203">As you can see, the notification area view identifier is different than the standard one.</span></span> <span data-ttu-id="c42b0-204">É importante que cada layout use um identificador exclusivo para áreas de notificação.</span><span class="sxs-lookup"><span data-stu-id="c42b0-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="c42b0-205">Esse exemplo simples de categoria faz com que as notificações de aplicativos (ou contidas em aplicativos) sejam exibidas na parte superior da tela.</span><span class="sxs-lookup"><span data-stu-id="c42b0-205">This simple example of category makes application (or in-app) notifications displayed at the top of the screen.</span></span> <span data-ttu-id="c42b0-206">Não alteramos os identificadores padrão usados na área de notificação em si.</span><span class="sxs-lookup"><span data-stu-id="c42b0-206">We did not change the standard identifiers used in the notification area itself.</span></span>

<span data-ttu-id="c42b0-207">Se desejar alterá-los, você precisará redefinir o método `EngagementDefaultNotifier.prepareInAppArea` .</span><span class="sxs-lookup"><span data-stu-id="c42b0-207">If you want to change that, you have to redefine the `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="c42b0-208">Se quiser esse nível de personalização avançada, recomenda-se examinar a documentação técnica e o código-fonte de `EngagementNotifier` e `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-208">It's recommended to look at the technical documentation and at the source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="c42b0-209">Notificações de sistema</span><span class="sxs-lookup"><span data-stu-id="c42b0-209">System notifications</span></span>
<span data-ttu-id="c42b0-210">Estendendo `EngagementDefaultNotifier`, você pode substituir `onNotificationPrepared` para alterar a notificação que foi preparada pela implementação padrão.</span><span class="sxs-lookup"><span data-stu-id="c42b0-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` to alter the notification that was prepared by the default implementation.</span></span>

<span data-ttu-id="c42b0-211">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c42b0-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="c42b0-212">Este exemplo cria um sistema de notificação para um conteúdo sendo exibido como um evento em andamento quando a categoria "em andamento" é usada.</span><span class="sxs-lookup"><span data-stu-id="c42b0-212">This example makes a system notification for a content being displayed as an ongoing event when the "ongoing" category is used.</span></span>

<span data-ttu-id="c42b0-213">Se deseja compilar o objeto `Notification` do zero, você pode retornar `false` para o método e chamar `notify` você mesmo no `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-213">If you want to build the `Notification` object from scratch, you can return `false` to the method and call `notify` yourself on the `NotificationManager`.</span></span> <span data-ttu-id="c42b0-214">Nesse caso, é importante que você mantenha um `contentIntent`, um `deleteIntent` e o identificador de notificação usado por `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and the notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="c42b0-215">Aqui está um exemplo correto de tal implementação:</span><span class="sxs-lookup"><span data-stu-id="c42b0-215">Here is a correct example of such an implementation:</span></span>

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
              manager.notify(getNotificationId(content), myNotification); // notice the call to get the right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="c42b0-216">Anúncios exclusivamente de notificação</span><span class="sxs-lookup"><span data-stu-id="c42b0-216">Notification only announcements</span></span>
<span data-ttu-id="c42b0-217">O gerenciamento do clique em um comunicado exclusivamente de notificação só pode ser personalizado substituindo-se `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` para modificar o preparado `Intent`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-217">The management of the click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` to modify the prepared `Intent`.</span></span> <span data-ttu-id="c42b0-218">Usar esse método permite ajustar os sinalizadores facilmente.</span><span class="sxs-lookup"><span data-stu-id="c42b0-218">Using this method allows you to tune the flags easily.</span></span>

<span data-ttu-id="c42b0-219">Por exemplo, para adicionar o sinalizador `SINGLE_TOP` :</span><span class="sxs-lookup"><span data-stu-id="c42b0-219">For example to add the `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="c42b0-220">Para usuários herdados do Engagement, observe que as notificações do sistema sem a ação do URL agora inicia o aplicativo se ele foi em segundo plano, para que esse método pode ser chamado com um comunicado sem a URL da ação.</span><span class="sxs-lookup"><span data-stu-id="c42b0-220">For legacy Engagement users, please note that system notifications without action URL now launches the application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="c42b0-221">Você deve considerar isso ao personalizar a intenção.</span><span class="sxs-lookup"><span data-stu-id="c42b0-221">You should consider that when customizing the intent.</span></span>

<span data-ttu-id="c42b0-222">Você também pode implementar o `EngagementNotifier.executeNotifAnnouncementAction` do zero.</span><span class="sxs-lookup"><span data-stu-id="c42b0-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="c42b0-223">Ciclo de vida de notificação</span><span class="sxs-lookup"><span data-stu-id="c42b0-223">Notification life cycle</span></span>
<span data-ttu-id="c42b0-224">Ao usar a categoria padrão, alguns métodos de ciclo de vida são chamados no objeto `EngagementReachInteractiveContent` para relatar estatísticas e atualizar o estado de campanha:</span><span class="sxs-lookup"><span data-stu-id="c42b0-224">When using the default category, some life cycle methods are called on the `EngagementReachInteractiveContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="c42b0-225">Quando a notificação é exibida no aplicativo ou colocada na barra de status, o método `displayNotification` (o qual reporta estatísticas) será chamado por `EngagementReachAgent` se `handleNotification` retornar `true`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-225">When the notification is displayed in application or put in the status bar, the `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="c42b0-226">Se a notificação é liberada, o método `exitNotification` é chamado, a estatística é relatada e as próximas campanhas agora podem ser processadas.</span><span class="sxs-lookup"><span data-stu-id="c42b0-226">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="c42b0-227">Se a notificação é clicada, `actionNotification` é chamado, a estatística é relatada e a intenção associada é iniciada.</span><span class="sxs-lookup"><span data-stu-id="c42b0-227">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated intent is launched.</span></span>

<span data-ttu-id="c42b0-228">Se sua implementação de `EngagementNotifier` ignora o comportamento padrão, você precisa chamar esses métodos de ciclo de vida por conta própria.</span><span class="sxs-lookup"><span data-stu-id="c42b0-228">If your implementation of `EngagementNotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="c42b0-229">Os exemplos a seguir ilustram alguns casos em que o comportamento padrão é ignorado:</span><span class="sxs-lookup"><span data-stu-id="c42b0-229">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="c42b0-230">Você não precisa estender `EngagementDefaultNotifier`, por exemplo, você implementou o tratamento de categoria a partir do zero.</span><span class="sxs-lookup"><span data-stu-id="c42b0-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="c42b0-231">Para notificações do sistema, você substituiu o `onNotificationPrepared` e modificou `contentIntent` ou `deleteIntent` no objeto `Notification`.</span><span class="sxs-lookup"><span data-stu-id="c42b0-231">For system notifications, you overrode the `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in the `Notification` object.</span></span>
* <span data-ttu-id="c42b0-232">Para notificações no aplicativo, você substituiu `prepareInAppArea`, certifique-se de mapear pelo menos `actionNotification` para um de seus controles de IU.</span><span class="sxs-lookup"><span data-stu-id="c42b0-232">For in-app notifications, you overrode `prepareInAppArea`, be sure to map at least `actionNotification` to one of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="c42b0-233">Se `handleNotification` lança uma exceção, o conteúdo é excluído e `dropContent` é chamado.</span><span class="sxs-lookup"><span data-stu-id="c42b0-233">If `handleNotification` throws an exception, the content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="c42b0-234">Isso é informado nas estatísticas e as próximas campanhas agora podem ser processadas.</span><span class="sxs-lookup"><span data-stu-id="c42b0-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="c42b0-235">Anúncios e pesquisas</span><span class="sxs-lookup"><span data-stu-id="c42b0-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="c42b0-236">Layouts</span><span class="sxs-lookup"><span data-stu-id="c42b0-236">Layouts</span></span>
<span data-ttu-id="c42b0-237">Você pode modificar os arquivos `engagement_text_announcement.xml`, `engagement_web_announcement.xml` e `engagement_poll.xml` para personalizar os anúncios de texto, anúncios da Web e pesquisas.</span><span class="sxs-lookup"><span data-stu-id="c42b0-237">You can modify the `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files to customize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="c42b0-238">Esses arquivos compartilham dois layouts comuns para a área de título e a área do botão.</span><span class="sxs-lookup"><span data-stu-id="c42b0-238">These files share two common layouts for the title area and the button area.</span></span> <span data-ttu-id="c42b0-239">O layout para o título é `engagement_content_title.xml` e usa o arquivo epônimo emitível para a tela de fundo.</span><span class="sxs-lookup"><span data-stu-id="c42b0-239">The layout for the title is `engagement_content_title.xml` and uses the eponymous drawable file for the background.</span></span> <span data-ttu-id="c42b0-240">O layout dos botões de ação e de saída é `engagement_button_bar.xml` e usa o arquivo epônimo emitível para a tela de fundo.</span><span class="sxs-lookup"><span data-stu-id="c42b0-240">The layout for the action and exit buttons is `engagement_button_bar.xml` and uses the eponymous drawable file for the background.</span></span>

<span data-ttu-id="c42b0-241">Em uma pesquisa, o layout de pergunta e suas opções são dinamicamente infladas usando várias vezes o arquivo de layout `engagement_question.xml` para as perguntas e o arquivo `engagement_choice.xml` para as opções.</span><span class="sxs-lookup"><span data-stu-id="c42b0-241">In a poll, the question layout and their choices are dynamically inflated using several times the `engagement_question.xml` layout file for the questions and the `engagement_choice.xml` file for the choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="c42b0-242">Categorias</span><span class="sxs-lookup"><span data-stu-id="c42b0-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="c42b0-243">Layouts alternativos</span><span class="sxs-lookup"><span data-stu-id="c42b0-243">Alternate layouts</span></span>
<span data-ttu-id="c42b0-244">Como as notificações, a categoria de campanha pode ser usada com layouts alternativos para seus anúncios e pesquisas.</span><span class="sxs-lookup"><span data-stu-id="c42b0-244">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="c42b0-245">Por exemplo, para criar uma categoria para um comunicado de texto, você pode estender `EngagementTextAnnouncementActivity` e fazer referência a ela no arquivo `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="c42b0-245">For example, to create a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it the `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="c42b0-246">Observe que a categoria no filtro de intenção é usada para fazer a diferença com a atividade de comunicado padrão.</span><span class="sxs-lookup"><span data-stu-id="c42b0-246">Note that the category in the intent filter is used to make the difference with the default announcement activity.</span></span>

<span data-ttu-id="c42b0-247">O SDK do Reach usa o sistema de intenção para resolver a atividade correta para uma categoria específica, e ele retorna para a categoria padrão se a resolução tiver falhado.</span><span class="sxs-lookup"><span data-stu-id="c42b0-247">The Reach SDK uses the intent system to resolve the right activity for a specific category and it falls back on the default category if the resolution failed.</span></span>

<span data-ttu-id="c42b0-248">Em seguida, você precisa implementar `MyCustomTextAnnouncementActivity`. Se quiser apenas alterar o layout (mas manter os mesmos identificadores de exibição), você só precisa definir a classe como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c42b0-248">Then you have to implement `MyCustomTextAnnouncementActivity`, if you just want to change the layout (but keep the same view identifiers), you just have to define the class like in the following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class to use R.layout.my_text_announcement
              }
            }

<span data-ttu-id="c42b0-249">Para substituir a categoria padrão de anúncios de texto, basta substituir `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` pela sua implementação.</span><span class="sxs-lookup"><span data-stu-id="c42b0-249">To replace the default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="c42b0-250">Pesquisas e anúncios da Web podem ser personalizadas de modo semelhante.</span><span class="sxs-lookup"><span data-stu-id="c42b0-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="c42b0-251">Para anúncios da Web, você pode estender `EngagementWebAnnouncementActivity` e declarar sua atividade no `AndroidManifest.xml`, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c42b0-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in the intent is the data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="c42b0-252">Para pesquisas, você pode estender `EngagementPollActivity` e declarar sua atividade no `AndroidManifest.xml`, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c42b0-252">For polls you can extend `EngagementPollActivity` and declare your in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="c42b0-253">Implementação do zero</span><span class="sxs-lookup"><span data-stu-id="c42b0-253">Implementation from scratch</span></span>
<span data-ttu-id="c42b0-254">Você pode implementar categorias para suas atividades de comunicado (e pesquisa) sem estender uma das classes `Engagement*Activity` fornecidas pelo SDK do Reach.</span><span class="sxs-lookup"><span data-stu-id="c42b0-254">You can implement categories for your announcement (and poll) activities without extending one of the `Engagement*Activity` classes provided by the Reach SDK.</span></span> <span data-ttu-id="c42b0-255">Isso é útil, por exemplo, se desejar definir um layout que não use as mesmas exibições que os layouts padrão.</span><span class="sxs-lookup"><span data-stu-id="c42b0-255">This is useful for example if you want to define a layout that does not use the same views as the standard layouts.</span></span>

<span data-ttu-id="c42b0-256">Como para personalização da notificação avançada, é recomendável examinar o código-fonte da implementação do padrão.</span><span class="sxs-lookup"><span data-stu-id="c42b0-256">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

<span data-ttu-id="c42b0-257">Aqui estão algumas coisas que devem ser consideradas: o Reach iniciará a atividade com um propósito específico (correspondente ao filtro intencional), além de um parâmetro extra que é o identificador de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="c42b0-257">Here are some things to keep in mind: Reach will launch the activity with a specific intent (corresponding to the intent filter) plus an extra parameter which is the content identifier.</span></span>

<span data-ttu-id="c42b0-258">Para recuperar o objeto de conteúdo que contém os campos que você especificou ao criar a campanha no site da Web, você pode fazer isso:</span><span class="sxs-lookup"><span data-stu-id="c42b0-258">To retrieve the content object which contain the fields you specified when creating the campaign on the web site you can do this:</span></span>

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

<span data-ttu-id="c42b0-259">Para estatísticas, você deve relatar o conteúdo que é exibido no evento `onResume`:</span><span class="sxs-lookup"><span data-stu-id="c42b0-259">For statistics, you should report the content is displayed in the `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark the content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="c42b0-260">Em seguida, não se esqueça de chamar `actionContent(this)` ou `exitContent(this)` no objeto de conteúdo antes que a atividade entre em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="c42b0-260">Then, don't forget to call either `actionContent(this)` or `exitContent(this)` on the content object before the activity goes into background.</span></span>

<span data-ttu-id="c42b0-261">Se você não chamar `actionContent` ou `exitContent`, as estatísticas não serão enviadas (ou seja, não haverá análise da campanha) e, mais importante, as próximas campanhas não serão notificadas até o processo do aplicativo ser reiniciado.</span><span class="sxs-lookup"><span data-stu-id="c42b0-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on the campaign) and more importantly, the next campaigns will not be notified until the application process is restarted.</span></span>

<span data-ttu-id="c42b0-262">A orientação ou outras alterações de configuração podem mudar o código, tornando difícil determinar se a atividade entra em segundo plano ou não. A implementação padrão garante que o conteúdo seja relatado como encerrado se o usuário sair da atividade (pressionando `HOME` ou `BACK`), mas isso não ocorre se a orientação for alterada.</span><span class="sxs-lookup"><span data-stu-id="c42b0-262">Orientation or other configuration changes can make the code tricky to determine whether the activity goes into background or not, the standard implementation makes sure the content is reported as exited if the user leaves the activity (either by pressing `HOME` or `BACK`) but not if the orientation changes.</span></span>

<span data-ttu-id="c42b0-263">Aqui está a parte interessante da implementação:</span><span class="sxs-lookup"><span data-stu-id="c42b0-263">Here is the interesting part of the implementation:</span></span>

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
                 * called so we don't have to check anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="c42b0-264">Como você pode ver, se tiver chamado `actionContent(this)` e então terminado a atividade, `exitContent(this)` pode ser chamado com segurança sem ter qualquer efeito.</span><span class="sxs-lookup"><span data-stu-id="c42b0-264">As you can see, if you called `actionContent(this)` then finished the activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
<span data-ttu-id="c42b0-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span><span class="sxs-lookup"><span data-stu-id="c42b0-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span></span>
<span data-ttu-id="c42b0-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span><span class="sxs-lookup"><span data-stu-id="c42b0-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span></span>
