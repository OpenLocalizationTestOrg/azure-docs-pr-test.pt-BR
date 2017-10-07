---
title: aaaAzure Kit de ferramentas para IntelliJ - depurar aplicativos remotamente no HDInsight Spark | Microsoft Docs
description: Saiba como usar as ferramentas do HDInsight no Kit de ferramentas do Azure para IntelliJ tooremotely depurar aplicativos executados em clusters de HDInsight Spark por meio de vpn.
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
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="a6bfa-103">Use o Kit de ferramentas do Azure para aplicativos de toodebug IntelliJ remotamente no HDInsight Spark por meio de VPN</span><span class="sxs-lookup"><span data-stu-id="a6bfa-103">Use Azure Toolkit for IntelliJ toodebug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="a6bfa-104">Recomendamos a forma de saudação de depuração remotamente por meio de applicaltion spark ssh.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-104">We recommend hello way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="a6bfa-105">Para obter instruções, consulte [Depurar aplicativos Spark remotamente em um cluster HDInsight com o kit de ferramentas do Azure para IntelliJ por meio do SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="a6bfa-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="a6bfa-106">Este artigo fornece orientações passo a passo sobre como toouse hello ferramentas HDInsight no Kit de ferramentas do Azure para IntelliJ toosubmit um trabalho Spark no cluster HDInsight Spark e depurá-lo remotamente de um computador desktop.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-106">This article provides step-by-step guidance on how toouse hello HDInsight Tools in Azure Toolkit for IntelliJ toosubmit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="a6bfa-107">toodo, portanto, você deve executar Olá seguindo as etapas de alto nível:</span><span class="sxs-lookup"><span data-stu-id="a6bfa-107">toodo so, you must perform hello following high-level steps:</span></span>

1. <span data-ttu-id="a6bfa-108">Crie uma Rede Virtual do Azure site a site ou ponto a site.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="a6bfa-109">etapas de saudação neste documento pressupõem que você use uma rede site a site.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-109">hello steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="a6bfa-110">Crie um cluster Spark no HDInsight do Azure que faz parte da saudação-to-site rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-110">Create a Spark cluster in Azure HDInsight that is part of hello site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="a6bfa-111">Verifique a conectividade de saudação entre o nó principal do cluster hello e sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-111">Verify hello connectivity between hello cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="a6bfa-112">Crie um aplicativo Scala no IntelliJ IDEA e configure-o para a depuração remota.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="a6bfa-113">Executar e depurar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-113">Run and debug hello application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6bfa-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a6bfa-114">Prerequisites</span></span>
* <span data-ttu-id="a6bfa-115">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-115">An Azure subscription.</span></span> <span data-ttu-id="a6bfa-116">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a6bfa-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="a6bfa-117">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="a6bfa-118">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="a6bfa-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="a6bfa-119">Kit de desenvolvimento Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-119">Oracle Java Development kit.</span></span> <span data-ttu-id="a6bfa-120">Você pode instalá-lo clicando [aqui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="a6bfa-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="a6bfa-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-121">IntelliJ IDEA.</span></span> <span data-ttu-id="a6bfa-122">Este artigo usa a versão 2017.1.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-122">This article uses version 2017.1.</span></span> <span data-ttu-id="a6bfa-123">Você pode instalá-lo clicando [aqui](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="a6bfa-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="a6bfa-124">Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="a6bfa-125">Ferramentas de HDInsight para IntelliJ estão disponíveis como parte do Kit de ferramentas do Azure para IntelliJ de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-125">HDInsight tools for IntelliJ are available as part of hello Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="a6bfa-126">Para obter instruções sobre como tooinstall Olá Kit de ferramentas do Azure, consulte [Olá instalando o Kit de ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="a6bfa-126">For instructions on how tooinstall hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="a6bfa-127">Faça logon em sua assinatura do Azure no IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="a6bfa-128">Siga as instruções de saudação [aqui](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="a6bfa-128">Follow hello instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="a6bfa-129">Ao executar o aplicativo Scala Spark para depuração remota em um computador Windows, você pode obter uma exceção conforme explicado em [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) que ocorre devido a falta de tooa WinUtils.exe no Windows.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due tooa missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="a6bfa-130">toowork alternativa para esse erro, você deve [baixar Olá executável aqui](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa local como **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-130">toowork around this error, you must [download hello executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="a6bfa-131">Em seguida, você deve adicionar uma variável de ambiente **HADOOP_HOME** e defina o valor de saudação da variável de saudação muito**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-131">You must then add an environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="a6bfa-132">Etapa 1: Criar uma rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="a6bfa-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="a6bfa-133">Siga as instruções de saudação do hello abaixo links toocreate uma rede Virtual do Azure e, em seguida, verifique a conectividade de saudação entre desktop saudação e rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-133">Follow hello instructions from hello below links toocreate an Azure Virtual Network and then verify hello connectivity between hello desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="a6bfa-134">Criar uma Rede Virtual com uma conexão VPN site a site usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a6bfa-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="a6bfa-135">Criar uma Rede Virtual com uma conexão VPN site a site usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6bfa-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="a6bfa-136">Configurar uma rede virtual do tooa conexão ponto a site usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6bfa-136">Configure a point-to-site connection tooa virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="a6bfa-137">Etapa 2: Criar um cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="a6bfa-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="a6bfa-138">Você também deve criar um cluster do Apache Spark no HDInsight do Azure que faz parte da saudação rede Virtual do Azure que você criou.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of hello Azure Virtual Network that you created.</span></span> <span data-ttu-id="a6bfa-139">Use as informações de saudação disponíveis no [baseados em Linux criar clusters de HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a6bfa-139">Use hello information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="a6bfa-140">Como parte da configuração opcional, selecione Olá rede Virtual do Azure que você criou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-140">As part of optional configuration, select hello Azure Virtual Network that you created in hello previous step.</span></span>

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a><span data-ttu-id="a6bfa-141">Etapa 3: Verificar a conectividade de saudação entre o nó principal do cluster hello e sua área de trabalho</span><span class="sxs-lookup"><span data-stu-id="a6bfa-141">Step 3: Verify hello connectivity between hello cluster headnode and your desktop</span></span>
1. <span data-ttu-id="a6bfa-142">Obter endereço IP Olá Olá um nó principal.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-142">Get hello IP address of hello headnode.</span></span> <span data-ttu-id="a6bfa-143">Abra o Ambari UI cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-143">Open Ambari UI for hello cluster.</span></span> <span data-ttu-id="a6bfa-144">Na folha de cluster hello, clique em **painel**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-144">From hello cluster blade, click **Dashboard**.</span></span>

    ![Localizar o IP do nó de cabeçalho](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="a6bfa-146">De Olá Ambari UI, do canto superior direito de saudação, clique em **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-146">From hello Ambari UI, from hello top-right corner, click **Hosts**.</span></span>

    ![Localizar o IP do nó de cabeçalho](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="a6bfa-148">Você deve ver uma lista de nós de cabeçalho, os nós de trabalho e os nós do zookeeper.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="a6bfa-149">Olá headnodes ter Olá **hn*** prefixo.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-149">hello headnodes have hello **hn*** prefix.</span></span> <span data-ttu-id="a6bfa-150">Clique em um nó principal do hello primeiro.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-150">Click hello first headnode.</span></span>

    ![Localizar o IP do nó de cabeçalho](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="a6bfa-152">Final Olá Olá página aberta, de saudação **resumo** caixa de endereço IP hello cópia do nó principal do hello e nome de host de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-152">At hello bottom of hello page that opens, from hello **Summary** box, copy hello IP address of hello headnode and hello host name.</span></span>

    ![Localizar o IP do nó de cabeçalho](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="a6bfa-154">Incluir endereço IP de saudação e nome de host de saudação do Olá um nó principal toohello **hosts** arquivo em computador Olá onde você deseja toorun e depurar remotamente trabalhos do Spark hello.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-154">Include hello IP address and hello host name of hello headnode toohello **hosts** file on hello computer from where you want toorun and remotely debug hello Spark jobs.</span></span> <span data-ttu-id="a6bfa-155">Isso permite que você toocommunicate com hello um nó principal usando endereço IP hello, bem como Olá hostname.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-155">This will enable you toocommunicate with hello headnode using hello IP address as well as hello hostname.</span></span>

   1. <span data-ttu-id="a6bfa-156">Abra um bloco de notas com permissões elevadas.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="a6bfa-157">No menu de arquivo hello, clique em **abrir** e, em seguida, navegue toohello local do arquivo de hosts de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-157">From hello file menu, click **Open** and then navigate toohello location of hello hosts file.</span></span> <span data-ttu-id="a6bfa-158">Em um computador com o Windows, é `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="a6bfa-159">Adicionar Olá após toohello **hosts** arquivo.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-159">Add hello following toohello **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="a6bfa-160">Em computador Olá conectado toohello rede Virtual do Azure que é usado pelo cluster do HDInsight Olá, verifique se você pode executar o ping ambos headnodes hello usando endereço IP hello, bem como Olá hostname.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-160">From hello computer that you connected toohello Azure Virtual Network that is used by hello HDInsight cluster, verify that you can ping both hello headnodes using hello IP address as well as hello hostname.</span></span>
7. <span data-ttu-id="a6bfa-161">SSH em Olá nó principal do cluster usando instruções Olá em [cluster do HDInsight tooan conectar usando o SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a6bfa-161">SSH into hello cluster headnode using hello instructions at [Connect tooan HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="a6bfa-162">Do nó principal do cluster hello, ping endereço IP de saudação do computador desktop saudação.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-162">From hello cluster headnode, ping hello IP address of hello desktop computer.</span></span> <span data-ttu-id="a6bfa-163">Você deve testar conectividade tooboth Olá endereços atribuídos toohello computador, um para a conexão de rede de saudação e Olá para Olá rede Virtual do Azure que Olá computador está conectado.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-163">You should test connectivity tooboth hello IP addresses assigned toohello computer, one for hello network connection and hello other for hello Azure Virtual Network that hello computer is connected to.</span></span>
8. <span data-ttu-id="a6bfa-164">Repita as etapas de Olá Olá também outros um nó principal.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-164">Repeat hello steps for hello other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="a6bfa-165">Etapa 4: Criar um aplicativo de Scala Spark usando ferramentas do HDInsight Olá no Kit de ferramentas do Azure para IntelliJ e configurá-lo para depuração remota</span><span class="sxs-lookup"><span data-stu-id="a6bfa-165">Step 4: Create a Spark Scala application using hello HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="a6bfa-166">Inicie o IntelliJ IDEA e crie um novo projeto.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="a6bfa-167">Na caixa de diálogo projeto novo hello, fazer Olá opções a seguir e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-167">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>

    ![Criar um aplicativo Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="a6bfa-169">No painel esquerdo do hello, selecione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-169">From hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="a6bfa-170">No painel direito da saudação, selecione **Spark no HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-170">From hello right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="a6bfa-171">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-171">Click **Next**.</span></span>
2. <span data-ttu-id="a6bfa-172">Na próxima janela de hello, forneça Olá detalhes de projeto a seguir e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-172">In hello next window, provide hello following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="a6bfa-173">Forneça um nome de projeto e o local do projeto.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="a6bfa-174">Para o **SDK de projeto**, use o Java 1.8 para o cluster do Spark 2.x e o Java 1.7 para o cluster do Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="a6bfa-175">Para a **versão do Spark**, o assistente de criação de projetos Scala integra a versão apropriada do SDK do Spark e do SDK do Scala.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="a6bfa-176">Se a versão do cluster spark Olá for inferior 2.0, escolha despertar 1. x.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-176">If hello spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="a6bfa-177">Caso contrário, você deve selecionar o spark2.x.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="a6bfa-178">Este exemplo usa o Spark 2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="a6bfa-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="a6bfa-179">![Criar um aplicativo Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="a6bfa-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="a6bfa-180">projeto do Spark Olá criará automaticamente um artefato para você.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-180">hello Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="a6bfa-181">artefato de saudação toosee, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-181">toosee hello artifact, follow these steps.</span></span>

   1. <span data-ttu-id="a6bfa-182">De saudação **arquivo** menu, clique em **estrutura do projeto**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-182">From hello **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="a6bfa-183">Em Olá **estrutura do projeto** caixa de diálogo, clique em **artefatos** toosee artefato de padrão de saudação que é criado.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-183">In hello **Project Structure** dialog box, click **Artifacts** toosee hello default artifact that is created.</span></span>
   <span data-ttu-id="a6bfa-184">![Criar JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="a6bfa-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="a6bfa-185">Você também pode criar seu próprios artefato bly clicando em Olá  **+**  ícone, realçado na imagem de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-185">You can also create your own artifact bly clicking on hello **+** icon, highlighted in hello image above.</span></span>

4. <span data-ttu-id="a6bfa-186">Adicione projeto de tooyour de bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-186">Add libraries tooyour project.</span></span> <span data-ttu-id="a6bfa-187">tooadd uma biblioteca, clique no nome do projeto Olá na árvore de projeto Olá e clique **abrir configurações de módulo**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-187">tooadd a library, right-click hello project name in hello project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="a6bfa-188">Em Olá **estrutura do projeto** caixa de diálogo, no painel esquerdo do hello, clique em **bibliotecas**, clique o símbolo de saudação (+) e, em seguida, clique em **do Maven**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-188">In hello **Project Structure** dialog box, from hello left pane, click **Libraries**, click hello (+) symbol, and then click **From Maven**.</span></span>

    ![Adicionar biblioteca](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="a6bfa-190">Em Olá **baixar a biblioteca do repositório Maven** caixa de diálogo caixa, pesquisar e adicionar Olá bibliotecas a seguir.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-190">In hello **Download Library from Maven Repository** dialog box, search and add hello following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="a6bfa-191">Cópia `yarn-site.xml` e `core-site.xml` de saudação um nó principal do cluster e adicioná-lo toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-191">Copy `yarn-site.xml` and `core-site.xml` from hello cluster headnode and add it toohello project.</span></span> <span data-ttu-id="a6bfa-192">Use Olá seguintes comandos toocopy Olá arquivos.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-192">Use hello following commands toocopy hello files.</span></span> <span data-ttu-id="a6bfa-193">Você pode usar [Cygwin](https://cygwin.com/install.html) a seguir Olá toorun `scp` comandos toocopy arquivos Olá Olá headnodes de cluster.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-193">You can use [Cygwin](https://cygwin.com/install.html) toorun hello following `scp` commands toocopy hello files from hello cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="a6bfa-194">Porque estamos já adicionado Olá cluster um nó principal IP endereços e nomes de host fo Olá arquivo hosts na área de trabalho hello, podemos usar Olá **scp** comandos Olá maneira a seguir.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-194">Because we already added hello cluster headnode IP address and hostnames fo hello hosts file on hello desktop, we can use hello **scp** commands in hello following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="a6bfa-195">Adicionar esses arquivos de projeto tooyour copiando-os em Olá **/src** pasta na árvore do projeto, por exemplo `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-195">Add these files tooyour project by copying them under hello **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="a6bfa-196">Saudação de atualização `core-site.xml` toomake Olá alterações a seguir.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-196">Update hello `core-site.xml` toomake hello following changes.</span></span>

   1. <span data-ttu-id="a6bfa-197">`core-site.xml`inclui a conta de armazenamento de chave toohello Olá criptografado associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-197">`core-site.xml` includes hello encrypted key toohello storage account associated with hello cluster.</span></span> <span data-ttu-id="a6bfa-198">Em Olá `core-site.xml` que você adicionou o projeto toohello, Olá de substituir chave criptografada com a chave de armazenamento real Olá associada à conta de armazenamento padrão hello.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-198">In hello `core-site.xml` that you added toohello project, replace hello encrypted key with hello actual storage key associated with hello default storage account.</span></span> <span data-ttu-id="a6bfa-199">Confira [Gerenciar as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="a6bfa-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="a6bfa-200">Remover Olá seguindo as entradas da saudação `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-200">Remove hello following entries from hello `core-site.xml`.</span></span>

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
   3. <span data-ttu-id="a6bfa-201">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-201">Save hello file.</span></span>
7. <span data-ttu-id="a6bfa-202">Adicione classe principal de saudação para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-202">Add hello Main class for your application.</span></span> <span data-ttu-id="a6bfa-203">De saudação **Explorador de projeto**, clique com botão direito **src**, ponto muito**novo**e, em seguida, clique em **Scala classe**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-203">From hello **Project Explorer**, right-click **src**, point too**New**, and then click **Scala class**.</span></span>

    ![Adicionar código-fonte](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="a6bfa-205">Em Olá **criar nova classe Scala** caixa de diálogo caixa, forneça um nome para **tipo** selecione **objeto**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-205">In hello **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Adicionar código-fonte](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="a6bfa-207">Em Olá `MyClusterAppMain.scala` de arquivo, cole Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-207">In hello `MyClusterAppMain.scala` file, paste hello following code.</span></span> <span data-ttu-id="a6bfa-208">Esse código cria um contexto de Spark hello e inicia um `executeJob` método da saudação `SparkSample` objeto.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-208">This code creates hello Spark context and launches an `executeJob` method from hello `SparkSample` object.</span></span>

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

10. <span data-ttu-id="a6bfa-209">Repita as etapas 8 e 9 acima tooadd um novo objeto Scala chamado `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-209">Repeat steps 8 and 9 above tooadd a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="a6bfa-210">classe toothis adicionar Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-210">toothis class add hello following code.</span></span> <span data-ttu-id="a6bfa-211">Esse código lê dados de saudação de saudação HVAC.csv (disponível em todos os clusters de HDInsight Spark), recupera linhas de saudação que têm apenas um dígito na coluna sétima Olá Olá CSV e grava a saída de hello muito**/HVACOut** em padrão Olá contêiner de armazenamento de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-211">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello seventh column in hello CSV, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="a6bfa-212">Repita as etapas 8 e 9 acima tooadd uma nova classe chamada `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-212">Repeat steps 8 and 9 above tooadd a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="a6bfa-213">Essa classe implementa uma estrutura de teste do Spark Olá é usada para depurar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-213">This class implements hello Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="a6bfa-214">Adicionar Olá toohello de código a seguir `RemoteClusterDebugging` classe.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-214">Add hello following code toohello `RemoteClusterDebugging` class.</span></span>

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

     <span data-ttu-id="a6bfa-215">Algumas coisas importantes toonote aqui:</span><span class="sxs-lookup"><span data-stu-id="a6bfa-215">Couple of important things toonote here:</span></span>

   * <span data-ttu-id="a6bfa-216">Para `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, certifique-se de saudação assembly Spark JAR está disponível no armazenamento de cluster Olá no caminho especificado hello.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure hello Spark assembly JAR is available on hello cluster storage at hello specified path.</span></span>
   * <span data-ttu-id="a6bfa-217">Para `setJars`, especifique Olá local onde jar do artefato Olá será criado.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-217">For `setJars`, specify hello location where hello artifact jar will be created.</span></span> <span data-ttu-id="a6bfa-218">Geralmente, é `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="a6bfa-219">Em Olá `RemoteClusterDebugging` da classe, clique com botão direito Olá `test` palavra-chave e selecione **criar RemoteClusterDebugging configuração**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-219">In hello `RemoteClusterDebugging` class, right-click hello `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="a6bfa-221">Na caixa de diálogo hello, forneça um nome para a configuração de saudação e selecione Olá **teste tipo** como **nome do teste**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-221">In hello dialog box, provide a name for hello configuration, and select hello **Test kind** as **Test name**.</span></span> <span data-ttu-id="a6bfa-222">Deixe todos os outros valores como padrão, clique em **Aplicar** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="a6bfa-224">Agora você deve ver uma **remoto executar** configuração suspensa na barra de menus do hello.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-224">You should now see a **Remote Run** configuration drop-down in hello menu bar.</span></span>

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a><span data-ttu-id="a6bfa-226">Etapa 5: Executar aplicativo hello no modo de depuração</span><span class="sxs-lookup"><span data-stu-id="a6bfa-226">Step 5: Run hello application in debug mode</span></span>
1. <span data-ttu-id="a6bfa-227">No seu projeto IntelliJ IDEIA, abra `SparkSample.scala` e criar um rdd1 de too'val próximo ponto de interrupção '.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next too\`val rdd1'.</span></span> <span data-ttu-id="a6bfa-228">No menu pop-up de saudação para a criação de um ponto de interrupção, selecione **linha na função executeJob**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-228">In hello pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Adicionar um ponto de interrupção](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="a6bfa-230">Clique em Olá **depurar executar** toohello próximo botão **remoto executar** toostart de lista suspensa de configuração executando o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-230">Click hello **Debug Run** button next toohello **Remote Run** configuration drop-down toostart running hello application.</span></span>

    ![Execute o programa de saudação no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="a6bfa-232">Quando a execução do programa hello atinge o ponto de interrupção hello, você verá um **depurador** guia no painel inferior de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-232">When hello program execution reaches hello breakpoint, you should see a **Debugger** tab in hello bottom pane.</span></span>

    ![Execute o programa de saudação no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="a6bfa-234">Clique em hello (**+**) ícone tooadd uma inspeção conforme mostrado na imagem de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-234">Click hello (**+**) icon tooadd a watch as shown in hello image below.</span></span>

    ![Execute o programa de saudação no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="a6bfa-236">Aqui, porque o aplicativo hello rompeu antes de variável Olá `rdd1` foi criado com essa inspeção podemos ver quais são Olá primeiras 5 linhas na variável de saudação `rdd`.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-236">Here, because hello application broke before hello variable `rdd1` was created, using this watch we can see what are hello first 5 rows in hello variable `rdd`.</span></span> <span data-ttu-id="a6bfa-237">Pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-237">Press **ENTER**.</span></span>

    ![Execute o programa de saudação no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="a6bfa-239">O que você vê na imagem de saudação acima é que, em tempo de execução, você poderia consultar terabytes de dados e de depuração como seu aplicativo avança.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-239">What you see in hello image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="a6bfa-240">Por exemplo, na saída de hello mostrada na imagem de saudação acima, você pode ver que Olá primeira linha da saída de hello é um cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-240">For example, in hello output shown in hello image above, you can see that hello first row of hello output is a header.</span></span> <span data-ttu-id="a6bfa-241">Com base nisso, você pode modificar a linha de cabeçalho do aplicativo código tooskip Olá se necessário.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-241">Based on this, you can modify your application code tooskip hello header row if required.</span></span>
5. <span data-ttu-id="a6bfa-242">Agora você pode clicar Olá **retomar programa** ícone tooproceed com seu aplicativo seja executado.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-242">You can now click hello **Resume Program** icon tooproceed with your application run.</span></span>

    ![Execute o programa de saudação no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="a6bfa-244">Se o aplicativo hello for concluído com êxito, você verá uma saída semelhante Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="a6bfa-244">If hello application completes successfully, you should see an output like hello following.</span></span>

    ![Execute o programa de saudação no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="a6bfa-246"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="a6bfa-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="a6bfa-247">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a6bfa-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="a6bfa-248">Demonstração</span><span class="sxs-lookup"><span data-stu-id="a6bfa-248">Demo</span></span>
* <span data-ttu-id="a6bfa-249">Criar projeto do Scala (vídeo): [Criar aplicativos Spark Scala](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="a6bfa-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="a6bfa-250">Depuração remota (vídeo): [Kit de ferramentas do uso do Azure para aplicativos de Spark toodebug IntelliJ remotamente no HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="a6bfa-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="a6bfa-251">Cenários</span><span class="sxs-lookup"><span data-stu-id="a6bfa-251">Scenarios</span></span>
* [<span data-ttu-id="a6bfa-252">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="a6bfa-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="a6bfa-253">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="a6bfa-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="a6bfa-254">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="a6bfa-254">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="a6bfa-255">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="a6bfa-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="a6bfa-256">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="a6bfa-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="a6bfa-257">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="a6bfa-257">Create and run applications</span></span>
* [<span data-ttu-id="a6bfa-258">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="a6bfa-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="a6bfa-259">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="a6bfa-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="a6bfa-260">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="a6bfa-260">Tools and extensions</span></span>
* [<span data-ttu-id="a6bfa-261">Usar as ferramentas do HDInsight no Kit de ferramentas do Azure para IntelliJ toocreate e enviar maiores Spark Scala aplicativos</span><span class="sxs-lookup"><span data-stu-id="a6bfa-261">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="a6bfa-262">Use o Kit de ferramentas do Azure para aplicativos de Spark toodebug IntelliJ remotamente por meio do SSH</span><span class="sxs-lookup"><span data-stu-id="a6bfa-262">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="a6bfa-263">Usar ferramentas do HDInsight para IntelliJ com a área restrita do Hortonworks</span><span class="sxs-lookup"><span data-stu-id="a6bfa-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="a6bfa-264">Use as ferramentas do HDInsight no Kit de ferramentas do Azure para aplicativos do Eclipse toocreate Spark</span><span class="sxs-lookup"><span data-stu-id="a6bfa-264">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="a6bfa-265">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="a6bfa-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="a6bfa-266">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="a6bfa-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="a6bfa-267">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="a6bfa-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="a6bfa-268">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="a6bfa-268">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="a6bfa-269">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="a6bfa-269">Manage resources</span></span>
* [<span data-ttu-id="a6bfa-270">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="a6bfa-270">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="a6bfa-271">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="a6bfa-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
