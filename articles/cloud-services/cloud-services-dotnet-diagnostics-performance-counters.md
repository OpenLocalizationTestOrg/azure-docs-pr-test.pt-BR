---
title: "Usar Contadores de Desempenho no Diagnóstico do Azure | Microsoft Docs"
description: "Use contadores de desempenho em serviços de nuvem ou máquinas virtuais do Azure para localizar afunilamentos e ajustar o desempenho."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: 2cf765cb034725199127c547a9b8b997a4a6089c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="fc276-103">Criar e usar contadores de desempenho em um aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="fc276-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="fc276-104">Este artigo descreve os benefícios de e como colocar os contadores de desempenho no seu aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-104">This article describes the benefits of and how to put performance counters into your Azure application.</span></span> <span data-ttu-id="fc276-105">Você pode usá-los para coletar dados, encontrar afunilamentos e ajustar o desempenho do sistema e do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fc276-105">You can use them to collect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="fc276-106">Os contadores de desempenho disponíveis para o Windows Server, o IIS e o ASP.NET podem ser coletados e usados para determinar a integridade das suas funções Web, funções de trabalho e Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used to determine the health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="fc276-107">Você também pode criar e usar contadores de desempenho personalizados.</span><span class="sxs-lookup"><span data-stu-id="fc276-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="fc276-108">É possível examinar os dados do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="fc276-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="fc276-109">Diretamente no host do aplicativo com a ferramenta Monitor de Desempenho acessada usando a Área de Trabalho Remota</span><span class="sxs-lookup"><span data-stu-id="fc276-109">Directly on the application host with the Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="fc276-110">Com o System Center Operations Manager, usando o Pacote de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="fc276-110">With System Center Operations Manager using the Azure Management Pack</span></span>
3. <span data-ttu-id="fc276-111">Com outras ferramentas de monitoramento que acessam os dados de diagnóstico transferidos para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-111">With other monitoring tools that access the diagnostic data transferred to Azure storage.</span></span> <span data-ttu-id="fc276-112">Consulte [Armazenar e exibir dados de diagnóstico no armazenamento do Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="fc276-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="fc276-113">Para saber mais sobre como monitorar o desempenho do seu aplicativo no [Portal do Azure](http://portal.azure.com/), consulte [Como Monitorar os Serviços de Nuvem](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="fc276-113">For more information on monitoring the performance of your application in the [Azure portal](http://portal.azure.com/), see [How to Monitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="fc276-114">Para obter orientações detalhadas adicionais sobre como criar uma estratégia de registro em log e rastreamento, e usar diagnóstico e outras técnicas para solucionar problemas e otimizar os aplicativos do Azure, consulte [Práticas recomendadas para a solução de problemas no desenvolvimento de aplicativos do Azure](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc276-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques to troubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="fc276-115">Habilitar o monitoramento do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="fc276-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="fc276-116">Os contadores de desempenho não estão habilitados por padrão.</span><span class="sxs-lookup"><span data-stu-id="fc276-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="fc276-117">O aplicativo ou uma tarefa de inicialização devem modificar a configuração padrão do agente de diagnóstico para incluir contadores de desempenho específicos que você deseja monitorar a cada instância de função.</span><span class="sxs-lookup"><span data-stu-id="fc276-117">Your application or a startup task must modify the default diagnostics agent configuration to include the specific performance counters that you wish to monitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="fc276-118">Contadores de desempenho disponíveis para o Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="fc276-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="fc276-119">O Azure fornece um subconjunto de contadores de desempenho disponíveis para o Windows Server, o IIS e a pilha ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fc276-119">Azure provides a subset of the performance counters available for Windows Server, IIS and the ASP.NET stack.</span></span> <span data-ttu-id="fc276-120">A tabela a seguir lista alguns dos contadores de desempenho relevantes para aplicativos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-120">The following table lists some of the performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="fc276-121">Categoria do contador: Objeto (instância)</span><span class="sxs-lookup"><span data-stu-id="fc276-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="fc276-122">Nome do contador</span><span class="sxs-lookup"><span data-stu-id="fc276-122">Counter Name</span></span> | <span data-ttu-id="fc276-123">Referência</span><span class="sxs-lookup"><span data-stu-id="fc276-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc276-124">Exceções CLR do .NET (*Globais*)</span><span class="sxs-lookup"><span data-stu-id="fc276-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="fc276-125">Nº de Exceções Geradas/s</span><span class="sxs-lookup"><span data-stu-id="fc276-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="fc276-126">Contadores de Desempenho de Exceção</span><span class="sxs-lookup"><span data-stu-id="fc276-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="fc276-127">Memória CLR do .NET (*Global*)</span><span class="sxs-lookup"><span data-stu-id="fc276-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="fc276-128">% de Tempo na GC</span><span class="sxs-lookup"><span data-stu-id="fc276-128">% Time in GC</span></span> |<span data-ttu-id="fc276-129">Contadores de Desempenho de Memória</span><span class="sxs-lookup"><span data-stu-id="fc276-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="fc276-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-130">ASP.NET</span></span> |<span data-ttu-id="fc276-131">Reinicializações de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="fc276-131">Application Restarts</span></span> |<span data-ttu-id="fc276-132">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fc276-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-133">ASP.NET</span></span> |<span data-ttu-id="fc276-134">Tempo de Execução de Solicitação</span><span class="sxs-lookup"><span data-stu-id="fc276-134">Request Execution Time</span></span> |<span data-ttu-id="fc276-135">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fc276-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-136">ASP.NET</span></span> |<span data-ttu-id="fc276-137">Solicitações Desconectadas</span><span class="sxs-lookup"><span data-stu-id="fc276-137">Requests Disconnected</span></span> |<span data-ttu-id="fc276-138">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fc276-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-139">ASP.NET</span></span> |<span data-ttu-id="fc276-140">Reinicializações do processo de trabalho</span><span class="sxs-lookup"><span data-stu-id="fc276-140">Worker Process Restarts</span></span> |<span data-ttu-id="fc276-141">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fc276-142">Aplicativos ASP.NET (**Total**)</span><span class="sxs-lookup"><span data-stu-id="fc276-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="fc276-143">Total de Solicitações</span><span class="sxs-lookup"><span data-stu-id="fc276-143">Requests Total</span></span> |<span data-ttu-id="fc276-144">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fc276-145">Aplicativos ASP.NET (**Total**)</span><span class="sxs-lookup"><span data-stu-id="fc276-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="fc276-146">Solicitações/s</span><span class="sxs-lookup"><span data-stu-id="fc276-146">Requests/Sec</span></span> |<span data-ttu-id="fc276-147">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fc276-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="fc276-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="fc276-149">Tempo de Execução de Solicitação</span><span class="sxs-lookup"><span data-stu-id="fc276-149">Request Execution Time</span></span> |<span data-ttu-id="fc276-150">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fc276-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="fc276-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="fc276-152">Tempo de Espera da Solicitação</span><span class="sxs-lookup"><span data-stu-id="fc276-152">Request Wait Time</span></span> |<span data-ttu-id="fc276-153">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fc276-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="fc276-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="fc276-155">Solicitações Atuais</span><span class="sxs-lookup"><span data-stu-id="fc276-155">Requests Current</span></span> |<span data-ttu-id="fc276-156">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fc276-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="fc276-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="fc276-158">Solicitações Enfileiradas</span><span class="sxs-lookup"><span data-stu-id="fc276-158">Requests Queued</span></span> |<span data-ttu-id="fc276-159">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fc276-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="fc276-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="fc276-161">Solicitações Rejeitadas</span><span class="sxs-lookup"><span data-stu-id="fc276-161">Requests Rejected</span></span> |<span data-ttu-id="fc276-162">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fc276-163">Memória</span><span class="sxs-lookup"><span data-stu-id="fc276-163">Memory</span></span> |<span data-ttu-id="fc276-164">MBytes Disponíveis</span><span class="sxs-lookup"><span data-stu-id="fc276-164">Available MBytes</span></span> |<span data-ttu-id="fc276-165">Contadores de Desempenho de Memória</span><span class="sxs-lookup"><span data-stu-id="fc276-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="fc276-166">Memória</span><span class="sxs-lookup"><span data-stu-id="fc276-166">Memory</span></span> |<span data-ttu-id="fc276-167">Bytes Confirmados</span><span class="sxs-lookup"><span data-stu-id="fc276-167">Committed Bytes</span></span> |<span data-ttu-id="fc276-168">Contadores de Desempenho de Memória</span><span class="sxs-lookup"><span data-stu-id="fc276-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="fc276-169">Processador(_Total)</span><span class="sxs-lookup"><span data-stu-id="fc276-169">Processor(_Total)</span></span> |<span data-ttu-id="fc276-170">% Tempo do Processador</span><span class="sxs-lookup"><span data-stu-id="fc276-170">% Processor Time</span></span> |<span data-ttu-id="fc276-171">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc276-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="fc276-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="fc276-172">TCPv4</span></span> |<span data-ttu-id="fc276-173">Falhas de Conexão</span><span class="sxs-lookup"><span data-stu-id="fc276-173">Connection Failures</span></span> |<span data-ttu-id="fc276-174">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="fc276-174">TCP Object</span></span> |
| <span data-ttu-id="fc276-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="fc276-175">TCPv4</span></span> |<span data-ttu-id="fc276-176">Conexões Estabelecidas</span><span class="sxs-lookup"><span data-stu-id="fc276-176">Connections Established</span></span> |<span data-ttu-id="fc276-177">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="fc276-177">TCP Object</span></span> |
| <span data-ttu-id="fc276-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="fc276-178">TCPv4</span></span> |<span data-ttu-id="fc276-179">Conexões Redefinidas</span><span class="sxs-lookup"><span data-stu-id="fc276-179">Connections Reset</span></span> |<span data-ttu-id="fc276-180">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="fc276-180">TCP Object</span></span> |
| <span data-ttu-id="fc276-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="fc276-181">TCPv4</span></span> |<span data-ttu-id="fc276-182">Segmentos Enviados/s</span><span class="sxs-lookup"><span data-stu-id="fc276-182">Segments Sent/sec</span></span> |<span data-ttu-id="fc276-183">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="fc276-183">TCP Object</span></span> |
| <span data-ttu-id="fc276-184">Interface de Rede(*)</span><span class="sxs-lookup"><span data-stu-id="fc276-184">Network Interface(*)</span></span> |<span data-ttu-id="fc276-185">Bytes Recebidos/s</span><span class="sxs-lookup"><span data-stu-id="fc276-185">Bytes Received/sec</span></span> |<span data-ttu-id="fc276-186">Objeto da Interface de Rede</span><span class="sxs-lookup"><span data-stu-id="fc276-186">Network Interface Object</span></span> |
| <span data-ttu-id="fc276-187">Interface de Rede(*)</span><span class="sxs-lookup"><span data-stu-id="fc276-187">Network Interface(*)</span></span> |<span data-ttu-id="fc276-188">Bytes Enviados/s</span><span class="sxs-lookup"><span data-stu-id="fc276-188">Bytes Sent/sec</span></span> |<span data-ttu-id="fc276-189">Objeto da Interface de Rede</span><span class="sxs-lookup"><span data-stu-id="fc276-189">Network Interface Object</span></span> |
| <span data-ttu-id="fc276-190">Interface de Rede (Adaptador de Rede do Barramento da Máquina Virtual da Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="fc276-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="fc276-191">Bytes Recebidos/s</span><span class="sxs-lookup"><span data-stu-id="fc276-191">Bytes Received/sec</span></span> |<span data-ttu-id="fc276-192">Objeto da Interface de Rede</span><span class="sxs-lookup"><span data-stu-id="fc276-192">Network Interface Object</span></span> |
| <span data-ttu-id="fc276-193">Interface de Rede (Adaptador de Rede do Barramento da Máquina Virtual da Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="fc276-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="fc276-194">Bytes Enviados/s</span><span class="sxs-lookup"><span data-stu-id="fc276-194">Bytes Sent/sec</span></span> |<span data-ttu-id="fc276-195">Objeto da Interface de Rede</span><span class="sxs-lookup"><span data-stu-id="fc276-195">Network Interface Object</span></span> |
| <span data-ttu-id="fc276-196">Interface de Rede (Adaptador de Rede do Barramento da Máquina Virtual da Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="fc276-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="fc276-197">Bytes Totais/s</span><span class="sxs-lookup"><span data-stu-id="fc276-197">Bytes Total/sec</span></span> |<span data-ttu-id="fc276-198">Objeto da Interface de Rede</span><span class="sxs-lookup"><span data-stu-id="fc276-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-to-your-application"></a><span data-ttu-id="fc276-199">Criar e adicionar contadores de desempenho personalizados ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="fc276-199">Create and add custom performance counters to your application</span></span>
<span data-ttu-id="fc276-200">O Azure dá suporte à criação e modificação de contadores de desempenho personalizados para funções Web e funções de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fc276-200">Azure has support to create and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="fc276-201">Os contadores podem ser usados para controlar e monitorar o comportamento específico do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fc276-201">The counters may be used to track and monitor application-specific behavior.</span></span> <span data-ttu-id="fc276-202">Você pode criar e excluir categorias de contador de desempenho personalizados e especificadores de uma tarefa de inicialização, função Web ou função de trabalho com permissões elevadas.</span><span class="sxs-lookup"><span data-stu-id="fc276-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="fc276-203">O código que faz alterações aos contadores de desempenho personalizados deve ter permissões elevadas para ser executado.</span><span class="sxs-lookup"><span data-stu-id="fc276-203">Code that makes changes to custom performance counters must have elevated permissions to run.</span></span> <span data-ttu-id="fc276-204">Se o código estiver em uma função Web ou função de trabalho, a função deverá incluir a marca <Runtime executionContext="elevated" /> no arquivo ServiceDefinition.csdef para a função ser inicializada corretamente.</span><span class="sxs-lookup"><span data-stu-id="fc276-204">If the code is in a web role or worker role, the role must include the tag <Runtime executionContext="elevated" /> in the ServiceDefinition.csdef file for the role to initialize properly.</span></span>
>
>

<span data-ttu-id="fc276-205">Você pode enviar dados personalizados de contador de desempenho para o armazenamento do Azure usando o agente de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="fc276-205">You can send custom performance counter data to Azure storage using the diagnostics agent.</span></span>

<span data-ttu-id="fc276-206">Os dados padrão do contador de desempenho são gerados pelos processos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-206">The standard performance counter data is generated by the Azure processes.</span></span> <span data-ttu-id="fc276-207">Os dados personalizados de contador de desempenho devem ser criados pela sua função de trabalho ou aplicativo Web de função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fc276-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="fc276-208">Consulte [Tipos de contador de desempenho](https://msdn.microsoft.com/library/z573042h.aspx) para obter informações sobre os tipos de dados que podem ser armazenados em contadores de desempenho personalizados.</span><span class="sxs-lookup"><span data-stu-id="fc276-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on the types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="fc276-209">Consulte [Exemplo de PerformanceCounters](http://code.msdn.microsoft.com/azure/) para ver um exemplo que cria e define os dados do contador de desempenho personalizados em uma função Web.</span><span class="sxs-lookup"><span data-stu-id="fc276-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="fc276-210">Armazenar e exibir dados do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="fc276-210">Store and view performance counter data</span></span>
<span data-ttu-id="fc276-211">O Azure armazena em cache os dados do contador de desempenho com outras informações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="fc276-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="fc276-212">Esses dados estão disponíveis para o monitoramento remoto enquanto a instância de função está em execução usando o acesso de área de trabalho remoto para exibir ferramentas como o Monitor de Desempenho.</span><span class="sxs-lookup"><span data-stu-id="fc276-212">This data is available for remote monitoring while the role instance is running using remote desktop access to view tools such as Performance Monitor.</span></span> <span data-ttu-id="fc276-213">Para manter os dados fora da instância de função, o agente de diagnóstico deve transferir os dados para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-213">To persist the data outside of the role instance, the diagnostics agent must transfer the data to Azure storage.</span></span> <span data-ttu-id="fc276-214">O limite de tamanho dos dados de contador de desempenho em cache pode ser configurado no agente de diagnóstico, ou pode ser configurado para ser parte de um limite compartilhado para todos os dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="fc276-214">The size limit of the cached performance counter data can be configured in the diagnostics agent, or it may be configured to be part of a shared limit for all the diagnostic data.</span></span> <span data-ttu-id="fc276-215">Para obter mais informações sobre como definir o tamanho do buffer, consulte [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) e [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc276-215">For more information about setting the buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="fc276-216">Consulte [Armazenar e exibir dados de diagnóstico no armazenamento do Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para obter uma visão geral de como configurar o agente de diagnóstico para transferir dados para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fc276-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up the diagnostics agent to transfer data to a storage account.</span></span>

<span data-ttu-id="fc276-217">Cada instância do contador de desempenho configurado é registrada em uma taxa de amostragem especificada e os dados de amostrados são transferidos para a conta de armazenamento por uma solicitação de transferência agendada ou uma solicitação de transferência sob demanda.</span><span class="sxs-lookup"><span data-stu-id="fc276-217">Each configured performance counter instance is recorded at a specified sampling rate, and the sampled data is transferred to the storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="fc276-218">As transferências automáticas podem ser agendadas com uma frequência de até uma vez por minuto.</span><span class="sxs-lookup"><span data-stu-id="fc276-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="fc276-219">Os dados do contador de desempenho transferidos pelo agente de diagnóstico são armazenados em uma tabela, WADPerformanceCountersTable, na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fc276-219">Performance counter data transferred by the diagnostics agent is stored in a table, WADPerformanceCountersTable, in the storage account.</span></span> <span data-ttu-id="fc276-220">Essa tabela pode ser acessada e consultada com métodos padrão da API do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="fc276-221">Consulte [Exemplo de PerformanceCounters do Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) para obter um exemplo de como consultar e exibir dados de contador de desempenho da tabela WADPerformanceCountersTable.</span><span class="sxs-lookup"><span data-stu-id="fc276-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from the WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="fc276-222">Dependendo da frequência de transferência do agente de diagnóstico e da latência da fila, os dados mais recentes do contador de desempenho na conta de armazenamento podem estar desatualizados em vários minutos.</span><span class="sxs-lookup"><span data-stu-id="fc276-222">Depending on the diagnostics agent transfer frequency and queue latency, the most recent performance counter data in the storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="fc276-223">Habilitar os contadores de desempenho usando o arquivo de configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="fc276-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="fc276-224">Use o procedimento a seguir para habilitar os contadores de desempenho em seu aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-224">Use the following procedure to enable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc276-225">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fc276-225">Prerequisites</span></span>
<span data-ttu-id="fc276-226">Este artigo pressupõe que você tenha importado o monitor de diagnóstico para seu aplicativo e adicionado o arquivo de configuração à sua solução do Visual Studio (diagnostics.wadcfg no SDK 2.4 e inferior ou diagnostics.wadcfgx no SDK 2.5 e superior).</span><span class="sxs-lookup"><span data-stu-id="fc276-226">This section assumes that you have imported the Diagnostics monitor into your application and added the diagnostics configuration file to your Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="fc276-227">Consulte as etapas 1 e 2 em [Habilitando o Diagnóstico nos Serviços de Nuvem do Azure e Máquinas Virtuais](cloud-services-dotnet-diagnostics.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="fc276-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="fc276-228">Etapa 1: Coletar e armazenar dados de contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="fc276-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="fc276-229">Depois de ter adicionado o arquivo de diagnóstico à solução do Visual Studio, você pode configurar a coleta e o armazenamento de dados do contador de desempenho em um aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-229">After you have added the diagnostics file to your Visual Studio solution, you can configure the collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="fc276-230">Isso é feito adicionando contadores de desempenho ao arquivo de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="fc276-230">This is done by adding performance counters to the diagnostics file.</span></span> <span data-ttu-id="fc276-231">Os dados de diagnóstico, incluindo os contadores de desempenho são primeiro coletados na instância.</span><span class="sxs-lookup"><span data-stu-id="fc276-231">Diagnostics data, including performance counters, is first collected on the instance.</span></span> <span data-ttu-id="fc276-232">Os dados são persistidos na tabela WADPerformanceCountersTable no serviço Tabela do Azure, portanto, você também precisa especificar a conta de armazenamento em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fc276-232">The data is then persisted to the WADPerformanceCountersTable table in the Azure Table service, so you will also need to specify the storage account in your application.</span></span> <span data-ttu-id="fc276-233">Se estiver testando o aplicativo localmente no Emulador de Computação, você também poderá armazenar dados de diagnóstico localmente no Emulador de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fc276-233">If you're testing your application locally in the Compute Emulator, you can also store diagnostics data locally in the Storage Emulator.</span></span> <span data-ttu-id="fc276-234">Antes de armazenar dados de diagnóstico, você deve primeiro ir para o [Portal do Azure](http://portal.azure.com/) e criar uma conta de armazenamento clássica.</span><span class="sxs-lookup"><span data-stu-id="fc276-234">Before you store diagnostics data, you must first go to the [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="fc276-235">Uma prática recomendada é localizar a conta de armazenamento na mesma localização geográfica que seu aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-235">A best practice is to locate your storage account in the same geo-location as your Azure application.</span></span> <span data-ttu-id="fc276-236">Ao manter o aplicativo do Azure e a conta de armazenamento na mesma localização geográfica, você evita custos externos de largura de banda e reduz a latência.</span><span class="sxs-lookup"><span data-stu-id="fc276-236">By keeping the Azure application and storage account are in the same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-to-the-diagnostics-file"></a><span data-ttu-id="fc276-237">Adicionar contadores de desempenho ao arquivo de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="fc276-237">Add performance counters to the diagnostics file</span></span>
<span data-ttu-id="fc276-238">Há muitos contadores que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="fc276-238">There are many counters you can use.</span></span> <span data-ttu-id="fc276-239">O exemplo a seguir mostra vários contadores de desempenho que são recomendados para monitoramento de funções Web e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fc276-239">The following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="fc276-240">Abra o arquivo de diagnóstico (diagnostics.wadcfg no SDK 2.4 e inferior ou diagnostics.wadcfgx no SDK 2.5 e posterior) e adicione o seguinte ao elemento DiagnosticMonitorConfiguration:</span><span class="sxs-lookup"><span data-stu-id="fc276-240">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use the Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use the Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

<span data-ttu-id="fc276-241">O atributo bufferQuotaInMB, que especifica a quantidade máxima de armazenamento do sistema de arquivos que está disponível para o tipo de coleta de dados (logs do Azure, logs do IIS etc.).</span><span class="sxs-lookup"><span data-stu-id="fc276-241">The bufferQuotaInMB attribute, which specifies the maximum amount of file system storage that is available for the data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="fc276-242">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="fc276-242">The default is 0.</span></span> <span data-ttu-id="fc276-243">Quando a cota é atingida, os dados mais antigos são excluídos enquanto novos dados são adicionados.</span><span class="sxs-lookup"><span data-stu-id="fc276-243">When the quota is reached, the oldest data is deleted as new data is added.</span></span> <span data-ttu-id="fc276-244">A soma de todas as propriedades de bufferQuotaInMB deve ser maior que o valor do atributo OverallQuotaInMB.</span><span class="sxs-lookup"><span data-stu-id="fc276-244">The sum of all the bufferQuotaInMB properties must be greater than the value of the OverallQuotaInMB attribute.</span></span> <span data-ttu-id="fc276-245">Para obter uma discussão mais detalhada sobre como determinar quanto armazenamento será necessário para a coleta de dados de diagnóstico, consulte a seção Configurar WAD de [Solução de problemas de práticas recomendadas para o desenvolvimento de aplicativos do Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc276-245">For a more detailed discussion of determining how much storage will be required for the collection of diagnostics data, see the Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="fc276-246">O atributo scheduledTransferPeriod que especifica o intervalo entre transferências agendadas de dados, arredondado para o minuto mais próximo.</span><span class="sxs-lookup"><span data-stu-id="fc276-246">The scheduledTransferPeriod attribute, which specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span> <span data-ttu-id="fc276-247">Nos exemplos a seguir ele é definido como PT30M (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="fc276-247">In the following examples, it is set to PT30M (30 minutes).</span></span> <span data-ttu-id="fc276-248">A definição do período de transferência para um valor pequeno, como 1 minuto, afetará negativamente o desempenho de seu aplicativo na produção, mas pode ser útil para ver o diagnóstico funcionar rapidamente quando você estiver testando.</span><span class="sxs-lookup"><span data-stu-id="fc276-248">Setting the transfer period to a small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="fc276-249">O período de transferência agendada deve ser pequeno o suficiente para garantir que os dados de diagnóstico não sejam substituídos na instância, mas grande o suficiente para que não afete o desempenho de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fc276-249">The scheduled transfer period should be small enough to ensure that diagnostic data is not overwritten on the instance, but large enough that it will not impact the performance of your application.</span></span>

<span data-ttu-id="fc276-250">O atributo counterSpecifier especifica o contador de desempenho para coleta.</span><span class="sxs-lookup"><span data-stu-id="fc276-250">The counterSpecifier attribute specifies the performance counter to collect.</span></span> <span data-ttu-id="fc276-251">O atributo sampleRate especifica a taxa em que o contador de desempenho deve ser amostrado, neste caso, 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="fc276-251">The sampleRate attribute specifies the rate at which the performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="fc276-252">Depois de adicionar os contadores de desempenho que deseja coletar, salve as alterações no arquivo de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="fc276-252">Once you've added the performance counters that you want to collect, save your changes to the diagnostics file.</span></span> <span data-ttu-id="fc276-253">Em seguida, você precisa especificar a conta de armazenamento na qual os dados de diagnóstico serão persistidos.</span><span class="sxs-lookup"><span data-stu-id="fc276-253">Next, you need to specify the storage account that the diagnostics data will be persisted to.</span></span>

### <a name="specify-the-storage-account"></a><span data-ttu-id="fc276-254">Especificar a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="fc276-254">Specify the storage account</span></span>
<span data-ttu-id="fc276-255">Para persistir as informações de diagnóstico em sua conta de Armazenamento do Azure, você deve especificar uma cadeia de conexão no arquivo de configuração do serviço (ServiceConfiguration.csfg).</span><span class="sxs-lookup"><span data-stu-id="fc276-255">To persist your diagnostics information to your Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="fc276-256">No SDK do Azure 2.5, a Conta de Armazenamento pode ser especificada no arquivo diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="fc276-256">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="fc276-257">Essas instruções se aplicam somente ao SDK 2.4 do Azure e inferior.</span><span class="sxs-lookup"><span data-stu-id="fc276-257">These instructions only apply to Azure SDK 2.4 and below.</span></span> <span data-ttu-id="fc276-258">No SDK do Azure 2.5, a Conta de Armazenamento pode ser especificada no arquivo diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="fc276-258">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="fc276-259">Para definir as cadeias de conexão:</span><span class="sxs-lookup"><span data-stu-id="fc276-259">To set the connection strings:</span></span>

1. <span data-ttu-id="fc276-260">Abra o arquivo ServiceConfiguration.Cloud.cscfg usando o seu editor de texto preferido e defina a cadeia de conexão da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fc276-260">Open the ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set the connection string for your storage.</span></span> <span data-ttu-id="fc276-261">Os valores *AccountName* e *AccountKey* são encontrados no Portal do Azure, no painel da conta de armazenamento, em Chaves de acesso.</span><span class="sxs-lookup"><span data-stu-id="fc276-261">The *AccountName* and *AccountKey* values are found in the Azure portal in the storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="fc276-262">Salve o arquivo ServiceConfiguration.Cloud.cscfg.</span><span class="sxs-lookup"><span data-stu-id="fc276-262">Save the ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="fc276-263">Abra o arquivo ServiceConfiguration.Local.cscfg e verifique se UseDevelopmentStorage está definido como verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="fc276-263">Open the ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set to true.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="fc276-264">Agora que as cadeias de conexão estão definidas, seu aplicativo irá persistir dados de diagnóstico em sua conta de armazenamento quando o aplicativo for implantado.</span><span class="sxs-lookup"><span data-stu-id="fc276-264">Now that the connection strings are set, your application will persist diagnostics data to your storage account when your application is deployed.</span></span>
4. <span data-ttu-id="fc276-265">Salve e compile seu projeto e implante seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fc276-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="fc276-266">Etapa 2: (Opcional) Criar contadores de desempenho personalizados</span><span class="sxs-lookup"><span data-stu-id="fc276-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="fc276-267">Além dos contadores de desempenho predefinidos, você pode adicionar seus próprios contadores de desempenho personalizados para monitorar as funções Web ou de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fc276-267">In addition to the pre-defined performance counters, you can add your own custom performance counters to monitor web or worker roles.</span></span> <span data-ttu-id="fc276-268">Os contadores de desempenho personalizados podem ser usados para acompanhar e monitorar o comportamento específico do aplicativo e podem ser criados ou excluídos em tarefas de inicialização, função Web ou função de trabalho com permissões elevadas.</span><span class="sxs-lookup"><span data-stu-id="fc276-268">Custom performance counters may be used to track and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="fc276-269">O agente de diagnóstico do Azure atualiza a configuração do contador de desempenho do arquivo .wadcfg um minuto após o início.</span><span class="sxs-lookup"><span data-stu-id="fc276-269">The Azure diagnostics agent refreshes the performance counter configuration from the .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="fc276-270">Se você criar contadores de desempenho personalizados no método OnStart e suas tarefas de inicialização demorarem mais de um minuto para serem executadas, os seus contadores de desempenho personalizados não terão sido criados quando o agente de diagnóstico do Azure tentar carregá-los.</span><span class="sxs-lookup"><span data-stu-id="fc276-270">If you create custom performance counters in the OnStart method and your startup tasks take longer than one minute to execute, your custom performance counters will not have been created when the Azure Diagnostics agent tries to load them.</span></span>  <span data-ttu-id="fc276-271">Nesse cenário, você verá que o diagnóstico do Azure captura corretamente todos os dados de diagnóstico exceto os seus contadores de desempenho personalizados.</span><span class="sxs-lookup"><span data-stu-id="fc276-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="fc276-272">Para resolver esse problema, crie os contadores de desempenho em uma tarefa de inicialização ou mova alguns trabalhos da sua tarefa de inicialização para o método OnStart depois de criar os contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="fc276-272">To resolve this issue, create the performance counters in a startup task or move some of your startup task work to the OnStart method after creating the performance counters.</span></span>

<span data-ttu-id="fc276-273">Execute as seguintes etapas para criar um contador de desempenho personalizado simples chamado "\MyCustomCounterCategory\MyButton1Counter":</span><span class="sxs-lookup"><span data-stu-id="fc276-273">Perform the following steps to create a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="fc276-274">Abra o arquivo de definição do serviço (CSDEF) de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fc276-274">Open the service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="fc276-275">Adicione o elemento Runtime ao elemento WebRole ou WorkerRole para permitir a execução com privilégios elevados:</span><span class="sxs-lookup"><span data-stu-id="fc276-275">Add the Runtime element to the WebRole or WorkerRole element to allow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="fc276-276">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="fc276-276">Save the file.</span></span>
4. <span data-ttu-id="fc276-277">Abra o arquivo de diagnóstico (diagnostics.wadcfg no SDK 2.4 e inferior ou diagnostics.wadcfgx no SDK 2.5 e posterior) e adicione o seguinte ao elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="fc276-277">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="fc276-278">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="fc276-278">Save the file.</span></span>
6. <span data-ttu-id="fc276-279">Crie a categoria do contador de desempenho personalizado no método OnStart de sua função, antes de invocar base.OnStart.</span><span class="sxs-lookup"><span data-stu-id="fc276-279">Create the custom performance counter category in the OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="fc276-280">O exemplo de C# a seguir criará uma nova categoria personalizada, caso ela ainda não exista:</span><span class="sxs-lookup"><span data-stu-id="fc276-280">The following C# example creates a custom category, if it does not already exist:</span></span>

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. <span data-ttu-id="fc276-281">Atualize os contadores dentro de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fc276-281">Update the counters within your application.</span></span> <span data-ttu-id="fc276-282">O exemplo a seguir atualiza um contador de desempenho personalizado em eventos Button1_Click:</span><span class="sxs-lookup"><span data-stu-id="fc276-282">The following example updates a custom performance counter on Button1_Click events:</span></span>

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. <span data-ttu-id="fc276-283">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="fc276-283">Save the file.</span></span>  

<span data-ttu-id="fc276-284">Os dados personalizados do contador de desempenho agora serão coletados pelo monitor de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="fc276-284">Custom performance counter data will now be collected by the Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="fc276-285">Etapa 3: Consultar dados do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="fc276-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="fc276-286">Depois que o aplicativo for implantado e estiver em execução, o monitor de diagnóstico começará a coletar contadores de desempenho e a persistir esses dados no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc276-286">Once your application is deployed and running, the Diagnostics monitor will begin collecting performance counters and persisting that data to Azure storage.</span></span> <span data-ttu-id="fc276-287">Use ferramentas, como o Gerenciador de Servidores no Visual Studio, [Gerenciador de Armazenamento do Azure](http://azurestorageexplorer.codeplex.com/) ou [Gerenciador de Diagnóstico do Azure ](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx), da Cerebrata para exibir os contadores de desempenho dados na tabela WADPerformanceCountersTable.</span><span class="sxs-lookup"><span data-stu-id="fc276-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata to view the performance counters data in the WADPerformanceCountersTable table.</span></span> <span data-ttu-id="fc276-288">Você pode consultar também programaticamente o serviço Tabela usando o [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md) ou [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="fc276-288">You can also programmatically query the Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="fc276-289">O seguinte exemplo de C# mostra uma consulta básica na tabela WADPerformanceCountersTable e salva os dados de diagnóstico em um arquivo CSV.</span><span class="sxs-lookup"><span data-stu-id="fc276-289">The following C# example shows a basic query against the WADPerformanceCountersTable table and saves the diagnostics data to a CSV file.</span></span> <span data-ttu-id="fc276-290">Depois que os contadores de desempenho forem salvos em um arquivo CSV, você poderá usar os recursos gráficos do Microsoft Excel ou alguma outra ferramenta para visualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="fc276-290">Once the performance counters are saved to a CSV file, you can use the graphing capabilities in Microsoft Excel or some other tool to visualize the data.</span></span> <span data-ttu-id="fc276-291">Certifique-se de adicionar uma referência ao Microsoft.WindowsAzure.Storage.dll, que está incluído no SDK do Azure para .NET de outubro 2012 e posterior.</span><span class="sxs-lookup"><span data-stu-id="fc276-291">Be sure to add a reference to Microsoft.WindowsAzure.Storage.dll, which is included in the Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="fc276-292">O assembly é instalado no diretório %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span><span class="sxs-lookup"><span data-stu-id="fc276-292">The assembly is installed to the %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get the connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using the Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use the CloudConfigurationManager type
// to retrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store the connection string in your web.config or app.config file.
// Use the ConfigurationManager type to retrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference to the storage account using the connection string.  You can also use the development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create the table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute the table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process the query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

<span data-ttu-id="fc276-293">As entidades mapeiam para objetos C# usando uma classe personalizada derivada de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="fc276-293">Entities map to C# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="fc276-294">O código a seguir define uma classe de entidade que representa um contador de desempenho na tabela **WADPerformanceCountersTable** .</span><span class="sxs-lookup"><span data-stu-id="fc276-294">The following code defines an entity class that represents a performance counter in the **WADPerformanceCountersTable** table.</span></span>

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="fc276-295">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fc276-295">Next Steps</span></span>
[<span data-ttu-id="fc276-296">Exibir artigos adicionais sobre o Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="fc276-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
