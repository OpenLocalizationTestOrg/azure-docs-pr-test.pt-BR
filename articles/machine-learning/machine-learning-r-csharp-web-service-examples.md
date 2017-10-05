---
title: "(preterido) Exemplos de serviços Web do Machine Learning criados com R - Azure | Microsoft Docs"
description: "(preterido) Encontre um conjunto útil de exemplos de serviços Web criados com código R e Machine Learning e publicado no Azure Marketplace."
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
redirect_document_id: TRUE
ms.openlocfilehash: 9514025db6f812f9e7934ea2d1575e948d6585b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a><span data-ttu-id="f8009-104">(preterido) Exemplos de serviços Web usando código R no Azure Machine Learning e publicados no Microsoft Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f8009-104">(deprecated) Web services examples using R code on Azure Machine Learning and published to Microsoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="f8009-105">O Microsoft DataMarket está sendo desativado e essas APIs foram preteridas.</span><span class="sxs-lookup"><span data-stu-id="f8009-105">The Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="f8009-106">Você pode encontrar muitos testes de exemplo úteis e APIs na [Galeria do Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="f8009-106">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="f8009-107">Para saber mais sobre a Galeria, confira [Compartilhar e descobrir soluções na Galeria do Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="f8009-107">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="f8009-108">Neste artigo, os serviços Web de exemplo são criados usando o Azure Machine Learning e publicados no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f8009-108">In this article are example web services were created using Azure Machine Learning and published to the Azure Marketplace.</span></span> <span data-ttu-id="f8009-109">Cada exemplo de serviço Web tem um documento abrangente anexado, incorporando exemplos de conjuntos de dados para testar os serviços e explicando como o usuário pode criar seu próprio serviço semelhante.</span><span class="sxs-lookup"><span data-stu-id="f8009-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing the services and explaining how the user can create a similar service themselves.</span></span> 

<span data-ttu-id="f8009-110">No Azure Machine Learning Studio, os usuários podem escrever código R e, com alguns cliques, publicá-lo como um serviço Web para aplicativos e dispositivos o consumirem em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="f8009-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices to consume around the world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="f8009-111">Desde produzir calculadoras simples que fornecem funcionalidade de estatística até a criação de um preditor personalizado de análise de sentimento de mineração de texto, por exemplo, os usuários novos e experientes do R podem aproveitar a facilidade com que os usuários de Azure Machine Learning podem operacionalizar o código R.</span><span class="sxs-lookup"><span data-stu-id="f8009-111">From producing simple calculators that provide statistical functionality to creating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from the ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="f8009-112">Embora esses serviços Web possam ser consumidos por usuários, potencialmente por meio de um aplicativo móvel ou de um site, a finalidade desses exemplos de serviços Web é mostrar como o Machine Learning pode colocar em operação Scripts R para fins analíticos e ser usado para criar serviços Web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="f8009-112">While these web services could be consumed by users, potentially through a mobile app or a website, the purpose of these web services examples is to show how Machine Learning can operationalize R scripts for analytical purposes and be used to create web services on top of R code.</span></span>

<span data-ttu-id="f8009-113">Cada exemplo inclui um exemplo de C# para consumo do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="f8009-113">Each example includes a C# example for web service consumption.</span></span>

![Diagrama de código R no Azure Machine Learning: soluções R para os proprietários usarem ou publicarem no Azure Marketplace.][1]

<span data-ttu-id="f8009-115">Considere os seguintes cenários.</span><span class="sxs-lookup"><span data-stu-id="f8009-115">Consider the following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="f8009-116">Cenário 1: Modelo genérico</span><span class="sxs-lookup"><span data-stu-id="f8009-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="f8009-117">Um usuário trabalha com um modelo genérico que pode ser aplicado a dados de um novo usuário, como uma previsão básica de dados de série temporal ou um método de R personalizado com análises avançadas.</span><span class="sxs-lookup"><span data-stu-id="f8009-117">A user works with a generic model that can be applied to a new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="f8009-118">Esse usuário publica o modelo como um serviço Web para que outros possam consumi-lo com seus dados.</span><span class="sxs-lookup"><span data-stu-id="f8009-118">This user publishes the model as a web service for others to consume with their data.</span></span>

* [<span data-ttu-id="f8009-119">Classificador binário</span><span class="sxs-lookup"><span data-stu-id="f8009-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="f8009-120">Modelo de cluster</span><span class="sxs-lookup"><span data-stu-id="f8009-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="f8009-121">Regressão linear multivariada</span><span class="sxs-lookup"><span data-stu-id="f8009-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="f8009-122">Previsão - Ajuste exponencial</span><span class="sxs-lookup"><span data-stu-id="f8009-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="f8009-123">Previsão ETS + STL</span><span class="sxs-lookup"><span data-stu-id="f8009-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="f8009-124">ARIMA (Forecasting-AutoRegressive Integrated Moving Average, média móvel integrada de previsão-autorregressão)</span><span class="sxs-lookup"><span data-stu-id="f8009-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="f8009-125">Análise de sobrevivência</span><span class="sxs-lookup"><span data-stu-id="f8009-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="f8009-126">Cenário 2: Modelo treinado – dados específicos</span><span class="sxs-lookup"><span data-stu-id="f8009-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="f8009-127">Um usuário tem dados que fornecem previsões úteis por meio de código R, como uma grande amostra de questionários de personalidade agrupados por meio de um algoritmo k-means, para prever os dados da pesquisa de saúde ou tipo de personalidade do usuário que podem ser usados para prever o risco de uma pessoa ter câncer de pulmão com um pacote R de análise de sobrevivência.</span><span class="sxs-lookup"><span data-stu-id="f8009-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm to predict the user’s personality type, or health survey data that can be used to predict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="f8009-128">O usuário publica os dados por meio de um serviço Web que prevê o resultado de um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="f8009-128">The user publishes the data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="f8009-129">Cenário 3: Modelo treinado – dados genéricos</span><span class="sxs-lookup"><span data-stu-id="f8009-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="f8009-130">Um usuário tem dados genéricos (por exemplo, um corpus de texto) que permitem desenvolver um serviço Web e aplicá-lo genericamente a diferentes tipos de cenários e casos de uso.</span><span class="sxs-lookup"><span data-stu-id="f8009-130">A user has generic data (such as a text corpus) that allows a web service to be built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="f8009-131">Análise de sentimento baseada em léxico</span><span class="sxs-lookup"><span data-stu-id="f8009-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="f8009-132">Cenário 4: Calculadora avançada</span><span class="sxs-lookup"><span data-stu-id="f8009-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="f8009-133">Um usuário fornece cálculos avançados ou simulações, que não requerem qualquer modelo treinado ou ajuste de um modelo aos dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="f8009-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model to the user’s data.</span></span>

* [<span data-ttu-id="f8009-134">Diferença no teste de proporções</span><span class="sxs-lookup"><span data-stu-id="f8009-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="f8009-135">Pacote de distribuição normal</span><span class="sxs-lookup"><span data-stu-id="f8009-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="f8009-136">Pacote de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="f8009-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="f8009-137">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="f8009-137">FAQ</span></span>
<span data-ttu-id="f8009-138">Para perguntas frequentes sobre o consumo do serviço Web ou a publicação no Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="f8009-138">For frequently asked questions on consumption of the web service or publishing to the Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



