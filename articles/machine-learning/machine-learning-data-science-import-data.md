---
title: Importar dados para o Machine Learning Studio | Microsoft Docs
description: "Como importar os dados para o Azure Machine Learning Studio de diferentes fontes de dados. Saiba quais tipos e formatos de dados têm suporte."
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
ms.openlocfilehash: b92b480e62f4ce4f4836dc5d0f6afbe80c6b664a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="f903b-105">Importar os dados de treinamento para o Azure Machine Learning Studio de diferentes fontes de dados</span><span class="sxs-lookup"><span data-stu-id="f903b-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="f903b-106">Para usar seus próprios dados no Machine Learning Studio para desenvolver e treinar uma solução de análise preditiva, você pode:</span><span class="sxs-lookup"><span data-stu-id="f903b-106">To use your own data in Machine Learning Studio to develop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="f903b-107">carregar dados de um **arquivo local** antes do tempo por meio do disco rígido para criar um módulo de conjunto de dados no espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="f903b-107">upload data from a **local file** ahead of time from your hard drive to create a dataset module in your workspace</span></span>
* <span data-ttu-id="f903b-108">acessar dados de uma das várias **fontes de dados online** enquanto o teste é executado usando o módulo [Importar Dados][import-data]</span><span class="sxs-lookup"><span data-stu-id="f903b-108">access data from one of several **online data sources** while your experiment is running using the [Import Data][import-data] module</span></span> 
* <span data-ttu-id="f903b-109">usar dados de outro **teste** do Azure Machine Learning salvo como um conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="f903b-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="f903b-110">usar dados de um **banco de dados do SQL Server** local</span><span class="sxs-lookup"><span data-stu-id="f903b-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="f903b-111">Cada uma dessas opções são descritas em um dos tópicos no menu abaixo.</span><span class="sxs-lookup"><span data-stu-id="f903b-111">Each of these options is described in one of the topics on the menu below.</span></span> <span data-ttu-id="f903b-112">Esse tópicos mostram como importar dados de várias fontes de dados para usar no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f903b-112">These topics show you how to import data from these various data sources to use in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="f903b-113">Há diversos conjuntos de dados de exemplo disponíveis no Machine Learning Studio que você pode usar para treinamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f903b-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="f903b-114">Para obter informações, consulte [Usar os conjuntos de dados de amostra no Azure Machine Learning Studio](machine-learning-use-sample-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="f903b-114">For information on these, see [Use the sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="f903b-115">Este tópico introdutório também mostra como preparar dados para uso no Machine Learning Studio e descreve quais formatos e tipos de dados tem suporte.</span><span class="sxs-lookup"><span data-stu-id="f903b-115">This introductory topic also discusses how to get data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="f903b-116">Preparar dados para uso no Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f903b-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="f903b-117">O Machine Learning Studio foi criado para trabalhar com dados tabulares ou retangulares, como dados de texto delimitados ou dados estruturados de um banco de dados, embora em algumas circunstâncias seja possível usar dados não retangulares.</span><span class="sxs-lookup"><span data-stu-id="f903b-117">Machine Learning Studio is designed to work with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="f903b-118">É melhor se os dados estiverem relativamente limpos.</span><span class="sxs-lookup"><span data-stu-id="f903b-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="f903b-119">Ou seja, você deve cuidar de problemas como cadeias de caracteres sem aspas antes de carregar os dados para seu experimento.</span><span class="sxs-lookup"><span data-stu-id="f903b-119">That is, you'll want to take care of issues such as unquoted strings before you upload the data into your experiment.</span></span>

<span data-ttu-id="f903b-120">No entanto, há módulos disponíveis no Machine Learning Studio que permitem fazer alguma manipulação de dados dentro do teste.</span><span class="sxs-lookup"><span data-stu-id="f903b-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="f903b-121">Dependendo dos algoritmos de aprendizado de máquina que for usar, talvez seja necessário decidir como você lidará com problemas estruturais dos dados, como valores ausentes e dados esparsos, e há módulos que podem ajudar com isso.</span><span class="sxs-lookup"><span data-stu-id="f903b-121">Depending on the machine learning algorithms you'll be using, you may need to decide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="f903b-122">Veja a seção **Transformação de Dados** da paleta de módulos para ver os módulos que executam essas funções.</span><span class="sxs-lookup"><span data-stu-id="f903b-122">Look in the **Data Transformation** section of the module palette for modules that perform these functions.</span></span>

<span data-ttu-id="f903b-123">A qualquer momento do teste, é possível exibir ou baixar os dados produzidos por um módulo clicando na porta de saída.</span><span class="sxs-lookup"><span data-stu-id="f903b-123">At any point in your experiment you can view or download the data that's produced by a module by clicking the output port.</span></span> <span data-ttu-id="f903b-124">Dependendo do módulo, pode haver opções de download diferentes disponíveis ou a possibilidade de visualizar os dados no seu navegador da Web no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f903b-124">Depending on the module, there may be different download options available, or you may be able to visualize the data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="f903b-125">Formatos e tipos de dados compatíveis</span><span class="sxs-lookup"><span data-stu-id="f903b-125">Data formats and data types supported</span></span>
<span data-ttu-id="f903b-126">Você pode importar vários tipos de dados para seu experimento, dependendo de qual mecanismo usar para importar os dados e de onde eles estão vindo:</span><span class="sxs-lookup"><span data-stu-id="f903b-126">You can import a number of data types into your experiment, depending on what mechanism you use to import data and where it's coming from:</span></span>

* <span data-ttu-id="f903b-127">Texto sem formatação (.txt)</span><span class="sxs-lookup"><span data-stu-id="f903b-127">Plain text (.txt)</span></span>
* <span data-ttu-id="f903b-128">Valores separados por vírgulas (CSV) com cabeçalho (.csv) ou sem (.nh.csv)</span><span class="sxs-lookup"><span data-stu-id="f903b-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="f903b-129">Valores separados por tabulação (TSV) com cabeçalho (.tsv) ou sem (.nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="f903b-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="f903b-130">Arquivo do Excel</span><span class="sxs-lookup"><span data-stu-id="f903b-130">Excel file</span></span>
* <span data-ttu-id="f903b-131">Tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="f903b-131">Azure table</span></span>
* <span data-ttu-id="f903b-132">Tabela do Hive</span><span class="sxs-lookup"><span data-stu-id="f903b-132">Hive table</span></span>
* <span data-ttu-id="f903b-133">Tabela de Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="f903b-133">SQL database table</span></span>
* <span data-ttu-id="f903b-134">Valores de OData</span><span class="sxs-lookup"><span data-stu-id="f903b-134">OData values</span></span>
* <span data-ttu-id="f903b-135">Dados SVMLight (.svmlight) (consulte a [definição de SVMLight](http://svmlight.joachims.org/) para obter informações sobre o formato)</span><span class="sxs-lookup"><span data-stu-id="f903b-135">SVMLight data (.svmlight) (see the [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="f903b-136">Attribute Relation File Format (ARFF) (.arff) (consulte a [definição de ARFF](http://weka.wikispaces.com/ARFF) para obter informações sobre o formato)</span><span class="sxs-lookup"><span data-stu-id="f903b-136">Attribute Relation File Format (ARFF) data (.arff) (see the [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="f903b-137">Arquivo zip (.zip)</span><span class="sxs-lookup"><span data-stu-id="f903b-137">Zip file (.zip)</span></span>
* <span data-ttu-id="f903b-138">Arquivo de espaço de trabalho ou objeto R (.RData)</span><span class="sxs-lookup"><span data-stu-id="f903b-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="f903b-139">Se você importar dados em um formato como ARFF, que inclui metadados, o Machine Learning Studio usa esses metadados para definir o cabeçalho e o tipo de dados de cada coluna.</span><span class="sxs-lookup"><span data-stu-id="f903b-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata to define the heading and data type of each column.</span></span>

<span data-ttu-id="f903b-140">Se você importar dados em um formato como TSV ou CSV, que não incluem esses metadados, o Machine Learning Studio infere o tipo de dados de cada coluna por amostragem dos dados.</span><span class="sxs-lookup"><span data-stu-id="f903b-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers the data type for each column by sampling the data.</span></span> <span data-ttu-id="f903b-141">Se os dados também não tiverem os cabeçalhos das colunas, o Machine Learning Studio fornece nomes padrão.</span><span class="sxs-lookup"><span data-stu-id="f903b-141">If the data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="f903b-142">É possível especificar explicitamente ou alterar os cabeçalhos e tipos de dados das colunas usando [Editar Metadados][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="f903b-142">You can explicitly specify or change the headings and data types for columns using the [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="f903b-143">Os **tipos de dados** a seguir são reconhecidos pelo Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="f903b-143">The following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="f903b-144">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f903b-144">String</span></span>
* <span data-ttu-id="f903b-145">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="f903b-145">Integer</span></span>
* <span data-ttu-id="f903b-146">Duplo</span><span class="sxs-lookup"><span data-stu-id="f903b-146">Double</span></span>
* <span data-ttu-id="f903b-147">Booliano</span><span class="sxs-lookup"><span data-stu-id="f903b-147">Boolean</span></span>
* <span data-ttu-id="f903b-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="f903b-148">DateTime</span></span>
* <span data-ttu-id="f903b-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="f903b-149">TimeSpan</span></span>

<span data-ttu-id="f903b-150">O Machine Learning Studio usa um tipo de dados interno chamado ***Tabela de Dados*** para transmitir dados entre módulos.</span><span class="sxs-lookup"><span data-stu-id="f903b-150">Machine Learning Studio uses an internal data type called ***Data Table*** to pass data between modules.</span></span> <span data-ttu-id="f903b-151">É possível converter explicitamente os dados para o formato de tabela de dados usando o módulo [Converter para Conjunto de Dados][convert-to-dataset].</span><span class="sxs-lookup"><span data-stu-id="f903b-151">You can explicitly convert your data into Data Table format using the [Convert to Dataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="f903b-152">Qualquer módulo que aceitar formatos diferentes do Data Table converterá os dados para Data Table silenciosamente antes de transmiti-los para o módulo seguinte.</span><span class="sxs-lookup"><span data-stu-id="f903b-152">Any module that accepts formats other than Data Table will convert the data to Data Table silently before passing it to the next module.</span></span>

<span data-ttu-id="f903b-153">Se necessário, você pode converter o formato Data Table de volta para o formato CSV, TSV, ARFF ou SVMLight usando outros módulos de conversão.</span><span class="sxs-lookup"><span data-stu-id="f903b-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="f903b-154">Veja a seção **Conversões de Formato de Dados** da paleta de módulos para ver os módulos que executam essas funções.</span><span class="sxs-lookup"><span data-stu-id="f903b-154">Look in the **Data Format Conversions** section of the module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
