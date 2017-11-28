---
title: "Kit de Ferramentas do Azure para IntelliJ – Depurar aplicativos Spark remotamente por meio do SSH | Microsoft Docs"
description: "Orientações passo a passo sobre como toouse ferramentas HDInsight no Kit de ferramentas do Azure para aplicativos de toodebug IntelliJ remotamente no HDInsight clusters por meio do SSH"
keywords: "depurar o intellij remotamente, depuração remota do intellij, ssh, intellij, hdinsight, depurar o intellij, depuração"
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="4838c-104">Depurar aplicativos Spark em um cluster HDInsight com o Kit de Ferramentas do Azure para IntelliJ por meio do SSH</span><span class="sxs-lookup"><span data-stu-id="4838c-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="4838c-105">Este artigo fornece orientação passo a passo sobre como toouse ferramentas HDInsight no Kit de ferramentas do Azure para IntelliJ toodebug aplicativos remotamente em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4838c-105">This article provides step-by-step guidance on how toouse HDInsight Tools in Azure Toolkit for IntelliJ toodebug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="4838c-106">toodebug seu projeto, você também pode exibir uma saudação [aplicativos de depurar HDInsight Spark com o Kit de ferramentas do Azure para IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) vídeo.</span><span class="sxs-lookup"><span data-stu-id="4838c-106">toodebug your project, you can also view hello [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="4838c-107">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="4838c-107">**Prerequisites**</span></span>

* <span data-ttu-id="4838c-108">**Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="4838c-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="4838c-109">Essa ferramenta faz parte do Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="4838c-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="4838c-110">Para mais informações, consulte [Instalar o Kit de Ferramentas do Azure para IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="4838c-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="4838c-111">**Kit de Ferramentas do Azure para IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="4838c-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="4838c-112">Use estes aplicativos de Spark toocreate Kit de ferramentas para um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4838c-112">Use this toolkit toocreate Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="4838c-113">Para obter mais informações, siga as instruções de saudação em [Kit de ferramentas do uso do Azure para aplicativos de Spark toocreate IntelliJ para um cluster HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span><span class="sxs-lookup"><span data-stu-id="4838c-113">For more information, follow hello instructions in [Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="4838c-114">**Serviço SSH do HDInsight com gerenciamento de nome de usuário e senha**.</span><span class="sxs-lookup"><span data-stu-id="4838c-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="4838c-115">Para obter mais informações, consulte [conectar tooHDInsight (Hadoop) usando o SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [usar SSH túnel tooaccess Ambari web da interface do usuário, JobHistory, NameNode, Oozie e outras interfaces do usuário da web](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span><span class="sxs-lookup"><span data-stu-id="4838c-115">For more information, see [Connect tooHDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="4838c-116">Criar um aplicativo Spark Scala e configurá-lo para depuração remota</span><span class="sxs-lookup"><span data-stu-id="4838c-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="4838c-117">Inicie o IDEA do IntelliJ e crie um projeto.</span><span class="sxs-lookup"><span data-stu-id="4838c-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="4838c-118">Em Olá **novo projeto** caixa de diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4838c-118">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="4838c-119">a.</span><span class="sxs-lookup"><span data-stu-id="4838c-119">a.</span></span> <span data-ttu-id="4838c-120">Selecione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4838c-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="4838c-121">b.</span><span class="sxs-lookup"><span data-stu-id="4838c-121">b.</span></span> <span data-ttu-id="4838c-122">Selecione um modelo Java ou Scala com base em sua preferência.</span><span class="sxs-lookup"><span data-stu-id="4838c-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="4838c-123">Selecione entre hello as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="4838c-123">Select between hello following options:</span></span>

      - <span data-ttu-id="4838c-124">**Spark no HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="4838c-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="4838c-125">**Spark no HDInsight (Java)**</span><span class="sxs-lookup"><span data-stu-id="4838c-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="4838c-126">**Amostra de execução do Spark no Cluster HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="4838c-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="4838c-127">Este exemplo usa um modelo de **Amostra de Execução do Spark no Cluster do HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="4838c-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="4838c-128">c.</span><span class="sxs-lookup"><span data-stu-id="4838c-128">c.</span></span> <span data-ttu-id="4838c-129">Em Olá **ferramenta de compilação** , selecione qualquer uma das Olá a seguir, de acordo com a necessidade de tooyour:</span><span class="sxs-lookup"><span data-stu-id="4838c-129">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      - <span data-ttu-id="4838c-130">**Maven**, para obter suporte ao assistente de criação de projetos Scala</span><span class="sxs-lookup"><span data-stu-id="4838c-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="4838c-131">**SBT**, para gerenciar dependências hello e criação de projeto de Scala Olá</span><span class="sxs-lookup"><span data-stu-id="4838c-131">**SBT**, for managing hello dependencies and building for hello Scala project</span></span> 

      ![Criar um projeto de depuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="4838c-133">d.</span><span class="sxs-lookup"><span data-stu-id="4838c-133">d.</span></span> <span data-ttu-id="4838c-134">Selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4838c-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="4838c-135">Em Olá próximo **novo projeto** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4838c-135">In hello next **New Project** window, do hello following:</span></span>

   ![Selecione Olá Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="4838c-137">a.</span><span class="sxs-lookup"><span data-stu-id="4838c-137">a.</span></span> <span data-ttu-id="4838c-138">Insira um nome de projeto e o local do projeto.</span><span class="sxs-lookup"><span data-stu-id="4838c-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="4838c-139">b.</span><span class="sxs-lookup"><span data-stu-id="4838c-139">b.</span></span> <span data-ttu-id="4838c-140">Em Olá **projeto SDK** lista suspensa, selecione **Java 1.8** para **despertar 2. x** do cluster ou selecione **Java 1.7** para **Spark 1. x** cluster.</span><span class="sxs-lookup"><span data-stu-id="4838c-140">In hello **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="4838c-141">c.</span><span class="sxs-lookup"><span data-stu-id="4838c-141">c.</span></span> <span data-ttu-id="4838c-142">Em Olá **versão Spark** lista suspensa, o Assistente de criação de projeto Olá Scala se integra a versão correta do Olá para Spark SDK e Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="4838c-142">In hello **Spark Version** drop-down list, hello Scala project creation wizard integrates hello correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="4838c-143">Se a versão do cluster spark Olá for anterior à 2.0, selecione **despertar 1. x**.</span><span class="sxs-lookup"><span data-stu-id="4838c-143">If hello spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="4838c-144">Caso contrário, selecione **Spark 2.x.**</span><span class="sxs-lookup"><span data-stu-id="4838c-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="4838c-145">Esse exemplo usa o **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="4838c-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="4838c-146">d.</span><span class="sxs-lookup"><span data-stu-id="4838c-146">d.</span></span> <span data-ttu-id="4838c-147">Selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="4838c-147">Select **Finish**.</span></span>

4. <span data-ttu-id="4838c-148">Selecione **src** > **principal** > **scala** tooopen seu código no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="4838c-148">Select **src** > **main** > **scala** tooopen your code in hello project.</span></span> <span data-ttu-id="4838c-149">Este exemplo usa Olá **SparkCore_wasbloTest** script.</span><span class="sxs-lookup"><span data-stu-id="4838c-149">This example uses hello **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="4838c-150">Olá tooaccess **editar configurações** menu, ícone Olá seleção no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="4838c-150">tooaccess hello **Edit Configurations** menu, select hello icon in hello upper-right corner.</span></span> <span data-ttu-id="4838c-151">Nesse menu, você pode criar ou editar as configurações de saudação para depuração remota.</span><span class="sxs-lookup"><span data-stu-id="4838c-151">From this menu, you can create or edit hello configurations for remote debugging.</span></span>

   ![Editar configurações](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="4838c-153">Em Olá **configurações de execução/depuração** caixa de diálogo, selecione hello mais sinal (**+**).</span><span class="sxs-lookup"><span data-stu-id="4838c-153">In hello **Run/Debug Configurations** dialog box, select hello plus sign (**+**).</span></span> <span data-ttu-id="4838c-154">Em seguida, selecione Olá **enviar trabalho de Spark** opção.</span><span class="sxs-lookup"><span data-stu-id="4838c-154">Then select hello **Submit Spark Job** option.</span></span>

   ![Adicionar nova configuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="4838c-156">Insira as informações em **Nome**, **Cluster do Spark** e **Nome da classe principal**.</span><span class="sxs-lookup"><span data-stu-id="4838c-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="4838c-157">Em seguida, selecione **Configurações avançadas**.</span><span class="sxs-lookup"><span data-stu-id="4838c-157">Then select **Advanced configuration**.</span></span> 

   ![Executar configurações de depuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="4838c-159">Em Olá **configuração avançada de envio Spark** caixa de diálogo, selecione **depuração remota Spark habilitar**.</span><span class="sxs-lookup"><span data-stu-id="4838c-159">In hello **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="4838c-160">Insira nome de usuário do hello SSH, digite uma senha ou usar um arquivo de chave privado.</span><span class="sxs-lookup"><span data-stu-id="4838c-160">Enter hello SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="4838c-161">configuração de saudação toosave, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="4838c-161">toosave hello configuration, select **OK**.</span></span>

   ![Habilitar depuração remota do Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="4838c-163">configuração Olá agora é salvo com o nome hello fornecido.</span><span class="sxs-lookup"><span data-stu-id="4838c-163">hello configuration is now saved with hello name you provided.</span></span> <span data-ttu-id="4838c-164">detalhes da configuração tooview Olá, nome da configuração Olá select.</span><span class="sxs-lookup"><span data-stu-id="4838c-164">tooview hello configuration details, select hello configuration name.</span></span> <span data-ttu-id="4838c-165">alterações de toomake, selecione **editar configurações**.</span><span class="sxs-lookup"><span data-stu-id="4838c-165">toomake changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="4838c-166">Depois de concluir as definições de configuração Olá, você pode executar o projeto de saudação no cluster remoto hello ou realizar a depuração remota.</span><span class="sxs-lookup"><span data-stu-id="4838c-166">After you complete hello configurations settings, you can run hello project against hello remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-tooperform-remote-debugging"></a><span data-ttu-id="4838c-167">Saiba como tooperform a depuração remota</span><span class="sxs-lookup"><span data-stu-id="4838c-167">Learn how tooperform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="4838c-168">Cenário 1: realizar a execução remota</span><span class="sxs-lookup"><span data-stu-id="4838c-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="4838c-169">Nesta seção, mostraremos como toodebug executores e drivers.</span><span class="sxs-lookup"><span data-stu-id="4838c-169">In this section, we show you how toodebug drivers and executors.</span></span>

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. <span data-ttu-id="4838c-170">Configurar pontos de quebra e, em seguida, selecione Olá **depurar** ícone.</span><span class="sxs-lookup"><span data-stu-id="4838c-170">Set up breaking points, and then select hello **Debug** icon.</span></span>

   ![Selecione o ícone de depuração Olá](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="4838c-172">Quando a execução do programa hello atinge o ponto de interrupção Olá, você verá um **Driver** guia e dois **Executor** guias no hello **depurador** painel.</span><span class="sxs-lookup"><span data-stu-id="4838c-172">When hello program execution reaches hello breaking point, you see a **Driver** tab and two **Executor** tabs in hello **Debugger** pane.</span></span> <span data-ttu-id="4838c-173">Selecione Olá **retomar programa** toocontinue ícone executar código hello, que atinge o próximo ponto de interrupção de saudação e enfoca Olá correspondente **Executor** guia. Você pode examinar os logs de execução de saudação em Olá correspondente **Console** guia.</span><span class="sxs-lookup"><span data-stu-id="4838c-173">Select hello **Resume Program** icon toocontinue running hello code, which then reaches hello next breakpoint and focuses on hello corresponding **Executor** tab. You can review hello execution logs on hello corresponding **Console** tab.</span></span>

   ![Guia depuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="4838c-175">Cenário 2: Executar depuração remota e correção de bugs</span><span class="sxs-lookup"><span data-stu-id="4838c-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="4838c-176">Nesta seção, mostraremos como toodynamically atualização Olá valor de variável usando Olá IntelliJ capacidade para uma solução simple de depuração.</span><span class="sxs-lookup"><span data-stu-id="4838c-176">In this section, we show you how toodynamically update hello variable value by using hello IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="4838c-177">Em Olá exemplo de código a seguir, uma exceção será lançada porque já existe um arquivo de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="4838c-177">In hello following code example, an exception is thrown because hello target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="4838c-178">depuração remota de tooperform e correção de bug</span><span class="sxs-lookup"><span data-stu-id="4838c-178">tooperform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="4838c-179">Configurar dois pontos de quebra e selecione Olá **depurar** Olá de toostart ícone processo de depuração remota.</span><span class="sxs-lookup"><span data-stu-id="4838c-179">Set up two breaking points, and then select hello **Debug** icon toostart hello remote debugging process.</span></span>

2. <span data-ttu-id="4838c-180">código Olá para Olá primeiro ponto de interrupção e parâmetro hello e informações de variáveis são mostrados no hello **variáveis** painel.</span><span class="sxs-lookup"><span data-stu-id="4838c-180">hello code stops at hello first breaking point, and hello parameter and variable information are shown in hello **Variables** pane.</span></span> 

3. <span data-ttu-id="4838c-181">Selecione Olá **retomar programa** toocontinue ícone.</span><span class="sxs-lookup"><span data-stu-id="4838c-181">Select hello **Resume Program** icon toocontinue.</span></span> <span data-ttu-id="4838c-182">Olá para de código no segundo ponto de saudação.</span><span class="sxs-lookup"><span data-stu-id="4838c-182">hello code stops at hello second point.</span></span> <span data-ttu-id="4838c-183">exceção de saudação é detectada conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="4838c-183">hello exception is caught as expected.</span></span>

  ![Gerar erro](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="4838c-185">Selecione Olá **retomar programa** ícone novamente.</span><span class="sxs-lookup"><span data-stu-id="4838c-185">Select hello **Resume Program** icon again.</span></span> <span data-ttu-id="4838c-186">Olá **HDInsight Spark envio** janela exibe um erro "Falha na execução de trabalho".</span><span class="sxs-lookup"><span data-stu-id="4838c-186">hello **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![Envio de erro](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="4838c-188">toodynamically atualização Olá valor variável usando o recurso de depuração de IntelliJ hello, selecione **depurar** novamente.</span><span class="sxs-lookup"><span data-stu-id="4838c-188">toodynamically update hello variable value by using hello IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="4838c-189">Olá **variáveis** painel é exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="4838c-189">hello **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="4838c-190">Destino de saudação com o botão direito em Olá **depurar** guia e, em seguida, selecione **definir valor**.</span><span class="sxs-lookup"><span data-stu-id="4838c-190">Right-click hello target on hello **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="4838c-191">Em seguida, insira um novo valor para a variável de saudação.</span><span class="sxs-lookup"><span data-stu-id="4838c-191">Next, enter a new value for hello variable.</span></span> <span data-ttu-id="4838c-192">Em seguida, selecione **Enter** toosave valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="4838c-192">Then select **Enter** toosave hello value.</span></span> 

  ![Definir valor](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="4838c-194">Selecione Olá **retomar programa** programa de saudação do ícone toocontinue toorun.</span><span class="sxs-lookup"><span data-stu-id="4838c-194">Select hello **Resume Program** icon toocontinue toorun hello program.</span></span> <span data-ttu-id="4838c-195">Neste momento, nenhuma exceção é detectada.</span><span class="sxs-lookup"><span data-stu-id="4838c-195">This time, no exception is caught.</span></span> <span data-ttu-id="4838c-196">Você pode ver o que projeto Olá for executado com êxito sem exceções.</span><span class="sxs-lookup"><span data-stu-id="4838c-196">You can see that hello project runs successfully without any exceptions.</span></span>

  ![Depurar sem exceção](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="4838c-198"><a name="seealso"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4838c-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="4838c-199">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4838c-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="4838c-200">Demonstração</span><span class="sxs-lookup"><span data-stu-id="4838c-200">Demo</span></span>
* <span data-ttu-id="4838c-201">Criar projeto do Scala (vídeo): [Criar aplicativos Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="4838c-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="4838c-202">Depuração remota (vídeo): [Kit de ferramentas do uso do Azure para aplicativos de Spark toodebug IntelliJ remotamente em um cluster HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="4838c-202">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="4838c-203">Cenários</span><span class="sxs-lookup"><span data-stu-id="4838c-203">Scenarios</span></span>
* [<span data-ttu-id="4838c-204">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="4838c-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="4838c-205">Spark com o aprendizado de máquina: Use o Spark no HDInsight tooanalyze criação temperatura usando dados HVAC</span><span class="sxs-lookup"><span data-stu-id="4838c-205">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="4838c-206">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="4838c-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="4838c-207">Streaming Spark: Use Spark no HDInsight toobuild aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="4838c-207">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="4838c-208">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="4838c-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="4838c-209">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="4838c-209">Create and run applications</span></span>
* [<span data-ttu-id="4838c-210">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="4838c-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="4838c-211">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="4838c-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="4838c-212">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="4838c-212">Tools and extensions</span></span>
* [<span data-ttu-id="4838c-213">Use o Kit de ferramentas do Azure para aplicativos de Spark toocreate IntelliJ para um cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="4838c-213">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="4838c-214">Use o Kit de ferramentas do Azure para aplicativos de Spark toodebug IntelliJ remotamente por meio de VPN</span><span class="sxs-lookup"><span data-stu-id="4838c-214">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="4838c-215">Usar ferramentas do HDInsight para IntelliJ com a área restrita do Hortonworks</span><span class="sxs-lookup"><span data-stu-id="4838c-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="4838c-216">Use as ferramentas do HDInsight no Kit de ferramentas do Azure para aplicativos do Eclipse toocreate Spark</span><span class="sxs-lookup"><span data-stu-id="4838c-216">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="4838c-217">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="4838c-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="4838c-218">Kernels disponíveis para o bloco de anotações do Jupyter no cluster do hello Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="4838c-218">Kernels available for Jupyter notebook in hello Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="4838c-219">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="4838c-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="4838c-220">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="4838c-220">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="4838c-221">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="4838c-221">Manage resources</span></span>
* [<span data-ttu-id="4838c-222">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="4838c-222">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="4838c-223">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="4838c-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
