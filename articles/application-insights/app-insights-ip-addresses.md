---
title: "Endereços IP usados pelo Application Insights | Microsoft Docs"
description: "Exceções de firewall de servidor exigidas pelo Application Insights"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 8/11/2017
ms.author: bwren
ms.openlocfilehash: 3bb076c63223fc1567c6b7b25c1a513bbc81ed58
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="6da93-103">Endereços IP usados pelo Application Insights</span><span class="sxs-lookup"><span data-stu-id="6da93-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="6da93-104">O serviço [Azure Application Insights](app-insights-overview.md) usa vários endereços IP.</span><span class="sxs-lookup"><span data-stu-id="6da93-104">The [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="6da93-105">Talvez seja necessário conhecer esses endereços se o aplicativo que você está monitorando estiver hospedado atrás de um firewall.</span><span class="sxs-lookup"><span data-stu-id="6da93-105">You might need to know these addresses if the app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="6da93-106">Embora esses endereços sejam estáticos, é possível que seja necessário alterá-los de tempos em tempos.</span><span class="sxs-lookup"><span data-stu-id="6da93-106">Although these addresses are static, it's possible that we will need to change them from time to time.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="6da93-107">Portas de saída</span><span class="sxs-lookup"><span data-stu-id="6da93-107">Outgoing ports</span></span>
<span data-ttu-id="6da93-108">Você precisa abrir algumas portas de saída no firewall do servidor para permitir que o SDK do Application Insights e/ou o Monitor de Status envie dados para o portal:</span><span class="sxs-lookup"><span data-stu-id="6da93-108">You need to open some outgoing ports in your server's firewall to allow the Application Insights SDK and/or Status Monitor to send data to the portal:</span></span>

| <span data-ttu-id="6da93-109">Finalidade</span><span class="sxs-lookup"><span data-stu-id="6da93-109">Purpose</span></span> | <span data-ttu-id="6da93-110">URL</span><span class="sxs-lookup"><span data-stu-id="6da93-110">URL</span></span> | <span data-ttu-id="6da93-111">IP</span><span class="sxs-lookup"><span data-stu-id="6da93-111">IP</span></span> | <span data-ttu-id="6da93-112">Portas</span><span class="sxs-lookup"><span data-stu-id="6da93-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6da93-113">Telemetria</span><span class="sxs-lookup"><span data-stu-id="6da93-113">Telemetry</span></span> |<span data-ttu-id="6da93-114">dc.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="6da93-115">dc.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6da93-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="6da93-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="6da93-116">40.114.241.141</span></span><br/><span data-ttu-id="6da93-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="6da93-117">104.45.136.42</span></span><br/><span data-ttu-id="6da93-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="6da93-118">40.84.189.107</span></span><br/><span data-ttu-id="6da93-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="6da93-119">168.63.242.221</span></span><br/><span data-ttu-id="6da93-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="6da93-120">52.167.221.184</span></span><br/><span data-ttu-id="6da93-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="6da93-121">52.169.64.244</span></span> |<span data-ttu-id="6da93-122">443</span><span class="sxs-lookup"><span data-stu-id="6da93-122">443</span></span> |
| <span data-ttu-id="6da93-123">Live Metrics Stream</span><span class="sxs-lookup"><span data-stu-id="6da93-123">Live Metrics Stream</span></span> |<span data-ttu-id="6da93-124">rt.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="6da93-125">rt.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6da93-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="6da93-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="6da93-126">23.96.28.38</span></span><br/><span data-ttu-id="6da93-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="6da93-127">13.92.40.198</span></span> |<span data-ttu-id="6da93-128">443</span><span class="sxs-lookup"><span data-stu-id="6da93-128">443</span></span> |
| <span data-ttu-id="6da93-129">Telemetria interna</span><span class="sxs-lookup"><span data-stu-id="6da93-129">Internal Telemetry</span></span> |<span data-ttu-id="6da93-130">breeze.aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6da93-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="6da93-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="6da93-131">52.161.11.71</span></span> |<span data-ttu-id="6da93-132">443</span><span class="sxs-lookup"><span data-stu-id="6da93-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="6da93-133">Monitor de status</span><span class="sxs-lookup"><span data-stu-id="6da93-133">Status Monitor</span></span>
<span data-ttu-id="6da93-134">Configuração do Monitor de Status - necessária somente ao fazer alterações.</span><span class="sxs-lookup"><span data-stu-id="6da93-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="6da93-135">Finalidade</span><span class="sxs-lookup"><span data-stu-id="6da93-135">Purpose</span></span> | <span data-ttu-id="6da93-136">URL</span><span class="sxs-lookup"><span data-stu-id="6da93-136">URL</span></span> | <span data-ttu-id="6da93-137">IP</span><span class="sxs-lookup"><span data-stu-id="6da93-137">IP</span></span> | <span data-ttu-id="6da93-138">Portas</span><span class="sxs-lookup"><span data-stu-id="6da93-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6da93-139">Configuração</span><span class="sxs-lookup"><span data-stu-id="6da93-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="6da93-140">Configuração</span><span class="sxs-lookup"><span data-stu-id="6da93-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="6da93-141">Configuração</span><span class="sxs-lookup"><span data-stu-id="6da93-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="6da93-142">Configuração</span><span class="sxs-lookup"><span data-stu-id="6da93-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="6da93-143">Configuração</span><span class="sxs-lookup"><span data-stu-id="6da93-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="6da93-144">Configuração</span><span class="sxs-lookup"><span data-stu-id="6da93-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="6da93-145">Configuração</span><span class="sxs-lookup"><span data-stu-id="6da93-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="6da93-146">Instalação</span><span class="sxs-lookup"><span data-stu-id="6da93-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="6da93-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="6da93-147">HockeyApp</span></span>
| <span data-ttu-id="6da93-148">Finalidade</span><span class="sxs-lookup"><span data-stu-id="6da93-148">Purpose</span></span> | <span data-ttu-id="6da93-149">URL</span><span class="sxs-lookup"><span data-stu-id="6da93-149">URL</span></span> | <span data-ttu-id="6da93-150">IP</span><span class="sxs-lookup"><span data-stu-id="6da93-150">IP</span></span> | <span data-ttu-id="6da93-151">Portas</span><span class="sxs-lookup"><span data-stu-id="6da93-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6da93-152">Dados de falha</span><span class="sxs-lookup"><span data-stu-id="6da93-152">Crash data</span></span> |<span data-ttu-id="6da93-153">gate.hockeyapp.net</span><span class="sxs-lookup"><span data-stu-id="6da93-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="6da93-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="6da93-154">104.45.136.42</span></span> |<span data-ttu-id="6da93-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="6da93-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="6da93-156">Testes de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="6da93-156">Availability tests</span></span>
<span data-ttu-id="6da93-157">Esta é a lista de endereços a partir dos quais [testes da web de disponibilidade](app-insights-monitor-web-app-availability.md) são executados.</span><span class="sxs-lookup"><span data-stu-id="6da93-157">This is the list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="6da93-158">Se você deseja executar testes da Web em seu aplicativo, mas o servidor Web está restrito a servir clientes específicos, você precisa permitir o tráfego de entrada dos nossos servidores de teste de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="6da93-158">If you want to run web tests on your app, but your web server is restricted to serving specific clients, then you will have to permit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="6da93-159">Abra as portas 80 (http) e 443 (https) para o tráfego de entrada destes endereços (endereços IP são agrupados por local):</span><span class="sxs-lookup"><span data-stu-id="6da93-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a><span data-ttu-id="6da93-160">API de acesso a dados</span><span class="sxs-lookup"><span data-stu-id="6da93-160">Data access API</span></span>
| <span data-ttu-id="6da93-161">Finalidade</span><span class="sxs-lookup"><span data-stu-id="6da93-161">Purpose</span></span> | <span data-ttu-id="6da93-162">URI</span><span class="sxs-lookup"><span data-stu-id="6da93-162">URI</span></span> | <span data-ttu-id="6da93-163">IP</span><span class="sxs-lookup"><span data-stu-id="6da93-163">IP</span></span> | <span data-ttu-id="6da93-164">Portas</span><span class="sxs-lookup"><span data-stu-id="6da93-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6da93-165">API</span><span class="sxs-lookup"><span data-stu-id="6da93-165">API</span></span> |<span data-ttu-id="6da93-166">api.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6da93-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="6da93-167">api1.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6da93-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="6da93-168">api2.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6da93-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="6da93-169">api3.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6da93-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="6da93-170">api4.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6da93-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="6da93-171">api5.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6da93-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="6da93-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="6da93-172">13.82.26.252</span></span><br/><span data-ttu-id="6da93-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="6da93-173">40.76.213.73</span></span> |<span data-ttu-id="6da93-174">80.443</span><span class="sxs-lookup"><span data-stu-id="6da93-174">80,443</span></span> |
| <span data-ttu-id="6da93-175">documentos da API</span><span class="sxs-lookup"><span data-stu-id="6da93-175">API docs</span></span> |<span data-ttu-id="6da93-176">dev.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6da93-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="6da93-177">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6da93-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="6da93-178">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6da93-179">www.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6da93-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="6da93-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6da93-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="6da93-181">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="6da93-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="6da93-182">13.82.24.149</span></span><br/><span data-ttu-id="6da93-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="6da93-183">40.114.82.10</span></span> |<span data-ttu-id="6da93-184">80.443</span><span class="sxs-lookup"><span data-stu-id="6da93-184">80,443</span></span> |
| <span data-ttu-id="6da93-185">API Interna</span><span class="sxs-lookup"><span data-stu-id="6da93-185">Internal API</span></span> |<span data-ttu-id="6da93-186">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6da93-187">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6da93-188">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6da93-189">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6da93-190">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6da93-191">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6da93-192">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="6da93-193">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-193">dynamic</span></span>|<span data-ttu-id="6da93-194">443</span><span class="sxs-lookup"><span data-stu-id="6da93-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="6da93-195">Análise do Application Insights</span><span class="sxs-lookup"><span data-stu-id="6da93-195">Application Insights Analytics</span></span>

| <span data-ttu-id="6da93-196">Finalidade</span><span class="sxs-lookup"><span data-stu-id="6da93-196">Purpose</span></span> | <span data-ttu-id="6da93-197">URI</span><span class="sxs-lookup"><span data-stu-id="6da93-197">URI</span></span> | <span data-ttu-id="6da93-198">IP</span><span class="sxs-lookup"><span data-stu-id="6da93-198">IP</span></span> | <span data-ttu-id="6da93-199">Portas</span><span class="sxs-lookup"><span data-stu-id="6da93-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6da93-200">Portal da análise</span><span class="sxs-lookup"><span data-stu-id="6da93-200">Analytics Portal</span></span> | <span data-ttu-id="6da93-201">analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6da93-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="6da93-202">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-202">dynamic</span></span> | <span data-ttu-id="6da93-203">80.443</span><span class="sxs-lookup"><span data-stu-id="6da93-203">80,443</span></span> |
| <span data-ttu-id="6da93-204">CDN</span><span class="sxs-lookup"><span data-stu-id="6da93-204">CDN</span></span> | <span data-ttu-id="6da93-205">applicationanalytics.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="6da93-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="6da93-206">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-206">dynamic</span></span> | <span data-ttu-id="6da93-207">80.443</span><span class="sxs-lookup"><span data-stu-id="6da93-207">80,443</span></span> |
| <span data-ttu-id="6da93-208">Mídia CDN</span><span class="sxs-lookup"><span data-stu-id="6da93-208">Media CDN</span></span> | <span data-ttu-id="6da93-209">applicationanalyticsmedia.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="6da93-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="6da93-210">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-210">dynamic</span></span> | <span data-ttu-id="6da93-211">80.443</span><span class="sxs-lookup"><span data-stu-id="6da93-211">80,443</span></span> |

<span data-ttu-id="6da93-212">Observação: o domínio *.applicationinsights.io pertence à equipe do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6da93-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="6da93-213">Extensão do Portal do Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="6da93-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="6da93-214">Finalidade</span><span class="sxs-lookup"><span data-stu-id="6da93-214">Purpose</span></span> | <span data-ttu-id="6da93-215">URI</span><span class="sxs-lookup"><span data-stu-id="6da93-215">URI</span></span> | <span data-ttu-id="6da93-216">IP</span><span class="sxs-lookup"><span data-stu-id="6da93-216">IP</span></span> | <span data-ttu-id="6da93-217">Portas</span><span class="sxs-lookup"><span data-stu-id="6da93-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6da93-218">Extensão do Application Insights</span><span class="sxs-lookup"><span data-stu-id="6da93-218">Application Insights Extension</span></span> | <span data-ttu-id="6da93-219">stamp2.app.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="6da93-220">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-220">dynamic</span></span> | <span data-ttu-id="6da93-221">80.443</span><span class="sxs-lookup"><span data-stu-id="6da93-221">80,443</span></span> |
| <span data-ttu-id="6da93-222">Extensão do Application Insights CDN</span><span class="sxs-lookup"><span data-stu-id="6da93-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="6da93-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6da93-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="6da93-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="6da93-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="6da93-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="6da93-226">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-226">dynamic</span></span> | <span data-ttu-id="6da93-227">80.443</span><span class="sxs-lookup"><span data-stu-id="6da93-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="6da93-228">SDKs do Application Insights</span><span class="sxs-lookup"><span data-stu-id="6da93-228">Application Insights SDKs</span></span>

| <span data-ttu-id="6da93-229">Finalidade</span><span class="sxs-lookup"><span data-stu-id="6da93-229">Purpose</span></span> | <span data-ttu-id="6da93-230">URI</span><span class="sxs-lookup"><span data-stu-id="6da93-230">URI</span></span> | <span data-ttu-id="6da93-231">IP</span><span class="sxs-lookup"><span data-stu-id="6da93-231">IP</span></span> | <span data-ttu-id="6da93-232">Portas</span><span class="sxs-lookup"><span data-stu-id="6da93-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6da93-233">SDK do Application Insights JS CDN</span><span class="sxs-lookup"><span data-stu-id="6da93-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="6da93-234">az416426.vo.msecnd.net</span><span class="sxs-lookup"><span data-stu-id="6da93-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="6da93-235">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-235">dynamic</span></span> | <span data-ttu-id="6da93-236">80.443</span><span class="sxs-lookup"><span data-stu-id="6da93-236">80,443</span></span> |
| <span data-ttu-id="6da93-237">Application Insights Java SDK</span><span class="sxs-lookup"><span data-stu-id="6da93-237">Application Insights Java SDK</span></span> | <span data-ttu-id="6da93-238">aijavasdk.blob.Core.Windows.net</span><span class="sxs-lookup"><span data-stu-id="6da93-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="6da93-239">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-239">dynamic</span></span> | <span data-ttu-id="6da93-240">80.443</span><span class="sxs-lookup"><span data-stu-id="6da93-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="6da93-241">Criador de perfil</span><span class="sxs-lookup"><span data-stu-id="6da93-241">Profiler</span></span>

| <span data-ttu-id="6da93-242">Finalidade</span><span class="sxs-lookup"><span data-stu-id="6da93-242">Purpose</span></span> | <span data-ttu-id="6da93-243">URI</span><span class="sxs-lookup"><span data-stu-id="6da93-243">URI</span></span> | <span data-ttu-id="6da93-244">IP</span><span class="sxs-lookup"><span data-stu-id="6da93-244">IP</span></span> | <span data-ttu-id="6da93-245">Portas</span><span class="sxs-lookup"><span data-stu-id="6da93-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6da93-246">Agente</span><span class="sxs-lookup"><span data-stu-id="6da93-246">Agent</span></span> | <span data-ttu-id="6da93-247">agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="6da93-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="6da93-248">*.agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="6da93-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="6da93-249">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-249">dynamic</span></span> | <span data-ttu-id="6da93-250">443</span><span class="sxs-lookup"><span data-stu-id="6da93-250">443</span></span>
| <span data-ttu-id="6da93-251">Portal</span><span class="sxs-lookup"><span data-stu-id="6da93-251">Portal</span></span> | <span data-ttu-id="6da93-252">gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="6da93-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="6da93-253">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-253">dynamic</span></span> | <span data-ttu-id="6da93-254">443</span><span class="sxs-lookup"><span data-stu-id="6da93-254">443</span></span>
| <span data-ttu-id="6da93-255">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="6da93-255">Storage</span></span> | <span data-ttu-id="6da93-256">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="6da93-256">*.core.windows.net</span></span> | <span data-ttu-id="6da93-257">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-257">dynamic</span></span> | <span data-ttu-id="6da93-258">443</span><span class="sxs-lookup"><span data-stu-id="6da93-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="6da93-259">Depurador de instantâneo</span><span class="sxs-lookup"><span data-stu-id="6da93-259">Snapshot Debugger</span></span>

| <span data-ttu-id="6da93-260">Finalidade</span><span class="sxs-lookup"><span data-stu-id="6da93-260">Purpose</span></span> | <span data-ttu-id="6da93-261">URI</span><span class="sxs-lookup"><span data-stu-id="6da93-261">URI</span></span> | <span data-ttu-id="6da93-262">IP</span><span class="sxs-lookup"><span data-stu-id="6da93-262">IP</span></span> | <span data-ttu-id="6da93-263">Portas</span><span class="sxs-lookup"><span data-stu-id="6da93-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6da93-264">Agente</span><span class="sxs-lookup"><span data-stu-id="6da93-264">Agent</span></span> | <span data-ttu-id="6da93-265">ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="6da93-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="6da93-266">*.ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="6da93-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="6da93-267">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-267">dynamic</span></span> | <span data-ttu-id="6da93-268">443</span><span class="sxs-lookup"><span data-stu-id="6da93-268">443</span></span>
| <span data-ttu-id="6da93-269">Portal</span><span class="sxs-lookup"><span data-stu-id="6da93-269">Portal</span></span> | <span data-ttu-id="6da93-270">ppe.gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="6da93-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="6da93-271">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-271">dynamic</span></span> | <span data-ttu-id="6da93-272">443</span><span class="sxs-lookup"><span data-stu-id="6da93-272">443</span></span>
| <span data-ttu-id="6da93-273">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="6da93-273">Storage</span></span> | <span data-ttu-id="6da93-274">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="6da93-274">*.core.windows.net</span></span> | <span data-ttu-id="6da93-275">dinâmico</span><span class="sxs-lookup"><span data-stu-id="6da93-275">dynamic</span></span> | <span data-ttu-id="6da93-276">443</span><span class="sxs-lookup"><span data-stu-id="6da93-276">443</span></span>
