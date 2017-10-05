---
title: "Kit de ferramentas do Azure para IntelliJ – depurar aplicativos remotamente no HDInsight Spark | Microsoft Docs"
description: Saiba como usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ para depurar remotamente os aplicativos executados em clusters HDInsight Spark por meio da VPN.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 5ce282aac94d0f22ea587cbe4005819310e23b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-debug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="e3566-103">Usar o kit de ferramentas do Azure para IntelliJ para depurar aplicativos remotamente no HDInsight Spark por meio da VPN</span><span class="sxs-lookup"><span data-stu-id="e3566-103">Use Azure Toolkit for IntelliJ to debug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="e3566-104">Recomendamos o modo de depuração remota do aplicativo Spark por meio do SSH.</span><span class="sxs-lookup"><span data-stu-id="e3566-104">We recommend the way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="e3566-105">Para obter instruções, consulte [Depurar aplicativos Spark remotamente em um cluster HDInsight com o kit de ferramentas do Azure para IntelliJ por meio do SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="e3566-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="e3566-106">Este artigo oferece diretrizes passo a passo sobre como usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ para enviar um trabalho do Spark no cluster HDInsight Spark e depurá-lo remotamente do seu computador desktop.</span><span class="sxs-lookup"><span data-stu-id="e3566-106">This article provides step-by-step guidance on how to use the HDInsight Tools in Azure Toolkit for IntelliJ to submit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="e3566-107">Para fazer isso, você deve executar as seguintes etapas de alto nível:</span><span class="sxs-lookup"><span data-stu-id="e3566-107">To do so, you must perform the following high-level steps:</span></span>

1. <span data-ttu-id="e3566-108">Crie uma Rede Virtual do Azure site a site ou ponto a site.</span><span class="sxs-lookup"><span data-stu-id="e3566-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="e3566-109">As etapas neste documento pressupõem que você esteja usando uma rede site a site.</span><span class="sxs-lookup"><span data-stu-id="e3566-109">The steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="e3566-110">Crie um cluster Spark no Azure HDInsight que faça parte da Rede Virtual do Azure site a site.</span><span class="sxs-lookup"><span data-stu-id="e3566-110">Create a Spark cluster in Azure HDInsight that is part of the site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="e3566-111">Verifique a conectividade entre o nó de cabeçalho do cluster e seu desktop.</span><span class="sxs-lookup"><span data-stu-id="e3566-111">Verify the connectivity between the cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="e3566-112">Crie um aplicativo Scala no IntelliJ IDEA e configure-o para a depuração remota.</span><span class="sxs-lookup"><span data-stu-id="e3566-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="e3566-113">Execute e depure o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3566-113">Run and debug the application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3566-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3566-114">Prerequisites</span></span>
* <span data-ttu-id="e3566-115">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3566-115">An Azure subscription.</span></span> <span data-ttu-id="e3566-116">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e3566-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e3566-117">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e3566-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e3566-118">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e3566-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="e3566-119">Kit de desenvolvimento Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="e3566-119">Oracle Java Development kit.</span></span> <span data-ttu-id="e3566-120">Você pode instalá-lo clicando [aqui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="e3566-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="e3566-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="e3566-121">IntelliJ IDEA.</span></span> <span data-ttu-id="e3566-122">Este artigo usa a versão 2017.1.</span><span class="sxs-lookup"><span data-stu-id="e3566-122">This article uses version 2017.1.</span></span> <span data-ttu-id="e3566-123">Você pode instalá-lo clicando [aqui](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="e3566-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="e3566-124">Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="e3566-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="e3566-125">As Ferramentas do HDInsight para IntelliJ estão disponíveis como parte do Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="e3566-125">HDInsight tools for IntelliJ are available as part of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="e3566-126">Para obter instruções sobre como instalar o Kit de Ferramentas do Azure, veja [Instalando o Kit de Ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="e3566-126">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="e3566-127">Faça logon em sua assinatura do Azure no IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="e3566-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="e3566-128">Siga as instruções [aqui](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="e3566-128">Follow the instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="e3566-129">Durante a execução do aplicativo Spark Scala para depuração remota em um computador com Windows, você pode receber uma exceção, conforme explicado em [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) , que ocorre devido a à ausência do WinUtils.exe no Windows.</span><span class="sxs-lookup"><span data-stu-id="e3566-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="e3566-130">Para solucionar esse erro, você deve [baixar aqui o executável](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) para um local como **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="e3566-130">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="e3566-131">Em seguida, adicione uma variável de ambiente **HADOOP_HOME** e defina o valor da variável como **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="e3566-131">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="e3566-132">Etapa 1: Criar uma rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="e3566-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="e3566-133">Siga as instruções dos links a seguir para criar uma Rede Virtual do Azure e então verifique a conectividade entre o desktop e a Rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3566-133">Follow the instructions from the below links to create an Azure Virtual Network and then verify the connectivity between the desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="e3566-134">Criar uma Rede Virtual com uma conexão VPN site a site usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e3566-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="e3566-135">Criar uma Rede Virtual com uma conexão VPN site a site usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3566-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="e3566-136">Configurar uma conexão Ponto a Site com uma rede virtual usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3566-136">Configure a point-to-site connection to a virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="e3566-137">Etapa 2: Criar um cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="e3566-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="e3566-138">Você também deve criar um cluster Apache Spark no Azure HDInsight que faça parte da Rede Virtual do Azure criada.</span><span class="sxs-lookup"><span data-stu-id="e3566-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of the Azure Virtual Network that you created.</span></span> <span data-ttu-id="e3566-139">Use as informações disponíveis em [Criar clusters baseados em Linux no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="e3566-139">Use the information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="e3566-140">Como parte da configuração opcional, selecione a Rede Virtual do Azure que você criou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="e3566-140">As part of optional configuration, select the Azure Virtual Network that you created in the previous step.</span></span>

## <a name="step-3-verify-the-connectivity-between-the-cluster-headnode-and-your-desktop"></a><span data-ttu-id="e3566-141">Etapa 3: Verificar a conectividade entre o nó de cabeçalho do cluster e seu desktop</span><span class="sxs-lookup"><span data-stu-id="e3566-141">Step 3: Verify the connectivity between the cluster headnode and your desktop</span></span>
1. <span data-ttu-id="e3566-142">Obter endereço IP do nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="e3566-142">Get the IP address of the headnode.</span></span> <span data-ttu-id="e3566-143">Abra a IU do Ambari para o cluster.</span><span class="sxs-lookup"><span data-stu-id="e3566-143">Open Ambari UI for the cluster.</span></span> <span data-ttu-id="e3566-144">Na folha do cluster, clique em **Painel**.</span><span class="sxs-lookup"><span data-stu-id="e3566-144">From the cluster blade, click **Dashboard**.</span></span>

    ![Localizar o IP do nó de cabeçalho](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="e3566-146">Na IU do Ambari, no canto superior direito, clique em **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="e3566-146">From the Ambari UI, from the top-right corner, click **Hosts**.</span></span>

    ![Localizar o IP do nó de cabeçalho](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="e3566-148">Você deve ver uma lista de nós de cabeçalho, os nós de trabalho e os nós do zookeeper.</span><span class="sxs-lookup"><span data-stu-id="e3566-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="e3566-149">Os nós de cabeçalho têm o prefixo **hn***.</span><span class="sxs-lookup"><span data-stu-id="e3566-149">The headnodes have the **hn*** prefix.</span></span> <span data-ttu-id="e3566-150">Clique no primeiro nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="e3566-150">Click the first headnode.</span></span>

    ![Localizar o IP do nó de cabeçalho](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="e3566-152">Na parte inferior da página , na caixa **Resumo** , copie o endereço IP do nó de cabeçalho e o nome do host.</span><span class="sxs-lookup"><span data-stu-id="e3566-152">At the bottom of the page that opens, from the **Summary** box, copy the IP address of the headnode and the host name.</span></span>

    ![Localizar o IP do nó de cabeçalho](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="e3566-154">Inclua o endereço IP e o nome do host do nó de cabeçalho no arquivo **hosts** no computador de onde você deseja executar e depurar os trabalhos Spark remotamente.</span><span class="sxs-lookup"><span data-stu-id="e3566-154">Include the IP address and the host name of the headnode to the **hosts** file on the computer from where you want to run and remotely debug the Spark jobs.</span></span> <span data-ttu-id="e3566-155">Isso permitirá que você se comunique com o nó de cabeçalho usando o endereço IP, bem como o nome do host.</span><span class="sxs-lookup"><span data-stu-id="e3566-155">This will enable you to communicate with the headnode using the IP address as well as the hostname.</span></span>

   1. <span data-ttu-id="e3566-156">Abra um bloco de notas com permissões elevadas.</span><span class="sxs-lookup"><span data-stu-id="e3566-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="e3566-157">No menu Arquivo, clique em **Abrir** e navegue até o local do arquivo hosts.</span><span class="sxs-lookup"><span data-stu-id="e3566-157">From the file menu, click **Open** and then navigate to the location of the hosts file.</span></span> <span data-ttu-id="e3566-158">Em um computador com o Windows, é `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="e3566-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="e3566-159">Adicione o seguinte ao arquivo **hosts** .</span><span class="sxs-lookup"><span data-stu-id="e3566-159">Add the following to the **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="e3566-160">No computador conectado à Rede Virtual do Azure usada pelo cluster HDInsight, verifique se você pode executar ping nos dois nós de cabeçalho usando o endereço IP, bem como o nome do host.</span><span class="sxs-lookup"><span data-stu-id="e3566-160">From the computer that you connected to the Azure Virtual Network that is used by the HDInsight cluster, verify that you can ping both the headnodes using the IP address as well as the hostname.</span></span>
7. <span data-ttu-id="e3566-161">Use o SSH para acessar o nó de cabeçalho do cluster usando as instruções em [Conectar-se a um cluster HDInsight usando SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e3566-161">SSH into the cluster headnode using the instructions at [Connect to an HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="e3566-162">Do nó de cabeçalho do cluster, execute ping no endereço IP do computador desktop.</span><span class="sxs-lookup"><span data-stu-id="e3566-162">From the cluster headnode, ping the IP address of the desktop computer.</span></span> <span data-ttu-id="e3566-163">Você deve testar a conectividade para os endereços IP atribuídos ao computador, um para a conexão de rede e outro para a Rede Virtual do Azure à qual o computador está conectado.</span><span class="sxs-lookup"><span data-stu-id="e3566-163">You should test connectivity to both the IP addresses assigned to the computer, one for the network connection and the other for the Azure Virtual Network that the computer is connected to.</span></span>
8. <span data-ttu-id="e3566-164">Repita estas etapas no outro nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="e3566-164">Repeat the steps for the other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-the-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="e3566-165">Etapa 4: Criar um aplicativo Scala Spark usando as Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ e configurá-lo para a depuração remota</span><span class="sxs-lookup"><span data-stu-id="e3566-165">Step 4: Create a Spark Scala application using the HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="e3566-166">Inicie o IntelliJ IDEA e crie um novo projeto.</span><span class="sxs-lookup"><span data-stu-id="e3566-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="e3566-167">Na caixa de diálogo Novo Projeto, faça o seguinte e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e3566-167">In the new project dialog box, make the following choices, and then click **Next**.</span></span>

    ![Criar um aplicativo Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="e3566-169">No painel esquerdo, escolha **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e3566-169">From the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="e3566-170">No painel direito, selecione **Spark no HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="e3566-170">From the right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="e3566-171">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e3566-171">Click **Next**.</span></span>
2. <span data-ttu-id="e3566-172">Na próxima janela, forneça os seguintes detalhes do projeto e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="e3566-172">In the next window, provide the following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="e3566-173">Forneça um nome de projeto e o local do projeto.</span><span class="sxs-lookup"><span data-stu-id="e3566-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="e3566-174">Para o **SDK de projeto**, use o Java 1.8 para o cluster do Spark 2.x e o Java 1.7 para o cluster do Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="e3566-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="e3566-175">Para a **versão do Spark**, o assistente de criação de projetos Scala integra a versão apropriada do SDK do Spark e do SDK do Scala.</span><span class="sxs-lookup"><span data-stu-id="e3566-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="e3566-176">Se a versão de cluster do Spark for inferior a 2.0, escolha o Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="e3566-176">If the spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="e3566-177">Caso contrário, você deve selecionar o spark2.x.</span><span class="sxs-lookup"><span data-stu-id="e3566-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="e3566-178">Este exemplo usa o Spark 2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="e3566-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="e3566-179">![Criar um aplicativo Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="e3566-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="e3566-180">O projeto do Spark criará automaticamente um artefato para você.</span><span class="sxs-lookup"><span data-stu-id="e3566-180">The Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="e3566-181">Para ver o artefato, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="e3566-181">To see the artifact, follow these steps.</span></span>

   1. <span data-ttu-id="e3566-182">No menu **Arquivo**, clique em **Estrutura do Projeto**.</span><span class="sxs-lookup"><span data-stu-id="e3566-182">From the **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="e3566-183">Na caixa de diálogo **Estrutura do Projeto**, clique em **Artefatos** para ver o artefato padrão criado.</span><span class="sxs-lookup"><span data-stu-id="e3566-183">In the **Project Structure** dialog box, click **Artifacts** to see the default artifact that is created.</span></span>
   <span data-ttu-id="e3566-184">![Criar JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="e3566-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="e3566-185">Você também pode criar seu próprio artefato clicando no ícone **+** , realçado na imagem acima.</span><span class="sxs-lookup"><span data-stu-id="e3566-185">You can also create your own artifact bly clicking on the **+** icon, highlighted in the image above.</span></span>

4. <span data-ttu-id="e3566-186">Adicione bibliotecas ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="e3566-186">Add libraries to your project.</span></span> <span data-ttu-id="e3566-187">Para adicionar uma biblioteca, clique com o botão direito do mouse no nome do projeto na árvore do projeto e clique em **Abrir Configurações do Módulo**.</span><span class="sxs-lookup"><span data-stu-id="e3566-187">To add a library, right-click the project name in the project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="e3566-188">Na caixa de diálogo **Estrutura do Projeto**, no painel esquerdo, clique em **Bibliotecas**, clique no símbolo (+) e clique em **Do Maven**.</span><span class="sxs-lookup"><span data-stu-id="e3566-188">In the **Project Structure** dialog box, from the left pane, click **Libraries**, click the (+) symbol, and then click **From Maven**.</span></span>

    ![Adicionar biblioteca](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="e3566-190">Na caixa de diálogo **Baixar a Biblioteca do Repositório Maven** , pesquise e adicione as bibliotecas a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3566-190">In the **Download Library from Maven Repository** dialog box, search and add the following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="e3566-191">Copie `yarn-site.xml` e `core-site.xml` do nó de cabeçalho do cluster e os adicione ao projeto.</span><span class="sxs-lookup"><span data-stu-id="e3566-191">Copy `yarn-site.xml` and `core-site.xml` from the cluster headnode and add it to the project.</span></span> <span data-ttu-id="e3566-192">Use os comandos a seguir para copiar os arquivos.</span><span class="sxs-lookup"><span data-stu-id="e3566-192">Use the following commands to copy the files.</span></span> <span data-ttu-id="e3566-193">Você pode usar [Cygwin](https://cygwin.com/install.html) para executar os seguintes comandos `scp` para copiar os arquivos dos nós de cabeçalho do cluster.</span><span class="sxs-lookup"><span data-stu-id="e3566-193">You can use [Cygwin](https://cygwin.com/install.html) to run the following `scp` commands to copy the files from the cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="e3566-194">Como nós já adicionamos o endereço IP e os nomes do host do nó de cabeçalho do cluster e para o arquivos hosts no desktop, podemos usar os comandos **scp** da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="e3566-194">Because we already added the cluster headnode IP address and hostnames fo the hosts file on the desktop, we can use the **scp** commands in the following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="e3566-195">Adicione esses arquivos ao seu projeto copiando-da pasta **/src** na sua árvore de projeto, por exemplo, `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="e3566-195">Add these files to your project by copying them under the **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="e3566-196">Atualize o `core-site.xml` para fazer as alterações a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3566-196">Update the `core-site.xml` to make the following changes.</span></span>

   1. <span data-ttu-id="e3566-197">`core-site.xml` inclui a chave criptografada para a conta de armazenamento associada ao cluster.</span><span class="sxs-lookup"><span data-stu-id="e3566-197">`core-site.xml` includes the encrypted key to the storage account associated with the cluster.</span></span> <span data-ttu-id="e3566-198">No `core-site.xml` que você adicionou ao projeto, substitua a chave criptografada pela chave de armazenamento real associada à conta de armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="e3566-198">In the `core-site.xml` that you added to the project, replace the encrypted key with the actual storage key associated with the default storage account.</span></span> <span data-ttu-id="e3566-199">Confira [Gerenciar as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="e3566-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="e3566-200">Remova as entradas a seguir do `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="e3566-200">Remove the following entries from the `core-site.xml`.</span></span>

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. <span data-ttu-id="e3566-201">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="e3566-201">Save the file.</span></span>
7. <span data-ttu-id="e3566-202">Adicione a classe Main ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3566-202">Add the Main class for your application.</span></span> <span data-ttu-id="e3566-203">No **Gerenciador de Projetos**, clique com o botão direito do mouse em **src**, aponte para **Novo** e clique em **Classe do Scala**.</span><span class="sxs-lookup"><span data-stu-id="e3566-203">From the **Project Explorer**, right-click **src**, point to **New**, and then click **Scala class**.</span></span>

    ![Adicionar código-fonte](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="e3566-205">Na caixa de diálogo **Criar Nova Classe do Scala**, forneça um nome, para **Variante** escolha **Objeto** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3566-205">In the **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Adicionar código-fonte](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="e3566-207">No arquivo `MyClusterAppMain.scala` , cole o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3566-207">In the `MyClusterAppMain.scala` file, paste the following code.</span></span> <span data-ttu-id="e3566-208">Esse código cria o contexto do Spark e inicia um método `executeJob` do objeto `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="e3566-208">This code creates the Spark context and launches an `executeJob` method from the `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. <span data-ttu-id="e3566-209">Repita as etapas 8 e 9 acima para adicionar um novo objeto Scala chamado `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="e3566-209">Repeat steps 8 and 9 above to add a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="e3566-210">Para essa classe, adicione o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3566-210">To this class add the following code.</span></span> <span data-ttu-id="e3566-211">Esse código lê os dados no HVAC.csv (disponível em todos os clusters Spark HDInsight), recupera as linhas com apenas um dígito na sétima coluna no CSV e grava a saída em **/HVACOut** no contêiner padrão de armazenamento do cluster.</span><span class="sxs-lookup"><span data-stu-id="e3566-211">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the seventh column in the CSV, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find the rows which have only one digit in the 7th column in the CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="e3566-212">Repita as etapas 8 e 9 acima para adicionar uma nova classe chamada `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="e3566-212">Repeat steps 8 and 9 above to add a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="e3566-213">Essa classe implementa a estrutura de teste Spark usada para depuração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e3566-213">This class implements the Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="e3566-214">Adicione o código a seguir à classe `RemoteClusterDebugging` .</span><span class="sxs-lookup"><span data-stu-id="e3566-214">Add the following code to the `RemoteClusterDebugging` class.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     <span data-ttu-id="e3566-215">Há dois aspectos importantes a serem observados:</span><span class="sxs-lookup"><span data-stu-id="e3566-215">Couple of important things to note here:</span></span>

   * <span data-ttu-id="e3566-216">Para `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, verifique se o assembly JAR do Spark está disponível no armazenamento de cluster no caminho especificado.</span><span class="sxs-lookup"><span data-stu-id="e3566-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure the Spark assembly JAR is available on the cluster storage at the specified path.</span></span>
   * <span data-ttu-id="e3566-217">Para `setJars`, especifique o local em que o artefato jar será criado.</span><span class="sxs-lookup"><span data-stu-id="e3566-217">For `setJars`, specify the location where the artifact jar will be created.</span></span> <span data-ttu-id="e3566-218">Geralmente, é `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="e3566-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="e3566-219">No `RemoteClusterDebugging` da classe, clique com botão direito do mouse na palavra-chave `test` e selecione **Criar Configuração de RemoteClusterDebugging**.</span><span class="sxs-lookup"><span data-stu-id="e3566-219">In the `RemoteClusterDebugging` class, right-click the `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="e3566-221">Na caixa de diálogo, forneça um nome para a configuração e selecione o **Variante de teste** como **Nome do teste**.</span><span class="sxs-lookup"><span data-stu-id="e3566-221">In the dialog box, provide a name for the configuration, and select the **Test kind** as **Test name**.</span></span> <span data-ttu-id="e3566-222">Deixe todos os outros valores como padrão, clique em **Aplicar** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3566-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="e3566-224">Agora você deve ver uma lista suspensa de configuração **Execução Remota** na barra de menus.</span><span class="sxs-lookup"><span data-stu-id="e3566-224">You should now see a **Remote Run** configuration drop-down in the menu bar.</span></span>

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-the-application-in-debug-mode"></a><span data-ttu-id="e3566-226">Etapa 5: Executar o aplicativo no modo de depuração</span><span class="sxs-lookup"><span data-stu-id="e3566-226">Step 5: Run the application in debug mode</span></span>
1. <span data-ttu-id="e3566-227">No projeto IntelliJ IDEA, abra `SparkSample.scala` e crie um ponto de interrupção ao lado de 'val rdd1'.</span><span class="sxs-lookup"><span data-stu-id="e3566-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next to \`val rdd1'.</span></span> <span data-ttu-id="e3566-228">No menu pop-up para a criação de um ponto de interrupção, selecione **linha na função executeJob**.</span><span class="sxs-lookup"><span data-stu-id="e3566-228">In the pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Adicionar um ponto de interrupção](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="e3566-230">Clique no botão **Execução de Depuração** ao lado da lista suspensa de configuração de **Execução Remota** para iniciar a execução do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3566-230">Click the **Debug Run** button next to the **Remote Run** configuration drop-down to start running the application.</span></span>

    ![Executar o programa no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="e3566-232">Quando a execução do programa atingir o ponto de interrupção, você verá uma guia **Depurador** no painel inferior.</span><span class="sxs-lookup"><span data-stu-id="e3566-232">When the program execution reaches the breakpoint, you should see a **Debugger** tab in the bottom pane.</span></span>

    ![Executar o programa no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="e3566-234">Clique no ícone (**+**) para adicionar uma inspeção, como mostrado na imagem abaixo.</span><span class="sxs-lookup"><span data-stu-id="e3566-234">Click the (**+**) icon to add a watch as shown in the image below.</span></span>

    ![Executar o programa no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="e3566-236">Aqui, como o aplicativo foi interrompido antes da criação da variável `rdd1`, usando essa inspeção conseguimos ver quais eram as cinco primeiras linhas da variável `rdd`.</span><span class="sxs-lookup"><span data-stu-id="e3566-236">Here, because the application broke before the variable `rdd1` was created, using this watch we can see what are the first 5 rows in the variable `rdd`.</span></span> <span data-ttu-id="e3566-237">Pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e3566-237">Press **ENTER**.</span></span>

    ![Executar o programa no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="e3566-239">O que você vê na imagem acima é que, em tempo de execução, você poderia consultar terabytes de dados e de depuração à medida que o aplicativo progride.</span><span class="sxs-lookup"><span data-stu-id="e3566-239">What you see in the image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="e3566-240">Por exemplo, na saída mostrada na imagem acima, você pode ver que a primeira linha da saída é um cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="e3566-240">For example, in the output shown in the image above, you can see that the first row of the output is a header.</span></span> <span data-ttu-id="e3566-241">Com base nisso, você pode modificar o código do aplicativo para ignorar a linha de cabeçalho, se necessário.</span><span class="sxs-lookup"><span data-stu-id="e3566-241">Based on this, you can modify your application code to skip the header row if required.</span></span>
5. <span data-ttu-id="e3566-242">Agora você pode clicar no ícone **Retomar Programa** para prosseguir com o execução do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3566-242">You can now click the **Resume Program** icon to proceed with your application run.</span></span>

    ![Executar o programa no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="e3566-244">Se o aplicativo for concluído com êxito, você verá uma saída semelhante à seguinte.</span><span class="sxs-lookup"><span data-stu-id="e3566-244">If the application completes successfully, you should see an output like the following.</span></span>

    ![Executar o programa no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="e3566-246"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="e3566-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="e3566-247">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3566-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="e3566-248">Demonstração</span><span class="sxs-lookup"><span data-stu-id="e3566-248">Demo</span></span>
* <span data-ttu-id="e3566-249">Criar projeto do Scala (vídeo): [Criar aplicativos Spark Scala](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="e3566-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="e3566-250">Depuração remota (Vídeo): [Usar o kit de ferramentas do Azure para IntelliJ para depurar aplicativos Spark remotamente no cluster HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="e3566-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="e3566-251">Cenários</span><span class="sxs-lookup"><span data-stu-id="e3566-251">Scenarios</span></span>
* [<span data-ttu-id="e3566-252">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="e3566-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e3566-253">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="e3566-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="e3566-254">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para prever resultados da inspeção de alimentos</span><span class="sxs-lookup"><span data-stu-id="e3566-254">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e3566-255">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="e3566-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="e3566-256">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3566-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="e3566-257">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="e3566-257">Create and run applications</span></span>
* [<span data-ttu-id="e3566-258">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="e3566-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e3566-259">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="e3566-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="e3566-260">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="e3566-260">Tools and extensions</span></span>
* [<span data-ttu-id="e3566-261">Usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ para criar e enviar aplicativos Spark Scala</span><span class="sxs-lookup"><span data-stu-id="e3566-261">Use HDInsight Tools in Azure Toolkit for IntelliJ to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e3566-262">Usar o kit de ferramentas do Azure para IntelliJ a fim de depurar aplicativos Spark remotamente por meio do SSH</span><span class="sxs-lookup"><span data-stu-id="e3566-262">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="e3566-263">Usar ferramentas do HDInsight para IntelliJ com a área restrita do Hortonworks</span><span class="sxs-lookup"><span data-stu-id="e3566-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="e3566-264">Usar as Ferramentas do HDInsight no Kit de Ferramentas do Azure para Eclipse para criar aplicativos Spark</span><span class="sxs-lookup"><span data-stu-id="e3566-264">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="e3566-265">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3566-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="e3566-266">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3566-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e3566-267">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="e3566-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="e3566-268">Instalar o Jupyter em seu computador e conectar-se a um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3566-268">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="e3566-269">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="e3566-269">Manage resources</span></span>
* [<span data-ttu-id="e3566-270">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3566-270">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e3566-271">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3566-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
