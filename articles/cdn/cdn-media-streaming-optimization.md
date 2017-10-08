---
title: "aaaMedia otimização via hello Azure rede de fornecimento de conteúdo de streaming"
description: "Otimizar arquivos de mídia de streaming para a distribuição suave"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: a05a86204708c7ea7ef1f9be04323cdda6a2d403
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="media-streaming-optimization-via-hello-azure-content-delivery-network"></a>Otimização via hello Azure rede de fornecimento de conteúdo de streaming de mídia 
 
Uso de vídeo de alta definição está aumentando em Olá Internet, que cria dificuldades para entrega eficiente de arquivos grandes. Os clientes esperam smooth reprodução de vídeo sob demanda ou live ativos de vídeo em uma variedade de clientes e redes em todo o Olá, mundo. Um mecanismo de entrega rápida e eficiente para arquivos de streaming de mídia é crítico tooensure uma experiência de consumidor e divertido e suave.  

Mídia de streaming ao vivo é especialmente difíceis toodeliver devido tamanhos grandes hello e número de visualizadores simultâneos. Atrasos longos causam tooleave de usuários. Como fluxos ao vivo não podem ser armazenado em cache antecipadamente e latências grandes não são aceitáveis tooviewers, fragmentos de vídeo devem ser entregue de maneira oportuna. 

padrões de solicitação de saudação do streaming também fornecem alguns novos desafios. Quando um fluxo ao vivo popular ou uma nova série é liberada para vídeo sob demanda, milhares toomillions dos visualizadores pode solicitar o fluxo de Olá Olá simultaneamente. Nesse caso, solicitação inteligente consolidação é vital toonot sobrecarregar os servidores de origem hello quando ativos Olá não estão em cache ainda.
 
saudação de rede de entrega de conteúdo do Azure do Akamai agora oferece um recurso que fornece transmissão de ativos de mídia com eficiência toousers globo Olá em escala. recurso de Olá reduz as latências porque ele reduz a carga de saudação em servidores de origem hello. Este recurso está disponível com a camada de preços padrão Akamai hello. 

saudação de rede de entrega de conteúdo do Azure da Verizon fornece streaming de mídia diretamente no tipo de otimização de entrega Olá web geral.
 
## <a name="configure-an-endpoint-toooptimize-media-streaming-in-hello-azure-content-delivery-network-from-akamai"></a>Configurar a mídia de toooptimize um ponto de extremidade de streaming em hello Azure rede de entrega de conteúdo do Akamai
 
Você pode configurar sua entrega de toooptimize de ponto de extremidade do fornecimento de conteúdo CDN (rede) para arquivos grandes por meio do portal do Azure de saudação. Você também pode usar nossas APIs REST ou qualquer um dos Olá cliente SDKs toodo isso. Olá, etapas a seguir mostram processo Olá via Olá portal do Azure:

1. tooadd um novo ponto de extremidade, em Olá **perfil CDN** página, selecione **ponto de extremidade**.
  
    ![Novo ponto de extremidade](./media/cdn-media-streaming-optimization/01_Adding.png)

2. Em Olá **otimizado para** lista suspensa, selecione **vídeo sob demanda de streaming de mídia** ativos de vídeo sob demanda. Se você fizer uma combinação do streaming de vídeo ao vivo e de vídeo por demanda, selecione **Streaming de mídia geral**.

    ![Streaming selecionado](./media/cdn-media-streaming-optimization/02_Creating.png) 
 
Depois de criar o ponto de extremidade hello, ela se aplica a otimização Olá para todos os arquivos que correspondem a certos critérios. Olá seção a seguir descreve esse processo. 
 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-akamai"></a>Otimizações para hello Azure rede de entrega de conteúdo do Akamai o streaming de mídia
 
A otimização de streaming de mídia da Akamai é eficaz para mídia de streaming de vídeo ao vivo ou de vídeo por demanda que usa fragmentos de mídia individuais para distribuição. Esse processo é diferente de um único ativo grande transferido por meio de download progressivo ou usando solicitações de intervalo de bytes. Para obter informações sobre esse estilo de distribuição de mídia, consulte [Otimização de arquivos grandes](cdn-large-file-optimization.md).


Olá geral vídeo sob demanda ou entrega de mídia entrega otimização tipos de mídia utilizam um CDN com ativos de mídia toodeliver otimizações de back-end mais rápido. Eles também usam configurações de ativos de mídia baseadas nas melhores práticas aprendidas ao longo do tempo.

### <a name="caching"></a>Cache

Se hello Azure rede de entrega de conteúdo do Akamai detectar que esse ativo Olá é um manifesto de streaming ou fragmento, ele usa diferentes tempos de expiração de cache de entrega da web geral. (Consulte a lista completa Olá Olá a tabela a seguir.) Como sempre, o cache-control ou expira enviada da origem de saudação é respeitadas. Se o ativo de saudação não é um ativo de mídia, ele armazena em cache usando os tempos de expiração Olá para a entrega da web geral.

tempo de cache negativo curto saudação é útil para descarregamento de origem quando muitos usuários solicitam um fragmento que ainda não existe. Um exemplo é um fluxo ao vivo, onde os pacotes de saudação não estão disponíveis da origem Olá esse segundo. intervalo de cache mais saudação também ajuda a aliviar solicitações de origem Olá porque o conteúdo de vídeo normalmente não é modificado.
 

|    | Geral<br> web<br>entrega contínua | Geral<br> mídia<br> streaming | Vídeo por demanda <br>mídia<br> streaming  
--- | --- | --- | ---
Cache: Positivo <br> HTTP 200, 203, 300, <br> 301, 302 e 410 | 7 dias |365 dias | 365 dias   
Cache: Negativo <br> HTTP 204, 305, 404, <br> e 405 | Nenhum | 1 segundo | 1 segundo
 
### <a name="deal-with-origin-failure"></a>Lidar com falhas de origem  

A distribuição de mídia geral e a distribuição de mídia de vídeo por demanda também têm um tempo limite de origem e um log de repetição baseados nas melhores práticas para padrões de solicitação típicos. Por exemplo, porque a entrega de mídia geral destina-se ao vivo e entrega de mídia de vídeo sob demanda, ele usa um tempo limite de conexão mais curto devido a natureza de detecção de hora toohello da transmissão ao vivo.

Quando uma conexão for interrompida, Olá CDN repete várias vezes antes de enviar um erro "504 - tempo limite do Gateway" toohello ao cliente. 

Quando um arquivo corresponde a lista de condições Olá arquivo tipo e tamanho, Olá CDN usa comportamento Olá para streaming de mídia. Caso contrário, ela usa a distribuição na Web geral.
   
### <a name="conditions-for-media-streaming-optimization"></a>Condições para otimização de streaming de mídia 

Olá, a tabela a seguir lista o conjunto de saudação de critérios toobe satisfeito para otimização de streaming de mídia: 
 
Tipos de streaming com suporte | Extensões de arquivo  
--- | ---  
HLS da Apple | m3u8, m3u, m3ub, key, ts, aac
HDS da Adobe | f4m, f4x, drmmeta, bootstrap, f4f,<br>Estrutura de URL Seg-Frag <br> (expressão regular correspondente: ^(/.*)Seq(\d+)-Frag(\d+)
DASH | mpd, dash, divx, ismv, m4s, m4v, mp4, mp4v, <br> sidx, webm, mp4a, m4a, isma
Streaming suave | /manifest/,/QualityLevels/Fragments/
  

 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-verizon"></a>Otimizações para hello Azure rede de entrega de conteúdo da Verizon o streaming de mídia

Olá rede de entrega de conteúdo do Azure da Verizon entrega ativos de mídia de streaming diretamente usando o tipo de otimização de entrega Olá web geral. Alguns recursos em Olá CDN ajudar diretamente no fornecimento de ativos de mídia por padrão.

### <a name="partial-cache-sharing"></a>Compartilhamento de cache parcial

Compartilhamento de cache parcial permite que solicitações de conteúdo toonew Olá CDN tooserve parcialmente em cache. Por exemplo, se toohello de solicitação primeiro Olá CDN resulta em um erro de cache, solicitação de saudação é enviada toohello origem. Embora esse conteúdo incompleto é carregado no hello cache CDN, toohello outras solicitações CDN pode começar a obter esses dados. 

### <a name="cache-fill-wait-time"></a>Tempo de espera de preenchimento do cache

 recurso de tempo de espera do preenchimento de cache Olá força toohold de servidor de borda Olá as solicitações subsequentes para Olá mesmo recurso até que a resposta HTTP cabeçalhos chegam do servidor de origem de saudação. Se os cabeçalhos de resposta HTTP da origem Olá chegarem antes Olá timer expira, todas as solicitações que foram colocadas em espera são atendidas fora Olá aumentando o cache. A saudação mesmo momento, hello cache é preenchido por dados de origem de saudação. Por padrão, o tempo de espera de preenchimento de cache de saudação é definido too3, 000 milissegundos. 

