---
title: "Solução de problemas e monitoramento do SAP HANA no Azure (Instâncias Grandes) | Microsoft Docs"
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
ms.openlocfilehash: ee5be707b443cbe42bf4a492d79390e534d4b91f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="cfe70-103">Como solucionar problemas e monitorar o SAP HANA (instâncias grandes) no Azure</span><span class="sxs-lookup"><span data-stu-id="cfe70-103">How to troubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="cfe70-104">Monitoramento no SAP HANA no Azure (Instâncias Grandes)</span><span class="sxs-lookup"><span data-stu-id="cfe70-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="cfe70-105">SAP HANA no Azure (Instâncias Grandes) não é diferente de qualquer outra implantação IaaS — você precisa monitorar o que o sistema operacional e o aplicativo estão fazendo e como eles consomem os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cfe70-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need to monitor what the OS and the application is doing and how these consume the following resources:</span></span>

- <span data-ttu-id="cfe70-106">CPU</span><span class="sxs-lookup"><span data-stu-id="cfe70-106">CPU</span></span>
- <span data-ttu-id="cfe70-107">Memória</span><span class="sxs-lookup"><span data-stu-id="cfe70-107">Memory</span></span>
- <span data-ttu-id="cfe70-108">Largura de banda de rede</span><span class="sxs-lookup"><span data-stu-id="cfe70-108">Network bandwidth</span></span>
- <span data-ttu-id="cfe70-109">Espaço em disco</span><span class="sxs-lookup"><span data-stu-id="cfe70-109">Disk space</span></span>

<span data-ttu-id="cfe70-110">Assim como ocorre com as Máquinas Virtuais do Azure, você precisa descobrir se as classes de recursos indicadas acima são suficientes, ou se elas se esgotam.</span><span class="sxs-lookup"><span data-stu-id="cfe70-110">As with Azure Virtual Machines you need to figure out whether the resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="cfe70-111">Confira mais detalhes sobre cada uma das diferentes classes:</span><span class="sxs-lookup"><span data-stu-id="cfe70-111">Here is more detail on each of the different classes:</span></span>

<span data-ttu-id="cfe70-112">**Consumo de recursos de CPU:** a proporção que a SAP definiu para certas cargas de trabalho no HANA é aplicada para garantir a existência de recursos de CPU suficientes disponíveis para trabalhar com os dados armazenados na memória.</span><span class="sxs-lookup"><span data-stu-id="cfe70-112">**CPU resource consumption:** The ratio that SAP defined for certain workload against HANA is enforced to make sure that there should be enough CPU resources available to work through the data that is stored in memory.</span></span> <span data-ttu-id="cfe70-113">No entanto, pode haver casos em que o HANA consome muita CPU executando consultas devido à ausência de índices ou problemas semelhantes.</span><span class="sxs-lookup"><span data-stu-id="cfe70-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due to missing indexes or similar issues.</span></span> <span data-ttu-id="cfe70-114">Isso significa que você deve monitorar o consumo de recursos de CPU da unidade de instância grande do HANA, bem como recursos de CPU consumidos por serviços específicos do HANA.</span><span class="sxs-lookup"><span data-stu-id="cfe70-114">This means you should monitor CPU resource consumption of the HANA large instance unit as well as CPU resources consumed by the specific HANA services.</span></span>

<span data-ttu-id="cfe70-115">**Consumo de memória:** é importante monitorar de dentro do HANA, bem como fora do HANA na unidade.</span><span class="sxs-lookup"><span data-stu-id="cfe70-115">**Memory consumption:** Is important to monitor from within HANA, as well as outside of HANA on the unit.</span></span> <span data-ttu-id="cfe70-116">Dentro do HANA, monitore como os dados estão consumindo memória alocada no HANA a fim de permanecer dentro das diretrizes de dimensionamento obrigatórias do SAP.</span><span class="sxs-lookup"><span data-stu-id="cfe70-116">Within HANA, monitor how the data is consuming HANA allocated memory in order to stay within the required sizing guidelines of SAP.</span></span> <span data-ttu-id="cfe70-117">Convém também monitorar o consumo de memória no nível da Instância Grande para certificar-se de que outros softwares não HANA instalados não consumam muita memória e, assim, compitam por memória com o HANA.</span><span class="sxs-lookup"><span data-stu-id="cfe70-117">You also want to monitor memory consumption on the Large Instance level to make sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="cfe70-118">**Largura de banda de rede:** o gateway de VNet do Azure tem uma limitação de largura de banda para dados em movimentação para a VNet do Azure, portanto, é útil monitorar os dados recebidos por todas as VMs do Azure em uma VNet para descobrir o quão próximo você está dos limites do SKU do gateway do Azure selecionado.</span><span class="sxs-lookup"><span data-stu-id="cfe70-118">**Network bandwidth:** The Azure VNet gateway is limited in bandwidth of data moving into the Azure VNet, so it is helpful to monitor the data received by all the Azure VMs within a VNet to figure out how close you are to the limits of the Azure gateway SKU you selected.</span></span> <span data-ttu-id="cfe70-119">Na unidade de Instância Grande do HANA, também faz sentido monitorar o tráfego de rede de entrada e saída, além de controlar os volumes manipulados ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="cfe70-119">On the HANA Large Instance unit, it does make sense to monitor incoming and outgoing network traffic as well, and to keep track of the volumes that are handled over time.</span></span>

<span data-ttu-id="cfe70-120">**Espaço em disco:** normalmente, o consumo de espaço em disco aumenta ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="cfe70-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="cfe70-121">Há muitos motivos para isso, mas a maioria deles é: aumento no volume de dados, execução de backups do log de transações, armazenamento de arquivos de rastreamento e execução de instantâneos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cfe70-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="cfe70-122">Portanto, é importante monitorar o uso do espaço em disco e gerenciar o espaço em disco associado à Instância Grande do HANA.</span><span class="sxs-lookup"><span data-stu-id="cfe70-122">Therefore, it is important to monitor disk space usage and manage the disk space associated with the HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="cfe70-123">Monitoramento e solução de problemas no lado do HANA</span><span class="sxs-lookup"><span data-stu-id="cfe70-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="cfe70-124">Para analisar efetivamente os problemas relacionados ao SAP HANA no Azure (Instâncias Grandes), é útil restringir a causa raiz do problema.</span><span class="sxs-lookup"><span data-stu-id="cfe70-124">In order to effectively analyze problems related to SAP HANA on Azure (Large Instances), it is useful to narrow down the root cause of a problem.</span></span> <span data-ttu-id="cfe70-125">O SAP publicou uma grande quantidade de documentação para ajudar você.</span><span class="sxs-lookup"><span data-stu-id="cfe70-125">SAP has published a large amount of documentation to help you.</span></span>

<span data-ttu-id="cfe70-126">Perguntas frequentes aplicáveis relacionadas ao desempenho do SAP HANA podem ser encontradas nas seguintes Notas SAP a seguir:</span><span class="sxs-lookup"><span data-stu-id="cfe70-126">Applicable FAQs related to SAP HANA performance can be found in the following SAP Notes:</span></span>

- [<span data-ttu-id="cfe70-127">Nota SAP nº 2222200 – Perguntas frequentes: Rede SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cfe70-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="cfe70-128">Nota SAP nº 2100040 – Perguntas frequentes: CPU SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cfe70-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="cfe70-129">Nota SAP nº 199997 – Perguntas frequentes: Memória SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cfe70-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="cfe70-130">Nota SAP nº 200000 – Perguntas frequentes: Otimização de desempenho SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cfe70-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="cfe70-131">Nota SAP nº 199930 – Perguntas frequentes: Análise de E/S SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cfe70-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="cfe70-132">Nota da SAP #2177064 – Perguntas frequentes: Reinicialização e falhas do serviço SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cfe70-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="cfe70-133">**Alertas do SAP HANA**</span><span class="sxs-lookup"><span data-stu-id="cfe70-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="cfe70-134">Como uma primeira etapa, verifique os logs de alerta atuais do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cfe70-134">As a first step, check the current SAP HANA alert logs.</span></span> <span data-ttu-id="cfe70-135">No SAP HANA Studio, acesse **Console de Administração: Alertas: Mostrar: todos os alertas**.</span><span class="sxs-lookup"><span data-stu-id="cfe70-135">In SAP HANA Studio, go to **Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="cfe70-136">Esta guia mostrará todos os alertas do SAP HANA para valores específicos (memória física livre, utilização de CPU etc.) que estão fora dos limites mínimo e máximo definidos.</span><span class="sxs-lookup"><span data-stu-id="cfe70-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of the set minimum and maximum thresholds.</span></span> <span data-ttu-id="cfe70-137">Por padrão, as verificações são atualizados automaticamente a cada 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="cfe70-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![No SAP HANA Studio, acesse Console de Administração: Alertas: Mostrar: todos os alertas](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="cfe70-139">**CPU**</span><span class="sxs-lookup"><span data-stu-id="cfe70-139">**CPU**</span></span>

<span data-ttu-id="cfe70-140">Para um alerta disparado devido à configuração incorreta do limite, uma resolução é redefinir para o valor padrão ou um valor de limite mais razoável.</span><span class="sxs-lookup"><span data-stu-id="cfe70-140">For an alert triggered due to improper threshold setting, a resolution is to reset to the default value or a more reasonable threshold value.</span></span>

![Redefinir para o valor padrão ou para um valor de limite mais razoável](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="cfe70-142">Os alertas a seguir podem indicar problemas de recursos de CPU:</span><span class="sxs-lookup"><span data-stu-id="cfe70-142">The following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="cfe70-143">Uso de CPU Host (Alerta 5)</span><span class="sxs-lookup"><span data-stu-id="cfe70-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="cfe70-144">Operação de ponto de salvamento mais recente (Alerta 28)</span><span class="sxs-lookup"><span data-stu-id="cfe70-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="cfe70-145">Duração do ponto de salvamento (Alerta 54)</span><span class="sxs-lookup"><span data-stu-id="cfe70-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="cfe70-146">Talvez você perceba o alto consumo de CPU em seu banco de dados SAP HANA em um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="cfe70-146">You may notice high CPU consumption on your SAP HANA database from one of the following:</span></span>

- <span data-ttu-id="cfe70-147">O Alerta 5 (Uso de CPU Host) é emitido para o uso de CPU atual ou anterior</span><span class="sxs-lookup"><span data-stu-id="cfe70-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="cfe70-148">O uso de CPU exibido na tela de visão geral</span><span class="sxs-lookup"><span data-stu-id="cfe70-148">The displayed CPU usage on the overview screen</span></span>

![Uso de CPU exibido na tela de visão geral](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="cfe70-150">O gráfico de Carregamento pode mostrar alto consumo de CPU ou alto consumo anterior:</span><span class="sxs-lookup"><span data-stu-id="cfe70-150">The Load graph might show high CPU consumption, or high consumption in the past:</span></span>

![O gráfico de Carregamento pode mostrar alto consumo de CPU ou alto consumo anterior](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="cfe70-152">Um alerta disparado devido à alta utilização de CPU pode ser causado por vários motivos, incluindo, mas sem limitação: execução de certas transações, carregamento de dados, travamento de trabalhos, instruções SQL de longa execução e desempenho ruim da consulta (por exemplo, com BW em cubos HANA).</span><span class="sxs-lookup"><span data-stu-id="cfe70-152">An alert triggered due to high CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="cfe70-153">Consulte o site [Solução de problemas do SAP HANA: causas e soluções relacionadas à CPU](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) para obter etapas de solução de problemas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="cfe70-153">Refer to the [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="cfe70-154">**Sistema operacional**</span><span class="sxs-lookup"><span data-stu-id="cfe70-154">**Operating System**</span></span>

<span data-ttu-id="cfe70-155">Uma das verificações mais importantes para o SAP HANA no Linux é certificar-se de que Transparent Huge Pages estejam desabilitadas, consulte a [Nota SAP nº 2131662 – THP (Transparent Huge Pages) em servidores SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="cfe70-155">One of the most important checks for SAP HANA on Linux is to make sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="cfe70-156">Você pode verificar se o Transparent Huge Pages está habilitado por meio do seguinte comando do Linux: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span><span class="sxs-lookup"><span data-stu-id="cfe70-156">You can check if Transparent Huge Pages are enabled through the following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="cfe70-157">Se _always_ estiver entre colchetes, conforme mostrado a seguir, significa que Transparent Huge Pages está habilitado: [always] madvise never; se _never_ estiver entre colchetes, conforme mostrado a seguir, significa que Transparent Huge Pages está desabilitado: always madvise [never]</span><span class="sxs-lookup"><span data-stu-id="cfe70-157">If _always_ is enclosed in brackets as below, it means that the Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that the Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="cfe70-158">O comando Linux a seguir não deve retornar nada: **rpm -qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="cfe70-158">The following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="cfe70-159">Se parecer que _ulimit_ está instalado, desinstale-o imediatamente.</span><span class="sxs-lookup"><span data-stu-id="cfe70-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="cfe70-160">**Memória**</span><span class="sxs-lookup"><span data-stu-id="cfe70-160">**Memory**</span></span>

<span data-ttu-id="cfe70-161">Você pode observar que a quantidade de memória alocada pelo banco de dados SAP HANA é maior do que o esperado.</span><span class="sxs-lookup"><span data-stu-id="cfe70-161">You may observe that the amount of memory allocated by the SAP HANA database is higher than expected.</span></span> <span data-ttu-id="cfe70-162">Os alertas a seguir indicam problemas com alto uso da memória:</span><span class="sxs-lookup"><span data-stu-id="cfe70-162">The following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="cfe70-163">Uso de memória do host físico (Alerta 1)</span><span class="sxs-lookup"><span data-stu-id="cfe70-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="cfe70-164">Uso de memória do servidor de nomes (Alerta 12)</span><span class="sxs-lookup"><span data-stu-id="cfe70-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="cfe70-165">Uso total da memória das tabelas do Repositório de Colunas (Alerta 40)</span><span class="sxs-lookup"><span data-stu-id="cfe70-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="cfe70-166">Uso de memória dos serviços (Alerta 43)</span><span class="sxs-lookup"><span data-stu-id="cfe70-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="cfe70-167">Uso de memória do armazenamento principal das tabelas do Repositório de Colunas (Alerta 45)</span><span class="sxs-lookup"><span data-stu-id="cfe70-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="cfe70-168">Arquivos de despejo em tempo de execução (Alerta 46)</span><span class="sxs-lookup"><span data-stu-id="cfe70-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="cfe70-169">Consulte o site [Solução de problemas do SAP HANA: problemas de memória](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) para obter etapas de solução de problemas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="cfe70-169">Refer to the [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="cfe70-170">**Rede**</span><span class="sxs-lookup"><span data-stu-id="cfe70-170">**Network**</span></span>

<span data-ttu-id="cfe70-171">Consulte a [Nota SAP nº 2081065 – Solução de problemas de rede do SAP HANA](https://launchpad.support.sap.com/#/notes/2081065) e execute as etapas de solução de problemas de rede desta Nota SAP.</span><span class="sxs-lookup"><span data-stu-id="cfe70-171">Refer to [SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform the network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="cfe70-172">Análise do tempo de ida e volta entre o cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="cfe70-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="cfe70-173">R.</span><span class="sxs-lookup"><span data-stu-id="cfe70-173">A.</span></span> <span data-ttu-id="cfe70-174">Execute o script SQL [_HANA\_Rede\_Clientes_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="cfe70-174">Run the SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="cfe70-175">Análise da comunicação entre nós.</span><span class="sxs-lookup"><span data-stu-id="cfe70-175">Analyze internode communication.</span></span>
  <span data-ttu-id="cfe70-176">R.</span><span class="sxs-lookup"><span data-stu-id="cfe70-176">A.</span></span> <span data-ttu-id="cfe70-177">Execute o script SQL [_HANA\_Rede\_Serviços_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="cfe70-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="cfe70-178">Execute o comando Linux **ifconfig** (a saída mostrará se ocorre quaisquer perdas de pacote).</span><span class="sxs-lookup"><span data-stu-id="cfe70-178">Run Linux command **ifconfig** (the output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="cfe70-179">Execute o comando Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="cfe70-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="cfe70-180">Além disso, use a ferramenta [IPERF](https://iperf.fr/) de código-fonte aberto (ou semelhante) para medir o desempenho real da rede do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cfe70-180">Also, use the open source [IPERF](https://iperf.fr/) tool (or similar) to measure real application network performance.</span></span>

<span data-ttu-id="cfe70-181">Consulte o site [Solução de problemas do SAP HANA: problemas de desempenho e conectividade](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) para obter etapas de solução de problemas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="cfe70-181">Refer to the [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="cfe70-182">**Armazenamento**</span><span class="sxs-lookup"><span data-stu-id="cfe70-182">**Storage**</span></span>

<span data-ttu-id="cfe70-183">Da perspectiva do usuário final, um aplicativo (ou o sistema como um todo) é executado lentamente, não está respondendo ou parece até mesmo travar se houver problemas com o desempenho de E/S.</span><span class="sxs-lookup"><span data-stu-id="cfe70-183">From an end-user perspective, an application (or the system as a whole) runs sluggishly, is unresponsive, or can even seem to hang if there are issues with I/O performance.</span></span> <span data-ttu-id="cfe70-184">Na guia **Volumes** no SAP HANA Studio, você pode ver os volumes conectados e quais volumes são usados por cada serviço.</span><span class="sxs-lookup"><span data-stu-id="cfe70-184">In the **Volumes** tab in SAP HANA Studio, you can see the attached volumes, and what volumes are used by each service.</span></span>

![Na guia Volumes no SAP HANA Studio, você pode ver os volumes conectados e quais volumes são usados por cada serviço](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="cfe70-186">Você pode ver detalhes dos volumes conectados na parte inferior da tela, como arquivos e estatísticas de E/S.</span><span class="sxs-lookup"><span data-stu-id="cfe70-186">Attached volumes in the lower part of the screen you can see details of the volumes, such as files and I/O statistics.</span></span>

![Você pode ver detalhes dos volumes conectados na parte inferior da tela, como arquivos e estatísticas de E/S](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="cfe70-188">Consulte os sites [Solução de problemas de SAP HANA: Principais causas e soluções relacionadas à E/S](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) e [Solução de problemas de SAP HANA: Principais causas e soluções relacionadas ao disco](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) para obter as etapas de solução de problemas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="cfe70-188">Refer to the [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="cfe70-189">**Ferramentas de Diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="cfe70-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="cfe70-190">Execute uma Verificação de Integridade do SAP HANA por meio do HANA\_Configuration\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="cfe70-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="cfe70-191">Essa ferramenta retorna possíveis problemas técnicos críticos que devem já ter sido gerados como alertas no SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="cfe70-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="cfe70-192">Consulte [Nota SAP nº1969700 – Coleta de instrução SQL para SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) e baixe o arquivo SQL Statements.zip anexado à nota.</span><span class="sxs-lookup"><span data-stu-id="cfe70-192">Refer to [SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download the SQL Statements.zip file attached to that note.</span></span> <span data-ttu-id="cfe70-193">Armazene esse arquivo .zip no disco rígido local.</span><span class="sxs-lookup"><span data-stu-id="cfe70-193">Store this .zip file on the local hard drive.</span></span>

<span data-ttu-id="cfe70-194">No SAP HANA Studio, na guia **Informações do Sistema**, clique com o botão direito na coluna **Nome** e selecione **Importar Instruções SQL**.</span><span class="sxs-lookup"><span data-stu-id="cfe70-194">In SAP HANA Studio, on the **System Information** tab, right-click in the **Name** column and select **Import SQL Statements**.</span></span>

![No SAP HANA Studio, na guia Informações do Sistema, clique com o botão direito na coluna Nome e selecione Importar Instruções SQL](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="cfe70-196">Selecione o arquivo SQL Statements.zip armazenado localmente, e uma pasta com instruções SQL correspondentes será importada.</span><span class="sxs-lookup"><span data-stu-id="cfe70-196">Select the SQL Statements.zip file stored locally, and a folder with the corresponding SQL statements will be imported.</span></span> <span data-ttu-id="cfe70-197">Neste ponto, as diversas verificações de diagnóstico podem ser executadas com essas instruções SQL.</span><span class="sxs-lookup"><span data-stu-id="cfe70-197">At this point, the many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="cfe70-198">Por exemplo, para testar os requisitos de largura de banda de replicação do sistema SAP HANA, clique com o botão direito na instrução **Largura de banda** em **Replicação: largura de banda** e selecione **Abrir** no Console do SQL.</span><span class="sxs-lookup"><span data-stu-id="cfe70-198">For example, to test SAP HANA System Replication bandwidth requirements, right-click the **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="cfe70-199">A instrução SQL completa é aberta, permitindo que os parâmetros de entrada (seção de modificação) sejam alterados e, em seguida, executados.</span><span class="sxs-lookup"><span data-stu-id="cfe70-199">The complete SQL statement opens allowing input parameters (modification section) to be changed and then executed.</span></span>

![A instrução SQL completa é aberta, permitindo que os parâmetros de entrada (seção de modificação) sejam alterados e, em seguida, executados](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="cfe70-201">Outro exemplo é clicar com o botão direito nas instruções em **Replicação: visão geral**.</span><span class="sxs-lookup"><span data-stu-id="cfe70-201">Another example is right-clicking on the statements under **Replication: Overview**.</span></span> <span data-ttu-id="cfe70-202">Selecione **Executar** no menu de contexto:</span><span class="sxs-lookup"><span data-stu-id="cfe70-202">Select **Execute** from the context menu:</span></span>

![Outro exemplo é clicar com o botão direito nas instruções em Replicação: visão geral.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="cfe70-205">Isso resulta em informações que ajudam com a solução de problemas:</span><span class="sxs-lookup"><span data-stu-id="cfe70-205">This results in information that helps with troubleshooting:</span></span>

![Isso resultará em informações que ajudam com a solução de problemas](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="cfe70-207">Faça o mesmo para as HANA\_Configuration\_Minichecks e verifique se há qualquer marca _X_ na coluna _C_ (Crítico).</span><span class="sxs-lookup"><span data-stu-id="cfe70-207">Do the same for HANA\_Configuration\_Minichecks and check for any _X_ marks in the _C_ (Critical) column.</span></span>

<span data-ttu-id="cfe70-208">Exemplos de saída:</span><span class="sxs-lookup"><span data-stu-id="cfe70-208">Sample outputs:</span></span>

<span data-ttu-id="cfe70-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** para verificações gerais do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cfe70-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_Configuration\_MiniChecks\_Rev102.01+1 para verificações gerais SAP HANA](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="cfe70-211">**HANA\_Services\_Overview** para uma visão geral de quais serviços SAP HANA estão em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="cfe70-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_Overview para uma visão geral de quais serviços SAP HANA estão em execução no momento](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="cfe70-213">**HANA\_Services\_Statistics** para informações de serviço do SAP HANA (CPU, memória etc.).</span><span class="sxs-lookup"><span data-stu-id="cfe70-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="cfe70-214">HANA\_Services\_Statistics para informações de serviço do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cfe70-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="cfe70-215">**HANA\_Configuration\_Overview\_Rev110+** para informações gerais sobre a instância do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cfe70-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on the SAP HANA instance.</span></span>

![HANA\_Configuration\_Overview\_Rev110+ para informações gerais sobre a instância do SAP HANA](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="cfe70-217">**HANA\_Configuration\_Parameters\_Rev70+** para verificar parâmetros do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cfe70-217">**HANA\_Configuration\_Parameters\_Rev70+** to check SAP HANA parameters.</span></span>

![HANA\_Configuration\_Parameters\_Rev70+ para verificar parâmetros do SAP HANA](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

