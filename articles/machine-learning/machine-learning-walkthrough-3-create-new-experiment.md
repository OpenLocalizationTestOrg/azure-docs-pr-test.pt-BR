---
title: 'Etapa 3: Criar um novo teste de Machine Learning | Microsoft Docs'
description: "Etapa 3 do hello desenvolver um passo a passo de solução de previsão: criar uma nova experiência de treinamento no estúdio de aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a>Passo a passo Etapa 3: Criar um novo teste de Azure Machine Learning
Isso é a terceira etapa Olá Olá explicação passo a passo, [desenvolver uma solução de análise preditiva em aprendizado de máquina do Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. 
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Carregar dados existentes](machine-learning-walkthrough-2-upload-data.md)
3. **Criar um novo teste**
4. [Treinar e avaliar modelos Olá](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Implantar o serviço Web de saudação](machine-learning-walkthrough-5-publish-web-service.md)
6. [Acessar o serviço Web Olá](machine-learning-walkthrough-6-access-web-service.md)

- - -
Olá próxima etapa neste passo a passo é toocreate um experimento no estúdio de aprendizado de máquina que usa o conjunto de dados de saudação que são carregados.  

1. No Studio, clique em **+ novo** na parte inferior da saudação da janela de saudação.
2. Selecione **TESTE**e, em seguida, selecione "Teste em branco". 

    ![Criar um novo experimento][0]

2. Padrão de Select Olá experimentar nome hello superior da tela hello e renomeie-a como toosomething significativo.

    ![Renomear o teste][5]
   
   > [!TIP]
   > É uma boa prática toofill **resumo** e **descrição** para teste de saudação em Olá **propriedades** painel. Esses fornecem propriedades Olá experimento de saudação toodocument oportunidade para que qualquer pessoa que analisa-lo mais tarde compreendam suas metas e metodologia.
   > 
   > ![Propriedades de teste][6]
   > 
3. Olá módulo paleta toohello à esquerda da tela de experimento hello, expanda **conjuntos de dados salvos**.
4. Localizar Olá conjunto de dados criado em **Meus conjuntos de dados** e arraste-o para a tela hello. Você também pode encontrar o conjunto de dados de saudação inserindo nome Olá Olá **pesquisa** caixa acima paleta hello.  

    ![Adicionar teste de toohello do conjunto de dados Olá][7]

## <a name="prepare-hello-data"></a>Preparar dados Olá
Você pode exibir hello as primeiras 100 linhas de dados hello e algumas informações estatísticas para Olá todo o conjunto de dados: clique Olá a porta de saída do conjunto de dados hello (Olá pequeno círculo na parte inferior da saudação) e selecione **visualizar**.  

Porque o arquivo de dados de saudação não foi fornecido com cabeçalhos de coluna, Studio forneceu títulos genéricos (Col1, Col2, *etc.*). BOM títulos não são essencial toocreating um modelo, mas eles tornam mais fácil toowork com dados de saudação experimento hello. Além disso, quando publicamos eventualmente esse modelo em um serviço web, cabeçalhos de saudação ajuda identificar Olá colunas toohello usuário do serviço de saudação.  

Podemos adicionar cabeçalhos de coluna usando Olá [editar metadados] [ edit-metadata] módulo.
Use Olá [editar metadados] [ edit-metadata] módulo toochange metadados associados a um conjunto de dados. Nesse caso, vamos usá-lo tooprovide nomes mais amigáveis para títulos de coluna. 

toouse [editar metadados][edit-metadata], você deve determinar quais toomodify colunas (nesse caso, todos eles.) Em seguida, você pode especificar Olá ação toobe executada nessas colunas (nesse caso, a alteração de cabeçalhos de coluna.)

1. Na paleta de módulo hello, digite "metadados" hello **pesquisa** caixa. Olá [editar metadados] [ edit-metadata] aparece na lista de módulos de saudação.

2. Clique e arraste Olá [editar metadados] [ edit-metadata] módulo no hello tela e solte-o abaixo Olá de conjunto de dados são adicionadas anteriormente.

3. Conectar Olá dataset toohello [editar metadados][edit-metadata]: clique Olá porta de saída do conjunto de dados hello (Olá pequeno círculo na parte inferior de saudação do conjunto de dados de saudação), arraste toohello porta de entrada de [editar metadados ] [ edit-metadata] (Olá pequeno círculo na parte superior de saudação do módulo de saudação), em seguida, solte o botão do mouse hello. módulo e o conjunto de dados Olá permanecerem conectados, mesmo se você move o na tela hello.
   
   experiência de saudação agora deve ser semelhante a esta:  
   
   ![Adicionar Editar Metadados][1]
   
   Olá vermelho ponto de exclamação indica que estamos ainda não definidas propriedades Olá para este módulo ainda. Faremos isso em seguida.
   
   > [!TIP]
   > Você pode adicionar um módulo de tooa comentário clicando duas vezes em módulo de saudação e a inserção de texto. Isso pode ajudá-lo a ver rapidamente quais módulo hello está fazendo sua experiência. Nesse caso, clique duas vezes em Olá [editar metadados] [ edit-metadata] módulo e tipo hello comentário "adicionar cabeçalhos de coluna". Clique em qualquer lugar na caixa de texto de saudação do hello tela tooclose. toodisplay Olá comentário, clique em Olá seta para baixo no módulo de saudação.
   > 
   > ![Módulo Editar Metadados com comentário adicionado][8]
   > 
4. Selecione [editar metadados][edit-metadata]e em Olá **propriedades** toohello painel à direita da tela hello, clique em **seletor de coluna iniciar**.

5. Em Olá **selecionar colunas** caixa de diálogo, selecione todos os Olá linhas em **colunas disponíveis** e clique em > toomove-los muito**colunas selecionadas**.
   caixa de diálogo Olá deve ter esta aparência:

   ![Seletor de coluna com todas as colunas selecionadas][2]

6. Clique em Olá **Okey** marca de seleção.

7. Em Olá **propriedades** painel, procure Olá **novos nomes de coluna** parâmetro. Neste campo, digite uma lista de nomes de colunas de 21 Olá no conjunto de dados hello, separados por vírgulas e na ordem de coluna. É possível obter nomes de colunas de saudação na documentação do conjunto de dados Olá no site UCI hello, ou para sua conveniência você pode copiar e colar Olá lista a seguir:  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   Painel de propriedades de saudação tem esta aparência:
   
   ![Propriedades de Editar Metadados][3]

> [!TIP]
> Se você quiser títulos de coluna tooverify hello, execute o teste de saudação (clique **executar** abaixo de tela de experimento Olá). Quando ela terminar a execução (uma marca de seleção verde é exibida em [editar metadados][edit-metadata]), clique em Olá porta de saída de hello [editar metadados] [ edit-metadata] módulo e selecione **visualizar**. Você pode exibir a saída de saudação de qualquer módulo no hello progresso da mesmo maneira tooview Olá de dados de saudação por meio de experiência de saudação.
> 
> 

## <a name="create-training-and-test-datasets"></a>Criar conjuntos de dados de treinamento e teste
Precisamos de alguns tootrain Olá modelo dados e alguns tootest-lo.
Na próxima etapa do experimento Olá Olá, dividiremos Olá conjunto de dados em dois conjuntos de dados separados: um para treinar nosso modelo e o outro para testá-lo.

toodo isso, usamos Olá [dividir dados] [ split] módulo.  

1. Localize Olá [dividir dados] [ split] módulo, arraste-o para a tela hello e conectá-lo toohello [editar metadados] [ edit-metadata] módulo.

2. Por padrão, a taxa de divisão de saudação é 0,5 e hello **divisão aleatória** parâmetro está definido. Isso significa que meia aleatória de dados Olá saída através de uma porta de saudação [dividir dados] [ split] módulo e meia a saudação outros. Você pode ajustar esses parâmetros, bem como Olá **semente aleatória** parâmetro, Olá toochange divididos entre dados de teste e treinamento. Neste exemplo, deixaremos como está.
   
   > [!TIP]
   > Olá propriedade **fração de linhas na Olá primeiro conjunto de dados de saída** determina a quantidade de dados de saudação é de saída por meio de saudação *esquerdo* porta de saída. Por exemplo, se você definir Olá taxa too0.7, 70% dos dados de saudação é saída por meio de saudação esquerda da porta e 30% por meio de porta de saudação à direita.  
   > 
   > 

3. Clique duas vezes em Olá [dividir dados] [ split] módulo e Inserir comentário hello, "50% de divisão de dados de treinamento/teste". 

Podemos usar saídas de saudação do hello [dividir dados] [ split] dados de testes de saída do módulo no entanto, como, mas vamos escolher toouse Olá esquerda saída como dados de treinamento e Olá à direita.  

Conforme mencionado em Olá [etapa anterior](machine-learning-walkthrough-2-upload-data.md), classifique um risco de crédito alta como baixo custo Olá é cinco vezes maior do que o custo de saudação do classifique um risco de crédito baixa como alto. tooaccount para isso, podemos gerar um novo conjunto de dados que reflete essa função de custo. Olá novo conjunto de dados, cada exemplo de alto risco é replicado cinco vezes, enquanto cada exemplo de baixo risco não é replicado.   

Podemos fazer essa replicação usando o código R:  

1. Localizar e arraste Olá [Executar Script R] [ execute-r-script] módulo na tela de experimento hello. 

2. Conectar-se a saudação à esquerda a porta de saída de hello [dividir dados] [ split] toohello módulo primeiro porta de entrada ("Dataset1") da saudação [Executar Script R] [ execute-r-script] módulo.

3. Clique duas vezes em Olá [Executar Script R] [ execute-r-script] módulo e Inserir comentário hello, "Conjunto de ajuste de custo".

4. Em Olá **propriedades** painel, excluir saudação padrão texto de saudação **Script R** parâmetro e digite este script:
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Script de R no módulo Executar Script R de saudação][9]

Precisamos toodo essa mesma operação de replicação para cada saída de saudação [dividir dados] [ split] módulo de forma que Olá dados de teste e treinamento ter Olá mesmo custo de ajuste. Olá toodo de maneira mais fácil trata duplicando Olá [Executar Script R] [ execute-r-script] módulo acabou de criar e conectá-lo toohello de saída de outra porta de saudação [dividir dados] [ split] módulo.

1. Saudação de atalho [Executar Script R] [ execute-r-script] módulo e selecione **cópia**.

2. Tela de experimento hello e selecione **colar**.

3. Arraste o novo módulo de saudação para a posição e conecte Olá porta de saída à direita de saudação [dividir dados] [ split] toohello módulo primeiro porta de entrada desse novo [Executar Script R] [ execute-r-script] módulo. 

4. Na parte inferior de saudação da tela hello, clique em **executar**. 

> [!TIP]
> cópia de saudação do módulo Executar Script R de saudação contém Olá mesmo script como módulo original hello. Quando você copiar e colar um módulo na tela hello, cópia Olá retém todas as propriedades de saudação do hello original.  
> 
> 

Nosso teste agora se parece com esse:

![Adicionando módulo Divisão e Scripts R][4]

Para obter mais informações sobre como usar scripts R em seus testes, consulte [Estender seu teste com R](machine-learning-extend-your-experiment-with-r.md).

**Em seguida: [treinar e avaliar modelos Olá](machine-learning-walkthrough-4-train-and-evaluate-models.md)**

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
