---
title: "solução de previsão aaaA para risco de crédito com o aprendizado de máquina | Microsoft Docs"
description: "Uma passo a passo detalhado mostrando como toocreate uma solução de análise de previsão para crédito avaliação de riscos no estúdio de aprendizado de máquina do Azure."
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
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="ec324-104">Passo a passo: Desenvolver uma solução de análise preditiva para avaliação de risco de crédito no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ec324-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="ec324-105">Neste passo a passo, vamos dar uma olhada estendida no processo de saudação do desenvolvimento de uma solução de análise de previsão no estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="ec324-105">In this walkthrough, we take an extended look at hello process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="ec324-106">Podemos desenvolver um modelo simples no estúdio de aprendizado de máquina e, em seguida, implantá-lo como um serviço web de aprendizado de máquina do Azure onde o modelo de saudação pode fazer previsões com os novos dados.</span><span class="sxs-lookup"><span data-stu-id="ec324-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where hello model can make predictions using new data.</span></span> 

<span data-ttu-id="ec324-107">Este passo a passo pressupõe que você tenha usado o Machine Learning Studio pelo menos uma vez e tenha noções básicas sobre conceitos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="ec324-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="ec324-108">Mas não pressupõe que você seja um especialista em qualquer um deles.</span><span class="sxs-lookup"><span data-stu-id="ec324-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="ec324-109">Se você nunca usou **estúdio de aprendizado de máquina do Azure** antes, talvez você queira toostart com tutorial hello, [criar seu primeiro ciência de dados de experiências no estúdio de aprendizado de máquina do Azure](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="ec324-109">If you've never used **Azure Machine Learning Studio** before, you might want toostart with hello tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="ec324-110">Esse tutorial apresenta estúdio de aprendizado de máquina para Olá primeira vez.</span><span class="sxs-lookup"><span data-stu-id="ec324-110">That tutorial takes you through Machine Learning Studio for hello first time.</span></span> <span data-ttu-id="ec324-111">Ele mostra noções básicas de saudação como toodrag-e-soltar módulos para sua experiência, conectá-los, executar teste hello e examinar os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec324-111">It shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="ec324-112">Outra ferramenta que pode ser útil para a guia de Introdução é um diagrama que fornece uma visão geral dos recursos de saudação do estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="ec324-112">Another tool that may be helpful for getting started is a diagram that gives an overview of hello capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="ec324-113">Você pode baixá-lo e imprimi-lo aqui: [Diagrama de visão geral dos recursos do Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="ec324-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="ec324-114">Se você for novo campo toohello da máquina de aprendizado em geral, há uma série de vídeo que pode ser útil tooyou.</span><span class="sxs-lookup"><span data-stu-id="ec324-114">If you're new toohello field of machine learning in general, there's a video series that might be helpful tooyou.</span></span> <span data-ttu-id="ec324-115">Ele é chamado [ciência de dados para iniciantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) e ele pode dar a você um aprendizado de toomachine excelente introdução usando linguagem cotidiana e conceitos.</span><span class="sxs-lookup"><span data-stu-id="ec324-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction toomachine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a><span data-ttu-id="ec324-116">problema de saudação</span><span class="sxs-lookup"><span data-stu-id="ec324-116">hello problem</span></span>

<span data-ttu-id="ec324-117">Suponha que você precisa toopredict risco de crédito de uma pessoa com base nas informações de saudação fornecida em um aplicativo de crédito.</span><span class="sxs-lookup"><span data-stu-id="ec324-117">Suppose you need toopredict an individual's credit risk based on hello information they gave on a credit application.</span></span>  

<span data-ttu-id="ec324-118">A avaliação de risco de crédito é um problema complexo, mas podemos simplificá-la um pouco para este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="ec324-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="ec324-119">Usaremos isso como um exemplo de como você pode criar uma solução de análise preditiva usando o Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="ec324-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="ec324-120">toodo isso, usamos o estúdio de aprendizado de máquina do Azure e um serviço web de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="ec324-120">toodo this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="hello-solution"></a><span data-ttu-id="ec324-121">solução de saudação</span><span class="sxs-lookup"><span data-stu-id="ec324-121">hello solution</span></span>

<span data-ttu-id="ec324-122">Neste passo a passo detalhado, vamos começar falando sobre os dados de risco de crédito disponíveis publicamente e desenvolver e treinar um modelo de previsão com base nesses dados.</span><span class="sxs-lookup"><span data-stu-id="ec324-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="ec324-123">Podemos implantar Olá modelo como um serviço web para que possa ser usada por outras pessoas para avaliação de risco de crédito.</span><span class="sxs-lookup"><span data-stu-id="ec324-123">Then we deploy hello model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="ec324-124">toocreate essa solução de avaliação de risco de crédito, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ec324-124">toocreate this credit risk assessment solution, we follow these steps:</span></span>  

1. <span data-ttu-id="ec324-125">
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)</span><span class="sxs-lookup"><span data-stu-id="ec324-125">[Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md)</span></span>
2. [<span data-ttu-id="ec324-126">Carregar dados existentes</span><span class="sxs-lookup"><span data-stu-id="ec324-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="ec324-127">Criar um experimento</span><span class="sxs-lookup"><span data-stu-id="ec324-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="ec324-128">Treinar e avaliar modelos Olá</span><span class="sxs-lookup"><span data-stu-id="ec324-128">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="ec324-129">Implantar o serviço web de saudação</span><span class="sxs-lookup"><span data-stu-id="ec324-129">Deploy hello web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="ec324-130">Serviço de acesso a saudação da web</span><span class="sxs-lookup"><span data-stu-id="ec324-130">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="ec324-131">Você pode encontrar uma cópia de trabalho do experimento Olá que desenvolvemos neste passo a passo em Olá [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="ec324-131">You can find a working copy of hello experiment that we develop in this walkthrough in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="ec324-132">Vá muito**[passo a passo - previsão de risco de crédito](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  e clique em **aberto no Studio** toodownload uma cópia do experimento Olá em seu espaço de trabalho do estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="ec324-132">Go too**[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="ec324-133">Este passo a passo se baseia em uma versão simplificada de experiência de exemplo hello, [classificação binária: previsão de risco de crédito](http://go.microsoft.com/fwlink/?LinkID=525270), também disponível no hello [galeria](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="ec324-133">This walkthrough is based on a simplified version of hello sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in hello [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
