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
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a>Tutorial de aprendizado de máquina: Crie sua primeira experiência no Azure Machine Learning Studio

Se você nunca usou o **Azure Machine Learning Studio** antes, este tutorial é para você.

Neste tutorial, examinaremos como toouse Studio para Olá primeiro tempo toocreate uma experiência de aprendizado de máquina. experiência de saudação testar um modelo analítico que prevê o preço de saudação de um automóvel com base em variáveis diferentes, como criar e especificações técnicas.

> [!NOTE]
> Este tutorial mostra a você noções básicas de saudação como toodrag-e-soltar módulos para sua experiência, conectá-los, executar teste hello e examinar os resultados de saudação. Não vamos toodiscuss Olá tópico geral de aprendizado de máquina ou como tooselect e use Olá 100 + algoritmos e dados manipulação módulos internos incluídos no estúdio.
>
>Se você for novo aprendizado de toomachine, Olá série de vídeos [ciência de dados para iniciantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) pode ser um bom lugar toostart. Esta série de vídeos é aprendizado de toomachine uma ótima introdução usando linguagem cotidiana e conceitos.
>
>Se você estiver familiarizado com o aprendizado de máquina, mas você estiver procurando para obter mais informações sobre o estúdio de aprendizado de máquina e contém os algoritmos de aprendizado de máquina Olá, aqui estão alguns bons recursos:
>
- [O que é o Machine Learning Studio?](machine-learning-what-is-ml-studio.md) – Essa é uma visão geral do Estúdio.
- [Noções básicas com exemplos de algoritmo de aprendizado de máquina](machine-learning-basics-infographic-with-algorithm-examples.md) -este infográfico é útil se você quiser toolearn mais sobre os tipos diferentes de saudação de algoritmos de aprendizagem de máquina, incluídos no estúdio de aprendizado de máquina.
- [Guia de aprendizado de máquina](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -este guia inclui informações semelhantes como Olá infográfico acima, mas em um formato interativo.
- [Roteiro do algoritmo de aprendizado de máquina](machine-learning-algorithm-cheat-sheet.md) e [como toochoose algoritmos de aprendizado de máquina do Microsoft Azure](machine-learning-algorithm-choice.md) -este pôster baixável e o artigo complementar discutem algoritmos de Studio Olá em camadas.
- [Estúdio de aprendizado de máquina: Algoritmo e Ajuda do módulo](https://msdn.microsoft.com/library/azure/dn905974.aspx) -esta é a referência completa Olá para todos os módulos do Studio, incluindo algoritmos de aprendizagem de máquina

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a>Como o Machine Learning Studio ajuda?

O estúdio de aprendizado de máquina torna fácil tooset backup de um experimento usando arrastar e soltar módulos previamente programados com técnicas de modelagem de previsão.

Usando um espaço de trabalho visual, interativo, você arrasta e solta ***conjuntos de dados*** e ***módulos*** de análise em telas interativas. Você conectá-los junto tooform um ***experimentar*** que são executados no estúdio de aprendizado de máquina.
Você ***criar um modelo de***, ***treinar modelo Olá***, e ***pontuação e teste Olá modelo***.

Você pode iterar em seu design de modelo, editando experiência hello e executá-lo até que ele oferece você Olá resultados que você está procurando. Quando o modelo estiver pronto, você poderá publicá-lo como um ***serviço Web*** para que outras pessoas possam enviar novos dados e obter previsões em troca.

## <a name="open-machine-learning-studio"></a>Abrir o Machine Learning Studio

tooget Introdução ao Studio, vá muito[https://studio.azureml.net](https://studio.azureml.net). Se você já entrou no Machine Learning Studio antes, clique em **Entrar**. Caso contrário, clique em **Inscrever-se aqui** e escolha entre as opções gratuitas e pagas.

![Entrar no estúdio de aprendizado do tooMachine][sign-in-to-studio]
<br/>
***Entrar no estúdio de aprendizado do tooMachine***

## <a name="five-steps-toocreate-an-experiment"></a>Cinco etapas toocreate um experimento

Neste tutorial de aprendizado de máquina, você execute um teste no estúdio de aprendizado de máquina toocreate, treinamento, toobuild de cinco etapas básicas e classificar seu modelo:

- **Criar um modelo**
    - [Etapa 1: Obter dados]
    - [Etapa 2: Preparar dados saudação]
    - [Etapa 3: Definir recursos]
- **Treinar modelo de saudação**
    - [Etapa 4: Escolher e aplicar um algoritmo de aprendizado]
- **Pontuação e teste Olá modelo**
    - [Etapa 5: Prever novos preços de automóveis]

[Etapa 1: Obter dados]: #step-1-get-data
[Etapa 2: Preparar dados saudação]: #step-2-prepare-the-data
[Etapa 3: Definir recursos]: #step-3-define-features
[Etapa 4: Escolher e aplicar um algoritmo de aprendizado]: #step-4-choose-and-apply-a-learning-algorithm
[Etapa 5: Prever novos preços de automóveis]: #step-5-predict-new-automobile-prices

> [!TIP] 
> Você pode encontrar uma cópia de trabalho do hello seguintes experiência em Olá [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com). Vá muito**[sua primeira ciência de dados de experiências - previsão de preços de automóvel](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  e clique em **aberto no Studio** toodownload uma cópia do experimento Olá para o aprendizado de máquina Espaço de trabalho do Studio.


## <a name="step-1-get-data"></a>Etapa 1: Obter dados

Olá primeira coisa tooperform aprendizado de máquina é de dados.
Há uma série de conjuntos de dados de exemplo incluídos no Machine Learning Studio que você pode usar ou você pode importar dados de várias fontes. Neste exemplo, vamos usar conjunto de dados de exemplo hello, **dados de preços de automóvel (Raw)**, que está incluído no espaço de trabalho.
Esse conjunto de dados inclui entradas para vários automóveis individuais, incluindo informações como marca, modelo, especificações técnicas e preço.

Aqui está como tooget Olá o conjunto de dados em sua experiência.

1. Crie um novo teste clicando **+ novo** na Olá inferior da janela do estúdio de aprendizado de máquina hello, selecione **EXPERIMENTAR**e, em seguida, selecione **experiências em branco**.

2. experiência de saudação recebe um nome padrão que você pode ver na parte superior de saudação da tela hello. Selecione esse texto e renomear toosomething significativo, por exemplo, **previsão de preços de automóvel**. nome da saudação não precisa toobe exclusivo.

    ![Renomear experimento Olá][rename-experiment]

2. toohello esquerda da tela de experimento Olá é uma paleta de conjuntos de dados e módulos. Tipo **automóvel** na caixa de pesquisa de saudação na parte superior da saudação deste conjunto de paleta toofind Olá dados rotulados **dados de preços de automóvel (Raw)**. Arraste esta tela de experimento toohello conjunto de dados.

    ![Localizar automóvel Olá de conjunto de dados e arraste-o para a tela de experimento Olá][type-automobile]
    <br/>
    ***Localizar automóvel Olá de conjunto de dados e arraste-o para a tela de experimento Olá***

toosee esses dados aparência como, clique em Olá a porta de saída na parte inferior de saudação do automóvel Olá de conjunto de dados e, em seguida, selecione **visualizar**.

![Clique em porta de saída de hello e selecione "Visualizar"][select-visualize]
<br/>
***Clique em porta de saída de hello e selecione "Visualizar"***

> [!TIP]
> Conjuntos de dados e módulos com entrada e portas de saída representadas por círculos pequenos - portas de entrada na parte superior do hello, saída portas na parte inferior da saudação.
toocreate um fluxo de dados por meio de sua experiência, você se conectará uma porta de saída da porta de entrada tooan um módulo de outro.
A qualquer momento, você pode clicar em Olá a porta de saída de um conjunto de dados ou o módulo toosee quais Olá aparência dos dados nesse ponto no fluxo de dados de saudação.

Neste conjunto de dados de exemplo, cada instância de um automóvel aparece como uma linha e variáveis de saudação associadas a cada automóvel aparecem como colunas. Considerando variáveis Olá para um automóvel específico, vamos preço de saudação do tootry toopredict na coluna à direita (coluna 26, intitulada "price").

![Exibir dados de automóvel Olá na janela de visualização de dados Olá][visualize-auto-data]
<br/>
***Exibir dados de automóvel Olá na janela de visualização de dados Olá***

Janela de visualização de saudação fechar clicando hello "**x**" no canto superior direito de saudação.

## <a name="step-2-prepare-hello-data"></a>Etapa 2: Preparar dados saudação

Um conjunto de dados geralmente requer algum pré-processamento antes de poder ser analisado. Por exemplo, você deve ter notado Olá faltando valores presentes nas colunas de saudação de várias linhas. Esses valores ausentes precisam toobe limpo modelo Olá pode analisar dados saudação corretamente. Em nosso caso, vamos remover quaisquer linhas que contém valores ausentes. Além disso, Olá **perdas normalizadas** coluna tem uma grande proporção de valores ausentes, portanto, o excluiremos essa coluna de modelo Olá completamente.

> [!TIP]
> Olá limpeza não valores de dados de entrada é um pré-requisito para usando a maioria dos módulos de saudação.

Primeiro, adicione um módulo que remove Olá **perdas normalizadas** coluna completamente, e, em seguida, podemos adicionar outro módulo que remove qualquer linha que tem dados ausentes.

1. Tipo **selecionar colunas** na caixa de pesquisa de saudação na parte superior da saudação de saudação do hello módulo paleta toofind [selecionar colunas no conjunto de dados] [ select-columns] módulo, arraste-a como tela de experimento toohello . Esse módulo permite tooselect Olá a quais colunas de dados que deseja tooinclude ou excluir no modelo.

2. Conecte-se a porta de saída de saudação do hello **dados de preços de automóvel (Raw)** toohello de conjunto de dados de entrada porta Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo.

    ![Adicione a tela de experimento hello "Selecionar colunas no conjunto de dados" módulo toohello e conectá-lo][type-select-columns]
    <br/>
    ***Adicione a tela de experimento hello "Selecionar colunas no conjunto de dados" módulo toohello e conectá-lo***

3. Clique em Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo e clique em **seletor de coluna iniciar** em Olá **propriedades** painel.

    - Olá esquerda, clique em **com regras**
    - Em **Começa com**, clique em **Todas as colunas**. Isso instrui [selecionar colunas no conjunto de dados] [ select-columns] toopass por meio de todas as colunas de saudação (exceto as colunas que estamos sobre tooexclude).
    - Olá listas suspensas, selecione **excluir** e **nomes de coluna**e, em seguida, clique na caixa de texto de saudação. Uma lista de colunas é exibida. Selecione **perdas normalizadas**, e é adicionado toohello caixa de texto.
    - Clique no hello marca de seleção (Okey) botão tooclose Olá seletor de coluna (em Olá inferior direito).

    ![Iniciar seletor de coluna hello e excluir coluna hello "perdas normalizadas"][launch-column-selector]
    <br/>
    ***Iniciar seletor de coluna hello e excluir coluna hello "perdas normalizadas"***

    Painel de propriedades de saudação agora para **selecionar colunas no conjunto de dados** indica que passa por todas as colunas do conjunto de dados Olá exceto **perdas normalizadas**.

    ![Painel de propriedades de saudação mostra que essa coluna hello "perdas normalizadas" foi excluída][showing-excluded-column]
    <br/>
    ***Painel de propriedades de saudação mostra que essa coluna hello "perdas normalizadas" foi excluída***

    > [!TIP]
    Você pode adicionar um módulo de tooa comentário clicando duas vezes em módulo de saudação e a inserção de texto. Isso pode ajudá-lo a ver rapidamente quais módulo hello está fazendo sua experiência. Nesse caso clique duas vezes em Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo e tipo hello comentário "Excluir normalizado perdas."
    >
    >


    ![Clique duas vezes em um módulo tooadd um comentário][add-comment]
    <br/>
    ***Clique duas vezes em um módulo tooadd um comentário***

3. Saudação de arrastar [limpar dados ausentes] [ clean-missing-data] toohello módulo experimentar tela e conectá-lo toohello [selecionar colunas no conjunto de dados] [ select-columns] módulo. Em Olá **propriedades** painel, selecione **remover toda a linha** em **modo de limpeza**. Isso instrui [limpar dados ausentes] [ clean-missing-data] tooclean dados de saudação removendo linhas com valores ausentes. Clique duas vezes no módulo hello e digite o comentário hello "Remover linhas de valor ausente".

    ![Definir o modo de limpeza de saudação muito "remover toda a linha" para o módulo de "Limpar dados ausentes" hello][set-remove-entire-row]
    <br/>
    ***Definir o modo de limpeza de saudação muito "remover toda a linha" para o módulo de "Limpar dados ausentes" hello***

4. Executar o teste de saudação clicando **executar** final Olá Olá página.

    Quando experimento Olá concluiu a execução, todos os módulos de saudação tem tooindicate uma marca de seleção verde que eles foi concluídos com êxito. Observe também Olá **terminar execução** status no canto superior direito de saudação.

![Depois de executá-lo, experimento Olá deve ser semelhante este][early-experiment-run]
<br/>
***Depois de executá-lo, experimento Olá deve ser semelhante este***

> [!TIP]
> Por que executamos experimento Olá agora? Por experiência de saudação em execução, definições de coluna Olá para nossos dados passam de conjunto de dados hello, por meio de saudação [selecionar colunas no conjunto de dados] [ select-columns] módulo e por meio de saudação [limpar dados ausentes] [ clean-missing-data] módulo. Isso significa que todos os módulos nos conectamos muito[limpar dados ausentes] [ clean-missing-data] também terá essas mesmas informações.

Tudo o que fizemos experimento Olá toothis ponto é dados saudação normal. O conjunto de dados do tooview Olá limpo, clique em Olá deixado porta de saída de hello [limpar dados ausentes] [ clean-missing-data] módulo e selecione **visualizar**. Observe que Olá **perdas normalizadas** coluna não é mais incluída e não existem valores ausentes.

Agora que os dados saudação estão limpas, estamos toospecify pronto quais recursos nós vamos toouse no modelo de previsão de saudação.

## <a name="step-3-define-features"></a>Etapa 3: Definir recursos

No aprendizado de máquina, *recursos* são propriedades individuais mensuráveis de algo em que você está interessado. Em nosso conjunto de dados, cada linha representa um automóvel e cada coluna é um recurso desse automóvel.

Localizando um bom conjunto de recursos para criar um modelo de previsão requer conhecimento sobre o problema de saudação e experimentação desejadas toosolve. Alguns recursos são melhores para prever um destino de saudação que outros. Além disso, alguns recursos têm uma forte correlação com outros recursos e podem ser removidos. Por exemplo, mpg cidade e estrada mpg estão intimamente relacionados podemos manter uma e remover outros Olá sem afetar significativamente a previsão de saudação.

Vamos criar um modelo que usa um subconjunto de recursos de saudação em nosso conjunto de dados. Volte mais tarde e selecionar recursos diferentes, execute novamente o teste de saudação e consulte se você obter resultados melhores. Mas toostart, vamos tentar Olá recursos a seguir:

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. Arraste outro [selecionar colunas no conjunto de dados] [ select-columns] toohello módulo experimentar a tela. Conecte-se a saudação à esquerda a porta de saída de hello [limpar dados ausentes] [ clean-missing-data] entrada do módulo toohello de saudação [selecionar colunas no conjunto de dados] [ select-columns] módulo.

    ![Conecte-se o módulo de "Limpar dados ausentes" hello "Selecionar colunas no conjunto de dados" módulo toohello][connect-clean-to-select]
    <br/>
    ***Conecte-se o módulo de "Limpar dados ausentes" hello "Selecionar colunas no conjunto de dados" módulo toohello***

2. Clique duas vezes no módulo hello e digite "Selecionar recursos para previsão."

2. Clique em **seletor de coluna iniciar** em Olá **propriedades** painel.

3. Clique em **Com regras**.

4. Em **Começa com**, clique em **Nenhuma coluna**. Na linha de filtro hello, selecione **incluir** e **nomes de coluna** e selecione a lista de nomes de coluna na caixa de texto de saudação. Isso instrui Olá módulo toonot a passagem de todas as colunas (recursos) exceto Olá aqueles que especificamos.

5. Clique o botão de marca de seleção (Okey) hello.

    ![Selecione Olá colunas (recursos) tooinclude na previsão Olá][select-columns-to-include]
    <br/>
    ***Selecione Olá colunas (recursos) tooinclude na previsão Olá***

Isso produz um conjunto de dados filtrado que contém apenas recursos Olá que queremos toohello toopass usaremos na próxima etapa de saudação do algoritmo de aprendizado. Posteriormente, é possível retornar e tentar novamente com uma seleção diferente de recursos.

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a>Etapa 4: Escolher e aplicar um algoritmo de aprendizado

Agora que os dados de saudação estiverem prontos, criar um modelo de previsão consiste em treinamento e teste. Vamos usar nosso modelo de saudação do tootrain de dados e, em seguida, nós o testaremos Olá modelo toosee proximidade é toopredict capaz de preços.
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

*Classificação* e *regressão* são dois tipos de técnicas de algoritmo de machine learning supervisionado. A classificação prevê uma resposta de um conjunto definido de categorias, como uma cor (vermelha, azul ou verde). A regressão é usada toopredict um número.

Como desejamos toopredict preço, que é um número, vamos usar um algoritmo de regressão. Neste exemplo, usaremos um modelo simples de *regressão linear*.

> [!TIP]
> Se você quiser toolearn mais informações sobre tipos diferentes de algoritmos de aprendizado de máquina e quando toouse-los, você pode exibir vídeo primeiro Olá no hello ciência de dados para a série de iniciantes [Olá cinco perguntas respostas de ciência de dados](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md). Você também poderá examinar Olá infográfico [Noções básicas com exemplos de algoritmo de aprendizado de máquina](machine-learning-basics-infographic-with-algorithm-examples.md), ou check-out Olá [roteiro do algoritmo de aprendizado de máquina](machine-learning-algorithm-cheat-sheet.md).

Treinamos modelo hello, dando a ele um conjunto de dados que inclui o preço de saudação. modelo de saudação examina dados saudação e procure correlações entre os recursos do exemplo um automóvel e seu preço. Em seguida, nós o testaremos modelo Olá - vamos dar a ele um conjunto de recursos para automóveis com que estamos familiarizados e veja como fechar modelo Olá vem preço conhecidos do toopredicting hello.

Vamos usar nossos dados de treinamento de modelo hello e testá-lo ao dividir dados saudação em conjuntos de dados de teste e treinamento separado.

1. Selecione e arraste Olá [dividir dados] [ split] toohello módulo experimentar tela e conectá-lo toohello última [selecionar colunas no conjunto de dados] [ select-columns] módulo.

2. Clique em Olá [dividir dados] [ split] módulo tooselect-lo. Localize Olá **fração de linhas na Olá primeiro conjunto de dados de saída** (no hello **propriedades** toohello painel à direita da tela de saudação) e defina-a como too0.75. Dessa forma, vamos usar 75 por cento Olá tootrain saudação do modelo de dados e reter 25% para teste (mais tarde, você pode experimentar diferentes porcentagens de uso).

    ![Olá conjunto dividir fração de hello "Dividir dados" módulo too0.75][set-split-data-percentage]
    <br/>
    ***Olá conjunto dividir fração de hello "Dividir dados" módulo too0.75***

    > [!TIP]
    > Alterando Olá **semente aleatória** parâmetro, você pode produzir diferentes amostras aleatórias para treinamento e teste. Este parâmetro controla a propagação do gerador de número pseudoaleatório Olá Olá.

2. Execute teste de saudação. Quando é executado experimento hello, Olá [selecionar colunas no conjunto de dados] [ select-columns] e [dividir dados] [ split] módulos passam toohello de definições de coluna módulos que incluiremos lado.  

3. Olá tooselect aprendizado algoritmo, expanda Olá **aprendizado de máquina** categoria no hello módulo paleta toohello à esquerda da saudação tela e, em seguida, expanda **inicializar modelo**. Isso exibe várias categorias de módulos que podem ser algoritmos de aprendizado de máquina tooinitialize usado. Para esse teste, selecione Olá [Regressão Linear] [ linear-regression] módulo em Olá **regressão** categoria e arraste-a tela de experimento toohello.
(Você também pode encontrar hello módulo digitando "regressão linear" na caixa de pesquisa de paleta hello.)

4. Localizar e arraste Olá [treinar modelo] [ train-model] toohello módulo experimentar a tela. Conecte a saída de saudação do hello [Regressão Linear] [ linear-regression] entrada de saudação à esquerda do módulo toohello [treinar modelo] [ train-model] módulo e conecte-se Olá treinamento de saída de dados (porta da esquerda) da saudação [dividir dados] [ split] entrada à direita do módulo toohello de saudação [treinar modelo] [ train-model] módulo.

    ![Conecte-se hello "Modelo de treinamento" módulo tooboth hello "Regressão Linear" e "Dados de divisão" módulos][connect-train-model]
    <br/>
    ***Conecte-se hello "Modelo de treinamento" módulo tooboth hello "Regressão Linear" e "Dados de divisão" módulos***

5. Clique em Olá [treinar modelo] [ train-model] módulo, clique em **seletor de coluna iniciar** em hello **propriedades** painel e, em seguida, selecione Olá **preço** coluna. Este é o valor de saudação nosso modelo é toopredict contínuo.

    Selecione Olá **preço** coluna no seletor de coluna hello, movendo-os de saudação **colunas disponíveis** lista toohello **colunas selecionadas** lista.

    ![Selecionar coluna de preço Olá para o módulo de "Modelo de treinamento" hello][select-price-column]
    <br/>
    ***Selecionar coluna de preço Olá para o módulo de "Modelo de treinamento" hello***

6. Execute teste de saudação.

Agora temos um modelo de regressão treinado que pode ser usado tooscore novos dados automóvel toomake preço previsões.

![Depois de executar, experimento Olá agora deve ser semelhante a este][second-experiment-run]
<br/>
***Depois de executar, experimento Olá agora deve ser semelhante a este***

## <a name="step-5-predict-new-automobile-prices"></a>Etapa 5: Prever novos preços de automóveis

Agora que nós já treinar o modelo de saudação usando 75% de nossos dados, podemos usar isso tooscore Olá outros 25 por cento de saudação dados toosee bem como funções de nosso modelo.

1. Localizar e arraste Olá [modelo de pontuação] [ score-model] toohello módulo experimentar a tela. Conecte a saída de saudação do hello [treinar modelo] [ train-model] toohello do módulo à esquerda de porta de entrada de [modelo de pontuação][score-model]. Conecte Olá teste dados saída (porta à direita) da saudação [dividir dados] [ split] toohello do módulo à direita de porta de entrada [modelo de pontuação][score-model].

    ![Conecte-se hello "Modelo de pontuação" módulo tooboth hello "Modelo de treinamento" e "Dados de divisão" módulos][connect-score-model]
    <br/>
    ***Conecte-se hello "Modelo de pontuação" módulo tooboth hello "Modelo de treinamento" e "Dados de divisão" módulos***

2. Executar teste hello e exibir saída de saudação do hello [modelo de pontuação] [ score-model] módulo (clique a porta de saída Olá [modelo de pontuação] [ score-model] e selecione **Visualizar**). Olá saída mostra Olá valores previstos para preço e Olá valores conhecidos de dados de teste de saudação.  

    ![Saída do módulo de "Modelo de pontuação" hello][score-model-output]
    <br/>
    ***Saída do módulo de "Modelo de pontuação" hello***

3. Por fim, podemos testar qualidade Olá dos resultados de saudação. Selecione e arraste Olá [avaliar modelo] [ evaluate-model] toohello módulo experiências de tela e conecte a saída Olá de saudação [modelo de pontuação] [ score-model] módulo toohello deixado entrada de [avaliar modelo][evaluate-model].

    > [!TIP]
    > Existem duas portas de entrada hello [avaliar modelo] [ evaluate-model] módulo porque ele pode ser usado toocompare dois modelos lado a lado. Posteriormente, você pode adicionar outro teste de toohello do algoritmo e usar [avaliar modelo] [ evaluate-model] toosee que fornece resultados melhores.

4. Execute teste de saudação.

saída de hello tooview de saudação [avaliar modelo] [ evaluate-model] módulo, clique em Olá porta de saída e, em seguida, selecione **visualizar**.

![Resultados da avaliação de experimento Olá][evaluation-results]
<br/>
***Resultados da avaliação de experimento Olá***

Olá estatísticas a seguir é mostrada para nosso modelo:

- **Erro de média absoluta** (MAE): Olá média dos erros absolutos (um *erro* Olá diferença entre Olá previsto valor e o valor real de saudação).
- **Erro ao quadrado da raiz significa** (RMSE): raiz quadrada de saudação da média de saudação de erros ao quadrado de previsões feitas no conjunto de dados de teste de saudação.
- **Erro absoluto relativo**: Olá média de diferença absoluta do erros absoluto toohello relativa entre os valores reais e Olá média de todos os valores reais.
- **Erro ao quadrado relativo**: diferença entre os valores reais hello e média de saudação de todos os valores reais de quadrado da média de saudação do toohello de erros ao quadrado relativo.
- **Coeficiente de determinação**: Olá também conhecido como **R quadrado valor**, essa é uma métrica estatística que indica como um modelo se ajusta a dados saudação.

Para cada erro Olá estatísticas, menor são melhor. Um valor menor indica que o previsões hello mais de perto correspondem os valores reais hello. Para **coeficiente de determinação**, hello mais próximo seu valor é tooone (1.0), melhores previsões de Olá Olá.

## <a name="final-experiment"></a>Experimento final

teste final Olá deve ter esta aparência:

![teste final Olá][complete-linear-regression-experiment]
<br/>
***teste final Olá***

## <a name="next-steps"></a>Próximas etapas

Agora que você concluiu o tutorial de aprendizado de máquina primeiro hello e tiver sua experiência configurada, você pode continuar tooimprove modelo de saudação e, em seguida, implantá-lo como um serviço web de previsão.

- **Iterar modelo de saudação do tootry tooimprove** -por exemplo, você pode alterar os recursos de saudação usar em sua previsão. Ou você pode modificar as propriedades de saudação do hello [Regressão Linear] [ linear-regression] algoritmo ou tente um algoritmo diferente completamente. Até mesmo, você pode adicionar vários computadores ao mesmo tempo de experiência de tooyour de algoritmos de aprendizado e comparar duas delas usando Olá [avaliar modelo] [ evaluate-model] módulo.
Para obter um exemplo de como toocompare vários modelos em uma única experiência, consulte [comparar Regressores](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) em Olá [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com).

    > [!TIP]
    > toocopy qualquer iteração de sua experiência, use Olá **Salvar como** botão final Olá Olá página. Você pode ver todas as iterações de saudação da sua experiência clicando **exibir o histórico de execução** final Olá Olá página. Para obter mais detalhes, consulte [Gerenciar iterações do experimento no Azure Machine Learning Studio][runhistory].

[runhistory]: machine-learning-manage-experiment-iterations.md

- **Implantar o modelo hello como um serviço web de previsão** - quando você estiver satisfeito com seu modelo, você pode implantá-lo como um toobe de serviço da web usado preços de automóvel toopredict usando novos dados. Consulte [Implantar um serviço Web do Azure Machine Learning][publish] para obter mais detalhes.

[publish]: machine-learning-publish-a-machine-learning-web-service.md

Deseja toolearn mais? Para obter uma explicação mais ampla e detalhada do processo de saudação de criação, treinamento, pontuação e implantando um modelo, consulte [desenvolver uma solução de previsão usando o aprendizado de máquina do Azure][walkthrough].

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
