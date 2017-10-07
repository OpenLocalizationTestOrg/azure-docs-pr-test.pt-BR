---
title: "aaaMedia análise na plataforma de serviços de mídia Olá | Microsoft Docs"
description: "Visão geral da versão prévia pública da Análise de Mídia, uma coleção de serviços de fala e de pesquisa visual computacional de nível empresarial, de conformidade, segurança e alcance global"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a>Análise de mídia na plataforma de serviços de mídia Olá
## <a name="overview"></a>Visão geral
Mais organizações estão usando o vídeo como Olá preferencial tootrain médio seus funcionários, envolver seus clientes e funções de negócios do documento. Fornece uma maneira toostore, de computação em nuvem de fluxo e acessar esses arquivos de mídia grandes. Mas à medida que aumenta a biblioteca de uma empresa de conteúdo de vídeo, precisa de uma forma igualmente eficaz de extração de informações de conteúdo de saudação. 

tooaddress essa necessidade crescente, os serviços de mídia do Azure oferece a análise de mídia do Azure. Análise de mídia é uma coleção de componentes de fala e visão que torna mais fácil para as organizações e empresas tooderive de informações práticas de seus arquivos de vídeo. Construído usando componentes de plataforma Olá principais serviços de mídia, análise de mídia pode lidar com processamento em escala em um dia de mídia.

Com a Análise de Mídia, os desenvolvedores podem trazer rapidamente funcionalidades de vídeo avançadas para aplicativos. Ele fornece os ambientes corporativos escala hello, conformidade, segurança e alcance global exigido por organizações de grandes porte.

Olá diagrama a seguir mostra a análise de mídia e outras partes principais da plataforma de serviços de mídia hello. 

![Fluxo de trabalho VoD](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

O processador de mídia da Análise de Mídia produz arquivos MP4 ou arquivos JSON. Se um processador de mídia produz um arquivo MP4, você pode baixar progressivamente arquivo hello. Se um processador de mídia produz um arquivo JSON, você pode baixar o arquivo de saudação do armazenamento de BLOBs do Azure. 

## <a name="media-analytics-services"></a>Serviços de Análise de Mídia

### <a name="indexer"></a>Indexador
Com o Azure Media Indexer, você pode tornar o conteúdo pesquisável e gerar faixas de legendagem. Versão anterior do toohello comparados, visualização de 2 do indexador de mídia do Azure tem mais ampla e indexação mais rápida de linguagem suporte. Dentre os idiomas com suporte estão: inglês, espanhol, francês, alemão, italiano, chinês, português e árabe. Para obter informações detalhadas e exemplos, consulte [Processar vídeos com o Azure Media Indexer 2](media-services-process-content-with-indexer2.md).
### <a name="hyperlapse"></a>Hyperlapse
Microsoft Hyperlapse combina os vídeos lapso de tempo de capacidade rápidos e consumo de toocreate de seu conteúdo de forma longa e estabilização de vídeo. Além de criar vídeo lapso de tempo, você pode usar Hyperlapse toocreate estáveis vídeos de vídeos shaky capturados por meio de telefones celulares e câmeras. Para ver informações detalhadas e exemplos, consulte [Arquivos de Mídia do Hyperlapse com o Azure Media Hyperlapse](media-services-hyperlapse-content.md).
### <a name="motion-detector"></a>Detector de Movimento
Você pode usar o movimento do Detector de movimento toodetect em um vídeo com planos de fundo estáticos. Isso torna possível toocheck para falsos positivos em eventos de movimento detectados pelo câmeras de vigilância. Para obter informações detalhadas e exemplos, consulte [Detecção de movimento para Análise de Mídia do Azure](media-services-motion-detection.md).
### <a name="face-detector"></a>Detector Facial
Usando o Face Detector, é possível detectar as faces das pessoas e suas emoções, incluindo felicidade, tristeza e surpresa. Isso tem várias aplicações úteis na indústria, descritas abaixo, incluindo agregar e analisar reações de pessoas participando de um evento. Para obter informações detalhadas e exemplos, consulte [Detecção facial e de emoções da Análise de Mídia do Azure](media-services-face-and-emotion-detection.md).
### <a name="video-summarization"></a>Resumo de vídeo
Resumo de vídeo pode ajudá-lo a criar resumos dos vídeos longos selecionando automaticamente trechos interessantes de vídeo de origem hello. Essa capacidade é útil quando você deseja tooprovide uma visão rápida do que tooexpect em um vídeo longo. Para obter informações detalhadas e exemplos, consulte [resumo de vídeo do uso do Azure Media vídeo miniaturas toocreate](media-services-video-summarization.md).
### <a name="optical-character-recognition"></a>Reconhecimento de caractere óptico
O OCR (reconhecimento óptico de caracteres) de Mídia do Azure permite que você converta o conteúdo de texto de arquivos de vídeo em texto digital editável e pesquisável. Em seguida, você pode automatizar extração Olá de metadados significativo de sinal de vídeo de saudação da sua mídia.
### <a name="scalable-face-redaction"></a>Edição facial escalonável
Redactor de mídia do Azure é um processador de mídia de análise de mídia que oferece redação face escalonável na nuvem hello. Usando face redação, você pode modificar seu vídeo tooblur as faces de pessoas selecionadas. Talvez você queira toouse o serviço de redação Olá face na mídia ou a segurança pública está envolvida. Alguns minutos do que contém várias faces podem levar horas tooredact manualmente, mas com esse serviço, redação face leva apenas algumas etapas simples. Para obter mais informações, consulte Olá [redigir faces com análise de mídia do Azure](media-services-face-redaction.md) artigo.

## <a name="common-scenarios"></a>Cenários comuns
A Análise de Mídia pode ajudar as organizações e empresas a obter novas informações de vídeos e gerenciar grandes volumes de conteúdo de vídeo com mais eficácia. Veja os diversos cenários a seguir:

* **Call centers**. Mesmo com o surgimento de saudação de mídia social, call centers de clientes ainda facilitam um grande percentual de transações de atendimento ao cliente. Codificado nesses dados de áudio é uma grande quantidade de informações do cliente que podem ser analisados tooachieve maior satisfação do cliente. Usando o Indexador de Mídia, as organizações podem extrair texto e criar índices de pesquisa e painéis. Em seguida, elas podem extrair inteligência sobre reclamações comuns, fontes de reclamações e outros dados relevantes.
* **Moderação de conteúdo gerado pelo usuário**. De departamentos de toopolice de tomadas de mídia, muitas organizações têm portais público que aceitam mídia gerado pelo usuário, como imagens e vídeos. volume de saudação de conteúdo pode ter picos toounexpected eventos de vencimento. Nesses cenários, é difícil tooconduct revisões de manual eficaz de conteúdo para conveniência. Os clientes podem depender Olá toofocus de moderação de conteúdo do serviço no conteúdo apropriado.
* **Vigilância**. Com hello crescimento em uso de câmeras IP é fornecido um inventário crescente de vídeo de vigilância. Revisar manualmente o vídeo de vigilância é toohuman intensiva e propensas a erro em tempo. Análise de mídia fornece serviços, como detecção de movimento, detecção de rosto e processo de saudação do Hyperlapse toomake de revisão, gerenciamento e criação de derivados.

## <a name="media-analytics-media-processors"></a>Processadores de mídia da Análise de Mídia
Esta seção lista processadores de mídia de análise de mídia de saudação e mostra como toouse .NET ou REST tooget um objeto de processador (MP) de mídia.

### <a name="mp-names"></a>Nomes dos MP
* Preview do Indexador de Mídia do Azure 2
* Indexador de Mídia do Azure
* Azure Media Hyperlapse
* Detector de Rostos em Mídias do Azure
* Detector de Movimento em Mídias do Azure
* Miniaturas de Vídeo de Mídia do Azure
* OCR de Mídia do Azure

### <a name="net"></a>.NET
Olá após a função usa um de saudação especificado MP nomes e retorna um objeto de pacote de gerenciamento.

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a>REST
Solicitação:

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

Resposta:

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a>Demonstrações
Consulte [Demonstrações da Análise de Mídia do Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).

## <a name="next-steps"></a>Próximas etapas
Examine os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Artigos relacionados
Consulte o [Comunicado da análise dos Serviços de Mídia](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
