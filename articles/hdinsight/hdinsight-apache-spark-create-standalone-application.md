---
title: aaaCreate Scala aplicativo toorun em clusters Spark - HDInsight do Azure | Microsoft Docs
description: "Crie um aplicativo Spark escrito em Scala com Apache Maven Olá build do sistema e um arquétipo Maven existente para Scala fornecido pelo IntelliJ IDEIA."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="988b6-103">Criar um toorun de aplicativo Scala Maven no cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="988b6-103">Create a Scala Maven application toorun on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="988b6-104">Saiba como toocreate um aplicativo Spark escrito em Scala usando Maven IntelliJ ideia.</span><span class="sxs-lookup"><span data-stu-id="988b6-104">Learn how toocreate a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="988b6-105">artigo Olá usa Apache Maven hello sistema de compilação e começa com um arquétipo Maven existente para Scala fornecido pelo IntelliJ IDEIA.</span><span class="sxs-lookup"><span data-stu-id="988b6-105">hello article uses Apache Maven as hello build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="988b6-106">Criando um aplicativo Scala no IntelliJ IDEIA envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="988b6-106">Creating a Scala application in IntelliJ IDEA involves hello following steps:</span></span>

* <span data-ttu-id="988b6-107">Use Maven como sistema de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="988b6-107">Use Maven as hello build system.</span></span>
* <span data-ttu-id="988b6-108">Atualize as dependências do módulo Spark de tooresolve de arquivo de modelo de objeto do projeto (POM).</span><span class="sxs-lookup"><span data-stu-id="988b6-108">Update Project Object Model (POM) file tooresolve Spark module dependencies.</span></span>
* <span data-ttu-id="988b6-109">Escreva seu aplicativo em Scala.</span><span class="sxs-lookup"><span data-stu-id="988b6-109">Write your application in Scala.</span></span>
* <span data-ttu-id="988b6-110">Gere um arquivo jar que pode ser enviado tooHDInsight Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="988b6-110">Generate a jar file that can be submitted tooHDInsight Spark clusters.</span></span>
* <span data-ttu-id="988b6-111">Execute o aplicativo hello no cluster do Spark usando Livy.</span><span class="sxs-lookup"><span data-stu-id="988b6-111">Run hello application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="988b6-112">HDInsight também fornece um processo IntelliJ IDEIA plug-in ferramenta tooease Olá de criar e enviar aplicativos tooan cluster HDInsight Spark no Linux.</span><span class="sxs-lookup"><span data-stu-id="988b6-112">HDInsight also provides an IntelliJ IDEA plugin tool tooease hello process of creating and submitting applications tooan HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="988b6-113">Para obter mais informações, consulte [Use HDInsight ferramentas de plug-in para toocreate IntelliJ IDEIA e enviar aplicativos Spark](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="988b6-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="988b6-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="988b6-114">Prerequisites</span></span>

* <span data-ttu-id="988b6-115">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="988b6-115">An Azure subscription.</span></span> <span data-ttu-id="988b6-116">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="988b6-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="988b6-117">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="988b6-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="988b6-118">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="988b6-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="988b6-119">Kit de desenvolvimento Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="988b6-119">Oracle Java Development kit.</span></span> <span data-ttu-id="988b6-120">Você pode instalá-lo clicando [aqui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="988b6-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="988b6-121">Um Java IDE.</span><span class="sxs-lookup"><span data-stu-id="988b6-121">A Java IDE.</span></span> <span data-ttu-id="988b6-122">Este artigo usa IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="988b6-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="988b6-123">Você pode instalá-lo clicando [aqui](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="988b6-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="988b6-124">Instalar o plug-in Scala para IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="988b6-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="988b6-125">Se instalação de IDEIA IntelliJ não não solicitar para habilitar o plug-in de Scala, inicie o IntelliJ IDEIA e percorrer Olá plug-in de saudação de tooinstall as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="988b6-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through hello following steps tooinstall hello plugin:</span></span>

1. <span data-ttu-id="988b6-126">Inicie o IntelliJ IDEA e, na tela de boas-vindas, clique em **Configurar** e, em seguida, clique em **Plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="988b6-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Habilitar plug-in do scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="988b6-128">Na próxima tela de saudação, clique em **JetBrains instalar plug-in** do canto inferior esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="988b6-128">In hello next screen, click **Install JetBrains plugin** from hello lower left corner.</span></span> <span data-ttu-id="988b6-129">Em Olá **Procurar plug-ins de JetBrains** caixa de diálogo que é aberta, procure Scala e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="988b6-129">In hello **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Instalar o plug-in do scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="988b6-131">Depois de saudação plug-in foi instalado com êxito, clique em Olá **botão reiniciar IntelliJ IDEIA** toorestart Olá IDE.</span><span class="sxs-lookup"><span data-stu-id="988b6-131">After hello plugin installs successfully, click hello **Restart IntelliJ IDEA button** toorestart hello IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="988b6-132">Criar um projeto de Scala autônomo</span><span class="sxs-lookup"><span data-stu-id="988b6-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="988b6-133">Inicie o IntelliJ IDEA e crie um novo projeto.</span><span class="sxs-lookup"><span data-stu-id="988b6-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="988b6-134">Na caixa de diálogo projeto novo hello, fazer Olá opções a seguir e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="988b6-134">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>
   
    ![Criar projeto Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="988b6-136">Selecione **Maven** como o tipo de projeto hello.</span><span class="sxs-lookup"><span data-stu-id="988b6-136">Select **Maven** as hello project type.</span></span>
   * <span data-ttu-id="988b6-137">Especifique um **SDK do projeto**.</span><span class="sxs-lookup"><span data-stu-id="988b6-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="988b6-138">Clique em novo e navegar o diretório de instalação do Java toohello, normalmente `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="988b6-138">Click New and navigate toohello Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="988b6-139">Selecione Olá **criar do arquétipo** opção.</span><span class="sxs-lookup"><span data-stu-id="988b6-139">Select hello **Create from archetype** option.</span></span>
   * <span data-ttu-id="988b6-140">Na lista de saudação do arquétipos, selecione **org.scala tools.archetypes:scala-arquétipo simples**.</span><span class="sxs-lookup"><span data-stu-id="988b6-140">From hello list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="988b6-141">Isso criará estrutura de diretório hello e baixar Olá necessário padrão dependências toowrite Scala programa.</span><span class="sxs-lookup"><span data-stu-id="988b6-141">This will create hello right directory structure and download hello required default dependencies toowrite Scala program.</span></span>
2. <span data-ttu-id="988b6-142">Forneça os valores relevantes para **GroupId**, **ArtifactId** e **versão**.</span><span class="sxs-lookup"><span data-stu-id="988b6-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="988b6-143">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="988b6-143">Click **Next**.</span></span>
3. <span data-ttu-id="988b6-144">Na próxima caixa de diálogo hello, em que você especificar o diretório base Maven e outras configurações do usuário, aceite os padrões de saudação e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="988b6-144">In hello next dialog box, where you specify Maven home directory and other user settings, accept hello defaults and click **Next**.</span></span>
4. <span data-ttu-id="988b6-145">Na caixa de diálogo última hello, especifique um nome de projeto e o local e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="988b6-145">In hello last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="988b6-146">Excluir Olá **MySpec.Scala** de arquivos no **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="988b6-146">Delete hello **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="988b6-147">Você não precisa isso para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="988b6-147">You do not need this for hello application.</span></span>
6. <span data-ttu-id="988b6-148">Se necessário, renomeie os arquivos de origem e de teste de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="988b6-148">If required, rename hello default source and test files.</span></span> <span data-ttu-id="988b6-149">No painel esquerdo de saudação no hello IntelliJ IDEIA, navegue muito**src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="988b6-149">From hello left pane in hello IntelliJ IDEA, navigate too**src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="988b6-150">Clique com botão direito **App.scala**, clique em **refatorar**, clique em Renomear o arquivo e na caixa de diálogo hello, forneça Olá novo nome para o aplicativo hello e, em seguida, clique em **refatorar**.</span><span class="sxs-lookup"><span data-stu-id="988b6-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in hello dialog box, provide hello new name for hello application and then click **Refactor**.</span></span>
   
    ![Renomear arquivos](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="988b6-152">As etapas subsequentes hello, você atualizará Olá pom.xml toodefine Olá dependências Olá Spark Scala aplicativo.</span><span class="sxs-lookup"><span data-stu-id="988b6-152">In hello subsequent steps, you will update hello pom.xml toodefine hello dependencies for hello Spark Scala application.</span></span> <span data-ttu-id="988b6-153">Para essas dependências toobe baixado e resolvidos automaticamente, que você deve configurar Maven adequadamente.</span><span class="sxs-lookup"><span data-stu-id="988b6-153">For those dependencies toobe downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Configurar Maven para downloads automáticos](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="988b6-155">De saudação **arquivo** menu, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="988b6-155">From hello **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="988b6-156">Em Olá **configurações** caixa de diálogo, navegue muito**implantação da compilação, execução,** > **ferramentas de compilação** > **Maven**  >  **Importando**.</span><span class="sxs-lookup"><span data-stu-id="988b6-156">In hello **Settings** dialog box, navigate too**Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="988b6-157">Selecione a opção de saudação muito**Maven importar projetos automaticamente**.</span><span class="sxs-lookup"><span data-stu-id="988b6-157">Select hello option too**Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="988b6-158">Clique em **Aplicar** e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="988b6-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="988b6-159">Atualize Olá Scala origem arquivo tooinclude seu código de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="988b6-159">Update hello Scala source file tooinclude your application code.</span></span> <span data-ttu-id="988b6-160">Abrir e substitua Olá código de exemplo existente com hello código a seguir e salve as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="988b6-160">Open and replace hello existing sample code with hello following code and save hello changes.</span></span> <span data-ttu-id="988b6-161">Esse código lê dados de saudação de Olá HVAC.csv (disponível em todos os clusters de HDInsight Spark), recupera linhas de saudação que têm apenas um dígito na coluna sexto hello e grava a saída de hello muito**/HVACOut** em armazenamento padrão da saudação contêiner de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="988b6-161">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello sixth column, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="988b6-162">Atualize pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="988b6-162">Update hello pom.xml.</span></span>
   
   1. <span data-ttu-id="988b6-163">Dentro de `<project>\<properties>` adicione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="988b6-163">Within `<project>\<properties>` add hello following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="988b6-164">Dentro de `<project>\<dependencies>` adicione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="988b6-164">Within `<project>\<dependencies>` add hello following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="988b6-165">Salve alterações toopom.xml.</span><span class="sxs-lookup"><span data-stu-id="988b6-165">Save changes toopom.xml.</span></span>
10. <span data-ttu-id="988b6-166">Crie o arquivo hello. jar.</span><span class="sxs-lookup"><span data-stu-id="988b6-166">Create hello .jar file.</span></span> <span data-ttu-id="988b6-167">O IntelliJ IDEA permite a criação de JAR como um artefato de um projeto.</span><span class="sxs-lookup"><span data-stu-id="988b6-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="988b6-168">Execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="988b6-168">Perform hello following steps.</span></span>
    
    1. <span data-ttu-id="988b6-169">De saudação **arquivo** menu, clique em **estrutura do projeto**.</span><span class="sxs-lookup"><span data-stu-id="988b6-169">From hello **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="988b6-170">Em Olá **estrutura do projeto** caixa de diálogo, clique em **artefatos** e, em seguida, clique em hello mais símbolo.</span><span class="sxs-lookup"><span data-stu-id="988b6-170">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="988b6-171">Na caixa de diálogo pop-up de saudação, clique em **JAR**e, em seguida, clique em **de módulos com dependências**.</span><span class="sxs-lookup"><span data-stu-id="988b6-171">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="988b6-173">Em Olá **criar JAR de módulos** caixa de diálogo, clique nas reticências da saudação (![reticências](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) em relação a saudação **classe principal**.</span><span class="sxs-lookup"><span data-stu-id="988b6-173">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against hello **Main Class**.</span></span>
    4. <span data-ttu-id="988b6-174">Em Olá **selecionar principal classe** caixa de diálogo, a classe Olá select que é exibido por padrão e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="988b6-174">In hello **Select Main Class** dialog box, select hello class that appears by default and then click **OK**.</span></span>
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="988b6-176">Em Olá **criar JAR de módulos** caixa de diálogo caixa, certifique-se de que a opção Olá muito**extrair toohello destino JAR** está selecionado e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="988b6-176">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="988b6-177">Isso cria um JAR único com todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="988b6-177">This creates a single JAR with all dependencies.</span></span>
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="988b6-179">Guia de layout de saída Olá lista todos os jars Olá que estão incluídos como parte do projeto de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="988b6-179">hello output layout tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="988b6-180">Você pode selecionar e excluir Olá aqueles nos quais Olá Scala aplicativo não tem nenhuma dependência direta.</span><span class="sxs-lookup"><span data-stu-id="988b6-180">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="988b6-181">Para o aplicativo hello, estamos criando aqui, você pode remover Olá tudo, exceto o último (**SparkSimpleApp saída de compilação**).</span><span class="sxs-lookup"><span data-stu-id="988b6-181">For hello application we are creating here, you can remove all but hello last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="988b6-182">Selecione Olá jars toodelete e clique em Olá **excluir** ícone.</span><span class="sxs-lookup"><span data-stu-id="988b6-182">Select hello jars toodelete and then click hello **Delete** icon.</span></span>
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="988b6-184">Certifique-se de **compilar no Verifique** caixa é selecionada, o que garante que jar Olá é criado sempre que o projeto Olá for criado ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="988b6-184">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="988b6-185">Clique em **Aplicar** e em **OK**.</span><span class="sxs-lookup"><span data-stu-id="988b6-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="988b6-186">Olá barra de menus, clique em **criar**e, em seguida, clique em **projeto Make**.</span><span class="sxs-lookup"><span data-stu-id="988b6-186">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="988b6-187">Você também pode clicar em **criar artefatos** toocreate jar de saudação.</span><span class="sxs-lookup"><span data-stu-id="988b6-187">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="988b6-188">Olá jar de saída é criado sob **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="988b6-188">hello output jar is created under **\out\artifacts**.</span></span>
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a><span data-ttu-id="988b6-190">Executar o aplicativo hello no cluster do Spark Olá</span><span class="sxs-lookup"><span data-stu-id="988b6-190">Run hello application on hello Spark cluster</span></span>
<span data-ttu-id="988b6-191">aplicativo de hello toorun no cluster hello, você deve fazer a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="988b6-191">toorun hello application on hello cluster, you must do hello following:</span></span>

* <span data-ttu-id="988b6-192">**Blob de armazenamento do Azure cópia Olá aplicativo jar toohello** associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="988b6-192">**Copy hello application jar toohello Azure storage blob** associated with hello cluster.</span></span> <span data-ttu-id="988b6-193">Você pode usar [ **AzCopy**](../storage/common/storage-use-azcopy.md), um comando de linha utilitário, toodo assim.</span><span class="sxs-lookup"><span data-stu-id="988b6-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="988b6-194">Há muitos outros clientes assim que você pode usar dados tooupload.</span><span class="sxs-lookup"><span data-stu-id="988b6-194">There are a lot of other clients as well that you can use tooupload data.</span></span> <span data-ttu-id="988b6-195">É possível saber mais sobre eles em [Carregar dados para trabalhos do Hadoop no HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="988b6-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="988b6-196">**Use Livy toosubmit um trabalho de aplicativo remotamente** toohello cluster do Spark.</span><span class="sxs-lookup"><span data-stu-id="988b6-196">**Use Livy toosubmit an application job remotely** toohello Spark cluster.</span></span> <span data-ttu-id="988b6-197">Clusters Spark no HDInsight inclui Livy que expõe os demais pontos de extremidade tooremotely enviar trabalhos Spark.</span><span class="sxs-lookup"><span data-stu-id="988b6-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints tooremotely submit Spark jobs.</span></span> <span data-ttu-id="988b6-198">Para obter mais informações, consulte [Enviar trabalhos do Spark remotamente usando Livy com clusters Spark no HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="988b6-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="988b6-199">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="988b6-199">Next step</span></span>

<span data-ttu-id="988b6-200">Neste artigo, você aprendeu como toocreate um aplicativo de scala Spark.</span><span class="sxs-lookup"><span data-stu-id="988b6-200">In this article you learned how toocreate a Spark scala application.</span></span> <span data-ttu-id="988b6-201">Adiantamento toohello próximo artigo toolearn como toorun este aplicativo em um HDInsight Spark cluster usando Livy.</span><span class="sxs-lookup"><span data-stu-id="988b6-201">Advance toohello next article toolearn how toorun this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="988b6-202">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="988b6-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

