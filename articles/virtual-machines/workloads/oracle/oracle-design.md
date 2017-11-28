---
title: aaaDesign e implementar um Oracle banco de dados no Azure | Microsoft Docs
description: Projete e implemente um banco de dados Oracle no seu ambiente do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="be6c3-103">Projete e implemente um banco de dados Oracle no Azure</span><span class="sxs-lookup"><span data-stu-id="be6c3-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="be6c3-104">Suposições</span><span class="sxs-lookup"><span data-stu-id="be6c3-104">Assumptions</span></span>

- <span data-ttu-id="be6c3-105">Você está planejando toomigrate um banco de dados Oracle de tooAzure local.</span><span class="sxs-lookup"><span data-stu-id="be6c3-105">You're planning toomigrate an Oracle database from on-premises tooAzure.</span></span>
- <span data-ttu-id="be6c3-106">Você tem uma compreensão de saudação várias métricas em relatórios AWR Oracle.</span><span class="sxs-lookup"><span data-stu-id="be6c3-106">You have an understanding of hello various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="be6c3-107">Você tem uma compreensão das linha de base do desempenho de aplicativo e da utilização da plataforma.</span><span class="sxs-lookup"><span data-stu-id="be6c3-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="be6c3-108">Metas</span><span class="sxs-lookup"><span data-stu-id="be6c3-108">Goals</span></span>

- <span data-ttu-id="be6c3-109">Entender como toooptimize sua implantação do Oracle no Azure.</span><span class="sxs-lookup"><span data-stu-id="be6c3-109">Understand how toooptimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="be6c3-110">Explorar as opções de ajuste de desempenho para um banco de dados Oracle em um ambiente do Azure.</span><span class="sxs-lookup"><span data-stu-id="be6c3-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="be6c3-111">Olá diferenças entre um local e a implementação do Azure</span><span class="sxs-lookup"><span data-stu-id="be6c3-111">hello differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="be6c3-112">A seguir estão algumas importantes tookeep coisas em mente ao migrar aplicativos tooAzure local.</span><span class="sxs-lookup"><span data-stu-id="be6c3-112">Following are some important things tookeep in mind when you're migrating on-premises applications tooAzure.</span></span> 

<span data-ttu-id="be6c3-113">Uma diferença importante é que, em uma implementação do Azure, recursos como VMs, discos e redes virtuais são compartilhados entre outros clientes.</span><span class="sxs-lookup"><span data-stu-id="be6c3-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="be6c3-114">Além disso, os recursos podem ser acelerados com base nos requisitos de saudação.</span><span class="sxs-lookup"><span data-stu-id="be6c3-114">In addition, resources can be throttled based on hello requirements.</span></span> <span data-ttu-id="be6c3-115">Em vez de nos concentrarmos no evitando falha MTBF (), Azure mais destina sobreviventes falha hello (MTTR).</span><span class="sxs-lookup"><span data-stu-id="be6c3-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving hello failure (MTTR).</span></span>

<span data-ttu-id="be6c3-116">Olá tabela a seguir lista algumas das diferenças de saudação entre uma implementação de local e uma implementação do Azure de um banco de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="be6c3-116">hello following table lists some of hello differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="be6c3-117">**Implementação local**</span><span class="sxs-lookup"><span data-stu-id="be6c3-117">**On-premises implementation**</span></span> | <span data-ttu-id="be6c3-118">**Implementação no Azure**</span><span class="sxs-lookup"><span data-stu-id="be6c3-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="be6c3-119">**Rede**</span><span class="sxs-lookup"><span data-stu-id="be6c3-119">**Networking**</span></span> |<span data-ttu-id="be6c3-120">LAN/WAN</span><span class="sxs-lookup"><span data-stu-id="be6c3-120">LAN/WAN</span></span>  |<span data-ttu-id="be6c3-121">SDN (Rede definida por software)</span><span class="sxs-lookup"><span data-stu-id="be6c3-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="be6c3-122">**Grupo de segurança**</span><span class="sxs-lookup"><span data-stu-id="be6c3-122">**Security group**</span></span> |<span data-ttu-id="be6c3-123">Ferramentas de restrições de IP/porta</span><span class="sxs-lookup"><span data-stu-id="be6c3-123">IP/port restriction tools</span></span> |[<span data-ttu-id="be6c3-124">NSG (Grupo de Segurança de Rede)</span><span class="sxs-lookup"><span data-stu-id="be6c3-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="be6c3-125">**Resiliência**</span><span class="sxs-lookup"><span data-stu-id="be6c3-125">**Resilience**</span></span> |<span data-ttu-id="be6c3-126">MTBF (tempo médio entre falhas)</span><span class="sxs-lookup"><span data-stu-id="be6c3-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="be6c3-127">MTTR (toorecovery tempo médio)</span><span class="sxs-lookup"><span data-stu-id="be6c3-127">MTTR (mean time toorecovery)</span></span>|
> | <span data-ttu-id="be6c3-128">**Manutenção planejada**</span><span class="sxs-lookup"><span data-stu-id="be6c3-128">**Planned maintenance**</span></span> |<span data-ttu-id="be6c3-129">Aplicação de patch/upgrades</span><span class="sxs-lookup"><span data-stu-id="be6c3-129">Patching/upgrades</span></span>|<span data-ttu-id="be6c3-130">[Conjuntos de disponibilidade](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (aplicação de patch/upgrades gerenciados pelo Azure)</span><span class="sxs-lookup"><span data-stu-id="be6c3-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="be6c3-131">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="be6c3-131">**Resource**</span></span> |<span data-ttu-id="be6c3-132">Dedicado</span><span class="sxs-lookup"><span data-stu-id="be6c3-132">Dedicated</span></span>  |<span data-ttu-id="be6c3-133">Compartilhado com outros clientes</span><span class="sxs-lookup"><span data-stu-id="be6c3-133">Shared with other clients</span></span>|
> | <span data-ttu-id="be6c3-134">**Regiões**</span><span class="sxs-lookup"><span data-stu-id="be6c3-134">**Regions**</span></span> |<span data-ttu-id="be6c3-135">Datacenters</span><span class="sxs-lookup"><span data-stu-id="be6c3-135">Datacenters</span></span> |[<span data-ttu-id="be6c3-136">Pares de regiões</span><span class="sxs-lookup"><span data-stu-id="be6c3-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="be6c3-137">**Armazenamento**</span><span class="sxs-lookup"><span data-stu-id="be6c3-137">**Storage**</span></span> |<span data-ttu-id="be6c3-138">SAN/discos físicos</span><span class="sxs-lookup"><span data-stu-id="be6c3-138">SAN/physical disks</span></span> |[<span data-ttu-id="be6c3-139">Armazenamento gerenciado pelo Azure</span><span class="sxs-lookup"><span data-stu-id="be6c3-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="be6c3-140">**Escala**</span><span class="sxs-lookup"><span data-stu-id="be6c3-140">**Scale**</span></span> |<span data-ttu-id="be6c3-141">Escala vertical</span><span class="sxs-lookup"><span data-stu-id="be6c3-141">Vertical scale</span></span> |<span data-ttu-id="be6c3-142">Escala horizontal</span><span class="sxs-lookup"><span data-stu-id="be6c3-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="be6c3-143">Requisitos</span><span class="sxs-lookup"><span data-stu-id="be6c3-143">Requirements</span></span>

- <span data-ttu-id="be6c3-144">Determine a taxa de tamanho e crescimento do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="be6c3-144">Determine hello database size and growth rate.</span></span>
- <span data-ttu-id="be6c3-145">Determine requisitos de IOPS hello, que você pode estimar com base em Oracle AWR relatórios ou outra ferramentas de monitoramento de rede.</span><span class="sxs-lookup"><span data-stu-id="be6c3-145">Determine hello IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="be6c3-146">Opções de configuração</span><span class="sxs-lookup"><span data-stu-id="be6c3-146">Configuration options</span></span>

<span data-ttu-id="be6c3-147">Há quatro áreas possíveis que você pode ajustar o desempenho de tooimprove em um ambiente do Azure:</span><span class="sxs-lookup"><span data-stu-id="be6c3-147">There are four potential areas that you can tune tooimprove performance in an Azure environment:</span></span>

- <span data-ttu-id="be6c3-148">Tamanho da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="be6c3-148">Virtual machine size</span></span>
- <span data-ttu-id="be6c3-149">Taxa de transferência de rede</span><span class="sxs-lookup"><span data-stu-id="be6c3-149">Network throughput</span></span>
- <span data-ttu-id="be6c3-150">Tipos e configurações de disco</span><span class="sxs-lookup"><span data-stu-id="be6c3-150">Disk types and configurations</span></span>
- <span data-ttu-id="be6c3-151">Configurações de cache de disco</span><span class="sxs-lookup"><span data-stu-id="be6c3-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="be6c3-152">Gerar um relatório AWR</span><span class="sxs-lookup"><span data-stu-id="be6c3-152">Generate an AWR report</span></span>

<span data-ttu-id="be6c3-153">Se você tiver um banco de dados Oracle existente e estiver planejando toomigrate tooAzure, você tem várias opções.</span><span class="sxs-lookup"><span data-stu-id="be6c3-153">If you have an existing an Oracle database and are planning toomigrate tooAzure, you have several options.</span></span> <span data-ttu-id="be6c3-154">Você pode executar Olá Oracle AWR relatório tooget Olá métricas (IOPS, Mbps, GiBs e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="be6c3-154">You can run hello Oracle AWR report tooget hello metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="be6c3-155">Em seguida, escolha Olá que VM com base nas métricas de saudação coletados.</span><span class="sxs-lookup"><span data-stu-id="be6c3-155">Then choose hello VM based on hello metrics that you collected.</span></span> <span data-ttu-id="be6c3-156">Ou você pode contatar a infra-estrutura team tooget semelhante de informações.</span><span class="sxs-lookup"><span data-stu-id="be6c3-156">Or you can contact your infrastructure team tooget similar information.</span></span>

<span data-ttu-id="be6c3-157">Considere a execução do relatório AWR durante cargas de trabalho regulares e de pico para poder comparar a diferença.</span><span class="sxs-lookup"><span data-stu-id="be6c3-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="be6c3-158">Com base nesses relatórios, você pode dimensionar Olá VMs com base na carga de trabalho média hello ou carga de trabalho máxima hello.</span><span class="sxs-lookup"><span data-stu-id="be6c3-158">Based on these reports, you can size hello VMs based on either hello average workload or hello maximum workload.</span></span>

<span data-ttu-id="be6c3-159">A seguir está um exemplo de como toogenerate um relatório AWR:</span><span class="sxs-lookup"><span data-stu-id="be6c3-159">Following is an example of how toogenerate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="be6c3-160">Métricas-chave</span><span class="sxs-lookup"><span data-stu-id="be6c3-160">Key metrics</span></span>

<span data-ttu-id="be6c3-161">Seguem as métricas de Olá Olá relatório AWR pode ser obtido:</span><span class="sxs-lookup"><span data-stu-id="be6c3-161">Following are hello metrics that you can obtain from hello AWR report:</span></span>

- <span data-ttu-id="be6c3-162">Número total de núcleos</span><span class="sxs-lookup"><span data-stu-id="be6c3-162">Total number of cores</span></span>
- <span data-ttu-id="be6c3-163">Velocidade de clock da CPU</span><span class="sxs-lookup"><span data-stu-id="be6c3-163">CPU clock speed</span></span>
- <span data-ttu-id="be6c3-164">Memória total em GB</span><span class="sxs-lookup"><span data-stu-id="be6c3-164">Total memory in GB</span></span>
- <span data-ttu-id="be6c3-165">Utilização da CPU</span><span class="sxs-lookup"><span data-stu-id="be6c3-165">CPU utilization</span></span>
- <span data-ttu-id="be6c3-166">Pico da taxa de transferência de dados</span><span class="sxs-lookup"><span data-stu-id="be6c3-166">Peak data transfer rate</span></span>
- <span data-ttu-id="be6c3-167">Taxa de alterações de E/S (leitura/gravação)</span><span class="sxs-lookup"><span data-stu-id="be6c3-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="be6c3-168">Taxa de log da fase refazer (MBPs)</span><span class="sxs-lookup"><span data-stu-id="be6c3-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="be6c3-169">Taxa de transferência de rede</span><span class="sxs-lookup"><span data-stu-id="be6c3-169">Network throughput</span></span>
- <span data-ttu-id="be6c3-170">Taxa de latência de rede (baixa/alta)</span><span class="sxs-lookup"><span data-stu-id="be6c3-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="be6c3-171">Tamanho do banco de dados em GB</span><span class="sxs-lookup"><span data-stu-id="be6c3-171">Database size in GB</span></span>
- <span data-ttu-id="be6c3-172">Bytes recebidos por meio do SQL * Net da / tooclient</span><span class="sxs-lookup"><span data-stu-id="be6c3-172">Bytes received via SQL*Net from/tooclient</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="be6c3-173">Tamanho da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="be6c3-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a><span data-ttu-id="be6c3-174">1. Estimar o tamanho da VM com base no uso de CPU, memória e e/s de saudação relatório AWR</span><span class="sxs-lookup"><span data-stu-id="be6c3-174">1. Estimate VM size based on CPU, memory, and I/O usage from hello AWR report</span></span>

<span data-ttu-id="be6c3-175">Uma coisa que você poderá examinar é Olá principais cinco atingiu o tempo em primeiro plano eventos que indicam onde estão os gargalos de sistema hello.</span><span class="sxs-lookup"><span data-stu-id="be6c3-175">One thing you might look at is hello top five timed foreground events that indicate where hello system bottlenecks are.</span></span>

<span data-ttu-id="be6c3-176">Por exemplo, em Olá diagrama a seguir, sincronização de arquivos de log de saudação é na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="be6c3-176">For example, in hello following diagram, hello log file sync is at hello top.</span></span> <span data-ttu-id="be6c3-177">Ele indica o número de saudação de esperas são necessários antes de saudação LGWR grava o arquivo de log de refazer Olá log buffer toohello.</span><span class="sxs-lookup"><span data-stu-id="be6c3-177">It indicates hello number of waits that are required before hello LGWR writes hello log buffer toohello redo log file.</span></span> <span data-ttu-id="be6c3-178">Esses resultados indicam que há a necessidade de armazenamento ou discos com um desempenho melhor.</span><span class="sxs-lookup"><span data-stu-id="be6c3-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="be6c3-179">Além disso, o diagrama de saudação também mostra número Olá da CPU (núcleos) e a quantidade de saudação de memória.</span><span class="sxs-lookup"><span data-stu-id="be6c3-179">In addition, hello diagram also shows hello number of CPU (cores) and hello amount of memory.</span></span>

![Captura de tela da página do relatório AWR Olá](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="be6c3-181">Olá diagrama a seguir mostra Olá total e/s de leitura e gravação.</span><span class="sxs-lookup"><span data-stu-id="be6c3-181">hello following diagram shows hello total I/O of read and write.</span></span> <span data-ttu-id="be6c3-182">Não havia 59 ler e 247.3 GB gravadas durante o tempo de saudação do relatório de saudação.</span><span class="sxs-lookup"><span data-stu-id="be6c3-182">There were 59 GB read and 247.3 GB written during hello time of hello report.</span></span>

![Captura de tela da página do relatório AWR Olá](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="be6c3-184">2. Escolher uma VM</span><span class="sxs-lookup"><span data-stu-id="be6c3-184">2. Choose a VM</span></span>

<span data-ttu-id="be6c3-185">Com base nas informações de saudação que você coletou da saudação relatório AWR, a saudação próxima etapa é toochoose uma VM de tamanho similar que atenda às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="be6c3-185">Based on hello information that you collected from hello AWR report, hello next step is toochoose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="be6c3-186">Você pode encontrar uma lista de VMs disponíveis no artigo Olá [otimizada de memória](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span><span class="sxs-lookup"><span data-stu-id="be6c3-186">You can find a list of available VMs in hello article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a><span data-ttu-id="be6c3-187">3. Ajustar tamanho da VM de saudação com uma série VM semelhante com base em Olá ACU</span><span class="sxs-lookup"><span data-stu-id="be6c3-187">3. Fine-tune hello VM sizing with a similar VM series based on hello ACU</span></span>

<span data-ttu-id="be6c3-188">Depois que você escolheu Olá VM, preste atenção toohello ACU para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="be6c3-188">After you've chosen hello VM, pay attention toohello ACU for hello VM.</span></span> <span data-ttu-id="be6c3-189">Você pode escolher uma VM diferente com base em Olá valor ACU que melhor atenda às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="be6c3-189">You might choose a different VM based on hello ACU value that better suits your requirements.</span></span> <span data-ttu-id="be6c3-190">Para saber mais, confira [Unidade de computação do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span><span class="sxs-lookup"><span data-stu-id="be6c3-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![Captura de tela da página de unidades ACU Olá](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="be6c3-192">Taxa de transferência de rede</span><span class="sxs-lookup"><span data-stu-id="be6c3-192">Network throughput</span></span>

<span data-ttu-id="be6c3-193">Olá diagrama a seguir mostra uma relação entre a taxa de transferência e IOPS hello:</span><span class="sxs-lookup"><span data-stu-id="be6c3-193">hello following diagram shows hello relation between throughput and IOPS:</span></span>

![Captura de tela da taxa de transferência](./media/oracle-design/throughput.png)

<span data-ttu-id="be6c3-195">taxa de transferência de rede total Olá é calculada com base em Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="be6c3-195">hello total network throughput is estimated based on hello following information:</span></span>
- <span data-ttu-id="be6c3-196">Tráfego SQL*Rede</span><span class="sxs-lookup"><span data-stu-id="be6c3-196">SQL*Net traffic</span></span>
- <span data-ttu-id="be6c3-197">MBps x número de servidores (fluxo de saída, como o Oracle Data Guard)</span><span class="sxs-lookup"><span data-stu-id="be6c3-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="be6c3-198">Outros fatores, como replicação de aplicativo</span><span class="sxs-lookup"><span data-stu-id="be6c3-198">Other factors, such as application replication</span></span>

![Captura de tela da saudação SQL * Net taxa de transferência](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="be6c3-200">Com base nos seus requisitos de largura de banda de rede, há vários tipos de gateway para você toochoose do.</span><span class="sxs-lookup"><span data-stu-id="be6c3-200">Based on your network bandwidth requirements, there are various gateway types for you toochoose from.</span></span> <span data-ttu-id="be6c3-201">Entre eles basic, VpnGw e Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="be6c3-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="be6c3-202">Para obter mais informações, consulte Olá [página de preços de gateway VPN](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span><span class="sxs-lookup"><span data-stu-id="be6c3-202">For more information, see hello [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="be6c3-203">**Recomendações**</span><span class="sxs-lookup"><span data-stu-id="be6c3-203">**Recommendations**</span></span>

- <span data-ttu-id="be6c3-204">Latência de rede é a implantação de local de tooan em comparação com o mais alto.</span><span class="sxs-lookup"><span data-stu-id="be6c3-204">Network latency is higher compared tooan on-premises deployment.</span></span> <span data-ttu-id="be6c3-205">Reduzir as viagens de ida e volta da rede pode melhorar significativamente o desempenho.</span><span class="sxs-lookup"><span data-stu-id="be6c3-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="be6c3-206">tooreduce viagens, consolidar aplicativos que têm transações alta ou aplicativos "tagarelas" em hello mesma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be6c3-206">tooreduce round-trips, consolidate applications that have high transactions or “chatty” apps on hello same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="be6c3-207">Tipos e configurações de disco</span><span class="sxs-lookup"><span data-stu-id="be6c3-207">Disk types and configurations</span></span>

- <span data-ttu-id="be6c3-208">*Discos padrão do SO*: esses tipos de disco oferecem dados persistentes e cache.</span><span class="sxs-lookup"><span data-stu-id="be6c3-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="be6c3-209">Eles são otimizados para acesso de SO na inicialização, e não foram projetados para cargas de trabalho transacionais ou de data warehouse (analíticas).</span><span class="sxs-lookup"><span data-stu-id="be6c3-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="be6c3-210">*Não gerenciado discos*: com esses tipos de disco, você gerenciar as contas de armazenamento de saudação que armazenam arquivos de disco rígido virtual (VHD) de saudação que correspondem a tooyour discos de VM.</span><span class="sxs-lookup"><span data-stu-id="be6c3-210">*Unmanaged disks*: With these disk types, you manage hello storage accounts that store hello virtual hard disk (VHD) files that correspond tooyour VM disks.</span></span> <span data-ttu-id="be6c3-211">Os arquivos VHD são armazenados como blobs de páginas nas contas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="be6c3-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="be6c3-212">*Discos gerenciado*: o Azure gerencia contas de armazenamento Olá que você pode usar para os discos VM.</span><span class="sxs-lookup"><span data-stu-id="be6c3-212">*Managed disks*: Azure manages hello storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="be6c3-213">Especifique o tipo de disco da saudação (padrão ou premium) e o tamanho de saudação do disco de saudação que você precisa.</span><span class="sxs-lookup"><span data-stu-id="be6c3-213">You specify hello disk type (premium or standard) and hello size of hello disk that you need.</span></span> <span data-ttu-id="be6c3-214">Azure cria e gerencia disco Olá para você.</span><span class="sxs-lookup"><span data-stu-id="be6c3-214">Azure creates and manages hello disk for you.</span></span>

- <span data-ttu-id="be6c3-215">*Discos de armazenamento premium*: esses tipos de disco são ideais para cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="be6c3-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="be6c3-216">Premium armazenamento dá suporte a discos de VM que podem ser anexado a série toospecific tamanho VMs, como as VMs da série DS, série DSv2, GS e F.</span><span class="sxs-lookup"><span data-stu-id="be6c3-216">Premium storage supports VM disks that can be attached toospecific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="be6c3-217">discos de premium Olá vem com tamanhos diferentes e você pode escolher entre os discos que variam de too4 de 32 GB, 096 GB.</span><span class="sxs-lookup"><span data-stu-id="be6c3-217">hello premium disk comes with different sizes, and you can choose between disks ranging from 32 GB too4,096 GB.</span></span> <span data-ttu-id="be6c3-218">Cada tamanho de disco tem suas próprias especificações de desempenho.</span><span class="sxs-lookup"><span data-stu-id="be6c3-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="be6c3-219">Dependendo dos requisitos de aplicativo, você pode anexar um ou mais discos tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="be6c3-219">Depending on your application requirements, you can attach one or more disks tooyour VM.</span></span>

<span data-ttu-id="be6c3-220">Quando você cria um novo disco gerenciado do portal hello, você pode escolher Olá **tipo de conta** para o tipo de saudação do disco que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="be6c3-220">When you create a new managed disk from hello portal, you can choose hello **Account type** for hello type of disk you want toouse.</span></span> <span data-ttu-id="be6c3-221">Tenha em mente que nem todos os discos disponíveis são mostrados no menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="be6c3-221">Keep in mind that not all available disks are shown in hello drop-down menu.</span></span> <span data-ttu-id="be6c3-222">Depois de escolher um tamanho VM específico, menu Olá mostra o armazenamento de premium disponível de saudação somente SKUs com base no tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="be6c3-222">After you choose a particular VM size, hello menu shows only hello available premium storage SKUs that are based on that VM size.</span></span>

![Captura de tela da página de disco gerenciado Olá](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="be6c3-224">Para saber mais, confira [Armazenamento Premium de alto desempenho e discos gerenciados para VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="be6c3-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="be6c3-225">Depois de configurar o armazenamento em uma máquina virtual, talvez você queira discos de saudação do tooload teste antes de criar um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="be6c3-225">After you configure your storage on a VM, you might want tooload test hello disks before creating a database.</span></span> <span data-ttu-id="be6c3-226">Saber a taxa de e/s de saudação em termos de latência e taxa de transferência pode ajudá-lo a determinar se o suportam a VMs Olá Olá esperado a produtividade com destinos de latência.</span><span class="sxs-lookup"><span data-stu-id="be6c3-226">Knowing hello I/O rate in terms of both latency and throughput can help you determine if hello VMs support hello expected throughput with latency targets.</span></span>

<span data-ttu-id="be6c3-227">Existem diversas ferramentas para realizar o teste de carga do aplicativo, como Oracle Orion, Sysbench e Fio.</span><span class="sxs-lookup"><span data-stu-id="be6c3-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="be6c3-228">Execute o teste de carga de saudação novamente depois que você implantou um banco de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="be6c3-228">Run hello load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="be6c3-229">Iniciar suas cargas de trabalho de pico e regulares e Olá Mostrar resultados Olá da linha de base do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="be6c3-229">Start your regular and peak workloads, and hello results show you hello baseline of your environment.</span></span>

<span data-ttu-id="be6c3-230">Talvez seja mais importante do armazenamento de saudação toosize com base na taxa de IOPS de saudação em vez de tamanho de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="be6c3-230">It might be more important toosize hello storage based on hello IOPS rate rather than hello storage size.</span></span> <span data-ttu-id="be6c3-231">Por exemplo, se Olá necessário IOPS é 5.000, mas você só precisa de 200 GB, discos de premium Olá P30 classe ainda pode obter, embora ele vem com mais de 200 GB de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="be6c3-231">For example, if hello required IOPS is 5,000, but you only need 200 GB, you might still get hello P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="be6c3-232">taxa de IOPS Olá pode ser obtida Olá relatório AWR.</span><span class="sxs-lookup"><span data-stu-id="be6c3-232">hello IOPS rate can be obtained from hello AWR report.</span></span> <span data-ttu-id="be6c3-233">Ele é determinado pelo log de refazer hello, leituras físicas e a taxa de gravações.</span><span class="sxs-lookup"><span data-stu-id="be6c3-233">It's determined by hello redo log, physical reads, and writes rate.</span></span>

![Captura de tela da página do relatório AWR Olá](./media/oracle-design/awr_report.png)

<span data-ttu-id="be6c3-235">Por exemplo, o tamanho de refazer Olá é 12,200,000 bytes por segundo, que é igual too11.63 MBPs.</span><span class="sxs-lookup"><span data-stu-id="be6c3-235">For example, hello redo size is 12,200,000 bytes per second, which is equal too11.63 MBPs.</span></span>
<span data-ttu-id="be6c3-236">Olá IOPS é 12,200,000 / 2,358 = 5,174.</span><span class="sxs-lookup"><span data-stu-id="be6c3-236">hello IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="be6c3-237">Depois de ter uma visão clara dos requisitos de e/s hello, você pode escolher uma combinação de unidades que são mais adequado toomeet esses requisitos.</span><span class="sxs-lookup"><span data-stu-id="be6c3-237">After you have a clear picture of hello I/O requirements, you can choose a combination of drives that are best suited toomeet those requirements.</span></span>

<span data-ttu-id="be6c3-238">**Recomendações**</span><span class="sxs-lookup"><span data-stu-id="be6c3-238">**Recommendations**</span></span>

- <span data-ttu-id="be6c3-239">Para dados de espaço de tabela, distribuir cargas de trabalho de e/s de saudação em um número de discos usando armazenamento gerenciado ou Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="be6c3-239">For data tablespace, spread hello I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="be6c3-240">À medida que aumenta o tamanho de bloco hello e/s para operações de leitura intensa e com uso intensivo de gravação, adicione mais discos de dados.</span><span class="sxs-lookup"><span data-stu-id="be6c3-240">As hello I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="be6c3-241">Aumente o tamanho do bloco Olá processos sequenciais grandes.</span><span class="sxs-lookup"><span data-stu-id="be6c3-241">Increase hello block size for large sequential processes.</span></span>
- <span data-ttu-id="be6c3-242">Use a e/s tooreduce de compactação de dados (para dados e índices).</span><span class="sxs-lookup"><span data-stu-id="be6c3-242">Use data compression tooreduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="be6c3-243">Separe os logs da fase refazer, sistema e temps e desfaça o TS em discos de dados separados.</span><span class="sxs-lookup"><span data-stu-id="be6c3-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="be6c3-244">Não coloque arquivos de aplicativo em discos do SO padrão (/dev/sda).</span><span class="sxs-lookup"><span data-stu-id="be6c3-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="be6c3-245">Esses discos são otimizados inicializações rápidas de VM, e talvez não forneçam um bom desempenho para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="be6c3-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="be6c3-246">Configurações de cache de disco</span><span class="sxs-lookup"><span data-stu-id="be6c3-246">Disk cache settings</span></span>

<span data-ttu-id="be6c3-247">Há três opções para o cache de host:</span><span class="sxs-lookup"><span data-stu-id="be6c3-247">There are three options for host caching:</span></span>

- <span data-ttu-id="be6c3-248">*Somente leitura*: todas as solicitações são armazenadas em cache para leituras futuras.</span><span class="sxs-lookup"><span data-stu-id="be6c3-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="be6c3-249">Todas as gravações são persistentes tooAzure diretamente o armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="be6c3-249">All writes are persisted directly tooAzure Blob storage.</span></span>

- <span data-ttu-id="be6c3-250">*Leitura e gravação*: este é um algoritmo de “leitura antecipada”.</span><span class="sxs-lookup"><span data-stu-id="be6c3-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="be6c3-251">Olá leituras e gravações em cache para futuras leituras.</span><span class="sxs-lookup"><span data-stu-id="be6c3-251">hello reads and writes are cached for future reads.</span></span> <span data-ttu-id="be6c3-252">Gravações de write-through não são persistidos cache local toohello primeiro.</span><span class="sxs-lookup"><span data-stu-id="be6c3-252">Non-write-through writes are persisted toohello local cache first.</span></span> <span data-ttu-id="be6c3-253">Para o SQL Server, gravações são persistente tooAzure armazenamento porque ela usa a gravação.</span><span class="sxs-lookup"><span data-stu-id="be6c3-253">For SQL Server, writes are persisted tooAzure Storage because it uses write-through.</span></span> <span data-ttu-id="be6c3-254">Ele também fornece o menor latência de disco Olá para cargas de trabalho leves.</span><span class="sxs-lookup"><span data-stu-id="be6c3-254">It also provides hello lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="be6c3-255">*Nenhum* (desabilitado): ao usar essa opção, você pode ignorar o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="be6c3-255">*None* (disabled): By using this option, you can bypass hello cache.</span></span> <span data-ttu-id="be6c3-256">Todos os dados de saudação toodisk transferido e persistentes tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="be6c3-256">All hello data is transferred toodisk and persisted tooAzure Storage.</span></span> <span data-ttu-id="be6c3-257">Isso proporciona método hello mais alta taxa de e/s para cargas de trabalho intensivas de e/s.</span><span class="sxs-lookup"><span data-stu-id="be6c3-257">This method gives you hello highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="be6c3-258">Você também precisa tootake "custo de transações" em consideração.</span><span class="sxs-lookup"><span data-stu-id="be6c3-258">You also need tootake “transaction cost” into consideration.</span></span>

<span data-ttu-id="be6c3-259">**Recomendações**</span><span class="sxs-lookup"><span data-stu-id="be6c3-259">**Recommendations**</span></span>

<span data-ttu-id="be6c3-260">taxa de transferência toomaximize hello, recomendamos que você inicie com **nenhum** para caching de host.</span><span class="sxs-lookup"><span data-stu-id="be6c3-260">toomaximize hello throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="be6c3-261">Para o armazenamento Premium, tenha em mente que você deve desabilitar barreiras"hello" ao montar o sistema de arquivos Olá Olá **ReadOnly** ou **nenhum** opções.</span><span class="sxs-lookup"><span data-stu-id="be6c3-261">For Premium Storage, keep in mind that you must disable hello "barriers" when you mount hello file system with hello **ReadOnly** or **None** options.</span></span> <span data-ttu-id="be6c3-262">Atualize arquivo /etc/fstab de saudação com discos de toohello UUID hello.</span><span class="sxs-lookup"><span data-stu-id="be6c3-262">Update hello /etc/fstab file with hello UUID toohello disks.</span></span>

<span data-ttu-id="be6c3-263">Para saber mais, veja [Armazenamento Premium para VMs Linux](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span><span class="sxs-lookup"><span data-stu-id="be6c3-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![Captura de tela da página de disco gerenciado Olá](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="be6c3-265">Para discos do sistema operacional, use o cache de **Leitura/Gravação** padrão.</span><span class="sxs-lookup"><span data-stu-id="be6c3-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="be6c3-266">Para SYSTEM, TEMP e UNDO, use **Nenhum** para o cache.</span><span class="sxs-lookup"><span data-stu-id="be6c3-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="be6c3-267">Para DATA, use **Nenhum** para armazenar em cache.</span><span class="sxs-lookup"><span data-stu-id="be6c3-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="be6c3-268">Porém, se o banco de dados for somente leitura ou leitura intensiva, use o cache de **Somente leitura**.</span><span class="sxs-lookup"><span data-stu-id="be6c3-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="be6c3-269">Depois que a configuração de disco de dados é salvo, você não pode alterar a configuração de cache de host de saudação, a menos que você desmontar a unidade de saudação em Olá nível do sistema operacional e, em seguida, remonte-lo depois de ter feito Olá alterar.</span><span class="sxs-lookup"><span data-stu-id="be6c3-269">After your data disk setting is saved, you can't change hello host cache setting unless you unmount hello drive at hello OS level and then remount it after you've made hello change.</span></span>


## <a name="security"></a><span data-ttu-id="be6c3-270">Segurança</span><span class="sxs-lookup"><span data-stu-id="be6c3-270">Security</span></span>

<span data-ttu-id="be6c3-271">Depois de você ter instalado e configurado o seu ambiente do Azure, Olá próxima etapa é toosecure sua rede.</span><span class="sxs-lookup"><span data-stu-id="be6c3-271">After you have set up and configured your Azure environment, hello next step is toosecure your network.</span></span> <span data-ttu-id="be6c3-272">Veja algumas recomendações:</span><span class="sxs-lookup"><span data-stu-id="be6c3-272">Here are some recommendations:</span></span>

- <span data-ttu-id="be6c3-273">*Política de NSG*: o NSG pode ser definido por uma sub-rede ou NIC.</span><span class="sxs-lookup"><span data-stu-id="be6c3-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="be6c3-274">É mais simples acesso toocontrol no nível de sub-rede Olá para segurança e forçar o roteamento para coisas como firewalls de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="be6c3-274">It's simpler toocontrol access at hello subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="be6c3-275">*Jumpbox*: para um acesso mais seguro, os administradores devem não conectar-se diretamente toohello serviço de aplicativo ou banco de dados.</span><span class="sxs-lookup"><span data-stu-id="be6c3-275">*Jumpbox*: For more secure access, administrators should not directly connect toohello application service or database.</span></span> <span data-ttu-id="be6c3-276">Um jumpbox é usado como uma mídia entre a máquina do administrador de saudação e recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="be6c3-276">A jumpbox is used as a media between hello administrator machine and Azure resources.</span></span>
<span data-ttu-id="be6c3-277">![Captura de tela da página de topologia Olá Jumpbox](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="be6c3-277">![Screenshot of hello Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="be6c3-278">máquina de administrador Olá deve oferecer acesso restrito por IP somente jumpbox de toohello.</span><span class="sxs-lookup"><span data-stu-id="be6c3-278">hello administrator machine should offer IP-restricted access toohello jumpbox only.</span></span> <span data-ttu-id="be6c3-279">Olá jumpbox deve ter acesso toohello aplicativo e banco de dados.</span><span class="sxs-lookup"><span data-stu-id="be6c3-279">hello jumpbox should have access toohello application and database.</span></span>

- <span data-ttu-id="be6c3-280">*Rede privada* (sub-redes): É recomendável que você tenha o serviço de aplicativo hello e banco de dados em sub-redes separadas, para melhor controle pode ser definido por diretiva NSG.</span><span class="sxs-lookup"><span data-stu-id="be6c3-280">*Private network* (subnets): We recommend that you have hello application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="be6c3-281">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="be6c3-281">Additional reading</span></span>

- [<span data-ttu-id="be6c3-282">Configurar o Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="be6c3-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="be6c3-283">Configurar o Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="be6c3-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="be6c3-284">Configurar o Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="be6c3-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="be6c3-285">Backup e recuperação do Oracle</span><span class="sxs-lookup"><span data-stu-id="be6c3-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="be6c3-286">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be6c3-286">Next steps</span></span>

- [<span data-ttu-id="be6c3-287">Tutorial: criar VMs altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="be6c3-287">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="be6c3-288">Explorar exemplos da CLI do Azure de implantação de VM</span><span class="sxs-lookup"><span data-stu-id="be6c3-288">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
