---
title: "dados de aaaImport no estúdio de aprendizado de máquina | Microsoft Docs"
description: "Como tooimport seus dados no estúdio de aprendizado de máquina do Azure de várias fontes de dados. Saiba quais tipos e formatos de dados têm suporte."
keywords: importar dados, formato de dados, tipos de dados, fontes de dados, dados de treinamento
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="a2527-105">Importar os dados de treinamento para o Azure Machine Learning Studio de diferentes fontes de dados</span><span class="sxs-lookup"><span data-stu-id="a2527-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="a2527-106">toouse seus próprios dados no estúdio de aprendizado de máquina toodevelop e treinar uma solução de análise de previsão, você pode:</span><span class="sxs-lookup"><span data-stu-id="a2527-106">toouse your own data in Machine Learning Studio toodevelop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="a2527-107">carregar dados de um **arquivo local** depois do tempo de sua unidade de disco rígido toocreate um módulo de conjunto de dados no espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="a2527-107">upload data from a **local file** ahead of time from your hard drive toocreate a dataset module in your workspace</span></span>
* <span data-ttu-id="a2527-108">acessar dados de uma das várias **fontes de dados online** enquanto o teste está em execução usando Olá [importar dados] [ import-data] módulo</span><span class="sxs-lookup"><span data-stu-id="a2527-108">access data from one of several **online data sources** while your experiment is running using hello [Import Data][import-data] module</span></span> 
* <span data-ttu-id="a2527-109">usar dados de outro **teste** do Azure Machine Learning salvo como um conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="a2527-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="a2527-110">usar dados de um **banco de dados do SQL Server** local</span><span class="sxs-lookup"><span data-stu-id="a2527-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="a2527-111">Cada uma dessas opções é descrita em um dos tópicos de saudação no menu de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="a2527-111">Each of these options is described in one of hello topics on hello menu below.</span></span> <span data-ttu-id="a2527-112">Esses tópicos mostram como dados de tooimport desses dados de várias fontes toouse no estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="a2527-112">These topics show you how tooimport data from these various data sources toouse in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="a2527-113">Há diversos conjuntos de dados de exemplo disponíveis no Machine Learning Studio que você pode usar para treinamento de dados.</span><span class="sxs-lookup"><span data-stu-id="a2527-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="a2527-114">Para obter informações sobre estas configurações, consulte [usar conjuntos de dados de exemplo hello no estúdio de aprendizado de máquina do Azure](machine-learning-use-sample-datasets.md)).</span><span class="sxs-lookup"><span data-stu-id="a2527-114">For information on these, see [Use hello sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="a2527-115">Este tópico introdutório também discute como tooget dados prontos para usam no estúdio de aprendizado de máquina e descreve quais tipos de dados e formatos de dados têm suporte.</span><span class="sxs-lookup"><span data-stu-id="a2527-115">This introductory topic also discusses how tooget data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="a2527-116">Preparar dados para uso no Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="a2527-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="a2527-117">O estúdio de aprendizado de máquina é projetado toowork com dados retangulares ou de tabela, como dados de texto delimitados ou estruturado dados de um banco de dados, embora em algumas circunstâncias não retangulares dados podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="a2527-117">Machine Learning Studio is designed toowork with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="a2527-118">É melhor se os dados estiverem relativamente limpos.</span><span class="sxs-lookup"><span data-stu-id="a2527-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="a2527-119">Ou seja, você desejará tootake respeito problemas como cadeias de caracteres sem aspas antes de carregar dados saudação em sua experiência.</span><span class="sxs-lookup"><span data-stu-id="a2527-119">That is, you'll want tootake care of issues such as unquoted strings before you upload hello data into your experiment.</span></span>

<span data-ttu-id="a2527-120">No entanto, há módulos disponíveis no Machine Learning Studio que permitem fazer alguma manipulação de dados dentro do teste.</span><span class="sxs-lookup"><span data-stu-id="a2527-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="a2527-121">Dependendo de algoritmos de aprendizado de máquina Olá você está usando, talvez seja necessário toodecide como você vai lidar com problemas estruturais de dados, como valores ausentes e dados esparsos e há módulos que podem ajudar com isso.</span><span class="sxs-lookup"><span data-stu-id="a2527-121">Depending on hello machine learning algorithms you'll be using, you may need toodecide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="a2527-122">Examinar Olá **transformação de dados** seção da paleta de módulo Olá para módulos que executam essas funções.</span><span class="sxs-lookup"><span data-stu-id="a2527-122">Look in hello **Data Transformation** section of hello module palette for modules that perform these functions.</span></span>

<span data-ttu-id="a2527-123">A qualquer momento em sua experiência, você pode exibir ou baixar dados Olá produzido por um módulo clicando Olá porta de saída.</span><span class="sxs-lookup"><span data-stu-id="a2527-123">At any point in your experiment you can view or download hello data that's produced by a module by clicking hello output port.</span></span> <span data-ttu-id="a2527-124">Dependendo do módulo hello, pode haver download diferentes opções disponíveis ou pode ser capaz de toovisualize dados de saudação em seu navegador da web no estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="a2527-124">Depending on hello module, there may be different download options available, or you may be able toovisualize hello data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="a2527-125">Formatos e tipos de dados compatíveis</span><span class="sxs-lookup"><span data-stu-id="a2527-125">Data formats and data types supported</span></span>
<span data-ttu-id="a2527-126">Você pode importar uma variedade de tipos de dados para sua experiência, dependendo de qual mecanismo de você usar dados tooimport e onde ele está vindo:</span><span class="sxs-lookup"><span data-stu-id="a2527-126">You can import a number of data types into your experiment, depending on what mechanism you use tooimport data and where it's coming from:</span></span>

* <span data-ttu-id="a2527-127">Texto sem formatação (.txt)</span><span class="sxs-lookup"><span data-stu-id="a2527-127">Plain text (.txt)</span></span>
* <span data-ttu-id="a2527-128">Valores separados por vírgulas (CSV) com cabeçalho (.csv) ou sem (.nh.csv)</span><span class="sxs-lookup"><span data-stu-id="a2527-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="a2527-129">Valores separados por tabulação (TSV) com cabeçalho (.tsv) ou sem (.nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="a2527-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="a2527-130">Arquivo do Excel</span><span class="sxs-lookup"><span data-stu-id="a2527-130">Excel file</span></span>
* <span data-ttu-id="a2527-131">Tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="a2527-131">Azure table</span></span>
* <span data-ttu-id="a2527-132">Tabela do Hive</span><span class="sxs-lookup"><span data-stu-id="a2527-132">Hive table</span></span>
* <span data-ttu-id="a2527-133">Tabela de Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="a2527-133">SQL database table</span></span>
* <span data-ttu-id="a2527-134">Valores de OData</span><span class="sxs-lookup"><span data-stu-id="a2527-134">OData values</span></span>
* <span data-ttu-id="a2527-135">Dados de SVMLight (.svmlight) (consulte Olá [SVMLight definição](http://svmlight.joachims.org/) informações de formato)</span><span class="sxs-lookup"><span data-stu-id="a2527-135">SVMLight data (.svmlight) (see hello [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="a2527-136">Atributo de dados de formato de arquivo de relação (ARFF) (.arff) (consulte Olá [definição ARFF](http://weka.wikispaces.com/ARFF) informações de formato)</span><span class="sxs-lookup"><span data-stu-id="a2527-136">Attribute Relation File Format (ARFF) data (.arff) (see hello [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="a2527-137">Arquivo zip (.zip)</span><span class="sxs-lookup"><span data-stu-id="a2527-137">Zip file (.zip)</span></span>
* <span data-ttu-id="a2527-138">Arquivo de espaço de trabalho ou objeto R (.RData)</span><span class="sxs-lookup"><span data-stu-id="a2527-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="a2527-139">Se você importar dados em um formato como ARFF que contém metadados, o estúdio de aprendizado de máquina usa esse cabeçalho de saudação toodefine metadados e o tipo de dados de cada coluna.</span><span class="sxs-lookup"><span data-stu-id="a2527-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata toodefine hello heading and data type of each column.</span></span>

<span data-ttu-id="a2527-140">Se você importar dados, como o formato TSV ou CSV que não inclua esses metadados, estúdio de aprendizado de máquina infere Olá o tipo de dados para cada coluna por amostragem de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2527-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers hello data type for each column by sampling hello data.</span></span> <span data-ttu-id="a2527-141">Se dados saudação também não tem títulos de coluna, o estúdio de aprendizado de máquina fornece nomes padrão.</span><span class="sxs-lookup"><span data-stu-id="a2527-141">If hello data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="a2527-142">Você pode especificar explicitamente ou alterar Olá cabeçalhos e tipos de dados para colunas usando Olá [editar metadados][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="a2527-142">You can explicitly specify or change hello headings and data types for columns using hello [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="a2527-143">a seguir Olá **tipos de dados** reconhecidos pelo estúdio de aprendizado de máquina:</span><span class="sxs-lookup"><span data-stu-id="a2527-143">hello following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="a2527-144">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="a2527-144">String</span></span>
* <span data-ttu-id="a2527-145">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="a2527-145">Integer</span></span>
* <span data-ttu-id="a2527-146">Duplo</span><span class="sxs-lookup"><span data-stu-id="a2527-146">Double</span></span>
* <span data-ttu-id="a2527-147">Booliano</span><span class="sxs-lookup"><span data-stu-id="a2527-147">Boolean</span></span>
* <span data-ttu-id="a2527-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="a2527-148">DateTime</span></span>
* <span data-ttu-id="a2527-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a2527-149">TimeSpan</span></span>

<span data-ttu-id="a2527-150">O estúdio de aprendizado de máquina usa um tipo de dados interno chamado ***tabela de dados*** toopass dados entre os módulos.</span><span class="sxs-lookup"><span data-stu-id="a2527-150">Machine Learning Studio uses an internal data type called ***Data Table*** toopass data between modules.</span></span> <span data-ttu-id="a2527-151">Você pode converter explicitamente os dados em formato de tabela de dados usando Olá [converter tooDataset] [ convert-to-dataset] módulo.</span><span class="sxs-lookup"><span data-stu-id="a2527-151">You can explicitly convert your data into Data Table format using hello [Convert tooDataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="a2527-152">Qualquer módulo que aceita formatos diferentes de tabela de dados serão convertidos Olá dados tooData tabela silenciosamente antes de passá-lo toohello próximo módulo.</span><span class="sxs-lookup"><span data-stu-id="a2527-152">Any module that accepts formats other than Data Table will convert hello data tooData Table silently before passing it toohello next module.</span></span>

<span data-ttu-id="a2527-153">Se necessário, você pode converter o formato Data Table de volta para o formato CSV, TSV, ARFF ou SVMLight usando outros módulos de conversão.</span><span class="sxs-lookup"><span data-stu-id="a2527-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="a2527-154">Examinar Olá **conversões de formato de dados** seção da paleta de módulo Olá para módulos que executam essas funções.</span><span class="sxs-lookup"><span data-stu-id="a2527-154">Look in hello **Data Format Conversions** section of hello module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
