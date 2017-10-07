---
title: "aaaStream ao vivo com codificadores locais que criam fluxos de várias taxas de bits - Azure | Microsoft Docs"
description: "Este tópico descreve como tooset um canal que recebe uma taxa de bits múltipla o fluxo ao vivo de um codificador de local. Olá fluxo pode ser entregue aplicativos de reprodução de tooclient por meio de um ou mais pontos de extremidade streaming, usando um dos seguintes protocolos de streaming adaptáveis de saudação: HLS, Smooth Streaming, DASH."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: d9f0912d-39ec-4c9c-817b-e5d9fcf1f7ea
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 04/12/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 00709cecfc3b5b5dcfaa8f1e4b25bcf9d470d50b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-with-on-premises-encoders-that-create-multi-bitrate-streams"></a>Transmissão ao vivo com codificadores locais que criam fluxos com múltiplas taxas de bits
## <a name="overview"></a>Visão geral
Nos Serviços de Mídia do Azure, um *Canal* representa um pipeline para processamento de conteúdo de streaming ao vivo. Um canal recebe fluxos de entrada ao vivo de uma das duas maneiras a seguir:

* Um codificador ao vivo no local envia um RTMP de taxa de bits múltipla ou Smooth Streaming (MP4 fragmentado) fluxo toohello canal que não é habilitado tooperform live codificação com os serviços de mídia. Olá incluídos fluxos passagem por meio de canais sem nenhum processamento adicional. Esse método é chamado *passagem*. Você pode usar o hello codificadores ao vivo com várias taxas de bits Smooth Streaming como saída a seguir: Excel de mídia, Ateme, Imagine comunicações, Envivio, Cisco e Elemental. Olá codificadores ao vivo a seguir têm RTMP como saída: Adobe Flash Live codificador de mídia, Telestream Wirecast, Haivision, Teradek e TriCaster. Um codificador ao vivo também pode enviar um canal de tooa de fluxo de taxa de bits única que não está habilitado para codificação ao vivo, mas não é recomendável que. Serviços de mídia oferece Olá fluxo toocustomers que solicitá-la.

  > [!NOTE]
  > Usando um método de passagem é a maneira de mais econômica Olá toodo live streaming.


* Um codificador ao vivo no local envia um canal de toohello de fluxo de taxa de bits única que é habilitada ao vivo de codificação com os serviços de mídia em um dos formatos a seguir de saudação do tooperform: RTP (MPEG-TS), RTMP ou Smooth Streaming (MP4 fragmentado). canal Hello, em seguida, executa a codificação ativa do hello taxas de bits única fluxo tooa várias taxas de bits (adaptável) vídeo fluxo de entrada. Serviços de mídia oferece Olá fluxo toocustomers que solicitá-la.

Começando com versão Olá 2.10 de serviços de mídia, quando você cria um canal, você pode especificar como você deseja que seu fluxo de entrada do canal tooreceive hello. Você também pode especificar se deseja Olá tooperform de canal ao vivo de codificação de seu fluxo. Você tem duas opções:

* **Passar**: especificar esse valor se você planejar toouse um codificador ao vivo no local que terá um fluxo de múltiplas taxas de bits (um fluxo de passagem) como saída. Nesse caso, o fluxo de entrada hello transmite toohello sem nenhuma codificação de saída. Esse é o comportamento de saudação de um canal antes da liberação Olá 2.10. Este tópico fornece detalhes sobre como trabalhar com canais desse tipo.
* **Live codificação**: Escolha esse valor se você planejar toouse serviços de mídia tooencode seu fluxo de múltiplas taxas de bits tooa taxas de bits única transmissão ao vivo. Lembre-se de que deixar um canal de codificação ativa em um estado **Executando** incorrerá em encargos de cobrança. Recomendamos que você interrompa imediatamente seus canais em execução após o evento de transmissão ao vivo é concluída tooavoid encargos adicionais por hora. Serviços de mídia oferece Olá fluxo toocustomers que solicitá-la.

> [!NOTE]
> Este tópico discute os atributos de canais que não estão habilitados tooperform de codificação ao vivo. Para obter informações sobre como trabalhar com canais que são habilitados tooperform de codificação ao vivo, consulte [transmissão ao vivo usando fluxos de várias taxas de bits do Azure Media Services toocreate](media-services-manage-live-encoder-enabled-channels.md).
>
>

Olá diagrama a seguir representa um fluxo de trabalho de transmissão ao vivo usa um fluxos do local codificador ao vivo toohave várias taxas de bits RTMP ou MP4 fragmentado (Smooth Streaming) como saída.

![Fluxo de trabalho ao vivo][live-overview]

## <a id="scenario"></a>Cenário comum de streaming ao vivo
Olá, etapas a seguir descrevem tarefas envolvidas na criação de aplicativos comuns de transmissão ao vivo.

1. Conecte um computador de tooa de câmera de vídeo. Inicie e configure um codificador ativo local que gere um fluxo RTMP com múltiplas taxas de bits ou MP4 fragmentado (Smooth Streaming). Para obter mais informações, consulte [Suporte RTMP dos Serviços de Mídia do Azure e Codificadores ao Vivo](http://go.microsoft.com/fwlink/?LinkId=532824).

    Essa etapa também pode ser realizada após a criação do canal.
2. Crie e inicie um Canal.

3. URL de ingestão do canal de saudação de recuperar.

    Olá Olá do codificador ao vivo usa ingestão canal toohello de fluxo de saudação do URL toosend.
4. Recupere a URL de visualização do canal hello.

    Use este tooverify URL que o canal está recebendo corretamente transmissão ao vivo hello.
5. Crie um programa.

    Quando você usa Olá portal do Azure, criar um programa também cria um ativo.

    Quando você usa Olá SDK .NET ou REST, você precisa toocreate um ativo e especifica toouse este ativo durante a criação de um programa.
6. Publica o ativo de saudação que está associado ao programa hello.   

    >[!NOTE]
    >Quando sua conta de serviços de mídia do Azure é criada, um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. saudação do qual você deseja que o conteúdo de toostream de ponto de extremidade de streaming tem toobe em Olá **executando** estado.

7. Inicie o programa de hello quando você estiver pronto toostart transmissão e o arquivamento.

8. Opcionalmente, o codificador ao vivo Olá pode ser sinalizado toostart um anúncio. anúncio de saudação é inserido no fluxo de saída de hello.

9. Pare o programa de saudação sempre que quiser toostop streaming e arquivamento evento hello.

10. Excluir o programa hello (e opcionalmente exclua o ativo de saudação).     

## <a id="channel"></a>Descrição de um canal e seus componentes relacionados
### <a id="channel_input"></a>Configurações de entrada de canal (ingestão)
#### <a id="ingest_protocols"></a>Protocolo de streaming de ingestão
Os Serviços de Mídia oferecem suporte à ingestão de feeds ao vivo usando MP4 fragmentado de múltipla taxas de bits e RTMP de múltiplas taxas de bits como protocolos de streaming. Quando Olá RTMP de ingestão protocolo de transmissão é selecionado, dois ingestão (entrados) de pontos de extremidade são criados para o canal de saudação:

* **URL primária**: especifica Olá URL totalmente qualificada do RTMP primário do canal de saudação do ponto de extremidade de ingestão.
* **URL secundária** (opcional): especifica Olá URL totalmente qualificada do RTMP secundário do canal de saudação do ponto de extremidade de ingestão.

Use URL secundária Olá tooimprove Olá durabilidade e tolerância a falhas do seu ingestão fluxo (bem como codificador failover e tolerância a falhas), especialmente para Olá os seguintes cenários:

- Codificador único envio por push duplo tooboth URLs de primárias e secundárias:

    Olá principal objetivo desse cenário é tooprovide mais flutuações de toonetwork resiliência e jitters. Alguns codificadores RTMP não tratam bem da desconexão de rede. Quando ocorre uma desconexão da rede, um codificador pode parar a codificação e não enviar dados em buffer de saudação quando ocorre uma reconexão. Isso provoca descontinuidades e perdas de dados. Desconecta de rede pode ocorrer devido a uma rede incorreta ou manutenção em saudação do lado do Azure. URLs primário/secundário reduzem problemas de rede hello e fornecem um processo de atualização controlado. Cada vez que ocorrer uma desconexão da rede agendada, Media Services gerencia Olá primário e secundário desconecta e fornece um atraso desconectar entre hello dois. Os codificadores, em seguida, tem tempo tookeep enviar dados e reconectar-se novamente. ordem de saudação do hello desconecta pode ser aleatório, mas sempre haverá um atraso entre URLs primário/secundário ou primário/secundário. Nesse cenário, codificador Olá ainda é o ponto de falha único hello.

- Vários codificadores, com cada codificador push tooa ponto dedicado:

    Este cenário fornece redundância de codificador e de inclusão. Nesse cenário, encoder1 envia URL primária toohello e encoder2 envia URL secundária toohello. Quando um codificador falha, hello outros codificador possa continuar enviando dados. Redundância de dados pode ser mantida porque os serviços de mídia não desconecta URLs primários e secundários em Olá simultaneamente. Este cenário pressupõe que os codificadores são sincronizado de tempo e fornecem exatamente Olá os mesmos dados.  

- Codificadores várias URLs de tooboth primário e secundário de envio de duplo:

    Nesse cenário, codificadores enviar por push dados tooboth URLs de primários e secundários. Isso fornece tolerância a falhas e confiabilidade melhor hello, bem como a redundância de dados. Este cenário pode tolerar falhas do codificador e desconexões, mesmo se um codificador para de funcionar. Ele pressupõe que os codificadores são sincronizado de tempo e fornecem exatamente Olá os mesmos dados.  

Para obter informações sobre codificadores ao vivo de RTMP, consulte [Suporte a RTMP dos Serviços de Mídia do Azure e codificadores ao vivo](http://go.microsoft.com/fwlink/?LinkId=532824).

#### <a name="ingest-urls-endpoints"></a>URLs de ingestão (pontos de extremidade)
Um canal fornece um ponto de extremidade de entrada (URL de ingestão) que você especificar no codificador ao vivo do hello, para o codificador Olá pode enviar fluxos tooyour canais.   

Você pode obter Olá URLs de ingestão, quando você criar o canal de saudação. Para você tooget essas URLs, canal Olá não tem toobe em Olá **executando** estado. Quando você estiver pronto toostart enviar por push o canal de dados toohello, canal Olá deve estar no hello **executando** estado. Depois que o canal de saudação inicia a ingestão de dados, você pode visualizar o fluxo por meio da URL de visualização de saudação.

Você tem a opção de ingerir uma transmissão ao vivo de MP4 fragmentado (Smooth Streaming) em uma conexão SSL. tooingest por SSL, verifique Olá de tooupdate se tooHTTPS de URL de ingestão. No momento, você não pode ingerir RTMP sobre SSL.

#### <a id="keyframe_interval"></a>Intervalo de quadro-chave
Quando você estiver usando um fluxo de múltiplas taxas de bits de toogenerate de codificador ao vivo no local, o intervalo de quadro-chave de saudação especifica a duração de saudação do grupo de saudação de imagens (GOP) conforme usado por esse codificador externo. Depois que o canal de saudação recebe o fluxo de entrada, você pode fornecer a transmissão ao vivo tooclient aplicativos de reprodução em qualquer um dos formatos a seguir de saudação: Smooth Streaming, Streaming adaptável dinâmico sobre HTTP (traço) e HTTP Live Streaming (HLS). Ao fazer streaming ao vivo, o HLS é sempre empacotado dinamicamente. Por padrão, o Media Services calcula automaticamente Olá empacotamento taxa de segmento HLS (fragmento por segmento) com base no intervalo de quadro-chave de saudação que é recebido do codificador dinâmico Olá.

Olá, a tabela a seguir mostra como a duração do segmento Olá é calculada:

| Intervalo de quadro-chave | Taxa de empacotamento de segmento HLS (FragmentsPerSegment) | Exemplo |
| --- | --- | --- |
| Menor que ou igual a too3 segundos |3:1 |Se o KeyFrameInterval (ou GOP) é 2 segundos, taxa de empacotamento de segmento HLS do saudação padrão é 3 too1. Isso cria um segmento HLS de seis segundos. |
| too5 3 segundos |2:1 |Se o KeyFrameInterval (ou GOP) é 4 segundos, a taxa de empacotamento de segmento de HLS de padrão de saudação é too1 2. Isso cria um segmento HLS de oito segundos. |
| Maior do que cinco segundos |1:1 |Se o KeyFrameInterval (ou GOP) tiver 6 segundos, a taxa de empacotamento de segmento de HLS de padrão de saudação é 1 too1. Isso cria um segmento HLS de seis segundos. |

Você pode alterar a taxa de fragmentos por segmento Olá configurar canal Olá saída e configuração FragmentsPerSegment em ChannelOutputHls.

Você também pode alterar o valor de intervalo de quadro-chave Olá definindo Olá KeyFrameInterval propriedade ChanneInput. Se você definir explicitamente o KeyFrameInterval, taxa de empacotamento de segmento HLS Olá FragmentsPerSegment é calculada por meio de regras de saudação descritas anteriormente.  

Se você definir explicitamente KeyFrameInterval e FragmentsPerSegment, os serviços de mídia usará valores hello que você definiu.

#### <a name="allowed-ip-addresses"></a>Endereços IP permitidos
Você pode definir os endereços IP hello permitidos toopublish toothis vídeo canal. Um endereço IP permitido pode ser especificado como um dos seguintes hello:

* Um único endereço IP (por exemplo, 10.0.0.1)
* Um intervalo de IPs que usa um endereço IP e uma máscara de sub-rede CIDR (por exemplo, 10.0.0.1/22)
* Um intervalo de IPs que usa um endereço IP e uma máscara de sub-rede de valor decimal (por exemplo, 10.0.0.1(255.255.252.0))

Se nenhum endereço IP for especificado e não houver definição de regra, nenhum endereço IP será permitido. tooallow qualquer endereço IP, crie uma regra e defina 0.0.0.0/0.

### <a name="channel-preview"></a>Visualização de canal
#### <a name="preview-urls"></a>URLs de visualização
Os canais oferecem uma empresa de visualização (URL de visualização) que você use toopreview e valida sua transmissão antes de processamento e entrega.

Você pode obter a URL de visualização de hello quando você criar o canal de saudação. Para você tooget Olá URL do canal de saudação não tem toobe em Olá **executando** estado. Depois que o canal de saudação inicia a ingestão de dados, você pode visualizar o fluxo.

Atualmente, o fluxo de visualização Olá pode ser entregues somente em MP4 fragmentado (Smooth Streaming) formato, independentemente de saudação especificado tipo de entrada. Você pode usar o hello [Smooth Streaming Health Monitor](http://smf.cloudapp.net/healthmonitor) smooth stream do player tootest hello. Você também pode usar um player que tenha hosted em Olá tooview portal do Azure seu fluxo.

#### <a name="allowed-ip-addresses"></a>Endereços IP permitidos
Você pode definir os endereços IP hello que têm permissão de ponto de extremidade de visualização de toohello tooconnect. Se nenhum endereço IP for especificado, qualquer endereço IP será permitido. Um endereço IP permitido pode ser especificado como um dos seguintes hello:

* Um único endereço IP (por exemplo, 10.0.0.1)
* Um intervalo de IPs que usa um endereço IP e uma máscara de sub-rede CIDR (por exemplo, 10.0.0.1/22)
* Um intervalo de IPs que usa um endereço IP e uma máscara de sub-rede de valor decimal (por exemplo, 10.0.0.1(255.255.252.0))

### <a name="channel-output"></a>Saída do canal
Para obter informações sobre o canal de saída, consulte Olá [intervalo de quadro-chave](#keyframe_interval) seção.

### <a name="channel-managed-programs"></a>Programas gerenciados por canal
Um canal é associado com programas que você pode usar a publicação Olá toocontrol e armazenamento de segmentos em uma transmissão ao vivo. Canais gerenciam programas. Olá, relação de canal e programa é muito semelhante mídia tootraditional, onde um canal tem um fluxo constante de conteúdo e um programa está no escopo toosome atingiu o tempo de evento naquele canal.

Você pode especificar o número de saudação horas deseja tooretain Olá registrada conteúdo para programa hello por configuração Olá **janela de arquivo** comprimento. Esse valor pode ser definido no mínimo 5 minutos tooa máximo 25 horas. Duração da janela de arquivo também determina o período de tempo que os clientes podem procurar de volta no tempo da posição atual ao vivo da saudação máximo hello. Programas podem ser executados pelo período de tempo especificado hello, mas o conteúdo que sai da duração da janela de saudação é continuamente descartado. Esse valor dessa propriedade também determina quanto tempo cliente Olá manifestos podem crescer.

Cada programa está associado um ativo que armazena o conteúdo de streaming de saudação. Um ativo é um contêiner de blob de bloco tooa mapeada na conta de armazenamento do Azure hello e arquivos Olá no ativo de saudação são armazenados como blobs no contêiner. toopublish programa Olá para que seus clientes possam ver o fluxo hello, você deve criar um localizador OnDemand para ativo Olá associado. Você pode usar esse localizador toobuild uma URL de streaming que pode fornecer tooyour clientes.

Um canal dá suporte para até toothree simultaneamente programas em execução, para que você pode criar diversos arquivos de saudação mesmo fluxo de entrada. Publique e arquive diferentes partes de um evento, conforme necessário. Por exemplo, imagine que o requisito de negócios é tooarchive 6 horas de um programa, mas Olá somente toobroadcast últimos 10 minutos. tooaccomplish isso, você precisa toocreate dois programas em execução simultaneamente. Um programa está definido tooarchive 6 horas do evento hello, mas Olá programa não será publicado. Olá outro programa é tooarchive conjunto por 10 minutos, e esse programa é publicado.

Você não deve reutilizar os programas existentes para novos eventos. Em vez disso, crie um novo programa para cada evento. Inicie o programa de hello quando você estiver pronto toostart transmissão e o arquivamento. Pare o programa de saudação sempre que quiser toostop streaming e arquivamento evento hello.

conteúdo toodelete arquivado, pare e excluir o programa hello e exclua ativo associado hello. Um ativo não pode ser excluído se um programa o utilizar. programa Hello deve ser excluído primeiro.

Mesmo depois de parar e excluir o programa hello, os usuários podem transmitir seu conteúdo arquivado como um vídeo sob demanda, até que você excluir Olá ativo. Se você deseja tooretain Olá arquivado conteúdo, mas ainda não disponível para streaming, exclua Olá localizador de streaming.

## <a id="states"></a>Estados de canal e cobrança
Os valores possíveis para o estado atual de um canal de Olá incluem:

* **Interrompido**: esse é o estado inicial de saudação do canal de saudação após sua criação. Nesse estado, propriedades do canal Olá podem ser atualizadas, mas não é permitido fazer streaming.
* **Iniciando**: canal hello está sendo iniciado. Nenhuma atualização ou streaming é permitido durante esse estado. Se ocorrer um erro, o canal de saudação retorna toohello **parado** estado.
* **Executando**: canal Olá pode processar transmissões ao vivo.
* **Parando**: canal hello está sendo interrompida. Nenhuma atualização ou streaming é permitido durante esse estado.
* **Excluindo**: Olá canal está sendo excluído. Nenhuma atualização ou streaming é permitido durante esse estado.

Olá tabela a seguir mostra como os estados de canal de modo de cobrança de toohello do mapa.

| Estado de canal | Indicadores de interface do usuário do portal | Cobrado? |
| --- | --- | --- | --- |
| **Iniciando** |**Iniciando** |Nenhum (estado transitório) |
| **Executando** |**Pronto** (nenhum programa em execução)<p><p>ou o<p>**Streaming** (há pelo menos um programa em execução) |Sim |
| **Parando** |**Parando** |Nenhum (estado transitório) |
| **Interrompido** |**Interrompido** |Não |

## <a id="cc_and_ads"></a>Legendagem oculta e inserção de anúncios
Olá, a tabela a seguir demonstra padrões com suporte para inserção de anúncios e legenda codificada.

| Standard | Observações |
| --- | --- |
| CEA-708 e EIA-608 (708/608) |CEA-708 e EIA-608 são legenda codificada padrões para Olá EUA e Canadá.<p><p>Atualmente, a legenda tem suporte somente se for realizada no fluxo de entrada codificado hello. É necessário toouse um codificador de mídia ao vivo que pode inserir legendas 608 ou 708 na Olá fluxo codificado que enviou tooMedia serviços. Serviços de mídia oferece conteúdo Olá visualizadores de tooyour legendas inseridas. |
| TTML em ismt (faixas de texto de Smooth Streaming) |Empacotamento dinâmico do Media Services permite que o conteúdo de toostream de clientes em qualquer um dos formatos a seguir de saudação: DASH, HLS ou Smooth Streaming. No entanto, se você incluir MP4 fragmentado (Smooth Streaming) com legendas dentro do. ismt (faixas de texto de Smooth Streaming), você pode entregar Olá fluxo tooonly clientes de Smooth Streaming. |
| SCTE-35 |SCTE-35 é um sistema de sinalização digital que usou a inserção da publicidade toocue. Os receptores downstream usam anúncios de toosplice sinal Olá em fluxo Olá para Olá alocado de tempo. SCTE-35 deve ser enviado como faixa esparsa no fluxo de entrada hello.<p><p>Atualmente, o formato de fluxo de entrada hello só tem suportada que transporta sinais do ad está fragmentado MP4 (Smooth Streaming). formato de saída de Hello só tem suportada também é Smooth Streaming. |

## <a id="considerations"></a>Considerações
Quando você estiver usando um codificador ao vivo de local toosend um canal de tooa de fluxo de múltiplas taxas de bits, Olá restrições a seguir se aplicam:

* Verifique se que tem suficientes livre Internet conectividade toosend dados toohello ingestão pontos.
* O uso de uma URL de ingestão secundária requer largura de banda adicional.
* fluxo de múltiplas taxas de bits de entrada Hello pode ter um máximo de 10 níveis de qualidade de vídeo (camadas) e um máximo de 5 faixas de áudio.
* Olá mais alta taxa de bits média para qualquer um dos níveis de qualidade de vídeo Olá deve ter menos de 10 Mbps.
* Olá agregado de taxas de bits médio para todos os fluxos de áudio e vídeo Olá Olá deve estar abaixo de 25 Mbps.
* Você não pode alterar o protocolo de entrada hello ao canal de saudação ou seus programas associados são executados. Se você precisar de protocolos diferentes, você deve criar canais separados para cada protocolo de entrada.
* Você pode ingerir uma taxa de bits única em seu canal. Mas como canal Olá não processar o fluxo Olá, aplicativos de cliente Olá também receberá um fluxo de taxa de bits única. (Não recomendamos essa opção.)

Eis outro tooworking de considerações relacionadas com canais e componentes relacionados:

* Sempre que você reconfigurar o codificador ao vivo hello, chame Olá **redefinir** método no canal de saudação. Antes de redefinir o canal de saudação, você tem o programa de saudação do toostop. Depois de redefinir o canal de saudação, reinicie o programa de saudação.
* Um canal pode ser interrompido somente quando ele está em Olá **executando** estado e todos os programas no canal de saudação foi interrompidos.
* Por padrão, você pode adicionar a conta de serviços de mídia tooyour apenas 5 canais. Para saber mais, consulte [Cotas e limitações](media-services-quotas-and-limitations.md).
* Você será cobrado somente quando o seu canal estiver no hello **executando** estado. Para obter mais informações, consulte toohello [Channel estados e cobrança](media-services-live-streaming-with-onprem-encoders.md#states) seção.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="feedback"></a>Comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Tópicos relacionados
[Especificação de ingestão dinâmica de MP4 fragmentado dos Serviços de Mídia do Azure](media-services-fmp4-live-ingest-overview.md)

[Visão geral e cenários comuns do Serviços de Mídia do Azure](media-services-overview.md)

[Conceitos dos Serviços de Mídia](media-services-concepts.md)

[live-overview]: ./media/media-services-manage-channels-overview/media-services-live-streaming-current.png
