---
title: Solucionar problemas do Storm usando o Azure HDInsight | Microsoft Docs
description: Obtenha respostas para perguntas comuns sobre o uso do Apache Storm com o Azure HDInsight.
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
ms.openlocfilehash: 70a3d762431d90acdd6ed2a432a569f34d0ce447
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="47ef8-104">Solucionar problemas do Storm usando o Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="47ef8-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="47ef8-105">Saiba mais sobre os principais problemas e suas soluções para trabalhar com cargas de Apache Storm no Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="47ef8-105">Learn about the top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-the-storm-ui-on-a-cluster"></a><span data-ttu-id="47ef8-106">Como fazer para acessar a interface do usuário do Storm em um cluster</span><span class="sxs-lookup"><span data-stu-id="47ef8-106">How do I access the Storm UI on a cluster</span></span>
<span data-ttu-id="47ef8-107">Você tem duas opções para acessar a interface do usuário do Storm em um navegador:</span><span class="sxs-lookup"><span data-stu-id="47ef8-107">You have two options for accessing the Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="47ef8-108">Interface do usuário do Ambari</span><span class="sxs-lookup"><span data-stu-id="47ef8-108">Ambari UI</span></span>
1. <span data-ttu-id="47ef8-109">Vá até o painel do Ambari.</span><span class="sxs-lookup"><span data-stu-id="47ef8-109">Go to the Ambari dashboard.</span></span>
2. <span data-ttu-id="47ef8-110">Na lista de serviços, selecione **Storm**.</span><span class="sxs-lookup"><span data-stu-id="47ef8-110">In the list of services, select **Storm**.</span></span>
3. <span data-ttu-id="47ef8-111">No menu **Links Rápidos**, selecione **Interface do Usuário do Storm**.</span><span class="sxs-lookup"><span data-stu-id="47ef8-111">In the **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="47ef8-112">Link direto</span><span class="sxs-lookup"><span data-stu-id="47ef8-112">Direct link</span></span>
<span data-ttu-id="47ef8-113">Você pode acessar a interface do usuário do Storm na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="47ef8-113">You can access the Storm UI at the following URL:</span></span>

<span data-ttu-id="47ef8-114">https://\<nome DNS do cluster\>/stormui</span><span class="sxs-lookup"><span data-stu-id="47ef8-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="47ef8-115">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="47ef8-115">Example:</span></span>

 <span data-ttu-id="47ef8-116">https://stormcluster.azurehdinsight.net/stormui</span><span class="sxs-lookup"><span data-stu-id="47ef8-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-to-another"></a><span data-ttu-id="47ef8-117">Como fazer para transferir informações de ponto de verificação de spout no hub de eventos Storm de uma topologia para outra</span><span class="sxs-lookup"><span data-stu-id="47ef8-117">How do I transfer Storm event hub spout checkpoint information from one topology to another</span></span>

<span data-ttu-id="47ef8-118">Quando desenvolve topologias que leem os Hubs de Eventos do Azure usando o arquivo .jar do spout do hub de eventos Storm no HDInsight, você precisa implantar uma topologia que tenha o mesmo nome em um novo cluster.</span><span class="sxs-lookup"><span data-stu-id="47ef8-118">When you develop topologies that read from Azure Event Hubs by using the HDInsight Storm event hub spout .jar file, you must deploy a topology that has the same name on a new cluster.</span></span> <span data-ttu-id="47ef8-119">No entanto, você precisa reter os dados de ponto de verificação que foram confirmados no ZooKeeper do Apache no cluster antigo.</span><span class="sxs-lookup"><span data-stu-id="47ef8-119">However, you must retain the checkpoint data that was committed to Apache ZooKeeper on the old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="47ef8-120">O local em que os dados de ponto de verificação são armazenados</span><span class="sxs-lookup"><span data-stu-id="47ef8-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="47ef8-121">Os dados de ponto de verificação para deslocamentos são armazenados pelo spout do hub de eventos no ZooKeeper em dois caminhos raiz:</span><span class="sxs-lookup"><span data-stu-id="47ef8-121">Checkpoint data for offsets is stored by the event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="47ef8-122">Pontos de verificação de spout não transacionais são armazenados em /eventhubspout.</span><span class="sxs-lookup"><span data-stu-id="47ef8-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="47ef8-123">Dados de pontos de verificação de spout transacionais são armazenados em /transactional.</span><span class="sxs-lookup"><span data-stu-id="47ef8-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-to-restore"></a><span data-ttu-id="47ef8-124">Como restaurar</span><span class="sxs-lookup"><span data-stu-id="47ef8-124">How to restore</span></span>
<span data-ttu-id="47ef8-125">Para fazer com que os scripts e bibliotecas que você usa exportem dados para fora do ZooKeeper e, em seguida, importar os dados de volta para o ZooKeeper com um novo nome, consulte [Exemplos de Storm no HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="47ef8-125">To get the scripts and libraries that you use to export data out of ZooKeeper and then import the data back to ZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="47ef8-126">A pasta lib tem arquivos .jar que contêm a implementação para a operação de exportação/importação.</span><span class="sxs-lookup"><span data-stu-id="47ef8-126">The lib folder has .jar files that contain the implementation for the export/import operation.</span></span> <span data-ttu-id="47ef8-127">A pasta bash tem um script de exemplo que demonstra como exportar dados do servidor do ZooKeeper no cluster antigo e importá-los de volta para o servidor do ZooKeeper no novo cluster.</span><span class="sxs-lookup"><span data-stu-id="47ef8-127">The bash folder has an example script that demonstrates how to export data from the ZooKeeper server on the old cluster, and then import it back to the ZooKeeper server on the new cluster.</span></span>

<span data-ttu-id="47ef8-128">Execute o script [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) nos nós do ZooKeeper para exportar e, em seguida, importar dados.</span><span class="sxs-lookup"><span data-stu-id="47ef8-128">Run the [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from the ZooKeeper nodes to export and then import data.</span></span> <span data-ttu-id="47ef8-129">Atualize o script para a versão correta da HDP (Hortonworks Data Platform).</span><span class="sxs-lookup"><span data-stu-id="47ef8-129">Update the script to the correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="47ef8-130">(Estamos trabalhando para tornar esses scripts genéricos no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47ef8-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="47ef8-131">Scripts genéricos podem ser executados em qualquer nó no cluster sem modificações pelo usuário.)</span><span class="sxs-lookup"><span data-stu-id="47ef8-131">Generic scripts can run from any node on the cluster without modifications by the user.)</span></span>

<span data-ttu-id="47ef8-132">O comando de exportação grava os metadados em um caminho de HDFS (Sistema de Arquivos Distribuído) do Apache Hadoop (em um repositório do Armazenamento de Blobs do Azure ou do Azure Data Lake Store) em um local que você definir.</span><span class="sxs-lookup"><span data-stu-id="47ef8-132">The export command writes the metadata to an Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="47ef8-133">Exemplos</span><span class="sxs-lookup"><span data-stu-id="47ef8-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="47ef8-134">Exportar metadados de deslocamento</span><span class="sxs-lookup"><span data-stu-id="47ef8-134">Export offset metadata</span></span>
1. <span data-ttu-id="47ef8-135">Use SSH para ir até o cluster do ZooKeeper no cluster do qual o deslocamento do ponto de verificação precisa ser exportado.</span><span class="sxs-lookup"><span data-stu-id="47ef8-135">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="47ef8-136">Execute o seguinte comando (depois de atualizar a cadeia de caracteres de versão do HDP) para exportar dados de deslocamento do ZooKeeper para o caminho do HDFS /stormmetadata/zkdata:</span><span class="sxs-lookup"><span data-stu-id="47ef8-136">Run the following command (after you update the HDP version string) to export ZooKeeper offset data to the /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="47ef8-137">Importar metadados de deslocamento</span><span class="sxs-lookup"><span data-stu-id="47ef8-137">Import offset metadata</span></span>
1. <span data-ttu-id="47ef8-138">Use SSH para ir até o cluster do ZooKeeper no cluster do qual o deslocamento do ponto de verificação precisa ser exportado.</span><span class="sxs-lookup"><span data-stu-id="47ef8-138">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="47ef8-139">Execute o seguinte comando (depois de atualizar a cadeia de caracteres de versão do HDP) para importar dados de deslocamento do ZooKeeper do caminho do HDFS /stormmetadata/zkdata para o servidor do ZooKeeper no cluster de destino:</span><span class="sxs-lookup"><span data-stu-id="47ef8-139">Run the following command (after you update the HDP version string) to import ZooKeeper offset data from the HDFS path /stormmetadata/zkdata to the ZooKeeper server on the target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-the-beginning-or-from-a-timestamp-that-the-user-chooses"></a><span data-ttu-id="47ef8-140">Exclua metadados de deslocamento para que as topologias possam começar a processar dados desde o início ou desde um carimbo de data/hora escolhido pelo usuário</span><span class="sxs-lookup"><span data-stu-id="47ef8-140">Delete offset metadata so that topologies can start processing data from the beginning, or from a timestamp that the user chooses</span></span>
1. <span data-ttu-id="47ef8-141">Use SSH para ir até o cluster do ZooKeeper no cluster do qual o deslocamento do ponto de verificação precisa ser exportado.</span><span class="sxs-lookup"><span data-stu-id="47ef8-141">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="47ef8-142">Execute o comando a seguir (depois de atualizar a cadeia de caracteres de versão do HDP) para excluir todos os dados de deslocamento do ZooKeeper no cluster atual:</span><span class="sxs-lookup"><span data-stu-id="47ef8-142">Run the following command (after you update the HDP version string) to delete all ZooKeeper offset data in the current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="47ef8-143">Como fazer para localizar binários do Storm em um cluster</span><span class="sxs-lookup"><span data-stu-id="47ef8-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="47ef8-144">Binários do Storm para a pilha do HDP atual estão em /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="47ef8-144">Storm binaries for the current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="47ef8-145">O local é o mesmo para nós de cabeçalho e para nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="47ef8-145">The location is the same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="47ef8-146">Pode haver vários binários para versões específicas do HDP em /usr/hdp (por exemplo, /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="47ef8-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="47ef8-147">A pasta /usr/hdp/current/storm-client está vinculada simbolicamente à versão mais recente em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="47ef8-147">The /usr/hdp/current/storm-client folder is symlinked to the latest version that is running on the cluster.</span></span>

<span data-ttu-id="47ef8-148">Para obter mais informações, consulte [Conectar-se a um cluster HDInsight usando SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="47ef8-148">For more information, see [Connect to an HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-the-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="47ef8-149">Como fazer para determinar a topologia de implantação de um cluster do Storm</span><span class="sxs-lookup"><span data-stu-id="47ef8-149">How do I determine the deployment topology of a Storm cluster</span></span>
<span data-ttu-id="47ef8-150">Primeiro, identifique todos os componentes instalados com o HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="47ef8-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="47ef8-151">Um cluster do Storm consiste em quatro categorias de nó:</span><span class="sxs-lookup"><span data-stu-id="47ef8-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="47ef8-152">Nós de gateway</span><span class="sxs-lookup"><span data-stu-id="47ef8-152">Gateway nodes</span></span>
* <span data-ttu-id="47ef8-153">Nós de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="47ef8-153">Head nodes</span></span>
* <span data-ttu-id="47ef8-154">Nós do ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="47ef8-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="47ef8-155">Nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="47ef8-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="47ef8-156">Nós de gateway</span><span class="sxs-lookup"><span data-stu-id="47ef8-156">Gateway nodes</span></span>
<span data-ttu-id="47ef8-157">Um nó de gateway é um serviço de proxy reverso e de gateway que habilita o acesso público a um serviço de gerenciamento do Ambari ativo.</span><span class="sxs-lookup"><span data-stu-id="47ef8-157">A gateway node is a gateway and reverse proxy service that enables public access to an active Ambari management service.</span></span> <span data-ttu-id="47ef8-158">Ele também lida com a seleção de líder do Ambari.</span><span class="sxs-lookup"><span data-stu-id="47ef8-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="47ef8-159">Nós de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="47ef8-159">Head nodes</span></span>
<span data-ttu-id="47ef8-160">Nós de cabeçalho do Storm executam os seguintes serviços:</span><span class="sxs-lookup"><span data-stu-id="47ef8-160">Storm head nodes run the following services:</span></span>
* <span data-ttu-id="47ef8-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="47ef8-161">Nimbus</span></span>
* <span data-ttu-id="47ef8-162">Servidor Ambari</span><span class="sxs-lookup"><span data-stu-id="47ef8-162">Ambari server</span></span>
* <span data-ttu-id="47ef8-163">Servidor de Métricas do Ambari</span><span class="sxs-lookup"><span data-stu-id="47ef8-163">Ambari Metrics server</span></span>
* <span data-ttu-id="47ef8-164">Coletor de Métricas do Ambari</span><span class="sxs-lookup"><span data-stu-id="47ef8-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="47ef8-165">Nós do ZooKeeper</span><span class="sxs-lookup"><span data-stu-id="47ef8-165">ZooKeeper nodes</span></span>
<span data-ttu-id="47ef8-166">O HDInsight tem um quorum do ZooKeeper de três nós.</span><span class="sxs-lookup"><span data-stu-id="47ef8-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="47ef8-167">O tamanho do quorum é fixo e não é configurável.</span><span class="sxs-lookup"><span data-stu-id="47ef8-167">The quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="47ef8-168">Serviços do Storm no cluster são configurados para usar o quorum do ZooKeeper automaticamente.</span><span class="sxs-lookup"><span data-stu-id="47ef8-168">Storm services in the cluster are configured to automatically use the ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="47ef8-169">Nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="47ef8-169">Worker nodes</span></span>
<span data-ttu-id="47ef8-170">Nós de trabalho do Storm executam os seguintes serviços:</span><span class="sxs-lookup"><span data-stu-id="47ef8-170">Storm worker nodes run the following services:</span></span>
* <span data-ttu-id="47ef8-171">Supervisor</span><span class="sxs-lookup"><span data-stu-id="47ef8-171">Supervisor</span></span>
* <span data-ttu-id="47ef8-172">JVMs (máquinas virtuais Java) de trabalho, para executar topologias</span><span class="sxs-lookup"><span data-stu-id="47ef8-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="47ef8-173">Agente do Ambari</span><span class="sxs-lookup"><span data-stu-id="47ef8-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="47ef8-174">Como fazer para localizar binários de spout do hub de eventos Storm para desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="47ef8-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="47ef8-175">Para obter mais informações sobre como usar arquivos .jar de spout do hub de eventos do Storm com sua topologia, consulte os seguintes recursos.</span><span class="sxs-lookup"><span data-stu-id="47ef8-175">For more information about using Storm event hub spout .jar files with your topology, see the following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="47ef8-176">Topologia baseada em Java</span><span class="sxs-lookup"><span data-stu-id="47ef8-176">Java-based topology</span></span>
[<span data-ttu-id="47ef8-177">Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="47ef8-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="47ef8-178">Topologia baseada em C# (Mono em clusters Storm Linux no HDInsight 3.4+)</span><span class="sxs-lookup"><span data-stu-id="47ef8-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="47ef8-179">Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="47ef8-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="47ef8-180">Binários de spout do hub de eventos Storm mais recentes para clusters Storm Linux no HDInsight 3.5+</span><span class="sxs-lookup"><span data-stu-id="47ef8-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="47ef8-181">Para saber como usar o spout de hub de eventos do Storm mais recente que funciona com clusters Storm Linux do HDInsight 3.5+, consulte o [arquivo Leiame](https://github.com/hdinsight/mvn-repo/blob/master/README.md) do repositório de mvn.</span><span class="sxs-lookup"><span data-stu-id="47ef8-181">To learn how to use the latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see the mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="47ef8-182">Exemplos de código-fonte</span><span class="sxs-lookup"><span data-stu-id="47ef8-182">Source code examples</span></span>
<span data-ttu-id="47ef8-183">Veja [exemplos](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) de ler e gravar no Hub de Eventos do Azure usando uma topologia do Apache Storm (escrita em Java) em um cluster do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47ef8-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how to read and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="47ef8-184">Como fazer para localizar arquivos de configuração do Storm Log4J nos clusters</span><span class="sxs-lookup"><span data-stu-id="47ef8-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="47ef8-185">Para identificar arquivos de configuração do Apache Log4J para serviços do Storm.</span><span class="sxs-lookup"><span data-stu-id="47ef8-185">To identify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="47ef8-186">Em nós de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="47ef8-186">On head nodes</span></span>
<span data-ttu-id="47ef8-187">A configuração de Log4J Nimbus é lida de /usr/hdp/\<versão de HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="47ef8-187">The Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="47ef8-188">Em nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="47ef8-188">On worker nodes</span></span>
<span data-ttu-id="47ef8-189">A configuração de Log4J de supervisor é lida de /usr/hdp/\<versão de HDP\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="47ef8-189">The supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="47ef8-190">O arquivo de configuração de Log4J de trabalho é lido de /usr/hdp/\<versão de HDP\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="47ef8-190">The worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="47ef8-191">Exemplos: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="47ef8-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

