---
title: Kit de Ferramentas do Azure para Eclipse - Criar aplicativos Scala para Spark do HDInsight | Microsoft Docs
description: "Usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para Eclipse para desenvolver aplicativos Spark escritos em Scala e enviá-los para um cluster HDInsight Spark, diretamente do IDE Eclipse."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 4bcb1987a62c0b7f4965e6fd257315e820004238
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-eclipse-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="9f589-103">Usar o Kit de ferramentas do Azure para Eclipse a fim de criar aplicativos Spark para cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f589-103">Use Azure Toolkit for Eclipse to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="9f589-104">Usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para Eclipse para desenvolver aplicativos Spark escritos em Scala e enviá-los para um cluster Spark no Azure HDInsight, diretamente do IDE Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9f589-104">Use HDInsight Tools in Azure Toolkit for Eclipse to develop Spark applications written in Scala and submit them to an Azure HDInsight Spark cluster, directly from the Eclipse IDE.</span></span> <span data-ttu-id="9f589-105">Você pode usar o plug-in Ferramentas do HDInsight de algumas maneiras diferentes:</span><span class="sxs-lookup"><span data-stu-id="9f589-105">You can use the HDInsight Tools plug-in in a few different ways:</span></span>

* <span data-ttu-id="9f589-106">Para desenvolver e enviar um aplicativo Scala Spark em um cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="9f589-106">To develop and submit a Scala Spark application on an HDInsight Spark cluster</span></span>
* <span data-ttu-id="9f589-107">Para acessar os recursos de cluster do Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="9f589-107">To access your Azure HDInsight Spark cluster resources</span></span>
* <span data-ttu-id="9f589-108">Para desenvolver e executar um aplicativo Scala Spark localmente</span><span class="sxs-lookup"><span data-stu-id="9f589-108">To develop and run a Scala Spark application locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f589-109">Essa ferramenta pode ser usada para criar e enviar aplicativos apenas para um cluster HDInsight Spark no Linux.</span><span class="sxs-lookup"><span data-stu-id="9f589-109">This tool can be used to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9f589-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9f589-110">Prerequisites</span></span>

* <span data-ttu-id="9f589-111">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f589-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="9f589-112">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="9f589-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="9f589-113">Oracle Java Development Kit versão 8, que é usado para o tempo de execução do IDE do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9f589-113">Oracle Java Development Kit version 8, which is used for the Eclipse IDE runtime.</span></span> <span data-ttu-id="9f589-114">Você pode baixá-lo do [site da Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="9f589-114">You can download it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="9f589-115">Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="9f589-115">Eclipse IDE.</span></span> <span data-ttu-id="9f589-116">Este artigo usa o Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="9f589-116">This article uses Eclipse Neon.</span></span> <span data-ttu-id="9f589-117">Você pode instalá-lo do [site do Eclipse](https://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9f589-117">You can install it from the [Eclipse website](https://www.eclipse.org/downloads/).</span></span>   
* <span data-ttu-id="9f589-118">Spark SDK.</span><span class="sxs-lookup"><span data-stu-id="9f589-118">Spark SDK.</span></span> <span data-ttu-id="9f589-119">Você pode baixá-lo do [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="9f589-119">You can download it from [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span>


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a><span data-ttu-id="9f589-120">Instalar as ferramentas do HDInsight no Kit de ferramentas do Azure para Eclipse e Scala plug-in</span><span class="sxs-lookup"><span data-stu-id="9f589-120">Install HDInsight Tools in Azure Toolkit for Eclipse and Scala Plugin</span></span>
### <a name="install-hdinsight-tools"></a><span data-ttu-id="9f589-121">Instalar Ferramentas do HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f589-121">Install HDInsight Tools</span></span>
<span data-ttu-id="9f589-122">As Ferramentas do HDInsight para Eclipse estão disponíveis como parte do Kit de Ferramentas do Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9f589-122">HDInsight Tools for Eclipse is available as part of Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="9f589-123">Para obter instruções de instalação, consulte [Instalando o Kit de Ferramentas do Azure para Eclipse](../azure-toolkit-for-eclipse-installation.md).</span><span class="sxs-lookup"><span data-stu-id="9f589-123">For installation instructions, see [Installing Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse-installation.md).</span></span>
### <a name="install-scala-plugin"></a><span data-ttu-id="9f589-124">Instalar o plug-in de Scala</span><span class="sxs-lookup"><span data-stu-id="9f589-124">Install Scala Plugin</span></span>
<span data-ttu-id="9f589-125">Quando você abre o Intellij, a ferramentas do HDInsight automática detecta se você instalou Scala plug-in ou não.</span><span class="sxs-lookup"><span data-stu-id="9f589-125">When you open the Intellij, the HDInsight Tools auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="9f589-126">Clique em **Okey** para continuar e siga as instruções para instalar o Marketplace do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9f589-126">Click **OK** to continue and follow the instructions to install by the Eclipse Marketplace.</span></span>

 ![Plug-in Scala de instalação automática](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="9f589-128">Entre em sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="9f589-128">Sign in to your Azure subscription</span></span>
1. <span data-ttu-id="9f589-129">Inicie o IDE Eclipse e abra o Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="9f589-129">Start the Eclipse IDE and open Azure Explorer.</span></span> <span data-ttu-id="9f589-130">No menu **Janela**, clique em **Mostrar Exibição** e clique em **Outros**.</span><span class="sxs-lookup"><span data-stu-id="9f589-130">On the **Window** menu, click **Show View**, and then click **Other**.</span></span> <span data-ttu-id="9f589-131">Na caixa de diálogo que é aberta, expanda **Azure**, clique em **Azure Explorer** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f589-131">In the dialog box that opens, expand **Azure**, click **Azure Explorer**, and then click **OK**.</span></span>

    ![Caixa de Diálogo Mostrar Modo de Exibição](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. <span data-ttu-id="9f589-133">Clique com o botão direito do mouse no nó **Azure** e clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="9f589-133">Right-click the **Azure** node, and then click **Sign in**.</span></span>
3. <span data-ttu-id="9f589-134">Na caixa de diálogo **Entrada do Azure**, escolha o modo de autenticação, clique em **Entrar** e insira suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f589-134">In the **Azure Sign In** dialog box, choose the authentication method, click **Sign in**, and enter your Azure credentials.</span></span>
   
    ![Caixa de diálogo Entrar no Azure](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. <span data-ttu-id="9f589-136">Após a entrada, a caixa de diálogo **Selecionar Assinaturas** listará todas as assinaturas do Azure associadas às credenciais.</span><span class="sxs-lookup"><span data-stu-id="9f589-136">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions associated with the credentials.</span></span> <span data-ttu-id="9f589-137">Clique em **Selecionar** para fechar a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f589-137">Click **Select** to close the dialog box.</span></span>

    ![Caixa de diálogo Selecionar Assinaturas](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. <span data-ttu-id="9f589-139">Na guia **Azure Explorer**, expanda **HDInsight** para ver os clusters Spark do HDInsight da sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="9f589-139">On the **Azure Explorer** tab, expand **HDInsight** to see the HDInsight Spark clusters under your subscription.</span></span>
   
    ![Clusters Spark do HDInsight no Azure Explorer](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. <span data-ttu-id="9f589-141">Além disso, você pode expandir um nó de nome de cluster para ver os recursos (por exemplo, contas de armazenamento) associados ao cluster.</span><span class="sxs-lookup"><span data-stu-id="9f589-141">You can further expand a cluster name node to see the resources (for example, storage accounts) associated with the cluster.</span></span>
   
    ![Expandindo um nome de cluster para ver recursos](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="9f589-143">Configurar um projeto Spark Scala para um cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="9f589-143">Set up a Spark Scala project for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="9f589-144">No espaço de trabalho do Eclipse IDE, clique em **Arquivo**, clique em **Novo** e, em seguida, clique em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="9f589-144">In the Eclipse IDE workspace, click **File**, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="9f589-145">No assistente Novo Projeto, expanda **HDInsight**, selecione **Spark no HDInsight (Scala)** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9f589-145">In the New Project wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then click **Next**.</span></span>

    ![Selecionando o projeto Spark no HDInsight (Scala)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. <span data-ttu-id="9f589-147">O assistente de criação de projetos Scala detecta automaticamente se você instalou o plug-in Scala ou não.</span><span class="sxs-lookup"><span data-stu-id="9f589-147">The Scala project creation wizard auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="9f589-148">Clique em **Okey** para continuar a baixar o plug-in Scala, siga as instruções para reiniciar o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9f589-148">Click **OK** to continue downloading the Scala plugin, then follow the instructions to restart Eclipse.</span></span>

    ![verificação do Scala](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. <span data-ttu-id="9f589-150">Na caixa de diálogo **Novo Projeto de Scala HDInsight**, forneça os seguintes valores e clique em **Avançar**:</span><span class="sxs-lookup"><span data-stu-id="9f589-150">In the **New HDInsight Scala Project** dialog box, provide the following values, and then click **Next**:</span></span>
   * <span data-ttu-id="9f589-151">Insira um nome para o projeto.</span><span class="sxs-lookup"><span data-stu-id="9f589-151">Enter a name for the project.</span></span>
   * <span data-ttu-id="9f589-152">Na área **JRE**, verifique se **Usar um ambiente de execução JRE** está definido como **JavaSE-1.7** ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9f589-152">In the **JRE** area, make sure that **Use an execution environment JRE** is set to **JavaSE-1.7** or later.</span></span>
   * <span data-ttu-id="9f589-153">O Spark SDK deve ser definido como o local onde você baixou o SDK.</span><span class="sxs-lookup"><span data-stu-id="9f589-153">Make sure that Spark SDK is set to the location where you downloaded the SDK.</span></span> <span data-ttu-id="9f589-154">O link para o local de download está incluído nos [pré-requisitos](#prerequisites) anteriormente apresentados neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9f589-154">The link to the download location is included in the [prerequisites](#prerequisites) earlier in this article.</span></span> <span data-ttu-id="9f589-155">Você também pode baixar o SDK no link incluído na caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f589-155">You can also download the SDK from the link included in the dialog box.</span></span>

    ![Caixa de diálogo Novo Projeto de Scala HDInsight](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  <span data-ttu-id="9f589-157">Na próxima caixa de diálogo, clique na guia **Bibliotecas**, mantenha os padrões e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="9f589-157">In the next dialog box, click the **Libraries** tab and keep the defaults, and then click **Finish**.</span></span> 
   
    ![Guia Bibliotecas](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="9f589-159">Criar um aplicativo Scala para cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f589-159">Create a Scala application for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="9f589-160">No Eclipse IDE, em Explorador de Pacotes, expanda o projeto que você criou anteriormente, clique com botão direito do mouse em **src**, aponte para **Novo** e clique em **Outros**.</span><span class="sxs-lookup"><span data-stu-id="9f589-160">In the Eclipse IDE, from Package Explorer, expand the project that you created earlier, right-click **src**, point to **New**, and then click **Other**.</span></span>
2. <span data-ttu-id="9f589-161">Na caixa de diálogo **Selecionar um assistente**, expanda **Assistentes Scala**, clique em **Objeto Scala** e em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9f589-161">In the **Select a wizard** dialog box, expand **Scala Wizards**, click **Scala Object**, and then click **Next**.</span></span>
   
    ![Selecione uma caixa de diálogo do assistente](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. <span data-ttu-id="9f589-163">Na caixa de diálogo **Criar um Novo Arquivo**, insira um nome para o objeto e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="9f589-163">In the **Create New File** dialog box, enter a name for the object, and then click **Finish**.</span></span>
   
    ![Criar caixa de diálogo Novo Arquivo](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. <span data-ttu-id="9f589-165">Cole o seguinte código no editor de texto:</span><span class="sxs-lookup"><span data-stu-id="9f589-165">Paste the following code in the text editor:</span></span>
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows that have only one digit in the seventh column in the CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. <span data-ttu-id="9f589-166">Execute o aplicativo em um cluster HDInsight Spark:</span><span class="sxs-lookup"><span data-stu-id="9f589-166">Run the application on an HDInsight Spark cluster:</span></span>
   
   1. <span data-ttu-id="9f589-167">No Explorador de Pacotes, clique com o botão direito do mouse no nome do projeto e escolha **Enviar Aplicativo Spark para HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9f589-167">From Package Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>        
   2. <span data-ttu-id="9f589-168">Na caixa de diálogo **Envio do Spark** , forneça os valores abaixo e clique em **Enviar**:</span><span class="sxs-lookup"><span data-stu-id="9f589-168">In the **Spark Submission** dialog box, provide the following values, and then click **Submit**:</span></span>
      
      * <span data-ttu-id="9f589-169">Para **Nome do Cluster**, selecione o cluster HDInsight Spark no qual você deseja executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f589-169">For **Cluster Name**, select the HDInsight Spark cluster on which you want to run your application.</span></span>
      * <span data-ttu-id="9f589-170">Selecione um artefato do projeto Eclipse ou selecionar uma opção do disco rígido.</span><span class="sxs-lookup"><span data-stu-id="9f589-170">Select an artifact from the Eclipse project, or select one from a hard drive.</span></span> <span data-ttu-id="9f589-171">O valor padrão depende do item no qual você clica com o botão direito do mouse por meio do gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="9f589-171">The default value depends on the item you right-click from package explorer.</span></span>
      * <span data-ttu-id="9f589-172">Na lista suspensa **Nome de classe principal**, o assistente de envio exibe todos os nomes de objeto do projeto selecionado.</span><span class="sxs-lookup"><span data-stu-id="9f589-172">In the **Main class name** dropdownlist, submission wizard displays all object names from your selected project.</span></span> <span data-ttu-id="9f589-173">Selecione ou insira um que você deseja executar.</span><span class="sxs-lookup"><span data-stu-id="9f589-173">Select or input one that you want to run.</span></span> <span data-ttu-id="9f589-174">Se você selecionar um artefato do disco rígido, você precisará inserir o nome de classe principal sozinho.</span><span class="sxs-lookup"><span data-stu-id="9f589-174">If you select artifact from hard disk, you need input main class name by yourself.</span></span> 
      * <span data-ttu-id="9f589-175">Como o código do aplicativo neste exemplo não exige argumentos de linha de comando ou JARs ou arquivos de referência, você pode deixar as caixas de texto restantes vazias.</span><span class="sxs-lookup"><span data-stu-id="9f589-175">Because the application code in this example does not require any command-line arguments or reference JARs or files, you can leave the remaining text boxes empty.</span></span>
        
       ![Caixa de diálogo Envio do Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. <span data-ttu-id="9f589-177">A guia **Envio de Spark** deve começar a exibir o progresso.</span><span class="sxs-lookup"><span data-stu-id="9f589-177">The **Spark Submission** tab should start displaying the progress.</span></span> <span data-ttu-id="9f589-178">Você pode interromper o aplicativo clicando no botão vermelho na janela **Envio do Spark**.</span><span class="sxs-lookup"><span data-stu-id="9f589-178">You can stop the application by clicking the red button in the **Spark Submission** window.</span></span> <span data-ttu-id="9f589-179">Você também pode exibir os logs para essa execução de aplicativo específica clicando no ícone de globo (indicado pela caixa azul na imagem).</span><span class="sxs-lookup"><span data-stu-id="9f589-179">You can also view the logs for this specific application run by clicking the globe icon (denoted by the blue box in the image).</span></span>
      
       ![Janela Envio do Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a><span data-ttu-id="9f589-181">Acessar e gerenciar clusters HDInsight Spark usando as Ferramentas do HDInsight no Kit de Ferramentas do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="9f589-181">Access and manage HDInsight Spark clusters by using HDInsight Tools in Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="9f589-182">Você pode executar várias operações usando as Ferramentas do HDInsight, incluindo o acesso à saída do trabalho.</span><span class="sxs-lookup"><span data-stu-id="9f589-182">You can perform various operations by using HDInsight Tools, including accessing the job output.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="9f589-183">Acessar a exibição do trabalho</span><span class="sxs-lookup"><span data-stu-id="9f589-183">Access the job view</span></span>
1. <span data-ttu-id="9f589-184">No Azure Explorer, expanda **HDInsight**, expanda o nome do cluster Spark, em seguida, clique em **Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="9f589-184">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then click **Jobs**.</span></span> 

    ![Nó de exibição de trabalho](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="9f589-186">Clique no **trabalhos** nó.</span><span class="sxs-lookup"><span data-stu-id="9f589-186">Click on the **Jobs** node.</span></span> <span data-ttu-id="9f589-187">As ferramentas do HDInsight detecta automaticamente se você instalou o plug-in de clipse E (fx) ou não.</span><span class="sxs-lookup"><span data-stu-id="9f589-187">The HDInsight Tools auto-detects whether you installed the E(fx)clipse plugin or not.</span></span> <span data-ttu-id="9f589-188">Clique em **Okey** para continuar e siga as instruções para instalar o Marketplace do Eclipse e reinicie o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9f589-188">Click **OK** to continue and follow the instructions to install the Eclipse Marketplace and restart Eclipse.</span></span>

    ![Instalar E(fx)clipse](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. <span data-ttu-id="9f589-190">Abra a Exibição de Trabalho do nó **Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="9f589-190">Open the Job View from the **Jobs** node.</span></span> <span data-ttu-id="9f589-191">No painel direito, a guia **Exibição de Trabalho do Spark** exibe todos os aplicativos que foram executados no cluster.</span><span class="sxs-lookup"><span data-stu-id="9f589-191">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="9f589-192">Clique no nome do aplicativo do qual você deseja ver mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="9f589-192">Click the name of the application for which you want to see more details.</span></span>

    ![Detalhes do aplicativo](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. <span data-ttu-id="9f589-194">Se você passar o mouse no gráfico de trabalho, ele exibe informações básicas de trabalho em execução.</span><span class="sxs-lookup"><span data-stu-id="9f589-194">If you hover on the job graph, it displays basic running job info.</span></span> <span data-ttu-id="9f589-195">Clicar no gráfico de trabalho mostra o gráfico de estágios e informações que gera todos os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="9f589-195">Clicking on the job graph shows the stages graph and info that every job generates.</span></span>

    ![Detalhes do estágio do trabalho](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. <span data-ttu-id="9f589-197">Os logs usados com frequência, incluindo informações do diretório, Driver Stdout e Stderr do Driver são listados no **Log** guia.</span><span class="sxs-lookup"><span data-stu-id="9f589-197">Frequently used logs, including Driver Stderr, Driver Stdout, and Directory Info, are listed in the **Log** tab.</span></span>

    ![Detalhes do log](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. <span data-ttu-id="9f589-199">Você também pode abrir a interface do usuário de histórico do Spark e a interface do usuário do YARN (no nível do aplicativo) clicando no respectivo hiperlink na parte superior da janela.</span><span class="sxs-lookup"><span data-stu-id="9f589-199">You can also open the Spark history UI and the YARN UI (at the application level) by clicking the respective hyperlink at the top of the window.</span></span>

### <a name="access-the-storage-container-for-the-cluster"></a><span data-ttu-id="9f589-200">Acessar o contêiner de armazenamento do cluster</span><span class="sxs-lookup"><span data-stu-id="9f589-200">Access the storage container for the cluster</span></span>
1. <span data-ttu-id="9f589-201">No Azure Explorer, expanda o nó raiz **HDInsight** para ver uma lista de clusters HDInsight Spark disponíveis.</span><span class="sxs-lookup"><span data-stu-id="9f589-201">In Azure Explorer, expand the **HDInsight** root node to see a list of HDInsight Spark clusters that are available.</span></span>
2. <span data-ttu-id="9f589-202">Expanda o nome do cluster para ver a conta de armazenamento e o contêiner de armazenamento padrão do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f589-202">Expand the cluster name to see the storage account and the default storage container for the cluster.</span></span>
   
    ![Contêiner de armazenamento padrão e a conta de armazenamento](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. <span data-ttu-id="9f589-204">Clique no nome do contêiner de armazenamento associado ao cluster.</span><span class="sxs-lookup"><span data-stu-id="9f589-204">Click the storage container name associated with the cluster.</span></span> <span data-ttu-id="9f589-205">No painel direito, clique duas vezes na pasta **HVACOut**.</span><span class="sxs-lookup"><span data-stu-id="9f589-205">In the right pane, double-click the **HVACOut** folder.</span></span> <span data-ttu-id="9f589-206">Abra um dos arquivos **part-** para ver a saída do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f589-206">Open one of the **part-** files to see the output of the application.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="9f589-207">Acessar o servidor de histórico do Spark</span><span class="sxs-lookup"><span data-stu-id="9f589-207">Access the Spark history server</span></span>
1. <span data-ttu-id="9f589-208">No Azure Explorer, clique com o botão direito do mouse no nome do cluster Spark e escolha **Abrir a Interface do Usuário de Histórico do Spark**.</span><span class="sxs-lookup"><span data-stu-id="9f589-208">In Azure Explorer, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> <span data-ttu-id="9f589-209">Quando solicitado, insira as credenciais de administrador para o cluster.</span><span class="sxs-lookup"><span data-stu-id="9f589-209">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="9f589-210">Elas devem ter sido especificadas no provisionamento do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f589-210">You must have specified these while provisioning the cluster.</span></span>
2. <span data-ttu-id="9f589-211">No painel do Servidor de Histórico do Spark, procure o aplicativo que você acabou de executar usando o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f589-211">In the Spark history server dashboard, you use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="9f589-212">No código anterior, você definiu o nome do aplicativo usando `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="9f589-212">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="9f589-213">Dessa forma, o nome do aplicativo Spark era **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="9f589-213">Hence, your Spark application name was **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="9f589-214">Iniciar o portal do Ambari</span><span class="sxs-lookup"><span data-stu-id="9f589-214">Start the Ambari portal</span></span>
1. <span data-ttu-id="9f589-215">No Azure Explorer, clique com o botão direito do mouse no nome do cluster Spark e escolha **Abrir o Portal de Gerenciamento do Cluster (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="9f589-215">In Azure Explorer, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 
2. <span data-ttu-id="9f589-216">Quando solicitado, insira as credenciais de administrador para o cluster.</span><span class="sxs-lookup"><span data-stu-id="9f589-216">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="9f589-217">Elas devem ter sido especificadas no provisionamento do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f589-217">You must have specified these while provisioning the cluster.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="9f589-218">Gerenciar assinaturas do Azure</span><span class="sxs-lookup"><span data-stu-id="9f589-218">Manage Azure subscriptions</span></span>
<span data-ttu-id="9f589-219">Por padrão, as Ferramentas do HDInsight no Kit de Ferramentas do Azure para Eclipse listam os clusters Spark de todas as suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f589-219">By default, HDInsight Tools in Azure Toolkit for Eclipse lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="9f589-220">Se for necessário, você poderá especificar as assinaturas para as quais deseja acessar o cluster.</span><span class="sxs-lookup"><span data-stu-id="9f589-220">If necessary, you can specify the subscriptions for which you want to access the cluster.</span></span> 

1. <span data-ttu-id="9f589-221">No Azure Explorer, clique com o botão direito do mouse no nó-raiz **Azure** e clique em **Gerenciar Assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="9f589-221">In Azure Explorer, right-click the **Azure** root node, and then click **Manage Subscriptions**.</span></span> 
2. <span data-ttu-id="9f589-222">Na caixa de diálogo, desmarque as caixas de seleção da assinatura que você não deseja acessar e clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="9f589-222">In the dialog box, clear the check boxes for the subscription that you don't want to access, and then click **Close**.</span></span> <span data-ttu-id="9f589-223">Você também poderá clicar em **Sair** se quiser fazer sair da sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f589-223">You can also click **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="9f589-224">Executar um aplicativo Scala Spark localmente</span><span class="sxs-lookup"><span data-stu-id="9f589-224">Run a Spark Scala application locally</span></span>
<span data-ttu-id="9f589-225">Você pode usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para Eclipse para executar aplicativos Spark Scala localmente em sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9f589-225">You can use HDInsight Tools in Azure Toolkit for Eclipse to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="9f589-226">Normalmente, esses aplicativos não precisam acessar recursos de cluster como um contêiner de armazenamento e você pode executá-los e testá-los localmente.</span><span class="sxs-lookup"><span data-stu-id="9f589-226">Typically, these applications don't need access to cluster resources such as a storage container, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="9f589-227">Pré-requisito</span><span class="sxs-lookup"><span data-stu-id="9f589-227">Prerequisite</span></span>
<span data-ttu-id="9f589-228">Durante a execução do aplicativo Spark Scala local em um computador Windows, você pode receber uma exceção, conforme explicado em [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="9f589-228">While you're running the local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="9f589-229">Essa exceção ocorre porque **WinUtils.exe** está ausente no Windows.</span><span class="sxs-lookup"><span data-stu-id="9f589-229">This exception occurs because **WinUtils.exe** is missing in Windows.</span></span> 

<span data-ttu-id="9f589-230">Para solucionar esse erro, você deve [baixar o executável](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) em um local como **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="9f589-230">To resolve this error, you must [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="9f589-231">Em seguida, adicione uma variável de ambiente **HADOOP_HOME** e defina o valor da variável como **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="9f589-231">You must then add the environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="9f589-232">Executar um aplicativo Scala Spark local</span><span class="sxs-lookup"><span data-stu-id="9f589-232">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="9f589-233">Inicie o Eclipse e crie um projeto.</span><span class="sxs-lookup"><span data-stu-id="9f589-233">Start Eclipse and create a project.</span></span> <span data-ttu-id="9f589-234">Na caixa de diálogo **Novo Projeto**, faça as opções a seguir e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9f589-234">In the **New Project** dialog box, make the following choices, and then click **Next**.</span></span>
   
   * <span data-ttu-id="9f589-235">No painel esquerdo, escolha **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9f589-235">In the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="9f589-236">No painel direito, selecione **Exemplo de Execução Local do Spark no HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="9f589-236">In the right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    ![Caixa de diálogo Novo Projeto](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. <span data-ttu-id="9f589-238">Para fornecer os detalhes do projeto, siga as etapas 3 a 6 da seção anterior [Configurar um projeto de Spark Scala para um cluster HDInsight Spark](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span><span class="sxs-lookup"><span data-stu-id="9f589-238">To provide the project details, follow steps 3 through 6 from the earlier section [Set up a Spark Scala project for an HDInsight Spark cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span></span>
3. <span data-ttu-id="9f589-239">O modelo adiciona um código de exemplo (**LogQuery**) na pasta **src** que pode ser executada localmente em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9f589-239">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![Local do LogQuery](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. <span data-ttu-id="9f589-241">Clique com botão direito do mouse no aplicativo **LogQuery**, aponte para **Executar como** e clique em **1 Aplicativo Scala**.</span><span class="sxs-lookup"><span data-stu-id="9f589-241">Right-click the **LogQuery** application, point to **Run As**, and then click **1 Scala Application**.</span></span> <span data-ttu-id="9f589-242">Você verá uma saída como esta na guia **Console** na parte inferior:</span><span class="sxs-lookup"><span data-stu-id="9f589-242">You will see an output like this in the **Console** tab at the bottom:</span></span>
   
   ![Resultado da execução local do Aplicativo Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a><span data-ttu-id="9f589-244">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="9f589-244">FAQ</span></span>
<span data-ttu-id="9f589-245">Para enviar um aplicativo ao Azure Data Lake Store, escolha o modo **Interativo** durante o processo de entrada no Azure.</span><span class="sxs-lookup"><span data-stu-id="9f589-245">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="9f589-246">Se você selecionar o modo **Automatizado**, obterá um erro.</span><span class="sxs-lookup"><span data-stu-id="9f589-246">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

<span data-ttu-id="9f589-248">Isso já está resolvido.</span><span class="sxs-lookup"><span data-stu-id="9f589-248">Now, we resolved it.</span></span> <span data-ttu-id="9f589-249">Você pode escolher um Cluster do Azure Data Lake para enviar seu aplicativo com qualquer método de entrada.</span><span class="sxs-lookup"><span data-stu-id="9f589-249">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="9f589-250">Comentários e problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="9f589-250">Feedback and known issues</span></span>
<span data-ttu-id="9f589-251">Atualmente, não há suporte para exibir saídas do Spark diretamente.</span><span class="sxs-lookup"><span data-stu-id="9f589-251">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="9f589-252">Se você tiver sugestões ou comentários, ou se encontrar problemas ao usar essa ferramenta, fique à vontade para enviar um email para hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="9f589-252">If you have any suggestions or feedback, or if you encounter any problems when using this tool, feel free to send us an email at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="9f589-253"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="9f589-253"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="9f589-254">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f589-254">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="9f589-255">Cenários</span><span class="sxs-lookup"><span data-stu-id="9f589-255">Scenarios</span></span>
* [<span data-ttu-id="9f589-256">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="9f589-256">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="9f589-257">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="9f589-257">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="9f589-258">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para prever resultados da inspeção de alimentos</span><span class="sxs-lookup"><span data-stu-id="9f589-258">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="9f589-259">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="9f589-259">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="9f589-260">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f589-260">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="9f589-261">Criando e executando aplicativos</span><span class="sxs-lookup"><span data-stu-id="9f589-261">Creating and running applications</span></span>
* [<span data-ttu-id="9f589-262">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="9f589-262">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="9f589-263">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="9f589-263">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="9f589-264">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="9f589-264">Tools and extensions</span></span>
* [<span data-ttu-id="9f589-265">Usar o Kit de Ferramentas do Azure para IntelliJ para criar e enviar aplicativos Spark Scala</span><span class="sxs-lookup"><span data-stu-id="9f589-265">Use Azure Toolkit for IntelliJ to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="9f589-266">Usar o kit de ferramentas do Azure para IntelliJ a fim de depurar aplicativos Spark remotamente por meio da VPN</span><span class="sxs-lookup"><span data-stu-id="9f589-266">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="9f589-267">Usar o kit de ferramentas do Azure para IntelliJ a fim de depurar aplicativos Spark remotamente por meio do SSH</span><span class="sxs-lookup"><span data-stu-id="9f589-267">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="9f589-268">Usar ferramentas do HDInsight para IntelliJ com a área restrita do Hortonworks</span><span class="sxs-lookup"><span data-stu-id="9f589-268">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="9f589-269">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f589-269">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="9f589-270">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f589-270">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="9f589-271">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="9f589-271">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="9f589-272">Instalar o Jupyter em seu computador e conectar-se a um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f589-272">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="9f589-273">Gerenciando recursos</span><span class="sxs-lookup"><span data-stu-id="9f589-273">Managing resources</span></span>
* [<span data-ttu-id="9f589-274">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f589-274">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="9f589-275">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f589-275">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

