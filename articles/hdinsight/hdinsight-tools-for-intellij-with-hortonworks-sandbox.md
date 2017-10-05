---
title: "Usar o Kit de Ferramentas do Azure para IntelliJ com a Área Restrita do Hortonworks | Microsoft Docs"
description: "Saiba como usar as ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ com a Área Restrita do Hortonworks."
keywords: "ferramentas do hadoop,consulta do hive,intellij,área restrita do hortonworks,kit de ferramentas do azure para intellij"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c49f185db5a035f70a711bf309b973182d94a2b0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="7447f-104">Usar ferramentas de HDInsight para IntelliJ com a área restrita do Hortonworks</span><span class="sxs-lookup"><span data-stu-id="7447f-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="7447f-105">Saiba como usar as Ferramentas do HDInsight para IntelliJ para desenvolver aplicativos Apache Scala e testar os aplicativos na [Área Restrita do Hortonworks](http://hortonworks.com/products/sandbox/) em execução em sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7447f-105">Learn how to use HDInsight Tools for IntelliJ to develop Apache Scala applications and then test the applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="7447f-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) é um ambiente de desenvolvimento integrado Java (IDE) para o desenvolvimento de software de computador.</span><span class="sxs-lookup"><span data-stu-id="7447f-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="7447f-107">Depois que você desenvolveu e testou seus aplicativos na área restrita do Hortonworks, você pode movê-los para [Azure HDInsight](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7447f-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them to [Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7447f-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7447f-108">Prerequisites</span></span>

<span data-ttu-id="7447f-109">Antes de começar este tutorial, você deverá ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7447f-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="7447f-110">HDP (Plataforma de Dados do Hortonworks) 2.4 na Área Restrita do Hortonworks em execução no seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="7447f-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="7447f-111">Para configurar o HDP, consulte [Introdução ao ecossistema Hadoop com uma área restrita do Hadoop em uma máquina virtual](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7447f-111">To configure HDP, see [Get started in the Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="7447f-112">As Ferramentas do HDInsight para IntelliJ foram testadas somente com HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="7447f-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="7447f-113">Para obter o HDP 2.4, expanda **Arquivamento da Área Restrita da Hortonworks** no [site de downloads da Área Restrita do Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="7447f-113">To get HDP 2.4, expand **Hortonworks Sandbox Archive** on the [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="7447f-114">[Java Developer Kit (JDK) versão 1.8 ou posterior](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="7447f-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="7447f-115">JDK é exigido pelo Kit de ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7447f-115">JDK is required by the Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="7447f-116">[Edição de comunidade do IntelliJ IDEA](https://www.jetbrains.com/idea/download) com o plug-in do [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) e o plug-in do [Kit de Ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij.md).</span><span class="sxs-lookup"><span data-stu-id="7447f-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with the [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and the [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="7447f-117">As Ferramentas do HDInsight para IntelliJ estão disponíveis como parte do Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7447f-117">HDInsight Tools for IntelliJ is available as a part of the Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="7447f-118">Para instalar os plug-ins, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7447f-118">To install the plug-ins, do the following:</span></span>

  1. <span data-ttu-id="7447f-119">Abra o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7447f-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="7447f-120">Na tela de **Boas-vindas**, selecione **Configurar** e, em seguida, selecione **Plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="7447f-120">On the **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="7447f-121">Selecione **Instalar o plug-in JetBrains** no canto inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="7447f-121">Select **Install JetBrains plugin** in the lower-left corner.</span></span>
  4. <span data-ttu-id="7447f-122">Use a função de pesquisa para pesquisar pelo **Scala** e, em seguida, selecione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="7447f-122">Use the search function to search for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="7447f-123">Selecione **Reiniciar IntelliJ IDEA** para concluir a instalação.</span><span class="sxs-lookup"><span data-stu-id="7447f-123">Select **Restart IntelliJ IDEA** to complete the installation.</span></span>
  6. <span data-ttu-id="7447f-124">Repita a etapa 4 e 5 para instalar o **Kit de ferramentas do Azure para IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="7447f-124">Repeat step 4 and 5 to install the **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="7447f-125">Para saber mais, confira [Instalar o Kit de Ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="7447f-125">For more information, see [Install the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="7447f-126">Criar um aplicativo Spark Scala</span><span class="sxs-lookup"><span data-stu-id="7447f-126">Create a Spark Scala application</span></span>

<span data-ttu-id="7447f-127">Nesta seção, você cria um projeto de exemplo do Scala usando o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7447f-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="7447f-128">Na próxima seção, você vincular IntelliJ IDEA à área restrita Hortonworks (emulador) antes de enviar o projeto.</span><span class="sxs-lookup"><span data-stu-id="7447f-128">In the next section, you link IntelliJ IDEA to the Hortonworks Sandbox (emulator) before you submit the project.</span></span>

1. <span data-ttu-id="7447f-129">Abra IntelliJ IDEA de sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7447f-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="7447f-130">Na caixa de diálogo **Novo Projeto** , faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7447f-130">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="7447f-131">a.</span><span class="sxs-lookup"><span data-stu-id="7447f-131">a.</span></span> <span data-ttu-id="7447f-132">Selecione **HDInsight** > **Spark no HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="7447f-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="7447f-133">b.</span><span class="sxs-lookup"><span data-stu-id="7447f-133">b.</span></span> <span data-ttu-id="7447f-134">Na lista **Ferramenta de build**, selecione uma das seguintes opções, de acordo com suas necessidades:</span><span class="sxs-lookup"><span data-stu-id="7447f-134">In the **Build tool** list, select either of the following, according to your need:</span></span>

    * <span data-ttu-id="7447f-135">**Maven**, para obter suporte ao assistente de criação de projetos Scala</span><span class="sxs-lookup"><span data-stu-id="7447f-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="7447f-136">**SBT**, para gerenciar as dependências e a compilação no projeto Scala</span><span class="sxs-lookup"><span data-stu-id="7447f-136">**SBT**, for managing the dependencies and building for the Scala project</span></span>

   ![A caixa de diálogo Novo Projeto](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="7447f-138">Selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="7447f-138">Select **Next**.</span></span>

3. <span data-ttu-id="7447f-139">Na caixa de diálogo **Novo Projeto** a seguir, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7447f-139">In the next **New Project** dialog box, do the following:</span></span>

    ![Criar IntelliJ Scala propriedades do projeto](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="7447f-141">a.</span><span class="sxs-lookup"><span data-stu-id="7447f-141">a.</span></span> <span data-ttu-id="7447f-142">Na caixa **Nome do projeto**, digite um nome para o projeto.</span><span class="sxs-lookup"><span data-stu-id="7447f-142">In the **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="7447f-143">b.</span><span class="sxs-lookup"><span data-stu-id="7447f-143">b.</span></span> <span data-ttu-id="7447f-144">Na caixa **Local do projeto**, digite um local para o projeto.</span><span class="sxs-lookup"><span data-stu-id="7447f-144">In the **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="7447f-145">c.</span><span class="sxs-lookup"><span data-stu-id="7447f-145">c.</span></span> <span data-ttu-id="7447f-146">Ao lado da lista suspensa **SDK do Projeto**, selecione **Novo**, selecione **JDK** e, em seguida, especifique a pasta do JDK Java versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7447f-146">Next to the **Project SDK** drop-down list, select **New**, select **JDK**, and then specify the folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="7447f-147">Selecione **Java 1.8** para o cluster Spark 2.x ou selecione **Java 1.7** para o cluster Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="7447f-147">Select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span> <span data-ttu-id="7447f-148">O local padrão é C:\Program Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="7447f-148">The default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="7447f-149">d.</span><span class="sxs-lookup"><span data-stu-id="7447f-149">d.</span></span> <span data-ttu-id="7447f-150">Na lista suspensa **Versão do Spark**, o assistente de criação de projeto Scala integra a versão apropriada do SDK do Spark e do SDK do Scala.</span><span class="sxs-lookup"><span data-stu-id="7447f-150">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="7447f-151">Se a versão do cluster do Spark for inferior a 2.0, selecione **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="7447f-151">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="7447f-152">Caso contrário, selecione **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="7447f-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="7447f-153">Esse exemplo usa o Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="7447f-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="7447f-154">Certifique de estar usando o repositório marcado como Scala 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="7447f-154">Make sure that you are using the repository marked Scala 2.10.x.</span></span> <span data-ttu-id="7447f-155">Não use o repositório marcado como Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="7447f-155">Do not use the repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="7447f-156">Selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="7447f-156">Select **Finish**.</span></span>

5. <span data-ttu-id="7447f-157">Se a exibição **Projeto** ainda não estiver aberta, pressione **Alt + 1** para abri-la.</span><span class="sxs-lookup"><span data-stu-id="7447f-157">If the **Project** view is not already open, press **Alt+1** to open it.</span></span>

6. <span data-ttu-id="7447f-158">Em **Explorador de Projeto**, expanda o projeto e, em seguida, selecione **src**.</span><span class="sxs-lookup"><span data-stu-id="7447f-158">In **Project Explorer**, expand the project, and then select **src**.</span></span>

7. <span data-ttu-id="7447f-159">Clique com o botão direito do mouse em **src**, aponte para **Novo** e, em seguida, selecione **Classe Scala**.</span><span class="sxs-lookup"><span data-stu-id="7447f-159">Right-click **src**, point to **New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="7447f-160">Digite um nome na caixa **Nome**, na caixa **Tipo**, selecione **Objeto** e, em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="7447f-160">In the **Name** box, enter a name, in the **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![A janela Criar Nova Classe Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="7447f-162">No arquivo .scala, cole este código:</span><span class="sxs-lookup"><span data-stu-id="7447f-162">In the .scala file, paste the following code:</span></span>

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. <span data-ttu-id="7447f-163">No menu **Compilar**, selecione **Compilar projeto**.</span><span class="sxs-lookup"><span data-stu-id="7447f-163">On the **Build** menu, select **Build project**.</span></span> <span data-ttu-id="7447f-164">Verifique se a compilação foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="7447f-164">Make sure that the compilation has been completed successfully.</span></span>


## <a name="link-to-the-hortonworks-sandbox"></a><span data-ttu-id="7447f-165">Link para a Área Restrita do Hortonworks</span><span class="sxs-lookup"><span data-stu-id="7447f-165">Link to the Hortonworks Sandbox</span></span>

<span data-ttu-id="7447f-166">Antes que possa estabelecer um vínculo com uma Área Restrita do Sandbox (emulador), você precisa ter um aplicativo IntelliJ existente.</span><span class="sxs-lookup"><span data-stu-id="7447f-166">Before you can link to a Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="7447f-167">Para estabelecer um vínculo com um emulador, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7447f-167">To link to an emulator, do the following:</span></span>

1. <span data-ttu-id="7447f-168">Abra o projeto no IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7447f-168">Open the project in IntelliJ.</span></span>

2. <span data-ttu-id="7447f-169">No menu **Exibir**, selecione **Janelas de Ferramentas** e selecione o **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="7447f-169">On the **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="7447f-170">Expanda **Azure**, clique com o botão direito do mouse em **HDInsight** e, em seguida, selecione **Vincular um Emulador**.</span><span class="sxs-lookup"><span data-stu-id="7447f-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="7447f-171">Na janela **Vincular um Novo Emulador**, digite a senha que você configurou para a conta raiz da Área de Restrita do Hortonworks, insira valores semelhantes aos que estão na seguinte captura de tela e, em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="7447f-171">In the **Link A New Emulator** window, enter the password that you've configured for the root account of the Hortonworks Sandbox, enter values similar to those in the following screenshot, and then select **OK**.</span></span> 

   ![A janela "Vincular um Novo Emulador"](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="7447f-173">Para configurar o emulador, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="7447f-173">To configure the emulator, select **Yes**.</span></span>

<span data-ttu-id="7447f-174">Quando for conectado com êxito, o emulador (Área Restrita do Hortonworks) será listado no nó do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7447f-174">When the emulator is connected successfully, the emulator (Hortonworks Sandbox) is listed in the HDInsight node.</span></span>

## <a name="submit-the-spark-scala-application-to-the-hortonworks-sandbox"></a><span data-ttu-id="7447f-175">Enviar o aplicativo Scala Spark à Área Restrita do Hortonworks</span><span class="sxs-lookup"><span data-stu-id="7447f-175">Submit the Spark Scala application to the Hortonworks Sandbox</span></span>

<span data-ttu-id="7447f-176">Após vincular o IntelliJ IDEA ao emulador, você pode enviar seu projeto.</span><span class="sxs-lookup"><span data-stu-id="7447f-176">After you have linked IntelliJ IDEA to the emulator, you can submit your project.</span></span>

<span data-ttu-id="7447f-177">Para enviar um projeto em um emulador, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7447f-177">To submit a project to an emulator, do the following:</span></span>

1. <span data-ttu-id="7447f-178">No **Explorador de Projetos**, clique com o botão direito do mouse no projeto e selecione **Enviar Aplicativo Spark ao HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7447f-178">In **Project Explorer**, right-click the project, and then select **Submit Spark application to HDInsight**.</span></span>

2. <span data-ttu-id="7447f-179">Faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7447f-179">Do the following:</span></span>

    <span data-ttu-id="7447f-180">a.</span><span class="sxs-lookup"><span data-stu-id="7447f-180">a.</span></span> <span data-ttu-id="7447f-181">Na lista suspensa **Cluster Spark (somente no Linux)**, selecione a Área Restrita do Hortonworks local.</span><span class="sxs-lookup"><span data-stu-id="7447f-181">In the **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="7447f-182">b.</span><span class="sxs-lookup"><span data-stu-id="7447f-182">b.</span></span> <span data-ttu-id="7447f-183">Na caixa **Nome de classe principal**, escolha ou digite o nome de classe principal.</span><span class="sxs-lookup"><span data-stu-id="7447f-183">In the **Main class name** box, choose or enter the main class name.</span></span> <span data-ttu-id="7447f-184">Para este tutorial, o nome é **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="7447f-184">For this tutorial, the name is **GroupByTest**.</span></span>

3. <span data-ttu-id="7447f-185">Selecione **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="7447f-185">Select **Submit**.</span></span> <span data-ttu-id="7447f-186">Os logs de envio de trabalho são mostrados na janela da ferramenta de envio Spark.</span><span class="sxs-lookup"><span data-stu-id="7447f-186">The job submission logs are shown in the Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7447f-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7447f-187">Next steps</span></span>

- <span data-ttu-id="7447f-188">Para saber como criar aplicativos Spark para HDInsight usando as Ferramentas do HDInsight para IntelliJ, vá até [Usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ a fim de criar aplicativos Spark para um cluster HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="7447f-188">To learn how to create Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="7447f-189">Para assistir a um vídeo sobre as Ferramentas do HDInsight para IntelliJ, vá até [Introduzir as Ferramentas do HDInsight para IntelliJ para desenvolvimento Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).</span><span class="sxs-lookup"><span data-stu-id="7447f-189">To watch a video of HDInsight Tools for IntelliJ, go to [Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="7447f-190">Para saber como depurar aplicativos Spark usando o kit de ferramentas remotamente no HDInsight por meio de SSH, consulte [Depurar aplicativos Spark remotamente em um cluster HDInsight com o kit de ferramentas do Azure para IntelliJ por meio do SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="7447f-190">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through SSH, go to [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="7447f-191">Para saber como depurar aplicativos Spark usando o kit de ferramentas remotamente no HDInsight por meio da VPN, vá até [Usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ para depurar aplicativos Spark remotamente para um cluster do HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="7447f-191">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through VPN, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="7447f-192">Para saber como usar as Ferramentas do HDInsight para Eclipse para criar um aplicativo Spark, vá até [Usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para Eclipse para criar aplicativos Spark](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="7447f-192">To learn how to use HDInsight Tools for Eclipse to create a Spark application, go to [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="7447f-193">Para assistir a um vídeo sobre as Ferramentas do HDInsight para Eclipse, vá até [Usar a Ferramenta do HDInsight para Eclipse para criar aplicativos Spark](https://mix.office.com/watch/1rau2mopb6fha).</span><span class="sxs-lookup"><span data-stu-id="7447f-193">To watch a video of HDInsight Tools for Eclipse, go to [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
