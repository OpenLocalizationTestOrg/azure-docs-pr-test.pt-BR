---
title: "web de aprendizado de máquina AAA(deprecated) serviços criados com R - Azure | Microsoft Docs"
description: "(preterido) Localize um conjunto útil de exemplos de serviços web criados com código de R e aprendizado de máquina e publicados toohello Azure Marketplace."
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
redirect_document_id: True
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a>(preterido) Exemplos que usam código R no aprendizado de máquina do Azure e publicado tooMicrosoft Azure Marketplace de serviços Web

> [!NOTE]
> Olá Microsoft DataMarket está sendo desativado e essas APIs foram preteridas. 
> 
> Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com). Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).

Neste artigo são web de exemplo serviços foram criados usando o aprendizado de máquina do Azure e publicados toohello Azure Marketplace. Cada exemplo de serviço da web tem um documento abrangente anexado, incorporação de conjuntos de dados de exemplo para testar serviços hello e explicando como Olá usuário pode criar um serviço semelhante próprios. 

No estúdio de aprendizado de máquina do Azure, os usuários podem escrever código R e com alguns cliques, publicá-lo como um serviço web para aplicativos e dispositivos tooconsume em torno de Olá, mundo. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

De produzir calculadoras simples que fornecem funcionalidade de estatística toocreating um indicador de análise de sentimento de mineração de texto personalizado, novos e experientes usuários de R podem se beneficiar de facilidade de saudação com a qual os usuários de aprendizado de máquina do Azure podem utilizar o R código. Enquanto esses serviços da web podem ser consumidos por usuários, possivelmente por meio de um aplicativo móvel ou um site, Olá finalidade desses serviços web exemplos é tooshow como pode utilizar o aprendizado de máquina R scripts para fins analíticos e ser usado toocreate serviços da web em parte superior do código R.

Cada exemplo inclui um exemplo de C# para consumo do serviço Web.

![Diagrama de código R no aprendizado de máquina do Azure: soluções de R para uso proprietário ou publicado toohello Azure Marketplace.][1]

Considere os seguintes cenários de saudação.

## <a name="scenario-1-generic-model"></a>Cenário 1: Modelo genérico
O usuário trabalha com um modelo genérico que pode ser dados aplicada tooa novo usuário, como uma previsão básica de dados de série temporal ou um método de R personalizado com análises avançadas. Este usuário publica Olá tooconsume com seus dados de modelo como um serviço web para que outras pessoas.

* [Classificador binário](machine-learning-r-csharp-binary-classifier.md)
* [Modelo de cluster](machine-learning-r-csharp-cluster-model.md)
* [Regressão linear multivariada](machine-learning-r-csharp-multivariate-linear-regression.md)
* [Previsão - Ajuste exponencial](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [Previsão ETS + STL](machine-learning-r-csharp-retail-demand-forecasting.md)
* [ARIMA (Forecasting-AutoRegressive Integrated Moving Average, média móvel integrada de previsão-autorregressão)](machine-learning-r-csharp-arima.md)
* [Análise de sobrevivência](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a>Cenário 2: Modelo treinado – dados específicos
Um usuário tem dados que fornece previsões úteis por meio de código R, como um grande exemplo de questionários personalidade em cluster por meio do tipo de personalidade k-means algoritmo toopredict saudação do usuário ou dados que podem ser usada toopredict uma pesquisa com integridade um indivíduo risco de câncer de Pulmão com um pacote de R de análise de sobrevivência. usuário Olá publica dados de saudação por meio de um serviço web que prevê o resultado de um novo usuário.

## <a name="scenario-3-trained-model--generic-data"></a>Cenário 3: Modelo treinado – dados genéricos
Um usuário tiver dados genéricos (por exemplo, um corpo de texto) que permite que um toobe de serviço web criado e aplicado genericamente em diferentes tipos de cenários e casos de uso.

* [Análise de sentimento baseada em léxico](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a>Cenário 4: Calculadora avançada
Um usuário fornece cálculos avançados ou simulações que não exigem qualquer modelo treinado ou uma conexão de dados do usuário de toohello um modelo.

* [Diferença no teste de proporções](machine-learning-r-csharp-difference-in-two-proportions.md)
* [Pacote de distribuição normal](machine-learning-r-csharp-normal-distribution.md)
* [Pacote de distribuição binomial](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a>Perguntas frequentes
Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



