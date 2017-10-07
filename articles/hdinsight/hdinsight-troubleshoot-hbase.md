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
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a>Solucionar problemas do HBase usando o Azure HDInsight

Saiba mais sobre questões hello e suas resoluções durante o trabalho com cargas Apache HBase no Apache Ambari.

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a>Como fazer para executar relatórios de comando hbck com várias regiões não atribuídas

Uma mensagem de erro comuns que você pode ver quando você executa Olá `hbase hbck` comando é "várias regiões que não está sendo atribuídas ou falhas na cadeia de saudação do regiões."

Em Olá UI HBase mestre, você pode ver o número de saudação das regiões que estão desbalanceadas entre todos os servidores de região. Em seguida, você pode executar `hbase hbck` toosee falhas na cadeia de região de saudação do comando.

Falhas podem ser causadas por regiões offline de hello, caso atribuições de saudação de correção primeiro. 

toobring Olá estado normal de retorno tooa regiões não atribuídos, conclua Olá etapas a seguir:

1. Entre no toohello cluster HDInsight HBase usando o SSH.
2. tooconnect com o shell de ZooKeeper hello, executar Olá `hbase zkcli` comando.
3. Executar Olá `rmr /hbase/regions-in-transition` comando ou hello `rmr /hbase-unsecure/regions-in-transition` comando.
4. tooexit de saudação `hbase zkcli` do shell, use Olá `exit` comando.
5. Abra Olá Apache Ambari UI e, em seguida, reinicie o serviço de Active HBase mestre de hello.
6. Executar Olá `hbase hbck` comando novamente (sem opções). Verifique a saída de saudação de tooensure esse comando que estão sendo atribuídas a todas as regiões.


## <a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Como fazer para corrigir problemas de tempo limite usando comandos hbck para atribuições de região

### <a name="issue"></a>Problema

Uma causa potencial de problemas de tempo limite quando você usar o hello `hbck` comando pode ser que várias regiões estão em hello "em transição" estado por um longo tempo. Você pode ver essas regiões como offline nos Olá UI HBase mestre. Porque um grande número de regiões está tentando tootransition, o mestre do HBase talvez tempo limite e ser toobring não é possível essas regiões online novamente.

### <a name="resolution-steps"></a>Etapas de resolução

1. Entre no toohello cluster HDInsight HBase usando o SSH.
2. tooconnect com o shell de ZooKeeper hello, executar Olá `hbase zkcli` comando.
3. Executar Olá `rmr /hbase/regions-in-transition` ou hello `rmr /hbase-unsecure/regions-in-transition` comando.
4. Olá tooexit `hbase zkcli` do shell, use Olá `exit` comando.
5. Em Olá Ambari UI, reinicie o serviço de Active HBase mestre de saudação.
6. Executar Olá `hbase hbck -fixAssignments` comando novamente.

## <a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Como forçar a desabilitação do modo de segurança de HDFS em um cluster

### <a name="issue"></a>Problema

Olá local Hadoop distribuídas arquivo de sistema (HDFS) está preso no modo de segurança no cluster do HDInsight hello.

### <a name="detailed-description"></a>Descrição detalhada

Esse erro pode ser causado por uma falha ao executar Olá HDFS comando a seguir:

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

Erro de saudação que podem ocorrer ao tentar o comando de saudação toorun tem esta aparência:

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

### <a name="probable-cause"></a>Causa provável

Olá cluster HDInsight foi reduzida tooa muito alguns nós. número de saudação de nós está abaixo ou feche o fator de replicação de HDFS toohello.

### <a name="resolution-steps"></a>Etapas de resolução 

1. Obter status de saudação do hello que HDFS no hello HDInsight cluster executando Olá comandos a seguir:

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
2. Você também pode verificar integridade de saudação do hello que HDFS no hello HDInsight cluster usando Olá comandos a seguir:

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

3. Se você determinar que não há nenhum bloco ausente, corrompido ou under-replicado ou que os blocos podem ser ignorados, execute Olá nó de nome do comando tootake Olá fora do modo de segurança a seguir:

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a>Como corrigir problemas de conectividade de JDBC ou SQLLine com o Apache Phoenix

### <a name="resolution-steps"></a>Etapas de resolução

tooconnect com Phoenix, você deve fornecer o endereço IP de saudação de um nó ativo do ZooKeeper. Certifique-se de que Olá ZooKeeper serviço toowhich sqlline.py está tentando tooconnect está em execução.
1. Entre no toohello cluster HDInsight usando o SSH.
2. Digite hello comando a seguir:
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > Você pode obter o endereço IP de saudação do nó ativo de ZooKeeper Olá de saudação Ambari UI. Vá muito**HBase** > **Links rápidos** > **ZK\* (ativo)** > **Zookeeper informações**. 

3. Se sqlline.py Olá conecta tooPhoenix e faz excede o tempo limite, comando a seguir Olá execução toovalidate disponibilidade de saudação e a integridade de Phoenix:

   ```apache
           !tables
           !quit
   ```      
4. Se esse comando funcionar, não haverá nenhum problema. endereço IP Hello fornecido pelo usuário Olá pode estar incorreto. No entanto, se o comando Olá pausa por um longo período e, em seguida, exibe o saudação erro a seguir, continue toostep 5.

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. Execute Olá comandos a seguir da condição de saudação do hello nó principal (hn0) toodiagnose de saudação Phoenix sistema. Tabela de catálogo:

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   comando Olá deve retornar uma erro semelhante toohello a seguir: 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. Olá Ambari UI, execute Olá após o serviço de HMaster de saudação do etapas toorestart em todos os nós de ZooKeeper:

    1. Em Olá **resumo** seção do HBase, ir muito**HBase** > **ativo HBase mestre**. 
    2. Em Olá **componentes** seção, reinicie o serviço do HBase mestre hello.
    3. Repita essas etapas para todos os serviços **Standby HBase Master** restantes. 

Pode levar até toofive minutos para Olá HBase mestre serviço toostabilize e concluir o processo de recuperação de saudação. Depois de alguns minutos, repita Olá sqlline.py comandos tooconfirm que Olá sistema. Tabela de catálogo está ativo e que ele pode ser consultado. 

Olá ao sistema. Tabela de catálogo é toonormal voltar, Olá conectividade problema tooPhoenix deve ser resolvido automaticamente.


## <a name="what-causes-a-master-server-toofail-toostart"></a>O que faz com que um servidor mestre toofail toostart

### <a name="error"></a>Erro 

Uma falha de renomeação atômica ocorre.

### <a name="detailed-description"></a>Descrição detalhada

Durante o processo de inicialização de saudação HMaster conclui muitas etapas de inicialização. Isso inclui a movimentação de dados desde o início da saudação (. tmp) pasta toohello pasta de dados. HMaster também analisa Olá toosee de pasta de logs write-ahead (WALs) se não houver nenhum servidor de região não responder, e assim por diante. 

Durante a inicialização, o HMaster executa um comando `list` básico nessas pastas. Se, a qualquer momento, o HMaster detectar um arquivo inesperado em qualquer uma dessas pastas, ele lançará uma exceção e não iniciará.  

### <a name="probable-cause"></a>Causa provável

Nos logs do servidor de região Olá, tente tooidentify Olá da linha do tempo de criação do arquivo hello e, em seguida, ver se houve que uma falha no processo ao redor do arquivo de saudação do tempo de saudação foi criada. (Entre em contato com HBase suporte tooassist você faz isso.) Isso nos ajuda a fornecer mecanismos mais robustos, para que você evite esse bug e garanta desligamentos de processo normais.

### <a name="resolution-steps"></a>Etapas de resolução

Verifique a pilha de chamadas de saudação e tente toodetermine qual pasta pode estar causando o problema de saudação (por exemplo, talvez ele esteja Olá WALs ou a pasta do hello. tmp). Em seguida, no Pesquisador de objetos de nuvem ou usando comandos do HDFS, tente arquivo com problema toolocate hello. Geralmente, é um arquivo \*-renamePending.json. (Olá \*-renamePending.json arquivo é um arquivo de diário que usou a operação de renomeação atômica Olá tooimplement no driver WASB hello. Conclusão toobugs nesta implementação, esses arquivos podem ser restantes após falhas de processo e assim por diante.) Force a exclusão desse arquivo no Cloud Explorer ou usando os comandos do HDFS. 

Às vezes, pode haver um arquivo temporário com um nome parecido com *$$$.$$$* nesse local. Você tem toouse HDFS `ls` comando toosee esse arquivo; você não puder ver o arquivo hello no Pesquisador de objetos de nuvem. toodelete esse arquivo, use Olá HDFS comando `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.  

Após a execução desses comandos, o HMaster deve iniciar imediatamente. 

### <a name="error"></a>Erro

Nenhum endereço de servidor está listado em *hbase: meta* para a região xxx.

### <a name="detailed-description"></a>Descrição detalhada

Você poderá ver uma mensagem no cluster do Linux que indica que Olá *hbase: meta* tabela não está online. A execução de `hbck` pode relatar que "replicaId 0 da tabela hbase: meta não foi encontrado em nenhuma região". problema de saudação pode ser HMaster não foi possível inicializar após reinicialização do HBase. Nos logs de HMaster hello, você poderá ver a mensagem de saudação: "nenhum endereço de servidor listado no hbase: meta para região hbase: backup \<nome da região\>".  

### <a name="resolution-steps"></a>Etapas de resolução

1. No shell do HBase do hello, digite Olá comandos (alteração de valores reais conforme aplicável) a seguir:  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. Excluir Olá *hbase: namespace* entrada. Essa entrada pode ser Olá igual ao que está sendo relatado quando hello *hbase: namespace* tabela é verificada.

3. toobring backup HBase em um estado em execução, Olá Ambari UI, reinicie o serviço de Active HMaster de saudação.  

4. Na saudação shell do HBase, toobring todas as tabelas offline, execute Olá comando a seguir:

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a>Leitura adicional

[Tabela do HBase Olá tooprocess não é possível](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a>Erro

HMaster expirar com um too"java.io.IOException semelhante de exceção fatal: 300000ms Timedout aguardando namespace tabela toobe atribuído."

### <a name="detailed-description"></a>Descrição detalhada

Você pode enfrentar esse problema se tiver muitas tabelas e regiões que não foram liberadas ao reiniciar os serviços do HMaster. Reinicialização falhe, e você verá Olá anterior a mensagem de erro.  

### <a name="probable-cause"></a>Causa provável

Este é um problema conhecido com hello HMaster serviço. Tarefas de inicialização de cluster geral podem levar muito tempo. HMaster desligado porque a tabela de namespace Olá ainda não está atribuída. Isso ocorre somente em cenários nos quais não há uma grande quantidade de dados não liberados, e um tempo limite de cinco minutos não é suficiente.
  
### <a name="resolution-steps"></a>Etapas de resolução

1. Olá Ambari UI, ir muito**HBase** > **configurações**. No arquivo de hbase-site.XML personalizado de hello, adicione Olá configuração a seguir: 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. Reinicie os serviços de saudação necessário (HMaster e possivelmente outros serviços do HBase).  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a>O que causa uma falha de reinicialização em um servidor de região

### <a name="issue"></a>Problema

É possível impedir uma falha de reinicialização em um servidor de região seguindo estas práticas recomendadas. É recomendável que você pausa atividade da carga de trabalho pesada quando você estiver planejando servidores de região HBase toorestart. Se um aplicativo continua tooconnect com servidores de região ao desligamento está em andamento, operação de reinicialização do servidor de região hello serão mais lenta por vários minutos. Além disso, é um toofirst boa ideia liberação de que todas as tabelas de hello. Para obter uma referência sobre como tooflush tabelas, consulte [HDInsight HBase: como cluster de HBase tooimprove Olá tempo de reinicialização, liberando tabelas](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).

Se você iniciar a operação de reinicialização de saudação em servidores de região HBase de saudação Ambari UI, você ver imediatamente que servidores de região Olá foi desativado, mas eles não reiniciar imediatamente. 

Aqui está o que está acontecendo em segundo plano da saudação: 

1. agente do Ambari Olá envia um servidor de região de toohello de solicitação de parada.
2. Olá Ambari agent espera 30 segundos para Olá região servidor tooshut para baixo normalmente. 
3. Se seu aplicativo continua tooconnect com o servidor de região hello, o servidor de saudação não desligado imediatamente. tempo limite de 30 segundos Olá expira antes que ocorra de desligamento. 
4. Depois de 30 segundos, o agente de Ambari de saudação envia um kill force (`kill -9`) servidor do comando toohello região. Você pode ver isso no log de agente ambari hello (em Olá /var diretório do nó do respectivos trabalho Olá):

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
Devido ao desligamento inesperado do hello, porta Olá associada Olá processo pode não ser liberada, mesmo que o processo do servidor de região Olá é interrompido. Essa situação pode levar tooan AddressBindException durante a inicialização do servidor da região hello, conforme mostrado no hello logs a seguir. Você pode verificar isso na região Olá-log no diretório de /var/log/hbase Olá em nós de trabalho Olá onde o servidor de região Olá falha toostart. 

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

### <a name="resolution-steps"></a>Etapas de resolução

1. Tente tooreduce Olá carga nos servidores de região Olá HBase antes de iniciar uma reinicialização. 
2. Como alternativa tente toomanually reinicialização região servidores de nós de trabalho hello usando Olá a seguir (se a etapa 1 não ajuda), comandos:

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

