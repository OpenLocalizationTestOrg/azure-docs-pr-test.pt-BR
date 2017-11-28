---
title: Executar trabalhos do Apache Sqoop com o Azure HDInsight (Hadoop) | Microsoft Docs
description: "Saiba como usar o PowerShell do Azure em uma estação de trabalho para executar importação e exportação do Sqoop entre um cluster do Hadoop e um Banco de Dados SQL do Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 8e77153493b6f37f5f48116b86bad6b25a50d1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="60a69-103">Use Sqoop com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="60a69-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="60a69-104">Saiba como usar o Sqoop no HDInsight para importar e exportar entre um cluster HDInsight e um banco de dados Azure SQL ou banco de dados SQL Server.</span><span class="sxs-lookup"><span data-stu-id="60a69-104">Learn how to use Sqoop in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="60a69-105">Embora o Hadoop seja uma opção natural para o processamento de dados semiestruturados e não estruturados, como logs e arquivos, também pode ser necessário processar dados estruturados armazenados em bancos de dados relacionais.</span><span class="sxs-lookup"><span data-stu-id="60a69-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="60a69-106">O [Sqoop][sqoop-user-guide-1.4.4] é uma ferramenta desenvolvida para transferir dados entre clusters Hadoop e bancos de dados relacionais.</span><span class="sxs-lookup"><span data-stu-id="60a69-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed to transfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="60a69-107">Você pode usá-lo para importar dados de um RDBMS (sistema de gerenciamento de banco de dados relacional), como SQL ou MySQL ou Oracle para o HDFS (Sistema de Arquivos Distribuído) do Hadoop, transformar os dados no Hadoop com MapReduce ou Hive e, em seguida, exportar os dados de volta para um RDBMS.</span><span class="sxs-lookup"><span data-stu-id="60a69-107">You can use it to import data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span> <span data-ttu-id="60a69-108">Neste tutorial, você está usando um Banco de Dados SQL como seu banco de dados relacional.</span><span class="sxs-lookup"><span data-stu-id="60a69-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="60a69-109">Para as versões do Sqoop com suporte em clusters HDInsight, confira [Novidades nas versões de clusters fornecidas pelo HDInsight?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="60a69-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-the-scenario"></a><span data-ttu-id="60a69-110">Compreender o cenário</span><span class="sxs-lookup"><span data-stu-id="60a69-110">Understand the scenario</span></span>

<span data-ttu-id="60a69-111">O cluster HDInsight é fornecido com alguns dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="60a69-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="60a69-112">Você usa estas duas amostras:</span><span class="sxs-lookup"><span data-stu-id="60a69-112">You use the following two samples:</span></span>

* <span data-ttu-id="60a69-113">Um arquivo de log log4j localizado em */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="60a69-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="60a69-114">Os seguintes logs são extraídos do arquivo:</span><span class="sxs-lookup"><span data-stu-id="60a69-114">The following logs are extracted from the file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="60a69-115">Uma tabela Hive chamada *hivesampletable*, que faz referência ao arquivo de dados localizado em */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="60a69-115">A Hive table named *hivesampletable*, which references the data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="60a69-116">A tabela contém alguns dados de dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="60a69-116">The table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="60a69-117">Campo</span><span class="sxs-lookup"><span data-stu-id="60a69-117">Field</span></span> | <span data-ttu-id="60a69-118">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="60a69-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="60a69-119">clientid</span><span class="sxs-lookup"><span data-stu-id="60a69-119">clientid</span></span> |<span data-ttu-id="60a69-120">string</span><span class="sxs-lookup"><span data-stu-id="60a69-120">string</span></span> |
  | <span data-ttu-id="60a69-121">querytime</span><span class="sxs-lookup"><span data-stu-id="60a69-121">querytime</span></span> |<span data-ttu-id="60a69-122">string</span><span class="sxs-lookup"><span data-stu-id="60a69-122">string</span></span> |
  | <span data-ttu-id="60a69-123">market</span><span class="sxs-lookup"><span data-stu-id="60a69-123">market</span></span> |<span data-ttu-id="60a69-124">string</span><span class="sxs-lookup"><span data-stu-id="60a69-124">string</span></span> |
  | <span data-ttu-id="60a69-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="60a69-125">deviceplatform</span></span> |<span data-ttu-id="60a69-126">string</span><span class="sxs-lookup"><span data-stu-id="60a69-126">string</span></span> |
  | <span data-ttu-id="60a69-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="60a69-127">devicemake</span></span> |<span data-ttu-id="60a69-128">string</span><span class="sxs-lookup"><span data-stu-id="60a69-128">string</span></span> |
  | <span data-ttu-id="60a69-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="60a69-129">devicemodel</span></span> |<span data-ttu-id="60a69-130">string</span><span class="sxs-lookup"><span data-stu-id="60a69-130">string</span></span> |
  | <span data-ttu-id="60a69-131">state</span><span class="sxs-lookup"><span data-stu-id="60a69-131">state</span></span> |<span data-ttu-id="60a69-132">string</span><span class="sxs-lookup"><span data-stu-id="60a69-132">string</span></span> |
  | <span data-ttu-id="60a69-133">country</span><span class="sxs-lookup"><span data-stu-id="60a69-133">country</span></span> |<span data-ttu-id="60a69-134">string</span><span class="sxs-lookup"><span data-stu-id="60a69-134">string</span></span> |
  | <span data-ttu-id="60a69-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="60a69-135">querydwelltime</span></span> |<span data-ttu-id="60a69-136">double</span><span class="sxs-lookup"><span data-stu-id="60a69-136">double</span></span> |
  | <span data-ttu-id="60a69-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="60a69-137">sessionid</span></span> |<span data-ttu-id="60a69-138">bigint</span><span class="sxs-lookup"><span data-stu-id="60a69-138">bigint</span></span> |
  | <span data-ttu-id="60a69-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="60a69-139">sessionpagevieworder</span></span> |<span data-ttu-id="60a69-140">bigint</span><span class="sxs-lookup"><span data-stu-id="60a69-140">bigint</span></span> |

<span data-ttu-id="60a69-141">Primeiro, você exporta o *sample.log* e a *hivesampletable* para o banco de dados SQL do Azure ou SQL Server e, em seguida, importa a tabela que contém os dados de dispositivos móveis de volta para o HDInsight usando o seguinte caminho:</span><span class="sxs-lookup"><span data-stu-id="60a69-141">First, you export *sample.log* and *hivesampletable* to the Azure SQL database or to SQL Server, and then import the table that contains the mobile device data back to HDInsight by using the following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="60a69-142">Criar o cluster e o Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="60a69-142">Create cluster and SQL database</span></span>
<span data-ttu-id="60a69-143">Esta seção mostra como criar um cluster, um Banco de Dados SQL e os esquemas do Banco de Dados SQL para executar o tutorial usando o Portal do Azure e um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="60a69-143">This section shows you how to create a cluster, a SQL Database, and the SQL database schemas for running the tutorial using the Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="60a69-144">O modelo pode ser encontrado em [Modelos de Início Rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="60a69-144">The template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="60a69-145">O modelo do Resource Manager chama um pacote bacpac para implantar os esquemas de tabela no Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="60a69-145">The Resource Manager template calls a bacpac package to deploy the table schemas to SQL database.</span></span>  <span data-ttu-id="60a69-146">O pacote bacpac está localizado em um contêiner de blob público, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="60a69-146">The bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="60a69-147">Se você quiser usar um contêiner particular para os arquivos bacpac, use os seguintes valores no modelo:</span><span class="sxs-lookup"><span data-stu-id="60a69-147">If you want to use a private container for the bacpac files, use the following values in the template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="60a69-148">Se você preferir usar o Azure PowerShell para criar o cluster e o Banco de Dados SQL, veja o [Apêndice A](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="60a69-148">If you prefer to use Azure PowerShell to create the cluster and the SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="60a69-149">Clique na imagem a seguir para abrir um modelo do Resource Manager no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-149">Click the following image to open a Resource Manager template in the Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy to Azure"></a>
   

2. <span data-ttu-id="60a69-150">Insira as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="60a69-150">Enter the following properties:</span></span>

    - <span data-ttu-id="60a69-151">**Subscription:** insira sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="60a69-152">**Grupo de Recursos**: crie um novo grupo de recursos do Azure ou escolha um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="60a69-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="60a69-153">Um grupo de recursos é para fins de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="60a69-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="60a69-154">Ele é um contêiner para objetos.</span><span class="sxs-lookup"><span data-stu-id="60a69-154">It is a container for objects.</span></span>
    - <span data-ttu-id="60a69-155">**Localização**: selecione uma região.</span><span class="sxs-lookup"><span data-stu-id="60a69-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="60a69-156">**ClusterName**: insira um nome para o cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="60a69-156">**ClusterName**: Enter a name for the Hadoop cluster.</span></span>
    - <span data-ttu-id="60a69-157">**Nome e senha de logon do cluster**: o nome de logon padrão é admin.</span><span class="sxs-lookup"><span data-stu-id="60a69-157">**Cluster login name and password**: The default login name is admin.</span></span>
    - <span data-ttu-id="60a69-158">**Nome de usuário e senha de SSH**.</span><span class="sxs-lookup"><span data-stu-id="60a69-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="60a69-159">**Nome de logon e senha do servidor de banco de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="60a69-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="60a69-160">**local de _artifacts**: use o valor padrão, a menos que você deseje usar seu próprio arquivo backpac em um local diferente.</span><span class="sxs-lookup"><span data-stu-id="60a69-160">**_artifacts Location**: Use the default value unless you want to use your own backpac file in a different location.</span></span>
    - <span data-ttu-id="60a69-161">**Token Sas do local de_artifacts**: deixe-o em branco.</span><span class="sxs-lookup"><span data-stu-id="60a69-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="60a69-162">**Nome do Arquivo Bacpac**: use o valor padrão, a menos que você deseje usar seu próprio arquivo bacpac.</span><span class="sxs-lookup"><span data-stu-id="60a69-162">**Bacpac File Name**: Use the default value unless you want to use your own backpac file.</span></span>
     
     <span data-ttu-id="60a69-163">Os seguintes valores estão codificados na seção de variáveis:</span><span class="sxs-lookup"><span data-stu-id="60a69-163">The following values are hardcoded in the variables section:</span></span>
     
     | <span data-ttu-id="60a69-164">Nome da conta de armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="60a69-164">Default storage account name</span></span> | <span data-ttu-id="60a69-165"><CluterName>repositório</span><span class="sxs-lookup"><span data-stu-id="60a69-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="60a69-166">Nome do servidor de banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-166">Azure SQL database server name</span></span> |<span data-ttu-id="60a69-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="60a69-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="60a69-168">Nome do banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="60a69-168">Azure SQL database name</span></span> |<span data-ttu-id="60a69-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="60a69-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="60a69-170">Anote esses valores.</span><span class="sxs-lookup"><span data-stu-id="60a69-170">Please write down these values.</span></span>  <span data-ttu-id="60a69-171">Você precisará deles mais tarde no tutorial.</span><span class="sxs-lookup"><span data-stu-id="60a69-171">You need them later in the tutorial.</span></span>

<span data-ttu-id="60a69-172">3. Clique em **OK** para salvar os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="60a69-172">3.Click **OK** to save the parameters.</span></span>

<span data-ttu-id="60a69-173">4. Na folha **Implantação personalizada**, clique na caixa suspensa **Grupo de recursos** e depois em **Novo** para criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="60a69-173">4.From the **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** to create a new resource group.</span></span> <span data-ttu-id="60a69-174">O grupo de recursos é um contêiner que agrupa o cluster, a conta de armazenamento dependente e outros recursos vinculados.</span><span class="sxs-lookup"><span data-stu-id="60a69-174">The resource group is a container that groups the cluster, the dependent storage account and other linked resource.</span></span>

<span data-ttu-id="60a69-175">5. Clique em **Termos legais** e em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="60a69-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="60a69-176">6. Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="60a69-176">6.Click **Create**.</span></span> <span data-ttu-id="60a69-177">Você poderá ver um novo bloco intitulado Como enviar a implantação para a implantação do modelo.</span><span class="sxs-lookup"><span data-stu-id="60a69-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="60a69-178">É preciso sobre cerca de 20 minutos para criar o cluster e o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="60a69-178">It takes about around 20 minutes to create the cluster and SQL database.</span></span>

<span data-ttu-id="60a69-179">Se você optar por usar o banco de dados SQL do Azure existente ou o Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="60a69-179">If you choose to use existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="60a69-180">**Banco de Dados SQL do Azure**: você deve configurar uma regra de firewall para o servidor de Banco de Dados SQL para permitir o acesso de sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="60a69-180">**Azure SQL database**: You must configure a firewall rule for the Azure SQL database server to allow access from your workstation.</span></span> <span data-ttu-id="60a69-181">Para obter instruções de como criar um Banco de Dados SQL do Azure e configurar o firewall, confira [Introdução ao uso do Banco de Dados SQL do Azure][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="60a69-181">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="60a69-182">Por padrão, um banco de dados SQL do Azure permite conexões de serviços do Azure, como o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60a69-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="60a69-183">Se essa configuração de firewall estiver desabilitada, você precisa habilitá-la no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-183">If this firewall setting is disabled, you need to enable it from the Azure portal.</span></span> <span data-ttu-id="60a69-184">Para obter instruções sobre como criar um Banco de Dados SQL do Azure e configurar as regras de firewall, confira [Criar e configurar o Banco de Dados SQL][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="60a69-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="60a69-185">**Servidor SQL**: se o cluster HDInsight estiver na mesma rede virtual do Azure que um SQL Server, você pode usar as etapas neste artigo para importar e exportar dados para um banco de dados SQL Server.</span><span class="sxs-lookup"><span data-stu-id="60a69-185">**SQL Server**: If your HDInsight cluster is on the same virtual network in Azure as SQL Server, you can use the steps in this article to import and export data to a SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="60a69-186">O Azure HDInsight oferece suporte somente a redes virtuais baseadas no local, e não trabalha atualmente com redes virtuais baseadas em grupos de afinidade.</span><span class="sxs-lookup"><span data-stu-id="60a69-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="60a69-187">Para criar e configurar uma rede virtual, confira [Criar uma Rede Virtual usando o portal do Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="60a69-187">To create and configure a virtual network, see [Create a virtual network using the Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="60a69-188">Ao usar o SQL Server no datacenter, você deve configurar a rede virtual como *site a site* ou *ponto a site*.</span><span class="sxs-lookup"><span data-stu-id="60a69-188">When you are using SQL Server in your datacenter, you must configure the virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="60a69-189">Para redes virtuais **ponto a site**, o SQL Server deve estar executando o aplicativo de configuração do cliente VPN, que está disponível no **Painel** da configuração da rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-189">For **point-to-site** virtual networks, SQL Server must be running the VPN client configuration application, which is available from the **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="60a69-190">Ao usar o SQL Server em uma Máquina Virtual do Azure, qualquer configuração de rede virtual pode ser usada, desde que a máquina virtual que hospeda o SQL Server seja membro da mesma rede virtual que o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60a69-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if the virtual machine hosting SQL Server is a member of the same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="60a69-191">Para criar um cluster HDInsight em uma rede virtual, confira [Criar clusters Hadoop no HDInsight usando opções de personalização](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="60a69-191">To create an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="60a69-192">O SQL Server também deve permitir autenticação.</span><span class="sxs-lookup"><span data-stu-id="60a69-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="60a69-193">Você deve usar um logon do SQL Server para as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="60a69-193">You must use a SQL Server login to complete the steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="60a69-194">Executar trabalhos do Sqoop</span><span class="sxs-lookup"><span data-stu-id="60a69-194">Run Sqoop jobs</span></span>
<span data-ttu-id="60a69-195">O HDInsight pode executar trabalhos do Sqoop usando vários métodos.</span><span class="sxs-lookup"><span data-stu-id="60a69-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="60a69-196">Use a tabela a seguir para decidir qual método é o melhor para você e siga o link para obter o passo-a-passo.</span><span class="sxs-lookup"><span data-stu-id="60a69-196">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="60a69-197">**Use** se quiser...</span><span class="sxs-lookup"><span data-stu-id="60a69-197">**Use this** if you want...</span></span> | <span data-ttu-id="60a69-198">...um shell **interativo**</span><span class="sxs-lookup"><span data-stu-id="60a69-198">...an **interactive** shell</span></span> | <span data-ttu-id="60a69-199">...Processamento em**lotes**</span><span class="sxs-lookup"><span data-stu-id="60a69-199">...**batch** processing</span></span> | <span data-ttu-id="60a69-200">... com esse **sistema operacional de cluster**</span><span class="sxs-lookup"><span data-stu-id="60a69-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="60a69-201">... desse **sistema operacional cliente**</span><span class="sxs-lookup"><span data-stu-id="60a69-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="60a69-202">SSH</span><span class="sxs-lookup"><span data-stu-id="60a69-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="60a69-203">✔</span><span class="sxs-lookup"><span data-stu-id="60a69-203">✔</span></span> |<span data-ttu-id="60a69-204">✔</span><span class="sxs-lookup"><span data-stu-id="60a69-204">✔</span></span> |<span data-ttu-id="60a69-205">Linux</span><span class="sxs-lookup"><span data-stu-id="60a69-205">Linux</span></span> |<span data-ttu-id="60a69-206">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="60a69-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="60a69-207">SDK .NET para Hadoop</span><span class="sxs-lookup"><span data-stu-id="60a69-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="60a69-208">✔</span><span class="sxs-lookup"><span data-stu-id="60a69-208">✔</span></span> |<span data-ttu-id="60a69-209">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="60a69-209">Linux or Windows</span></span> |<span data-ttu-id="60a69-210">Windows (por enquanto)</span><span class="sxs-lookup"><span data-stu-id="60a69-210">Windows (for now)</span></span> |
| [<span data-ttu-id="60a69-211">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="60a69-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="60a69-212">✔</span><span class="sxs-lookup"><span data-stu-id="60a69-212">✔</span></span> |<span data-ttu-id="60a69-213">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="60a69-213">Linux or Windows</span></span> |<span data-ttu-id="60a69-214">Windows</span><span class="sxs-lookup"><span data-stu-id="60a69-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="60a69-215">Limitações</span><span class="sxs-lookup"><span data-stu-id="60a69-215">Limitations</span></span>
* <span data-ttu-id="60a69-216">Exportação em massa — com HDInsight baseado em Linux, o conector Sqoop usado para exportar dados no Microsoft SQL Server ou no Banco de Dados SQL do Azure, atualmente, não permite inserções em massa.</span><span class="sxs-lookup"><span data-stu-id="60a69-216">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="60a69-217">Envio em lote — Com HDInsight baseado em Linux, ao usar o comutador `-batch` ao executar inserções, o Sqoop realizará várias inserções em vez de operações de inserção em lotes.</span><span class="sxs-lookup"><span data-stu-id="60a69-217">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60a69-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60a69-218">Next steps</span></span>
<span data-ttu-id="60a69-219">Você aprendeu como usar Sqoop.</span><span class="sxs-lookup"><span data-stu-id="60a69-219">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="60a69-220">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="60a69-220">To learn more, see:</span></span>

* [<span data-ttu-id="60a69-221">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="60a69-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="60a69-222">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="60a69-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="60a69-223">[Usar o Oozie com o HDInsight][hdinsight-use-oozie]: use a ação do Sqoop no fluxo de trabalho do Oozie.</span><span class="sxs-lookup"><span data-stu-id="60a69-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="60a69-224">[Analisar dados de atraso de voos usando o HDInsight][hdinsight-analyze-flight-data]: use o Hive para analisar dados de atraso de voos e o Sqoop para exportar os dados para o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="60a69-225">[Carregar dados no HDInsight][hdinsight-upload-data]: localize outros métodos de carregamento de dados no HDInsight/Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-225">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="60a69-226">Apêndice A - um exemplo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="60a69-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="60a69-227">O exemplo do PowerShell executa as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="60a69-227">The PowerShell sample performs the following steps:</span></span>

1. <span data-ttu-id="60a69-228">Conecte-se ao Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-228">Connect to Azure.</span></span>
2. <span data-ttu-id="60a69-229">Crie um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-229">Create an Azure resource group.</span></span> <span data-ttu-id="60a69-230">Para obter mais informações, consulte [Usando o PowerShell do Azure com o Gerenciador de Recursos do Azure](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="60a69-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="60a69-231">Crie um servidor de Banco de Dados SQL do Azure, um banco de dados SQL do Azure e duas tabelas.</span><span class="sxs-lookup"><span data-stu-id="60a69-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="60a69-232">Se, em vez disso, você usar o SQL Server, use as seguintes instruções para criar as tabelas:</span><span class="sxs-lookup"><span data-stu-id="60a69-232">If you use SQL Server instead, use the following statements to create the tables:</span></span>
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    <span data-ttu-id="60a69-233">A maneira mais fácil de examinar as tabelas e o banco de dados é usar o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60a69-233">The easiest way to examine the database and tables is to use Visual Studio.</span></span> <span data-ttu-id="60a69-234">O servidor de banco de dados e o banco de dados podem ser examinados pelo portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-234">The database server and the database can be examined using the Azure portal.</span></span>
4. <span data-ttu-id="60a69-235">Crie um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60a69-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="60a69-236">Para examinar o cluster, você pode usar o portal do Azure ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60a69-236">To examine the cluster, you can use the Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="60a69-237">Pré-processe o arquivo de dados de origem.</span><span class="sxs-lookup"><span data-stu-id="60a69-237">Pre-process the source data file.</span></span>
   
    <span data-ttu-id="60a69-238">Neste tutorial, você exporta um arquivo de log log4j (um arquivo delimitado) e uma tabela Hive para o banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table to an Azure SQL database.</span></span> <span data-ttu-id="60a69-239">O arquivo delimitado é */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="60a69-239">The delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="60a69-240">No início do tutorial, você vê alguns exemplos de logs de log4j.</span><span class="sxs-lookup"><span data-stu-id="60a69-240">Earlier in the tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="60a69-241">No arquivo de log, há algumas linhas vazias e algumas outras linhas semelhantes a:</span><span class="sxs-lookup"><span data-stu-id="60a69-241">In the log file, there are some empty lines and some lines similar to these:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="60a69-242">Isso está correto para outros exemplos que usam esses dados, mas é preciso remover essas exceções antes de ser possível importar para o banco de dados SQL do Azure ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="60a69-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into the Azure SQL database or SQL Server.</span></span> <span data-ttu-id="60a69-243">Haverá falha na exportação do Sqoop se houver uma cadeia de caracteres vazia ou uma linha com um número menor de elementos que o número de campos definidos na tabela do banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than the number of fields defined in the Azure SQL database table.</span></span> <span data-ttu-id="60a69-244">A tabela log4jlogs contém sete campos de tipo de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60a69-244">The log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="60a69-245">Este procedimento cria um novo arquivo no cluster: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="60a69-245">This procedure creates a new file on the cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="60a69-246">Para examinar o arquivo de dados modificado, você pode usar o Portal do Azure, uma ferramenta de exploração do Armazenamento do Azure ou o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-246">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="60a69-247">A [Introdução ao HDInsight][hdinsight-get-started] tem um exemplo de código sobre como usar o Azure PowerShell para baixar um arquivo e exibir o conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="60a69-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell to download a file and display the file content.</span></span>
6. <span data-ttu-id="60a69-248">Exporte um arquivo de dados para o banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-248">Export a data file to the Azure SQL database.</span></span>
   
    <span data-ttu-id="60a69-249">O arquivo de origem é tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="60a69-249">The source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="60a69-250">A tabela para a qual os dados são exportados é chamada de log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="60a69-250">The table where the data is exported to is called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="60a69-251">Além das informações de cadeia de conexão, as etapas nesta seção devem funcionar para o Banco de Dados SQL do Azure ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="60a69-251">Other than connection string information, the steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="60a69-252">Essas etapas foram testadas com relação à seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="60a69-252">These steps were tested by using the following configuration:</span></span>
   > 
   > * <span data-ttu-id="60a69-253">**Configuração ponto a site da rede virtual do Azure**: uma rede virtual conectando o cluster HDInsight a um SQL Server em um datacenter privado.</span><span class="sxs-lookup"><span data-stu-id="60a69-253">**Azure virtual network point-to-site configuration**: A virtual network connected the HDInsight cluster to a SQL Server in a private datacenter.</span></span> <span data-ttu-id="60a69-254">Consulte [Configurar um VPN ponto a site no Portal de Gerenciamento](../vpn-gateway/vpn-gateway-point-to-site-create.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="60a69-254">See [Configure a Point-to-Site VPN in the Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="60a69-255">**Azure HDInsight 3.1**: confira [Crie clusters Hadoop no HDInsight usando opções de personalização](hdinsight-hadoop-provision-linux-clusters.md) para saber mais sobre a criação de um cluster em uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="60a69-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="60a69-256">**SQL Server 2014**: configurado para permitir Autenticação SQL e executando o pacote de configuração do cliente VPN para conectar-se com segurança à rede virtual</span><span class="sxs-lookup"><span data-stu-id="60a69-256">**SQL Server 2014**: Configured to allow authentication and running the VPN client configuration package to connect securely to the virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="60a69-257">Exporte uma tabela do Hive para o banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-257">Export a Hive table to the Azure SQL database.</span></span>
8. <span data-ttu-id="60a69-258">Importe a tabela mobiledata para o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60a69-258">Import the mobiledata table to the HDInsight cluster.</span></span>
   
    <span data-ttu-id="60a69-259">Para examinar o arquivo de dados modificado, você pode usar o Portal do Azure, uma ferramenta de exploração do Armazenamento do Azure ou o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="60a69-259">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="60a69-260">A [Introdução ao HDInsight][hdinsight-get-started] tem um exemplo de código sobre como usar o Azure PowerShell para baixar um arquivo e exibir o conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="60a69-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell to download a file and display the file content.</span></span>

### <a name="the-powershell-sample"></a><span data-ttu-id="60a69-261">O exemplo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="60a69-261">The PowerShell sample</span></span>
    # Prepare an Azure SQL database to be used by the Sqoop tutorial

    #region - provide the following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription to access the server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating the log4jlogs table and the mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create the log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create the mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating the HDInsight cluster and the dependent services ..." -ForegroundColor Green

    # Create the default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create the HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate the cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process the source file

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define the connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing the source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from the source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into the destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process the source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove the "java.lang.Exception" from the first element of the array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList to remove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove the lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write to the destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from the cluster to the SQL database

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
