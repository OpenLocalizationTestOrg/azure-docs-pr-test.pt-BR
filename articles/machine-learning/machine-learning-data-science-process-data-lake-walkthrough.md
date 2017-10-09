---
title: "Ciência de Dados Escalonáveis com o Azure Data Lake: um passo a passo de ponta a ponta | Microsoft Docs"
description: "Como as tarefas toouse Azure Data Lake toodo binários e exploração a classificação de dados em um conjunto de dados."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="5bfff-103">Ciência de Dados Escalonáveis com o Azure Data Lake: um passo a passo de ponta a ponta</span><span class="sxs-lookup"><span data-stu-id="5bfff-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="5bfff-104">Este passo a passo mostra como a exploração de dados do Azure Data Lake toodo toouse e tarefas de classificação binária em uma amostra de saudação NYC táxi viagem e passagens toopredict de conjunto de dados ou não uma dica será paga por uma tarifa.</span><span class="sxs-lookup"><span data-stu-id="5bfff-104">This walkthrough shows how toouse Azure Data Lake toodo data exploration and binary classification tasks on a sample of hello NYC taxi trip and fare dataset toopredict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="5bfff-105">Lhe orienta pelas etapas de saudação do hello [processo de ciência de dados de equipe](http://aka.ms/datascienceprocess)fim a fim de treinamento de toomodel de aquisição de dados e, em seguida, a implantação de toohello de um serviço web que publica o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bfff-105">It walks you through hello steps of hello [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition toomodel training, and then toohello deployment of a web service that publishes hello model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="5bfff-106">Análise Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="5bfff-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="5bfff-107">Olá [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) tem todos os toomake necessários recursos de hello mais fácil cientistas toostore de dados de qualquer processamento de dados de tamanho, forma e velocidade e tooconduct, avançados de análise e modelagem de aprendizado de máquina com alta escalabilidade de maneira econômica.</span><span class="sxs-lookup"><span data-stu-id="5bfff-107">hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all hello capabilities required toomake it easy for data scientists toostore data of any size, shape and speed, and tooconduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="5bfff-108">Você paga por trabalho, somente quando os dados estão realmente sendo processados.</span><span class="sxs-lookup"><span data-stu-id="5bfff-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="5bfff-109">Análise do Azure Data Lake inclui U-SQL, uma linguagem Geométrico Olá natureza declarativa do SQL com poder expressivo de saudação do c# tooprovide escalonável distribuído funcionalidade de consulta.</span><span class="sxs-lookup"><span data-stu-id="5bfff-109">Azure Data Lake Analytics includes U-SQL, a language that blends hello declarative nature of SQL with hello expressive power of C# tooprovide scalable distributed query capability.</span></span> <span data-ttu-id="5bfff-110">Ele permite tooprocess de dados não estruturados, aplicando o esquema na leitura, inserção lógica personalizada e definida pelo usuário (UDFs) de funções e inclui extensibilidade tooenable um controle refinado sobre como tooexecute em escala.</span><span class="sxs-lookup"><span data-stu-id="5bfff-110">It enables you tooprocess unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility tooenable fine grained control over how tooexecute at scale.</span></span> <span data-ttu-id="5bfff-111">toolearn mais sobre filosofia de design Olá atrás U-SQL, consulte [postagem de blog do Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="5bfff-111">toolearn more about hello design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="5bfff-112">A Análise Data Lake também é um componente importante do Cortana Analytics Suite e funciona com o Azure SQL Data Warehouse, Power BI e Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5bfff-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="5bfff-113">Isso fornece uma plataforma de nuvem completa de análise avançada e big data.</span><span class="sxs-lookup"><span data-stu-id="5bfff-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="5bfff-114">Este passo a passo começa descrevendo os pré-requisitos de saudação e recursos que são necessários toocomplete Olá tarefas com análise Data Lake que formam o processo de ciência de dados hello e como tooinstall-los.</span><span class="sxs-lookup"><span data-stu-id="5bfff-114">This walkthrough begins by describing hello prerequisites and resources that are needed toocomplete hello tasks with Data Lake Analytics that form hello data science process and how tooinstall them.</span></span> <span data-ttu-id="5bfff-115">Descreve as etapas de processamento de dados hello usando U-SQL e conclui mostrando como toouse Python e seção com toobuild estúdio de aprendizado de máquina do Azure e implantar modelos de previsão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bfff-115">Then it outlines hello data processing steps using U-SQL and concludes by showing how toouse Python and Hive with Azure Machine Learning Studio toobuild and deploy hello predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="5bfff-116">U-SQL e Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5bfff-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="5bfff-117">Este passo a passo recomenda o uso do conjunto de dados do Visual Studio tooedit U-SQL scripts tooprocess hello.</span><span class="sxs-lookup"><span data-stu-id="5bfff-117">This walkthrough recommends using Visual Studio tooedit U-SQL scripts tooprocess hello dataset.</span></span> <span data-ttu-id="5bfff-118">scripts de U-SQL de saudação são descritas aqui e fornecidos em um arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="5bfff-118">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="5bfff-119">processo de saudação inclui ingestão, explorar e Olá dados de amostragem.</span><span class="sxs-lookup"><span data-stu-id="5bfff-119">hello process includes ingesting, exploring, and sampling hello data.</span></span> <span data-ttu-id="5bfff-120">Ele também mostra como toorun um U-SQL script trabalho da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfff-120">It also shows how toorun a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="5bfff-121">Tabelas de hive são criadas para dados de saudação em um associado construção do HDInsight cluster toofacilitate hello e a implantação de um modelo de classificação binária no estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfff-121">Hive tables are created for hello data in an associated HDInsight cluster toofacilitate hello building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="5bfff-122">Python</span><span class="sxs-lookup"><span data-stu-id="5bfff-122">Python</span></span>
<span data-ttu-id="5bfff-123">Este passo a passo também contém uma seção que mostra como toobuild e implantar um modelo de previsão usando Python com estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfff-123">This walkthrough also contains a section that shows how toobuild and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="5bfff-124">Fornecemos um bloco de anotações do Jupyter com scripts de Python Olá para essas etapas neste processo.</span><span class="sxs-lookup"><span data-stu-id="5bfff-124">We provide a Jupyter notebook with hello Python scripts for these steps in this process.</span></span> <span data-ttu-id="5bfff-125">bloco de anotações de saudação inclui código para algumas etapas de engenharia de recurso adicional e a construção de modelos, como classificação multiclasse e modelo de classificação binária toohello descrito aqui além de modelagem de regressão.</span><span class="sxs-lookup"><span data-stu-id="5bfff-125">hello notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition toohello binary classification model outlined here.</span></span> <span data-ttu-id="5bfff-126">tarefa de regressão de saudação é toopredict Olá Olá dica com base em outros recursos de dica.</span><span class="sxs-lookup"><span data-stu-id="5bfff-126">hello regression task is toopredict hello amount of hello tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="5bfff-127">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5bfff-127">Azure Machine Learning</span></span>
<span data-ttu-id="5bfff-128">Estúdio de aprendizado de máquina do Azure é usado toobuild e implantar modelos de previsão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bfff-128">Azure Machine Learning Studio is used toobuild and deploy hello predictive models.</span></span> <span data-ttu-id="5bfff-129">Isso é feito usando duas abordagens: primeiro com scripts de Python e, em seguida, tabelas de Hive em um cluster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="5bfff-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="5bfff-130">Scripts</span><span class="sxs-lookup"><span data-stu-id="5bfff-130">Scripts</span></span>
<span data-ttu-id="5bfff-131">Somente as principais etapas de hello são descritas neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="5bfff-131">Only hello principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="5bfff-132">Você pode baixar Olá completo **script U-SQL** e **Jupyter Notebook** de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="5bfff-132">You can download hello full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bfff-133">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5bfff-133">Prerequisites</span></span>
<span data-ttu-id="5bfff-134">Antes de começar estes tópicos, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="5bfff-134">Before you begin these topics, you must have hello following:</span></span>

* <span data-ttu-id="5bfff-135">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfff-135">An Azure subscription.</span></span> <span data-ttu-id="5bfff-136">Se ainda não tiver uma, veja [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5bfff-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="5bfff-137">[Recomendado] Visual Studio 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5bfff-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="5bfff-138">Se ainda não tiver uma dessas versões instaladas, você poderá baixar uma versão Community gratuita da [Comunidade do Visual Studio](https://www.visualstudio.com/vs/community/).</span><span class="sxs-lookup"><span data-stu-id="5bfff-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="5bfff-139">Em vez do Visual Studio, você também pode usar consultas do hello Azure Portal toosubmit Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5bfff-139">Instead of Visual Studio, you can also use hello Azure Portal toosubmit Azure Data Lake queries.</span></span> <span data-ttu-id="5bfff-140">Podemos fornecerão instruções sobre como toodo então com o Visual Studio e no portal de saudação na seção Olá intitulada **processar dados com U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="5bfff-140">We will provide instructions on how toodo so both with Visual Studio and on hello portal in hello section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="5bfff-141">Preparar ambiente de ciência de dados para o Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="5bfff-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="5bfff-142">ambiente de ciência de dados tooprepare Olá para este passo a passo, crie Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5bfff-142">tooprepare hello data science environment for this walkthrough, create hello following resources:</span></span>

* <span data-ttu-id="5bfff-143">ADLS (Repositório Azure Data Lake)</span><span class="sxs-lookup"><span data-stu-id="5bfff-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="5bfff-144">ADLA (Análise Azure Data Lake)</span><span class="sxs-lookup"><span data-stu-id="5bfff-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="5bfff-145">Conta de armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="5bfff-145">Azure Blob storage account</span></span>
* <span data-ttu-id="5bfff-146">Conta do Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5bfff-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="5bfff-147">Ferramentas do Azure Data Lake para Visual Studio (Recomendado)</span><span class="sxs-lookup"><span data-stu-id="5bfff-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="5bfff-148">Esta seção fornece instruções sobre como toocreate desses recursos.</span><span class="sxs-lookup"><span data-stu-id="5bfff-148">This section provides instructions on how toocreate each of these resources.</span></span> <span data-ttu-id="5bfff-149">Se você escolher toouse tabelas de Hive com o aprendizado de máquina do Azure, em vez de Python, toobuild um modelo, você também precisará tooprovision um cluster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="5bfff-149">If you choose toouse Hive tables with Azure Machine Learning, instead of Python, toobuild a model,you will also need tooprovision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="5bfff-150">Esse procedimento alternativo descrito na seção de apropriada de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="5bfff-150">This alternative procedure in described in hello appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="5bfff-151">Olá **repositório Azure Data Lake** podem ser criadas separadamente ou quando você cria Olá **análise Azure Data Lake** como armazenamento de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bfff-151">hello **Azure Data Lake Store** can be created either separately or when you create hello **Azure Data Lake Analytics** as hello default storage.</span></span> <span data-ttu-id="5bfff-152">As instruções são referenciadas para a criação de cada um desses recursos separadamente, a seguir, mas Olá conta de armazenamento do Data Lake não precisa ser criado separadamente.</span><span class="sxs-lookup"><span data-stu-id="5bfff-152">Instructions are referenced for creating each of these resources separately below, but hello Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="5bfff-153">Criar um Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="5bfff-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="5bfff-154">Criar um ADLS de saudação [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5bfff-154">Create an ADLS from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="5bfff-155">Para obter detalhes, consulte [Criar um cluster HDInsight com o Repositório Data Lake usando o Portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5bfff-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="5bfff-156">Ser tooset-se de que a saudação Cluster AAD identidade no hello **DataSource** folha de saudação **configuração opcional** folha descrita lá.</span><span class="sxs-lookup"><span data-stu-id="5bfff-156">Be sure tooset up hello Cluster AAD Identity in hello **DataSource** blade of hello **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="5bfff-158">Criar uma conta da Análise Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="5bfff-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="5bfff-159">Criar uma conta ADLA de saudação [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5bfff-159">Create an ADLA account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="5bfff-160">Para obter detalhes, consulte [Tutorial: introdução à Análise Azure Data Lake usando o Portal do Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5bfff-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="5bfff-162">Criar uma conta de Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="5bfff-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="5bfff-163">Criar uma conta de armazenamento de BLOBs do Azure de saudação [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5bfff-163">Create an Azure Blob storage account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="5bfff-164">Para obter detalhes, consulte Olá criar uma conta de armazenamento seção [contas de armazenamento do Azure sobre](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5bfff-164">For details, see hello Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="5bfff-166">Configurar uma conta do Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5bfff-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="5bfff-167">Inscrever-se/no estúdio de aprendizado de máquina do Azure de saudação [aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) página.</span><span class="sxs-lookup"><span data-stu-id="5bfff-167">Sign up/into Azure Machine Learning Studio from hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="5bfff-168">Clique em Olá **comece agora** botão e, em seguida, escolha um "Espaço livre" ou "Espaço de trabalho padrão".</span><span class="sxs-lookup"><span data-stu-id="5bfff-168">Click on hello **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="5bfff-169">Depois disso será capaz de toocreate experiências no Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="5bfff-169">After this you will be able toocreate experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="5bfff-170">Instalar Ferramentas do Azure Data Lake [Recomendado]</span><span class="sxs-lookup"><span data-stu-id="5bfff-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="5bfff-171">Instale as Ferramentas do Azure Data Lake para sua versão do Visual Studio das [Ferramentas do Azure Data Lake para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="5bfff-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="5bfff-173">Após a conclusão bem-sucedida da instalação hello, abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5bfff-173">After hello installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="5bfff-174">Você deve ver o menu de saudação do hello Data Lake guia na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5bfff-174">You should see hello Data Lake tab hello menu at hello top.</span></span> <span data-ttu-id="5bfff-175">Os recursos do Azure devem aparecer no painel esquerdo do hello quando você entrar com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfff-175">Your Azure resources should appear in hello left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a><span data-ttu-id="5bfff-177">Olá NYC táxi viagens dataset</span><span class="sxs-lookup"><span data-stu-id="5bfff-177">hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="5bfff-178">Olá conjunto de dados são usados aqui é um conjunto de dados disponível publicamente – hello [NYC táxi viagens dataset](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="5bfff-178">hello data set we used here is a publicly available dataset -- hello [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="5bfff-179">Olá dados NYC táxi Trip consiste em cerca de 20GB de arquivos compactados de CSV (~ 48GB descompactado), registrar mais de milhões de 173 hello e viagens individuais é pago para cada viagem.</span><span class="sxs-lookup"><span data-stu-id="5bfff-179">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="5bfff-180">Cada registro de viagem inclui locais de retirada e redistribuição hello e vezes, anônimas invadir o número de licença (do driver) e Olá número medallion (id exclusiva do táxi).</span><span class="sxs-lookup"><span data-stu-id="5bfff-180">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="5bfff-181">dados saudação abrange todas as viagens no ano Olá 2013 e são fornecidos em dois conjuntos de dados a seguir para cada mês de saudação:</span><span class="sxs-lookup"><span data-stu-id="5bfff-181">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

* <span data-ttu-id="5bfff-182">Olá 'trip_data' CSV contém detalhes da visita, como o número de passageiros, coleta e pontos de redução, duração da viagem e comprimento de viagem.</span><span class="sxs-lookup"><span data-stu-id="5bfff-182">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="5bfff-183">Aqui estão alguns exemplos de registros:</span><span class="sxs-lookup"><span data-stu-id="5bfff-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="5bfff-184">Olá 'trip_fare' CSV contém detalhes de passagens Olá pagado para cada viagem, como tipo de pagamento, quantidade de passagens, sobretaxa e impostos, dicas e pedágio e quantidade total de saudação paga.</span><span class="sxs-lookup"><span data-stu-id="5bfff-184">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="5bfff-185">Aqui estão alguns exemplos de registros:</span><span class="sxs-lookup"><span data-stu-id="5bfff-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="5bfff-186">viagem de toojoin de chave exclusivo Olá\_dados e viagem\_passagens é composta de saudação três campos a seguir: medallion, ataques\_licença e retirada\_datetime.</span><span class="sxs-lookup"><span data-stu-id="5bfff-186">hello unique key toojoin trip\_data and trip\_fare is composed of hello following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="5bfff-187">os arquivos CSV raw Olá podem ser acessados de um blob de armazenamento do Azure públicos.</span><span class="sxs-lookup"><span data-stu-id="5bfff-187">hello raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="5bfff-188">Olá script U-SQL para essa junção está em Olá [associar tabelas viagem e passagens](#join) seção.</span><span class="sxs-lookup"><span data-stu-id="5bfff-188">hello U-SQL script for this join is in hello [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="5bfff-189">Processar dados com o U-SQL</span><span class="sxs-lookup"><span data-stu-id="5bfff-189">Process data with U-SQL</span></span>
<span data-ttu-id="5bfff-190">as tarefas de processamento de dados de Olá ilustradas nesta seção incluem ingestão, verificando a qualidade, explorar e Olá dados de amostragem.</span><span class="sxs-lookup"><span data-stu-id="5bfff-190">hello data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling hello data.</span></span> <span data-ttu-id="5bfff-191">Também mostramos como tabelas de viagem e passagens toojoin.</span><span class="sxs-lookup"><span data-stu-id="5bfff-191">We also show how toojoin trip and fare tables.</span></span> <span data-ttu-id="5bfff-192">seção final Olá mostra executar um trabalho com script U-SQL de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfff-192">hello final section shows run a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="5bfff-193">Estes são links tooeach subseção:</span><span class="sxs-lookup"><span data-stu-id="5bfff-193">Here are links tooeach subsection:</span></span>

* [<span data-ttu-id="5bfff-194">Ingestão de dados: dados de leitura de blob público</span><span class="sxs-lookup"><span data-stu-id="5bfff-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="5bfff-195">Verificações de qualidade de dados</span><span class="sxs-lookup"><span data-stu-id="5bfff-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="5bfff-196">Exploração de dados</span><span class="sxs-lookup"><span data-stu-id="5bfff-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="5bfff-197">Unir tabelas de corrida e tarifa</span><span class="sxs-lookup"><span data-stu-id="5bfff-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="5bfff-198">Amostragem de dados</span><span class="sxs-lookup"><span data-stu-id="5bfff-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="5bfff-199">Executar trabalhos com U-SQL</span><span class="sxs-lookup"><span data-stu-id="5bfff-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="5bfff-200">scripts de U-SQL de saudação são descritas aqui e fornecidos em um arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="5bfff-200">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="5bfff-201">Você pode baixar Olá completo **scripts U-SQL** de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="5bfff-201">You can download hello full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="5bfff-202">tooexecute U-SQL, abra o Visual Studio, clique em **arquivo--> Novo--> projeto**, escolha **U-SQL projeto**, nome e salvá-lo tooa pasta.</span><span class="sxs-lookup"><span data-stu-id="5bfff-202">tooexecute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it tooa folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="5bfff-204">É possível toouse hello Azure Portal tooexecute U-SQL em vez do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5bfff-204">It is possible toouse hello Azure Portal tooexecute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="5bfff-205">Você pode navegar recursos de análise do Azure Data Lake toohello no portal de saudação e enviar consultas diretamente, como ilustrado na figura a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bfff-205">You can navigate toohello Azure Data Lake Analytics resource on hello portal and submit queries directly as illustrated in hello following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="5bfff-207"><a name="ingest"></a>Ingestão de dados: dados de leitura de blob público</span><span class="sxs-lookup"><span data-stu-id="5bfff-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="5bfff-208">local de Olá de dados Olá Olá BLOBs do Azure é referenciada como  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  e podem ser extraídos usando **Extractors.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="5bfff-208">hello location of hello data in hello Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="5bfff-209">Substituir seu próprio nome de contêiner e o nome da conta de armazenamento em scripts a seguir para container_name@blob_storage_account_name no endereço de wasb hello.</span><span class="sxs-lookup"><span data-stu-id="5bfff-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in hello wasb address.</span></span> <span data-ttu-id="5bfff-210">Como os nomes de arquivo hello estão no mesmo formato, podemos usar **viagem\_data_ {\*\}. csv** tooread em todos os arquivos de viagem 12.</span><span class="sxs-lookup"><span data-stu-id="5bfff-210">Since hello file names are in same format, we can use **trip\_data_{\*\}.csv** tooread in all 12 trip files.</span></span> 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

<span data-ttu-id="5bfff-211">Como há cabeçalhos na primeira linha de saudação, precisamos cabeçalhos de saudação tooremove e alterar os tipos de coluna para as apropriadas.</span><span class="sxs-lookup"><span data-stu-id="5bfff-211">Since there are headers in hello first row, we need tooremove hello headers and change column types into appropriate ones.</span></span> <span data-ttu-id="5bfff-212">Podemos salvar Olá processado dados tooAzure Data Lake armazenamento usando **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ ou tooAzure armazenamento de Blob de conta usando  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** .</span><span class="sxs-lookup"><span data-stu-id="5bfff-212">We can either save hello processed data tooAzure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or tooAzure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="5bfff-213">Da mesma forma, pode ler em conjuntos de dados de passagens hello.</span><span class="sxs-lookup"><span data-stu-id="5bfff-213">Similarly we can read in hello fare data sets.</span></span> <span data-ttu-id="5bfff-214">Clique com botão direito repositório Azure Data Lake, você pode escolher toolook de seus dados nos **Portal do Azure--> Data Explorer** ou **Explorador de arquivos** dentro do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5bfff-214">Right click Azure Data Lake Store, you can choose toolook at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="5bfff-217"><a name="quality"></a>Verificações de qualidade de dados</span><span class="sxs-lookup"><span data-stu-id="5bfff-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="5bfff-218">Depois de viagem e passagens tabelas tenham sido lidos em, verificações de qualidade de dados podem ser feitas em Olá maneira a seguir.</span><span class="sxs-lookup"><span data-stu-id="5bfff-218">After trip and fare tables have been read in, data quality checks can be done in hello following way.</span></span> <span data-ttu-id="5bfff-219">Olá resultante arquivos CSV pode ser o armazenamento de Blob tooAzure saída ou repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5bfff-219">hello resulting CSV files can be output tooAzure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="5bfff-220">Localize o número de saudação do medallions e um número exclusivo de medallions:</span><span class="sxs-lookup"><span data-stu-id="5bfff-220">Find hello number of medallions and unique number of medallions:</span></span>

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="5bfff-221">Localize os medalhões com mais de 100 corridas:</span><span class="sxs-lookup"><span data-stu-id="5bfff-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="5bfff-222">Localize esses registros inválidos em termos de pickup_longitude:</span><span class="sxs-lookup"><span data-stu-id="5bfff-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="5bfff-223">Encontre os valores ausentes para algumas variáveis:</span><span class="sxs-lookup"><span data-stu-id="5bfff-223">Find missing values for some variables:</span></span>

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="5bfff-224"><a name="explore"></a>Exploração de dados</span><span class="sxs-lookup"><span data-stu-id="5bfff-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="5bfff-225">Podemos fazer algumas tooget de exploração de dados uma melhor compreensão dos dados saudação.</span><span class="sxs-lookup"><span data-stu-id="5bfff-225">We can do some data exploration tooget a better understanding of hello data.</span></span>

<span data-ttu-id="5bfff-226">Localize a distribuição de saudação de Oblíquo e não-Oblíquo viagens de:</span><span class="sxs-lookup"><span data-stu-id="5bfff-226">Find hello distribution of tipped and non-tipped trips:</span></span>

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="5bfff-227">Localizar a distribuição de saudação do valor de dica com valores de corte: 0,5,10 e 20 dólares.</span><span class="sxs-lookup"><span data-stu-id="5bfff-227">Find hello distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="5bfff-228">Localize as estatísticas básicas de distância de corrida:</span><span class="sxs-lookup"><span data-stu-id="5bfff-228">Find basic statistics of trip distance:</span></span>

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="5bfff-229">Localize os percentuais de saudação de distância de viagem:</span><span class="sxs-lookup"><span data-stu-id="5bfff-229">Find hello percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="5bfff-230"><a name="join"></a>Unir tabelas de corrida e tarifa</span><span class="sxs-lookup"><span data-stu-id="5bfff-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="5bfff-231">Tabelas de corrida e tarifa podem ser unidas por medalhão, hack_license e pickup_time.</span><span class="sxs-lookup"><span data-stu-id="5bfff-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="5bfff-232">Para cada nível de contagem de passageiro, calcule o número de saudação de registros, quantidade média de ponta, variação do valor de dica, porcentagem de viagens oblíquo.</span><span class="sxs-lookup"><span data-stu-id="5bfff-232">For each level of passenger count, calculate hello number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="5bfff-233"><a name="sample"></a>Amostragem de dados</span><span class="sxs-lookup"><span data-stu-id="5bfff-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="5bfff-234">Primeiro aleatoriamente selecionamos 0,1% dos dados de saudação da tabela unida hello:</span><span class="sxs-lookup"><span data-stu-id="5bfff-234">First we randomly select 0.1% of hello data from hello joined table:</span></span>

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="5bfff-235">Em seguida, fazemos a amostragem estratificada pela variável binária tip_class:</span><span class="sxs-lookup"><span data-stu-id="5bfff-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="5bfff-236"><a name="run"></a>Executar trabalhos com U-SQL</span><span class="sxs-lookup"><span data-stu-id="5bfff-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="5bfff-237">Quando você terminar de editar scripts U-SQL, você pode enviá-los toohello servidor usando sua conta da análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5bfff-237">When you finish editing U-SQL scripts, you can submit them toohello server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="5bfff-238">Clique em **Data Lake**, **Enviar Trabalho**, selecione sua **Conta de Análise**, escolha **Paralelismo** e clique no botão **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="5bfff-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="5bfff-240">Quando o trabalho de saudação é compilado com êxito, status de saudação do seu trabalho será exibido no Visual Studio para monitoramento.</span><span class="sxs-lookup"><span data-stu-id="5bfff-240">When hello job is complied successfully, hello status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="5bfff-241">Após a execução do trabalho de saudação for concluída, você pode até mesmo Olá trabalho execução do processo de repetição e descobrir Olá afunilar etapas tooimprove a eficiência de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5bfff-241">After hello job finishes running, you can even replay hello job execution process and find out hello bottleneck steps tooimprove your job efficiency.</span></span> <span data-ttu-id="5bfff-242">Você também pode ir tooAzure status de saudação do Portal toocheck dos trabalhos U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5bfff-242">You can also go tooAzure Portal toocheck hello status of your U-SQL jobs.</span></span>

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="5bfff-245">Agora você pode verificar Olá arquivos de saída no armazenamento de BLOBs do Azure ou no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfff-245">Now you can check hello output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="5bfff-246">Usaremos os dados de exemplo hello estratificada para nosso modelagem na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="5bfff-246">We will use hello stratified sample data for our modeling in hello next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="5bfff-249">Compilar e implantar modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5bfff-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="5bfff-250">Demonstraremos duas opções disponíveis para seus dados toopull em toobuild de aprendizado de máquina do Azure e</span><span class="sxs-lookup"><span data-stu-id="5bfff-250">We demonstrate two options available for you toopull data into Azure Machine Learning toobuild and</span></span> 

* <span data-ttu-id="5bfff-251">Na opção de primeira hello, use os dados Olá amostrada gravou tooan BLOBs do Azure (em Olá **amostragem de dados** etapa acima) e usar o Python toobuild e implantar modelos de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfff-251">In hello first option, you use hello sampled data that has been written tooan Azure Blob (in hello **Data sampling** step above) and use Python toobuild and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="5bfff-252">Na segunda opção de saudação, você consulta dados de saudação em Azure Data Lake diretamente usando uma consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="5bfff-252">In hello second option, you query hello data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="5bfff-253">Essa opção requer que você crie um novo cluster HDInsight ou usa um cluster HDInsight existente onde Olá Hive tabelas toohello de ponto de dados de táxi NY no armazenamento do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5bfff-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where hello Hive tables point toohello NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="5bfff-254">Discutiremos ambas as opções abaixo.</span><span class="sxs-lookup"><span data-stu-id="5bfff-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a><span data-ttu-id="5bfff-255">Opção 1: Use Python toobuild e implantar modelos de aprendizado de máquina</span><span class="sxs-lookup"><span data-stu-id="5bfff-255">Option 1: Use Python toobuild and deploy machine learning models</span></span>
<span data-ttu-id="5bfff-256">toobuild e implantar modelos de aprendizado de máquina usando o Python, crie um bloco de anotações do Jupyter em seu computador local ou no estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfff-256">toobuild and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="5bfff-257">Olá Jupyter Notebook fornecido em [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contém Olá tooexplore de código completo, visualizar dados, engenharia de recurso, modelagem e implantação.</span><span class="sxs-lookup"><span data-stu-id="5bfff-257">hello Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains hello full code tooexplore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="5bfff-258">Neste artigo, mostramos apenas a modelagem de saudação e a implantação.</span><span class="sxs-lookup"><span data-stu-id="5bfff-258">In this article, we show just hello modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="5bfff-259">Importar bibliotecas Python</span><span class="sxs-lookup"><span data-stu-id="5bfff-259">Import Python libraries</span></span>
<span data-ttu-id="5bfff-260">Na saudação de toorun de ordem de exemplo de anotações do Jupyter ou Olá o arquivo de script de Python, hello pacotes Python a seguir são necessários.</span><span class="sxs-lookup"><span data-stu-id="5bfff-260">In order toorun hello sample Jupyter Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="5bfff-261">Se você estiver usando Olá serviço AzureML Notebook, esses pacotes foram pré-instalados.</span><span class="sxs-lookup"><span data-stu-id="5bfff-261">If you are using hello AzureML Notebook service, these packages have been pre-installed.</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a><span data-ttu-id="5bfff-262">Ler dados de saudação do blob</span><span class="sxs-lookup"><span data-stu-id="5bfff-262">Read in hello data from blob</span></span>
* <span data-ttu-id="5bfff-263">Cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="5bfff-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="5bfff-264">Ler como texto</span><span class="sxs-lookup"><span data-stu-id="5bfff-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="5bfff-266">Adicionar nomes de colunas e separar colunas</span><span class="sxs-lookup"><span data-stu-id="5bfff-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="5bfff-267">Alterar toonumeric algumas colunas</span><span class="sxs-lookup"><span data-stu-id="5bfff-267">Change some columns toonumeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="5bfff-268">Compilar modelos de aprendizado de máquina</span><span class="sxs-lookup"><span data-stu-id="5bfff-268">Build machine learning models</span></span>
<span data-ttu-id="5bfff-269">Aqui criamos uma toopredict do modelo de classificação binária, se uma viagem-Oblíquo ou não.</span><span class="sxs-lookup"><span data-stu-id="5bfff-269">Here we build a binary classification model toopredict whether a trip is tipped or not.</span></span> <span data-ttu-id="5bfff-270">Saudação de anotações do Jupyter, você encontrará outros dois modelos: classificação multiclasse e modelos de regressão.</span><span class="sxs-lookup"><span data-stu-id="5bfff-270">In hello Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="5bfff-271">Primeiro, precisamos toocreate variáveis fictício que podem ser usados em scikit-Saiba modelos</span><span class="sxs-lookup"><span data-stu-id="5bfff-271">First we need toocreate dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="5bfff-272">Criar um quadro de dados para modelagem de saudação</span><span class="sxs-lookup"><span data-stu-id="5bfff-272">Create data frame for hello modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="5bfff-273">Divisão 60-40 entre treinamento e teste</span><span class="sxs-lookup"><span data-stu-id="5bfff-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="5bfff-274">Regressão logística no conjunto de treinamento</span><span class="sxs-lookup"><span data-stu-id="5bfff-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="5bfff-275">Conjunto de dados de testes de pontuação</span><span class="sxs-lookup"><span data-stu-id="5bfff-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="5bfff-276">Calcular métricas de Avaliação</span><span class="sxs-lookup"><span data-stu-id="5bfff-276">Calculate Evaluation metrics</span></span>
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="5bfff-277">Compilar a API do Serviço Web e consumi-la no Python</span><span class="sxs-lookup"><span data-stu-id="5bfff-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="5bfff-278">Queremos que a máquina de saudação toooperationalize aprender o modelo depois que ele foi criado.</span><span class="sxs-lookup"><span data-stu-id="5bfff-278">We want toooperationalize hello machine learning model after it has been built.</span></span> <span data-ttu-id="5bfff-279">Aqui usamos o modelo de logística binário hello como um exemplo.</span><span class="sxs-lookup"><span data-stu-id="5bfff-279">Here we use hello binary logistic model as an example.</span></span> <span data-ttu-id="5bfff-280">Certifique-se de que scikit de saudação-saber a versão em sua máquina local é 0.15.1.</span><span class="sxs-lookup"><span data-stu-id="5bfff-280">Make sure hello scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="5bfff-281">Você não tem tooworry sobre isso, se você usar o serviço do Azure ML studio.</span><span class="sxs-lookup"><span data-stu-id="5bfff-281">You don't have tooworry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="5bfff-282">Localize suas credenciais do espaço de trabalho nas configurações do Estúdio AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfff-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="5bfff-283">No Azure Machine Learning Studio, clique em **Configurações** --> **Nome** --> **Tokens de Autorização**.</span><span class="sxs-lookup"><span data-stu-id="5bfff-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="5bfff-285">Criar um Serviço Web</span><span class="sxs-lookup"><span data-stu-id="5bfff-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="5bfff-286">Obter as credenciais do serviço Web</span><span class="sxs-lookup"><span data-stu-id="5bfff-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="5bfff-287">Chame a API do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="5bfff-287">Call Web service API.</span></span> <span data-ttu-id="5bfff-288">Você tem toowait 5 a 10 segundos após a etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="5bfff-288">You have toowait 5-10 seconds after hello previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="5bfff-289">Opção 2: criar e implantar modelos diretamente no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5bfff-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="5bfff-290">Estúdio de aprendizado de máquina do Azure pode ler dados diretamente do repositório Azure Data Lake e, em seguida, ser toocreate usado e implantar modelos.</span><span class="sxs-lookup"><span data-stu-id="5bfff-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used toocreate and deploy models.</span></span> <span data-ttu-id="5bfff-291">Essa abordagem usa uma tabela de Hive que aponta em Olá repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5bfff-291">This approach uses a Hive table that points at hello Azure Data Lake Store.</span></span> <span data-ttu-id="5bfff-292">Isso requer que um cluster Azure HDInsight separado ser provisionado, no qual Olá Hive tabela é criada.</span><span class="sxs-lookup"><span data-stu-id="5bfff-292">This requires that a separate Azure HDInsight cluster be provisioned, on which hello Hive table is created.</span></span> <span data-ttu-id="5bfff-293">Olá Mostrar seções a seguir como toodo isso.</span><span class="sxs-lookup"><span data-stu-id="5bfff-293">hello following sections show how toodo this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="5bfff-294">Criar um Cluster HDInsight em Linux</span><span class="sxs-lookup"><span data-stu-id="5bfff-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="5bfff-295">Criar um HDInsight Cluster (Linux) de saudação [Portal do Azure](http://portal.azure.com). Para obter detalhes, consulte Olá **criar um cluster HDInsight com acesso tooAzure repositório Data Lake** seção [criar um cluster HDInsight com repositório Data Lake usando o Portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5bfff-295">Create an HDInsight Cluster (Linux) from hello [Azure Portal](http://portal.azure.com).For details, see hello **Create an HDInsight cluster with access tooAzure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="5bfff-297">Criar tabela de Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="5bfff-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="5bfff-298">Agora podemos criar Hive tabelas toobe usado no estúdio de aprendizado de máquina do Azure no cluster do HDInsight hello usando Olá dados armazenados no repositório Azure Data Lake na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="5bfff-298">Now we create Hive tables toobe used in Azure Machine Learning Studio in hello HDInsight cluster using hello data stored in Azure Data Lake Store in hello previous step.</span></span> <span data-ttu-id="5bfff-299">Vá toohello cluster HDInsight que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="5bfff-299">Go toohello HDInsight cluster just created.</span></span> <span data-ttu-id="5bfff-300">Clique em **configurações** --> **propriedades** --> **Cluster identidade AAD** --> **acesso ADLS**, Certifique-se de que sua conta do repositório Azure Data Lake é adicionada na lista de saudação com leitura, gravação e execução de direitos.</span><span class="sxs-lookup"><span data-stu-id="5bfff-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in hello list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="5bfff-302">Em seguida, clique em **painel** toohello próximo **configurações** botão e uma janela serão exibida.</span><span class="sxs-lookup"><span data-stu-id="5bfff-302">Then click **Dashboard** next toohello **Settings** button and a window will pop up.</span></span> <span data-ttu-id="5bfff-303">Clique em **exibição Hive** Olá canto superior direito da página hello e você verá Olá **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="5bfff-303">Click **Hive View** in hello upper right corner of hello page and you will see hello **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="5bfff-306">Cole Olá toocreate de scripts de Hive a seguir uma tabela.</span><span class="sxs-lookup"><span data-stu-id="5bfff-306">Paste in hello following Hive scripts toocreate a table.</span></span> <span data-ttu-id="5bfff-307">Olá local da fonte de dados é referência do repositório Azure Data Lake desta forma: **adl://data_lake_store_name.azuredatalakestore.net:443 nome_da_pasta/file_name**.</span><span class="sxs-lookup"><span data-stu-id="5bfff-307">hello location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


<span data-ttu-id="5bfff-308">Quando a execução da consulta de saudação for concluído, você verá resultados hello como este:</span><span class="sxs-lookup"><span data-stu-id="5bfff-308">When hello query finishes running, you will see hello results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="5bfff-310">Compilar e implantar modelos no Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5bfff-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="5bfff-311">Estamos agora toobuild pronto e implantar um modelo que prevê se ou não uma dica é pago com o aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfff-311">We are now ready toobuild and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="5bfff-312">dados de amostra estratificada Hello estão pronto toobe usado nesta classificação binária (dica ou não) problema.</span><span class="sxs-lookup"><span data-stu-id="5bfff-312">hello stratified sample data is ready toobe used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="5bfff-313">Olá modelos de previsão usando classificação multiclasse (tip_class) e regressão (tip_amount) também pode ser criado e implantado com o estúdio de aprendizado de máquina do Azure, mas aqui apenas mostramos como toohandle Olá caso usando Olá modelo de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="5bfff-313">hello predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how toohandle hello case using hello binary classification model.</span></span>

1. <span data-ttu-id="5bfff-314">Obter dados de saudação no Azure ML usando Olá **importar dados** módulo, disponível no hello **dados de entrada e saída** seção.</span><span class="sxs-lookup"><span data-stu-id="5bfff-314">Get hello data into Azure ML using hello **Import Data** module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="5bfff-315">Para obter mais informações, consulte Olá [módulo de importação de dados](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) página de referência.</span><span class="sxs-lookup"><span data-stu-id="5bfff-315">For more information, see hello [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="5bfff-316">Selecione **consulta de Hive** como Olá **fonte de dados** em Olá **propriedades** painel.</span><span class="sxs-lookup"><span data-stu-id="5bfff-316">Select **Hive Query** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="5bfff-317">Olá colar a seguir de script do Hive em Olá **consulta de banco de dados de Hive** editor</span><span class="sxs-lookup"><span data-stu-id="5bfff-317">Paste hello following Hive script in hello **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="5bfff-318">Insira o cluster do URI do HDInsight hello (Isso pode ser encontrado no Portal do Azure), as credenciais do Hadoop, local de dados de saída e o nome do contêiner/de chave de nome de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bfff-318">Enter hello URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="5bfff-320">Um exemplo de um experimento de classificação binária a leitura de dados da tabela de Hive é mostrado na figura de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="5bfff-320">An example of a binary classification experiment reading data from Hive table is shown in hello figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="5bfff-322">Depois de experiência de saudação é criada, clique em **configurar o serviço Web** --> **serviço Web de previsão**</span><span class="sxs-lookup"><span data-stu-id="5bfff-322">After hello experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="5bfff-324">Saudação de execução criada automaticamente pontuação experimento, quando ele for concluído, clique em **implantar o serviço da Web**</span><span class="sxs-lookup"><span data-stu-id="5bfff-324">Run hello automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="5bfff-326">Painel de saudação do serviço da web será exibida em breve:</span><span class="sxs-lookup"><span data-stu-id="5bfff-326">hello web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="5bfff-328">Resumo</span><span class="sxs-lookup"><span data-stu-id="5bfff-328">Summary</span></span>
<span data-ttu-id="5bfff-329">Ao executar esse passo a passo, você terá criado um ambiente de ciência de dados para compilar soluções de ponta a ponta escalonáveis no Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5bfff-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="5bfff-330">Esse ambiente foi usado tooanalyze público conjuntos de dados grandes, colocá-lo pelas etapas de Olá canônico de saudação processo de ciência de dados, da aquisição de dados por meio de treinamento do modelo, e, em seguida, toohello implantação de saudação modelo como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="5bfff-330">This environment was used tooanalyze a large public dataset, taking it through hello canonical steps of hello Data Science Process, from data acquisition through model training, and then toohello deployment of hello model as a web service.</span></span> <span data-ttu-id="5bfff-331">U-SQL foi usado tooprocess, explorar e Olá dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5bfff-331">U-SQL was used tooprocess, explore and sample hello data.</span></span> <span data-ttu-id="5bfff-332">Python e Hive foram usados com toobuild estúdio de aprendizado de máquina do Azure e implantar modelos de previsão.</span><span class="sxs-lookup"><span data-stu-id="5bfff-332">Python and Hive were used with Azure Machine Learning Studio toobuild and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="5bfff-333">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="5bfff-333">What's next?</span></span>
<span data-ttu-id="5bfff-334">saudação de aprendizado para o [processo de ciência de dados da equipe (TDSP)](http://aka.ms/datascienceprocess) fornece links tootopics que descrevem cada etapa em Olá avançado do processo de análise.</span><span class="sxs-lookup"><span data-stu-id="5bfff-334">hello learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links tootopics describing each step in hello advanced analytics process.</span></span> <span data-ttu-id="5bfff-335">Há uma série de instruções passo a passo detalhada em Olá [explicações passo a passo do processo de ciência de dados de equipe](data-science-process-walkthroughs.md) página que showcase como toouse recursos e serviços em vários cenários de análise de previsão:</span><span class="sxs-lookup"><span data-stu-id="5bfff-335">There are a series of walkthroughs itemized on hello [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how toouse resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="5bfff-336">Olá processo de ciência de dados de equipe em ação: usando o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5bfff-336">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="5bfff-337">Olá processo de ciência de dados de equipe em ação: usar clusters de HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="5bfff-337">hello Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="5bfff-338">Olá, equipe de processo de ciência de dados: usando o SQL Server</span><span class="sxs-lookup"><span data-stu-id="5bfff-338">hello Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="5bfff-339">Visão geral do uso do processo de ciência de dados de saudação despertar no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5bfff-339">Overview of hello Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

