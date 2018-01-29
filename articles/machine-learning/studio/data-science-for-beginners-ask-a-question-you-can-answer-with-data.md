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
ms.date: 01/03/2018
ms.author: cgronlun
ms.openlocfilehash: 2f3d8d5c2e7cf1ebc88dc1ff1d7d03bf85383884
ms.sourcegitcommit: 4bd369fc472dced985239aef736fece42fecfb3b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2018
---
# <a name="ask-a-question-you-can-answer-with-data"></a>Fazer uma pergunta que você possa responder com dados
## <a name="video-3-data-science-for-beginners-series"></a>Vídeo 3: Série de ciência de dados para iniciantes
Saiba como transformar um problema de ciência de dados em uma pergunta no Vídeo Ciência de Dados para Iniciantes 3. Esse vídeo inclui uma comparação de perguntas para os algoritmos de classificação e regressão.

Para aproveitar ao máximo da série, assista a todos os vídeos. [Acesse a lista de vídeos](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a>Outros vídeos nesta série
*Ciência de dados para iniciantes* é uma breve introdução à ciência de dados em cinco vídeos curtos.

* Vídeo 1: [As cinco perguntas que a ciência de dados responde](data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min e 14 s)*
* Vídeo 2: [Seus dados estão prontos para a ciência de dados?](data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min 56 s)*
* Video 3: Faça uma pergunta que você possa responder com dados
* Vídeo 4: [Preveja uma resposta com um modelo simples](data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 s)*
* Vídeo 5: [Copie o trabalho de outras pessoas para fazer a ciência de dados](data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 s)*

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a>Transcrição: Faça uma pergunta que você possa responder com dados
Bem-vindo ao terceiro vídeo da série "Ciência de dados para iniciantes."  

Nele, você obterá algumas dicas para formular uma pergunta que possa responder com dados.

Você pode obter mais desse vídeo se primeiro observar dois vídeos anteriores na série: "As cinco perguntas que a ciência de dados pode responder" e "Seus dados estão prontos para a ciência de dados?"

## <a name="ask-a-sharp-question"></a>Faça uma pergunta inteligente
Falamos sobre como a ciência de dados é o processo de usar nomes (também chamados de categorias ou rótulos) e números para prever uma resposta para uma pergunta. Mas não pode ser uma pergunta qualquer; deve ser uma *pergunta inteligente.*

Uma pergunta vaga não precisa ser respondida com um nome ou um número. Uma pergunta inteligente sim.

Imagine que você encontrou uma lâmpada mágica com um gênio que responderá de verdade qualquer pergunta feita. Mas é um gênio mau e ele tentará tornar sua resposta o mais vaga e confusa que puder para se dar bem. Você deseja forçá-lo com uma pergunta incontestável para que ele não possa fazer nada, exceto dizer o que você deseja saber.

Se você fizesse uma pergunta vaga, como: "O que acontecerá com minhas ações?", o gênio poderia responder: "O preço mudará". É uma resposta sincera, mas não é muito útil.

Mas se fizesse uma pergunta direta, como: "Qual será o preço de venda de minhas ações na próxima semana?", o gênio não poderia fazer nada, exceto dar uma resposta específica e prever um preço de venda.

## <a name="examples-of-your-answer-target-data"></a>Exemplos de resposta: dados de destino
Depois de formular sua pergunta, verifique para saber se você tem exemplos de resposta em seus dados.

Se nossa pergunta é "Qual será o preço de venda do meu estoque na próxima semana?", temos que verificar se nossos dados incluem o histórico de preços de ações.

Se nossa pergunta é "Qual carro em minha frota vai falhar primeiro?", temos que verificar se nossos dados incluem informações sobre falhas anteriores.

![Dados de destino - exemplos de resposta. Formule uma pergunta da ciência de dados.](./media/data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

Esses exemplos de respostas são chamados de destino. Um destino é o que estamos tentando prever sobre os futuros pontos de dados, seja uma categoria seja um número.

Se você não tiver nenhum dado de destino, precisará obter algum. Você não conseguirá responder à sua pergunta sem ele.

## <a name="reformulate-your-question"></a>Reformular sua pergunta
Às vezes, você pode reformular sua pergunta para obter uma resposta mais útil.

A pergunta "Estes dados são do ponto A ou B?" prevê a categoria (ou nome ou rótulo) de algo. Para respondê-la, usamos um *algoritmo de classificação*.

A pergunta "Quanto?" ou "Quantos?" prevê uma quantia. Para respondê-la, usamos um *algoritmo de regressão*.

Para ver como podemos transformar isso, vejamos a pergunta: "Qual notícia é mais interessante para este leitor?" Solicita uma previsão de uma opção simples entre muitas possibilidades – em outras palavras, "É A, B, C ou D?" - e usaria um algoritmo de classificação.

Mas, essa pergunta poderá ser mais fácil de responder se você reformulá-la como: "O quanto interessante é cada história nesta lista para este leitor?" Agora, você pode dar a cada artigo uma pontuação numérica e será fácil identificar o artigo com a pontuação mais alta. Isto é uma reformulação da pergunta de classificação em uma pergunta de regressão ou do tipo Quanto?

![Reformule sua pergunta. Pergunta de classificação versus pergunta de regressão.](./media/data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

Como você faz uma pergunta é uma dica sobre qual algoritmo poderá dar uma resposta.

Você descobrirá que certas famílias de algoritmos - como aquelas em nosso exemplo de notícia - estão intimamente relacionadas. Você pode reformular sua pergunta para usar o algoritmo que fornece a resposta mais útil.

Porém, o mais importante é fazer uma pergunta inteligente - a pergunta que você pode responder com dados. E verifique se você tem os dados certos para respondê-la.

Falamos sobre alguns princípios básicos para fazer uma pergunta que você pode responder com dados.

Confira outros vídeos da série "Ciência de dados para iniciantes" no Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Próximas etapas
* [Teste um primeiro experimento da ciência de dados com o Machine Learning Studio](create-experiment.md)
* [Obtenha uma introdução ao Machine Learning no Microsoft Azure](what-is-machine-learning.md)
