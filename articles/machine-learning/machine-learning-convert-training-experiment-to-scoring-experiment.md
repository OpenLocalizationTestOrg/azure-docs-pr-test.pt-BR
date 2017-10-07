---
title: "aaaHow tooprepare seu modelo de implantação no estúdio de aprendizado de máquina do Azure | Microsoft Docs"
description: "Como tooprepare o modelo treinado para implantação como um web serviço convertendo o treinamento do estúdio de aprendizado de máquina experimentar tooa experimento de previsão."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: eb943c45-541a-401d-844a-c3337de82da6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: garye
ms.openlocfilehash: d25bc68be63679a803bfc24a9e29e009a9263f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprepare-your-model-for-deployment-in-azure-machine-learning-studio"></a>Como tooprepare seu modelo de implantação no estúdio de aprendizado de máquina do Azure

Permite que o estúdio de aprendizado de máquina do Azure Olá ferramentas necessárias toodevelop um modelo de análise de previsão e, em seguida, colocá-lo Implantando-o como um serviço web do Azure.

toodo isso, use toocreate Studio um experimento - chamado um *experiência de treinamento* - onde você treinar, pontuação e editar seu modelo. Quando estiver satisfeito, você obtém seu toodeploy pronto do modelo convertendo sua tooa de experiência de treinamento *experimento previsão* que configurou tooscore dados de usuário.

Você pode ver um exemplo desse processo em [Passo a passo: Desenvolver uma solução de análise preditiva para avaliação de risco de crédito no Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

Este artigo usa um mergulho no detalhes de saudação do como uma experiência de treinamento é convertida em uma experiência previsível e como essa experiência de previsão é implantada. Compreendendo esses detalhes, você pode aprender como tooconfigure toomake seu modelo implantado-lo mais eficiente.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>Visão geral 

processo de saudação de conversão de um teste do treinamento experimento tooa previsão envolve três etapas:

1. Substitua os módulos com o modelo treinado algoritmo de aprendizado de máquina Olá.
2. Corte Olá experimento tooonly os módulos que são necessários para pontuação. Uma experiência de treinamento inclui um número de módulos que são necessárias para treinamento, mas não são necessários quando Olá modelo é treinado.
3. Defina como seu modelo aceita dados de usuário do serviço web hello e quais dados serão retornados.

> [!TIP]
> No teste de treinamento, você estará concentrado em treinar e pontuar o modelo usando seus próprios dados. Mas, uma vez implantado, os usuários enviará o novo modelo de tooyour de dados e retornará resultados da previsão. Portanto, como converter seu treinamento experimento tooa experimento previsão tooget, ele está pronto para implantação, tenha em mente como Olá modelo será usado por outras pessoas.
> 
> 

## <a name="set-up-web-service-button"></a>Botão Configurar Serviço Web
Depois de executar o teste (clique **executar** na parte inferior da saudação da tela de experimento Olá), clique Olá **configurar o serviço Web** botão (Olá selecione **serviço Web de previsão** opção). **Configurar o serviço Web** executa para Olá três etapas de conversão de sua experiência de previsão de tooa de experiência de treinamento:

1. Ele salva o modelo treinado em Olá **modelos treinados** seção da paleta de módulo hello (toohello à esquerda da tela de experimento Olá). Ele substitui o algoritmo de aprendizado de máquina hello e [treinar modelo] [ train-model] modelo módulos com hello salvadas treinados.
2. Ele analisa o seu teste e remove os módulos que foram claramente usados apenas para treinamento e não são mais necessários.
3. Ele insere módulos de _entrada_ e _saída de serviço Web_ em locais padrão no seu teste (esses módulos aceitam e retornam dados do usuário).

Por exemplo, a seguir Olá experimentar treina um modelo de árvore de decisão ampliada de duas classes usando dados de censo de exemplo:

![experimento de treinamento][figure1]

módulos de saudação nesse experimento executam basicamente em quatro funções diferentes:

![Funções de módulo][figure2]

Quando você converter esse teste do treinamento experimento tooa preditiva, alguns desses módulos não são mais necessários ou servem agora uma finalidade diferente:

* **Dados** -dados Olá deste conjunto de dados de exemplo não são usadas durante a pontuação - usuário saudação do serviço web de saudação fornecerá Olá toobe de dados classificado. No entanto, os metadados de Olá desse conjunto de dados, como tipos de dados, são usados pelo modelo treinado hello. Portanto, você precisa tookeep Olá dataset no experimento previsão Olá para que ele pode fornecer esses metadados.

* **Preparação do** - dependendo dos dados de usuário de saudação que serão enviadas para pontuação, esses módulos podem ou não ser necessário tooprocess os dados de entrada hello. Olá **configurar o serviço Web** botão toque esses - você precisa toodecide como você deseja toohandle-los.
  
    Por exemplo, neste exemplo hello conjunto de dados de exemplo pode ter valores ausentes, assim um [limpar dados ausentes] [ clean-missing-data] módulo foi incluído toodeal com eles. Além disso, o conjunto de dados de exemplo hello inclui colunas que não são necessários tootrain modelo de saudação. Portanto um [selecionar colunas no conjunto de dados] [ select-columns] módulo foi incluído tooexclude essas colunas extras de Olá fluxo de dados. Se você souber dados Olá que serão enviados para pontuação por meio de saudação o serviço web não terá valores ausentes, você poderá remover Olá [limpar dados ausentes] [ clean-missing-data] módulo. No entanto, como Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo ajuda a definir Olá colunas de dados modelo treinado Olá espera, que o módulo precisa tooremain.

* **Treinar** -esses módulos são usados tootrain modelo de saudação. Quando você clica em **configurar o serviço Web**, esses módulos são substituídos por um único módulo que contém o modelo Olá treinamento. Este novo módulo é salvo no hello **modelos treinados** seção da paleta de módulo hello.

* **Pontuação** - neste exemplo, Olá [dividir dados] [ split] módulo é o fluxo de dados de saudação do toodivide usados em dados de treinamento e de dados de teste. Na experiência de previsão hello, podemos estiver não treinamento, isso [dividir dados] [ split] pode ser removido. Da mesma forma, Olá segundo [modelo de pontuação] [ score-model] módulo e hello [avaliar modelo] [ evaluate-model] módulo usado toocompare resultados de teste de saudação dados, então esses módulos não são necessários Olá previsão experiências. Olá restantes [modelo de pontuação] [ score-model] módulo, no entanto, é necessário tooreturn um resultado de pontuação pelo serviço da web de saudação.

Veja como fica nosso exemplo depois do clique em **Configurar Serviço Web**:

![Teste preditivo convertido][figure3]

Olá trabalho feito pelo **configurar o serviço Web** pode ser suficiente tooprepare seu toobe experimento implantado como um serviço web. No entanto, talvez você queira toodo experimento de tooyour específico algum trabalho adicional.

### <a name="adjust-input-and-output-modules"></a>Ajustar os módulos de entrada e saída
Em sua experiência de treinamento, você usou um conjunto de dados de treinamento e, em seguida, alguns tooget de processamento foi Olá dados em um formulário que Olá algoritmo de aprendizado de máquina necessário. Se dados Olá esperados tooreceive por meio do serviço da web de saudação não precisará esse processamento, você pode ignorá-lo: conectar-se a saída de saudação do hello **módulo de entrada de serviço da Web** tooa de módulo diferentes em sua experiência. dados de saudação do usuário agora chegará no modelo de saudação neste local.

Por exemplo, por padrão **configurar o serviço Web** coloca Olá **Web serviço entrada** módulo na parte superior de saudação do seu fluxo de dados, conforme mostrado na figura acima a saudação. Mas é possível posicionar manualmente Olá **Web serviço entrada** após Olá módulos de processamento de dados:

![Entrada de serviço de web hello móvel][figure4]

dados de entrada Hello fornecido por meio de saudação serviço web agora passará diretamente no módulo do modelo de pontuação Olá sem nenhum pré-processamento.

Da mesma forma, por padrão **configurar o serviço Web** coloca Olá módulo de saída do serviço Web na parte inferior de saudação do seu fluxo de dados. Neste exemplo, serviço web de saudação retornará a saída de hello usuário toohello de saudação [modelo de pontuação] [ score-model] módulo, que inclui o vetor de dados completa de entrada hello mais Olá resultados de pontuação.
No entanto, se você preferir tooreturn algo diferente, em seguida, você pode adicionar módulos adicionais antes de saudação **Web de saída do serviço** módulo. 

Por exemplo, apenas resultados de pontuação Olá tooreturn e Olá vetor de inteiro de dados de entrada, adicione um [selecionar colunas no conjunto de dados] [ select-columns] tooexclude módulo todas as colunas exceto Olá resultados de pontuação. Mova Olá **Web de saída do serviço** saída do módulo toohello de hello [selecionar colunas no conjunto de dados] [ select-columns] módulo. experiência de saudação tem esta aparência:

![Movendo a saída de serviço da web hello][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a>Adicionar ou remover módulos de processamento de dados adicionais
Se houver mais módulos no seu experimento que você sabe que não será necessário durante a pontuação, eles podem ser removidos. Por exemplo, porque mudamos Olá **Web serviço entrada** tooa módulo ponto depois hello módulos de processamento de dados, podemos remover Olá [limpar dados ausentes] [ clean-missing-data] módulo de experiência de previsão Hello.

Nosso teste preditivo ficou assim:

![Removendo o módulo adicional][figure6]


### <a name="add-optional-web-service-parameters"></a>Adicionar parâmetros de serviço Web opcionais
Em alguns casos, convém tooallow usuário de saudação de seu comportamento de saudação do toochange de serviço web de módulos ao serviço de saudação é acessado. *Parâmetros de serviço de Web* permitem toodo isso.

Um exemplo comum é configurar um [importar dados] [ import-data] módulo para usuário Olá Olá implantado o serviço web pode especificar uma fonte de dados diferente quando o serviço web de saudação é acessado. Ou então, configurar o módulo [Exportar Dados][export-data] para que um destino diferente possa ser especificado.

Você pode definir os Parâmetros de Serviço Web e associá-los a um ou mais parâmetros de módulo, podendo também especificar se eles são obrigatórios ou opcionais. usuário de saudação do serviço web de saudação fornece valores para esses parâmetros quando o serviço Olá é acessado e ações de módulo Olá forem modificadas de acordo.

Para obter mais informações sobre quais parâmetros de serviço da Web estão e como toouse-los, consulte [usando o Azure Machine Learning parâmetros do Web Service][webserviceparameters].

[webserviceparameters]: machine-learning-web-service-parameters.md


## <a name="deploy-hello-predictive-experiment-as-a-web-service"></a>Implantar a experiência de previsão hello como um serviço web
Agora que tenha sido preparado suficientemente experimento previsão Olá, você pode implantá-lo como um serviço web do Azure. Usando o serviço web de hello, os usuários podem enviar o modelo de dados de tooyour e modelo Olá retornará suas previsões.

Para obter mais informações sobre o processo de implantação completa hello, consulte [implantar um serviço web de aprendizado de máquina do Azure][deploy]

[deploy]: machine-learning-publish-a-machine-learning-web-service.md


<!-- Images -->
[figure1]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure1.png
[figure2]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure2.png
[figure3]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure3.png
[figure4]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure4.png
[figure5]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure5.png
[figure6]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure6.png


<!-- Module References -->
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[export-data]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/
