---
title: "Integração do SDK do Android do Azure Mobile Engagement"
description: "Atualizações e procedimentos mais recentes para o SDK do Android do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 43987962ea2b7b825b88643d18b4db65f1f1670e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-adm-with-engagement"></a><span data-ttu-id="e969d-103">Como integrar ADM ao Engagement</span><span class="sxs-lookup"><span data-stu-id="e969d-103">How to Integrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e969d-104">Você deve seguir o procedimento de integração descrito no documento Como Integrar o Engagement, antes de seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="e969d-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="e969d-105">Este documento será útil apenas se você já tiver integrado o módulo de Alcance e planeja enviar por push os dispositivos Amazon.</span><span class="sxs-lookup"><span data-stu-id="e969d-105">This document is useful only if you already integrated the Reach module and plan to push Amazon devices.</span></span> <span data-ttu-id="e969d-106">Para integrar campanhas de Alcance em seu aplicativo, leia primeiro Como Integrar o Engagement Reach no Android.</span><span class="sxs-lookup"><span data-stu-id="e969d-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="e969d-107">Introdução</span><span class="sxs-lookup"><span data-stu-id="e969d-107">Introduction</span></span>
<span data-ttu-id="e969d-108">A integração do ADM permite que o seu aplicativo seja enviado por push ao direcionar dispositivos do Amazon Android.</span><span class="sxs-lookup"><span data-stu-id="e969d-108">Integrating ADM allows your application to be pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="e969d-109">As cargas de ADM enviadas para o SDK sempre contêm a chave `azme` no objeto de dados.</span><span class="sxs-lookup"><span data-stu-id="e969d-109">ADM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="e969d-110">Portanto, se você usar o ADM para outra finalidade em seu aplicativo, é possível filtrar os pushes com base nessa chave.</span><span class="sxs-lookup"><span data-stu-id="e969d-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e969d-111">Somente dispositivos Amazon Kindle executando Android 4.0.3 ou acima têm suporte pelo Amazon Device Messaging; no entanto, você pode integrar esse código com segurança em outros dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e969d-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-to-adm"></a><span data-ttu-id="e969d-112">Inscrever-se para ADM</span><span class="sxs-lookup"><span data-stu-id="e969d-112">Sign up to ADM</span></span>
<span data-ttu-id="e969d-113">Se ainda não tiver feito, você deve habilitar o ADM em sua conta da Amazon.</span><span class="sxs-lookup"><span data-stu-id="e969d-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="e969d-114">O procedimento é detalhado em: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="e969d-114">The procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="e969d-115">Depois de concluir o procedimento, você obtém:</span><span class="sxs-lookup"><span data-stu-id="e969d-115">Upon completing the procedure, you get:</span></span>

* <span data-ttu-id="e969d-116">Credenciais OAuth (uma ID de cliente e um segredo do cliente) para o Engagement para poder enviar por push seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e969d-116">OAuth credentials (a Client ID and a Client Secret) for Engagement to be able to push your devices.</span></span>
* <span data-ttu-id="e969d-117">Uma chave de API que deve ser integrada ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e969d-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="e969d-118">Integração do SDK</span><span class="sxs-lookup"><span data-stu-id="e969d-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="e969d-119">Gerenciando registros de dispositivo</span><span class="sxs-lookup"><span data-stu-id="e969d-119">Managing device registrations</span></span>
<span data-ttu-id="e969d-120">Cada dispositivo deve enviar um comando de registro aos servidores do ADM, caso contrário eles não poderão ser alcançados.</span><span class="sxs-lookup"><span data-stu-id="e969d-120">Each device must send a registration command to the ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="e969d-121">Se você já usa a [biblioteca de cliente do ADM], e já tiver o [ADM integrado] você pode ir diretamente para o android-sdk-adm-receive.</span><span class="sxs-lookup"><span data-stu-id="e969d-121">If you already use the [ADM client library], and already have [integrated ADM] you can directly go to android-sdk-adm-receive.</span></span>

<span data-ttu-id="e969d-122">Se você ainda não tiver o ADM integrado, o Engagement tem uma maneira mais simples para habilitá-lo em seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="e969d-122">If you have not integrated ADM yet, Engagement has a simpler way to enable it in your application:</span></span>

<span data-ttu-id="e969d-123">Edite seu arquivo `AndroidManifest.xml` :</span><span class="sxs-lookup"><span data-stu-id="e969d-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="e969d-124">Adicione o namespace Amazon, o arquivo deve começar como este:</span><span class="sxs-lookup"><span data-stu-id="e969d-124">Add the Amazon namespace, the file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="e969d-125">Dentro da marca `<application/>` , adicione essa seção:</span><span class="sxs-lookup"><span data-stu-id="e969d-125">Inside the `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="e969d-126">Depois de adicionar a marca da amazon, você poderá ter um erro de compilação se o Destino de Compilação do Projeto estiver abaixo da versão 2.1 do Android.</span><span class="sxs-lookup"><span data-stu-id="e969d-126">After adding the amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="e969d-127">É necessário usar um destino de compilação **Android 2.1+** (não se preocupe, você ainda pode ter um `minSdkVersion` definido como 4).</span><span class="sxs-lookup"><span data-stu-id="e969d-127">You have to use an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set to 4).</span></span>
* <span data-ttu-id="e969d-128">Integre a chave de API do ADM como um ativo seguindo [este procedimento].</span><span class="sxs-lookup"><span data-stu-id="e969d-128">Integrate the ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="e969d-129">Siga as instruções das próximas seções.</span><span class="sxs-lookup"><span data-stu-id="e969d-129">Then follow the instructions of the next sections.</span></span>

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="e969d-130">Comunicar a id de registro para o serviço de envio por push do Engagement e receber notificações</span><span class="sxs-lookup"><span data-stu-id="e969d-130">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="e969d-131">Para comunicar a ID de registro do dispositivo para o serviço de Envio por Push do Engagement e receber notificações, adicione o seguinte ao seu arquivo `AndroidManifest.xml`  dentro da marca `<application/>` (mesmo que você use ADM sem Engagement):</span><span class="sxs-lookup"><span data-stu-id="e969d-131">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you use ADM without Engagement):</span></span>

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

<span data-ttu-id="e969d-132">Certifique-se de ter as seguintes permissões em seu `AndroidManifest.xml` (antes da marca `</application>`).</span><span class="sxs-lookup"><span data-stu-id="e969d-132">Ensure you have the following permissions in your `AndroidManifest.xml` (before the `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="e969d-133">Conceda as credenciais do Engagement OAuth</span><span class="sxs-lookup"><span data-stu-id="e969d-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="e969d-134">Envie suas credenciais OAuth (ID do Cliente e Segredo do Cliente) no Portal do Engagement.</span><span class="sxs-lookup"><span data-stu-id="e969d-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

<span data-ttu-id="e969d-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span><span class="sxs-lookup"><span data-stu-id="e969d-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span></span>
<span data-ttu-id="e969d-136">[biblioteca de cliente do ADM]:https://developer.amazon.com/sdk/adm/setup.html</span><span class="sxs-lookup"><span data-stu-id="e969d-136">[ADM client library]:https://developer.amazon.com/sdk/adm/setup.html</span></span>
<span data-ttu-id="e969d-137">[ADM integrado]:https://developer.amazon.com/sdk/adm/integrating-app.html</span><span class="sxs-lookup"><span data-stu-id="e969d-137">[integrated ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span></span>
<span data-ttu-id="e969d-138">[este procedimento]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span><span class="sxs-lookup"><span data-stu-id="e969d-138">[this procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span></span>
