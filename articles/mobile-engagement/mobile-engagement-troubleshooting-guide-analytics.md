---
title: "Guia de Solução de Problemas do Azure Mobile Engagement - Análise"
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
ms.openlocfilehash: e30c9ac0a8421ffcf4fc3e2548cfd7ac49701900
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="fc581-103">Guia de solução para problemas de Análise, Monitoramento, Segmentação e Painel</span><span class="sxs-lookup"><span data-stu-id="fc581-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="fc581-104">Estes são os possíveis problemas que podem ser encontrados em como o Azure Mobile Engagement reúne informações sobre seus aplicativos, dispositivos e usuários.</span><span class="sxs-lookup"><span data-stu-id="fc581-104">The following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="fc581-105">Informações Ausentes/Atrasadas</span><span class="sxs-lookup"><span data-stu-id="fc581-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="fc581-106">Problema</span><span class="sxs-lookup"><span data-stu-id="fc581-106">Issue</span></span>
* <span data-ttu-id="fc581-107">As informações ficam atrasadas ao aparecerem na Análise, Segmentação ou Painel.</span><span class="sxs-lookup"><span data-stu-id="fc581-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="fc581-108">Faltam informações no Monitoramento.</span><span class="sxs-lookup"><span data-stu-id="fc581-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="fc581-109">As informações estão ausentes na Análise, Segmentação ou Painel.</span><span class="sxs-lookup"><span data-stu-id="fc581-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="fc581-110">Limite de segmentação atingido.</span><span class="sxs-lookup"><span data-stu-id="fc581-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="fc581-111">Causas</span><span class="sxs-lookup"><span data-stu-id="fc581-111">Causes</span></span>
* <span data-ttu-id="fc581-112">Você pode usar a API da Análise, API do Monitor e API dos Segmentos para verificar se todos os dados que faltam na interface do usuário são visíveis através das APIs.</span><span class="sxs-lookup"><span data-stu-id="fc581-112">You can use the Analytics API, Monitor API, and Segments API to see if any data you are missing from the UI is visible through the APIs.</span></span>
* <span data-ttu-id="fc581-113">Se o SDK do Azure Mobile Engagement não estiver integrado corretamente em seu aplicativo, você não conseguirá ver informações na Análise, Segmentação, Monitoramento ou Painéis.</span><span class="sxs-lookup"><span data-stu-id="fc581-113">If the Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able to see information in the Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="fc581-114">Os segmentos não podem ser alterados depois de criados; os segmentos só podem ser "clonados" (copiados) ou "destruídos" (excluídos).</span><span class="sxs-lookup"><span data-stu-id="fc581-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="fc581-115">Os segmentos podem conter apenas 10 critérios.</span><span class="sxs-lookup"><span data-stu-id="fc581-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="fc581-116">A melhor maneira de testar as informações ausentes do monitoramento é configurar um dispositivo de teste, desinstalação e/ou reinstalar o aplicativo no dispositivo de teste.</span><span class="sxs-lookup"><span data-stu-id="fc581-116">The best way to test missing information from monitoring is to setup a test device, uninstall and/or reinstall the app on the test device.</span></span>
* <span data-ttu-id="fc581-117">As informações são atualizadas a cada 24 horas para a Análise, Segmentação ou Painéis.</span><span class="sxs-lookup"><span data-stu-id="fc581-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="fc581-118">Informações em novos segmentos não podem ser exibidas até 24 horas após elas terem sido criadas, mesmo se o segmento estiver baseado nas informações anteriores.</span><span class="sxs-lookup"><span data-stu-id="fc581-118">Information in new segments may not be displayed until 24 hours after they are created even if the segment is based on previous information.</span></span>
* <span data-ttu-id="fc581-119">Filtrar seus dados de análise na interface do usuário mostrará todos os exemplos desse tipo, independentemente da versão de seu aplicativo (por exemplo, as "Falhas" filtradas pelo nome aparecerão a partir das versões 1 e 2 de seu aplicativo).</span><span class="sxs-lookup"><span data-stu-id="fc581-119">Filtering your analytics data in the UI will show all examples of this type regardless of the version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="fc581-120">O período de tempo para a Análise baseia-se na data das configurações do dispositivo dos usuários, portanto, um usuário cujo telefone tem a data definida incorretamente pode aparecer no período de tempo incorreto.</span><span class="sxs-lookup"><span data-stu-id="fc581-120">The time period for Analytics is based on the date from the users' device settings, so a user whose phone has the date incorrectly set could show up in the wrong time period.</span></span>
* <span data-ttu-id="fc581-121">Nenhum dado do lado do servidor é registrado quando você usa o botão “testar” envios, os dados são registrados apenas para campanhas de envio real.</span><span class="sxs-lookup"><span data-stu-id="fc581-121">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="fc581-122">Não é possível localizar itens na interface do usuário</span><span class="sxs-lookup"><span data-stu-id="fc581-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="fc581-123">Problema</span><span class="sxs-lookup"><span data-stu-id="fc581-123">Issue</span></span>
* <span data-ttu-id="fc581-124">Não é possível criar segmentos com base em certos critérios incorporados ou de marca de informações do aplicativo personalizado.</span><span class="sxs-lookup"><span data-stu-id="fc581-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="fc581-125">Não é possível localizar certos critérios incorporados ou de marca de informações do aplicativo personalizado na Análise, Monitoramento ou Painéis.</span><span class="sxs-lookup"><span data-stu-id="fc581-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="fc581-126">Não é possível interpretar os dados na Análise, Monitoramento, Segmentação ou Painéis.</span><span class="sxs-lookup"><span data-stu-id="fc581-126">Can't interpret the data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="fc581-127">Causas</span><span class="sxs-lookup"><span data-stu-id="fc581-127">Causes</span></span>
* <span data-ttu-id="fc581-128">Alguns itens incorporados e marcas de informações do aplicativo só estão disponíveis como critérios por push, mas podem não estar adicionados a um segmento nem visíveis na Análise, Monitoramento ou Painel.</span><span class="sxs-lookup"><span data-stu-id="fc581-128">Some built in items and app info tags are only available as push criteria but may not be added to a segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="fc581-129">Para os itens incorporados e marcas de informações do aplicativo que não podem ser adicionados a um segmento, você precisará configurar uma lista de critérios de destino em cada campanha para executar a mesma função como o destino com base em um segmento.</span><span class="sxs-lookup"><span data-stu-id="fc581-129">For built in items and app info tags that can't be added to a segment, you will need to setup list of targeting criteria in each campaign to perform the same function as targeting based on a segment.</span></span>
* <span data-ttu-id="fc581-130">Consulte os menus contextuais nas seções Análise, Monitoramento, Segmentação e Painéis da interface do usuário do Azure Mobile Engagement para obter mais ajuda e informações.</span><span class="sxs-lookup"><span data-stu-id="fc581-130">See the context menus in the Analytics, Monitoring, Segmentation, and Dashboards sections of the Azure Mobile Engagement UI for more help and how to information.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="fc581-131">Solucionar problemas de falhas</span><span class="sxs-lookup"><span data-stu-id="fc581-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="fc581-132">Problema</span><span class="sxs-lookup"><span data-stu-id="fc581-132">Issue</span></span>
* <span data-ttu-id="fc581-133">Falhas do Aplicativo que aparecem na Análise, Monitoramento ou Painel.</span><span class="sxs-lookup"><span data-stu-id="fc581-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="fc581-134">Causas</span><span class="sxs-lookup"><span data-stu-id="fc581-134">Causes</span></span>
* <span data-ttu-id="fc581-135">Para solucionar as Falhas do Aplicativo vistas na Análise, Monitoramento ou Painel, verifique as notas de versão para os problemas conhecidos com as versões anteriores do SDK.</span><span class="sxs-lookup"><span data-stu-id="fc581-135">To troubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure to check the release notes for known issues with previous versions of the SDK.</span></span>
* <span data-ttu-id="fc581-136">Para solucionar falhas adicionais do aplicativo execute um evento de um dispositivo de teste com seu aplicativo instalado e procure o ID do dispositivo na seção “Monitor – eventos” da interface de usuário do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="fc581-136">To further troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in the “Monitor – Events” section of the Azure Mobile Engagement UI.</span></span> <span data-ttu-id="fc581-137">Em seguida, execute o mesmo que está causando a falha no seu aplicativo e pesquise por informações adicionais na seção “Monitoramento – falha” na interface do usuário do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="fc581-137">Then perform the event that is causing your application to crash and look up additional information in the “Monitor – Crash” section of the Azure Mobile Engagement UI.</span></span> 

