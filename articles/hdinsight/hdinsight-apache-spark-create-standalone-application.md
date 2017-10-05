---
title: "Criar aplicativos do Scala para execução em clusters do Spark – Azure HDInsight | Microsoft Docs"
description: "Crie um aplicativo do Spark escrito no Scala com o Apache Maven como o sistema de build e um arquétipo Maven existente para Scala fornecido pelo IntelliJ IDEA."
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
ms.openlocfilehash: 95dba08744357f8800b05e3d4b892e3a363d5985
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-scala-maven-application-to-run-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="053f1-103">Criar um aplicativo Maven Scala para execução no cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="053f1-103">Create a Scala Maven application to run on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="053f1-104">Saiba como criar um aplicativo Spark escrito em Scala usando o Maven com IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="053f1-104">Learn how to create a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="053f1-105">O artigo usa o Apache Maven como o sistema de build e começa com um arquétipo Maven existente para Scala fornecido pelo IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="053f1-105">The article uses Apache Maven as the build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="053f1-106">Criar um aplicativo Scala no IntelliJ IDEA envolve as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="053f1-106">Creating a Scala application in IntelliJ IDEA involves the following steps:</span></span>

* <span data-ttu-id="053f1-107">Usar o Maven como o sistema de compilação.</span><span class="sxs-lookup"><span data-stu-id="053f1-107">Use Maven as the build system.</span></span>
* <span data-ttu-id="053f1-108">Atualize o arquivo do POM (Modelo de Objeto do Projeto) para resolver as dependências do módulo Spark.</span><span class="sxs-lookup"><span data-stu-id="053f1-108">Update Project Object Model (POM) file to resolve Spark module dependencies.</span></span>
* <span data-ttu-id="053f1-109">Escreva seu aplicativo em Scala.</span><span class="sxs-lookup"><span data-stu-id="053f1-109">Write your application in Scala.</span></span>
* <span data-ttu-id="053f1-110">Gere um arquivo jar que pode ser enviado aos clusters HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="053f1-110">Generate a jar file that can be submitted to HDInsight Spark clusters.</span></span>
* <span data-ttu-id="053f1-111">Executar os aplicativos em um cluster do Spark usando Livy.</span><span class="sxs-lookup"><span data-stu-id="053f1-111">Run the application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="053f1-112">O HDInsight também fornece uma ferramenta de plug-in do IntelliJ IDEA para facilitar o processo de criação e envio de aplicativos para um cluster HDInsight Spark no Linux.</span><span class="sxs-lookup"><span data-stu-id="053f1-112">HDInsight also provides an IntelliJ IDEA plugin tool to ease the process of creating and submitting applications to an HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="053f1-113">Para obter mais informações, consulte [Usar o plug-in de Ferramentas do HDInsight para IntelliJ IDEA para criar e enviar aplicativos Spark](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="053f1-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="053f1-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="053f1-114">Prerequisites</span></span>

* <span data-ttu-id="053f1-115">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="053f1-115">An Azure subscription.</span></span> <span data-ttu-id="053f1-116">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="053f1-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="053f1-117">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="053f1-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="053f1-118">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="053f1-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="053f1-119">Kit de desenvolvimento Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="053f1-119">Oracle Java Development kit.</span></span> <span data-ttu-id="053f1-120">Você pode instalá-lo clicando [aqui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="053f1-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="053f1-121">Um Java IDE.</span><span class="sxs-lookup"><span data-stu-id="053f1-121">A Java IDE.</span></span> <span data-ttu-id="053f1-122">Este artigo usa IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="053f1-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="053f1-123">Você pode instalá-lo clicando [aqui](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="053f1-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="053f1-124">Instalar o plug-in Scala para IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="053f1-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="053f1-125">Se a instalação do IntelliJ IDEA não solicitar para habilitar o plug-in Scala, inicie IntelliJ IDEA e percorra as etapas a seguir para instalar o plug-in:</span><span class="sxs-lookup"><span data-stu-id="053f1-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through the following steps to install the plugin:</span></span>

1. <span data-ttu-id="053f1-126">Inicie o IntelliJ IDEA e, na tela de boas-vindas, clique em **Configurar** e, em seguida, clique em **Plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="053f1-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Habilitar plug-in do scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="053f1-128">Na próxima tela, clique em **Instalar o plugin JetBrains** no canto inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="053f1-128">In the next screen, click **Install JetBrains plugin** from the lower left corner.</span></span> <span data-ttu-id="053f1-129">Na caixa de diálogo **Procurar plug-ins da JetBrains** que é aberta, pesquise por Scala e, em seguida, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="053f1-129">In the **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Instalar o plug-in do scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="053f1-131">Depois que o plug-in for instalado com êxito, clique no **botão Reiniciar IntelliJ IDEA** para reiniciar o IDE.</span><span class="sxs-lookup"><span data-stu-id="053f1-131">After the plugin installs successfully, click the **Restart IntelliJ IDEA button** to restart the IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="053f1-132">Criar um projeto de Scala autônomo</span><span class="sxs-lookup"><span data-stu-id="053f1-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="053f1-133">Inicie o IntelliJ IDEA e crie um novo projeto.</span><span class="sxs-lookup"><span data-stu-id="053f1-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="053f1-134">Na caixa de diálogo Novo Projeto, faça o seguinte e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="053f1-134">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![Criar projeto Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="053f1-136">Selecione **Maven** como o tipo de projeto.</span><span class="sxs-lookup"><span data-stu-id="053f1-136">Select **Maven** as the project type.</span></span>
   * <span data-ttu-id="053f1-137">Especifique um **SDK do projeto**.</span><span class="sxs-lookup"><span data-stu-id="053f1-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="053f1-138">Clique em Novo e navegue até o diretório de instalação do Java, normalmente `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="053f1-138">Click New and navigate to the Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="053f1-139">Selecione a opção **Criar do Arquétipo** .</span><span class="sxs-lookup"><span data-stu-id="053f1-139">Select the **Create from archetype** option.</span></span>
   * <span data-ttu-id="053f1-140">Na lista de arquétipos, selecione **org.scala-tools.archetypes:scala-archetype-simple**.</span><span class="sxs-lookup"><span data-stu-id="053f1-140">From the list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="053f1-141">Isso criará a estrutura de diretório certa e baixará as dependências padrão necessárias para gravar o programa Scala.</span><span class="sxs-lookup"><span data-stu-id="053f1-141">This will create the right directory structure and download the required default dependencies to write Scala program.</span></span>
2. <span data-ttu-id="053f1-142">Forneça os valores relevantes para **GroupId**, **ArtifactId** e **versão**.</span><span class="sxs-lookup"><span data-stu-id="053f1-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="053f1-143">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="053f1-143">Click **Next**.</span></span>
3. <span data-ttu-id="053f1-144">Na caixa de diálogo seguinte, na qual você especificará o diretório inicial do Maven e outras configurações do usuário, aceite os padrões e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="053f1-144">In the next dialog box, where you specify Maven home directory and other user settings, accept the defaults and click **Next**.</span></span>
4. <span data-ttu-id="053f1-145">Na última caixa de diálogo, especifique um nome de projeto e local e, em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="053f1-145">In the last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="053f1-146">Exclua o arquivo **MySpec.Scala** em **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="053f1-146">Delete the **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="053f1-147">Você não precisa disso para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="053f1-147">You do not need this for the application.</span></span>
6. <span data-ttu-id="053f1-148">Se necessário, renomeie os arquivos de origem e de teste padrão.</span><span class="sxs-lookup"><span data-stu-id="053f1-148">If required, rename the default source and test files.</span></span> <span data-ttu-id="053f1-149">No painel à esquerda, no IntelliJ IDEA, navegue até **src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="053f1-149">From the left pane in the IntelliJ IDEA, navigate to **src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="053f1-150">Clique com botão direito do mouse em **App.scala**, clique em **Refatorar**, clique em Renomear Arquivo, forneça o novo nome para o aplicativo na caixa de diálogo e clique em **Refatorar**.</span><span class="sxs-lookup"><span data-stu-id="053f1-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in the dialog box, provide the new name for the application and then click **Refactor**.</span></span>
   
    ![Renomear arquivos](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="053f1-152">Nas etapas subsequentes, você irá atualizar o pom.xml para definir as dependências do aplicativo Spark Scala.</span><span class="sxs-lookup"><span data-stu-id="053f1-152">In the subsequent steps, you will update the pom.xml to define the dependencies for the Spark Scala application.</span></span> <span data-ttu-id="053f1-153">Para que essas dependências sejam baixadas e resolvidas automaticamente, você deve configurar o Maven adequadamente.</span><span class="sxs-lookup"><span data-stu-id="053f1-153">For those dependencies to be downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Configurar Maven para downloads automáticos](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="053f1-155">No menu **Arquivo**, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="053f1-155">From the **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="053f1-156">Na caixa de diálogo **Configurações**, navegue até **Build, Execução, Implantação** > **Ferramentas de Compilação** > **Maven** > **Importando**.</span><span class="sxs-lookup"><span data-stu-id="053f1-156">In the **Settings** dialog box, navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="053f1-157">Selecione a opção para **Importar projetos Maven automaticamente**.</span><span class="sxs-lookup"><span data-stu-id="053f1-157">Select the option to **Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="053f1-158">Clique em **Aplicar** e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="053f1-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="053f1-159">Atualize o arquivo de origem Scala para incluir o código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="053f1-159">Update the Scala source file to include your application code.</span></span> <span data-ttu-id="053f1-160">Abra e substitua o código de exemplo existente pelo código a seguir e salve as alterações.</span><span class="sxs-lookup"><span data-stu-id="053f1-160">Open and replace the existing sample code with the following code and save the changes.</span></span> <span data-ttu-id="053f1-161">Esse código lê os dados no HVAC.csv (disponível em todos os clusters Spark HDInsight), recupera as linhas com apenas um dígito na sexta coluna e grava a saída em **/HVACOut** no contêiner padrão de armazenamento do cluster.</span><span class="sxs-lookup"><span data-stu-id="053f1-161">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the sixth column, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO to wasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows which have only one digit in the 7th column in the CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="053f1-162">Atualize o pom.xml.</span><span class="sxs-lookup"><span data-stu-id="053f1-162">Update the pom.xml.</span></span>
   
   1. <span data-ttu-id="053f1-163">Dentro de `<project>\<properties>`, adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="053f1-163">Within `<project>\<properties>` add the following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="053f1-164">Dentro de `<project>\<dependencies>`, adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="053f1-164">Within `<project>\<dependencies>` add the following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="053f1-165">Salve as alterações a pom.xml.</span><span class="sxs-lookup"><span data-stu-id="053f1-165">Save changes to pom.xml.</span></span>
10. <span data-ttu-id="053f1-166">Crie o arquivo .jar.</span><span class="sxs-lookup"><span data-stu-id="053f1-166">Create the .jar file.</span></span> <span data-ttu-id="053f1-167">O IntelliJ IDEA permite a criação de JAR como um artefato de um projeto.</span><span class="sxs-lookup"><span data-stu-id="053f1-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="053f1-168">Execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="053f1-168">Perform the following steps.</span></span>
    
    1. <span data-ttu-id="053f1-169">No menu **Arquivo**, clique em **Estrutura do Projeto**.</span><span class="sxs-lookup"><span data-stu-id="053f1-169">From the **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="053f1-170">Na caixa de diálogo **Estrutura do Projeto**, clique em **Artefatos** e, em seguida, clique no sinal de mais.</span><span class="sxs-lookup"><span data-stu-id="053f1-170">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="053f1-171">Na caixa de diálogo pop-up, clique em **JAR** e, em seguida, clique em **Dos módulos com dependências**.</span><span class="sxs-lookup"><span data-stu-id="053f1-171">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="053f1-173">Na caixa de diálogo **Criar JAR de Módulos![, clique no botão de reticências (**reticências](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png)) em relação à **Classe Principal**.</span><span class="sxs-lookup"><span data-stu-id="053f1-173">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against the **Main Class**.</span></span>
    4. <span data-ttu-id="053f1-174">Na caixa de diálogo **Selecionar Classe Principal**, selecione a classe que é exibida por padrão e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="053f1-174">In the **Select Main Class** dialog box, select the class that appears by default and then click **OK**.</span></span>
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="053f1-176">Na caixa de diálogo **Criar JAR de Módulos**, certifique-se de que a opção **extrair para o JAR de destino** esteja selecionada e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="053f1-176">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="053f1-177">Isso cria um JAR único com todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="053f1-177">This creates a single JAR with all dependencies.</span></span>
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="053f1-179">A guia layout de saída lista todos os jars incluídos como parte do projeto Maven.</span><span class="sxs-lookup"><span data-stu-id="053f1-179">The output layout tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="053f1-180">Você pode selecionar e excluir aqueles dos quais o aplicativo Scala não tem qualquer dependência direta.</span><span class="sxs-lookup"><span data-stu-id="053f1-180">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="053f1-181">Para o aplicativo que estamos criando aqui, você pode remover tudo, exceto o último (**saída de compilação SparkSimpleApp**).</span><span class="sxs-lookup"><span data-stu-id="053f1-181">For the application we are creating here, you can remove all but the last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="053f1-182">Selecione os jars para excluir e, em seguida, clique no ícone **Excluir** .</span><span class="sxs-lookup"><span data-stu-id="053f1-182">Select the jars to delete and then click the **Delete** icon.</span></span>
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="053f1-184">Certifique-se de que a caixa **Compilar à criação** esteja marcada, o que garante que o jar seja criado sempre que o projeto for criado ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="053f1-184">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="053f1-185">Clique em **Aplicar** e em **OK**.</span><span class="sxs-lookup"><span data-stu-id="053f1-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="053f1-186">Na barra de menus, clique em **Compilar** e, em seguida, clique em **Criar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="053f1-186">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="053f1-187">Você também pode clicar em **Compilar Artefatos** para criar o jar.</span><span class="sxs-lookup"><span data-stu-id="053f1-187">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="053f1-188">O jar de saída é criado em **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="053f1-188">The output jar is created under **\out\artifacts**.</span></span>
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-the-application-on-the-spark-cluster"></a><span data-ttu-id="053f1-190">Executar o aplicativo no cluster do Spark</span><span class="sxs-lookup"><span data-stu-id="053f1-190">Run the application on the Spark cluster</span></span>
<span data-ttu-id="053f1-191">Para executar o aplicativo no cluster, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="053f1-191">To run the application on the cluster, you must do the following:</span></span>

* <span data-ttu-id="053f1-192">**Copie o jar do aplicativo para o blob de armazenamento do Azure** associado ao cluster.</span><span class="sxs-lookup"><span data-stu-id="053f1-192">**Copy the application jar to the Azure storage blob** associated with the cluster.</span></span> <span data-ttu-id="053f1-193">Você pode usar [**AzCopy**](../storage/common/storage-use-azcopy.md), um utilitário de linha de comando, para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="053f1-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="053f1-194">Há muitos outros clientes também que você pode usar para carregar dados.</span><span class="sxs-lookup"><span data-stu-id="053f1-194">There are a lot of other clients as well that you can use to upload data.</span></span> <span data-ttu-id="053f1-195">É possível saber mais sobre eles em [Carregar dados para trabalhos do Hadoop no HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="053f1-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="053f1-196">**Use Livy para enviar um trabalho de aplicativo remotamente** para o cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="053f1-196">**Use Livy to submit an application job remotely** to the Spark cluster.</span></span> <span data-ttu-id="053f1-197">Os clusters Spark no HDInsight incluem Livy, que expõe pontos de extremidade REST para enviar remotamente trabalhos do Spark.</span><span class="sxs-lookup"><span data-stu-id="053f1-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints to remotely submit Spark jobs.</span></span> <span data-ttu-id="053f1-198">Para obter mais informações, consulte [Enviar trabalhos do Spark remotamente usando Livy com clusters Spark no HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="053f1-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="053f1-199">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="053f1-199">Next step</span></span>

<span data-ttu-id="053f1-200">Neste artigo, você aprendeu como criar um aplicativo Spark Scala.</span><span class="sxs-lookup"><span data-stu-id="053f1-200">In this article you learned how to create a Spark scala application.</span></span> <span data-ttu-id="053f1-201">Avance para o próximo artigo para saber como executar esse aplicativo em um cluster do HDInsight Spark usando Livy.</span><span class="sxs-lookup"><span data-stu-id="053f1-201">Advance to the next article to learn how to run this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="053f1-202">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="053f1-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

