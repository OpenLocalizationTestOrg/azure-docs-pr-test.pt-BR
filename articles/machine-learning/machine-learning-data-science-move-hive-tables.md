---
title: aaaCreate tabelas de Hive e carregar dados do armazenamento de BLOBs do Azure | Microsoft Docs
description: Criar tabelas de Hive e carregar dados nas tabelas de toohive de blob
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="e2bf7-103">Criar tabelas do Hive e carregar dados do Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="e2bf7-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="e2bf7-104">Neste tópico, são apresentadas consultas genéricas do Hive que criam tabelas do Hive e carregam dados do armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="e2bf7-105">Orientação também é fornecida sobre particionamento de tabelas de Hive e uso Olá linha de otimização Colunar (ORC) formatação tooimprove desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-105">Some guidance is also provided on partitioning Hive tables and on using hello Optimized Row Columnar (ORC) formatting tooimprove query performance.</span></span>

<span data-ttu-id="e2bf7-106">Isso **menu** links tootopics que descrevem como dados tooingest em ambientes de destino onde os dados saudação podem ser armazenados e processados durante Olá processo de ciência de dados da equipe (TDSP).</span><span class="sxs-lookup"><span data-stu-id="e2bf7-106">This **menu** links tootopics that describe how tooingest data into target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="e2bf7-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e2bf7-107">Prerequisites</span></span>
<span data-ttu-id="e2bf7-108">Este artigo supõe que você:</span><span class="sxs-lookup"><span data-stu-id="e2bf7-108">This article assumes that you have:</span></span>

* <span data-ttu-id="e2bf7-109">Criou uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-109">Created an Azure storage account.</span></span> <span data-ttu-id="e2bf7-110">Se precisar de instruções, consulte [Sobre Contas de Armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e2bf7-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="e2bf7-111">Provisionar um cluster de Hadoop personalizado com hello serviço HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-111">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="e2bf7-112">Se precisar de instruções, consulte [Personalizar os clusters do Hadoop do Azure HDInsight para análise avançada](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e2bf7-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="e2bf7-113">Cluster de toohello de acesso remoto habilitado, conectado e abrir o console de linha de comando do Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-113">Enabled remote access toohello cluster, logged in, and opened hello Hadoop Command-Line console.</span></span> <span data-ttu-id="e2bf7-114">Se você precisar de instruções, consulte [Olá acesso cabeçotes de nó de Cluster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="e2bf7-114">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="e2bf7-115">Carregue o armazenamento de blob de tooAzure de dados</span><span class="sxs-lookup"><span data-stu-id="e2bf7-115">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="e2bf7-116">Se você tiver criado uma máquina virtual do Azure seguindo Olá instruções fornecidas na [configurar uma máquina virtual do Azure para análise avançada](machine-learning-data-science-setup-virtual-machine.md), esse arquivo de script deve ter sido baixado toohello *c:\\ Os usuários\\\<nome de usuário\>\\documentos\\Scripts de ciência de dados* diretório na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-116">If you created an Azure virtual machine by following hello instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded toohello *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on hello virtual machine.</span></span> <span data-ttu-id="e2bf7-117">Essas consultas de Hive exigem apenas que você conecte seu próprio esquema de dados e a configuração de armazenamento de BLOBs do Azure no hello campos apropriados toobe pronto para envio.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in hello appropriate fields toobe ready for submission.</span></span>

<span data-ttu-id="e2bf7-118">Vamos supor que dados Olá para tabelas de Hive estão em um **descompactados** formato tabular e que dados saudação foi carregado toohello padrão (ou tooan adicional) contêiner Olá da conta de armazenamento usada pelo cluster de Hadoop de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-118">We assume that hello data for Hive tables is in an **uncompressed** tabular format, and that hello data has been uploaded toohello default (or tooan additional) container of hello storage account used by hello Hadoop cluster.</span></span>

<span data-ttu-id="e2bf7-119">Se você quiser toopractice em Olá **NYC táxi Trip dados**, você precisa:</span><span class="sxs-lookup"><span data-stu-id="e2bf7-119">If you want toopractice on hello **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="e2bf7-120">**baixar** Olá 24 [NYC táxi Trip dados](http://www.andresmh.com/nyctaxitrips) arquivos (arquivos de viagem 12 e arquivos de passagens 12),</span><span class="sxs-lookup"><span data-stu-id="e2bf7-120">**download** hello 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="e2bf7-121">**descompactar** todos os arquivos em arquivos .csv, e</span><span class="sxs-lookup"><span data-stu-id="e2bf7-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="e2bf7-122">**carregar** -los toohello padrão (ou contêiner apropriado) do hello conta de armazenamento do Azure que foi criada pelo procedimento Olá descrito Olá [clusters de Hadoop de HDInsight do Azure personalizar para o processo de análise avançada e tecnologia ](machine-learning-data-science-customize-hadoop-cluster.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-122">**upload** them toohello default (or appropriate container) of hello Azure storage account that was created by hello procedure outlined in hello [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="e2bf7-123">Olá processo tooupload hello. csv arquivos toohello contêiner padrão na conta de armazenamento Olá pode ser encontrada neste [página](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="e2bf7-123">hello process tooupload hello .csv files toohello default container on hello storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="e2bf7-124"><a name="submit"></a>Como consultas de Hive toosubmit</span><span class="sxs-lookup"><span data-stu-id="e2bf7-124"><a name="submit"></a>How toosubmit Hive queries</span></span>
<span data-ttu-id="e2bf7-125">Consultas de Hive podem ser enviadas usando:</span><span class="sxs-lookup"><span data-stu-id="e2bf7-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="e2bf7-126">Enviar consultas de Hive por meio de Linha de comando do Hadoop no nó principal do cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="e2bf7-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="e2bf7-127">Enviar consultas Hive com hello Editor Hive</span><span class="sxs-lookup"><span data-stu-id="e2bf7-127">Submit Hive queries with hello Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="e2bf7-128">Enviar consultas de Hive com comandos do PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="e2bf7-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="e2bf7-129">Consultas de Hive são semelhantes ao SQL.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="e2bf7-130">Se você estiver familiarizado com o SQL, você pode encontrar hello [Hive para SQL usuários Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) útil.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-130">If you are familiar with SQL, you may find hello [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="e2bf7-131">Ao enviar uma consulta de Hive, você também pode controlar o destino Olá da saída de saudação de consultas de Hive, seja em Olá tela ou tooa arquivo local no nó principal hello ou tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-131">When submitting a Hive query, you can also control hello destination of hello output from Hive queries, whether it be on hello screen or tooa local file on hello head node or tooan Azure blob.</span></span>

### <span data-ttu-id="e2bf7-132"><a name="headnode"></a> 1. Enviar consultas de Hive por meio de Linha de comando do Hadoop no nó principal do cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="e2bf7-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="e2bf7-133">Se o Hive Olá consulta é complexa, enviando diretamente no nó principal de saudação do cluster de Hadoop de saudação normalmente leva toofaster de retorno que enviá-lo com um Editor Hive ou scripts do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-133">If hello Hive query is complex, submitting it directly in hello head node of hello Hadoop cluster typically leads toofaster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="e2bf7-134">Login toohello o nó principal do cluster de Hadoop hello, abra Olá linha de comando do Hadoop na área de trabalho de saudação do nó principal hello e digite o comando `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-134">Log in toohello head node of hello Hadoop cluster, open hello Hadoop Command Line on hello desktop of hello head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="e2bf7-135">Você tem três consultas de Hive toosubmit maneiras em Olá linha de comando do Hadoop:</span><span class="sxs-lookup"><span data-stu-id="e2bf7-135">You have three ways toosubmit Hive queries in hello Hadoop Command Line:</span></span>

* <span data-ttu-id="e2bf7-136">diretamente</span><span class="sxs-lookup"><span data-stu-id="e2bf7-136">directly</span></span>
* <span data-ttu-id="e2bf7-137">usando arquivos .hql</span><span class="sxs-lookup"><span data-stu-id="e2bf7-137">using .hql files</span></span>
* <span data-ttu-id="e2bf7-138">com hello Hive console de comando</span><span class="sxs-lookup"><span data-stu-id="e2bf7-138">with hello Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="e2bf7-139">Enviar consultas de Hive diretamente na Linha de Comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="e2bf7-140">Você pode executar o comando como `hive -e "<your hive query>;` toosubmit consultas de Hive simples diretamente no Hadoop linha de comando.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-140">You can run command like `hive -e "<your hive query>;` toosubmit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="e2bf7-141">Aqui está um exemplo onde estruturas de caixa Olá vermelho Olá comando que envia a consulta de Hive hello e Olá caixa verde contornos Olá saída da consulta de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-141">Here is an example, where hello red box outlines hello command that submits hello Hive query, and hello green box outlines hello output from hello Hive query.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="e2bf7-143">Enviar consultas de Hive em arquivos de .hql</span><span class="sxs-lookup"><span data-stu-id="e2bf7-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="e2bf7-144">Quando a consulta de Hive Olá é mais complicada e tem várias linhas, a edição de consultas no console de comando de Hive ou de linha de comando não é prático.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-144">When hello Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="e2bf7-145">Uma alternativa é toouse um editor de texto no nó principal de saudação do hello Hadoop cluster toosave Olá consultas de Hive em um arquivo .hql em um diretório local do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-145">An alternative is toouse a text editor in hello head node of hello Hadoop cluster toosave hello Hive queries in a .hql file in a local directory of hello head node.</span></span> <span data-ttu-id="e2bf7-146">E consulta de Hive Olá no arquivo de .hql Olá pode ser submetida usando Olá `-f` argumento da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e2bf7-146">Then hello Hive query in hello .hql file can be submitted by using hello `-f` argument as follows:</span></span>

    hive -f "<path toohello .hql file>"

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="e2bf7-148">**Suprimir a impressão da tela de status de progresso de consultas de Hive**</span><span class="sxs-lookup"><span data-stu-id="e2bf7-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="e2bf7-149">Por padrão, após a consulta de Hive é enviada na linha de comando do Hadoop, progresso de saudação do trabalho de mapear/reduzir Olá é impresso na tela.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-149">By default, after Hive query is submitted in Hadoop Command Line, hello progress of hello Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="e2bf7-150">toosuppress Olá impressão de tela de andamento do trabalho de mapear/reduzir hello, você pode usar um argumento `-S` ("S" em letras maiusculas) em Olá linha de comando da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e2bf7-150">toosuppress hello screen print of hello Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in hello command line as follows:</span></span>

    hive -S -f "<path toohello .hql file>"
<span data-ttu-id="e2bf7-151">.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-151">.</span></span>    <span data-ttu-id="e2bf7-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="e2bf7-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="e2bf7-153">Enviar consultas de Hive no console de comando de Hive.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="e2bf7-154">Você pode inserir primeiro console de comando de Hive Olá executando o comando `hive` na linha de comando do Hadoop e, em seguida, enviar consultas de Hive no console de comando do Hive.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-154">You can also first enter hello Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="e2bf7-155">Aqui está um exemplo.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-155">Here is an example.</span></span> <span data-ttu-id="e2bf7-156">Neste exemplo, Olá duas caixas vermelhas realce Olá comandos usados tooenter Olá console de comando de Hive e Olá consulta de Hive enviada no console de comando de Hive, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-156">In this example, hello two red boxes highlight hello commands used tooenter hello Hive command console, and hello Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="e2bf7-157">caixa Olá verde realça saída Olá da consulta de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-157">hello green box highlights hello output from hello Hive query.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="e2bf7-159">exemplos anteriores Olá diretamente resultados de consulta de Hive Olá na tela de saída.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-159">hello previous examples directly output hello Hive query results on screen.</span></span> <span data-ttu-id="e2bf7-160">Você também pode escrever um arquivo local de saudação saída tooa no nó principal do hello, ou tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-160">You can also write hello output tooa local file on hello head node, or tooan Azure blob.</span></span> <span data-ttu-id="e2bf7-161">Em seguida, você pode usar outras ferramentas toofurther analisar a saída de saudação de consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-161">Then, you can use other tools toofurther analyze hello output of Hive queries.</span></span>

<span data-ttu-id="e2bf7-162">**Saída Hive consulta resultados tooa arquivo local.**</span><span class="sxs-lookup"><span data-stu-id="e2bf7-162">**Output Hive query results tooa local file.**</span></span>
<span data-ttu-id="e2bf7-163">toooutput Hive consulta resultados tooa diretório local no nó principal do hello, tiver consulta de Hive Olá toosubmit em Olá Hadoop linha de comando da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e2bf7-163">toooutput Hive query results tooa local directory on hello head node, you have toosubmit hello Hive query in hello Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in hello head node>

<span data-ttu-id="e2bf7-164">Em Olá exemplo a seguir, saída de saudação da consulta de Hive é gravada em um arquivo `hivequeryoutput.txt` no diretório `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-164">In hello following example, hello output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="e2bf7-166">**Saída tooan de resultados de consulta de Hive BLOBs do Azure**</span><span class="sxs-lookup"><span data-stu-id="e2bf7-166">**Output Hive query results tooan Azure blob**</span></span>

<span data-ttu-id="e2bf7-167">Você também pode gerar Olá Hive consulta resultados tooan BLOBs do Azure, no contêiner do cluster de Hadoop de saudação padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-167">You can also output hello Hive query results tooan Azure blob, within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="e2bf7-168">consulta de Hive Olá para isso é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e2bf7-168">hello Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

<span data-ttu-id="e2bf7-169">Em Olá exemplo a seguir, saída de saudação da consulta de Hive é gravada diretório de blob tooa `queryoutputdir` no contêiner do cluster de Hadoop de saudação padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-169">In hello following example, hello output of Hive query is written tooa blob directory `queryoutputdir` within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="e2bf7-170">Aqui, você só precisa de nome do diretório tooprovide hello, sem nome de blob hello.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-170">Here, you only need tooprovide hello directory name, without hello blob name.</span></span> <span data-ttu-id="e2bf7-171">Um erro será gerado se você fornecer os nomes do blob e do diretório, como `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="e2bf7-173">Se você abrir o contêiner padrão de saudação do cluster de Hadoop hello usando o Azure Storage Explorer, você pode ver a saída Olá da consulta de Hive Olá conforme mostrado na figura a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-173">If you open hello default container of hello Hadoop cluster using Azure Storage Explorer, you can see hello output of hello Hive query as shown in hello following figure.</span></span> <span data-ttu-id="e2bf7-174">Você pode aplicar Olá filtro (realçado por caixa vermelha) tooonly recuperar Olá blob com as letras nos nomes especificadas.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-174">You can apply hello filter (highlighted by red box) tooonly retrieve hello blob with specified letters in names.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="e2bf7-176"><a name="hive-editor"></a> 2. Enviar consultas Hive com hello Editor Hive</span><span class="sxs-lookup"><span data-stu-id="e2bf7-176"><a name="hive-editor"></a> 2. Submit Hive queries with hello Hive Editor</span></span>
<span data-ttu-id="e2bf7-177">Você também pode usar o hello Console de consulta (Editor Hive) digitando uma URL do formulário de saudação *https://&#60; Nome do cluster Hadoop >.azurehdinsight.net/Home/HiveEditor* em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-177">You can also use hello Query Console (Hive Editor) by entering a URL of hello form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="e2bf7-178">Você deve ser registrado no hello, consulte este console e portanto você precisa de suas credenciais de cluster Hadoop aqui.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-178">You must be logged in hello see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="e2bf7-179"><a name="ps"></a> 3. Enviar consultas de Hive com comandos do PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="e2bf7-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="e2bf7-180">Você também pode usar consultas de Hive toosubmit PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-180">You can also use PowerShell toosubmit Hive queries.</span></span> <span data-ttu-id="e2bf7-181">Para obter instruções, confira [Enviar trabalhos do Hive usando o PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e2bf7-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="e2bf7-182"><a name="create-tables"></a>Criar banco de dados e tabelas Hive</span><span class="sxs-lookup"><span data-stu-id="e2bf7-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="e2bf7-183">Olá consultas de Hive são compartilhadas em Olá [repositório GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) e pode ser baixado a partir daí.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-183">hello Hive queries are shared in hello [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="e2bf7-184">Aqui está uma consulta de Hive Olá que cria uma tabela de Hive.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-184">Here is hello Hive query that creates a Hive table.</span></span>

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

<span data-ttu-id="e2bf7-185">Aqui estão descrições de saudação dos campos de saudação que você precisa tooplug no e outras configurações:</span><span class="sxs-lookup"><span data-stu-id="e2bf7-185">Here are hello descriptions of hello fields that you need tooplug in and other configurations:</span></span>

* <span data-ttu-id="e2bf7-186">**&#60; o nome do banco de dados >**: nome de saudação do banco de dados de saudação que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-186">**&#60;database name>**: hello name of hello database that you want toocreate.</span></span> <span data-ttu-id="e2bf7-187">Se você quiser apenas o banco de dados padrão do toouse hello, Olá consulta *criar banco de dados...*  pode ser omitido.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-187">If you just want toouse hello default database, hello query *create database...* can be omitted.</span></span>
* <span data-ttu-id="e2bf7-188">**&#60; o nome da tabela >**: nome de saudação da tabela de saudação que você deseja toocreate no banco de dados especificado hello.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-188">**&#60;table name>**: hello name of hello table that you want toocreate within hello specified database.</span></span> <span data-ttu-id="e2bf7-189">Se você quiser que o banco de dados do toouse saudação padrão, tabela Olá pode ser chamada diretamente por *&#60; o nome da tabela >* sem &#60; o nome do banco de dados >.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-189">If you want toouse hello default database, hello table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="e2bf7-190">**&#60; separador >**: separador Olá que delimita campos Olá toobe de arquivo de dados carregado toohello tabela de Hive.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-190">**&#60;field separator>**: hello separator that delimits fields in hello data file toobe uploaded toohello Hive table.</span></span>
* <span data-ttu-id="e2bf7-191">**&#60; separador de linha >**: separador Olá que delimita linhas no arquivo de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-191">**&#60;line separator>**: hello separator that delimits lines in hello data file.</span></span>
* <span data-ttu-id="e2bf7-192">**&#60; local de armazenamento >**: Olá dados do armazenamento do Azure local toosave saudação de tabelas de Hive.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-192">**&#60;storage location>**: hello Azure storage location toosave hello data of Hive tables.</span></span> <span data-ttu-id="e2bf7-193">Se você não especificar *local &#60; local de armazenamento >*, Olá banco de dados e hello tabelas são armazenadas em *hive/warehouse/* diretório no contêiner de padrão de saudação do cluster de Hive Olá por padrão.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-193">If you do not specify *LOCATION &#60;storage location>*, hello database and hello tables are stored in *hive/warehouse/* directory in hello default container of hello Hive cluster by default.</span></span> <span data-ttu-id="e2bf7-194">Se você quiser toospecify Olá armazenamento local, o local de armazenamento Olá tem toobe no contêiner do saudação padrão para o banco de dados de saudação e tabelas.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-194">If you want toospecify hello storage location, hello storage location has toobe within hello default container for hello database and tables.</span></span> <span data-ttu-id="e2bf7-195">Essa localização tem toobe conhecido como contêiner do local relativo toohello padrão de cluster Olá no formato de saudação do *' wasb: / / / &#60; diretório 1 > /'* ou *' wasb: / / / &#60; diretório 1 > / &#60; diretório 2 > /'*, etc. Após Olá consulta é executada, diretórios relativo Olá são criados no contêiner de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-195">This location has toobe referred as location relative toohello default container of hello cluster in hello format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After hello query is executed, hello relative directories are created within hello default container.</span></span>
* <span data-ttu-id="e2bf7-196">**TBLPROPERTIES("Skip.Header.line.Count"="1")**: se o arquivo de dados de saudação tem uma linha de cabeçalho, têm tooadd essa propriedade **final Olá** de saudação *criar tabela* consulta.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If hello data file has a header line, you have tooadd this property **at hello end** of hello *create table* query.</span></span> <span data-ttu-id="e2bf7-197">Caso contrário, a linha de cabeçalho de saudação é carregada como uma tabela de registro toohello.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-197">Otherwise, hello header line is loaded as a record toohello table.</span></span> <span data-ttu-id="e2bf7-198">Se o arquivo de dados de saudação não tem uma linha de cabeçalho, essa configuração pode ser omitida na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-198">If hello data file does not have a header line, this configuration can be omitted in hello query.</span></span>

## <span data-ttu-id="e2bf7-199"><a name="load-data"></a>Carregar dados tooHive tabelas</span><span class="sxs-lookup"><span data-stu-id="e2bf7-199"><a name="load-data"></a>Load data tooHive tables</span></span>
<span data-ttu-id="e2bf7-200">Aqui está uma consulta de Hive Olá que carrega dados em uma tabela de Hive.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-200">Here is hello Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="e2bf7-201">**&#60; dados de caminho de tooblob >**: Olá se Olá blob arquivo toobe carregado toohello Hive tabela estiver no contêiner de padrão de saudação do hello cluster HDInsight Hadoop, *&#60; dados de caminho de tooblob >* deve estar no formato de saudação *' wasb: / / / &#60; diretório neste contêiner > / &#60; o nome de arquivo do blob >'*.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-201">**&#60;path tooblob data>**: If hello blob file toobe uploaded toohello Hive table is in hello default container of hello HDInsight Hadoop cluster, hello *&#60;path tooblob data>* should be in hello format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="e2bf7-202">arquivo de blob Olá também pode estar em um recipiente adicional de saudação cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-202">hello blob file can also be in an additional container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="e2bf7-203">Nesse caso, *&#60; dados de caminho de tooblob >* deve estar no formato de saudação *' wasb: / / &#60; nome do contêiner > @&#60; o nome da conta de armazenamento >.blob.core.windows.net/ &#60; o nome de arquivo do blob >'*.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-203">In this case, *&#60;path tooblob data>* should be in hello format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e2bf7-204">Olá blob dados toobe carregado tooHive tabela tem toobe no padrão de saudação ou no contêiner adicional Olá da conta de armazenamento de cluster de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-204">hello blob data toobe uploaded tooHive table has toobe in hello default or additional container of hello storage account for hello Hadoop cluster.</span></span> <span data-ttu-id="e2bf7-205">Caso contrário, Olá *carregar dados* indicando que ele não pode acessar dados saudação ocorre falha na consulta.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-205">Otherwise, hello *LOAD DATA* query fails complaining that it cannot access hello data.</span></span>
  >
  >

## <span data-ttu-id="e2bf7-206"><a name="partition-orc"></a>Tópicos avançados: tabela e repositório de dados Hive particionados no formato ORC</span><span class="sxs-lookup"><span data-stu-id="e2bf7-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="e2bf7-207">Se dados saudação forem grandes, o particionamento de tabela Olá é útil para consultas que precisam apenas tooscan algumas partições da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-207">If hello data is large, partitioning hello table is beneficial for queries that only need tooscan a few partitions of hello table.</span></span> <span data-ttu-id="e2bf7-208">Por exemplo, é razoável toopartition dados de log de saudação de um site da web por datas.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-208">For instance, it is reasonable toopartition hello log data of a web site by dates.</span></span>

<span data-ttu-id="e2bf7-209">Em adição toopartitioning Hive tabelas, também é benéfico toostore os dados de Hive Olá no formato de linha de otimização Colunar (ORC) hello.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-209">In addition toopartitioning Hive tables, it is also beneficial toostore hello Hive data in hello Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="e2bf7-210">Para obter mais informações sobre a formatação ORC, consulte <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Usando arquivos ORC melhora o desempenho quando o Hive lê, grava e processa dados</a>.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="e2bf7-211">Tabela particionada</span><span class="sxs-lookup"><span data-stu-id="e2bf7-211">Partitioned table</span></span>
<span data-ttu-id="e2bf7-212">Aqui está uma consulta de Hive Olá que cria uma tabela particionada e carrega dados nele.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-212">Here is hello Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="e2bf7-213">Ao consultar tabelas particionadas, é recomendável tooadd condição de partição Olá no hello **início** de saudação `where` cláusula como isso melhora a eficácia de saudação da pesquisa significativamente.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-213">When querying partitioned tables, it is recommended tooadd hello partition condition in hello **beginning** of hello `where` clause as this improves hello efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="e2bf7-214"><a name="orc"></a>Armazenar dados Hive no formato ORC</span><span class="sxs-lookup"><span data-stu-id="e2bf7-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="e2bf7-215">Diretamente, você não pode carregar dados do armazenamento de blob em tabelas de Hive que são armazenados em formato ORC hello.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-215">You cannot directly load data from blob storage into Hive tables that is stored in hello ORC format.</span></span> <span data-ttu-id="e2bf7-216">Aqui estão as etapas de saudação tooHive tabelas armazenadas no formato ORC os blobs que Olá precisar de tootake tooload dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-216">Here are hello steps that hello you need tootake tooload data from Azure blobs tooHive tables stored in ORC format.</span></span>

<span data-ttu-id="e2bf7-217">Crie uma tabela externa **arquivo de texto ARMAZENADO como** e carregar dados da tabela de toohello de armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage toohello table.</span></span>

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="e2bf7-218">Criar uma tabela interna com hello mesmo esquema da tabela externa de saudação na etapa 1, com hello mesmo delimitador de campo e armazenar Olá Hive dados no formato ORC hello.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-218">Create an internal table with hello same schema as hello external table in step 1, with hello same field delimiter, and store hello Hive data in hello ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="e2bf7-219">Selecionar dados de tabela externa de saudação na etapa 1 e inserir a tabela ORC Olá</span><span class="sxs-lookup"><span data-stu-id="e2bf7-219">Select data from hello external table in step 1 and insert into hello ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="e2bf7-220">Se tabela de arquivo de texto de saudação *&#60; o nome do banco de dados >. &#60; o nome da tabela externa do arquivo de texto >* tem partições, na etapa 3, hello `SELECT * FROM <database name>.<external textfile table name>` comando selecionará Olá variável de partição como um campo em Olá retornou um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-220">If hello TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, hello `SELECT * FROM <database name>.<external textfile table name>` command selects hello partition variable as a field in hello returned data set.</span></span> <span data-ttu-id="e2bf7-221">Inseri-lo no hello *&#60; o nome do banco de dados >. &#60; o nome da tabela ORC >* falhar desde *&#60; o nome do banco de dados >. &#60; o nome da tabela ORC >* não tem uma variável de partição hello como um campo no esquema da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-221">Inserting it into hello *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have hello partition variable as a field in hello table schema.</span></span> <span data-ttu-id="e2bf7-222">Nesse caso, você precisa toospecifically Olá selecione campos toobe inserido muito*&#60; o nome do banco de dados >. &#60; o nome da tabela ORC >* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e2bf7-222">In this case, you need toospecifically select hello fields toobe inserted too*&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="e2bf7-223">É seguro toodrop Olá *&#60; o nome da tabela externa do arquivo de texto >* quando usar Olá após todos os dados a seguir consulta tenha sido inserido no *&#60; o nome do banco de dados >. &#60; o nome da tabela ORC >*:</span><span class="sxs-lookup"><span data-stu-id="e2bf7-223">It is safe toodrop hello *&#60;external textfile table name>* when using hello following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="e2bf7-224">Depois de seguir este procedimento, você deve ter uma tabela com dados em toouse pronto do hello ORC formato.</span><span class="sxs-lookup"><span data-stu-id="e2bf7-224">After following this procedure, you should have a table with data in hello ORC format ready toouse.</span></span>  
