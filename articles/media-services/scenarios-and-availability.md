---
title: "aaaMicrosoft Azure Media Services cenários e disponibilidade de recursos em data centers | Microsoft Docs"
description: "Este tópico fornece uma visão geral dos cenários dos Serviços de Mídia do Microsoft Azure e a disponibilidade de recursos e serviços nos datacenters."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a>Cenários e disponibilidade de recursos dos Serviços de Mídia em datacenters

Microsoft Azure Media Services (AMS) permite que você toosecurely carregar, armazenar, codificar e empacotar conteúdo de áudio ou vídeo sob demanda e ao vivo streaming entrega toovarious clientes (por exemplo, TV, PC e dispositivos móveis).

AMS opera em vários data centers Olá, mundo. Esses centros de dados são agrupados em regiões toogeographic, dando a você a flexibilidade de escolher onde toobuild seus aplicativos. Você pode examinar Olá [lista de regiões e seus locais](https://azure.microsoft.com/regions/). 

Este tópico mostra os cenários comuns de entrega de conteúdo [ao vivo](#live_scenarios) ou [sob demanda](#vod_scenarios). tópico Olá também fornece detalhes sobre a disponibilidade de recursos de mídia e serviços nos data centers.

## <a name="overview"></a>Visão geral

### <a name="prerequisites"></a>Pré-requisitos

toostart usando serviços de mídia do Azure, você deve ter o seguinte hello:

* Uma conta do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com).
* Uma conta de Serviços de Mídia do Azure. Para obter mais informações, veja [Criar conta](media-services-portal-create-account.md).
* saudação do qual você deseja que o conteúdo de toostream de ponto de extremidade de streaming tem toobe em Olá **executando** estado.

    Quando sua conta AMS é criada, um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming de streaming tem toobe em Olá **executando** estado.

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a>Os objetos normalmente usados ao desenvolver em relação a saudação modelo AMS OData

Hello imagem a seguir mostra alguns dos objetos hello mais comumente usada durante o desenvolvimento em modelo de mídia serviços OData hello.

Clique em Olá imagem tooview-tamanho máximo.  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

Você pode exibir uma saudação todo modelo [aqui](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a>Proteger o conteúdo no armazenamento e streaming de mídia no hello entregar Limpar (não criptografado)

![Fluxo de trabalho VoD](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. Carregue um arquivo de mídia de alta qualidade em um ativo.

    Recomenda-se ativo tooapply armazenamento criptografia opção tooyour em ordem tooprotect seu conteúdo durante o carregamento e enquanto em repouso no armazenamento.
2. Codifica tooa conjunto de arquivos MP4 com taxa de bits adaptável.

    É recomendável tooapply toohello de opção de criptografia de armazenamento saída ativo em ordem tooprotect do conteúdo em repouso.
3. Configure a política de entrega de ativos (usada pelo empacotamento dinâmico).

    Se seu ativo tiver o armazenamento criptografado, você **deverá** configurar a política de entrega de ativos.
4. Publica o ativo de saudação criando um localizador OnDemand.
5. Fluxo de conteúdo publicado.

Para obter informações sobre a disponibilidade em data centers, consulte Olá [disponibilidade](#availability) seção.

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a>Proteger o conteúdo no armazenamento, fornecer mídia de streaming criptografada dinamicamente

![Proteger com o PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. Carregue um arquivo de mídia de alta qualidade em um ativo. Aplica o ativo de toohello de opção de criptografia de armazenamento.
2. Codifica tooa conjunto de arquivos MP4 com taxa de bits adaptável. Aplica o ativo de saída toohello do opção de criptografia de armazenamento.
3. Crie chave de criptografia de conteúdo para ativo Olá que deseja toobe dinamicamente criptografado durante a reprodução.
4. Configure a política de autorização de chave de conteúdo.
5. Configure a política de entrega de ativos (usada pelo empacotamento dinâmico e criptografia dinâmica).
6. Publica o ativo de saudação criando um localizador OnDemand.
7. Fluxo de conteúdo publicado.

Para obter informações sobre a disponibilidade em data centers, consulte Olá [disponibilidade](#availability) seção.

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a>Usar análise de mídia tooderive acionável insights de vídeos

Análise de mídia é uma coleção de componentes de fala e visão que facilitam para organizações e empresas tooderive de informações práticas de seus arquivos de vídeo. Para saber mais, confira [Visão geral a Análise dos Serviços de Mídia do Azure](media-services-analytics-overview.md).

1. Carregue um arquivo de mídia de alta qualidade em um ativo.
2. Processar seus vídeos com um dos serviços de análise de mídia Olá descritos Olá [visão geral da análise de mídia](media-services-analytics-overview.md) seção.
3. O processador de mídia da Análise de Mídia produz arquivos MP4 ou arquivos JSON. Se um processador de mídia produziu um arquivo MP4, você pode baixar progressivamente arquivo hello. Se um processador de mídia produziu um arquivo JSON, você pode baixar o arquivo de saudação do hello armazenamento de BLOBs do Azure.

Para obter informações sobre a disponibilidade em data centers, consulte Olá [disponibilidade](#availability) seção.

## <a name="deliver-progressive-download"></a>Entregar o download progressivo

1. Carregue um arquivo de mídia de alta qualidade em um ativo.
2. Codifica o arquivo MP4 único de tooa.
3. Publica o ativo de saudação criando um localizador OnDemand ou SAS.

    Se usando o localizador SAS, Olá é baixado do hello armazenamento de BLOBs do Azure. Nesse caso, você não precisa toohave streaming pontos de extremidade no estado iniciado.
4. Download progressivo de conteúdo.

## <a id="live_scenarios"></a>Entregando eventos de streaming ao vivo 

1. Inclua o conteúdo ao vivo usando diversos protocolos de streaming ao vivo (por exemplo, RTMP ou Smooth Streaming).
2. (opcionalmente) Codifique seu stream no fluxo de bits adaptável.
3. Visualize seu stream ao vivo.
4. entregar conteúdo Olá por meio de protocolos de transmissão comuns (por exemplo, MPEG DASH, Smooth, HLS) diretamente tooyour clientes ou tooa rede de fornecimento de conteúdo (CDN) para melhor distribuição.

    -ou-

    Registro e o repositório de conteúdo de saudação incluído na ordem toobe transmitido posterior (vídeo sob demanda).

Ao fazer a transmissão ao vivo, você pode escolher uma das seguintes Olá roteia:

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Trabalhando com canais que recebem a transmissão ao vivo de múltiplas taxas de bits de codificadores locais (passagem)

Olá diagrama a seguir mostra Olá partes principais da plataforma Olá AMS envolvidos no hello **passagem** fluxo de trabalho.

![Fluxo de trabalho ao vivo](./media/scenarios-and-availability/media-services-live-streaming-current.png)

Para obter mais informações, consulte [Trabalhando com Canais que Recebem a Transmissão ao Vivo de Múltiplas Taxas de Bits de Codificadores Locais](media-services-live-streaming-with-onprem-encoders.md).

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Trabalhando com canais que são habilitados tooperform ao vivo de codificação com os serviços de mídia do Azure

Olá diagrama a seguir mostra Olá principais partes da plataforma de AMS Olá que estão envolvidos no fluxo de trabalho de transmissão ao vivo em que um canal é habilitado tooperform ao vivo de codificação com os serviços de mídia.

![Fluxo de trabalho ao vivo](./media/scenarios-and-availability/media-services-live-streaming-new.png)

Para obter mais informações, consulte [trabalhando com canais que é habilitado tooPerform Live codificação com o Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Para obter informações sobre a disponibilidade em data centers, consulte Olá [disponibilidade](#availability) seção.

## <a name="consuming-content"></a>Consumo de conteúdo

O Azure Media Services fornece ferramentas Olá necessário toocreate avançada, aplicativos de player de cliente dinâmicos para a maioria das plataformas, incluindo: dispositivos iOS, dispositivos Android, Windows, Windows Phone, Xbox e superior do conjunto de caixas. Olá tópico a seguir fornece links tooSDKs e estruturas de Player que você pode usar toodevelop seus próprios aplicativos de cliente que podem consumir mídia de streaming dos serviços de mídia. Para obter mais informações, consulte [Desenvolvendo aplicativos do cliente de vídeo](media-services-develop-video-players.md)

## <a name="enabling-azure-cdn"></a>Habilitando o CDN do Azure

Os Serviços de Mídia dão suporte à integração com o CDN do Azure. Para obter informações sobre como tooenable CDN do Azure, consulte [como tooManage pontos de extremidade de Streaming em uma conta do Media Services](media-services-portal-manage-streaming-endpoints.md).

## <a id="scaling"></a>Dimensionando uma conta dos Serviços de Mídia

Os clientes AMS podem dimensionar os pontos de extremidade do streaming, processamento de mídia e armazenamento em suas contas AMS.

* Os clientes dos Serviços de Mídia podem escolher um ponto de extremidade de streaming **Standard** ou do streaming **Premium**. Um ponto de extremidade de streaming **Standard** é adequado para a maior parte das cargas de trabalho do streaming. Ele inclui Olá mesmos recursos como um **Premium** automaticamente os pontos de extremidade e escalas de largura de banda de saída de streaming. 

    Os pontos de extremidade do streaming **Premium** são adequados para as cargas de trabalho avançadas, fornecendo uma capacidade de largura de banda dimensionável e dedicada. Os clientes que têm um ponto de extremidade de streaming **Premium**, por padrão, obtêm uma US (Unidade de Streaming). saudação de ponto de extremidade de streaming pode ser dimensionada adicionando SUs. Cada SU fornece capacidade de largura de banda adicional toohello de aplicativo. Para obter mais informações sobre como dimensionar **Premium** pontos de extremidade de streaming, consulte Olá [dimensionamento pontos de extremidade de streaming](media-services-portal-scale-streaming-endpoints.md) tópico.

* Uma conta de serviços de mídia está associada um tipo de unidade reservada, que determina a velocidade de saudação com a qual a mídia de processamento de tarefas é processada. Você pode escolher entre os seguintes Olá reservado tipos de unidade: **S1**, **S2**, ou **S3**. Por exemplo, Olá mesmo trabalho de codificação é executada mais rapidamente ao usar o hello **S2** tipo de unidade reservada comparar toohello **S1** tipo.

    Além disso, toospecifying Olá reservado tipo de unidade, você pode especificar tooprovision sua conta com **unidades reservadas** (RUs). número de saudação de RUs provisionados determina o número de saudação de tarefas de mídia que podem ser processadas simultaneamente em uma conta.

    >[!NOTE]
    >As URs trabalham para paralelizar todo o processamento de mídia, incluindo os trabalhos de indexação, usando o Azure Media Indexer. No entanto, ao contrário da codificação, a indexação de trabalhos não será processada mais rapidamente com unidades reservadas mais rápidas.

    Para obter mais informações, consulte [Processamento de mídia de escala](media-services-portal-scale-media-processing.md).
* Você também pode dimensionar sua conta do Media Services adicionando tooit de contas de armazenamento. Cada conta de armazenamento é limitado too500 TB. tooexpand o armazenamento além de limitações do saudação padrão, você pode escolher tooattach várias contas tooa único Media Services conta de armazenamento. Para saber mais, consulte [Gerenciar contas de armazenamento](meda-services-managing-multiple-storage-accounts.md).

##<a id="availability"></a>Disponibilidade de recursos dos Serviços de Mídia nos datacenters

Esta seção fornece detalhes sobre a disponibilidade de recursos dos Serviços de Mídia nos datacenters.

### <a name="ams-accounts"></a>Contas AMS

#### <a name="availability"></a>Disponibilidade

Você pode criar contas de serviços de mídia no hello seguintes regiões: norte da Europa, Europa Ocidental, oeste dos EUA, Leste dos EUA, Sudeste da Ásia, Ásia Oriental, oeste do Japão, Leste do Japão, Sul do Brasil, Índia Oeste, Sul da Índia e Índia Central. 

### <a name="streaming-endpoints"></a>Pontos de extremidade de streaming 

Os clientes dos Serviços de Mídia podem escolher um ponto de extremidade de streaming **Standard** ou do streaming **Premium**. Para obter mais informações, consulte Olá [dimensionamento](#scaling) seção.

#### <a name="availability"></a>Disponibilidade

|Nome|Status|Datacenters
|---|---|---|
|Standard|GA|Todos|
|Premium|GA|Todos|

### <a name="live-encoding"></a>Codificação ativa

#### <a name="availability"></a>Disponibilidade

Disponível em todos os datacenters, exceto: Alemanha, sul do Brasil, Índia Ocidental, sul da Índia e Índia Central. 

### <a name="encoding-media-processors"></a>Codificando processadores de mídia

A AMS oferece dois codificadores de sob demanda **Media Encoder Standard** e **Fluxo de Trabalho do Media Encoder Premium**. Para obter mais informações, consulte [Visão geral e comparação dos codificadores de mídia sob demanda do Azure](media-services-encode-asset.md). 

#### <a name="availability"></a>Disponibilidade

|Nome do processador de mídia|Status|Datacenters
|---|---|---|
|Media Encoder Standard|GA|Todos|
|Fluxo de trabalho do Media Encoder Premium|GA|Todos, exceto China|

### <a name="analytics-media-processors"></a>Processadores de mídia da Análise

Análise de mídia é uma coleção de componentes de fala e visão que torna mais fácil para as organizações e empresas tooderive de informações práticas de seus arquivos de vídeo. Para saber mais, confira [Visão geral a Análise dos Serviços de Mídia do Azure](media-services-analytics-overview.md).

#### <a name="availability"></a>Disponibilidade

|Nome do processador de mídia|Status|Datacenters
|---|---|---|
|Detector de Rostos em Mídias do Azure|Visualização|Todos|
|Azure Media Hyperlapse|Visualização|Todos|
|Indexador de Mídia do Azure|GA|Todos|
|Detector de Movimento em Mídias do Azure|Visualização|Todos|
|OCR de Mídia do Azure|Visualização|Todos|
|Azure Media Redactor|Visualização|Todos|
|Azure Media Stabilizer|Visualização|Todos|
|Miniaturas de Vídeo de Mídia do Azure|Visualização|Todos|
|Azure Media Indexer 2|Visualização|Todos, exceto regiões da China e do Governo Federal|

### <a name="protection"></a>Proteção

Serviços de mídia do Microsoft Azure permite que você toosecure sua mídia do tempo de saudação deixa o computador por meio de armazenamento, processamento e entrega. Para obter mais informações, consulte [Protegendo o conteúdo AMS](media-services-content-protection-overview.md).

#### <a name="availability"></a>Disponibilidade

|Criptografia|Status|Datacenters|
|---|---|---| 
|Armazenamento|GA|Todos|
|Chaves AES-128|GA|Todos|
|FairPlay|GA|Todos|
|PlayReady|GA|Todos|
|Widevine|GA|Todos, exceto Alemanha, Governo Federal e China.

### <a name="reserved-units-rus"></a>Unidades Reservadas (URs)

número de saudação de unidades reservadas provisionadas determina o número de saudação de tarefas de mídia que podem ser processadas simultaneamente em uma determinada conta. 

Para obter mais informações, consulte Olá [dimensionamento](#scaling) seção.

#### <a name="availability"></a>Disponibilidade

Disponível em todos os datacenters.

### <a name="reserved-unit-ru-type"></a>Tipo de unidade reservada (UR)

Uma conta de serviços de mídia está associada um tipo de unidade reservada, que determina a velocidade de saudação com a qual a mídia de processamento de tarefas é processada. Você pode escolher entre os seguintes Olá reservado tipos de unidade: S1, S2 ou S3.

Para obter mais informações, consulte Olá [dimensionamento](#scaling) seção.

#### <a name="availability"></a>Disponibilidade

|Nome do tipo de UR|Status|Datacenters
|---|---|---|
|S1|GA|Todos|
|S2|GA|Todos, exceto sul do Brasil e Índia Ocidental|
|S3|GA|Todos, exceto Índia Ocidental|

## <a name="next-steps"></a>Próximas etapas

Examine os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

