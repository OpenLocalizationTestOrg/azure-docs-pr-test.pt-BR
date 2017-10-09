---
title: "dados de aaaCollect de CollectD na análise de Log do OMS | Microsoft Docs"
description: "CollectD é um daemon do Linux de software livre que coleta periodicamente dados de aplicativos e informações de nível de sistema.  Este artigo fornece informações sobre a coleta de dados do CollectD no Log Analytics."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="11280-104">Coletar dados do CollectD em agentes do Linux no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="11280-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="11280-105">O [CollectD](https://collectd.org/) é um daemon do Linux de software livre que coleta periodicamente métricas de desempenho de aplicativos e informações de nível de sistema.</span><span class="sxs-lookup"><span data-stu-id="11280-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="11280-106">Aplicativos de exemplo incluem Nginx, Olá Máquina Virtual Java (JVM) e do MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="11280-106">Example applications include hello Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="11280-107">Este artigo fornece informações sobre a coleta de dados de desempenho do CollectD no Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="11280-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="11280-108">Uma lista completa de plug-ins disponíveis pode ser encontrada na [Tabela de Plug-ins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="11280-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![Visão geral do CollectD](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="11280-110">Olá CollectD configuração a seguir está incluída no hello agente do OMS para Linux tooroute CollectD dados toohello agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="11280-110">hello following CollectD configuration is included in hello OMS Agent for Linux tooroute  CollectD data toohello OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="11280-111">Além disso, se usando um versões collectD antes 5.5 usar Olá seguinte configuração em vez disso.</span><span class="sxs-lookup"><span data-stu-id="11280-111">Additionally, if using an versions of collectD before 5.5 use hello following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="11280-112">configuração de CollectD Olá usa o padrão de saudação`write_http` dados métrica de desempenho do toosend de plug-in pela porta 26000 tooOMS agente para Linux.</span><span class="sxs-lookup"><span data-stu-id="11280-112">hello CollectD configuration uses hello default`write_http` plugin toosend performance metric data over port 26000 tooOMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="11280-113">Essa porta pode ser configurado tooa personalizadas se necessário.</span><span class="sxs-lookup"><span data-stu-id="11280-113">This port can be configured tooa custom-defined port if needed.</span></span>

<span data-ttu-id="11280-114">Olá agente do OMS para Linux também escuta na porta 26000 CollectD métricas e converte-os tooOMS métricas de esquema.</span><span class="sxs-lookup"><span data-stu-id="11280-114">hello OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them tooOMS schema metrics.</span></span> <span data-ttu-id="11280-115">Olá, a seguir é hello agente do OMS para Linux configuração `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="11280-115">hello following is hello OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="11280-116">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="11280-116">Versions supported</span></span>
- <span data-ttu-id="11280-117">O Log Analytics dá suporte atualmente às versões 4.8 e superiores do CollectD.</span><span class="sxs-lookup"><span data-stu-id="11280-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="11280-118">O Agente do OMS para Linux v1.1.0-217 ou superior é necessário para coleta de métrica do CollectD.</span><span class="sxs-lookup"><span data-stu-id="11280-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="11280-119">Configuração</span><span class="sxs-lookup"><span data-stu-id="11280-119">Configuration</span></span>
<span data-ttu-id="11280-120">Olá seguem coleção de tooconfigure etapas básicas de CollectD dados na análise de Log.</span><span class="sxs-lookup"><span data-stu-id="11280-120">hello following are basic steps tooconfigure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="11280-121">Configure CollectD toosend dados toohello agente do OMS para Linux usando o plug-in do hello write_http.</span><span class="sxs-lookup"><span data-stu-id="11280-121">Configure CollectD toosend data toohello OMS Agent for Linux using hello write_http plugin.</span></span>  
2. <span data-ttu-id="11280-122">Configure hello agente do OMS para Linux toolisten para Olá CollectD dados na porta apropriada hello.</span><span class="sxs-lookup"><span data-stu-id="11280-122">Configure hello OMS Agent for Linux toolisten for hello CollectD data on hello appropriate port.</span></span>
3. <span data-ttu-id="11280-123">Reinicie o CollectD e o Agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="11280-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-tooforward-data"></a><span data-ttu-id="11280-124">Configurar CollectD tooforward dados</span><span class="sxs-lookup"><span data-stu-id="11280-124">Configure CollectD tooforward data</span></span> 

1. <span data-ttu-id="11280-125">tooroute CollectD dados toohello agente do OMS para Linux, `oms.conf` necessidades toobe adicionado o diretório de configuração do tooCollectD.</span><span class="sxs-lookup"><span data-stu-id="11280-125">tooroute CollectD data toohello OMS Agent for Linux, `oms.conf` needs toobe added tooCollectD's configuration directory.</span></span> <span data-ttu-id="11280-126">destino de saudação do arquivo depende Olá distribuição de Linux de sua máquina.</span><span class="sxs-lookup"><span data-stu-id="11280-126">hello destination of this file depends on hello Linux  distro of your machine.</span></span>

    <span data-ttu-id="11280-127">Se o diretório de configuração CollectD está localizado em /etc/collectd.d/:</span><span class="sxs-lookup"><span data-stu-id="11280-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="11280-128">Se o diretório de configuração CollectD está localizado em /etc/collectd/collectd.conf.d/:</span><span class="sxs-lookup"><span data-stu-id="11280-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="11280-129">Para versões CollectD antes 5.5 terá marcas de saudação toomodify `oms.conf` como mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="11280-129">For CollectD versions before 5.5 you will have toomodify hello tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="11280-130">Copie o diretório de configuração omsagent collectd.conf toohello desejado do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="11280-130">Copy collectd.conf toohello desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="11280-131">Reinicie o CollectD e o agente do OMS para Linux com hello comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="11280-131">Restart CollectD and OMS Agent for Linux with hello following commands.</span></span>

    <span data-ttu-id="11280-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="11280-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a><span data-ttu-id="11280-133">Métricas de CollectD tooLog conversão do esquema de análise</span><span class="sxs-lookup"><span data-stu-id="11280-133">CollectD metrics tooLog Analytics schema conversion</span></span>
<span data-ttu-id="11280-134">toomaintain um modelo familiar entre as métricas de infraestrutura já coletados pelo agente do OMS para Linux e hello novas métricas coletadas pelo CollectD Olá mapeamento de esquema a seguir é usado:</span><span class="sxs-lookup"><span data-stu-id="11280-134">toomaintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and hello new metrics collected by CollectD hello following schema mapping is used:</span></span>

| <span data-ttu-id="11280-135">Campo Métrica do CollectD</span><span class="sxs-lookup"><span data-stu-id="11280-135">CollectD Metric field</span></span> | <span data-ttu-id="11280-136">Campo Log Analytics</span><span class="sxs-lookup"><span data-stu-id="11280-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="11280-137">host</span><span class="sxs-lookup"><span data-stu-id="11280-137">host</span></span> | <span data-ttu-id="11280-138">Computador</span><span class="sxs-lookup"><span data-stu-id="11280-138">Computer</span></span> |
| <span data-ttu-id="11280-139">plug-in</span><span class="sxs-lookup"><span data-stu-id="11280-139">plugin</span></span> | <span data-ttu-id="11280-140">Nenhum</span><span class="sxs-lookup"><span data-stu-id="11280-140">None</span></span> |
| <span data-ttu-id="11280-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="11280-141">plugin_instance</span></span> | <span data-ttu-id="11280-142">Nome da Instância</span><span class="sxs-lookup"><span data-stu-id="11280-142">Instance Name</span></span><br><span data-ttu-id="11280-143">Se **plugin_instance** é *null*, então InstanceName="*_Total*"</span><span class="sxs-lookup"><span data-stu-id="11280-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="11280-144">type</span><span class="sxs-lookup"><span data-stu-id="11280-144">type</span></span> | <span data-ttu-id="11280-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="11280-145">ObjectName</span></span> |
| <span data-ttu-id="11280-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="11280-146">type_instance</span></span> | <span data-ttu-id="11280-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="11280-147">CounterName</span></span><br><span data-ttu-id="11280-148">Se **type_instance** é *null*, então CounterName=**blank**</span><span class="sxs-lookup"><span data-stu-id="11280-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="11280-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="11280-149">dsnames[]</span></span> | <span data-ttu-id="11280-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="11280-150">CounterName</span></span> |
| <span data-ttu-id="11280-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="11280-151">dstypes</span></span> | <span data-ttu-id="11280-152">Nenhum</span><span class="sxs-lookup"><span data-stu-id="11280-152">None</span></span> |
| <span data-ttu-id="11280-153">values[]</span><span class="sxs-lookup"><span data-stu-id="11280-153">values[]</span></span> | <span data-ttu-id="11280-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="11280-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="11280-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11280-155">Next steps</span></span>
* <span data-ttu-id="11280-156">Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções.</span><span class="sxs-lookup"><span data-stu-id="11280-156">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="11280-157">Use [campos personalizados](log-analytics-custom-fields.md) tooparse dados de registros de syslog em campos individuais.</span><span class="sxs-lookup"><span data-stu-id="11280-157">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>

