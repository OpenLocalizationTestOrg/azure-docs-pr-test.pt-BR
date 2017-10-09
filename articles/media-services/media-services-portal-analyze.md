---
title: "aaaAnalyze sua mídia usando Olá portal do Azure | Microsoft Docs"
description: "Este tópico discute como tooprocess Olá de mídia com processadores de mídia de análise de mídia (MPs) usando o portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a>Analisar sua mídia usando Olá portal do Azure
> [!NOTE]
> toocomplete neste tutorial, você precisa de uma conta do Azure. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

## <a name="overview"></a>Visão geral
Análise de serviços de mídia do Azure é uma coleção de componentes de visão e fala (em escala empresarial, conformidade, segurança e alcance global) que facilitam para organizações e empresas tooderive de informações práticas de seus arquivos de vídeo. Para maiores detalhes da Análise de Serviços de Mídia do Azure consulte [esse](media-services-analytics-overview.md) tópico. 

Este tópico discute como tooprocess Olá de mídia com processadores de mídia de análise de mídia (MPs) usando o portal do Azure. Os MPs da Análise de Mídia produzem arquivos MP4 ou arquivos JSON. Se um processador de mídia produziu um arquivo MP4, você pode baixar progressivamente arquivo hello. Se um processador de mídia produziu um arquivo JSON, você pode baixar o arquivo de saudação do hello armazenamento de BLOBs do Azure. 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a>Escolha um ativo que você deseja tooanalyze
1. Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.
2. Em Olá **configurações** janela, selecione **ativos**.  
   .
    ![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. Ativo Olá selecione que você gostaria de saudação tooanalyze e pressione **analisar** botão.
   
    ![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. Em Olá **ativo de mídia do processo com análise de mídia** janela, processador Olá select. 
   
    restante de saudação do artigo Olá explica por que e como toouse cada processador. 
5. Pressione **criar** toohello iniciar um trabalho.

## <a name="azure-media-indexer"></a>Indexador de Mídia do Azure
Olá **Azure Media Indexer** processador de mídia permite que você toomake arquivos de mídia e conteúdo pesquisável, bem como gerar faixas de legendas fechadas. Esta seção fornece alguns detalhes sobre as opções que você pode especificar para esse MP.

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a>idioma
Olá toobe de linguagem natural reconhecido no arquivo de multimídia hello. Por exemplo, inglês ou espanhol. 

### <a name="captions"></a>Legendas
Você pode escolher um formato de legenda que será gerado do seu conteúdo. Um trabalho de indexação pode gerar arquivos de legenda codificada Olá formatos a seguir:  

* **SAMI**
* **TTML**
* **WebVTT**

Arquivos fechados de legenda (CC) nos seguintes formatos podem ser usados toomake áudio e vídeo arquivos toopeople acessível com deficiência auditiva.

### <a name="aib-file"></a>Arquivo AIB
Selecione esta opção se você seria como arquivo de Blob de índice de áudio toogenerate Olá para uso com hello IFilter personalizadas de servidor SQL. Para saber mais, confira [este](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.

### <a name="keywords"></a>Palavras-chave
Selecione esta opção se você gostaria que toogenerate um arquivo XML de palavras-chave. Este arquivo contém palavras-chave extraídas do conteúdo de fala hello, com frequência e a informação de deslocamento.

### <a name="job-name"></a>Nome do trabalho
Um nome amigável que permite identificar o trabalho de saudação. [Isso](media-services-portal-check-job-progress.md) artigo descreve como você pode monitorar o andamento de saudação de um trabalho. 

### <a name="output-file"></a>Arquivo de saída
Um nome amigável que permite identificar Olá conteúdo de saída. 

## <a name="azure-media-hyperlapse"></a>Azure Media Hyperlapse
O Azure Media Hyperlapse é um MP que cria vídeos suaves de lapso de tempo de conteúdo de primeira pessoa ou de uma câmera de ação.  Para obter mais informações, consulte [este](media-services-hyperlapse-content.md) tópico. Esta seção fornece alguns detalhes sobre as opções que você pode especificar para esse MP.

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a>Velocidade
Especifique a velocidade de saudação com qual toospeed o vídeo de entrada hello. saída de Hello é uma representação estabilizar e tempo decorrido de vídeo de entrada hello.

### <a name="job-name"></a>Nome do trabalho
Um nome amigável que permite identificar o trabalho de saudação. [Isso](media-services-portal-check-job-progress.md) artigo descreve como você pode monitorar o andamento de saudação de um trabalho. 

### <a name="output-file"></a>Arquivo de saída
Um nome amigável que permite identificar Olá conteúdo de saída. 

## <a name="azure-media-face-detector"></a>Detector de Rostos em Mídias do Azure
Olá **Detector de Face de mídia do Azure** processador de mídia (MP) permite que você toocount, acompanhar movimentos e até mesmo a participação do medidor público e reação via expressões faciais. Este serviço contém dois recursos: 

* **Detecção facial**
  
    A detecção facial localiza e acompanha as faces humanas em um vídeo. Várias faces podem ser detectadas e posteriormente ser controladas à medida que se movimentam, com metadados de hora e o local de saudação retornados em um arquivo JSON. Durante o rastreamento, ele tentará toogive um toohello ID consistente mesmo enfrentam enquanto pessoa Olá é mover-se na tela, mesmo se eles são obstruídos ou deixam brevemente quadro hello.
  
  > [!NOTE]
  > Esses serviços não realizam o reconhecimento facial. Uma pessoa que sai do quadro de saudação ou se torna obstruída para muito tempo será fornecida uma nova ID quando elas retornam.
  > 
  > 
* **Detecção de emoções**
  
    Detecção de emoção é um componente opcional do hello processador de mídia de detecção de rosto que retorna análise em vários atributos emocionais de faces Olá detectadas, inclusive felicidade, tristeza, medo, irritação e muito mais. 

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a>Modo de detecção
Uma saudação modos a seguir pode ser usada pelo processador de saudação:

* detecção facial
* detecção de emoções faciais
* detecção de emoção de agregada

### <a name="job-name"></a>Nome do trabalho
Um nome amigável que permite identificar o trabalho de saudação. [Isso](media-services-portal-check-job-progress.md) artigo descreve como você pode monitorar o andamento de saudação de um trabalho. 

### <a name="output-file"></a>Arquivo de saída
Um nome amigável que permite identificar Olá conteúdo de saída. 

## <a name="azure-media-motion-detector"></a>Detector de Movimento em Mídias do Azure
Olá **Detector de movimento de mídia do Azure** habilita (MP) do processador de mídia tooefficiently você identificar seções de interesse em um vídeo de outra forma longa e sem problemas. Detecção de movimento pode ser usada em câmera estático filmagens tooidentify seções de vídeo Olá onde ocorre a animação. Ele gera um arquivo JSON que contém um metadados com carimbos de hora e hello delimitadora região em que ocorreu o evento hello.

Destinado a feeds de vídeo de segurança, essa tecnologia é capaz de toocategorize movimento em eventos relevantes e falsos positivos, como alterações de iluminação e sombras. Isso permite toogenerate alertas de segurança de feeds de câmera sem recebam eventos irrelevantes infinito, enquanto estiver sendo momentos tooextract capaz de interesse de vídeos de vigilância muito longos.

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a>Miniaturas de Vídeo de Mídia do Azure
Este processador pode ajudá-lo a criar resumos dos vídeos longos selecionando automaticamente trechos interessantes de vídeo de origem hello. Isso é útil quando você deseja tooprovide uma visão rápida do que tooexpect em um vídeo longo. Para obter informações detalhadas e exemplos, consulte [tooCreate de uso do Azure Media Video miniaturas um resumo de vídeo](media-services-video-summarization.md)

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a>Nome do trabalho
Um nome amigável que permite identificar o trabalho de saudação. [Isso](media-services-portal-check-job-progress.md) artigo descreve como você pode monitorar o andamento de saudação de um trabalho. 

### <a name="output-file"></a>Arquivo de saída
Um nome amigável que permite identificar Olá conteúdo de saída. 

## <a name="next-steps"></a>Próximas etapas
Exibir os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

