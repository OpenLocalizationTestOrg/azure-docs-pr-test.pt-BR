---
title: "Etapa 6: Acessar o serviço da Web de aprendizado de máquina de saudação | Microsoft Docs"
description: "Etapa 6 do hello desenvolver um passo a passo de solução de previsão: acessar um serviço Web de aprendizado de máquina do Azure ativo."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a>Etapa 6 do passo a passo: Saudação de acesso serviço web de aprendizado de máquina do Azure

Esta é a última etapa Olá Olá explicação passo a passo, [desenvolver uma solução de análise preditiva em aprendizado de máquina do Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. 
            [Criar um espaço de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Carregar dados existentes](machine-learning-walkthrough-2-upload-data.md)
3. [Criar um novo teste](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Treinar e avaliar modelos Olá](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Implantar o serviço Web de saudação](machine-learning-walkthrough-5-publish-web-service.md)
6. **Acessar o serviço Web Olá**

- - -
Na etapa anterior de saudação neste passo a passo é implantado um serviço web que usa o nosso modelo de previsão de risco de crédito. Agora os usuários são capazes de toosend dados tooit e recebem resultados. 

Olá serviço Web é um serviço web do Azure que pode receber e retornar dados usando APIs REST de uma das duas maneiras:  

* **Solicitação/resposta** - usuário Olá envia uma ou mais linhas de crédito toohello de dados de serviço usando um protocolo HTTP e Olá serviço responde com um ou mais conjuntos de resultados.
* **Execução em lote** - usuário Olá armazena uma ou mais linhas de dados de crédito em um Azure blob e, em seguida, envia o serviço de toohello Olá blob local. Olá de pontuações de serviço Olá que todos Olá linhas de dados no blob de entrada, repositórios hello resulta em outro blob e retorna Olá URL do contêiner.  

Olá tooaccess de maneira mais rápida e fácil um serviço da web clássico é por meio de saudação [aplicativo Web de serviço de solicitação-resposta do Azure ML](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) ou [modelo de aplicativo do Azure ML lote execução do serviço Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).

Esses modelos de aplicativo Web podem compilar um aplicativo Web personalizado que conhece os dados de entrada do seu serviço Web e o que ele retornará. Você só precisa toodo é fornecer acesso tooyour web serviço e os dados e modelo Olá Olá rest.

Para obter mais informações sobre como usar modelos de aplicativo web hello, consulte [consumir um serviço Web de aprendizado de máquina do Azure com um modelo de aplicativo da web](machine-learning-consume-web-service-with-web-app-template.md).

Você também pode desenvolver um aplicativo personalizado tooaccess Olá web service usando código inicial fornecido em R, c# e linguagens de programação Python.

Você pode encontrar detalhes completos em [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).

