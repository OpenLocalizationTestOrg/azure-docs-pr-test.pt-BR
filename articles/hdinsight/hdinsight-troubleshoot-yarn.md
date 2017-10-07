---
title: aaaTroubleshoot YARN usando o Azure HDInsight | Microsoft Docs
description: Obter respostas a perguntas toocommon sobre como trabalhar com o Apache Hadoop YARN e HDInsight do Azure.
keywords: "Azure HDInsight, YARN, perguntas frequentes, guia de solução de problemas, perguntas comuns"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="f557c-104">Solucionar problemas de YARN usando o Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f557c-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="f557c-105">Saiba mais sobre questões hello e suas resoluções durante o trabalho com cargas Apache Hadoop YARN no Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="f557c-105">Learn about hello top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="f557c-106">Como fazer para criar uma nova fila do YARN em um cluster</span><span class="sxs-lookup"><span data-stu-id="f557c-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="f557c-107">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="f557c-107">Resolution steps</span></span> 

<span data-ttu-id="f557c-108">Use Olá seguinte etapas Ambari toocreate uma nova fila YARN e, em seguida, equilibrar a alocação de capacidade de saudação entre todas as filas de saudação.</span><span class="sxs-lookup"><span data-stu-id="f557c-108">Use hello following steps in Ambari toocreate a new YARN queue, and then balance hello capacity allocation among all hello queues.</span></span> 

<span data-ttu-id="f557c-109">Neste exemplo, duas filas existentes (**padrão** e **thriftsvr**) são alterados de 50% capacidade too25% da capacidade, que fornece a nova capacidade de 50% de fila (spark) hello.</span><span class="sxs-lookup"><span data-stu-id="f557c-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity too25% capacity, which gives hello new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="f557c-110">Fila</span><span class="sxs-lookup"><span data-stu-id="f557c-110">Queue</span></span> | <span data-ttu-id="f557c-111">Capacity</span><span class="sxs-lookup"><span data-stu-id="f557c-111">Capacity</span></span> | <span data-ttu-id="f557c-112">Capacidade máxima</span><span class="sxs-lookup"><span data-stu-id="f557c-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f557c-113">padrão</span><span class="sxs-lookup"><span data-stu-id="f557c-113">default</span></span> | <span data-ttu-id="f557c-114">25%</span><span class="sxs-lookup"><span data-stu-id="f557c-114">25%</span></span> | <span data-ttu-id="f557c-115">50%</span><span class="sxs-lookup"><span data-stu-id="f557c-115">50%</span></span> |
| <span data-ttu-id="f557c-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="f557c-116">thrftsvr</span></span> | <span data-ttu-id="f557c-117">25%</span><span class="sxs-lookup"><span data-stu-id="f557c-117">25%</span></span> | <span data-ttu-id="f557c-118">50%</span><span class="sxs-lookup"><span data-stu-id="f557c-118">50%</span></span> |
| <span data-ttu-id="f557c-119">spark</span><span class="sxs-lookup"><span data-stu-id="f557c-119">spark</span></span> | <span data-ttu-id="f557c-120">50%</span><span class="sxs-lookup"><span data-stu-id="f557c-120">50%</span></span> | <span data-ttu-id="f557c-121">50%</span><span class="sxs-lookup"><span data-stu-id="f557c-121">50%</span></span> |

1. <span data-ttu-id="f557c-122">Selecione Olá **Ambari exibições** ícone e, em seguida, selecione Olá grade padrão.</span><span class="sxs-lookup"><span data-stu-id="f557c-122">Select hello **Ambari Views** icon, and then select hello grid pattern.</span></span> <span data-ttu-id="f557c-123">Em seguida, selecione **Gerenciador de Filas do YARN**.</span><span class="sxs-lookup"><span data-stu-id="f557c-123">Next, select **YARN Queue Manager**.</span></span>

    ![Selecione o ícone de modos de exibição do Ambari do hello](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="f557c-125">Selecione Olá **padrão** fila.</span><span class="sxs-lookup"><span data-stu-id="f557c-125">Select hello **default** queue.</span></span>

    ![Selecione a fila de padrão de saudação](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="f557c-127">Para Olá **padrão** de fila, altere Olá **capacidade** de too25 de 50% %.</span><span class="sxs-lookup"><span data-stu-id="f557c-127">For hello **default** queue, change hello **capacity** from 50% too25%.</span></span> <span data-ttu-id="f557c-128">Para Olá **thriftsvr** de fila, altere Olá **capacidade** too25%.</span><span class="sxs-lookup"><span data-stu-id="f557c-128">For hello **thriftsvr** queue, change hello **capacity** too25%.</span></span>

    ![Alterar Olá capacidade too25% para filas de saudação padrão e thriftsvr](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="f557c-130">toocreate uma nova fila, selecione **adicionar fila**.</span><span class="sxs-lookup"><span data-stu-id="f557c-130">toocreate a new queue, select **Add Queue**.</span></span>

    ![Selecionar Adicionar Fila](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="f557c-132">Nome hello nova fila.</span><span class="sxs-lookup"><span data-stu-id="f557c-132">Name hello new queue.</span></span>

    ![Nome da fila de saudação Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="f557c-134">Deixe Olá **capacidade** valores em 50% e, em seguida, selecione hello **ações** botão.</span><span class="sxs-lookup"><span data-stu-id="f557c-134">Leave hello **capacity** values at 50%, and then select hello **Actions** button.</span></span>

    ![Selecione o botão de ações de saudação](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="f557c-136">Escolha **Salvar e Atualizar Filas**.</span><span class="sxs-lookup"><span data-stu-id="f557c-136">Select **Save and Refresh Queues**.</span></span>

    ![Escolha Salvar e Atualizar Filas](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="f557c-138">Essas alterações são visíveis imediatamente em Olá YARN da interface do usuário de Agendador.</span><span class="sxs-lookup"><span data-stu-id="f557c-138">These changes are visible immediately on hello YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="f557c-139">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="f557c-139">Additional reading</span></span>

- [<span data-ttu-id="f557c-140">YARN CapacityScheduler</span><span class="sxs-lookup"><span data-stu-id="f557c-140">YARN CapacityScheduler</span></span>](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="f557c-141">Como fazer para baixar logs do YARN de um cluster</span><span class="sxs-lookup"><span data-stu-id="f557c-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="f557c-142">Etapas de resolução</span><span class="sxs-lookup"><span data-stu-id="f557c-142">Resolution steps</span></span> 

1. <span data-ttu-id="f557c-143">Conecte o cluster do HDInsight toohello usando um cliente do Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="f557c-143">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="f557c-144">Para saber mais, veja [Leituras adicionais](#additional-reading-2).</span><span class="sxs-lookup"><span data-stu-id="f557c-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="f557c-145">toolist todos Olá IDs de aplicativo dos aplicativos de YARN Olá atualmente em execução, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f557c-145">toolist all hello application IDs of hello YARN applications that are currently running, run hello following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="f557c-146">Olá IDs são listadas na Olá **APPLICATIONID** coluna.</span><span class="sxs-lookup"><span data-stu-id="f557c-146">hello IDs are listed in hello **APPLICATIONID** column.</span></span> <span data-ttu-id="f557c-147">Você pode baixar os logs do hello **APPLICATIONID** coluna.</span><span class="sxs-lookup"><span data-stu-id="f557c-147">You can download logs from hello **APPLICATIONID** column.</span></span>

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. <span data-ttu-id="f557c-148">logs de contêiner YARN toodownload para todos os mestres de aplicativo, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f557c-148">toodownload YARN container logs for all application masters, use hello following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="f557c-149">Este comando cria um arquivo de log chamado amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="f557c-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="f557c-150">logs de contêiner YARN toodownload somente mestre mais recente de aplicativo de hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f557c-150">toodownload YARN container logs for only hello latest application master, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="f557c-151">Este comando cria um arquivo de log chamado latestamlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="f557c-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="f557c-152">logs de contêiner YARN toodownload para mestres de dois aplicativos primeiro hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f557c-152">toodownload YARN container logs for hello first two application masters, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="f557c-153">Este comando cria um arquivo de log chamado first2amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="f557c-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="f557c-154">toodownload todos os logs de contêiner YARN, use Olá seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f557c-154">toodownload all YARN container logs, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="f557c-155">Este comando cria um arquivo de log chamado logs.txt.</span><span class="sxs-lookup"><span data-stu-id="f557c-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="f557c-156">log de contêiner toodownload Olá YARN para um contêiner específico, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f557c-156">toodownload hello YARN container log for a specific container, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="f557c-157">Este comando cria um arquivo de log chamado containerlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="f557c-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="f557c-158"><a name="additional-reading-2"></a>Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="f557c-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="f557c-159">Conecte-se tooHDInsight (Hadoop) usando o SSH</span><span class="sxs-lookup"><span data-stu-id="f557c-159">Connect tooHDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [<span data-ttu-id="f557c-160">Aplicativos e conceitos do Apache Hadoop YARN</span><span class="sxs-lookup"><span data-stu-id="f557c-160">Apache Hadoop YARN concepts and applications</span></span>](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)







