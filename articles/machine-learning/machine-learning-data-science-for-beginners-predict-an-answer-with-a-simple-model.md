---
title: "Prever uma resposta com um modelo simples de regressão – Azure Machine Learning | Microsoft Docs"
description: "Como criar um modelo simples de regressão para prever um preço no vídeo 4, Ciência de dados para iniciantes. Inclui uma regressão linear com os dados de destino."
keywords: "criar um modelo, modelo simples, previsão de preço, modelo simples de regressão"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 24df1823af2610a5111118f47e4cadbcfcc0eff1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a><span data-ttu-id="435b6-105">Prever uma resposta com um modelo simples</span><span class="sxs-lookup"><span data-stu-id="435b6-105">Predict an answer with a simple model</span></span>
## <a name="video-4-data-science-for-beginners-series"></a><span data-ttu-id="435b6-106">Vídeo 4: Série de ciência de dados para iniciantes</span><span class="sxs-lookup"><span data-stu-id="435b6-106">Video 4: Data Science for Beginners series</span></span>
<span data-ttu-id="435b6-107">Aprenda como criar um modelo simples de regressão para prever o preço de um diamante no vídeo 4, Ciência de dados para iniciantes.</span><span class="sxs-lookup"><span data-stu-id="435b6-107">Learn how to create a simple regression model to predict the price of a diamond in Data Science for Beginners video 4.</span></span> <span data-ttu-id="435b6-108">Vamos desenhar um modelo de regressão com dados de destino.</span><span class="sxs-lookup"><span data-stu-id="435b6-108">We'll draw a regression model with target data.</span></span>

<span data-ttu-id="435b6-109">Para aproveitar ao máximo da série, assista a todos os vídeos.</span><span class="sxs-lookup"><span data-stu-id="435b6-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="435b6-110">[Acessar a lista de vídeos](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="435b6-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="435b6-111">Outros vídeos nesta série</span><span class="sxs-lookup"><span data-stu-id="435b6-111">Other videos in this series</span></span>
<span data-ttu-id="435b6-112">*Ciência de dados para iniciantes* é uma breve introdução à ciência de dados em cinco vídeos curtos.</span><span class="sxs-lookup"><span data-stu-id="435b6-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="435b6-113">Vídeo 1: [As cinco perguntas que a ciência de dados responde](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min e 14 s)*</span><span class="sxs-lookup"><span data-stu-id="435b6-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="435b6-114">Vídeo 2: [Seus dados estão prontos para a ciência de dados?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="435b6-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="435b6-115">*(4 min 56 s)*</span><span class="sxs-lookup"><span data-stu-id="435b6-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="435b6-116">Video 3: [Faça uma pergunta que você possa responder com dados](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 s)*</span><span class="sxs-lookup"><span data-stu-id="435b6-116">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="435b6-117">Vídeo 4: Preveja uma resposta com um modelo simples</span><span class="sxs-lookup"><span data-stu-id="435b6-117">Video 4: Predict an answer with a simple model</span></span>
* <span data-ttu-id="435b6-118">Vídeo 5: [Copie o trabalho de outras pessoas para fazer a ciência de dados](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 s)*</span><span class="sxs-lookup"><span data-stu-id="435b6-118">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-predict-an-answer-with-a-simple-model"></a><span data-ttu-id="435b6-119">Transcrição: Preveja uma resposta com um modelo simples</span><span class="sxs-lookup"><span data-stu-id="435b6-119">Transcript: Predict an answer with a simple model</span></span>
<span data-ttu-id="435b6-120">Bem-vindos ao quarto vídeo da série "Ciência de dados para iniciantes".</span><span class="sxs-lookup"><span data-stu-id="435b6-120">Welcome to the fourth video in the "Data Science for Beginners" series.</span></span> <span data-ttu-id="435b6-121">Neste vídeo, vamos criar um modelo simples e fazer uma previsão.</span><span class="sxs-lookup"><span data-stu-id="435b6-121">In this one, we'll build a simple model and make a prediction.</span></span>

<span data-ttu-id="435b6-122">Um *modelo* é uma história simplificada sobre nossos dados.</span><span class="sxs-lookup"><span data-stu-id="435b6-122">A *model* is a simplified story about our data.</span></span> <span data-ttu-id="435b6-123">Mostrarei o que quero dizer.</span><span class="sxs-lookup"><span data-stu-id="435b6-123">I'll show you what I mean.</span></span>

## <a name="collect-relevant-accurate-connected-enough-data"></a><span data-ttu-id="435b6-124">Colete dados relevantes, precisos, conectados e suficientes</span><span class="sxs-lookup"><span data-stu-id="435b6-124">Collect relevant, accurate, connected, enough data</span></span>
<span data-ttu-id="435b6-125">Vamos supor que eu queira comprar um diamante.</span><span class="sxs-lookup"><span data-stu-id="435b6-125">Say I want to shop for a diamond.</span></span> <span data-ttu-id="435b6-126">Eu tenho um anel que pertencia a minha avó com um espaço para um diamante de 1,35 quilate, e eu quero ter uma ideia de quanto esse diamante custará.</span><span class="sxs-lookup"><span data-stu-id="435b6-126">I have a ring that belonged to my grandmother with a setting for a 1.35 carat diamond, and I want to get an idea of how much it will cost.</span></span> <span data-ttu-id="435b6-127">Levo um bloco de notas e uma caneta até a loja de joias e anoto o preço e o quilate de todos os diamantes em exposição.</span><span class="sxs-lookup"><span data-stu-id="435b6-127">I take a notepad and pen into the jewelry store, and I write down the price of all of the diamonds in the case and how much they weigh in carats.</span></span> <span data-ttu-id="435b6-128">Começando com o primeiro diamante: ele tem 1,01 quilate e custa $7.366.</span><span class="sxs-lookup"><span data-stu-id="435b6-128">Starting with the first diamond - it's 1.01 carats and $7,366.</span></span>

<span data-ttu-id="435b6-129">Agora eu faço isso para os outros diamantes na loja.</span><span class="sxs-lookup"><span data-stu-id="435b6-129">Now I go through and do this for all the other diamonds in the store.</span></span>

![Colunas de dados de diamante](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

<span data-ttu-id="435b6-131">Observe que a nossa lista tem duas colunas.</span><span class="sxs-lookup"><span data-stu-id="435b6-131">Notice that our list has two columns.</span></span> <span data-ttu-id="435b6-132">Cada coluna tem um atributo diferente - peso em quilate e preço - e cada linha é um único ponto de dados que representa um único diamante.</span><span class="sxs-lookup"><span data-stu-id="435b6-132">Each column has a different attribute - weight in carats and price - and each row is a single data point that represents a single diamond.</span></span>

<span data-ttu-id="435b6-133">Na verdade, criamos um pequeno conjunto de dados aqui; uma tabela.</span><span class="sxs-lookup"><span data-stu-id="435b6-133">We've actually created a small data set here - a table.</span></span> <span data-ttu-id="435b6-134">Observe que isso atende aos nossos critérios de qualidade:</span><span class="sxs-lookup"><span data-stu-id="435b6-134">Notice that it meets our criteria for quality:</span></span>

* <span data-ttu-id="435b6-135">Os dados são **relevantes** — o peso está definitivamente relacionado ao preço</span><span class="sxs-lookup"><span data-stu-id="435b6-135">The data is **relevant** - weight is definitely related to price</span></span>
* <span data-ttu-id="435b6-136">Eles são **precisos** — verificamos os preços que anotamos mais de uma vez</span><span class="sxs-lookup"><span data-stu-id="435b6-136">It's **accurate** - we double-checked the prices that we write down</span></span>
* <span data-ttu-id="435b6-137">Eles estão **conectados** — não há espaço em branco em qualquer uma dessas colunas</span><span class="sxs-lookup"><span data-stu-id="435b6-137">It's **connected** - there are no blank spaces in either of these columns</span></span>
* <span data-ttu-id="435b6-138">E, como veremos, eles têm uma quantidade **suficiente** de dados para responder à nossa pergunta</span><span class="sxs-lookup"><span data-stu-id="435b6-138">And, as we'll see, it's **enough** data to answer our question</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="435b6-139">Faça uma pergunta inteligente</span><span class="sxs-lookup"><span data-stu-id="435b6-139">Ask a sharp question</span></span>
<span data-ttu-id="435b6-140">Agora, faremos nosso pergunta de uma forma direta: "Quanto custará para comprar um diamante de 1,35 quilate?"</span><span class="sxs-lookup"><span data-stu-id="435b6-140">Now we'll pose our question in a sharp way: "How much will it cost to buy a 1.35 carat diamond?"</span></span>

<span data-ttu-id="435b6-141">Nossa lista não tem um diamante de 1,35 quilate, então teremos que usar o restante de dados para obter uma resposta para a pergunta.</span><span class="sxs-lookup"><span data-stu-id="435b6-141">Our list doesn't have a 1.35 carat diamond in it, so we'll have to use the rest of our data to get an answer to the question.</span></span>

## <a name="plot-the-existing-data"></a><span data-ttu-id="435b6-142">Plotar os dados existentes</span><span class="sxs-lookup"><span data-stu-id="435b6-142">Plot the existing data</span></span>
<span data-ttu-id="435b6-143">A primeira coisa que faremos é desenhar uma linha horizontal de números, chamada de eixo, para colocar os pesos no gráfico.</span><span class="sxs-lookup"><span data-stu-id="435b6-143">The first thing we'll do is draw a horizontal number line, called an axis, to chart the weights.</span></span> <span data-ttu-id="435b6-144">A faixa dos pesos vai de 0 a 2, portanto, vamos desenhar uma linha que cubra essa faixa e colocar marcações a cada meio quilate.</span><span class="sxs-lookup"><span data-stu-id="435b6-144">The range of the weights is 0 to 2, so we'll draw a line that covers that range and put ticks for each half carat.</span></span>

<span data-ttu-id="435b6-145">Em seguida, desenharemos um eixo vertical para registrar o preço e o conectaremos ao eixo horizontal de peso.</span><span class="sxs-lookup"><span data-stu-id="435b6-145">Next we'll draw a vertical axis to record the price and connect it to the horizontal weight axis.</span></span> <span data-ttu-id="435b6-146">Isso será em unidades de dólares.</span><span class="sxs-lookup"><span data-stu-id="435b6-146">This will be in units of dollars.</span></span> <span data-ttu-id="435b6-147">Agora temos um conjunto de eixos coordenados.</span><span class="sxs-lookup"><span data-stu-id="435b6-147">Now we have a set of coordinate axes.</span></span>

![Eixos de peso e preço](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

<span data-ttu-id="435b6-149">Agora, vamos pegar esses dados e transformá-los em uma *dispersão*.</span><span class="sxs-lookup"><span data-stu-id="435b6-149">We're going to take this data now and turn it into a *scatter plot*.</span></span> <span data-ttu-id="435b6-150">Essa é uma excelente maneira de visualizar conjuntos de dados numéricos.</span><span class="sxs-lookup"><span data-stu-id="435b6-150">This is a great way to visualize numerical data sets.</span></span>

<span data-ttu-id="435b6-151">Para o primeiro ponto de dados, desenhamos uma linha vertical no quilate 1,01.</span><span class="sxs-lookup"><span data-stu-id="435b6-151">For the first data point, we eyeball a vertical line at 1.01 carats.</span></span> <span data-ttu-id="435b6-152">Em seguida, desenhamos uma linha horizontal em $7.366.</span><span class="sxs-lookup"><span data-stu-id="435b6-152">Then, we eyeball a horizontal line at $7,366.</span></span> <span data-ttu-id="435b6-153">No local onde elas se encontram, desenhamos um ponto.</span><span class="sxs-lookup"><span data-stu-id="435b6-153">Where they meet, we draw a dot.</span></span> <span data-ttu-id="435b6-154">Isso representa nosso primeiro diamante.</span><span class="sxs-lookup"><span data-stu-id="435b6-154">This represents our first diamond.</span></span>

<span data-ttu-id="435b6-155">Agora fazemos isso para cada diamante nesta lista.</span><span class="sxs-lookup"><span data-stu-id="435b6-155">Now we go through each diamond on this list and do the same thing.</span></span> <span data-ttu-id="435b6-156">Quando terminarmos, este será o resultado: um monte de pontos, um para cada diamante.</span><span class="sxs-lookup"><span data-stu-id="435b6-156">When we're through, this is what we get: a bunch of dots, one for each diamond.</span></span>

![dispersão](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-the-model-through-the-data-points"></a><span data-ttu-id="435b6-158">Desenhar o modelo usando os pontos de dados</span><span class="sxs-lookup"><span data-stu-id="435b6-158">Draw the model through the data points</span></span>
<span data-ttu-id="435b6-159">Agora, se você os pontos e semicerrar os olhos, a coleção parecerá uma linha espessa e difusa.</span><span class="sxs-lookup"><span data-stu-id="435b6-159">Now if you look at the dots and squint, the collection looks like a fat, fuzzy line.</span></span> <span data-ttu-id="435b6-160">Podemos usar nosso marcador para desenhar uma linha reta através deles.</span><span class="sxs-lookup"><span data-stu-id="435b6-160">We can take our marker and draw a straight line through it.</span></span>

<span data-ttu-id="435b6-161">Desenhando uma linha, criamos um *modelo*.</span><span class="sxs-lookup"><span data-stu-id="435b6-161">By drawing a line, we created a *model*.</span></span> <span data-ttu-id="435b6-162">Pense nisso como pegar o mundo real e fazer uma versão simples em desenho dele.</span><span class="sxs-lookup"><span data-stu-id="435b6-162">Think of this as taking the real world and making a simplistic cartoon version of it.</span></span> <span data-ttu-id="435b6-163">Agora, o desenho está incorreto, a linha não passa por todos os pontos de dados.</span><span class="sxs-lookup"><span data-stu-id="435b6-163">Now the cartoon is wrong - the line doesn't go through all the data points.</span></span> <span data-ttu-id="435b6-164">Mas, é uma simplificação útil.</span><span class="sxs-lookup"><span data-stu-id="435b6-164">But, it's a useful simplification.</span></span>

![Linha da regressão linear](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

<span data-ttu-id="435b6-166">O fato de que todos os pontos não passam exatamente pela linha não tem qualquer problema.</span><span class="sxs-lookup"><span data-stu-id="435b6-166">The fact that all the dots don't go exactly through the line is OK.</span></span> <span data-ttu-id="435b6-167">Cientistas de dados explicam isso dizendo que há o modelo (essa é a linha) e cada ponto tem algum *ruído* ou *variação* associado a ele.</span><span class="sxs-lookup"><span data-stu-id="435b6-167">Data scientists explain this by saying that there's the model - that's the line - and then each dot has some *noise* or *variance* associated with it.</span></span> <span data-ttu-id="435b6-168">Há a relação perfeita subjacente, e há o mundo real que adiciona ruído e incerteza.</span><span class="sxs-lookup"><span data-stu-id="435b6-168">There's the underlying perfect relationship, and then there's the gritty, real world that adds noise and uncertainty.</span></span>

<span data-ttu-id="435b6-169">Como estamos tentando responder à pergunta *quanto custa?*, isso é chamado de *regressão*.</span><span class="sxs-lookup"><span data-stu-id="435b6-169">Because we're trying to answer the question *How much?* this is called a *regression*.</span></span> <span data-ttu-id="435b6-170">E, como estamos usando uma linha reta, é uma *regressão linear*.</span><span class="sxs-lookup"><span data-stu-id="435b6-170">And because we're using a straight line, it's a *linear regression*.</span></span>

## <a name="use-the-model-to-find-the-answer"></a><span data-ttu-id="435b6-171">Usar o modelo para encontrar a resposta</span><span class="sxs-lookup"><span data-stu-id="435b6-171">Use the model to find the answer</span></span>
<span data-ttu-id="435b6-172">Agora, temos um modelo e fazemos a nossa pergunta: quanto custará um diamante de 1,35 quilate?</span><span class="sxs-lookup"><span data-stu-id="435b6-172">Now we have a model and we ask it our question: How much will a 1.35 carat diamond cost?</span></span>

<span data-ttu-id="435b6-173">Para responder à nossa pergunta, nós identificamos visualmente o 1,35 quilate e desenhamos uma linha vertical.</span><span class="sxs-lookup"><span data-stu-id="435b6-173">To answer our question, we eyeball 1.35 carats and draw a vertical line.</span></span> <span data-ttu-id="435b6-174">Onde ela cruzar a linha do modelo, identificamos visualmente uma linha horizontal no eixo de dólar.</span><span class="sxs-lookup"><span data-stu-id="435b6-174">Where it crosses the model line, we eyeball a horizontal line to the dollar axis.</span></span> <span data-ttu-id="435b6-175">Ela atinge diretamente 10.000.</span><span class="sxs-lookup"><span data-stu-id="435b6-175">It hits right at 10,000.</span></span> <span data-ttu-id="435b6-176">Pronto!</span><span class="sxs-lookup"><span data-stu-id="435b6-176">Boom!</span></span> <span data-ttu-id="435b6-177">Essa é a resposta: um diamante de 1,35 quilate custa aproximadamente $10.000.</span><span class="sxs-lookup"><span data-stu-id="435b6-177">That's the answer: A 1.35 carat diamond costs about $10,000.</span></span>

![Encontrar a resposta no modelo](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a><span data-ttu-id="435b6-179">Criar um intervalo de confiança</span><span class="sxs-lookup"><span data-stu-id="435b6-179">Create a confidence interval</span></span>
<span data-ttu-id="435b6-180">É natural se preocupar com a precisão dessa previsão.</span><span class="sxs-lookup"><span data-stu-id="435b6-180">It's natural to wonder how precise this prediction is.</span></span> <span data-ttu-id="435b6-181">É muito útil saber se o preço do diamante de 1,35 quilate será muito próximo de $10.000, mais barato ou mais caro.</span><span class="sxs-lookup"><span data-stu-id="435b6-181">It's useful to know whether the 1.35 carat diamond will be very close to $10,000, or a lot higher or lower.</span></span> <span data-ttu-id="435b6-182">Para descobrir isso, vamos desenhar um envelope ao redor da linha de regressão que inclua a maioria dos pontos.</span><span class="sxs-lookup"><span data-stu-id="435b6-182">To figure this out, let's draw an envelope around the regression line that includes most of the dots.</span></span> <span data-ttu-id="435b6-183">Esse envelope é chamado de nosso *intervalo de confiança*: estamos bem confiantes de que os preços se enquadram nesse envelope, pois, no passado, a maioria deles se enquadrou.</span><span class="sxs-lookup"><span data-stu-id="435b6-183">This envelope is called our *confidence interval*: We're pretty confident that prices fall within this envelope, because in the past most of them have.</span></span> <span data-ttu-id="435b6-184">Podemos desenhar outras duas linhas horizontais a partir das quais a linha de 1,35 quilate cruza a parte superior e inferior do envelope.</span><span class="sxs-lookup"><span data-stu-id="435b6-184">We can draw two more horizontal lines from where the 1.35 carat line crosses the top and the bottom of that envelope.</span></span>

![intervalo de confiança](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

<span data-ttu-id="435b6-186">Agora podemos dizer algo sobre o intervalo de confiança: podemos dizer com segurança que o preço de um diamante de 1,35 quilate é de aproximadamente $10.000, mas pode ser $8.000 e pode ser $12.000.</span><span class="sxs-lookup"><span data-stu-id="435b6-186">Now we can say something about our confidence interval:  We can say confidently that the price of a 1.35 carat diamond is about $10,000 - but it might be as low as $8,000 and it might be as high as $12,000.</span></span>

## <a name="were-done-with-no-math-or-computers"></a><span data-ttu-id="435b6-187">Pronto, sem matemática ou computadores</span><span class="sxs-lookup"><span data-stu-id="435b6-187">We're done, with no math or computers</span></span>
<span data-ttu-id="435b6-188">Fizemos o que os cientistas de dados são pagos para fazer, e fizemos isso apenas desenhando:</span><span class="sxs-lookup"><span data-stu-id="435b6-188">We did what data scientists get paid to do, and we did it just by drawing:</span></span>

* <span data-ttu-id="435b6-189">Fizemos uma pergunta que pudemos responder com dados</span><span class="sxs-lookup"><span data-stu-id="435b6-189">We asked a question that we could answer with data</span></span>
* <span data-ttu-id="435b6-190">Criamos um *modelo* usando a *regressão linear*</span><span class="sxs-lookup"><span data-stu-id="435b6-190">We built a *model* using *linear regression*</span></span>
* <span data-ttu-id="435b6-191">Fizemos uma *previsão*, completa com um *intervalo de confiança*</span><span class="sxs-lookup"><span data-stu-id="435b6-191">We made a *prediction*, complete with a *confidence interval*</span></span>

<span data-ttu-id="435b6-192">E não usamos matemática ou computadores para isso.</span><span class="sxs-lookup"><span data-stu-id="435b6-192">And we didn't use math or computers to do it.</span></span>

<span data-ttu-id="435b6-193">Agora, se tivéssemos mais informações, como...</span><span class="sxs-lookup"><span data-stu-id="435b6-193">Now if we'd had more information, like...</span></span>

* <span data-ttu-id="435b6-194">o design do diamante</span><span class="sxs-lookup"><span data-stu-id="435b6-194">the cut of the diamond</span></span>
* <span data-ttu-id="435b6-195">variações de cor (quão próximo do branco o diamante é)</span><span class="sxs-lookup"><span data-stu-id="435b6-195">color variations (how close the diamond is to being white)</span></span>
* <span data-ttu-id="435b6-196">o número de inclusões no diamante</span><span class="sxs-lookup"><span data-stu-id="435b6-196">the number of inclusions in the diamond</span></span>

<span data-ttu-id="435b6-197">…teríamos mais colunas.</span><span class="sxs-lookup"><span data-stu-id="435b6-197">...then we would have had more columns.</span></span> <span data-ttu-id="435b6-198">Nesse caso, a matemática se torna útil.</span><span class="sxs-lookup"><span data-stu-id="435b6-198">In that case, math becomes helpful.</span></span> <span data-ttu-id="435b6-199">Se você tiver mais de duas colunas, é difícil desenhar pontos no papel.</span><span class="sxs-lookup"><span data-stu-id="435b6-199">If you have more than two columns, it's hard to draw dots on paper.</span></span> <span data-ttu-id="435b6-200">A matemática permite o encaixe perfeito dessa linha ou desse plano aos seus dados.</span><span class="sxs-lookup"><span data-stu-id="435b6-200">The math lets you fit that line or that plane to your data very nicely.</span></span>

<span data-ttu-id="435b6-201">Além disso, se em vez de apenas um punhado de diamantes, tivéssemos dois mil ou dois milhões, esse trabalho seria muito mais otimizado com um computador.</span><span class="sxs-lookup"><span data-stu-id="435b6-201">Also, if instead of just a handful of diamonds, we had two thousand or two million, then you can do that work much faster with a computer.</span></span>

<span data-ttu-id="435b6-202">Hoje, falamos sobre como fazer a regressão linear e fizemos uma previsão usando dados.</span><span class="sxs-lookup"><span data-stu-id="435b6-202">Today, we've talked about how to do linear regression, and we made a prediction using data.</span></span>

<span data-ttu-id="435b6-203">Confira outros vídeos da série "Ciência de dados para iniciantes" no Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="435b6-203">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="435b6-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="435b6-204">Next steps</span></span>
* [<span data-ttu-id="435b6-205">Teste um primeiro experimento da ciência de dados com o Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="435b6-205">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* <span data-ttu-id="435b6-206">
            [Obtenha uma introdução ao Machine Learning no Microsoft Azure](machine-learning-what-is-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="435b6-206">[Get an introduction to Machine Learning on Microsoft Azure](machine-learning-what-is-machine-learning.md)</span></span>
