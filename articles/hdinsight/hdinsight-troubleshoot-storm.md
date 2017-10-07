---
title: aaaTroubleshoot Storm usando o Azure HDInsight | Microsoft Docs
description: Obter respostas a perguntas toocommon sobre o uso do Apache Storm com HDInsight do Azure.
keywords: "Azure HDInsight, Storm, perguntas frequentes, guia de solução de problemas, problemas comuns"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="3d506-104">Solucionar problemas do Storm usando o Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3d506-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="3d506-105">Saiba mais sobre questões hello e suas resoluções para trabalhar com cargas do Apache Storm no Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="3d506-105">Learn about hello top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a><span data-ttu-id="3d506-106">Como acessar o hello profusão de interface do usuário em um cluster</span><span class="sxs-lookup"><span data-stu-id="3d506-106">How do I access hello Storm UI on a cluster</span></span>
<span data-ttu-id="3d506-107">Você tem duas opções para acessar Olá profusão de interface do usuário em um navegador:</span><span class="sxs-lookup"><span data-stu-id="3d506-107">You have two options for accessing hello Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="3d506-108">Interface do usuário do Ambari</span><span class="sxs-lookup"><span data-stu-id="3d506-108">Ambari UI</span></span>
1. <span data-ttu-id="3d506-109">Vá toohello Ambari painel.</span><span class="sxs-lookup"><span data-stu-id="3d506-109">Go toohello Ambari dashboard.</span></span>
2. <span data-ttu-id="3d506-110">Na lista de saudação de serviços, selecione **Storm**.</span><span class="sxs-lookup"><span data-stu-id="3d506-110">In hello list of services, select **Storm**.</span></span>
3. <span data-ttu-id="3d506-111">Em Olá **Links rápidos** menu, selecione **profusão de interface do usuário**.</span><span class="sxs-lookup"><span data-stu-id="3d506-111">In hello **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="3d506-112">Link direto</span><span class="sxs-lookup"><span data-stu-id="3d506-112">Direct link</span></span>
<span data-ttu-id="3d506-113">Você pode acessar Olá profusão de interface do usuário em Olá URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d506-113">You can access hello Storm UI at hello following URL:</span></span>

<span data-ttu-id="3d506-114">https://\<nome DNS do cluster\>/stormui</span><span class="sxs-lookup"><span data-stu-id="3d506-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="3d506-115">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3d506-115">Example:</span></span>

 <span data-ttu-id="3d506-116">https://stormcluster.azurehdinsight.net/stormui</span><span class="sxs-lookup"><span data-stu-id="3d506-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a><span data-ttu-id="3d506-117">Como posso transferir informações de ponto de verificação spout do hub de evento profusão de uma topologia tooanother</span><span class="sxs-lookup"><span data-stu-id="3d506-117">How do I transfer Storm event hub spout checkpoint information from one topology tooanother</span></span>

<span data-ttu-id="3d506-118">Quando você desenvolve topologias que leem dos Hubs de eventos do Azure usando Olá arquivo. jar do HDInsight Storm evento hub spout, você deve implantar uma topologia que tem o mesmo nome em um novo cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d506-118">When you develop topologies that read from Azure Event Hubs by using hello HDInsight Storm event hub spout .jar file, you must deploy a topology that has hello same name on a new cluster.</span></span> <span data-ttu-id="3d506-119">No entanto, você deve reter dados de ponto de verificação de saudação que foi confirmada tooApache ZooKeeper no cluster antigo hello.</span><span class="sxs-lookup"><span data-stu-id="3d506-119">However, you must retain hello checkpoint data that was committed tooApache ZooKeeper on hello old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="3d506-120">O local em que os dados de ponto de verificação são armazenados</span><span class="sxs-lookup"><span data-stu-id="3d506-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="3d506-121">Dados de ponto de verificação de deslocamentos são armazenados por spout de hub de evento Olá no ZooKeeper em dois caminhos de raiz:</span><span class="sxs-lookup"><span data-stu-id="3d506-121">Checkpoint data for offsets is stored by hello event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="3d506-122">Pontos de verificação de spout não transacionais são armazenados em /eventhubspout.</span><span class="sxs-lookup"><span data-stu-id="3d506-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="3d506-123">Dados de pontos de verificação de spout transacionais são armazenados em /transactional.</span><span class="sxs-lookup"><span data-stu-id="3d506-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-toorestore"></a><span data-ttu-id="3d506-124">Como toorestore</span><span class="sxs-lookup"><span data-stu-id="3d506-124">How toorestore</span></span>
<span data-ttu-id="3d506-125">scripts de saudação tooget e bibliotecas que você use dados tooexport ZooKeeper e, em seguida, importa Olá dados back tooZooKeeper com um novo nome, consulte [exemplos profusão de HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="3d506-125">tooget hello scripts and libraries that you use tooexport data out of ZooKeeper and then import hello data back tooZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="3d506-126">pasta lib de saudação tem arquivos. jar que contêm a implementação de saudação para operação de importação/exportação de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d506-126">hello lib folder has .jar files that contain hello implementation for hello export/import operation.</span></span> <span data-ttu-id="3d506-127">Olá bash pasta tiver um script de exemplo que demonstra como dados tooexport Olá server ZooKeeper no cluster antigo hello e importe-o servidor de ZooKeeper toohello Voltar no novo cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d506-127">hello bash folder has an example script that demonstrates how tooexport data from hello ZooKeeper server on hello old cluster, and then import it back toohello ZooKeeper server on hello new cluster.</span></span>

<span data-ttu-id="3d506-128">Executar Olá [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) Olá ZooKeeper nós tooexport de script e, em seguida, importar dados.</span><span class="sxs-lookup"><span data-stu-id="3d506-128">Run hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from hello ZooKeeper nodes tooexport and then import data.</span></span> <span data-ttu-id="3d506-129">Atualização Olá script toohello plataforma HDP (Hortonworks Data) versão correta.</span><span class="sxs-lookup"><span data-stu-id="3d506-129">Update hello script toohello correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="3d506-130">(Estamos trabalhando para tornar esses scripts genéricos no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3d506-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="3d506-131">Scripts genéricos podem executar de qualquer nó no cluster Olá sem modificações pelo usuário hello.)</span><span class="sxs-lookup"><span data-stu-id="3d506-131">Generic scripts can run from any node on hello cluster without modifications by hello user.)</span></span>

<span data-ttu-id="3d506-132">o comando de exportação Olá grava Olá tooan sistema de arquivos distribuído (HDFS) do Apache Hadoop caminho de metadados (em um repositório de armazenamento de BLOBs do Azure ou do repositório Azure Data Lake) em um local que você definir.</span><span class="sxs-lookup"><span data-stu-id="3d506-132">hello export command writes hello metadata tooan Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="3d506-133">Exemplos</span><span class="sxs-lookup"><span data-stu-id="3d506-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="3d506-134">Exportar metadados de deslocamento</span><span class="sxs-lookup"><span data-stu-id="3d506-134">Export offset metadata</span></span>
1. <span data-ttu-id="3d506-135">Use o cluster do SSH toogo toohello ZooKeeper no cluster de saudação do ponto de verificação que Olá deslocamento precisa toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="3d506-135">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="3d506-136">Olá executar comando a seguir (após a atualização Olá cadeia de caracteres de versão HDP) tooexport ZooKeeper deslocamento dados toohello /stormmetadta/zkdata HDFS caminho:</span><span class="sxs-lookup"><span data-stu-id="3d506-136">Run hello following command (after you update hello HDP version string) tooexport ZooKeeper offset data toohello /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="3d506-137">Importar metadados de deslocamento</span><span class="sxs-lookup"><span data-stu-id="3d506-137">Import offset metadata</span></span>
1. <span data-ttu-id="3d506-138">Use o cluster do SSH toogo toohello ZooKeeper no cluster de saudação do ponto de verificação que Olá deslocamento precisa toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="3d506-138">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="3d506-139">Execução hello seguinte comando (depois de atualizar a cadeia de caracteres de versão do hello HDP) tooimport ZooKeeper deslocamento dados de saudação caminho/stormmetadata/zkdata toohello ZooKeeper do servidor HDFS no cluster de destino hello:</span><span class="sxs-lookup"><span data-stu-id="3d506-139">Run hello following command (after you update hello HDP version string) tooimport ZooKeeper offset data from hello HDFS path /stormmetadata/zkdata toohello ZooKeeper server on hello target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a><span data-ttu-id="3d506-140">Excluir metadados deslocamento topologias podem iniciar o processamento de dados desde o início de hello, ou de um carimbo de hora que o usuário Olá escolhe</span><span class="sxs-lookup"><span data-stu-id="3d506-140">Delete offset metadata so that topologies can start processing data from hello beginning, or from a timestamp that hello user chooses</span></span>
1. <span data-ttu-id="3d506-141">Use o cluster do SSH toogo toohello ZooKeeper no cluster de saudação do ponto de verificação que Olá deslocamento precisa toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="3d506-141">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="3d506-142">Execução hello seguinte comando (depois de atualizar a cadeia de caracteres de versão do hello HDP) toodelete todos os ZooKeeper deslocamento dados no cluster de saudação atual:</span><span class="sxs-lookup"><span data-stu-id="3d506-142">Run hello following command (after you update hello HDP version string) toodelete all ZooKeeper offset data in hello current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="3d506-143">Como fazer para localizar binários do Storm em um cluster</span><span class="sxs-lookup"><span data-stu-id="3d506-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="3d506-144">Binários de profusão de pilha atual de HDP Olá estão em /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="3d506-144">Storm binaries for hello current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="3d506-145">local de saudação é Olá mesmo para nós de cabeçalho e nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3d506-145">hello location is hello same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="3d506-146">Pode haver vários binários para versões específicas do HDP em /usr/hdp (por exemplo, /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="3d506-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="3d506-147">pasta de /usr/hdp/current/storm-client Olá é symlinked toohello versão mais recente que está em execução no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d506-147">hello /usr/hdp/current/storm-client folder is symlinked toohello latest version that is running on hello cluster.</span></span>

<span data-ttu-id="3d506-148">Para obter mais informações, consulte [cluster do HDInsight tooan conectar usando o SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="3d506-148">For more information, see [Connect tooan HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="3d506-149">Como determinar a topologia de implantação de saudação de um cluster Storm</span><span class="sxs-lookup"><span data-stu-id="3d506-149">How do I determine hello deployment topology of a Storm cluster</span></span>
<span data-ttu-id="3d506-150">Primeiro, identifique todos os componentes instalados com o HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="3d506-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="3d506-151">Um cluster do Storm consiste em quatro categorias de nó:</span><span class="sxs-lookup"><span data-stu-id="3d506-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="3d506-152">Nós de gateway</span><span class="sxs-lookup"><span data-stu-id="3d506-152">Gateway nodes</span></span>
* <span data-ttu-id="3d506-153">Nós de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="3d506-153">Head nodes</span></span>
* <span data-ttu-id="3d506-154">Nós do ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="3d506-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="3d506-155">Nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="3d506-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="3d506-156">Nós de gateway</span><span class="sxs-lookup"><span data-stu-id="3d506-156">Gateway nodes</span></span>
<span data-ttu-id="3d506-157">Um nó do gateway é um gateway e o serviço de proxy reverso que permite acesso público tooan active Ambari management service.</span><span class="sxs-lookup"><span data-stu-id="3d506-157">A gateway node is a gateway and reverse proxy service that enables public access tooan active Ambari management service.</span></span> <span data-ttu-id="3d506-158">Ele também lida com a seleção de líder do Ambari.</span><span class="sxs-lookup"><span data-stu-id="3d506-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="3d506-159">Nós de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="3d506-159">Head nodes</span></span>
<span data-ttu-id="3d506-160">Nós de cabeçalho Storm execute Olá serviços a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d506-160">Storm head nodes run hello following services:</span></span>
* <span data-ttu-id="3d506-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="3d506-161">Nimbus</span></span>
* <span data-ttu-id="3d506-162">Servidor Ambari</span><span class="sxs-lookup"><span data-stu-id="3d506-162">Ambari server</span></span>
* <span data-ttu-id="3d506-163">Servidor de Métricas do Ambari</span><span class="sxs-lookup"><span data-stu-id="3d506-163">Ambari Metrics server</span></span>
* <span data-ttu-id="3d506-164">Coletor de Métricas do Ambari</span><span class="sxs-lookup"><span data-stu-id="3d506-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="3d506-165">Nós do ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="3d506-165">ZooKeeper nodes</span></span>
<span data-ttu-id="3d506-166">O HDInsight tem um quorum do ZooKeeper de três nós.</span><span class="sxs-lookup"><span data-stu-id="3d506-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="3d506-167">tamanho de quorum Olá é fixo e não pode ser reconfigurado.</span><span class="sxs-lookup"><span data-stu-id="3d506-167">hello quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="3d506-168">Serviços de storm em cluster Olá são quorum de ZooKeeper tooautomatically configurado use hello.</span><span class="sxs-lookup"><span data-stu-id="3d506-168">Storm services in hello cluster are configured tooautomatically use hello ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="3d506-169">Nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="3d506-169">Worker nodes</span></span>
<span data-ttu-id="3d506-170">Nós de trabalho Storm executam Olá serviços a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d506-170">Storm worker nodes run hello following services:</span></span>
* <span data-ttu-id="3d506-171">Supervisor</span><span class="sxs-lookup"><span data-stu-id="3d506-171">Supervisor</span></span>
* <span data-ttu-id="3d506-172">JVMs (máquinas virtuais Java) de trabalho, para executar topologias</span><span class="sxs-lookup"><span data-stu-id="3d506-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="3d506-173">Agente do Ambari</span><span class="sxs-lookup"><span data-stu-id="3d506-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="3d506-174">Como fazer para localizar binários de spout do hub de eventos Storm para desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="3d506-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="3d506-175">Para obter mais informações sobre como usar arquivos. jar do Storm evento hub spout com sua topologia, consulte Olá recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="3d506-175">For more information about using Storm event hub spout .jar files with your topology, see hello following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="3d506-176">Topologia baseada em Java</span><span class="sxs-lookup"><span data-stu-id="3d506-176">Java-based topology</span></span>
[<span data-ttu-id="3d506-177">Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="3d506-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="3d506-178">Topologia baseada em C# (Mono em clusters Storm Linux no HDInsight 3.4+)</span><span class="sxs-lookup"><span data-stu-id="3d506-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="3d506-179">Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="3d506-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="3d506-180">Binários de spout do hub de eventos Storm mais recentes para clusters Storm Linux no HDInsight 3.5+</span><span class="sxs-lookup"><span data-stu-id="3d506-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="3d506-181">toolearn como toouse hello mais recente Storm evento hub spout que funciona com o HDInsight 3.5 + Linux Storm clusters, consulte Olá mvn-repo [arquivo Leiame](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="3d506-181">toolearn how toouse hello latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see hello mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="3d506-182">Exemplos de código-fonte</span><span class="sxs-lookup"><span data-stu-id="3d506-182">Source code examples</span></span>
<span data-ttu-id="3d506-183">Consulte [exemplos](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) como tooread e gravação de Hub de eventos do Azure usando uma topologia do Apache Storm (escrita em Java) em um cluster HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d506-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how tooread and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="3d506-184">Como fazer para localizar arquivos de configuração do Storm Log4J nos clusters</span><span class="sxs-lookup"><span data-stu-id="3d506-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="3d506-185">arquivos de configuração tooidentify Log4J Apache para serviços Storm.</span><span class="sxs-lookup"><span data-stu-id="3d506-185">tooidentify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="3d506-186">Em nós de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="3d506-186">On head nodes</span></span>
<span data-ttu-id="3d506-187">Olá Nimbus Log4J configuração é lida em /usr. hdp/\<versão HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="3d506-187">hello Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="3d506-188">Em nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="3d506-188">On worker nodes</span></span>
<span data-ttu-id="3d506-189">configuração de supervisor Log4J Olá é lido de em /usr. hdp/\<versão HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="3d506-189">hello supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="3d506-190">arquivo de configuração de trabalho Log4J Olá é lido em /usr. hdp/\<versão HDP\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="3d506-190">hello worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="3d506-191">Exemplos: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="3d506-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

