---
title: Migrar para as ferramentas do Azure Resource Manager do HDInsight | Microsoft Docs
description: Como migrar para as ferramentas de desenvolvimento do Azure Resource Manager para clusters HDInsight
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 708d22b9ce53d4dbc07c6bcde0c46dcd238291bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="migrating-to-azure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="b0f8e-103">Migrando para ferramentas de desenvolvimento baseadas no Azure Resource Manager dos clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0f8e-103">Migrating to Azure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="b0f8e-104">O HDInsight está preterindo as ferramentas baseadas em ASM (Azure Service Manager) para o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="b0f8e-105">Se você usa o Azure PowerShell, a CLI do Azure ou o SDK do .NET do HDInsight para trabalhar com clusters HDInsight, nós o incentivamos a usar as versões baseadas em ARM (Azure Resource Manager) do PowerShell, da CLI e do SDK do .NET no futuro.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-105">If you have been using Azure PowerShell, Azure CLI, or the HDInsight .NET SDK to work with HDInsight clusters, you are encouraged to use the Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="b0f8e-106">Este artigo fornece sugestões sobre como migrar para a nova abordagem baseada em ARM.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-106">This article provides pointers on how to migrate to the new ARM-based approach.</span></span> <span data-ttu-id="b0f8e-107">Sempre que aplicável, este artigo também destaca as diferenças entre as abordagens do ASM e ARM em relação ao HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-107">Wherever applicable, this article also points out the differences between the ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0f8e-108">O suporte para o PowerShell, a CLI e o SDK do .NET baseado em ASM será descontinuado em **1º de janeiro de 2017**.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-108">The support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-to-azure-resource-manager"></a><span data-ttu-id="b0f8e-109">Migrando a CLI do Azure para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b0f8e-109">Migrating Azure CLI to Azure Resource Manager</span></span>
<span data-ttu-id="b0f8e-110">Agora a CLI do Azure usa como padrão o modo ARM (Azure Resource Manager), a menos que você esteja atualizando uma instalação anterior; nesse caso, talvez seja necessário usar o comando `azure config mode arm` para alternar para o modo ARM.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-110">The Azure CLI now defaults to Azure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need to use the `azure config mode arm` command to switch to ARM mode.</span></span>

<span data-ttu-id="b0f8e-111">Os comandos básicos que a CLI do Azure fornecidos para trabalhar com o HDInsight usando o ASM (Gerenciamento de Serviços do Azure) são os mesmos que os usados no ARM; no entanto, alguns parâmetros e opções podem ter novos nomes, e há muitos novos parâmetros disponíveis ao usar o ARM.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-111">The basic commands that the Azure CLI provided to work with HDInsight using Azure Service Management (ASM) are the same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="b0f8e-112">Por exemplo, agora é possível usar `azure hdinsight cluster create` para especificar a Rede Virtual do Azure na qual um cluster deve ser criado ou usar as informações de metastore do Hive e Oozie.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-112">For example, you can now use `azure hdinsight cluster create` to specify the Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="b0f8e-113">Os comandos básicos para trabalhar com o HDInsight por meio do Azure Resource Manager são:</span><span class="sxs-lookup"><span data-stu-id="b0f8e-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="b0f8e-114">`azure hdinsight cluster create` - cria um novo cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0f8e-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="b0f8e-115">`azure hdinsight cluster delete` - exclui um cluster HDInsight existente</span><span class="sxs-lookup"><span data-stu-id="b0f8e-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="b0f8e-116">`azure hdinsight cluster show` - exibe informações sobre um cluster existente</span><span class="sxs-lookup"><span data-stu-id="b0f8e-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="b0f8e-117">`azure hdinsight cluster list` - lista os clusters HDInsight de sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="b0f8e-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="b0f8e-118">Use a opção `-h` para inspecionar os parâmetros e as opções disponíveis para cada comando.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-118">Use the `-h` switch to inspect the parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="b0f8e-119">Novos comandos</span><span class="sxs-lookup"><span data-stu-id="b0f8e-119">New commands</span></span>
<span data-ttu-id="b0f8e-120">Os novos comandos disponíveis no Azure Resource Manager são:</span><span class="sxs-lookup"><span data-stu-id="b0f8e-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="b0f8e-121">`azure hdinsight cluster resize` - altera dinamicamente o número de nós de trabalho no cluster</span><span class="sxs-lookup"><span data-stu-id="b0f8e-121">`azure hdinsight cluster resize` - dynamically changes the number of worker nodes in the cluster</span></span>
* <span data-ttu-id="b0f8e-122">`azure hdinsight cluster enable-http-access` - habilita o acesso HTTPs ao cluster (ativado por padrão)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access to the cluster (on by default)</span></span>
* <span data-ttu-id="b0f8e-123">`azure hdinsight cluster disable-http-access` - desabilita o acesso HTTPs ao cluster</span><span class="sxs-lookup"><span data-stu-id="b0f8e-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access to the cluster</span></span>
* <span data-ttu-id="b0f8e-124">`azure hdinsight script-action` - fornece comandos para criar/gerenciar as Ações de Script em um cluster</span><span class="sxs-lookup"><span data-stu-id="b0f8e-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="b0f8e-125">`azure hdinsight config` - fornece comandos para criar um arquivo de configuração que pode ser usado com o comando `hdinsight cluster create` para fornecer informações de configuração.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with the `hdinsight cluster create` command to provide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="b0f8e-126">Comandos preteridos</span><span class="sxs-lookup"><span data-stu-id="b0f8e-126">Deprecated commands</span></span>
<span data-ttu-id="b0f8e-127">Se você usar os comandos `azure hdinsight job` para enviar trabalhos ao cluster HDInsight, eles não estarão disponíveis por meio dos comandos ARM.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-127">If you use the `azure hdinsight job` commands to submit jobs to your HDInsight cluster, these are not available through the ARM commands.</span></span> <span data-ttu-id="b0f8e-128">Se você precisar enviar trabalhos ao HDInsight por meio de scripts de forma programática, será necessário usar as APIs REST fornecidas pelo HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-128">If you need to programmatically submit jobs to HDInsight from scripts, you should instead use the REST APIs provided by HDInsight.</span></span> <span data-ttu-id="b0f8e-129">Para obter mais informações sobre como enviar trabalhos usando as APIs REST, confira os seguintes documentos.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-129">For more information on submitting jobs using REST APIs, see the following documents.</span></span>

* [<span data-ttu-id="b0f8e-130">Executar trabalhos do MapReduce com o Hadoop no HDInsight usando a cURL</span><span class="sxs-lookup"><span data-stu-id="b0f8e-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="b0f8e-131">Executar consultas do Hive com o Hadoop no HDInsight usando a cURL</span><span class="sxs-lookup"><span data-stu-id="b0f8e-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="b0f8e-132">Executar trabalhos do Pig com o Hadoop no HDInsight usando a cURL</span><span class="sxs-lookup"><span data-stu-id="b0f8e-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="b0f8e-133">Para obter informações sobre outras maneiras de executar o MapReduce, Hive e Pig de forma interativa, veja [Usar o MapReduce com o Hadoop no HDInsight](hdinsight-use-mapreduce.md), [Usar o Hive com o Hadoop no HDInsight](hdinsight-use-hive.md) e [Usar o Pig com o Hadoop no HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="b0f8e-133">For information on other ways to run MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="b0f8e-134">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b0f8e-134">Examples</span></span>
<span data-ttu-id="b0f8e-135">**Criando um cluster**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-135">**Creating a cluster**</span></span>

* <span data-ttu-id="b0f8e-136">Comando antigo (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="b0f8e-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="b0f8e-137">Novo comando (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="b0f8e-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="b0f8e-138">**Excluindo um cluster**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="b0f8e-139">Comando antigo (ASM) - `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="b0f8e-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="b0f8e-140">Novo comando (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="b0f8e-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="b0f8e-141">**Listar clusters**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-141">**List clusters**</span></span>

* <span data-ttu-id="b0f8e-142">Comando antigo (ASM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="b0f8e-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="b0f8e-143">Novo comando (ARM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="b0f8e-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="b0f8e-144">Para o comando “list”, a especificação do grupo de recursos usando `-g` retornará apenas os clusters no grupo de recursos especificado.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-144">For the list command, specifying the resource group using `-g` will return only the clusters in the specified resource group.</span></span>
> 
> 

<span data-ttu-id="b0f8e-145">**Mostrar informações de cluster**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-145">**Show cluster information**</span></span>

* <span data-ttu-id="b0f8e-146">Comando antigo (ASM) - `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="b0f8e-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="b0f8e-147">Novo comando (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="b0f8e-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-to-azure-resource-manager"></a><span data-ttu-id="b0f8e-148">Migrando o Azure PowerShell para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b0f8e-148">Migrating Azure PowerShell to Azure Resource Manager</span></span>
<span data-ttu-id="b0f8e-149">As informações gerais sobre o Azure PowerShell no modo ARM (Azure Resource Manager) podem ser encontradas em [Usando o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b0f8e-149">The general information about Azure PowerShell in the Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="b0f8e-150">Os cmdlets do ARM do Azure PowerShell podem ser instalados lado a lado com os cmdlets do ASM.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-150">The Azure PowerShell ARM cmdlets can be installed side-by-side with the ASM cmdlets.</span></span> <span data-ttu-id="b0f8e-151">Os cmdlets dos dois modos podem ser diferenciados por seus nomes.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-151">The cmdlets from the two modes can be distinguished by their names.</span></span>  <span data-ttu-id="b0f8e-152">O modo ARM contém *AzureRmHDInsight* nos nomes de cmdlet, em comparação com *AzureHDInsight* no modo ASM.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-152">The ARM mode has *AzureRmHDInsight* in the cmdlet names comparing to *AzureHDInsight* in the ASM mode.</span></span>  <span data-ttu-id="b0f8e-153">Por exemplo, *New-AzureRmHDInsightCluster* versus *New-AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="b0f8e-154">Os parâmetros e as opções podem ter nomes novos, e há muitos novos parâmetros disponíveis ao usar o ARM.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="b0f8e-155">Por exemplo, vários cmdlets exigem uma nova opção chamada *-ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="b0f8e-156">Antes de usar os cmdlets do HDInsight, é necessário se conectar à sua conta do Azure e criar um novo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="b0f8e-156">Before you can use the HDInsight cmdlets, you must connect to your Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="b0f8e-157">Login-AzureRmAccount ou [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0f8e-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="b0f8e-158">Veja [Autenticando uma entidade de serviço com o Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="b0f8e-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b0f8e-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="b0f8e-160">Cmdlets renomeados</span><span class="sxs-lookup"><span data-stu-id="b0f8e-160">Renamed cmdlets</span></span>
<span data-ttu-id="b0f8e-161">Para listar os cmdlets do ASM do HDInsight no console do Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b0f8e-161">To list the HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="b0f8e-162">A tabela a seguir lista os cmdlets do ASM e seus nomes no modo ARM:</span><span class="sxs-lookup"><span data-stu-id="b0f8e-162">The following table lists the ASM cmdlets and their names in the ARM mode:</span></span>

| <span data-ttu-id="b0f8e-163">Cmdlets do ASM</span><span class="sxs-lookup"><span data-stu-id="b0f8e-163">ASM cmdlets</span></span> | <span data-ttu-id="b0f8e-164">Cmdlets do ARM</span><span class="sxs-lookup"><span data-stu-id="b0f8e-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="b0f8e-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="b0f8e-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="b0f8e-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="b0f8e-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="b0f8e-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="b0f8e-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="b0f8e-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="b0f8e-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="b0f8e-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="b0f8e-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="b0f8e-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="b0f8e-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="b0f8e-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="b0f8e-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="b0f8e-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="b0f8e-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="b0f8e-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="b0f8e-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="b0f8e-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="b0f8e-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="b0f8e-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="b0f8e-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="b0f8e-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="b0f8e-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="b0f8e-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="b0f8e-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="b0f8e-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="b0f8e-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="b0f8e-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="b0f8e-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="b0f8e-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="b0f8e-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="b0f8e-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="b0f8e-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="b0f8e-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="b0f8e-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="b0f8e-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="b0f8e-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="b0f8e-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="b0f8e-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="b0f8e-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="b0f8e-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="b0f8e-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="b0f8e-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="b0f8e-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="b0f8e-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="b0f8e-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="b0f8e-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="b0f8e-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="b0f8e-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="b0f8e-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="b0f8e-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="b0f8e-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="b0f8e-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="b0f8e-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="b0f8e-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="b0f8e-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="b0f8e-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="b0f8e-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="b0f8e-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="b0f8e-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="b0f8e-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="b0f8e-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="b0f8e-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="b0f8e-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="b0f8e-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="b0f8e-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="b0f8e-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="b0f8e-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="b0f8e-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="b0f8e-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="b0f8e-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="b0f8e-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="b0f8e-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="b0f8e-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="b0f8e-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="b0f8e-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="b0f8e-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="b0f8e-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="b0f8e-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="b0f8e-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="b0f8e-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="b0f8e-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="b0f8e-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="b0f8e-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="b0f8e-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="b0f8e-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="b0f8e-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="b0f8e-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="b0f8e-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="b0f8e-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="b0f8e-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="b0f8e-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="b0f8e-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="b0f8e-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="b0f8e-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="b0f8e-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="b0f8e-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="b0f8e-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="b0f8e-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="b0f8e-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="b0f8e-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="b0f8e-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="b0f8e-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="b0f8e-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="b0f8e-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="b0f8e-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="b0f8e-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="b0f8e-219">Novos cmdlets</span><span class="sxs-lookup"><span data-stu-id="b0f8e-219">New cmdlets</span></span>
<span data-ttu-id="b0f8e-220">Apresentamos a seguir os novos cmdlets que só estão disponíveis no modo ARM.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-220">The following are the new cmdlets that are only available in the ARM mode.</span></span> 

<span data-ttu-id="b0f8e-221">**Cmdlets relacionados à ação de script:**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="b0f8e-222">**Get-AzureRmHDInsightPersistedScriptAction**: obtém as ações de script persistentes de um cluster e as lista em ordem cronológica ou obtém detalhes de uma ação de script persistente especificada.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets the persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="b0f8e-223">**Get-AzureRmHDInsightScriptActionHistory**: obtém o histórico de ação de script de um cluster e o lista em ordem cronológica inversa ou obtém detalhes de uma ação de script executada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets the script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="b0f8e-224">**Remove-AzureRmHDInsightPersistedScriptAction**: remove uma ação de script persistente de um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="b0f8e-225">**Set-AzureRmHDInsightPersistedScriptAction**: define uma ação de script executada anteriormente como uma ação de script persistente.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action to be a persisted script action.</span></span>
* <span data-ttu-id="b0f8e-226">**Submit-AzureRmHDInsightScriptAction**: envia uma nova ação de script para um cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action to an Azure HDInsight cluster.</span></span> 

<span data-ttu-id="b0f8e-227">Para obter mais informações de uso, veja [Personalizar clusters HDInsight baseados em Linux usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b0f8e-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="b0f8e-228">**Cmdlets relacionados à identidade do cluster:**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="b0f8e-229">**Add-AzureRmHDInsightClusterIdentity**: adiciona uma identidade de cluster a um objeto de configuração de cluster para que o cluster HDInsight possa acessar Repositórios Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity to a cluster configuration object so that the HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="b0f8e-230">Veja [Criar um cluster HDInsight com o Repositório Data Lake usando o Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b0f8e-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="b0f8e-231">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b0f8e-231">Examples</span></span>
<span data-ttu-id="b0f8e-232">**Criar cluster**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-232">**Create cluster**</span></span>

<span data-ttu-id="b0f8e-233">Comando antigo (ASM):</span><span class="sxs-lookup"><span data-stu-id="b0f8e-233">Old command (ASM):</span></span> 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

<span data-ttu-id="b0f8e-234">Novo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="b0f8e-234">New command (ARM):</span></span>

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


<span data-ttu-id="b0f8e-235">**Excluir cluster**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-235">**Delete cluster**</span></span>

<span data-ttu-id="b0f8e-236">Comando antigo (ASM):</span><span class="sxs-lookup"><span data-stu-id="b0f8e-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="b0f8e-237">Novo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="b0f8e-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="b0f8e-238">**Listar clusters**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-238">**List cluster**</span></span>

<span data-ttu-id="b0f8e-239">Comando antigo (ASM):</span><span class="sxs-lookup"><span data-stu-id="b0f8e-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="b0f8e-240">Novo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="b0f8e-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="b0f8e-241">**Mostrar cluster**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-241">**Show cluster**</span></span>

<span data-ttu-id="b0f8e-242">Comando antigo (ASM):</span><span class="sxs-lookup"><span data-stu-id="b0f8e-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="b0f8e-243">Novo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="b0f8e-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="b0f8e-244">Outras amostras</span><span class="sxs-lookup"><span data-stu-id="b0f8e-244">Other samples</span></span>
* [<span data-ttu-id="b0f8e-245">Criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0f8e-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="b0f8e-246">Enviar trabalhos Hive</span><span class="sxs-lookup"><span data-stu-id="b0f8e-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="b0f8e-247">Enviar trabalhos do Pig</span><span class="sxs-lookup"><span data-stu-id="b0f8e-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="b0f8e-248">Enviar trabalhos do Sqoop</span><span class="sxs-lookup"><span data-stu-id="b0f8e-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-to-the-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="b0f8e-249">Migrando para o SDK do .NET do HDInsight baseado em ARM</span><span class="sxs-lookup"><span data-stu-id="b0f8e-249">Migrating to the ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="b0f8e-250">O [SDK do .NET do HDInsight](https://msdn.microsoft.com/library/azure/mt416619.aspx) baseado em ASM (Gerenciamento de Serviços do Azure) foi preterido.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-250">The Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="b0f8e-251">Nós o incentivamos a usar o [SDK do .NET do HDInsight](https://msdn.microsoft.com/library/azure/mt271028.aspx)baseado em ARM (Gerenciamento de Recursos do Azure).</span><span class="sxs-lookup"><span data-stu-id="b0f8e-251">You are encouraged to use the Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="b0f8e-252">Os seguintes pacotes HDInsight baseados em ASM estão sendo preteridos.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-252">The following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="b0f8e-253">Esta seção fornece sugestões de mais informações sobre como executar determinadas tarefas usando o SDK baseado em ARM.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-253">This section provides pointers to more information on how to perform certain tasks using the ARM-based SDK.</span></span>

| <span data-ttu-id="b0f8e-254">Como usar o SDK do HDInsight baseado em ARM</span><span class="sxs-lookup"><span data-stu-id="b0f8e-254">How to... using the ARM-based HDInsight SDK</span></span> | <span data-ttu-id="b0f8e-255">Links</span><span class="sxs-lookup"><span data-stu-id="b0f8e-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="b0f8e-256">Criar clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="b0f8e-257">Veja [Criar clusters HDInsight usando o SDK do .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="b0f8e-258">Personalizar um cluster usando a Ação de Script com o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="b0f8e-259">Veja [Personalizar os clusters HDInsight do Linux usando a Ação de Script](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="b0f8e-260">Autenticar aplicativos de forma interativa usando o Azure Active Directory com o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="b0f8e-261">Veja [Executar consultas do Hive usando o SDK do .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b0f8e-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="b0f8e-262">O trecho de código neste artigo usa o método de autenticação interativa.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-262">The code snippet in this article uses the interactive authentication approach.</span></span> |
| <span data-ttu-id="b0f8e-263">Autenticar aplicativos de forma não interativa usando o Azure Active Directory com o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="b0f8e-264">Veja [Criar aplicativos não interativos para o HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="b0f8e-265">Enviar um trabalho do Hive usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="b0f8e-266">Veja [Enviar trabalhos do Hive](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="b0f8e-267">Enviar um trabalho do Pig usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="b0f8e-268">Veja [Enviar trabalhos do Pig](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="b0f8e-269">Enviar um trabalho do Sqoop usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="b0f8e-270">Veja [Enviar trabalhos do Sqoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="b0f8e-271">Listar clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="b0f8e-272">Veja [Listar os clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="b0f8e-273">Escalar clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="b0f8e-274">Veja [Escalar clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="b0f8e-275">Conceder/revogar acesso aos clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-275">Grant/revoke access to HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="b0f8e-276">Veja [Conceder/revogar acesso aos clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-276">See [Grant/revoke access to HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="b0f8e-277">Atualizar credenciais de usuário HTTP de clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="b0f8e-278">Veja [Atualizar credenciais de usuário HTTP de clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="b0f8e-279">Encontrar a conta de armazenamento padrão para clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-279">Find the default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="b0f8e-280">Veja [Encontrar a conta de armazenamento padrão para clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-280">See [Find the default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="b0f8e-281">Excluir clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0f8e-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="b0f8e-282">Veja [Excluir clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="b0f8e-283">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b0f8e-283">Examples</span></span>
<span data-ttu-id="b0f8e-284">Estes são alguns exemplos sobre como uma operação é executada usando o SDK baseado em ASM e o trecho de código equivalente para o SDK baseado em ARM.</span><span class="sxs-lookup"><span data-stu-id="b0f8e-284">Following are some examples on how an operation is performed using the ASM-based SDK and the equivalent code snippet for the ARM-based SDK.</span></span>

<span data-ttu-id="b0f8e-285">**Criando um cliente CRUD do cluster**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="b0f8e-286">Comando antigo (ASM)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs the application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="b0f8e-287">Novo comando (ARM) (Autorização de entidade de serviço)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log the application in as itself, rather than on behalf of a specific user.
        //For details, including how to set up the application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="b0f8e-288">Novo comando (ARM) (Autorização de usuário)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log the application in on behalf of the user.
        //The end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="b0f8e-289">**Criando um cluster**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-289">**Creating a cluster**</span></span>

* <span data-ttu-id="b0f8e-290">Comando antigo (ASM)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-290">Old command (ASM)</span></span>
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* <span data-ttu-id="b0f8e-291">Novo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-291">New command (ARM)</span></span>
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

<span data-ttu-id="b0f8e-292">**Habilitando o acesso HTTP**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="b0f8e-293">Comando antigo (ASM)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="b0f8e-294">Novo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="b0f8e-295">**Excluindo um cluster**</span><span class="sxs-lookup"><span data-stu-id="b0f8e-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="b0f8e-296">Comando antigo (ASM)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="b0f8e-297">Novo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="b0f8e-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

