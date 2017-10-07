---
title: "aaaUse contadores de desempenho no diagnóstico do Azure | Microsoft Docs"
description: "Use os contadores de desempenho em serviços de nuvem do Azure ou máquina virtual toofind afunilamentos e ajustar o desempenho."
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
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="844a0-103">Criar e usar contadores de desempenho em um aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="844a0-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="844a0-104">Este artigo descreve os benefícios de saudação do e como os contadores de desempenho de tooput em seu aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="844a0-104">This article describes hello benefits of and how tooput performance counters into your Azure application.</span></span> <span data-ttu-id="844a0-105">Você pode usá-los toocollect dados, detectar gargalos de e ajustar o desempenho do sistema e do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="844a0-105">You can use them toocollect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="844a0-106">Contadores de desempenho disponíveis para o Windows Server, IIS e ASP.NET também podem ser coletados e usados toodetermine integridade de saudação de suas funções web do Azure, funções de trabalho e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="844a0-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used toodetermine hello health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="844a0-107">Você também pode criar e usar contadores de desempenho personalizados.</span><span class="sxs-lookup"><span data-stu-id="844a0-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="844a0-108">É possível examinar os dados do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="844a0-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="844a0-109">Diretamente no host de aplicativo hello com a ferramenta de Monitor de desempenho Olá acessada usando a área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="844a0-109">Directly on hello application host with hello Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="844a0-110">Com o System Center Operations Manager usando Olá o pacote de gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="844a0-110">With System Center Operations Manager using hello Azure Management Pack</span></span>
3. <span data-ttu-id="844a0-111">Com outras ferramentas de monitoramentos que acessam Olá dados de diagnóstico transferidos tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="844a0-111">With other monitoring tools that access hello diagnostic data transferred tooAzure storage.</span></span> <span data-ttu-id="844a0-112">Consulte [Armazenar e exibir dados de diagnóstico no armazenamento do Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="844a0-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="844a0-113">Para obter mais informações sobre como monitorar o desempenho de saudação do seu aplicativo em Olá [portal do Azure](http://portal.azure.com/), consulte [como serviços em nuvem tooMonitor](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="844a0-113">For more information on monitoring hello performance of your application in hello [Azure portal](http://portal.azure.com/), see [How tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="844a0-114">Para obter orientação detalhada adicional sobre como criar um registro em log e rastreamento estratégia e uso de diagnóstico e outros problemas de tootroubleshoot técnicas e otimizar aplicativos do Azure, consulte [práticas recomendadas de solução de problemas para desenvolver o Azure Aplicativos](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="844a0-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques tootroubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="844a0-115">Habilitar o monitoramento do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="844a0-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="844a0-116">Os contadores de desempenho não estão habilitados por padrão.</span><span class="sxs-lookup"><span data-stu-id="844a0-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="844a0-117">O aplicativo ou uma tarefa de inicialização deve modificar o diagnóstico de padrão de saudação contadores de desempenho de específicos de saudação do agente configuração tooinclude que você deseja toomonitor para cada instância de função.</span><span class="sxs-lookup"><span data-stu-id="844a0-117">Your application or a startup task must modify hello default diagnostics agent configuration tooinclude hello specific performance counters that you wish toomonitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="844a0-118">Contadores de desempenho disponíveis para o Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="844a0-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="844a0-119">Azure fornece um subconjunto de contadores de desempenho de saudação disponíveis para Windows Server, IIS e Olá pilha do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="844a0-119">Azure provides a subset of hello performance counters available for Windows Server, IIS and hello ASP.NET stack.</span></span> <span data-ttu-id="844a0-120">Olá tabela a seguir lista alguns dos contadores de desempenho de saudação de interesse específico para aplicativos do Azure.</span><span class="sxs-lookup"><span data-stu-id="844a0-120">hello following table lists some of hello performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="844a0-121">Categoria do contador: Objeto (instância)</span><span class="sxs-lookup"><span data-stu-id="844a0-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="844a0-122">Nome do contador</span><span class="sxs-lookup"><span data-stu-id="844a0-122">Counter Name</span></span> | <span data-ttu-id="844a0-123">Referência</span><span class="sxs-lookup"><span data-stu-id="844a0-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="844a0-124">Exceções CLR do .NET (*Globais*)</span><span class="sxs-lookup"><span data-stu-id="844a0-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="844a0-125">Nº de Exceções Geradas/s</span><span class="sxs-lookup"><span data-stu-id="844a0-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="844a0-126">Contadores de Desempenho de Exceção</span><span class="sxs-lookup"><span data-stu-id="844a0-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="844a0-127">Memória CLR do .NET (*Global*)</span><span class="sxs-lookup"><span data-stu-id="844a0-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="844a0-128">% de Tempo na GC</span><span class="sxs-lookup"><span data-stu-id="844a0-128">% Time in GC</span></span> |<span data-ttu-id="844a0-129">Contadores de Desempenho de Memória</span><span class="sxs-lookup"><span data-stu-id="844a0-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="844a0-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-130">ASP.NET</span></span> |<span data-ttu-id="844a0-131">Reinicializações de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="844a0-131">Application Restarts</span></span> |<span data-ttu-id="844a0-132">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="844a0-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-133">ASP.NET</span></span> |<span data-ttu-id="844a0-134">Tempo de Execução de Solicitação</span><span class="sxs-lookup"><span data-stu-id="844a0-134">Request Execution Time</span></span> |<span data-ttu-id="844a0-135">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="844a0-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-136">ASP.NET</span></span> |<span data-ttu-id="844a0-137">Solicitações Desconectadas</span><span class="sxs-lookup"><span data-stu-id="844a0-137">Requests Disconnected</span></span> |<span data-ttu-id="844a0-138">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="844a0-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-139">ASP.NET</span></span> |<span data-ttu-id="844a0-140">Reinicializações do processo de trabalho</span><span class="sxs-lookup"><span data-stu-id="844a0-140">Worker Process Restarts</span></span> |<span data-ttu-id="844a0-141">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="844a0-142">Aplicativos ASP.NET (**Total**)</span><span class="sxs-lookup"><span data-stu-id="844a0-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="844a0-143">Total de Solicitações</span><span class="sxs-lookup"><span data-stu-id="844a0-143">Requests Total</span></span> |<span data-ttu-id="844a0-144">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="844a0-145">Aplicativos ASP.NET (**Total**)</span><span class="sxs-lookup"><span data-stu-id="844a0-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="844a0-146">Solicitações/s</span><span class="sxs-lookup"><span data-stu-id="844a0-146">Requests/Sec</span></span> |<span data-ttu-id="844a0-147">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="844a0-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="844a0-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="844a0-149">Tempo de Execução de Solicitação</span><span class="sxs-lookup"><span data-stu-id="844a0-149">Request Execution Time</span></span> |<span data-ttu-id="844a0-150">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="844a0-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="844a0-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="844a0-152">Tempo de Espera da Solicitação</span><span class="sxs-lookup"><span data-stu-id="844a0-152">Request Wait Time</span></span> |<span data-ttu-id="844a0-153">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="844a0-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="844a0-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="844a0-155">Solicitações Atuais</span><span class="sxs-lookup"><span data-stu-id="844a0-155">Requests Current</span></span> |<span data-ttu-id="844a0-156">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="844a0-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="844a0-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="844a0-158">Solicitações Enfileiradas</span><span class="sxs-lookup"><span data-stu-id="844a0-158">Requests Queued</span></span> |<span data-ttu-id="844a0-159">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="844a0-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="844a0-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="844a0-161">Solicitações Rejeitadas</span><span class="sxs-lookup"><span data-stu-id="844a0-161">Requests Rejected</span></span> |<span data-ttu-id="844a0-162">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="844a0-163">Memória</span><span class="sxs-lookup"><span data-stu-id="844a0-163">Memory</span></span> |<span data-ttu-id="844a0-164">MBytes Disponíveis</span><span class="sxs-lookup"><span data-stu-id="844a0-164">Available MBytes</span></span> |<span data-ttu-id="844a0-165">Contadores de Desempenho de Memória</span><span class="sxs-lookup"><span data-stu-id="844a0-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="844a0-166">Memória</span><span class="sxs-lookup"><span data-stu-id="844a0-166">Memory</span></span> |<span data-ttu-id="844a0-167">Bytes Confirmados</span><span class="sxs-lookup"><span data-stu-id="844a0-167">Committed Bytes</span></span> |<span data-ttu-id="844a0-168">Contadores de Desempenho de Memória</span><span class="sxs-lookup"><span data-stu-id="844a0-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="844a0-169">Processador(_Total)</span><span class="sxs-lookup"><span data-stu-id="844a0-169">Processor(_Total)</span></span> |<span data-ttu-id="844a0-170">% Tempo do Processador</span><span class="sxs-lookup"><span data-stu-id="844a0-170">% Processor Time</span></span> |<span data-ttu-id="844a0-171">Contadores de Desempenho do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="844a0-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="844a0-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="844a0-172">TCPv4</span></span> |<span data-ttu-id="844a0-173">Falhas de Conexão</span><span class="sxs-lookup"><span data-stu-id="844a0-173">Connection Failures</span></span> |<span data-ttu-id="844a0-174">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="844a0-174">TCP Object</span></span> |
| <span data-ttu-id="844a0-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="844a0-175">TCPv4</span></span> |<span data-ttu-id="844a0-176">Conexões Estabelecidas</span><span class="sxs-lookup"><span data-stu-id="844a0-176">Connections Established</span></span> |<span data-ttu-id="844a0-177">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="844a0-177">TCP Object</span></span> |
| <span data-ttu-id="844a0-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="844a0-178">TCPv4</span></span> |<span data-ttu-id="844a0-179">Conexões Redefinidas</span><span class="sxs-lookup"><span data-stu-id="844a0-179">Connections Reset</span></span> |<span data-ttu-id="844a0-180">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="844a0-180">TCP Object</span></span> |
| <span data-ttu-id="844a0-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="844a0-181">TCPv4</span></span> |<span data-ttu-id="844a0-182">Segmentos Enviados/s</span><span class="sxs-lookup"><span data-stu-id="844a0-182">Segments Sent/sec</span></span> |<span data-ttu-id="844a0-183">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="844a0-183">TCP Object</span></span> |
| <span data-ttu-id="844a0-184">Interface de Rede(*)</span><span class="sxs-lookup"><span data-stu-id="844a0-184">Network Interface(*)</span></span> |<span data-ttu-id="844a0-185">Bytes Recebidos/s</span><span class="sxs-lookup"><span data-stu-id="844a0-185">Bytes Received/sec</span></span> |<span data-ttu-id="844a0-186">Objeto da Interface de Rede</span><span class="sxs-lookup"><span data-stu-id="844a0-186">Network Interface Object</span></span> |
| <span data-ttu-id="844a0-187">Interface de Rede(*)</span><span class="sxs-lookup"><span data-stu-id="844a0-187">Network Interface(*)</span></span> |<span data-ttu-id="844a0-188">Bytes Enviados/s</span><span class="sxs-lookup"><span data-stu-id="844a0-188">Bytes Sent/sec</span></span> |<span data-ttu-id="844a0-189">Objeto da Interface de Rede</span><span class="sxs-lookup"><span data-stu-id="844a0-189">Network Interface Object</span></span> |
| <span data-ttu-id="844a0-190">Interface de Rede (Adaptador de Rede do Barramento da Máquina Virtual da Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="844a0-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="844a0-191">Bytes Recebidos/s</span><span class="sxs-lookup"><span data-stu-id="844a0-191">Bytes Received/sec</span></span> |<span data-ttu-id="844a0-192">Objeto da Interface de Rede</span><span class="sxs-lookup"><span data-stu-id="844a0-192">Network Interface Object</span></span> |
| <span data-ttu-id="844a0-193">Interface de Rede (Adaptador de Rede do Barramento da Máquina Virtual da Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="844a0-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="844a0-194">Bytes Enviados/s</span><span class="sxs-lookup"><span data-stu-id="844a0-194">Bytes Sent/sec</span></span> |<span data-ttu-id="844a0-195">Objeto da Interface de Rede</span><span class="sxs-lookup"><span data-stu-id="844a0-195">Network Interface Object</span></span> |
| <span data-ttu-id="844a0-196">Interface de Rede (Adaptador de Rede do Barramento da Máquina Virtual da Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="844a0-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="844a0-197">Bytes Totais/s</span><span class="sxs-lookup"><span data-stu-id="844a0-197">Bytes Total/sec</span></span> |<span data-ttu-id="844a0-198">Objeto da Interface de Rede</span><span class="sxs-lookup"><span data-stu-id="844a0-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a><span data-ttu-id="844a0-199">Criar e adicionar o aplicativo de tooyour de contadores de desempenho personalizados</span><span class="sxs-lookup"><span data-stu-id="844a0-199">Create and add custom performance counters tooyour application</span></span>
<span data-ttu-id="844a0-200">O Azure tem suporte toocreate e modificar os contadores de desempenho personalizados para funções web e funções de trabalho.</span><span class="sxs-lookup"><span data-stu-id="844a0-200">Azure has support toocreate and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="844a0-201">contadores de saudação podem ser usado comportamento de específicas do aplicativo de tootrack e monitor.</span><span class="sxs-lookup"><span data-stu-id="844a0-201">hello counters may be used tootrack and monitor application-specific behavior.</span></span> <span data-ttu-id="844a0-202">Você pode criar e excluir categorias de contador de desempenho personalizados e especificadores de uma tarefa de inicialização, função Web ou função de trabalho com permissões elevadas.</span><span class="sxs-lookup"><span data-stu-id="844a0-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="844a0-203">Código que faz alterações toocustom contadores de desempenho deve ter elevado toorun de permissões.</span><span class="sxs-lookup"><span data-stu-id="844a0-203">Code that makes changes toocustom performance counters must have elevated permissions toorun.</span></span> <span data-ttu-id="844a0-204">Se código Olá estiver em uma função web ou função de trabalho, função hello deve incluir a marca Olá <Runtime executionContext="elevated" /> em Olá servicedefinition. Csdef de arquivos para Olá função tooinitialize corretamente.</span><span class="sxs-lookup"><span data-stu-id="844a0-204">If hello code is in a web role or worker role, hello role must include hello tag <Runtime executionContext="elevated" /> in hello ServiceDefinition.csdef file for hello role tooinitialize properly.</span></span>
>
>

<span data-ttu-id="844a0-205">Você pode enviar o armazenamento de desempenho personalizado contador dados tooAzure usando o agente de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="844a0-205">You can send custom performance counter data tooAzure storage using hello diagnostics agent.</span></span>

<span data-ttu-id="844a0-206">dados do contador de desempenho padrão Olá são gerados pelo hello que Azure processa.</span><span class="sxs-lookup"><span data-stu-id="844a0-206">hello standard performance counter data is generated by hello Azure processes.</span></span> <span data-ttu-id="844a0-207">Os dados personalizados de contador de desempenho devem ser criados pela sua função de trabalho ou aplicativo Web de função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="844a0-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="844a0-208">Consulte [tipos de contador de desempenho](https://msdn.microsoft.com/library/z573042h.aspx) para obter informações sobre tipos de saudação de dados que podem ser armazenados em contadores de desempenho personalizados.</span><span class="sxs-lookup"><span data-stu-id="844a0-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on hello types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="844a0-209">Consulte [Exemplo de PerformanceCounters](http://code.msdn.microsoft.com/azure/) para ver um exemplo que cria e define os dados do contador de desempenho personalizados em uma função Web.</span><span class="sxs-lookup"><span data-stu-id="844a0-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="844a0-210">Armazenar e exibir dados do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="844a0-210">Store and view performance counter data</span></span>
<span data-ttu-id="844a0-211">O Azure armazena em cache os dados do contador de desempenho com outras informações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="844a0-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="844a0-212">Esses dados estão disponíveis para monitoramento remoto enquanto a instância de função hello está em execução usando as ferramentas de tooview de acesso de área de trabalho remota como o Monitor de desempenho.</span><span class="sxs-lookup"><span data-stu-id="844a0-212">This data is available for remote monitoring while hello role instance is running using remote desktop access tooview tools such as Performance Monitor.</span></span> <span data-ttu-id="844a0-213">toopersist Olá fora da instância de função hello, agente de diagnóstico Olá deve transferência de dados de armazenamento de tooAzure Olá dados.</span><span class="sxs-lookup"><span data-stu-id="844a0-213">toopersist hello data outside of hello role instance, hello diagnostics agent must transfer hello data tooAzure storage.</span></span> <span data-ttu-id="844a0-214">limite de tamanho de saudação de saudação em cache dados do contador de desempenho pode ser configurada no agente de diagnóstico hello, ou pode ser configurado toobe parte de um limite compartilhado para todos os dados de diagnóstico de hello.</span><span class="sxs-lookup"><span data-stu-id="844a0-214">hello size limit of hello cached performance counter data can be configured in hello diagnostics agent, or it may be configured toobe part of a shared limit for all hello diagnostic data.</span></span> <span data-ttu-id="844a0-215">Para obter mais informações sobre como definir o tamanho do buffer hello, consulte [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) e [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="844a0-215">For more information about setting hello buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="844a0-216">Consulte [armazenar e exibir dados de diagnóstico no armazenamento do Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para obter uma visão geral de configuração de conta de armazenamento Olá diagnóstico agente tootransfer dados tooa.</span><span class="sxs-lookup"><span data-stu-id="844a0-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up hello diagnostics agent tootransfer data tooa storage account.</span></span>

<span data-ttu-id="844a0-217">Cada instância do contador de desempenho configurado é registrada em uma taxa de amostragem especificada e dados de amostra de saudação for transferidos toohello conta de armazenamento por uma solicitação de transferência agendada ou uma solicitação de transferência sob demanda.</span><span class="sxs-lookup"><span data-stu-id="844a0-217">Each configured performance counter instance is recorded at a specified sampling rate, and hello sampled data is transferred toohello storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="844a0-218">As transferências automáticas podem ser agendadas com uma frequência de até uma vez por minuto.</span><span class="sxs-lookup"><span data-stu-id="844a0-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="844a0-219">Dados de contador de desempenho transferidos pelo agente de diagnóstico de saudação é armazenados em uma tabela, WADPerformanceCountersTable, na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="844a0-219">Performance counter data transferred by hello diagnostics agent is stored in a table, WADPerformanceCountersTable, in hello storage account.</span></span> <span data-ttu-id="844a0-220">Essa tabela pode ser acessada e consultada com métodos padrão da API do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="844a0-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="844a0-221">Consulte [exemplo de PerformanceCounters do Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) para obter um exemplo de como consultar e exibir dados de contador de desempenho da tabela de WADPerformanceCountersTable hello.</span><span class="sxs-lookup"><span data-stu-id="844a0-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from hello WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="844a0-222">Dependendo da frequência de transferência de agente de diagnóstico hello e latência de fila, hello dados mais recentes do contador de desempenho na conta de armazenamento Olá podem estar vários minutos desatualizados.</span><span class="sxs-lookup"><span data-stu-id="844a0-222">Depending on hello diagnostics agent transfer frequency and queue latency, hello most recent performance counter data in hello storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="844a0-223">Habilitar os contadores de desempenho usando o arquivo de configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="844a0-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="844a0-224">Use Olá seguintes contadores de desempenho do procedimento tooenable em seu aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="844a0-224">Use hello following procedure tooenable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="844a0-225">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="844a0-225">Prerequisites</span></span>
<span data-ttu-id="844a0-226">Esta seção pressupõe que você tiver importado o monitor de diagnóstico de saudação para seu aplicativo e adicionado Olá diagnóstico configuração arquivo tooyour Visual Studio solução (wadcfg no SDK 2.4 e abaixo ou wadcfgx no SDK 2.5 e superior).</span><span class="sxs-lookup"><span data-stu-id="844a0-226">This section assumes that you have imported hello Diagnostics monitor into your application and added hello diagnostics configuration file tooyour Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="844a0-227">Consulte as etapas 1 e 2 em [Habilitando o Diagnóstico nos Serviços de Nuvem do Azure e Máquinas Virtuais](cloud-services-dotnet-diagnostics.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="844a0-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="844a0-228">Etapa 1: Coletar e armazenar dados de contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="844a0-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="844a0-229">Depois que você adicionou Olá diagnóstico arquivo tooyour solução do Visual Studio, você pode configurar coleta de saudação e o armazenamento de dados do contador de desempenho em um aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="844a0-229">After you have added hello diagnostics file tooyour Visual Studio solution, you can configure hello collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="844a0-230">Isso é feito adicionando o arquivo de diagnóstico de toohello de contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="844a0-230">This is done by adding performance counters toohello diagnostics file.</span></span> <span data-ttu-id="844a0-231">Dados de diagnóstico, incluindo contadores de desempenho são coletados primeiro na instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="844a0-231">Diagnostics data, including performance counters, is first collected on hello instance.</span></span> <span data-ttu-id="844a0-232">dados de saudação forem persistente toohello WADPerformanceCountersTable tabela Olá serviço tabela do Azure, para que você também precisa toospecify Olá conta de armazenamento em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="844a0-232">hello data is then persisted toohello WADPerformanceCountersTable table in hello Azure Table service, so you will also need toospecify hello storage account in your application.</span></span> <span data-ttu-id="844a0-233">Se você estiver testando seu aplicativo localmente no emulador de computação do hello, você também pode armazenar dados de diagnóstico localmente no emulador de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="844a0-233">If you're testing your application locally in hello Compute Emulator, you can also store diagnostics data locally in hello Storage Emulator.</span></span> <span data-ttu-id="844a0-234">Antes de armazenar dados de diagnóstico, você deverá primeiro ir toohello [portal do Azure](http://portal.azure.com/) e crie uma conta de armazenamento clássicos.</span><span class="sxs-lookup"><span data-stu-id="844a0-234">Before you store diagnostics data, you must first go toohello [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="844a0-235">Uma prática recomendada é toolocate sua conta de armazenamento Olá mesma localização geográfica que seu aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="844a0-235">A best practice is toolocate your storage account in hello same geo-location as your Azure application.</span></span> <span data-ttu-id="844a0-236">Por manter Olá conta de armazenamento e de aplicativo do Azure estão em Olá mesma localização geográfica, evitar pagar custos externos de largura de banda e reduzir a latência.</span><span class="sxs-lookup"><span data-stu-id="844a0-236">By keeping hello Azure application and storage account are in hello same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-toohello-diagnostics-file"></a><span data-ttu-id="844a0-237">Adicionar arquivo de diagnóstico de toohello de contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="844a0-237">Add performance counters toohello diagnostics file</span></span>
<span data-ttu-id="844a0-238">Há muitos contadores que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="844a0-238">There are many counters you can use.</span></span> <span data-ttu-id="844a0-239">Olá, exemplo a seguir mostra vários contadores de desempenho que são recomendados para web e monitoramento de função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="844a0-239">hello following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="844a0-240">Abra o arquivo de diagnóstico hello (wadcfg no SDK 2.4 e anterior ou wadcfgx no SDK 2.5 e superior) e adicione Olá toohello DiagnosticMonitorConfiguration elemento a seguir:</span><span class="sxs-lookup"><span data-stu-id="844a0-240">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
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

<span data-ttu-id="844a0-241">atributo de bufferQuotaInMB Hello, que especifica a quantidade máxima de saudação do armazenamento do sistema de arquivos que está disponível para o tipo de coleção de dados de saudação (logs do Azure, logs do IIS, etc.).</span><span class="sxs-lookup"><span data-stu-id="844a0-241">hello bufferQuotaInMB attribute, which specifies hello maximum amount of file system storage that is available for hello data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="844a0-242">saudação padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="844a0-242">hello default is 0.</span></span> <span data-ttu-id="844a0-243">Quando Olá cota for atingida, dados mais antigos Olá são excluídos como novos dados são adicionados.</span><span class="sxs-lookup"><span data-stu-id="844a0-243">When hello quota is reached, hello oldest data is deleted as new data is added.</span></span> <span data-ttu-id="844a0-244">soma de saudação de todas as propriedades de bufferQuotaInMB Olá deve ser maior que o valor do atributo de OverallQuotaInMB Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="844a0-244">hello sum of all hello bufferQuotaInMB properties must be greater than hello value of hello OverallQuotaInMB attribute.</span></span> <span data-ttu-id="844a0-245">Para obter uma discussão mais detalhada de determinar a quantidade de armazenamento será necessária para a saudação de coleta de dados de diagnóstico, consulte Olá seção Configurar WAD de [práticas recomendadas de solução de problemas para desenvolver aplicativos do Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="844a0-245">For a more detailed discussion of determining how much storage will be required for hello collection of diagnostics data, see hello Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="844a0-246">atributo de scheduledTransferPeriod Hello, que especifica o intervalo de saudação entre transferências agendadas de dados, arredondado toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="844a0-246">hello scheduledTransferPeriod attribute, which specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span> <span data-ttu-id="844a0-247">Olá exemplos a seguir, ele é definido tooPT30M (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="844a0-247">In hello following examples, it is set tooPT30M (30 minutes).</span></span> <span data-ttu-id="844a0-248">Configuração Olá transferência tooa período valor pequeno, como 1 minuto, afetará negativamente o desempenho do seu aplicativo em produção, mas pode ser útil para ver o diagnóstico funcionando rapidamente quando você está testando.</span><span class="sxs-lookup"><span data-stu-id="844a0-248">Setting hello transfer period tooa small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="844a0-249">o período de transferência programado Olá deve ser pequeno o suficiente tooensure que os dados de diagnóstico não são substituídos na instância de hello, mas grande o suficiente para que ele não afetará o desempenho de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="844a0-249">hello scheduled transfer period should be small enough tooensure that diagnostic data is not overwritten on hello instance, but large enough that it will not impact hello performance of your application.</span></span>

<span data-ttu-id="844a0-250">atributo de counterSpecifier Olá Especifica Olá toocollect de contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="844a0-250">hello counterSpecifier attribute specifies hello performance counter toocollect.</span></span> <span data-ttu-id="844a0-251">atributo de sampleRate Olá Especifica a taxa de saudação em que o contador de desempenho Olá deve ser testado, nesse caso 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="844a0-251">hello sampleRate attribute specifies hello rate at which hello performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="844a0-252">Depois de adicionar contadores de desempenho de saudação que você deseja toocollect, salve o arquivo de diagnóstico de toohello de alterações.</span><span class="sxs-lookup"><span data-stu-id="844a0-252">Once you've added hello performance counters that you want toocollect, save your changes toohello diagnostics file.</span></span> <span data-ttu-id="844a0-253">Em seguida, você precisa de conta de armazenamento de Olá toospecify que os dados de diagnóstico hello serão persistidos.</span><span class="sxs-lookup"><span data-stu-id="844a0-253">Next, you need toospecify hello storage account that hello diagnostics data will be persisted to.</span></span>

### <a name="specify-hello-storage-account"></a><span data-ttu-id="844a0-254">Especifique a conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="844a0-254">Specify hello storage account</span></span>
<span data-ttu-id="844a0-255">toopersist conta sua informações de diagnóstico tooyour armazenamento do Azure, você deve especificar uma cadeia de caracteres de conexão no arquivo de configuração (ServiceConfiguration. cscfg) do serviço.</span><span class="sxs-lookup"><span data-stu-id="844a0-255">toopersist your diagnostics information tooyour Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="844a0-256">2.5 do SDK do Azure, Olá conta de armazenamento pode ser especificado no arquivo de wadcfgx hello.</span><span class="sxs-lookup"><span data-stu-id="844a0-256">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="844a0-257">Essas instruções se aplicam somente a tooAzure SDK 2.4 e anterior.</span><span class="sxs-lookup"><span data-stu-id="844a0-257">These instructions only apply tooAzure SDK 2.4 and below.</span></span> <span data-ttu-id="844a0-258">2.5 do SDK do Azure, Olá conta de armazenamento pode ser especificado no arquivo de wadcfgx hello.</span><span class="sxs-lookup"><span data-stu-id="844a0-258">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="844a0-259">cadeias de conexão de saudação tooset:</span><span class="sxs-lookup"><span data-stu-id="844a0-259">tooset hello connection strings:</span></span>

1. <span data-ttu-id="844a0-260">Abra o arquivo de ServiceConfiguration hello usando seu editor de texto favorito e a cadeia de caracteres de conexão do conjunto Olá para seu armazenamento.</span><span class="sxs-lookup"><span data-stu-id="844a0-260">Open hello ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set hello connection string for your storage.</span></span> <span data-ttu-id="844a0-261">Olá *AccountName* e *AccountKey* valores são encontrados na Olá portal do Azure no painel de conta de armazenamento hello, em chaves de acesso.</span><span class="sxs-lookup"><span data-stu-id="844a0-261">hello *AccountName* and *AccountKey* values are found in hello Azure portal in hello storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="844a0-262">Salve o arquivo de ServiceConfiguration hello.</span><span class="sxs-lookup"><span data-stu-id="844a0-262">Save hello ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="844a0-263">Abrir o arquivo de ServiceConfiguration Olá e verificar se UseDevelopmentStorage está definida tootrue.</span><span class="sxs-lookup"><span data-stu-id="844a0-263">Open hello ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set tootrue.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="844a0-264">Agora que as cadeias de caracteres de conexão Olá forem definidas, o aplicativo persistirá conta de armazenamento do tooyour de dados de diagnóstico quando seu aplicativo é implantado.</span><span class="sxs-lookup"><span data-stu-id="844a0-264">Now that hello connection strings are set, your application will persist diagnostics data tooyour storage account when your application is deployed.</span></span>
4. <span data-ttu-id="844a0-265">Salve e compile seu projeto e implante seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="844a0-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="844a0-266">Etapa 2: (Opcional) Criar contadores de desempenho personalizados</span><span class="sxs-lookup"><span data-stu-id="844a0-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="844a0-267">Além disso toohello predefinidas contadores de desempenho, você pode adicionar que sua próprias de desempenho personalizados contadores toomonitor funções de web ou de trabalho.</span><span class="sxs-lookup"><span data-stu-id="844a0-267">In addition toohello pre-defined performance counters, you can add your own custom performance counters toomonitor web or worker roles.</span></span> <span data-ttu-id="844a0-268">Contadores de desempenho personalizados podem ser comportamento usado tootrack e monitor de específicas do aplicativo e pode ser criados ou excluídos em uma tarefa de inicialização, a função web ou a função de trabalho com permissões elevadas.</span><span class="sxs-lookup"><span data-stu-id="844a0-268">Custom performance counters may be used tootrack and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="844a0-269">Agente de diagnóstico do Azure Olá atualiza Olá desempenho configuração do contador do arquivo. wadcfg de saudação um minuto após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="844a0-269">hello Azure diagnostics agent refreshes hello performance counter configuration from hello .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="844a0-270">Se você criar contadores de desempenho personalizados no método OnStart da saudação e suas tarefas de inicialização demorar mais do que um minuto tooexecute, seus contadores de desempenho personalizados não terá sido criadas quando o agente de diagnóstico do Azure Olá tenta tooload-los.</span><span class="sxs-lookup"><span data-stu-id="844a0-270">If you create custom performance counters in hello OnStart method and your startup tasks take longer than one minute tooexecute, your custom performance counters will not have been created when hello Azure Diagnostics agent tries tooload them.</span></span>  <span data-ttu-id="844a0-271">Nesse cenário, você verá que o diagnóstico do Azure captura corretamente todos os dados de diagnóstico exceto os seus contadores de desempenho personalizados.</span><span class="sxs-lookup"><span data-stu-id="844a0-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="844a0-272">tooresolve esse problema, crie Olá contadores de desempenho em uma tarefa de inicialização ou mover alguns dos sua tarefa de inicialização funcionam toohello OnStart método depois de criar hello contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="844a0-272">tooresolve this issue, create hello performance counters in a startup task or move some of your startup task work toohello OnStart method after creating hello performance counters.</span></span>

<span data-ttu-id="844a0-273">Execute Olá etapas toocreate um contador denominado "\MyCustomCounterCategory\MyButton1Counter" de desempenho personalizado simples a seguir:</span><span class="sxs-lookup"><span data-stu-id="844a0-273">Perform hello following steps toocreate a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="844a0-274">Abra o arquivo de definição de serviço hello (CSDEF) para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="844a0-274">Open hello service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="844a0-275">Adicione Olá Runtime elemento toohello WebRole ou WorkerRole elemento tooallow execução com privilégios elevados:</span><span class="sxs-lookup"><span data-stu-id="844a0-275">Add hello Runtime element toohello WebRole or WorkerRole element tooallow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="844a0-276">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="844a0-276">Save hello file.</span></span>
4. <span data-ttu-id="844a0-277">Abra o arquivo de diagnóstico hello (wadcfg no SDK 2.4 e anterior ou wadcfgx no SDK 2.5 e superior) e adicione Olá toohello DiagnosticMonitorConfiguration a seguir</span><span class="sxs-lookup"><span data-stu-id="844a0-277">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="844a0-278">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="844a0-278">Save hello file.</span></span>
6. <span data-ttu-id="844a0-279">Crie categoria do contador de desempenho personalizados Olá no método OnStart de saudação de sua função, antes de chamar base. OnStart.</span><span class="sxs-lookup"><span data-stu-id="844a0-279">Create hello custom performance counter category in hello OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="844a0-280">Olá c# exemplo a seguir cria uma categoria personalizada, se ele ainda não existir:</span><span class="sxs-lookup"><span data-stu-id="844a0-280">hello following C# example creates a custom category, if it does not already exist:</span></span>

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
7. <span data-ttu-id="844a0-281">Atualize contadores hello dentro de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="844a0-281">Update hello counters within your application.</span></span> <span data-ttu-id="844a0-282">saudação de exemplo a seguir atualiza um contador de desempenho personalizados em eventos Button1_Click:</span><span class="sxs-lookup"><span data-stu-id="844a0-282">hello following example updates a custom performance counter on Button1_Click events:</span></span>

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
8. <span data-ttu-id="844a0-283">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="844a0-283">Save hello file.</span></span>  

<span data-ttu-id="844a0-284">Dados do contador de desempenho personalizados agora serão coletados pelo monitor de diagnóstico do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="844a0-284">Custom performance counter data will now be collected by hello Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="844a0-285">Etapa 3: Consultar dados do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="844a0-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="844a0-286">Depois que seu aplicativo é implantado e em execução, o monitor de diagnóstico Olá começarão a coletar contadores de desempenho e persistentes que tooAzure de armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="844a0-286">Once your application is deployed and running, hello Diagnostics monitor will begin collecting performance counters and persisting that data tooAzure storage.</span></span> <span data-ttu-id="844a0-287">Use ferramentas como o Gerenciador de servidores no Visual Studio, [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), ou [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) por Cerebrata dados Olá de contadores de desempenho de saudação do tooview Tabela WADPerformanceCountersTable.</span><span class="sxs-lookup"><span data-stu-id="844a0-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata tooview hello performance counters data in hello WADPerformanceCountersTable table.</span></span> <span data-ttu-id="844a0-288">Você pode consultar também programaticamente usando o serviço tabela Olá [c#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), ou [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="844a0-288">You can also programmatically query hello Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="844a0-289">Olá c# de exemplo seguinte mostra uma consulta básica em relação à tabela WADPerformanceCountersTable hello e salva o arquivo CSV do hello diagnóstico dados tooa.</span><span class="sxs-lookup"><span data-stu-id="844a0-289">hello following C# example shows a basic query against hello WADPerformanceCountersTable table and saves hello diagnostics data tooa CSV file.</span></span> <span data-ttu-id="844a0-290">Depois que os contadores de desempenho de saudação são salvos tooa arquivo CSV, você pode usar Olá graficamente recursos no Microsoft Excel ou outros ferramenta toovisualize Olá dados.</span><span class="sxs-lookup"><span data-stu-id="844a0-290">Once hello performance counters are saved tooa CSV file, you can use hello graphing capabilities in Microsoft Excel or some other tool toovisualize hello data.</span></span> <span data-ttu-id="844a0-291">Ser tooadd se tooMicrosoft.WindowsAzure.Storage.dll uma referência, que está incluído no hello Azure SDK para .NET de outubro de 2012 e posterior.</span><span class="sxs-lookup"><span data-stu-id="844a0-291">Be sure tooadd a reference tooMicrosoft.WindowsAzure.Storage.dll, which is included in hello Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="844a0-292">assembly Hello é instalado toohello % programa Files%\Microsoft SDKs\Microsoft Azure.NET sdk\version-num\ref\. directory.</span><span class="sxs-lookup"><span data-stu-id="844a0-292">hello assembly is installed toohello %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
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

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
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

<span data-ttu-id="844a0-293">Entidades são mapeadas tooC # objetos usando uma classe personalizada derivada de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="844a0-293">Entities map tooC# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="844a0-294">Olá, código a seguir define uma classe de entidade que representa um contador de desempenho no hello **WADPerformanceCountersTable** tabela.</span><span class="sxs-lookup"><span data-stu-id="844a0-294">hello following code defines an entity class that represents a performance counter in hello **WADPerformanceCountersTable** table.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="844a0-295">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="844a0-295">Next Steps</span></span>
[<span data-ttu-id="844a0-296">Exibir artigos adicionais sobre o Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="844a0-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
