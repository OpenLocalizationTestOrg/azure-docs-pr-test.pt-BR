---
title: "aaaHow um modelo de aprendizado de máquina do Azure torna-se um serviço web | Microsoft Docs"
description: "Uma visão geral dos mecanismos de saudação de como seu progride de modelo de aprendizado de máquina do Azure de um desenvolvimento experimentar tooan operacionalizada serviço da Web."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 25e0c025-f8b0-44ab-beaf-d0f2d485eb91
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 2bbe09fa8fa22662cf8ec4a8b6249d23c87c8ddf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-a-machine-learning-model-progresses-from-an-experiment-tooan-operationalized-web-service"></a>Como uma progride de modelo de aprendizado de máquina de um experimento tooan operacionalizada o serviço Web
O estúdio de aprendizado de máquina do Azure fornece uma tela interativa que permite que você toodevelop, executar, testar e iterar um ***experimentar*** representando um modelo de análise de previsão. Há uma grande variedade de módulos disponíveis que podem:

* Inserir dados em seu teste
* Manipular dados Olá
* Treinar um modelo usando algoritmos de aprendizado de máquina
* Modelo de saudação de pontuação
* Avaliar os resultados de saudação
* Exibir os valores finais

Quando estiver satisfeito com seu teste, você poderá implantá-lo como um ***serviço Web clássico do Azure Machine Learning*** ou ***Novo serviço Web do Azure Machine Learning*** para que os usuários possam enviar novos dados e receber resultados.

Neste artigo, fornecemos uma visão geral dos mecanismos de saudação de como seu progride de modelo de aprendizado de máquina de um tooan de experiência de desenvolvimento operacionalizada serviço da Web.

> [!NOTE]
> Existem outra maneiras toodevelop e implantar modelos de aprendizado de máquina, mas este artigo se concentra em como você pode usar o estúdio de aprendizado de máquina. Por exemplo, tooread uma descrição de como toocreate um clássico Web service preditivo com R, consulte Olá postagem de blog [ML do Azure e implantar previsão Web Apps usando RStudio & compilação](http://blogs.technet.com/b/machinelearning/archive/2015/09/25/build-and-deploy-a-predictive-web-app-using-rstudio-and-azure-ml.aspx).
> 
> 

Enquanto o estúdio de aprendizado de máquina do Azure é projetado toohelp desenvolver e implantar um *modelo de análise de previsão*, é possível toouse Studio toodevelop um experimento que não inclui um modelo de análise de previsão. Por exemplo, um experimento pode apenas de entrada de dados, manipulá-lo e, em seguida, Olá resultados de saída. Assim como uma experiência de análise de previsão, você pode implantar esse teste não previsão como um serviço Web, mas é um processo mais simples porque experimento Olá não treinamento ou um modelo de aprendizado de máquina de pontuação. Embora não seja Olá toouse Studio típico dessa forma, podemos irá incluí-la discussão Olá para que possamos dar uma explicação completa de como funciona o Studio.

## <a name="developing-and-deploying-a-predictive-web-service"></a>Desenvolvendo e implantando um serviço Web preditivo
Aqui estão as fases de saudação que uma solução típica segue como desenvolver e implantá-lo usando o estúdio de aprendizado de máquina:

![Fluxo de implantação](media/machine-learning-model-progression-experiment-to-web-service/model-stages-from-experiment-to-web-service.png)

*Figura 1 - Estágios de um modelo típico de análise preditiva*

### <a name="hello-training-experiment"></a>experiência de treinamento Olá
Olá ***experiência de treinamento*** é a fase inicial de saudação do desenvolvimento de seu serviço Web no estúdio de aprendizado de máquina. finalidade de saudação da experiência de treinamento Olá é toogive você toodevelop um local, testar, repetir e, eventualmente, treinar uma modelo de aprendizado de máquina. Você pode até mesmo treinar vários modelos simultaneamente como você procurar a melhor solução de hello, mas depois de terminar a experimentar você selecionará um único treinado de modelo e eliminar Olá restante de experiência de saudação. Para obter um exemplo de como desenvolver um teste de análise preditiva, veja [Desenvolver uma solução de análise preditiva para avaliação de risco de crédito no Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="hello-predictive-experiment"></a>experiência de previsão Olá
Quando você tiver um modelo treinado em sua experiência de treinamento, clique em **configurar o serviço Web** e selecione **previsão Web Service** no processo de saudação do estúdio de aprendizado de máquina tooinitiate de converter o treinamento Experimente tooa ***experimento previsão***. Olá finalidade do experimento previsão Olá é toouse seu modelo treinado tooscore novos dados, com objetivo de saudação de, eventualmente, tornando-se operacionalizada como um serviço Web do Azure.

Essa conversão é feita para você por meio de saudação etapas a seguir:

* Converter o conjunto de saudação de módulos usados para treinamento em um único módulo e salvá-lo como um modelo treinado
* Eliminar todos os módulos externos não relacionados tooscoring
* Adicionar a entrada e saída portas Olá eventual Web serviço usará

Pode haver mais alterações que você deseja toomake tooget toodeploy de pronto sua experiência de previsão como um serviço Web. Por exemplo, se você quiser Olá Web serviço toooutput apenas um subconjunto de resultados, você pode adicionar um módulo de filtragem antes de porta de saída de hello.

No processo de conversão, experiência de treinamento de saudação não será descartada. Quando o processo de saudação for concluído, você tem duas guias no Studio: um para teste de treinamento de saudação e outro para teste de previsão de saudação. Dessa forma, que você pode fazer alterações experiência de treinamento toohello antes de implantar seu serviço Web e recriar a experiência de previsão hello. Ou você pode salvar uma cópia da saudação treinamento experimento toostart outra linha de experimentação.

> [!NOTE]
> Quando você clica em **previsão Web Service** iniciar um processo automático tooconvert sua experiência de previsão de tooa de experiência de treinamento, e isso funciona bem na maioria dos casos. Se a sua experiência de treinamento é complexa (por exemplo, se você tiver vários caminhos para treinamento que você unir), talvez você prefira toodo essa conversão manualmente. Para obter mais informações, consulte [como tooprepare seu modelo de implantação no estúdio de aprendizado de máquina do Azure](machine-learning-convert-training-experiment-to-scoring-experiment.md).
> 
> 

### <a name="hello-web-service"></a>saudação de serviço Web
Quando estiver satisfeito que seu teste preditivo está pronto, você pode implantar o serviço como um serviço Web clássico ou um novo serviço Web com base no Azure Resource Manager. toooperationalize seu modelo, implantando-a como uma *serviço Web de aprendizado de máquina clássico*, clique em **implantar o serviço da Web** e selecione **implantar o serviço Web [clássico]**. toodeploy como *serviço Web de aprendizado de máquina novo*, clique em **implantar o serviço da Web** e selecione **implantar o serviço de Web [novo]**. Agora, os usuários podem enviar o modelo de tooyour de dados usando a API REST do serviço da Web hello e receber resultados Olá voltar. Para obter mais informações, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).

## <a name="hello-non-typical-case-creating-a-non-predictive-web-service"></a>Olá caso não típico: Criando um serviço Web sem preditivo
Se a sua experiência não treinar um modelo de análise de previsão, você não precisa toocreate uma experiência de treinamento e uma experiência de pontuação - há apenas um experimento e implantá-lo como um serviço Web. O estúdio de aprendizado de máquina detecta se sua experiência contém um modelo de previsão, analisando os módulos de saudação que você usou.

Depois que você tiver iterado no experimento e estiver satisfeito com ele:

1. Clique em **Configurar Serviço Web** e selecione **Novo Treinamento de Serviço Web** – nós de entrada e saída são adicionados automaticamente
2. Clique em **Executar**
3. Clique em **implantar o serviço da Web** e selecione **implantar o serviço Web [clássico]** ou **implantar o serviço de Web [novo]** dependendo Olá ambiente toowhich você queira toodeploy.

Seu serviço Web está implantado, e você pode acessá-lo e gerenciá-lo como um serviço Web preditivo.

## <a name="updating-your-web-service"></a>Atualização de seu serviço Web
Agora que você implantou sua experiência como um serviço Web, se você precisar tooupdate-lo?

O que é necessário que depende de tooupdate:

**Deseja toochange Olá entrada ou saída, ou você deseja toomodify como Olá serviço Web manipula dados**

Se você não estiver alterando o modelo hello, mas apenas alterar como Olá serviço Web lida com dados, você pode editar experiência previsível hello e, em seguida, clique em **implantar o serviço da Web** e selecione **implantar o serviço Web [clássico]** ou **implantar o serviço de Web [novo]** novamente. saudação de serviço da Web for interrompida, hello experimento previsão atualizado é implantado e Olá serviço Web é reiniciado.

Aqui está um exemplo: suponha que sua experiência de previsão retorna toda a linha de dados de entrada com Olá Olá prevista de resultados. Você pode decidir que deseja que o resultado de retorno Olá Olá Web serviço toojust. Portanto, você pode adicionar uma **colunas do projeto** módulo experimento previsão hello, logo antes de porta de saída de hello tooexclude colunas diferentes Olá resultam. Quando você clica em **implantar o serviço da Web** e selecione **implantar o serviço Web [clássico]** ou **implantar o serviço de Web [novo]** novamente, Olá serviço Web é atualizado.

**Você quer tooretrain Olá modelo com novos dados**

Se você deseja tookeep seu modelo de aprendizado de máquina, mas você gostaria que tooretrain-lo com novos dados, você tem duas opções:

1. **Treinar novamente o modelo de saudação enquanto Olá serviço Web está em execução** -se você quiser tooretrain seu modelo, enquanto Olá previsão Web serviço está em execução, você pode fazer isso ao fazer algumas modificações toohello treinamento experimento toomake-lo um *** experiência de treinamento***, em seguida, você pode implantá-lo como um  ***web novos treinamentos* service**. Para obter instruções sobre como toodo isso, consulte [aprendizado de máquina treinar novamente modelos programaticamente](machine-learning-retrain-models-programmatically.md).
2. **Voltar a experiência de treinamento original toohello e usar toodevelop de dados de treinamento diferentes seu modelo** - sua experiência de previsão é vinculado toohello serviço da Web, mas a experiência de treinamento Olá não está diretamente vinculada dessa maneira. Se você modificar a experiência de treinamento original hello e clique em **configurar o serviço Web**, ele criará uma *novo* previsão experiências que, quando implantado, criará uma *novo* Web serviço. Ele apenas não atualiza o serviço da Web hello.
   
   Se você precisar de experiência de treinamento Olá toomodify, abra-o e clique em **Salvar como** toomake uma cópia. Isso fará a experiência de treinamento original intacta hello, experiência de previsão e serviço Web. Agora você pode criar um novo serviço Web com suas alterações. Depois que você implantou Olá novo serviço da Web, em seguida, você pode decidir se toostop Olá serviço da Web anterior ou mantê-lo executando junto com hello uma nova.

**Você deseja tootrain um modelo diferente**

Se você quiser toomake altera tooyour original previsão experimento, como selecionar uma algoritmo de aprendizado de máquina diferente tentar um método diferente de treinamento, etc., em seguida, você precisa toofollow Olá segundo procedimento descrito acima para treinar novamente seu modelo: Abra o teste de treinamento hello, clique em **Salvar como** toomake uma cópia e iniciar o caminho de novo Olá de desenvolver seu modelo, criar experiência previsível hello e implantação Olá serviço da web. Isso criará um novo serviço da Web não relacionados toohello original - você pode decidir quais tookeep um ou ambos, em execução.

## <a name="next-steps"></a>Próximas etapas
Para obter mais detalhes sobre o processo de saudação de desenvolvimento e teste, consulte Olá artigos a seguir:

* Convertendo experimento Olá - [como tooprepare seu modelo de implantação no estúdio de aprendizado de máquina do Azure](machine-learning-convert-training-experiment-to-scoring-experiment.md)
* Implantando o serviço de Web hello - [implantar um serviço web de aprendizado de máquina do Azure](machine-learning-publish-a-machine-learning-web-service.md)
* modelo de novos treinamentos Olá - [aprendizado de máquina treinar novamente modelos programaticamente](machine-learning-retrain-models-programmatically.md)

Para obter exemplos de todo o processo hello, consulte:

* 
            [Tutorial de aprendizado de máquina: Crie sua primeira experiência no Azure Machine Learning Studio](machine-learning-create-experiment.md)
* [Passo a passo: Desenvolver uma solução de análise preditiva para avaliação de risco de crédito no Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

