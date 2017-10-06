---
title: "aaaPredict uma resposta com um modelo de regressão simples - aprendizado de máquina do Azure | Microsoft Docs"
description: "Como toocreate uma regressão simple modelo toopredict um preço na ciência de dados para iniciantes 4 de vídeo. Inclui uma regressão linear com os dados de destino."
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
ms.openlocfilehash: d4270c2237c33b7e898b78a08b292bc9d62e49ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a>Prever uma resposta com um modelo simples
## <a name="video-4-data-science-for-beginners-series"></a>Vídeo 4: Série de ciência de dados para iniciantes
Saiba como toocreate uma toopredict do modelo de regressão simples Olá preço de um losango na ciência de dados para iniciantes 4 de vídeo. Vamos desenhar um modelo de regressão com dados de destino.

Olá tooget máximo série hello, assista a todos eles. [Acesse a lista de toohello de vídeos](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a>Outros vídeos nesta série
*Ciência de dados para iniciantes* é uma breve introdução toodata ciência cinco vídeos curtos.

* Vídeo 1: [Olá 5 perguntas respostas de ciência de dados](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 seg)*
* Vídeo 2: [Seus dados estão prontos para a ciência de dados?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min 56 s)*
* Video 3: [Faça uma pergunta que você possa responder com dados](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 s)*
* Vídeo 4: Preveja uma resposta com um modelo simples
* Vídeo 5: [copiar ciência de dados de outras pessoas trabalho toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 minutos 18 segundos)*

## <a name="transcript-predict-an-answer-with-a-simple-model"></a>Transcrição: Preveja uma resposta com um modelo simples
Bem-vindo toohello quarto vídeo de saudação série "Dados ciência para iniciantes". Neste vídeo, vamos criar um modelo simples e fazer uma previsão.

Um *modelo* é uma história simplificada sobre nossos dados. Mostrarei o que quero dizer.

## <a name="collect-relevant-accurate-connected-enough-data"></a>Colete dados relevantes, precisos, conectados e suficientes
Digamos que desejo tooshop para um losango. Tenho um anel que pertencia toomy avó com uma configuração para um losango circunflexo 1,35 e desejo tooget uma ideia do quanto custará. Posso obter um bloco de notas e caneta no repositório de joias hello e, anote o preço de saudação de todos os losangos Olá no caso de Olá e o quanto eles pesam em carats. Iniciando com losango primeiro Olá - do-1.01 carats e US $7,366.

Agora percorrer e faça isso para Olá todos os outros losangos no repositório de saudação.

![Colunas de dados de diamante](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

Observe que a nossa lista tem duas colunas. Cada coluna tem um atributo diferente - peso em quilate e preço - e cada linha é um único ponto de dados que representa um único diamante.

Na verdade, criamos um pequeno conjunto de dados aqui; uma tabela. Observe que isso atende aos nossos critérios de qualidade:

* Olá dados **relevantes** -peso é tooprice definitivamente relacionado
* Ele tem **precisas** -nós com verificação dupla preços Olá escrevemos para baixo
* Eles estão **conectados** — não há espaço em branco em qualquer uma dessas colunas
* E, como veremos, ele tem **suficiente** dados tooanswer nossa pergunta

## <a name="ask-a-sharp-question"></a>Faça uma pergunta inteligente
Agora podemos será digite nossa pergunta de forma curva: "quantos será custo toobuy um losango circunflexo 1,35?"

Nossa lista não tem um losango 1,35 circunflexo, portanto teremos restante Olá toouse tooget nossos dados uma pergunta de toohello de resposta.

## <a name="plot-hello-existing-data"></a>Plotar dados existentes Olá
primeira coisa Olá que faremos é desenhar uma linha horizontal de número, chamada de um eixo, pesos de saudação toochart. intervalo de saudação de pesos de saudação é too2 0, portanto vamos desenhar uma linha que abrange que variam e colocar tiques para cada semestre intercalação.

Em seguida vamos desenhar um preço de saudação do eixo vertical toorecord e conectá-lo toohello eixo de peso horizontal. Isso será em unidades de dólares. Agora temos um conjunto de eixos coordenados.

![Eixos de peso e preço](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

Estamos tootake contínuo esses dados agora e transformá-la em um *dispersão*. Esta é uma ótima maneira toovisualize numéricos conjuntos de dados.

Saudação do primeiro ponto de dados, é possível identificar uma linha vertical no carats 1.01. Em seguida, desenhamos uma linha horizontal em $7.366. No local onde elas se encontram, desenhamos um ponto. Isso representa nosso primeiro diamante.

Agora percorrer cada losango nessa lista e Olá a mesma coisa. Quando terminarmos, este será o resultado: um monte de pontos, um para cada diamante.

![dispersão](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a>Desenhar modelo Olá por meio de pontos de dados Olá
Agora se você observar squint e pontos de hello, coleção Olá parece uma linha fat, difusa. Podemos usar nosso marcador para desenhar uma linha reta através deles.

Desenhando uma linha, criamos um *modelo*. Pense nisso como colocar Olá, mundo real e fazer uma versão simplificada personagem de desenho dele. Agora personagem de desenho hello está errada - linha hello não passar por todos os pontos de dados de saudação. Mas, é uma simplificação útil.

![Linha da regressão linear](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

fato Olá todos os pontos de saudação não passam exatamente por linha hello é Okey. Os cientistas de dados explicam isso dizendo que há Olá modelo - linha hello - e, em seguida, cada ponto tem algumas *ruído* ou *variação* associados a ele. Há Olá subjacente relação perfeita, e, em seguida, há Olá mundo real, interessa que adiciona ruído e incerteza.

Porque estamos tentando pergunta de saudação tooanswer *quanto?* isso é chamado de um *regressão*. E, como estamos usando uma linha reta, é uma *regressão linear*.

## <a name="use-hello-model-toofind-hello-answer"></a>Use a resposta de Olá Olá modelo toofind
Agora, temos um modelo e fazemos a nossa pergunta: quanto custará um diamante de 1,35 quilate?

tooanswer nossa pergunta, podemos identificar carats 1,35 e desenhar uma linha vertical. Em que ele cruze a linha de modelo hello, podemos identificar um eixo de dólar toohello linha horizontal. Ela atinge diretamente 10.000. Pronto! Que é a resposta de saudação: um losango circunflexo 1,35 custa cerca de US $10.000.

![Encontrar a resposta de saudação no modelo de saudação](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a>Criar um intervalo de confiança
É natural toowonder a precisão é desta previsão. É útil tooknow se losango de intercalação 1,35 Olá será muito próxima muito US $10.000 ou muito maior ou menor. toofigure esse limite, vamos desenhar um envelope em torno da linha de regressão de saudação que inclui a maioria dos pontos de saudação. Este envelope é chamado nosso *intervalo de confiança*: estamos muito certo de que os preços se enquadra este envelope, porque em Olá anterior a maioria delas tem. Podemos desenhar duas linhas horizontais mais de onde a linha de intercalação 1,35 de Olá cruza superior hello e inferior de saudação do envelope.

![intervalo de confiança](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

Agora podemos dizer algo sobre nosso intervalo de confiança: podemos dizer com confiança preço Olá um losango circunflexo 1,35 é aproximadamente US $10.000 -, mas pode ser tão baixo quanto $8.000 e pode ser de até US $12.000.

## <a name="were-done-with-no-math-or-computers"></a>Pronto, sem matemática ou computadores
Fizemos os cientistas de dados que receberá toodo e fizemos apenas desenhando:

* Fizemos uma pergunta que pudemos responder com dados
* Criamos um *modelo* usando a *regressão linear*
* Fizemos uma *previsão*, completa com um *intervalo de confiança*

E não usamos matemática ou computadores toodo-lo.

Agora, se tivéssemos mais informações, como...

* Olá recorta de losango Olá
* variações de cor (como fechar losango Olá é toobeing branco)
* número de saudação de inclusões no losango Olá

…teríamos mais colunas. Nesse caso, a matemática se torna útil. Se você tiver mais de duas colunas, é toodraw rígido pontos em papel. matemática Olá permite que você ajusta o plano tooyour dados ou linha muito bem.

Além disso, se em vez de apenas um punhado de diamantes, tivéssemos dois mil ou dois milhões, esse trabalho seria muito mais otimizado com um computador.

Hoje, falamos sobre como regressão linear toodo e é feita uma previsão usando os dados.

Ser toocheck se out Olá outros vídeos em "Dados ciência para iniciantes", de aprendizado de máquina do Microsoft Azure.

## <a name="next-steps"></a>Próximas etapas
* [Teste um primeiro experimento da ciência de dados com o Machine Learning Studio](machine-learning-create-experiment.md)
* [Obter uma introdução tooMachine aprendizado no Microsoft Azure](machine-learning-what-is-machine-learning.md)
