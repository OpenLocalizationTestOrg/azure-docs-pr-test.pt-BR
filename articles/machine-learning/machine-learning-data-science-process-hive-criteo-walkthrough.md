---
title: "Olá processo de ciência de dados de equipe na ação - usando um Cluster de Hadoop de HDInsight do Azure em um conjunto de dados de 1 TB | Microsoft Docs"
description: "Usando Olá, equipe de processo de ciência de dados para um cenário de ponta a ponta empregando uma HDInsight Hadoop toobuild de cluster e implantar um modelo usando (1 TB) disponível publicamente conjuntos de dados grandes"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="3e068-103">Olá processo de ciência de dados de equipe na ação - usando um Cluster de Hadoop de HDInsight do Azure em um conjunto de dados de 1 TB</span><span class="sxs-lookup"><span data-stu-id="3e068-103">hello Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="3e068-104">Neste passo a passo, estamos demonstram o uso Olá o processo de ciência de dados de equipe em um cenário de ponta a ponta com um [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, explorar, engenheiro de recursos e para baixo de dados de exemplo de uma saudação publicamente disponível [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="3e068-104">In this walkthrough, we demonstrate using hello Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data from one of hello publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="3e068-105">Usamos o aprendizado de máquina do Azure toobuild um modelo de classificação binária nesses dados.</span><span class="sxs-lookup"><span data-stu-id="3e068-105">We use Azure Machine Learning toobuild a binary classification model on this data.</span></span> <span data-ttu-id="3e068-106">Também mostramos como toopublish um desses modelos como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="3e068-106">We also show how toopublish one of these models as a Web service.</span></span>

<span data-ttu-id="3e068-107">Também é possível toouse um tarefas de saudação do IPython notebook tooaccomplish apresentadas neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="3e068-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented in this walkthrough.</span></span> <span data-ttu-id="3e068-108">Os usuários que seriam como tootry essa abordagem deve consultar Olá [Criteo passo a passo usando uma conexão ODBC Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tópico.</span><span class="sxs-lookup"><span data-stu-id="3e068-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="3e068-109"><a name="dataset"></a>Descrição do conjunto de dados da Criteo</span><span class="sxs-lookup"><span data-stu-id="3e068-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="3e068-110">Olá Criteo dados são um conjunto de dados de previsão de clique que é de aproximadamente 370GB dos arquivos TSV de gzip compactado (~1.3TB descompactados), que inclui mais de 4.3 bilhões de registros.</span><span class="sxs-lookup"><span data-stu-id="3e068-110">hello Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="3e068-111">Ele é obtido a partir de 24 dias de cliques de dados disponibilizados pela [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="3e068-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="3e068-112">Para conveniência de saudação do cientistas de dados, nós forem descompactados tooexperiment disponível toous de dados com.</span><span class="sxs-lookup"><span data-stu-id="3e068-112">For hello convenience of data scientists, we have unzipped data available toous tooexperiment with.</span></span>

<span data-ttu-id="3e068-113">Cada registro deste conjunto de dados contém 40 colunas:</span><span class="sxs-lookup"><span data-stu-id="3e068-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="3e068-114">Olá primeira coluna é uma coluna de rótulo que indica se um usuário clica em um **adicionar** (valor 1) ou não clique em um (valor 0)</span><span class="sxs-lookup"><span data-stu-id="3e068-114">hello first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="3e068-115">as 13 colunas seguintes são numéricas e</span><span class="sxs-lookup"><span data-stu-id="3e068-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="3e068-116">as últimas 26 colunas são colunas categóricas</span><span class="sxs-lookup"><span data-stu-id="3e068-116">last 26 are categorical columns</span></span>

<span data-ttu-id="3e068-117">colunas de saudação são anônimas e usar uma série de nomes enumeradas: "Col1" (para a coluna de rótulo Olá) muito ' Col40 "(para última coluna de categóricos Olá).</span><span class="sxs-lookup"><span data-stu-id="3e068-117">hello columns are anonymized and use a series of enumerated names: "Col1" (for hello label column) too'Col40" (for hello last categorical column).</span></span>            

<span data-ttu-id="3e068-118">Aqui está um trecho da saudação primeiro 20 colunas de duas observações (linhas) desse conjunto de dados:</span><span class="sxs-lookup"><span data-stu-id="3e068-118">Here is an excerpt of hello first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="3e068-119">Há valores ausentes em ambas as colunas numéricas e categóricos do hello este conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="3e068-119">There are missing values in both hello numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="3e068-120">Descrevemos um método simples para lidar com valores ausentes hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-120">We describe a simple method for handling hello missing values.</span></span> <span data-ttu-id="3e068-121">Detalhes adicionais de dados saudação são explorados quando armazenamos em tabelas de Hive.</span><span class="sxs-lookup"><span data-stu-id="3e068-121">Additional details of hello data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="3e068-122">**Definição:** *taxa de Clickthrough (CTR):* é Olá porcentagem de cliques em dados saudação.</span><span class="sxs-lookup"><span data-stu-id="3e068-122">**Definition:** *Clickthrough rate (CTR):* This is hello percentage of clicks in hello data.</span></span> <span data-ttu-id="3e068-123">Este conjunto de dados Criteo, Olá CTR é cerca de % 3.3 ou 0.033.</span><span class="sxs-lookup"><span data-stu-id="3e068-123">In this Criteo dataset, hello CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="3e068-124"><a name="mltasks"></a>Exemplos de tarefas de previsão</span><span class="sxs-lookup"><span data-stu-id="3e068-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="3e068-125">Dois exemplos de problemas de previsão são abordados neste passo a passo:</span><span class="sxs-lookup"><span data-stu-id="3e068-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="3e068-126">**Classificação binária**: prevê se um usuário clicou em um anúncio:</span><span class="sxs-lookup"><span data-stu-id="3e068-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="3e068-127">Classe 0: não clicou</span><span class="sxs-lookup"><span data-stu-id="3e068-127">Class 0: No Click</span></span>
   * <span data-ttu-id="3e068-128">Classe 1: clicou</span><span class="sxs-lookup"><span data-stu-id="3e068-128">Class 1: Click</span></span>
2. <span data-ttu-id="3e068-129">**Regressão**: prevê a probabilidade de saudação do, clique em um anúncio de recursos do usuário.</span><span class="sxs-lookup"><span data-stu-id="3e068-129">**Regression**: Predicts hello probability of an ad click from user features.</span></span>

## <span data-ttu-id="3e068-130"><a name="setup"></a>Configurar um cluster Hadoop do HDInsight para ciência de dados</span><span class="sxs-lookup"><span data-stu-id="3e068-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="3e068-131">**Observação:** normalmente, esta é uma tarefa para o **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="3e068-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="3e068-132">Configure seu ambiente de Ciência de dados do Azure para a criação de soluções analíticas de previsão com clusters do HDInsight em três etapas:</span><span class="sxs-lookup"><span data-stu-id="3e068-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="3e068-133">[Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md): esta conta de armazenamento é usada toostore dados no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e068-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used toostore data in Azure Blob Storage.</span></span> <span data-ttu-id="3e068-134">dados de saudação usados em clusters de HDInsight são armazenados aqui.</span><span class="sxs-lookup"><span data-stu-id="3e068-134">hello data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="3e068-135">[Personalizar clusters Hadoop do Azure HDInsight para ciência de dados](machine-learning-data-science-customize-hadoop-cluster.md): esta etapa cria um cluster Hadoop do Azure HDInsight com o Anaconda Python 2.7 de 64 bits instalado em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="3e068-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="3e068-136">Há dois toocomplete de etapas importantes (descritas neste tópico) ao personalizar o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-136">There are two important steps (described in this topic) toocomplete when customizing hello HDInsight cluster.</span></span>
   
   * <span data-ttu-id="3e068-137">Você deve vincular a conta de armazenamento Olá criada na etapa 1 com o cluster HDInsight quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="3e068-137">You must link hello storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="3e068-138">Esta conta de armazenamento é usada para acessar os dados que podem ser processados em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-138">This storage account is used for accessing data that can be processed within hello cluster.</span></span>
   * <span data-ttu-id="3e068-139">Você deve habilitar o nó principal do toohello de acesso remoto de cluster Olá depois que ele é criado.</span><span class="sxs-lookup"><span data-stu-id="3e068-139">You must enable Remote Access toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="3e068-140">Lembre-se de credenciais de acesso remoto Olá você especificar aqui (diferentes das especificadas para cluster Olá em sua criação): é necessário toocomplete Olá seguintes procedimentos.</span><span class="sxs-lookup"><span data-stu-id="3e068-140">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them toocomplete hello following procedures.</span></span>
3. <span data-ttu-id="3e068-141">[Criar um espaço de trabalho do Azure ML](machine-learning-create-workspace.md): aprendizado de máquina do Azure este espaço de trabalho é usado para criar modelos de aprendizado de máquina após uma exploração de dados inicial e para baixo de amostragem no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on hello HDInsight cluster.</span></span>

## <span data-ttu-id="3e068-142"><a name="getdata"></a>Obter e consumir dados de uma fonte de pública</span><span class="sxs-lookup"><span data-stu-id="3e068-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="3e068-143">Olá [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) conjunto de dados pode ser acessado clicando no link hello, aceitando os termos de uso do hello e fornecer um nome.</span><span class="sxs-lookup"><span data-stu-id="3e068-143">hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on hello link, accepting hello terms of use, and providing a name.</span></span> <span data-ttu-id="3e068-144">Um instantâneo desse processo é mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="3e068-144">A snapshot of what this looks like is shown here:</span></span>

![Aceitar os termos da Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="3e068-146">Clique em **tooDownload continuar** tooread mais sobre o conjunto de dados hello e sua disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3e068-146">Click **Continue tooDownload** tooread more about hello dataset and its availability.</span></span>

<span data-ttu-id="3e068-147">dados de saudação residem em um público [armazenamento de BLOBs do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) local: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="3e068-147">hello data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="3e068-148">Olá "wasb" refere-se o local de armazenamento de Blob tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3e068-148">hello "wasb" refers tooAzure Blob Storage location.</span></span> 

1. <span data-ttu-id="3e068-149">dados de saudação nesse armazenamento de blob público consistem em três subpastas dos dados descompactados.</span><span class="sxs-lookup"><span data-stu-id="3e068-149">hello data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="3e068-150">Olá subpasta *bruto/count/* contém Olá primeiro 21 dias de dados - dia\_tooday 00\_20</span><span class="sxs-lookup"><span data-stu-id="3e068-150">hello subfolder *raw/count/* contains hello first 21 days of data - from day\_00 tooday\_20</span></span>
   2. <span data-ttu-id="3e068-151">Olá subpasta *bruto/treinar/* consiste em um único dia de dados, dia\_21</span><span class="sxs-lookup"><span data-stu-id="3e068-151">hello subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="3e068-152">Olá subpasta *bruto/teste/* consiste em dois dias de dados, dia\_22 e dia\_23</span><span class="sxs-lookup"><span data-stu-id="3e068-152">hello subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="3e068-153">Para aqueles que desejam toostart com dados brutos gzip de saudação, eles também estão disponíveis na pasta principal Olá *bruto /* como day_NN.gz, onde NN vai de too23 00.</span><span class="sxs-lookup"><span data-stu-id="3e068-153">For those who want toostart with hello raw gzip data, these are also available in hello main folder *raw/* as day_NN.gz, where NN goes from 00 too23.</span></span>

<span data-ttu-id="3e068-154">Tooaccess uma abordagem alternativa, explore e modele esses dados que não requerem que todos os downloads de locais é explicado mais adiante neste passo a passo durante a criação de tabelas de Hive.</span><span class="sxs-lookup"><span data-stu-id="3e068-154">An alternative approach tooaccess, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="3e068-155"><a name="login"></a>Faça logon no nó principal do cluster toohello</span><span class="sxs-lookup"><span data-stu-id="3e068-155"><a name="login"></a>Log in toohello cluster headnode</span></span>
<span data-ttu-id="3e068-156">toolog em toohello um nó principal do cluster hello, use Olá [portal do Azure](https://ms.portal.azure.com) toolocate cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e068-156">toolog in toohello headnode of hello cluster, use hello [Azure portal](https://ms.portal.azure.com) toolocate hello cluster.</span></span> <span data-ttu-id="3e068-157">Clique elefante ícone HDInsight Olá Olá à esquerda e, em seguida, clique duas vezes no nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="3e068-157">Click hello HDInsight elephant icon on hello left and then double-click hello name of your cluster.</span></span> <span data-ttu-id="3e068-158">Navegue toohello **configuração** guia, clique duas vezes Olá conectar na parte inferior da saudação da página hello e insira suas credenciais de acesso remoto quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="3e068-158">Navigate toohello **Configuration** tab, double-click hello CONNECT icon on hello bottom of hello page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="3e068-159">Isso leva você toohello um nó principal do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-159">This takes you toohello headnode of hello cluster.</span></span>

<span data-ttu-id="3e068-160">Um típico primeiro log no nó principal do cluster toohello é semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="3e068-160">Here is what a typical first log in toohello cluster headnode looks like:</span></span>

![Faça logon no toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="3e068-162">Olá esquerda, vemos hello "Hadoop linha de comando", que é nossa força de trabalho Olá exploração de dados.</span><span class="sxs-lookup"><span data-stu-id="3e068-162">On hello left, we see hello "Hadoop Command Line", which is our workhorse for hello data exploration.</span></span> <span data-ttu-id="3e068-163">Nós também vemos duas URLs úteis - "Status do Hadoop Yarn" e "Nó de Nome do Hadoop".</span><span class="sxs-lookup"><span data-stu-id="3e068-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="3e068-164">Olá yarn status URL mostra o andamento do trabalho e URL do nó nome hello fornece detalhes sobre configuração de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e068-164">hello yarn status URL shows job progress and hello name node URL gives details on hello cluster configuration.</span></span>

<span data-ttu-id="3e068-165">Agora são configurados e pronto toobegin primeira parte da saudação passo a passo: usando Hive e preparar dados para o aprendizado de máquina do Azure a exploração de dados.</span><span class="sxs-lookup"><span data-stu-id="3e068-165">Now we are set up and ready toobegin first part of hello walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="3e068-166"><a name="hive-db-tables"></a> Criar tabelas e banco de dados do Hive</span><span class="sxs-lookup"><span data-stu-id="3e068-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="3e068-167">toocreate Hive tabelas para nosso conjunto de dados Criteo, abra Olá ***linha de comando do Hadoop*** na Olá a área de trabalho do nó principal hello e insira o diretório de Hive Olá digitando o comando Olá</span><span class="sxs-lookup"><span data-stu-id="3e068-167">toocreate Hive tables for our Criteo dataset, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="3e068-168">Executar todos os comandos de Hive neste passo a passo do compartimento de Hive Olá / prompt do diretório.</span><span class="sxs-lookup"><span data-stu-id="3e068-168">Run all Hive commands in this walkthrough from hello Hive bin/ directory prompt.</span></span> <span data-ttu-id="3e068-169">Isso soluciona automaticamente possíveis problemas de caminho.</span><span class="sxs-lookup"><span data-stu-id="3e068-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="3e068-170">Usamos termos Olá "Hive diretório" prompt, "Hive bin / aviso diretório" e "linha de comando do Hadoop" alternadamente.</span><span class="sxs-lookup"><span data-stu-id="3e068-170">We use hello terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="3e068-171">tooexecute qualquer consulta de Hive, você sempre pode usar Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e068-171">tooexecute any Hive query, one can always use hello following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="3e068-172">Após Olá Hive REPL aparece com um "hive >" entrar, basta recortar e colar Olá consulta tooexecute-lo.</span><span class="sxs-lookup"><span data-stu-id="3e068-172">After hello Hive REPL appears with a "hive >"sign, simply cut and paste hello query tooexecute it.</span></span>

<span data-ttu-id="3e068-173">Olá código a seguir cria um banco de dados "criteo" e, em seguida, gera 4 tabelas:</span><span class="sxs-lookup"><span data-stu-id="3e068-173">hello following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="3e068-174">um *tabela para gerar contagens* criado no dia dias\_tooday 00\_20,</span><span class="sxs-lookup"><span data-stu-id="3e068-174">a *table for generating counts* built on days day\_00 tooday\_20,</span></span>
* <span data-ttu-id="3e068-175">um *tabela para uso como Olá conjunto de dados de treinamento* criado no dia\_21, e</span><span class="sxs-lookup"><span data-stu-id="3e068-175">a *table for use as hello train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="3e068-176">dois *conjuntos de dados de teste de tabelas para uso como Olá* criado no dia\_22 e dia\_23 respectivamente.</span><span class="sxs-lookup"><span data-stu-id="3e068-176">two *tables for use as hello test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="3e068-177">Dividiremos nosso conjunto de dados de teste em duas tabelas diferentes, porque um dos dias Olá é um feriado e queremos toodetermine se modelo Olá pode detectar diferenças entre um feriado e não feriado da taxa de clickthrough hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-177">We split our test dataset into two different tables because one of hello days is a holiday, and we want toodetermine if hello model can detect differences between a holiday and non-holiday from hello clickthrough rate.</span></span>

<span data-ttu-id="3e068-178">Olá script [exemplo #95; hive & #95; criar & #95; criteo & #95; banco de dados & #95; e & #95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) será exibido aqui para sua conveniência:</span><span class="sxs-lookup"><span data-stu-id="3e068-178">hello script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

<span data-ttu-id="3e068-179">Observe que todas essas tabelas são externas como podemos simplesmente locais de armazenamento de Blob (wasb) tooAzure de ponto.</span><span class="sxs-lookup"><span data-stu-id="3e068-179">We note that all these tables are external as we simply point tooAzure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="3e068-180">**Há duas maneiras tooexecute Hive qualquer consulta que mencionamos agora.**</span><span class="sxs-lookup"><span data-stu-id="3e068-180">**There are two ways tooexecute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="3e068-181">**Usando Olá Hive REPL de linha de comando**: Olá primeiro é tooissue um comando "hive" e copie e cole uma consulta em Olá Hive REPL de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="3e068-181">**Using hello Hive REPL command-line**: hello first is tooissue a "hive" command and copy and paste a query at hello Hive REPL command-line.</span></span> <span data-ttu-id="3e068-182">toodo isso, execute:</span><span class="sxs-lookup"><span data-stu-id="3e068-182">toodo this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="3e068-183">Agora no hello REPL de linha de comando, recortando e colando consulta Olá executa-o.</span><span class="sxs-lookup"><span data-stu-id="3e068-183">Now at hello REPL command-line, cutting and pasting hello query executes it.</span></span>
2. <span data-ttu-id="3e068-184">**Salvar consultas tooa arquivo e executar o comando Olá**: Olá segundo é o arquivo de .hql do toosave Olá consultas tooa ([exemplo #95; hive & #95; criar & #95; criteo & #95; banco de dados & #95; e & #95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) e, em seguida, que o comando de problema a seguir de saudação tooexecute consulta de saudação:</span><span class="sxs-lookup"><span data-stu-id="3e068-184">**Saving queries tooa file and executing hello command**: hello second is toosave hello queries tooa .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue hello following command tooexecute hello query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="3e068-185">Confirme a criação do banco de dados e da tabela</span><span class="sxs-lookup"><span data-stu-id="3e068-185">Confirm database and table creation</span></span>
<span data-ttu-id="3e068-186">Em seguida, podemos confirmar a criação de Olá do banco de dados de saudação com hello comando a seguir do compartimento de Hive Olá / aviso diretório:</span><span class="sxs-lookup"><span data-stu-id="3e068-186">Next, we confirm hello creation of hello database with hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="3e068-187">Isso fornece:</span><span class="sxs-lookup"><span data-stu-id="3e068-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="3e068-188">Isso confirma a criação de saudação do banco de dados de novo hello, "criteo".</span><span class="sxs-lookup"><span data-stu-id="3e068-188">This confirms hello creation of hello new database, "criteo".</span></span>

<span data-ttu-id="3e068-189">toosee quais tabelas criadas, podemos simplesmente execute Olá comando aqui do compartimento de Hive Olá / aviso diretório:</span><span class="sxs-lookup"><span data-stu-id="3e068-189">toosee what tables we created, we simply issue hello command here from hello Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="3e068-190">Em seguida, vemos Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e068-190">We then see hello following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="3e068-191"><a name="exploration"></a> Exploração de dados no Hive</span><span class="sxs-lookup"><span data-stu-id="3e068-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="3e068-192">Agora estamos prontos toodo alguma exploração de dados básica no Hive.</span><span class="sxs-lookup"><span data-stu-id="3e068-192">Now we are ready toodo some basic data exploration in Hive.</span></span> <span data-ttu-id="3e068-193">Vamos começar contando Olá número de exemplos no treinamento de saudação e tabelas de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="3e068-193">We begin by counting hello number of examples in hello train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="3e068-194">Número de exemplos de treinamento</span><span class="sxs-lookup"><span data-stu-id="3e068-194">Number of train examples</span></span>
<span data-ttu-id="3e068-195">Olá conteúdo de [exemplo & #95; hive & #95; contagem & #95; treinar #95; tabela & #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) são mostradas aqui:</span><span class="sxs-lookup"><span data-stu-id="3e068-195">hello contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="3e068-196">Isso resulta em:</span><span class="sxs-lookup"><span data-stu-id="3e068-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="3e068-197">Como alternativa, um também pode emitir Olá comando a seguir do compartimento de Hive Olá / aviso diretório:</span><span class="sxs-lookup"><span data-stu-id="3e068-197">Alternatively, one may also issue hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a><span data-ttu-id="3e068-198">Número de exemplos de teste Olá dois conjuntos de dados de teste</span><span class="sxs-lookup"><span data-stu-id="3e068-198">Number of test examples in hello two test datasets</span></span>
<span data-ttu-id="3e068-199">Podemos contar o número de Olá exemplos Olá dois conjuntos de dados de teste agora.</span><span class="sxs-lookup"><span data-stu-id="3e068-199">We now count hello number of examples in hello two test datasets.</span></span> <span data-ttu-id="3e068-200">Olá conteúdo de [exemplo & #95 hive & #95; contagem & #95; criteo & #95; teste & #95; dia & #95; 22 & #95; tabela de & #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) aqui:</span><span class="sxs-lookup"><span data-stu-id="3e068-200">hello contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="3e068-201">Isso resulta em:</span><span class="sxs-lookup"><span data-stu-id="3e068-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="3e068-202">Como de costume, podemos também pode chamar script hello do compartimento de Hive Olá / diretório prompt emitindo o comando hello:</span><span class="sxs-lookup"><span data-stu-id="3e068-202">As usual, we may also call hello script from hello Hive bin/ directory prompt by issuing hello command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="3e068-203">Por fim, podemos examinar número Olá dos exemplos de teste no conjunto de dados de teste de saudação com base no dia\_23.</span><span class="sxs-lookup"><span data-stu-id="3e068-203">Finally, we examine hello number of test examples in hello test dataset based on day\_23.</span></span>

<span data-ttu-id="3e068-204">Olá comando toodo isso é semelhante toohello mostrada apenas (consulte muito[exemplo & #95; hive #95; contagem & #95; criteo & #95; teste & #95; dia & #95; 23 & #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="3e068-204">hello command toodo this is similar toohello one just shown (refer too[sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="3e068-205">Isso fornece:</span><span class="sxs-lookup"><span data-stu-id="3e068-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a><span data-ttu-id="3e068-206">Distribuição de rótulo no conjunto de dados de treinamento Olá</span><span class="sxs-lookup"><span data-stu-id="3e068-206">Label distribution in hello train dataset</span></span>
<span data-ttu-id="3e068-207">distribuição de rótulo Olá no conjunto de dados de treinamento de saudação é de interesse.</span><span class="sxs-lookup"><span data-stu-id="3e068-207">hello label distribution in hello train dataset is of interest.</span></span> <span data-ttu-id="3e068-208">toosee isso, vamos mostrar conteúdo do [exemplo & #95; hive & #95; criteo & #95; rótulo #95; distribuição & #95; treinar & #95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="3e068-208">toosee this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="3e068-209">Isso resulta em distribuição de rótulo hello:</span><span class="sxs-lookup"><span data-stu-id="3e068-209">This yields hello label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="3e068-210">Observe que a porcentagem de saudação de rótulos positivos é 3.3% (consistente com o conjunto de dados original Olá).</span><span class="sxs-lookup"><span data-stu-id="3e068-210">Note that hello percentage of positive labels is about 3.3% (consistent with hello original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="3e068-211">Distribuições de histograma de algumas variáveis numéricas em Olá treinar o conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="3e068-211">Histogram distributions of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="3e068-212">Podemos usar nativo do Hive "histograma\_numérico" função toofind out que distribuição Olá de variáveis numéricas Olá aparência.</span><span class="sxs-lookup"><span data-stu-id="3e068-212">We can use Hive's native "histogram\_numeric" function toofind out what hello distribution of hello numeric variables looks like.</span></span> <span data-ttu-id="3e068-213">Aqui estão os conteúdos de saudação do [exemplo & #95; hive #95; criteo & #95; histograma & #95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="3e068-213">Here are hello contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="3e068-214">Isso gera o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="3e068-214">This yields hello following:</span></span>

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

<span data-ttu-id="3e068-215">Olá LATERAL exibição - explodir combinação na seção serve tooproduce uma saída semelhante a SQL em vez de lista de saudação normal.</span><span class="sxs-lookup"><span data-stu-id="3e068-215">hello LATERAL VIEW - explode combination in Hive serves tooproduce a SQL-like output instead of hello usual list.</span></span> <span data-ttu-id="3e068-216">Observe que no hello essa tabela, a primeira coluna de saudação corresponde toohello bin center e hello segundo toohello bin frequência.</span><span class="sxs-lookup"><span data-stu-id="3e068-216">Note that in hello this table, hello first column corresponds toohello bin center and hello second toohello bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="3e068-217">Percentuais aproximados de algumas variáveis numéricas em Olá treinar o conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="3e068-217">Approximate percentiles of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="3e068-218">Também interesse com variáveis numéricas é computar Olá percentuais aproximados.</span><span class="sxs-lookup"><span data-stu-id="3e068-218">Also of interest with numeric variables is hello computation of approximate percentiles.</span></span> <span data-ttu-id="3e068-219">O "percentile\_approx" nativo do Hive faz isso para nós.</span><span class="sxs-lookup"><span data-stu-id="3e068-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="3e068-220">Olá conteúdo de [exemplo & #95; hive #95; criteo & #95; aproximado & #95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) são:</span><span class="sxs-lookup"><span data-stu-id="3e068-220">hello contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="3e068-221">Isso resulta em:</span><span class="sxs-lookup"><span data-stu-id="3e068-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="3e068-222">Podemos remarque distribuição Olá percentuais é toohello relacionadas histograma distribuição de qualquer variável numérica normalmente.</span><span class="sxs-lookup"><span data-stu-id="3e068-222">We remark that hello distribution of percentiles is closely related toohello histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a><span data-ttu-id="3e068-223">Localize o número de valores exclusivos para algumas colunas categóricas no conjunto de dados de treinamento Olá</span><span class="sxs-lookup"><span data-stu-id="3e068-223">Find number of unique values for some categorical columns in hello train dataset</span></span>
<span data-ttu-id="3e068-224">Continuar a exploração de dados Olá, encontramos agora, para algumas colunas categóricas, número de saudação de valores exclusivos que eles executam.</span><span class="sxs-lookup"><span data-stu-id="3e068-224">Continuing hello data exploration, we now find, for some categorical columns, hello number of unique values they take.</span></span> <span data-ttu-id="3e068-225">toodo isso, vamos mostrar conteúdo do [exemplo & #95; hive #95; criteo & #95; exclusivo & #95; valores & #95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="3e068-225">toodo this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="3e068-226">Isso resulta em:</span><span class="sxs-lookup"><span data-stu-id="3e068-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="3e068-227">Observe que Col15 tem valores exclusivos em 19M!</span><span class="sxs-lookup"><span data-stu-id="3e068-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="3e068-228">Essas variáveis categóricas altamente dimensional usando técnicas simples como "hot uma codificação" tooencode for inviável.</span><span class="sxs-lookup"><span data-stu-id="3e068-228">Using naive techniques like "one-hot encoding" tooencode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="3e068-229">Em particular, nós explicamos e demonstramos uma técnica poderosa e robusta chamada [Aprendizado com contagens](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) para lidar com esse problema de modo eficaz.</span><span class="sxs-lookup"><span data-stu-id="3e068-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="3e068-230">Podemos terminar esta subseção examinando Olá número de valores exclusivos de algumas outras colunas categóricas também.</span><span class="sxs-lookup"><span data-stu-id="3e068-230">We end this sub-section by looking at hello number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="3e068-231">Olá conteúdo de [exemplo & #95; hive #95; criteo & #95; exclusivo & #95; valores & #95; vários & #95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) são:</span><span class="sxs-lookup"><span data-stu-id="3e068-231">hello contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="3e068-232">Isso resulta em:</span><span class="sxs-lookup"><span data-stu-id="3e068-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="3e068-233">Novamente, vemos que, exceto Col20, todos os Olá outras colunas têm muitos valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="3e068-233">Again we see that except for Col20, all hello other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a><span data-ttu-id="3e068-234">Contagens de ocorrência do conjunto de pares de variáveis categóricas no conjunto de dados de treinamento Olá</span><span class="sxs-lookup"><span data-stu-id="3e068-234">Co-occurrence counts of pairs of categorical variables in hello train dataset</span></span>

<span data-ttu-id="3e068-235">contagens de ocorrência colegas Olá de pares de variáveis categóricas também é de interesse.</span><span class="sxs-lookup"><span data-stu-id="3e068-235">hello co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="3e068-236">Isso pode ser determinado usando o código Olá [exemplo & #95; hive #95; criteo & #95; emparelhados & #95; categóricos & #95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="3e068-236">This can be determined using hello code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="3e068-237">Nós inverter a ordem Olá contagens por sua ocorrência e procure na parte superior do hello 15 nesse caso.</span><span class="sxs-lookup"><span data-stu-id="3e068-237">We reverse order hello counts by their occurrence and look at hello top 15 in this case.</span></span> <span data-ttu-id="3e068-238">Isso nos fornece:</span><span class="sxs-lookup"><span data-stu-id="3e068-238">This gives us:</span></span>

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <span data-ttu-id="3e068-239"><a name="downsample"></a>Para conjuntos de dados do exemplo hello para aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="3e068-239"><a name="downsample"></a> Down sample hello datasets for Azure Machine Learning</span></span>
<span data-ttu-id="3e068-240">Ter explorado Olá conjuntos de dados e demonstrar como podemos pode fazer esse tipo de exploração para quaisquer variáveis (incluindo combinações), que agora para baixo de conjuntos de dados do exemplo hello para que podemos criar modelos no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e068-240">Having explored hello datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample hello data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="3e068-241">Lembre-se nos concentraremos no problema Olá é: dado um conjunto de atributos de exemplo (valores de recurso de Col2 - Col40), podemos prever se Col1 é 0 (nenhum clique) ou 1 (clique).</span><span class="sxs-lookup"><span data-stu-id="3e068-241">Recall that hello problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="3e068-242">toodown exemplo nosso treinar e testar conjuntos de dados too1% do tamanho original hello, usamos a função RAND () da nativa do Hive.</span><span class="sxs-lookup"><span data-stu-id="3e068-242">toodown sample our train and test datasets too1% of hello original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="3e068-243">Olá próximo script, [exemplo & #95; hive #95; criteo & #95; diminuir a resolução & #95; treinar & #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) faz isso para o conjunto de dados de treinamento hello:</span><span class="sxs-lookup"><span data-stu-id="3e068-243">hello next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for hello train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="3e068-244">Isso resulta em:</span><span class="sxs-lookup"><span data-stu-id="3e068-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="3e068-245">Olá script [exemplo & #95; hive #95; criteo & #95; diminuir a resolução & #95; teste & #95; dia & #95; 22 & #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) faz isso para dados de teste, dia\_22:</span><span class="sxs-lookup"><span data-stu-id="3e068-245">hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="3e068-246">Isso resulta em:</span><span class="sxs-lookup"><span data-stu-id="3e068-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="3e068-247">Por fim, Olá script [exemplo & #95; hive #95; criteo & #95; diminuir a resolução & #95; teste & #95; dia & #95; 23 & #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) faz isso para dados de teste, dia\_23:</span><span class="sxs-lookup"><span data-stu-id="3e068-247">Finally, hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="3e068-248">Isso resulta em:</span><span class="sxs-lookup"><span data-stu-id="3e068-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="3e068-249">Com isso, estamos toouse pronto nosso baixo amostra treinar e testar os conjuntos de dados para a criação de modelos no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e068-249">With this, we are ready toouse our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="3e068-250">Há um componente importante final antes de continuarmos tooAzure aprendizado de máquina, que é a tabela de contagem de saudação preocupações.</span><span class="sxs-lookup"><span data-stu-id="3e068-250">There is a final important component before we move on tooAzure Machine Learning, which is concerns hello count table.</span></span> <span data-ttu-id="3e068-251">Olá próxima subseção, discutiremos isso em detalhes.</span><span class="sxs-lookup"><span data-stu-id="3e068-251">In hello next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="3e068-252"><a name="count"></a>Uma breve discussão sobre a tabela de contagem de saudação</span><span class="sxs-lookup"><span data-stu-id="3e068-252"><a name="count"></a> A brief discussion on hello count table</span></span>
<span data-ttu-id="3e068-253">Como vimos, diversas variáveis categóricas têm uma dimensionalidade muito alta.</span><span class="sxs-lookup"><span data-stu-id="3e068-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="3e068-254">Em nosso passo a passo, vamos apresentar uma técnica poderosa chamada [aprendizado com contagens](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode essas variáveis de maneira eficiente e robusta.</span><span class="sxs-lookup"><span data-stu-id="3e068-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="3e068-255">Para obter mais informações sobre essa técnica são Olá link fornecido.</span><span class="sxs-lookup"><span data-stu-id="3e068-255">More information on this technique is in hello link provided.</span></span>

[!NOTE]
><span data-ttu-id="3e068-256">Este passo a passo, vamos nos concentrar em usando tooproduce de tabelas de contagem compact representações de recursos categóricos altamente dimensional.</span><span class="sxs-lookup"><span data-stu-id="3e068-256">In this walkthrough, we focus on using count tables tooproduce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="3e068-257">Isso não é Olá somente modo tooencode recursos categóricos; Para obter mais informações sobre outras técnicas, os usuários interessados podem check-out [um hot-codificação](http://en.wikipedia.org/wiki/One-hot) e [hash de recurso](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="3e068-257">This is not hello only way tooencode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="3e068-258">tabelas de contagem de toobuild nos dados de contagem de Olá, usamos Olá dados na pasta bruto de saudação/contagem.</span><span class="sxs-lookup"><span data-stu-id="3e068-258">toobuild count tables on hello count data, we use hello data in hello folder raw/count.</span></span> <span data-ttu-id="3e068-259">Em Olá modelagem seção, vamos mostrar aos usuários como toobuild elas contam tabelas para recursos categóricos do zero ou, Alternativamente, toouse uma tabela de contagem predefinidos para seus explorações.</span><span class="sxs-lookup"><span data-stu-id="3e068-259">In hello modeling section, we show users how toobuild these count tables for categorical features from scratch, or alternatively toouse a pre-built count table for their explorations.</span></span> <span data-ttu-id="3e068-260">O que segue, quando fazemos referência muito "pré-criados tabelas de contagem", queremos dizer usando tabelas de contagem de saudação que fornecemos.</span><span class="sxs-lookup"><span data-stu-id="3e068-260">In what follows, when we refer too"pre-built count tables", we mean using hello count tables that we provide.</span></span> <span data-ttu-id="3e068-261">Instruções detalhadas sobre como tooaccess essas tabelas são fornecidas na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="3e068-261">Detailed instructions on how tooaccess these tables are provided in hello next section.</span></span>

## <span data-ttu-id="3e068-262">
            <a name="aml">
            </a> Criar um modelo com o Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3e068-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="3e068-263">Nosso processo de criação de modelo no Azure Machine Learning seguirá estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3e068-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="3e068-264">Obter dados de saudação de tabelas de Hive para aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="3e068-264">Get hello data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="3e068-265">Criar experiência Olá: limpar dados saudação e featurize com tabelas de contagem</span><span class="sxs-lookup"><span data-stu-id="3e068-265">Create hello experiment: clean hello data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="3e068-266">Compilação, treinar e modelo de pontuação Olá</span><span class="sxs-lookup"><span data-stu-id="3e068-266">Build, train, and score hello model</span></span>](#step3)
4. [<span data-ttu-id="3e068-267">Avaliar modelo Olá</span><span class="sxs-lookup"><span data-stu-id="3e068-267">Evaluate hello model</span></span>](#step4)
5. [<span data-ttu-id="3e068-268">Publicar o modelo de saudação como um serviço web</span><span class="sxs-lookup"><span data-stu-id="3e068-268">Publish hello model as a web-service</span></span>](#step5)

<span data-ttu-id="3e068-269">Agora estamos prontos toobuild modelos no estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e068-269">Now we are ready toobuild models in Azure Machine Learning studio.</span></span> <span data-ttu-id="3e068-270">Os dados de amostrados para baixo é salvo como tabelas de Hive no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-270">Our down sampled data is saved as Hive tables in hello cluster.</span></span> <span data-ttu-id="3e068-271">Usamos hello Azure Machine Learning **importar dados** tooread módulo esses dados.</span><span class="sxs-lookup"><span data-stu-id="3e068-271">We use hello Azure Machine Learning **Import Data** module tooread this data.</span></span> <span data-ttu-id="3e068-272">conta de armazenamento de Olá Olá credenciais tooaccess desse cluster são fornecidas a seguir.</span><span class="sxs-lookup"><span data-stu-id="3e068-272">hello credentials tooaccess hello storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="3e068-273"><a name="step1"></a>Etapa 1: Obter dados de tabelas de Hive no aprendizado de máquina do Azure usando o módulo de importação de dados hello e selecioná-lo para uma experiência de aprendizado de máquina</span><span class="sxs-lookup"><span data-stu-id="3e068-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using hello Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="3e068-274">Comece selecionando **+NOVO** -> **EXPERIMENTO** -> **Experimento em Branco**.</span><span class="sxs-lookup"><span data-stu-id="3e068-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="3e068-275">Em seguida, de saudação **pesquisa** caixa Olá parte superior esquerda, pesquise "Importar dados".</span><span class="sxs-lookup"><span data-stu-id="3e068-275">Then, from hello **Search** box on hello top left, search for "Import Data".</span></span> <span data-ttu-id="3e068-276">Saudação de arrastar e soltar **importar dados** módulo no módulo de saudação de toouse toohello experimento tela (Olá parte do meio da tela hello) para acesso a dados.</span><span class="sxs-lookup"><span data-stu-id="3e068-276">Drag and drop hello **Import Data** module on toohello experiment canvas (hello middle portion of hello screen) toouse hello module for data access.</span></span>

<span data-ttu-id="3e068-277">Isso é que hello **importar dados** parece com ao obter dados da tabela de Hive hello:</span><span class="sxs-lookup"><span data-stu-id="3e068-277">This is what hello **Import Data** looks like while getting data from hello Hive table:</span></span>

![Importar Dados obtém os dados](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="3e068-279">Para Olá **importar dados** módulo, valores de Olá dos parâmetros de saudação que são fornecidas no hello gráfico são apenas exemplos de saudação classificação de valores que você precisa tooprovide.</span><span class="sxs-lookup"><span data-stu-id="3e068-279">For hello **Import Data** module, hello values of hello parameters that are provided in hello graphic are just examples of hello sort of values you need tooprovide.</span></span> <span data-ttu-id="3e068-280">Aqui estão algumas diretrizes gerais sobre como toofill parâmetro hello out definidas para Olá **importar dados** módulo.</span><span class="sxs-lookup"><span data-stu-id="3e068-280">Here is some general guidance on how toofill out hello parameter set for hello **Import Data** module.</span></span>

1. <span data-ttu-id="3e068-281">Escolha "Consulta de Hive" para **Fonte de dados**</span><span class="sxs-lookup"><span data-stu-id="3e068-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="3e068-282">Em Olá **consulta de banco de dados de Hive** caixa, um simples SELECT * FROM < seu\_banco de dados\_name.your\_tabela\_nome >-é suficiente.</span><span class="sxs-lookup"><span data-stu-id="3e068-282">In hello **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="3e068-283">**URI do servidor Hcatalog**: se o cluster é"abc", isso é simplesmente: https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="3e068-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="3e068-284">**Nome de conta de usuário do Hadoop**: nome de usuário Olá escolhido no momento da saudação de preparação de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-284">**Hadoop user account name**: hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="3e068-285">(Não Olá acesso remoto nome de usuário!)</span><span class="sxs-lookup"><span data-stu-id="3e068-285">(NOT hello Remote Access user name!)</span></span>
5. <span data-ttu-id="3e068-286">**Senha de conta de usuário do Hadoop**: senha Olá Olá nome de usuário escolhido no momento da saudação de preparação de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-286">**Hadoop user account password**: hello password for hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="3e068-287">(Não senha de acesso remoto Olá!)</span><span class="sxs-lookup"><span data-stu-id="3e068-287">(NOT hello Remote Access password!)</span></span>
6. <span data-ttu-id="3e068-288">**Local dos dados de saída**: escolha "Azure"</span><span class="sxs-lookup"><span data-stu-id="3e068-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="3e068-289">**Nome da conta de armazenamento do Azure**: Olá conta de armazenamento associada ao cluster Olá</span><span class="sxs-lookup"><span data-stu-id="3e068-289">**Azure storage account name**: hello storage account associated with hello cluster</span></span>
8. <span data-ttu-id="3e068-290">**Chave de conta de armazenamento do Azure**: chave Olá Olá da conta de armazenamento associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="3e068-290">**Azure storage account key**: hello key of hello storage account associated with hello cluster.</span></span>
9. <span data-ttu-id="3e068-291">**Nome do contêiner do Azure**: se o nome de cluster Olá é "abc", isso costuma ser simplesmente "abc",.</span><span class="sxs-lookup"><span data-stu-id="3e068-291">**Azure container name**: If hello cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="3e068-292">Uma vez Olá **importar dados** termina a obtenção de dados (consulte escala Olá verde no módulo de saudação), salvar os dados como um conjunto de dados (com um nome de sua escolha).</span><span class="sxs-lookup"><span data-stu-id="3e068-292">Once hello **Import Data** finishes getting data (you see hello green tick on hello Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="3e068-293">A aparência é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="3e068-293">What this looks like:</span></span>

![Importar Dados salva os dados](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="3e068-295">Porta de saudação de saída de saudação do botão direito do mouse **importar dados** módulo.</span><span class="sxs-lookup"><span data-stu-id="3e068-295">Right-click hello output port of hello **Import Data** module.</span></span> <span data-ttu-id="3e068-296">Isso revela uma opção **Salvar como conjunto de dados** e uma opção **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="3e068-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="3e068-297">Olá **visualizar** opção, se selecionada, exibe 100 linhas de dados hello, juntamente com um painel à direita que é útil para algumas estatísticas de resumo.</span><span class="sxs-lookup"><span data-stu-id="3e068-297">hello **Visualize** option, if clicked, displays 100 rows of hello data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="3e068-298">dados de toosave, basta selecionar **Salvar como conjunto de dados** e siga as instruções.</span><span class="sxs-lookup"><span data-stu-id="3e068-298">toosave data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="3e068-299">tooselect Olá Salvar conjunto de dados para uso em uma experiência de aprendizado de máquina, localize Olá conjuntos de dados usando Olá **pesquisa** caixa mostrada na figura a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e068-299">tooselect hello saved dataset for use in a machine learning experiment, locate hello datasets using hello **Search** box shown in hello following figure.</span></span> <span data-ttu-id="3e068-300">Em seguida, basta digitar nome hello você deu Olá conjunto de dados parcialmente tooaccess-lo e arraste Olá dataset em Olá painel principal.</span><span class="sxs-lookup"><span data-stu-id="3e068-300">Then simply type out hello name you gave hello dataset partially tooaccess it and drag hello dataset onto hello main panel.</span></span> <span data-ttu-id="3e068-301">Removendo-o para o painel principal Olá seleciona-lo para uso em modelagem de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="3e068-301">Dropping it onto hello main panel selects it for use in machine learning modeling.</span></span>

![Drage conjunto de dados para o painel principal Olá](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="3e068-303">Faça isso para treinar hello e conjuntos de dados de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e068-303">Do this for both hello train and hello test datasets.</span></span> <span data-ttu-id="3e068-304">Além disso, lembre-se de nome de banco de dados toouse hello e nomes de tabela que você atribuiu para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="3e068-304">Also, remember toouse hello database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="3e068-305">valores de saudação usados na Figura Olá são apenas para ilustração purposes.* *</span><span class="sxs-lookup"><span data-stu-id="3e068-305">hello values used in hello figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="3e068-306"><a name="step2"></a>Etapa 2: Criar uma experiência simples no aprendizado de máquina do Azure toopredict cliques / nenhuma cliques</span><span class="sxs-lookup"><span data-stu-id="3e068-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning toopredict clicks / no clicks</span></span>
<span data-ttu-id="3e068-307">Nosso experimento do AM do Azure tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="3e068-307">Our Azure ML experiment looks like this:</span></span>

![Teste do Machine Learning](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="3e068-309">Agora, podemos examinar principais componentes de saudação desse teste.</span><span class="sxs-lookup"><span data-stu-id="3e068-309">We now examine hello key components of this experiment.</span></span> <span data-ttu-id="3e068-310">Como um lembrete, é preciso toodrag nosso salvo treinar e testar os conjuntos de dados na tela de experimento tooour primeiro.</span><span class="sxs-lookup"><span data-stu-id="3e068-310">As a reminder, we need toodrag our saved train and test datasets on tooour experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="3e068-311">Limpar dados ausentes</span><span class="sxs-lookup"><span data-stu-id="3e068-311">Clean Missing Data</span></span>
<span data-ttu-id="3e068-312">Olá **limpar dados ausentes** módulo faz o nome sugere: limpa os dados ausentes de maneiras que podem ser especificados pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="3e068-312">hello **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="3e068-313">Examinando este módulo, vemos isso:</span><span class="sxs-lookup"><span data-stu-id="3e068-313">Looking into this module, we see this:</span></span>

![Limpar dados ausentes](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="3e068-315">Aqui, escolhemos tooreplace todos os valores ausentes com um 0.</span><span class="sxs-lookup"><span data-stu-id="3e068-315">Here, we chose tooreplace all missing values with a 0.</span></span> <span data-ttu-id="3e068-316">Há outras opções, que podem ser vistas examinando as listas suspensas de saudação no módulo hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-316">There are other options as well, which can be seen by looking at hello dropdowns in hello module.</span></span>

#### <a name="feature-engineering-on-hello-data"></a><span data-ttu-id="3e068-317">Engenharia de recurso nos dados Olá</span><span class="sxs-lookup"><span data-stu-id="3e068-317">Feature engineering on hello data</span></span>
<span data-ttu-id="3e068-318">Pode haver milhões de valores exclusivos para alguns recursos categóricos de grandes conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="3e068-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="3e068-319">Usar métodos simples como codificação one-hot para representar recursos categóricos altamente dimensionais é totalmente impraticável.</span><span class="sxs-lookup"><span data-stu-id="3e068-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="3e068-320">Neste passo a passo, demonstraremos como recursos de contagem de toouse usando toogenerate interna de módulos de aprendizado de máquina do Azure compact representações dessas variáveis categóricas altamente dimensional.</span><span class="sxs-lookup"><span data-stu-id="3e068-320">In this walkthrough, we demonstrate how toouse count features using built-in Azure Machine Learning modules toogenerate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="3e068-321">Olá resultado final é um tamanho menor de modelo, mais rápidos de treinamento e métricas de desempenho que são bastante semelhante toousing outras técnicas.</span><span class="sxs-lookup"><span data-stu-id="3e068-321">hello end-result is a smaller model size, faster training times, and performance metrics that are quite comparable toousing other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="3e068-322">Criando transformações de contagem</span><span class="sxs-lookup"><span data-stu-id="3e068-322">Building counting transforms</span></span>
<span data-ttu-id="3e068-323">recursos de contagem de toobuild, usamos Olá **criar contagem transformar** módulo que está disponível no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e068-323">toobuild count features, we use hello **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="3e068-324">módulo de saudação tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="3e068-324">hello module looks like this:</span></span>

<span data-ttu-id="3e068-325">![Módulo Compilar Transformação de Contagem](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Módulo Compilar Transformação de Contagem](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="3e068-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3e068-326">Em Olá **contagem de colunas** caixa, podemos inserir as colunas que desejamos tooperform conta em.</span><span class="sxs-lookup"><span data-stu-id="3e068-326">In hello **Count columns** box, we enter those columns that we wish tooperform counts on.</span></span> <span data-ttu-id="3e068-327">Geralmente, essas são (conforme mencionado) colunas categóricas altamente dimensionais.</span><span class="sxs-lookup"><span data-stu-id="3e068-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="3e068-328">No início de saudação mencionamos Olá Criteo conjunto de dados tem 26 colunas categóricas: de Col15 tooCol40.</span><span class="sxs-lookup"><span data-stu-id="3e068-328">At hello start, we mentioned that hello Criteo dataset has 26 categorical columns: from Col15 tooCol40.</span></span> <span data-ttu-id="3e068-329">Aqui, podemos contar todos eles e dar seus índices (de 15 too40 separadas por vírgulas, como mostrado).</span><span class="sxs-lookup"><span data-stu-id="3e068-329">Here, we count on all of them and give their indices (from 15 too40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="3e068-330">módulo Olá toouse Olá MapReduce modo (apropriado para grandes conjuntos de dados), é necessário acessar o cluster HDInsight Hadoop de tooan (Olá usada para exploração de recurso pode ser reutilizada para essa finalidade bem) e suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="3e068-330">toouse hello module in hello MapReduce mode (appropriate for large datasets), we need access tooan HDInsight Hadoop cluster (hello one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="3e068-331">figuras anteriores Olá ilustram quais Olá preenchido valores como (substituir valores hello fornecidos para ilustração com aqueles relevantes para seu próprio caso de uso).</span><span class="sxs-lookup"><span data-stu-id="3e068-331">hello  previous figures illustrate what hello filled-in values look like (replace hello values provided for illustration with those relevant for your own use-case).</span></span>

![Parâmetros do módulo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="3e068-333">Figura Olá acima, mostramos como o blob de entrada hello tooenter local.</span><span class="sxs-lookup"><span data-stu-id="3e068-333">In hello figure above, we show how tooenter hello input blob location.</span></span> <span data-ttu-id="3e068-334">Esse local tem dados de saudação reservados para a criação de tabelas de contagem.</span><span class="sxs-lookup"><span data-stu-id="3e068-334">This location has hello data reserved for building count tables on.</span></span>

<span data-ttu-id="3e068-335">Após esse módulo de execução, poderemos Salvar transformação Olá para mais tarde clicando duas vezes o módulo hello e selecionando Olá **Salvar como transformar** opção:</span><span class="sxs-lookup"><span data-stu-id="3e068-335">After this module finishes running, we can save hello transform for later by right-clicking hello module and selecting hello **Save as Transform** option:</span></span>

![Opção “Salvar como transformação”](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="3e068-337">Em nossa arquitetura de teste mostrada acima, dataset hello "ytransform2" corresponde precisamente tooa salvo transformação de contagem.</span><span class="sxs-lookup"><span data-stu-id="3e068-337">In our experiment architecture shown above, hello dataset "ytransform2" corresponds precisely tooa saved count transform.</span></span> <span data-ttu-id="3e068-338">Restante Olá esse teste, vamos supor que leitor Olá usado um **criar contagem transformar** módulo em alguns dados toogenerate contagens e, em seguida, pode usar esses recursos de contagem de toogenerate contagens em trem hello e conjuntos de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="3e068-338">For hello remainder of this experiment, we assume that hello reader used a **Build Counting Transform** module on some data toogenerate counts, and can then use those counts toogenerate count features on hello train and test datasets.</span></span>

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a><span data-ttu-id="3e068-339">Escolher o que contar tooinclude recursos como parte de treinar hello e conjuntos de dados de teste</span><span class="sxs-lookup"><span data-stu-id="3e068-339">Choosing what count features tooinclude as part of hello train and test datasets</span></span>
<span data-ttu-id="3e068-340">Assim que tivermos uma contagem de transformar pronto, usuário Olá pode escolher quais tooinclude recursos em seu treinar e testar conjuntos de dados usando Olá **modificar parâmetros de tabela de contagem** módulo.</span><span class="sxs-lookup"><span data-stu-id="3e068-340">Once we have a count transform ready, hello user can choose what features tooinclude in their train and test datasets using hello **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="3e068-341">Vamos mostrar esse módulo aqui para fins de conclusão, mas, para manter a simplicidade, não use de fato no nosso experimento.</span><span class="sxs-lookup"><span data-stu-id="3e068-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![Parâmetros Modificar Tabela de Contagem](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="3e068-343">Nesse caso, como pode ser visto, escolhemos toouse probabilidades de log apenas hello e tooignore Olá retirada da coluna.</span><span class="sxs-lookup"><span data-stu-id="3e068-343">In this case, as can be seen, we have chosen toouse just hello log-odds and tooignore hello back off column.</span></span> <span data-ttu-id="3e068-344">Podemos também definir parâmetros, como o limite de compartimento de lixo hello, quantos tooadd exemplos pseudo anterior para suavizar, e se toouse qualquer Laplaciana de ruído ou não.</span><span class="sxs-lookup"><span data-stu-id="3e068-344">We can also set parameters such as hello garbage bin threshold, how many pseudo-prior examples tooadd for smoothing, and whether toouse any Laplacian noise or not.</span></span> <span data-ttu-id="3e068-345">Todos esses são os recursos avançados e é toobe observado valores padrão de saudação são um bom ponto de partida para usuários que são um novo tipo de toothis de geração de recurso.</span><span class="sxs-lookup"><span data-stu-id="3e068-345">All these are advanced features and it is toobe noted that hello default values are a good starting point for users who are new toothis type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-hello-count-features"></a><span data-ttu-id="3e068-346">Transformação de dados antes de gerar recursos de contagem de saudação</span><span class="sxs-lookup"><span data-stu-id="3e068-346">Data transformation before generating hello count features</span></span>
<span data-ttu-id="3e068-347">Agora se concentrar em um ponto importante sobre como transformar nosso treinar e testar dados tooactually anteriores gerar recursos de contagem.</span><span class="sxs-lookup"><span data-stu-id="3e068-347">Now we focus on an important point about transforming our train and test data prior tooactually generating count features.</span></span> <span data-ttu-id="3e068-348">Observe que há dois **Executar Script R** módulos usados antes de ser dados de tooour de transformação de contagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e068-348">Note that there are two **Execute R Script** modules used before we apply hello count transform tooour data.</span></span>

![Executar Script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="3e068-350">Aqui está o script de R primeiro hello:</span><span class="sxs-lookup"><span data-stu-id="3e068-350">Here is hello first R script:</span></span>

![Primeiro script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="3e068-352">Nesse script R, podemos renomear nossa toonames colunas "Col1" muito "Col40".</span><span class="sxs-lookup"><span data-stu-id="3e068-352">In this R script, we rename our columns toonames "Col1" too"Col40".</span></span> <span data-ttu-id="3e068-353">Isso ocorre porque a transformação de contagem de saudação espera nomes desse formato.</span><span class="sxs-lookup"><span data-stu-id="3e068-353">This is because hello count transform expects names of this format.</span></span>

<span data-ttu-id="3e068-354">Script de R segundo Olá, podemos equilibrar distribuição Olá entre classes positivos e negativos (classes 1 e 0 respectivamente) pela classe negativo de saudação da resolução.</span><span class="sxs-lookup"><span data-stu-id="3e068-354">In hello second R script, we balance hello distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling hello negative class.</span></span> <span data-ttu-id="3e068-355">Olá R script aqui mostra como toodo isso:</span><span class="sxs-lookup"><span data-stu-id="3e068-355">hello R script here shows how toodo this:</span></span>

![Segundo script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="3e068-357">Esse script simple do R, usamos "pos\_neg\_taxa" quantidade de saudação do tooset de equilíbrio entre hello positivo e classes negativo hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-357">In this simple R script, we use "pos\_neg\_ratio" tooset hello amount of balance between hello positive and hello negative classes.</span></span> <span data-ttu-id="3e068-358">Isso é importante toodo como melhorar desequilíbrio de classe normalmente tem benefícios de desempenho para problemas de classificação em que a distribuição de classe Olá é desviada (Lembre-se que em nosso caso, temos classes positivo 3.3% e 96,7% negativo).</span><span class="sxs-lookup"><span data-stu-id="3e068-358">This is important toodo since improving class imbalance usually has performance benefits for classification problems where hello class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-hello-count-transformation-on-our-data"></a><span data-ttu-id="3e068-359">Aplicar transformação de contagem de saudação em nossos dados</span><span class="sxs-lookup"><span data-stu-id="3e068-359">Applying hello count transformation on our data</span></span>
<span data-ttu-id="3e068-360">Por fim, podemos usar Olá **Aplicar transformação** tooapply módulo Olá transformações de contagem em nosso treinar e testar conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="3e068-360">Finally, we can use hello **Apply Transformation** module tooapply hello count transforms on our train and test datasets.</span></span> <span data-ttu-id="3e068-361">Este módulo usa a transformação de contagem de saudação salvada como uma entrada e hello treinar ou testar conjuntos de dados como Olá outras entradas e retorna dados com recursos de contagem.</span><span class="sxs-lookup"><span data-stu-id="3e068-361">This module takes hello saved count transform as one input and hello train or test datasets as hello other input, and returns data with count features.</span></span> <span data-ttu-id="3e068-362">Isso é mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="3e068-362">It is shown here:</span></span>

![Aplicar o módulo de transformação](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a><span data-ttu-id="3e068-364">Um trecho da aparência de recursos de contagem de saudação</span><span class="sxs-lookup"><span data-stu-id="3e068-364">An excerpt of what hello count features look like</span></span>
<span data-ttu-id="3e068-365">É instrutivo toosee quais recursos de contagem de saudação aparecem no nosso caso.</span><span class="sxs-lookup"><span data-stu-id="3e068-365">It is instructive toosee what hello count features look like in our case.</span></span> <span data-ttu-id="3e068-366">Mostramos aqui um trecho disso:</span><span class="sxs-lookup"><span data-stu-id="3e068-366">Here we show an excerpt of this:</span></span>

![Recursos de contagem](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="3e068-368">Neste trecho, mostramos que para as colunas de saudação que são contados em, podemos obter contagens de saudação e probabilidades de log em adição tooany relevantes backoffs.</span><span class="sxs-lookup"><span data-stu-id="3e068-368">In this excerpt, we show that for hello columns that we counted on, we get hello counts and log odds in addition tooany relevant backoffs.</span></span>

<span data-ttu-id="3e068-369">Agora estamos pronto toobuild um modelo de aprendizado de máquina do Azure usando esses conjuntos de dados transformados.</span><span class="sxs-lookup"><span data-stu-id="3e068-369">We are now ready toobuild an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="3e068-370">Na próxima seção, Olá, mostramos como isso pode ser feito.</span><span class="sxs-lookup"><span data-stu-id="3e068-370">In hello next section, we show how this can be done.</span></span>

### <span data-ttu-id="3e068-371"><a name="step3"></a>Etapa 3: Criar, treinar e classificar Olá modelo</span><span class="sxs-lookup"><span data-stu-id="3e068-371"><a name="step3"></a> Step 3: Build, train, and score hello model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="3e068-372">Opção do aprendiz</span><span class="sxs-lookup"><span data-stu-id="3e068-372">Choice of learner</span></span>
<span data-ttu-id="3e068-373">Primeiro, precisamos toochoose um aprendiz.</span><span class="sxs-lookup"><span data-stu-id="3e068-373">First, we need toochoose a learner.</span></span> <span data-ttu-id="3e068-374">Estamos indo toouse uma árvore de decisão de duas classes ampliada como nosso aprendiz.</span><span class="sxs-lookup"><span data-stu-id="3e068-374">We are going toouse a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="3e068-375">Aqui estão as opções padrão da saudação esse aprendiz:</span><span class="sxs-lookup"><span data-stu-id="3e068-375">Here are hello default options for this learner:</span></span>

![Parâmetros da árvore de decisão aumentada de duas classes](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="3e068-377">Para nossa experiência, estamos valores padrão do andamento toochoose hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-377">For our experiment, we are going toochoose hello default values.</span></span> <span data-ttu-id="3e068-378">Observe que Olá padrões são geralmente significativa e uma boa maneira tooget rápido linhas de base de desempenho.</span><span class="sxs-lookup"><span data-stu-id="3e068-378">We note that hello defaults are usually meaningful and a good way tooget quick baselines on performance.</span></span> <span data-ttu-id="3e068-379">Você pode melhorar o desempenho por varredura parâmetros se você escolher tooonce que você tem uma linha de base.</span><span class="sxs-lookup"><span data-stu-id="3e068-379">You can improve on performance by sweeping parameters if you choose tooonce you have a baseline.</span></span>

#### <a name="train-hello-model"></a><span data-ttu-id="3e068-380">Treinar modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="3e068-380">Train hello model</span></span>
<span data-ttu-id="3e068-381">Para obter treinamento, podemos simplesmente invocar um módulo **Modelo de treinamento** .</span><span class="sxs-lookup"><span data-stu-id="3e068-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="3e068-382">Olá duas entradas tooit são Aprendiz de árvore de decisão ampliada duas classes hello e nosso conjunto de dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="3e068-382">hello two inputs tooit are hello Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="3e068-383">Isso é mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="3e068-383">This is shown here:</span></span>

![Módulo Treinar Modelo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a><span data-ttu-id="3e068-385">Modelo de saudação de pontuação</span><span class="sxs-lookup"><span data-stu-id="3e068-385">Score hello model</span></span>
<span data-ttu-id="3e068-386">Assim que tivermos um modelo treinado, estamos prontos tooscore em Olá testar dataset e tooevaluate seu desempenho.</span><span class="sxs-lookup"><span data-stu-id="3e068-386">Once we have a trained model, we are ready tooscore on hello test dataset and tooevaluate its performance.</span></span> <span data-ttu-id="3e068-387">Podemos fazer isso usando Olá **modelo de pontuação** módulo mostrado Olá seguinte figura, juntamente com um **avaliar modelo** módulo:</span><span class="sxs-lookup"><span data-stu-id="3e068-387">We do this by using hello **Score Model** module shown in hello following figure, along with an **Evaluate Model** module:</span></span>

![Módulo de Modelo de Pontuação](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="3e068-389"><a name="step4"></a>Etapa 4: Avaliar modelo Olá</span><span class="sxs-lookup"><span data-stu-id="3e068-389"><a name="step4"></a> Step 4: Evaluate hello model</span></span>
<span data-ttu-id="3e068-390">Por fim, esperamos que tooanalyze o desempenho do modelo.</span><span class="sxs-lookup"><span data-stu-id="3e068-390">Finally, we would like tooanalyze model performance.</span></span> <span data-ttu-id="3e068-391">Geralmente, para dois problemas de classificação (binário) de classe, um bom exemplo é hello AUC.</span><span class="sxs-lookup"><span data-stu-id="3e068-391">Usually, for two class (binary) classification problems, a good measure is hello AUC.</span></span> <span data-ttu-id="3e068-392">toovisualize isso, podemos conectar Olá **modelo de pontuação** módulo tooan **avaliar modelo** módulo para isso.</span><span class="sxs-lookup"><span data-stu-id="3e068-392">toovisualize this, we hook up hello **Score Model** module tooan **Evaluate Model** module for this.</span></span> <span data-ttu-id="3e068-393">Clicando em **visualizar** em Olá **avaliar modelo** módulo produz um gráfico como Olá seguindo um:</span><span class="sxs-lookup"><span data-stu-id="3e068-393">Clicking **Visualize** on hello **Evaluate Model** module yields a graphic like hello following one:</span></span>

![Avaliar o modelo de BDT do módulo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="3e068-395">Binário (ou classe dois) problemas de classificação, uma boa medida de precisão da previsão é Olá área na curva (AUC).</span><span class="sxs-lookup"><span data-stu-id="3e068-395">In binary (or two class) classification problems, a good measure of prediction accuracy is hello Area Under Curve (AUC).</span></span> <span data-ttu-id="3e068-396">A seguir, mostramos nossos resultados usando esse modelo em nosso conjunto de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="3e068-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="3e068-397">tooget porta de saída de hello, com o botão direito da saudação **avaliar modelo** módulo e, em seguida, **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="3e068-397">tooget this, right-click hello output port of hello **Evaluate Model** module and then **Visualize**.</span></span>

![Módulo Visualizar modelo de avaliação](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="3e068-399"><a name="step5"></a>Etapa 5: Publicar o modelo de saudação como um serviço Web</span><span class="sxs-lookup"><span data-stu-id="3e068-399"><a name="step5"></a> Step 5: Publish hello model as a Web service</span></span>
<span data-ttu-id="3e068-400">Olá capacidade toopublish um modelo de aprendizado de máquina do Azure como serviços web com um mínimo de confusão é um recurso valioso para disponibilizá-la amplamente.</span><span class="sxs-lookup"><span data-stu-id="3e068-400">hello ability toopublish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="3e068-401">Depois disso, qualquer pessoa poderá tornar o serviço web toohello chamadas com dados de entrada que precisam que as previsões para, e serviço web de saudação usa Olá modelo tooreturn essas previsões.</span><span class="sxs-lookup"><span data-stu-id="3e068-401">Once that is done, anyone can make calls toohello web service with input data that they need predictions for, and hello web service uses hello model tooreturn those predictions.</span></span>

<span data-ttu-id="3e068-402">toodo isso, podemos primeiro salvar nosso modelo treinado como um objeto de modelo treinado.</span><span class="sxs-lookup"><span data-stu-id="3e068-402">toodo this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="3e068-403">Isso é feito clicando Olá **treinar modelo** módulo e usar Olá **Salvar como modelo treinado** opção.</span><span class="sxs-lookup"><span data-stu-id="3e068-403">This is done by right-clicking hello **Train Model** module and using hello **Save as Trained Model** option.</span></span>

<span data-ttu-id="3e068-404">Em seguida, precisamos toocreate de entrada e saída de portas para nosso serviço web:</span><span class="sxs-lookup"><span data-stu-id="3e068-404">Next, we need toocreate input and output ports for our web service:</span></span>

* <span data-ttu-id="3e068-405">uma porta de entrada usa dados em Olá mesmo formulário como dados de saudação que precisamos previsões para</span><span class="sxs-lookup"><span data-stu-id="3e068-405">an input port takes data in hello same form as hello data that we need predictions for</span></span>
* <span data-ttu-id="3e068-406">uma porta de saída retorna Olá rótulos de pontuação e as probabilidades de saudação associada.</span><span class="sxs-lookup"><span data-stu-id="3e068-406">an output port returns hello Scored Labels and hello associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a><span data-ttu-id="3e068-407">Selecione algumas linhas de dados para a porta de entrada hello</span><span class="sxs-lookup"><span data-stu-id="3e068-407">Select a few rows of data for hello input port</span></span>
<span data-ttu-id="3e068-408">É conveniente toouse um **Aplicar transformação de SQL** dados de porta de entrada do módulo tooselect apenas 10 linhas tooserve como Olá.</span><span class="sxs-lookup"><span data-stu-id="3e068-408">It is convenient toouse an **Apply SQL Transformation** module tooselect just 10 rows tooserve as hello input port data.</span></span> <span data-ttu-id="3e068-409">Selecione apenas essas linhas de dados da nossa porta de entrada usando a consulta SQL Olá mostrada aqui:</span><span class="sxs-lookup"><span data-stu-id="3e068-409">Select just these rows of data for our input port using hello SQL query shown here:</span></span>

![Dados na porta de entrada](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="3e068-411">Serviço Web</span><span class="sxs-lookup"><span data-stu-id="3e068-411">Web service</span></span>
<span data-ttu-id="3e068-412">Agora estamos prontos toorun um experimento pequeno que pode ser usado toopublish nosso serviço web.</span><span class="sxs-lookup"><span data-stu-id="3e068-412">Now we are ready toorun a small experiment that can be used toopublish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="3e068-413">Gerar dados de entrada para o serviço Web</span><span class="sxs-lookup"><span data-stu-id="3e068-413">Generate input data for webservice</span></span>
<span data-ttu-id="3e068-414">Como uma etapa de zero, como tabela de contagem de saudação for grande, vamos poucas linhas de dados de teste e gerar dados de saída dele com recursos de contagem.</span><span class="sxs-lookup"><span data-stu-id="3e068-414">As a zeroth step, since hello count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="3e068-415">Isso pode servir como formato de dados de entrada hello para nosso serviço Web.</span><span class="sxs-lookup"><span data-stu-id="3e068-415">This can serve as hello input data format for our webservice.</span></span> <span data-ttu-id="3e068-416">Isso é mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="3e068-416">This is shown here:</span></span>

![Criar dados de entrada de BDT](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="3e068-418">Para o formato de dados de entrada hello, agora podemos usar Olá saída de hello **Featurizer de contagem** módulo.</span><span class="sxs-lookup"><span data-stu-id="3e068-418">For hello input data format, we now use hello OUTPUT of hello **Count Featurizer** module.</span></span> <span data-ttu-id="3e068-419">Depois que isso experimentar termina em execução, salvar a saída de saudação do hello **Featurizer de contagem** módulo como um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="3e068-419">Once this experiment finishes running, save hello output from hello **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="3e068-420">Este conjunto de dados é usado para dados de entrada hello em Olá webservice.</span><span class="sxs-lookup"><span data-stu-id="3e068-420">This Dataset is used for hello input data in hello webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="3e068-421">Experimento de pontuação publicação do serviço Web</span><span class="sxs-lookup"><span data-stu-id="3e068-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="3e068-422">Primeiro, mostramos sua aparência.</span><span class="sxs-lookup"><span data-stu-id="3e068-422">First, we show what this looks like.</span></span> <span data-ttu-id="3e068-423">estrutura essencial Olá é um **modelo de pontuação** módulo que aceita nosso objeto treinado e algumas linhas de dados de entrada que são gerados nas etapas anteriores de saudação usando Olá **Featurizer de contagem** módulo.</span><span class="sxs-lookup"><span data-stu-id="3e068-423">hello essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in hello previous steps using hello **Count Featurizer** module.</span></span> <span data-ttu-id="3e068-424">Usamos tooproject "Selecionar colunas no conjunto de dados" hello classificado rótulos e as probabilidades de pontuação hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-424">We use "Select Columns in Dataset" tooproject out hello Scored labels and hello Score probabilities.</span></span>

![Projetar Colunas no Conjunto de Dados](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="3e068-426">Observe como Olá **selecionar colunas no conjunto de dados** módulo pode ser usado para 'Filtrar' dados de um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="3e068-426">Notice how hello **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="3e068-427">Vamos mostrar o conteúdo de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="3e068-427">We show hello contents here:</span></span>

![Filtrando com hello selecionar colunas no módulo de conjunto de dados](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="3e068-429">portas de saudação azul de entrada e saída tooget, basta clicar em **preparar webservice** na parte inferior de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="3e068-429">tooget hello blue input and output ports, you simply click **prepare webservice** at hello bottom right.</span></span> <span data-ttu-id="3e068-430">Executar esse teste também permite que nós toopublish Olá web serviço: clique em Olá **publicar WEB SERVICE** ícone no hello inferior direita mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="3e068-430">Running this experiment also allows us toopublish hello web service: click hello **PUBLISH WEB SERVICE** icon at hello bottom right, shown here:</span></span>

![PUBLICAR SERVIÇO WEB](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="3e068-432">Depois de publicado webservice hello, obtemos tooa redirecionado página que parece assim:</span><span class="sxs-lookup"><span data-stu-id="3e068-432">Once hello webservice is published, we get redirected tooa page that looks thus:</span></span>

![Painel de serviço Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="3e068-434">Podemos ver dois links para webservices no lado esquerdo da saudação:</span><span class="sxs-lookup"><span data-stu-id="3e068-434">We see two links for webservices on hello left side:</span></span>

* <span data-ttu-id="3e068-435">Olá **solicitação/resposta** serviço (ou RRS) são destinados para previsões únicas e é o que utilizamos este workshop.</span><span class="sxs-lookup"><span data-stu-id="3e068-435">hello **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="3e068-436">Olá **BATCH EXECUTION** Service (BES) é usada para previsões em lote e requer que Olá dados de entrada usados toomake previsões residem no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e068-436">hello **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that hello input data used toomake predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="3e068-437">Clicando no link Olá **solicitação/resposta** levamos tooa página que nos permite previamente gravados código em c#, python e R. Esse código pode ser usado para fazer chamadas toohello webservice convenientemente.</span><span class="sxs-lookup"><span data-stu-id="3e068-437">Clicking on hello link **REQUEST/RESPONSE** takes us tooa page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls toohello webservice.</span></span> <span data-ttu-id="3e068-438">Observe que a chave de API nesta página Olá precisa toobe usado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="3e068-438">Note that hello API key on this page needs toobe used for authentication.</span></span>

<span data-ttu-id="3e068-439">É conveniente toocopy este python code pela nova célula tooa no bloco de anotações de IPython hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-439">It is convenient toocopy this python code over tooa new cell in hello IPython notebook.</span></span>

<span data-ttu-id="3e068-440">Aqui, mostramos um segmento de código python com chave de API Olá correto.</span><span class="sxs-lookup"><span data-stu-id="3e068-440">Here we show a segment of python code with hello correct API key.</span></span>

![Código Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="3e068-442">Observe que substituímos chave de API saudação padrão com a chave de API do nosso webservices.</span><span class="sxs-lookup"><span data-stu-id="3e068-442">Note that we replaced hello default API key with our webservices's API key.</span></span> <span data-ttu-id="3e068-443">Clicando em **executar** nessa célula em uma IPython notebook gera Olá resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e068-443">Clicking **Run** on this cell in an IPython notebook yields hello following response:</span></span>

![Resposta do IPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="3e068-445">Podemos ver para Olá dois teste exemplos que perguntamos (na estrutura JSON de saudação do script de python Olá), obtemos respostas na forma de hello "Classificado rótulos, classificado probabilidades".</span><span class="sxs-lookup"><span data-stu-id="3e068-445">We see that for hello two test examples we asked about (in hello JSON framework of hello python script), we get back answers in hello form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="3e068-446">Observe que nesse caso, escolhemos valores padrão de saudação código pré-configurado Olá fornece (0 para todas as colunas numéricas e de cadeia de caracteres hello "value" para todas as colunas categóricas).</span><span class="sxs-lookup"><span data-stu-id="3e068-446">Note that in this case, we chose hello default values that hello pre-canned code provides (0's for all numeric columns and hello string "value" for all categorical columns).</span></span>

<span data-ttu-id="3e068-447">Isso conclui nosso mostrando passo a passo de ponta a ponta como toohandle conjunto de dados em larga escala usando o aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e068-447">This concludes our end-to-end walkthrough showing how toohandle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="3e068-448">Começamos com um terabyte de dados, criado um modelo de previsão e implantá-lo como um serviço web na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="3e068-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in hello cloud.</span></span>

