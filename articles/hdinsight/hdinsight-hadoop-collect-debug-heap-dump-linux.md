---
title: "Habilitar despejos de heap para serviços do Hadoop no HDInsight – Azure | Microsoft Docs"
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
ms.openlocfilehash: 59942e989d622c2486edf181d76e13344c71e6f9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="fd329-103">Habilitar despejos heap para serviços Hadoop no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="fd329-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="fd329-104">Despejos de heap contêm um instantâneo da memória do aplicativo, incluindo os valores das variáveis no momento em que o despejo foi criado.</span><span class="sxs-lookup"><span data-stu-id="fd329-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="fd329-105">Portanto, eles são úteis para diagnosticar problemas que ocorrem no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="fd329-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd329-106">As etapas neste documento funcionam somente com clusters HDInsight que usam Linux.</span><span class="sxs-lookup"><span data-stu-id="fd329-106">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="fd329-107">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="fd329-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fd329-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="fd329-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="fd329-109"><a name="whichServices"></a>Serviços</span><span class="sxs-lookup"><span data-stu-id="fd329-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="fd329-110">Você pode habilitar o despejo de heap para os seguintes serviços:</span><span class="sxs-lookup"><span data-stu-id="fd329-110">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="fd329-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="fd329-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="fd329-112">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="fd329-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="fd329-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="fd329-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="fd329-114">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="fd329-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="fd329-115">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="fd329-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="fd329-116">Você também pode habilitar despejos de heap para os processos de mapeamento e redução executados pelo HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fd329-116">You can also enable heap dumps for the map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="fd329-117"><a name="configuration"></a>Compreendendo a configuração do despejo de heap</span><span class="sxs-lookup"><span data-stu-id="fd329-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="fd329-118">Despejos de heap são habilitados transmitindo opções (às vezes conhecidas como opts, ou parâmetros) para a JVM quando um serviço é iniciado.</span><span class="sxs-lookup"><span data-stu-id="fd329-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) to the JVM when a service is started.</span></span> <span data-ttu-id="fd329-119">Para a maioria dos serviços Hadoop, é possível modificar o script de shell usado para iniciar o serviço para transmitir essas opções.</span><span class="sxs-lookup"><span data-stu-id="fd329-119">For most Hadoop services, you can modify the shell script used to start the service to pass these options.</span></span>

<span data-ttu-id="fd329-120">Em cada script, há uma exportação para **\*\_OPTS**, que contém as opções passadas para a JVM.</span><span class="sxs-lookup"><span data-stu-id="fd329-120">In each script, there is an export for **\*\_OPTS**, which contains the options passed to the JVM.</span></span> <span data-ttu-id="fd329-121">Por exemplo, no script **hadoop-env.sh**, a linha que começa com `export HADOOP_NAMENODE_OPTS=` contém as opções para o serviço NameNode.</span><span class="sxs-lookup"><span data-stu-id="fd329-121">For example, in the **hadoop-env.sh** script, the line that begins with `export HADOOP_NAMENODE_OPTS=` contains the options for the NameNode service.</span></span>

<span data-ttu-id="fd329-122">Os processos de mapeamento e redução são ligeiramente diferentes, uma vez que essas operações são processos filho do serviço MapReduce.</span><span class="sxs-lookup"><span data-stu-id="fd329-122">Map and reduce processes are slightly different, as these operations are a child process of the MapReduce service.</span></span> <span data-ttu-id="fd329-123">Cada processo de mapeamento ou redução é executado em um contêiner filho, e há duas entradas que contêm as opções de JVM.</span><span class="sxs-lookup"><span data-stu-id="fd329-123">Each map or reduce process runs in a child container, and there are two entries that contain the JVM options.</span></span> <span data-ttu-id="fd329-124">Contidos em **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="fd329-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="fd329-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="fd329-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="fd329-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="fd329-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="fd329-127">Recomendamos usar o Ambari para modificar os scripts e configurações de mapred-site.xml, pois ele processa a réplica de alterações nos nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="fd329-127">We recommend using Ambari to modify both the scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in the cluster.</span></span> <span data-ttu-id="fd329-128">Consulte a seção [Usando o Ambari](#using-ambari) para ver as etapas específicas.</span><span class="sxs-lookup"><span data-stu-id="fd329-128">See the [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="fd329-129">Habilitar despejos de heap</span><span class="sxs-lookup"><span data-stu-id="fd329-129">Enable heap dumps</span></span>

<span data-ttu-id="fd329-130">A seguinte opção habilita os despejos de heap quando ocorre um OutOfMemoryError:</span><span class="sxs-lookup"><span data-stu-id="fd329-130">The following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="fd329-131">O **+** indica que a opção está habilitada.</span><span class="sxs-lookup"><span data-stu-id="fd329-131">The **+** indicates that this option is enabled.</span></span> <span data-ttu-id="fd329-132">Por padrão, ela fica desabilitada.</span><span class="sxs-lookup"><span data-stu-id="fd329-132">The default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="fd329-133">Despejos de heap não são habilitados para serviços do Hadoop no HDInsight por padrão, pois os arquivos de despejo podem ser grandes.</span><span class="sxs-lookup"><span data-stu-id="fd329-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as the dump files can be large.</span></span> <span data-ttu-id="fd329-134">Se você habilitá-los para solução de problemas, lembre-se de desabilitá-los após ter reproduzido o problema e coletado os arquivos de despejo.</span><span class="sxs-lookup"><span data-stu-id="fd329-134">If you do enable them for troubleshooting, remember to disable them once you have reproduced the problem and gathered the dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="fd329-135">Local do despejo</span><span class="sxs-lookup"><span data-stu-id="fd329-135">Dump location</span></span>

<span data-ttu-id="fd329-136">O local padrão para o arquivo de despejo é o diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="fd329-136">The default location for the dump file is the current working directory.</span></span> <span data-ttu-id="fd329-137">Você pode controlar onde o arquivo é armazenado usando a seguinte opção:</span><span class="sxs-lookup"><span data-stu-id="fd329-137">You can control where the file is stored using the following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="fd329-138">Por exemplo, usar `-XX:HeapDumpPath=/tmp` fará com que os despejos sejam armazenados no diretório /tmp.</span><span class="sxs-lookup"><span data-stu-id="fd329-138">For example, using `-XX:HeapDumpPath=/tmp` causes the dumps to be stored in the /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="fd329-139">Scripts</span><span class="sxs-lookup"><span data-stu-id="fd329-139">Scripts</span></span>

<span data-ttu-id="fd329-140">Você também pode disparar um script quando um **OutOfMemoryError** ocorrer.</span><span class="sxs-lookup"><span data-stu-id="fd329-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="fd329-141">Por exemplo, disparar uma notificação para que você saiba que o erro ocorreu.</span><span class="sxs-lookup"><span data-stu-id="fd329-141">For example, triggering a notification so you know that the error has occurred.</span></span> <span data-ttu-id="fd329-142">Use a opção a seguir para disparar um script em um __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="fd329-142">Use the following option to trigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="fd329-143">Como o Hadoop é um sistema distribuído, qualquer script usado deve ser colocado em todos os nós no cluster em que o serviço é executado.</span><span class="sxs-lookup"><span data-stu-id="fd329-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in the cluster that the service runs on.</span></span>
> 
> <span data-ttu-id="fd329-144">O script deve também estar em um local que seja acessível pela conta em que o serviço é executado e deve fornecer permissões de execução.</span><span class="sxs-lookup"><span data-stu-id="fd329-144">The script must also be in a location that is accessible by the account the service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="fd329-145">Por exemplo, você pode optar por armazenar scripts em `/usr/local/bin` e usar `chmod go+rx /usr/local/bin/filename.sh` para conceder permissões de leitura e execução.</span><span class="sxs-lookup"><span data-stu-id="fd329-145">For example, you may wish to store scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` to grant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="fd329-146">Usando o Ambari</span><span class="sxs-lookup"><span data-stu-id="fd329-146">Using Ambari</span></span>

<span data-ttu-id="fd329-147">Para modificar a configuração de um serviço, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="fd329-147">To modify the configuration for a service, use the following steps:</span></span>

1. <span data-ttu-id="fd329-148">Abra a UI da Web do Ambari para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="fd329-148">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="fd329-149">A URL será https://NOMEDOSEUCLUSTER.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="fd329-149">The URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="fd329-150">Quando solicitado, autentique-se no site usando o nome da conta HTTP (padrão: admin) e a senha do seu cluster.</span><span class="sxs-lookup"><span data-stu-id="fd329-150">When prompted, authenticate to the site using the HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fd329-151">O Ambari poderá solicitar o nome de usuário e senha mais uma vez.</span><span class="sxs-lookup"><span data-stu-id="fd329-151">You may be prompted a second time by Ambari for the user name and password.</span></span> <span data-ttu-id="fd329-152">Nesse caso, insira o mesmo nome de conta e senha</span><span class="sxs-lookup"><span data-stu-id="fd329-152">If so, enter the same account name and password</span></span>

2. <span data-ttu-id="fd329-153">Usando a lista à esquerda, selecione a área de serviço que você deseja modificar.</span><span class="sxs-lookup"><span data-stu-id="fd329-153">Using the list of on the left, select the service area you want to modify.</span></span> <span data-ttu-id="fd329-154">Por exemplo, **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="fd329-154">For example, **HDFS**.</span></span> <span data-ttu-id="fd329-155">Na área central, selecione a guia **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="fd329-155">In the center area, select the **Configs** tab.</span></span>

    ![Imagem do Ambari Web com a guia de Configurações de HDFS selecionada](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="fd329-157">Usando a entrada **Filtrar...**, insira **opts**.</span><span class="sxs-lookup"><span data-stu-id="fd329-157">Using the **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="fd329-158">Apenas os itens que contêm esse texto são exibidos.</span><span class="sxs-lookup"><span data-stu-id="fd329-158">Only items containing this text are displayed.</span></span>

    ![Lista filtrada](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="fd329-160">Encontre a entrada **\*\_OPTS** do serviço para o qual você deseja habilitar os despejos de heap e adicione as opções que deseja habilitar.</span><span class="sxs-lookup"><span data-stu-id="fd329-160">Find the **\*\_OPTS** entry for the service you want to enable heap dumps for, and add the options you wish to enable.</span></span> <span data-ttu-id="fd329-161">Na imagem a seguir, adicionei `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` à entrada **HADOOP\_NAMENODE\_OPTS**:</span><span class="sxs-lookup"><span data-stu-id="fd329-161">In the following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` to the **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS com -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="fd329-163">Ao habilitar despejos de heap para o processo filho de mapeamento ou redução, procure os campos denominados **mapreduce.admin.map.child.java.opts** e **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="fd329-163">When enabling heap dumps for the map or reduce child process, look for the fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="fd329-164">Use o botão **Salvar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="fd329-164">Use the **Save** button to save the changes.</span></span> <span data-ttu-id="fd329-165">Você pode inserir uma nota breve que descreve as alterações.</span><span class="sxs-lookup"><span data-stu-id="fd329-165">You can enter a short note describing the changes.</span></span>

5. <span data-ttu-id="fd329-166">Após as alterações serem aplicadas, o ícone **Reinicialização necessária** aparecerá ao lado de um ou mais serviços.</span><span class="sxs-lookup"><span data-stu-id="fd329-166">Once the changes have been applied, the **Restart required** icon appears beside one or more services.</span></span>

    ![botão de reinicialização necessária e botão de reinicialização](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="fd329-168">Selecione cada serviço que precisa ser reiniciado e use o botão **Ações de Serviço** para **Ativar o Modo de Manutenção**.</span><span class="sxs-lookup"><span data-stu-id="fd329-168">Select each service that needs a restart, and use the **Service Actions** button to **Turn On Maintenance Mode**.</span></span> <span data-ttu-id="fd329-169">O modo de manutenção impede que alertas sejam gerados pelo serviço ao reiniciá-lo.</span><span class="sxs-lookup"><span data-stu-id="fd329-169">Maintenance mode prevents alerts from being generated from the service when you restart it.</span></span>

    ![Ativar o menu do modo de manutenção](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="fd329-171">Após ter habilitado o modo de manutenção, use o botão **Reiniciar** para o serviço **Reiniciar Todos os Afetados**</span><span class="sxs-lookup"><span data-stu-id="fd329-171">Once you have enabled maintenance mode, use the **Restart** button for the service to **Restart All Effected**</span></span>

    ![Entrada Reiniciar todos os afetados](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="fd329-173">as entradas do botão **Reiniciar** podem ser diferentes para outros serviços.</span><span class="sxs-lookup"><span data-stu-id="fd329-173">the entries for the **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="fd329-174">Após os serviços serem reiniciados, use o botão **Ações de Serviço** para **Desativar o Modo de Manutenção**.</span><span class="sxs-lookup"><span data-stu-id="fd329-174">Once the services have been restarted, use the **Service Actions** button to **Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="fd329-175">Use este Ambari para retomar o monitoramento dos alertas do serviço.</span><span class="sxs-lookup"><span data-stu-id="fd329-175">This Ambari to resume monitoring for alerts for the service.</span></span>

