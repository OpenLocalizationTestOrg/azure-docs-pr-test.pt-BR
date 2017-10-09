---
title: "aaaTroubleshooting e monitoramento do SAP HANA no Azure (instâncias grandes) | Microsoft Docs"
description: "Solução de problemas e monitoramento do SAP HANA no Azure (Instâncias Grandes)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="7273b-103">Como tootroubleshoot e monitor SAP HANA (instâncias grandes) no Azure</span><span class="sxs-lookup"><span data-stu-id="7273b-103">How tootroubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="7273b-104">Monitoramento no SAP HANA no Azure (Instâncias Grandes)</span><span class="sxs-lookup"><span data-stu-id="7273b-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="7273b-105">SAP HANA no Azure (instâncias grandes) não é diferente de qualquer outra implantação de IaaS — necessário toomonitor que Olá o sistema operacional e o aplicativo hello é isso e como elas consomem Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7273b-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need toomonitor what hello OS and hello application is doing and how these consume hello following resources:</span></span>

- <span data-ttu-id="7273b-106">CPU</span><span class="sxs-lookup"><span data-stu-id="7273b-106">CPU</span></span>
- <span data-ttu-id="7273b-107">Memória</span><span class="sxs-lookup"><span data-stu-id="7273b-107">Memory</span></span>
- <span data-ttu-id="7273b-108">Largura de banda de rede</span><span class="sxs-lookup"><span data-stu-id="7273b-108">Network bandwidth</span></span>
- <span data-ttu-id="7273b-109">Espaço em disco</span><span class="sxs-lookup"><span data-stu-id="7273b-109">Disk space</span></span>

<span data-ttu-id="7273b-110">Como com as máquinas virtuais do Azure, você precisa toofigure se classes de recursos Olá citados acima são suficientes ou se eles obtenham esgotados.</span><span class="sxs-lookup"><span data-stu-id="7273b-110">As with Azure Virtual Machines you need toofigure out whether hello resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="7273b-111">Aqui estão mais detalhes sobre cada uma das classes diferentes de saudação:</span><span class="sxs-lookup"><span data-stu-id="7273b-111">Here is more detail on each of hello different classes:</span></span>

<span data-ttu-id="7273b-112">**Consumo de recursos de CPU:** taxa de saudação SAP definido para determinadas cargas de trabalho em relação a HANA é imposto toomake-se de que deve ser suficiente recursos de CPU disponível toowork pelos dados de saudação que são armazenados na memória.</span><span class="sxs-lookup"><span data-stu-id="7273b-112">**CPU resource consumption:** hello ratio that SAP defined for certain workload against HANA is enforced toomake sure that there should be enough CPU resources available toowork through hello data that is stored in memory.</span></span> <span data-ttu-id="7273b-113">No entanto, pode haver casos onde HANA consome muito da CPU ao executar consultas de conclusão toomissing índices ou problemas semelhantes.</span><span class="sxs-lookup"><span data-stu-id="7273b-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due toomissing indexes or similar issues.</span></span> <span data-ttu-id="7273b-114">Isso significa que você deve monitorar o consumo de recursos de CPU de unidade de instância grande HANA hello, bem como recursos de CPU consumidos por serviços específicos de HANA hello.</span><span class="sxs-lookup"><span data-stu-id="7273b-114">This means you should monitor CPU resource consumption of hello HANA large instance unit as well as CPU resources consumed by hello specific HANA services.</span></span>

<span data-ttu-id="7273b-115">**Consumo de memória:** é importante toomonitor de dentro do HANA, bem como fora do HANA na unidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="7273b-115">**Memory consumption:** Is important toomonitor from within HANA, as well as outside of HANA on hello unit.</span></span> <span data-ttu-id="7273b-116">Dentro do HANA, monitore como dados saudação está consumindo HANA alocada memória em ordem toostay em Olá necessário dimensionar as diretrizes do SAP.</span><span class="sxs-lookup"><span data-stu-id="7273b-116">Within HANA, monitor how hello data is consuming HANA allocated memory in order toostay within hello required sizing guidelines of SAP.</span></span> <span data-ttu-id="7273b-117">Você também deseja toomonitor o consumo de memória em toomake nível de instância grande de saudação se software adicional instalado não-HANA não consomem muita memória e, portanto, concorre com HANA para a memória.</span><span class="sxs-lookup"><span data-stu-id="7273b-117">You also want toomonitor memory consumption on hello Large Instance level toomake sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="7273b-118">**Largura de banda de rede:** gateway de rede virtual do Azure Olá é limitado em largura de banda de dados em movimento em Olá VNet do Azure, portanto, é útil dados de saudação toomonitor recebidos por todos os Olá VMs do Azure dentro de um toofigure VNet o quão distante você toohello limites de saudação do Azure Gateway SKU selecionada.</span><span class="sxs-lookup"><span data-stu-id="7273b-118">**Network bandwidth:** hello Azure VNet gateway is limited in bandwidth of data moving into hello Azure VNet, so it is helpful toomonitor hello data received by all hello Azure VMs within a VNet toofigure out how close you are toohello limits of hello Azure gateway SKU you selected.</span></span> <span data-ttu-id="7273b-119">Na unidade de instância grande HANA Olá, ele fazer sentido toomonitor entrada e saída de tráfego de rede bem e acompanhar tookeep de volumes de saudação que são tratadas ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="7273b-119">On hello HANA Large Instance unit, it does make sense toomonitor incoming and outgoing network traffic as well, and tookeep track of hello volumes that are handled over time.</span></span>

<span data-ttu-id="7273b-120">**Espaço em disco:** normalmente, o consumo de espaço em disco aumenta ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="7273b-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="7273b-121">Há muitos motivos para isso, mas a maioria deles é: aumento no volume de dados, execução de backups do log de transações, armazenamento de arquivos de rastreamento e execução de instantâneos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7273b-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="7273b-122">Portanto, é importante toomonitor uso de espaço em disco e gerenciar o espaço de disco Olá associado Olá instância grande HANA unidade.</span><span class="sxs-lookup"><span data-stu-id="7273b-122">Therefore, it is important toomonitor disk space usage and manage hello disk space associated with hello HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="7273b-123">Monitoramento e solução de problemas no lado do HANA</span><span class="sxs-lookup"><span data-stu-id="7273b-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="7273b-124">Em ordem tooeffectively analisar problemas relacionados tooSAP HANA no Azure (instâncias grandes), é útil toonarrow para baixo da causa raiz de saudação de um problema.</span><span class="sxs-lookup"><span data-stu-id="7273b-124">In order tooeffectively analyze problems related tooSAP HANA on Azure (Large Instances), it is useful toonarrow down hello root cause of a problem.</span></span> <span data-ttu-id="7273b-125">SAP publicou uma grande quantidade de documentação toohelp você.</span><span class="sxs-lookup"><span data-stu-id="7273b-125">SAP has published a large amount of documentation toohelp you.</span></span>

<span data-ttu-id="7273b-126">Aplicável perguntas frequentes relacionadas tooSAP HANA desempenho pode ser encontrado no hello SAP observações a seguir:</span><span class="sxs-lookup"><span data-stu-id="7273b-126">Applicable FAQs related tooSAP HANA performance can be found in hello following SAP Notes:</span></span>

- [<span data-ttu-id="7273b-127">Nota SAP nº 2222200 – Perguntas frequentes: Rede SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7273b-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="7273b-128">Nota SAP nº 2100040 – Perguntas frequentes: CPU SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7273b-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="7273b-129">Nota SAP nº 199997 – Perguntas frequentes: Memória SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7273b-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="7273b-130">Nota SAP nº 200000 – Perguntas frequentes: Otimização de desempenho SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7273b-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="7273b-131">Nota SAP nº 199930 – Perguntas frequentes: Análise de E/S SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7273b-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="7273b-132">Nota da SAP #2177064 – Perguntas frequentes: Reinicialização e falhas do serviço SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7273b-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="7273b-133">**Alertas do SAP HANA**</span><span class="sxs-lookup"><span data-stu-id="7273b-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="7273b-134">Como uma primeira etapa, verifique os logs atuais de alerta de SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="7273b-134">As a first step, check hello current SAP HANA alert logs.</span></span> <span data-ttu-id="7273b-135">SAP HANA Studio, vá muito**Console de administração: alertas: mostrar: todos os alertas**.</span><span class="sxs-lookup"><span data-stu-id="7273b-135">In SAP HANA Studio, go too**Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="7273b-136">Este guia mostrará todos os alertas do SAP HANA valores específicos (memória física livre, utilização da CPU, etc.) que estão fora da saudação definir mínimo e máximo limites.</span><span class="sxs-lookup"><span data-stu-id="7273b-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of hello set minimum and maximum thresholds.</span></span> <span data-ttu-id="7273b-137">Por padrão, as verificações são atualizados automaticamente a cada 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="7273b-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![No SAP HANA Studio, vá tooAdministration Console: alertas: mostrar: todos os alertas](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="7273b-139">**CPU**</span><span class="sxs-lookup"><span data-stu-id="7273b-139">**CPU**</span></span>

<span data-ttu-id="7273b-140">Para um alerta foi disparado devido a configuração de limite de tooimproper, uma resolução é valor de padrão de toohello tooreset ou um valor de limite mais razoável.</span><span class="sxs-lookup"><span data-stu-id="7273b-140">For an alert triggered due tooimproper threshold setting, a resolution is tooreset toohello default value or a more reasonable threshold value.</span></span>

![Redefinir o valor padrão de toohello ou um valor de limite mais razoável](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="7273b-142">Olá alertas a seguir pode indicar problemas de recursos de CPU:</span><span class="sxs-lookup"><span data-stu-id="7273b-142">hello following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="7273b-143">Uso de CPU Host (Alerta 5)</span><span class="sxs-lookup"><span data-stu-id="7273b-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="7273b-144">Operação de ponto de salvamento mais recente (Alerta 28)</span><span class="sxs-lookup"><span data-stu-id="7273b-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="7273b-145">Duração do ponto de salvamento (Alerta 54)</span><span class="sxs-lookup"><span data-stu-id="7273b-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="7273b-146">Você pode observar o alto consumo de CPU em seu banco de dados do SAP HANA da saudação seguinte:</span><span class="sxs-lookup"><span data-stu-id="7273b-146">You may notice high CPU consumption on your SAP HANA database from one of hello following:</span></span>

- <span data-ttu-id="7273b-147">O Alerta 5 (Uso de CPU Host) é emitido para o uso de CPU atual ou anterior</span><span class="sxs-lookup"><span data-stu-id="7273b-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="7273b-148">Olá exibido o uso da CPU na tela de visão geral de saudação</span><span class="sxs-lookup"><span data-stu-id="7273b-148">hello displayed CPU usage on hello overview screen</span></span>

![Exibido o uso da CPU na tela de visão geral de saudação](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="7273b-150">gráfico de carga Olá pode mostrar o alto consumo de CPU ou alto consumo nas Olá anterior:</span><span class="sxs-lookup"><span data-stu-id="7273b-150">hello Load graph might show high CPU consumption, or high consumption in hello past:</span></span>

![gráfico de carga Olá pode mostrar o alto consumo de CPU ou alto consumo nas Olá anterior](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="7273b-152">Um alerta disparado devido a utilização de CPU de toohigh pode ser causado por vários motivos, incluindo, mas não se limitando a: execução de determinadas transações, o carregamento de dados, o deslocamento de trabalhos de longa execução instruções SQL e o desempenho de consulta inválida (por exemplo, com BW em HANA cubos).</span><span class="sxs-lookup"><span data-stu-id="7273b-152">An alert triggered due toohigh CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="7273b-153">Consulte toohello [solução de problemas do SAP HANA: soluções e CPU relacionados faz com que o](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site para etapas de solução de problemas detalhada.</span><span class="sxs-lookup"><span data-stu-id="7273b-153">Refer toohello [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="7273b-154">**Sistema operacional**</span><span class="sxs-lookup"><span data-stu-id="7273b-154">**Operating System**</span></span>

<span data-ttu-id="7273b-155">Um dos mais importantes de saudação verifica para SAP HANA no Linux é toomake se páginas enorme transparente estiver desabilitadas, consulte [2131662 de # nota SAP – transparente enorme páginas (THP) em servidores do SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="7273b-155">One of hello most important checks for SAP HANA on Linux is toomake sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="7273b-156">Você pode verificar se páginas enorme transparente são habilitadas por meio de saudação Linux comando a seguir: **cat /sys/kernel/mm/transparent\_hugepage/habilitado**</span><span class="sxs-lookup"><span data-stu-id="7273b-156">You can check if Transparent Huge Pages are enabled through hello following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="7273b-157">Se _sempre_ é colocado entre colchetes, como a seguir, isso significa que páginas enorme transparente de saudação estão habilitadas: [sempre] madvise nunca; se _nunca_ é colocado entre colchetes, como a seguir, isso significa que Olá transparente Páginas enormes estão desabilitadas: sempre madvise [nunca]</span><span class="sxs-lookup"><span data-stu-id="7273b-157">If _always_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="7273b-158">Olá Linux comando a seguir deve retornar nada: **rpm - qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="7273b-158">hello following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="7273b-159">Se parecer que _ulimit_ está instalado, desinstale-o imediatamente.</span><span class="sxs-lookup"><span data-stu-id="7273b-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="7273b-160">**Memória**</span><span class="sxs-lookup"><span data-stu-id="7273b-160">**Memory**</span></span>

<span data-ttu-id="7273b-161">Você pode observar essa quantidade de saudação de memória alocada pelo Olá SAP HANA banco de dados é maior do que o esperado.</span><span class="sxs-lookup"><span data-stu-id="7273b-161">You may observe that hello amount of memory allocated by hello SAP HANA database is higher than expected.</span></span> <span data-ttu-id="7273b-162">Olá alertas a seguir indica problemas com alto uso da memória:</span><span class="sxs-lookup"><span data-stu-id="7273b-162">hello following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="7273b-163">Uso de memória do host físico (Alerta 1)</span><span class="sxs-lookup"><span data-stu-id="7273b-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="7273b-164">Uso de memória do servidor de nomes (Alerta 12)</span><span class="sxs-lookup"><span data-stu-id="7273b-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="7273b-165">Uso total da memória das tabelas do Repositório de Colunas (Alerta 40)</span><span class="sxs-lookup"><span data-stu-id="7273b-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="7273b-166">Uso de memória dos serviços (Alerta 43)</span><span class="sxs-lookup"><span data-stu-id="7273b-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="7273b-167">Uso de memória do armazenamento principal das tabelas do Repositório de Colunas (Alerta 45)</span><span class="sxs-lookup"><span data-stu-id="7273b-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="7273b-168">Arquivos de despejo em tempo de execução (Alerta 46)</span><span class="sxs-lookup"><span data-stu-id="7273b-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="7273b-169">Consulte toohello [solução de problemas do SAP HANA: problemas de memória](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site para etapas de solução de problemas detalhada.</span><span class="sxs-lookup"><span data-stu-id="7273b-169">Refer toohello [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="7273b-170">**Rede**</span><span class="sxs-lookup"><span data-stu-id="7273b-170">**Network**</span></span>

<span data-ttu-id="7273b-171">Consulte também[2081065 de # nota SAP – Solucionando problemas de rede do SAP HANA](https://launchpad.support.sap.com/#/notes/2081065) e executar as etapas nesta nota da SAP de solução de problemas de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="7273b-171">Refer too[SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform hello network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="7273b-172">Análise do tempo de ida e volta entre o cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="7273b-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="7273b-173">R.</span><span class="sxs-lookup"><span data-stu-id="7273b-173">A.</span></span> <span data-ttu-id="7273b-174">Executar script SQL Olá [ _HANA\_rede\_clientes_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="7273b-174">Run hello SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="7273b-175">Análise da comunicação entre nós.</span><span class="sxs-lookup"><span data-stu-id="7273b-175">Analyze internode communication.</span></span>
  <span data-ttu-id="7273b-176">R.</span><span class="sxs-lookup"><span data-stu-id="7273b-176">A.</span></span> <span data-ttu-id="7273b-177">Execute o script SQL [_HANA\_Rede\_Serviços_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="7273b-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="7273b-178">Execute o comando do Linux **ifconfig** (saída Olá mostra se quaisquer perdas de pacote estão ocorrendo).</span><span class="sxs-lookup"><span data-stu-id="7273b-178">Run Linux command **ifconfig** (hello output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="7273b-179">Execute o comando Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="7273b-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="7273b-180">Além disso, use o código-fonte aberto Olá [IPERF](https://iperf.fr/) ferramenta (ou semelhante) toomeasure desempenho de rede do aplicativo real.</span><span class="sxs-lookup"><span data-stu-id="7273b-180">Also, use hello open source [IPERF](https://iperf.fr/) tool (or similar) toomeasure real application network performance.</span></span>

<span data-ttu-id="7273b-181">Consulte toohello [solução de problemas do SAP HANA: desempenho do sistema de rede e problemas de conectividade](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site para etapas de solução de problemas detalhada.</span><span class="sxs-lookup"><span data-stu-id="7273b-181">Refer toohello [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="7273b-182">**Armazenamento**</span><span class="sxs-lookup"><span data-stu-id="7273b-182">**Storage**</span></span>

<span data-ttu-id="7273b-183">Da perspectiva do usuário final, um aplicativo (ou sistema hello como um todo) é executado lentamente, não está respondendo ou até mesmo pode parecer toohang se houver problemas com o desempenho de e/s.</span><span class="sxs-lookup"><span data-stu-id="7273b-183">From an end-user perspective, an application (or hello system as a whole) runs sluggishly, is unresponsive, or can even seem toohang if there are issues with I/O performance.</span></span> <span data-ttu-id="7273b-184">Em Olá **Volumes** guia SAP HANA Studio, você pode ver Olá anexado volumes e quais volumes são usadas por cada serviço.</span><span class="sxs-lookup"><span data-stu-id="7273b-184">In hello **Volumes** tab in SAP HANA Studio, you can see hello attached volumes, and what volumes are used by each service.</span></span>

![Na guia de Volumes de saudação do SAP HANA Studio, você pode ver Olá anexado volumes e quais volumes são usadas por cada serviço](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="7273b-186">Na parte inferior de saudação da tela hello de que você pode ver os detalhes seus volumes anexados Olá volumes, como arquivos e estatísticas de e/s.</span><span class="sxs-lookup"><span data-stu-id="7273b-186">Attached volumes in hello lower part of hello screen you can see details of hello volumes, such as files and I/O statistics.</span></span>

![Na parte inferior de saudação da tela hello de que você pode ver os detalhes seus volumes anexados Olá volumes, como arquivos e estatísticas de e/s](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="7273b-188">Consulte toohello [solução de problemas do SAP HANA: e/s relacionadas causas e soluções](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) e [solução de problemas do SAP HANA: disco relacionadas causas e soluções](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site para etapas de solução de problemas detalhada.</span><span class="sxs-lookup"><span data-stu-id="7273b-188">Refer toohello [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="7273b-189">**Ferramentas de Diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="7273b-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="7273b-190">Execute uma Verificação de Integridade do SAP HANA por meio do HANA\_Configuration\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="7273b-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="7273b-191">Essa ferramenta retorna possíveis problemas técnicos críticos que devem já ter sido gerados como alertas no SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="7273b-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="7273b-192">Consulte também[1969700 de # nota SAP – conjunto de instrução SQL para o SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) e baixar Observação do hello SQL Statements.zip arquivo toothat anexado.</span><span class="sxs-lookup"><span data-stu-id="7273b-192">Refer too[SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download hello SQL Statements.zip file attached toothat note.</span></span> <span data-ttu-id="7273b-193">Armazene esse arquivo. zip na unidade de disco rígido local hello.</span><span class="sxs-lookup"><span data-stu-id="7273b-193">Store this .zip file on hello local hard drive.</span></span>

<span data-ttu-id="7273b-194">No Studio do HANA SAP, em Olá **informações do sistema** guia, clique com botão direito no hello **nome** coluna e selecione **instruções SQL de importação**.</span><span class="sxs-lookup"><span data-stu-id="7273b-194">In SAP HANA Studio, on hello **System Information** tab, right-click in hello **Name** column and select **Import SQL Statements**.</span></span>

![No SAP HANA Studio, na guia de informações do sistema Olá, clique na coluna de nome hello e selecione instruções SQL de importação](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="7273b-196">Selecione Olá SQL Statements.zip arquivo armazenado localmente e uma pasta com instruções SQL correspondentes de saudação será importada.</span><span class="sxs-lookup"><span data-stu-id="7273b-196">Select hello SQL Statements.zip file stored locally, and a folder with hello corresponding SQL statements will be imported.</span></span> <span data-ttu-id="7273b-197">Neste ponto, Olá que várias verificações de diagnósticas diferentes podem ser executadas com essas instruções SQL.</span><span class="sxs-lookup"><span data-stu-id="7273b-197">At this point, hello many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="7273b-198">Por exemplo, os requisitos de largura de banda de replicação de sistema do SAP HANA tootest, clique Olá **largura de banda** instrução em **replicação: largura de banda** e selecione **abrir** no Console do SQL.</span><span class="sxs-lookup"><span data-stu-id="7273b-198">For example, tootest SAP HANA System Replication bandwidth requirements, right-click hello **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="7273b-199">instrução de SQL completa Olá abre toobe de parâmetros de entrada (seção de modificação) permitindo alterado e, em seguida, é executado.</span><span class="sxs-lookup"><span data-stu-id="7273b-199">hello complete SQL statement opens allowing input parameters (modification section) toobe changed and then executed.</span></span>

![instrução de SQL completa Olá abre toobe de parâmetros de entrada (seção de modificação) permitindo alterado e, em seguida, executado](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="7273b-201">Outro exemplo é com o botão direito em instruções de saudação em **replicação: Visão geral do**.</span><span class="sxs-lookup"><span data-stu-id="7273b-201">Another example is right-clicking on hello statements under **Replication: Overview**.</span></span> <span data-ttu-id="7273b-202">Selecione **Execute** Olá no menu de contexto:</span><span class="sxs-lookup"><span data-stu-id="7273b-202">Select **Execute** from hello context menu:</span></span>

![Outro exemplo é com o botão direito em instruções de saudação em replicação: Visão geral.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="7273b-205">Isso resulta em informações que ajudam com a solução de problemas:</span><span class="sxs-lookup"><span data-stu-id="7273b-205">This results in information that helps with troubleshooting:</span></span>

![Isso resultará em informações que ajudam com a solução de problemas](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="7273b-207">Olá mesmo para HANA\_configuração\_Minichecks e verificar se há qualquer _X_ marcas no hello _C_ coluna (crítico).</span><span class="sxs-lookup"><span data-stu-id="7273b-207">Do hello same for HANA\_Configuration\_Minichecks and check for any _X_ marks in hello _C_ (Critical) column.</span></span>

<span data-ttu-id="7273b-208">Exemplos de saída:</span><span class="sxs-lookup"><span data-stu-id="7273b-208">Sample outputs:</span></span>

<span data-ttu-id="7273b-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** para verificações gerais do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7273b-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_Configuration\_MiniChecks\_Rev102.01+1 para verificações gerais SAP HANA](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="7273b-211">**HANA\_Services\_Overview** para uma visão geral de quais serviços SAP HANA estão em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="7273b-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_Overview para uma visão geral de quais serviços SAP HANA estão em execução no momento](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="7273b-213">**HANA\_Services\_Statistics** para informações de serviço do SAP HANA (CPU, memória etc.).</span><span class="sxs-lookup"><span data-stu-id="7273b-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="7273b-214">HANA\_Services\_Statistics para informações de serviço do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7273b-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="7273b-215">**HANA\_configuração\_visão geral\_Rev110 +** para obter informações gerais sobre a instância do SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="7273b-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on hello SAP HANA instance.</span></span>

![HANA\_configuração\_visão geral\_Rev110 + para obter informações gerais sobre a instância do SAP HANA Olá](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="7273b-217">**HANA\_configuração\_parâmetros\_Rev70 +** toocheck parâmetros de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7273b-217">**HANA\_Configuration\_Parameters\_Rev70+** toocheck SAP HANA parameters.</span></span>

![HANA\_configuração\_parâmetros\_Rev70 + toocheck parâmetros de SAP HANA](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

