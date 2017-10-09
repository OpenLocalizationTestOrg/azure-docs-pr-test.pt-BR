---
title: coordenador de Hadoop Oozie aaaUse baseadas no HDInsight | Microsoft Docs
description: "Usar o Coordenador do Oozie com o Hadoop baseado no tempo no HDInsight, um serviço de big data. Saiba como toodefine Oozie coordenadores e fluxos de trabalho e enviar trabalhos."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a><span data-ttu-id="5b682-104">Usar o coordenador de Oozie baseada em tempo com Hadoop no HDInsight toodefine os fluxos de trabalho e coordenar trabalhos</span><span class="sxs-lookup"><span data-stu-id="5b682-104">Use time-based Oozie coordinator with Hadoop in HDInsight toodefine workflows and coordinate jobs</span></span>
<span data-ttu-id="5b682-105">Neste artigo, você aprenderá como fluxos de trabalho toodefine e coordenadores e como tootrigger Olá trabalhos do coordenador, com base no tempo.</span><span class="sxs-lookup"><span data-stu-id="5b682-105">In this article, you'll learn how toodefine workflows and coordinators, and how tootrigger hello coordinator jobs, based on time.</span></span> <span data-ttu-id="5b682-106">É útil toogo por meio de [Oozie de uso com o HDInsight] [ hdinsight-use-oozie] antes de ler este artigo.</span><span class="sxs-lookup"><span data-stu-id="5b682-106">It is helpful toogo through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="5b682-107">Além disso tooOozie, também é possível agendar trabalhos usando o Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5b682-107">In addition tooOozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="5b682-108">toolearn do Azure Data Factory, consulte [usar o Pig e Hive com a fábrica de dados](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="5b682-108">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5b682-109">Este artigo requer um cluster HDInsight baseado no Windows.</span><span class="sxs-lookup"><span data-stu-id="5b682-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="5b682-110">Para obter informações sobre como usar Oozie, incluindo trabalhos baseados em tempo, em um cluster baseado em Linux, consulte [Oozie Use com toodefine Hadoop e executar um fluxo de trabalho no HDInsight baseados em Linux](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="5b682-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="5b682-111">O que é o Oozie</span><span class="sxs-lookup"><span data-stu-id="5b682-111">What is Oozie</span></span>
<span data-ttu-id="5b682-112">O Apache Oozie é um sistema de fluxo de trabalho/coordenação que gerencia trabalhos do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5b682-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="5b682-113">Ele é integrado com pilha de Hadoop hello e dá suporte à trabalhos de Hadoop MapReduce Apache, Pig do Apache, Apache Hive e Apache Sqoop.</span><span class="sxs-lookup"><span data-stu-id="5b682-113">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="5b682-114">Ele também pode ser tooschedule usado trabalhos que são tooa específicas do sistema, como programas de Java ou scripts de shell.</span><span class="sxs-lookup"><span data-stu-id="5b682-114">It can also be used tooschedule jobs that are specific tooa system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="5b682-115">Olá, imagem a seguir mostra Olá de fluxo de trabalho que você implementará:</span><span class="sxs-lookup"><span data-stu-id="5b682-115">hello following image shows hello workflow you will implement:</span></span>

![Diagrama de fluxo de trabalho][img-workflow-diagram]

<span data-ttu-id="5b682-117">fluxo de trabalho Olá contém duas ações:</span><span class="sxs-lookup"><span data-stu-id="5b682-117">hello workflow contains two actions:</span></span>

1. <span data-ttu-id="5b682-118">Uma ação de Hive executa uma saudação de toocount script HiveQL ocorrências de cada tipo de nível de log em um arquivo de log log4j.</span><span class="sxs-lookup"><span data-stu-id="5b682-118">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="5b682-119">Cada log log4j consiste em uma linha de campos que contém um [nível de LOG] campo tooshow Olá tipo e hello gravidade, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5b682-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field tooshow hello type and hello severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="5b682-120">saudação de saída do script de Hive é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="5b682-120">hello Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="5b682-121">Para obter mais informações sobre o Hive, consulte [Usar o Hive com o HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="5b682-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="5b682-122">Uma ação de Sqoop exporta a tabela de tooa de saída Olá HiveQL ação em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5b682-122">A Sqoop action exports hello HiveQL action output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="5b682-123">Para saber mais sobre o Sqoop, confira [Usar o Sqoop com o HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="5b682-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="5b682-124">Para versões com suporte do Oozie em clusters de HDInsight, consulte [Novidades nas versões de cluster Olá fornecidas pelo HDInsight?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="5b682-124">For supported Oozie versions on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="5b682-125">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5b682-125">Prerequisites</span></span>
<span data-ttu-id="5b682-126">Antes de começar este tutorial, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="5b682-126">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="5b682-127">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5b682-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5b682-128">O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e será removido em 1º de janeiro de 2017.</span><span class="sxs-lookup"><span data-stu-id="5b682-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="5b682-129">Olá etapas para esse documento use Olá novos cmdlets do HDInsight que funcionam com o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b682-129">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="5b682-130">Siga as etapas de saudação em [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Olá última versão do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b682-130">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="5b682-131">Se você tiver scripts que toobe necessidade modificado toouse Olá novos cmdlets que funcionam com o Gerenciador de recursos do Azure, consulte [tooAzure migrando desenvolvimento baseado no Gerenciador de recursos de ferramentas para clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="5b682-131">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="5b682-132">**Um cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5b682-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="5b682-133">Para saber mais sobre como criar um cluster HDInsight, confira [Criar cluster HDInsight][hdinsight-provision] ou [Introdução ao HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="5b682-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="5b682-134">Você precisará Olá toogo dados tutorial Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b682-134">You will need hello following data toogo through hello tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="5b682-135">Propriedade do cluster</span><span class="sxs-lookup"><span data-stu-id="5b682-135">Cluster property</span></span></th><th><span data-ttu-id="5b682-136">Nome de variável do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b682-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="5b682-137">Valor</span><span class="sxs-lookup"><span data-stu-id="5b682-137">Value</span></span></th><th><span data-ttu-id="5b682-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b682-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="5b682-139">Nome do cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="5b682-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="5b682-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="5b682-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="5b682-141">cluster de HDInsight Olá no qual você executará este tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b682-141">hello HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="5b682-142">Nome de usuário do cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="5b682-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="5b682-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="5b682-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="5b682-144">nome de usuário do cluster do HDInsight Hello.</span><span class="sxs-lookup"><span data-stu-id="5b682-144">hello HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="5b682-145">Senha de usuário do cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="5b682-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="5b682-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="5b682-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="5b682-147">senha de usuário do cluster do HDInsight Hello.</span><span class="sxs-lookup"><span data-stu-id="5b682-147">hello HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="5b682-148">Nome da conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5b682-148">Azure storage account name</span></span></td><td><span data-ttu-id="5b682-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="5b682-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="5b682-150">Um cluster de HDInsight de toohello disponíveis de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b682-150">An Azure Storage account available toohello HDInsight cluster.</span></span> <span data-ttu-id="5b682-151">Para este tutorial, use a conta de armazenamento de padrão de Olá que você especificou durante o processo de provisionamento de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5b682-151">For this tutorial, use hello default storage account that you specified during hello cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="5b682-152">Nome do contêiner de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="5b682-152">Azure Blob container name</span></span></td><td><span data-ttu-id="5b682-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="5b682-153">$containerName</span></span></td><td></td><td><span data-ttu-id="5b682-154">Neste exemplo, use o contêiner de armazenamento de BLOBs do Azure Olá que é usado para o sistema de arquivos de cluster de HDInsight do saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="5b682-154">For this example, use hello Azure Blob storage container that is used for hello default HDInsight cluster file system.</span></span> <span data-ttu-id="5b682-155">Por padrão, ele tem Olá mesmo nome do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5b682-155">By default, it has hello same name as hello HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="5b682-156">
* **Um banco de dados SQL do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5b682-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="5b682-157">Você deve configurar uma regra de firewall para Olá tooallow acesso ao servidor de banco de dados SQL de sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5b682-157">You must configure a firewall rule for hello SQL Database server tooallow access from your workstation.</span></span> <span data-ttu-id="5b682-158">Para obter instruções sobre como criar um banco de dados do SQL Azure e configurando o firewall do hello, consulte [se familiarizar com o banco de dados do SQL Azure] [sqldatabase-get-iniciado].</span><span class="sxs-lookup"><span data-stu-id="5b682-158">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="5b682-159">Este artigo fornece um script do Windows PowerShell para criar a tabela de banco de dados do SQL Azure Olá é necessário para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b682-159">This article provides a Windows PowerShell script for creating hello Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="5b682-160">Propriedade de banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="5b682-160">SQL database property</span></span></th><th><span data-ttu-id="5b682-161">Nome de variável do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b682-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="5b682-162">Valor</span><span class="sxs-lookup"><span data-stu-id="5b682-162">Value</span></span></th><th><span data-ttu-id="5b682-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b682-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="5b682-164">Nome do servidor de banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="5b682-164">SQL database server name</span></span></td><td><span data-ttu-id="5b682-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="5b682-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="5b682-166">Olá SQL database server toowhich Sqoop exportará dados.</span><span class="sxs-lookup"><span data-stu-id="5b682-166">hello SQL database server toowhich Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="5b682-167">Nome de logon do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="5b682-167">SQL database login name</span></span></td><td><span data-ttu-id="5b682-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="5b682-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="5b682-169">Nome de logon do banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="5b682-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="5b682-170">Senha de logon do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="5b682-170">SQL database login password</span></span></td><td><span data-ttu-id="5b682-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="5b682-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="5b682-172">Senha de logon do banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="5b682-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="5b682-173">Nome do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="5b682-173">SQL database name</span></span></td><td><span data-ttu-id="5b682-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="5b682-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="5b682-175">toowhich de banco de dados SQL do Azure de saudação Sqoop exportará dados.</span><span class="sxs-lookup"><span data-stu-id="5b682-175">hello Azure SQL database toowhich Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="5b682-176">Por padrão, um banco de dados SQL do Azure permite conexões de serviços do Azure, como o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5b682-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="5b682-177">Se essa configuração de firewall estiver desabilitada, você deve habilitá-lo da saudação Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b682-177">If this firewall setting is disabled, you must enable it from hello Azure Portal.</span></span> <span data-ttu-id="5b682-178">Para saber mais sobre como criar um Banco de Dados SQL e configurar regras de firewall, confira [Criar e configurar o Banco de Dados SQL][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="5b682-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="5b682-179">Valores de saudação de preenchimento em tabelas de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b682-179">Fill-in hello values in hello tables.</span></span> <span data-ttu-id="5b682-180">Isso poderá ser útil para percorrer este tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b682-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="5b682-181">Definir o fluxo de trabalho do Oozie e Olá script HiveQL relacionados</span><span class="sxs-lookup"><span data-stu-id="5b682-181">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="5b682-182">As definições de fluxos de trabalho do Oozie são escritas em hPDL (uma Linguagem de Definição de Processo XML).</span><span class="sxs-lookup"><span data-stu-id="5b682-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="5b682-183">nome de arquivo de fluxo de trabalho saudação padrão *. XML*.</span><span class="sxs-lookup"><span data-stu-id="5b682-183">hello default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="5b682-184">Você salvar o arquivo de fluxo de trabalho Olá localmente e, em seguida, implantá-lo cluster do HDInsight toohello por usar PowerShell do Azure, mais adiante neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b682-184">You will save hello workflow file locally, and then deploy it toohello HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="5b682-185">Olá ação de Hive no fluxo de trabalho Olá chama um arquivo de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="5b682-185">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="5b682-186">Esse arquivo de script contém três instruções HiveQL:</span><span class="sxs-lookup"><span data-stu-id="5b682-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="5b682-187">**Olá instrução DROP TABLE** exclusões Olá log4j Hive tabela se ela existir.</span><span class="sxs-lookup"><span data-stu-id="5b682-187">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="5b682-188">**Olá instrução CREATE TABLE** cria uma log4j Hive tabela externa, que aponta toohello local do arquivo de log do hello log4j;</span><span class="sxs-lookup"><span data-stu-id="5b682-188">**hello CREATE TABLE statement** creates a log4j Hive external table, which points toohello location of hello log4j log file;</span></span>
3. <span data-ttu-id="5b682-189">**Olá local do arquivo de log do hello log4j**.</span><span class="sxs-lookup"><span data-stu-id="5b682-189">**hello location of hello log4j log file**.</span></span> <span data-ttu-id="5b682-190">é o delimitador de campo Hello ",".</span><span class="sxs-lookup"><span data-stu-id="5b682-190">hello field delimiter is ",".</span></span> <span data-ttu-id="5b682-191">delimitador de linha Hello padrão é "\n".</span><span class="sxs-lookup"><span data-stu-id="5b682-191">hello default line delimiter is "\n".</span></span> <span data-ttu-id="5b682-192">Uma tabela externa Hive é o arquivo de dados de saudação de tooavoid usado que está sendo removido do local original do hello, caso você deseje fluxo de trabalho toorun Olá Oozie várias vezes.</span><span class="sxs-lookup"><span data-stu-id="5b682-192">A Hive external table is used tooavoid hello data file being removed from hello original location, in case you want toorun hello Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="5b682-193">**Olá instrução inserir substituir** contagens de ocorrências de saudação de cada tipo de nível de log do hello log4j tabela de Hive e salva o local de armazenamento de BLOBs do Azure do hello saída tooan.</span><span class="sxs-lookup"><span data-stu-id="5b682-193">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and it saves hello output tooan Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="5b682-194">Há um erro conhecido do caminho do Hive.</span><span class="sxs-lookup"><span data-stu-id="5b682-194">There is a known Hive path issue.</span></span> <span data-ttu-id="5b682-195">Você encontrará esse problema ao enviar um trabalho do Oozie.</span><span class="sxs-lookup"><span data-stu-id="5b682-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="5b682-196">Olá instruções para corrigir o problema de saudação pode ser encontrada no hello Wiki do TechNet: [Hive do HDInsight erro: não é possível toorename][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="5b682-196">hello instructions for fixing hello issue can be found on hello TechNet Wiki: [HDInsight Hive error: Unable toorename][technetwiki-hive-error].</span></span>

<span data-ttu-id="5b682-197">**toobe toodefine Olá HiveQL script arquivo chamado pelo fluxo de trabalho Olá**</span><span class="sxs-lookup"><span data-stu-id="5b682-197">**toodefine hello HiveQL script file toobe called by hello workflow**</span></span>

1. <span data-ttu-id="5b682-198">Crie um arquivo de texto com hello seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="5b682-198">Create a text file with hello following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="5b682-199">Há três variáveis usadas em script hello:</span><span class="sxs-lookup"><span data-stu-id="5b682-199">There are three variables used in hello script:</span></span>

   * <span data-ttu-id="5b682-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="5b682-200">${hiveTableName}</span></span>
   * <span data-ttu-id="5b682-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="5b682-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="5b682-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="5b682-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="5b682-203">arquivo de definição de fluxo de trabalho (. XML neste tutorial) Olá passará toothis esses valores script HiveQL em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5b682-203">hello workflow definition file (workflow.xml in this tutorial) will pass these values toothis HiveQL script at run time.</span></span>
2. <span data-ttu-id="5b682-204">Salve o arquivo hello como **C:\Tutorials\UseOozie\useooziewf.hql** usando a codificação ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="5b682-204">Save hello file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="5b682-205">(Use o Bloco de Notas se o seu editor de texto não fornecer essa opção.) Esse arquivo de script será implantado toohello HDInsight cluster posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b682-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed toohello HDInsight cluster later in hello tutorial.</span></span>

<span data-ttu-id="5b682-206">**toodefine um fluxo de trabalho**</span><span class="sxs-lookup"><span data-stu-id="5b682-206">**toodefine a workflow**</span></span>

1. <span data-ttu-id="5b682-207">Crie um arquivo de texto com hello seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="5b682-207">Create a text file with hello following content:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="5b682-208">Há duas ações definidas no fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b682-208">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="5b682-209">Olá start-tooaction é *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="5b682-209">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="5b682-210">Se a ação de saudação executa *Okey*, ação Avançar Olá é *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="5b682-210">If hello action runs *OK*, hello next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="5b682-211">Olá RunHiveScript tem diversas variáveis.</span><span class="sxs-lookup"><span data-stu-id="5b682-211">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="5b682-212">Passa valores hello quando você enviar o trabalho de Oozie de saudação de sua estação de trabalho usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b682-212">You will pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="5b682-213">Variáveis de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="5b682-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="5b682-214">Variáveis de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="5b682-214">Workflow variables</span></span></th><th><span data-ttu-id="5b682-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b682-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="5b682-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="5b682-216">${jobTracker}</span></span></td><td><span data-ttu-id="5b682-217">Especifique a URL de saudação do rastreador de trabalho do Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="5b682-217">Specify hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="5b682-218">Use <strong>jobtrackerhost:9010</strong> no cluster HDInsight versões 3.0 e 2.0.</span><span class="sxs-lookup"><span data-stu-id="5b682-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="5b682-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="5b682-219">${nameNode}</span></span></td><td><span data-ttu-id="5b682-220">Especifica URL de saudação do nó do nome de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="5b682-220">Specify hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="5b682-221">Usar saudação padrão arquivo sistema wasb: / / endereço, por exemplo, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. >.blob.Core.Windows.NET</i>.</span><span class="sxs-lookup"><span data-stu-id="5b682-221">Use hello default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="5b682-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="5b682-222">${queueName}</span></span></td><td><span data-ttu-id="5b682-223">Especifica o nome de fila Olá Olá trabalho será enviado para.</span><span class="sxs-lookup"><span data-stu-id="5b682-223">Specifies hello queue name that hello job will be submitted to.</span></span> <span data-ttu-id="5b682-224">Use <strong>padrão</strong>.</span><span class="sxs-lookup"><span data-stu-id="5b682-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="5b682-225">Variáveis de ação do Hive</span><span class="sxs-lookup"><span data-stu-id="5b682-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="5b682-226">Variável de ação do Hive</span><span class="sxs-lookup"><span data-stu-id="5b682-226">Hive action variable</span></span></th><th><span data-ttu-id="5b682-227">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b682-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="5b682-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="5b682-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="5b682-229">diretório de origem Olá para Olá comando Hive Create Table.</span><span class="sxs-lookup"><span data-stu-id="5b682-229">hello source directory for hello Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="5b682-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="5b682-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="5b682-231">pasta de saída Olá para Olá instrução inserir substituir.</span><span class="sxs-lookup"><span data-stu-id="5b682-231">hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="5b682-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="5b682-232">${hiveTableName}</span></span></td><td><span data-ttu-id="5b682-233">nome de saudação da tabela de Hive Olá que faz referência a arquivos de dados de log4j hello.</span><span class="sxs-lookup"><span data-stu-id="5b682-233">hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="5b682-234">Variáveis de ação do Sqoop</span><span class="sxs-lookup"><span data-stu-id="5b682-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="5b682-235">Variável de ação do Sqoop</span><span class="sxs-lookup"><span data-stu-id="5b682-235">Sqoop action variable</span></span></th><th><span data-ttu-id="5b682-236">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b682-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="5b682-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="5b682-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="5b682-238">Cadeia de conexão do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="5b682-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="5b682-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="5b682-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="5b682-240">saudação de dados do SQL Azure banco de dados tabela toowhere saudação será exportada.</span><span class="sxs-lookup"><span data-stu-id="5b682-240">hello Azure SQL database table toowhere hello data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="5b682-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="5b682-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="5b682-242">pasta de saída Olá para Olá instrução Hive inserir substituir.</span><span class="sxs-lookup"><span data-stu-id="5b682-242">hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="5b682-243">Isso é hello mesma pasta para exportação de Sqoop hello (export-dir).</span><span class="sxs-lookup"><span data-stu-id="5b682-243">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="5b682-244">Para obter mais informações sobre o fluxo de trabalho do Oozie e usando as ações de fluxo de trabalho de saudação, consulte [documentação do Apache Oozie 4.0] [ apache-oozie-400] (para a versão 3.0 do cluster HDInsight) ou [Oozie Apache 3.3.2 documentação] [ apache-oozie-332] (para a versão 2.1 do cluster HDInsight).</span><span class="sxs-lookup"><span data-stu-id="5b682-244">For more information about Oozie workflow and using hello workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="5b682-245">Salve o arquivo hello como **C:\Tutorials\UseOozie\workflow.xml** usando a codificação ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="5b682-245">Save hello file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="5b682-246">(Use o Bloco de Notas se o seu editor de texto não fornecer essa opção.)</span><span class="sxs-lookup"><span data-stu-id="5b682-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="5b682-247">**coordenador de toodefine**</span><span class="sxs-lookup"><span data-stu-id="5b682-247">**toodefine coordinator**</span></span>

1. <span data-ttu-id="5b682-248">Crie um arquivo de texto com hello seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="5b682-248">Create a text file with hello following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="5b682-249">Há cinco variáveis usadas no arquivo de definição de saudação:</span><span class="sxs-lookup"><span data-stu-id="5b682-249">There are five variables used in hello definition file:</span></span>

   | <span data-ttu-id="5b682-250">Variável</span><span class="sxs-lookup"><span data-stu-id="5b682-250">Variable</span></span> | <span data-ttu-id="5b682-251">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b682-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="5b682-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="5b682-252">${coordFrequency}</span></span> |<span data-ttu-id="5b682-253">Tempo de pausa do trabalho.</span><span class="sxs-lookup"><span data-stu-id="5b682-253">Job pause time.</span></span> <span data-ttu-id="5b682-254">A frequência sempre é expressa em minutos.</span><span class="sxs-lookup"><span data-stu-id="5b682-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="5b682-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="5b682-255">${coordStart}</span></span> |<span data-ttu-id="5b682-256">Hora de início do trabalho.</span><span class="sxs-lookup"><span data-stu-id="5b682-256">Job start time.</span></span> |
   | <span data-ttu-id="5b682-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="5b682-257">${coordEnd}</span></span> |<span data-ttu-id="5b682-258">Hora de término do trabalho.</span><span class="sxs-lookup"><span data-stu-id="5b682-258">Job end time.</span></span> |
   | <span data-ttu-id="5b682-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="5b682-259">${coordTimezone}</span></span> |<span data-ttu-id="5b682-260">O Oozie processa trabalhos do coordenador em um fuso horário fixo sem horário de verão (geralmente representado pelo UTC).</span><span class="sxs-lookup"><span data-stu-id="5b682-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="5b682-261">Este fuso horário é conhecido como hello "Oozie processamento de fuso horário."</span><span class="sxs-lookup"><span data-stu-id="5b682-261">This time zone is referred as hello "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="5b682-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="5b682-262">${wfPath}</span></span> |<span data-ttu-id="5b682-263">caminho Hello. Olá XML.</span><span class="sxs-lookup"><span data-stu-id="5b682-263">hello path for hello workflow.xml.</span></span>  <span data-ttu-id="5b682-264">Se o nome de arquivo de fluxo de trabalho de saudação não é um nome de arquivo padrão de saudação (. xml), você deve especificar isto.</span><span class="sxs-lookup"><span data-stu-id="5b682-264">If hello workflow file name is not hello default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="5b682-265">Salve o arquivo hello como **C:\Tutorials\UseOozie\coordinator.xml** usando a codificação do hello ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="5b682-265">Save hello file as **C:\Tutorials\UseOozie\coordinator.xml** by using hello ANSI (ASCII) encoding.</span></span> <span data-ttu-id="5b682-266">(Use o Bloco de Notas se o seu editor de texto não fornecer essa opção.)</span><span class="sxs-lookup"><span data-stu-id="5b682-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a><span data-ttu-id="5b682-267">Implantar projeto do Oozie hello e preparar o tutorial Olá</span><span class="sxs-lookup"><span data-stu-id="5b682-267">Deploy hello Oozie project and prepare hello tutorial</span></span>
<span data-ttu-id="5b682-268">Você executará uma Azure PowerShell a seguir Olá script tooperform:</span><span class="sxs-lookup"><span data-stu-id="5b682-268">You will run an Azure PowerShell script tooperform hello following:</span></span>

* <span data-ttu-id="5b682-269">Saudação de copiar o armazenamento de Blob tooAzure HiveQL script (useoozie.hql), wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="5b682-269">Copy hello HiveQL script (useoozie.hql) tooAzure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="5b682-270">Copie toowasb:///tutorials/useoozie/workflow.xml. XML.</span><span class="sxs-lookup"><span data-stu-id="5b682-270">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="5b682-271">Copie coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="5b682-271">Copy coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="5b682-272">Copiar arquivo de dados de saudação (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="5b682-272">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="5b682-273">Criar uma tabela do Banco de Dados SQL para armazenar os dados de exportação do Sqoop.</span><span class="sxs-lookup"><span data-stu-id="5b682-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="5b682-274">nome da tabela Olá é *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="5b682-274">hello table name is *log4jLogCount*.</span></span>

<span data-ttu-id="5b682-275">**Compreender o armazenamento do HDInsight**</span><span class="sxs-lookup"><span data-stu-id="5b682-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="5b682-276">O HDInsight usa o armazenamento de blob do Azure para o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="5b682-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="5b682-277">wasb: / / é a implementação da Microsoft do sistema de arquivo hello distribuído de Hadoop (HDFS) no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b682-277">wasb:// is Microsoft's implementation of hello Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="5b682-278">Para obter mais informações, consulte [Usar o Armazenamento de Blobs do Azure com o HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="5b682-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="5b682-279">Quando você provisiona um cluster HDInsight, uma conta de armazenamento de BLOBs do Azure e um contêiner específico dessa conta é designado como o sistema de arquivos padrão hello, como no HDFS.</span><span class="sxs-lookup"><span data-stu-id="5b682-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as hello default file system, like in HDFS.</span></span> <span data-ttu-id="5b682-280">Além disso toothis conta de armazenamento, você pode adicionar contas de armazenamento adicional da saudação mesmo assinatura do Azure ou de assinaturas do Azure diferentes durante o processo de provisionamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b682-280">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or from different Azure subscriptions during hello provisioning process.</span></span> <span data-ttu-id="5b682-281">Para saber mais sobre como adicionar mais contas de armazenamento, confira [Provisionar clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="5b682-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="5b682-282">script do toosimplify hello Azure PowerShell usado neste tutorial, todos os Olá arquivos são armazenados no contêiner do sistema de arquivos saudação padrão localizados no *tutoriais/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="5b682-282">toosimplify hello Azure PowerShell script used in this tutorial, all of hello files are stored in hello default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="5b682-283">Por padrão, esse contêiner tiver Olá mesmo nome como o nome do cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5b682-283">By default, this container has hello same name as hello HDInsight cluster name.</span></span>
<span data-ttu-id="5b682-284">Olá sintaxe é:</span><span class="sxs-lookup"><span data-stu-id="5b682-284">hello syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="5b682-285">Olá somente *wasb: / /* sintaxe tem suporte na versão 3.0 do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5b682-285">Only hello *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="5b682-286">Olá antigo *asv: / /* sintaxe tem suporte no HDInsight 2.1 e 1.6 clusters, mas não há suporte em clusters de HDInsight 3.0.</span><span class="sxs-lookup"><span data-stu-id="5b682-286">hello older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="5b682-287">Olá wasb: / / caminho é um caminho virtual.</span><span class="sxs-lookup"><span data-stu-id="5b682-287">hello wasb:// path is a virtual path.</span></span> <span data-ttu-id="5b682-288">Para obter mais informações, consulte [Usar o Armazenamento de Blobs do Azure com o HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="5b682-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="5b682-289">Um arquivo que é armazenado no contêiner do sistema de arquivos saudação padrão pode ser acessado do HDInsight usando qualquer Olá URIs (estou usando. XML como um exemplo) a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b682-289">A file that is stored in hello default file system container can be accessed from HDInsight by using any of hello following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="5b682-290">Se desejar que o arquivo de saudação do tooaccess diretamente da conta de armazenamento Olá, nome do blob Olá para o arquivo hello é:</span><span class="sxs-lookup"><span data-stu-id="5b682-290">If you want tooaccess hello file directly from hello storage account, hello blob name for hello file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="5b682-291">**Compreender a tabela interna e a tabela externa do Hive**</span><span class="sxs-lookup"><span data-stu-id="5b682-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="5b682-292">Há algumas coisas que você precisa tooknow sobre tabelas internas e externas de Hive:</span><span class="sxs-lookup"><span data-stu-id="5b682-292">There are a few things you need tooknow about Hive internal and external tables:</span></span>

* <span data-ttu-id="5b682-293">Olá comando CREATE TABLE cria uma tabela interna, também conhecido como uma tabela gerenciada.</span><span class="sxs-lookup"><span data-stu-id="5b682-293">hello CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="5b682-294">arquivo de dados Olá deve estar localizado no contêiner de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b682-294">hello data file must be located in hello default container.</span></span>
* <span data-ttu-id="5b682-295">Olá comando CREATE TABLE move dados saudação arquivotoohello/hive/warehouse/<TableName> pasta no contêiner de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b682-295">hello CREATE TABLE command moves hello data file toohello /hive/warehouse/<TableName> folder in hello default container.</span></span>
* <span data-ttu-id="5b682-296">Olá comando CREATE EXTERNAL TABLE cria uma tabela externa.</span><span class="sxs-lookup"><span data-stu-id="5b682-296">hello CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="5b682-297">arquivo de dados Olá pode estar localizado fora da saudação padrão contêiner.</span><span class="sxs-lookup"><span data-stu-id="5b682-297">hello data file can be located outside hello default container.</span></span>
* <span data-ttu-id="5b682-298">Olá comando CREATE EXTERNAL TABLE não mover o arquivo de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b682-298">hello CREATE EXTERNAL TABLE command does not move hello data file.</span></span>
* <span data-ttu-id="5b682-299">Olá comando CREATE EXTERNAL TABLE não permite que todas as subpastas na pasta Olá especificado na cláusula de local de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b682-299">hello CREATE EXTERNAL TABLE command doesn't allow any subfolders under hello folder that is specified in hello LOCATION clause.</span></span> <span data-ttu-id="5b682-300">Essa é Olá razão por que o tutorial Olá faz uma cópia do arquivo de sample.log hello.</span><span class="sxs-lookup"><span data-stu-id="5b682-300">This is hello reason why hello tutorial makes a copy of hello sample.log file.</span></span>

<span data-ttu-id="5b682-301">Para obter mais informações, consulte [HDInsight: introdução às tabelas internas e externas do Hive][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="5b682-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="5b682-302">**tutorial de saudação tooprepare**</span><span class="sxs-lookup"><span data-stu-id="5b682-302">**tooprepare hello tutorial**</span></span>

1. <span data-ttu-id="5b682-303">Saudação de abrir o Windows PowerShell ISE (na tela inicial do Windows 8 hello, digite **PowerShell_ISE**e, em seguida, clique em **o Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="5b682-303">Open hello Windows PowerShell ISE (in hello Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="5b682-304">Para obter mais informações, confira [Iniciar o Windows PowerShell no Windows 8 e no Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="5b682-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="5b682-305">No painel inferior do hello, execute Olá comando tooconnect tooyour assinatura do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b682-305">In hello bottom pane, run hello following command tooconnect tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="5b682-306">Você será solicitado tooenter suas credenciais de conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b682-306">You will be prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="5b682-307">Esse método de adição de uma conexão de assinatura expira e depois de 12 horas, você terá toorun Olá cmdlet novamente.</span><span class="sxs-lookup"><span data-stu-id="5b682-307">This method of adding a subscription connection times out, and after 12 hours, you will have toorun hello cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5b682-308">Se você tiver várias assinaturas do Azure e assinatura do saudação padrão não é Olá aquele que você deseja toouse, use Olá <strong>Select-AzureSubscription</strong> tooselect cmdlet uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="5b682-308">If you have multiple Azure subscriptions and hello default subscription is not hello one you want toouse, use hello <strong>Select-AzureSubscription</strong> cmdlet tooselect a subscription.</span></span>

3. <span data-ttu-id="5b682-309">Copie Olá script a seguir no painel de script hello e então definir variáveis de seis primeiras hello:</span><span class="sxs-lookup"><span data-stu-id="5b682-309">Copy hello following script into hello script pane, and then set hello first six variables:</span></span>

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    <span data-ttu-id="5b682-310">Para obter mais descrições de variáveis de hello, consulte Olá [pré-requisitos](#prerequisites) seção neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b682-310">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="5b682-311">Acrescente Olá toohello script no painel de script hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b682-311">Append hello following toohello script in hello script pane:</span></span>

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="5b682-312">Clique em **Executar Script** ou pressione **F5** toorun script de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b682-312">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="5b682-313">saída de Hello será semelhante a:</span><span class="sxs-lookup"><span data-stu-id="5b682-313">hello output will be similar to:</span></span>

    ![Saída de preparação do tutorial][img-preparation-output]

## <a name="run-hello-oozie-project"></a><span data-ttu-id="5b682-315">Executar Olá Oozie projeto</span><span class="sxs-lookup"><span data-stu-id="5b682-315">Run hello Oozie project</span></span>
<span data-ttu-id="5b682-316">Atualmente, o PowerShell do Azure não fornece nenhum cmdlet para definir trabalhos do Oozie.</span><span class="sxs-lookup"><span data-stu-id="5b682-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="5b682-317">Você pode usar o hello **Invoke-RestMethod** tooinvoke cmdlet Oozie os serviços da web.</span><span class="sxs-lookup"><span data-stu-id="5b682-317">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="5b682-318">API de serviços web de Oozie Olá é uma API de JSON de REST de HTTP.</span><span class="sxs-lookup"><span data-stu-id="5b682-318">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="5b682-319">Para obter mais informações sobre a API de serviços web de Oozie hello, consulte [documentação do Apache Oozie 4.0] [ apache-oozie-400] (para a versão 3.0 do cluster HDInsight) ou [documentação do Apache Oozie 3.3.2] [ apache-oozie-332] (para a versão 2.1 do cluster HDInsight).</span><span class="sxs-lookup"><span data-stu-id="5b682-319">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="5b682-320">**toosubmit um trabalho Oozie**</span><span class="sxs-lookup"><span data-stu-id="5b682-320">**toosubmit an Oozie job**</span></span>

1. <span data-ttu-id="5b682-321">Saudação de abrir o Windows PowerShell ISE (na tela inicial do Windows 8, digite **PowerShell_ISE**e, em seguida, clique em **o Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="5b682-321">Open hello Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="5b682-322">Para obter mais informações, confira [Iniciar o Windows PowerShell no Windows 8 e no Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="5b682-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="5b682-323">Script a seguir de saudação de cópia no painel de script hello e, em seguida, o conjunto Olá variáveis primeiro quatorze (no entanto, ignorar **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="5b682-323">Copy hello following script into hello script pane, and then set hello first fourteen variables (however, skip **$storageUri**).</span></span>

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    <span data-ttu-id="5b682-324">Para obter mais descrições de variáveis de hello, consulte Olá [pré-requisitos](#prerequisites) seção neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5b682-324">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="5b682-325">$coordstart e $coordend são Olá início de fluxo de trabalho e a hora de término.</span><span class="sxs-lookup"><span data-stu-id="5b682-325">$coordstart and $coordend are hello workflow starting and ending time.</span></span> <span data-ttu-id="5b682-326">toofind horário de UTC/GMT hello, pesquise "hora do utc" em bing.com. Olá $coordFrequency é a frequência em minutos que o fluxo de trabalho do toorun hello.</span><span class="sxs-lookup"><span data-stu-id="5b682-326">toofind out hello UTC/GMT time, search "utc time" on bing.com. hello $coordFrequency is how often in minutes you want toorun hello workflow.</span></span>
3. <span data-ttu-id="5b682-327">Acrescente Olá toohello script a seguir.</span><span class="sxs-lookup"><span data-stu-id="5b682-327">Append hello following toohello script.</span></span> <span data-ttu-id="5b682-328">Esta parte define a carga do Oozie hello:</span><span class="sxs-lookup"><span data-stu-id="5b682-328">This part defines hello Oozie payload:</span></span>

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > <span data-ttu-id="5b682-329">Olá, o arquivo de carga de envio do principal diferença em comparação comparada toohello fluxo de trabalho é variável Olá **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="5b682-329">hello major difference compared toohello workflow submission payload file is hello variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="5b682-330">Ao enviar um trabalho de fluxo de trabalho, use **oozie.wf.application.path** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="5b682-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="5b682-331">Acrescente Olá toohello script a seguir.</span><span class="sxs-lookup"><span data-stu-id="5b682-331">Append hello following toohello script.</span></span> <span data-ttu-id="5b682-332">Esta parte verifica o status do serviço Olá Oozie web:</span><span class="sxs-lookup"><span data-stu-id="5b682-332">This part checks hello Oozie web service status:</span></span>

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="5b682-333">Acrescente Olá toohello script a seguir.</span><span class="sxs-lookup"><span data-stu-id="5b682-333">Append hello following toohello script.</span></span> <span data-ttu-id="5b682-334">Esta parte cria um trabalho Oozie:</span><span class="sxs-lookup"><span data-stu-id="5b682-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="5b682-335">Quando você envia um fluxo de trabalho, você deve fazer outro web serviço chamada toostart Olá trabalho depois que o trabalho de saudação é criado.</span><span class="sxs-lookup"><span data-stu-id="5b682-335">When you submit a workflow job, you must make another web service call toostart hello job after hello job is created.</span></span> <span data-ttu-id="5b682-336">Nesse caso, o trabalho de coordenador de saudação é disparado por vez.</span><span class="sxs-lookup"><span data-stu-id="5b682-336">In this case, hello coordinator job is triggered by time.</span></span> <span data-ttu-id="5b682-337">trabalho de saudação será iniciado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5b682-337">hello job will start automatically.</span></span>

6. <span data-ttu-id="5b682-338">Acrescente Olá toohello script a seguir.</span><span class="sxs-lookup"><span data-stu-id="5b682-338">Append hello following toohello script.</span></span> <span data-ttu-id="5b682-339">Esta parte verifica o status do trabalho Oozie hello:</span><span class="sxs-lookup"><span data-stu-id="5b682-339">This part checks hello Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. <span data-ttu-id="5b682-340">(Opcional) Acrescente Olá toohello script a seguir.</span><span class="sxs-lookup"><span data-stu-id="5b682-340">(Optional) Append hello following toohello script.</span></span>

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="5b682-341">Acrescente Olá toohello script a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b682-341">Append hello following toohello script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="5b682-342">Remova sinais de # Olá funções adicionais do toorun hello.</span><span class="sxs-lookup"><span data-stu-id="5b682-342">Remove hello # signs if you want toorun hello additional functions.</span></span>
9. <span data-ttu-id="5b682-343">Se seu cluster HDinsight for versão 2.1, substitua "https://$clusterName.azurehdinsight.net:443/oozie/v2/" por "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span><span class="sxs-lookup"><span data-stu-id="5b682-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="5b682-344">Versão 2.1 do cluster HDInsight não não dá suporte à versão 2 Olá serviços da web.</span><span class="sxs-lookup"><span data-stu-id="5b682-344">HDInsight cluster version 2.1 does not supports version 2 of hello web services.</span></span>
10. <span data-ttu-id="5b682-345">Clique em **Executar Script** ou pressione **F5** toorun script de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b682-345">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="5b682-346">saída de Hello será semelhante a:</span><span class="sxs-lookup"><span data-stu-id="5b682-346">hello output will be similar to:</span></span>

     ![Saída do fluxo de trabalho da execução do tutorial][img-runworkflow-output]
11. <span data-ttu-id="5b682-348">Conecte-se tooyour dados do banco de dados SQL toosee hello exportada.</span><span class="sxs-lookup"><span data-stu-id="5b682-348">Connect tooyour SQL Database toosee hello exported data.</span></span>

<span data-ttu-id="5b682-349">**log de erros de trabalho toocheck Olá**</span><span class="sxs-lookup"><span data-stu-id="5b682-349">**toocheck hello job error log**</span></span>

<span data-ttu-id="5b682-350">tootroubleshoot um fluxo de trabalho, arquivo de log do Oozie Olá pode ser encontrado em C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log do nó principal do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="5b682-350">tootroubleshoot a workflow, hello Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from hello cluster headnode.</span></span> <span data-ttu-id="5b682-351">Para obter informações sobre o RDP, consulte [Olá de clusters HDInsight administrando usando o portal do Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="5b682-351">For information on RDP, see [Administering HDInsight clusters using hello Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="5b682-352">**tutorial de saudação toorerun**</span><span class="sxs-lookup"><span data-stu-id="5b682-352">**toorerun hello tutorial**</span></span>

<span data-ttu-id="5b682-353">fluxo de trabalho toorerun hello, você deve executar Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b682-353">toorerun hello workflow, you must perform hello following tasks:</span></span>

* <span data-ttu-id="5b682-354">Exclua o arquivo de saída do script de Hive de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b682-354">Delete hello Hive script output file.</span></span>
* <span data-ttu-id="5b682-355">Exclua dados de saudação na tabela de log4jLogsCount hello.</span><span class="sxs-lookup"><span data-stu-id="5b682-355">Delete hello data in hello log4jLogsCount table.</span></span>

<span data-ttu-id="5b682-356">Este é um exemplo de script do Windows PowerShell que você pode usar:</span><span class="sxs-lookup"><span data-stu-id="5b682-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="5b682-357">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5b682-357">Next steps</span></span>
<span data-ttu-id="5b682-358">Neste tutorial, você aprendeu como toodefine um fluxo de trabalho do Oozie e um coordenador Oozie e como toorun um coordenador Oozie de trabalho usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b682-358">In this tutorial, you learned how toodefine an Oozie workflow and an Oozie coordinator, and how toorun an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="5b682-359">toolearn mais, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b682-359">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="5b682-360">[Introdução ao HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="5b682-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="5b682-361">[Usar o armazenamento de Blobs do Azure com o HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="5b682-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="5b682-362">[Administrar clusters HDInsight usando o Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="5b682-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="5b682-363">[Carregar dados tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="5b682-363">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="5b682-364">[Use o Sqoop com o HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="5b682-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="5b682-365">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="5b682-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="5b682-366">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="5b682-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="5b682-367">[Desenvolver programas Java MapReduce para HDInsight][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="5b682-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
