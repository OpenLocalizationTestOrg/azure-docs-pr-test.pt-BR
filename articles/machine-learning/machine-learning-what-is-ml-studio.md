---
title: "aaaWhat é estúdio de aprendizado de máquina do Azure? | Microsoft Docs"
description: "Visão geral do Estúdio AM do Azure, uma ferramenta do tipo \"arrastar e soltar\" para criar rapidamente modelos em de uma biblioteca de algoritmos e módulos pronta para uso."
keywords: "aprendizado de máquina do azure, am do azure, estúdio am"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e65c8fe1-7991-4a2a-86ef-fd80a7a06269
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: a25f2d9e75d088a37930de98240c6e14c9567fa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-machine-learning-studio"></a>O que é o Azure Machine Learning Studio?
Estúdio de aprendizado de máquina do Microsoft Azure é uma ferramenta de colaboração, arrastar e soltar, você pode usar toobuild, testar e implantar soluções de análise preditiva em seus dados. O Machine Learning Studio publica modelos como serviços Web que podem ser facilmente consumidos por aplicativos personalizados ou ferramentas de BI como o Excel.

O Machine Learning Studio é onde a ciência de dados, as análises preditivas, os recursos de nuvem e seus dados se encontram!

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-machine-learning-studio-interactive-workspace"></a>espaço de trabalho interativo Olá estúdio de aprendizado de máquina
toodevelop um modelo de análise de previsão, você normalmente usa dados de uma ou mais fontes, transformar e analisar esses dados por meio de várias funções estatísticas e manipulação de dados e gerar um conjunto de resultados. Desenvolver um modelo como este é um processo iterativo. Quando você modifica Olá várias funções e seus parâmetros, os resultados convergirem até ficar satisfeito que você tenha um modelo treinado e eficiente.

**O estúdio de aprendizado de máquina do Azure** fornece um espaço de trabalho interativos, visual tooeasily compilar, testar e iterar em um modelo de análise de previsão. Você arrastar e soltar ***conjuntos de dados*** e análise ***módulos*** para uma tela interativa, conectá-los junto tooform um ***experimentar***, que são executados no aprendizado de máquina Studio. tooiterate no design de modelo, edite a experiência hello, salve uma cópia, se desejado e executá-lo novamente. Quando você estiver pronto, você pode converter seu ***experiência de treinamento*** tooa ***experimento previsão***e, em seguida, publicá-lo como um ***serviço web*** para que seu modelo pode ser acessado por outras pessoas.

Não há nenhuma programação é necessária, conectando apenas visualmente conjuntos de dados e módulos tooconstruct seu modelo de análise de previsão.

> [!TIP]
> toodownload e imprimir um diagrama que fornece uma visão geral dos recursos de saudação do estúdio de aprendizado de máquina, consulte [diagrama de visão geral dos recursos do estúdio de aprendizado de máquina do Azure](machine-learning-studio-overview-diagram.md).
> 
> 

![Diagrama do Estúdio AM do Azure: criar testes, ler dados de várias fontes, gravar dados de pontuação, escrever modelos.][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a>Introdução ao Machine Learning Studio
Quando você insere primeiro [estúdio de aprendizado de máquina](https://studio.azureml.net) consulte Olá **início** página. Aqui você pode exibir a documentação, vídeos, seminários na Web e obter outros recursos valiosos.

Clique em menu da parte superior esquerda de Olá ![Menu](media/machine-learning-what-is-ml-studio/menu.png) e você verá várias opções.

### <a name="cortana-intelligence"></a>Cortana Intelligence
Clique em **Cortana Intelligence** e você será levado toohello home page do hello [Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite). Olá Cortana Intelligence Suite é uma grande de dados totalmente gerenciados e advanced analytics suite tootransform seus dados em ação inteligente. Consulte a home page do hello Suite para a documentação completa, inclusive histórias de clientes.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Há duas opções aqui, **início**, página Olá onde você iniciou, e **Studio**.

Clique em **Studio** e você será levado toohello **estúdio de aprendizado de máquina do Azure**. Primeiro você terá toosign usando sua conta da Microsoft ou sua conta corporativa ou escolar. Depois de conectado, você verá Olá guias a seguir Olá esquerda:

* **PROJETOS** - coleções de testes, conjuntos de dados, blocos de anotações e outros recursos que representam um único projeto
* **TESTES** – Testes que você criou e executou ou salvou como rascunhos
* **SERVIÇOS WEB** -serviços Web que você implantou dos testes
* **NOTEBOOKS** - Notebooks Jupyter que você criou
* **CONJUNTOS DE DADOS** - Conjuntos de dados que você carregou no Estúdio
* **MODELOS TREINADOS** - Modelos que você treinou em testes e salvos no Estúdio
* **CONFIGURAÇÕES de** -uma coleção de configurações que você pode usar tooconfigure sua conta e recursos.

### <a name="gallery"></a>Galeria
Clique em **galeria** e você será levado toohello  **[Cortana Intelligence galeria](http://gallery.cortanaintelligence.com/)**. Olá Galeria é um local onde uma comunidade de desenvolvedores e cientistas de dados compartilhar soluções criadas usando componentes de saudação Cortana Intelligence Suite.

Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir soluções no hello Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).

## <a name="components-of-an-experiment"></a>Componentes de um teste
Um experimento consiste em conjuntos de dados que fornecem os módulos de tooanalytical de dados, que você conecta tooconstruct um modelo de análise de previsão. Especificamente, um teste válido possui três características:

* experiência de saudação tem pelo menos um conjunto de dados e um módulo
* Conjuntos de dados podem ser conectado toomodules somente
* Módulos podem ser conectados tooeither conjuntos de dados ou outros módulos
* Todas as portas de entrada para os módulos devem ter alguns dados de toohello conexão fluxo
* Todos os parâmetros necessários para cada módulo devem estar configurados.

Você pode criar uma experiência do zero, ou você pode usar uma experiência de exemplo existente como um modelo. Para obter mais informações, consulte [toocreate novas experiências de aprendizado de máquina de experiências de exemplo de cópia](machine-learning-sample-experiments.md).

Para obter um exemplo de criação de um teste simples, consulte [Criar um teste simples no Azure Machine Learning Studio](machine-learning-create-experiment.md).

Para obter uma explicação mais completa da criação de uma solução de análise preditiva, consulte [Desenvolver uma solução preditiva com o Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="datasets"></a>CONJUNTOS DE DADOS
Um conjunto de dados é de dados que tem sido carregado tooMachine estúdio de aprendizado para que ele pode ser usado no processo de modelagem de saudação. Um número de conjuntos de dados de exemplo está incluído no estúdio de aprendizado de máquina para você tooexperiment com, e você pode carregar mais conjuntos de dados conforme necessário. Aqui estão alguns exemplos dos conjuntos de dados incluídos:

* **Dados MPG para vários automóveis** – valores MPG (milhas por galão) para automóveis identificados por número de cilindros, cavalo-vapor, etc.
* **Dados de câncer de mama** – dados de diagnósticos de câncer de mama
* **Dados de incêndios em florestas** – tamanhos dos incêndios em floresta na região nordeste de Portugal

Como criar uma experiência você pode escolher na lista de saudação de conjuntos de dados disponíveis toohello à esquerda da tela de saudação.

Para obter uma lista de conjuntos de dados de exemplo incluídos no estúdio de aprendizado de máquina, consulte [usar conjuntos de dados de exemplo hello no estúdio de aprendizado de máquina do Azure](machine-learning-use-sample-datasets.md).

### <a name="modules"></a>Módulos
Um módulo é um algoritmo que você pode executar em seus dados. Estúdio de aprendizado de máquina tem um número de módulos que variam de processos de tootraining, pontuação e validação de funções de ingresso do dados. Aqui estão alguns exemplos dos módulos incluídos:

* [Converter tooARFF] [ convert-to-arff] -formato de arquivo converte uma relação de tooAttribute do conjunto de dados serializados .NET (ARFF).
* [Calcular Estatísticas Elementares][elementary-statistics] – calcula as estatísticas elementares como média, desvio padrão etc.
* [Regressão Linear][linear-regression] – cria um modelo online de regressão linear com base em descendência gradiente.
* [Modelo de Pontuação][score-model] – pontua uma classificação treinada ou modelo de regressão.

Como criar uma experiência você pode escolher na lista de saudação de módulos disponíveis toohello à esquerda da tela de saudação.  

Um módulo pode ter um conjunto de parâmetros que você pode usar algoritmos internos do módulo de saudação tooconfigure. Quando você seleciona um módulo na tela hello, os parâmetros do módulo Olá são exibidos no hello **propriedades** toohello painel à direita da tela de saudação. Você pode modificar parâmetros de saudação em tootune esse painel seu modelo.

Para alguns ajuda navegar pela biblioteca de grande Olá dos algoritmos de aprendizado de máquina disponíveis, consulte [como toochoose algoritmos de aprendizado de máquina do Microsoft Azure](machine-learning-algorithm-choice.md).

## <a name="deploying-a-predictive-analytics-web-service"></a>Implantando um serviço Web de análise preditiva
Quando seu modelo de análise preditiva estiver pronto, você pode implantá-lo como um serviço Web diretamente no Machine Learning Studio. Para obter mais detalhes sobre esse processo, consulte [Implantar um serviço Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
