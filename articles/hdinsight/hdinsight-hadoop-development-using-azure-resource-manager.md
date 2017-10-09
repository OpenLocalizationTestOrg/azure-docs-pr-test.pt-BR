---
title: aaaMigrate tooAzure Gerenciador de recursos de ferramentas para HDInsight | Microsoft Docs
description: Como as ferramentas de toomigrate tooAzure Gerenciador de recursos de desenvolvimento para clusters de HDInsight
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
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="7e386-103">Ferramentas de desenvolvimento com base no Gerenciador de recursos tooAzure migrando para clusters de HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e386-103">Migrating tooAzure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="7e386-104">O HDInsight está preterindo as ferramentas baseadas em ASM (Azure Service Manager) para o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e386-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="7e386-105">Se você tiver sido usar Azure PowerShell, CLI do Azure ou Olá HDInsight .NET SDK toowork com clusters de HDInsight, você está toouse incentivados hello Azure Resource Manager ARM versões do PowerShell, CLI e .NET SDK no futuro.</span><span class="sxs-lookup"><span data-stu-id="7e386-105">If you have been using Azure PowerShell, Azure CLI, or hello HDInsight .NET SDK toowork with HDInsight clusters, you are encouraged toouse hello Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="7e386-106">Este artigo fornece ponteiros sobre como toomigrate toohello nova baseado em ARM abordagem.</span><span class="sxs-lookup"><span data-stu-id="7e386-106">This article provides pointers on how toomigrate toohello new ARM-based approach.</span></span> <span data-ttu-id="7e386-107">Onde aplicável, este artigo também aponta diferenças Olá entre Olá abordagens ASM e ARM para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e386-107">Wherever applicable, this article also points out hello differences between hello ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e386-108">suporte a saudação ASM com base em PowerShell, CLI, e .NET SDK será descontinuado em **1 de janeiro de 2017**.</span><span class="sxs-lookup"><span data-stu-id="7e386-108">hello support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a><span data-ttu-id="7e386-109">Migrando tooAzure de CLI do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7e386-109">Migrating Azure CLI tooAzure Resource Manager</span></span>
<span data-ttu-id="7e386-110">Olá CLI do Azure agora padrões tooAzure modo de Resource Manager (ARM), a menos que você estiver atualizando de uma instalação anterior; Nesse caso, talvez seja necessário toouse Olá `azure config mode arm` modo do comando tooswitch tooARM.</span><span class="sxs-lookup"><span data-stu-id="7e386-110">hello Azure CLI now defaults tooAzure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need toouse hello `azure config mode arm` command tooswitch tooARM mode.</span></span>

<span data-ttu-id="7e386-111">comandos de saudação que Olá CLI do Azure acompanha toowork HDInsight usando o gerenciamento de serviço do Azure (ASM) são Olá mesmo ao usar ARM; No entanto alguns parâmetros e comutadores podem ter novos nomes, e há muitos novos parâmetros disponíveis ao usar ARM.</span><span class="sxs-lookup"><span data-stu-id="7e386-111">hello basic commands that hello Azure CLI provided toowork with HDInsight using Azure Service Management (ASM) are hello same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="7e386-112">Por exemplo, você pode agora usar `azure hdinsight cluster create` toospecify Olá rede Virtual do Azure que deve ser criado em um cluster ou Hive e Oozie metastore informações.</span><span class="sxs-lookup"><span data-stu-id="7e386-112">For example, you can now use `azure hdinsight cluster create` toospecify hello Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="7e386-113">Os comandos básicos para trabalhar com o HDInsight por meio do Azure Resource Manager são:</span><span class="sxs-lookup"><span data-stu-id="7e386-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="7e386-114">`azure hdinsight cluster create` - cria um novo cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e386-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="7e386-115">`azure hdinsight cluster delete` - exclui um cluster HDInsight existente</span><span class="sxs-lookup"><span data-stu-id="7e386-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="7e386-116">`azure hdinsight cluster show` - exibe informações sobre um cluster existente</span><span class="sxs-lookup"><span data-stu-id="7e386-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="7e386-117">`azure hdinsight cluster list` - lista os clusters HDInsight de sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="7e386-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="7e386-118">Saudação de uso `-h` alternar parâmetros de saudação tooinspect e as opções disponíveis para cada comando.</span><span class="sxs-lookup"><span data-stu-id="7e386-118">Use hello `-h` switch tooinspect hello parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="7e386-119">Novos comandos</span><span class="sxs-lookup"><span data-stu-id="7e386-119">New commands</span></span>
<span data-ttu-id="7e386-120">Os novos comandos disponíveis no Azure Resource Manager são:</span><span class="sxs-lookup"><span data-stu-id="7e386-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="7e386-121">`azure hdinsight cluster resize`-dinamicamente as alterações Olá número de nós de trabalho no cluster Olá</span><span class="sxs-lookup"><span data-stu-id="7e386-121">`azure hdinsight cluster resize` - dynamically changes hello number of worker nodes in hello cluster</span></span>
* <span data-ttu-id="7e386-122">`azure hdinsight cluster enable-http-access`-permite que o cluster de toohello acesso HTTPs (em por padrão)</span><span class="sxs-lookup"><span data-stu-id="7e386-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access toohello cluster (on by default)</span></span>
* <span data-ttu-id="7e386-123">`azure hdinsight cluster disable-http-access`-desativa o cluster de toohello acesso HTTPs</span><span class="sxs-lookup"><span data-stu-id="7e386-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access toohello cluster</span></span>
* <span data-ttu-id="7e386-124">`azure hdinsight script-action` - fornece comandos para criar/gerenciar as Ações de Script em um cluster</span><span class="sxs-lookup"><span data-stu-id="7e386-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="7e386-125">`azure hdinsight config`-fornece comandos para criar um arquivo de configuração que pode ser usado com hello `hdinsight cluster create` comando tooprovide informações de configuração.</span><span class="sxs-lookup"><span data-stu-id="7e386-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with hello `hdinsight cluster create` command tooprovide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="7e386-126">Comandos preteridos</span><span class="sxs-lookup"><span data-stu-id="7e386-126">Deprecated commands</span></span>
<span data-ttu-id="7e386-127">Se você usar o hello `azure hdinsight job` comandos toosubmit trabalhos tooyour HDInsight cluster não estiverem disponíveis por meio de comandos ARM hello.</span><span class="sxs-lookup"><span data-stu-id="7e386-127">If you use hello `azure hdinsight job` commands toosubmit jobs tooyour HDInsight cluster, these are not available through hello ARM commands.</span></span> <span data-ttu-id="7e386-128">Se você precisar tooprogrammatically tooHDInsight de trabalhos de envio de scripts, em vez disso, você deve usar Olá APIs de REST fornecida pelo HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e386-128">If you need tooprogrammatically submit jobs tooHDInsight from scripts, you should instead use hello REST APIs provided by HDInsight.</span></span> <span data-ttu-id="7e386-129">Para obter mais informações sobre como enviar trabalhos usando APIs REST, consulte Olá documentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="7e386-129">For more information on submitting jobs using REST APIs, see hello following documents.</span></span>

* [<span data-ttu-id="7e386-130">Executar trabalhos do MapReduce com o Hadoop no HDInsight usando a cURL</span><span class="sxs-lookup"><span data-stu-id="7e386-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="7e386-131">Executar consultas do Hive com o Hadoop no HDInsight usando a cURL</span><span class="sxs-lookup"><span data-stu-id="7e386-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="7e386-132">Executar trabalhos do Pig com o Hadoop no HDInsight usando a cURL</span><span class="sxs-lookup"><span data-stu-id="7e386-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="7e386-133">Para obter informações sobre outra maneiras de toorun MapReduce, Hive e Pig interativamente, consulte [Use MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md), [uso de Hive do Hadoop no HDInsight](hdinsight-use-hive.md), e [usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="7e386-133">For information on other ways toorun MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="7e386-134">Exemplos</span><span class="sxs-lookup"><span data-stu-id="7e386-134">Examples</span></span>
<span data-ttu-id="7e386-135">**Criando um cluster**</span><span class="sxs-lookup"><span data-stu-id="7e386-135">**Creating a cluster**</span></span>

* <span data-ttu-id="7e386-136">Comando antigo (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="7e386-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="7e386-137">Novo comando (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="7e386-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="7e386-138">**Excluindo um cluster**</span><span class="sxs-lookup"><span data-stu-id="7e386-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="7e386-139">Comando antigo (ASM) - `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="7e386-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="7e386-140">Novo comando (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="7e386-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="7e386-141">**Listar clusters**</span><span class="sxs-lookup"><span data-stu-id="7e386-141">**List clusters**</span></span>

* <span data-ttu-id="7e386-142">Comando antigo (ASM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="7e386-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="7e386-143">Novo comando (ARM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="7e386-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="7e386-144">Para o comando lista hello, especificando hello usando o recurso grupo `-g` retornará apenas os clusters Olá no grupo de recursos especificado hello.</span><span class="sxs-lookup"><span data-stu-id="7e386-144">For hello list command, specifying hello resource group using `-g` will return only hello clusters in hello specified resource group.</span></span>
> 
> 

<span data-ttu-id="7e386-145">**Mostrar informações de cluster**</span><span class="sxs-lookup"><span data-stu-id="7e386-145">**Show cluster information**</span></span>

* <span data-ttu-id="7e386-146">Comando antigo (ASM) - `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="7e386-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="7e386-147">Novo comando (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="7e386-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a><span data-ttu-id="7e386-148">Migração do Azure PowerShell tooAzure Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="7e386-148">Migrating Azure PowerShell tooAzure Resource Manager</span></span>
<span data-ttu-id="7e386-149">Olá informações gerais sobre o Azure PowerShell no modo do hello Azure Resource Manager (ARM) podem ser encontradas em [usando o PowerShell do Azure com o Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7e386-149">hello general information about Azure PowerShell in hello Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="7e386-150">Olá cmdlets do Azure PowerShell ARM pode ser instalada lado a lado com hello ASM cmdlets.</span><span class="sxs-lookup"><span data-stu-id="7e386-150">hello Azure PowerShell ARM cmdlets can be installed side-by-side with hello ASM cmdlets.</span></span> <span data-ttu-id="7e386-151">cmdlets de saudação de dois modos de saudação podem ser diferenciados por seus nomes.</span><span class="sxs-lookup"><span data-stu-id="7e386-151">hello cmdlets from hello two modes can be distinguished by their names.</span></span>  <span data-ttu-id="7e386-152">o modo ARM Olá tem *AzureRmHDInsight* em nomes de cmdlet Olá comparando muito*AzureHDInsight* no modo ASM hello.</span><span class="sxs-lookup"><span data-stu-id="7e386-152">hello ARM mode has *AzureRmHDInsight* in hello cmdlet names comparing too*AzureHDInsight* in hello ASM mode.</span></span>  <span data-ttu-id="7e386-153">Por exemplo, *New-AzureRmHDInsightCluster* versus *New-AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="7e386-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="7e386-154">Os parâmetros e as opções podem ter nomes novos, e há muitos novos parâmetros disponíveis ao usar o ARM.</span><span class="sxs-lookup"><span data-stu-id="7e386-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="7e386-155">Por exemplo, vários cmdlets exigem uma nova opção chamada *-ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="7e386-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="7e386-156">Antes de usar cmdlets do HDInsight Olá, você deve conectar tooyour conta do Azure e criar um novo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="7e386-156">Before you can use hello HDInsight cmdlets, you must connect tooyour Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="7e386-157">Login-AzureRmAccount ou [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e386-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="7e386-158">Veja [Autenticando uma entidade de serviço com o Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="7e386-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="7e386-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7e386-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="7e386-160">Cmdlets renomeados</span><span class="sxs-lookup"><span data-stu-id="7e386-160">Renamed cmdlets</span></span>
<span data-ttu-id="7e386-161">Olá toolist cmdlets de HDInsight ASM no console do Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7e386-161">toolist hello HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="7e386-162">Olá tabela a seguir lista Olá ASM cmdlets e os nomes no modo ARM hello:</span><span class="sxs-lookup"><span data-stu-id="7e386-162">hello following table lists hello ASM cmdlets and their names in hello ARM mode:</span></span>

| <span data-ttu-id="7e386-163">Cmdlets do ASM</span><span class="sxs-lookup"><span data-stu-id="7e386-163">ASM cmdlets</span></span> | <span data-ttu-id="7e386-164">Cmdlets do ARM</span><span class="sxs-lookup"><span data-stu-id="7e386-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="7e386-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="7e386-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="7e386-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="7e386-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="7e386-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="7e386-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="7e386-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="7e386-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="7e386-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="7e386-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="7e386-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="7e386-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="7e386-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="7e386-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="7e386-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="7e386-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="7e386-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7e386-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="7e386-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7e386-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="7e386-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7e386-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="7e386-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7e386-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="7e386-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="7e386-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="7e386-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="7e386-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="7e386-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="7e386-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="7e386-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="7e386-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="7e386-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7e386-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="7e386-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7e386-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="7e386-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="7e386-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="7e386-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7e386-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="7e386-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="7e386-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="7e386-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="7e386-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="7e386-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7e386-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="7e386-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7e386-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="7e386-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="7e386-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="7e386-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="7e386-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="7e386-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7e386-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="7e386-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7e386-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="7e386-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7e386-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="7e386-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7e386-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="7e386-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7e386-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="7e386-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7e386-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="7e386-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7e386-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="7e386-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7e386-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="7e386-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7e386-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="7e386-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7e386-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="7e386-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7e386-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="7e386-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7e386-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="7e386-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7e386-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="7e386-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7e386-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="7e386-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="7e386-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="7e386-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7e386-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="7e386-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="7e386-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="7e386-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="7e386-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="7e386-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="7e386-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="7e386-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="7e386-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="7e386-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7e386-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="7e386-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7e386-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="7e386-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7e386-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="7e386-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7e386-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="7e386-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7e386-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="7e386-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7e386-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="7e386-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7e386-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="7e386-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7e386-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="7e386-219">Novos cmdlets</span><span class="sxs-lookup"><span data-stu-id="7e386-219">New cmdlets</span></span>
<span data-ttu-id="7e386-220">Olá seguem Olá novos cmdlets que só estão disponíveis no modo ARM hello.</span><span class="sxs-lookup"><span data-stu-id="7e386-220">hello following are hello new cmdlets that are only available in hello ARM mode.</span></span> 

<span data-ttu-id="7e386-221">**Cmdlets relacionados à ação de script:**</span><span class="sxs-lookup"><span data-stu-id="7e386-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="7e386-222">**Get-AzureRmHDInsightPersistedScriptAction**: Olá obtém persistentes ações de script para um cluster de lista em ordem cronológica e obtém os detalhes para uma ação de script persistentes especificado.</span><span class="sxs-lookup"><span data-stu-id="7e386-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets hello persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="7e386-223">**Get-AzureRmHDInsightScriptActionHistory**: obtém o histórico de ação de script hello para um cluster e lista em ordem cronológica inversa ou obtém os detalhes de uma ação de script executado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7e386-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets hello script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="7e386-224">**Remove-AzureRmHDInsightPersistedScriptAction**: remove uma ação de script persistente de um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e386-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="7e386-225">**Conjunto AzureRmHDInsightPersistedScriptAction**: define um toobe de ação do script executado anteriormente uma ação de script persistentes.</span><span class="sxs-lookup"><span data-stu-id="7e386-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action toobe a persisted script action.</span></span>
* <span data-ttu-id="7e386-226">**Enviar AzureRmHDInsightScriptAction**: envia um novo cluster de HDInsight do Azure de tooan de ação de script.</span><span class="sxs-lookup"><span data-stu-id="7e386-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action tooan Azure HDInsight cluster.</span></span> 

<span data-ttu-id="7e386-227">Para obter mais informações de uso, veja [Personalizar clusters HDInsight baseados em Linux usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7e386-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="7e386-228">**Cmdlets relacionados à identidade do cluster:**</span><span class="sxs-lookup"><span data-stu-id="7e386-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="7e386-229">**Adicionar AzureRmHDInsightClusterIdentity**: adiciona um objeto de configuração de cluster do cluster identidade tooa para que hello cluster HDInsight pode acessar repositórios do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="7e386-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity tooa cluster configuration object so that hello HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="7e386-230">Veja [Criar um cluster HDInsight com o Repositório Data Lake usando o Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7e386-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="7e386-231">Exemplos</span><span class="sxs-lookup"><span data-stu-id="7e386-231">Examples</span></span>
<span data-ttu-id="7e386-232">**Criar cluster**</span><span class="sxs-lookup"><span data-stu-id="7e386-232">**Create cluster**</span></span>

<span data-ttu-id="7e386-233">Comando antigo (ASM):</span><span class="sxs-lookup"><span data-stu-id="7e386-233">Old command (ASM):</span></span> 

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

<span data-ttu-id="7e386-234">Novo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="7e386-234">New command (ARM):</span></span>

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


<span data-ttu-id="7e386-235">**Excluir cluster**</span><span class="sxs-lookup"><span data-stu-id="7e386-235">**Delete cluster**</span></span>

<span data-ttu-id="7e386-236">Comando antigo (ASM):</span><span class="sxs-lookup"><span data-stu-id="7e386-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="7e386-237">Novo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="7e386-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="7e386-238">**Listar clusters**</span><span class="sxs-lookup"><span data-stu-id="7e386-238">**List cluster**</span></span>

<span data-ttu-id="7e386-239">Comando antigo (ASM):</span><span class="sxs-lookup"><span data-stu-id="7e386-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="7e386-240">Novo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="7e386-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="7e386-241">**Mostrar cluster**</span><span class="sxs-lookup"><span data-stu-id="7e386-241">**Show cluster**</span></span>

<span data-ttu-id="7e386-242">Comando antigo (ASM):</span><span class="sxs-lookup"><span data-stu-id="7e386-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="7e386-243">Novo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="7e386-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="7e386-244">Outras amostras</span><span class="sxs-lookup"><span data-stu-id="7e386-244">Other samples</span></span>
* [<span data-ttu-id="7e386-245">Criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e386-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="7e386-246">Enviar trabalhos Hive</span><span class="sxs-lookup"><span data-stu-id="7e386-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="7e386-247">Enviar trabalhos do Pig</span><span class="sxs-lookup"><span data-stu-id="7e386-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="7e386-248">Enviar trabalhos do Sqoop</span><span class="sxs-lookup"><span data-stu-id="7e386-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="7e386-249">Migrando toohello baseado em ARM HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7e386-249">Migrating toohello ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="7e386-250">Olá baseados no gerenciamento de serviço do Azure [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) agora está obsoleta.</span><span class="sxs-lookup"><span data-stu-id="7e386-250">hello Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="7e386-251">São incentivado toouse Olá baseados no gerenciamento de recursos do Azure [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e386-251">You are encouraged toouse hello Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="7e386-252">Olá seguintes pacotes de HDInsight com base em ASM estão sendo substituídos.</span><span class="sxs-lookup"><span data-stu-id="7e386-252">hello following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="7e386-253">Esta seção fornece ponteiros toomore informações sobre como tooperform certas tarefas usando Olá SDK baseado em ARM.</span><span class="sxs-lookup"><span data-stu-id="7e386-253">This section provides pointers toomore information on how tooperform certain tasks using hello ARM-based SDK.</span></span>

| <span data-ttu-id="7e386-254">Como … usando Olá baseado em ARM HDInsight SDK</span><span class="sxs-lookup"><span data-stu-id="7e386-254">How to... using hello ARM-based HDInsight SDK</span></span> | <span data-ttu-id="7e386-255">Links</span><span class="sxs-lookup"><span data-stu-id="7e386-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="7e386-256">Criar clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7e386-257">Veja [Criar clusters HDInsight usando o SDK do .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7e386-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="7e386-258">Personalizar um cluster usando a Ação de Script com o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="7e386-259">Veja [Personalizar os clusters HDInsight do Linux usando a Ação de Script](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="7e386-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="7e386-260">Autenticar aplicativos de forma interativa usando o Azure Active Directory com o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="7e386-261">Veja [Executar consultas do Hive usando o SDK do .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7e386-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="7e386-262">trecho de código Olá neste artigo usa o método de autenticação interativa do hello.</span><span class="sxs-lookup"><span data-stu-id="7e386-262">hello code snippet in this article uses hello interactive authentication approach.</span></span> |
| <span data-ttu-id="7e386-263">Autenticar aplicativos de forma não interativa usando o Azure Active Directory com o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="7e386-264">Veja [Criar aplicativos não interativos para o HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="7e386-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="7e386-265">Enviar um trabalho do Hive usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="7e386-266">Veja [Enviar trabalhos do Hive](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7e386-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="7e386-267">Enviar um trabalho do Pig usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="7e386-268">Veja [Enviar trabalhos do Pig](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7e386-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="7e386-269">Enviar um trabalho do Sqoop usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="7e386-270">Veja [Enviar trabalhos do Sqoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7e386-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="7e386-271">Listar clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7e386-272">Veja [Listar os clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="7e386-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="7e386-273">Escalar clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7e386-274">Veja [Escalar clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="7e386-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="7e386-275">Grant/revoke acesso tooHDInsight clusters usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-275">Grant/revoke access tooHDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7e386-276">Consulte [clusters de tooHDInsight acesso Grant/revoke](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="7e386-276">See [Grant/revoke access tooHDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="7e386-277">Atualizar credenciais de usuário HTTP de clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7e386-278">Veja [Atualizar credenciais de usuário HTTP de clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="7e386-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="7e386-279">Localizar a conta de armazenamento padrão Olá para clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-279">Find hello default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7e386-280">Consulte [localizar a conta de armazenamento padrão Olá para clusters de HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="7e386-280">See [Find hello default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="7e386-281">Excluir clusters HDInsight usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7e386-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7e386-282">Veja [Excluir clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="7e386-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="7e386-283">Exemplos</span><span class="sxs-lookup"><span data-stu-id="7e386-283">Examples</span></span>
<span data-ttu-id="7e386-284">Estes são alguns exemplos de como uma operação é executada usando hello SDK do ASM e trecho de código equivalentes Olá para Olá SDK baseado em ARM.</span><span class="sxs-lookup"><span data-stu-id="7e386-284">Following are some examples on how an operation is performed using hello ASM-based SDK and hello equivalent code snippet for hello ARM-based SDK.</span></span>

<span data-ttu-id="7e386-285">**Criando um cliente CRUD do cluster**</span><span class="sxs-lookup"><span data-stu-id="7e386-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="7e386-286">Comando antigo (ASM)</span><span class="sxs-lookup"><span data-stu-id="7e386-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="7e386-287">Novo comando (ARM) (Autorização de entidade de serviço)</span><span class="sxs-lookup"><span data-stu-id="7e386-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="7e386-288">Novo comando (ARM) (Autorização de usuário)</span><span class="sxs-lookup"><span data-stu-id="7e386-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="7e386-289">**Criando um cluster**</span><span class="sxs-lookup"><span data-stu-id="7e386-289">**Creating a cluster**</span></span>

* <span data-ttu-id="7e386-290">Comando antigo (ASM)</span><span class="sxs-lookup"><span data-stu-id="7e386-290">Old command (ASM)</span></span>
  
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
* <span data-ttu-id="7e386-291">Novo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="7e386-291">New command (ARM)</span></span>
  
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

<span data-ttu-id="7e386-292">**Habilitando o acesso HTTP**</span><span class="sxs-lookup"><span data-stu-id="7e386-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="7e386-293">Comando antigo (ASM)</span><span class="sxs-lookup"><span data-stu-id="7e386-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="7e386-294">Novo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="7e386-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="7e386-295">**Excluindo um cluster**</span><span class="sxs-lookup"><span data-stu-id="7e386-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="7e386-296">Comando antigo (ASM)</span><span class="sxs-lookup"><span data-stu-id="7e386-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="7e386-297">Novo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="7e386-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

