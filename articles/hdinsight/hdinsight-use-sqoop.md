---
title: aaaRun Sqoop Apache trabalhos com o Azure HDInsight (Hadoop) | Microsoft Docs
description: "Saiba como toouse PowerShell do Azure de uma estação de trabalho de toorun Sqoop de importação e exportação entre um cluster de Hadoop e um banco de dados do SQL Azure."
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
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="2e937-103">Use Sqoop com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e937-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="2e937-104">Saiba como toouse Sqoop em HDInsight tooimport e exportar entre o cluster HDInsight e o banco de dados do SQL Azure ou o banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2e937-104">Learn how toouse Sqoop in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="2e937-105">Embora Hadoop é uma opção natural para processar dados semi-estruturados e não estruturados, como logs e arquivos, também pode haver uma necessidade de dados tooprocess estruturados armazenados em bancos de dados relacionais.</span><span class="sxs-lookup"><span data-stu-id="2e937-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="2e937-106">[Sqoop] [ sqoop-user-guide-1.4.4] é uma ferramenta desenvolvida tootransfer dados entre bancos de dados relacionais e clusters de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2e937-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed tootransfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="2e937-107">Você pode usá-lo tooimport dados de um sistema de gerenciamento de banco de dados relacional (RDBMS), como SQL Server, MySQL ou Oracle no sistema de arquivo hello distribuído de Hadoop (HDFS), transformar dados Olá no Hadoop MapReduce ou Hive e, em seguida, exportar dados de saudação volta para um RDBMS.</span><span class="sxs-lookup"><span data-stu-id="2e937-107">You can use it tooimport data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="2e937-108">Neste tutorial, você está usando um Banco de Dados SQL como seu banco de dados relacional.</span><span class="sxs-lookup"><span data-stu-id="2e937-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="2e937-109">Para versões de Sqoop que têm suporte em clusters de HDInsight, consulte [Novidades nas versões de cluster Olá fornecidas pelo HDInsight?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="2e937-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-hello-scenario"></a><span data-ttu-id="2e937-110">Entender o cenário de saudação</span><span class="sxs-lookup"><span data-stu-id="2e937-110">Understand hello scenario</span></span>

<span data-ttu-id="2e937-111">O cluster HDInsight é fornecido com alguns dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="2e937-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="2e937-112">Use o hello dois exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e937-112">You use hello following two samples:</span></span>

* <span data-ttu-id="2e937-113">Um arquivo de log log4j localizado em */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="2e937-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="2e937-114">Olá logs a seguir é extraído do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="2e937-114">hello following logs are extracted from hello file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="2e937-115">Uma tabela de Hive denominada *hivesampletable*, que referências Olá arquivo de dados localizado em */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="2e937-115">A Hive table named *hivesampletable*, which references hello data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="2e937-116">Olá tabela contém alguns dados de dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="2e937-116">hello table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="2e937-117">Campo</span><span class="sxs-lookup"><span data-stu-id="2e937-117">Field</span></span> | <span data-ttu-id="2e937-118">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="2e937-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="2e937-119">clientid</span><span class="sxs-lookup"><span data-stu-id="2e937-119">clientid</span></span> |<span data-ttu-id="2e937-120">string</span><span class="sxs-lookup"><span data-stu-id="2e937-120">string</span></span> |
  | <span data-ttu-id="2e937-121">querytime</span><span class="sxs-lookup"><span data-stu-id="2e937-121">querytime</span></span> |<span data-ttu-id="2e937-122">string</span><span class="sxs-lookup"><span data-stu-id="2e937-122">string</span></span> |
  | <span data-ttu-id="2e937-123">market</span><span class="sxs-lookup"><span data-stu-id="2e937-123">market</span></span> |<span data-ttu-id="2e937-124">string</span><span class="sxs-lookup"><span data-stu-id="2e937-124">string</span></span> |
  | <span data-ttu-id="2e937-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="2e937-125">deviceplatform</span></span> |<span data-ttu-id="2e937-126">string</span><span class="sxs-lookup"><span data-stu-id="2e937-126">string</span></span> |
  | <span data-ttu-id="2e937-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="2e937-127">devicemake</span></span> |<span data-ttu-id="2e937-128">string</span><span class="sxs-lookup"><span data-stu-id="2e937-128">string</span></span> |
  | <span data-ttu-id="2e937-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="2e937-129">devicemodel</span></span> |<span data-ttu-id="2e937-130">string</span><span class="sxs-lookup"><span data-stu-id="2e937-130">string</span></span> |
  | <span data-ttu-id="2e937-131">state</span><span class="sxs-lookup"><span data-stu-id="2e937-131">state</span></span> |<span data-ttu-id="2e937-132">string</span><span class="sxs-lookup"><span data-stu-id="2e937-132">string</span></span> |
  | <span data-ttu-id="2e937-133">country</span><span class="sxs-lookup"><span data-stu-id="2e937-133">country</span></span> |<span data-ttu-id="2e937-134">string</span><span class="sxs-lookup"><span data-stu-id="2e937-134">string</span></span> |
  | <span data-ttu-id="2e937-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="2e937-135">querydwelltime</span></span> |<span data-ttu-id="2e937-136">double</span><span class="sxs-lookup"><span data-stu-id="2e937-136">double</span></span> |
  | <span data-ttu-id="2e937-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="2e937-137">sessionid</span></span> |<span data-ttu-id="2e937-138">bigint</span><span class="sxs-lookup"><span data-stu-id="2e937-138">bigint</span></span> |
  | <span data-ttu-id="2e937-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="2e937-139">sessionpagevieworder</span></span> |<span data-ttu-id="2e937-140">bigint</span><span class="sxs-lookup"><span data-stu-id="2e937-140">bigint</span></span> |

<span data-ttu-id="2e937-141">Primeiro, você exportar *sample.log* e *hivesampletable* toohello banco de dados do SQL Azure ou tooSQL servidor e, em seguida, importação de tabela Olá que contém dados do dispositivo móvel Olá fazer tooHDInsight usando Olá caminho a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e937-141">First, you export *sample.log* and *hivesampletable* toohello Azure SQL database or tooSQL Server, and then import hello table that contains hello mobile device data back tooHDInsight by using hello following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="2e937-142">Criar o cluster e o Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="2e937-142">Create cluster and SQL database</span></span>
<span data-ttu-id="2e937-143">Esta seção mostra como toocreate um cluster, um banco de dados SQL e esquemas de banco de dados SQL Olá para em execução Olá tutorial usando Olá portal do Azure e um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e937-143">This section shows you how toocreate a cluster, a SQL Database, and hello SQL database schemas for running hello tutorial using hello Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="2e937-144">Olá modelo pode ser encontrado no [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="2e937-144">hello template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="2e937-145">modelo do Gerenciador de recursos de saudação chama um bacpac pacote toodeploy Olá tabela esquemas tooSQL banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2e937-145">hello Resource Manager template calls a bacpac package toodeploy hello table schemas tooSQL database.</span></span>  <span data-ttu-id="2e937-146">pacote de bacpac Hello está localizado em um contêiner de blob público, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="2e937-146">hello bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="2e937-147">Se você quiser toouse um contêiner privado para arquivos de bacpac Olá, use Olá valores no modelo de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e937-147">If you want toouse a private container for hello bacpac files, use hello following values in hello template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="2e937-148">Se preferir que o cluster de saudação de toocreate toouse PowerShell do Azure e hello banco de dados SQL, consulte [Apêndice A](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="2e937-148">If you prefer toouse Azure PowerShell toocreate hello cluster and hello SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="2e937-149">Clique em Olá imagem tooopen um modelo do Gerenciador de recursos no portal do Azure de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="2e937-149">Click hello following image tooopen a Resource Manager template in hello Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. <span data-ttu-id="2e937-150">Digite hello propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e937-150">Enter hello following properties:</span></span>

    - <span data-ttu-id="2e937-151">**Subscription:** insira sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e937-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="2e937-152">**Grupo de Recursos**: crie um novo grupo de recursos do Azure ou escolha um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="2e937-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="2e937-153">Um grupo de recursos é para fins de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="2e937-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="2e937-154">Ele é um contêiner para objetos.</span><span class="sxs-lookup"><span data-stu-id="2e937-154">It is a container for objects.</span></span>
    - <span data-ttu-id="2e937-155">**Localização**: selecione uma região.</span><span class="sxs-lookup"><span data-stu-id="2e937-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="2e937-156">**ClusterName**: insira um nome para o cluster de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="2e937-156">**ClusterName**: Enter a name for hello Hadoop cluster.</span></span>
    - <span data-ttu-id="2e937-157">**Nome de logon e senha do cluster**: nome de logon do saudação padrão é Admin.</span><span class="sxs-lookup"><span data-stu-id="2e937-157">**Cluster login name and password**: hello default login name is admin.</span></span>
    - <span data-ttu-id="2e937-158">**Nome de usuário e senha de SSH**.</span><span class="sxs-lookup"><span data-stu-id="2e937-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="2e937-159">**Nome de logon e senha do servidor de banco de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="2e937-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="2e937-160">**_artifacts local**: usar o valor padrão de saudação, a menos que você deseja toouse seu próprio arquivo backpac em um local diferente.</span><span class="sxs-lookup"><span data-stu-id="2e937-160">**_artifacts Location**: Use hello default value unless you want toouse your own backpac file in a different location.</span></span>
    - <span data-ttu-id="2e937-161">**Token Sas do local de_artifacts**: deixe-o em branco.</span><span class="sxs-lookup"><span data-stu-id="2e937-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="2e937-162">**Nome do arquivo Bacpac**: usar o valor de padrão de saudação, a menos que você deseja toouse seu próprio arquivo de backpac.</span><span class="sxs-lookup"><span data-stu-id="2e937-162">**Bacpac File Name**: Use hello default value unless you want toouse your own backpac file.</span></span>
     
     <span data-ttu-id="2e937-163">Olá valores a seguir é embutidos em código na seção de variáveis de saudação:</span><span class="sxs-lookup"><span data-stu-id="2e937-163">hello following values are hardcoded in hello variables section:</span></span>
     
     | <span data-ttu-id="2e937-164">Nome da conta de armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="2e937-164">Default storage account name</span></span> | <span data-ttu-id="2e937-165"><CluterName>repositório</span><span class="sxs-lookup"><span data-stu-id="2e937-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="2e937-166">Nome do servidor de banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e937-166">Azure SQL database server name</span></span> |<span data-ttu-id="2e937-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="2e937-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="2e937-168">Nome do banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="2e937-168">Azure SQL database name</span></span> |<span data-ttu-id="2e937-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="2e937-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="2e937-170">Anote esses valores.</span><span class="sxs-lookup"><span data-stu-id="2e937-170">Please write down these values.</span></span>  <span data-ttu-id="2e937-171">Você precisa-los mais tarde no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e937-171">You need them later in hello tutorial.</span></span>

<span data-ttu-id="2e937-172">3. clique em **Okey** toosave parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e937-172">3.Click **OK** toosave hello parameters.</span></span>

<span data-ttu-id="2e937-173">4. de saudação **implantação personalizada** folha, clique em **grupo de recursos** suspensa caixa e, em seguida, clique em **novo** toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2e937-173">4.From hello **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** toocreate a new resource group.</span></span> <span data-ttu-id="2e937-174">grupo de recursos de saudação é um contêiner que agrupa cluster hello, conta de armazenamento dependente de saudação e outros recursos vinculados.</span><span class="sxs-lookup"><span data-stu-id="2e937-174">hello resource group is a container that groups hello cluster, hello dependent storage account and other linked resource.</span></span>

<span data-ttu-id="2e937-175">5. Clique em **Termos legais** e em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2e937-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="2e937-176">6. Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2e937-176">6.Click **Create**.</span></span> <span data-ttu-id="2e937-177">Você poderá ver um novo bloco intitulado Como enviar a implantação para a implantação do modelo.</span><span class="sxs-lookup"><span data-stu-id="2e937-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="2e937-178">Demora cerca de cluster de saudação toocreate aproximadamente 20 minutos e o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="2e937-178">It takes about around 20 minutes toocreate hello cluster and SQL database.</span></span>

<span data-ttu-id="2e937-179">Se você escolher o banco de dados do SQL Azure existente toouse ou Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="2e937-179">If you choose toouse existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="2e937-180">**Banco de dados do SQL Azure**: você deve configurar uma regra de firewall para Olá acesso tooallow ao servidor de banco de dados SQL do Azure de sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2e937-180">**Azure SQL database**: You must configure a firewall rule for hello Azure SQL database server tooallow access from your workstation.</span></span> <span data-ttu-id="2e937-181">Para obter instruções sobre como criar um banco de dados do SQL Azure e configurando o firewall do hello, consulte [começar a usar o banco de dados do SQL Azure][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="2e937-181">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="2e937-182">Por padrão, um banco de dados SQL do Azure permite conexões de serviços do Azure, como o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2e937-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="2e937-183">Se essa configuração de firewall estiver desabilitada, você precisa tooenable de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e937-183">If this firewall setting is disabled, you need tooenable it from hello Azure portal.</span></span> <span data-ttu-id="2e937-184">Para obter instruções sobre como criar um Banco de Dados SQL do Azure e configurar as regras de firewall, confira [Criar e configurar o Banco de Dados SQL][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="2e937-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="2e937-185">**SQL Server**: se o seu cluster HDInsight está em Olá mesma rede virtual no Azure como o SQL Server, você pode usar etapas Olá neste artigo tooimport e exportar dados tooa do SQL Server banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2e937-185">**SQL Server**: If your HDInsight cluster is on hello same virtual network in Azure as SQL Server, you can use hello steps in this article tooimport and export data tooa SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2e937-186">O Azure HDInsight oferece suporte somente a redes virtuais baseadas no local, e não trabalha atualmente com redes virtuais baseadas em grupos de afinidade.</span><span class="sxs-lookup"><span data-stu-id="2e937-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="2e937-187">toocreate e configurar uma rede virtual, consulte [criar uma rede virtual usando o portal do Azure de saudação](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="2e937-187">toocreate and configure a virtual network, see [Create a virtual network using hello Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="2e937-188">Quando você estiver usando o SQL Server em seu data center, você deve configurar a rede virtual hello como *site a site* ou *ponto a site*.</span><span class="sxs-lookup"><span data-stu-id="2e937-188">When you are using SQL Server in your datacenter, you must configure hello virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="2e937-189">Para **ponto a site** redes virtuais, o SQL Server devem estar em execução do cliente VPN Olá aplicativo de configuração, que está disponível no hello **painel** da sua configuração de rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e937-189">For **point-to-site** virtual networks, SQL Server must be running hello VPN client configuration application, which is available from hello **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="2e937-190">Quando você estiver usando o SQL Server em uma máquina virtual do Azure, qualquer configuração de rede virtual pode ser usada se a máquina virtual de saudação hospedando o SQL Server é um membro da saudação mesma rede virtual HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2e937-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if hello virtual machine hosting SQL Server is a member of hello same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="2e937-191">toocreate um cluster HDInsight em uma rede virtual, consulte [Hadoop criar clusters de HDInsight usando opções personalizadas](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="2e937-191">toocreate an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="2e937-192">O SQL Server também deve permitir autenticação.</span><span class="sxs-lookup"><span data-stu-id="2e937-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="2e937-193">Você deve usar um SQL Server saudação do logon toocomplete as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2e937-193">You must use a SQL Server login toocomplete hello steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="2e937-194">Executar trabalhos do Sqoop</span><span class="sxs-lookup"><span data-stu-id="2e937-194">Run Sqoop jobs</span></span>
<span data-ttu-id="2e937-195">O HDInsight pode executar trabalhos do Sqoop usando vários métodos.</span><span class="sxs-lookup"><span data-stu-id="2e937-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="2e937-196">Usar o hello toodecide tabela qual método é ideal para você a seguir, siga o link Olá para obter uma explicação.</span><span class="sxs-lookup"><span data-stu-id="2e937-196">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="2e937-197">**Use** se quiser...</span><span class="sxs-lookup"><span data-stu-id="2e937-197">**Use this** if you want...</span></span> | <span data-ttu-id="2e937-198">...um shell **interativo**</span><span class="sxs-lookup"><span data-stu-id="2e937-198">...an **interactive** shell</span></span> | <span data-ttu-id="2e937-199">...Processamento em**lotes**</span><span class="sxs-lookup"><span data-stu-id="2e937-199">...**batch** processing</span></span> | <span data-ttu-id="2e937-200">... com esse **sistema operacional de cluster**</span><span class="sxs-lookup"><span data-stu-id="2e937-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="2e937-201">... desse **sistema operacional cliente**</span><span class="sxs-lookup"><span data-stu-id="2e937-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="2e937-202">SSH</span><span class="sxs-lookup"><span data-stu-id="2e937-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="2e937-203">✔</span><span class="sxs-lookup"><span data-stu-id="2e937-203">✔</span></span> |<span data-ttu-id="2e937-204">✔</span><span class="sxs-lookup"><span data-stu-id="2e937-204">✔</span></span> |<span data-ttu-id="2e937-205">Linux</span><span class="sxs-lookup"><span data-stu-id="2e937-205">Linux</span></span> |<span data-ttu-id="2e937-206">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="2e937-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="2e937-207">SDK .NET para Hadoop</span><span class="sxs-lookup"><span data-stu-id="2e937-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="2e937-208">✔</span><span class="sxs-lookup"><span data-stu-id="2e937-208">✔</span></span> |<span data-ttu-id="2e937-209">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="2e937-209">Linux or Windows</span></span> |<span data-ttu-id="2e937-210">Windows (por enquanto)</span><span class="sxs-lookup"><span data-stu-id="2e937-210">Windows (for now)</span></span> |
| [<span data-ttu-id="2e937-211">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="2e937-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="2e937-212">✔</span><span class="sxs-lookup"><span data-stu-id="2e937-212">✔</span></span> |<span data-ttu-id="2e937-213">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="2e937-213">Linux or Windows</span></span> |<span data-ttu-id="2e937-214">Windows</span><span class="sxs-lookup"><span data-stu-id="2e937-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="2e937-215">Limitações</span><span class="sxs-lookup"><span data-stu-id="2e937-215">Limitations</span></span>
* <span data-ttu-id="2e937-216">A exportação em massa - HDInsight baseados em Linux com, Olá Sqoop conector usado tooexport dados tooMicrosoft do SQL Server ou banco de dados do SQL Azure atualmente não dá suporte para inserções em massa.</span><span class="sxs-lookup"><span data-stu-id="2e937-216">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="2e937-217">Envio em lote - com HDInsight baseados em Linux, ao usar o hello `-batch` opção ao executar inserções, Sqoop executa várias inserções em vez de envio em lote as operações de inserção hello.</span><span class="sxs-lookup"><span data-stu-id="2e937-217">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e937-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2e937-218">Next steps</span></span>
<span data-ttu-id="2e937-219">Agora que você aprendeu como toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="2e937-219">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="2e937-220">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="2e937-220">toolearn more, see:</span></span>

* [<span data-ttu-id="2e937-221">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e937-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="2e937-222">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e937-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="2e937-223">[Usar o Oozie com o HDInsight][hdinsight-use-oozie]: use a ação do Sqoop no fluxo de trabalho do Oozie.</span><span class="sxs-lookup"><span data-stu-id="2e937-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="2e937-224">[Analisar dados de atraso de voo usando HDInsight][hdinsight-analyze-flight-data]: usar Hive tooanalyze voo atrasar dados e, em seguida, usar o banco de dados do Sqoop tooexport dados tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2e937-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="2e937-225">[Carregar dados tooHDInsight][hdinsight-upload-data]: encontrar outros métodos para carregar o armazenamento de BLOBs do Azure/tooHDInsight de dados.</span><span class="sxs-lookup"><span data-stu-id="2e937-225">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="2e937-226">Apêndice A - um exemplo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e937-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="2e937-227">exemplo do PowerShell Olá executa Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e937-227">hello PowerShell sample performs hello following steps:</span></span>

1. <span data-ttu-id="2e937-228">Conecte-se tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2e937-228">Connect tooAzure.</span></span>
2. <span data-ttu-id="2e937-229">Crie um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e937-229">Create an Azure resource group.</span></span> <span data-ttu-id="2e937-230">Para obter mais informações, consulte [Usando o PowerShell do Azure com o Gerenciador de Recursos do Azure](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="2e937-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="2e937-231">Crie um servidor de Banco de Dados SQL do Azure, um banco de dados SQL do Azure e duas tabelas.</span><span class="sxs-lookup"><span data-stu-id="2e937-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="2e937-232">Se você usar o SQL Server em vez disso, use Olá instruções toocreate Olá tabelas seguintes:</span><span class="sxs-lookup"><span data-stu-id="2e937-232">If you use SQL Server instead, use hello following statements toocreate hello tables:</span></span>
   
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
   
    <span data-ttu-id="2e937-233">tabelas e o banco de dados do hello mais fácil maneira tooexamine Olá é toouse Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2e937-233">hello easiest way tooexamine hello database and tables is toouse Visual Studio.</span></span> <span data-ttu-id="2e937-234">servidor de banco de dados de saudação e o banco de dados de saudação podem ser examinadas usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e937-234">hello database server and hello database can be examined using hello Azure portal.</span></span>
4. <span data-ttu-id="2e937-235">Crie um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2e937-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="2e937-236">cluster de saudação tooexamine, você pode usar o hello portal do Azure ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e937-236">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="2e937-237">Pré-processe o arquivo de dados de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e937-237">Pre-process hello source data file.</span></span>
   
    <span data-ttu-id="2e937-238">Neste tutorial, você pode exportar um arquivo de log log4j (um arquivo delimitado) e um banco de dados do Hive tabela tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2e937-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table tooan Azure SQL database.</span></span> <span data-ttu-id="2e937-239">Olá arquivo delimitado é chamado */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="2e937-239">hello delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="2e937-240">Anteriormente no tutorial hello, você viu alguns exemplos de log4j logs.</span><span class="sxs-lookup"><span data-stu-id="2e937-240">Earlier in hello tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="2e937-241">No arquivo de log hello, há algumas linhas vazias e alguns toothese semelhantes de linhas:</span><span class="sxs-lookup"><span data-stu-id="2e937-241">In hello log file, there are some empty lines and some lines similar toothese:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="2e937-242">Isso é bom para obter outros exemplos que usam esses dados, mas é necessário remover essas exceções antes podemos importar no banco de dados do SQL Azure hello ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2e937-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into hello Azure SQL database or SQL Server.</span></span> <span data-ttu-id="2e937-243">Exportação de Sqoop falha se houver uma cadeia de caracteres vazia ou uma linha com menos elementos que número de saudação de campos definidos na tabela de banco de dados do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2e937-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than hello number of fields defined in hello Azure SQL database table.</span></span> <span data-ttu-id="2e937-244">tabela de log4jlogs Olá tem 7 campos de tipo de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2e937-244">hello log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="2e937-245">Este procedimento cria um novo arquivo em cluster Olá: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="2e937-245">This procedure creates a new file on hello cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="2e937-246">tooexamine arquivo de dados modificados hello, você pode usar o hello portal do Azure, uma ferramenta de Gerenciador de armazenamento do Azure ou do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e937-246">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="2e937-247">[Introdução ao HDInsight] [ hdinsight-get-started] tem um código de exemplo para usar o Azure PowerShell toodownload um arquivo e exibir o conteúdo do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="2e937-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell toodownload a file and display hello file content.</span></span>
6. <span data-ttu-id="2e937-248">Exporte um banco de dados de SQL do Azure de toohello do arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="2e937-248">Export a data file toohello Azure SQL database.</span></span>
   
    <span data-ttu-id="2e937-249">arquivo de origem de saudação é tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="2e937-249">hello source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="2e937-250">Olá tabela onde Olá dados exportados toois chamado log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="2e937-250">hello table where hello data is exported toois called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2e937-251">Diferente de informações da cadeia de conexão, etapas Olá nesta seção devem funcionar para um banco de dados do SQL Azure ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2e937-251">Other than connection string information, hello steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="2e937-252">Essas etapas foram testadas usando Olá a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="2e937-252">These steps were tested by using hello following configuration:</span></span>
   > 
   > * <span data-ttu-id="2e937-253">**Configuração de ponto para site de rede virtual do Azure**: uma rede virtual conectado tooa cluster HDInsight saudação do SQL Server em um datacenter particular.</span><span class="sxs-lookup"><span data-stu-id="2e937-253">**Azure virtual network point-to-site configuration**: A virtual network connected hello HDInsight cluster tooa SQL Server in a private datacenter.</span></span> <span data-ttu-id="2e937-254">Consulte [configurar uma VPN ponto a Site no Portal de gerenciamento de saudação](../vpn-gateway/vpn-gateway-point-to-site-create.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="2e937-254">See [Configure a Point-to-Site VPN in hello Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="2e937-255">**Azure HDInsight 3.1**: confira [Crie clusters Hadoop no HDInsight usando opções de personalização](hdinsight-hadoop-provision-linux-clusters.md) para saber mais sobre a criação de um cluster em uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2e937-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="2e937-256">**SQL Server 2014**: configurada autenticação tooallow e tooconnect de pacote de configuração de cliente do hello VPN em execução com segurança rede virtual toohello.</span><span class="sxs-lookup"><span data-stu-id="2e937-256">**SQL Server 2014**: Configured tooallow authentication and running hello VPN client configuration package tooconnect securely toohello virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="2e937-257">Exporte um banco de dados do Hive tabela toohello SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2e937-257">Export a Hive table toohello Azure SQL database.</span></span>
8. <span data-ttu-id="2e937-258">Importe o cluster HDInsight do hello mobiledata tabela toohello.</span><span class="sxs-lookup"><span data-stu-id="2e937-258">Import hello mobiledata table toohello HDInsight cluster.</span></span>
   
    <span data-ttu-id="2e937-259">tooexamine arquivo de dados modificados hello, você pode usar o hello portal do Azure, uma ferramenta de Gerenciador de armazenamento do Azure ou do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e937-259">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="2e937-260">[Introdução ao HDInsight] [ hdinsight-get-started] tem um código de exemplo sobre como usar o Azure PowerShell toodownload um arquivo e exibir o conteúdo do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="2e937-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell toodownload a file and display hello file content.</span></span>

### <a name="hello-powershell-sample"></a><span data-ttu-id="2e937-261">exemplo do PowerShell Olá</span><span class="sxs-lookup"><span data-stu-id="2e937-261">hello PowerShell sample</span></span>
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

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

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
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

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
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
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
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

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

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
