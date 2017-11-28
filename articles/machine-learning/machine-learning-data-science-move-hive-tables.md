---
title: Criar tabelas do Hive e carregar dados do Armazenamento de Blobs do Azure | Microsoft Docs
description: Criar tabelas Hive e carregar dados em blobs para tabelas hive
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
ms.openlocfilehash: eca4ecd8f639bb9816903f4b1d1f999755da819c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="0fd9e-103">Criar tabelas do Hive e carregar dados do Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="0fd9e-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="0fd9e-104">Neste tópico, são apresentadas consultas genéricas do Hive que criam tabelas do Hive e carregam dados do armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="0fd9e-105">Também são fornecida algumas orientações sobre o particionamento de tabelas Hive e sobre como usar a formatação ORC (Colunar de Linha Otimizado) para melhorar o desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-105">Some guidance is also provided on partitioning Hive tables and on using the Optimized Row Columnar (ORC) formatting to improve query performance.</span></span>

<span data-ttu-id="0fd9e-106">Este **menu** vincula-se a tópicos que descrevem a inclusão de dados em ambientes de destino em que os dados podem ser armazenados e processados durante o TDSP (Processo de Ciência de Dados de Equipe).</span><span class="sxs-lookup"><span data-stu-id="0fd9e-106">This **menu** links to topics that describe how to ingest data into target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="0fd9e-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0fd9e-107">Prerequisites</span></span>
<span data-ttu-id="0fd9e-108">Este artigo supõe que você:</span><span class="sxs-lookup"><span data-stu-id="0fd9e-108">This article assumes that you have:</span></span>

* <span data-ttu-id="0fd9e-109">Criou uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-109">Created an Azure storage account.</span></span> <span data-ttu-id="0fd9e-110">Se precisar de instruções, consulte [Sobre Contas de Armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="0fd9e-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="0fd9e-111">Provisionou um cluster do Hadoop personalizado com o serviço HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-111">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="0fd9e-112">Se precisar de instruções, consulte [Personalizar os clusters do Hadoop do Azure HDInsight para análise avançada](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="0fd9e-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="0fd9e-113">Habilitou o acesso remoto para o cluster, conectou-se e abriu o Console de Linha de Comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-113">Enabled remote access to the cluster, logged in, and opened the Hadoop Command-Line console.</span></span> <span data-ttu-id="0fd9e-114">Se precisar de instruções, consulte [Acessar o nó principal do Cluster do Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="0fd9e-114">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="0fd9e-115">Carregar dados no armazenamento de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="0fd9e-115">Upload data to Azure blob storage</span></span>
<span data-ttu-id="0fd9e-116">Se você criou uma máquina virtual do Azure seguindo as instruções fornecidas em [Configurar uma máquina virtual do Azure para análise avançada](machine-learning-data-science-setup-virtual-machine.md), esse arquivo de script deve ter sido baixado no diretório *C:\\User\\\<suser name\>\\Documents\\Data Science Scripts* na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-116">If you created an Azure virtual machine by following the instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded to the *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on the virtual machine.</span></span> <span data-ttu-id="0fd9e-117">Essas consultas de Hive exigem somente conectar em seu próprio esquema de dados e que a configuração de armazenamento de blobs do Azure nos campos apropriados esteja pronta para envio.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in the appropriate fields to be ready for submission.</span></span>

<span data-ttu-id="0fd9e-118">Supomos que os dados de tabelas Hive estejam em formato de tabela **descompactado** e que os dados foram carregado no contêiner padrão (ou em um adicional) da conta de armazenamento usada pelo cluster do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-118">We assume that the data for Hive tables is in an **uncompressed** tabular format, and that the data has been uploaded to the default (or to an additional) container of the storage account used by the Hadoop cluster.</span></span>

<span data-ttu-id="0fd9e-119">Se quiser praticar com os **Dados de viagens de táxi de NYC**, você precisará:</span><span class="sxs-lookup"><span data-stu-id="0fd9e-119">If you want to practice on the **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="0fd9e-120">**baixar** os 24 arquivos de [Dados de viagens de táxi de NYC](http://www.andresmh.com/nyctaxitrips) (12 arquivos de viagens e 12 arquivos de tarifas),</span><span class="sxs-lookup"><span data-stu-id="0fd9e-120">**download** the 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="0fd9e-121">**descompactar** todos os arquivos em arquivos .csv, e</span><span class="sxs-lookup"><span data-stu-id="0fd9e-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="0fd9e-122">**carregar** os arquivos no contêiner padrão (ou contêiner apropriado) da conta de armazenamento do Azure que foi criada pelo procedimento descrito no tópico [Personalizar os clusters do Hadoop do Azure HDInsight para Processo e Tecnologia de Análise Avançada](machine-learning-data-science-customize-hadoop-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="0fd9e-122">**upload** them to the default (or appropriate container) of the Azure storage account that was created by the procedure outlined in the [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="0fd9e-123">O processo para carregar os arquivos .csv para o contêiner padrão na conta de armazenamento pode ser encontrado nesta [página](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="0fd9e-123">The process to upload the .csv files to the default container on the storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="0fd9e-124"><a name="submit"></a>Como enviar consultas de Hive</span><span class="sxs-lookup"><span data-stu-id="0fd9e-124"><a name="submit"></a>How to submit Hive queries</span></span>
<span data-ttu-id="0fd9e-125">Consultas de Hive podem ser enviadas usando:</span><span class="sxs-lookup"><span data-stu-id="0fd9e-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="0fd9e-126">Enviar consultas de Hive por meio de Linha de comando do Hadoop no nó principal do cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="0fd9e-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="0fd9e-127">Enviar consultas de Hive com o Editor de Hive</span><span class="sxs-lookup"><span data-stu-id="0fd9e-127">Submit Hive queries with the Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="0fd9e-128">Enviar consultas de Hive com comandos do PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="0fd9e-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="0fd9e-129">Consultas de Hive são semelhantes ao SQL.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="0fd9e-130">Se já estiver familiarizado com o SQL, talvez você considere o [Roteiro para usuários do Hive para SQL](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) útil.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-130">If you are familiar with SQL, you may find the [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="0fd9e-131">Ao enviar uma consulta de Hive, você também pode controlar o destino da saída de consultas de Hive, seja na tela, para um arquivo local no nó principal ou para um blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-131">When submitting a Hive query, you can also control the destination of the output from Hive queries, whether it be on the screen or to a local file on the head node or to an Azure blob.</span></span>

### <span data-ttu-id="0fd9e-132"><a name="headnode"></a> 1. Enviar consultas de Hive por meio de Linha de comando do Hadoop no nó principal do cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="0fd9e-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="0fd9e-133">Se a consulta é complexa, o envio de consultas de Hive diretamente ao nó principal do cluster Hadoop normalmente leva a um resultado mais rápido do que enviá-la com scripts do Editor de Hive ou do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-133">If the Hive query is complex, submitting it directly in the head node of the Hadoop cluster typically leads to faster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="0fd9e-134">Faça logon no nó principal do cluster do Hadoop, abra a Linha de Comando do Hadoop na área de trabalho do nó principal e digite o comando `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-134">Log in to the head node of the Hadoop cluster, open the Hadoop Command Line on the desktop of the head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="0fd9e-135">Você tem três maneiras de enviar consultas de Hive na Linha de Comando do Hadoop:</span><span class="sxs-lookup"><span data-stu-id="0fd9e-135">You have three ways to submit Hive queries in the Hadoop Command Line:</span></span>

* <span data-ttu-id="0fd9e-136">diretamente</span><span class="sxs-lookup"><span data-stu-id="0fd9e-136">directly</span></span>
* <span data-ttu-id="0fd9e-137">usando arquivos .hql</span><span class="sxs-lookup"><span data-stu-id="0fd9e-137">using .hql files</span></span>
* <span data-ttu-id="0fd9e-138">com o console de comando do Hive</span><span class="sxs-lookup"><span data-stu-id="0fd9e-138">with the Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="0fd9e-139">Enviar consultas de Hive diretamente na Linha de Comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="0fd9e-140">Você pode executar o comando como `hive -e "<your hive query>;` para enviar consultas de Hive simples diretamente na Linha de Comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-140">You can run command like `hive -e "<your hive query>;` to submit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="0fd9e-141">Veja um exemplo, no qual a caixa vermelha descreve o comando que envia a consulta Hive e a caixa verde descreve a saída da consulta Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-141">Here is an example, where the red box outlines the command that submits the Hive query, and the green box outlines the output from the Hive query.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="0fd9e-143">Enviar consultas de Hive em arquivos de .hql</span><span class="sxs-lookup"><span data-stu-id="0fd9e-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="0fd9e-144">Quando a consulta Hive é mais complicada e tem várias linhas, não é prático editar consultas na linha de comando ou no console de comando de Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-144">When the Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="0fd9e-145">Uma alternativa é usar um editor de texto no nó principal do cluster do Hadoop para salvar as consultas de Hive em um arquivo .hql em um diretório local do nó principal.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-145">An alternative is to use a text editor in the head node of the Hadoop cluster to save the Hive queries in a .hql file in a local directory of the head node.</span></span> <span data-ttu-id="0fd9e-146">Em seguida, a consulta de Hive no arquivo HQL pode ser enviada usando o argumento `-f` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0fd9e-146">Then the Hive query in the .hql file can be submitted by using the `-f` argument as follows:</span></span>

    hive -f "<path to the .hql file>"

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="0fd9e-148">**Suprimir a impressão da tela de status de progresso de consultas de Hive**</span><span class="sxs-lookup"><span data-stu-id="0fd9e-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="0fd9e-149">Por padrão, após a consulta Hive ser enviada na Linha de Comando do Hadoop, o andamento do trabalho de Mapear/Reduzir será impresso na tela.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-149">By default, after Hive query is submitted in Hadoop Command Line, the progress of the Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="0fd9e-150">Para suprimir a impressão da tela de andamento do trabalho de Mapear/Reduzir, você pode usar um argumento `-S` ("S" em letra maiúscula) na linha de comando da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0fd9e-150">To suppress the screen print of the Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in the command line as follows:</span></span>

    hive -S -f "<path to the .hql file>"
<span data-ttu-id="0fd9e-151">.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-151">.</span></span>    <span data-ttu-id="0fd9e-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="0fd9e-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="0fd9e-153">Enviar consultas de Hive no console de comando de Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="0fd9e-154">Você também pode entrar primeiro no console de comando de Hive executando o comando `hive` na Linha de Comando do Hadoop e enviar consultas de Hive no console de comando de Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-154">You can also first enter the Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="0fd9e-155">Aqui está um exemplo.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-155">Here is an example.</span></span> <span data-ttu-id="0fd9e-156">Neste exemplo, as duas caixas vermelhas realçam os comandos usados para inserir o console de comando de Hive e a consulta de Hive enviada no console de comando de Hive, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-156">In this example, the two red boxes highlight the commands used to enter the Hive command console, and the Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="0fd9e-157">A caixa verde realça a saída da consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-157">The green box highlights the output from the Hive query.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="0fd9e-159">Os exemplos anteriores mostram os resultados da consulta de Hive diretamente na tela.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-159">The previous examples directly output the Hive query results on screen.</span></span> <span data-ttu-id="0fd9e-160">Você também pode gravar a saída em um arquivo local no nó principal ou em um blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-160">You can also write the output to a local file on the head node, or to an Azure blob.</span></span> <span data-ttu-id="0fd9e-161">Em seguida, você pode usar outras ferramentas para analisar com mais detalhes a saída das consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-161">Then, you can use other tools to further analyze the output of Hive queries.</span></span>

<span data-ttu-id="0fd9e-162">**Resultados da consulta de Hive em um arquivo local de saída.**</span><span class="sxs-lookup"><span data-stu-id="0fd9e-162">**Output Hive query results to a local file.**</span></span>
<span data-ttu-id="0fd9e-163">Para exibir os resultados da consulta de Hive em um diretório local no nó principal, você precisa enviar a consulta de Hive na Linha de Comando do Hadoop da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0fd9e-163">To output Hive query results to a local directory on the head node, you have to submit the Hive query in the Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in the head node>

<span data-ttu-id="0fd9e-164">No exemplo a seguir, a saída da consulta de Hive é gravada em um arquivo `hivequeryoutput.txt` no diretório `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-164">In the following example, the output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="0fd9e-166">**Exportar a saída de consulta de Hive para um blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="0fd9e-166">**Output Hive query results to an Azure blob**</span></span>

<span data-ttu-id="0fd9e-167">Você também pode exportar a saída da consulta de Hive para um blob do Azure dentro do contêiner padrão do cluster do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-167">You can also output the Hive query results to an Azure blob, within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="0fd9e-168">Veja a seguir a consulta de Hive para esse procedimento:</span><span class="sxs-lookup"><span data-stu-id="0fd9e-168">The Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within the default container> <select clause from ...>

<span data-ttu-id="0fd9e-169">No exemplo a seguir, a saída da consulta de Hive é gravada em um diretório de blob `queryoutputdir` no contêiner padrão do cluster do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-169">In the following example, the output of Hive query is written to a blob directory `queryoutputdir` within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="0fd9e-170">Aqui, você precisa fornecer apenas o nome do diretório, sem o nome do blob.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-170">Here, you only need to provide the directory name, without the blob name.</span></span> <span data-ttu-id="0fd9e-171">Um erro será gerado se você fornecer os nomes do blob e do diretório, como `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="0fd9e-173">Se abrir o contêiner padrão do cluster do Hadoop usando o Gerenciador de Armazenamento do Azure, você verá a saída da consulta de Hive da forma indicada na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-173">If you open the default container of the Hadoop cluster using Azure Storage Explorer, you can see the output of the Hive query as shown in the following figure.</span></span> <span data-ttu-id="0fd9e-174">Você pode aplicar o filtro (destacado pela caixa vermelha) para recuperar apenas o blob com letras específicas nos nomes.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-174">You can apply the filter (highlighted by red box) to only retrieve the blob with specified letters in names.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="0fd9e-176"><a name="hive-editor"></a> 2. Enviar consultas de Hive com o Editor de Hive</span><span class="sxs-lookup"><span data-stu-id="0fd9e-176"><a name="hive-editor"></a> 2. Submit Hive queries with the Hive Editor</span></span>
<span data-ttu-id="0fd9e-177">Você também pode usar o console de consulta (Editor de Hive) digitando uma URL do formulário nome do cluster *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-177">You can also use the Query Console (Hive Editor) by entering a URL of the form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="0fd9e-178">Você precisa estar conectado ao console, de forma que precisa de suas credenciais do cluster do Hadoop aqui.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-178">You must be logged in the see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="0fd9e-179"><a name="ps"></a> 3. Enviar consultas de Hive com comandos do PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="0fd9e-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="0fd9e-180">Você também pode usar o PowerShell para enviar consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-180">You can also use PowerShell to submit Hive queries.</span></span> <span data-ttu-id="0fd9e-181">Para obter instruções, confira [Enviar trabalhos do Hive usando o PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0fd9e-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="0fd9e-182"><a name="create-tables"></a>Criar banco de dados e tabelas Hive</span><span class="sxs-lookup"><span data-stu-id="0fd9e-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="0fd9e-183">As consultas de Hive são compartilhadas no [repositório GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) e podem ser baixadas de lá.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-183">The Hive queries are shared in the [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="0fd9e-184">Veja aqui a consulta Hive que cria uma tabela Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-184">Here is the Hive query that creates a Hive table.</span></span>

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

<span data-ttu-id="0fd9e-185">Veja aqui as descrições dos campos de que você precisa para plug-ins e outras configurações:</span><span class="sxs-lookup"><span data-stu-id="0fd9e-185">Here are the descriptions of the fields that you need to plug in and other configurations:</span></span>

* <span data-ttu-id="0fd9e-186">**&#60;nome do banco de dados>**: o nome do banco de dados que você deseja criar.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-186">**&#60;database name>**: the name of the database that you want to create.</span></span> <span data-ttu-id="0fd9e-187">Se quiser apenas usar o banco de dados padrão, a consulta *create database...* poderá ser omitida.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-187">If you just want to use the default database, the query *create database...* can be omitted.</span></span>
* <span data-ttu-id="0fd9e-188">**&#60;nome da tabela>**: o nome da tabela que você deseja criar no banco de dados especificado.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-188">**&#60;table name>**: the name of the table that you want to create within the specified database.</span></span> <span data-ttu-id="0fd9e-189">Se quiser usar o banco de dados padrão, a tabela poderá ser referida diretamente por *&#60;nome da tabela>* sem &#60;nome do banco de dados>.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-189">If you want to use the default database, the table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="0fd9e-190">**&#60;separador de campo>**: o separador que delimita os campos no arquivo de dados a serem carregados na tabela Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-190">**&#60;field separator>**: the separator that delimits fields in the data file to be uploaded to the Hive table.</span></span>
* <span data-ttu-id="0fd9e-191">**&#60;separador de linha>**: o separador que delimita as linhas no arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-191">**&#60;line separator>**: the separator that delimits lines in the data file.</span></span>
* <span data-ttu-id="0fd9e-192">**&#60;local de armazenamento>**: o local de armazenamento do Azure para salvar os dados das tabelas Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-192">**&#60;storage location>**: the Azure storage location to save the data of Hive tables.</span></span> <span data-ttu-id="0fd9e-193">Se você não especificar *LOCATION &#60;local de armazenamento>*, o banco de dados e as tabelas serão armazenados no diretório *hive/warehouse/* no contêiner padrão do cluster de Hive por padrão.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-193">If you do not specify *LOCATION &#60;storage location>*, the database and the tables are stored in *hive/warehouse/* directory in the default container of the Hive cluster by default.</span></span> <span data-ttu-id="0fd9e-194">Se você quiser especificar a localização de armazenamento, esta deverá estar dentro do contêiner padrão para o banco de dados e tabelas.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-194">If you want to specify the storage location, the storage location has to be within the default container for the database and tables.</span></span> <span data-ttu-id="0fd9e-195">Esse local precisa ser chamado como um local relativo ao contêiner padrão do cluster no formato *'wasb:///&#60;diretório 1>/'* ou *'wasb:///&#60;diretório 1>/&#60;diretório 2>/'*, etc. Após a consulta ser executada, os diretórios relativos serão criados no contêiner padrão.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-195">This location has to be referred as location relative to the default container of the cluster in the format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After the query is executed, the relative directories are created within the default container.</span></span>
* <span data-ttu-id="0fd9e-196">**TBLPROPERTIES("skip.header.line.count"="1")**: Se o arquivo de dados tiver uma linha de cabeçalho, você precisará adicionar essa propriedade **ao final** da consulta *create table*.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If the data file has a header line, you have to add this property **at the end** of the *create table* query.</span></span> <span data-ttu-id="0fd9e-197">Caso contrário, a linha de cabeçalho será carregada como um registro para a tabela.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-197">Otherwise, the header line is loaded as a record to the table.</span></span> <span data-ttu-id="0fd9e-198">Se o arquivo de dados não tiver uma linha de cabeçalho, essa configuração pode ser omitida na consulta.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-198">If the data file does not have a header line, this configuration can be omitted in the query.</span></span>

## <span data-ttu-id="0fd9e-199"><a name="load-data"></a>Carregar dados para tabelas Hive</span><span class="sxs-lookup"><span data-stu-id="0fd9e-199"><a name="load-data"></a>Load data to Hive tables</span></span>
<span data-ttu-id="0fd9e-200">Veja aqui a consulta Hive que carrega dados em uma tabela Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-200">Here is the Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path to blob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="0fd9e-201">**&#60;caminho para dados de blob>**: se o arquivo de blob a ser carregado para a tabela Hive estiver no contêiner padrão do cluster do Hadoop do HDInsight, o *&#60;caminho para dados de blob>* deve estar no formato 'wasb:///&#60;diretório neste *contêiner>/&#60;nome do arquivo de blob>'*.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-201">**&#60;path to blob data>**: If the blob file to be uploaded to the Hive table is in the default container of the HDInsight Hadoop cluster, the *&#60;path to blob data>* should be in the format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="0fd9e-202">O arquivo de blob também pode estar em um contêiner adicional do cluster do Hadoop do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-202">The blob file can also be in an additional container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="0fd9e-203">Nesse caso, *&#60;caminho para dados de blob>* deve estar no formato *'wasb://&#60;nome do contêiner>@&#60;nome da conta de armazenamento>.blob.core.windows.net/&#60;nome do arquivo de blob>'*.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-203">In this case, *&#60;path to blob data>* should be in the format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0fd9e-204">Os dados blob a serem carregados na tabela Hive deve estar no contêiner padrão ou adicional da conta de armazenamento para o cluster do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-204">The blob data to be uploaded to Hive table has to be in the default or additional container of the storage account for the Hadoop cluster.</span></span> <span data-ttu-id="0fd9e-205">Caso contrário, a consulta *LOAD DATA* falhará reclamando que não pode acessar os dados.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-205">Otherwise, the *LOAD DATA* query fails complaining that it cannot access the data.</span></span>
  >
  >

## <span data-ttu-id="0fd9e-206"><a name="partition-orc"></a>Tópicos avançados: tabela e repositório de dados Hive particionados no formato ORC</span><span class="sxs-lookup"><span data-stu-id="0fd9e-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="0fd9e-207">Se os dados forem grandes, particionar a tabela é útil para consultas que só precisam verificar algumas partições da tabela.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-207">If the data is large, partitioning the table is beneficial for queries that only need to scan a few partitions of the table.</span></span> <span data-ttu-id="0fd9e-208">Por exemplo, é útil particionar os dados de log de um site da Web por datas.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-208">For instance, it is reasonable to partition the log data of a web site by dates.</span></span>

<span data-ttu-id="0fd9e-209">Além do particionamento de tabelas Hive, também é útil armazenar os dados Hive no formato ORC (Colunar de Linha Otimizado).</span><span class="sxs-lookup"><span data-stu-id="0fd9e-209">In addition to partitioning Hive tables, it is also beneficial to store the Hive data in the Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="0fd9e-210">Para obter mais informações sobre a formatação ORC, consulte <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Usando arquivos ORC melhora o desempenho quando o Hive lê, grava e processa dados</a>.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="0fd9e-211">Tabela particionada</span><span class="sxs-lookup"><span data-stu-id="0fd9e-211">Partitioned table</span></span>
<span data-ttu-id="0fd9e-212">Aqui está a consulta de Hive que cria uma tabela particionada e carrega dados nela.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-212">Here is the Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="0fd9e-213">Ao consultar tabelas particionadas, é recomendável adicionar a condição de partição no **início** da cláusula `where`, pois isso melhora a eficácia de pesquisa significativamente.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-213">When querying partitioned tables, it is recommended to add the partition condition in the **beginning** of the `where` clause as this improves the efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="0fd9e-214"><a name="orc"></a>Armazenar dados Hive no formato ORC</span><span class="sxs-lookup"><span data-stu-id="0fd9e-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="0fd9e-215">Você não pode carregar dados diretamente do armazenamento de blobs em tabelas Hive armazenadas no formato ORC.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-215">You cannot directly load data from blob storage into Hive tables that is stored in the ORC format.</span></span> <span data-ttu-id="0fd9e-216">Veja aqui etapas que você deve executar para carregar dados de blobs do Azure para tabelas Hive armazenadas no formato ORC.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-216">Here are the steps that the you need to take to load data from Azure blobs to Hive tables stored in ORC format.</span></span>

<span data-ttu-id="0fd9e-217">Crie uma tabela externa **ARMAZENADA COMO ARQUIVO DE TEXTO** e carregue dados do armazenamento de blob na tabela.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage to the table.</span></span>

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

        LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="0fd9e-218">Crie uma tabela interna com o mesmo esquema que a tabela externa na etapa 1 e o mesmo delimitador de campo, e armazene dados Hive no formato ORC.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-218">Create an internal table with the same schema as the external table in step 1, with the same field delimiter, and store the Hive data in the ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="0fd9e-219">Selecione os dados da tabela externa da etapa 1 e insira-os na tabela ORC</span><span class="sxs-lookup"><span data-stu-id="0fd9e-219">Select data from the external table in step 1 and insert into the ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="0fd9e-220">Se a tabela ARQUIVO DE TEXTO *&#60;nome do banco de dados>.&#60;nome da tabela de arquivo de texto externa>* tiver partições, na ETAPA 3, o comando `SELECT * FROM <database name>.<external textfile table name>` selecionará a variável de partição como um campo no conjunto de dados retornados.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-220">If the TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, the `SELECT * FROM <database name>.<external textfile table name>` command selects the partition variable as a field in the returned data set.</span></span> <span data-ttu-id="0fd9e-221">Inserir no *&#60;nome do banco de dados>.&#60;nome da tabela ORC>* falhará, uma vez que o *&#60;nome do banco de dados>.&#60;nome da tabela ORC>* não tem a variável de partição como um campo no esquema de tabela.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-221">Inserting it into the *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have the partition variable as a field in the table schema.</span></span> <span data-ttu-id="0fd9e-222">Nesse caso, você precisa selecionar especificamente os campos que serão inseridos ao *&#60;nome do banco de dados>.&#60;nome da tabela ORC>*, como mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="0fd9e-222">In this case, you need to specifically select the fields to be inserted to *&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="0fd9e-223">É seguro remover o *&#60;nome da tabela do arquivo de texto externa>* ao usar a consulta a seguir depois de todos os dados serem inseridos no *&#60;nome do banco de dados>.&#60;nome da tabela ORC>*:</span><span class="sxs-lookup"><span data-stu-id="0fd9e-223">It is safe to drop the *&#60;external textfile table name>* when using the following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="0fd9e-224">Depois de seguir esse procedimento, você deve ter uma tabela com dados no formato ORC pronta para uso.</span><span class="sxs-lookup"><span data-stu-id="0fd9e-224">After following this procedure, you should have a table with data in the ORC format ready to use.</span></span>  
