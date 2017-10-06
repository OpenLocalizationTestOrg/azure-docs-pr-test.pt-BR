---
title: 'Etapa 2: carregar dados em um experimento do Machine Learning | Microsoft Docs'
description: "Etapa 2 de saudação desenvolver um passo a passo de solução de previsão: carregamento armazenado dados públicos no estúdio de aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a>Etapa 2 do passo a passo: carregar dados existentes no experimento de Azure Machine Learning
Esta é a segunda etapa Olá Olá explicação passo a passo, [desenvolver uma solução de análise preditiva em aprendizado de máquina do Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. 
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. **Carregar dados existentes**
3. [Criar um novo teste](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Treinar e avaliar modelos Olá](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Implantar o serviço Web de saudação](machine-learning-walkthrough-5-publish-web-service.md)
6. [Acessar o serviço Web Olá](machine-learning-walkthrough-6-access-web-service.md)

- - -
toodevelop um modelo de previsão para o risco de crédito, precisamos de dados que podemos usar tootrain e, em seguida, testar o modelo de saudação. Para este passo a passo, usaremos hello "Conjunto de dados do UCI Statlog (dados de crédito alemão)" do repositório de aprendizado de máquina do UC Irvine hello. Você pode encontrá-lo aqui:   
<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a>

Vamos usar arquivo hello chamado **german.data**. Baixe este arquivo tooyour de disco rígido local.  

Olá **german.data** conjunto de dados contém linhas de 20 variáveis para 1000 candidatos anteriores de crédito. Essas 20 variáveis representam o conjunto de saudação do conjunto de recursos (Olá *vetor de recurso*), que fornece as características de identifica para cada candidato de crédito. Uma coluna adicional em cada linha representa um risco de crédito calculado do candidato Olá, com 700 candidatos identificados como um risco de crédito baixa e 300 como um alto risco.

site UCI Olá fornece uma descrição dos atributos de saudação do vetor de recurso Olá para esses dados. Isso inclui informações financeiras, histórico de crédito, status de emprego e informações pessoais. Para cada candidato, foi dada uma classificação binária indicando se são um risco baixo ou alto de crédito. 

Vamos usar essa tootrain dados um modelo de análise de previsão. Quando terminamos, nosso modelo deve ser capaz de tooaccept um vetor de recurso para um novo indivíduo e prever se ele é um risco de crédito baixa ou alta.  

Aqui está uma mudança interessante. Olá descrição do conjunto de dados de saudação em Olá UCI site menciona o custo se nós misclassify o risco de crédito de uma pessoa.
Se o modelo de saudação prevê um risco de crédito alta para alguém que é realmente um risco de crédito baixa, modelo Olá fez uma misclassification.
Mas misclassification inversa Olá é cinco vezes mais cara instituição financeira de toohello: se o modelo de saudação prevê um risco de crédito baixa para alguém que é realmente um risco de crédito alta.

Assim, desejamos tootrain nosso modelo para que o custo de saudação este último tipo de misclassification é cinco vezes maior do que classifique Olá outra maneira.
Toodo de uma maneira simples isso ao modelo Olá em nossa experiência de treinamento é duplicando (cinco vezes) dessas entradas que representam uma pessoa com um risco de crédito alta. Em seguida, se o modelo de saudação classificar incorretamente alguém como um risco de crédito baixa quando eles são, na verdade, um alto risco, Olá modelo faz esse mesmo misclassification cinco vezes, uma vez para cada linha duplicada. Isso aumentará o custo de saudação do erro nos resultados de treinamento hello.


## <a name="convert-hello-dataset-format"></a>Converter o formato de conjunto de dados Olá
saudação de conjunto de dados original usa um formato de separadas por espaço em branco. Estúdio de aprendizado de máquina funciona melhor com um arquivo de valores separados por vírgulas (CSV), portanto converteremos Olá conjunto de dados, substituindo espaços por vírgulas.  

Há muitos tooconvert de maneiras esses dados. É uma maneira usando Olá comando do Windows PowerShell a seguir:   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

Outra maneira é usando o comando de sed Olá Unix:  

    sed 's/ /,/g' german.data > german.csv  

Em ambos os casos, criamos uma versão separada por vírgulas dos dados de saudação em um arquivo chamado **german.csv** que podemos usar nossa experiência.

## <a name="upload-hello-dataset-toomachine-learning-studio"></a>Carregar Olá dataset tooMachine estúdio de aprendizado
Depois que dados saudação tem sido convertido tooCSV formato, precisamos tooupload no estúdio de aprendizado de máquina. 

1. Home page do hello abrir estúdio de aprendizado de máquina ([https://studio.azureml.net](https://studio.azureml.net)). 

2. Clique em menu Olá ![Menu][1] no canto superior esquerdo de saudação da janela de saudação, clique em **aprendizado de máquina do Azure**, selecione **Studio**e entre.

3. Clique em **+ novo** na parte inferior da saudação da janela de saudação.

4. Selecione **CONJUNTO DE DADOS**.

5. Selecione **DO ARQUIVO LOCAL**.

    ![Adicionar um conjunto de dados de um arquivo local][2]

6. Em Olá **carregar um novo conjunto de dados** caixa de diálogo, clique em **procurar** e localize Olá **german.csv** arquivo que você criou.

7. Insira um nome para o conjunto de dados de saudação. Para este passo a passo, vamos chamá-lo de "Dados do cartão de crédito alemão UCI".

8. Para tipo de dados, selecione **Arquivo CSV genérico sem cabeçalho (.nh.csv)**.

9. Inclua uma descrição se desejar.

10. Clique em Olá **Okey** marca de seleção.  

    ![Carregar o conjunto de dados Olá][3]

Isso carrega dados saudação em um módulo de conjunto de dados que podemos usar em um experimento.

Você pode gerenciar conjuntos de dados que você carregou tooStudio clicando Olá **conjuntos de dados** toohello guia à esquerda da janela do Studio hello.

![Gerenciar conjuntos de dados][4]

Para obter mais informações sobre como importar outros tipos de dados para um teste, consulte [Importar dados de treinamento para o Azure Machine Learning Studio](machine-learning-data-science-import-data.md).

**A seguir: [criar um novo experimento](machine-learning-walkthrough-3-create-new-experiment.md)**

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
