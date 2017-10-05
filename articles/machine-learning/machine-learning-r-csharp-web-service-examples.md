---
title: "(preterido) Exemplos de serviços Web do Machine Learning criados com R - Azure | Microsoft Docs"
description: "(preterido) Encontre um conjunto útil de exemplos de serviços Web criados com código R e Machine Learning e publicado no Azure Marketplace."
keywords: "csharp, código r, exemplos de serviço Web"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 9514025db6f812f9e7934ea2d1575e948d6585b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a>(preterido) Exemplos de serviços Web usando código R no Azure Machine Learning e publicados no Microsoft Azure Marketplace

> [!NOTE]
> O Microsoft DataMarket está sendo desativado e essas APIs foram preteridas. 
> 
> Você pode encontrar muitos testes de exemplo úteis e APIs na [Galeria do Cortana Intelligence](http://gallery.cortanaintelligence.com). Para saber mais sobre a Galeria, confira [Compartilhar e descobrir soluções na Galeria do Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).

Neste artigo, os serviços Web de exemplo são criados usando o Azure Machine Learning e publicados no Azure Marketplace. Cada exemplo de serviço Web tem um documento abrangente anexado, incorporando exemplos de conjuntos de dados para testar os serviços e explicando como o usuário pode criar seu próprio serviço semelhante. 

No Azure Machine Learning Studio, os usuários podem escrever código R e, com alguns cliques, publicá-lo como um serviço Web para aplicativos e dispositivos o consumirem em todo o mundo. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Desde produzir calculadoras simples que fornecem funcionalidade de estatística até a criação de um preditor personalizado de análise de sentimento de mineração de texto, por exemplo, os usuários novos e experientes do R podem aproveitar a facilidade com que os usuários de Azure Machine Learning podem operacionalizar o código R. Embora esses serviços Web possam ser consumidos por usuários, potencialmente por meio de um aplicativo móvel ou de um site, a finalidade desses exemplos de serviços Web é mostrar como o Machine Learning pode colocar em operação Scripts R para fins analíticos e ser usado para criar serviços Web sobre o código R.

Cada exemplo inclui um exemplo de C# para consumo do serviço Web.

![Diagrama de código R no Azure Machine Learning: soluções R para os proprietários usarem ou publicarem no Azure Marketplace.][1]

Considere os seguintes cenários.

## <a name="scenario-1-generic-model"></a>Cenário 1: Modelo genérico
Um usuário trabalha com um modelo genérico que pode ser aplicado a dados de um novo usuário, como uma previsão básica de dados de série temporal ou um método de R personalizado com análises avançadas. Esse usuário publica o modelo como um serviço Web para que outros possam consumi-lo com seus dados.

* [Classificador binário](machine-learning-r-csharp-binary-classifier.md)
* [Modelo de cluster](machine-learning-r-csharp-cluster-model.md)
* [Regressão linear multivariada](machine-learning-r-csharp-multivariate-linear-regression.md)
* [Previsão - Ajuste exponencial](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [Previsão ETS + STL](machine-learning-r-csharp-retail-demand-forecasting.md)
* [ARIMA (Forecasting-AutoRegressive Integrated Moving Average, média móvel integrada de previsão-autorregressão)](machine-learning-r-csharp-arima.md)
* [Análise de sobrevivência](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a>Cenário 2: Modelo treinado – dados específicos
Um usuário tem dados que fornecem previsões úteis por meio de código R, como uma grande amostra de questionários de personalidade agrupados por meio de um algoritmo k-means, para prever os dados da pesquisa de saúde ou tipo de personalidade do usuário que podem ser usados para prever o risco de uma pessoa ter câncer de pulmão com um pacote R de análise de sobrevivência. O usuário publica os dados por meio de um serviço Web que prevê o resultado de um novo usuário.

## <a name="scenario-3-trained-model--generic-data"></a>Cenário 3: Modelo treinado – dados genéricos
Um usuário tem dados genéricos (por exemplo, um corpus de texto) que permitem desenvolver um serviço Web e aplicá-lo genericamente a diferentes tipos de cenários e casos de uso.

* [Análise de sentimento baseada em léxico](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a>Cenário 4: Calculadora avançada
Um usuário fornece cálculos avançados ou simulações, que não requerem qualquer modelo treinado ou ajuste de um modelo aos dados do usuário.

* [Diferença no teste de proporções](machine-learning-r-csharp-difference-in-two-proportions.md)
* [Pacote de distribuição normal](machine-learning-r-csharp-normal-distribution.md)
* [Pacote de distribuição binomial](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a>Perguntas frequentes
Para perguntas frequentes sobre o consumo do serviço Web ou a publicação no Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



