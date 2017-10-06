---
title: "aaaMonitor clusters de Hadoop no HDInsight usando Olá Ambari API - Azure | Microsoft Docs"
description: "Use Olá Apache Ambari APIs para criar, gerenciar e monitorar clusters Hadoop. Operador intuitivo ferramentas e APIs ocultar a complexidade de saudação do Hadoop."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: d61a8aae5ddfcd7d44f2e4cc899e0a4da5e5fdcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a><span data-ttu-id="0ad2f-104">Monitorar clusters Hadoop em HDInsight usando Olá Ambari API</span><span class="sxs-lookup"><span data-stu-id="0ad2f-104">Monitor Hadoop clusters in HDInsight using hello Ambari API</span></span>
<span data-ttu-id="0ad2f-105">Saiba como toomonitor HDInsight clusters por meio de APIs do Ambari.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-105">Learn how toomonitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="0ad2f-106">informações de saudação neste artigo são principalmente para clusters HDInsight baseados em Windows, que fornecem uma versão somente leitura do hello API REST do Ambari.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-106">hello information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of hello Ambari REST API.</span></span> <span data-ttu-id="0ad2f-107">Para clusters baseados em Linux, consulte [Gerenciar clusters do Hadoop usando Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="0ad2f-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="0ad2f-108">O que é Ambari?</span><span class="sxs-lookup"><span data-stu-id="0ad2f-108">What is Ambari?</span></span>
<span data-ttu-id="0ad2f-109">O [Apache Ambari][ambari-home] é usado para provisionar, gerenciar e monitorar clusters do Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="0ad2f-110">Ele inclui uma coleção de intuitiva das ferramentas de operador e um conjunto robusto de APIs que ocultam a complexidade de saudação do Hadoop, simplificando a operação de saudação de clusters.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide hello complexity of Hadoop, simplifying hello operation of clusters.</span></span> <span data-ttu-id="0ad2f-111">Para obter mais informações sobre Olá APIs, consulte [referência de API do Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="0ad2f-111">For more information about hello APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="0ad2f-112">HDInsight atualmente suporta apenas Olá Ambari recurso de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-112">HDInsight currently supports only hello Ambari monitoring feature.</span></span> <span data-ttu-id="0ad2f-113">A API da Ambari v1.0 tem suporte pelos clusters HDInsight versões 3.0 e 2.1.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="0ad2f-114">Este artigo aborda o acesso às APIs da Ambari em clusters do HDInsight versões 3.1 e 2.1.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="0ad2f-115">Olá principal diferença entre Olá duas é que alguns dos componentes de saudação foram alteradas com introdução de saudação de novas funcionalidades (como Olá servidor de histórico de trabalho).</span><span class="sxs-lookup"><span data-stu-id="0ad2f-115">hello key difference between hello two is that some of hello components have changed with hello introduction of new capabilities (such as hello Job History Server).</span></span> 

<span data-ttu-id="0ad2f-116">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="0ad2f-116">**Prerequisites**</span></span>

<span data-ttu-id="0ad2f-117">Antes de começar este tutorial, você deve ter Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ad2f-117">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="0ad2f-118">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="0ad2f-119">(Opcional) [cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="0ad2f-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="0ad2f-120">tooinstall, consulte [cURL versões e Downloads][curl-download].</span><span class="sxs-lookup"><span data-stu-id="0ad2f-120">tooinstall it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="0ad2f-121">Quando usa o comando de ondulação Olá no Windows, use aspas duplas em vez de aspas para valores de opção de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-121">When use hello cURL command in Windows, use double-quotation marks instead of single-quotation marks for hello option values.</span></span>
  > 
  > 
* <span data-ttu-id="0ad2f-122">**Um cluster Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="0ad2f-123">Para obter informações sobre como provisionar um cluster, consulte [Introdução ao HDInsight][hdinsight-get-started] ou [Provisionar clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="0ad2f-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="0ad2f-124">Você precisa Olá toogo dados tutorial Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ad2f-124">You need hello following data toogo through hello tutorial:</span></span>
  
  | <span data-ttu-id="0ad2f-125">Propriedade do cluster</span><span class="sxs-lookup"><span data-stu-id="0ad2f-125">Cluster property</span></span> | <span data-ttu-id="0ad2f-126">Nome de variável do PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="0ad2f-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="0ad2f-127">Valor</span><span class="sxs-lookup"><span data-stu-id="0ad2f-127">Value</span></span> | <span data-ttu-id="0ad2f-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="0ad2f-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="0ad2f-129">Nome do cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ad2f-129">HDInsight cluster name</span></span> |<span data-ttu-id="0ad2f-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="0ad2f-130">$clusterName</span></span> | |<span data-ttu-id="0ad2f-131">nome de saudação do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-131">hello name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="0ad2f-132">Nome de usuário do cluster</span><span class="sxs-lookup"><span data-stu-id="0ad2f-132">Cluster username</span></span> |<span data-ttu-id="0ad2f-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="0ad2f-133">$clusterUsername</span></span> | |<span data-ttu-id="0ad2f-134">Nome de usuário de cluster especificado quando o cluster Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-134">Cluster user name specified when hello cluster was created.</span></span> |
  |   <span data-ttu-id="0ad2f-135">Senha do cluster</span><span class="sxs-lookup"><span data-stu-id="0ad2f-135">Cluster password</span></span> |<span data-ttu-id="0ad2f-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="0ad2f-136">$clusterPassword</span></span> | |<span data-ttu-id="0ad2f-137">Senha do usuário do cluster.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="0ad2f-138">Início rápido</span><span class="sxs-lookup"><span data-stu-id="0ad2f-138">Jump-start</span></span>
<span data-ttu-id="0ad2f-139">Há várias maneiras de clusters de HDInsight toouse Ambari toomonitor.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-139">There are several ways toouse Ambari toomonitor HDInsight clusters.</span></span>

<span data-ttu-id="0ad2f-140">**Usar o Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="0ad2f-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="0ad2f-141">Olá script do PowerShell do Azure a seguir obtém informações de rastreador do trabalho de MapReduce Olá *em um cluster HDInsight 3.5.*</span><span class="sxs-lookup"><span data-stu-id="0ad2f-141">hello following Azure PowerShell script gets hello MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="0ad2f-142">Olá principal diferença é que podemos pull esses detalhes do serviço YARN hello (em vez de MapReduce).</span><span class="sxs-lookup"><span data-stu-id="0ad2f-142">hello key difference is that we pull these details from hello YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="0ad2f-143">saudação de script do PowerShell a seguir obtém informações de rastreador do trabalho de MapReduce Olá *em um cluster HDInsight 2.1*:</span><span class="sxs-lookup"><span data-stu-id="0ad2f-143">hello following PowerShell script gets hello MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="0ad2f-144">saída de Hello é:</span><span class="sxs-lookup"><span data-stu-id="0ad2f-144">hello output is:</span></span>

![Saída de jobtracker][img-jobtracker-output]

<span data-ttu-id="0ad2f-146">**Usar cURL**</span><span class="sxs-lookup"><span data-stu-id="0ad2f-146">**Use cURL**</span></span>

<span data-ttu-id="0ad2f-147">Olá exemplo a seguir obtém informações de cluster usando ondulação:</span><span class="sxs-lookup"><span data-stu-id="0ad2f-147">hello following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="0ad2f-148">saída de Hello é:</span><span class="sxs-lookup"><span data-stu-id="0ad2f-148">hello output is:</span></span>

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

<span data-ttu-id="0ad2f-149">**Versão de 8/10/2014 Olá**:</span><span class="sxs-lookup"><span data-stu-id="0ad2f-149">**For hello 10/8/2014 release**:</span></span>

<span data-ttu-id="0ad2f-150">Quando usar Olá Ambari ponto de extremidade, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", Olá *host_name* campo Retorna o nome de domínio totalmente qualificado (FQDN) saudação do nó de saudação em vez do nome de host de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-150">When using hello Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* field returns hello fully qualified domain name (FQDN) of hello node instead of hello host name.</span></span> <span data-ttu-id="0ad2f-151">Antes do lançamento de 8/10/2014 hello, este exemplo retornado simplesmente "**headnode0**".</span><span class="sxs-lookup"><span data-stu-id="0ad2f-151">Before hello 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="0ad2f-152">Após o lançamento de 8/10/2014 hello, você obtém Olá FQDN "**headnode0. { ClusterDNS} .azurehdinsight .net**", conforme mostrado no exemplo anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-152">After hello 10/8/2014 release, you get hello FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in hello previous example.</span></span> <span data-ttu-id="0ad2f-153">Essa alteração foi necessária toofacilitate cenários onde vários tipos de cluster (por exemplo, HBase e Hadoop) podem ser implantados em uma rede virtual (VNET).</span><span class="sxs-lookup"><span data-stu-id="0ad2f-153">This change was required toofacilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="0ad2f-154">Isso acontece, por exemplo, ao usar HBase como uma plataforma de back-end para o Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="0ad2f-155">APIs de monitoramento da Ambari</span><span class="sxs-lookup"><span data-stu-id="0ad2f-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="0ad2f-156">Olá tabela a seguir lista alguns hello mais comuns Ambari monitoramentos de chamadas de API.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-156">hello following table lists some of hello most common Ambari monitoring API calls.</span></span> <span data-ttu-id="0ad2f-157">Para obter mais informações sobre Olá API, consulte [referência de API do Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="0ad2f-157">For more information about hello API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="0ad2f-158">Monitorar a chamada de API</span><span class="sxs-lookup"><span data-stu-id="0ad2f-158">Monitor API call</span></span> | <span data-ttu-id="0ad2f-159">URI</span><span class="sxs-lookup"><span data-stu-id="0ad2f-159">URI</span></span> | <span data-ttu-id="0ad2f-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="0ad2f-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ad2f-161">Obter clusters</span><span class="sxs-lookup"><span data-stu-id="0ad2f-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="0ad2f-162">Obter informações do cluster.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="0ad2f-163">clusters, serviços, hosts</span><span class="sxs-lookup"><span data-stu-id="0ad2f-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="0ad2f-164">Obter serviços</span><span class="sxs-lookup"><span data-stu-id="0ad2f-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="0ad2f-165">O serviços incluem: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="0ad2f-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="0ad2f-166">Obter informações dos serviços.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="0ad2f-167">Obter componentes do serviço</span><span class="sxs-lookup"><span data-stu-id="0ad2f-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="0ad2f-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="0ad2f-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="0ad2f-169">Obter informações do componente.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="0ad2f-170">ServiceComponentInfo, host-components, métricas</span><span class="sxs-lookup"><span data-stu-id="0ad2f-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="0ad2f-171">Obter hosts</span><span class="sxs-lookup"><span data-stu-id="0ad2f-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="0ad2f-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="0ad2f-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="0ad2f-173">Obter informações do host.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="0ad2f-174">Obter componentes do host</span><span class="sxs-lookup"><span data-stu-id="0ad2f-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="0ad2f-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="0ad2f-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="0ad2f-176">Obter informações de componente do host.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="0ad2f-177">HostRoles, componente, host, métrica</span><span class="sxs-lookup"><span data-stu-id="0ad2f-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="0ad2f-178">Obter configurações</span><span class="sxs-lookup"><span data-stu-id="0ad2f-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="0ad2f-179">Tipos de configuração: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="0ad2f-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="0ad2f-180">Obter informações de configuração.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="0ad2f-181">Tipos de configuração: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="0ad2f-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0ad2f-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0ad2f-182">Next Steps</span></span>
<span data-ttu-id="0ad2f-183">Agora que você aprendeu como chamadas de API de monitoramento do Ambari toouse.</span><span class="sxs-lookup"><span data-stu-id="0ad2f-183">Now you have learned how toouse Ambari monitoring API calls.</span></span> <span data-ttu-id="0ad2f-184">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="0ad2f-184">toolearn more, see:</span></span>

* <span data-ttu-id="0ad2f-185">[Gerenciar clusters de HDInsight usando Olá portal do Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="0ad2f-185">[Manage HDInsight clusters using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="0ad2f-186">[Gerenciar clusters HDInsight usando o Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="0ad2f-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="0ad2f-187">[Gerenciar clusters HDInsight usando a interface de linha de comando][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="0ad2f-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="0ad2f-188">[Documentação do HDInsight][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="0ad2f-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="0ad2f-189">[Introdução ao HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="0ad2f-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[img-jobtracker-output]: ./media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png
