---
title: "aaaCreate avançado codificação fluxos de trabalho com o Designer de fluxo de trabalho | Microsoft Docs"
description: "Saiba mais sobre como toocreate avançado fluxos de trabalho de codificação com o Designer de fluxo de trabalho."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 004815f2-0761-4706-87a1-675ba36e0322
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako;johndeu;anilmur
ms.openlocfilehash: 3744cde54c78bec7c7b586962ec1a8fe9529c1d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-advanced-encoding-workflows-with-workflow-designer"></a>Criar fluxos de trabalho de codificação avançada com o Designer de Fluxo de Trabalho
## <a name="overview"></a>Visão geral
Olá **Designer de fluxo de trabalho** é uma ferramenta de área de trabalho do Windows que é usados toodesign e criar fluxos de trabalho personalizados para codificação com **o fluxo de trabalho do Media Encoder Premium**.
Usando a ativação de saudação da ferramenta do designer de fluxo de trabalho hello, você pode projetar e criar fluxos de trabalho complexos que são executados no **Premium do codificador de mídia**.  

Fluxos de trabalho podem incluir a lógica de decisão do cliente e a ramificação com base nas propriedades do arquivo de fonte de entrada hello. Você pode criar fluxos de trabalho com substituíveis propriedades e valores dinâmicos toomake Olá até mesmo mais complexo codificação tarefas fácil toorepeat e personalizar na nuvem hello.

Os fluxos de trabalho de exemplo que você pode criar incluem:

* Decisão com base em fluxos de trabalho inspecionar o conteúdo de origem Olá para resolução e codificar controla somente de saída de saudação desejada.  Isso é helfpul eliminando rastreia Olá desperdiçada gerado pela colocação em escala maior Olá fonte conteúdo inadvertidamente.
* Vários arquivos de entrada podem ser usados toosupport legendas, sobreposições e junção de conteúdo junto. 

Essa ferramenta também pode ser usado toomodify qualquer um dos nossos [publicado fluxos de trabalho](media-services-workflow-designer.md#existing_workflows). 

> [!NOTE]
> tooget sua cópia da ferramenta de Designer de fluxo de trabalho hello, entre em contato com mepd@microsoft.com.
> 
> 

Quando um arquivo de fluxo de trabalho é criado, ele pode ser carregado como um Ativo e, em seguida, ser usado para codificar arquivos de mídia. Para obter informações sobre como tooencode com **o fluxo de trabalho do Media Encoder Premium** usando **.NET**, consulte [avançados de codificação com o fluxo de trabalho do Media Encoder Premium](media-services-encode-with-premium-workflow.md).

## <a id="existing_workflows"></a>Modificar fluxos de trabalho existentes
Olá padrão [publicado fluxos de trabalho](media-services-workflow-designer.md#existing_workflows) podem ser modificadas usando a ferramenta de designer hello. Você pode obter os arquivos de fluxo de trabalho padrão Olá [aqui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). pasta Olá também contém a descrição de saudação desses arquivos.

Olá vídeos a seguir demonstram como toouse Olá designer.

### <a name="day-1--getting-started"></a>Dia 1 - Introdução
O vídeo do Dia 1 abrange:

* Visão geral do designer
* Fluxos de trabalho básicos – “Hello World”
* Criar vários arquivos MP4 de saída para uso com o streaming dos Serviços de Mídia do Azure

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-1/player]
> 
> 

### <a name="day-2"></a>Dia 2
O vídeo do Dia 2 abrange:

* Diversos cenários de arquivo de origem – a manipulação do áudio
* Fluxos de trabalho com lógica avançada
* Estágios de gráfico

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-2/player]
> 
> 

### <a name="day-3"></a>Dia 3
O vídeo do Dia 3 abrange:

* Scripts em fluxos de trabalho/plantas
* Restrições com hello codificador atual
* Perguntas e respostas

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-3/player]
> 
> 

## <a name="next-step"></a>Próxima etapa
Revise os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

Se precisar de suporte ou tiver perguntas sobre a criação de fluxos de trabalho personalizados na ferramenta de designer de fluxo de trabalho hello, envie um email toomepd@microsoft.com.

## <a name="see-also"></a>Consulte também
[Vídeos de treinamento de Designer de Fluxo de Trabalho do Azure Premium Encoder](http://johndeutscher.com/2015/07/06/azure-premium-encoder-workflow-designer-training-videos/)

