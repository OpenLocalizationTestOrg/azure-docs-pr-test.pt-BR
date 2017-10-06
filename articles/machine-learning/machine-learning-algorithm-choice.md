---
title: algoritmos de aprendizagem de computador toochoose aaaHow | Microsoft Docs
description: "Como toochoose algoritmos de aprendizado de máquina do Azure para aprendizado supervisionado e não no cluster, classificação ou regressão experiências."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a3b23d7f-f083-49c4-b6b1-3911cd69f1b4
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/25/2017
ms.author: garye
ms.openlocfilehash: 367b2278acc2435f27f9d24ead8199db58aca283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-algorithms-for-microsoft-azure-machine-learning"></a>Como toochoose algoritmos de aprendizado de máquina do Microsoft Azure
Olá pergunta toohello "qual máquina algoritmo de aprendizagem devo usar?" sempre será "Depende". Ele depende de tamanho hello, a qualidade e a natureza dos dados de saudação. Depende do que você deseja toodo com resposta hello. Depende de como matemática de saudação do algoritmo de saudação foi convertida em instruções para computador Olá que está usando. E depende de quanto tempo você tem. Até mesmo os cientistas de dados hello mais experiente não podem determinar qual algoritmo executará melhor antes de tentá-los.

## <a name="hello-machine-learning-algorithm-cheat-sheet"></a>Olá Cheat Sheet de algoritmo de aprendizado de máquina
Olá **Microsoft Azure máquina de aprendizado algoritmo Cheat Sheet** ajuda a escolher o direito de saudação algoritmo de aprendizado para suas soluções de análise preditiva da biblioteca de aprendizado de máquina do Microsoft Azure Olá dos algoritmos da máquina.
Este artigo orienta como toouse-lo.

> [!NOTE]
> roteiro de saudação toodownload e siga junto com este artigo, vá muito[máquina roteiro do algoritmo de aprendizagem para o estúdio de aprendizado de máquina do Microsoft Azure](machine-learning-algorithm-cheat-sheet.md).
> 
> 

Este roteiro tem um público muito específico em mente: um cientista de dados começando com o aprendizado de máquina de nível superior, tentar toochoose um toostart algoritmo no estúdio de aprendizado de máquina do Azure. Isso significa que ela faz algumas generalizações e simplificações excessivas, mas aponta uma direção segura para você. Isso também significa que há muitos algoritmos não listados aqui. Como o aprendizado de máquina do Azure aumenta tooencompass um conjunto mais completo de métodos disponíveis, vamos adicioná-los.

Essas recomendações são comentários e dicas compilados de vários cientistas de dados e especialistas em aprendizado de máquina. Nós não concordar com tudo, mas tentei tooharmonize nossas opiniões em um consenso aproximado. A maioria das instruções de saudação de divergência começa com "Depende..."

### <a name="how-toouse-hello-cheat-sheet"></a>Como toouse Olá roteiro
Rótulos de caminho e o algoritmo de saudação no gráfico de saudação como de leitura "para  *&lt;rótulo de caminho&gt;*, use  *&lt;algoritmo&gt;*." Por exemplo, “Para *velocidade*, use *regressão logística de duas classes*”. Às vezes, mais de uma ramificação se aplica.
Às vezes, nenhuma delas é a solução perfeita. Eles está toobe pretendido recomendações de regra de ouro, então não se preocupe sendo exata.
Vários cientistas de dados, falamos com disse que Olá somente se até encontrar o algoritmo de melhor Olá é tootry todos eles.

Aqui está um exemplo de hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com/) de um experimento que tenta vários algoritmos em relação a saudação mesmos dados e compara Olá resultados: [classificadores de comparação de classe vários: reconhecimento de letra ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

> [!TIP]
> toodownload e imprimir um diagrama que fornece uma visão geral dos recursos de saudação do estúdio de aprendizado de máquina, consulte [diagrama de visão geral dos recursos do estúdio de aprendizado de máquina do Azure](machine-learning-studio-overview-diagram.md).
> 
> 

## <a name="flavors-of-machine-learning"></a>Tipos de aprendizado de máquina
### <a name="supervised"></a>Supervisionado
Os algoritmos de aprendizado supervisionados fazem previsões com base em um conjunto de exemplos. Por exemplo, os preços de estoque históricos podem ser palpites toohazard usado com preços futuros. Cada exemplo usado para treinamento é rotulado com valor de saudação de interesse — nesse caso, Olá preço de estoque. Um algoritmo de aprendizado supervisionado procura por padrões nesses rótulos de valor. Ele pode usar todas as informações que podem ser relevantes — dia de saudação da semana hello, temporada hello, dados financeiros da empresa hello, tipo de saudação do setor, presença Olá interrupções eventos geopolíticos — e cada algoritmo procura diferentes tipos de padrões. Depois que o algoritmo de saudação encontra padrão melhor hello, ele pode, ele usa que previsões de toomake padrão para sem rótulo dados de teste — os preços do futuro.

O aprendizado supervisionado é um tipo popular e útil de aprendizado de máquina. Com uma exceção, todos os módulos de saudação no aprendizado de máquina do Azure são supervisionados algoritmos de aprendizagem. Há vários tipos específicos de aprendizado supervisionado representados no Azure Machine Learning: classificação, regressão e detecção de anomalias.

* **Classificação**. Quando dados saudação estão sendo usada toopredict uma categoria, aprendizado supervisionado também é chamado de classificação. Esse é o caso de Olá durante a atribuição de uma imagem como uma imagem de um 'cat' ou 'dog'. Quando há apenas duas opções, isso é chamado de **classificação binomial** ou de **duas classes**. Quando há mais de categorias, como durante a previsão vencedor de saudação do torneio de comportamento estranho de março de NCAA hello, esse problema é conhecido como **classificação multiclasse**.
* **Regressão**. Quando um valor estiver sendo previsto, assim como acontece com preços de cotações, o aprendizado supervisionado será chamado de regressão.
* **Detecção de anomalias**. Às vezes, hello meta é tooidentify pontos de dados são simplesmente incomuns. Na detecção de fraudes, por exemplo, quaisquer padrões incomuns de gasto em cartão de crédito são suspeitos. possíveis variações de saudação são tão numerosas e Olá exemplos de treinamento para alguns, que é não é viável toolearn quais atividades fraudulentas aparência. A abordagem que leva de detecção de anomalias é toosimply saber que atividade normal aparência (usando um transações de histórico não fraudulentos) e identificar qualquer coisa que é significativamente diferente.

### <a name="unsupervised"></a>Não supervisionado
No aprendizado não supervisionado, os pontos de dados não têm rótulos associados a eles. Em vez disso, objetivo Olá um supervisionados aprendizado algoritmo é organizar dados saudação de alguma forma ou toodescribe sua estrutura. Isso pode significar agrupá-los em clusters ou encontrar diferentes maneiras de consultar dados complexos para que eles pareçam mais simples ou mais organizados.

### <a name="reinforcement-learning"></a>Aprendizado de reforço
No aprendizado de Reforce seu algoritmo Olá obtém toochoose uma ação no ponto de dados de tooeach de resposta. algoritmo de aprendizado Olá também recebe um sinal de recompensa foi um curto período de tempo mais tarde, que indica o quão boa decisão de saudação.
Com base nisso, o algoritmo Olá modifica sua estratégia de recompensa mais alta da ordem tooachieve hello. Atualmente, não há nenhum módulo de algoritmo de reforço de aprendizado no Aprendizado de Máquina do Azure. Aprendizado Reforce seu é comum em robótica, onde hello, conjunto de leituras de sensor em um ponto no tempo é um ponto de dados e o algoritmo Olá deve escolher ação próxima do robô Olá. Também é um ajuste natural para aplicativos da Internet das Coisas.

## <a name="considerations-when-choosing-an-algorithm"></a>Considerações ao escolher um algoritmo
### <a name="accuracy"></a>Precisão
Obter resposta mais precisa Olá possíveis nem sempre é necessário.
Às vezes uma aproximação será adequada, dependendo do uso que você quiser dar a ela. Se esse for o caso de Olá, você pode ser capaz de toocut o tempo de processamento drasticamente por adequar-se com os métodos mais aproximados. Outra vantagem dos métodos mais aproximados é que eles naturalmente tendem a evitar o [superajuste](https://youtu.be/DQWI1kvmwRg).

### <a name="training-time"></a>Tempo de treinamento
Olá o número de minutos ou horas necessário tootrain um modelo varia muito entre algoritmos. O tempo de treinamento é geralmente ligado ao precisão — um normalmente acompanha Olá outros. Além disso, alguns algoritmos são mais confidenciais toohello quantos pontos de dados que outros.
Quando o tempo é limitado podem gerar escolha de saudação do algoritmo, especialmente quando o conjunto de dados de saudação é grande.

### <a name="linearity"></a>Linearidade
Muitos algoritmos de aprendizado de máquina usam a linearidade. Os algoritmos de classificação linear supõem que as classes podem ser separadas por uma linha reta (ou seu análogo em dimensões maiores). Isso inclui a regressão logística e as máquinas de vetor de suporte (como implementado no Aprendizado de Máquina do Azure).
Os algoritmos de regressão linear supõem que as tendências de dados seguem uma linha reta. Essas suposições não são ruins para alguns problemas, mas em outros elas podem reduzir a precisão.

![Limite de classe não linear][1]

***Limite de classe não linear*** *- contar com um algoritmo de classificação linear resultaria em baixa precisão*

![Dados com uma tendência não linear][2]

***Dados com uma tendência não linear*** *- usar um método de regressão linear geraria erros muito maiores do que o necessário*

Apesar de seus riscos, os algoritmos lineares são muito populares como uma primeira linha de ataque. Eles tendem a toobe maneira algorítmica simple e rápido para treinar.

### <a name="number-of-parameters"></a>Número de parâmetros
Os parâmetros são botões Olá um cientista de dados obtém tooturn ao configurar um algoritmo. Eles são números que afetam o comportamento do algoritmo hello, como a tolerância de erro ou o número de iterações ou opções entre variantes de comportamento do algoritmo de saudação. tempo de treinamento de saudação e a precisão do algoritmo hello, às vezes, podem ser configurações corretas de saudação apenas toogetting muito confidenciais. Normalmente, os algoritmos com parâmetros de grandes números exigem hello mais avaliação e erro toofind uma combinação válida.

Como alternativa, há um bloco de módulo de [limpeza de parâmetro](machine-learning-algorithm-parameters-optimize.md) no Azure Machine Learning que experimenta automaticamente todas as combinações de parâmetro em qualquer granularidade que você escolher. Quando esta é uma ótima maneira toomake se tiver estendido o espaço de parâmetro hello, Olá tempo necessário tootrain um modelo aumenta exponencialmente com número de saudação de parâmetros.

Olá vantagem é que ter muitos parâmetros geralmente indica que um algoritmo tem maior flexibilidade. Geralmente, isso pode significar uma precisão muito boa. Fornecida a que você pode encontrar a combinação certa de saudação de configurações de parâmetro.

### <a name="number-of-features"></a>Número de recursos
Para determinados tipos de dados, o número de saudação de recursos pode ser muito grandes toohello em comparação com o número de pontos de dados. Geralmente, esse é o caso de Olá com genetics ou dados textuais. número grande de saudação de recursos pode reduzir alguns algoritmos de aprendizado, fazendo com que o treinamento unfeasibly longo de tempo. Máquinas de vetor de suporte são especialmente adequado toothis caso (veja abaixo).

### <a name="special-cases"></a>Casos especiais
Alguns algoritmos de aprendizado fazem suposições específicas sobre estrutura Olá dados saudação ou resultados de saudação desejado. Se você conseguir encontrar um que atenda às suas necessidades, ele oferecerá resultados mais úteis, previsões mais exatas ou tempos de treinamento menores.

| **Algoritmo** | **Precisão** | **Tempo de treinamento** | **Linearidade** | **Parâmetros** | **Observações** |
| --- |:---:|:---:|:---:|:---:| --- |
| **Classificação de duas classes** | | | | | |
| [regressão logística](https://msdn.microsoft.com/library/azure/dn905994.aspx) | |● |● |5 | |
| [floresta de decisão](https://msdn.microsoft.com/library/azure/dn906008.aspx) |● |○ | |6 | |
| [selva de decisão](https://msdn.microsoft.com/library/azure/dn905976.aspx) |● |○ | |6 |Volume de memória insuficiente |
| [árvore de decisão aumentada](https://msdn.microsoft.com/library/azure/dn906025.aspx) |● |○ | |6 |Grande volume de memória |
| [rede neural](https://msdn.microsoft.com/library/azure/dn905947.aspx) |● | | |9 |[A personalização adicional é possível](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [perceptron médio](https://msdn.microsoft.com/library/azure/dn906036.aspx) |○ |○ |● |4 | |
| [máquina de vetor de suporte](https://msdn.microsoft.com/library/azure/dn905835.aspx) | |○ |● |5 |Bom para conjuntos de recursos grandes |
| [máquina de vetor de suporte localmente profunda](https://msdn.microsoft.com/library/azure/dn913070.aspx) |○ | | |8 |Bom para conjuntos de recursos grandes |
| [computador do ponto de Bayes](https://msdn.microsoft.com/library/azure/dn905930.aspx) | |○ |● |3 | |
| **Classificação multiclasse** | | | | | |
| [regressão logística](https://msdn.microsoft.com/library/azure/dn905853.aspx) | |● |● |5 | |
| [floresta de decisão](https://msdn.microsoft.com/library/azure/dn906015.aspx) |● |○ | |6 | |
| [selva de decisão ](https://msdn.microsoft.com/library/azure/dn905963.aspx) |● |○ | |6 |Volume de memória insuficiente |
| [rede neural](https://msdn.microsoft.com/library/azure/dn906030.aspx) |● | | |9 |[A personalização adicional é possível](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [one-v-all](https://msdn.microsoft.com/library/azure/dn905887.aspx) |- |- |- |- |Consulte as propriedades do método de duas classes hello selecionado |
| **Regressão** | | | | | |
| [linear](https://msdn.microsoft.com/library/azure/dn905978.aspx) | |● |● |4 | |
| [Linear Bayesiana](https://msdn.microsoft.com/library/azure/dn906022.aspx) | |○ |● |2 | |
| [floresta de decisão](https://msdn.microsoft.com/library/azure/dn905862.aspx) |● |○ | |6 | |
| [árvore de decisão aumentada](https://msdn.microsoft.com/library/azure/dn905801.aspx) |● |○ | |5 |Grande volume de memória |
| [Quantil de floresta rápida](https://msdn.microsoft.com/library/azure/dn913093.aspx) |● |○ | |9 |Distribuições em vez de previsões de ponto |
| [rede neural](https://msdn.microsoft.com/library/azure/dn905924.aspx) |● | | |9 |[A personalização adicional é possível](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [Poisson](https://msdn.microsoft.com/library/azure/dn905988.aspx) | | |● |5 |Tecnicamente linear de log. Para prever contagens |
| [ordinal](https://msdn.microsoft.com/library/azure/dn906029.aspx) | | | |0 |Para prever a ordem de classificação |
| **Detecção de anomalias** | | | | | |
| [máquina de vetor de suporte](https://msdn.microsoft.com/library/azure/dn913103.aspx) |○ |○ | |2 |Especialmente bom para conjuntos de recursos grandes |
| [Detecção de anomalias baseada em PCA](https://msdn.microsoft.com/library/azure/dn913102.aspx) | |○ |● |3 | |
| [K-means](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/) | |○ |● |4 |Um algoritmo de clustering |

**Propriedades do algoritmo:**

**●** -mostra excelente precisão, o tempo de treinamento rápido e o uso de saudação de linearidade

**○** - mostra boa precisão e tempos de treinamento moderados

## <a name="algorithm-notes"></a>Anotações sobre algoritmo
### <a name="linear-regression"></a>Regressão linear
Conforme mencionado anteriormente, [regressão linear](https://msdn.microsoft.com/library/azure/dn905978.aspx) se ajusta a um conjunto de dados toohello linha (ou plano ou hiperplano). Ela é uma força de trabalho, simples e rápida, mas pode ser muito simplista para alguns problemas.
Veja aqui um [tutorial de regressão linear](machine-learning-linear-regression-in-azure.md).

![Dados com uma tendência linear][3]

***Dados com uma tendência linear***

### <a name="logistic-regression"></a>Regressão logística
Embora erroneamente inclui 'regressão' no nome hello, Regressão logística é realmente uma ferramenta poderosa para [duas classes](https://msdn.microsoft.com/library/azure/dn905994.aspx) e [multiclasse](https://msdn.microsoft.com/library/azure/dn905853.aspx) classificação. É rápida e simples. Olá o fato de que ele usa de um '-moldada curva em vez de uma linha reta torna uma opção natural para dividir dados em grupos. A regressão logística oferece limites de classe lineares e, portanto, quando for usá-la, verifique se uma aproximação linear serve para você.

![Dados de classe tootwo de regressão logística com apenas um recurso][4]

***Dados de classe tootwo uma regressão logística com apenas um recurso*** *-o limite de classe é o ponto de saudação no qual Olá curva logística é fechar apenas como classes de tooboth*

### <a name="trees-forests-and-jungles"></a>Árvores, florestas e selvas
Florestas de decisão ([regressão](https://msdn.microsoft.com/library/azure/dn905862.aspx), [duas classes](https://msdn.microsoft.com/library/azure/dn906008.aspx) e [multiclasse](https://msdn.microsoft.com/library/azure/dn906015.aspx)), selvas de decisão ([duas classes](https://msdn.microsoft.com/library/azure/dn905976.aspx) e [multiclasse](https://msdn.microsoft.com/library/azure/dn905963.aspx)) e árvores de decisão aumentadas ([regressão](https://msdn.microsoft.com/library/azure/dn905801.aspx) e [duas classes](https://msdn.microsoft.com/library/azure/dn906025.aspx)) são todos baseados em árvores de decisão, um conceito fundamental de aprendizado de máquina. Há muitas variantes de árvores de decisão, mas fazem a mesma coisa — subdividir espaço do recurso Olá em regiões com principalmente Olá mesmo rótulo. Elas podem ser regiões de categoria consistente ou de valor constante, dependendo se você estiver fazendo classificação ou regressão.

![A árvore de decisão subdivide um espaço de recurso][5]

***Uma árvore de decisão subdivide um espaço de recursos em regiões de valores aproximadamente uniformes***

Como um espaço de recurso pode ser subdividido em regiões arbitrariamente pequenas, é fácil tooimagine dividindo eficiente suficiente toohave um ponto de dados por região. Esse é um exemplo extremo de superajuste. Ordem tooavoid isso, um grande conjunto de árvores são construídos com especial matemático cuidados que árvores de saudação não estão correlacionados. Média de saudação desta "floresta de decisão" é uma árvore que evita o sobreajuste. As florestas de decisão podem usar muita memória. Selvas de decisão são um tipo variant que consome menos memória à custa de saudação de um tempo de treinamento um pouco mais.

As árvores de decisão aumentadas evitam o superajuste ao limitarem o número de vezes que podem se subdividir e como poucos pontos de dados são permitidos em cada região. O algoritmo constrói uma sequência de árvores, cada um deles aprende para compensar o erro Olá deixado pela árvore Olá antes. resultado de saudação é um aprendiz muito preciso que tende a toouse muita memória. Para obter descrição técnico completo Olá, confira [papel original de Friedman](http://www-stat.stanford.edu/~jhf/ftp/trebst.pdf).

[A rápida de regressão de Quantil de floresta](https://msdn.microsoft.com/library/azure/dn913093.aspx) é uma variação de árvores de decisão para um caso especial de saudação onde você deseja saber não apenas Olá típico () valor mediano dos dados hello dentro de uma região, mas sua distribuição na forma de saudação de quantis.

### <a name="neural-networks-and-perceptrons"></a>Redes neurais e perceptrons
As redes neurais são algoritmos de aprendizado inspirados no cérebro que cobrem problemas [multiclasse](https://msdn.microsoft.com/library/azure/dn906030.aspx), de [duas classes](https://msdn.microsoft.com/library/azure/dn905947.aspx) e de [regressão](https://msdn.microsoft.com/library/azure/dn905924.aspx). Entram em uma série infinita, mas as redes neurais hello dentro de aprendizado de máquina do Azure são todas do formulário de saudação de gráficos acíclicos direcionados. Isso significa que os recursos de entrada são passados para a frente (nunca para trás) por meio de uma sequência de camadas transformadas em saídas. Em cada camada, as entradas são ponderadas em várias combinações, somado e passados para a próxima camada de saudação. Essa combinação de resultados de cálculos simples de toolearn a capacidade sofisticado tendências de limites e dados de classe, aparentemente por mágica. Em muitos níveis redes desse tipo executam hello "aprendizado" que alimenta reporting tanto de tecnologia e ficção científica.

No entanto, esse alto desempenho tem um preço. Redes neurais podem levar um longo tempo tootrain, especialmente para grandes conjuntos de dados com muitos recursos. Eles também têm mais parâmetros que a maioria dos algoritmos, o que significa que a limpeza de parâmetro expande tempo de treinamento de saudação muito.
E para esses overachievers que desejarem muito[especificar sua própria estrutura de rede](http://go.microsoft.com/fwlink/?LinkId=402867), as possibilidades são inesgotável.

![Limites aprendidas por redes neurais][6]
***limites Olá aprendidos por redes neurais podem ser complexos e irregulares***

Olá [perceptron de média de duas classes](https://msdn.microsoft.com/library/azure/dn906036.aspx) é o tempo de treinamento de tooskyrocketing de resposta de redes neurais. Ele usa uma estrutura de rede que fornece os limites de classe linear. É quase primitivo pelos padrões de hoje, mas ele tem uma longa história de trabalho robustez e é pequeno o suficiente toolearn rapidamente.

### <a name="svms"></a>SVMs
Suporte a máquinas de vetor (SVMs) encontrar limites Olá que separa as classes por como uma grande margem possível. Quando duas classes de saudação não podem ser claramente separados, algoritmos de saudação encontrar limites melhor hello, que eles podem. Conforme foi escrito no aprendizado de máquina do Azure, Olá [duas classes SVM](https://msdn.microsoft.com/library/azure/dn905835.aspx) faz isso com apenas uma linha reta. (No jargão da SVM, usa um kernel linear). Como faz essa aproximação linear, é capaz de toorun rapidamente. Mas o seu verdadeiro ponto forte são os dados de uso intenso de recursos, como texto ou genoma. Nesses casos SVMs são capazes de tooseparate classes mais rapidamente e com menos superajuste que a maioria dos outros algoritmos, além de toorequiring apenas uma pequena quantidade de memória.

![Limite de classe de computador de vetor de suporte][7]

***Um limite de classe de máquina de vetor suporte típico maximiza a margem Olá separando duas classes***

Outro produto da Microsoft Research, Olá [duas classes SVM profunda local](https://msdn.microsoft.com/library/azure/dn913070.aspx) é uma variante não linear de SVM que mantém a maioria de velocidade e memória eficiência da versão linear Olá Olá. Ele é ideal para casos em que a abordagem linear Olá não dá respostas precisas o suficiente. os desenvolvedores de saudação removeu rápido dividindo problema Olá em um grupo de pequenos problemas SVM lineares. Saudação de leitura [completo descrição](http://research.microsoft.com/um/people/manik/pubs/Jose13.pdf) para obter detalhes de saudação sobre como tirados esse truque.

Usando uma extensão inteligente de SVMs não lineares, Olá [SVM de uma classe](https://msdn.microsoft.com/library/azure/dn913103.aspx) desenha um limite que descreve totalmente Olá todo o conjunto de dados. Ela é útil para a detecção de anomalias. Quaisquer novos pontos de dados que estão muito fora desse limite são bastante incomum toobe notável.

### <a name="bayesian-methods"></a>Métodos Bayesianos
Os métodos Bayesianos possuem uma qualidade altamente desejável: eles evitam o superajuste. Eles fazem isso fazendo algumas suposições com antecedência sobre distribuição de probabilidade Olá de resposta de saudação. Outro subproduto dessa abordagem é que eles têm muito poucos parâmetros. O Azure Machine Learning tem dois algoritmos Bayesianos para classificação ([computador do ponto de Bayes de duas classes](https://msdn.microsoft.com/library/azure/dn905930.aspx)) e regressão ([regressão linear Bayesiana](https://msdn.microsoft.com/library/azure/dn906022.aspx)).
Observe que essas assumir que dados saudação podem ser divididos ou ajustar com uma linha reta.

Em uma nota histórica, os computadores de ponto de Bayes foram desenvolvidos no Microsoft Research. Eles têm algum trabalho teórico excepcionalmente belo por trás deles. aluno interessado Olá é direcionado toohello [artigo original em JMLR](http://jmlr.org/papers/volume1/herbrich01a/herbrich01a.pdf) e um [criteriosos blog por Chris Bishop](http://blogs.technet.com/b/machinelearning/archive/2014/10/30/embracing-uncertainty-probabilistic-inference.aspx).

### <a name="specialized-algorithms"></a>Algoritmos especializados
Se você tiver um objetivo muito específico, este talvez seja o seu dia de sorte. Em Olá coleção de aprendizado de máquina do Azure, há algoritmos especializadas em:

- previsão de classificação ([regressão ordinal](https://msdn.microsoft.com/library/azure/dn906029.aspx));
- previsão de contagem ([regressão Poisson](https://msdn.microsoft.com/library/azure/dn905988.aspx));
- detecção de anomalias (uma baseada na [análise de componentes principais](https://msdn.microsoft.com/library/azure/dn913102.aspx) e outra baseada em [máquinas de vetor de suporte](https://msdn.microsoft.com/library/azure/dn913103.aspx))
- clustering ([K-means](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/))

![Detecção de anomalias baseada em PCA][8]

***Detecção de anomalias com base em PCA*** *-a grande maioria Olá dos dados saudação se enquadra em uma distribuição stereotypical; pontos desviam drasticamente-se de que tipo de distribuição estão sob suspeita*

![Conjunto de dados agrupados usando K-means][9]

***Um conjunto de dados é agrupado em cinco clusters usando K-means***

Também há um ensemble [classificador multiclasse um-v-todos](https://msdn.microsoft.com/library/azure/dn905887.aspx), qual problema de classificação quebras Olá classe N problemas de classificação de duas classes de n-1. Propriedades de linearidade, tempo de treinamento e a precisão de saudação são determinadas por classificadores de duas classes Olá usados.

![Classificadores de duas classes combinados tooform um classificador de três classes][10]

***Um par de classificadores de duas classes combinar tooform um classificador de três classes***

Aprendizado de máquina do Azure também inclui o framework de aprendizado de máquina avançada tooa acesso sob o título de saudação do [Vowpal Wabbit](https://msdn.microsoft.com/library/azure/8383eb49-c0a3-45db-95c8-eb56a1fef5bf).
O VW desafia a categorização aqui, já que pode aprender problemas de classificação e de regressão e pode até aprender de dados parcialmente sem rótulo. Você pode configurá-lo toouse qualquer um de vários algoritmos de otimização, funções de perda e algoritmos de aprendizado. Ele foi criado Olá Terra backup toobe extremamente rápida, paralelo e eficiente. Ele lida com conjuntos de recursos absurdamente grandes com pouco esforço aparente.
Iniciado e liderado pelo próprio John Langford, da Microsoft Research, o VW é uma entrada de Fórmula 1 em um campo de algoritmos de stock cars. Nem todo problema se encaixa VW, mas se sua, ele pode ser vale a pena tooclimb a curva de aprendizado em sua interface. Ele também está disponível como [código-fonte aberto autônomo](https://github.com/JohnLangford/vowpal_wabbit) em várias linguagens.

## <a name="more-help-with-algorithms"></a>Obter ajuda com algoritmos
* Para obter um infográfico para baixar que descreve algoritmos e fornece exemplos, consulte [Infográfico para baixar: conceitos básicos do aprendizado de máquina com exemplos de algoritmo](machine-learning-basics-infographic-with-algorithm-examples.md).
* Para obter uma lista por categoria de algoritmos de aprendizado de máquina Olá todos disponíveis no estúdio de aprendizado de máquina do Azure, consulte [inicializar modelo] [ initialize-model] em hello algoritmo Studio de aprendizado de máquina e a Ajuda do módulo.
* Para obter uma lista completa em ordem alfabética dos algoritmos e dos módulos no Azure Machine Learning Studio, consulte a [Lista de A–Z de módulos do Machine Learning Studio][a-z-list] na Ajuda de algoritmo e módulo do Machine Learning Studio.
* toodownload e imprimir um diagrama que fornece uma visão geral dos recursos de saudação do estúdio de aprendizado de máquina do Azure, consulte [diagrama de visão geral dos recursos do estúdio de aprendizado de máquina do Azure](machine-learning-studio-overview-diagram.md).


<!-- Reference links -->
[initialize-model]: https://msdn.microsoft.com/library/azure/dn905812.aspx
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx

<!-- Media -->

[1]: ./media/machine-learning-algorithm-choice/image1.png
[2]: ./media/machine-learning-algorithm-choice/image2.png
[3]: ./media/machine-learning-algorithm-choice/image3.png
[4]: ./media/machine-learning-algorithm-choice/image4.png
[5]: ./media/machine-learning-algorithm-choice/image5.png
[6]: ./media/machine-learning-algorithm-choice/image6.png
[7]: ./media/machine-learning-algorithm-choice/image7.png
[8]: ./media/machine-learning-algorithm-choice/image8.png
[9]: ./media/machine-learning-algorithm-choice/image9.png
[10]: ./media/machine-learning-algorithm-choice/image10.png
