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
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a>Monitorar clusters Hadoop em HDInsight usando Olá Ambari API
Saiba como toomonitor HDInsight clusters por meio de APIs do Ambari.

> [!NOTE]
> informações de saudação neste artigo são principalmente para clusters HDInsight baseados em Windows, que fornecem uma versão somente leitura do hello API REST do Ambari. Para clusters baseados em Linux, consulte [Gerenciar clusters do Hadoop usando Ambari](hdinsight-hadoop-manage-ambari.md).
> 
> 

## <a name="what-is-ambari"></a>O que é Ambari?
O [Apache Ambari][ambari-home] é usado para provisionar, gerenciar e monitorar clusters do Apache Hadoop. Ele inclui uma coleção de intuitiva das ferramentas de operador e um conjunto robusto de APIs que ocultam a complexidade de saudação do Hadoop, simplificando a operação de saudação de clusters. Para obter mais informações sobre Olá APIs, consulte [referência de API do Ambari][ambari-api-reference]. 

HDInsight atualmente suporta apenas Olá Ambari recurso de monitoramento. A API da Ambari v1.0 tem suporte pelos clusters HDInsight versões 3.0 e 2.1. Este artigo aborda o acesso às APIs da Ambari em clusters do HDInsight versões 3.1 e 2.1. Olá principal diferença entre Olá duas é que alguns dos componentes de saudação foram alteradas com introdução de saudação de novas funcionalidades (como Olá servidor de histórico de trabalho). 

**Pré-requisitos**

Antes de começar este tutorial, você deve ter Olá itens a seguir:

* **Uma estação de trabalho com o PowerShell do Azure**.
* (Opcional) [cURL][curl]. tooinstall, consulte [cURL versões e Downloads][curl-download].
  
  > [!NOTE]
  > Quando usa o comando de ondulação Olá no Windows, use aspas duplas em vez de aspas para valores de opção de saudação.
  > 
  > 
* **Um cluster Azure HDInsight**. Para obter informações sobre como provisionar um cluster, consulte [Introdução ao HDInsight][hdinsight-get-started] ou [Provisionar clusters HDInsight][hdinsight-provision]. Você precisa Olá toogo dados tutorial Olá a seguir:
  
  | Propriedade do cluster | Nome de variável do PowerShell do Azure | Valor | Descrição |
  | --- | --- | --- | --- |
  |   Nome do cluster HDInsight |$clusterName | |nome de saudação do seu cluster HDInsight. |
  |   Nome de usuário do cluster |$clusterUsername | |Nome de usuário de cluster especificado quando o cluster Olá foi criado. |
  |   Senha do cluster |$clusterPassword | |Senha do usuário do cluster. |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a>Início rápido
Há várias maneiras de clusters de HDInsight toouse Ambari toomonitor.

**Usar o Azure PowerShell**

Olá script do PowerShell do Azure a seguir obtém informações de rastreador do trabalho de MapReduce Olá *em um cluster HDInsight 3.5.*  Olá principal diferença é que podemos pull esses detalhes do serviço YARN hello (em vez de MapReduce).

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

saudação de script do PowerShell a seguir obtém informações de rastreador do trabalho de MapReduce Olá *em um cluster HDInsight 2.1*:

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

saída de Hello é:

![Saída de jobtracker][img-jobtracker-output]

**Usar cURL**

Olá exemplo a seguir obtém informações de cluster usando ondulação:

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

saída de Hello é:

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

**Versão de 8/10/2014 Olá**:

Quando usar Olá Ambari ponto de extremidade, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", Olá *host_name* campo Retorna o nome de domínio totalmente qualificado (FQDN) saudação do nó de saudação em vez do nome de host de saudação. Antes do lançamento de 8/10/2014 hello, este exemplo retornado simplesmente "**headnode0**". Após o lançamento de 8/10/2014 hello, você obtém Olá FQDN "**headnode0. { ClusterDNS} .azurehdinsight .net**", conforme mostrado no exemplo anterior de saudação. Essa alteração foi necessária toofacilitate cenários onde vários tipos de cluster (por exemplo, HBase e Hadoop) podem ser implantados em uma rede virtual (VNET). Isso acontece, por exemplo, ao usar HBase como uma plataforma de back-end para o Hadoop.

## <a name="ambari-monitoring-apis"></a>APIs de monitoramento da Ambari
Olá tabela a seguir lista alguns hello mais comuns Ambari monitoramentos de chamadas de API. Para obter mais informações sobre Olá API, consulte [referência de API do Ambari][ambari-api-reference].

| Monitorar a chamada de API | URI | Descrição |
| --- | --- | --- |
| Obter clusters |`/api/v1/clusters` | |
| Obter informações do cluster. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |clusters, serviços, hosts |
| Obter serviços |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |O serviços incluem: hdfs, mapreduce |
| Obter informações dos serviços. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| Obter componentes do serviço |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker |
| Obter informações do componente. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |ServiceComponentInfo, host-components, métricas |
| Obter hosts |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |headnode0, workernode0 |
| Obter informações do host. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| Obter componentes do host |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |namenode, resourcemanager |
| Obter informações de componente do host. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |HostRoles, componente, host, métrica |
| Obter configurações |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |Tipos de configuração: core-site, hdfs-site, mapred-site, hive-site |
| Obter informações de configuração. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |Tipos de configuração: core-site, hdfs-site, mapred-site, hive-site |

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu como chamadas de API de monitoramento do Ambari toouse. toolearn mais, consulte:

* [Gerenciar clusters de HDInsight usando Olá portal do Azure][hdinsight-admin-portal]
* [Gerenciar clusters HDInsight usando o Azure PowerShell][hdinsight-admin-powershell]
* [Gerenciar clusters HDInsight usando a interface de linha de comando][hdinsight-admin-cli]
* [Documentação do HDInsight][hdinsight-documentation]
* [Introdução ao HDInsight][hdinsight-get-started]

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
