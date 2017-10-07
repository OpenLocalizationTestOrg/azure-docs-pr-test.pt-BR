---
title: "os despejos de pilha de aaaEnable para serviços do Hadoop no HDInsight - Azure | Microsoft Docs"
description: "Habilite despejos de heap para serviços do Hadoop por meio de clusters do HDInsight baseados em Linux para depuração e análise."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a>Habilitar despejos heap para serviços Hadoop no HDInsight baseado em Linux

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Despejos de pilha contém um instantâneo de memória do aplicativo hello, incluindo valores hello das variáveis no tempo Olá Olá despejo foi criado. Portanto, eles são úteis para diagnosticar problemas que ocorrem no tempo de execução.

> [!IMPORTANT]
> Olá etapas deste documento só funcionam com clusters de HDInsight que usam o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="whichServices"></a>Serviços

Você pode habilitar os despejos de pilha para Olá serviços a seguir:

* **hcatalog** - tempelton
* **hive** - hiveserver2, metastore, derbyserver
* **mapreduce** - jobhistoryserver
* **yarn** - resourcemanager, nodemanager, timelineserver
* **hdfs** - datanode, secondarynamenode, namenode

Você também pode habilitar os despejos de pilha para mapa de saudação e reduzir processos executaram por HDInsight.

## <a name="configuration"></a>Compreendendo a configuração do despejo de heap

Despejos de pilha estão habilitados, passando opções (às vezes conhecido como aceita, ou parâmetros) toohello JVM quando um serviço é iniciado. Para a maioria dos serviços de Hadoop, você pode modificar essas opções Olá shell script usado toostart Olá serviço toopass.

Em cada script, há uma exportação para  **\* \_OPTS**, que contém opções de saudação passado toohello JVM. Por exemplo, em Olá **hadoop env.sh** scripts de linha de saudação que começa com `export HADOOP_NAMENODE_OPTS=` contém opções de saudação para Olá NameNode de serviço.

Mapear e reduzir os processos são um pouco diferentes, como essas operações são um processo filho de saudação MapReduce serviço. Cada mapa ou reduzir o processo é executado em um contêiner filho, e há duas entradas que contenham Olá JVM opções. Contidos em **mapred-site.xml**:

* **mapreduce.admin.map.child.java.opts**
* **mapreduce.admin.reduce.child.java.opts**

> [!NOTE]
> É recomendável usando o Ambari toomodify ambos Olá scripts e configurações mapred-site.XML, como Ambari tratar replicar alterações em nós de cluster de saudação. Consulte Olá [Ambari usando](#using-ambari) seção para etapas específicas.

### <a name="enable-heap-dumps"></a>Habilitar despejos de heap

Olá opção a seguir permite que os despejos de pilha quando ocorre um OutOfMemoryError:

    -XX:+HeapDumpOnOutOfMemoryError

Olá  **+**  indica que essa opção está habilitada. saudação padrão é disabled.

> [!WARNING]
> Despejos de pilha não estão habilitados para serviços do Hadoop no HDInsight por padrão, como arquivos de despejo Olá podem ser grandes. Se você habilitá-los para solução de problemas, lembre-se toodisable-los após ter reproduzido Olá problema e os arquivos de despejo Olá coletadas.

### <a name="dump-location"></a>Local do despejo

local de padrão de Olá Olá arquivo de despejo é o diretório de trabalho atual hello. Você pode controlar onde hello arquivo é armazenado usando Olá opção a seguir:

    -XX:HeapDumpPath=/path

Por exemplo, usando `-XX:HeapDumpPath=/tmp` faz com que o hello despejos toobe armazenado no diretório /tmp de saudação.

### <a name="scripts"></a>Scripts

Você também pode disparar um script quando um **OutOfMemoryError** ocorrer. Por exemplo, disparar uma notificação para que você saiba que esse erro Olá ocorreu. A seguir use Olá opção tootrigger um script em um __OutOfMemoryError__:

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> Como o Hadoop é um sistema distribuído, qualquer script usado deve ser colocado em todos os nós no cluster Olá Olá serviço será executado.
> 
> script Hello deve também estar em um local que seja acessível pelos Olá conta Olá o serviço é executado como e deve fornecer permissões de execução. Por exemplo, você poderá scripts toostore `/usr/local/bin` e usar `chmod go+rx /usr/local/bin/filename.sh` toogrant permissões read e execute.

## <a name="using-ambari"></a>Usando o Ambari

configuração de saudação toomodify para um serviço, Olá use as etapas a seguir:

1. Abra Olá Ambari web da interface do usuário para seu cluster. Olá URL é https://YOURCLUSTERNAME.azurehdinsight.net.

    Quando solicitado, autentique toohello site usando o nome da conta Olá HTTP (padrão: administrador) e a senha para seu cluster.

   > [!NOTE]
   > Você pode ser solicitado pela segunda vez por Ambari para Olá nome de usuário e senha. Nesse caso, digite Olá o mesmo nome de conta e senha

2. Usando a lista de saudação do hello esquerda, selecione o hello serviço área a ser toomodify. Por exemplo, **HDFS**. Na área do Centro de saudação, selecione Olá **configurações** guia.

    ![Imagem do Ambari Web com a guia de Configurações de HDFS selecionada](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. Usando Olá **filtro...**  entrada, digite **aceita**. Apenas os itens que contêm esse texto são exibidos.

    ![Lista filtrada](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. Localize Olá  **\* \_OPTS** entrada hello serviço você deseja tooenable despejos de pilha para e adicionar Olá opções que você deseja tooenable. Olá a imagem a seguir, adicionei `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entrada:

    ![HADOOP_NAMENODE_OPTS com -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > Ao habilitar despejos de pilha para Olá mapearem ou reduzem o processo filho, procure por campos Olá denominados **mapreduce.admin.map.child.java.opts** e **mapreduce.admin.reduce.child.java.opts**.

    Saudação de uso **salvar** botão toosave alterações de saudação. Você pode inserir uma breve mensagem descrevendo Olá alterações.

5. Depois que tiverem sido aplicadas alterações hello, Olá **reinicialização necessária** ícone é exibido ao lado de um ou mais serviços.

    ![botão de reinicialização necessária e botão de reinicialização](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. Selecione cada serviço que precisa de uma reinicialização e use Olá **ações de serviço** botão muito**ativar no modo de manutenção**. Modo de manutenção impede que alertas sendo gerados do serviço hello quando você reiniciá-lo.

    ![Ativar o menu do modo de manutenção](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. Depois que você tiver habilitado o modo de manutenção, use Olá **reiniciar** botão para serviço Olá muito**reiniciar todos os afetados**

    ![Entrada Reiniciar todos os afetados](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > Olá entradas para Olá **reiniciar** botão pode ser diferente para outros serviços.

8. Depois de saudação serviços foram reiniciados, use Olá **ações de serviço** botão muito**ativar desativar o modo de manutenção**. Este tooresume Ambari monitoramento de alertas para o serviço de saudação.

