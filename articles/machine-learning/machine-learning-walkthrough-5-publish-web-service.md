---
title: "Etapa 5: Implantar o serviço de web de aprendizado de máquina Olá | Microsoft Docs"
description: "Etapa 5 da saudação desenvolver um passo a passo de solução de previsão: implantar um experimento de previsão no estúdio de aprendizado de máquina como um serviço web."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a>Etapa 5 do passo a passo: Implantar o serviço de web de aprendizado de máquina do Azure Olá
Isso é a quinta etapa Olá Olá explicação passo a passo, [desenvolver uma solução de análise preditiva em aprendizado de máquina do Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. 
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Carregar dados existentes](machine-learning-walkthrough-2-upload-data.md)
3. [Criar um novo teste](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Treinar e avaliar modelos Olá](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. **Implantar o serviço web de saudação**
6. [Serviço de acesso a saudação da web](machine-learning-walkthrough-6-access-web-service.md)

- - -
toogive outros toouse uma chance Olá desenvolvemos neste passo a passo do modelo de previsão, é possível implantá-lo como um serviço web no Azure.

Ponto toothis vamos Estive testando com nosso modelo de treinamento. Mas serviço Olá implantado não vai toodo treinamento - será toogenerate novas previsões pela entrada do usuário Olá com base em nosso modelo de pontuação. Por isso vamos toodo tooconvert alguma preparação isso experiências de um ***treinamento*** experimentar tooa ***previsão*** experiências. 

Esse é um processo de três etapas:  

1. Remova um dos modelos de saudação
2. Converter Olá *experiência de treinamento* criamos em um *experimento preditivo*
3. Implantar a experiência de previsão hello como um serviço web

## <a name="remove-one-of-hello-models"></a>Remova um dos modelos de saudação

Primeiro, precisamos tootrim esse teste para baixo um pouco. No momento, temos dois modelos diferentes no experimento hello, mas só queremos toouse um modelo quando for implantada isso como um serviço web.  

Digamos que decidimos esse modelo de árvore Olá ampliada melhor do que o modelo SVM Olá executada. Olá primeira coisa toodo é remover Olá [máquina de vetor de suporte de duas classes] [ two-class-support-vector-machine] módulo e Olá módulos que foram usados para treinar a ele. Convém toomake uma cópia do experimento Olá primeiro clicando **Salvar como** final Olá Olá experimentar tela.

Precisamos Olá toodelete seguintes módulos:  

* [Computador de Vetor de Suporte de Duas Classes][two-class-support-vector-machine]
* [Treinar modelo] [ train-model] e [modelo de pontuação] [ score-model] módulos que estavam conectado tooit
* [Normalizar Dados][normalize-data] (ambos)
* [Avaliar modelo] [ evaluate-model] (porque terminamos avaliar modelos Olá)

Selecione cada módulo e pressione a tecla Delete de saudação ou módulo de saudação do botão direito do mouse e selecione **excluir**. 

![Remover modelo SVM de saudação][3a]

Nosso modelo agora deve ser semelhante ao seguinte:

![Remover modelo SVM de saudação][3]

Agora estamos pronto toodeploy modelo usando Olá [árvore de decisão ampliada de duas classes][two-class-boosted-decision-tree].

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Converter a experiência de previsão do hello treinamento experimento tooa

tooget esse modelo pronto para implantação, precisamos tooconvert essa experiência tooa previsão experiência de treinamento. Isso envolve três etapas:

1. Salvar modelo Olá podemos tiver treinado e, em seguida, substituir os módulos de treinamento
2. Trim Olá experimento tooremove os módulos que foram necessário apenas para treinamento
3. Definir onde o serviço web de saudação aceitará entrada e onde ele gera a saída de hello

Podemos fazer isso manualmente, mas felizmente todas as três etapas podem ser realizadas clicando **configurar o serviço Web** na parte inferior da saudação da tela de experimento hello (e selecionando Olá **previsão Web Service** opção).

> [!TIP]
> Se você quiser obter mais detalhes sobre o que acontece quando você converte um tooa de experiência de treinamento previsão experimentar, consulte [como tooprepare seu modelo de implantação no estúdio de aprendizado de máquina do Azure](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Quando você clica em **Configurar Serviço Web**, várias coisas acontecem:

* modelo treinado Hello é convertido tooa único **treinado** módulo e armazenados em Olá módulo paleta toohello esquerda da saudação experimentar tela (você pode encontrar em **modelos treinados**)
* Os módulos que foram usados para o treinamento são removidos; especificamente:
  * [Árvore de Decisão Aumentada em Duas Classes][two-class-boosted-decision-tree]
  * [Modelo de Treinamento][train-model]
  * [Dados Divididos][split]
  * Olá segundo [Executar Script R] [ execute-r-script] módulo que foi usado para dados de teste
* treinado Olá salvada é adicionado no experimento Olá
* **Entrada de serviço de Web** e **Web de saída do serviço** módulos são adicionados (eles identificam onde os dados do usuário Olá entrará modelo hello e quais dados são retornados, quando o serviço web de saudação é acessado)

> [!NOTE]
> Você pode ver que experimento Olá é salvo em duas partes em guias que foram adicionados na parte superior de saudação da tela de experimento hello. Olá experiência de treinamento original é na guia Olá **experiência de treinamento**, e Olá recém-criado experimento previsão está sob **experimento previsão**. experiência de previsão Olá é hello um que nós implantará como um serviço web.

Precisamos de uma etapa adicional tootake com esse teste específico.
Adicionamos dois [Executar Script R] [ execute-r-script] tooprovide módulos uma ponderação função toohello dados. Que estavam apenas uma rodada que é necessário para treinamento e teste, vamos esses módulos no modelo final hello.
O estúdio de aprendizado de máquina removido um [Executar Script R] [ execute-r-script] módulo quando ele removido Olá [divisão] [ split] módulo. Agora podemos remover Olá outros e conecte-se [Editor de metadados] [ metadata-editor] diretamente muito[modelo de pontuação][score-model].    

Agora o teste deve se parecer como isto:  

![Pontuação treinado Olá][4]  

> [!NOTE]
> Você deve estar se perguntando por que foi deixado dataset de dados de cartão de crédito alemão UCI Olá experimento previsão hello. serviço de saudação será tooscore Olá dados usuário, não Olá conjunto de dados original, então por que deixam Olá conjunto de dados original no modelo de saudação?
> 
> É verdade que serviço Olá não precisa Olá dados originais de cartão de crédito. Mas é necessário esquema Olá para os dados, que inclui informações como o número de colunas há e quais colunas são numéricas. Essas informações de esquema são necessário toointerpret Olá dados de usuário. Vamos deixar esses componentes conectados de modo que hello pontuação módulo tem esquema de conjunto de dados hello quando Olá serviço está em execução. dados de saudação não for usados, apenas o esquema hello.  
> 
> 

Executar teste Olá pela última vez (clique **executar**.) Tooverify que Olá modelo ainda está funcionando, clique em saída Olá Olá [modelo de pontuação] [ score-model] módulo e selecione **exibir resultados**. Você pode ver dados originais Olá são exibidos, juntamente com o valor de risco de crédito hello ("rótulos de pontuação") e hello pontuação valor de probabilidade ("classificado probabilidades".) 

## <a name="deploy-hello-web-service"></a>Implantar o serviço web de saudação
Você pode implantar Olá experiência como um serviço de web clássico ou como um novo serviço da web com base no Gerenciador de recursos do Azure.

### <a name="deploy-as-a-classic-web-service"></a>Implantar como serviço Web clássico
toodeploy um clássico web serviço derivado de nossa experiência, clique em **implantar o serviço da Web** abaixo Olá tela e selecione **implantar o serviço Web [clássico]**. Estúdio de aprendizado de máquina implanta Olá experiência como um serviço web e vai toohello painel para o serviço web. Nessa página, você pode retornar toohello experimento (**exibir instantâneo** ou **exibir mais recente**) e executar um teste simple de serviço da web de saudação (consulte **testar Olá web serviço** abaixo). Há também informações para a criação de aplicativos que podem acessar o serviço web da saudação (mais detalhes na próxima etapa Olá deste passo a passo).

![Painel de serviço Web][6]

Você pode configurar o serviço de saudação clicando Olá **configuração** guia. Aqui você pode modificar o nome do serviço hello (é Olá determinado nome de teste por padrão) e dê a ele uma descrição. Você também pode fornecer mais rótulos amigáveis para Olá dados de entrada e saídos.  

![Configurar o serviço web de saudação][5]  

### <a name="deploy-as-a-new-web-service"></a>Implantar como um novo serviço Web

> [!NOTE] 
> toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você está implantando Olá serviço da web. Para obter mais informações, consulte [gerenciar um serviço web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md). 

toodeploy um novo serviço web derivado da nossa experiência:

1. Clique em **implantar o serviço da Web** abaixo Olá tela e selecione **implantar o serviço de Web [novo]**. O estúdio de aprendizado de máquina transfere dos serviços web de aprendizado de máquina do Azure toohello **implantar experimento** página.

2. Insira um nome para o serviço web de saudação. 

3. Para **plano de preço**, você pode selecionar um plano de preços existente ou selecione "Criar novo" e dê Olá novo plano de um nome e uma opção de plano mensal Olá select. plano de saudação camadas padrão toohello planos para sua região padrão e o serviço web é implantado toothat região.

4. Clique em **Implantar**.

Depois de alguns minutos, Olá **Quickstart** página para seu serviço da web é aberta.

Você pode configurar o serviço de saudação clicando Olá **configurar** guia. Aqui você pode modificar o serviço Olá title e dê a ele uma descrição. 

Olá tootest serviço da web, clique em Olá **teste** guia (consulte **testar Olá web serviço** abaixo). Para obter informações sobre como criar aplicativos que podem acessar o serviço web de saudação, clique em Olá **consumir** guia (a próxima etapa Olá neste passo a passo entrará em mais detalhes).

> [!TIP]
> Você pode atualizar o serviço web de saudação depois que você implantou. Por exemplo, se você quiser toochange seu modelo, você pode editar experiência de treinamento hello, ajustar os parâmetros de modelo Olá e clique em **implantar o serviço da Web**, selecionando **implantar o serviço Web [clássico]** ou  **Implantar o serviço da Web [novo]**. Quando você implanta o experimento Olá novamente, ele substitui o serviço da web hello, usando o modelo atualizado.  
> 
> 

## <a name="test-hello-web-service"></a>Testar o serviço web de saudação

Quando o serviço web de saudação é acessado, dados do usuário Olá entram por Olá **Web serviço entrada** módulo onde ele passou toohello [modelo de pontuação] [ score-model] módulo e classificados. forma Olá que configuramos o experimento previsão Olá, o modelo Olá espera dados no hello mesmo formato que o dataset de risco de crédito original hello.
resultados de saudação são retornados toohello usuário do serviço web de saudação por meio de saudação **Web de saída do serviço** módulo.

> [!TIP]
> forma Olá Olá previsão experimento configurado, Olá inteira, temos os resultados de saudação [modelo de pontuação] [ score-model] módulo são retornados. Isso inclui todos os dados de entrada hello mais valor de risco de crédito hello e hello pontuação de probabilidade. Mas você pode retornar algo diferente se você quiser - por exemplo, você poderia retornar apenas Olá valor de risco de crédito. toodo, inserir um [colunas do projeto] [ project-columns] módulo entre [modelo de pontuação] [ score-model] e hello **Webdesaídadeserviço** tooeliminate colunas indesejadas Olá tooreturn de serviço web. 
> 
> 

Você pode testar uma web clássico de serviço em **estúdio de aprendizado de máquina** ou em Olá **serviços de Web de aprendizado de máquina do Azure** portal.
Você pode testar um novo serviço da web apenas no hello **serviços de Web do aprendizado de máquina** portal.

> [!TIP]
> Durante o teste no portal de serviços de Web de aprendizado de máquina do Azure Olá, você pode fazer com que o portal Olá criar dados de exemplo que você pode usar o serviço do tootest Olá solicitação-resposta. Em Olá **configurar** , selecione "Sim" para **habilitado de dados de exemplo?**. Quando você abre a guia Olá Olá solicitação-resposta **teste** página, portal Olá preenche os dados de exemplo obtidos Olá original dataset de risco de crédito.

### <a name="test-a-classic-web-service"></a>Testar um serviço Web Clássico

Você pode testar um serviço da web clássico no estúdio de aprendizado de máquina ou no portal de serviços de Web do aprendizado de máquina hello. 

#### <a name="test-in-machine-learning-studio"></a>Testar no Machine Learning Studio

1. Em Olá **painel** para serviço web de saudação, clique em Olá **teste** botão em **ponto de extremidade padrão**. Uma caixa de diálogo será exibida e solicita dados de entrada hello para serviço de saudação. Esses é Olá mesmas colunas que eram exibidos no dataset de risco de crédito original hello.  

2. Insira um conjunto de dados e clique em **OK**. 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a>Teste no portal de serviços de Web do aprendizado de máquina Olá

1. Em Olá **painel** para serviço web de saudação, clique em Olá **visualização de teste** link em **ponto de extremidade padrão**. página de teste de saudação no portal de serviços de Web de aprendizado de máquina do Azure Olá para o ponto de extremidade de serviço de web hello abre e solicita dados de entrada hello para serviço de saudação. Esses é Olá mesmas colunas que eram exibidos no dataset de risco de crédito original hello.

2. Clique em **Solicitação-Resposta**. 

### <a name="test-a-new-web-service"></a>Testar um novo serviço Web

Você pode testar um novo serviço da web apenas no portal de serviços de Web do aprendizado de máquina de saudação.

1. Em Olá [serviços de Web de aprendizado de máquina do Azure](https://services.azureml.net/quickstart) portal, clique **teste** na parte superior de saudação da página de saudação. Olá **teste** página abre e você pode inserir dados para o serviço de saudação. campos de entrada Hello exibidos correspondem toohello colunas que eram exibidos no dataset de risco de crédito original hello. 

2. Insira um conjunto de dados e clique em **Testar solicitação-resposta**.

Olá resultados de teste de saudação são exibidos no lado direito de saudação da página Olá na coluna de saída de hello. 


## <a name="manage-hello-web-service"></a>Gerenciar o serviço web de saudação

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a>Gerenciar um serviço da web clássico no hello portal clássico do Azure

Depois de implantar seu serviço da web clássico, você pode gerenciá-lo de saudação [portal clássico do Azure](https://manage.windowsazure.com).

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com)
2. No painel de serviços do Microsoft Azure hello, clique em **APRENDIZADO de máquina**
3. Clique no espaço de trabalho
4. Clique em Olá **serviços Web** guia
5. Clique em Olá web service criamos
6. Clique em ponto de extremidade do hello "padrão"

A partir daqui, você pode fazer coisas como monitorar como o serviço web de saudação está fazendo e fazer ajustes de desempenho, alterando o serviço de saudação quantas chamadas simultâneas pode manipular.

Para obter mais informações, consulte:

* [Criando pontos de extremidade](machine-learning-create-endpoint.md)
* [Dimensionando serviço Web](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a>Gerenciar um clássico ou um novo serviço da web no portal de serviços de Web de aprendizado de máquina do Azure Olá

Assim que tiver implantado o serviço web, se clássico ou novo, você pode gerenciá-lo de saudação [serviços Web de aprendizado de máquina do Microsoft Azure](https://services.azureml.net/quickstart) portal.

desempenho de saudação toomonitor do serviço web:

1. Entrar toohello [serviços Web de aprendizado de máquina do Microsoft Azure](https://services.azureml.net/quickstart) portal
2. Clique em **Serviços Web**
3. Clique no seu serviço Web
4. Clique em Olá **painel**

- - -
**Em seguida: [acessar o serviço web Olá](machine-learning-walkthrough-6-access-web-service.md)**

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
