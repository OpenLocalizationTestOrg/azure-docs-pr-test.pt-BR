---
title: "Estatísticas em tempo real na CDN do Azure | Microsoft Docs"
description: "As estatísticas em tempo real fornecem dados em tempo real sobre o desempenho da CDN do Azure ao fornecer conteúdo para os clientes."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e9b9522de6b2c54dc794b00100ffe358296ecfdd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="2b42b-103">Estatísticas em tempo real na CDN do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2b42b-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="2b42b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2b42b-104">Overview</span></span>
<span data-ttu-id="2b42b-105">Este documento explica as estatísticas em tempo real na CDN do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2b42b-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="2b42b-106">Essa funcionalidade fornece dados em tempo real, como a largura de banda, status do cache e conexões simultâneas, para seu perfil da CDN ao fornecer conteúdo para os clientes.</span><span class="sxs-lookup"><span data-stu-id="2b42b-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections to your CDN profile when delivering content to your clients.</span></span> <span data-ttu-id="2b42b-107">Isso permite o monitoramento contínuo da integridade do serviço a qualquer momento, incluindo eventos de ativação.</span><span class="sxs-lookup"><span data-stu-id="2b42b-107">This enables continuous monitoring of the health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="2b42b-108">Os gráficos a seguir estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="2b42b-108">The following graphs are available:</span></span>

* [<span data-ttu-id="2b42b-109">Largura de banda</span><span class="sxs-lookup"><span data-stu-id="2b42b-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="2b42b-110">Códigos de status</span><span class="sxs-lookup"><span data-stu-id="2b42b-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="2b42b-111">Status do Cache</span><span class="sxs-lookup"><span data-stu-id="2b42b-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="2b42b-112">Conexões</span><span class="sxs-lookup"><span data-stu-id="2b42b-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="2b42b-113">Acessando as estatísticas em tempo real</span><span class="sxs-lookup"><span data-stu-id="2b42b-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="2b42b-114">No [Portal do Azure](https://portal.azure.com), navegue para seu perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="2b42b-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Folha Perfil CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="2b42b-116">Na folha do perfil CDN, clique no botão **Gerenciar** .</span><span class="sxs-lookup"><span data-stu-id="2b42b-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="2b42b-118">O portal de gerenciamento da CDN é aberto.</span><span class="sxs-lookup"><span data-stu-id="2b42b-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="2b42b-119">Passe o mouse sobre a guia **Análise**, em seguida, sobre o submenu **statísticas em Tempo Real**.</span><span class="sxs-lookup"><span data-stu-id="2b42b-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="2b42b-120">Clique em **Objeto grande de HTTP**.</span><span class="sxs-lookup"><span data-stu-id="2b42b-120">Click on **HTTP Large Object**.</span></span>
   
    ![Portal de gerenciamento da CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="2b42b-122">Os gráficos de estatísticas em tempo real são exibidos.</span><span class="sxs-lookup"><span data-stu-id="2b42b-122">The real-time stats graphs are displayed.</span></span>

<span data-ttu-id="2b42b-123">Cada um dos gráficos exibe estatísticas em tempo real para o período de tempo selecionado, iniciando quando a página carrega.</span><span class="sxs-lookup"><span data-stu-id="2b42b-123">Each of the graphs displays real-time statistics for the selected time span, starting when the page loads.</span></span>  <span data-ttu-id="2b42b-124">Os gráficos são atualizados automaticamente em alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="2b42b-124">The graphs update automatically every few seconds.</span></span>  <span data-ttu-id="2b42b-125">O botão **Atualizar Gráfico** , se presente, limpará o gráfico, depois exibirá apenas os dados selecionados.</span><span class="sxs-lookup"><span data-stu-id="2b42b-125">The **Refresh Graph** button, if present, will clear the graph, after which it will only display the selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="2b42b-126">Largura de banda</span><span class="sxs-lookup"><span data-stu-id="2b42b-126">Bandwidth</span></span>
![Gráfico da largura de banda](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="2b42b-128">O gráfico **Largura de Banda** exibe a quantidade de largura de banda usada para a plataforma atual durante um período de tempo selecionado.</span><span class="sxs-lookup"><span data-stu-id="2b42b-128">The **Bandwidth** graph displays the amount of bandwidth used for the current platform over the selected time span.</span></span> <span data-ttu-id="2b42b-129">A parte sombreada do gráfico indica o uso de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="2b42b-129">The shaded portion of the graph indicates bandwidth usage.</span></span> <span data-ttu-id="2b42b-130">A quantidade exata de largura de banda usada atualmente é exibida diretamente abaixo do gráfico de linha.</span><span class="sxs-lookup"><span data-stu-id="2b42b-130">The exact amount of bandwidth currently being used is displayed directly below the line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="2b42b-131">Códigos de status</span><span class="sxs-lookup"><span data-stu-id="2b42b-131">Status Codes</span></span>
![Gráfico do código de status](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="2b42b-133">O gráfico **Códigos de Status** indica com que frequência determinados códigos de resposta HTTP estão ocorrendo no período de tempo selecionado.</span><span class="sxs-lookup"><span data-stu-id="2b42b-133">The **Status Codes** graph indicates how often certain HTTP response codes are occurring over the selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="2b42b-134">Para obter uma descrição de cada opção do código de status HTTP, confira [Códigos de Status HTTP da CDN do Azure](https://msdn.microsoft.com/library/mt759238.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b42b-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="2b42b-135">É exibida uma lista dos códigos de status HTTP diretamente acima do gráfico.</span><span class="sxs-lookup"><span data-stu-id="2b42b-135">A list of HTTP status codes is displayed directly above the graph.</span></span> <span data-ttu-id="2b42b-136">Essa lista indica cada código de status que pode ser incluído no gráfico de linha e o número de ocorrências por segundo para esse código de status.</span><span class="sxs-lookup"><span data-stu-id="2b42b-136">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="2b42b-137">Por padrão, uma linha é exibida para cada um destes códigos de status no gráfico.</span><span class="sxs-lookup"><span data-stu-id="2b42b-137">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="2b42b-138">No entanto, você pode optar por monitorar apenas os códigos de status que têm um significado especial para a sua configuração de CDN.</span><span class="sxs-lookup"><span data-stu-id="2b42b-138">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="2b42b-139">Para fazer isso, verifique os códigos de status desejados, desmarque todas as outras opções e clique em **Atualizar Gráfico**.</span><span class="sxs-lookup"><span data-stu-id="2b42b-139">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="2b42b-140">Você pode ocultar temporariamente os dados registrados para um código de status específico.</span><span class="sxs-lookup"><span data-stu-id="2b42b-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="2b42b-141">Na legenda diretamente abaixo do gráfico, clique no código de status que você deseja ocultar.</span><span class="sxs-lookup"><span data-stu-id="2b42b-141">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="2b42b-142">O código de status será imediatamente ocultado no gráfico.</span><span class="sxs-lookup"><span data-stu-id="2b42b-142">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="2b42b-143">Clicar novamente no código de status fará com que essa opção seja exibida mais uma vez.</span><span class="sxs-lookup"><span data-stu-id="2b42b-143">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="2b42b-144">Status do Cache</span><span class="sxs-lookup"><span data-stu-id="2b42b-144">Cache Statuses</span></span>
![Gráficos dos Status do Cache](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="2b42b-146">O gráfico **Status do Cache** indica com que frequência determinados tipos de status do cache estão ocorrendo no período de tempo selecionado.</span><span class="sxs-lookup"><span data-stu-id="2b42b-146">The **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over the selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="2b42b-147">Para obter uma descrição de cada opção do código de status do cache, consulte [Códigos de Status do Cache da CDN do Azure](https://msdn.microsoft.com/library/mt759237.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b42b-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="2b42b-148">É exibida uma lista dos códigos de status do cache diretamente acima do gráfico.</span><span class="sxs-lookup"><span data-stu-id="2b42b-148">A list of cache status codes is displayed directly above the graph.</span></span> <span data-ttu-id="2b42b-149">Essa lista indica cada código de status que pode ser incluído no gráfico de linha e o número de ocorrências por segundo para esse código de status.</span><span class="sxs-lookup"><span data-stu-id="2b42b-149">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="2b42b-150">Por padrão, uma linha é exibida para cada um destes códigos de status no gráfico.</span><span class="sxs-lookup"><span data-stu-id="2b42b-150">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="2b42b-151">No entanto, você pode optar por monitorar apenas os códigos de status que têm um significado especial para a sua configuração de CDN.</span><span class="sxs-lookup"><span data-stu-id="2b42b-151">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="2b42b-152">Para fazer isso, verifique os códigos de status desejados, desmarque todas as outras opções e clique em **Atualizar Gráfico**.</span><span class="sxs-lookup"><span data-stu-id="2b42b-152">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="2b42b-153">Você pode ocultar temporariamente os dados registrados para um código de status específico.</span><span class="sxs-lookup"><span data-stu-id="2b42b-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="2b42b-154">Na legenda diretamente abaixo do gráfico, clique no código de status que você deseja ocultar.</span><span class="sxs-lookup"><span data-stu-id="2b42b-154">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="2b42b-155">O código de status será imediatamente ocultado no gráfico.</span><span class="sxs-lookup"><span data-stu-id="2b42b-155">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="2b42b-156">Clicar novamente no código de status fará com que essa opção seja exibida mais uma vez.</span><span class="sxs-lookup"><span data-stu-id="2b42b-156">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="2b42b-157">Conexões</span><span class="sxs-lookup"><span data-stu-id="2b42b-157">Connections</span></span>
![Gráfico das Conexões](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="2b42b-159">Esse gráfico indica quantas conexões foram estabelecidas para seus servidores de borda.</span><span class="sxs-lookup"><span data-stu-id="2b42b-159">This graph indicates how many connections have been established to your edge servers.</span></span> <span data-ttu-id="2b42b-160">Cada solicitação de um ativo que passa por nossos resultados da CDN em uma conexão.</span><span class="sxs-lookup"><span data-stu-id="2b42b-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b42b-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b42b-161">Next Steps</span></span>
* <span data-ttu-id="2b42b-162">Receba uma notificação com [Alertas em tempo real no Azure CDN](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="2b42b-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="2b42b-163">Saiba mais com os [relatórios HTTP avançados](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="2b42b-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="2b42b-164">Analisar os [padrões de uso](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="2b42b-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

