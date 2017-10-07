---
title: aaaTroubleshoot HBase usando o Azure HDInsight | Microsoft Docs
description: Obter respostas a perguntas toocommon sobre como trabalhar com HBase e HDInsight do Azure.
services: hdinsight
documentationcenter: 
author: nitinver
manager: ashitg
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 7/7/2017
ms.author: nitinver
ms.openlocfilehash: 5210184f8ea95628952a95df8c98f5b98e37c53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="44be3-103">Solucionar problemas do HBase usando o Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="44be3-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="44be3-104">Saiba mais sobre questões hello e suas resoluções durante o trabalho com cargas Apache HBase no Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="44be3-104">Learn about hello top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="44be3-105">Como fazer para executar relatórios de comando hbck com várias regiões não atribuídas</span><span class="sxs-lookup"><span data-stu-id="44be3-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="44be3-106">Uma mensagem de erro comuns que você pode ver quando você executa Olá `hbase hbck` comando é "várias regiões que não está sendo atribuídas ou falhas na cadeia de saudação do regiões."</span><span class="sxs-lookup"><span data-stu-id="44be3-106">A common error message that you might see when you run hello `hbase hbck` command is "multiple regions being unassigned or holes in hello chain of regions."</span></span>

<span data-ttu-id="44be3-107">Em Olá UI HBase mestre, você pode ver o número de saudação das regiões que estão desbalanceadas entre todos os servidores de região.</span><span class="sxs-lookup"><span data-stu-id="44be3-107">In hello HBase Master UI, you can see hello number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="44be3-108">Em seguida, você pode executar `hbase hbck` toosee falhas na cadeia de região de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="44be3-108">Then, you can run `hbase hbck` command toosee holes in hello region chain.</span></span>

<span data-ttu-id="44be3-109">Falhas podem ser causadas por regiões offline de hello, caso atribuições de saudação de correção primeiro.</span><span class="sxs-lookup"><span data-stu-id="44be3-109">Holes might be caused by hello offline regions, so fix hello assignments first.</span></span> 

<span data-ttu-id="44be3-110">toobring Olá estado normal de retorno tooa regiões não atribuídos, conclua Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="44be3-110">toobring hello unassigned regions back tooa normal state, complete hello following steps:</span></span>

1. <span data-ttu-id="44be3-111">Entre no toohello cluster HDInsight HBase usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="44be3-111">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="44be3-112">tooconnect com o shell de ZooKeeper hello, executar Olá `hbase zkcli` comando.</span><span class="sxs-lookup"><span data-stu-id="44be3-112">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="44be3-113">Executar Olá `rmr /hbase/regions-in-transition` comando ou hello `rmr /hbase-unsecure/regions-in-transition` comando.</span><span class="sxs-lookup"><span data-stu-id="44be3-113">Run hello `rmr /hbase/regions-in-transition` command or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="44be3-114">tooexit de saudação `hbase zkcli` do shell, use Olá `exit` comando.</span><span class="sxs-lookup"><span data-stu-id="44be3-114">tooexit from hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="44be3-115">Abra Olá Apache Ambari UI e, em seguida, reinicie o serviço de Active HBase mestre de hello.</span><span class="sxs-lookup"><span data-stu-id="44be3-115">Open hello Apache Ambari UI, and then restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="44be3-116">Executar Olá `hbase hbck` comando novamente (sem opções).</span><span class="sxs-lookup"><span data-stu-id="44be3-116">Run hello `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="44be3-117">Verifique a saída de saudação de tooensure esse comando que estão sendo atribuídas a todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="44be3-117">Check hello output of this command tooensure that all regions are being assigned.</span></span>


## <span data-ttu-id="44be3-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Como fazer para corrigir problemas de tempo limite usando comandos hbck para atribuições de região</span><span class="sxs-lookup"><span data-stu-id="44be3-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="44be3-119">Problema</span><span class="sxs-lookup"><span data-stu-id="44be3-119">Issue</span></span>

<span data-ttu-id="44be3-120">Uma causa potencial de problemas de tempo limite quando você usar o hello `hbck` comando pode ser que várias regiões estão em hello "em transição" estado por um longo tempo.</span><span class="sxs-lookup"><span data-stu-id="44be3-120">A potential cause for timeout issues when you use hello `hbck` command might be that several regions are in hello "in transition" state for a long time.</span></span> <span data-ttu-id="44be3-121">Você pode ver essas regiões como offline nos Olá UI HBase mestre.</span><span class="sxs-lookup"><span data-stu-id="44be3-121">You can see those regions as offline in hello HBase Master UI.</span></span> <span data-ttu-id="44be3-122">Porque um grande número de regiões está tentando tootransition, o mestre do HBase talvez tempo limite e ser toobring não é possível essas regiões online novamente.</span><span class="sxs-lookup"><span data-stu-id="44be3-122">Because a high number of regions are attempting tootransition, HBase Master might timeout and be unable toobring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="44be3-123">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="44be3-123">Resolution steps</span></span>

1. <span data-ttu-id="44be3-124">Entre no toohello cluster HDInsight HBase usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="44be3-124">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="44be3-125">tooconnect com o shell de ZooKeeper hello, executar Olá `hbase zkcli` comando.</span><span class="sxs-lookup"><span data-stu-id="44be3-125">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="44be3-126">Executar Olá `rmr /hbase/regions-in-transition` ou hello `rmr /hbase-unsecure/regions-in-transition` comando.</span><span class="sxs-lookup"><span data-stu-id="44be3-126">Run hello `rmr /hbase/regions-in-transition` or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="44be3-127">Olá tooexit `hbase zkcli` do shell, use Olá `exit` comando.</span><span class="sxs-lookup"><span data-stu-id="44be3-127">tooexit hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="44be3-128">Em Olá Ambari UI, reinicie o serviço de Active HBase mestre de saudação.</span><span class="sxs-lookup"><span data-stu-id="44be3-128">In hello Ambari UI, restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="44be3-129">Executar Olá `hbase hbck -fixAssignments` comando novamente.</span><span class="sxs-lookup"><span data-stu-id="44be3-129">Run hello `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="44be3-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Como forçar a desabilitação do modo de segurança de HDFS em um cluster</span><span class="sxs-lookup"><span data-stu-id="44be3-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="44be3-131">Problema</span><span class="sxs-lookup"><span data-stu-id="44be3-131">Issue</span></span>

<span data-ttu-id="44be3-132">Olá local Hadoop distribuídas arquivo de sistema (HDFS) está preso no modo de segurança no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="44be3-132">hello local Hadoop Distributed File System (HDFS) is stuck in safe mode on hello HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="44be3-133">Descrição detalhada</span><span class="sxs-lookup"><span data-stu-id="44be3-133">Detailed description</span></span>

<span data-ttu-id="44be3-134">Esse erro pode ser causado por uma falha ao executar Olá HDFS comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="44be3-134">This error might be caused by a failure when you run hello following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="44be3-135">Erro de saudação que podem ocorrer ao tentar o comando de saudação toorun tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="44be3-135">hello error you might see when you try toorun hello command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" tooturn safe mode off.
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1359)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:4010)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1102)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:630)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:640)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:982)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2313)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2309)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:422)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1724)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2307)
        at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1552)
        at org.apache.hadoop.ipc.Client.call(Client.java:1496)
        at org.apache.hadoop.ipc.Client.call(Client.java:1396)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:233)
        at com.sun.proxy.$Proxy10.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.mkdirs(ClientNamenodeProtocolTranslatorPB.java:603)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:278)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:194)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:176)
        at com.sun.proxy.$Proxy11.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:3061)
        at org.apache.hadoop.hdfs.DFSClient.mkdirs(DFSClient.java:3031)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1162)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1158)
        at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirsInternal(DistributedFileSystem.java:1158)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirs(DistributedFileSystem.java:1150)
        at org.apache.hadoop.fs.FileSystem.mkdirs(FileSystem.java:1898)
        at org.apache.hadoop.fs.shell.Mkdir.processNonexistentPath(Mkdir.java:76)
        at org.apache.hadoop.fs.shell.Command.processArgument(Command.java:273)
        at org.apache.hadoop.fs.shell.Command.processArguments(Command.java:255)
        at org.apache.hadoop.fs.shell.FsCommand.processRawArguments(FsCommand.java:119)
        at org.apache.hadoop.fs.shell.Command.run(Command.java:165)
        at org.apache.hadoop.fs.FsShell.run(FsShell.java:297)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:90)
        at org.apache.hadoop.fs.FsShell.main(FsShell.java:350)
mkdir: Cannot create directory /temp. Name node is in safe mode.
```

### <a name="probable-cause"></a><span data-ttu-id="44be3-136">Causa provável</span><span class="sxs-lookup"><span data-stu-id="44be3-136">Probable cause</span></span>

<span data-ttu-id="44be3-137">Olá cluster HDInsight foi reduzida tooa muito alguns nós.</span><span class="sxs-lookup"><span data-stu-id="44be3-137">hello HDInsight cluster has been scaled down tooa very few nodes.</span></span> <span data-ttu-id="44be3-138">número de saudação de nós está abaixo ou feche o fator de replicação de HDFS toohello.</span><span class="sxs-lookup"><span data-stu-id="44be3-138">hello number of nodes is below or close toohello HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="44be3-139">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="44be3-139">Resolution steps</span></span> 

1. <span data-ttu-id="44be3-140">Obter status de saudação do hello que HDFS no hello HDInsight cluster executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="44be3-140">Get hello status of hello HDFS on hello HDInsight cluster by running hello following commands:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   ```

   ```apache
   hdiuser@hn0-spark2:~$ hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   Safe mode is ON
   Configured Capacity: 3372381241344 (3.07 TB)
   Present Capacity: 3138625077248 (2.85 TB)
   DFS Remaining: 3102710317056 (2.82 TB)
   DFS Used: 35914760192 (33.45 GB)
   DFS Used%: 1.14%
   Under replicated blocks: 0
   Blocks with corrupt replicas: 0
   Missing blocks: 0
   Missing blocks (with replication factor 1): 0

   -------------------------------------------------
   Live datanodes (8):

   Name: 10.0.0.17:30010 (10.0.0.17)
   Hostname: 10.0.0.17
   Decommission Status : Normal
   Configured Capacity: 421547655168 (392.60 GB)
   DFS Used: 5288128512 (4.92 GB)
   Non DFS Used: 29087272960 (27.09 GB)
   DFS Remaining: 387172253696 (360.58 GB)
   DFS Used%: 1.25%
   DFS Remaining%: 91.85%
   Configured Cache Capacity: 0 (0 B)
   Cache Used: 0 (0 B)
   Cache Remaining: 0 (0 B)
   Cache Used%: 100.00%
   Cache Remaining%: 0.00%
   Xceivers: 2
   Last contact: Wed Apr 05 16:22:00 UTC 2017
   ...

   ```
2. <span data-ttu-id="44be3-141">Você também pode verificar integridade de saudação do hello que HDFS no hello HDInsight cluster usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="44be3-141">You also can check hello integrity of hello HDFS on hello HDInsight cluster by using hello following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting toonamenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
   FSCK started by hdiuser (auth:SIMPLE) from /10.0.0.22 for path / at Wed Apr 05 16:40:28 UTC 2017
   ....................................................................................................

   ....................................................................................................
   ..................Status: HEALTHY
   Total size:    9330539472 B
   Total dirs:    37
   Total files:   2618
   Total symlinks:                0 (Files currently being written: 2)
   Total blocks (validated):      2535 (avg. block size 3680686 B)
   Minimally replicated blocks:   2535 (100.0 %)
   Over-replicated blocks:        0 (0.0 %)
   Under-replicated blocks:       0 (0.0 %)
   Mis-replicated blocks:         0 (0.0 %)
   Default replication factor:    3
   Average block replication:     3.0
   Corrupt blocks:                0
   Missing replicas:              0 (0.0 %)
   Number of data-nodes:          8
   Number of racks:               1
   FSCK ended at Wed Apr 05 16:40:28 UTC 2017 in 187 milliseconds

   hello filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="44be3-142">Se você determinar que não há nenhum bloco ausente, corrompido ou under-replicado ou que os blocos podem ser ignorados, execute Olá nó de nome do comando tootake Olá fora do modo de segurança a seguir:</span><span class="sxs-lookup"><span data-stu-id="44be3-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run hello following command tootake hello name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="44be3-143">Como corrigir problemas de conectividade de JDBC ou SQLLine com o Apache Phoenix</span><span class="sxs-lookup"><span data-stu-id="44be3-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="44be3-144">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="44be3-144">Resolution steps</span></span>

<span data-ttu-id="44be3-145">tooconnect com Phoenix, você deve fornecer o endereço IP de saudação de um nó ativo do ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="44be3-145">tooconnect with Phoenix, you must provide hello IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="44be3-146">Certifique-se de que Olá ZooKeeper serviço toowhich sqlline.py está tentando tooconnect está em execução.</span><span class="sxs-lookup"><span data-stu-id="44be3-146">Ensure that hello ZooKeeper service toowhich sqlline.py is trying tooconnect is up and running.</span></span>
1. <span data-ttu-id="44be3-147">Entre no toohello cluster HDInsight usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="44be3-147">Sign in toohello HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="44be3-148">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="44be3-148">Enter hello following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="44be3-149">Você pode obter o endereço IP de saudação do nó ativo de ZooKeeper Olá de saudação Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="44be3-149">You can get hello IP address of hello active ZooKeeper node from hello Ambari UI.</span></span> <span data-ttu-id="44be3-150">Vá muito**HBase** > **Links rápidos** > **ZK\* (ativo)** > **Zookeeper informações**.</span><span class="sxs-lookup"><span data-stu-id="44be3-150">Go too**HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="44be3-151">Se sqlline.py Olá conecta tooPhoenix e faz excede o tempo limite, comando a seguir Olá execução toovalidate disponibilidade de saudação e a integridade de Phoenix:</span><span class="sxs-lookup"><span data-stu-id="44be3-151">If hello sqlline.py connects tooPhoenix and does not timeout, run hello following command toovalidate hello availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="44be3-152">Se esse comando funcionar, não haverá nenhum problema.</span><span class="sxs-lookup"><span data-stu-id="44be3-152">If this command works, there is no issue.</span></span> <span data-ttu-id="44be3-153">endereço IP Hello fornecido pelo usuário Olá pode estar incorreto.</span><span class="sxs-lookup"><span data-stu-id="44be3-153">hello IP address provided by hello user might be incorrect.</span></span> <span data-ttu-id="44be3-154">No entanto, se o comando Olá pausa por um longo período e, em seguida, exibe o saudação erro a seguir, continue toostep 5.</span><span class="sxs-lookup"><span data-stu-id="44be3-154">However, if hello command pauses for an extended time and then displays hello following error, continue toostep 5.</span></span>

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="44be3-155">Execute Olá comandos a seguir da condição de saudação do hello nó principal (hn0) toodiagnose de saudação Phoenix sistema. Tabela de catálogo:</span><span class="sxs-lookup"><span data-stu-id="44be3-155">Run hello following commands from hello head node (hn0) toodiagnose hello condition of hello Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="44be3-156">comando Olá deve retornar uma erro semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="44be3-156">hello command should return an error similar toohello following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="44be3-157">Olá Ambari UI, execute Olá após o serviço de HMaster de saudação do etapas toorestart em todos os nós de ZooKeeper:</span><span class="sxs-lookup"><span data-stu-id="44be3-157">In hello Ambari UI, complete hello following steps toorestart hello HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="44be3-158">Em Olá **resumo** seção do HBase, ir muito**HBase** > **ativo HBase mestre**.</span><span class="sxs-lookup"><span data-stu-id="44be3-158">In hello **Summary** section of HBase, go too**HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="44be3-159">Em Olá **componentes** seção, reinicie o serviço do HBase mestre hello.</span><span class="sxs-lookup"><span data-stu-id="44be3-159">In hello **Components** section, restart hello HBase Master service.</span></span>
    3. <span data-ttu-id="44be3-160">Repita essas etapas para todos os serviços **Standby HBase Master** restantes.</span><span class="sxs-lookup"><span data-stu-id="44be3-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="44be3-161">Pode levar até toofive minutos para Olá HBase mestre serviço toostabilize e concluir o processo de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="44be3-161">It can take up toofive minutes for hello HBase Master service toostabilize and finish hello recovery process.</span></span> <span data-ttu-id="44be3-162">Depois de alguns minutos, repita Olá sqlline.py comandos tooconfirm que Olá sistema. Tabela de catálogo está ativo e que ele pode ser consultado.</span><span class="sxs-lookup"><span data-stu-id="44be3-162">After a few minutes, repeat hello sqlline.py commands tooconfirm that hello SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="44be3-163">Olá ao sistema. Tabela de catálogo é toonormal voltar, Olá conectividade problema tooPhoenix deve ser resolvido automaticamente.</span><span class="sxs-lookup"><span data-stu-id="44be3-163">When hello SYSTEM.CATALOG table is back toonormal, hello connectivity issue tooPhoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-toofail-toostart"></a><span data-ttu-id="44be3-164">O que faz com que um servidor mestre toofail toostart</span><span class="sxs-lookup"><span data-stu-id="44be3-164">What causes a master server toofail toostart</span></span>

### <a name="error"></a><span data-ttu-id="44be3-165">Erro</span><span class="sxs-lookup"><span data-stu-id="44be3-165">Error</span></span> 

<span data-ttu-id="44be3-166">Uma falha de renomeação atômica ocorre.</span><span class="sxs-lookup"><span data-stu-id="44be3-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="44be3-167">Descrição detalhada</span><span class="sxs-lookup"><span data-stu-id="44be3-167">Detailed description</span></span>

<span data-ttu-id="44be3-168">Durante o processo de inicialização de saudação HMaster conclui muitas etapas de inicialização.</span><span class="sxs-lookup"><span data-stu-id="44be3-168">During hello startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="44be3-169">Isso inclui a movimentação de dados desde o início da saudação (. tmp) pasta toohello pasta de dados.</span><span class="sxs-lookup"><span data-stu-id="44be3-169">These include moving data from hello scratch (.tmp) folder toohello data folder.</span></span> <span data-ttu-id="44be3-170">HMaster também analisa Olá toosee de pasta de logs write-ahead (WALs) se não houver nenhum servidor de região não responder, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="44be3-170">HMaster also looks at hello write-ahead logs (WALs) folder toosee if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="44be3-171">Durante a inicialização, o HMaster executa um comando `list` básico nessas pastas.</span><span class="sxs-lookup"><span data-stu-id="44be3-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="44be3-172">Se, a qualquer momento, o HMaster detectar um arquivo inesperado em qualquer uma dessas pastas, ele lançará uma exceção e não iniciará.</span><span class="sxs-lookup"><span data-stu-id="44be3-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="44be3-173">Causa provável</span><span class="sxs-lookup"><span data-stu-id="44be3-173">Probable cause</span></span>

<span data-ttu-id="44be3-174">Nos logs do servidor de região Olá, tente tooidentify Olá da linha do tempo de criação do arquivo hello e, em seguida, ver se houve que uma falha no processo ao redor do arquivo de saudação do tempo de saudação foi criada.</span><span class="sxs-lookup"><span data-stu-id="44be3-174">In hello region server logs, try tooidentify hello timeline of hello file creation, and then see if there was a process crash around hello time hello file was created.</span></span> <span data-ttu-id="44be3-175">(Entre em contato com HBase suporte tooassist você faz isso.) Isso nos ajuda a fornecer mecanismos mais robustos, para que você evite esse bug e garanta desligamentos de processo normais.</span><span class="sxs-lookup"><span data-stu-id="44be3-175">(Contact HBase support tooassist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="44be3-176">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="44be3-176">Resolution steps</span></span>

<span data-ttu-id="44be3-177">Verifique a pilha de chamadas de saudação e tente toodetermine qual pasta pode estar causando o problema de saudação (por exemplo, talvez ele esteja Olá WALs ou a pasta do hello. tmp).</span><span class="sxs-lookup"><span data-stu-id="44be3-177">Check hello call stack and try toodetermine which folder might be causing hello problem (for instance, it might be hello WALs folder or hello .tmp folder).</span></span> <span data-ttu-id="44be3-178">Em seguida, no Pesquisador de objetos de nuvem ou usando comandos do HDFS, tente arquivo com problema toolocate hello.</span><span class="sxs-lookup"><span data-stu-id="44be3-178">Then, in Cloud Explorer or by using HDFS commands, try toolocate hello problem file.</span></span> <span data-ttu-id="44be3-179">Geralmente, é um arquivo \*-renamePending.json.</span><span class="sxs-lookup"><span data-stu-id="44be3-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="44be3-180">(Olá \*-renamePending.json arquivo é um arquivo de diário que usou a operação de renomeação atômica Olá tooimplement no driver WASB hello.</span><span class="sxs-lookup"><span data-stu-id="44be3-180">(hello \*-renamePending.json file is a journal file that's used tooimplement hello atomic rename operation in hello WASB driver.</span></span> <span data-ttu-id="44be3-181">Conclusão toobugs nesta implementação, esses arquivos podem ser restantes após falhas de processo e assim por diante.) Force a exclusão desse arquivo no Cloud Explorer ou usando os comandos do HDFS.</span><span class="sxs-lookup"><span data-stu-id="44be3-181">Due toobugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="44be3-182">Às vezes, pode haver um arquivo temporário com um nome parecido com *$$$.$$$* nesse local.</span><span class="sxs-lookup"><span data-stu-id="44be3-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="44be3-183">Você tem toouse HDFS `ls` comando toosee esse arquivo; você não puder ver o arquivo hello no Pesquisador de objetos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="44be3-183">You have toouse HDFS `ls` command toosee this file; you cannot see hello file in Cloud Explorer.</span></span> <span data-ttu-id="44be3-184">toodelete esse arquivo, use Olá HDFS comando `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span><span class="sxs-lookup"><span data-stu-id="44be3-184">toodelete this file, use hello HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="44be3-185">Após a execução desses comandos, o HMaster deve iniciar imediatamente.</span><span class="sxs-lookup"><span data-stu-id="44be3-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="44be3-186">Erro</span><span class="sxs-lookup"><span data-stu-id="44be3-186">Error</span></span>

<span data-ttu-id="44be3-187">Nenhum endereço de servidor está listado em *hbase: meta* para a região xxx.</span><span class="sxs-lookup"><span data-stu-id="44be3-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="44be3-188">Descrição detalhada</span><span class="sxs-lookup"><span data-stu-id="44be3-188">Detailed description</span></span>

<span data-ttu-id="44be3-189">Você poderá ver uma mensagem no cluster do Linux que indica que Olá *hbase: meta* tabela não está online.</span><span class="sxs-lookup"><span data-stu-id="44be3-189">You might see a message on your Linux cluster that indicates that hello *hbase: meta* table is not online.</span></span> <span data-ttu-id="44be3-190">A execução de `hbck` pode relatar que "replicaId 0 da tabela hbase: meta não foi encontrado em nenhuma região".</span><span class="sxs-lookup"><span data-stu-id="44be3-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="44be3-191">problema de saudação pode ser HMaster não foi possível inicializar após reinicialização do HBase.</span><span class="sxs-lookup"><span data-stu-id="44be3-191">hello problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="44be3-192">Nos logs de HMaster hello, você poderá ver a mensagem de saudação: "nenhum endereço de servidor listado no hbase: meta para região hbase: backup \<nome da região\>".</span><span class="sxs-lookup"><span data-stu-id="44be3-192">In hello HMaster logs, you might see hello message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="44be3-193">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="44be3-193">Resolution steps</span></span>

1. <span data-ttu-id="44be3-194">No shell do HBase do hello, digite Olá comandos (alteração de valores reais conforme aplicável) a seguir:</span><span class="sxs-lookup"><span data-stu-id="44be3-194">In hello HBase shell, enter hello following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="44be3-195">Excluir Olá *hbase: namespace* entrada.</span><span class="sxs-lookup"><span data-stu-id="44be3-195">Delete hello *hbase: namespace* entry.</span></span> <span data-ttu-id="44be3-196">Essa entrada pode ser Olá igual ao que está sendo relatado quando hello *hbase: namespace* tabela é verificada.</span><span class="sxs-lookup"><span data-stu-id="44be3-196">This entry might be hello same error that's being reported when hello *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="44be3-197">toobring backup HBase em um estado em execução, Olá Ambari UI, reinicie o serviço de Active HMaster de saudação.</span><span class="sxs-lookup"><span data-stu-id="44be3-197">toobring up HBase in a running state, in hello Ambari UI, restart hello Active HMaster service.</span></span>  

4. <span data-ttu-id="44be3-198">Na saudação shell do HBase, toobring todas as tabelas offline, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="44be3-198">In hello HBase shell, toobring up all offline tables, run hello following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="44be3-199">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="44be3-199">Additional reading</span></span>

[<span data-ttu-id="44be3-200">Tabela do HBase Olá tooprocess não é possível</span><span class="sxs-lookup"><span data-stu-id="44be3-200">Unable tooprocess hello HBase table</span></span>](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a><span data-ttu-id="44be3-201">Erro</span><span class="sxs-lookup"><span data-stu-id="44be3-201">Error</span></span>

<span data-ttu-id="44be3-202">HMaster expirar com um too"java.io.IOException semelhante de exceção fatal: 300000ms Timedout aguardando namespace tabela toobe atribuído."</span><span class="sxs-lookup"><span data-stu-id="44be3-202">HMaster times out with a fatal exception similar too"java.io.IOException: Timedout 300000ms waiting for namespace table toobe assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="44be3-203">Descrição detalhada</span><span class="sxs-lookup"><span data-stu-id="44be3-203">Detailed description</span></span>

<span data-ttu-id="44be3-204">Você pode enfrentar esse problema se tiver muitas tabelas e regiões que não foram liberadas ao reiniciar os serviços do HMaster.</span><span class="sxs-lookup"><span data-stu-id="44be3-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="44be3-205">Reinicialização falhe, e você verá Olá anterior a mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="44be3-205">Restart might fail, and you'll see hello preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="44be3-206">Causa provável</span><span class="sxs-lookup"><span data-stu-id="44be3-206">Probable cause</span></span>

<span data-ttu-id="44be3-207">Este é um problema conhecido com hello HMaster serviço.</span><span class="sxs-lookup"><span data-stu-id="44be3-207">This is a known issue with hello HMaster service.</span></span> <span data-ttu-id="44be3-208">Tarefas de inicialização de cluster geral podem levar muito tempo.</span><span class="sxs-lookup"><span data-stu-id="44be3-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="44be3-209">HMaster desligado porque a tabela de namespace Olá ainda não está atribuída.</span><span class="sxs-lookup"><span data-stu-id="44be3-209">HMaster shuts down because hello namespace table isn’t yet assigned.</span></span> <span data-ttu-id="44be3-210">Isso ocorre somente em cenários nos quais não há uma grande quantidade de dados não liberados, e um tempo limite de cinco minutos não é suficiente.</span><span class="sxs-lookup"><span data-stu-id="44be3-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="44be3-211">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="44be3-211">Resolution steps</span></span>

1. <span data-ttu-id="44be3-212">Olá Ambari UI, ir muito**HBase** > **configurações**.</span><span class="sxs-lookup"><span data-stu-id="44be3-212">In hello Ambari UI, go too**HBase** > **Configs**.</span></span> <span data-ttu-id="44be3-213">No arquivo de hbase-site.XML personalizado de hello, adicione Olá configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="44be3-213">In hello custom hbase-site.xml file, add hello following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="44be3-214">Reinicie os serviços de saudação necessário (HMaster e possivelmente outros serviços do HBase).</span><span class="sxs-lookup"><span data-stu-id="44be3-214">Restart hello required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="44be3-215">O que causa uma falha de reinicialização em um servidor de região</span><span class="sxs-lookup"><span data-stu-id="44be3-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="44be3-216">Problema</span><span class="sxs-lookup"><span data-stu-id="44be3-216">Issue</span></span>

<span data-ttu-id="44be3-217">É possível impedir uma falha de reinicialização em um servidor de região seguindo estas práticas recomendadas.</span><span class="sxs-lookup"><span data-stu-id="44be3-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="44be3-218">É recomendável que você pausa atividade da carga de trabalho pesada quando você estiver planejando servidores de região HBase toorestart.</span><span class="sxs-lookup"><span data-stu-id="44be3-218">We recommend that you pause heavy workload activity when you are planning toorestart HBase region servers.</span></span> <span data-ttu-id="44be3-219">Se um aplicativo continua tooconnect com servidores de região ao desligamento está em andamento, operação de reinicialização do servidor de região hello serão mais lenta por vários minutos.</span><span class="sxs-lookup"><span data-stu-id="44be3-219">If an application continues tooconnect with region servers when shutdown is in progress, hello region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="44be3-220">Além disso, é um toofirst boa ideia liberação de que todas as tabelas de hello.</span><span class="sxs-lookup"><span data-stu-id="44be3-220">Also, it's a good idea toofirst flush all hello tables.</span></span> <span data-ttu-id="44be3-221">Para obter uma referência sobre como tooflush tabelas, consulte [HDInsight HBase: como cluster de HBase tooimprove Olá tempo de reinicialização, liberando tabelas](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span><span class="sxs-lookup"><span data-stu-id="44be3-221">For a reference on how tooflush tables, see [HDInsight HBase: How tooimprove hello HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="44be3-222">Se você iniciar a operação de reinicialização de saudação em servidores de região HBase de saudação Ambari UI, você ver imediatamente que servidores de região Olá foi desativado, mas eles não reiniciar imediatamente.</span><span class="sxs-lookup"><span data-stu-id="44be3-222">If you initiate hello restart operation on HBase region servers from hello Ambari UI, you immediately see that hello region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="44be3-223">Aqui está o que está acontecendo em segundo plano da saudação:</span><span class="sxs-lookup"><span data-stu-id="44be3-223">Here's what's happening behind hello scenes:</span></span> 

1. <span data-ttu-id="44be3-224">agente do Ambari Olá envia um servidor de região de toohello de solicitação de parada.</span><span class="sxs-lookup"><span data-stu-id="44be3-224">hello Ambari agent sends a stop request toohello region server.</span></span>
2. <span data-ttu-id="44be3-225">Olá Ambari agent espera 30 segundos para Olá região servidor tooshut para baixo normalmente.</span><span class="sxs-lookup"><span data-stu-id="44be3-225">hello Ambari agent waits for 30 seconds for hello region server tooshut down gracefully.</span></span> 
3. <span data-ttu-id="44be3-226">Se seu aplicativo continua tooconnect com o servidor de região hello, o servidor de saudação não desligado imediatamente.</span><span class="sxs-lookup"><span data-stu-id="44be3-226">If your application continues tooconnect with hello region server, hello server won't shut down immediately.</span></span> <span data-ttu-id="44be3-227">tempo limite de 30 segundos Olá expira antes que ocorra de desligamento.</span><span class="sxs-lookup"><span data-stu-id="44be3-227">hello 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="44be3-228">Depois de 30 segundos, o agente de Ambari de saudação envia um kill force (`kill -9`) servidor do comando toohello região.</span><span class="sxs-lookup"><span data-stu-id="44be3-228">After 30 seconds, hello Ambari agent sends a force-kill (`kill -9`) command toohello region server.</span></span> <span data-ttu-id="44be3-229">Você pode ver isso no log de agente ambari hello (em Olá /var diretório do nó do respectivos trabalho Olá):</span><span class="sxs-lookup"><span data-stu-id="44be3-229">You can see this in hello ambari-agent log (in hello /var/log/ directory of hello respective worker node):</span></span>

   ```apache
           2017-03-21 13:22:09,171 - Execute['/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/current/hbase-regionserver/conf stop regionserver'] {'only_if': 'ambari-sudo.sh  -H -E t
           est -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1', 'on_timeout': '! ( ambari-sudo.sh  -H -E test -
           f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H 
           -E cat /var/run/hbase/hbase-hbase-regionserver.pid`', 'timeout': 30, 'user': 'hbase'}
           2017-03-21 13:22:40,268 - Executing '! ( ambari-sudo.sh  -H -E test -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >
           /dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid`'. Reason: Execution of 'ambari-sudo.sh su hbase -l -s /bin/bash -c 'export  
           PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/var/lib/ambari-agent ; /usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/curre
           nt/hbase-regionserver/conf stop regionserver was killed due timeout after 30 seconds
           2017-03-21 13:22:40,285 - File['/var/run/hbase/hbase-hbase-regionserver.pid'] {'action': ['delete']}
           2017-03-21 13:22:40,285 - Deleting File['/var/run/hbase/hbase-hbase-regionserver.pid']
   ```
<span data-ttu-id="44be3-230">Devido ao desligamento inesperado do hello, porta Olá associada Olá processo pode não ser liberada, mesmo que o processo do servidor de região Olá é interrompido.</span><span class="sxs-lookup"><span data-stu-id="44be3-230">Because of hello abrupt shutdown, hello port associated with hello process might not be released, even though hello region server process is stopped.</span></span> <span data-ttu-id="44be3-231">Essa situação pode levar tooan AddressBindException durante a inicialização do servidor da região hello, conforme mostrado no hello logs a seguir.</span><span class="sxs-lookup"><span data-stu-id="44be3-231">This situation can lead tooan AddressBindException when hello region server is starting, as shown in hello following logs.</span></span> <span data-ttu-id="44be3-232">Você pode verificar isso na região Olá-log no diretório de /var/log/hbase Olá em nós de trabalho Olá onde o servidor de região Olá falha toostart.</span><span class="sxs-lookup"><span data-stu-id="44be3-232">You can verify this in hello region-server.log in hello /var/log/hbase directory on hello worker nodes where hello region server fails toostart.</span></span> 

   ```apache

   2017-03-21 13:25:47,061 ERROR [main] regionserver.HRegionServerCommandLine: Region server exiting
   java.lang.RuntimeException: Failed construction of Regionserver: class org.apache.hadoop.hbase.regionserver.HRegionServer
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2636)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.start(HRegionServerCommandLine.java:64)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.run(HRegionServerCommandLine.java:87)
   at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
   at org.apache.hadoop.hbase.util.ServerCommandLine.doMain(ServerCommandLine.java:126)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.main(HRegionServer.java:2651)
        
   Caused by: java.lang.reflect.InvocationTargetException
   at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
   at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
   at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
   at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2634)
   ... 5 more
        
   Caused by: java.net.BindException: Problem binding too/10.2.0.4:16020 : Address already in use
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2497)
   at org.apache.hadoop.hbase.ipc.RpcServer$Listener.<init>(RpcServer.java:580)
   at org.apache.hadoop.hbase.ipc.RpcServer.<init>(RpcServer.java:1982)
   at org.apache.hadoop.hbase.regionserver.RSRpcServices.<init>(RSRpcServices.java:863)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.createRpcServices(HRegionServer.java:632)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.<init>(HRegionServer.java:532)
   ... 10 more
        
   Caused by: java.net.BindException: Address already in use
   at sun.nio.ch.Net.bind0(Native Method)
   at sun.nio.ch.Net.bind(Net.java:463)
   at sun.nio.ch.Net.bind(Net.java:455)
   at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
   at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2495)
   ... 15 more
   ```

### <a name="resolution-steps"></a><span data-ttu-id="44be3-233">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="44be3-233">Resolution steps</span></span>

1. <span data-ttu-id="44be3-234">Tente tooreduce Olá carga nos servidores de região Olá HBase antes de iniciar uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="44be3-234">Try tooreduce hello load on hello HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="44be3-235">Como alternativa tente toomanually reinicialização região servidores de nós de trabalho hello usando Olá a seguir (se a etapa 1 não ajuda), comandos:</span><span class="sxs-lookup"><span data-stu-id="44be3-235">Alternatively (if step 1 doesn't help), try toomanually restart region servers on hello worker nodes by using hello following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

