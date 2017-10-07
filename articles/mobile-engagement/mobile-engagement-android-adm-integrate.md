---
title: "aaaAzure integração do Mobile Engagement Android SDK"
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
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a><span data-ttu-id="3eeeb-103">Como tooIntegrate ADM com contrato</span><span class="sxs-lookup"><span data-stu-id="3eeeb-103">How tooIntegrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3eeeb-104">Você deve seguir o procedimento de integração de saudação descrito em hello como tooIntegrate contrato no Android documento antes de seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="3eeeb-105">Este documento é útil apenas se você já Olá alcance módulo e o plano toopush Amazon dispositivos integrado.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-105">This document is useful only if you already integrated hello Reach module and plan toopush Amazon devices.</span></span> <span data-ttu-id="3eeeb-106">campanhas de alcance toointegrate em seu aplicativo, leia primeiro como tooIntegrate contrato chegar no Android.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="3eeeb-107">Introdução</span><span class="sxs-lookup"><span data-stu-id="3eeeb-107">Introduction</span></span>
<span data-ttu-id="3eeeb-108">Integração ADM permite que seu toobe aplicativo enviada por push ao direcionar dispositivos com Android da Amazon.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-108">Integrating ADM allows your application toobe pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="3eeeb-109">Cargas ADM enviadas toohello SDK sempre contêm Olá `azme` chave no objeto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-109">ADM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="3eeeb-110">Portanto, se você usar o ADM para outra finalidade em seu aplicativo, é possível filtrar os pushes com base nessa chave.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3eeeb-111">Somente dispositivos Amazon Kindle executando Android 4.0.3 ou acima têm suporte pelo Amazon Device Messaging; no entanto, você pode integrar esse código com segurança em outros dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-tooadm"></a><span data-ttu-id="3eeeb-112">Inscreva-se tooADM</span><span class="sxs-lookup"><span data-stu-id="3eeeb-112">Sign up tooADM</span></span>
<span data-ttu-id="3eeeb-113">Se ainda não tiver feito, você deve habilitar o ADM em sua conta da Amazon.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="3eeeb-114">procedimento de saudação é detalhado no: [ <https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="3eeeb-114">hello procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="3eeeb-115">Após concluir o procedimento hello, você obtém:</span><span class="sxs-lookup"><span data-stu-id="3eeeb-115">Upon completing hello procedure, you get:</span></span>

* <span data-ttu-id="3eeeb-116">OAuth credenciais (uma ID de cliente e um segredo do cliente) para o contrato toobe capaz de toopush seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-116">OAuth credentials (a Client ID and a Client Secret) for Engagement toobe able toopush your devices.</span></span>
* <span data-ttu-id="3eeeb-117">Uma chave de API que deve ser integrada ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="3eeeb-118">Integração do SDK</span><span class="sxs-lookup"><span data-stu-id="3eeeb-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="3eeeb-119">Gerenciando registros de dispositivo</span><span class="sxs-lookup"><span data-stu-id="3eeeb-119">Managing device registrations</span></span>
<span data-ttu-id="3eeeb-120">Cada dispositivo deve enviar um toohello do comando de registro de servidores ADM, caso contrário, não pode ser alcançados.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-120">Each device must send a registration command toohello ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="3eeeb-121">Se você já usa Olá [biblioteca de cliente ADM]e já tiver [integrado ADM] poderá ir diretamente tooandroid-sdk-adm-receber.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-121">If you already use hello [ADM client library], and already have [integrated ADM] you can directly go tooandroid-sdk-adm-receive.</span></span>

<span data-ttu-id="3eeeb-122">Se você não tiver integrado ADM ainda, contrato tem um tooenable de forma mais simples-lo em seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="3eeeb-122">If you have not integrated ADM yet, Engagement has a simpler way tooenable it in your application:</span></span>

<span data-ttu-id="3eeeb-123">Edite seu arquivo `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="3eeeb-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="3eeeb-124">Adicione Olá Amazon namespace, Olá arquivo deve começar como este:</span><span class="sxs-lookup"><span data-stu-id="3eeeb-124">Add hello Amazon namespace, hello file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="3eeeb-125">Olá interna `<application/>` marca, adicionar nesta seção:</span><span class="sxs-lookup"><span data-stu-id="3eeeb-125">Inside hello `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="3eeeb-126">Depois de adicionar a marca do amazon hello, você pode ter um erro de compilação se o destino de compilação de projeto está abaixo Android 2.1.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-126">After adding hello amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="3eeeb-127">Você tem toouse um **Android 2.1 +** destino de compilação (não se preocupe, você ainda pode ter um `minSdkVersion` definido too4).</span><span class="sxs-lookup"><span data-stu-id="3eeeb-127">You have toouse an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set too4).</span></span>
* <span data-ttu-id="3eeeb-128">Integrar Olá ADM chave de API como um ativo seguindo [esse procedimento].</span><span class="sxs-lookup"><span data-stu-id="3eeeb-128">Integrate hello ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="3eeeb-129">Siga as instruções de saudação de próximas seções de saudação.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-129">Then follow hello instructions of hello next sections.</span></span>

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="3eeeb-130">Comunicar-se o serviço de envio do contrato de toohello do registro id e receber notificações</span><span class="sxs-lookup"><span data-stu-id="3eeeb-130">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="3eeeb-131">Na id de registro de saudação ordem toocommunicate de saudação dispositivo toohello envio do contrato de serviço e receber notificações, adicionar Olá após tooyour `AndroidManifest.xml` arquivo, dentro de saudação `<application/>` marca (mesmo se você usar ADM sem compromisso):</span><span class="sxs-lookup"><span data-stu-id="3eeeb-131">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you use ADM without Engagement):</span></span>

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

<span data-ttu-id="3eeeb-132">Certifique-se de ter Olá as seguintes permissões no seu `AndroidManifest.xml` (antes da saudação `</application>` marca).</span><span class="sxs-lookup"><span data-stu-id="3eeeb-132">Ensure you have hello following permissions in your `AndroidManifest.xml` (before hello `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="3eeeb-133">Conceda as credenciais do Engagement OAuth</span><span class="sxs-lookup"><span data-stu-id="3eeeb-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="3eeeb-134">Envie suas credenciais OAuth (ID do Cliente e Segredo do Cliente) no Portal do Engagement.</span><span class="sxs-lookup"><span data-stu-id="3eeeb-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[biblioteca de cliente ADM]:https://developer.amazon.com/sdk/adm/setup.html
[integrado ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[esse procedimento]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
