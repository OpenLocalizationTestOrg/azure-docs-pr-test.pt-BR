---
title: "Etapa 4: Treinar e avaliar modelos de análise preditiva Olá | Microsoft Docs"
description: "Etapa 4 do hello desenvolver um passo a passo de solução de previsão: trem, classificar e avaliar vários modelos no estúdio de aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a>Etapa 4 do passo a passo: Treinar e avaliar modelos de análise preditiva Olá
Este tópico contém a quarta etapa Olá Olá explicação passo a passo, [desenvolver uma solução de análise preditiva em aprendizado de máquina do Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. 
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Carregar dados existentes](machine-learning-walkthrough-2-upload-data.md)
3. [Criar um novo teste](machine-learning-walkthrough-3-create-new-experiment.md)
4. **Treinar e avaliar modelos Olá**
5. [Implantar o serviço Web de saudação](machine-learning-walkthrough-5-publish-web-service.md)
6. [Acessar o serviço Web Olá](machine-learning-walkthrough-6-access-web-service.md)

- - -
Um dos benefícios de saudação do estúdio de aprendizado de máquina do Azure para criar modelos de aprendizado de máquina é Olá capacidade tootry mais de um tipo de modelo de cada vez em uma única experiência e comparar os resultados de saudação. Esse tipo de experimentação ajuda você a encontrar a melhor solução de saudação para o seu problema.

Experiência de saudação que desenvolve neste passo a passo, vamos criar dois tipos diferentes de modelos e, em seguida, compare seu toodecide resultados pontuação qual algoritmo queremos toouse em nossa experiência final.  

Existem diversos modelos dentre os quais podemos escolher. modelos de saudação toosee disponíveis, expanda Olá **aprendizado de máquina** nó na paleta de módulo Olá e, em seguida, expanda **inicializar modelo** e Olá nós abaixo dela. Para fins de saudação desse teste, estamos selecionará Olá [máquina de vetor de suporte de duas classes] [ two-class-support-vector-machine] (SVM) e hello [árvore de decisão ampliada de duas classes] [ two-class-boosted-decision-tree] módulos.    

> [!TIP]
> Ajuda tooget decidir qual algoritmo de aprendizado de máquina melhor atende às problema específico de saudação estiver tentando toosolve, consulte [como toochoose algoritmos de aprendizado de máquina do Microsoft Azure](machine-learning-algorithm-choice.md).
> 
> 

## <a name="train-hello-models"></a>Treinar modelos Olá

Vamos adicionar os dois Olá [árvore de decisão ampliada de duas classes] [ two-class-boosted-decision-tree] módulo e [máquina de vetor de suporte de duas classes] [ two-class-support-vector-machine] módulo neste experiência.

### <a name="two-class-boosted-decision-tree"></a>Árvore de decisão aumentada em duas classes

Primeiro, vamos configurar o modelo de árvore de decisão ampliada de saudação.

1. Localize Olá [árvore de decisão ampliada de duas classes] [ two-class-boosted-decision-tree] módulo na paleta de módulo hello e arraste-o para a tela hello.

2. Localize Olá [treinar modelo] [ train-model] módulo, arraste-o para a tela hello e, em seguida, conecte a saída de saudação do hello [árvore de decisão ampliada de duas classes] [ two-class-boosted-decision-tree]porta de entrada de saudação à esquerda do módulo toohello [treinar modelo] [ train-model] módulo.
   
   Olá [árvore de decisão ampliada de duas classes] [ two-class-boosted-decision-tree] módulo inicializa modelo genérico de Olá, e [treinar modelo] [ train-model] usa dados de treinamento modelo de saudação tootrain. 

3. Conecte a saída à esquerda Olá da esquerda Olá [Executar Script R] [ execute-r-script] porta de saudação de entrada do módulo toohello direito [treinar modelo] [ train-model] módulo (nós decidir em [etapa 3](machine-learning-walkthrough-3-create-new-experiment.md) desses dados passo a passo toouse hello proveniente Olá lado esquerdo de módulo de dividir dados Olá para treinamento).
   
   > [!TIP]
   > Não é necessário duas entradas hello e uma das saídas de saudação do hello [Executar Script R] [ execute-r-script] módulo para esse teste, portanto, pode deixá-los desanexada. 
   > 
   > 

Esta parte da experiência de saudação agora tem a seguinte aparência:  

![Treinando um modelo][1]

Agora precisamos Olá tootell [treinar modelo] [ train-model] que desejamos que o valor de risco de crédito Olá modelo toopredict saudação do módulo.

1. Selecione Olá [treinar modelo] [ train-model] módulo. Em Olá **propriedades** painel, clique em **seletor de coluna iniciar**.

2. Em Olá **selecionar uma única coluna** caixa de diálogo, digite "risco de crédito" no campo de pesquisa de saudação em **colunas disponíveis**, selecione "Risco de crédito" abaixo e clique botão de seta para a direita da saudação ( **>** ) toomove muito "crédito risco"**colunas selecionadas**. 

    ![Selecionar coluna de risco de crédito Olá para o módulo treinar modelo de saudação][0]

3. Clique em Olá **Okey** marca de seleção.

### <a name="two-class-support-vector-machine"></a>Computador de vetor de suporte de duas classes

Em seguida, configuramos o modelo SVM hello.  

Primeiro, uma pequena explicação sobre o SVM. Árvores de decisão aumentadas funcionam bem com recursos de qualquer tipo. No entanto, desde que o módulo SVM hello gera um classificador linear, o modelo de saudação que ele gera tem erro de teste melhor hello quando todos os recursos numéricos tem Olá mesma escala. tooconvert numérico todos os recursos toohello mesmo dimensionar, usamos uma transformação de "Tanh" (com hello [normalizar dados] [ normalize-data] módulo). Isso transforma os números em intervalo Olá [0,1]. módulo SVM Olá converte os recursos de toocategorical de recursos de cadeia de caracteres e, em seguida, de toobinary 0/1, portanto, não precisa toomanually transformar os recursos de cadeia de caracteres. Além disso, nós não desejamos tootransform Olá risco de crédito coluna (21) - ele for numérico, mas é valor Olá nós estiver treinamento Olá toopredict de modelo, por isso, precisamos tooleave-lo sozinho.  

tooset o modelo de SVM hello, Olá a seguir:

1. Localize Olá [máquina de vetor de suporte de duas classes] [ two-class-support-vector-machine] módulo na paleta de módulo hello e arraste-o para a tela hello.

2. Saudação de atalho [treinar modelo] [ train-model] módulo, selecione **cópia**e, em seguida, clique com botão direito tela hello e selecione **colar**. Olá cópia da saudação [treinar modelo] [ train-model] módulo tem Olá mesmo seleção de coluna como Olá original.

3. Conecte a saída de saudação do hello [máquina de vetor de suporte de duas classes] [ two-class-support-vector-machine] toohello do módulo à esquerda a porta de entrada de saudação segundo [treinar modelo] [ train-model] módulo.

4. Localize Olá [normalizar dados] [ normalize-data] módulo e arraste-o para a tela hello.

5. Conecte a saída à esquerda Olá da esquerda Olá [Executar Script R] [ execute-r-script] entrada do módulo toohello deste módulo (Observe que Olá a porta de saída de um módulo pode ser conectado toomore que um outro módulo).

6. Conectar-se a saudação à esquerda a porta de saída de hello [normalizar dados] [ normalize-data] toohello do módulo à direita de entrada porta Olá segundo [treinar modelo] [ train-model] módulo.

Esta parte de nosso teste deve se parecer um pouco com o seguinte:  

![Modelo de segundo de saudação do treinamento][2]  

Configurar Olá [normalizar dados] [ normalize-data] módulo:

1. Clique em Olá tooselect [normalizar dados] [ normalize-data] módulo. Em Olá **propriedades** painel, selecione **Tanh** para Olá **método de transformação** parâmetro.

2. Clique em **seletor de coluna iniciar**, não selecione "Nenhum colunas" para **começa com**, selecione **incluir** no hello primeiro menu suspenso, selecione **tipo de coluna**Olá segundo menu suspenso e selecione **numérico** na lista suspensa de terceiro hello. Especifica que todos os hello colunas numéricas (e somente numérico) são transformadas.

3. Clique em Olá toohello de sinal de adição (+) à direita dessa linha - isso cria uma linha de listas suspensas. Selecione **excluir** no hello primeiro menu suspenso, selecione **nomes de coluna** Olá segundo menu suspenso e digite "Risco de crédito" no campo de texto de saudação. Isso especifica a coluna Olá risco de crédito deve ser ignorada (precisamos toodo isso porque essa coluna é numérica e assim seria transformado se podemos não excluí-la).

4. Clique em Olá **Okey** marca de seleção.  

    ![Selecione as colunas para o módulo de normalizar dados Olá][5]

Olá [normalizar dados] [ normalize-data] módulo agora é conjunto tooperform uma transformação Tanh em todas as colunas numéricas, exceto a coluna de risco de crédito hello.  

## <a name="score-and-evaluate-hello-models"></a>Classificar e avaliar modelos Olá

Usamos Olá dados de teste que foi separados por Olá [dividir dados] [ split] tooscore módulo nossos modelos treinados. Podemos pode comparar resultados Olá Olá dois modelos toosee que gerou resultados melhores.  

### <a name="add-hello-score-model-modules"></a>Adicionar módulos do modelo de pontuação Olá

1. Localize Olá [modelo de pontuação] [ score-model] módulo e arraste-o para a tela hello.

2. Conecte-se a saudação [treinar modelo] [ train-model] módulo que está conectado toohello [árvore de decisão ampliada de duas classes] [ two-class-boosted-decision-tree] entrada do módulo toohello esquerda porta de saudação [modelo de pontuação] [ score-model] módulo.

3. Conecte-se o direito de saudação [Executar Script R] [ execute-r-script] toohello de módulo (nossos dados de teste) à direita de entrada porta Olá [modelo de pontuação] [ score-model] módulo.

    ![Módulo Modelo de Pontuação conectado][6]
   
   Olá [modelo de pontuação] [ score-model] módulo agora pode ter informações de crédito de saudação do hello dados, executados-lo por meio do modelo de saudação de teste e comparar previsões de saudação modelo hello gera com hello real risco de crédito coluna Olá dados de teste.

4. Copie e cole Olá [modelo de pontuação] [ score-model] toocreate módulo uma segunda cópia.

5. Conecte a saída de saudação do modelo SVM hello (ou seja, porta de saudação de saída de hello [treinar modelo] [ train-model] módulo que está conectado toohello [máquina de vetor de suporte de duas classes] [ two-class-support-vector-machine] módulo) toohello entrada porta Olá segundo [modelo de pontuação] [ score-model] módulo.

6. Para o modelo SVM hello, temos toodo Olá mesmo dados de teste de toohello de transformação como fizemos toohello dados de treinamento. Para copiar e colar Olá [normalizar dados] [ normalize-data] toocreate módulo uma segunda cópia e conecte-o direito de toohello [Executar Script R] [ execute-r-script] módulo.

7. Conecte-se a saída à esquerda Olá Olá segundo [normalizar dados] [ normalize-data] toohello do módulo à direita de entrada porta Olá segundo [modelo de pontuação] [ score-model] módulo.

    ![Os dois módulos Modelo de Pontuação estão conectados][7]

### <a name="add-hello-evaluate-model-module"></a>Adicionar módulo de avaliar modelo Olá

tooevaluate Olá dois resultados de pontuação e compará-los, usamos um [avaliar modelo] [ evaluate-model] módulo.  

1. Localize Olá [avaliar modelo] [ evaluate-model] módulo e arraste-o para a tela hello.

2. Conecte-se a porta de saída de saudação do hello [modelo de pontuação] [ score-model] módulo associado Olá ampliada decisão toohello de modelo de árvore à esquerda de porta de saudação entrada [avaliar modelo] [ evaluate-model] módulo.

3. Conectar-se a saudação outros [modelo de pontuação] [ score-model] toohello do módulo à direita de porta de entrada.  

    ![Módulo Modelo de Avaliação conectado][8]

### <a name="run-hello-experiment-and-check-hello-results"></a>Executar teste hello e Olá resultados da verificação

toorun Olá experimento, clique em Olá **executar** botão abaixo tela hello. Isso pode levar alguns minutos. Um indicador de rotação em cada módulo mostra que ele está em execução e, em seguida, uma marca de seleção verde mostra quando o módulo de saudação for concluído. Quando todos os módulos de saudação tem uma marca de seleção, experimento Olá concluiu a execução.

experiência de saudação agora deve ser semelhante a esta:  

![Avaliando os dois modelos][3]

resultados de saudação toocheck, clique em Olá a porta de saída de hello [avaliar modelo] [ evaluate-model] módulo e selecione **visualizar**.  

Olá [avaliar modelo] [ evaluate-model] módulo gera um par de curvas e métricas que permitem a você resultados de saudação toocompare dois modelos de classificado Olá. Você pode exibir os resultados da saudação como curvas característica de operador do receptor (ROC), precisão/recuperação curvas ou curvas de comparação de precisão. Dados adicionais exibidos incluem uma matriz de confusão, cumulativos valores para a área de saudação sob a curva de saudação (AUC) e outras métricas. Você pode alterar o valor de limite de saudação pela movimentação controle deslizante à esquerda ou direita do hello e ver como ele afeta o conjunto de saudação de métricas.  

toohello à direita do gráfico de saudação, clique em **conjunto de dados classificado** ou **classificado toocompare de conjunto de dados** toohighlight Olá associado curva e toodisplay Olá associados métricas abaixo. Na legenda Olá para curvas hello, "Conjunto de dados classificado" corresponde toohello à esquerda de porta de entrada de saudação [avaliar modelo] [ evaluate-model] módulo - em nosso caso, isso é o modelo de árvore de decisão ampliada de saudação. "Toocompare de conjunto de dados de pontuação" corresponde a porta de entrada à direita do toohello - modelo SVM Olá em nosso caso. Quando você clicar em uma dessas etiquetas, curva Olá para o modelo é realçada e métricas de saudação correspondentes são exibidas, conforme mostrado no gráfico a seguir de saudação.  

![Curvas ROC dos modelos][4]

Ao examinar esses valores, você pode decidir qual modelo é o mais próximo toogiving que Olá resultados que você está procurando. Você pode voltar e iterar em sua experiência alterando os valores de parâmetro em modelos diferentes de saudação. 

ciência Hello e arte de interpretar esses resultados e ajuste de desempenho do modelo hello está fora do escopo Olá este passo a passo. Para obter ajuda adicional, você pode ler Olá artigos a seguir:
- [Como tooevaluate modelo desempenho no aprendizado de máquina do Azure](machine-learning-evaluate-model-performance.md)
- [Escolher parâmetros toooptimize seus algoritmos de aprendizado de máquina do Azure](machine-learning-algorithm-parameters-optimize.md)
- [Interpretar os resultados do modelo no Azure Machine Learning](machine-learning-interpret-model-results.md)

> [!TIP]
> Cada vez que executar o teste de saudação um registro de iteração é mantido no histórico de execução de saudação. Você pode exibir essas iterações e retornar tooany, clicando em **exibir o histórico de execução** abaixo tela hello. Você também pode clicar em **anteriores executar** em Olá **propriedades** iteração de toohello tooreturn painel imediatamente anterior Olá um aberto.
> 
> Você pode fazer uma cópia de qualquer iteração de sua experiência clicando **salvar AS** abaixo tela hello. 
> Use a experiência de saudação **resumo** e **descrição** propriedades tookeep um registro de que você tentou seu iterações de teste.
> 
> Consulte [Gerenciar iterações do experimento no Machine Learning Studio do Azure](machine-learning-manage-experiment-iterations.md)para obter mais detalhes.  
> 
> 

- - -
**Em seguida: [implantar Olá web service](machine-learning-walkthrough-5-publish-web-service.md)**

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
