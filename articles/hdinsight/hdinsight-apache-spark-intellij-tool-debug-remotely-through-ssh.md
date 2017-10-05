---
title: "Kit de Ferramentas do Azure para IntelliJ – Depurar aplicativos Spark remotamente por meio do SSH | Microsoft Docs"
description: "Instruções passo a passo sobre como usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ para depurar aplicativos remotamente nos clusters do HDInsight por meio do SSH"
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
ms.openlocfilehash: 19053e31d6eb097bc91a04ef9c6af5772aaa16da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="e3d15-104">Depurar aplicativos Spark em um cluster HDInsight com o Kit de Ferramentas do Azure para IntelliJ por meio do SSH</span><span class="sxs-lookup"><span data-stu-id="e3d15-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="e3d15-105">Este artigo fornece instruções passo a passo sobre como usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ para depurar aplicativos remotamente em um cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e3d15-105">This article provides step-by-step guidance on how to use HDInsight Tools in Azure Toolkit for IntelliJ to debug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="e3d15-106">Para depurar seu projeto, você também poderá exibir o vídeo [Depurar aplicativos do HDInsight Spark com o Kit de Ferramentas do Azure para IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ).</span><span class="sxs-lookup"><span data-stu-id="e3d15-106">To debug your project, you can also view the [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="e3d15-107">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="e3d15-107">**Prerequisites**</span></span>

* <span data-ttu-id="e3d15-108">**Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="e3d15-109">Essa ferramenta faz parte do Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="e3d15-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="e3d15-110">Para mais informações, consulte [Instalar o Kit de Ferramentas do Azure para IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="e3d15-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="e3d15-111">**Kit de Ferramentas do Azure para IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="e3d15-112">Use esse kit de ferramentas para criar aplicativos Spark para o cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e3d15-112">Use this toolkit to create Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="e3d15-113">Para obter mais informações, siga as instruções em [Usar o Kit de Ferramentas do Azure para IntelliJ para criar aplicativos Spark para um cluster do HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span><span class="sxs-lookup"><span data-stu-id="e3d15-113">For more information, follow the instructions in [Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="e3d15-114">**Serviço SSH do HDInsight com gerenciamento de nome de usuário e senha**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="e3d15-115">Para obter mais informações, consulte [Conectar ao HDInsight (Hadoop) usando o SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [Usar o túnel SSH para acessar a interface do usuário Web do Ambari, JobHistory, NameNode, Oozie, entre outras](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span><span class="sxs-lookup"><span data-stu-id="e3d15-115">For more information, see [Connect to HDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="e3d15-116">Criar um aplicativo Spark Scala e configurá-lo para depuração remota</span><span class="sxs-lookup"><span data-stu-id="e3d15-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="e3d15-117">Inicie o IDEA do IntelliJ e crie um projeto.</span><span class="sxs-lookup"><span data-stu-id="e3d15-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="e3d15-118">Na caixa de diálogo **Novo Projeto** , faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e3d15-118">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="e3d15-119">a.</span><span class="sxs-lookup"><span data-stu-id="e3d15-119">a.</span></span> <span data-ttu-id="e3d15-120">Selecione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="e3d15-121">b.</span><span class="sxs-lookup"><span data-stu-id="e3d15-121">b.</span></span> <span data-ttu-id="e3d15-122">Selecione um modelo Java ou Scala com base em sua preferência.</span><span class="sxs-lookup"><span data-stu-id="e3d15-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="e3d15-123">Selecione entre as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="e3d15-123">Select between the following options:</span></span>

      - <span data-ttu-id="e3d15-124">**Spark no HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="e3d15-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="e3d15-125">**Spark no HDInsight (Java)**</span><span class="sxs-lookup"><span data-stu-id="e3d15-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="e3d15-126">**Amostra de execução do Spark no Cluster HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="e3d15-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="e3d15-127">Este exemplo usa um modelo de **Amostra de Execução do Spark no Cluster do HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="e3d15-128">c.</span><span class="sxs-lookup"><span data-stu-id="e3d15-128">c.</span></span> <span data-ttu-id="e3d15-129">Na lista **Ferramenta de build**, selecione uma das seguintes opções, de acordo com suas necessidades:</span><span class="sxs-lookup"><span data-stu-id="e3d15-129">In the **Build tool** list, select either of the following, according to your need:</span></span>

      - <span data-ttu-id="e3d15-130">**Maven**, para obter suporte ao assistente de criação de projetos Scala</span><span class="sxs-lookup"><span data-stu-id="e3d15-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="e3d15-131">**SBT**, para gerenciar as dependências e a compilação no projeto Scala</span><span class="sxs-lookup"><span data-stu-id="e3d15-131">**SBT**, for managing the dependencies and building for the Scala project</span></span> 

      ![Criar um projeto de depuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="e3d15-133">d.</span><span class="sxs-lookup"><span data-stu-id="e3d15-133">d.</span></span> <span data-ttu-id="e3d15-134">Selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="e3d15-135">Na janela **Novo Projeto** a seguir, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e3d15-135">In the next **New Project** window, do the following:</span></span>

   ![Selecione o SDK do Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="e3d15-137">a.</span><span class="sxs-lookup"><span data-stu-id="e3d15-137">a.</span></span> <span data-ttu-id="e3d15-138">Insira um nome de projeto e o local do projeto.</span><span class="sxs-lookup"><span data-stu-id="e3d15-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="e3d15-139">b.</span><span class="sxs-lookup"><span data-stu-id="e3d15-139">b.</span></span> <span data-ttu-id="e3d15-140">Na lista suspensa **SDK do Projeto**, selecione **Java 1.8** para o cluster **Spark 2.x** ou selecione **Java 1.7** para o cluster **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-140">In the **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="e3d15-141">c.</span><span class="sxs-lookup"><span data-stu-id="e3d15-141">c.</span></span> <span data-ttu-id="e3d15-142">Na lista suspensa **Versão do Spark**, o assistente de criação de projeto Scala integra a versão correta do SDK do Spark e do SDK do Scala.</span><span class="sxs-lookup"><span data-stu-id="e3d15-142">In the **Spark Version** drop-down list, the Scala project creation wizard integrates the correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="e3d15-143">Se a versão do cluster do Spark for inferior à versão 2.0, selecione **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-143">If the spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="e3d15-144">Caso contrário, selecione **Spark 2.x.**</span><span class="sxs-lookup"><span data-stu-id="e3d15-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="e3d15-145">Esse exemplo usa o **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="e3d15-146">d.</span><span class="sxs-lookup"><span data-stu-id="e3d15-146">d.</span></span> <span data-ttu-id="e3d15-147">Selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-147">Select **Finish**.</span></span>

4. <span data-ttu-id="e3d15-148">Selecione **src** > **main** > **scala** para abrir seu código no projeto.</span><span class="sxs-lookup"><span data-stu-id="e3d15-148">Select **src** > **main** > **scala** to open your code in the project.</span></span> <span data-ttu-id="e3d15-149">Este exemplo usa o script **SparkCore_wasbloTest**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-149">This example uses the **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="e3d15-150">Para acessar o menu **Editar Configurações**, selecione o ícone no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="e3d15-150">To access the **Edit Configurations** menu, select the icon in the upper-right corner.</span></span> <span data-ttu-id="e3d15-151">Nesse menu, você poderá criar ou editar as configurações de depuração remota.</span><span class="sxs-lookup"><span data-stu-id="e3d15-151">From this menu, you can create or edit the configurations for remote debugging.</span></span>

   ![Editar configurações](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="e3d15-153">Na caixa de diálogo **Configurações de Execução/Depuração**, selecione o sinal de mais (**+**).</span><span class="sxs-lookup"><span data-stu-id="e3d15-153">In the **Run/Debug Configurations** dialog box, select the plus sign (**+**).</span></span> <span data-ttu-id="e3d15-154">Selecione a opção **Enviar trabalho do Spark**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-154">Then select the **Submit Spark Job** option.</span></span>

   ![Adicionar nova configuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="e3d15-156">Insira as informações em **Nome**, **Cluster do Spark** e **Nome da classe principal**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="e3d15-157">Em seguida, selecione **Configurações avançadas**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-157">Then select **Advanced configuration**.</span></span> 

   ![Executar configurações de depuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="e3d15-159">Na caixa de diálogo **Configuração avançada de envio do Spark**, selecione **Habilitar depuração remota do Spark**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-159">In the **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="e3d15-160">Insira o nome de usuário do SSH e insira uma senha ou use um arquivo de chave privada.</span><span class="sxs-lookup"><span data-stu-id="e3d15-160">Enter the SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="e3d15-161">Selecione **OK** para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="e3d15-161">To save the configuration, select **OK**.</span></span>

   ![Habilitar depuração remota do Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="e3d15-163">Agora, a configuração está salva com o nome fornecido.</span><span class="sxs-lookup"><span data-stu-id="e3d15-163">The configuration is now saved with the name you provided.</span></span> <span data-ttu-id="e3d15-164">Para exibir os detalhes de configuração, selecione o nome da configuração.</span><span class="sxs-lookup"><span data-stu-id="e3d15-164">To view the configuration details, select the configuration name.</span></span> <span data-ttu-id="e3d15-165">Para fazer alterações, selecione **Editar configurações**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-165">To make changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="e3d15-166">Após concluir as definições de configurações, você poderá executar o projeto no cluster remoto ou realizar a depuração remota.</span><span class="sxs-lookup"><span data-stu-id="e3d15-166">After you complete the configurations settings, you can run the project against the remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-to-perform-remote-debugging"></a><span data-ttu-id="e3d15-167">Saiba como realizar a depuração remota</span><span class="sxs-lookup"><span data-stu-id="e3d15-167">Learn how to perform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="e3d15-168">Cenário 1: realizar a execução remota</span><span class="sxs-lookup"><span data-stu-id="e3d15-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="e3d15-169">Nesta seção, mostraremos como depurar drivers e executores.</span><span class="sxs-lookup"><span data-stu-id="e3d15-169">In this section, we show you how to debug drivers and executors.</span></span>

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
        /** Tracks the total query count and number of aggregate bytes for a particular group. */
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


1. <span data-ttu-id="e3d15-170">Configure pontos de interrupção e, em seguida, selecione o ícone **Depurar**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-170">Set up breaking points, and then select the **Debug** icon.</span></span>

   ![Selecione o ícone de depuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="e3d15-172">Quando a execução do programa atingir o ponto de interrupção, você verá uma guia **Driver** e duas guias **Executor** no painel **Depurador**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-172">When the program execution reaches the breaking point, you see a **Driver** tab and two **Executor** tabs in the **Debugger** pane.</span></span> <span data-ttu-id="e3d15-173">Selecione o ícone **Retomar Programa** para continuar a execução do código, que alcança o próximo ponto de interrupção e enfoca na guia **Executor** correspondente. Você pode examinar os logs de execução na guia **Console** correspondente.</span><span class="sxs-lookup"><span data-stu-id="e3d15-173">Select the **Resume Program** icon to continue running the code, which then reaches the next breakpoint and focuses on the corresponding **Executor** tab. You can review the execution logs on the corresponding **Console** tab.</span></span>

   ![Guia depuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="e3d15-175">Cenário 2: Executar depuração remota e correção de bugs</span><span class="sxs-lookup"><span data-stu-id="e3d15-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="e3d15-176">Nesta seção, mostraremos como atualizar dinamicamente o valor da variável usando a capacidade de depuração do IntelliJ para uma correção simples.</span><span class="sxs-lookup"><span data-stu-id="e3d15-176">In this section, we show you how to dynamically update the variable value by using the IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="e3d15-177">No exemplo de código a seguir, uma exceção será lançada porque o arquivo de destino já existe.</span><span class="sxs-lookup"><span data-stu-id="e3d15-177">In the following code example, an exception is thrown because the target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find the rows that have only one digit in the sixth column.
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


#### <a name="to-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="e3d15-178">Para realizar a depuração remota e a correção de bugs</span><span class="sxs-lookup"><span data-stu-id="e3d15-178">To perform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="e3d15-179">Configure dois pontos de interrupção e, em seguida, selecione o ícone **Depurar** para iniciar o processo de depuração remota.</span><span class="sxs-lookup"><span data-stu-id="e3d15-179">Set up two breaking points, and then select the **Debug** icon to start the remote debugging process.</span></span>

2. <span data-ttu-id="e3d15-180">O código para no primeiro ponto de interrupção e as informações de parâmetro e de variáveis são mostradas no painel **Variáveis**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-180">The code stops at the first breaking point, and the parameter and variable information are shown in the **Variables** pane.</span></span> 

3. <span data-ttu-id="e3d15-181">Selecione o ícone **Retomar Programa** para continuar.</span><span class="sxs-lookup"><span data-stu-id="e3d15-181">Select the **Resume Program** icon to continue.</span></span> <span data-ttu-id="e3d15-182">O código para no segundo ponto.</span><span class="sxs-lookup"><span data-stu-id="e3d15-182">The code stops at the second point.</span></span> <span data-ttu-id="e3d15-183">A exceção é capturada conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="e3d15-183">The exception is caught as expected.</span></span>

  ![Gerar erro](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="e3d15-185">Selecione o ícone **Retomar Programa** novamente.</span><span class="sxs-lookup"><span data-stu-id="e3d15-185">Select the **Resume Program** icon again.</span></span> <span data-ttu-id="e3d15-186">A janela **Envio do HDInsight Spark** exibe um erro de “falha na execução do trabalho”.</span><span class="sxs-lookup"><span data-stu-id="e3d15-186">The **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![Envio de erro](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="e3d15-188">Para atualizar dinamicamente o valor da variável usando a capacidade de depuração do IntelliJ, selecione **Depurar** novamente.</span><span class="sxs-lookup"><span data-stu-id="e3d15-188">To dynamically update the variable value by using the IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="e3d15-189">O painel **Variáveis** é exibido novamente.</span><span class="sxs-lookup"><span data-stu-id="e3d15-189">The **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="e3d15-190">Clique com o botão direito do mouse no destino na guia **Depurar** e, então, selecione **Definir valor**.</span><span class="sxs-lookup"><span data-stu-id="e3d15-190">Right-click the target on the **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="e3d15-191">Em seguida, insira um novo valor para a variável.</span><span class="sxs-lookup"><span data-stu-id="e3d15-191">Next, enter a new value for the variable.</span></span> <span data-ttu-id="e3d15-192">Depois, selecione **Enter** para salvar o valor.</span><span class="sxs-lookup"><span data-stu-id="e3d15-192">Then select **Enter** to save the value.</span></span> 

  ![Definir valor](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="e3d15-194">Selecione o ícone **Retomar Programa** para continuar a execução do programa.</span><span class="sxs-lookup"><span data-stu-id="e3d15-194">Select the **Resume Program** icon to continue to run the program.</span></span> <span data-ttu-id="e3d15-195">Neste momento, nenhuma exceção é detectada.</span><span class="sxs-lookup"><span data-stu-id="e3d15-195">This time, no exception is caught.</span></span> <span data-ttu-id="e3d15-196">Você pode ver que o projeto é executado com êxito, sem exceções.</span><span class="sxs-lookup"><span data-stu-id="e3d15-196">You can see that the project runs successfully without any exceptions.</span></span>

  ![Depurar sem exceção](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="e3d15-198"><a name="seealso"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3d15-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="e3d15-199">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3d15-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="e3d15-200">Demonstração</span><span class="sxs-lookup"><span data-stu-id="e3d15-200">Demo</span></span>
* <span data-ttu-id="e3d15-201">Criar projeto do Scala (vídeo): [Criar aplicativos Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="e3d15-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="e3d15-202">Depuração remota (vídeo): [Usar o Kit de Ferramentas do Azure para IntelliJ para depurar aplicativos Spark remotamente em um cluster do HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="e3d15-202">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="e3d15-203">Cenários</span><span class="sxs-lookup"><span data-stu-id="e3d15-203">Scenarios</span></span>
* [<span data-ttu-id="e3d15-204">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="e3d15-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e3d15-205">Spark com Machine Learning: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="e3d15-205">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="e3d15-206">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para prever resultados da inspeção de alimentos</span><span class="sxs-lookup"><span data-stu-id="e3d15-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e3d15-207">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="e3d15-207">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="e3d15-208">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3d15-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="e3d15-209">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="e3d15-209">Create and run applications</span></span>
* [<span data-ttu-id="e3d15-210">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="e3d15-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e3d15-211">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="e3d15-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="e3d15-212">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="e3d15-212">Tools and extensions</span></span>
* [<span data-ttu-id="e3d15-213">Usar o Kit de Ferramentas do Azure para IntelliJ para criar aplicativos Spark para um cluster do HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3d15-213">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e3d15-214">Usar o kit de ferramentas do Azure para IntelliJ a fim de depurar aplicativos Spark remotamente por meio da VPN</span><span class="sxs-lookup"><span data-stu-id="e3d15-214">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="e3d15-215">Usar ferramentas do HDInsight para IntelliJ com a área restrita do Hortonworks</span><span class="sxs-lookup"><span data-stu-id="e3d15-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="e3d15-216">Usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para Eclipse para criar aplicativos Spark</span><span class="sxs-lookup"><span data-stu-id="e3d15-216">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="e3d15-217">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3d15-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="e3d15-218">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3d15-218">Kernels available for Jupyter notebook in the Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e3d15-219">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="e3d15-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="e3d15-220">Instalar o Jupyter em seu computador e conectar-se a um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3d15-220">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="e3d15-221">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="e3d15-221">Manage resources</span></span>
* [<span data-ttu-id="e3d15-222">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3d15-222">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e3d15-223">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3d15-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
