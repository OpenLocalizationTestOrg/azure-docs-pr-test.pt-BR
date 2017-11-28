---
title: "Uma solução preditiva para o risco de crédito com o Machine Learning | Microsoft Docs"
description: "Um passo a passo detalhado mostrando como criar uma solução de análise preditiva para avaliação de risco de crédito no Azure Machine Learning Studio."
keywords: "risco de crédito, solução de análise preditiva, avaliação de riscos"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: e1af999b2fde8ffa2a0ffd1b88230f0aaab32b37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="4ebf7-104">Passo a passo: Desenvolver uma solução de análise preditiva para avaliação de risco de crédito no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4ebf7-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="4ebf7-105">Neste passo a passo, vamos conferir de forma aprofundada o processo de desenvolvimento de uma solução de análise preditiva no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-105">In this walkthrough, we take an extended look at the process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="4ebf7-106">Vamos desenvolver um modelo simples no Machine Learning Studio e implantá-lo como um serviço Web do Machine Learning do Azure, em que o modelo pode fazer previsões usando novos dados.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where the model can make predictions using new data.</span></span> 

<span data-ttu-id="4ebf7-107">Este passo a passo pressupõe que você tenha usado o Machine Learning Studio pelo menos uma vez e tenha noções básicas sobre conceitos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="4ebf7-108">Mas não pressupõe que você seja um especialista em qualquer um deles.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="4ebf7-109">Se você nunca usou **Azure Machine Learning Studio** antes, convém iniciar pelo tutorial [Criar seu primeiro experimento de ciência de dados no Azure Machine Learning Studio](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="4ebf7-109">If you've never used **Azure Machine Learning Studio** before, you might want to start with the tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="4ebf7-110">Esse tutorial leva você a explorar o Machine Learning Studio pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-110">That tutorial takes you through Machine Learning Studio for the first time.</span></span> <span data-ttu-id="4ebf7-111">Ele mostra os conceitos básicos de como arrastar e soltar módulos no seu experimento, conectá-los, executar o experimento e examinar os resultados.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-111">It shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="4ebf7-112">Outra ferramenta que pode ser útil para introdução é um diagrama que fornece uma visão geral dos recursos do Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-112">Another tool that may be helpful for getting started is a diagram that gives an overview of the capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="4ebf7-113">Você pode baixá-lo e imprimi-lo aqui: [Diagrama de visão geral dos recursos do Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="4ebf7-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="4ebf7-114">Se você é novo no campo de aprendizado de máquina em geral, há uma série de vídeos que pode ser útil para você.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-114">If you're new to the field of machine learning in general, there's a video series that might be helpful to you.</span></span> <span data-ttu-id="4ebf7-115">Ela é chamada de [Ciência de dados para iniciantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) e pode fornecer uma excelente introdução ao aprendizado de máquina usando linguagem e conceitos do dia a dia.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction to machine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="the-problem"></a><span data-ttu-id="4ebf7-116">O problema</span><span class="sxs-lookup"><span data-stu-id="4ebf7-116">The problem</span></span>

<span data-ttu-id="4ebf7-117">Suponha que você precisa prever o risco de crédito de uma pessoa com base nas informações dadas em um aplicativo de crédito.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-117">Suppose you need to predict an individual's credit risk based on the information they gave on a credit application.</span></span>  

<span data-ttu-id="4ebf7-118">A avaliação de risco de crédito é um problema complexo, mas podemos simplificá-la um pouco para este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="4ebf7-119">Usaremos isso como um exemplo de como você pode criar uma solução de análise preditiva usando o Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="4ebf7-120">Para fazer isso, usamos o Azure Machine Learning Studio e um serviço Web do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-120">To do this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="the-solution"></a><span data-ttu-id="4ebf7-121">A solução</span><span class="sxs-lookup"><span data-stu-id="4ebf7-121">The solution</span></span>

<span data-ttu-id="4ebf7-122">Neste passo a passo detalhado, vamos começar falando sobre os dados de risco de crédito disponíveis publicamente e desenvolver e treinar um modelo de previsão com base nesses dados.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="4ebf7-123">Então podemos implantar o modelo como um serviço Web para que ele pode ser usado por outras pessoas para avaliação de risco de crédito.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-123">Then we deploy the model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="4ebf7-124">Para criar essa solução de avaliação de risco de crédito, vamos seguir estas etapas:</span><span class="sxs-lookup"><span data-stu-id="4ebf7-124">To create this credit risk assessment solution, we follow these steps:</span></span>  

1. <span data-ttu-id="4ebf7-125">
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)</span><span class="sxs-lookup"><span data-stu-id="4ebf7-125">[Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md)</span></span>
2. [<span data-ttu-id="4ebf7-126">Carregar dados existentes</span><span class="sxs-lookup"><span data-stu-id="4ebf7-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="4ebf7-127">Criar um experimento</span><span class="sxs-lookup"><span data-stu-id="4ebf7-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="4ebf7-128">Treinar e avaliar os modelos</span><span class="sxs-lookup"><span data-stu-id="4ebf7-128">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="4ebf7-129">Implantar o serviço Web</span><span class="sxs-lookup"><span data-stu-id="4ebf7-129">Deploy the web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="4ebf7-130">Acessar o serviço Web</span><span class="sxs-lookup"><span data-stu-id="4ebf7-130">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="4ebf7-131">Você pode encontrar uma cópia funcional do experimento que desenvolvemos neste passo a passo na [Galeria do Cortana Intelligence](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4ebf7-131">You can find a working copy of the experiment that we develop in this walkthrough in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4ebf7-132">Vá até **[Passo a passo – Previsão de risco de crédito](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** e clique em **Abrir no Studio** para baixar uma cópia do experimento no seu espaço de trabalho do Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4ebf7-132">Go to **[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="4ebf7-133">Este passo a passo baseia-se em uma versão simplificada do experimento de exemplo, [Classificação binária: previsão de risco de crédito](http://go.microsoft.com/fwlink/?LinkID=525270) disponível também na [Galeria](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="4ebf7-133">This walkthrough is based on a simplified version of the sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in the [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
