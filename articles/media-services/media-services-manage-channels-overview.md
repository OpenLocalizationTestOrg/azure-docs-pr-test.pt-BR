---
title: "aaaOverview de transmissão ao vivo usando os serviços de mídia do Azure | Microsoft Docs"
description: "Este tópico fornece uma visão geral da transmissão ao vivo usando os Serviços de Mídia do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fb63502e-914d-4c1f-853c-4a7831bb08e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: edc49069db6b491902bdcbb808b1974858cc92f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-live-streaming-using-azure-media-services"></a>Visão geral da transmissão ao vivo usando os Serviços de Mídia do Azure
## <a name="overview"></a>Visão geral
Durante a entrega ao vivo streaming eventos com os serviços de mídia do Azure Olá componentes a seguir normalmente envolvida:

* Uma câmera é usada toobroadcast um evento.
* Um codificador de vídeo ao vivo que converte sinais da saudação câmera toostreams enviadas tooa serviço de streaming em tempo real.

    Opcionalmente, vários codificadores sincronizados em tempo real. Para certos eventos importantes ao vivo que demanda muito alta disponibilidade e experiência de qualidade, recomenda-se tooemploy os codificadores redundantes ativo-ativo com tempo sincronização tooachieve failover contínuo sem perda de dados.
* Um serviço de transmissão ao vivo que permite que você toodo Olá a seguir:

  * inclusão de conteúdo ao vivo usando diversos protocolos de transmissão ao vivo (por exemplo RTMP ou Smooth Streaming),
  * (opcionalmente) codificação de seu fluxo no fluxo de taxa de bits adaptável
  * visualização de sua transmissão ao vivo,
  * Registro e o repositório de conteúdo de saudação incluído na ordem toobe transmitido posterior (vídeo sob demanda)
  * entregar conteúdo Olá por meio de protocolos de transmissão comuns (por exemplo, MPEG DASH, Smooth, HLS) diretamente tooyour clientes ou tooa rede de fornecimento de conteúdo (CDN) para melhor distribuição.

**Serviços de mídia do Microsoft Azure** (AMS) fornece Olá tooingest de capacidade, codificar, visualizar, armazenar e entregar o conteúdo de streaming ao vivo.

Ao entregar seu conteúdo toocustomers sua meta é toodeliver dispositivos de vídeo toovarious de alta qualidade em condições de rede diferente. tooachieve isso, use live codificadores tooencode seu fluxo de vídeo de taxa de bits múltipla (taxa de bits adaptável) do fluxo tooa.  tootake respeito streaming em dispositivos diferentes, use os serviços de mídia [empacotamento dinâmico](media-services-dynamic-packaging-overview.md) toodynamically novamente os protocolos de toodifferent de fluxo do pacote. Serviços de mídia oferece suporte à entrega de saudação seguintes tecnologias de streaming de taxa de bits adaptável: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.

Nos serviços de mídia do Azure, **canais**, **programas**, e **StreamingEndpoints** identificador Olá todos live streaming funcionalidades, inclusive ingestão, formatação, DVR, segurança, escalabilidade e redundância.

Um **Canal** representa um pipeline para o processamento de conteúdo de transmissão ao vivo. Um canal pode receber um dinâmica entrada fluxos Olá maneiras a seguir:

* Um codificador ao vivo no local envia várias taxas de bits **RTMP** ou **Smooth Streaming** (MP4 fragmentado) toohello Channel configurado para **passagem** entrega. Olá **passagem** entrega é quando fluxos Olá incluído passam **Channel**s sem nenhum processamento adicional. Você pode usar o hello codificadores ao vivo que geram várias taxas de bits Smooth Streaming a seguir: MediaExcel, Ateme, Imagine comunicações, Envivio, Cisco e Elemental. Olá, seguintes codificadores dinâmicos saída RTMP: transcodificadores certificação Adobe Flash Media ao vivo codificador (FMLE), Telestream Wirecast, Haivision, Teradek e Tricaster.  Um codificador ao vivo também pode enviar um canal de tooa no fluxo de taxa de bits única que não está habilitado para codificação ao vivo, mas que não é recomendado. Quando solicitado, os serviços de mídia oferece Olá fluxo toocustomers.

  > [!NOTE]
  > Usando um método de passagem é a maneira de mais econômica Olá toodo transmissão ao vivo quando você estiver fazendo vários eventos durante um longo período de tempo, e você já investiram nos codificadores de local. Veja os detalhes de [preços](https://azure.microsoft.com/pricing/details/media-services/) .
  > 
  > 
* Um codificador ao vivo no local envia um fluxo de taxa de bits única canal toohello que é habilitado tooperform live codificação com os serviços de mídia em um dos formatos a seguir de saudação: RTMP ou Smooth Streaming (MP4 fragmentado). RTP (MPEG-TS) também é suportado, desde que você tenha um conexão dedicada toohello data center do Azure. Olá codificadores ao vivo com RTMP a seguir são conhecidos toowork com canais desse tipo de saída: Telestream Wirecast, FMLE. Olá Channel, em seguida, executa a codificação ao vivo de entrada de saudação taxa de bits única fluxo tooa várias taxas de bits (adaptável) fluxo de vídeo. Quando solicitado, os serviços de mídia oferece Olá fluxo toocustomers.

Começando com versão Olá 2.10 de serviços de mídia, quando você cria um canal, você pode especificar em qual modo você deseja para seu fluxo de entrada do canal tooreceive hello e se deseja ou não para Olá canal tooperform live codificação de sua transmissão. Você tem duas opções:

* **Nenhum** (passagem) – Especifique esse valor, se você planejar toouse um codificador ao vivo no local, que resultará em fluxo de múltiplas taxas de bits (um fluxo de passagem). Nesse caso, o fluxo de entrada hello passado toohello sem nenhuma codificação de saída. Esse é o comportamento de saudação de uma versão anterior too2.10 de canal.  
* **Padrão** – escolha esse valor, se você planejar toouse serviços de mídia tooencode seu fluxo de toomulti taxas de bits de transmissão ao vivo de taxa de bits única. Esse método é mais econômico para escalar verticalmente de forma rápida para eventos incomuns. Lembre-se de que há um impacto de cobrança para codificação ao vivo e você deve se lembrar que deixar um canal de codificação ao vivo em estado de "Running" hello incorrerão em cobranças.  É recomendável que você interrompa imediatamente seus canais em execução após o evento de transmissão ao vivo é concluída tooavoid encargos adicionais por hora.

## <a name="comparison-of-channel-types"></a>Comparação dos tipos de canais
Tabela a seguir fornece um guia de toocomparing Olá dois tipos de canal com suporte nos serviços de mídia

| Recurso | Canal de passagem | Canal padrão |
| --- | --- | --- |
| Taxa de bits única entrada é codificada em várias taxas de bits na nuvem Olá |Não |Sim |
| Resolução máxima, número de camadas |1080p, 8 camadas, 60+fps |720p, 6 camadas, 30 fps |
| Protocolos de entrada |RTMP, Smooth Streaming |RTMP, Smooth Streaming e RTP |
| Preço |Consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/media-services/) e clique na guia "Vídeo ao vivo" |Consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/media-services/) |
| Tempo de execução máximo |24x7 |8 horas |
| Suporte para inserção de imagens fixas |Não |Sim |
| Suporte para sinalização de anúncios |Não |Sim |
| Legendas CEA 608/708 de passagem |Sim |Sim |
| Toorecover de capacidade de breves interrupções no feed de contribuição |Sim |Não (O canal começará a exibir imagens fixas após um período superior a 6 segundos sem dados de entrada) |
| Suporte para GOPs de entrada não uniforme |Sim |Não – a entrada deve ser GOPs de 2 s fixos |
| Suporte para entrada de taxa de quadros variável |Sim |Não – a entrada deve ser uma taxa de quadros fixa.<br/>Pequenas variações são toleradas, por exemplo, durante cenas ricas em movimento. Mas o codificador não é possível descartar too10 quadros por segundo. |
| Desligamento automático de Canais quando há perda do feed de entrada |Não |Após 12 horas, se não houver nenhum Programa em execução |

## <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Trabalhando com canais que recebem a transmissão ao vivo de taxa de bits múltipla de codificadores locais (passagem)
Olá diagrama a seguir mostra Olá partes principais da plataforma Olá AMS envolvidos no hello **passagem** fluxo de trabalho.

![Fluxo de trabalho ao vivo](./media/media-services-live-streaming-workflow/media-services-live-streaming-current.png)

Para obter mais informações, consulte [Trabalhando com Canais que Recebem a Transmissão ao Vivo de Múltiplas Taxas de Bits de Codificadores Locais](media-services-live-streaming-with-onprem-encoders.md).

## <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Trabalhando com canais que são habilitados tooperform ao vivo de codificação com os serviços de mídia do Azure
Olá diagrama a seguir mostra Olá principais partes da plataforma de AMS Olá que estão envolvidos no fluxo de trabalho de transmissão ao vivo em que um canal é habilitado tooperform ao vivo de codificação com os serviços de mídia.

![Fluxo de trabalho ao vivo](./media/media-services-live-streaming-workflow/media-services-live-streaming-new.png)

Para obter mais informações, consulte [trabalhando com canais que é habilitado tooPerform Live codificação com o Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

## <a name="description-of-a-channel-and-its-related-components"></a>Descrição de um Canal e seus componentes relacionados
### <a name="channel"></a>Canal
Nos Serviços de Mídia, [Canais](https://docs.microsoft.com/rest/api/media/operations/channel)são responsáveis pelo processamento de conteúdo de transmissão ao vivo. Um canal fornece um ponto de extremidade de entrada (URL de ingestão) que você forneça transcodificador ao vivo tooa. canal de saudação recebe fluxos ao vivo de entrada do transcodificador ao vivo hello e disponibiliza para transmissão através de um ou mais StreamingEndpoints. Os canais também oferecem uma empresa de visualização (URL de visualização) que você use toopreview e valida sua transmissão antes de processamento e entrega.

Você pode obter Olá ingestão URL e a URL de visualização hello quando você criar o canal de saudação. tooget essas URLs, Olá canal não ter toobe em estado Olá iniciado. Quando você estiver pronto toostart enviar dados de um transcodificador ao vivo no canal hello, canal Olá deve ser iniciado. Depois que o transcodificador ao vivo Olá inicia a ingestão de dados, você pode visualizar o fluxo.

Cada conta dos Serviços de Mídia pode conter vários canais, vários programas e vários StreamingEndpoints. Dependendo das necessidades de largura de banda e segurança hello, serviços de StreamingEndpoint podem ser tooone dedicado ou mais canais. Qualquer StreamingEndpoint pode executar pull de qualquer canal.

### <a name="program"></a>Programa
Um [programa](https://docs.microsoft.com/rest/api/media/operations/program) permite a publicação de saudação toocontrol e armazenamento de segmentos em uma transmissão ao vivo. Canais gerenciam programas. Olá relação de canal e programa é uma mídia tootraditional muito semelhantes em que um canal tem um fluxo constante de conteúdo e um programa está no escopo toosome atingiu o tempo de evento naquele canal.
Você pode especificar o número de saudação horas deseja tooretain Olá registrada conteúdo para programa hello por configuração Olá **ArchiveWindowLength** propriedade. Esse valor pode ser definido no mínimo 5 minutos tooa máximo 25 horas.

ArchiveWindowLength também determina o período de tempo que os clientes podem procurar de volta no tempo da posição atual ao vivo da saudação máximo hello. Programas podem ser executados pelo período de tempo especificado hello, mas o conteúdo que sai da duração da janela de saudação é continuamente descartado. Esse valor dessa propriedade também determina quanto tempo cliente Olá manifestos podem crescer.

Cada programa está associado um ativo. programa de saudação toopublish você deve criar um localizador para Olá associados ativo. Ter esse localizador permitirá que você toobuild uma URL de streaming que pode fornecer tooyour clientes.

Um canal dá suporte para até toothree simultaneamente programas em execução para que você pode criar diversos arquivos de saudação mesmo fluxo de entrada. Isso permite que você toopublish e arquivamento diferentes partes de um evento, conforme necessário. Por exemplo, o requisito de negócios é tooarchive 6 horas de um programa, mas toobroadcast apenas últimos 10 minutos. tooaccomplish isso, você precisa toocreate dois programas em execução simultaneamente. Um programa está definido tooarchive 6 horas do evento Olá mas Olá programa não será publicado. Olá outro programa é tooarchive conjunto por 10 minutos e esse programa é publicado.

## <a name="billing-implications"></a>Implicações de cobrança
Um canal começa assim que seu estado faz a transição "Running" muito via Olá API de cobrança.  

Olá tabela a seguir mostra como os estados de canal mapeiam estados toobilling Olá API e portal do Azure. Observe que Olá estados são ligeiramente diferentes entre hello API e UX Portal. Assim que um canal está no estado "Em execução" hello via API de hello, ou em hello "Pronta" ou "Streaming" estado Olá portal do Azure, a cobrança será ativa.

Canal de saudação toostop de cobrança é ainda mais, você tem tooStop Olá canal por meio da API de saudação ou em Olá portal do Azure.
Você é responsável por parar seus canais quando terminar o canal de saudação. Canal de saudação toostop falha resultará na cobrança contínua.

> [!NOTE]
> Ao trabalhar com canais padrão, AMS serão automaticamente desligamento por qualquer canal que ainda está em estado "Em execução" 12 horas depois de feed de entrada hello é perdido e não existem programas em execução. No entanto, você ainda será cobrado para Olá Olá de tempo que canal estava no estado "Em execução".
>
>

### <a id="states"></a>Estados de canal e como eles serão mapeados toohello modo de cobrança
estado atual de saudação de um canal. Os valores possíveis incluem:

* **Parado**. Esse é o estado inicial de saudação do hello canal após sua criação (a menos que o autostart foi selecionado no portal de hello.) Não há cobrança nesse estado. Nesse estado, propriedades do canal Olá podem ser atualizadas, mas não é permitido fazer streaming.
* **Iniciando**. Olá canal está sendo iniciado. Não há cobrança nesse estado. Nenhuma atualização ou streaming é permitido durante esse estado. Se ocorrer um erro, Olá canal retorna toohello estado parado.
* **Executando**. Olá canal é capaz de processar transmissões ao vivo. Agora o uso está sendo cobrado. Você deve parar Olá canal tooprevent adicional de cobrança.
* **Parando**. Olá canal está sendo interrompida. Não haverá cobrança nesse estado transitório. Nenhuma atualização ou streaming é permitido durante esse estado.
* **Excluindo**. Olá canal está sendo excluído. Não haverá cobrança nesse estado transitório. Nenhuma atualização ou streaming é permitido durante esse estado.

Olá tabela a seguir mostra como os estados de canal de modo de cobrança de toohello do mapa.

| Estado de canal | Indicadores da interface do usuário do portal | Trata-se de cobrança? |
| --- | --- | --- |
| Iniciando |Iniciando |Nenhum (estado transitório) |
| Executando |Pronto (nenhum programa em execução)<br/>ou o<br/>Streaming (pelo menos um programa em execução) |SIM |
| Parando |Parando |Nenhum (estado transitório) |
| Parado |Parado |Não |

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Tópicos relacionados
[Especificação de ingestão dinâmica de MP4 fragmentado dos Serviços de Mídia do Azure](media-services-fmp4-live-ingest-overview.md)

[Trabalhando com canais que é habilitado tooPerform Live codificação com os serviços de mídia do Azure](media-services-manage-live-encoder-enabled-channels.md)

[Trabalhando com Canais que recebam transmissão ao vivo de múltiplas taxas de bits de codificadores locais](media-services-live-streaming-with-onprem-encoders.md)

[Cotas e limitações](media-services-quotas-and-limitations.md).  

[Conceitos de Serviços de Mídia](media-services-concepts.md)
