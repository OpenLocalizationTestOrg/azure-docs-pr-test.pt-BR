---
title: aaaUse Kit de ferramentas do Azure para IntelliJ com Hortonworks Sandbox | Microsoft Docs
description: Saiba como toouse HDInsight ferramentas no Kit de ferramentas do Azure para IntelliJ com Hortonworks seguro.
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
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="02e81-104">Usar ferramentas de HDInsight para IntelliJ com a área restrita do Hortonworks</span><span class="sxs-lookup"><span data-stu-id="02e81-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="02e81-105">Saiba como toouse ferramentas do HDInsight para IntelliJ toodevelop Apache Scala aplicativos e, então, testar Olá aplicativos em [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) em execução em sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="02e81-105">Learn how toouse HDInsight Tools for IntelliJ toodevelop Apache Scala applications and then test hello applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="02e81-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) é um ambiente de desenvolvimento integrado Java (IDE) para o desenvolvimento de software de computador.</span><span class="sxs-lookup"><span data-stu-id="02e81-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="02e81-107">Depois de ter desenvolvido e testar seus aplicativos na área restrita do Hortonworks, você pode movê-los muito[HDInsight do Azure](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="02e81-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them too[Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02e81-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="02e81-108">Prerequisites</span></span>

<span data-ttu-id="02e81-109">Antes de começar este tutorial, você deverá ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="02e81-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="02e81-110">HDP (Plataforma de Dados do Hortonworks) 2.4 na Área Restrita do Hortonworks em execução no seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="02e81-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="02e81-111">tooconfigure HDP, consulte [começar no ecossistema do Hadoop Olá com um sandbox Hadoop em uma máquina virtual](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="02e81-111">tooconfigure HDP, see [Get started in hello Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="02e81-112">As Ferramentas do HDInsight para IntelliJ foram testadas somente com HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="02e81-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="02e81-113">tooget HDP 2.4, expanda **Hortonworks Sandbox arquivamento** em Olá [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="02e81-113">tooget HDP 2.4, expand **Hortonworks Sandbox Archive** on hello [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="02e81-114">[Java Developer Kit (JDK) versão 1.8 ou posterior](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="02e81-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="02e81-115">JDK é exigida pelo Olá Kit de ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="02e81-115">JDK is required by hello Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="02e81-116">[Edição de comunidade IDEIA IntelliJ](https://www.jetbrains.com/idea/download) com hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in e hello [Kit de ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span><span class="sxs-lookup"><span data-stu-id="02e81-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and hello [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="02e81-117">Ferramentas de HDInsight para IntelliJ está disponível como parte do Kit de ferramentas do Azure para IntelliJ de saudação.</span><span class="sxs-lookup"><span data-stu-id="02e81-117">HDInsight Tools for IntelliJ is available as a part of hello Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="02e81-118">tooinstall Olá plug-ins, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="02e81-118">tooinstall hello plug-ins, do hello following:</span></span>

  1. <span data-ttu-id="02e81-119">Abra o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="02e81-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="02e81-120">Em Olá **bem-vindo** tela, selecione **configurar**e, em seguida, selecione **plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="02e81-120">On hello **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="02e81-121">Selecione **JetBrains instalar plug-in** no canto inferior esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="02e81-121">Select **Install JetBrains plugin** in hello lower-left corner.</span></span>
  4. <span data-ttu-id="02e81-122">Use Olá toosearch de função de pesquisa para **Scala**e, em seguida, selecione **instalar**.</span><span class="sxs-lookup"><span data-stu-id="02e81-122">Use hello search function toosearch for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="02e81-123">Selecione **reiniciar IntelliJ IDEIA** toocomplete instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="02e81-123">Select **Restart IntelliJ IDEA** toocomplete hello installation.</span></span>
  6. <span data-ttu-id="02e81-124">Saudação de tooinstall Repita a etapa 4 e 5 **Kit de ferramentas do Azure para IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="02e81-124">Repeat step 4 and 5 tooinstall hello **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="02e81-125">Para obter mais informações, consulte [Olá instalar o Kit de ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="02e81-125">For more information, see [Install hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="02e81-126">Criar um aplicativo Spark Scala</span><span class="sxs-lookup"><span data-stu-id="02e81-126">Create a Spark Scala application</span></span>

<span data-ttu-id="02e81-127">Nesta seção, você cria um projeto de exemplo do Scala usando o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="02e81-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="02e81-128">Na próxima seção, Olá, você vincular IDEIA IntelliJ toohello Hortonworks área restrita (emulador) antes de enviar o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="02e81-128">In hello next section, you link IntelliJ IDEA toohello Hortonworks Sandbox (emulator) before you submit hello project.</span></span>

1. <span data-ttu-id="02e81-129">Abra IntelliJ IDEA de sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="02e81-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="02e81-130">Em Olá **novo projeto** caixa de diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="02e81-130">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="02e81-131">a.</span><span class="sxs-lookup"><span data-stu-id="02e81-131">a.</span></span> <span data-ttu-id="02e81-132">Selecione **HDInsight** > **Spark no HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="02e81-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="02e81-133">b.</span><span class="sxs-lookup"><span data-stu-id="02e81-133">b.</span></span> <span data-ttu-id="02e81-134">Em Olá **ferramenta de compilação** , selecione qualquer uma das Olá a seguir, de acordo com a necessidade de tooyour:</span><span class="sxs-lookup"><span data-stu-id="02e81-134">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

    * <span data-ttu-id="02e81-135">**Maven**, para obter suporte ao assistente de criação de projetos Scala</span><span class="sxs-lookup"><span data-stu-id="02e81-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="02e81-136">**SBT**, para gerenciar dependências hello e criação de projeto de Scala Olá</span><span class="sxs-lookup"><span data-stu-id="02e81-136">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

   ![caixa de diálogo Novo projeto Olá](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="02e81-138">Selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="02e81-138">Select **Next**.</span></span>

3. <span data-ttu-id="02e81-139">Em Olá próximo **novo projeto** caixa de diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="02e81-139">In hello next **New Project** dialog box, do hello following:</span></span>

    ![Criar IntelliJ Scala propriedades do projeto](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="02e81-141">a.</span><span class="sxs-lookup"><span data-stu-id="02e81-141">a.</span></span> <span data-ttu-id="02e81-142">Em Olá **nome do projeto** , digite um nome de projeto.</span><span class="sxs-lookup"><span data-stu-id="02e81-142">In hello **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="02e81-143">b.</span><span class="sxs-lookup"><span data-stu-id="02e81-143">b.</span></span> <span data-ttu-id="02e81-144">Em Olá **local do projeto** caixa, digite o local do projeto.</span><span class="sxs-lookup"><span data-stu-id="02e81-144">In hello **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="02e81-145">c.</span><span class="sxs-lookup"><span data-stu-id="02e81-145">c.</span></span> <span data-ttu-id="02e81-146">Próxima toohello **projeto SDK** lista suspensa, selecione **novo**, selecione **JDK**, e, em seguida, especifique a pasta de saudação do JDK Java versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="02e81-146">Next toohello **Project SDK** drop-down list, select **New**, select **JDK**, and then specify hello folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="02e81-147">Selecione **Java 1.8** para cluster de 2. x Spark hello, ou selecione **Java 1.7** para cluster 1. x do hello Spark.</span><span class="sxs-lookup"><span data-stu-id="02e81-147">Select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span> <span data-ttu-id="02e81-148">local do saudação padrão é C:\Program Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="02e81-148">hello default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="02e81-149">d.</span><span class="sxs-lookup"><span data-stu-id="02e81-149">d.</span></span> <span data-ttu-id="02e81-150">Em Olá **versão Spark** lista suspensa, o Assistente de criação de projeto Scala se integra a versão correta do Olá para Spark SDK e Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="02e81-150">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="02e81-151">Se a versão do cluster Spark Olá for anterior à 2.0, selecione **despertar 1. x**.</span><span class="sxs-lookup"><span data-stu-id="02e81-151">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="02e81-152">Caso contrário, selecione **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="02e81-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="02e81-153">Esse exemplo usa o Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="02e81-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="02e81-154">Certifique-se de que você está usando o repositório de saudação marcado Scala 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="02e81-154">Make sure that you are using hello repository marked Scala 2.10.x.</span></span> <span data-ttu-id="02e81-155">Não use o repositório Olá marcado Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="02e81-155">Do not use hello repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="02e81-156">Selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="02e81-156">Select **Finish**.</span></span>

5. <span data-ttu-id="02e81-157">Se hello **projeto** exibição não ainda estiver aberta, pressione **Alt + 1** tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="02e81-157">If hello **Project** view is not already open, press **Alt+1** tooopen it.</span></span>

6. <span data-ttu-id="02e81-158">Em **Explorador de projeto**, expanda o projeto hello e, em seguida, selecione **src**.</span><span class="sxs-lookup"><span data-stu-id="02e81-158">In **Project Explorer**, expand hello project, and then select **src**.</span></span>

7. <span data-ttu-id="02e81-159">Clique com botão direito **src**, ponto muito**novo**e, em seguida, selecione **Scala classe**.</span><span class="sxs-lookup"><span data-stu-id="02e81-159">Right-click **src**, point too**New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="02e81-160">Em Olá **nome** , digite um nome em Olá **tipo** selecione **objeto**e, em seguida, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="02e81-160">In hello **Name** box, enter a name, in hello **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![janela de criar uma nova classe de Scala Olá](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="02e81-162">No arquivo de .scala hello, cole Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="02e81-162">In hello .scala file, paste hello following code:</span></span>

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

10. <span data-ttu-id="02e81-163">Em Olá **criar** menu, selecione **projeto de compilação**.</span><span class="sxs-lookup"><span data-stu-id="02e81-163">On hello **Build** menu, select **Build project**.</span></span> <span data-ttu-id="02e81-164">Certifique-se de que compilação Olá foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="02e81-164">Make sure that hello compilation has been completed successfully.</span></span>


## <a name="link-toohello-hortonworks-sandbox"></a><span data-ttu-id="02e81-165">Vincular toohello Hortonworks seguro</span><span class="sxs-lookup"><span data-stu-id="02e81-165">Link toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="02e81-166">Antes de poder vincular tooa Hortonworks área restrita (emulador), você deve ter um aplicativo IntelliJ existente.</span><span class="sxs-lookup"><span data-stu-id="02e81-166">Before you can link tooa Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="02e81-167">emulador de tooan toolink, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="02e81-167">toolink tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="02e81-168">Projeto de saudação aberto no IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="02e81-168">Open hello project in IntelliJ.</span></span>

2. <span data-ttu-id="02e81-169">Em Olá **exibição** menu, selecione **ferramentas Windows**e, em seguida, selecione **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="02e81-169">On hello **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="02e81-170">Expanda **Azure**, clique com o botão direito do mouse em **HDInsight** e, em seguida, selecione **Vincular um Emulador**.</span><span class="sxs-lookup"><span data-stu-id="02e81-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="02e81-171">Em Olá **Link um novo emulador** janela, digite a senha de saudação configurou para a conta raiz de saudação do hello Hortonworks Sandbox, digite toothose de valores semelhantes no hello captura de tela a seguir e, em seguida, selecione **Okey** .</span><span class="sxs-lookup"><span data-stu-id="02e81-171">In hello **Link A New Emulator** window, enter hello password that you've configured for hello root account of hello Hortonworks Sandbox, enter values similar toothose in hello following screenshot, and then select **OK**.</span></span> 

   ![janela de "Vincular um novo emulador" Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="02e81-173">emulador de saudação tooconfigure, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="02e81-173">tooconfigure hello emulator, select **Yes**.</span></span>

<span data-ttu-id="02e81-174">Quando emulador Olá estiver conectado com êxito, emulador hello (Hortonworks área restrita) é listado no nó de HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="02e81-174">When hello emulator is connected successfully, hello emulator (Hortonworks Sandbox) is listed in hello HDInsight node.</span></span>

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a><span data-ttu-id="02e81-175">Enviar Olá Spark Scala aplicativo toohello Hortonworks seguro</span><span class="sxs-lookup"><span data-stu-id="02e81-175">Submit hello Spark Scala application toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="02e81-176">Depois de vincular o emulador de toohello IntelliJ IDEIA, você poderá enviar seu projeto.</span><span class="sxs-lookup"><span data-stu-id="02e81-176">After you have linked IntelliJ IDEA toohello emulator, you can submit your project.</span></span>

<span data-ttu-id="02e81-177">toosubmit um emulador de tooan de projeto, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="02e81-177">toosubmit a project tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="02e81-178">Em **Explorador de projeto**, clique com botão direito hello e, em seguida, selecione **tooHDInsight do aplicativo de envio Spark**.</span><span class="sxs-lookup"><span data-stu-id="02e81-178">In **Project Explorer**, right-click hello project, and then select **Submit Spark application tooHDInsight**.</span></span>

2. <span data-ttu-id="02e81-179">Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="02e81-179">Do hello following:</span></span>

    <span data-ttu-id="02e81-180">a.</span><span class="sxs-lookup"><span data-stu-id="02e81-180">a.</span></span> <span data-ttu-id="02e81-181">Em Olá **cluster Spark (Linux)** lista suspensa, selecione o local seguro de Hortonworks.</span><span class="sxs-lookup"><span data-stu-id="02e81-181">In hello **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="02e81-182">b.</span><span class="sxs-lookup"><span data-stu-id="02e81-182">b.</span></span> <span data-ttu-id="02e81-183">Em Olá **nome da classe principal** caixa, escolha ou insira o nome da classe principal de saudação.</span><span class="sxs-lookup"><span data-stu-id="02e81-183">In hello **Main class name** box, choose or enter hello main class name.</span></span> <span data-ttu-id="02e81-184">Para este tutorial, o nome de saudação é **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="02e81-184">For this tutorial, hello name is **GroupByTest**.</span></span>

3. <span data-ttu-id="02e81-185">Selecione **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="02e81-185">Select **Submit**.</span></span> <span data-ttu-id="02e81-186">Olá logs de envio de trabalho são mostrados na janela de ferramenta de envio Olá Spark.</span><span class="sxs-lookup"><span data-stu-id="02e81-186">hello job submission logs are shown in hello Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02e81-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="02e81-187">Next steps</span></span>

- <span data-ttu-id="02e81-188">toolearn como toocreate aplicativos de Spark para HDInsight usando ferramentas de HDInsight para IntelliJ, ir muito[usar ferramentas de HDInsight no Kit de ferramentas do Azure para aplicativos do IntelliJ toocreate Spark para HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="02e81-188">toolearn how toocreate Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="02e81-189">toowatch um vídeo de ferramentas de HDInsight para IntelliJ, ir muito[introduzir ferramentas de HDInsight para IntelliJ para desenvolvimento Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).</span><span class="sxs-lookup"><span data-stu-id="02e81-189">toowatch a video of HDInsight Tools for IntelliJ, go too[Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="02e81-190">toolearn como aplicativos de Spark toodebug usando Olá toolkit remotamente no HDInsight por meio do SSH, ir muito[depurar remotamente aplicativos Spark em um cluster de HDInsight com o Kit de ferramentas do Azure para IntelliJ por meio do SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="02e81-190">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through SSH, go too[Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="02e81-191">toolearn como aplicativos de Spark toodebug usando Olá toolkit remotamente no HDInsight por meio de VPN, vá muito[usar ferramentas de HDInsight no Kit de ferramentas do Azure para aplicativos de Spark toodebug IntelliJ remotamente no cluster HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="02e81-191">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through VPN, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="02e81-192">toolearn como toouse ferramentas HDInsight para Eclipse toocreate um aplicativo Spark, ir muito[usar ferramentas de HDInsight no Kit de ferramentas do Azure para aplicativos do Eclipse toocreate Spark](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="02e81-192">toolearn how toouse HDInsight Tools for Eclipse toocreate a Spark application, go too[Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="02e81-193">toowatch um vídeo de ferramentas HDInsight para o Eclipse, vá muito[usar a ferramenta de HDInsight para aplicativos do Eclipse toocreate Spark](https://mix.office.com/watch/1rau2mopb6fha).</span><span class="sxs-lookup"><span data-stu-id="02e81-193">toowatch a video of HDInsight Tools for Eclipse, go too[Use HDInsight Tool for Eclipse toocreate Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
