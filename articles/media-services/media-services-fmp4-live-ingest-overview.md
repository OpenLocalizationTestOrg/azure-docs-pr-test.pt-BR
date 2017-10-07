---
title: "especificação de ingestão aaaAzure os serviços de mídia ao vivo MP4 fragmentado | Microsoft Docs"
description: "Essa especificação descreve o protocolo de saudação e formato fragmentados com base em MP4 live streaming inclusão para serviços de mídia do Azure. Você pode usar eventos ao vivo do Azure Media Services toostream e transmitir o conteúdo em tempo real usando o Azure como plataforma de nuvem hello. Este documento também aborda as práticas recomendadas para criação de mecanismos robustos de ingestão dinâmica e altamente redundantes."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 43fac263-a5ea-44af-8dd5-cc88e423b4de
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 0c191f8d6c5a595621feaba0e571fb984b666f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-fragmented-mp4-live-ingest-specification"></a>Especificação da ingestão dinâmica de MP4 fragmentado para os Serviços de Mídia do Azure
Essa especificação descreve o protocolo de saudação e formato fragmentados com base em MP4 live streaming inclusão para serviços de mídia do Azure. Serviços de mídia fornecem um serviço de transmissão ao vivo que os clientes podem usar eventos ao vivo toostream e transmitir o conteúdo em tempo real usando o Azure como plataforma de nuvem hello. Este documento também aborda as práticas recomendadas para criação de mecanismos robustos de ingestão dinâmica e altamente redundantes.

## <a name="1-conformance-notation"></a>1. Notação de conformidade
Olá palavras-chave "deve", "não deve," "Exigido", "Deverá", "não deverá", "Deveria", "Não devem,", "Recomendado", "Maio" e "Opcional" deste documento são toobe interpretado como elas são descritas no RFC 2119.

## <a name="2-service-diagram"></a>2. Diagrama de serviço
Olá diagrama a seguir mostra arquitetura de alto nível de saudação do hello ao vivo de serviço nos serviços de mídia de streaming:

1. Um codificador ao vivo envia toochannels ao vivo que são criados e provisionados por meio de saudação SDK do Azure Media Services.
2. Nuvem de canais, programas e pontos de extremidade de streaming no identificador de serviços de mídia Olá todos live streaming funcionalidades, inclusive ingestão, formatação, DVR, segurança, escalabilidade e redundância.
3. Opcionalmente, os clientes podem escolher toodeploy uma camada de rede de fornecimento de conteúdo do Azure entre Olá Olá os pontos de extremidade e de ponto de extremidade de streaming.
4. Fluxo de pontos de extremidade de cliente do hello ponto de extremidade de streaming por meio de protocolos de Streaming adaptável de HTTP. Os exemplos incluem Microsoft Smooth Streaming, Streaming adaptável dinâmico via HTTP (DASH ou MPEG-DASH) e Apple HTTP Live Streaming (HLS).

![fluxo de ingestão][image1]

## <a name="3-bitstream-format--iso-14496-12-fragmented-mp4"></a>3. Formato de fluxo de bits – MP4 fragmentado ISO 14496-12
Hello formato com fio para transmissão ao vivo de ingestão discutido neste documento baseia-se no [ISO-14496-12]. Para ver uma explicação detalhada do formato MP4 fragmentado e das extensões para arquivos de vídeo sob demanda e ingestão de transmissão ao vivo, consulte [[MS-SSTR]](http://msdn.microsoft.com/library/ff469518.aspx).

### <a name="live-ingest-format-definitions"></a>Definições de formato de ingestão ao vivo
Olá lista a seguir descreve formato especial definições que se aplicam toolive ingestão nos serviços de mídia do Azure:

1. Olá **ftyp**, **Live Server manifesto caixa**, e **moov** caixas devem ser enviadas com cada solicitação (HTTP POST). Essas caixas devem ser enviadas no início de saudação do fluxo de saudação e qualquer tempo de codificador Olá deve se reconectar tooresume fluxo de ingestão. Para saber mais, consulte a Seção 6 em [1].
2. A Seção 3.3.2 em [1] define uma caixa opcional chamada **StreamManifestBox** para ingestão dinâmica. Devido a lógica de roteamento de toohello hello Azure do balanceador de carga, usar essa caixa é preterido. caixa de saudação não deve estar presente quando ingestão nos serviços de mídia. Se essa caixa estiver presente, os Serviços de Mídia vão ignorá-la silenciosamente.
3. Olá **TrackFragmentExtendedHeaderBox** caixa definida no 3.2.3.2 em [1] deve estar presente para cada fragmento.
4. Versão 2 do hello **TrackFragmentExtendedHeaderBox** caixa deve ser usado toogenerate segmentos de mídia que têm URLs idênticos em vários data centers. o campo de índice de fragmento Olá é obrigatório para o failover entre data centers de formatos de streaming baseada em índice como Apple HLS e MPEG-DASH baseada em índice. tooenable entre data centers failover, o índice de fragmento de saudação deve ser sincronizado entre vários codificadores e ser aumentado em 1 para cada fragmento de mídia sucessivas, mesmo em reinicializações de codificador ou falhas.
5. Seção 3.3.6 [1] define uma caixa denominada **MovieFragmentRandomAccessBox** (**mfra**) que podem ser enviados no final de saudação do canal de toohello inclusão dinâmica tooindicate final de fluxo (EOS). Vencimento toohello ingestão lógica dos serviços de mídia usando EOS foi preterido e Olá **mfra** caixa para inclusão dinâmica não deve ser enviada. Se enviada, os Serviços de Mídia vão ignorá-la silenciosamente. estado de saudação tooreset de saudação ingestão ponto, é recomendável que você use [redefinir canal](https://docs.microsoft.com/rest/api/media/operations/channel#reset_channels). Também é recomendável que você use [programa parar](https://msdn.microsoft.com/library/azure/dn783463.aspx#stop_programs) tooend uma apresentação e o fluxo.
6. duração de fragmento Olá MP4 deve ser constante, tamanho de saudação tooreduce de manifestos de saudação do cliente. Uma duração de fragmento MP4 constante também melhora a heurística de download do cliente por meio do uso de saudação de marcas de repetição. duração de saudação pode flutuar toocompensate para taxas de quadros não inteiro.
7. duração de fragmento Olá MP4 deve estar entre aproximadamente 2 e 6 segundos.
8. Os carimbos de data/hora e índices do fragmento MP4 (**TrackFragmentExtendedHeaderBox** `fragment_ absolute_ time` e `fragment_index`) DEVEM chegar na ordem crescente. Embora os serviços de mídia seja resiliente tooduplicate fragmentos, ela tem limitada fragmentos de tooreorder de capacidade de acordo com o cronograma de mídia toohello.

## <a name="4-protocol-format--http"></a>4. Formato de protocolo – HTTP
ISO fragmentado MP4 com base em tempo real de ingestão para serviços de mídia usa um padrão demoradas HTTP POST tootransmit codificado mídia dados de solicitação que estão empacotados no serviço de toohello de formato MP4 fragmentado. Cada POSTAGEM HTTP envia uma completa fragmentado bits de MP4 ("fluxo"), a partir do início da saudação com caixas de cabeçalho (**ftyp**, **Live Server manifesto caixa**, e **moov** caixas) e continuar com uma sequência de fragmentos (**moof** e **mdat** caixas). Para obter a sintaxe de URL para solicitação de HTTP POST hello, consulte a seção em 9.2 [1]. Um exemplo de hello URL de POST é: 

    http://customer.channel.mediaservices.windows.net/ingest.isml/streams(720p)

### <a name="requirements"></a>Requisitos
Aqui estão os requisitos detalhados de hello:

1. Olá codificador deve iniciar Olá difusão enviando uma solicitação HTTP POST com vazio Olá "body" (conteúdo comprimento zero) usando a mesma URL de ingestão. Isso pode ajudar o codificador Olá rapidamente detectar se o ponto de extremidade de inclusão dinâmica Olá é válido e se não houver nenhuma autenticação ou outras condições necessárias. Por protocolo HTTP, servidor de saudação não é possível enviar novamente uma resposta HTTP até hello toda solicitação, incluindo o corpo do POST Olá, é recebida. Considerando a natureza de longa execução Olá de um evento ao vivo, sem essa etapa, o codificador de saudação pode não ser capaz de toodetect qualquer erro até que ele termina de enviar todos os dados de saudação.
2. codificador Olá deve tratar erros ou desafios de autenticação devido a (1). Se (1) for bem-sucedido com uma resposta 200, continue.
3. codificador Olá deve iniciar uma nova solicitação de HTTP POST com hello fragmentado MP4 fluxo. carga Olá deve começar com caixas de cabeçalho hello, seguidas de fragmentos. Observe que Olá **ftyp**, **Live Server manifesto caixa**, e **moov** caixas (em ordem) devem ser enviadas com cada solicitação, mesmo que o codificador Olá deve se reconectar porque Olá solicitação anterior foi encerrada toohello anterior final do fluxo de saudação. 
4. codificador Olá deve usar para carregamento de codificação de transferência em partes, porque é impossível toopredict Olá todo comprimento do conteúdo da saudação de evento ao vivo.
5. Quando o evento de saudação é, após o envio de fragmento da última Olá, codificador Olá normalmente deve terminar a sequência de mensagem (a maioria das pilhas de cliente HTTP tratá-la automaticamente) de codificação de transferência de saudação em partes. codificador Olá deve aguardar o código de resposta final Olá serviço tooreturn hello e, em seguida, encerre a conexão hello. 
6. codificador de saudação não deve usar Olá `Events()` substantivo conforme descrito em in 9.2 [1] para inclusão em tempo real em serviços de mídia.
7. Se solicitação de HTTP POST Olá encerra ou horários com extremidade TCP erro toohello anterior do fluxo de saudação codificador Olá deve emitir uma nova solicitação POST usando uma nova conexão e siga Olá requisitos anteriores. Além disso, codificador Olá deve reenviar Olá anterior dois fragmentos de MP4 para cada controle no fluxo de saudação e continuar sem introduzir uma descontinuidade na linha do tempo de mídia hello. Reenviar Olá últimos dois fragmentos de MP4 para cada faixa garante que não há nenhuma perda de dados. Em outras palavras, se um fluxo contém um áudio e uma faixa de vídeo e solicitação POST atual Olá falha, codificador Olá deve se reconectar e reenviar Olá últimos dois fragmentos de faixa de áudio hello, que anteriormente foram enviados com êxito, e Olá últimos dois fragmentos do Olá faixa de vídeo, que foram anteriormente enviado com êxito, tooensure que não há nenhuma perda de dados. codificador Olá deve manter um buffer "forward" de fragmentos de mídia, que reenvia quando ele se reconectar.

## <a name="5-timescale"></a>5. Escala de tempo
[[MS-SSTR] ](https://msdn.microsoft.com/library/ff469518.aspx) descreve o uso de saudação da escala de tempo para **SmoothStreamingMedia** (seção 2.2.2.1), **StreamElement** (seção 2.2.2.3), **StreamFragmentElement**(Seção 2.2.2.6), e **LiveSMIL** (seção 2.2.7.3.1). Se o valor de escala de tempo de saudação não estiver presente, o valor de padrão de saudação usado é 10.000.000 (MHz 10). Embora Olá especificação de formato de Smooth Streaming não bloqueia o uso de outros valores de escala de tempo, a maioria das implementações de codificador usar esse padrão toogenerate de valor (10 MHz) Smooth Streaming ingestão de dados. Vencimento toohello [empacotamento dinâmico do Azure Media](media-services-dynamic-packaging-overview.md) recurso, é recomendável que você use uma escala de tempo KHz 90 para fluxos de vídeo e 44,1 KHz ou 48.1 KHz para fluxos de áudio. Se os valores de escala de tempo diferentes são usados para diferentes fluxos, escala de tempo de nível de fluxo Olá deve ser enviada. Para obter mais informações, consulte [[MS-SSTR]](https://msdn.microsoft.com/library/ff469518.aspx).     

## <a name="6-definition-of-stream"></a>6. Definição de “fluxo”
Fluxo é Olá unidade básica da operação de inclusão dinâmica para compor apresentações ao vivo, tratamento de failover de streaming e cenários de redundância. Fluxo é definido como um único fluxo de bits MP4 fragmentado exclusivo que pode conter uma única faixa ou várias faixas. Uma apresentação ao vivo completa pode conter um ou mais fluxos, dependendo da configuração de saudação do codificadores ao vivo hello. Olá exemplos a seguir ilustra várias opções de como usar fluxos toocompose uma apresentação ao vivo completo.

**Exemplo:** 

Um cliente deseja toocreate uma apresentação de transmissão ao vivo que inclui Olá taxas de bits de áudio/vídeo a seguir:

Vídeo – 3000 kbps, 1500 kbps, 750 kbps

Áudio – 128 kbps

### <a name="option-1-all-tracks-in-one-stream"></a>Opção 1: Todas as faixas em um fluxo
Nessa opção, um único codificador gera todas as faixas de áudio/vídeo e, em seguida, empacota-los em um fluxo de bits MP4 fragmentado. Olá fragmentados MP4 bits é enviado por meio de uma única conexão de HTTP POST. Neste exemplo, há apenas um fluxo para esta apresentação ao vivo.

![Fluxos de uma faixa][image2]

### <a name="option-2-each-track-in-a-separate-stream"></a>Opção 2: Cada faixa em um fluxo separado
Essa opção, codificador Olá coloca uma faixa em cada fragmento MP4 bits e, em seguida, envia todos os fluxos de saudação em conexões de HTTP separadas. Isso pode ser feito com um codificador ou com vários codificadores. inclusão dinâmica Olá vê esta apresentação ao vivo como composto por quatro fluxos.

![Fluxos de faixas separadas][image3]

### <a name="option-3-bundle-audio-track-with-hello-lowest-bitrate-video-track-into-one-stream"></a>Opção 3: Agrupar a faixa de áudio com menor faixa de vídeo de taxa de bits Olá em um fluxo
Essa opção, Prezado cliente escolhe faixa de áudio de saudação do toobundle com a faixa de vídeo de taxa de bits mais baixa Olá em bits de um fragmento MP4 e deixe Olá outras duas faixas de vídeo como fluxos separados. 

![Fluxos com faixas de áudio e vídeo][image4]

### <a name="summary"></a>Resumo
Essa não é uma lista completa de todas as opções possíveis de ingestão para este exemplo. Na verdade, qualquer agrupamento de faixas em fluxos tem suporte da ingestão dinâmica. Os clientes e fornecedores de codificadores podem escolher suas próprias implementações com base na complexidade de engenharia, na capacidade do codificador e nas considerações de failover e redundância. No entanto, na maioria dos casos, há apenas uma faixa de áudio para toda a apresentação ao vivo hello. Portanto, é importante tooensure Olá healthiness de saudação ingestão fluxo que contém a faixa de áudio hello. Esta consideração geralmente resulta em colocar a faixa de áudio Olá em seu próprio fluxo (como opção 2) ou agrupando-lo com a faixa de vídeo de taxa de bits mais baixa hello (como a opção 3). Além disso, para melhor redundância e tolerância a falhas, enviando Olá mesmo faixa de áudio em dois fluxos diferentes (opção 2 com redundância faixas de áudio) ou a faixa de áudio de saudação empacotamento com pelo menos duas das faixas de vídeo Olá taxas de bits menores (opção 3 com áudio agregado sem pelo menos dois fluxos vídeos) altamente recomendado ao vivo para inclusão nos serviços de mídia.

## <a name="7-service-failover"></a>7. Failover de serviço
Fornecido Olá a natureza da transmissão ao vivo, suporte a failover BOM é essencial para garantir a disponibilidade do serviço Olá Olá. Serviços de mídia é projetado toohandle vários tipos de falhas, incluindo erros de rede, erros de servidor e problemas de armazenamento. Quando usado em conjunto com a lógica de failover apropriado do lado do codificador dinâmico Olá, os clientes podem obter um serviço de transmissão ao vivo altamente confiável da nuvem de saudação.

Nesta seção, abordamos os cenários de failover de serviço. Nesse caso, falha de saudação acontece em algum lugar no serviço de saudação e se manifesta como um erro de rede. Aqui estão algumas recomendações para implementação de codificador Olá para lidar com o failover do serviço:

1. Use um tempo limite de 10 segundos para estabelecer a conexão de TCP hello. Se uma conexão de saudação tooestablish tentativa demora mais do que 10 segundos, anular Olá operação e tente novamente. 
2. Use um tempo limite curto para o envio de fragmentos de mensagem de solicitação de saudação HTTP. Se duração de fragmento de MP4 de destino Olá N segundos, use um tempo limite de envio entre N e 2 N segundos; Por exemplo, se a duração de fragmento de MP4 Olá é 6 segundos, use um tempo limite de 6 segundos too12. Se ocorrer uma expiração, redefinição Olá conexão, abra uma nova conexão e retomar fluxo de ingestão em conexão nova hello. 
3. Manter um buffer sem interrupção com hello últimos dois fragmentos para cada faixa com êxito e completamente enviados toohello serviço.  Se solicitação de HTTP POST Olá para um fluxo é encerrada ou expira toohello anterior final do fluxo de hello, abra uma nova conexão e começar outra solicitação HTTP POST, reenviar cabeçalhos de fluxo de saudação, reenviar Olá últimos dois fragmentos para cada faixa e retomar o fluxo de saudação sem introduzindo uma descontinuidade na mídia de saudação da linha do tempo. Isso reduz a chance de saudação de perda de dados.
4. É recomendável que codificador Olá não limitar o número de saudação de novas tentativas tooestablish uma conexão ou retomar o fluxo contínuo após ocorrer um erro TCP.
5. Após um erro TCP:
  
    a. Olá atual conexão deve ser fechado e uma nova conexão deve ser criado para uma nova solicitação de HTTP POST.

    b. Olá novo HTTP POST URL deve ser Olá mesmo Olá URL inicial da publicação.
  
    c. Hello novo HTTP POST deve incluir cabeçalhos de fluxo (**ftyp**, **Live Server manifesto caixa**, e **moov** caixas) que são idênticos toohello cabeçalhos de fluxo em Olá inicial POST.
  
    d. última dois fragmentos de saudação enviados para cada faixa devem ser reenviados e streaming deve continuar sem introduzir uma descontinuidade na mídia de saudação da linha do tempo. Olá MP4 carimbos de hora do fragmento deve aumentar continuamente, mesmo em solicitações HTTP POST.
6. codificador Olá deve encerrar a solicitação de HTTP POST Olá se os dados não estão sendo enviados a uma taxa proporcional com duração de fragmento de MP4 hello.  Uma solicitação HTTP POST que não enviam dados pode impedir que os serviços de mídia rapidamente se desconectar do codificador Olá no evento de saudação de uma atualização de serviço. Por esse motivo, Olá HTTP POST para esparsas rastreia (sinal de anúncio) deve ser curta duração, encerrando como fragmento esparsas Olá é enviado.

## <a name="8-encoder-failover"></a>8. Failover do codificador
Failover de codificador é o segundo tipo de saudação do cenário de failover que precisa toobe endereçado para entrega de streaming ao vivo de ponta a ponta. Nesse cenário, condição de erro Olá ocorre no lado do codificador hello. 

![failover do codificador][image5]

Olá expectativas a seguir se aplicam do ponto de extremidade de inclusão dinâmica hello quando ocorre o failover de codificador:

1. Uma nova instância do codificador deve ser criada toocontinue streaming, conforme ilustrado no diagrama de saudação (fluxo de 3000k vídeo com linha tracejada).
2. codificador de novo Olá deve usar Olá mesmo solicitações de URL de HTTP POST como Olá Falha na instância.
3. Olá POSTAGEM solicitação do codificador nova deve incluir Olá mesmo fragmentado MP4 caixas de cabeçalho como Olá instância com falha.
4. codificador novo Olá deve ser sincronizado corretamente com todos os outros codificadores em execução para o mesmo toogenerate de apresentação ao vivo hello sincronizados exemplos de áudio/vídeo com limites de fragmento alinhado.
5. novo fluxo de saudação deve ser semanticamente equivalente ao fluxo de saudação anterior e intercambiáveis nos níveis de cabeçalho e um fragmento de saudação.
6. codificador novo Olá deve tentar toominimize perda de dados. Olá `fragment_absolute_time` e `fragment_index` da mídia de fragmentos devem aumentar de ponto de saudação onde o codificador Olá última interrupção. Olá `fragment_absolute_time` e `fragment_index` deve aumentar de forma contínua, mas é permitido toointroduce uma descontinuidade, se necessário. Serviços de mídia ignora fragmentos que ele já foi recebida e processada, portanto, é melhor tooerr no lado de saudação do reenviar fragmentos que descontinuidades toointroduce na linha de tempo de mídia de saudação. 

## <a name="9-encoder-redundancy"></a>9. Redundância do codificador
Para certos eventos importantes ao vivo que demanda ainda maior disponibilidade e experiência de qualidade, recomendamos que você use codificadores redundantes ativo-ativo tooachieve perfeita failover sem perda de dados.

![redundância do codificador][image6]

Conforme ilustrado neste diagrama, dois grupos de codificadores push duas cópias de cada fluxo simultaneamente no serviço de saudação ao vivo. Essa configuração tem suporte porque os Serviços de Mídia podem filtrar fragmentos duplicados com base na ID do fluxo e no carimbo de data/hora do fragmento. Olá resultante de transmissão ao vivo e o arquivamento é uma única cópia de todos os fluxos de saudação que é a agregação de possíveis melhor Olá de duas fontes de saudação. Por exemplo, em casos extremos hipotético, desde que exista um codificador (ele não tem toobe Olá mesmo) em execução em qualquer ponto no tempo para cada fluxo, hello resultante fluxo ao vivo do serviço de saudação é contínuo sem perda de dados. 

requisitos de saudação para este cenário são quase Olá mesmo como requisitos de saudação em caso de "Failover de codificador" Olá, com exceção de saudação segundo conjunto de saudação de codificadores são executados em Olá a mesma hora como Olá codificadores primários.

## <a name="10-service-redundancy"></a>10. Redundância de serviço
Para distribuição global altamente redundante, às vezes, você deve ter desastres regionais toohandle backup entre regiões. Expandindo topologia de "Redundância de codificador" Olá, os clientes podem escolher toohave uma implantação do serviço de redundância em uma região diferente que está conectada com o segundo conjunto de saudação de codificadores. Os clientes também podem trabalhar com um provedor de rede de fornecimento de conteúdo toodeploy um Gerenciador de tráfego Global na frente do tráfego de cliente do hello dois serviço implantações tooseamlessly rota. requisitos de saudação para codificadores Olá são Olá mesmo Olá caso "Redundância de codificador". Olá apenas a exceção é segundo conjunto de saudação de codificadores necessidades toobe apontada tooa diferente ao vivo ponto de extremidade de ingestão. Olá diagrama a seguir mostra essa configuração:

![redundância de serviço][image7]

## <a name="11-special-types-of-ingestion-formats"></a>11. Tipos especiais de formatos de ingestão
Esta seção discute tipos especiais de formatos de inclusão dinâmica cenários específicos toohandle projetado.

### <a name="sparse-track"></a>Faixa esparsa
Ao realizar uma apresentação de transmissão ao vivo com uma experiência de cliente avançado, geralmente é necessário tootransmit sincronizados com o tempo eventos ou sinaliza em banda com dados de mídia principal hello. Um exemplo disso é a inserção dinâmica de anúncios em tempo real. Esse tipo de sinalização de evento é diferente do streaming regular de áudio/vídeo devido à sua natureza esparsa. Em outras palavras, Olá sinalização de dados normalmente não ocorrem continuamente, e o intervalo de saudação pode ser toopredict de disco rígido. conceito de saudação de faixa esparsa foi projetado tooingest e dados de sinalização de difusão em banda.

Olá, etapas a seguir são uma implementação recomendada para a ingestão de faixa esparsa:

1. Crie um fluxo de bits MP4 fragmentado separado que contenha apenas faixas esparsas sem faixas de áudio/vídeo.
2. Em Olá **Live Server manifesto caixa** conforme definido na seção 6 em [1], use Olá *parentTrackName* nome do parâmetro toospecify Olá da faixa de pai hello. Para saber mais, consulte a Seção 4.2.1.2.1.2 em [1].
3. Em Olá **Live Server manifesto caixa**, **manifestOutput** deve ser definido muito**true**.
4. Devido a natureza esparsas Olá Olá sinalização de evento, é recomendável seguir hello:
   
    a. No início de saudação do evento ao vivo hello, codificador Olá envia caixas de cabeçalho inicial Olá toohello serviço, que permite que a faixa esparsa do Olá Olá serviço tooregister no manifesto do cliente hello.
   
    b. codificador Olá deve encerrar a solicitação de HTTP POST hello quando dados não estão sendo enviados. Um POST HTTP de longa execução que não enviam dados pode impedir que os serviços de mídia rapidamente se desconectar do codificador Olá no evento de saudação de uma reinicialização do serviço servidor ou de atualização. Nesses casos, o servidor de mídia hello está temporariamente bloqueado em uma operação de recebimento no soquete hello.
   
    c. Durante o tempo de saudação quando sinalização de dados não está disponível, codificador Olá deve fechar a solicitação de HTTP POST hello. Enquanto a solicitação POST Olá estiver ativa, o codificador de saudação deve enviar os dados.

    d. Ao enviar fragmentos esparsos, codificador Olá pode definir um cabeçalho de content-length explícito, se estiver disponível.

    e. Ao enviar esparsos fragmentos com uma nova conexão, codificador Olá deve começar a enviar de saudação cabeçalho seguido por fragmentos novo hello. Isso é para casos no qual o failover ocorre nesse meio e conexão esparsos do novo hello está sendo estabelecida tooa novo servidor que não viu a faixa esparsa Olá antes.

    f. fragmento de faixa esparsa Olá torna-se disponível toohello cliente quando Olá pai acompanhar fragmento correspondente que tem um valor de carimbo de hora igual ou maior é feito cliente toohello disponíveis. Por exemplo, se o fragmento esparsas Olá tem um carimbo de hora de t = 1000, espera-se que depois que o cliente Olá vê timestamp 1000 de fragmento "vídeo" (supondo que o nome da faixa Olá pai é "vídeo") ou posterior, ele pode baixar Olá fragmento esparsas t = 1000. Observe que Olá sinal real pode ser usado para uma posição diferente na linha de tempo de apresentação de saudação para sua finalidade designada. Neste exemplo, ele do possíveis que Olá esparso fragmento de t = 1000 tem uma carga XML, que é para inserir um anúncio em uma posição de alguns segundos mais tarde.

    g. carga de saudação de fragmentos de faixa esparsa pode ser em formatos diferentes (como XML, texto ou binário), dependendo do cenário de saudação.

### <a name="redundant-audio-track"></a>Faixa de áudio redundante
Em um HTTP adaptive streaming cenário típico (por exemplo, Smooth Streaming ou traço), muitas vezes, há apenas uma faixa de áudio em toda a apresentação hello. Ao contrário de faixas de vídeo, que têm vários níveis de qualidade para toochoose de cliente de saudação em condições de erro, faixa de áudio Olá pode ser um ponto único de falha se hello inclusão de fluxo de saudação que contém a faixa de áudio Olá for interrompida. 

toosolve oferece suporte a esse problema, os serviços de mídia ao vivo a inclusão de faixas de áudio redundantes. Olá, trata-que Olá mesmo faixa de áudio pode ser enviada várias vezes em diferentes fluxos. Embora hello serviço apenas registra faixa de áudio Olá uma vez no manifesto do cliente hello, ele pode usar faixas de áudio redundantes como backups para recuperar fragmentos de áudio se faixa de áudio principal Olá tem problemas. faixas de áudio de tooingest redundantes, codificador Olá precisa:

1. Crie hello faixa de áudio mesmo fragmento vários bitstreams MP4. faixas de áudio redundantes Olá devem ser equivalentes semanticamente, com hello mesmo fragmentar os carimbos de hora e ser intercambiáveis no cabeçalho hello e níveis de fragmento.
2. Certifique-se de entrada "áudio" hello em Olá Live Server manifesto (seção 6 em [1]) é hello mesmo para redundância todas as faixas de áudio.

Olá implementação a seguir é recomendado para faixas de áudio redundantes:

1. Envie cada faixa de áudio exclusiva em um fluxo por si só. Além disso, enviar um fluxo redundante para cada um desses fluxos de faixa de áudio, onde a segundo fluxo de saudação difere de saudação somente por identificador Olá Olá URL de POSTAGEM HTTP: {protocolo} :// {endereço do servidor} / {path}/Streams({identifier}) de ponto de publicação.
2. Use fluxos separados toosend Olá dois menores vídeo taxas de bits. Cada um desses fluxos também DEVE conter uma cópia de cada faixa de áudio exclusiva. Por exemplo, quando há suporte para vários idiomas, esses fluxos DEVEM conter faixas de áudio para cada idioma.
3. Usar tooencode de instâncias de servidor separados (codificador) e enviar fluxos de redundância Olá mencionados em (1) e (2). 

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[image1]: ./media/media-services-fmp4-live-ingest-overview/media-services-image1.png
[image2]: ./media/media-services-fmp4-live-ingest-overview/media-services-image2.png
[image3]: ./media/media-services-fmp4-live-ingest-overview/media-services-image3.png
[image4]: ./media/media-services-fmp4-live-ingest-overview/media-services-image4.png
[image5]: ./media/media-services-fmp4-live-ingest-overview/media-services-image5.png
[image6]: ./media/media-services-fmp4-live-ingest-overview/media-services-image6.png
[image7]: ./media/media-services-fmp4-live-ingest-overview/media-services-image7.png
