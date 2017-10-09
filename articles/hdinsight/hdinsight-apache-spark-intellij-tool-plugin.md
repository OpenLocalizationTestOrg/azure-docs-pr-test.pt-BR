---
title: 'Kit de Ferramentas do Azure para IntelliJ: criar aplicativos Spark para um cluster HDInsight | Microsoft Docs'
description: "Use Olá Kit de ferramentas do Azure para os aplicativos IntelliJ toodevelop Spark escritos em Scala e enviá-los tooan cluster HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="0a993-103">Use o Kit de ferramentas do Azure para aplicativos de Spark toocreate IntelliJ para um cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a993-103">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="0a993-104">Use Olá Kit de ferramentas do Azure para aplicativos de Spark toodevelop plug-in IntelliJ escritos em Scala e, em seguida, enviá-los tooan cluster HDInsight Spark diretamente do ambiente de desenvolvimento integrado Olá IntelliJ (IDE).</span><span class="sxs-lookup"><span data-stu-id="0a993-104">Use hello Azure Toolkit for IntelliJ plug-in toodevelop Spark applications written in Scala, and then submit them tooan HDInsight Spark cluster directly from hello IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="0a993-105">Você pode usar o plug-in de algumas maneiras de saudação:</span><span class="sxs-lookup"><span data-stu-id="0a993-105">You can use hello plug-in in a few ways:</span></span>

* <span data-ttu-id="0a993-106">Desenvolver e enviar um aplicativo Scala Spark em um cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="0a993-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="0a993-107">Acessar os recursos de cluster Spark do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0a993-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="0a993-108">Desenvolver e executar um aplicativo Scala Spark localmente.</span><span class="sxs-lookup"><span data-stu-id="0a993-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="0a993-109">toocreate seu projeto, a saudação de exibição [criar aplicativos de Spark com hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) vídeo.</span><span class="sxs-lookup"><span data-stu-id="0a993-109">toocreate your project, view hello [Create Spark Applications with hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a993-110">Você pode usar esse plug-in toocreate e enviar aplicativos apenas para um cluster HDInsight Spark no Linux.</span><span class="sxs-lookup"><span data-stu-id="0a993-110">You can use this plug-in toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="0a993-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0a993-111">Prerequisites</span></span>

- <span data-ttu-id="0a993-112">Um cluster do Apache Spark no HDInsight no Linux.</span><span class="sxs-lookup"><span data-stu-id="0a993-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="0a993-113">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="0a993-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="0a993-114">Kit de desenvolvimento Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="0a993-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="0a993-115">Você pode instalá-lo de saudação [site Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="0a993-115">You can install it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="0a993-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="0a993-116">IntelliJ IDEA.</span></span> <span data-ttu-id="0a993-117">Este artigo usa a versão 2017.1.</span><span class="sxs-lookup"><span data-stu-id="0a993-117">This article uses version 2017.1.</span></span> <span data-ttu-id="0a993-118">Você pode instalá-lo de saudação [JetBrains site](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="0a993-118">You can install it from hello [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="0a993-119">Instalar Kit de Ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0a993-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="0a993-120">Para obter instruções de instalação, confira [Instalação do Kit de Ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="0a993-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="0a993-121">Entrar tooyour assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="0a993-121">Sign in tooyour Azure subscription</span></span>

1. <span data-ttu-id="0a993-122">Inicie Olá IntelliJ IDE e abra o Gerenciador do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a993-122">Start hello IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="0a993-123">Em Olá **exibição** menu, selecione **janelas de ferramentas**e, em seguida, selecione **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="0a993-123">On hello **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![link do Hello Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="0a993-125">Saudação de atalho **Azure** nó e selecione **entrar**.</span><span class="sxs-lookup"><span data-stu-id="0a993-125">Right-click hello **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="0a993-126">Em Olá **Azure entrar** caixa de diálogo, selecione **entrar**e, em seguida, insira suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a993-126">In hello **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Hello Azure caixa de diálogo Conecte](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="0a993-128">Depois que você está conectado, Olá **selecione assinaturas** Olá a caixa de diálogo lista todos os Olá assinaturas do Azure que são associadas com as credenciais.</span><span class="sxs-lookup"><span data-stu-id="0a993-128">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions that are associated with hello credentials.</span></span> <span data-ttu-id="0a993-129">Selecione Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="0a993-129">Select hello **Select** button.</span></span>

    ![caixa de diálogo Selecionar assinaturas Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="0a993-131">Em Olá **Azure Explorer** guia, expanda **HDInsight** Olá tooview HDInsight Spark clusters que estão em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="0a993-131">On hello **Azure Explorer** tab, expand **HDInsight** tooview hello HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Clusters Spark do HDInsight no Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="0a993-133">tooview Olá recursos (por exemplo, contas de armazenamento) que estão associados com cluster hello, você pode expandir ainda mais um nó do nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="0a993-133">tooview hello resources (for example, storage accounts) that are associated with hello cluster, you can further expand a cluster-name node.</span></span>
   
    ![Um nó de nome de cluster expandido](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="0a993-135">Executar um aplicativo Scala Spark em um cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="0a993-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="0a993-136">Inicie o IDEA do IntelliJ e crie um projeto.</span><span class="sxs-lookup"><span data-stu-id="0a993-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="0a993-137">Em Olá **novo projeto** caixa de diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a993-137">In hello **New Project** dialog box, do hello following:</span></span> 

   <span data-ttu-id="0a993-138">a.</span><span class="sxs-lookup"><span data-stu-id="0a993-138">a.</span></span> <span data-ttu-id="0a993-139">Selecione **HDInsight** > **Spark no HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="0a993-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="0a993-140">b.</span><span class="sxs-lookup"><span data-stu-id="0a993-140">b.</span></span> <span data-ttu-id="0a993-141">Em Olá **ferramenta de compilação** , selecione qualquer uma das Olá a seguir, de acordo com a necessidade de tooyour:</span><span class="sxs-lookup"><span data-stu-id="0a993-141">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="0a993-142">**Maven**, para obter suporte ao assistente de criação de projetos Scala</span><span class="sxs-lookup"><span data-stu-id="0a993-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="0a993-143">**SBT**, para gerenciar dependências hello e criação de projeto de Scala Olá</span><span class="sxs-lookup"><span data-stu-id="0a993-143">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![caixa de diálogo Novo projeto Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="0a993-145">Selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="0a993-145">Select **Next**.</span></span>

3. <span data-ttu-id="0a993-146">Assistente de criação do projeto Scala Olá detecta automaticamente se você instalou Olá Scala plug-in.</span><span class="sxs-lookup"><span data-stu-id="0a993-146">hello Scala project-creation wizard automatically detects whether you've installed hello Scala plug-in.</span></span> <span data-ttu-id="0a993-147">Selecione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="0a993-147">Select **Install**.</span></span>

   ![Verificação do plug-in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="0a993-149">Olá toodownload Scala plug-in, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="0a993-149">toodownload hello Scala plug-in, select **OK**.</span></span> <span data-ttu-id="0a993-150">Siga as instruções de saudação toorestart IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0a993-150">Follow hello instructions toorestart IntelliJ.</span></span> 

   ![caixa de diálogo Instalação do plug-in de Scala Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="0a993-152">Em Olá **novo projeto** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a993-152">In hello **New Project** window, do hello following:</span></span>  

    ![Selecionando Olá Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="0a993-154">a.</span><span class="sxs-lookup"><span data-stu-id="0a993-154">a.</span></span> <span data-ttu-id="0a993-155">Insira um nome e o local do projeto.</span><span class="sxs-lookup"><span data-stu-id="0a993-155">Enter a project name and location.</span></span>

   <span data-ttu-id="0a993-156">b.</span><span class="sxs-lookup"><span data-stu-id="0a993-156">b.</span></span> <span data-ttu-id="0a993-157">Em Olá **projeto SDK** lista suspensa, selecione **Java 1.8** para cluster de 2. x Spark hello, ou selecione **Java 1.7** para cluster 1. x do hello Spark.</span><span class="sxs-lookup"><span data-stu-id="0a993-157">In hello **Project SDK** drop-down list, select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span>

   <span data-ttu-id="0a993-158">c.</span><span class="sxs-lookup"><span data-stu-id="0a993-158">c.</span></span> <span data-ttu-id="0a993-159">Em Olá **versão Spark** lista suspensa, o Assistente de criação de projeto Scala se integra a versão correta do Olá para Spark SDK e Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="0a993-159">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="0a993-160">Se a versão do cluster Spark Olá for anterior à 2.0, selecione **despertar 1. x**.</span><span class="sxs-lookup"><span data-stu-id="0a993-160">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="0a993-161">Caso contrário, selecione **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="0a993-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="0a993-162">Esse exemplo usa o **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="0a993-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="0a993-163">Selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="0a993-163">Select **Finish**.</span></span>

7. <span data-ttu-id="0a993-164">projeto do Spark Olá cria automaticamente um artefato para você.</span><span class="sxs-lookup"><span data-stu-id="0a993-164">hello Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="0a993-165">artefato de saudação tooview, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a993-165">tooview hello artifact, do hello following:</span></span>

   <span data-ttu-id="0a993-166">a.</span><span class="sxs-lookup"><span data-stu-id="0a993-166">a.</span></span> <span data-ttu-id="0a993-167">Em Olá **arquivo** menu, selecione **estrutura do projeto**.</span><span class="sxs-lookup"><span data-stu-id="0a993-167">On hello **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="0a993-168">b.</span><span class="sxs-lookup"><span data-stu-id="0a993-168">b.</span></span> <span data-ttu-id="0a993-169">Em Olá **estrutura do projeto** caixa de diálogo, selecione **artefatos** tooview artefato de padrão de saudação que é criado.</span><span class="sxs-lookup"><span data-stu-id="0a993-169">In hello **Project Structure** dialog box, select **Artifacts** tooview hello default artifact that is created.</span></span> <span data-ttu-id="0a993-170">Você também pode criar seu próprios artefato selecionando o sinal de adição hello (**+**).</span><span class="sxs-lookup"><span data-stu-id="0a993-170">You can also create your own artifact by selecting hello plus sign (**+**).</span></span>

      ![Informações de artefato na caixa de diálogo Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="0a993-172">Adicione seu código-fonte aplicativo hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="0a993-172">Add your application source code by doing hello following:</span></span>

   <span data-ttu-id="0a993-173">a.</span><span class="sxs-lookup"><span data-stu-id="0a993-173">a.</span></span> <span data-ttu-id="0a993-174">No Explorador de projeto, clique com botão direito **src**, ponto muito**novo**e, em seguida, selecione **Scala classe**.</span><span class="sxs-lookup"><span data-stu-id="0a993-174">In Project Explorer, right-click **src**, point too**New**, and then select **Scala Class**.</span></span>
      
      ![Comandos para criar uma classe Scala do Explorador do Projeto](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="0a993-176">b.</span><span class="sxs-lookup"><span data-stu-id="0a993-176">b.</span></span> <span data-ttu-id="0a993-177">Em Olá **criar nova classe Scala** caixa de diálogo caixa, forneça um nome, selecione **objeto** em Olá **tipo** caixa e, em seguida, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="0a993-177">In hello **Create New Scala Class** dialog box, provide a name, select **Object** in hello **Kind** box, and then select **OK**.</span></span>
      
      ![Criar caixa de diálogo Nova Classe Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="0a993-179">c.</span><span class="sxs-lookup"><span data-stu-id="0a993-179">c.</span></span> <span data-ttu-id="0a993-180">Em Olá **MyClusterApp.scala** de arquivos, cole Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="0a993-180">In hello **MyClusterApp.scala** file, paste hello following code.</span></span> <span data-ttu-id="0a993-181">Olá código lê os dados de saudação do HVAC.csv (disponível em todos os clusters de HDInsight Spark), recupera linhas de saudação que têm apenas um dígito na coluna de sétimo Olá no arquivo CSV de saudação e grava a saída de hello muito**/HVACOut** em padrão Olá contêiner de armazenamento de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0a993-181">hello code reads hello data from HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that have only one digit in hello seventh column in hello CSV file, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="0a993-182">Execute o aplicativo hello em um cluster HDInsight Spark fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="0a993-182">Run hello application on an HDInsight Spark cluster by doing hello following:</span></span>

   <span data-ttu-id="0a993-183">a.</span><span class="sxs-lookup"><span data-stu-id="0a993-183">a.</span></span> <span data-ttu-id="0a993-184">No Explorador de projeto, nome do projeto hello e, em seguida, selecione **tooHDInsight enviar Spark aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="0a993-184">In Project Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>
      
      ![saudação de comando do aplicativo do Spark enviar tooHDInsight](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="0a993-186">b.</span><span class="sxs-lookup"><span data-stu-id="0a993-186">b.</span></span> <span data-ttu-id="0a993-187">Você está tooenter solicitada as credenciais de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a993-187">You are prompted tooenter your Azure subscription credentials.</span></span> <span data-ttu-id="0a993-188">Em Olá **envio Spark** caixa de diálogo, forneça Olá valores a seguir e, em seguida, selecione **enviar**.</span><span class="sxs-lookup"><span data-stu-id="0a993-188">In hello **Spark Submission** dialog box, provide hello following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="0a993-189">Para **despertar clusters (Linux)**, selecione o aplicativo de cluster HDInsight Spark no qual você deseja toorun hello.</span><span class="sxs-lookup"><span data-stu-id="0a993-189">For **Spark clusters (Linux only)**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>

      * <span data-ttu-id="0a993-190">Selecione um artefato do projeto de IntelliJ hello, ou selecione um na unidade de disco rígido hello.</span><span class="sxs-lookup"><span data-stu-id="0a993-190">Select an artifact from hello IntelliJ project, or select one from hello hard drive.</span></span>

      * <span data-ttu-id="0a993-191">Em Olá **nome da classe principal** caixa reticências Olá select (**...** ), selecione a classe principal da saudação no código fonte do aplicativo e, em seguida, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="0a993-191">In hello **Main class name** box, select hello ellipsis (**...**), select hello main class in your application source code, and then select **OK**.</span></span>

        ![caixa de diálogo Selecionar classe do principal Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="0a993-193">Porque o código do aplicativo hello neste exemplo não exigem argumentos de linha de comando ou referência JARs ou arquivos, você pode deixar Olá restantes caixas vazias.</span><span class="sxs-lookup"><span data-stu-id="0a993-193">Because hello application code in this example does not require command-line arguments or reference JARs or files, you can leave hello remaining boxes empty.</span></span> <span data-ttu-id="0a993-194">Depois de fornecer todas as informações de hello, caixa de diálogo Olá deve se assemelhar Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="0a993-194">After you provide all hello information, hello dialog box should resemble hello following image.</span></span>
        
        ![caixa de diálogo de envio Spark Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="0a993-196">c.</span><span class="sxs-lookup"><span data-stu-id="0a993-196">c.</span></span> <span data-ttu-id="0a993-197">Olá **envio Spark** guia na parte inferior da saudação da janela Olá deve iniciar exibindo andamento hello.</span><span class="sxs-lookup"><span data-stu-id="0a993-197">hello **Spark Submission** tab at hello bottom of hello window should start displaying hello progress.</span></span> <span data-ttu-id="0a993-198">Você também pode interromper o aplicativo hello, selecionando o botão Olá vermelho no hello **envio Spark** janela.</span><span class="sxs-lookup"><span data-stu-id="0a993-198">You can also stop hello application by selecting hello red button in hello **Spark Submission** window.</span></span>
      
      ![janela de envio Spark Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="0a993-200">toolearn como tooaccess Olá saída de trabalho, consulte hello "acesso e gerenciar clusters de HDInsight Spark usando o Kit de ferramentas do Azure para IntelliJ" seção mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="0a993-200">toolearn how tooaccess hello job output, see hello "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="0a993-201">Executar ou depurar um aplicativo Scala Spark em um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a993-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="0a993-202">Também é recomendável outra maneira de envio de cluster de toohello de aplicativo hello Spark.</span><span class="sxs-lookup"><span data-stu-id="0a993-202">We also recommend another way of submitting hello Spark application toohello cluster.</span></span> <span data-ttu-id="0a993-203">Você pode fazer isso definindo parâmetros de saudação no hello **configurações de execução/depuração** IDE.</span><span class="sxs-lookup"><span data-stu-id="0a993-203">You can do so by setting hello parameters in hello **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="0a993-204">Para saber mais, confira [Depurar aplicativos Spark remotamente em um cluster HDInsight com o kit de ferramentas do Azure para IntelliJ por meio do SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="0a993-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="0a993-205">Acessar e gerenciar clusters Spark do HDInsight usando o Kit de Ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0a993-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="0a993-206">Você pode executar várias operações usando o Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0a993-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="0a993-207">Modo de exibição de trabalho do Access Olá</span><span class="sxs-lookup"><span data-stu-id="0a993-207">Access hello job view</span></span>
1. <span data-ttu-id="0a993-208">No Pesquisador de objetos do Azure, expanda **HDInsight**, expanda o nome do cluster Spark hello e, em seguida, selecione **trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="0a993-208">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then select **Jobs**.</span></span>  

    ![Nó de exibição de trabalho](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="0a993-210">No painel direito da saudação, Olá **Spark trabalho exibição** guia exibe todos os aplicativos de saudação que foram executados no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a993-210">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="0a993-211">Selecione o nome de saudação do aplicativo hello para o qual você deseja toosee obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="0a993-211">Select hello name of hello application for which you want toosee more details.</span></span>

    ![Detalhes do aplicativo](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="0a993-213">toodisplay executando trabalho informações básicas, passe o mouse sobre o gráfico de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="0a993-213">toodisplay basic running job information, hover over hello job graph.</span></span> <span data-ttu-id="0a993-214">gráfico de estágios de saudação tooview e informações que gera todos os trabalhos, selecione um nó no gráfico de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="0a993-214">tooview hello stages graph and information that every job generates, select a node on hello job graph.</span></span>

    ![Detalhes do estágio do trabalho](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="0a993-216">tooview os logs, usados com frequência, como *Driver Stderr*, *Driver Stdout*, e *informações do diretório*, selecione Olá **Log** guia.</span><span class="sxs-lookup"><span data-stu-id="0a993-216">tooview frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select hello **Log** tab.</span></span>

    ![Detalhes do log](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="0a993-218">Você também pode exibir hello histórico Spark da interface do usuário e Olá YARN da interface do usuário (em nível de aplicativo hello) selecionando um link na parte superior de saudação da janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a993-218">You can also view hello Spark history UI and hello YARN UI (at hello application level) by selecting a link at hello top of hello window.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="0a993-219">Servidor de histórico do acesso Olá Spark</span><span class="sxs-lookup"><span data-stu-id="0a993-219">Access hello Spark history server</span></span>
1. <span data-ttu-id="0a993-220">No Azure Explorer, expanda o **HDInsight**, clique com o botão direito do mouse no nome do cluster Spark e selecione **Abrir IU do Histórico Spark**.</span><span class="sxs-lookup"><span data-stu-id="0a993-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="0a993-221">Quando você for solicitado, insira as credenciais de administrador do cluster hello, que você especificou ao configurar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a993-221">When you're prompted, enter hello cluster's admin credentials, which you specified when you set up hello cluster.</span></span>

3. <span data-ttu-id="0a993-222">No painel de servidor do histórico do Spark hello, você pode usar Olá toolook de nome de aplicativo para o aplicativo hello que você acabou de execução.</span><span class="sxs-lookup"><span data-stu-id="0a993-222">On hello Spark history server dashboard, you can use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="0a993-223">Em Olá precede o código, você definir nome do aplicativo hello usando `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="0a993-223">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="0a993-224">Portanto, o nome do aplicativo Spark é **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="0a993-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="0a993-225">Iniciar o portal do Ambari Olá</span><span class="sxs-lookup"><span data-stu-id="0a993-225">Start hello Ambari portal</span></span>
1. <span data-ttu-id="0a993-226">No Azure Explorer, expanda **HDInsight**, clique com o botão direito do mouse no nome do cluster Spark e selecione **Abrir Portal de Gerenciamento do Cluster (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="0a993-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="0a993-227">Quando você for solicitado, insira as credenciais de administrador de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0a993-227">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="0a993-228">Você especificou essas credenciais durante o processo de instalação de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0a993-228">You specified these credentials during hello cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="0a993-229">Gerenciar assinaturas do Azure</span><span class="sxs-lookup"><span data-stu-id="0a993-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="0a993-230">Por padrão, o Kit de ferramentas do Azure para IntelliJ lista clusters do Spark saudação de todas as suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a993-230">By default, Azure Toolkit for IntelliJ lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="0a993-231">Se necessário, você pode especificar que você deseja tooaccess de assinaturas de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a993-231">If necessary, you can specify hello subscriptions that you want tooaccess.</span></span> 

1. <span data-ttu-id="0a993-232">No Pesquisador de objetos do Azure, clique com botão direito Olá **Azure** nó raiz e, em seguida, selecione **gerenciar assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="0a993-232">In Azure Explorer, right-click hello **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="0a993-233">Na caixa de diálogo hello, desmarque Olá caixas de seleção próxima toohello assinaturas que não deseja tooaccess e, em seguida, selecione **fechar**.</span><span class="sxs-lookup"><span data-stu-id="0a993-233">In hello dialog box, clear hello check boxes next toohello subscriptions that you don't want tooaccess, and then select **Close**.</span></span> <span data-ttu-id="0a993-234">Você também pode selecionar **sair** se deseja toosign fora de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a993-234">You can also select **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="0a993-235">Executar um aplicativo Scala Spark localmente</span><span class="sxs-lookup"><span data-stu-id="0a993-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="0a993-236">Você pode usar o Kit de ferramentas do Azure para IntelliJ toorun Spark Scala aplicativos localmente em sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0a993-236">You can use Azure Toolkit for IntelliJ toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="0a993-237">Olá aplicativos geralmente não precisam acessar toocluster recursos, como contêineres de armazenamento, e você pode executar e testá-las localmente.</span><span class="sxs-lookup"><span data-stu-id="0a993-237">hello applications usually don't need access toocluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="0a993-238">Pré-requisito</span><span class="sxs-lookup"><span data-stu-id="0a993-238">Prerequisite</span></span>
<span data-ttu-id="0a993-239">Durante a execução do aplicativo do Olá local Spark Scala em um computador Windows, você pode obter uma exceção, conforme explicado em [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="0a993-239">While you're running hello local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="0a993-240">ocorrerá uma exceção de saudação porque WinUtils.exe está ausente no Windows.</span><span class="sxs-lookup"><span data-stu-id="0a993-240">hello exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="0a993-241">tooresolve esse erro, [baixar Olá executável](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa local como **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="0a993-241">tooresolve this error, [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="0a993-242">Em seguida, adicione a variável de ambiente Olá **HADOOP_HOME**e defina o valor de saudação da variável de saudação muito**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="0a993-242">Then, add hello environment variable **HADOOP_HOME**, and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="0a993-243">Executar um aplicativo Scala Spark local</span><span class="sxs-lookup"><span data-stu-id="0a993-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="0a993-244">Inicie o IDEA do IntelliJ e crie um projeto.</span><span class="sxs-lookup"><span data-stu-id="0a993-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="0a993-245">Em Olá **novo projeto** caixa de diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a993-245">In hello **New Project** dialog box, do hello following:</span></span>
   
    <span data-ttu-id="0a993-246">a.</span><span class="sxs-lookup"><span data-stu-id="0a993-246">a.</span></span> <span data-ttu-id="0a993-247">Escolha **HDInsight** > **Exemplo de Execução Local do Spark no HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="0a993-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="0a993-248">b.</span><span class="sxs-lookup"><span data-stu-id="0a993-248">b.</span></span> <span data-ttu-id="0a993-249">Em Olá **ferramenta de compilação** , selecione qualquer uma das Olá a seguir, de acordo com a necessidade de tooyour:</span><span class="sxs-lookup"><span data-stu-id="0a993-249">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="0a993-250">**Maven**, para obter suporte ao assistente de criação de projetos Scala</span><span class="sxs-lookup"><span data-stu-id="0a993-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="0a993-251">**SBT**, para gerenciar dependências hello e criação de projeto de Scala Olá</span><span class="sxs-lookup"><span data-stu-id="0a993-251">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![caixa de diálogo Novo projeto Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="0a993-253">Selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="0a993-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="0a993-254">Na próxima janela de hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a993-254">In hello next window, do hello following:</span></span>
   
    <span data-ttu-id="0a993-255">a.</span><span class="sxs-lookup"><span data-stu-id="0a993-255">a.</span></span> <span data-ttu-id="0a993-256">Insira um nome e o local do projeto.</span><span class="sxs-lookup"><span data-stu-id="0a993-256">Enter a project name and location.</span></span>

    <span data-ttu-id="0a993-257">b.</span><span class="sxs-lookup"><span data-stu-id="0a993-257">b.</span></span> <span data-ttu-id="0a993-258">Em Olá **projeto SDK** lista suspensa, selecione uma versão de Java é posterior à versão 1.7.</span><span class="sxs-lookup"><span data-stu-id="0a993-258">In hello **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="0a993-259">c.</span><span class="sxs-lookup"><span data-stu-id="0a993-259">c.</span></span> <span data-ttu-id="0a993-260">Em Olá **versão Spark** lista suspensa, versão select Olá de Scala que você deseja toouse: Scala 2.11.x Spark 2.0 ou Scala 2.10.x para Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="0a993-260">In hello **Spark Version** drop-down list, select hello version of Scala that you want toouse: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![caixa de diálogo Novo projeto Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="0a993-262">Selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="0a993-262">Select **Finish**.</span></span>

6. <span data-ttu-id="0a993-263">modelo de saudação adiciona um código de exemplo (**LogQuery**) em Olá **src** pasta pode ser executada localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="0a993-263">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![Local do LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="0a993-265">Saudação de atalho **LogQuery** aplicativo e, em seguida, selecione **execução 'LogQuery'**.</span><span class="sxs-lookup"><span data-stu-id="0a993-265">Right-click hello **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="0a993-266">Em Olá **executar** guia na parte inferior do hello, verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="0a993-266">On hello **Run** tab at hello bottom, you see an output like hello following:</span></span>
   
   ![Resultado da execução local do aplicativo Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a><span data-ttu-id="0a993-268">Converter toouse de aplicativos existente IDEIA IntelliJ Kit de ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0a993-268">Convert existing IntelliJ IDEA applications toouse Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="0a993-269">Você pode converter Olá Spark Scala os aplicativos existentes que você criou no IntelliJ IDEIA toobe compatível com o Kit de ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0a993-269">You can convert hello existing Spark Scala applications that you created in IntelliJ IDEA toobe compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="0a993-270">Você pode usar Olá toosubmit plug-in Olá aplicativos tooan cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="0a993-270">You can then use hello plug-in toosubmit hello applications tooan HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="0a993-271">Para um aplicativo Spark Scala existente que foi criado por meio de IntelliJ IDEIA, abra o arquivo de .iml associados de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a993-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open hello associated .iml file.</span></span>

2. <span data-ttu-id="0a993-272">Na raiz da saudação nível é um **módulo** elemento como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a993-272">At hello root level is a **module** element like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="0a993-273">Editar saudação elemento tooadd `UniqueKey="HDInsightTool"` assim que Olá **módulo** elemento semelhante ao seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="0a993-273">Edit hello element tooadd `UniqueKey="HDInsightTool"` so that hello **module** element looks like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="0a993-274">Salve alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a993-274">Save hello changes.</span></span> <span data-ttu-id="0a993-275">Seu aplicativo deve ser compatível com o Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0a993-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="0a993-276">Você pode testá-lo clicando com o nome do projeto Olá no Explorador de projeto.</span><span class="sxs-lookup"><span data-stu-id="0a993-276">You can test it by right-clicking hello project name in Project Explorer.</span></span> <span data-ttu-id="0a993-277">menu pop-up Olá agora tem a opção de saudação **tooHDInsight enviar Spark aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="0a993-277">hello pop-up menu now has hello option **Submit Spark Application tooHDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0a993-278">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="0a993-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="0a993-279">Erro na execução local: *Use um tamanho de heap maior*</span><span class="sxs-lookup"><span data-stu-id="0a993-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="0a993-280">Spark 1.6, se você estiver usando um SDK de Java de 32 bits durante a execução local, você pode encontrar hello os erros a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a993-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter hello following errors:</span></span>

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

<span data-ttu-id="0a993-281">Esses erros ocorrem porque o tamanho do heap Olá não é grande o suficiente para toorun Spark.</span><span class="sxs-lookup"><span data-stu-id="0a993-281">These errors happen because hello heap size is not large enough for Spark toorun.</span></span> <span data-ttu-id="0a993-282">O Spark requer pelo menos 471 MB.</span><span class="sxs-lookup"><span data-stu-id="0a993-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="0a993-283">(Para saber mais, confira [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) Uma solução simple é toouse um SDK de Java de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="0a993-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is toouse a 64-bit Java SDK.</span></span> <span data-ttu-id="0a993-284">Você também pode alterar configurações da JVM Olá IntelliJ adicionando Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a993-284">You can also change hello JVM settings in IntelliJ by adding hello following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Adicionando opções toohello "Opções de VM" caixa IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="0a993-286">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="0a993-286">FAQ</span></span>
<span data-ttu-id="0a993-287">toosubmit um repositório do aplicativo tooAzure Data Lake, escolha **interativo** modo durante o processo de saudação entrada do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a993-287">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="0a993-288">Se você selecionar o modo **Automatizado**, obterá um erro.</span><span class="sxs-lookup"><span data-stu-id="0a993-288">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="0a993-290">Isso já está resolvido.</span><span class="sxs-lookup"><span data-stu-id="0a993-290">Now, we resolved it.</span></span> <span data-ttu-id="0a993-291">Você pode escolher um Cluster do Azure Data Lake toosubmit seu aplicativo com qualquer método de entrada.</span><span class="sxs-lookup"><span data-stu-id="0a993-291">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="0a993-292">Comentários e problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0a993-292">Feedback and known issues</span></span>
<span data-ttu-id="0a993-293">Atualmente, não há suporte para exibir saídas do Spark diretamente.</span><span class="sxs-lookup"><span data-stu-id="0a993-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="0a993-294">Se você tiver sugestões ou comentários, ou se encontrar problemas ao usar esse plug-in, envie-nos um email para hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="0a993-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="0a993-295"><a name="seealso"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a993-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="0a993-296">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a993-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="0a993-297">Demonstração</span><span class="sxs-lookup"><span data-stu-id="0a993-297">Demo</span></span>
* <span data-ttu-id="0a993-298">Criar projeto do Scala (vídeo): [Criar aplicativos Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="0a993-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="0a993-299">Depuração remota (vídeo): [Kit de ferramentas do uso do Azure para aplicativos de Spark toodebug IntelliJ remotamente no HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="0a993-299">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="0a993-300">Cenários</span><span class="sxs-lookup"><span data-stu-id="0a993-300">Scenarios</span></span>
* [<span data-ttu-id="0a993-301">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="0a993-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="0a993-302">Spark com o aprendizado de máquina: Use o Spark no HDInsight tooanalyze criação temperatura usando dados HVAC</span><span class="sxs-lookup"><span data-stu-id="0a993-302">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="0a993-303">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="0a993-303">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="0a993-304">Streaming Spark: Use Spark no HDInsight toobuild aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="0a993-304">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="0a993-305">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a993-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="0a993-306">Criando e executando aplicativos</span><span class="sxs-lookup"><span data-stu-id="0a993-306">Creating and running applications</span></span>
* [<span data-ttu-id="0a993-307">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="0a993-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="0a993-308">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="0a993-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="0a993-309">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="0a993-309">Tools and extensions</span></span>
* [<span data-ttu-id="0a993-310">Use o Kit de ferramentas do Azure para aplicativos de Spark toodebug IntelliJ remotamente por meio de VPN</span><span class="sxs-lookup"><span data-stu-id="0a993-310">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="0a993-311">Use o Kit de ferramentas do Azure para aplicativos de Spark toodebug IntelliJ remotamente por meio do SSH</span><span class="sxs-lookup"><span data-stu-id="0a993-311">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="0a993-312">Usar ferramentas do HDInsight para IntelliJ com a área restrita do Hortonworks</span><span class="sxs-lookup"><span data-stu-id="0a993-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="0a993-313">Use as ferramentas do HDInsight no Kit de ferramentas do Azure para aplicativos do Eclipse toocreate Spark</span><span class="sxs-lookup"><span data-stu-id="0a993-313">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="0a993-314">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a993-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="0a993-315">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a993-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="0a993-316">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="0a993-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="0a993-317">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="0a993-317">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="0a993-318">Gerenciando recursos</span><span class="sxs-lookup"><span data-stu-id="0a993-318">Managing resources</span></span>
* [<span data-ttu-id="0a993-319">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="0a993-319">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="0a993-320">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a993-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

