---
title: "aaaLive streaming usando fluxos de várias taxas de bits do Azure Media Services toocreate | Microsoft Docs"
description: "Este tópico descreve como tooset um canal que recebe uma taxa de bits única live fluxo de um codificador de local e, em seguida, executa o fluxo de taxa de bits tooadaptive codificação ao vivo com os serviços de mídia. Olá fluxo pode ser entregue aplicativos de reprodução de tooclient por meio de um ou mais extremidades de Streaming, usando um dos seguintes protocolos de streaming adaptáveis de saudação: HLS, Smooth Stream, MPEG DASH."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 30ce6556-b0ff-46d8-a15d-5f10e4c360e2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: a8bbdd1570cc9a11bfc2de7bb4ceb9006cc25534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams"></a>O uso do Azure Media Services toocreate várias taxas de bits fluxos de transmissão ao vivo
## <a name="overview"></a>Visão geral
No AMS (Serviços de Mídia do Azure), um **Canal** representa um pipeline para o processamento de conteúdo de transmissão ao vivo. Um **Canal** recebe transmissões de entrada ao vivo de uma das duas maneiras a seguir:

* Um codificador ao vivo no local envia um fluxo de taxa de bits única canal toohello que é habilitado tooperform live codificação com os serviços de mídia em um dos formatos a seguir de saudação: RTP (MPEG-TS), RTMP ou Smooth Streaming (MP4 fragmentado). Olá Channel, em seguida, executa a codificação ao vivo de entrada de saudação taxa de bits única fluxo tooa várias taxas de bits (adaptável) fluxo de vídeo. Quando solicitado, os serviços de mídia oferece Olá fluxo toocustomers.
* Um codificador ao vivo no local envia uma taxa de bits múltipla **RTMP** ou **Smooth Streaming** o canal de toohello (MP4 fragmentado) que não é habilitado tooperform ao vivo de codificação com AMS. fluxos de saudação incluído passam **Channel**s sem nenhum processamento adicional. Esse método é chamado **passagem**. Você pode usar o hello codificadores ao vivo que geram várias taxas de bits Smooth Streaming a seguir: MediaExcel, Ateme, Imagine comunicações, Envivio, Cisco e Elemental. Olá, seguintes codificadores dinâmicos saída RTMP: codificadores certificação Adobe Flash Media ao vivo codificador (FMLE), Telestream Wirecast, Haivision, Teradek e Tricaster.  Um codificador ao vivo também pode enviar um canal de tooa no fluxo de taxa de bits única que não está habilitado para codificação ao vivo, mas que não é recomendado. Quando solicitado, os serviços de mídia oferece Olá fluxo toocustomers.
  
  > [!NOTE]
  > Usando um método de passagem é a maneira de mais econômica Olá toodo live streaming.
  > 
  > 

Começando com versão Olá 2.10 de serviços de mídia, quando você cria um canal, você pode especificar em qual modo você deseja para seu fluxo de entrada do canal tooreceive hello e se deseja ou não para Olá canal tooperform live codificação de sua transmissão. Você tem duas opções:

* **Nenhum** – especifique esse valor, se você planejar toouse um codificador ao vivo no local, que resultará em fluxo de múltiplas taxas de bits (um fluxo de passagem). Nesse caso, o fluxo de entrada hello passado toohello sem nenhuma codificação de saída. Esse é o comportamento de saudação de uma versão anterior too2.10 de canal.  Para obter informações mais detalhadas sobre como trabalhar com canais desse tipo, confira [Transmissão ao vivo com codificadores locais que criam transmissões de múltiplas taxas de bits](media-services-live-streaming-with-onprem-encoders.md).
* **Padrão** – escolha esse valor, se você planejar toouse serviços de mídia tooencode seu fluxo de toomulti taxas de bits de transmissão ao vivo de taxa de bits única. Lembre-se de que há um impacto de cobrança para codificação ao vivo e você deve se lembrar que deixar um canal de codificação ao vivo em estado de "Running" hello incorrerão em cobranças.  É recomendável que você interrompa imediatamente seus canais em execução após o evento de transmissão ao vivo é concluída tooavoid encargos adicionais por hora.

> [!NOTE]
> Este tópico discute os atributos de canais que são habilitados tooperform de codificação ao vivo (**padrão** tipo de codificação). Para obter informações sobre como trabalhar com canais não estão habilitados tooperform de codificação ao vivo, consulte [transmissão ao vivo com codificadores locais que criam fluxos de várias taxas de bits](media-services-live-streaming-with-onprem-encoders.md).
> 
> Verifique se Olá de tooreview [considerações](media-services-manage-live-encoder-enabled-channels.md#Considerations) seção.
> 
> 

## <a name="billing-implications"></a>Implicações de cobrança
Um canal de codificação ao vivo começa assim que seu estado faz a transição "Running" muito via Olá API de cobrança.   Você também pode exibir o estado de saudação em Olá portal do Azure, ou na ferramenta de Gerenciador de serviços de mídia do Azure hello (http://aka.ms/amse).

Olá tabela a seguir mostra como os estados de canal mapeiam estados toobilling Olá API e portal do Azure. Observe que Olá estados são ligeiramente diferentes entre hello API e UX Portal. Assim que um canal está no estado "Em execução" hello via API de hello, ou em hello "Pronta" ou "Streaming" estado Olá portal do Azure, a cobrança será ativa.
Canal de saudação toostop de cobrança é ainda mais, você tem tooStop Olá canal por meio da API de saudação ou em Olá portal do Azure.
Você é responsável por parar as canais quando tiver terminado com o canal de codificação ao vivo hello.  Falha toostop um canal de codificação resulta em cobrança contínua.

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

### <a name="automatic-shut-off-for-unused-channels"></a>Desligamento automático para canais não usados
A partir de 25 de janeiro de 2016, os Serviços de Mídia distribuíram uma atualização que interrompe automaticamente um canal (com codificação ativa desabilitada) depois que ele tiver sido executado em um estado não utilizado por um longo período. Isso se aplica a tooChannels com nenhuma programas ativos e que não receberam uma contribuição entrada feed por um longo período de tempo.

limite de saudação por um período não utilizado é uma de 12 horas, mas é toochange de assunto.

## <a name="live-encoding-workflow"></a>Fluxo de trabalho da codificação ativa
Olá, diagrama a seguir representa um fluxo de trabalho de streaming ao vivo em um canal recebe um fluxo de taxa de bits única em um dos seguintes protocolos de saudação: RTMP, Smooth Streaming ou RTP (MPEG-TS); ele, em seguida, codifica o fluxo de múltiplas taxas de bits de tooa Olá fluxo. 

![Fluxo de trabalho ao vivo][live-overview]

## <a id="scenario"></a>Cenário comum de streaming ao vivo
Olá seguem geral de etapas envolvidas na criação de aplicativos comuns de transmissão ao vivo.

> [!NOTE]
> Atualmente, Olá máximo recomendado de duração de um evento ao vivo é 8 horas. Entre em contato com amslived em Microsoft.com se você precisar toorun um canal para períodos de tempo mais longos. Lembre-se de que há um impacto de cobrança para codificação ao vivo e você deve se lembrar que deixar um canal de codificação ao vivo em estado de "Running" hello incorrerão em cobranças por hora.  É recomendável que você interrompa imediatamente seus canais em execução após o evento de transmissão ao vivo é concluída tooavoid encargos adicionais por hora. 
> 
> 

1. Conecte um computador de tooa de câmera de vídeo. Inicie e configure um codificador ao vivo no local que pode produzir um **único** fluxo de taxa de bits em um dos seguintes protocolos de saudação: RTMP, Smooth Streaming ou RTP (MPEG-TS). 
   
    Essa etapa também pode ser realizada após a criação do canal.
2. Crie e inicie um Canal. 
3. URL de ingestão recuperar Olá canal. 
   
    URL de ingestão Olá é usado pelo Olá codificador ao vivo toosend Olá fluxo toohello canal.
4. Recupere a URL de visualização do canal hello. 
   
    Use este tooverify URL que o canal está recebendo corretamente transmissão ao vivo hello.
5. Crie um programa. 
   
    Quando usar hello portal do Azure, criar um programa também cria um ativo. 
   
    Ao usar o SDK .NET ou REST você precisa toocreate um ativo e especifica toouse este ativo durante a criação de um programa. 
6. Publica o ativo de saudação associado ao programa hello.   
   
    >[!NOTE]
    >Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. saudação do qual você deseja que o conteúdo de toostream de ponto de extremidade de streaming tem toobe em Olá **executando** estado. 
    
7. Inicie o programa de hello quando você estiver pronto toostart transmissão e o arquivamento.
8. Opcionalmente, o codificador ao vivo Olá pode ser sinalizado toostart um anúncio. anúncio de saudação é inserido no fluxo de saída de hello.
9. Pare o programa de saudação sempre que quiser toostop streaming e arquivamento evento hello.
10. Excluir Olá programa (e opcionalmente exclua o ativo de saudação).   

> [!NOTE]
> É muito importante não tooforget tooStop um canal de codificação ao vivo. Lembre-se de que não há impacto para codificação ao vivo de cobrança por hora e você deve se lembrar que deixar um canal de codificação ao vivo em estado de "Running" hello incorrerão em cobranças.  É recomendável que você interrompa imediatamente seus canais em execução após o evento de transmissão ao vivo é concluída tooavoid encargos adicionais por hora. 
> 
> 

## <a id="channel"></a>Configurações de entrada (ingestão) do canal
### <a id="Ingest_Protocols"></a>Protocolo de streaming de ingestão
Se hello **tipo de codificador** está definido muito**padrão**, as opções válidas são:

* **RTP** (MPEG-TS): fluxo de transporte de MPEG-2 por RTP.  
* **RTMP**
* **MP4 fragmentado** de taxa de bits única (Smooth Streaming)

#### <a name="rtp-mpeg-ts---mpeg-2-transport-stream-over-rtp"></a>RTP (MPEG TS) - fluxo de transporte de MPEG-2 por RTP.
Caso de uso típico: 

As emissoras Professional geralmente trabalham com codificadores ao vivo de local high-end de fornecedores como tecnologias elementar, Ericsson, Ateme, Imagine ou Envivio toosend um fluxo. Geralmente usado em conjunto com o departamento de TI e redes privadas.

Considerações:

* uso de saudação de um fluxo de transporte de programa único (SPTS) de entrada é altamente recomendável. 
* Você pode inserir too8 fluxos de áudio usando MPEG-2 TS sobre RTP. 
* fluxo de vídeo Olá deve ter uma taxa de bits média abaixo 15 Mbps
* Olá agregação taxa de bits média de fluxos de áudio Olá deve ter menos de 1 Mbps
* A seguir são Olá codecs com suporte:
  
  * Vídeo MPEG-2 / H.262 
    
    * Perfil Principal (4:2:0)
    * Perfil Alto (4:2:0, 4:2:2)
    * Perfil 422 (4:2:0, 4:2:2)
  * Vídeo MPEG-4 AVC / H.264  
    
    * Linha de base, Principal, Perfil Alto (8 bits 4:2:0)
    * Perfil Alto 10 (10 bits 4:2:0)
    * Perfil Alto 422 (10 bits 4:2:2)
  * Áudio MPEG-2 AAC-LC 
    
    * Mono, Estéreo, Surround (5.1, 7.1)
    * Empacotamento de ADTS estilo MPEG-2
  * Áudio Dolby Digital (AC-3) 
    
    * Mono, Estéreo, Surround (5.1, 7.1)
  * Áudio MPEG (camada II e III) 
    
    * Mono, estéreo
* Os codificadores para difusão recomendados incluem:
  
  * Imagine Communications Selenio ENC 1
  * Imagine Communications Selenio ENC 2
  * Elemental Live

#### <a id="single_bitrate_RTMP"></a>RTMP de taxa de bits única
Considerações:

* fluxo de entrada Hello não pode conter várias taxas de bits vídeo
* fluxo de vídeo Olá deve ter uma taxa de bits média abaixo 15 Mbps
* fluxo de áudio Olá deve ter uma taxa de bits média abaixo de 1 Mbps
* A seguir são Olá codecs com suporte:
* Vídeo MPEG-4 AVC / H.264
* Linha de base, Principal, Perfil Alto (8 bits 4:2:0)
* Perfil Alto 10 (10 bits 4:2:0)
* Perfil Alto 422 (10 bits 4:2:2)
* Áudio MPEG-2 AAC-LC
* Mono, Estéreo, Surround (5.1, 7.1)
* Taxa de amostragem de 44,1 kHz
* Empacotamento de ADTS estilo MPEG-2
* Os codificadores recomendados incluem:
* Telestream Wirecast
* Flash Media Live Encoder

#### <a name="single-bitrate-fragmented-mp4-smooth-streaming"></a>MP4 fragmentado de taxa de bits única (Smooth Streaming)
Caso de uso típico:

Usar local codificadores ao vivo de fornecedores como tecnologias elementar, Ericsson, Ateme, Envivio toosend Olá fluxo de entrada sobre Olá abra internet tooa nas proximidades de data center do Azure.

Considerações:

O mesmo que o mencionado para [RTMP com taxa de bits única](media-services-manage-live-encoder-enabled-channels.md#single_bitrate_RTMP).

#### <a name="other-considerations"></a>Outras considerações
* Você não pode alterar o protocolo de entrada hello durante a saudação canal ou seus programas associados são executados. Se você precisar de protocolos diferentes, você deve criar canais separados para cada protocolo de entrada.
* Resolução máxima para o fluxo de vídeo de entrada hello está 1920 x 1080, no máximo 60 campos/segundo se entrelaçada e 30 quadros por segundo se progressivo.

### <a name="ingest-urls-endpoints"></a>URLs de ingestão (pontos de extremidade)
Um canal fornece um ponto de extremidade de entrada (URL de ingestão) que você especificar no codificador ao vivo do hello, para o codificador Olá pode enviar fluxos tooyour canais.

Você pode obter Olá URLs de ingestão, quando você cria um canal. tooget essas URLs, Olá canal não tem toobe em Olá **executando** estado. Quando você estiver pronto toostart enviar dados por push em Olá canal, ele deve estar no hello **executando** estado. Depois que o canal de saudação inicia a ingestão de dados, você pode visualizar o fluxo por meio da URL de visualização de saudação.

Você tem a opção de ingerir fluxo ao vivo (Smooth Streaming) de MP4 fragmentado por uma conexão SSL. tooingest por SSL, verifique Olá de tooupdate se tooHTTPS de URL de ingestão. Observe que, atualmente, o AMS não dá suporte ao SSL com domínios personalizados.  

### <a name="allowed-ip-addresses"></a>Endereços IP permitidos
Você pode definir os endereços IP hello permitidos toopublish toothis vídeo canal. Os endereços IP permitidos podem ser especificados como um endereço IP individual (por exemplo, '10.0.0.1'), um intervalo de IPs usando um endereço IP e uma máscara de sub-rede CIDR (por exemplo, ‘10.0.0.1/22’), ou um intervalo de IPs usando um endereço IP e uma máscara de sub-rede decimal com pontos (por exemplo, '10.0.0.1(255.255.252.0)').

Se nenhum endereço IP for especificado e não houver definição de regra, nenhum endereço IP será permitido. tooallow qualquer endereço IP, crie uma regra e defina 0.0.0.0/0.

## <a name="channel-preview"></a>Visualização de canal
### <a name="preview-urls"></a>URLs de visualização
Os canais oferecem uma empresa de visualização (URL de visualização) que você use toopreview e valida sua transmissão antes de processamento e entrega.

Você pode obter a URL de visualização de hello quando você criar o canal de saudação. tooget Olá URL, canal Olá não tem toobe em Olá **executando** estado.

Depois que o canal de saudação inicia a ingestão de dados, você pode visualizar o fluxo.

> [!NOTE]
> Atualmente fluxo de visualização Olá só pode ser entregues em MP4 fragmentado (Smooth Streaming) formato independentemente Olá especificado tipo de entrada. Você pode usar o hello [http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor) player tootest Olá Smooth Stream. Você também pode usar um player hospedado no hello tooview portal do Azure seu fluxo.
> 
> 

### <a name="allowed-ip-addresses"></a>Endereços IP permitidos
Você pode definir os endereços IP hello que têm permissão de ponto de extremidade de visualização de toohello tooconnect. Se nenhum endereço IP for especificado, qualquer endereço IP será permitido. Os endereços IP permitidos podem ser especificados como um endereço IP individual (por exemplo, '10.0.0.1'), um intervalo de IPs usando um endereço IP e uma máscara de sub-rede CIDR (por exemplo, ‘10.0.0.1/22’), ou um intervalo de IPs usando um endereço IP e uma máscara de sub-rede decimal com pontos (por exemplo, ‘10.0.0.1(255.255.252.0)’).

## <a name="live-encoding-settings"></a>Configurações de codificação ao vivo
Esta seção descreve como configurações Olá para o codificador ao vivo de saudação no hello canal podem ser ajustada, hello quando **o tipo de codificação** de um canal é definido muito**padrão**.

> [!NOTE]
> Ao inserir várias faixas de idioma e fazer a codificação ao vivo com o Azure, somente o RTP tem suporte para vários idioma entrada. Você pode definir fluxos de áudio too8 usando MPEG-2 TS sobre RTP. A ingestão de várias faixas de áudio com RTMP ou Smooth streaming não tem suporte atualmente. Ao realizar a codificação ativa com [local live codifica](media-services-live-streaming-with-onprem-encoders.md), não há nenhuma limitação tal porque tudo o que é enviado tooAMS passa por um canal sem nenhum processamento adicional.
> 
> 

### <a name="ad-marker-source"></a>Origem do marcador de anúncio
Você pode especificar a origem Olá para sinais de marcadores de anúncio. Valor padrão é **Api**, que indica que codificador ao vivo de saudação em Olá canal deve escutar tooan assíncrona **API do marcador Ad**.

Olá outra opção válida é **Scte35** (permitido somente se Olá ingestão protocolo de transmissão é definido tooRTP (MPEG-TS). Quando Scte35 for especificado, codificador ao vivo Olá analisa os sinais SCTE-35 Olá RTP (MPEG-TS) do fluxo de entrada.

### <a name="cea-708-closed-captions"></a>Legendas CEA 708
Um sinalizador opcional que informa Olá codificador ao vivo tooignore quaisquer dados de legendas CEA 708 incorporados no vídeo de entrada hello. Quando o sinalizador de saudação é definido toofalse (padrão), codificador Olá detectará e insira novamente os dados CEA 708 em fluxos de vídeo de saída de hello.

### <a name="video-stream"></a>Transmissão de vídeo
Opcional. Descreve o fluxo de vídeo entrada hello. Se esse campo não for especificado, o valor padrão de saudação é usado. Essa configuração é permitida somente se o protocolo de transmissão é definido tooRTP (MPEG-TS) de entrada hello.

#### <a name="index"></a>Índice
Um índice de base zero que especifica qual fluxo de vídeo de entrada deve ser processado pelo codificador ao vivo de saudação no canal de saudação. Essa configuração se aplica apenas se o protocolo de streaming de ingestão é RTP (MPEG-TS).

O valor padrão é zero. É recomendável toosend em um fluxo de transporte de programa único (SPTS). Se o fluxo de entrada hello contiver vários programas, codificador ao vivo Olá analisa Olá tabela de mapa de programa (PGTO) na entrada hello, identifica Olá entradas que têm um nome de tipo de fluxo de vídeo MPEG-2 ou h. 264 e as organiza na ordem de saudação especificada no hello PGTO. índice de base zero de saudação é usado toopick a entrada de n-ésimo Olá na organização.

### <a name="audio-stream"></a>Fluxo de áudio
Opcional. Descreve os fluxos de áudio de entrada de saudação. Se esse campo não for especificado, valores padrão de saudação especificados se aplicam. Essa configuração é permitida somente se o protocolo de transmissão é definido tooRTP (MPEG-TS) de entrada hello.

#### <a name="index"></a>Índice
É recomendável toosend em um fluxo de transporte de programa único (SPTS). Se o fluxo de entrada hello contiver vários programas, hello codificador ao vivo no canal de saudação analisa Olá tabela de mapa de programa (PGTO) na entrada hello, identifica Olá entradas que têm um nome de tipo de fluxo de MPEG-2 AAC ADTS ou AC-3 sistema-A ou AC-3 sistema-B ou MPEG-2 privada PES ou áudio MPEG-1 ou áudio MPEG-2 e as organiza na ordem de saudação especificada no hello PGTO. índice de base zero de saudação é usado toopick a entrada de n-ésimo Olá na organização.

#### <a name="language"></a>idioma
Olá identificador de idioma do fluxo de áudio hello, conforme tooISO 639-2, como ENG. Se não estiver presente, o padrão de saudação é UND (indefinido).

Pode haver o fluxo de áudio too8 conjuntos especificados se Olá entrada toohello canal for MPEG-2 TS sobre RTP. No entanto, não pode haver nenhum duas entradas com hello mesmo valor de índice.

### <a id="preset"></a>Predefinição do sistema
Especifica a saudação predefinição toobe usada pelo codificador ao vivo de saudação nesse canal. Olá no momento, somente permitido é de valor **Default720p** (padrão).

Observe que, se você precisar de predefinições personalizadas, você deverá entrar em contato com amslived em Microsoft.com.

**Default720p** codifica vídeo Olá em Olá 7 camadas a seguir.

#### <a name="output-video-stream"></a>Fluxo de vídeo de saída
| Taxa de bits | Largura | Altura | MáxFPS | Perfil | Nome do fluxo de saída |
| --- | --- | --- | --- | --- | --- |
| 3500 |1280 |720 |30 |Alto |Video_1280x720_3500kbps |
| 2200 |960 |540 |30 |Principal |Video_960x540_2200kbps |
| 1350 |704 |396 |30 |Principal |Video_704x396_1350kbps |
| 850 |512 |288 |30 |Principal |Video_512x288_850kbps |
| 550 |384 |216 |30 |Principal |Video_384x216_550kbps |
| 350 |340 |192 |30 |Linha de base |Video_340x192_350kbps |
| 200 |340 |192 |30 |Linha de base |Video_340x192_200kbps |

#### <a name="output-audio-stream"></a>Fluxo de áudio de saída
Áudio é codificado toostereo AAC-LC a 64 kbps, taxa de 44,1 kHz de amostragem.

## <a name="signaling-advertisements"></a>Sinalização de anúncios
Quando o canal está com codificação ao vivo habilitada, você tem um componente em seu pipeline de processamento de vídeo e pode manipulá-lo. Você pode sinalizar para Olá canal tooinsert slates e/ou anúncios no fluxo de taxa de bits adaptável saída hello. Slates ainda são imagens que você pode usar toocover o feed de ao vivo entrada hello em alguns casos (por exemplo, durante um intervalo comercial). Sinais de publicidade, são sincronizadas sinais que inserir em Olá saída fluxo tootell Olá player de vídeo tootake ação especial – como tooswitch tooan anúncio no momento apropriado hello. Consulte este [blog](https://codesequoia.wordpress.com/2014/02/24/understanding-scte-35/) para obter uma visão geral do mecanismo de sinalização Olá SCTE-35 usado para essa finalidade. Abaixo está um cenário típico que você poderia implementar em seu evento ao vivo.

1. Ter seus visualizadores de obter uma imagem de antes do evento antes do início do evento hello.
2. Ter seus visualizadores de obter uma imagem após o evento após o término do evento hello.
3. Ter seus visualizadores de obter uma imagem de evento de erro, se houver um problema durante o evento de saudação (por exemplo, falta de energia no Estádio Olá).
4. Envie um intervalo de anúncio imagem toohide Olá evento ao vivo feed durante um intervalo comercial.

Olá seguem propriedades Olá que você pode definir quando a sinalização de anúncios. 

### <a name="duration"></a>Duration
duração de Hello, em segundos, de intervalo comercial hello. Isso tem um valor positivo diferente de zero toobe no intervalo comercial da ordem toostart hello. Quando um intervalo comercial está em andamento e a duração de saudação conjunto toozero com hello CueId correspondentes intervalo comercial do hello contínuo, em seguida, esse intervalo é cancelado.

### <a name="cueid"></a>CueId
Uma ID exclusiva para o intervalo comercial hello, toobe usado pelo aplicativo downstream tootake as ações apropriadas. Precisa de toobe um número inteiro positivo. Você pode definir este valor tooany aleatória inteiro ou usar uma saudação de tootrack sistema upstream Ids de indicação. Verifique determinado toonormalize qualquer inteiros de toopositive ids antes de enviar por meio da API de saudação.

### <a name="show-slate"></a>Mostrar slate
Opcional. Sinaliza Olá codificador ao vivo tooswitch toohello [padrão Tablet](media-services-manage-live-encoder-enabled-channels.md#default_slate) imagem durante um intervalo comercial e ocultar a alimentação de vídeo entrada hello. O áudio também é desligado durante o slate. O padrão é **false**. 

imagem de saudação usada será Olá especificada por meio da propriedade Id de ativo de slate padrão Olá em tempo de saudação da criação do canal de saudação. Tablet Olá será ampliada toofit tamanho da imagem de exibição de saudação. 

## <a name="insert-slate--images"></a>Inserir imagens fixas
codificador ao vivo de saudação no hello canal pode ser sinalizado tooswitch tooa slate imagem. Ele também pode ser sinalizado tooend um slate contínuo. 

codificador ao vivo Olá pode ser configurado tooswitch tooa slate imagem e ocultar Olá vídeo sinal de entrada em determinadas situações, por exemplo, durante um intervalo de anúncio. Se um slate desse tipo não estiver configurado, o vídeo de entrada não é mascarado durante esse intervalo comercial.

### <a name="duration"></a>Duration
duração de saudação do Tablet saudação em segundos. Isso tem um valor positivo diferente de zero toobe no Tablet de saudação do toostart de ordem. Se houver um slate em andamento e uma duração de zero for especificada, esse slate será encerrado.

### <a name="insert-slate-on-ad-marker"></a>Inserir o slate no marcador de anúncio
Quando o conjunto tootrue, essa configuração configura Olá codificador ao vivo tooinsert uma imagem slate durante um intervalo de anúncio. valor padrão de saudação é true. 

### <a id="default_slate"></a>ID de ativo de slate padrão

Opcional. Especifica a saudação Id do ativo de hello ativo de serviços de mídia que contém a imagem de saudação slate. O padrão é nulo. 


>[!NOTE] 
>Antes de criar o canal hello, hello imagem slate com hello restrições a seguir deve ser carregada como um ativo dedicado (nenhum outro arquivo deve estar nesse ativo). Esta imagem é usada somente quando o codificador ao vivo hello está inserindo um Tablet devido tooan intervalo de anúncio ou tenha sido explicitamente sinalizado tooinsert um Tablet. codificador ao vivo Olá também pode ir em um modo de slate durante determinadas condições de erro – por exemplo se o sinal de entrada hello serão perdido. Não há atualmente nenhuma toouse opção uma imagem personalizada ao codificador ao vivo Olá entra em tal um estado 'perdido de sinal de entrada'. Você pode votar para esse recurso [aqui](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/10190457-define-custom-slate-image-on-a-live-encoder-channel).


* No máximo 1920x1080 na resolução.
* No máximo 3 megabytes de tamanho.
* nome do arquivo Hello deve ter uma extensão *.jpg.
* imagem de saudação deve ser carregada em um ativo como Olá que assetfile somente nesse ativo e esse AssetFile devem ser marcado como arquivo principal hello. Olá ativo não pode ser armazenamento criptografado.

Se hello **Id do ativo de slate padrão** não for especificado, e **inserir slate no marcador ad** está definido muito**true**, uma imagem de serviços de mídia do Azure padrão será usado toohide Olá de entrada fluxo de vídeo. O áudio também é desligado durante o slate. 

## <a name="channels-programs"></a>Programas do canal
Um canal está associado a programas que permitem a publicação de saudação toocontrol e armazenamento de segmentos em uma transmissão ao vivo. Canais gerenciam programas. Olá relação de canal e programa é uma mídia tootraditional muito semelhantes em que um canal tem um fluxo constante de conteúdo e um programa está no escopo toosome atingiu o tempo de evento naquele canal.

Você pode especificar o número de saudação horas deseja tooretain Olá registrada conteúdo para programa hello por configuração Olá **janela de arquivo** comprimento. Esse valor pode ser definido no mínimo 5 minutos tooa máximo 25 horas. Duração da janela de arquivo também determina o período de tempo que os clientes podem procurar de volta no tempo da posição atual ao vivo da saudação máximo hello. Programas podem ser executados pelo período de tempo especificado hello, mas o conteúdo que sai da duração da janela de saudação é continuamente descartado. Esse valor dessa propriedade também determina quanto tempo cliente Olá manifestos podem crescer.

Cada programa está associado um ativo que armazena o conteúdo de streaming de saudação. Um ativo é um contêiner de blob de bloco tooa mapeada na conta de armazenamento do Azure hello e arquivos Olá no ativo de saudação são armazenados como blobs no contêiner. programa de saudação toopublish para que os clientes podem exibir o fluxo de hello, você deve criar um localizador OnDemand para Olá associados ativo. Ter esse localizador permitirá que você toobuild uma URL de streaming que pode fornecer tooyour clientes.

Um canal dá suporte para até toothree simultaneamente programas em execução para que você pode criar diversos arquivos de saudação mesmo fluxo de entrada. Isso permite que você toopublish e arquivamento diferentes partes de um evento, conforme necessário. Por exemplo, o requisito de negócios é tooarchive 6 horas de um programa, mas toobroadcast apenas últimos 10 minutos. tooaccomplish isso, você precisa toocreate dois programas em execução simultaneamente. Um programa está definido tooarchive 6 horas do evento Olá mas Olá programa não será publicado. Olá outro programa é tooarchive conjunto por 10 minutos e esse programa é publicado.

Você não deve reutilizar os programas existentes para novos eventos. Em vez disso, crie e inicie um novo programa para cada evento conforme descrito na seção de programação de aplicativos de fluxo ao vivo hello.

Inicie o programa de hello quando você estiver pronto toostart transmissão e o arquivamento. Pare o programa de saudação sempre que quiser toostop streaming e arquivamento evento hello. 

conteúdo toodelete arquivado, parar e excluir o programa hello e em seguida, exclua o ativo associado Olá. Um ativo não pode ser excluído se ele é usado por um programa; programa Hello deve ser excluído primeiro. 

Mesmo depois de parar e excluir o programa hello, Olá usuários seria capaz de toostream seu conteúdo arquivado como um vídeo sob demanda, para desde que você não excluir Olá ativo.

Se você deseja tooretain Olá arquivado conteúdo, mas não tem disponível para streaming, exclua Olá localizador de streaming.

## <a name="getting-a-thumbnail-preview-of-a-live-feed"></a>Obtenção uma visualização em miniatura de uma transmissão ao vivo
Quando a codificação ao vivo está habilitada, agora você pode obter uma visualização do feed dinâmico Olá como atingir Olá canal. Isso pode ser uma ferramenta valiosa toocheck se o feed em tempo real está realmente chegando Olá canal. 

## <a id="states"></a>Estados de canal e como estados mapeiam toohello modo de cobrança
estado atual de saudação de um canal. Os valores possíveis incluem:

* **Parado**. Este é o estado inicial de saudação do hello canal após sua criação. Nesse estado, propriedades do canal Olá podem ser atualizadas, mas não é permitido fazer streaming.
* **Iniciando**. Olá canal está sendo iniciado. Nenhuma atualização ou streaming é permitido durante esse estado. Se ocorrer um erro, Olá canal retorna toohello estado parado.
* **Executando**. Olá canal é capaz de processar transmissões ao vivo.
* **Parando**. Olá canal está sendo interrompida. Nenhuma atualização ou streaming é permitido durante esse estado.
* **Excluindo**. Olá canal está sendo excluído. Nenhuma atualização ou streaming é permitido durante esse estado.

Olá tabela a seguir mostra como os estados de canal de modo de cobrança de toohello do mapa. 

| Estado de canal | Indicadores da interface do usuário do portal | Cobrado? |
| --- | --- | --- |
| Iniciando |Iniciando |Nenhum (estado transitório) |
| Executando |Pronto (nenhum programa em execução)<br/>ou o<br/>Streaming (há pelo menos um programa em execução) |SIM |
| Parando |Parando |Nenhum (estado transitório) |
| Parado |Parado |Não |

> [!NOTE]
> Atualmente, a média de início do canal de saudação é de cerca de 2 minutos, mas às vezes, pode levar até too20 + minutos. Redefinições de canal podem demorar até too5 minutos.
> 
> 

## <a id="Considerations"></a>Considerações
* Quando um canal de **padrão** tipo de codificação passa por uma perda de feed de origem/contribuição de entrada, ele indica para ele, substituindo Olá áudio/vídeo de origem por um estado de erro e silêncio. Olá canal continuará tooemit um Tablet até Olá entrada/contribuição feed é retomada. É recomendável que um canal ao vivo não seja deixado em tal estado por mais de 2 horas. Além desse ponto, o comportamento de saudação do hello canal na reconexão de entrada não é garantido, nem é seu comportamento na resposta tooa comando Reset. Você terá toostop Olá canal, excluí-lo e criar um novo.
* Você não pode alterar o protocolo de entrada hello durante a saudação canal ou seus programas associados são executados. Se você precisar de protocolos diferentes, você deve criar canais separados para cada protocolo de entrada.
* Sempre que você reconfigurar o codificador ao vivo hello, chame Olá **redefinir** método no canal de saudação. Antes de redefinir o canal de saudação, você tem o programa de saudação do toostop. Depois de redefinir o canal de saudação, reinicie o programa de saudação.
* Um canal pode ser interrompido somente quando está no estado de execução hello e todos os programas no canal Olá foram interrompidos.
* Por padrão, você só pode adicionar 5 canais tooyour conta do Media Services. Essa é uma cota flexível em todas as novas contas. Para obter mais informações, consulte [Cotas e limitações](media-services-quotas-and-limitations.md).
* Você não pode alterar o protocolo de entrada hello durante a saudação canal ou seus programas associados são executados. Se você precisar de protocolos diferentes, você deve criar canais separados para cada protocolo de entrada.
* Você só será cobrado quando o seu canal estiver no hello **executando** estado. Para obter mais informações, consulte muito[isso](media-services-manage-live-encoder-enabled-channels.md#states) seção.
* Atualmente, Olá máximo recomendado de duração de um evento ao vivo é 8 horas. Entre em contato com amslived em Microsoft.com se você precisar toorun um canal para períodos de tempo mais longos.
* Certifique-se de toohave Olá ponto de extremidade de streaming do qual você deseja que o conteúdo toostream Olá **executando** estado.
* Ao inserir várias faixas de idioma e fazer a codificação ao vivo com o Azure, somente o RTP tem suporte para vários idioma entrada. Você pode definir fluxos de áudio too8 usando MPEG-2 TS sobre RTP. A ingestão de várias faixas de áudio com RTMP ou Smooth streaming não tem suporte atualmente. Ao realizar a codificação ativa com [local live codifica](media-services-live-streaming-with-onprem-encoders.md), não há nenhuma limitação tal porque tudo o que é enviado tooAMS passa por um canal sem nenhum processamento adicional.
* usos de predefinição codificação Olá Olá noção de "taxa de quadros max" de 30 fps. Portanto, se hello entrada é 60fps / 59.97i, quadros de entrada hello são descartadas/de-interlaced fps too30/29,97. Se a entrada hello é 50fps/50i, quadros de entrada hello são descartadas/de-interlaced too25 fps. Se a entrada de saudação é 25 fps, saída permanece em 25 fps.
* Não se esqueça de tooSTOP seus canais quando terminar. Caso contrário, a cobrança continuará.

## <a name="known-issues"></a>Problemas conhecidos
* O tempo de inicialização do canal foi aprimorada tooan média de 2 minutos, mas às vezes de aumento da demanda ainda pode levar até too20 + minutos.
* O suporte RTP é fornecido na para difusores profissionais. Analise observações de saudação sobre RTP em [isso](https://azure.microsoft.com/blog/2015/04/13/an-introduction-to-live-encoding-with-azure-media-services/) blog.
* Imagens de slate devem estar de acordo com toorestrictions descrito [aqui](media-services-manage-live-encoder-enabled-channels.md#default_slate). Se você tentar crie um canal com um erro slate do padrão que seja maior que 1920 x 1080, hello solicitação será eventualmente.
* Uma vez... não se esqueça de tooSTOP seus canais quando você terminar de streaming. Caso contrário, a cobrança continuará.

## <a name="next-step"></a>Próxima etapa
Revise os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Tópicos relacionados
[Trabalhando com Eventos de Live Streaming com os Serviços de Mídia do Azure](media-services-overview.md)

[Criar canais de executam a codificação ao vivo de um fluxo de taxa de bits única taxa de bits tooadaptive com o Portal](media-services-portal-creating-live-encoder-enabled-channel.md)

[Criar canais de executam a codificação ao vivo de um fluxo de taxa de bits única taxa de bits tooadaptive com o SDK .NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)

[Gerenciar canais com a API REST](https://docs.microsoft.com/rest/api/media/operations/channel)
 
[Conceitos de Serviços de Mídia](media-services-concepts.md)

[Especificação de ingestão dinâmica de MP4 fragmentado dos Serviços de Mídia do Azure](media-services-fmp4-live-ingest-overview.md)

[live-overview]: ./media/media-services-manage-live-encoder-enabled-channels/media-services-live-streaming-new.png

