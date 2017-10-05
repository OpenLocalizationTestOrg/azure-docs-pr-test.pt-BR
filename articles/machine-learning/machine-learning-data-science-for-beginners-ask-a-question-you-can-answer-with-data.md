---
title: "Fazer uma pergunta que os dados possam responder – problemas de ciência de dados – Azure Machine Learning | Microsoft Docs"
description: "Saiba como formular uma pergunta precisa de ciência de dados no Vídeo Ciência de Dados para Iniciantes 3. Inclui uma comparação das perguntas de classificação e regressão."
keywords: "problemas com ciência de dados, perguntas da ciência de dados, formular a pergunta, perguntas de regressão, perguntas de classificação, pergunta inteligente"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: 5b9501e3-9964-417a-8ffc-8913103da77b
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 0495dbab72024e504ae33d35f16a212a2084bc10
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="ask-a-question-you-can-answer-with-data"></a><span data-ttu-id="8e793-105">Fazer uma pergunta que você possa responder com dados</span><span class="sxs-lookup"><span data-stu-id="8e793-105">Ask a question you can answer with data</span></span>
## <a name="video-3-data-science-for-beginners-series"></a><span data-ttu-id="8e793-106">Vídeo 3: Série de ciência de dados para iniciantes</span><span class="sxs-lookup"><span data-stu-id="8e793-106">Video 3: Data Science for Beginners series</span></span>
<span data-ttu-id="8e793-107">Saiba como transformar um problema de ciência de dados em uma pergunta no Vídeo Ciência de Dados para Iniciantes 3.</span><span class="sxs-lookup"><span data-stu-id="8e793-107">Learn how to formulate a data science problem into a question in Data Science for Beginners video 3.</span></span> <span data-ttu-id="8e793-108">Esse vídeo inclui uma comparação de perguntas para os algoritmos de classificação e regressão.</span><span class="sxs-lookup"><span data-stu-id="8e793-108">This video includes a comparison of questions for classification and regression algorithms.</span></span>

<span data-ttu-id="8e793-109">Para aproveitar ao máximo da série, assista a todos os vídeos.</span><span class="sxs-lookup"><span data-stu-id="8e793-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="8e793-110">[Acessar a lista de vídeos](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="8e793-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="8e793-111">Outros vídeos nesta série</span><span class="sxs-lookup"><span data-stu-id="8e793-111">Other videos in this series</span></span>
<span data-ttu-id="8e793-112">*Ciência de dados para iniciantes* é uma breve introdução à ciência de dados em cinco vídeos curtos.</span><span class="sxs-lookup"><span data-stu-id="8e793-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="8e793-113">Vídeo 1: [As cinco perguntas que a ciência de dados responde](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min e 14 s)*</span><span class="sxs-lookup"><span data-stu-id="8e793-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="8e793-114">Vídeo 2: [Seus dados estão prontos para a ciência de dados?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="8e793-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="8e793-115">*(4 min 56 s)*</span><span class="sxs-lookup"><span data-stu-id="8e793-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="8e793-116">Video 3: Faça uma pergunta que você possa responder com dados</span><span class="sxs-lookup"><span data-stu-id="8e793-116">Video 3: Ask a question you can answer with data</span></span>
* <span data-ttu-id="8e793-117">Vídeo 4: [Preveja uma resposta com um modelo simples](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 s)*</span><span class="sxs-lookup"><span data-stu-id="8e793-117">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="8e793-118">Vídeo 5: [Copie o trabalho de outras pessoas para fazer a ciência de dados](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 s)*</span><span class="sxs-lookup"><span data-stu-id="8e793-118">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a><span data-ttu-id="8e793-119">Transcrição: Faça uma pergunta que você possa responder com dados</span><span class="sxs-lookup"><span data-stu-id="8e793-119">Transcript: Ask a question you can answer with data</span></span>
<span data-ttu-id="8e793-120">Bem-vindo ao terceiro vídeo da série "Ciência de dados para iniciantes."</span><span class="sxs-lookup"><span data-stu-id="8e793-120">Welcome to the third video in the series "Data Science for Beginners."</span></span>  

<span data-ttu-id="8e793-121">Nele, você obterá algumas dicas para formular uma pergunta que possa responder com dados.</span><span class="sxs-lookup"><span data-stu-id="8e793-121">In this one, you'll get some tips for formulating a question you can answer with data.</span></span>

<span data-ttu-id="8e793-122">Você pode obter mais desse vídeo se primeiro observar dois vídeos anteriores na série: "As cinco perguntas que a ciência de dados pode responder" e "Seus dados estão prontos para a ciência de dados?"</span><span class="sxs-lookup"><span data-stu-id="8e793-122">You might get more out of this video, if you first watch the two earlier videos in this series: "The 5 questions data science can answer" and "Is your data is ready for data science?"</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="8e793-123">Faça uma pergunta inteligente</span><span class="sxs-lookup"><span data-stu-id="8e793-123">Ask a sharp question</span></span>
<span data-ttu-id="8e793-124">Falamos sobre como a ciência de dados é o processo de usar nomes (também chamados de categorias ou rótulos) e números para prever uma resposta para uma pergunta.</span><span class="sxs-lookup"><span data-stu-id="8e793-124">We've talked about how data science is the process of using names (also called categories or labels) and numbers to predict an answer to a question.</span></span> <span data-ttu-id="8e793-125">Mas não pode ser uma pergunta qualquer; deve ser uma *pergunta inteligente.*</span><span class="sxs-lookup"><span data-stu-id="8e793-125">But it can't be just any question; it has to be a *sharp question.*</span></span>

<span data-ttu-id="8e793-126">Uma pergunta vaga não precisa ser respondida com um nome ou um número.</span><span class="sxs-lookup"><span data-stu-id="8e793-126">A vague question doesn't have to be answered with a name or a number.</span></span> <span data-ttu-id="8e793-127">Uma pergunta inteligente sim.</span><span class="sxs-lookup"><span data-stu-id="8e793-127">A sharp question must.</span></span>

<span data-ttu-id="8e793-128">Imagine que você encontrou uma lâmpada mágica com um gênio que responderá de verdade qualquer pergunta feita.</span><span class="sxs-lookup"><span data-stu-id="8e793-128">Imagine you found a magic lamp with a genie who will truthfully answer any question you ask.</span></span> <span data-ttu-id="8e793-129">Mas é um gênio mau e ele tentará tornar sua resposta o mais vaga e confusa que puder para se dar bem.</span><span class="sxs-lookup"><span data-stu-id="8e793-129">But it's a mischievous genie, and he'll try to make his answer as vague and confusing as he can get away with.</span></span> <span data-ttu-id="8e793-130">Você deseja forçá-lo com uma pergunta incontestável para que ele não possa fazer nada, exceto dizer o que você deseja saber.</span><span class="sxs-lookup"><span data-stu-id="8e793-130">You want to pin him down with a question so airtight that he can't help but tell you what you want to know.</span></span>

<span data-ttu-id="8e793-131">Se você fizesse uma pergunta vaga, como: "O que acontecerá com minhas ações?", o gênio poderia responder: "O preço mudará".</span><span class="sxs-lookup"><span data-stu-id="8e793-131">If you were to ask a vague question, like "What's going to happen with my stock?", the genie might answer, "The price will change".</span></span> <span data-ttu-id="8e793-132">É uma resposta sincera, mas não é muito útil.</span><span class="sxs-lookup"><span data-stu-id="8e793-132">That's a truthful answer, but it's not very helpful.</span></span>

<span data-ttu-id="8e793-133">Mas se fizesse uma pergunta direta, como: "Qual será o preço de venda de minhas ações na próxima semana?", o gênio não poderia fazer nada, exceto dar uma resposta específica e prever um preço de venda.</span><span class="sxs-lookup"><span data-stu-id="8e793-133">But if you were to ask a sharp question, like "What will my stock's sale price be next week?", the genie can't help but give you a specific answer and predict a sale price.</span></span>

## <a name="examples-of-your-answer-target-data"></a><span data-ttu-id="8e793-134">Exemplos de resposta: dados de destino</span><span class="sxs-lookup"><span data-stu-id="8e793-134">Examples of your answer: Target data</span></span>
<span data-ttu-id="8e793-135">Depois de formular sua pergunta, verifique para saber se você tem exemplos de resposta em seus dados.</span><span class="sxs-lookup"><span data-stu-id="8e793-135">Once you formulate your question, check to see whether you have examples of the answer in your data.</span></span>

<span data-ttu-id="8e793-136">Se nossa pergunta é "Qual será o preço de venda do meu estoque na próxima semana?",</span><span class="sxs-lookup"><span data-stu-id="8e793-136">If our question is "What will my stock's sale price be next week?"</span></span> <span data-ttu-id="8e793-137">temos que verificar se nossos dados incluem o histórico de preços de ações.</span><span class="sxs-lookup"><span data-stu-id="8e793-137">then we have to make sure our data includes the stock price history.</span></span>

<span data-ttu-id="8e793-138">Se nossa pergunta é "Qual carro em minha frota vai falhar primeiro?",</span><span class="sxs-lookup"><span data-stu-id="8e793-138">If our question is "Which car in my fleet is going to fail first?"</span></span> <span data-ttu-id="8e793-139">temos que verificar se nossos dados incluem informações sobre falhas anteriores.</span><span class="sxs-lookup"><span data-stu-id="8e793-139">then we have to make sure our data includes information about previous failures.</span></span>

![Dados de destino - exemplos de resposta.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

<span data-ttu-id="8e793-142">Esses exemplos de respostas são chamados de destino.</span><span class="sxs-lookup"><span data-stu-id="8e793-142">These examples of answers are called a target.</span></span> <span data-ttu-id="8e793-143">Um destino é o que estamos tentando prever sobre os futuros pontos de dados, seja uma categoria seja um número.</span><span class="sxs-lookup"><span data-stu-id="8e793-143">A target is what we are trying to predict about future data points, whether it's a category or a number.</span></span>

<span data-ttu-id="8e793-144">Se você não tiver nenhum dado de destino, precisará obter algum.</span><span class="sxs-lookup"><span data-stu-id="8e793-144">If you don't have any target data, you'll need to get some.</span></span> <span data-ttu-id="8e793-145">Você não conseguirá responder à sua pergunta sem ele.</span><span class="sxs-lookup"><span data-stu-id="8e793-145">You won't be able to answer your question without it.</span></span>

## <a name="reformulate-your-question"></a><span data-ttu-id="8e793-146">Reformular sua pergunta</span><span class="sxs-lookup"><span data-stu-id="8e793-146">Reformulate your question</span></span>
<span data-ttu-id="8e793-147">Às vezes, você pode reformular sua pergunta para obter uma resposta mais útil.</span><span class="sxs-lookup"><span data-stu-id="8e793-147">Sometimes you can reword your question to get a more useful answer.</span></span>

<span data-ttu-id="8e793-148">A pergunta "Estes dados são do ponto A ou B?"</span><span class="sxs-lookup"><span data-stu-id="8e793-148">The question "Is this data point A or B?"</span></span> <span data-ttu-id="8e793-149">prevê a categoria (ou nome ou rótulo) de algo.</span><span class="sxs-lookup"><span data-stu-id="8e793-149">predicts the category (or name or label) of something.</span></span> <span data-ttu-id="8e793-150">Para respondê-la, usamos um *algoritmo de classificação*.</span><span class="sxs-lookup"><span data-stu-id="8e793-150">To answer it, we use a *classification algorithm*.</span></span>

<span data-ttu-id="8e793-151">A pergunta "Quanto?"</span><span class="sxs-lookup"><span data-stu-id="8e793-151">The question "How much?"</span></span> <span data-ttu-id="8e793-152">ou "Quantos?"</span><span class="sxs-lookup"><span data-stu-id="8e793-152">or "How many?"</span></span> <span data-ttu-id="8e793-153">prevê uma quantia.</span><span class="sxs-lookup"><span data-stu-id="8e793-153">predicts an amount.</span></span> <span data-ttu-id="8e793-154">Para respondê-la, usamos um *algoritmo de regressão*.</span><span class="sxs-lookup"><span data-stu-id="8e793-154">To answer it we use a *regression algorithm*.</span></span>

<span data-ttu-id="8e793-155">Para ver como podemos transformar isso, vejamos a pergunta: "Qual notícia é mais interessante para este leitor?"</span><span class="sxs-lookup"><span data-stu-id="8e793-155">To see how we can transform these, let's look at the question, "Which news story is the most interesting to this reader?"</span></span> <span data-ttu-id="8e793-156">Solicita uma previsão de uma opção simples entre muitas possibilidades – em outras palavras, "É A, B, C ou D?"</span><span class="sxs-lookup"><span data-stu-id="8e793-156">It asks for a prediction of a single choice from many possibilities - in other words "Is this A or B or C or D?"</span></span> <span data-ttu-id="8e793-157">- e usaria um algoritmo de classificação.</span><span class="sxs-lookup"><span data-stu-id="8e793-157">- and would use a classification algorithm.</span></span>

<span data-ttu-id="8e793-158">Mas, essa pergunta poderá ser mais fácil de responder se você reformulá-la como: "O quanto interessante é cada história nesta lista para este leitor?"</span><span class="sxs-lookup"><span data-stu-id="8e793-158">But, this question may be easier to answer if you reword it as "How interesting is each story on this list to this reader?"</span></span> <span data-ttu-id="8e793-159">Agora, você pode dar a cada artigo uma pontuação numérica e será fácil identificar o artigo com a pontuação mais alta.</span><span class="sxs-lookup"><span data-stu-id="8e793-159">Now you can give each article a numerical score, and then it's easy to identify the highest-scoring article.</span></span> <span data-ttu-id="8e793-160">Isto é uma reformulação da pergunta de classificação em uma pergunta de regressão ou do tipo Quanto?</span><span class="sxs-lookup"><span data-stu-id="8e793-160">This is a rephrasing of the classification question into a regression question or How much?</span></span>

![Reformule sua pergunta.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

<span data-ttu-id="8e793-163">Como você faz uma pergunta é uma dica sobre qual algoritmo poderá dar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="8e793-163">How you ask a question is a clue to which algorithm can give you an answer.</span></span>

<span data-ttu-id="8e793-164">Você descobrirá que certas famílias de algoritmos - como aquelas em nosso exemplo de notícia - estão intimamente relacionadas.</span><span class="sxs-lookup"><span data-stu-id="8e793-164">You'll find that certain families of algorithms - like the ones in our news story example - are closely related.</span></span> <span data-ttu-id="8e793-165">Você pode reformular sua pergunta para usar o algoritmo que fornece a resposta mais útil.</span><span class="sxs-lookup"><span data-stu-id="8e793-165">You can reformulate your question to use the algorithm that gives you the most useful answer.</span></span>

<span data-ttu-id="8e793-166">Porém, o mais importante é fazer uma pergunta inteligente - a pergunta que você pode responder com dados.</span><span class="sxs-lookup"><span data-stu-id="8e793-166">But, most important, ask that sharp question - the question that you can answer with data.</span></span> <span data-ttu-id="8e793-167">E verifique se você tem os dados certos para respondê-la.</span><span class="sxs-lookup"><span data-stu-id="8e793-167">And be sure you have the right data to answer it.</span></span>

<span data-ttu-id="8e793-168">Falamos sobre alguns princípios básicos para fazer uma pergunta que você pode responder com dados.</span><span class="sxs-lookup"><span data-stu-id="8e793-168">We've talked about some basic principles for asking a question you can answer with data.</span></span>

<span data-ttu-id="8e793-169">Confira outros vídeos da série "Ciência de dados para iniciantes" no Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8e793-169">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e793-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8e793-170">Next steps</span></span>
* [<span data-ttu-id="8e793-171">Teste um primeiro experimento da ciência de dados com o Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="8e793-171">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* <span data-ttu-id="8e793-172">
            [Obtenha uma introdução ao Machine Learning no Microsoft Azure](machine-learning-what-is-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="8e793-172">[Get an introduction to Machine Learning on Microsoft Azure](machine-learning-what-is-machine-learning.md)</span></span>
