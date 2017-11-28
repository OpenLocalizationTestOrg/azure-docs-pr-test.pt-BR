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
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="d4dbd-103">Habilitar despejos heap para serviços Hadoop no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="d4dbd-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="d4dbd-104">Despejos de pilha contém um instantâneo de memória do aplicativo hello, incluindo valores hello das variáveis no tempo Olá Olá despejo foi criado.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="d4dbd-105">Portanto, eles são úteis para diagnosticar problemas que ocorrem no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4dbd-106">Olá etapas deste documento só funcionam com clusters de HDInsight que usam o Linux.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-106">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="d4dbd-107">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d4dbd-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d4dbd-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="d4dbd-109"><a name="whichServices"></a>Serviços</span><span class="sxs-lookup"><span data-stu-id="d4dbd-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="d4dbd-110">Você pode habilitar os despejos de pilha para Olá serviços a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4dbd-110">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="d4dbd-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="d4dbd-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="d4dbd-112">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="d4dbd-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="d4dbd-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="d4dbd-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="d4dbd-114">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="d4dbd-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="d4dbd-115">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="d4dbd-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="d4dbd-116">Você também pode habilitar os despejos de pilha para mapa de saudação e reduzir processos executaram por HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-116">You can also enable heap dumps for hello map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="d4dbd-117"><a name="configuration"></a>Compreendendo a configuração do despejo de heap</span><span class="sxs-lookup"><span data-stu-id="d4dbd-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="d4dbd-118">Despejos de pilha estão habilitados, passando opções (às vezes conhecido como aceita, ou parâmetros) toohello JVM quando um serviço é iniciado.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) toohello JVM when a service is started.</span></span> <span data-ttu-id="d4dbd-119">Para a maioria dos serviços de Hadoop, você pode modificar essas opções Olá shell script usado toostart Olá serviço toopass.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-119">For most Hadoop services, you can modify hello shell script used toostart hello service toopass these options.</span></span>

<span data-ttu-id="d4dbd-120">Em cada script, há uma exportação para  **\* \_OPTS**, que contém opções de saudação passado toohello JVM.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-120">In each script, there is an export for **\*\_OPTS**, which contains hello options passed toohello JVM.</span></span> <span data-ttu-id="d4dbd-121">Por exemplo, em Olá **hadoop env.sh** scripts de linha de saudação que começa com `export HADOOP_NAMENODE_OPTS=` contém opções de saudação para Olá NameNode de serviço.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-121">For example, in hello **hadoop-env.sh** script, hello line that begins with `export HADOOP_NAMENODE_OPTS=` contains hello options for hello NameNode service.</span></span>

<span data-ttu-id="d4dbd-122">Mapear e reduzir os processos são um pouco diferentes, como essas operações são um processo filho de saudação MapReduce serviço.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-122">Map and reduce processes are slightly different, as these operations are a child process of hello MapReduce service.</span></span> <span data-ttu-id="d4dbd-123">Cada mapa ou reduzir o processo é executado em um contêiner filho, e há duas entradas que contenham Olá JVM opções.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-123">Each map or reduce process runs in a child container, and there are two entries that contain hello JVM options.</span></span> <span data-ttu-id="d4dbd-124">Contidos em **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="d4dbd-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="d4dbd-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="d4dbd-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="d4dbd-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="d4dbd-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="d4dbd-127">É recomendável usando o Ambari toomodify ambos Olá scripts e configurações mapred-site.XML, como Ambari tratar replicar alterações em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-127">We recommend using Ambari toomodify both hello scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in hello cluster.</span></span> <span data-ttu-id="d4dbd-128">Consulte Olá [Ambari usando](#using-ambari) seção para etapas específicas.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-128">See hello [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="d4dbd-129">Habilitar despejos de heap</span><span class="sxs-lookup"><span data-stu-id="d4dbd-129">Enable heap dumps</span></span>

<span data-ttu-id="d4dbd-130">Olá opção a seguir permite que os despejos de pilha quando ocorre um OutOfMemoryError:</span><span class="sxs-lookup"><span data-stu-id="d4dbd-130">hello following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="d4dbd-131">Olá  **+**  indica que essa opção está habilitada.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-131">hello **+** indicates that this option is enabled.</span></span> <span data-ttu-id="d4dbd-132">saudação padrão é disabled.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-132">hello default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="d4dbd-133">Despejos de pilha não estão habilitados para serviços do Hadoop no HDInsight por padrão, como arquivos de despejo Olá podem ser grandes.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as hello dump files can be large.</span></span> <span data-ttu-id="d4dbd-134">Se você habilitá-los para solução de problemas, lembre-se toodisable-los após ter reproduzido Olá problema e os arquivos de despejo Olá coletadas.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-134">If you do enable them for troubleshooting, remember toodisable them once you have reproduced hello problem and gathered hello dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="d4dbd-135">Local do despejo</span><span class="sxs-lookup"><span data-stu-id="d4dbd-135">Dump location</span></span>

<span data-ttu-id="d4dbd-136">local de padrão de Olá Olá arquivo de despejo é o diretório de trabalho atual hello.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-136">hello default location for hello dump file is hello current working directory.</span></span> <span data-ttu-id="d4dbd-137">Você pode controlar onde hello arquivo é armazenado usando Olá opção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4dbd-137">You can control where hello file is stored using hello following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="d4dbd-138">Por exemplo, usando `-XX:HeapDumpPath=/tmp` faz com que o hello despejos toobe armazenado no diretório /tmp de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-138">For example, using `-XX:HeapDumpPath=/tmp` causes hello dumps toobe stored in hello /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="d4dbd-139">Scripts</span><span class="sxs-lookup"><span data-stu-id="d4dbd-139">Scripts</span></span>

<span data-ttu-id="d4dbd-140">Você também pode disparar um script quando um **OutOfMemoryError** ocorrer.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="d4dbd-141">Por exemplo, disparar uma notificação para que você saiba que esse erro Olá ocorreu.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-141">For example, triggering a notification so you know that hello error has occurred.</span></span> <span data-ttu-id="d4dbd-142">A seguir use Olá opção tootrigger um script em um __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="d4dbd-142">Use hello following option tootrigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="d4dbd-143">Como o Hadoop é um sistema distribuído, qualquer script usado deve ser colocado em todos os nós no cluster Olá Olá serviço será executado.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in hello cluster that hello service runs on.</span></span>
> 
> <span data-ttu-id="d4dbd-144">script Hello deve também estar em um local que seja acessível pelos Olá conta Olá o serviço é executado como e deve fornecer permissões de execução.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-144">hello script must also be in a location that is accessible by hello account hello service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="d4dbd-145">Por exemplo, você poderá scripts toostore `/usr/local/bin` e usar `chmod go+rx /usr/local/bin/filename.sh` toogrant permissões read e execute.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-145">For example, you may wish toostore scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` toogrant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="d4dbd-146">Usando o Ambari</span><span class="sxs-lookup"><span data-stu-id="d4dbd-146">Using Ambari</span></span>

<span data-ttu-id="d4dbd-147">configuração de saudação toomodify para um serviço, Olá use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4dbd-147">toomodify hello configuration for a service, use hello following steps:</span></span>

1. <span data-ttu-id="d4dbd-148">Abra Olá Ambari web da interface do usuário para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-148">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="d4dbd-149">Olá URL é https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-149">hello URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="d4dbd-150">Quando solicitado, autentique toohello site usando o nome da conta Olá HTTP (padrão: administrador) e a senha para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-150">When prompted, authenticate toohello site using hello HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d4dbd-151">Você pode ser solicitado pela segunda vez por Ambari para Olá nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-151">You may be prompted a second time by Ambari for hello user name and password.</span></span> <span data-ttu-id="d4dbd-152">Nesse caso, digite Olá o mesmo nome de conta e senha</span><span class="sxs-lookup"><span data-stu-id="d4dbd-152">If so, enter hello same account name and password</span></span>

2. <span data-ttu-id="d4dbd-153">Usando a lista de saudação do hello esquerda, selecione o hello serviço área a ser toomodify.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-153">Using hello list of on hello left, select hello service area you want toomodify.</span></span> <span data-ttu-id="d4dbd-154">Por exemplo, **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-154">For example, **HDFS**.</span></span> <span data-ttu-id="d4dbd-155">Na área do Centro de saudação, selecione Olá **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-155">In hello center area, select hello **Configs** tab.</span></span>

    ![Imagem do Ambari Web com a guia de Configurações de HDFS selecionada](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="d4dbd-157">Usando Olá **filtro...**  entrada, digite **aceita**.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-157">Using hello **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="d4dbd-158">Apenas os itens que contêm esse texto são exibidos.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-158">Only items containing this text are displayed.</span></span>

    ![Lista filtrada](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="d4dbd-160">Localize Olá  **\* \_OPTS** entrada hello serviço você deseja tooenable despejos de pilha para e adicionar Olá opções que você deseja tooenable.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-160">Find hello **\*\_OPTS** entry for hello service you want tooenable heap dumps for, and add hello options you wish tooenable.</span></span> <span data-ttu-id="d4dbd-161">Olá a imagem a seguir, adicionei `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entrada:</span><span class="sxs-lookup"><span data-stu-id="d4dbd-161">In hello following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS com -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="d4dbd-163">Ao habilitar despejos de pilha para Olá mapearem ou reduzem o processo filho, procure por campos Olá denominados **mapreduce.admin.map.child.java.opts** e **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-163">When enabling heap dumps for hello map or reduce child process, look for hello fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="d4dbd-164">Saudação de uso **salvar** botão toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-164">Use hello **Save** button toosave hello changes.</span></span> <span data-ttu-id="d4dbd-165">Você pode inserir uma breve mensagem descrevendo Olá alterações.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-165">You can enter a short note describing hello changes.</span></span>

5. <span data-ttu-id="d4dbd-166">Depois que tiverem sido aplicadas alterações hello, Olá **reinicialização necessária** ícone é exibido ao lado de um ou mais serviços.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-166">Once hello changes have been applied, hello **Restart required** icon appears beside one or more services.</span></span>

    ![botão de reinicialização necessária e botão de reinicialização](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="d4dbd-168">Selecione cada serviço que precisa de uma reinicialização e use Olá **ações de serviço** botão muito**ativar no modo de manutenção**.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-168">Select each service that needs a restart, and use hello **Service Actions** button too**Turn On Maintenance Mode**.</span></span> <span data-ttu-id="d4dbd-169">Modo de manutenção impede que alertas sendo gerados do serviço hello quando você reiniciá-lo.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-169">Maintenance mode prevents alerts from being generated from hello service when you restart it.</span></span>

    ![Ativar o menu do modo de manutenção](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="d4dbd-171">Depois que você tiver habilitado o modo de manutenção, use Olá **reiniciar** botão para serviço Olá muito**reiniciar todos os afetados**</span><span class="sxs-lookup"><span data-stu-id="d4dbd-171">Once you have enabled maintenance mode, use hello **Restart** button for hello service too**Restart All Effected**</span></span>

    ![Entrada Reiniciar todos os afetados](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="d4dbd-173">Olá entradas para Olá **reiniciar** botão pode ser diferente para outros serviços.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-173">hello entries for hello **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="d4dbd-174">Depois de saudação serviços foram reiniciados, use Olá **ações de serviço** botão muito**ativar desativar o modo de manutenção**.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-174">Once hello services have been restarted, use hello **Service Actions** button too**Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="d4dbd-175">Este tooresume Ambari monitoramento de alertas para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4dbd-175">This Ambari tooresume monitoring for alerts for hello service.</span></span>

