---
title: "aaaAsk pode responder a uma data de pergunta - problemas de ciência de dados - aprendizado de máquina do Azure | Microsoft Docs"
description: "Saiba como tooformulate uma ciência de dados numérico pergunta na ciência de dados para iniciantes 3 de vídeo. Inclui uma comparação das perguntas de classificação e regressão."
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
ms.openlocfilehash: 00c328f51e6d9ff6654b5966eb97d6762582f7e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ask-a-question-you-can-answer-with-data"></a>Fazer uma pergunta que você possa responder com dados
## <a name="video-3-data-science-for-beginners-series"></a>Vídeo 3: Série de ciência de dados para iniciantes
Saiba como tooformulate um problema de ciência de dados em uma pergunta na ciência de dados para iniciantes 3 de vídeo. Esse vídeo inclui uma comparação de perguntas para os algoritmos de classificação e regressão.

Olá tooget máximo série hello, assista a todos eles. [Acesse a lista de toohello de vídeos](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a>Outros vídeos nesta série
*Ciência de dados para iniciantes* é uma breve introdução toodata ciência cinco vídeos curtos.

* Vídeo 1: [Olá 5 perguntas respostas de ciência de dados](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 seg)*
* Vídeo 2: [Seus dados estão prontos para a ciência de dados?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min 56 s)*
* Video 3: Faça uma pergunta que você possa responder com dados
* Vídeo 4: [Preveja uma resposta com um modelo simples](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 s)*
* Vídeo 5: [copiar ciência de dados de outras pessoas trabalho toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 minutos 18 segundos)*

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a>Transcrição: Faça uma pergunta que você possa responder com dados
Bem-vindo vídeo de terceiro toohello em série hello "Ciência de dados para iniciantes."  

Nele, você obterá algumas dicas para formular uma pergunta que possa responder com dados.

Você pode obter o máximo neste vídeo, se você observar primeiro dois vídeos anteriores Olá nesta série: "pode responder a ciência de dados Olá 5 perguntas" e "É que seus dados estão prontos para ciência de dados?"

## <a name="ask-a-sharp-question"></a>Faça uma pergunta inteligente
Falamos sobre como ciência de dados é o processo de saudação do uso de nomes (também chamados de categorias ou rótulos) e números toopredict uma pergunta de tooa de resposta. Mas ele não pode ser qualquer pergunta; ele tem toobe um *pergunta curva.*

Uma pergunta vaga não tem toobe respondeu com um nome ou um número. Uma pergunta inteligente sim.

Imagine que você encontrou uma lâmpada mágica com um gênio que responderá de verdade qualquer pergunta feita. Mas é um genie mal intencionada e ele tentará toomake sua resposta como vagas e confuso como ele pode escapar. Você deseja toopin-lo para baixo com uma pergunta impenetrável assim que ele não pode ajudar mas informa o que você deseja tooknow.

Se você tooask uma pergunta vaga, como "O que está acontecendo toohappen com meu estoque?", genie Olá pode responder, "mudará preço Olá". É uma resposta sincera, mas não é muito útil.

Mas se você fosse tooask uma curva pergunta, como "Qual o preço de venda do meu estoque será próxima semana?", hello genie não pode ajudar, mas oferecem uma determinada responde e prever um preço de venda.

## <a name="examples-of-your-answer-target-data"></a>Exemplos de resposta: dados de destino
Quando você formula sua pergunta, consulte toosee se você tem exemplos de resposta de saudação em seus dados.

Se nossa pergunta é "Qual será o preço de venda do meu estoque na próxima semana?", em seguida, temos toomake-se de que nossos dados incluem histórico de preço de estoque hello.

Se nosso pergunta é "quais carro em meu fleet toofail contínuo primeiro". em seguida, temos toomake-se de que nossos dados incluem informações sobre falhas anteriores.

![Dados de destino - exemplos de resposta. Formule uma pergunta da ciência de dados.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

Esses exemplos de respostas são chamados de destino. Um destino é o que estamos tentando toopredict sobre pontos de dados futuros, se é uma categoria ou um número.

Se você não tem nenhum dado de destino, você precisará tooget alguns. Você não será capaz de tooanswer sua pergunta sem ele.

## <a name="reformulate-your-question"></a>Reformular sua pergunta
Às vezes, você pode reformular tooget sua pergunta uma resposta mais útil.

Olá pergunta "é esse ponto de dados A ou B?" prevê Olá categoria (ou nome ou rótulo) de algo. tooanswer, usamos um *algoritmo de classificação*.

Olá pergunta "Quanto?" ou "Quantos?" prevê uma quantia. tooanswer-usamos uma *algoritmo de regressão*.

toosee como é possível transformar esses, vejamos Olá pergunta "quais notícia leitor de toothis mais interessante Olá?" Solicita uma previsão de uma opção simples entre muitas possibilidades – em outras palavras, "É A, B, C ou D?" - e usaria um algoritmo de classificação.

Mas, essa questão pode ser tooanswer mais fácil se você reformular-o como "quão interessante é cada história no leitor de toothis lista?" Agora você pode dar a cada artigo uma pontuação numérica e, em seguida, é artigo de classificação mais alta de saudação tooidentify fácil. Este é um reformular da questão da classificação de saudação em uma pergunta de regressão ou quanto?

![Reformule sua pergunta. Pergunta de classificação versus pergunta de regressão.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

Como você pedir que uma pergunta é um algoritmo de toowhich pista pode fornecer uma resposta.

Você encontrará determinadas famílias de algoritmos - como Olá aqueles em nosso exemplo de artigo de notícias - estão intimamente relacionadas. Pode reformular seu algoritmo Olá toouse de pergunta que lhe Olá resposta mais úteis.

Mas, mais importante, faça essa pergunta curva - pergunta Olá que você pode responder com dados. E certifique-se de ter Olá dados certos tooanswê-lo.

Falamos sobre alguns princípios básicos para fazer uma pergunta que você pode responder com dados.

Ser toocheck se out Olá outros vídeos em "Dados ciência para iniciantes", de aprendizado de máquina do Microsoft Azure.

## <a name="next-steps"></a>Próximas etapas
* [Teste um primeiro experimento da ciência de dados com o Machine Learning Studio](machine-learning-create-experiment.md)
* [Obter uma introdução tooMachine aprendizado no Microsoft Azure](machine-learning-what-is-machine-learning.md)
