---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
description: "Solucionando problemas de integração do SDK no Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="fd5d8-103">Guia de solução de problemas de integração do SDK</span><span class="sxs-lookup"><span data-stu-id="fd5d8-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="fd5d8-104">Olá seguem possíveis problemas que podem ocorrer com como do Azure Mobile Engagement se integra ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-104">hello following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="fd5d8-105">Problemas SDK descobertos por uma falha em outra área do aplicativo</span><span class="sxs-lookup"><span data-stu-id="fd5d8-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="fd5d8-106">Problema</span><span class="sxs-lookup"><span data-stu-id="fd5d8-106">Issue</span></span>
* <span data-ttu-id="fd5d8-107">Falha de coleta de dados da interface do usuário (em Análise, Monitoramento, Segmentação ou Painéis).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="fd5d8-108">Falhas de envios por push (os envios por push não funcionam no aplicativo, fora do aplicativo ou ambos).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="fd5d8-109">Falhas de Recursos Avançados (Rastreamento, Localização geográfica ou Envios por Push de plataformas específicas que não funcionam).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="fd5d8-110">Falhas de API (geralmente, as falhas de API são silenciosas, sem mensagens de erro).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="fd5d8-111">Falhas de Serviço (nada no Azure Mobile Engagement funciona para seu aplicativo).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="fd5d8-112">Causas</span><span class="sxs-lookup"><span data-stu-id="fd5d8-112">Causes</span></span>
* <span data-ttu-id="fd5d8-113">A maioria dos problemas que precisam toobe resolvido com hello SDK do Azure Mobile Engagement serão descobertos por uma falha em seu aplicativo (por exemplo, uma falha de coleta de dados de interface do usuário, falha de envio, falha de recurso avançado, falha da API, falhas de aplicativo ou serviço aparente interrupção).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-113">Most issues that need toobe resolved with hello Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="fd5d8-114">Se um recurso específico do Azure Mobile Engagement nunca trabalhou em seu aplicativo antes, você precisará toocomplete integração de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need toocomplete hello integration.</span></span> 
* <span data-ttu-id="fd5d8-115">Se um recurso específico do Azure Mobile Engagement estava trabalhando e interrompido, talvez seja necessário tooupgrade toohello a última versão com hello SDK do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need tooupgrade toohello last version with hello Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="fd5d8-116">Lembre-se de que há uma versão diferente do hello SDK do Azure Mobile Engagement para cada plataforma com suporte pelo Azure Mobile Engagement (Android, iOS, Windows e Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-116">Remember that there is a different version of hello Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="fd5d8-117">Integração do SDK</span><span class="sxs-lookup"><span data-stu-id="fd5d8-117">SDK Integration</span></span>
* <span data-ttu-id="fd5d8-118">O Azure Mobile Engagement não está corretamente integrado no SDK (Análise).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="fd5d8-119">O Alcance não está corretamente integrado no SDK (Envio por Push No Aplicativo e Fora do Aplicativo).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="fd5d8-120">Certificado expirado ou incorreto PROD versus DEV (somente iOS).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="fd5d8-121">GCM ou ADM não estão corretamente integrados no SDK (somente Android - Envios por Push Específicos do Serviço).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="fd5d8-122">O rastreamento não está corretamente integrado no SDK (instalar rastreamento de loja).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="fd5d8-123">Localização lenta ou Localização de GPS não estão corretamente integradas no SDK (direcionamento por localização geográfica).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="fd5d8-124">**Consulte também:**</span><span class="sxs-lookup"><span data-stu-id="fd5d8-124">**See also:**</span></span>

* <span data-ttu-id="fd5d8-125">[Documentação do SDK ‑ Guias de Integração][Link 5]</span><span class="sxs-lookup"><span data-stu-id="fd5d8-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="fd5d8-126">[Guia de solução de problemas – Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="fd5d8-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="fd5d8-127">Atualização do SDK</span><span class="sxs-lookup"><span data-stu-id="fd5d8-127">SDK Upgrade</span></span>
* <span data-ttu-id="fd5d8-128">Precisa de problemas de tooresolve tooupgrade SDK com versões mais antigas do hello SDK (geralmente relacionados toonewer versões do SO do dispositivo Olá).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-128">Need tooupgrade SDK tooresolve issues with older versions of hello SDK (often related toonewer versions of hello device OS).</span></span>
* <span data-ttu-id="fd5d8-129">Desinstale todas as versões anteriores do aplicativo do dispositivo e reinstale a versão mais recente de saudação do seu aplicativo, Olá registrar novamente a ID do dispositivo de tooconfirm de interface de usuário do Azure Mobile Engagement Olá que seu dispositivo está usando a versão mais recente de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-129">Uninstall all previous versions of your app from your device and reinstall hello newest version of your app, hello re-register your Device ID from hello Azure Mobile Engagement UI tooconfirm that your device is using hello newest version of your app.</span></span>

<span data-ttu-id="fd5d8-130">**Consulte também:**</span><span class="sxs-lookup"><span data-stu-id="fd5d8-130">**See also:**</span></span>

* [<span data-ttu-id="fd5d8-131">Documentação do SDK - Notas de versão</span><span class="sxs-lookup"><span data-stu-id="fd5d8-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="fd5d8-132">Documentação do SDK - Guias de atualização</span><span class="sxs-lookup"><span data-stu-id="fd5d8-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="fd5d8-133">Outros problemas no SDK</span><span class="sxs-lookup"><span data-stu-id="fd5d8-133">SDK Other</span></span>
* <span data-ttu-id="fd5d8-134">Erros no manifesto do aplicativo "AndroidManifest.xml" podem fazer com que o Azure Mobile Engagement toowork (somente Android).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not toowork (Android only).</span></span>
* <span data-ttu-id="fd5d8-135">Um problema comum com integração SDK e o uso da API é tooconfuse hello chave SDK e Olá chave de API.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-135">A common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>

<span data-ttu-id="fd5d8-136">**Consulte também:**</span><span class="sxs-lookup"><span data-stu-id="fd5d8-136">**See also:**</span></span>

* <span data-ttu-id="fd5d8-137">[Conceitos ‑ Glossário][Link 6]</span><span class="sxs-lookup"><span data-stu-id="fd5d8-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="fd5d8-138">Problemas de codificação avançados</span><span class="sxs-lookup"><span data-stu-id="fd5d8-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="fd5d8-139">Problema</span><span class="sxs-lookup"><span data-stu-id="fd5d8-139">Issue</span></span>
* <span data-ttu-id="fd5d8-140">Código específico de plataforma não estão diretamente relacionadas tooAzure que Mobile Engagement pode causar problemas no iOS, Android e Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-140">Platform specific code not directly related tooAzure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="fd5d8-141">Causas</span><span class="sxs-lookup"><span data-stu-id="fd5d8-141">Causes</span></span>
* <span data-ttu-id="fd5d8-142">Muitos problemas de codificação com o Azure Mobile Engagement avançados são causados por plataforma escrita incorretamente o código específico não estão diretamente relacionadas tooAzure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related tooAzure Mobile Engagement.</span></span> <span data-ttu-id="fd5d8-143">Você precisará tooconsult plataforma de toohello específico de documentação que está desenvolvendo para além de documentação do Mobile Engagement tooAzure (Android, iOS, Web, Windows e Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-143">You will need tooconsult documentation specific toohello platform you are developing for in addition tooAzure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="fd5d8-144">Configurar não corretamente "categorias", impede a vinculação de um local de tooanother notificação dentro ou fora do aplicativo hello (somente Android).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-144">Not correctly configuring "categories", prevents linking from a notification tooanother location either inside or outside of hello app (Android only).</span></span> 
* <span data-ttu-id="fd5d8-145">Não, definindo "UIKit.framework" muito "opcional" no código do iOS, exibe um "Símbolo não encontrado o erro" e/ou falhas em dispositivos mais antigos do iOS (somente iOS).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-145">Not setting "UIKit.framework" too"optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="fd5d8-146">Certificados expirados ou não corretamente usando Olá desenvolvimento ou a versão de produção do cert hello, problemas de envio de causas (somente iOS).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-146">Expired certificates or not correctly using hello DEV or Prod version of hello cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="fd5d8-147">Há alguns plataforma tooa inerentes limitações que não é possível controlar o Azure Mobile Engagement (como como Olá system center funciona para fora do aplicativo envia no Android e iOS).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-147">There are some limitations inherent tooa platform that Azure Mobile Engagement can't control (like how hello system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="fd5d8-148">O Azure Mobile Engagement publica uma lista completa dos pacotes de interno Olá usado pelo Azure Mobile Engagement para Android e iOS para referência.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-148">Azure Mobile Engagement publishes a full list of hello internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="fd5d8-149">Tenha em mente que alguns recursos do Azure Mobile Engagement são toohello específico de plataforma (Android, iOS, Web, Windows e Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-149">Keep in mind that some features of Azure Mobile Engagement are specific toohello platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="fd5d8-150">Consulte também</span><span class="sxs-lookup"><span data-stu-id="fd5d8-150">See also</span></span>
* <span data-ttu-id="fd5d8-151">[Guia de solução de problemas – Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="fd5d8-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="fd5d8-152">[Documentação do SDK – Notas de Versão][Link 5]</span><span class="sxs-lookup"><span data-stu-id="fd5d8-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="fd5d8-153">[Documentação do SDK ‑ Guias de Atualização][Link 5]</span><span class="sxs-lookup"><span data-stu-id="fd5d8-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="fd5d8-154">Falhas do aplicativo</span><span class="sxs-lookup"><span data-stu-id="fd5d8-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="fd5d8-155">Problema</span><span class="sxs-lookup"><span data-stu-id="fd5d8-155">Issue</span></span>
* <span data-ttu-id="fd5d8-156">Falhas do seu aplicativo no dispositivo Olá dos usuários finais.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-156">Your application crashes on hello end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="fd5d8-157">Causas</span><span class="sxs-lookup"><span data-stu-id="fd5d8-157">Causes</span></span>
* <span data-ttu-id="fd5d8-158">Informações de falha podem ser exibidas no hello *análise de interface do usuário* ou hello *API de análise*</span><span class="sxs-lookup"><span data-stu-id="fd5d8-158">Crash information can be viewed in hello *Analytics UI* or hello *Analytics API*</span></span>
* <span data-ttu-id="fd5d8-159">Você pode encontrar hello ID do dispositivo do seu dispositivo de teste e tomar Olá mesma ação que causou toocrash seu aplicativo para um usuário final toohelp identificar a causa de saudação do sua falha.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-159">You can find hello Device ID of your test device and take hello same action that caused your application toocrash for an end user toohelp identify hello cause of your crash.</span></span>
* <span data-ttu-id="fd5d8-160">Problemas conhecidos com hello SDK do Azure Mobile Engagement que fazer com que aplicativos toocrash às vezes são resolvidos pela atualização toohello a versão mais recente do SDK de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-160">Known issues with hello Azure Mobile Engagement SDK that cause applications toocrash are sometimes resolved by upgrading toohello latest version of hello SDK.</span></span> <span data-ttu-id="fd5d8-161">Verifique se toocheck Olá notas sobre sua plataforma ao investigar falhas.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-161">Make sure toocheck hello release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="fd5d8-162">Consulte também</span><span class="sxs-lookup"><span data-stu-id="fd5d8-162">See also</span></span>
* <span data-ttu-id="fd5d8-163">[Documentação do SDK – Notas de Versão][Link 5]</span><span class="sxs-lookup"><span data-stu-id="fd5d8-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="fd5d8-164">[Documentação do SDK ‑ Guias de Atualização][Link 5]</span><span class="sxs-lookup"><span data-stu-id="fd5d8-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="fd5d8-165">Falhas de carregamento nas lojas de aplicativos</span><span class="sxs-lookup"><span data-stu-id="fd5d8-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="fd5d8-166">Problema</span><span class="sxs-lookup"><span data-stu-id="fd5d8-166">Issue</span></span>
* <span data-ttu-id="fd5d8-167">Erros relacionados a versão mais recente do toouploading saudação do aplicativo tooApple, Google ou armazenamento de aplicativo do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-167">Errors related toouploading hello latest version of your app tooApple, Google, or hello Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="fd5d8-168">Causas</span><span class="sxs-lookup"><span data-stu-id="fd5d8-168">Causes</span></span>
* <span data-ttu-id="fd5d8-169">Aplicativo às vezes armazenar aplicativos de bloco com determinados recursos habilitados (por exemplo, Olá Apple Store impede o uso de saudação do IDFV em aplicativos no repositório de saudação e repositório de GooglePlay Olá impede Olá compartilhamento de informações de aplicativo entre aplicativos).</span><span class="sxs-lookup"><span data-stu-id="fd5d8-169">App stores sometimes block apps with certain features enabled (e.g. hello Apple Store prevents hello use of IDFV in apps in hello store and hello GooglePlay store prevents hello sharing of application information between apps).</span></span> 
* <span data-ttu-id="fd5d8-170">Certifique-se de que você verifique as notas de versão de hello sobre a plataforma e a versão atual do SDK de saudação se você tiver dificuldade para carregar uma loja de aplicativos toohello.</span><span class="sxs-lookup"><span data-stu-id="fd5d8-170">Make sure that you check hello release notes about your platform and current version of hello SDK if you have difficulty uploading an app toohello store.</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

