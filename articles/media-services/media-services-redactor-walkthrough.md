---
title: "as faces aaaRedact com instruções passo a passo de análise de mídia do Azure | Microsoft Docs"
description: "Este tópico mostra instruções passo a passo sobre como toorun um fluxo de trabalho de redação completo usando o Azure Media Services Explorer (AMSE) e o Azure Media Redactor visualizador (ferramenta de software livre)."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a>Passo a passo de edição facial com o Azure Media Analytics

## <a name="overview"></a>Visão geral

**Redactor de mídia do Azure** é um [análise de mídia do Azure](media-services-analytics-overview.md) processador de mídia (MP) que oferece redação face escalonável na nuvem hello. Redação da face permite que você toomodify o vídeo em faces de tooblur de ordem de pessoas selecionadas. Talvez você queira serviço de redação de face toouse Olá em cenários de segurança e mídia públicos. Alguns minutos do que contém várias faces podem levar horas tooredact manualmente, mas com esta face de saudação do serviço redação processo requer apenas algumas etapas simples. Para saber mais, confira [este](https://azure.microsoft.com/blog/azure-media-redactor/)blog.

Para obter detalhes sobre **Redactor de mídia do Azure**, consulte Olá [visão geral de redação de Face](media-services-face-redaction.md) tópico.

Este tópico mostra instruções passo a passo sobre como toorun um fluxo de trabalho de redação completo usando o Azure Media Services Explorer (AMSE) e o Azure Media Redactor visualizador (ferramenta de software livre).

Olá **Redactor de mídia do Azure** MP está atualmente em visualização. Ele está disponível em todas as regiões públicas do Azure, bem como em data centers do Governo dos EUA e da China. Esta visualização está disponível gratuitamente no momento. Na versão atual do hello, há um limite de 10 minutos no comprimento de vídeo processado.

Para saber mais, confira [este](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.

## <a name="azure-media-services-explorer-workflow"></a>Fluxo de trabalho do Explorador dos Serviços de Mídia do Azure

Olá tooget de maneira mais fácil de Introdução ao Redactor é a ferramenta AMSE de código aberto toouse Olá no github. Você pode executar um fluxo de trabalho simplificado por meio de **combinados** modo, se você não precisa acessar toohello anotação json ou hello face imagens jpg.

### <a name="download-and-setup"></a>Download e configuração

1. Baixar a ferramenta de AMSE de saudação do [aqui](https://github.com/Azure/Azure-Media-Services-Explorer).
1. Faça logon na conta de serviços de mídia usando sua chave de serviço de tooyour.

    tooobtain Olá nome da conta e informações de chave, vá toohello [portal do Azure](https://portal.azure.com/) e selecione sua conta AMS. Em seguida, selecione Configurações > Chaves. windows do Hello gerenciar chaves mostra o nome da conta hello e as chaves primárias e secundárias Olá é exibida. Copie os valores do nome da conta hello e Olá primary key.

![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a>Primeira aprovação – modo de análise

1. Carregue seu arquivo de mídia em Ativo –> Carregar, ou arrastando e soltando. 
1. Clique com botão direito e processe o arquivo de mídia usando a Análise de Mídia –> Azure Media Redactor –> Modo de Análise. 


![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

saída de Hello incluirá um arquivo json de anotações com dados de local de face, bem como jpg cada face detectado. 

![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a>Segunda aprovação – modo de edição

1. Carregue seu toohello ativo de vídeo original de saída da primeira passagem de saudação e definido como um ativo primário. 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. (Opcional) Carregar um arquivo de 'Dance_idlist.txt', que inclui uma lista delimitada de nova linha de saudação IDs que você deseja tooredact. 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. (Opcional) Fazer com que qualquer arquivo de annotations.json toohello edições como aumentar Olá limites da caixa delimitadora. 
4. Olá ativo de saída da primeira passagem de saudação clique com botão direito, selecione Olá Redactor e executar com hello **Redact** modo. 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. Baixar ou compartilhar Olá ativo de saída redigida final. 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a>Ferramenta de código-fonte aberto Azure Media Redactor Visualizador

Um código-fonte aberto [ferramenta Visualizador](https://github.com/Microsoft/azure-media-redactor-visualizer) é projetado toohelp desenvolvedores começando com o formato de anotações de saudação com análise e usando a saída de hello.

Após clonar o repositório de hello, no projeto de saudação do toorun ordem, você precisará toodownload FFMPEG de seus [site oficial do](https://ffmpeg.org/download.html).

Se você for um desenvolvedor tentar tooparse Olá dados de anotação de JSON, examinar Models.MetaData para obter exemplos de código de exemplo.

### <a name="set-up-hello-tool"></a>Configurar a ferramenta de saudação

1.  Baixar e compile a solução inteira hello. 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  Baixe FFMPEG [aqui](https://ffmpeg.org/download.html). Este projeto foi desenvolvido originalmente com a versão be1d324 (2016-10-04) e com vinculação estática. 
3.  Copiar toohello ffmpeg.exe e ffprobe.exe mesma pasta de saída como AzureMediaRedactor.exe. 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. Execute AzureMediaRedactor.exe. 

### <a name="use-hello-tool"></a>Use a ferramenta Olá

1. Processe o vídeo em sua conta de serviços de mídia do Azure com hello Redactor MP no modo de analisar. 
2. Baixar o arquivo de vídeo original hello e saída Olá Olá redação - analisar o trabalho. 
3. Execute o aplicativo de visualizador hello e escolher Olá arquivos acima. 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. Visualize o arquivo. Selecione qual faces você gostaria que tooblur por meio de barra lateral Olá Olá direita. 
    
    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  campo de texto Olá inferior será atualizado com face Olá IDs. Crie um arquivo chamado "idlist.txt" com essas IDs como uma lista delimitada por nova linha. 

    >[!NOTE]
    > Olá idlist.txt devem ser salvos em ANSI. Você pode usar o bloco de notas toosave ANSI.
    
6.  Carregar este ativo de saída do arquivo toohello da etapa 1. Carregar Olá toothis vídeo ativo original também e definido como ativo primário. 
7.  Execute trabalho de redação deste ativo com "Redact" modo tooget Olá final redigido vídeo. 

## <a name="next-steps"></a>Próximas etapas 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Links relacionados
[Visão geral do Azure Media Services Analytics](media-services-analytics-overview.md)

[Demonstrações do Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[Anunciando a redação da face da Análise de Mídia do Azure](https://azure.microsoft.com/blog/azure-media-redactor/)
