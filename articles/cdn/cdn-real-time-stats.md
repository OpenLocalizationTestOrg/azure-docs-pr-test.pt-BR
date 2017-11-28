---
title: "estatísticas de tempo de aaaReal no Azure CDN | Microsoft Docs"
description: "Estatísticas em tempo real fornecem dados em tempo real sobre o desempenho de saudação da CDN do Azure durante a entrega de conteúdo tooyour clientes."
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
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="f60f4-103">Estatísticas em tempo real na CDN do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f60f4-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="f60f4-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f60f4-104">Overview</span></span>
<span data-ttu-id="f60f4-105">Este documento explica as estatísticas em tempo real na CDN do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f60f4-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="f60f4-106">Essa funcionalidade fornece dados em tempo real, como largura de banda, o status de cache e conexões simultâneas tooyour CDN perfil durante a entrega de conteúdo tooyour clientes.</span><span class="sxs-lookup"><span data-stu-id="f60f4-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections tooyour CDN profile when delivering content tooyour clients.</span></span> <span data-ttu-id="f60f4-107">Isso permite o monitoramento contínuo da integridade de saudação do seu serviço a qualquer momento, incluindo eventos de ativação.</span><span class="sxs-lookup"><span data-stu-id="f60f4-107">This enables continuous monitoring of hello health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="f60f4-108">Olá gráficos a seguir está disponível:</span><span class="sxs-lookup"><span data-stu-id="f60f4-108">hello following graphs are available:</span></span>

* [<span data-ttu-id="f60f4-109">Largura de banda</span><span class="sxs-lookup"><span data-stu-id="f60f4-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="f60f4-110">Códigos de status</span><span class="sxs-lookup"><span data-stu-id="f60f4-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="f60f4-111">Status do Cache</span><span class="sxs-lookup"><span data-stu-id="f60f4-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="f60f4-112">Conexões</span><span class="sxs-lookup"><span data-stu-id="f60f4-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="f60f4-113">Acessando as estatísticas em tempo real</span><span class="sxs-lookup"><span data-stu-id="f60f4-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="f60f4-114">Em Olá [Portal do Azure](https://portal.azure.com), procurar tooyour perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="f60f4-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Folha Perfil CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="f60f4-116">Na folha de perfil CDN hello, clique em Olá **gerenciar** botão.</span><span class="sxs-lookup"><span data-stu-id="f60f4-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="f60f4-118">portal de gerenciamento de CDN Olá é aberto.</span><span class="sxs-lookup"><span data-stu-id="f60f4-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="f60f4-119">Passe o mouse sobre Olá **análise** guia, em seguida, passe o mouse sobre Olá **estatísticas em tempo real** flutuante.</span><span class="sxs-lookup"><span data-stu-id="f60f4-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="f60f4-120">Clique em **Objeto grande de HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f60f4-120">Click on **HTTP Large Object**.</span></span>
   
    ![Portal de gerenciamento da CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="f60f4-122">gráficos de estatísticas em tempo real de saudação são exibidos.</span><span class="sxs-lookup"><span data-stu-id="f60f4-122">hello real-time stats graphs are displayed.</span></span>

<span data-ttu-id="f60f4-123">Cada um dos gráficos de saudação exibe estatísticas em tempo real para o período de tempo de saudação selecionado, começando quando Olá página for carregada.</span><span class="sxs-lookup"><span data-stu-id="f60f4-123">Each of hello graphs displays real-time statistics for hello selected time span, starting when hello page loads.</span></span>  <span data-ttu-id="f60f4-124">gráficos de saudação são atualizadas automaticamente em alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="f60f4-124">hello graphs update automatically every few seconds.</span></span>  <span data-ttu-id="f60f4-125">Olá **atualizar gráfico** botão, se presente, limpará gráfico hello, após o qual ele só exibirá dados saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="f60f4-125">hello **Refresh Graph** button, if present, will clear hello graph, after which it will only display hello selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="f60f4-126">Largura de banda</span><span class="sxs-lookup"><span data-stu-id="f60f4-126">Bandwidth</span></span>
![Gráfico da largura de banda](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="f60f4-128">Olá **largura de banda** gráfico exibe a quantidade de saudação de largura de banda usada para a plataforma atual Olá por período de tempo de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="f60f4-128">hello **Bandwidth** graph displays hello amount of bandwidth used for hello current platform over hello selected time span.</span></span> <span data-ttu-id="f60f4-129">a parte sombreada saudação do gráfico de saudação indica o uso de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="f60f4-129">hello shaded portion of hello graph indicates bandwidth usage.</span></span> <span data-ttu-id="f60f4-130">a quantidade exata Olá de largura de banda está sendo usada no momento é exibida diretamente abaixo de gráfico de linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="f60f4-130">hello exact amount of bandwidth currently being used is displayed directly below hello line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="f60f4-131">Códigos de status</span><span class="sxs-lookup"><span data-stu-id="f60f4-131">Status Codes</span></span>
![Gráfico do código de status](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="f60f4-133">Olá **códigos de Status** gráfico indica quantas vezes determinados códigos de resposta HTTP estão ocorrendo em um período de tempo de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="f60f4-133">hello **Status Codes** graph indicates how often certain HTTP response codes are occurring over hello selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="f60f4-134">Para obter uma descrição de cada opção do código de status HTTP, confira [Códigos de Status HTTP da CDN do Azure](https://msdn.microsoft.com/library/mt759238.aspx).</span><span class="sxs-lookup"><span data-stu-id="f60f4-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="f60f4-135">Uma lista de códigos de status HTTP é exibida diretamente acima gráfico hello.</span><span class="sxs-lookup"><span data-stu-id="f60f4-135">A list of HTTP status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="f60f4-136">Essa lista indica cada código de status que pode ser incluído no gráfico de linha hello e o número atual de saudação de ocorrências por segundo para esse código de status.</span><span class="sxs-lookup"><span data-stu-id="f60f4-136">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="f60f4-137">Por padrão, uma linha é exibida para cada um desses códigos de status no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="f60f4-137">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="f60f4-138">No entanto, você pode escolher tooonly códigos de status de saudação do monitor que têm um significado especial para a sua configuração de CDN.</span><span class="sxs-lookup"><span data-stu-id="f60f4-138">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="f60f4-139">toodo isso, verifique os códigos de status de saudação desejado e desmarque todas as outras opções e clique em **atualizar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="f60f4-139">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="f60f4-140">Você pode ocultar temporariamente os dados registrados para um código de status específico.</span><span class="sxs-lookup"><span data-stu-id="f60f4-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="f60f4-141">De legenda Olá diretamente abaixo gráfico hello, clique em código de status de saudação deseja toohide.</span><span class="sxs-lookup"><span data-stu-id="f60f4-141">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="f60f4-142">código de status de saudação ficará oculta imediatamente do gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="f60f4-142">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="f60f4-143">Clicando novamente o código de status que fará com que esse toobe opção exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="f60f4-143">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="f60f4-144">Status do Cache</span><span class="sxs-lookup"><span data-stu-id="f60f4-144">Cache Statuses</span></span>
![Gráficos dos Status do Cache](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="f60f4-146">Olá **Cache status** gráfico indica quantas vezes determinados tipos de status do cache estão ocorrendo por período de tempo de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="f60f4-146">hello **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over hello selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="f60f4-147">Para obter uma descrição de cada opção do código de status do cache, consulte [Códigos de Status do Cache da CDN do Azure](https://msdn.microsoft.com/library/mt759237.aspx).</span><span class="sxs-lookup"><span data-stu-id="f60f4-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="f60f4-148">Uma lista de códigos de status do cache é exibida diretamente acima gráfico hello.</span><span class="sxs-lookup"><span data-stu-id="f60f4-148">A list of cache status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="f60f4-149">Essa lista indica cada código de status que pode ser incluído no gráfico de linha hello e o número atual de saudação de ocorrências por segundo para esse código de status.</span><span class="sxs-lookup"><span data-stu-id="f60f4-149">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="f60f4-150">Por padrão, uma linha é exibida para cada um desses códigos de status no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="f60f4-150">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="f60f4-151">No entanto, você pode escolher tooonly códigos de status de saudação do monitor que têm um significado especial para a sua configuração de CDN.</span><span class="sxs-lookup"><span data-stu-id="f60f4-151">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="f60f4-152">toodo isso, verifique os códigos de status de saudação desejado e desmarque todas as outras opções e clique em **atualizar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="f60f4-152">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="f60f4-153">Você pode ocultar temporariamente os dados registrados para um código de status específico.</span><span class="sxs-lookup"><span data-stu-id="f60f4-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="f60f4-154">De legenda Olá diretamente abaixo gráfico hello, clique em código de status de saudação deseja toohide.</span><span class="sxs-lookup"><span data-stu-id="f60f4-154">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="f60f4-155">código de status de saudação ficará oculta imediatamente do gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="f60f4-155">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="f60f4-156">Clicando novamente o código de status que fará com que esse toobe opção exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="f60f4-156">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="f60f4-157">Conexões</span><span class="sxs-lookup"><span data-stu-id="f60f4-157">Connections</span></span>
![Gráfico das Conexões](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="f60f4-159">Esse gráfico indica quantas conexões foram estabelecidas tooyour os servidores de borda.</span><span class="sxs-lookup"><span data-stu-id="f60f4-159">This graph indicates how many connections have been established tooyour edge servers.</span></span> <span data-ttu-id="f60f4-160">Cada solicitação de um ativo que passa por nossos resultados da CDN em uma conexão.</span><span class="sxs-lookup"><span data-stu-id="f60f4-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f60f4-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f60f4-161">Next Steps</span></span>
* <span data-ttu-id="f60f4-162">Receba uma notificação com [Alertas em tempo real no Azure CDN](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="f60f4-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="f60f4-163">Saiba mais com os [relatórios HTTP avançados](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="f60f4-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="f60f4-164">Analisar os [padrões de uso](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="f60f4-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

