---
title: 'Kit de Ferramentas do Azure para IntelliJ: criar aplicativos Spark para um cluster HDInsight | Microsoft Docs'
description: "Use o Kit de Ferramentas do Azure para IntelliJ a fim de desenvolver aplicativos Spark escritos em Scala e enviá-los a um cluster Spark do HDInsight."
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
ms.openlocfilehash: 19cb8f436fa4d86f323013a5d4b3b50bf6c80a1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="f065f-103">Usar o Kit de Ferramentas do Azure para IntelliJ a fim de criar aplicativos Spark para um cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="f065f-103">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="f065f-104">Use o plug-in Kit de Ferramentas do Azure para IntelliJ a fim de desenvolver aplicativos Spark escritos em Scala e enviá-los a um cluster Spark do HDInsight diretamente do IDE (ambiente de desenvolvimento integrado) do IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="f065f-104">Use the Azure Toolkit for IntelliJ plug-in to develop Spark applications written in Scala, and then submit them to an HDInsight Spark cluster directly from the IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="f065f-105">Você pode usar o plug-in destas maneiras:</span><span class="sxs-lookup"><span data-stu-id="f065f-105">You can use the plug-in in a few ways:</span></span>

* <span data-ttu-id="f065f-106">Desenvolver e enviar um aplicativo Scala Spark em um cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f065f-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="f065f-107">Acessar os recursos de cluster Spark do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f065f-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="f065f-108">Desenvolver e executar um aplicativo Scala Spark localmente.</span><span class="sxs-lookup"><span data-stu-id="f065f-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="f065f-109">Para criar seu projeto, veja o vídeo [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (Criar aplicativos Spark com o Kit de Ferramentas do Azure para IntelliJ).</span><span class="sxs-lookup"><span data-stu-id="f065f-109">To create your project, view the [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f065f-110">Você pode usar esse plug-in e enviar aplicativos somente para um cluster Spark do HDInsight no Linux.</span><span class="sxs-lookup"><span data-stu-id="f065f-110">You can use this plug-in to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="f065f-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f065f-111">Prerequisites</span></span>

- <span data-ttu-id="f065f-112">Um cluster do Apache Spark no HDInsight no Linux.</span><span class="sxs-lookup"><span data-stu-id="f065f-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="f065f-113">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f065f-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="f065f-114">Kit de desenvolvimento Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="f065f-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="f065f-115">Você pode instalá-lo do [site da Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="f065f-115">You can install it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="f065f-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="f065f-116">IntelliJ IDEA.</span></span> <span data-ttu-id="f065f-117">Este artigo usa a versão 2017.1.</span><span class="sxs-lookup"><span data-stu-id="f065f-117">This article uses version 2017.1.</span></span> <span data-ttu-id="f065f-118">Você pode instalá-lo do [site da JetBrains](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="f065f-118">You can install it from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="f065f-119">Instalar Kit de Ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="f065f-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="f065f-120">Para obter instruções de instalação, confira [Instalação do Kit de Ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="f065f-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="f065f-121">Entre em sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="f065f-121">Sign in to your Azure subscription</span></span>

1. <span data-ttu-id="f065f-122">Inicie o IDE do IntelliJ e abra o Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="f065f-122">Start the IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="f065f-123">No menu **Exibir**, selecione **Janelas de Ferramentas** e **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f065f-123">On the **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![O link do Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="f065f-125">Clique com o botão direito do mouse no nó **Azure** e selecione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f065f-125">Right-click the **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="f065f-126">Na caixa de diálogo **Entrada do Azure**, selecione **Entrar** e insira suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="f065f-126">In the **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![A caixa de diálogo Entrada do Azure](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="f065f-128">Depois que você estiver conectado, a caixa de diálogo **Selecionar Assinaturas** listará todas as assinaturas do Azure associadas às credenciais.</span><span class="sxs-lookup"><span data-stu-id="f065f-128">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions that are associated with the credentials.</span></span> <span data-ttu-id="f065f-129">Escolha o botão **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="f065f-129">Select the **Select** button.</span></span>

    ![A caixa de diálogo Selecionar Assinaturas](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="f065f-131">Na guia **Azure Explorer**, expanda **HDInsight** para ver os clusters Spark do HDInsight em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="f065f-131">On the **Azure Explorer** tab, expand **HDInsight** to view the HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Clusters Spark do HDInsight no Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="f065f-133">Para exibir os recursos (por exemplo, contas de armazenamento) associados ao cluster, você poderá expandir ainda mais um nó de nome de cluster.</span><span class="sxs-lookup"><span data-stu-id="f065f-133">To view the resources (for example, storage accounts) that are associated with the cluster, you can further expand a cluster-name node.</span></span>
   
    ![Um nó de nome de cluster expandido](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="f065f-135">Executar um aplicativo Scala Spark em um cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="f065f-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="f065f-136">Inicie o IDEA do IntelliJ e crie um projeto.</span><span class="sxs-lookup"><span data-stu-id="f065f-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="f065f-137">Na caixa de diálogo **Novo Projeto** , faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f065f-137">In the **New Project** dialog box, do the following:</span></span> 

   <span data-ttu-id="f065f-138">a.</span><span class="sxs-lookup"><span data-stu-id="f065f-138">a.</span></span> <span data-ttu-id="f065f-139">Selecione **HDInsight** > **Spark no HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="f065f-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="f065f-140">b.</span><span class="sxs-lookup"><span data-stu-id="f065f-140">b.</span></span> <span data-ttu-id="f065f-141">Na lista **Ferramenta de build**, selecione uma das seguintes opções, de acordo com suas necessidades:</span><span class="sxs-lookup"><span data-stu-id="f065f-141">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="f065f-142">**Maven**, para obter suporte ao assistente de criação de projetos Scala</span><span class="sxs-lookup"><span data-stu-id="f065f-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="f065f-143">**SBT**, para gerenciar as dependências e a compilação no projeto Scala</span><span class="sxs-lookup"><span data-stu-id="f065f-143">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![A caixa de diálogo Novo Projeto](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="f065f-145">Selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f065f-145">Select **Next**.</span></span>

3. <span data-ttu-id="f065f-146">O assistente de criação de projetos Scala detecta automaticamente se você instalou o plug-in Scala.</span><span class="sxs-lookup"><span data-stu-id="f065f-146">The Scala project-creation wizard automatically detects whether you've installed the Scala plug-in.</span></span> <span data-ttu-id="f065f-147">Selecione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="f065f-147">Select **Install**.</span></span>

   ![Verificação do plug-in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="f065f-149">Para baixar o plug-in Scala, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="f065f-149">To download the Scala plug-in, select **OK**.</span></span> <span data-ttu-id="f065f-150">Siga as instruções para reiniciar o IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="f065f-150">Follow the instructions to restart IntelliJ.</span></span> 

   ![A caixa de diálogo Instalação do plug-in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="f065f-152">Na janela **Novo Projeto**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f065f-152">In the **New Project** window, do the following:</span></span>  

    ![Selecionando o SDK do Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="f065f-154">a.</span><span class="sxs-lookup"><span data-stu-id="f065f-154">a.</span></span> <span data-ttu-id="f065f-155">Insira um nome e o local do projeto.</span><span class="sxs-lookup"><span data-stu-id="f065f-155">Enter a project name and location.</span></span>

   <span data-ttu-id="f065f-156">b.</span><span class="sxs-lookup"><span data-stu-id="f065f-156">b.</span></span> <span data-ttu-id="f065f-157">Na lista suspensa **SDK do Projeto**, selecione **Java 1.8** para o cluster Spark 2.x ou selecione **Java 1.7** para o cluster Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="f065f-157">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span>

   <span data-ttu-id="f065f-158">c.</span><span class="sxs-lookup"><span data-stu-id="f065f-158">c.</span></span> <span data-ttu-id="f065f-159">Na lista suspensa **Versão do Spark**, o assistente de criação de projeto Scala integra a versão apropriada do SDK do Spark e do SDK do Scala.</span><span class="sxs-lookup"><span data-stu-id="f065f-159">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="f065f-160">Se a versão do cluster do Spark for inferior a 2.0, selecione **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="f065f-160">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="f065f-161">Caso contrário, selecione **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="f065f-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="f065f-162">Esse exemplo usa o **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="f065f-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="f065f-163">Selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="f065f-163">Select **Finish**.</span></span>

7. <span data-ttu-id="f065f-164">O projeto do Spark cria automaticamente um artefato para você.</span><span class="sxs-lookup"><span data-stu-id="f065f-164">The Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="f065f-165">Para exibir o artefato, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f065f-165">To view the artifact, do the following:</span></span>

   <span data-ttu-id="f065f-166">a.</span><span class="sxs-lookup"><span data-stu-id="f065f-166">a.</span></span> <span data-ttu-id="f065f-167">No menu **Arquivo**, escolha **Estrutura do Projeto**.</span><span class="sxs-lookup"><span data-stu-id="f065f-167">On the **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="f065f-168">b.</span><span class="sxs-lookup"><span data-stu-id="f065f-168">b.</span></span> <span data-ttu-id="f065f-169">Na caixa de diálogo **Estrutura do Projeto**, clique em **Artefatos** para exibir o artefato padrão criado.</span><span class="sxs-lookup"><span data-stu-id="f065f-169">In the **Project Structure** dialog box, select **Artifacts** to view the default artifact that is created.</span></span> <span data-ttu-id="f065f-170">Você também pode criar seu próprio artefato selecionando o sinal de mais (**+**).</span><span class="sxs-lookup"><span data-stu-id="f065f-170">You can also create your own artifact by selecting the plus sign (**+**).</span></span>

      ![Informações de artefato na caixa de diálogo](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="f065f-172">Adicione o código-fonte do aplicativo seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="f065f-172">Add your application source code by doing the following:</span></span>

   <span data-ttu-id="f065f-173">a.</span><span class="sxs-lookup"><span data-stu-id="f065f-173">a.</span></span> <span data-ttu-id="f065f-174">No Gerenciador de Projetos, clique com o botão direito do mouse em **src**, aponte para **Novo** e escolha **Classe do Scala**.</span><span class="sxs-lookup"><span data-stu-id="f065f-174">In Project Explorer, right-click **src**, point to **New**, and then select **Scala Class**.</span></span>
      
      ![Comandos para criar uma classe Scala do Explorador do Projeto](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="f065f-176">b.</span><span class="sxs-lookup"><span data-stu-id="f065f-176">b.</span></span> <span data-ttu-id="f065f-177">Na caixa de diálogo **Criar Nova Classe do Scala**, forneça um nome, selecione **Objeto** na caixa **Tipo** e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="f065f-177">In the **Create New Scala Class** dialog box, provide a name, select **Object** in the **Kind** box, and then select **OK**.</span></span>
      
      ![Criar caixa de diálogo Nova Classe Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="f065f-179">c.</span><span class="sxs-lookup"><span data-stu-id="f065f-179">c.</span></span> <span data-ttu-id="f065f-180">No arquivo **MyClusterApp.scala** , cole o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="f065f-180">In the **MyClusterApp.scala** file, paste the following code.</span></span> <span data-ttu-id="f065f-181">O código lê os dados no HVAC.csv (disponível em todos os clusters Spark do HDInsight), recupera as linhas com apenas um dígito na sétima coluna no arquivo CSV e grava a saída em **/HVACOut** no contêiner padrão de armazenamento do cluster.</span><span class="sxs-lookup"><span data-stu-id="f065f-181">The code reads the data from HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that have only one digit in the seventh column in the CSV file, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find the rows that have only one digit in the seventh column in the CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="f065f-182">Execute o aplicativo em um cluster Spark do HDInsight seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="f065f-182">Run the application on an HDInsight Spark cluster by doing the following:</span></span>

   <span data-ttu-id="f065f-183">a.</span><span class="sxs-lookup"><span data-stu-id="f065f-183">a.</span></span> <span data-ttu-id="f065f-184">No Explorador de Projetos, clique com o botão direito do mouse no nome do projeto e selecione **Enviar Aplicativo Spark para HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f065f-184">In Project Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>
      
      ![O comando Enviar Aplicativo Spark para HDInsight](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="f065f-186">b.</span><span class="sxs-lookup"><span data-stu-id="f065f-186">b.</span></span> <span data-ttu-id="f065f-187">Você recebe uma solicitação para inserir suas credenciais de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f065f-187">You are prompted to enter your Azure subscription credentials.</span></span> <span data-ttu-id="f065f-188">Na caixa de diálogo **Envio do Spark**, forneça os valores a seguir e escolha **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="f065f-188">In the **Spark Submission** dialog box, provide the following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="f065f-189">Para **clusters Spark (somente no Linux)**, selecione o cluster HDInsight Spark no qual você deseja executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f065f-189">For **Spark clusters (Linux only)**, select the HDInsight Spark cluster on which you want to run your application.</span></span>

      * <span data-ttu-id="f065f-190">Selecione um artefato do projeto IntelliJ ou uma opção do disco rígido.</span><span class="sxs-lookup"><span data-stu-id="f065f-190">Select an artifact from the IntelliJ project, or select one from the hard drive.</span></span>

      * <span data-ttu-id="f065f-191">Na caixa **Nome da classe principal**, escolha o botão de reticências (**...** ), selecione a classe principal no código-fonte do aplicativo e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="f065f-191">In the **Main class name** box, select the ellipsis (**...**), select the main class in your application source code, and then select **OK**.</span></span>

        ![A caixa de diálogo Selecionar Classe Principal](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="f065f-193">Como o código do aplicativo neste exemplo não exige argumentos de linha de comando nem JARs ou arquivos de referência, você pode deixar as caixas restantes em branco.</span><span class="sxs-lookup"><span data-stu-id="f065f-193">Because the application code in this example does not require command-line arguments or reference JARs or files, you can leave the remaining boxes empty.</span></span> <span data-ttu-id="f065f-194">Depois de fornecer todas as informações, a caixa de diálogo deve ser semelhante à imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="f065f-194">After you provide all the information, the dialog box should resemble the following image.</span></span>
        
        ![A caixa de diálogo Envio do Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="f065f-196">c.</span><span class="sxs-lookup"><span data-stu-id="f065f-196">c.</span></span> <span data-ttu-id="f065f-197">A guia **Envio do Spark** na parte inferior da janela deve começar a exibir o progresso.</span><span class="sxs-lookup"><span data-stu-id="f065f-197">The **Spark Submission** tab at the bottom of the window should start displaying the progress.</span></span> <span data-ttu-id="f065f-198">Você também pode interromper o aplicativo escolhendo o botão vermelho na janela **Envio do Spark**.</span><span class="sxs-lookup"><span data-stu-id="f065f-198">You can also stop the application by selecting the red button in the **Spark Submission** window.</span></span>
      
      ![A janela Envio do Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="f065f-200">Para saber como acessar a saída do trabalho, confira a seção "Acessar e gerenciar clusters Spark do HDInsight usando o Kit de Ferramentas do Azure para IntelliJ" mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f065f-200">To learn how to access the job output, see the "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="f065f-201">Executar ou depurar um aplicativo Scala Spark em um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="f065f-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="f065f-202">Também recomendamos outra forma de enviar o aplicativo Spark ao cluster.</span><span class="sxs-lookup"><span data-stu-id="f065f-202">We also recommend another way of submitting the Spark application to the cluster.</span></span> <span data-ttu-id="f065f-203">Você pode fazer isso definido os parâmetros no IDE **Executar/Depurar configurações**.</span><span class="sxs-lookup"><span data-stu-id="f065f-203">You can do so by setting the parameters in the **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="f065f-204">Para saber mais, confira [Depurar aplicativos Spark remotamente em um cluster HDInsight com o kit de ferramentas do Azure para IntelliJ por meio do SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="f065f-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="f065f-205">Acessar e gerenciar clusters Spark do HDInsight usando o Kit de Ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="f065f-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="f065f-206">Você pode executar várias operações usando o Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="f065f-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="f065f-207">Acessar a exibição do trabalho</span><span class="sxs-lookup"><span data-stu-id="f065f-207">Access the job view</span></span>
1. <span data-ttu-id="f065f-208">No Azure Explorer, expanda **HDInsight**, expanda o nome do cluster Spark e escolha **Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="f065f-208">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then select **Jobs**.</span></span>  

    ![Nó de exibição de trabalho](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="f065f-210">No painel direito, a guia **Exibição de Trabalho do Spark** exibe todos os aplicativos que foram executados no cluster.</span><span class="sxs-lookup"><span data-stu-id="f065f-210">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="f065f-211">Selecione o nome do aplicativo do qual você deseja ver mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="f065f-211">Select the name of the application for which you want to see more details.</span></span>

    ![Detalhes do aplicativo](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="f065f-213">Para exibir informações básicas do trabalho em execução, passe o mouse sobre o gráfico de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="f065f-213">To display basic running job information, hover over the job graph.</span></span> <span data-ttu-id="f065f-214">Para exibir o gráfico de estágios e as informações geradas pelos trabalhos, escolha um nó no gráfico de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="f065f-214">To view the stages graph and information that every job generates, select a node on the job graph.</span></span>

    ![Detalhes do estágio do trabalho](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="f065f-216">Para exibir logs usados frequentemente, como *Stderr do Driver*, *Stdout do Driver* e *Informações do diretório*, escolha a guia **Log**.</span><span class="sxs-lookup"><span data-stu-id="f065f-216">To view frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select the **Log** tab.</span></span>

    ![Detalhes do log](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="f065f-218">Você também pode exibir a interface do usuário de histórico do Spark e a interface do usuário do YARN (no nível do aplicativo) selecionando um link na parte superior da janela.</span><span class="sxs-lookup"><span data-stu-id="f065f-218">You can also view the Spark history UI and the YARN UI (at the application level) by selecting a link at the top of the window.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="f065f-219">Acessar o servidor de histórico do Spark</span><span class="sxs-lookup"><span data-stu-id="f065f-219">Access the Spark history server</span></span>
1. <span data-ttu-id="f065f-220">No Azure Explorer, expanda o **HDInsight**, clique com o botão direito do mouse no nome do cluster Spark e selecione **Abrir IU do Histórico Spark**.</span><span class="sxs-lookup"><span data-stu-id="f065f-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="f065f-221">Quando for solicitado, insira as credenciais do administrador do cluster, que você especificou ao configurar o cluster.</span><span class="sxs-lookup"><span data-stu-id="f065f-221">When you're prompted, enter the cluster's admin credentials, which you specified when you set up the cluster.</span></span>

3. <span data-ttu-id="f065f-222">No painel do servidor de histórico do Spark, é possível usar o nome do aplicativo para procurar o que você acabou de executar.</span><span class="sxs-lookup"><span data-stu-id="f065f-222">On the Spark history server dashboard, you can use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="f065f-223">No código anterior, você definiu o nome do aplicativo usando `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="f065f-223">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="f065f-224">Portanto, o nome do aplicativo Spark é **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="f065f-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="f065f-225">Iniciar o portal do Ambari</span><span class="sxs-lookup"><span data-stu-id="f065f-225">Start the Ambari portal</span></span>
1. <span data-ttu-id="f065f-226">No Azure Explorer, expanda **HDInsight**, clique com o botão direito do mouse no nome do cluster Spark e selecione **Abrir Portal de Gerenciamento do Cluster (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="f065f-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="f065f-227">Quando solicitado, insira as credenciais de administrador para o cluster.</span><span class="sxs-lookup"><span data-stu-id="f065f-227">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="f065f-228">Você especificou essas credenciais durante o processo de configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="f065f-228">You specified these credentials during the cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="f065f-229">Gerenciar assinaturas do Azure</span><span class="sxs-lookup"><span data-stu-id="f065f-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="f065f-230">Por padrão, o Kit de Ferramentas do Azure para IntelliJ listam os clusters Spark de todas as suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="f065f-230">By default, Azure Toolkit for IntelliJ lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="f065f-231">Se for necessário, você poderá especificar as assinaturas que deseja acessar.</span><span class="sxs-lookup"><span data-stu-id="f065f-231">If necessary, you can specify the subscriptions that you want to access.</span></span> 

1. <span data-ttu-id="f065f-232">No Azure Explorer, clique com o botão direito do mouse no nó-raiz **Azure** e selecione **Gerenciar Assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="f065f-232">In Azure Explorer, right-click the **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="f065f-233">Na caixa de diálogo, desmarque as caixas de seleção ao lado das assinaturas que você não deseja acessar e escolha **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="f065f-233">In the dialog box, clear the check boxes next to the subscriptions that you don't want to access, and then select **Close**.</span></span> <span data-ttu-id="f065f-234">Você também poderá escolher **Sair** se quiser sair da sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f065f-234">You can also select **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="f065f-235">Executar um aplicativo Scala Spark localmente</span><span class="sxs-lookup"><span data-stu-id="f065f-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="f065f-236">Você pode usar o Kit de Ferramentas do Azure para IntelliJ para executar aplicativos Spark Scala localmente em sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f065f-236">You can use Azure Toolkit for IntelliJ to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="f065f-237">Normalmente, os aplicativos não precisam acessar recursos de cluster, como contêineres de armazenamento, e você pode executá-los e testá-los localmente.</span><span class="sxs-lookup"><span data-stu-id="f065f-237">The applications usually don't need access to cluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="f065f-238">Pré-requisito</span><span class="sxs-lookup"><span data-stu-id="f065f-238">Prerequisite</span></span>
<span data-ttu-id="f065f-239">Durante a execução do aplicativo Scala Spark local em um computador Windows, você pode receber uma exceção, conforme explicado em [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="f065f-239">While you're running the local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="f065f-240">A exceção ocorre porque WinUtils.exe está ausente no Windows.</span><span class="sxs-lookup"><span data-stu-id="f065f-240">The exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="f065f-241">Para resolver esse erro, [baixe o executável](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) em um local como **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="f065f-241">To resolve this error, [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="f065f-242">Em seguida, adicione uma variável de ambiente **HADOOP_HOME** e defina o valor da variável para **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="f065f-242">Then, add the environment variable **HADOOP_HOME**, and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="f065f-243">Executar um aplicativo Scala Spark local</span><span class="sxs-lookup"><span data-stu-id="f065f-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="f065f-244">Inicie o IDEA do IntelliJ e crie um projeto.</span><span class="sxs-lookup"><span data-stu-id="f065f-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="f065f-245">Na caixa de diálogo **Novo Projeto** , faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f065f-245">In the **New Project** dialog box, do the following:</span></span>
   
    <span data-ttu-id="f065f-246">a.</span><span class="sxs-lookup"><span data-stu-id="f065f-246">a.</span></span> <span data-ttu-id="f065f-247">Escolha **HDInsight** > **Exemplo de Execução Local do Spark no HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="f065f-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="f065f-248">b.</span><span class="sxs-lookup"><span data-stu-id="f065f-248">b.</span></span> <span data-ttu-id="f065f-249">Na lista **Ferramenta de build**, selecione uma das seguintes opções, de acordo com suas necessidades:</span><span class="sxs-lookup"><span data-stu-id="f065f-249">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="f065f-250">**Maven**, para obter suporte ao assistente de criação de projetos Scala</span><span class="sxs-lookup"><span data-stu-id="f065f-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="f065f-251">**SBT**, para gerenciar as dependências e a compilação no projeto Scala</span><span class="sxs-lookup"><span data-stu-id="f065f-251">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![A caixa de diálogo Novo Projeto](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="f065f-253">Selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f065f-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="f065f-254">Na próxima janela, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f065f-254">In the next window, do the following:</span></span>
   
    <span data-ttu-id="f065f-255">a.</span><span class="sxs-lookup"><span data-stu-id="f065f-255">a.</span></span> <span data-ttu-id="f065f-256">Insira um nome e o local do projeto.</span><span class="sxs-lookup"><span data-stu-id="f065f-256">Enter a project name and location.</span></span>

    <span data-ttu-id="f065f-257">b.</span><span class="sxs-lookup"><span data-stu-id="f065f-257">b.</span></span> <span data-ttu-id="f065f-258">Na lista suspensa **SDK do Projeto**, escolha uma versão do Java que seja posterior à versão 1.7.</span><span class="sxs-lookup"><span data-stu-id="f065f-258">In the **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="f065f-259">c.</span><span class="sxs-lookup"><span data-stu-id="f065f-259">c.</span></span> <span data-ttu-id="f065f-260">Na lista suspensa **Versão do Spark**, escolha a versão do Scala que você deseja usar: Scala 2.11.x para Spark 2.0 ou Scala 2.10.x para Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="f065f-260">In the **Spark Version** drop-down list, select the version of Scala that you want to use: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![A caixa de diálogo Novo Projeto](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="f065f-262">Selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="f065f-262">Select **Finish**.</span></span>

6. <span data-ttu-id="f065f-263">O modelo adiciona um código de exemplo (**LogQuery**) na pasta **src** que pode ser executada localmente em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f065f-263">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![Local do LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="f065f-265">Clique com o botão direito do mouse no aplicativo **LogQuery** e escolha **Executar 'LogQuery'**.</span><span class="sxs-lookup"><span data-stu-id="f065f-265">Right-click the **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="f065f-266">Na guia **Executar** na parte inferior, você verá uma saída como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="f065f-266">On the **Run** tab at the bottom, you see an output like the following:</span></span>
   
   ![Resultado da execução local do aplicativo Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-to-use-azure-toolkit-for-intellij"></a><span data-ttu-id="f065f-268">Converter aplicativos IntelliJ IDEA existentes a fim de usar o Kit de Ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="f065f-268">Convert existing IntelliJ IDEA applications to use Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="f065f-269">Você pode converter os aplicativos Scala Spark existentes criados no IDEA do IntelliJ para serem compatíveis com o Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="f065f-269">You can convert the existing Spark Scala applications that you created in IntelliJ IDEA to be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="f065f-270">Em seguida, você pode usar o plug-in para enviar os aplicativos a um cluster Spark do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f065f-270">You can then use the plug-in to submit the applications to an HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="f065f-271">Para um aplicativo Scala Spark existente criado no IDEA do IntelliJ, abra o arquivo .iml associado.</span><span class="sxs-lookup"><span data-stu-id="f065f-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open the associated .iml file.</span></span>

2. <span data-ttu-id="f065f-272">Há um elemento **module** no nível de raiz, como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f065f-272">At the root level is a **module** element like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="f065f-273">Edite o elemento para adicionar `UniqueKey="HDInsightTool"` , de modo que o elemento **module** seja semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f065f-273">Edit the element to add `UniqueKey="HDInsightTool"` so that the **module** element looks like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="f065f-274">Salve as alterações.</span><span class="sxs-lookup"><span data-stu-id="f065f-274">Save the changes.</span></span> <span data-ttu-id="f065f-275">Seu aplicativo deve ser compatível com o Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="f065f-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="f065f-276">Você pode testar isso clicando com o botão direito do mouse no nome do projeto no Gerenciador de Projetos.</span><span class="sxs-lookup"><span data-stu-id="f065f-276">You can test it by right-clicking the project name in Project Explorer.</span></span> <span data-ttu-id="f065f-277">Agora, o menu pop-up tem a opção **Enviar Aplicativo Spark ao HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f065f-277">The pop-up menu now has the option **Submit Spark Application to HDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f065f-278">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="f065f-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="f065f-279">Erro na execução local: *Use um tamanho de heap maior*</span><span class="sxs-lookup"><span data-stu-id="f065f-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="f065f-280">No Spark 1.6, se você estiver usando um SDK Java de 32 bits durante a execução local, poderá encontrar os seguintes erros:</span><span class="sxs-lookup"><span data-stu-id="f065f-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter the following errors:</span></span>

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

<span data-ttu-id="f065f-281">Esses erros acontecem porque o tamanho do heap não é grande o suficiente para Spark ser executado.</span><span class="sxs-lookup"><span data-stu-id="f065f-281">These errors happen because the heap size is not large enough for Spark to run.</span></span> <span data-ttu-id="f065f-282">O Spark requer pelo menos 471 MB.</span><span class="sxs-lookup"><span data-stu-id="f065f-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="f065f-283">(Para saber mais, confira [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) Uma solução simples é usar um SDK do Java de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="f065f-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is to use a 64-bit Java SDK.</span></span> <span data-ttu-id="f065f-284">Você também pode alterar as configurações da JVM no IntelliJ adicionando as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="f065f-284">You can also change the JVM settings in IntelliJ by adding the following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Adicionando opções à caixa "Opções de VM" no IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="f065f-286">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="f065f-286">FAQ</span></span>
<span data-ttu-id="f065f-287">Para enviar um aplicativo ao Azure Data Lake Store, escolha o modo **Interativo** durante o processo de entrada no Azure.</span><span class="sxs-lookup"><span data-stu-id="f065f-287">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="f065f-288">Se você selecionar o modo **Automatizado**, obterá um erro.</span><span class="sxs-lookup"><span data-stu-id="f065f-288">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="f065f-290">Isso já está resolvido.</span><span class="sxs-lookup"><span data-stu-id="f065f-290">Now, we resolved it.</span></span> <span data-ttu-id="f065f-291">Você pode escolher um Cluster do Azure Data Lake para enviar seu aplicativo com qualquer método de entrada.</span><span class="sxs-lookup"><span data-stu-id="f065f-291">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="f065f-292">Comentários e problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="f065f-292">Feedback and known issues</span></span>
<span data-ttu-id="f065f-293">Atualmente, não há suporte para exibir saídas do Spark diretamente.</span><span class="sxs-lookup"><span data-stu-id="f065f-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="f065f-294">Se você tiver sugestões ou comentários, ou se encontrar problemas ao usar esse plug-in, envie-nos um email para hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="f065f-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="f065f-295"><a name="seealso"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f065f-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="f065f-296">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f065f-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="f065f-297">Demonstração</span><span class="sxs-lookup"><span data-stu-id="f065f-297">Demo</span></span>
* <span data-ttu-id="f065f-298">Criar projeto do Scala (vídeo): [Criar aplicativos Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f065f-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="f065f-299">Depuração remota (vídeo): [Usar o Kit de Ferramentas do Azure para IntelliJ para depurar aplicativos Spark remotamente no cluster HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f065f-299">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="f065f-300">Cenários</span><span class="sxs-lookup"><span data-stu-id="f065f-300">Scenarios</span></span>
* [<span data-ttu-id="f065f-301">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="f065f-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f065f-302">Spark com Machine Learning: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="f065f-302">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f065f-303">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para prever resultados da inspeção de alimentos</span><span class="sxs-lookup"><span data-stu-id="f065f-303">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f065f-304">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="f065f-304">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="f065f-305">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f065f-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="f065f-306">Criando e executando aplicativos</span><span class="sxs-lookup"><span data-stu-id="f065f-306">Creating and running applications</span></span>
* [<span data-ttu-id="f065f-307">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="f065f-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f065f-308">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="f065f-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f065f-309">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="f065f-309">Tools and extensions</span></span>
* [<span data-ttu-id="f065f-310">Usar o kit de ferramentas do Azure para IntelliJ a fim de depurar aplicativos Spark remotamente por meio da VPN</span><span class="sxs-lookup"><span data-stu-id="f065f-310">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f065f-311">Usar o kit de ferramentas do Azure para IntelliJ a fim de depurar aplicativos Spark remotamente por meio do SSH</span><span class="sxs-lookup"><span data-stu-id="f065f-311">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="f065f-312">Usar ferramentas do HDInsight para IntelliJ com a área restrita do Hortonworks</span><span class="sxs-lookup"><span data-stu-id="f065f-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="f065f-313">Usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para Eclipse para criar aplicativos Spark</span><span class="sxs-lookup"><span data-stu-id="f065f-313">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="f065f-314">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f065f-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f065f-315">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="f065f-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f065f-316">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="f065f-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="f065f-317">Instalar o Jupyter em seu computador e conectar-se a um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="f065f-317">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="f065f-318">Gerenciando recursos</span><span class="sxs-lookup"><span data-stu-id="f065f-318">Managing resources</span></span>
* [<span data-ttu-id="f065f-319">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f065f-319">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f065f-320">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f065f-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

