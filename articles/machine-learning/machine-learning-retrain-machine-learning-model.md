---
title: "um modelo de aprendizado de máquina do aaaRetrain | Microsoft Docs"
description: "Saiba como tooretrain um modelo e atualização Olá Web serviço toouse Olá recentemente treinado no aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a>Readaptar um modelo do Machine Learning
Como parte do processo de saudação do operacionalização de modelos de aprendizado de máquina no aprendizado de máquina do Azure, o modelo é treinado e salvo. Em seguida, use-toocreate um serviço Web predicative. saudação de serviço da Web pode ser consumida em sites da web, painéis e aplicativos móveis. 

Os modelos que você cria usando o Machine Learning geralmente não são estáticos. À medida que novos dados se torna disponíveis ou quando o consumidor Olá Olá API tem seu próprio modelo de saudação de dados precisa toobe treinados novamente. 

A readaptação pode ocorrer com frequência. Com recurso de programação API treinamento hello, programaticamente você pode treinar novamente modelo hello usando o serviço de Web de saudação de APIs de treinamento e de atualização de Olá Olá recentemente treinado. 

Este documento descreve Olá processo de treinamento e mostra como toouse Olá APIs de treinamento.

## <a name="why-retrain-defining-hello-problem"></a>Por que treinar novamente: definindo Olá problema
Como parte do processo de treinamento de aprendizado de máquina hello, um modelo é treinado usando um conjunto de dados. Os modelos que você cria usando o Machine Learning geralmente não são estáticos. À medida que novos dados se torna disponíveis ou quando o consumidor Olá Olá API tem seu próprio modelo de saudação de dados precisa toobe treinados novamente.

Nesses cenários, uma API de programação fornece uma maneira conveniente de tooallow você ou hello consumidor de seu toocreate APIs um cliente que pode, em uma base única ou regular, treinar novamente modelo hello usando seus próprios dados. Em seguida, podem avaliar os resultados de saudação do treinamento e atualizar Olá Web serviço API toouse Olá recentemente treinado.

> [!NOTE]
> Se você tiver uma experiência de treinamento existentes e o serviço Web de novo, convém toocheck out treinar novamente uma previsão Web serviço em vez de seguir Olá passo a passo mencionada na Olá seção a seguir.
> 
> 

## <a name="end-to-end-workflow"></a>Fluxos de trabalho completos
Olá, processo envolve Olá componentes a seguir: uma experiência de treinamento e teste uma previsão publicado como um serviço Web. tooenable treinamento de um modelo treinado, Olá experiência de treinamento deve ser publicado como um serviço Web com saída de saudação de um modelo treinado. Isso permite que o modelo de toohello de acesso de API para treinamento. 

Olá, as etapas a seguir se aplicam a tooboth novo e clássico serviços da Web:

Crie serviço Web de previsão inicial de saudação:

* Criar um teste de treinamento
* Criar um teste da Web preditivo
* Implantar um serviço Web preditivo

Treinar novamente o serviço Web de saudação:

* Atualizar tooallow de experiência de treinamento para treinamento
* Implantar Olá treinamento serviço web
* Usar o modelo de saudação do hello serviço de execução de lote código tooretrain

Para obter uma explicação da saudação etapas anteriores, consulte [aprendizado de máquina treinar novamente modelos programaticamente](machine-learning-retrain-models-programmatically.md).

> [!NOTE] 
> toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você implantar o serviço web de saudação. Para obter mais informações, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md). 

Se você implantou um Serviço Web Clássico:

* Criar um novo ponto de extremidade no serviço Web de previsão de saudação
* Obter URL de PATCH hello e código
* Use Olá URL PATCH toopoint Olá novo ponto de extremidade no hello treinados novamente o modelo 

Para obter uma explicação da saudação etapas anteriores, consulte [treinar novamente um serviço Web clássico](machine-learning-retrain-a-classic-web-service.md).

Se você tiver dificuldade para treinamento de um serviço Web clássico, consulte [Olá treinamento de um serviço Web clássico do Azure Machine Learning de solução de problemas](machine-learning-troubleshooting-retraining-models.md).

Se você tiver implantado um Novo serviço Web:

* Entrar tooyour conta de Gerenciador de recursos do Azure
* Obter definição de serviço Web Olá
* Saudação de exportação de definição de serviço Web como JSON
* Atualizar Olá referência toohello `ilearner` blob em Olá JSON
* Importar Olá JSON em uma definição de serviço Web
* Olá Web serviço de atualização com a nova definição de serviço Web

Para obter uma explicação da saudação etapas anteriores, consulte [treinar novamente um serviço Web de novo usando cmdlets do PowerShell de gerenciamento de aprendizado de máquina Olá](machine-learning-retrain-new-web-service-using-powershell.md).

processo de saudação para configurar o treinamento de um serviço Web clássico envolve Olá etapas a seguir:

![Visão geral do processo readaptação][1]

processo de saudação para configurar o treinamento de um serviço Web de novo envolve Olá etapas a seguir:

![Visão geral do processo readaptação][7]

## <a name="other-resources"></a>Outros recursos
* [Retraining and Updating Azure Machine Learning models with Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/) (Readaptando e atualizando modelos do Machine Learning com o Azure Data Factory)
* [Criar vários modelos do Machine Learning e pontos de extremidade de serviço Web com base em um teste usando o PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md)
* Olá [AML treinar novamente modelos usando APIs](https://www.youtube.com/watch?v=wwjglA8xllg) vídeo mostra como modelos de aprendizado de máquina tooretrain criados no aprendizado de máquina do Azure usando Olá PowerShell e APIs de treinamento.

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

