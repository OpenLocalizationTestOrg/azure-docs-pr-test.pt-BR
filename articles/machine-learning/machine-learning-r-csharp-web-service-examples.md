---
title: "web de aprendizado de máquina AAA(deprecated) serviços criados com R - Azure | Microsoft Docs"
description: "(preterido) Localize um conjunto útil de exemplos de serviços web criados com código de R e aprendizado de máquina e publicados toohello Azure Marketplace."
keywords: "csharp, código r, exemplos de serviço Web"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a><span data-ttu-id="4b57c-104">(preterido) Exemplos que usam código R no aprendizado de máquina do Azure e publicado tooMicrosoft Azure Marketplace de serviços Web</span><span class="sxs-lookup"><span data-stu-id="4b57c-104">(deprecated) Web services examples using R code on Azure Machine Learning and published tooMicrosoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="4b57c-105">Olá Microsoft DataMarket está sendo desativado e essas APIs foram preteridas.</span><span class="sxs-lookup"><span data-stu-id="4b57c-105">hello Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="4b57c-106">Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4b57c-106">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4b57c-107">Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="4b57c-107">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="4b57c-108">Neste artigo são web de exemplo serviços foram criados usando o aprendizado de máquina do Azure e publicados toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4b57c-108">In this article are example web services were created using Azure Machine Learning and published toohello Azure Marketplace.</span></span> <span data-ttu-id="4b57c-109">Cada exemplo de serviço da web tem um documento abrangente anexado, incorporação de conjuntos de dados de exemplo para testar serviços hello e explicando como Olá usuário pode criar um serviço semelhante próprios.</span><span class="sxs-lookup"><span data-stu-id="4b57c-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing hello services and explaining how hello user can create a similar service themselves.</span></span> 

<span data-ttu-id="4b57c-110">No estúdio de aprendizado de máquina do Azure, os usuários podem escrever código R e com alguns cliques, publicá-lo como um serviço web para aplicativos e dispositivos tooconsume em torno de Olá, mundo.</span><span class="sxs-lookup"><span data-stu-id="4b57c-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices tooconsume around hello world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="4b57c-111">De produzir calculadoras simples que fornecem funcionalidade de estatística toocreating um indicador de análise de sentimento de mineração de texto personalizado, novos e experientes usuários de R podem se beneficiar de facilidade de saudação com a qual os usuários de aprendizado de máquina do Azure podem utilizar o R código.</span><span class="sxs-lookup"><span data-stu-id="4b57c-111">From producing simple calculators that provide statistical functionality toocreating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from hello ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="4b57c-112">Enquanto esses serviços da web podem ser consumidos por usuários, possivelmente por meio de um aplicativo móvel ou um site, Olá finalidade desses serviços web exemplos é tooshow como pode utilizar o aprendizado de máquina R scripts para fins analíticos e ser usado toocreate serviços da web em parte superior do código R.</span><span class="sxs-lookup"><span data-stu-id="4b57c-112">While these web services could be consumed by users, potentially through a mobile app or a website, hello purpose of these web services examples is tooshow how Machine Learning can operationalize R scripts for analytical purposes and be used toocreate web services on top of R code.</span></span>

<span data-ttu-id="4b57c-113">Cada exemplo inclui um exemplo de C# para consumo do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="4b57c-113">Each example includes a C# example for web service consumption.</span></span>

![Diagrama de código R no aprendizado de máquina do Azure: soluções de R para uso proprietário ou publicado toohello Azure Marketplace.][1]

<span data-ttu-id="4b57c-115">Considere os seguintes cenários de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b57c-115">Consider hello following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="4b57c-116">Cenário 1: Modelo genérico</span><span class="sxs-lookup"><span data-stu-id="4b57c-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="4b57c-117">O usuário trabalha com um modelo genérico que pode ser dados aplicada tooa novo usuário, como uma previsão básica de dados de série temporal ou um método de R personalizado com análises avançadas.</span><span class="sxs-lookup"><span data-stu-id="4b57c-117">A user works with a generic model that can be applied tooa new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="4b57c-118">Este usuário publica Olá tooconsume com seus dados de modelo como um serviço web para que outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="4b57c-118">This user publishes hello model as a web service for others tooconsume with their data.</span></span>

* [<span data-ttu-id="4b57c-119">Classificador binário</span><span class="sxs-lookup"><span data-stu-id="4b57c-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="4b57c-120">Modelo de cluster</span><span class="sxs-lookup"><span data-stu-id="4b57c-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="4b57c-121">Regressão linear multivariada</span><span class="sxs-lookup"><span data-stu-id="4b57c-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="4b57c-122">Previsão - Ajuste exponencial</span><span class="sxs-lookup"><span data-stu-id="4b57c-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="4b57c-123">Previsão ETS + STL</span><span class="sxs-lookup"><span data-stu-id="4b57c-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="4b57c-124">ARIMA (Forecasting-AutoRegressive Integrated Moving Average, média móvel integrada de previsão-autorregressão)</span><span class="sxs-lookup"><span data-stu-id="4b57c-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="4b57c-125">Análise de sobrevivência</span><span class="sxs-lookup"><span data-stu-id="4b57c-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="4b57c-126">Cenário 2: Modelo treinado – dados específicos</span><span class="sxs-lookup"><span data-stu-id="4b57c-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="4b57c-127">Um usuário tem dados que fornece previsões úteis por meio de código R, como um grande exemplo de questionários personalidade em cluster por meio do tipo de personalidade k-means algoritmo toopredict saudação do usuário ou dados que podem ser usada toopredict uma pesquisa com integridade um indivíduo risco de câncer de Pulmão com um pacote de R de análise de sobrevivência.</span><span class="sxs-lookup"><span data-stu-id="4b57c-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm toopredict hello user’s personality type, or health survey data that can be used toopredict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="4b57c-128">usuário Olá publica dados de saudação por meio de um serviço web que prevê o resultado de um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="4b57c-128">hello user publishes hello data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="4b57c-129">Cenário 3: Modelo treinado – dados genéricos</span><span class="sxs-lookup"><span data-stu-id="4b57c-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="4b57c-130">Um usuário tiver dados genéricos (por exemplo, um corpo de texto) que permite que um toobe de serviço web criado e aplicado genericamente em diferentes tipos de cenários e casos de uso.</span><span class="sxs-lookup"><span data-stu-id="4b57c-130">A user has generic data (such as a text corpus) that allows a web service toobe built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="4b57c-131">Análise de sentimento baseada em léxico</span><span class="sxs-lookup"><span data-stu-id="4b57c-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="4b57c-132">Cenário 4: Calculadora avançada</span><span class="sxs-lookup"><span data-stu-id="4b57c-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="4b57c-133">Um usuário fornece cálculos avançados ou simulações que não exigem qualquer modelo treinado ou uma conexão de dados do usuário de toohello um modelo.</span><span class="sxs-lookup"><span data-stu-id="4b57c-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model toohello user’s data.</span></span>

* [<span data-ttu-id="4b57c-134">Diferença no teste de proporções</span><span class="sxs-lookup"><span data-stu-id="4b57c-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="4b57c-135">Pacote de distribuição normal</span><span class="sxs-lookup"><span data-stu-id="4b57c-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="4b57c-136">Pacote de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="4b57c-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="4b57c-137">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="4b57c-137">FAQ</span></span>
<span data-ttu-id="4b57c-138">Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4b57c-138">For frequently asked questions on consumption of hello web service or publishing toohello Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



