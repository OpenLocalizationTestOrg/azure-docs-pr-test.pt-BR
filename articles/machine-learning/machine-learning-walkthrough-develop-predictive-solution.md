---
title: "solução de previsão aaaA para risco de crédito com o aprendizado de máquina | Microsoft Docs"
description: "Uma passo a passo detalhado mostrando como toocreate uma solução de análise de previsão para crédito avaliação de riscos no estúdio de aprendizado de máquina do Azure."
keywords: "risco de crédito, solução de análise preditiva, avaliação de riscos"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a>Passo a passo: Desenvolver uma solução de análise preditiva para avaliação de risco de crédito no Azure Machine Learning

Neste passo a passo, vamos dar uma olhada estendida no processo de saudação do desenvolvimento de uma solução de análise de previsão no estúdio de aprendizado de máquina. Podemos desenvolver um modelo simples no estúdio de aprendizado de máquina e, em seguida, implantá-lo como um serviço web de aprendizado de máquina do Azure onde o modelo de saudação pode fazer previsões com os novos dados. 

Este passo a passo pressupõe que você tenha usado o Machine Learning Studio pelo menos uma vez e tenha noções básicas sobre conceitos de aprendizado de máquina. Mas não pressupõe que você seja um especialista em qualquer um deles.

Se você nunca usou **estúdio de aprendizado de máquina do Azure** antes, talvez você queira toostart com tutorial hello, [criar seu primeiro ciência de dados de experiências no estúdio de aprendizado de máquina do Azure](machine-learning-create-experiment.md). Esse tutorial apresenta estúdio de aprendizado de máquina para Olá primeira vez. Ele mostra noções básicas de saudação como toodrag-e-soltar módulos para sua experiência, conectá-los, executar teste hello e examinar os resultados de saudação. Outra ferramenta que pode ser útil para a guia de Introdução é um diagrama que fornece uma visão geral dos recursos de saudação do estúdio de aprendizado de máquina. Você pode baixá-lo e imprimi-lo aqui: [Diagrama de visão geral dos recursos do Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
 
Se você for novo campo toohello da máquina de aprendizado em geral, há uma série de vídeo que pode ser útil tooyou. Ele é chamado [ciência de dados para iniciantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) e ele pode dar a você um aprendizado de toomachine excelente introdução usando linguagem cotidiana e conceitos.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a>problema de saudação

Suponha que você precisa toopredict risco de crédito de uma pessoa com base nas informações de saudação fornecida em um aplicativo de crédito.  

A avaliação de risco de crédito é um problema complexo, mas podemos simplificá-la um pouco para este passo a passo. Usaremos isso como um exemplo de como você pode criar uma solução de análise preditiva usando o Microsoft Azure Machine Learning. toodo isso, usamos o estúdio de aprendizado de máquina do Azure e um serviço web de aprendizado de máquina.  

## <a name="hello-solution"></a>solução de saudação

Neste passo a passo detalhado, vamos começar falando sobre os dados de risco de crédito disponíveis publicamente e desenvolver e treinar um modelo de previsão com base nesses dados. Podemos implantar Olá modelo como um serviço web para que possa ser usada por outras pessoas para avaliação de risco de crédito.

toocreate essa solução de avaliação de risco de crédito, siga estas etapas:  

1. 
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Carregar dados existentes](machine-learning-walkthrough-2-upload-data.md)
3. [Criar um experimento](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Treinar e avaliar modelos Olá](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Implantar o serviço web de saudação](machine-learning-walkthrough-5-publish-web-service.md)
6. [Serviço de acesso a saudação da web](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> Você pode encontrar uma cópia de trabalho do experimento Olá que desenvolvemos neste passo a passo em Olá [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com). Vá muito**[passo a passo - previsão de risco de crédito](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  e clique em **aberto no Studio** toodownload uma cópia do experimento Olá em seu espaço de trabalho do estúdio de aprendizado de máquina.
> 
> Este passo a passo se baseia em uma versão simplificada de experiência de exemplo hello, [classificação binária: previsão de risco de crédito](http://go.microsoft.com/fwlink/?LinkID=525270), também disponível no hello [galeria](http://gallery.cortanaintelligence.com/).
