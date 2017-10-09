---
title: "serviço da web aaaTroubleshoot treinamento um clássico de aprendizado de máquina do Azure | Microsoft Docs"
description: "Identifique e corrija encontrado comum de problemas quando você estiver treinamento modelo Olá para um serviço de Web do aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a>Olá treinamento de um serviço Web clássico do Azure Machine Learning de solução de problemas
## <a name="retraining-overview"></a>Visão geral da readaptação
Quando você implanta um experimento de previsão como um serviço Web de pontuação, ele é um modelo estático. Conforme novos dados se torna disponíveis ou quando o consumidor Olá Olá API tem seus próprios dados, o modelo Olá precisa toobe treinados novamente. 

Para obter uma explicação completa de saudação treinar novamente o processo de um serviço Web clássico, consulte [treinar novamente Machine Learning modelos por meio de programação](machine-learning-retrain-models-programmatically.md).

## <a name="retraining-process"></a>Processo de readaptação
Quando você precisar tooretrain Olá serviço da Web, você deve adicionar algumas informações adicionais:

* Um serviço da Web implantado por meio de saudação experiência de treinamento. experiência de saudação deve ter uma **saída do serviço Web** módulo anexado toohello saída de hello **treinar modelo** módulo.  
  
    ![Anexe o modelo de treinamento de toohello Olá web serviço saída.][image1]
* Um novo ponto de extremidade adicionados tooyour serviço Web de pontuação.  Você pode adicionar o ponto de extremidade Olá programaticamente usando código de exemplo hello referenciado em Olá aprendizado de máquina treinar novamente modelos programaticamente tópico ou por meio de saudação portal clássico do Azure.

Você pode usar código c# exemplo de saudação do modelo de tooretrain do serviço de Web do treinamento Olá API ajuda página. Depois de ter avaliado resultados Olá e está satisfeito com eles, você atualizar o modelo treinado hello, serviço web usando Olá novo ponto de extremidade que você adicionou a pontuação.

Com todas as partes da saudação em vigor, etapas principais hello, você deve executar o modelo de saudação tooretrain são:

1. Chamar hello serviço da Web de treinamento: chamada hello toohello serviço de execução de lote (BES), não Olá serviço de resposta de solicitação (RR). Você pode usar o código c# exemplo hello na chamada de Olá Olá API ajuda página toomake. 
2. Localizar valores de saudação para Olá *BaseLocation*, *RelativeLocation*, e *SasBlobToken*: esses valores são retornados na saída de saudação do toohello sua chamada de treinamento Serviço. 
   ![Mostrar saída Olá Olá treinamento valores BaseLocation, RelativeLocation e SasBlobToken de exemplo e hello.][image6]
3. Atualização Olá adicionado modelo treinado do ponto de extremidade do hello novo serviço web com hello de pontuação: usando o código de exemplo hello fornecido Olá aprendizado de máquina treinar novamente modelos programaticamente, atualizar novo ponto de extremidade de saudação adicionado toohello pontuação modelos com hello recentemente modelo treinado de saudação serviço da Web de treinamento.

## <a name="common-obstacles"></a>Obstáculos comuns
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a>Verificar toosee se você tiver Olá corrigir PATCH URL
Olá PATCH URL que está usando deve ser Olá associado Olá novo ponto de extremidade de pontuação adicionado toohello serviço Web de pontuação. Há uma série de maneiras tooobtain Olá PATCH URL:

**Opção 1: use um programa**

Olá tooget corrigir PATCH URL:

1. Executar Olá [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) código de exemplo.
2. Da saída de saudação de AddEndpoint, localize Olá *HelpLocation* valor e copie a URL de saudação.
   
   ![HelpLocation na saída de saudação do exemplo de addEndpoint hello.][image2]
3. Cole a URL de saudação em uma página de tooa toonavigate de navegador que fornece links de ajuda para Olá serviço da Web.
4. Clique em Olá **recurso de atualização** página de Ajuda do link tooopen Olá patch.

**Opção 2: Usar Olá portal clássico do Azure**

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Guia de aprendizado de máquina Olá aberto. ![Guia Machine Learning.][image4]
3. Clique no nome do espaço de trabalho e depois em **Serviços Web**.
4. Clique em Olá serviço Web que você está trabalhando com a pontuação. (Se você não modificou o nome padrão de saudação do serviço web de saudação, ela terminará em [pontuação Exp]..)
5. Clicar em **Adicionar Ponto de Extremidade**.
6. Depois que o ponto de extremidade de saudação é adicionado, clique em nome do ponto de extremidade de saudação. Em seguida, clique em **recurso de atualização** tooopen Olá a página de ajuda de aplicação de patch.

> [!NOTE]
> Se você tiver adicionado toohello serviço da Web de treinamento do ponto de extremidade Olá em vez da saudação serviço Web de previsão, você receberá Olá erro a seguir quando você clica em Olá **recurso de atualização** link: Desculpe, mas não há suporte para esse recurso ou disponível neste contexto. Este serviço Web não tem recursos atualizáveis. Lamentamos o inconveniente hello e está trabalhando em melhorar o fluxo de trabalho.
> 
> 

![Painel Novo ponto de extremidade.][image3]

página de ajuda de PATCH Olá contém Olá URL PATCH, você deve usar e fornece código de exemplo, você pode usar toocall-lo.

![URL de patch.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a>Toosee de seleção que você está atualizando Olá pontuação ponto de extremidade correto
* Patch não Olá serviço da Web de treinamento: operação de patch Olá deve ser executada em Olá pontuação serviço da Web.
* Não corrigir o ponto de extremidade saudação padrão no serviço Web: operação de patch Olá deve ser executada em Olá pontuação novo ponto de extremidade de serviço de Web que você adicionou.

Você pode verificar qual ponto de extremidade de saudação do Web service é ativado por Olá visitando portal clássico do Azure. 

> [!NOTE]
> Certifique-se de que você está adicionando toohello de ponto de extremidade Olá serviço Web de previsão, Olá serviço da Web de treinamento. Se você tiver implantado corretamente um serviço Web de previsão e um serviço da Web de treinamento, você verá dois serviços Web separados listados. Olá serviço Web de previsão deve terminar com "[previsão exp]"..
> 
> 

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Guia de aprendizado de máquina Olá aberto. ![IU do espaço de trabalho do Machine Learning.][image4]
3. Selecione o espaço de trabalho.
4. Clique em **Serviços Web**.
5. Selecione o Serviço Web de previsão.
6. Verifique se o novo ponto de extremidade foi adicionado toohello Web service.

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a>Verificar espaço de trabalho de saudação que seu serviço web está em tooensure é na região correta Olá
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Selecione o aprendizado de máquina no menu de saudação.
   ![IU da região do Machine Learning.][image4]
3. Verifique se o local de saudação do seu espaço de trabalho.

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
