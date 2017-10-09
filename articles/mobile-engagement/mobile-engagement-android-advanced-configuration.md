---
title: "configuração de aaaAdvanced para Android SDK do Azure Mobile Engagement"
description: "Descreve Olá incluindo Olá manifesto do Android com o SDK do Azure Mobile Engagement Android de opções de configuração avançada"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="4e1d0-103">Configuração avançada do SDK do Azure Mobile Engagement para Android</span><span class="sxs-lookup"><span data-stu-id="4e1d0-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e1d0-104">Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="4e1d0-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="4e1d0-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="4e1d0-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="4e1d0-106">iOS</span><span class="sxs-lookup"><span data-stu-id="4e1d0-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="4e1d0-107">Android</span><span class="sxs-lookup"><span data-stu-id="4e1d0-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="4e1d0-108">Este procedimento descreve como tooconfigure várias opções de configuração para aplicativos do Azure Mobile Engagement Android.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e1d0-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4e1d0-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="4e1d0-110">Requisitos de permissão</span><span class="sxs-lookup"><span data-stu-id="4e1d0-110">Permission Requirements</span></span>
<span data-ttu-id="4e1d0-111">Algumas opções requerem permissões específicas, que são listadas aqui para referência e em linha no recurso específico de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-111">Some options require specific permissions, all of which are listed here for reference, and in-line in hello specific feature.</span></span> <span data-ttu-id="4e1d0-112">Adicionar toohello essas permissões AndroidManifest.xml do seu projeto imediatamente antes ou após Olá `<application>` marca.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-112">Add these permissions toohello AndroidManifest.xml of your project immediately before or after hello `<application>` tag.</span></span>

<span data-ttu-id="4e1d0-113">código de permissão de saudação precisa toolook com hello seguinte, onde você preenche a permissão apropriada Olá da tabela de saudação que segue.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-113">hello permission code needs toolook like hello following, where you fill in hello appropriate permission from hello table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="4e1d0-114">Permissão</span><span class="sxs-lookup"><span data-stu-id="4e1d0-114">Permission</span></span> | <span data-ttu-id="4e1d0-115">Quando usado</span><span class="sxs-lookup"><span data-stu-id="4e1d0-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="4e1d0-116">INTERNET</span><span class="sxs-lookup"><span data-stu-id="4e1d0-116">INTERNET</span></span> |<span data-ttu-id="4e1d0-117">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-117">Required.</span></span> <span data-ttu-id="4e1d0-118">Para relatório básico</span><span class="sxs-lookup"><span data-stu-id="4e1d0-118">For basic reporting</span></span> |
| <span data-ttu-id="4e1d0-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="4e1d0-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="4e1d0-120">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-120">Required.</span></span> <span data-ttu-id="4e1d0-121">Para relatório básico</span><span class="sxs-lookup"><span data-stu-id="4e1d0-121">For basic reporting</span></span> |
| <span data-ttu-id="4e1d0-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="4e1d0-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="4e1d0-123">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-123">Required.</span></span> <span data-ttu-id="4e1d0-124">tooshow a Central de notificações de saudação após a reinicialização do dispositivo</span><span class="sxs-lookup"><span data-stu-id="4e1d0-124">tooshow up hello notifications center after device reboot</span></span> |
| <span data-ttu-id="4e1d0-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="4e1d0-125">WAKE_LOCK</span></span> |<span data-ttu-id="4e1d0-126">Recomendável.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-126">Recommended.</span></span> <span data-ttu-id="4e1d0-127">Habilita a coleta de dados ao usar Wi-Fi ou quando a tela estiver desligada</span><span class="sxs-lookup"><span data-stu-id="4e1d0-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="4e1d0-128">VIBRATE</span><span class="sxs-lookup"><span data-stu-id="4e1d0-128">VIBRATE</span></span> |<span data-ttu-id="4e1d0-129">Opcional.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-129">Optional.</span></span> <span data-ttu-id="4e1d0-130">Habilita a vibração após o recebimento de notificações</span><span class="sxs-lookup"><span data-stu-id="4e1d0-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="4e1d0-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="4e1d0-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="4e1d0-132">Opcional.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-132">Optional.</span></span> <span data-ttu-id="4e1d0-133">Habilita a notificação de visão geral do Android</span><span class="sxs-lookup"><span data-stu-id="4e1d0-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="4e1d0-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="4e1d0-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="4e1d0-135">Opcional.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-135">Optional.</span></span> <span data-ttu-id="4e1d0-136">Habilita a notificação de visão geral do Android</span><span class="sxs-lookup"><span data-stu-id="4e1d0-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="4e1d0-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="4e1d0-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="4e1d0-138">Opcional.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-138">Optional.</span></span> <span data-ttu-id="4e1d0-139">Habilita o relatório de local em tempo real</span><span class="sxs-lookup"><span data-stu-id="4e1d0-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="4e1d0-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="4e1d0-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="4e1d0-141">Opcional.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-141">Optional.</span></span> <span data-ttu-id="4e1d0-142">Habilita o relatório de local baseado em GPS</span><span class="sxs-lookup"><span data-stu-id="4e1d0-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="4e1d0-143">A partir do Android M, [algumas permissões são gerenciadas em tempo de execução](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="4e1d0-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="4e1d0-144">Se você já estiver usando ``ACCESS_FINE_LOCATION``, em seguida, você não precisa tooalso usar ``ACCESS_COARSE_LOCATION``.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need tooalso use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="4e1d0-145">Opções de configuração do manifesto do Android</span><span class="sxs-lookup"><span data-stu-id="4e1d0-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="4e1d0-146">Relatório de falha</span><span class="sxs-lookup"><span data-stu-id="4e1d0-146">Crash report</span></span>
<span data-ttu-id="4e1d0-147">relatórios de falha de toodisable, adicione este código entre hello `<application>` e `</application>` marcas:</span><span class="sxs-lookup"><span data-stu-id="4e1d0-147">toodisable crash reports, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="4e1d0-148">Limite de intermitência</span><span class="sxs-lookup"><span data-stu-id="4e1d0-148">Burst threshold</span></span>
<span data-ttu-id="4e1d0-149">Por padrão, os relatórios de serviço de contrato de saudação logs em tempo real.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-149">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="4e1d0-150">Se seus logs de aplicativo de relatório variam de acordo com frequência, é melhor toobuffer Olá logs e tooreport-los todos de uma vez em um base de tempo regulares (chamado de "modo de disparar").</span><span class="sxs-lookup"><span data-stu-id="4e1d0-150">If your application report logs vary frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="4e1d0-151">toodo por isso, adicione este código entre hello `<application>` e `</application>` marcas:</span><span class="sxs-lookup"><span data-stu-id="4e1d0-151">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="4e1d0-152">Modo intermitente ligeiramente aumenta a vida útil da bateria Olá mas tem um impacto em Olá contrato Monitor: todas as sessões e trabalhos a duração são arredondados toohello intermitência limite (portanto, sessões e menor do que o limite de disparo Olá pode não estar visível de trabalhos).</span><span class="sxs-lookup"><span data-stu-id="4e1d0-152">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="4e1d0-153">O limite de disparo contínuo não deve ser maior do que 30.000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="4e1d0-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="4e1d0-154">Tempo limite da sessão</span><span class="sxs-lookup"><span data-stu-id="4e1d0-154">Session timeout</span></span>
 <span data-ttu-id="4e1d0-155">Você pode finalizar uma atividade pressionando Olá **início** ou **novamente** chave, por definição Olá telefone ocioso ou pulando em outro aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-155">You can end an activity by pressing hello **Home** or **Back** key, by setting hello phone idle or by jumping into another application.</span></span> <span data-ttu-id="4e1d0-156">Por padrão, uma sessão será encerrada dez segundos após o término de saudação de sua última atividade.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-156">By default, a session is ended ten seconds after hello end of its last activity.</span></span> <span data-ttu-id="4e1d0-157">Isso evita uma divisão de sessão cada usuário em tempo de saudação encerrado e retorna o aplicativo toohello rapidamente, que pode acontecer quando o usuário Olá pega uma imagem, verifica uma notificação, etc. Talvez você queira toomodify esse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-157">This avoids a session split each time hello user exits and returns toohello application quickly, which can happen when hello user picks up an image, checks a notification, etc. You may want toomodify this parameter.</span></span> <span data-ttu-id="4e1d0-158">toodo por isso, adicione este código entre hello `<application>` e `</application>` marcas:</span><span class="sxs-lookup"><span data-stu-id="4e1d0-158">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="4e1d0-159">Desabilitar o relatório de log</span><span class="sxs-lookup"><span data-stu-id="4e1d0-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="4e1d0-160">Usando uma chamada de método</span><span class="sxs-lookup"><span data-stu-id="4e1d0-160">Using a method call</span></span>
<span data-ttu-id="4e1d0-161">Se você quiser toostop contrato envio de logs, você pode chamar:</span><span class="sxs-lookup"><span data-stu-id="4e1d0-161">If you want Engagement toostop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="4e1d0-162">Essa chamada é persistente: ela utiliza um arquivo de preferências compartilhado.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="4e1d0-163">Se o contrato está ativo, quando você chamar essa função, pode levar um minuto para Olá toostop de serviço.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-163">If Engagement is active when you call this function, it may take one minute for hello service toostop.</span></span> <span data-ttu-id="4e1d0-164">No entanto, não é possível abrir serviço Olá Olá todos próxima vez que você iniciar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-164">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="4e1d0-165">Você pode habilitar o log de relatórios novamente chamando Olá a mesma função com `true`.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-165">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="4e1d0-166">Integração em seu próprio `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="4e1d0-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="4e1d0-167">Em vez de chamar essa função, você também pode integrar esta configuração diretamente em seu arquivo existente `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="4e1d0-168">Você pode configurar contrato toouse suas preferências de arquivo (com modo desejado de saudação) Olá `AndroidManifest.xml` arquivo com `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="4e1d0-168">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="4e1d0-169">Olá `engagement:agent:settings:name` chave é usado toodefine Olá nome do arquivo de preferências compartilhadas Olá.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-169">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="4e1d0-170">Olá `engagement:agent:settings:mode` chave é o modo de saudação toodefine usado do arquivo de preferências compartilhadas hello.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-170">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file.</span></span> <span data-ttu-id="4e1d0-171">Use Olá mesmo modo que no seu `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-171">Use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="4e1d0-172">Olá modo deve ser passado como um número: se você estiver usando uma combinação de sinalizadores constantes em seu código, verifique o valor total de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-172">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="4e1d0-173">Contrato sempre usa Olá `engagement:key` booliano chave no arquivo de preferências de saudação para gerenciar essa configuração.</span><span class="sxs-lookup"><span data-stu-id="4e1d0-173">Engagement always uses hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="4e1d0-174">Olá seguindo o exemplo de `AndroidManifest.xml` mostra Olá valores padrão:</span><span class="sxs-lookup"><span data-stu-id="4e1d0-174">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="4e1d0-175">Em seguida, você pode adicionar um `CheckBoxPreference` em seu layout de preferência como Olá seguindo um:</span><span class="sxs-lookup"><span data-stu-id="4e1d0-175">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
