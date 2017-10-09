---
title: disponibilidade de aaaHigh para Hadoop - HDInsight do Azure | Microsoft Docs
description: "Saiba como clusters HDInsight melhoram a confiabilidade e a disponibilidade usando um nó principal adicional. Saiba como isso afeta os serviços Hadoop, como Ambari e Hive, bem como tooindividually conectar tooeach nó principal usando o SSH."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: alta disponibilidade hadoop
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a>Disponibilidade e confiabilidade dos clusters Hadoop em HDInsight

Clusters HDInsight fornecem duas disponibilidade de saudação tooincrease nós de cabeçalho e a confiabilidade dos serviços Hadoop e trabalhos em execução.

O Hadoop atinge a alta disponibilidade e confiabilidade replicando serviços e dados em múltiplos nós em um cluster. No entanto, em geral, as distribuições padrão do Hadoop têm apenas um único nó de cabeçalho. Qualquer interrupção do nó de cabeçalho único Olá pode fazer com que o trabalho de toostop cluster hello. HDInsight fornece disponibilidade e a confiabilidade do duas headnodes tooimprove Hadoop.

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="availability-and-reliability-of-nodes"></a>Disponibilidade e confiabilidade dos nós

Os nós em um cluster HDInsight são implementados com o uso de Máquinas Virtuais do Azure. Olá seções a seguir discutem os tipos de nós individuais Olá usados com HDInsight. 

> [!NOTE]
> Nem todos os tipos de nó são usados para um tipo de cluster. Por exemplo, um tipo de cluster Hadoop não tem nenhum nó Nimbus. Para obter mais informações sobre nós usado pelos tipos de cluster HDInsight, consulte a seção de tipos de Cluster de saudação do hello [Hadoop baseado em Linux criar clusters de HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) documento.

### <a name="head-nodes"></a>Nós de cabeçalho

a alta disponibilidade de serviços Hadoop tooensure, HDInsight fornece dois nós de cabeçalho. Ambos os nós de cabeçalho estão ativo e em execução no cluster do HDInsight Olá simultaneamente. Alguns serviços, como HDFS ou YARN, só estão “ativos” em um nó de cabeçalho a qualquer momento. Outros serviços, como HiveServer2 ou MetaStore Hive estão ativos em ambos os nós principal no hello simultaneamente.

Nós de cabeçalho (e outros nós no HDInsight) tem um valor numérico como parte do nome de host de saudação do nó de saudação. Por exemplo, `hn0-CLUSTERNAME` ou `hn4-CLUSTERNAME`.

> [!IMPORTANT]
> Não associe valor numérico Olá se um nó é primário ou secundário. valor numérico de saudação é tooprovide presente apenas um nome exclusivo para cada nó.

### <a name="nimbus-nodes"></a>Nós Nimbus

Nós Nimbus estão disponíveis nos clusters Storm. nós de Nimbus Olá fornecem semelhante funcionalidade toohello Hadoop JobTracker por distribuição e monitoramento de processamento entre nós de trabalho. O HDInsight oferece dois nós Nimbus para clusters Storm

### <a name="zookeeper-nodes"></a>Nós do Zookeeper

Os nós [ZooKeeper](http://zookeeper.apache.org/) são usados para eleição de líder de serviços mestres em nós principais. Eles também são usada tooinsure que serviços, nós de dados (trabalho) e gateways sabem qual nó principal mestra do serviço está ativa no. Por padrão, o HDInsight fornece três nós do ZooKeeper.

### <a name="worker-nodes"></a>Nós de trabalho

Nós de trabalho executam análise de dados reais de saudação quando um trabalho é enviado toohello cluster. Se um nó de trabalho falhar, a tarefa de saudação que estava executando é nó de trabalho tooanother enviados. Por padrão, o HDInsight cria quatro nós de trabalho. Você pode alterar esse número toosuit suas necessidades durante e após a criação do cluster.

### <a name="edge-node"></a>Nó de borda

Um nó de borda não participará na análise de dados em cluster Olá ativamente. Ele é usado por desenvolvedores ou cientistas de dados ao trabalhar com o Hadoop. Olá borda nó vidas em Olá mesma rede Virtual do Azure Olá outros nós no cluster hello e podem acessar diretamente a todos os outros nós. nó de borda Olá pode ser usado sem colocar recursos longe serviços críticos do Hadoop ou trabalhos de análise.

No momento, o servidor de R no HDInsight é Olá somente tipo de cluster que fornece um nó de borda padrão. Para o servidor do R no HDInsight, o nó de borda de saudação é usado o código de teste R localmente no nó de saudação antes do envio cluster toohello para processamento distribuído.

Para obter informações sobre o uso de um nó de borda com tipos de cluster que não seja o servidor de R, consulte Olá [usar nós de borda em HDInsight](hdinsight-apps-use-edge-node.md) documento.

## <a name="accessing-hello-nodes"></a>Acessar nós Olá

Cluster de toohello de acesso sobre Olá internet é fornecido por meio de um gateway público. O acesso é limitado tooconnecting toohello nós de cabeçalho e (se houver) Olá nó de borda. Acesso tooservices em execução em nós de cabeça Olá não é afetado por ter vários nós de cabeçalho. Olá gateway pública rotas solicitações toohello nó principal que hospeda Olá serviço solicitado. Por exemplo, se Ambari está hospedado no momento no nó de cabeçalho secundário hello, gateway Olá roteia solicitações de entrada para o nó de toothat Ambari.

O acesso por gateway pública Olá é limitado tooport 443 (HTTPS), 22 e 23.

* Porta __443__ é usado tooaccess Ambari e outros web interface do usuário ou APIs REST hospedadas em nós de cabeça hello.

* Porta __22__ é nó de cabeçalho principal usado tooaccess hello ou nó de borda com o SSH.

* Porta __23__ é usado tooaccess Olá secundário nó principal com SSH. Por exemplo, `ssh username@mycluster-ssh.azurehdinsight.net` conecta toohello nó primário de principal do cluster Olá denominado **mycluster**.

Para obter mais informações sobre como usar SSH, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

### <a name="internal-fully-qualified-domain-names-fqdn"></a>Nomes internos de domínio totalmente qualificado (FQDN)

Nós em um cluster HDInsight tem um endereço IP e o FQDN que só pode ser acessado do cluster Olá interno. Ao acessar serviços em cluster hello usando o endereço IP ou FQDN interno do hello, você deve usar o Ambari tooverify Olá IP ou FQDN toouse ao acessar o serviço de saudação.

Por exemplo, Olá Oozie serviço só pode ser executado em um nó principal e usando Olá `oozie` comando de uma sessão SSH requer o serviço de toohello Olá URL. Essa URL pode ser recuperado do Ambari usando Olá comando a seguir:

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

Esse comando retorna um toohello semelhante de valor a seguir de comando, que contém a saudação toouse interno de URL com hello `oozie` comando:

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

Para obter mais informações sobre como trabalhar com hello Ambari REST API, consulte [monitorar e gerenciar o HDInsight usando Olá API REST do Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).

### <a name="accessing-other-node-types"></a>Acessando outros tipos de nó

Você pode conectar toonodes que são não diretamente acessível via Olá internet usando Olá métodos a seguir:

* **SSH**: uma vez conectado tooa nó principal usando SSH, em seguida, você pode usar SSH de saudação nó principal tooconnect tooother nós Olá cluster. Para obter mais informações, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

* **Túnel SSH**: se você precisar tooaccess um serviço web hospedado em um de nós de saudação que não seja exposto toohello internet, você deve usar um túnel SSH. Para obter mais informações, consulte Olá [usar um túnel SSH com HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.

* **Rede Virtual do Azure**: se o HDInsight cluster faz parte de uma rede Virtual do Azure, qualquer recurso em Olá mesmo rede Virtual pode acessar todos os nós no cluster de saudação diretamente. Para obter mais informações, consulte Olá [HDInsight estender usando a rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md) documento.

## <a name="how-toocheck-on-a-service-status"></a>Como toocheck em um status de serviço

status de saudação toocheck de serviços que são executados em nós de cabeçalho Olá, use Olá Ambari Web UI ou Olá Ambari REST API.

### <a name="ambari-web-ui"></a>Interface do usuário da Ambari Web

Olá Ambari Web UI é visível em https://CLUSTERNAME.azurehdinsight.net. Substituir **CLUSTERNAME** com nome de saudação do cluster. Quando solicitado, insira as credenciais do usuário Olá HTTP para o cluster. nome de usuário saudação padrão HTTP é **admin** e a senha de saudação é Olá senha ao criar o cluster de saudação.

Ao chegar na página de Ambari hello, serviços Olá instalado estão listados Olá esquerda da página de saudação.

![Serviços instalados](./media/hdinsight-high-availability-linux/services.png)

Há uma série de ícones que podem aparecer próximo status de tooindicate do serviço tooa. Todos os alertas relacionados ao serviço tooa pode ser exibido usando Olá **alertas** link na parte superior de saudação da página de saudação. Você pode selecionar cada tooview de serviço para obter mais informações sobre ele.

Enquanto a página de serviço Olá fornece informações sobre o status de saudação e a configuração de cada serviço, ele não fornece informações em que está sendo executado no serviço de saudação do nó principal. tooview essa informações, use Olá **Hosts** link na parte superior de saudação da página de saudação. Esta página exibe os hosts no cluster hello, incluindo nós de cabeçalho hello.

![lista de hosts](./media/hdinsight-high-availability-linux/hosts.png)

Link de Olá selecionando para um de nós de cabeçalho de saudação exibe serviços hello e componentes em execução nesse nó.

![Status do componente](./media/hdinsight-high-availability-linux/nodeservices.png)

Para obter mais informações sobre como usar o Ambari, consulte [monitorar e gerenciar o HDInsight usando Olá da interface do usuário do Ambari Web](hdinsight-hadoop-manage-ambari.md).

### <a name="ambari-rest-api"></a>API REST do Ambari

Olá Ambari REST API está disponível por Olá internet. gateway público do HDInsight Olá manipula roteamento solicitações toohello nó principal que está hospedando Olá API REST.

Você pode usar o hello estado de saudação do comando toocheck de um serviço por meio de saudação Ambari API de REST a seguir:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* Substituir **senha** com a senha da conta de usuário (admin) Olá HTTP.
* Substituir **CLUSTERNAME** com o nome de saudação do cluster hello.
* Substituir **SERVICENAME** com o nome de saudação do serviço de saudação você deseja toocheck status de saudação do.

Por exemplo, o status de saudação toocheck de saudação **HDFS** serviço em um cluster denominado **mycluster**, com uma senha de **senha**, você usaria Olá comando a seguir:

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

resposta de saudação é semelhante toohello JSON a seguir:

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

Olá URL informa que o serviço hello está sendo executado em um nó de cabeçalho chamado **hn0 CLUSTERNAME**.

Olá estado informa que o serviço hello está sendo executado, ou **iniciado**.

Se você não souber quais serviços estão instalados no cluster hello, você pode usar o hello tooretrieve comando uma lista a seguir:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

Para obter mais informações sobre como trabalhar com hello Ambari REST API, consulte [monitorar e gerenciar o HDInsight usando Olá API REST do Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).

#### <a name="service-components"></a>Componentes do serviço

Serviços podem conter componentes que você deseja status Olá toocheck individualmente. Por exemplo, HDFS contém componente de NameNode de saudação. tooview informações em um componente, comando Olá seria:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

Se você não souber quais componentes são fornecidos por um serviço, você pode usar o hello tooretrieve comando uma lista a seguir:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a>Como tooaccess arquivos de log em nós de cabeçalho Olá

### <a name="ssh"></a>SSH

Ao nó de cabeçalho tooa conectados por meio do SSH, os arquivos de log podem ser encontrados em **/var/log**. Por exemplo, **/var/log/hadoop-yarn/yarn** contêm logs para YARN.

Cada nó de cabeçalho pode ter entradas de log exclusivo, por isso, você deve verificar Olá logs em ambos os.

### <a name="sftp"></a>SFTP

Você também pode conectar toohello nó principal usando Olá SSH File Transfer Protocol ou proteger arquivos Transfer Protocol (SFTP) e baixar os arquivos de log Olá diretamente.

Toousing semelhante um cliente SSH, ao se conectar a cluster toohello forneça Olá SSH usuário conta nome e Olá SSH o endereço de cluster hello. Por exemplo: `sftp username@mycluster-ssh.azurehdinsight.net`. Fornecer a senha de saudação conta hello quando solicitado, ou forneça uma chave pública usando Olá `-i` parâmetro.

Depois de conectado, você verá um prompt `sftp>` . Neste prompt, é possível alterar os diretórios, além de carregar e baixar arquivos. Por exemplo, a saudação comandos a seguir alterar diretórios toohello **/var/log/hadoop/hdfs** diretório e, em seguida, baixar todos os arquivos no diretório de saudação.

    cd /var/log/hadoop/hdfs
    get *

Para obter uma lista de comandos disponíveis, digite `help` em Olá `sftp>` prompt.

> [!NOTE]
> Também há interfaces gráficas que permitem que você toovisualize sistema de arquivos hello quando conectado usando SFTP. Por exemplo, [MobaXTerm](http://mobaxterm.mobatek.net/) permite sistema de arquivos de saudação toobrowse usando um tooWindows semelhantes da interface Explorer.

### <a name="ambari"></a>Ambari

> [!NOTE]
> usando o Ambari de arquivos de log de tooaccess, você deve usar um túnel SSH. interfaces de web Olá para serviços individuais Olá não são expostas publicamente Olá da Internet. Para obter informações sobre o uso de um túnel SSH, consulte Olá [Use SSH túnel](hdinsight-linux-ambari-ssh-tunnel.md) documento.

De saudação da interface do usuário do Ambari Web, selecione Serviço de saudação que deseja tooview logs (por exemplo, YARN). Em seguida, use **Links rápidos** tooselect registra quais Olá tooview de nó principal para.

![Usar rápida links tooview logs](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a>Como tooconfigure Olá tamanho de nó

tamanho de saudação de um nó só pode ser selecionado durante a criação do cluster. Você pode encontrar uma lista de saudação diferentes tamanhos VM disponíveis para HDInsight no hello [página de preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

Ao criar um cluster, você pode especificar o tamanho de saudação de nós de saudação. Olá informações a seguir fornecem orientação sobre como toospecify Olá tamanho usando Olá [portal do Azure][preview-portal], [Azure PowerShell][azure-powershell], e hello [CLI do Azure][azure-cli]:

* **Portal do Azure**: ao criar um cluster, você pode definir o tamanho de saudação de nós Olá usados pelo cluster hello:

    ![Imagem do Assistente de criação de cluster com a seleção de tamanho do nó](./media/hdinsight-high-availability-linux/headnodesize.png)

* **CLI do Azure**: ao usar o hello `azure hdinsight cluster create` de comando, você pode definir o tamanho de saudação do cabeçalho hello, trabalho e nós ZooKeeper usando Olá `--headNodeSize`, `--workerNodeSize`, e `--zookeeperNodeSize` parâmetros.

* **O Azure PowerShell**: ao usar o hello `New-AzureRmHDInsightCluster` cmdlet, você pode definir o tamanho de saudação do cabeçalho hello, trabalho e nós ZooKeeper usando Olá `-HeadNodeVMSize`, `-WorkerNodeSize`, e `-ZookeeperNodeSize` parâmetros.

## <a name="next-steps"></a>Próximas etapas

Use Olá seguindo os links toolearn mais coisas mencionados neste documento.

* [Referência REST do Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [Instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md)
* [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview)
* [Gerenciar clusters HDInsight usando o Ambari](hdinsight-hadoop-manage-ambari.md)
* [Provisionar os clusters HDInsight baseados em Linux](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
