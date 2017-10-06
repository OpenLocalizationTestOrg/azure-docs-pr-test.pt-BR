---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - análise"
description: "Solução para problemas de Análise, Monitoramento, Segmentação e Painel no Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="96921-103">Guia de solução para problemas de Análise, Monitoramento, Segmentação e Painel</span><span class="sxs-lookup"><span data-stu-id="96921-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="96921-104">Olá, estes são os problemas possíveis podem ser encontrados em como o Azure Mobile Engagement reúne informações sobre dispositivos, aplicativos e usuários.</span><span class="sxs-lookup"><span data-stu-id="96921-104">hello following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="96921-105">Informações Ausentes/Atrasadas</span><span class="sxs-lookup"><span data-stu-id="96921-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="96921-106">Problema</span><span class="sxs-lookup"><span data-stu-id="96921-106">Issue</span></span>
* <span data-ttu-id="96921-107">As informações ficam atrasadas ao aparecerem na Análise, Segmentação ou Painel.</span><span class="sxs-lookup"><span data-stu-id="96921-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="96921-108">Faltam informações no Monitoramento.</span><span class="sxs-lookup"><span data-stu-id="96921-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="96921-109">As informações estão ausentes na Análise, Segmentação ou Painel.</span><span class="sxs-lookup"><span data-stu-id="96921-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="96921-110">Limite de segmentação atingido.</span><span class="sxs-lookup"><span data-stu-id="96921-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="96921-111">Causas</span><span class="sxs-lookup"><span data-stu-id="96921-111">Causes</span></span>
* <span data-ttu-id="96921-112">Você pode usar o hello análise de API, API de Monitor, e segmentos API toosee se todos os dados que você está ausente da saudação da interface do usuário é visível por meio de APIs de saudação.</span><span class="sxs-lookup"><span data-stu-id="96921-112">You can use hello Analytics API, Monitor API, and Segments API toosee if any data you are missing from hello UI is visible through hello APIs.</span></span>
* <span data-ttu-id="96921-113">Se Olá SDK do Azure Mobile Engagement não estiver integrado corretamente em seu aplicativo não será capaz de toosee informações Olá Analytics, segmentação, monitoramento ou painéis.</span><span class="sxs-lookup"><span data-stu-id="96921-113">If hello Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able toosee information in hello Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="96921-114">Os segmentos não podem ser alterados depois de criados; os segmentos só podem ser "clonados" (copiados) ou "destruídos" (excluídos).</span><span class="sxs-lookup"><span data-stu-id="96921-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="96921-115">Os segmentos podem conter apenas 10 critérios.</span><span class="sxs-lookup"><span data-stu-id="96921-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="96921-116">Olá melhor maneira tootest faltando informações de monitoramento é toosetup um dispositivo de teste, desinstalar e/ou reinstalar o aplicativo hello no dispositivo de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="96921-116">hello best way tootest missing information from monitoring is toosetup a test device, uninstall and/or reinstall hello app on hello test device.</span></span>
* <span data-ttu-id="96921-117">As informações são atualizadas a cada 24 horas para a Análise, Segmentação ou Painéis.</span><span class="sxs-lookup"><span data-stu-id="96921-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="96921-118">Informações em novos segmentos não podem ser exibidas até 24 horas após eles são criados, mesmo se o segmento de saudação se baseia em informações anteriores.</span><span class="sxs-lookup"><span data-stu-id="96921-118">Information in new segments may not be displayed until 24 hours after they are created even if hello segment is based on previous information.</span></span>
* <span data-ttu-id="96921-119">Filtrar seus dados de análise de saudação da interface do usuário mostrará todos os exemplos desse tipo, independentemente da versão de saudação do seu aplicativo (por exemplo as "Falhas" filtradas pelo nome aparecerão a partir das versões 1 e 2 de seu aplicativo).</span><span class="sxs-lookup"><span data-stu-id="96921-119">Filtering your analytics data in hello UI will show all examples of this type regardless of hello version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="96921-120">Hello período de tempo para análise é baseado nas Olá data dos usuários Olá configurações de dispositivo, para que um usuário cujo telefone tiver date de hello definida incorretamente pode aparecer em Olá errado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="96921-120">hello time period for Analytics is based on hello date from hello users' device settings, so a user whose phone has hello date incorrectly set could show up in hello wrong time period.</span></span>
* <span data-ttu-id="96921-121">Nenhum lado servidor dados são registrados quando você usar o botão de saudação muito "testar" envia, somente os dados serão registrados para campanhas de push real.</span><span class="sxs-lookup"><span data-stu-id="96921-121">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="96921-122">Não é possível localizar itens na interface do usuário</span><span class="sxs-lookup"><span data-stu-id="96921-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="96921-123">Problema</span><span class="sxs-lookup"><span data-stu-id="96921-123">Issue</span></span>
* <span data-ttu-id="96921-124">Não é possível criar segmentos com base em certos critérios incorporados ou de marca de informações do aplicativo personalizado.</span><span class="sxs-lookup"><span data-stu-id="96921-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="96921-125">Não é possível localizar certos critérios incorporados ou de marca de informações do aplicativo personalizado na Análise, Monitoramento ou Painéis.</span><span class="sxs-lookup"><span data-stu-id="96921-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="96921-126">Não é possível interpretar Olá dados em análises, monitoramento, segmentação ou painéis.</span><span class="sxs-lookup"><span data-stu-id="96921-126">Can't interpret hello data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="96921-127">Causas</span><span class="sxs-lookup"><span data-stu-id="96921-127">Causes</span></span>
* <span data-ttu-id="96921-128">Alguns itens internos e informações de aplicativo marcas só estão disponíveis como critérios de envio, mas não podem ser adicionadas tooa segmento ou visíveis de análise, monitoramento ou painel.</span><span class="sxs-lookup"><span data-stu-id="96921-128">Some built in items and app info tags are only available as push criteria but may not be added tooa segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="96921-129">Para baseado em itens e informações de aplicativo tooa segmento as marcas que não podem ser adicionadas, você precisará toosetup lista de critérios em cada Olá tooperform de campanha mesmo funcionar como destino com base em um segmento de direcionamento.</span><span class="sxs-lookup"><span data-stu-id="96921-129">For built in items and app info tags that can't be added tooa segment, you will need toosetup list of targeting criteria in each campaign tooperform hello same function as targeting based on a segment.</span></span>
* <span data-ttu-id="96921-130">Consulte menus de contexto Olá nas seções painéis, monitoramento, a segmentação e análise Olá Olá interface de usuário do Azure Mobile Engagement para obter mais ajuda e como tooinformation.</span><span class="sxs-lookup"><span data-stu-id="96921-130">See hello context menus in hello Analytics, Monitoring, Segmentation, and Dashboards sections of hello Azure Mobile Engagement UI for more help and how tooinformation.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="96921-131">Solucionar problemas de falhas</span><span class="sxs-lookup"><span data-stu-id="96921-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="96921-132">Problema</span><span class="sxs-lookup"><span data-stu-id="96921-132">Issue</span></span>
* <span data-ttu-id="96921-133">Falhas do Aplicativo que aparecem na Análise, Monitoramento ou Painel.</span><span class="sxs-lookup"><span data-stu-id="96921-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="96921-134">Causas</span><span class="sxs-lookup"><span data-stu-id="96921-134">Causes</span></span>
* <span data-ttu-id="96921-135">tootroubleshoot vistos no painel, monitoramento ou análise de falhas de aplicativo verifique se toocheck Olá notas para problemas conhecidos com versões anteriores do SDK de saudação.</span><span class="sxs-lookup"><span data-stu-id="96921-135">tootroubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure toocheck hello release notes for known issues with previous versions of hello SDK.</span></span>
* <span data-ttu-id="96921-136">toofurther solucionar falhas executam um evento de um dispositivo de teste com seu aplicativo seja instalado e procure a ID do dispositivo na seção hello "monitorar eventos de –" hello Azure Mobile Engagement interface de usuário de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="96921-136">toofurther troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in hello “Monitor – Events” section of hello Azure Mobile Engagement UI.</span></span> <span data-ttu-id="96921-137">Em seguida, execute o evento Olá que está causando toocrash seu aplicativo e pesquisar informações adicionais na Olá seção "Monitor – falhas" hello interface de usuário do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="96921-137">Then perform hello event that is causing your application toocrash and look up additional information in hello “Monitor – Crash” section of hello Azure Mobile Engagement UI.</span></span> 

