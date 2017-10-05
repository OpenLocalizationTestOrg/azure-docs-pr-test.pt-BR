---
title: "Integração do SDK do Android do Azure Mobile Engagement"
description: "Atualizações e procedimentos mais recentes para o SDK do Android do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: c179c39a43da0aa35e945acceacbf27fe8e328f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes"></a><span data-ttu-id="281df-103">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="281df-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="281df-104">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="281df-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="281df-105">Corrigir uma falha que raramente poderia acontecer ao chamar `EngagementAgentUtils.isInDedicatedEngagementProcess`, que também é usado pela classe `EngagementApplication`.</span><span class="sxs-lookup"><span data-stu-id="281df-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="281df-106">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="281df-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="281df-107">Suporte para Android 8 (versões anteriores do SDK não funcionarão em Android 8).</span><span class="sxs-lookup"><span data-stu-id="281df-107">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="281df-108">Não há mais dependência da biblioteca de suporte.</span><span class="sxs-lookup"><span data-stu-id="281df-108">No more dependency on support library.</span></span>
* <span data-ttu-id="281df-109">Remover classe `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="281df-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="281df-110">Devido a [Limites de Execução em Segundo de Fundo](https://developer.android.com/preview/features/background.html) no Android 8, logs no segundo plano podem ser atrasados até que o usuário interaja com o dispositivo. Isso terá um impacto sobre Campanha de Push **Entregue** e estatísticas de **Notificação do sistema exibida** sendo atrasadas no caso de dispositivo estar em suspensão (a notificação ainda será exibida, tocará e vibrará em tempo real sem problemas).</span><span class="sxs-lookup"><span data-stu-id="281df-110">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="281df-111">Devido a [Limites de Local do Segundo Plano](https://developer.android.com/preview/features/background-location-limits.html), o local em tempo real em segundo plano não será atualizado com frequência no Android 8.</span><span class="sxs-lookup"><span data-stu-id="281df-111">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="281df-112">4.2.4 (30/03/2017)</span><span class="sxs-lookup"><span data-stu-id="281df-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="281df-113">Corrija cores do texto de notificação no aplicativo Android 7 para serem as mesmas de versões mais antigas do Android.</span><span class="sxs-lookup"><span data-stu-id="281df-113">Fix in-app notification text colors on Android 7 to be the same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="281df-114">4.2.3 (08/10/2016)</span><span class="sxs-lookup"><span data-stu-id="281df-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="281df-115">Nenhum outro bloqueio de WIFI.</span><span class="sxs-lookup"><span data-stu-id="281df-115">No more WIFI lock.</span></span>
* <span data-ttu-id="281df-116">Corrige um deadlock ao chamar getDeviceId antes de init (bug introduzido na versão 4.2.0).</span><span class="sxs-lookup"><span data-stu-id="281df-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="281df-117">4.2.2 (17/05/2016)</span><span class="sxs-lookup"><span data-stu-id="281df-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="281df-118">Aprimoramentos de estabilidade.</span><span class="sxs-lookup"><span data-stu-id="281df-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="281df-119">4.2.1 (10/05/2016)</span><span class="sxs-lookup"><span data-stu-id="281df-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="281df-120">Segurança: desabilite o acesso de arquivo local de exibição na Web.</span><span class="sxs-lookup"><span data-stu-id="281df-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="281df-121">Segurança: remova a classe `EngagementPreferenceActivity` que estende a classe `PreferenceActivity` obsoleta e não segura.</span><span class="sxs-lookup"><span data-stu-id="281df-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="281df-122">Segurança: as atividades de alcance agora estão documentadas para usar `exported="false"`; esse sinalizador também pode ser usado nas versões anteriores do SDK.</span><span class="sxs-lookup"><span data-stu-id="281df-122">Security: reach activities are now documented to use `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="281df-123">4.2.0 (03/11/2016)</span><span class="sxs-lookup"><span data-stu-id="281df-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="281df-124">O SDK está licenciado sob MIT.</span><span class="sxs-lookup"><span data-stu-id="281df-124">The SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="281df-125">Permita a especificação de um identificador de dispositivo personalizado no momento de inicialização do SDK.</span><span class="sxs-lookup"><span data-stu-id="281df-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="281df-126">4.1.5 (01/02/2016)</span><span class="sxs-lookup"><span data-stu-id="281df-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="281df-127">Aprimoramentos de estabilidade.</span><span class="sxs-lookup"><span data-stu-id="281df-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="281df-128">4.1.4 (26/01/2016)</span><span class="sxs-lookup"><span data-stu-id="281df-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="281df-129">Aprimoramentos de estabilidade.</span><span class="sxs-lookup"><span data-stu-id="281df-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="281df-130">4.1.3 (09/12/2015)</span><span class="sxs-lookup"><span data-stu-id="281df-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="281df-131">Aprimoramentos de estabilidade.</span><span class="sxs-lookup"><span data-stu-id="281df-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="281df-132">4.1.2 (25/11/2015)</span><span class="sxs-lookup"><span data-stu-id="281df-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="281df-133">Aprimoramentos de estabilidade.</span><span class="sxs-lookup"><span data-stu-id="281df-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="281df-134">4.1.1 (04/11/2015)</span><span class="sxs-lookup"><span data-stu-id="281df-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="281df-135">Aprimoramentos de estabilidade.</span><span class="sxs-lookup"><span data-stu-id="281df-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="281df-136">4.1.0 (25/08/2015)</span><span class="sxs-lookup"><span data-stu-id="281df-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="281df-137">Lidar com o novo modelo de permissão para Android M.</span><span class="sxs-lookup"><span data-stu-id="281df-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="281df-138">Agora é possível configurar os recursos de localização no tempo de execução em vez de usar o `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="281df-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="281df-139">Corrija um bug de permissão: se você usar `ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION` não será mais necessário.</span><span class="sxs-lookup"><span data-stu-id="281df-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="281df-140">Aprimoramentos de estabilidade.</span><span class="sxs-lookup"><span data-stu-id="281df-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="281df-141">4.0.0 (07/06/2015)</span><span class="sxs-lookup"><span data-stu-id="281df-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="281df-142">Alterações de protocolo interno para tornar a análise e o envio mais confiáveis.</span><span class="sxs-lookup"><span data-stu-id="281df-142">Internal protocol changes to make analytics and push more reliable.</span></span>
* <span data-ttu-id="281df-143">O push nativo (GCM/ADM) agora também é usado nas notificações de aplicativo para que você deve configurar as credenciais de push nativo para qualquer tipo de campanha de envio.</span><span class="sxs-lookup"><span data-stu-id="281df-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="281df-144">Corrigir a notificação de visão geral: foram exibidas somente 10s depois de enviadas.</span><span class="sxs-lookup"><span data-stu-id="281df-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="281df-145">Corrigir um bug no modo de exibição da web: ao clicar em um link também estava sendo executada a URL da ação padrão.</span><span class="sxs-lookup"><span data-stu-id="281df-145">Fix a bug in web view: clicking on a link was also executing the default action URL.</span></span>
* <span data-ttu-id="281df-146">Corrigir uma falha rara relacionada ao gerenciamento de armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="281df-146">Fix a rare crash related to local storage management.</span></span>
* <span data-ttu-id="281df-147">Corrigir o gerenciamento de cadeia de caracteres de configuração dinâmica.</span><span class="sxs-lookup"><span data-stu-id="281df-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="281df-148">Atualizar EULA.</span><span class="sxs-lookup"><span data-stu-id="281df-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="281df-149">3.0.0 (17/02/2015)</span><span class="sxs-lookup"><span data-stu-id="281df-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="281df-150">Versão Inicial do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="281df-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="281df-151">A configuração do appId é substituída por uma configuração de cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="281df-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="281df-152">Removida a API para enviar e receber mensagens XMPP arbitrárias de entidades XMPP arbitrárias.</span><span class="sxs-lookup"><span data-stu-id="281df-152">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="281df-153">Removida a API para enviar e receber mensagens entre dispositivos.</span><span class="sxs-lookup"><span data-stu-id="281df-153">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="281df-154">Aprimoramentos de segurança.</span><span class="sxs-lookup"><span data-stu-id="281df-154">Security improvements.</span></span>
* <span data-ttu-id="281df-155">Acompanhamento do Google Play e SmartAd removido.</span><span class="sxs-lookup"><span data-stu-id="281df-155">Google Play and SmartAd tracking removed.</span></span>

