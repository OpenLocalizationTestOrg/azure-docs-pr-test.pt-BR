---
title: "experiência simples de aaaA no estúdio de aprendizado de máquina | Microsoft Docs"
description: "Este tutorial de aprendizado de máquina percorre um teste de ciência de dados. Podemos será prever o preço de saudação de um carro usando um algoritmo de regressão."
keywords: "teste,regressão linear,algoritmos de aprendizado de máquina,tutorial de aprendizado de máquina,técnicas de modelos de previsão, teste de ciência de dados"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="02cb8-105">Tutorial de aprendizado de máquina: Crie sua primeira experiência no Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="02cb8-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="02cb8-106">Se você nunca usou o **Azure Machine Learning Studio** antes, este tutorial é para você.</span><span class="sxs-lookup"><span data-stu-id="02cb8-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="02cb8-107">Neste tutorial, examinaremos como toouse Studio para Olá primeiro tempo toocreate uma experiência de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="02cb8-107">In this tutorial, we'll walk through how toouse Studio for hello first time toocreate a machine learning experiment.</span></span> <span data-ttu-id="02cb8-108">experiência de saudação testar um modelo analítico que prevê o preço de saudação de um automóvel com base em variáveis diferentes, como criar e especificações técnicas.</span><span class="sxs-lookup"><span data-stu-id="02cb8-108">hello experiment will test an analytical model that predicts hello price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="02cb8-109">Este tutorial mostra a você noções básicas de saudação como toodrag-e-soltar módulos para sua experiência, conectá-los, executar teste hello e examinar os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-109">This tutorial shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="02cb8-110">Não vamos toodiscuss Olá tópico geral de aprendizado de máquina ou como tooselect e use Olá 100 + algoritmos e dados manipulação módulos internos incluídos no estúdio.</span><span class="sxs-lookup"><span data-stu-id="02cb8-110">We're not going toodiscuss hello general topic of machine learning or how tooselect and use hello 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="02cb8-111">Se você for novo aprendizado de toomachine, Olá série de vídeos [ciência de dados para iniciantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) pode ser um bom lugar toostart.</span><span class="sxs-lookup"><span data-stu-id="02cb8-111">If you're new toomachine learning, hello video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place toostart.</span></span> <span data-ttu-id="02cb8-112">Esta série de vídeos é aprendizado de toomachine uma ótima introdução usando linguagem cotidiana e conceitos.</span><span class="sxs-lookup"><span data-stu-id="02cb8-112">This video series is a great introduction toomachine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="02cb8-113">Se você estiver familiarizado com o aprendizado de máquina, mas você estiver procurando para obter mais informações sobre o estúdio de aprendizado de máquina e contém os algoritmos de aprendizado de máquina Olá, aqui estão alguns bons recursos:</span><span class="sxs-lookup"><span data-stu-id="02cb8-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and hello machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="02cb8-114">O que é o Machine Learning Studio?</span><span class="sxs-lookup"><span data-stu-id="02cb8-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="02cb8-115">– Essa é uma visão geral do Estúdio.</span><span class="sxs-lookup"><span data-stu-id="02cb8-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="02cb8-116">[Noções básicas com exemplos de algoritmo de aprendizado de máquina](machine-learning-basics-infographic-with-algorithm-examples.md) -este infográfico é útil se você quiser toolearn mais sobre os tipos diferentes de saudação de algoritmos de aprendizagem de máquina, incluídos no estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="02cb8-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want toolearn more about hello different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="02cb8-117">[Guia de aprendizado de máquina](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -este guia inclui informações semelhantes como Olá infográfico acima, mas em um formato interativo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as hello infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="02cb8-118">[Roteiro do algoritmo de aprendizado de máquina](machine-learning-algorithm-cheat-sheet.md) e [como toochoose algoritmos de aprendizado de máquina do Microsoft Azure](machine-learning-algorithm-choice.md) -este pôster baixável e o artigo complementar discutem algoritmos de Studio Olá em camadas.</span><span class="sxs-lookup"><span data-stu-id="02cb8-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss hello Studio algorithms in depth.</span></span>
- <span data-ttu-id="02cb8-119">[Estúdio de aprendizado de máquina: Algoritmo e Ajuda do módulo](https://msdn.microsoft.com/library/azure/dn905974.aspx) -esta é a referência completa Olá para todos os módulos do Studio, incluindo algoritmos de aprendizagem de máquina</span><span class="sxs-lookup"><span data-stu-id="02cb8-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is hello complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="02cb8-120">Como o Machine Learning Studio ajuda?</span><span class="sxs-lookup"><span data-stu-id="02cb8-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="02cb8-121">O estúdio de aprendizado de máquina torna fácil tooset backup de um experimento usando arrastar e soltar módulos previamente programados com técnicas de modelagem de previsão.</span><span class="sxs-lookup"><span data-stu-id="02cb8-121">Machine Learning Studio makes it easy tooset up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="02cb8-122">Usando um espaço de trabalho visual, interativo, você arrasta e solta ***conjuntos de dados*** e ***módulos*** de análise em telas interativas.</span><span class="sxs-lookup"><span data-stu-id="02cb8-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="02cb8-123">Você conectá-los junto tooform um ***experimentar*** que são executados no estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="02cb8-123">You connect them together tooform an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="02cb8-124">Você ***criar um modelo de***, ***treinar modelo Olá***, e ***pontuação e teste Olá modelo***.</span><span class="sxs-lookup"><span data-stu-id="02cb8-124">You ***create a model***, ***train hello model***, and ***score and test hello model***.</span></span>

<span data-ttu-id="02cb8-125">Você pode iterar em seu design de modelo, editando experiência hello e executá-lo até que ele oferece você Olá resultados que você está procurando.</span><span class="sxs-lookup"><span data-stu-id="02cb8-125">You can iterate on your model design, editing hello experiment and running it until it gives you hello results you're looking for.</span></span> <span data-ttu-id="02cb8-126">Quando o modelo estiver pronto, você poderá publicá-lo como um ***serviço Web*** para que outras pessoas possam enviar novos dados e obter previsões em troca.</span><span class="sxs-lookup"><span data-stu-id="02cb8-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="02cb8-127">Abrir o Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="02cb8-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="02cb8-128">tooget Introdução ao Studio, vá muito[https://studio.azureml.net](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="02cb8-128">tooget started with Studio, go too[https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="02cb8-129">Se você já entrou no Machine Learning Studio antes, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="02cb8-130">Caso contrário, clique em **Inscrever-se aqui** e escolha entre as opções gratuitas e pagas.</span><span class="sxs-lookup"><span data-stu-id="02cb8-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="02cb8-131">![Entrar no estúdio de aprendizado do tooMachine][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="02cb8-131">![Sign in tooMachine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="02cb8-132">
***Entrar no estúdio de aprendizado do tooMachine***</span><span class="sxs-lookup"><span data-stu-id="02cb8-132">
***Sign in tooMachine Learning Studio***</span></span>

## <a name="five-steps-toocreate-an-experiment"></a><span data-ttu-id="02cb8-133">Cinco etapas toocreate um experimento</span><span class="sxs-lookup"><span data-stu-id="02cb8-133">Five steps toocreate an experiment</span></span>

<span data-ttu-id="02cb8-134">Neste tutorial de aprendizado de máquina, você execute um teste no estúdio de aprendizado de máquina toocreate, treinamento, toobuild de cinco etapas básicas e classificar seu modelo:</span><span class="sxs-lookup"><span data-stu-id="02cb8-134">In this machine learning tutorial, you'll follow five basic steps toobuild an experiment in Machine Learning Studio toocreate, train, and score your model:</span></span>

- <span data-ttu-id="02cb8-135">**Criar um modelo**</span><span class="sxs-lookup"><span data-stu-id="02cb8-135">**Create a model**</span></span>
    - <span data-ttu-id="02cb8-136">[Etapa 1: Obter dados]</span><span class="sxs-lookup"><span data-stu-id="02cb8-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="02cb8-137">[Etapa 2: Preparar dados saudação]</span><span class="sxs-lookup"><span data-stu-id="02cb8-137">[Step 2: Prepare hello data]</span></span>
    - <span data-ttu-id="02cb8-138">[Etapa 3: Definir recursos]</span><span class="sxs-lookup"><span data-stu-id="02cb8-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="02cb8-139">**Treinar modelo de saudação**</span><span class="sxs-lookup"><span data-stu-id="02cb8-139">**Train hello model**</span></span>
    - <span data-ttu-id="02cb8-140">[Etapa 4: Escolher e aplicar um algoritmo de aprendizado]</span><span class="sxs-lookup"><span data-stu-id="02cb8-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="02cb8-141">**Pontuação e teste Olá modelo**</span><span class="sxs-lookup"><span data-stu-id="02cb8-141">**Score and test hello model**</span></span>
    - <span data-ttu-id="02cb8-142">[Etapa 5: Prever novos preços de automóveis]</span><span class="sxs-lookup"><span data-stu-id="02cb8-142">[Step 5: Predict new automobile prices]</span></span>

[Etapa 1: Obter dados]: #step-1-get-data
[Etapa 2: Preparar dados saudação]: #step-2-prepare-the-data
[Etapa 3: Definir recursos]: #step-3-define-features
[Etapa 4: Escolher e aplicar um algoritmo de aprendizado]: #step-4-choose-and-apply-a-learning-algorithm
[Etapa 5: Prever novos preços de automóveis]: #step-5-predict-new-automobile-prices

> [!TIP] 
> <span data-ttu-id="02cb8-148">Você pode encontrar uma cópia de trabalho do hello seguintes experiência em Olá [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="02cb8-148">You can find a working copy of hello following experiment in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="02cb8-149">Vá muito**[sua primeira ciência de dados de experiências - previsão de preços de automóvel](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  e clique em **aberto no Studio** toodownload uma cópia do experimento Olá para o aprendizado de máquina Espaço de trabalho do Studio.</span><span class="sxs-lookup"><span data-stu-id="02cb8-149">Go too**[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="02cb8-150">Etapa 1: Obter dados</span><span class="sxs-lookup"><span data-stu-id="02cb8-150">Step 1: Get data</span></span>

<span data-ttu-id="02cb8-151">Olá primeira coisa tooperform aprendizado de máquina é de dados.</span><span class="sxs-lookup"><span data-stu-id="02cb8-151">hello first thing you need tooperform machine learning is data.</span></span>
<span data-ttu-id="02cb8-152">Há uma série de conjuntos de dados de exemplo incluídos no Machine Learning Studio que você pode usar ou você pode importar dados de várias fontes.</span><span class="sxs-lookup"><span data-stu-id="02cb8-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="02cb8-153">Neste exemplo, vamos usar conjunto de dados de exemplo hello, **dados de preços de automóvel (Raw)**, que está incluído no espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="02cb8-153">For this example, we'll use hello sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="02cb8-154">Esse conjunto de dados inclui entradas para vários automóveis individuais, incluindo informações como marca, modelo, especificações técnicas e preço.</span><span class="sxs-lookup"><span data-stu-id="02cb8-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="02cb8-155">Aqui está como tooget Olá o conjunto de dados em sua experiência.</span><span class="sxs-lookup"><span data-stu-id="02cb8-155">Here's how tooget hello dataset into your experiment.</span></span>

1. <span data-ttu-id="02cb8-156">Crie um novo teste clicando **+ novo** na Olá inferior da janela do estúdio de aprendizado de máquina hello, selecione **EXPERIMENTAR**e, em seguida, selecione **experiências em branco**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-156">Create a new experiment by clicking **+NEW** at hello bottom of hello Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="02cb8-157">experiência de saudação recebe um nome padrão que você pode ver na parte superior de saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="02cb8-157">hello experiment is given a default name that you can see at hello top of hello canvas.</span></span> <span data-ttu-id="02cb8-158">Selecione esse texto e renomear toosomething significativo, por exemplo, **previsão de preços de automóvel**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-158">Select this text and rename it toosomething meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="02cb8-159">nome da saudação não precisa toobe exclusivo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-159">hello name doesn't need toobe unique.</span></span>

    ![Renomear experimento Olá][rename-experiment]

2. <span data-ttu-id="02cb8-161">toohello esquerda da tela de experimento Olá é uma paleta de conjuntos de dados e módulos.</span><span class="sxs-lookup"><span data-stu-id="02cb8-161">toohello left of hello experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="02cb8-162">Tipo **automóvel** na caixa de pesquisa de saudação na parte superior da saudação deste conjunto de paleta toofind Olá dados rotulados **dados de preços de automóvel (Raw)**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-162">Type **automobile** in hello Search box at hello top of this palette toofind hello dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="02cb8-163">Arraste esta tela de experimento toohello conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="02cb8-163">Drag this dataset toohello experiment canvas.</span></span>

    <span data-ttu-id="02cb8-164">![Localizar automóvel Olá de conjunto de dados e arraste-o para a tela de experimento Olá][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-164">![Find hello automobile dataset and drag it onto hello experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="02cb8-165">***Localizar automóvel Olá de conjunto de dados e arraste-o para a tela de experimento Olá***</span><span class="sxs-lookup"><span data-stu-id="02cb8-165">***Find hello automobile dataset and drag it onto hello experiment canvas***</span></span>

<span data-ttu-id="02cb8-166">toosee esses dados aparência como, clique em Olá a porta de saída na parte inferior de saudação do automóvel Olá de conjunto de dados e, em seguida, selecione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-166">toosee what this data looks like, click hello output port at hello bottom of hello automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="02cb8-167">![Clique em porta de saída de hello e selecione "Visualizar"][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="02cb8-167">![Click hello output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="02cb8-168">
***Clique em porta de saída de hello e selecione "Visualizar"***</span><span class="sxs-lookup"><span data-stu-id="02cb8-168">
***Click hello output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="02cb8-169">Conjuntos de dados e módulos com entrada e portas de saída representadas por círculos pequenos - portas de entrada na parte superior do hello, saída portas na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-169">Datasets and modules have input and output ports represented by small circles - input ports at hello top, output ports at hello bottom.</span></span>
<span data-ttu-id="02cb8-170">toocreate um fluxo de dados por meio de sua experiência, você se conectará uma porta de saída da porta de entrada tooan um módulo de outro.</span><span class="sxs-lookup"><span data-stu-id="02cb8-170">toocreate a flow of data through your experiment, you'll connect an output port of one module tooan input port of another.</span></span>
<span data-ttu-id="02cb8-171">A qualquer momento, você pode clicar em Olá a porta de saída de um conjunto de dados ou o módulo toosee quais Olá aparência dos dados nesse ponto no fluxo de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-171">At any time, you can click hello output port of a dataset or module toosee what hello data looks like at that point in hello data flow.</span></span>

<span data-ttu-id="02cb8-172">Neste conjunto de dados de exemplo, cada instância de um automóvel aparece como uma linha e variáveis de saudação associadas a cada automóvel aparecem como colunas.</span><span class="sxs-lookup"><span data-stu-id="02cb8-172">In this sample dataset, each instance of an automobile appears as a row, and hello variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="02cb8-173">Considerando variáveis Olá para um automóvel específico, vamos preço de saudação do tootry toopredict na coluna à direita (coluna 26, intitulada "price").</span><span class="sxs-lookup"><span data-stu-id="02cb8-173">Given hello variables for a specific automobile, we're going tootry toopredict hello price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="02cb8-174">![Exibir dados de automóvel Olá na janela de visualização de dados Olá][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="02cb8-174">![View hello automobile data in hello data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="02cb8-175">
***Exibir dados de automóvel Olá na janela de visualização de dados Olá***</span><span class="sxs-lookup"><span data-stu-id="02cb8-175">
***View hello automobile data in hello data visualization window***</span></span>

<span data-ttu-id="02cb8-176">Janela de visualização de saudação fechar clicando hello "**x**" no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-176">Close hello visualization window by clicking hello "**x**" in hello upper-right corner.</span></span>

## <a name="step-2-prepare-hello-data"></a><span data-ttu-id="02cb8-177">Etapa 2: Preparar dados saudação</span><span class="sxs-lookup"><span data-stu-id="02cb8-177">Step 2: Prepare hello data</span></span>

<span data-ttu-id="02cb8-178">Um conjunto de dados geralmente requer algum pré-processamento antes de poder ser analisado.</span><span class="sxs-lookup"><span data-stu-id="02cb8-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="02cb8-179">Por exemplo, você deve ter notado Olá faltando valores presentes nas colunas de saudação de várias linhas.</span><span class="sxs-lookup"><span data-stu-id="02cb8-179">For example, you might have noticed hello missing values present in hello columns of various rows.</span></span> <span data-ttu-id="02cb8-180">Esses valores ausentes precisam toobe limpo modelo Olá pode analisar dados saudação corretamente.</span><span class="sxs-lookup"><span data-stu-id="02cb8-180">These missing values need toobe cleaned so hello model can analyze hello data correctly.</span></span> <span data-ttu-id="02cb8-181">Em nosso caso, vamos remover quaisquer linhas que contém valores ausentes.</span><span class="sxs-lookup"><span data-stu-id="02cb8-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="02cb8-182">Além disso, Olá **perdas normalizadas** coluna tem uma grande proporção de valores ausentes, portanto, o excluiremos essa coluna de modelo Olá completamente.</span><span class="sxs-lookup"><span data-stu-id="02cb8-182">Also, hello **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from hello model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="02cb8-183">Olá limpeza não valores de dados de entrada é um pré-requisito para usando a maioria dos módulos de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-183">Cleaning hello missing values from input data is a prerequisite for using most of hello modules.</span></span>

<span data-ttu-id="02cb8-184">Primeiro, adicione um módulo que remove Olá **perdas normalizadas** coluna completamente, e, em seguida, podemos adicionar outro módulo que remove qualquer linha que tem dados ausentes.</span><span class="sxs-lookup"><span data-stu-id="02cb8-184">First we add a module that removes hello **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="02cb8-185">Tipo **selecionar colunas** na caixa de pesquisa de saudação na parte superior da saudação de saudação do hello módulo paleta toofind [selecionar colunas no conjunto de dados] [ select-columns] módulo, arraste-a como tela de experimento toohello .</span><span class="sxs-lookup"><span data-stu-id="02cb8-185">Type **select columns** in hello Search box at hello top of hello module palette toofind hello [Select Columns in Dataset][select-columns] module, then drag it toohello experiment canvas.</span></span> <span data-ttu-id="02cb8-186">Esse módulo permite tooselect Olá a quais colunas de dados que deseja tooinclude ou excluir no modelo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-186">This module allows us tooselect which columns of data we want tooinclude or exclude in hello model.</span></span>

2. <span data-ttu-id="02cb8-187">Conecte-se a porta de saída de saudação do hello **dados de preços de automóvel (Raw)** toohello de conjunto de dados de entrada porta Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-187">Connect hello output port of hello **Automobile price data (Raw)** dataset toohello input port of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="02cb8-188">![Adicione a tela de experimento hello "Selecionar colunas no conjunto de dados" módulo toohello e conectá-lo][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-188">![Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="02cb8-189">***Adicione a tela de experimento hello "Selecionar colunas no conjunto de dados" módulo toohello e conectá-lo***</span><span class="sxs-lookup"><span data-stu-id="02cb8-189">***Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it***</span></span>

3. <span data-ttu-id="02cb8-190">Clique em Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo e clique em **seletor de coluna iniciar** em Olá **propriedades** painel.</span><span class="sxs-lookup"><span data-stu-id="02cb8-190">Click hello [Select Columns in Dataset][select-columns] module and click **Launch column selector** in hello **Properties** pane.</span></span>

    - <span data-ttu-id="02cb8-191">Olá esquerda, clique em **com regras**</span><span class="sxs-lookup"><span data-stu-id="02cb8-191">On hello left, click **With rules**</span></span>
    - <span data-ttu-id="02cb8-192">Em **Começa com**, clique em **Todas as colunas**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="02cb8-193">Isso instrui [selecionar colunas no conjunto de dados] [ select-columns] toopass por meio de todas as colunas de saudação (exceto as colunas que estamos sobre tooexclude).</span><span class="sxs-lookup"><span data-stu-id="02cb8-193">This directs [Select Columns in Dataset][select-columns] toopass through all hello columns (except those columns we're about tooexclude).</span></span>
    - <span data-ttu-id="02cb8-194">Olá listas suspensas, selecione **excluir** e **nomes de coluna**e, em seguida, clique na caixa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-194">From hello drop-downs, select **Exclude** and **column names**, and then click inside hello text box.</span></span> <span data-ttu-id="02cb8-195">Uma lista de colunas é exibida.</span><span class="sxs-lookup"><span data-stu-id="02cb8-195">A list of columns is displayed.</span></span> <span data-ttu-id="02cb8-196">Selecione **perdas normalizadas**, e é adicionado toohello caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="02cb8-196">Select **normalized-losses**, and it's added toohello text box.</span></span>
    - <span data-ttu-id="02cb8-197">Clique no hello marca de seleção (Okey) botão tooclose Olá seletor de coluna (em Olá inferior direito).</span><span class="sxs-lookup"><span data-stu-id="02cb8-197">Click hello check mark (OK) button tooclose hello column selector (on hello lower-right).</span></span>

    <span data-ttu-id="02cb8-198">![Iniciar seletor de coluna hello e excluir coluna hello "perdas normalizadas"][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-198">![Launch hello column selector and exclude hello "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="02cb8-199">***Iniciar seletor de coluna hello e excluir coluna hello "perdas normalizadas"***</span><span class="sxs-lookup"><span data-stu-id="02cb8-199">***Launch hello column selector and exclude hello "normalized-losses" column***</span></span>

    <span data-ttu-id="02cb8-200">Painel de propriedades de saudação agora para **selecionar colunas no conjunto de dados** indica que passa por todas as colunas do conjunto de dados Olá exceto **perdas normalizadas**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-200">Now hello properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from hello dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="02cb8-201">![Painel de propriedades de saudação mostra que essa coluna hello "perdas normalizadas" foi excluída][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-201">![hello properties pane shows that hello "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="02cb8-202">***Painel de propriedades de saudação mostra que essa coluna hello "perdas normalizadas" foi excluída***</span><span class="sxs-lookup"><span data-stu-id="02cb8-202">***hello properties pane shows that hello "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="02cb8-203">Você pode adicionar um módulo de tooa comentário clicando duas vezes em módulo de saudação e a inserção de texto.</span><span class="sxs-lookup"><span data-stu-id="02cb8-203">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="02cb8-204">Isso pode ajudá-lo a ver rapidamente quais módulo hello está fazendo sua experiência.</span><span class="sxs-lookup"><span data-stu-id="02cb8-204">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="02cb8-205">Nesse caso clique duas vezes em Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo e tipo hello comentário "Excluir normalizado perdas."</span><span class="sxs-lookup"><span data-stu-id="02cb8-205">In this case double-click hello [Select Columns in Dataset][select-columns] module and type hello comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="02cb8-206">![Clique duas vezes em um módulo tooadd um comentário][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-206">![Double-click a module tooadd a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="02cb8-207">***Clique duas vezes em um módulo tooadd um comentário***</span><span class="sxs-lookup"><span data-stu-id="02cb8-207">***Double-click a module tooadd a comment***</span></span>

3. <span data-ttu-id="02cb8-208">Saudação de arrastar [limpar dados ausentes] [ clean-missing-data] toohello módulo experimentar tela e conectá-lo toohello [selecionar colunas no conjunto de dados] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-208">Drag hello [Clean Missing Data][clean-missing-data] module toohello experiment canvas and connect it toohello [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="02cb8-209">Em Olá **propriedades** painel, selecione **remover toda a linha** em **modo de limpeza**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-209">In hello **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="02cb8-210">Isso instrui [limpar dados ausentes] [ clean-missing-data] tooclean dados de saudação removendo linhas com valores ausentes.</span><span class="sxs-lookup"><span data-stu-id="02cb8-210">This directs [Clean Missing Data][clean-missing-data] tooclean hello data by removing rows that have any missing values.</span></span> <span data-ttu-id="02cb8-211">Clique duas vezes no módulo hello e digite o comentário hello "Remover linhas de valor ausente".</span><span class="sxs-lookup"><span data-stu-id="02cb8-211">Double-click hello module and type hello comment "Remove missing value rows."</span></span>

    <span data-ttu-id="02cb8-212">![Definir o modo de limpeza de saudação muito "remover toda a linha" para o módulo de "Limpar dados ausentes" hello][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-212">![Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="02cb8-213">***Definir o modo de limpeza de saudação muito "remover toda a linha" para o módulo de "Limpar dados ausentes" hello***</span><span class="sxs-lookup"><span data-stu-id="02cb8-213">***Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="02cb8-214">Executar o teste de saudação clicando **executar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="02cb8-214">Run hello experiment by clicking **RUN** at hello bottom of hello page.</span></span>

    <span data-ttu-id="02cb8-215">Quando experimento Olá concluiu a execução, todos os módulos de saudação tem tooindicate uma marca de seleção verde que eles foi concluídos com êxito.</span><span class="sxs-lookup"><span data-stu-id="02cb8-215">When hello experiment has finished running, all hello modules have a green check mark tooindicate that they finished successfully.</span></span> <span data-ttu-id="02cb8-216">Observe também Olá **terminar execução** status no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-216">Notice also hello **Finished running** status in hello upper-right corner.</span></span>

<span data-ttu-id="02cb8-217">![Depois de executá-lo, experimento Olá deve ser semelhante este][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="02cb8-217">![After running it, hello experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="02cb8-218">
***Depois de executá-lo, experimento Olá deve ser semelhante este***</span><span class="sxs-lookup"><span data-stu-id="02cb8-218">
***After running it, hello experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="02cb8-219">Por que executamos experimento Olá agora?</span><span class="sxs-lookup"><span data-stu-id="02cb8-219">Why did we run hello experiment now?</span></span> <span data-ttu-id="02cb8-220">Por experiência de saudação em execução, definições de coluna Olá para nossos dados passam de conjunto de dados hello, por meio de saudação [selecionar colunas no conjunto de dados] [ select-columns] módulo e por meio de saudação [limpar dados ausentes] [ clean-missing-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-220">By running hello experiment, hello column definitions for our data pass from hello dataset, through hello [Select Columns in Dataset][select-columns] module, and through hello [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="02cb8-221">Isso significa que todos os módulos nos conectamos muito[limpar dados ausentes] [ clean-missing-data] também terá essas mesmas informações.</span><span class="sxs-lookup"><span data-stu-id="02cb8-221">This means that any modules we connect too[Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="02cb8-222">Tudo o que fizemos experimento Olá toothis ponto é dados saudação normal.</span><span class="sxs-lookup"><span data-stu-id="02cb8-222">All we have done in hello experiment up toothis point is clean hello data.</span></span> <span data-ttu-id="02cb8-223">O conjunto de dados do tooview Olá limpo, clique em Olá deixado porta de saída de hello [limpar dados ausentes] [ clean-missing-data] módulo e selecione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-223">If you want tooview hello cleaned dataset, click hello left output port of hello [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="02cb8-224">Observe que Olá **perdas normalizadas** coluna não é mais incluída e não existem valores ausentes.</span><span class="sxs-lookup"><span data-stu-id="02cb8-224">Notice that hello **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="02cb8-225">Agora que os dados saudação estão limpas, estamos toospecify pronto quais recursos nós vamos toouse no modelo de previsão de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-225">Now that hello data is clean, we're ready toospecify what features we're going toouse in hello predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="02cb8-226">Etapa 3: Definir recursos</span><span class="sxs-lookup"><span data-stu-id="02cb8-226">Step 3: Define features</span></span>

<span data-ttu-id="02cb8-227">No aprendizado de máquina, *recursos* são propriedades individuais mensuráveis de algo em que você está interessado.</span><span class="sxs-lookup"><span data-stu-id="02cb8-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="02cb8-228">Em nosso conjunto de dados, cada linha representa um automóvel e cada coluna é um recurso desse automóvel.</span><span class="sxs-lookup"><span data-stu-id="02cb8-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="02cb8-229">Localizando um bom conjunto de recursos para criar um modelo de previsão requer conhecimento sobre o problema de saudação e experimentação desejadas toosolve.</span><span class="sxs-lookup"><span data-stu-id="02cb8-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about hello problem you want toosolve.</span></span> <span data-ttu-id="02cb8-230">Alguns recursos são melhores para prever um destino de saudação que outros.</span><span class="sxs-lookup"><span data-stu-id="02cb8-230">Some features are better for predicting hello target than others.</span></span> <span data-ttu-id="02cb8-231">Além disso, alguns recursos têm uma forte correlação com outros recursos e podem ser removidos.</span><span class="sxs-lookup"><span data-stu-id="02cb8-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="02cb8-232">Por exemplo, mpg cidade e estrada mpg estão intimamente relacionados podemos manter uma e remover outros Olá sem afetar significativamente a previsão de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove hello other without significantly affecting hello prediction.</span></span>

<span data-ttu-id="02cb8-233">Vamos criar um modelo que usa um subconjunto de recursos de saudação em nosso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="02cb8-233">Let's build a model that uses a subset of hello features in our dataset.</span></span> <span data-ttu-id="02cb8-234">Volte mais tarde e selecionar recursos diferentes, execute novamente o teste de saudação e consulte se você obter resultados melhores.</span><span class="sxs-lookup"><span data-stu-id="02cb8-234">You can come back later and select different features, run hello experiment again, and see if you get better results.</span></span> <span data-ttu-id="02cb8-235">Mas toostart, vamos tentar Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="02cb8-235">But toostart, let's try hello following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="02cb8-236">Arraste outro [selecionar colunas no conjunto de dados] [ select-columns] toohello módulo experimentar a tela.</span><span class="sxs-lookup"><span data-stu-id="02cb8-236">Drag another [Select Columns in Dataset][select-columns] module toohello experiment canvas.</span></span> <span data-ttu-id="02cb8-237">Conecte-se a saudação à esquerda a porta de saída de hello [limpar dados ausentes] [ clean-missing-data] entrada do módulo toohello de saudação [selecionar colunas no conjunto de dados] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-237">Connect hello left output port of hello [Clean Missing Data][clean-missing-data] module toohello input of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="02cb8-238">![Conecte-se o módulo de "Limpar dados ausentes" hello "Selecionar colunas no conjunto de dados" módulo toohello][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-238">![Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="02cb8-239">***Conecte-se o módulo de "Limpar dados ausentes" hello "Selecionar colunas no conjunto de dados" módulo toohello***</span><span class="sxs-lookup"><span data-stu-id="02cb8-239">***Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="02cb8-240">Clique duas vezes no módulo hello e digite "Selecionar recursos para previsão."</span><span class="sxs-lookup"><span data-stu-id="02cb8-240">Double-click hello module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="02cb8-241">Clique em **seletor de coluna iniciar** em Olá **propriedades** painel.</span><span class="sxs-lookup"><span data-stu-id="02cb8-241">Click **Launch column selector** in hello **Properties** pane.</span></span>

3. <span data-ttu-id="02cb8-242">Clique em **Com regras**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-242">Click **With rules**.</span></span>

4. <span data-ttu-id="02cb8-243">Em **Começa com**, clique em **Nenhuma coluna**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="02cb8-244">Na linha de filtro hello, selecione **incluir** e **nomes de coluna** e selecione a lista de nomes de coluna na caixa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-244">In hello filter row, select **Include** and **column names** and select our list of column names in hello text box.</span></span> <span data-ttu-id="02cb8-245">Isso instrui Olá módulo toonot a passagem de todas as colunas (recursos) exceto Olá aqueles que especificamos.</span><span class="sxs-lookup"><span data-stu-id="02cb8-245">This directs hello module toonot pass through any columns (features) except hello ones that we specify.</span></span>

5. <span data-ttu-id="02cb8-246">Clique o botão de marca de seleção (Okey) hello.</span><span class="sxs-lookup"><span data-stu-id="02cb8-246">Click hello check mark (OK) button.</span></span>

    <span data-ttu-id="02cb8-247">![Selecione Olá colunas (recursos) tooinclude na previsão Olá][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-247">![Select hello columns (features) tooinclude in hello prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="02cb8-248">***Selecione Olá colunas (recursos) tooinclude na previsão Olá***</span><span class="sxs-lookup"><span data-stu-id="02cb8-248">***Select hello columns (features) tooinclude in hello prediction***</span></span>

<span data-ttu-id="02cb8-249">Isso produz um conjunto de dados filtrado que contém apenas recursos Olá que queremos toohello toopass usaremos na próxima etapa de saudação do algoritmo de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="02cb8-249">This produces a filtered dataset containing only hello features we want toopass toohello learning algorithm we'll use in hello next step.</span></span> <span data-ttu-id="02cb8-250">Posteriormente, é possível retornar e tentar novamente com uma seleção diferente de recursos.</span><span class="sxs-lookup"><span data-stu-id="02cb8-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="02cb8-251">Etapa 4: Escolher e aplicar um algoritmo de aprendizado</span><span class="sxs-lookup"><span data-stu-id="02cb8-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="02cb8-252">Agora que os dados de saudação estiverem prontos, criar um modelo de previsão consiste em treinamento e teste.</span><span class="sxs-lookup"><span data-stu-id="02cb8-252">Now that hello data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="02cb8-253">Vamos usar nosso modelo de saudação do tootrain de dados e, em seguida, nós o testaremos Olá modelo toosee proximidade é toopredict capaz de preços.</span><span class="sxs-lookup"><span data-stu-id="02cb8-253">We'll use our data tootrain hello model, and then we'll test hello model toosee how closely it's able toopredict prices.</span></span>
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

<span data-ttu-id="02cb8-254">*Classificação* e *regressão* são dois tipos de técnicas de algoritmo de machine learning supervisionado.</span><span class="sxs-lookup"><span data-stu-id="02cb8-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="02cb8-255">A classificação prevê uma resposta de um conjunto definido de categorias, como uma cor (vermelha, azul ou verde).</span><span class="sxs-lookup"><span data-stu-id="02cb8-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="02cb8-256">A regressão é usada toopredict um número.</span><span class="sxs-lookup"><span data-stu-id="02cb8-256">Regression is used toopredict a number.</span></span>

<span data-ttu-id="02cb8-257">Como desejamos toopredict preço, que é um número, vamos usar um algoritmo de regressão.</span><span class="sxs-lookup"><span data-stu-id="02cb8-257">Because we want toopredict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="02cb8-258">Neste exemplo, usaremos um modelo simples de *regressão linear*.</span><span class="sxs-lookup"><span data-stu-id="02cb8-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="02cb8-259">Se você quiser toolearn mais informações sobre tipos diferentes de algoritmos de aprendizado de máquina e quando toouse-los, você pode exibir vídeo primeiro Olá no hello ciência de dados para a série de iniciantes [Olá cinco perguntas respostas de ciência de dados](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="02cb8-259">If you want toolearn more about different types of machine learning algorithms and when toouse them, you might view hello first video in hello Data Science for Beginners series, [hello five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="02cb8-260">Você também poderá examinar Olá infográfico [Noções básicas com exemplos de algoritmo de aprendizado de máquina](machine-learning-basics-infographic-with-algorithm-examples.md), ou check-out Olá [roteiro do algoritmo de aprendizado de máquina](machine-learning-algorithm-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="02cb8-260">You might also look at hello infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out hello [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="02cb8-261">Treinamos modelo hello, dando a ele um conjunto de dados que inclui o preço de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-261">We train hello model by giving it a set of data that includes hello price.</span></span> <span data-ttu-id="02cb8-262">modelo de saudação examina dados saudação e procure correlações entre os recursos do exemplo um automóvel e seu preço.</span><span class="sxs-lookup"><span data-stu-id="02cb8-262">hello model scans hello data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="02cb8-263">Em seguida, nós o testaremos modelo Olá - vamos dar a ele um conjunto de recursos para automóveis com que estamos familiarizados e veja como fechar modelo Olá vem preço conhecidos do toopredicting hello.</span><span class="sxs-lookup"><span data-stu-id="02cb8-263">Then we'll test hello model - we'll give it a set of features for automobiles we're familiar with and see how close hello model comes toopredicting hello known price.</span></span>

<span data-ttu-id="02cb8-264">Vamos usar nossos dados de treinamento de modelo hello e testá-lo ao dividir dados saudação em conjuntos de dados de teste e treinamento separado.</span><span class="sxs-lookup"><span data-stu-id="02cb8-264">We'll use our data for both training hello model and testing it by splitting hello data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="02cb8-265">Selecione e arraste Olá [dividir dados] [ split] toohello módulo experimentar tela e conectá-lo toohello última [selecionar colunas no conjunto de dados] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-265">Select and drag hello [Split Data][split] module toohello experiment canvas and connect it toohello last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="02cb8-266">Clique em Olá [dividir dados] [ split] módulo tooselect-lo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-266">Click hello [Split Data][split] module tooselect it.</span></span> <span data-ttu-id="02cb8-267">Localize Olá **fração de linhas na Olá primeiro conjunto de dados de saída** (no hello **propriedades** toohello painel à direita da tela de saudação) e defina-a como too0.75.</span><span class="sxs-lookup"><span data-stu-id="02cb8-267">Find hello **Fraction of rows in hello first output dataset** (in hello **Properties** pane toohello right of hello canvas) and set it too0.75.</span></span> <span data-ttu-id="02cb8-268">Dessa forma, vamos usar 75 por cento Olá tootrain saudação do modelo de dados e reter 25% para teste (mais tarde, você pode experimentar diferentes porcentagens de uso).</span><span class="sxs-lookup"><span data-stu-id="02cb8-268">This way, we'll use 75 percent of hello data tootrain hello model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="02cb8-269">![Olá conjunto dividir fração de hello "Dividir dados" módulo too0.75][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-269">![Set hello split fraction of hello "Split Data" module too0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="02cb8-270">***Olá conjunto dividir fração de hello "Dividir dados" módulo too0.75***</span><span class="sxs-lookup"><span data-stu-id="02cb8-270">***Set hello split fraction of hello "Split Data" module too0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="02cb8-271">Alterando Olá **semente aleatória** parâmetro, você pode produzir diferentes amostras aleatórias para treinamento e teste.</span><span class="sxs-lookup"><span data-stu-id="02cb8-271">By changing hello **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="02cb8-272">Este parâmetro controla a propagação do gerador de número pseudoaleatório Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="02cb8-272">This parameter controls hello seeding of hello pseudo-random number generator.</span></span>

2. <span data-ttu-id="02cb8-273">Execute teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-273">Run hello experiment.</span></span> <span data-ttu-id="02cb8-274">Quando é executado experimento hello, Olá [selecionar colunas no conjunto de dados] [ select-columns] e [dividir dados] [ split] módulos passam toohello de definições de coluna módulos que incluiremos lado.</span><span class="sxs-lookup"><span data-stu-id="02cb8-274">When hello experiment is run, hello [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions toohello modules we'll be adding next.</span></span>  

3. <span data-ttu-id="02cb8-275">Olá tooselect aprendizado algoritmo, expanda Olá **aprendizado de máquina** categoria no hello módulo paleta toohello à esquerda da saudação tela e, em seguida, expanda **inicializar modelo**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-275">tooselect hello learning algorithm, expand hello **Machine Learning** category in hello module palette toohello left of hello canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="02cb8-276">Isso exibe várias categorias de módulos que podem ser algoritmos de aprendizado de máquina tooinitialize usado.</span><span class="sxs-lookup"><span data-stu-id="02cb8-276">This displays several categories of modules that can be used tooinitialize machine learning algorithms.</span></span> <span data-ttu-id="02cb8-277">Para esse teste, selecione Olá [Regressão Linear] [ linear-regression] módulo em Olá **regressão** categoria e arraste-a tela de experimento toohello.</span><span class="sxs-lookup"><span data-stu-id="02cb8-277">For this experiment, select hello [Linear Regression][linear-regression] module under hello **Regression** category, and drag it toohello experiment canvas.</span></span>
<span data-ttu-id="02cb8-278">(Você também pode encontrar hello módulo digitando "regressão linear" na caixa de pesquisa de paleta hello.)</span><span class="sxs-lookup"><span data-stu-id="02cb8-278">(You can also find hello module by typing "linear regression" in hello palette Search box.)</span></span>

4. <span data-ttu-id="02cb8-279">Localizar e arraste Olá [treinar modelo] [ train-model] toohello módulo experimentar a tela.</span><span class="sxs-lookup"><span data-stu-id="02cb8-279">Find and drag hello [Train Model][train-model] module toohello experiment canvas.</span></span> <span data-ttu-id="02cb8-280">Conecte a saída de saudação do hello [Regressão Linear] [ linear-regression] entrada de saudação à esquerda do módulo toohello [treinar modelo] [ train-model] módulo e conecte-se Olá treinamento de saída de dados (porta da esquerda) da saudação [dividir dados] [ split] entrada à direita do módulo toohello de saudação [treinar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-280">Connect hello output of hello [Linear Regression][linear-regression] module toohello left input of hello [Train Model][train-model] module, and connect hello training data output (left port) of hello [Split Data][split] module toohello right input of hello [Train Model][train-model] module.</span></span>

    <span data-ttu-id="02cb8-281">![Conecte-se hello "Modelo de treinamento" módulo tooboth hello "Regressão Linear" e "Dados de divisão" módulos][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-281">![Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="02cb8-282">***Conecte-se hello "Modelo de treinamento" módulo tooboth hello "Regressão Linear" e "Dados de divisão" módulos***</span><span class="sxs-lookup"><span data-stu-id="02cb8-282">***Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="02cb8-283">Clique em Olá [treinar modelo] [ train-model] módulo, clique em **seletor de coluna iniciar** em hello **propriedades** painel e, em seguida, selecione Olá **preço** coluna.</span><span class="sxs-lookup"><span data-stu-id="02cb8-283">Click hello [Train Model][train-model] module, click **Launch column selector** in hello **Properties** pane, and then select hello **price** column.</span></span> <span data-ttu-id="02cb8-284">Este é o valor de saudação nosso modelo é toopredict contínuo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-284">This is hello value that our model is going toopredict.</span></span>

    <span data-ttu-id="02cb8-285">Selecione Olá **preço** coluna no seletor de coluna hello, movendo-os de saudação **colunas disponíveis** lista toohello **colunas selecionadas** lista.</span><span class="sxs-lookup"><span data-stu-id="02cb8-285">You select hello **price** column in hello column selector by moving it from hello **Available columns** list toohello **Selected columns** list.</span></span>

    <span data-ttu-id="02cb8-286">![Selecionar coluna de preço Olá para o módulo de "Modelo de treinamento" hello][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-286">![Select hello price column for hello "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="02cb8-287">***Selecionar coluna de preço Olá para o módulo de "Modelo de treinamento" hello***</span><span class="sxs-lookup"><span data-stu-id="02cb8-287">***Select hello price column for hello "Train Model" module***</span></span>

6. <span data-ttu-id="02cb8-288">Execute teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-288">Run hello experiment.</span></span>

<span data-ttu-id="02cb8-289">Agora temos um modelo de regressão treinado que pode ser usado tooscore novos dados automóvel toomake preço previsões.</span><span class="sxs-lookup"><span data-stu-id="02cb8-289">We now have a trained regression model that can be used tooscore new automobile data toomake price predictions.</span></span>

<span data-ttu-id="02cb8-290">![Depois de executar, experimento Olá agora deve ser semelhante a este][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="02cb8-290">![After running, hello experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="02cb8-291">
***Depois de executar, experimento Olá agora deve ser semelhante a este***</span><span class="sxs-lookup"><span data-stu-id="02cb8-291">
***After running, hello experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="02cb8-292">Etapa 5: Prever novos preços de automóveis</span><span class="sxs-lookup"><span data-stu-id="02cb8-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="02cb8-293">Agora que nós já treinar o modelo de saudação usando 75% de nossos dados, podemos usar isso tooscore Olá outros 25 por cento de saudação dados toosee bem como funções de nosso modelo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-293">Now that we've trained hello model using 75 percent of our data, we can use it tooscore hello other 25 percent of hello data toosee how well our model functions.</span></span>

1. <span data-ttu-id="02cb8-294">Localizar e arraste Olá [modelo de pontuação] [ score-model] toohello módulo experimentar a tela.</span><span class="sxs-lookup"><span data-stu-id="02cb8-294">Find and drag hello [Score Model][score-model] module toohello experiment canvas.</span></span> <span data-ttu-id="02cb8-295">Conecte a saída de saudação do hello [treinar modelo] [ train-model] toohello do módulo à esquerda de porta de entrada de [modelo de pontuação][score-model].</span><span class="sxs-lookup"><span data-stu-id="02cb8-295">Connect hello output of hello [Train Model][train-model] module toohello left input port of [Score Model][score-model].</span></span> <span data-ttu-id="02cb8-296">Conecte Olá teste dados saída (porta à direita) da saudação [dividir dados] [ split] toohello do módulo à direita de porta de entrada [modelo de pontuação][score-model].</span><span class="sxs-lookup"><span data-stu-id="02cb8-296">Connect hello test data output (right port) of hello [Split Data][split] module toohello right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="02cb8-297">![Conecte-se hello "Modelo de pontuação" módulo tooboth hello "Modelo de treinamento" e "Dados de divisão" módulos][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-297">![Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="02cb8-298">***Conecte-se hello "Modelo de pontuação" módulo tooboth hello "Modelo de treinamento" e "Dados de divisão" módulos***</span><span class="sxs-lookup"><span data-stu-id="02cb8-298">***Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="02cb8-299">Executar teste hello e exibir saída de saudação do hello [modelo de pontuação] [ score-model] módulo (clique a porta de saída Olá [modelo de pontuação] [ score-model] e selecione **Visualizar**).</span><span class="sxs-lookup"><span data-stu-id="02cb8-299">Run hello experiment and view hello output from hello [Score Model][score-model] module (click hello output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="02cb8-300">Olá saída mostra Olá valores previstos para preço e Olá valores conhecidos de dados de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-300">hello output shows hello predicted values for price and hello known values from hello test data.</span></span>  

    <span data-ttu-id="02cb8-301">![Saída do módulo de "Modelo de pontuação" hello][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="02cb8-301">![Output of hello "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="02cb8-302">***Saída do módulo de "Modelo de pontuação" hello***</span><span class="sxs-lookup"><span data-stu-id="02cb8-302">***Output of hello "Score Model" module***</span></span>

3. <span data-ttu-id="02cb8-303">Por fim, podemos testar qualidade Olá dos resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-303">Finally, we test hello quality of hello results.</span></span> <span data-ttu-id="02cb8-304">Selecione e arraste Olá [avaliar modelo] [ evaluate-model] toohello módulo experiências de tela e conecte a saída Olá de saudação [modelo de pontuação] [ score-model] módulo toohello deixado entrada de [avaliar modelo][evaluate-model].</span><span class="sxs-lookup"><span data-stu-id="02cb8-304">Select and drag hello [Evaluate Model][evaluate-model] module toohello experiment canvas, and connect hello output of hello [Score Model][score-model] module toohello left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="02cb8-305">Existem duas portas de entrada hello [avaliar modelo] [ evaluate-model] módulo porque ele pode ser usado toocompare dois modelos lado a lado.</span><span class="sxs-lookup"><span data-stu-id="02cb8-305">There are two input ports on hello [Evaluate Model][evaluate-model] module because it can be used toocompare two models side by side.</span></span> <span data-ttu-id="02cb8-306">Posteriormente, você pode adicionar outro teste de toohello do algoritmo e usar [avaliar modelo] [ evaluate-model] toosee que fornece resultados melhores.</span><span class="sxs-lookup"><span data-stu-id="02cb8-306">Later, you can add another algorithm toohello experiment and use [Evaluate Model][evaluate-model] toosee which one gives better results.</span></span>

4. <span data-ttu-id="02cb8-307">Execute teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-307">Run hello experiment.</span></span>

<span data-ttu-id="02cb8-308">saída de hello tooview de saudação [avaliar modelo] [ evaluate-model] módulo, clique em Olá porta de saída e, em seguida, selecione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="02cb8-308">tooview hello output from hello [Evaluate Model][evaluate-model] module, click hello output port, and then select **Visualize**.</span></span>

<span data-ttu-id="02cb8-309">![Resultados da avaliação de experimento Olá][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="02cb8-309">![Evaluation results for hello experiment][evaluation-results]
</span></span><br/><span data-ttu-id="02cb8-310">
***Resultados da avaliação de experimento Olá***</span><span class="sxs-lookup"><span data-stu-id="02cb8-310">
***Evaluation results for hello experiment***</span></span>

<span data-ttu-id="02cb8-311">Olá estatísticas a seguir é mostrada para nosso modelo:</span><span class="sxs-lookup"><span data-stu-id="02cb8-311">hello following statistics are shown for our model:</span></span>

- <span data-ttu-id="02cb8-312">**Erro de média absoluta** (MAE): Olá média dos erros absolutos (um *erro* Olá diferença entre Olá previsto valor e o valor real de saudação).</span><span class="sxs-lookup"><span data-stu-id="02cb8-312">**Mean Absolute Error** (MAE): hello average of absolute errors (an *error* is hello difference between hello predicted value and hello actual value).</span></span>
- <span data-ttu-id="02cb8-313">**Erro ao quadrado da raiz significa** (RMSE): raiz quadrada de saudação da média de saudação de erros ao quadrado de previsões feitas no conjunto de dados de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-313">**Root Mean Squared Error** (RMSE): hello square root of hello average of squared errors of predictions made on hello test dataset.</span></span>
- <span data-ttu-id="02cb8-314">**Erro absoluto relativo**: Olá média de diferença absoluta do erros absoluto toohello relativa entre os valores reais e Olá média de todos os valores reais.</span><span class="sxs-lookup"><span data-stu-id="02cb8-314">**Relative Absolute Error**: hello average of absolute errors relative toohello absolute difference between actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="02cb8-315">**Erro ao quadrado relativo**: diferença entre os valores reais hello e média de saudação de todos os valores reais de quadrado da média de saudação do toohello de erros ao quadrado relativo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-315">**Relative Squared Error**: hello average of squared errors relative toohello squared difference between hello actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="02cb8-316">**Coeficiente de determinação**: Olá também conhecido como **R quadrado valor**, essa é uma métrica estatística que indica como um modelo se ajusta a dados saudação.</span><span class="sxs-lookup"><span data-stu-id="02cb8-316">**Coefficient of Determination**: Also known as hello **R squared value**, this is a statistical metric indicating how well a model fits hello data.</span></span>

<span data-ttu-id="02cb8-317">Para cada erro Olá estatísticas, menor são melhor.</span><span class="sxs-lookup"><span data-stu-id="02cb8-317">For each of hello error statistics, smaller is better.</span></span> <span data-ttu-id="02cb8-318">Um valor menor indica que o previsões hello mais de perto correspondem os valores reais hello.</span><span class="sxs-lookup"><span data-stu-id="02cb8-318">A smaller value indicates that hello predictions more closely match hello actual values.</span></span> <span data-ttu-id="02cb8-319">Para **coeficiente de determinação**, hello mais próximo seu valor é tooone (1.0), melhores previsões de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="02cb8-319">For **Coefficient of Determination**, hello closer its value is tooone (1.0), hello better hello predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="02cb8-320">Experimento final</span><span class="sxs-lookup"><span data-stu-id="02cb8-320">Final experiment</span></span>

<span data-ttu-id="02cb8-321">teste final Olá deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="02cb8-321">hello final experiment should look something like this:</span></span>

<span data-ttu-id="02cb8-322">![teste final Olá][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="02cb8-322">![hello final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="02cb8-323">
***teste final Olá***</span><span class="sxs-lookup"><span data-stu-id="02cb8-323">
***hello final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="02cb8-324">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="02cb8-324">Next steps</span></span>

<span data-ttu-id="02cb8-325">Agora que você concluiu o tutorial de aprendizado de máquina primeiro hello e tiver sua experiência configurada, você pode continuar tooimprove modelo de saudação e, em seguida, implantá-lo como um serviço web de previsão.</span><span class="sxs-lookup"><span data-stu-id="02cb8-325">Now that you've completed hello first machine learning tutorial and have your experiment set up, you can continue tooimprove hello model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="02cb8-326">**Iterar modelo de saudação do tootry tooimprove** -por exemplo, você pode alterar os recursos de saudação usar em sua previsão.</span><span class="sxs-lookup"><span data-stu-id="02cb8-326">**Iterate tootry tooimprove hello model** - For example, you can change hello features you use in your prediction.</span></span> <span data-ttu-id="02cb8-327">Ou você pode modificar as propriedades de saudação do hello [Regressão Linear] [ linear-regression] algoritmo ou tente um algoritmo diferente completamente.</span><span class="sxs-lookup"><span data-stu-id="02cb8-327">Or you can modify hello properties of hello [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="02cb8-328">Até mesmo, você pode adicionar vários computadores ao mesmo tempo de experiência de tooyour de algoritmos de aprendizado e comparar duas delas usando Olá [avaliar modelo] [ evaluate-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="02cb8-328">You can even add multiple machine learning algorithms tooyour experiment at one time and compare two of them by using hello [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="02cb8-329">Para obter um exemplo de como toocompare vários modelos em uma única experiência, consulte [comparar Regressores](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) em Olá [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="02cb8-329">For an example of how toocompare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="02cb8-330">toocopy qualquer iteração de sua experiência, use Olá **Salvar como** botão final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="02cb8-330">toocopy any iteration of your experiment, use hello **SAVE AS** button at hello bottom of hello page.</span></span> <span data-ttu-id="02cb8-331">Você pode ver todas as iterações de saudação da sua experiência clicando **exibir o histórico de execução** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="02cb8-331">You can see all hello iterations of your experiment by clicking **VIEW RUN HISTORY** at hello bottom of hello page.</span></span> <span data-ttu-id="02cb8-332">Para obter mais detalhes, consulte [Gerenciar iterações do experimento no Azure Machine Learning Studio][runhistory].</span><span class="sxs-lookup"><span data-stu-id="02cb8-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="02cb8-333">**Implantar o modelo hello como um serviço web de previsão** - quando você estiver satisfeito com seu modelo, você pode implantá-lo como um toobe de serviço da web usado preços de automóvel toopredict usando novos dados.</span><span class="sxs-lookup"><span data-stu-id="02cb8-333">**Deploy hello model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service toobe used toopredict automobile prices by using new data.</span></span> <span data-ttu-id="02cb8-334">Consulte [Implantar um serviço Web do Azure Machine Learning][publish] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="02cb8-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="02cb8-335">Deseja toolearn mais?</span><span class="sxs-lookup"><span data-stu-id="02cb8-335">Want toolearn more?</span></span> <span data-ttu-id="02cb8-336">Para obter uma explicação mais ampla e detalhada do processo de saudação de criação, treinamento, pontuação e implantando um modelo, consulte [desenvolver uma solução de previsão usando o aprendizado de máquina do Azure][walkthrough].</span><span class="sxs-lookup"><span data-stu-id="02cb8-336">For a more extensive and detailed walkthrough of hello process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
