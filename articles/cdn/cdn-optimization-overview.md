---
title: "fornecimento de conteúdo do Azure para seu cenário de aaaOptimize"
description: "Como toooptimize entrega do conteúdo para cenários específicos"
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
ms.openlocfilehash: 922a92fdbf7e6e21f2b5ae9a2fb4ac32735fc15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a>Otimizar a distribuição de conteúdo do Azure para seu cenário

Quando você entregar conteúdo tooa grande público global, é entrega de saudação otimizada tooensure crítico do seu conteúdo. Hello Azure Content Delivery Network pode otimizar a experiência de entrega de saudação com base no tipo de saudação do conteúdo que você tem. O conteúdo pode ser um site, uma transmissão ao vivo, um vídeo ou um arquivo grande para download. Quando você cria um ponto de extremidade CDN (rede) de fornecimento de conteúdo, você especificar um cenário em Olá **otimizado para** opção. Sua escolha determina quais otimização é aplicado toohello conteúdo distribuído do ponto de extremidade CDN hello.

Opções de otimização são desempenho de fornecimento de conteúdo de tooimprove toouse projetado comportamentos de práticas recomendadas e descarregamento de origem melhor. Suas escolhas de cenário afetam o desempenho, modificando as configurações para cache parcial, o agrupamento de objeto e política de repetição de falha de origem hello. 

Este artigo fornece uma visão geral dos diversos recursos de otimização e quando eles devem ser usados. Para obter mais informações sobre os recursos e limitações, consulte os artigos de respectivos de saudação em cada tipo de otimização individuais.

> [!NOTE]
> O **otimizado para** opções podem variar com base no provedor de saudação selecionado. Provedores CDN aplicam o aprimoramento de maneiras diferentes, dependendo do cenário de saudação. 

## <a name="provider-options"></a>Opções de provedor

Olá rede de fornecimento de conteúdo do Azure do Akamai dá suporte a:

* Distribuição na Web geral 

* Streaming de mídia geral

* Streaming de mídia de vídeo por demanda

* Download de arquivos grandes

* Aceleração de site dinâmica 

Olá rede de entrega de conteúdo do Azure da Verizon oferece suporte somente a entrega da web geral. Ela pode ser usada para vídeo por demanda e download de arquivos grandes. Você não tem um tipo de otimização para tooselect.

É altamente recomendável que você teste as variações de desempenho entre o provedor ideal de diferentes provedores tooselect Olá para a entrega.

## <a name="select-and-configure-optimization-types"></a>Selecionar e configurar os tipos de otimização

toocreate um novo ponto de extremidade, selecione um tipo de otimização que melhor corresponde ao cenário de saudação e tipo de conteúdo que você deseja Olá toodeliver de ponto de extremidade. **Entrega geral web** é a seleção padrão de saudação. Você pode atualizar a opção de otimização Olá para qualquer ponto de extremidade do Akamai existente a qualquer momento. Essa alteração não interrompe a entrega de saudação CDN. 

1. Selecione um ponto de extremidade em um perfil Standard da Akamai.

    ![Seleção de ponto de extremidade ](./media/cdn-optimization-overview/01_Akamai.png)

2. Em **CONFIGURAÇÕES**, selecione **Otimização**. Em seguida, selecione um tipo de saudação **otimizado para** lista suspensa.

    ![Otimização e seleção de tipo](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a>Otimização para cenários específicos

Você pode otimizar o ponto de extremidade do hello CDN para um dos seguintes cenários de saudação. 

### <a name="general-web-delivery"></a>Distribuição na Web geral

Entrega geral web é a opção de otimização mais comuns de saudação. Ela foi projetada para otimização de conteúdo da Web geral, como páginas da Web e aplicativos Web. Essa otimização também pode ser usada para downloads de arquivo e vídeo.

Um site típico contém conteúdo estático e dinâmico. Conteúdo estático inclui imagens, bibliotecas JavaScript e folhas de estilo que podem ser armazenado em cache e entregue toodifferent usuários. Conteúdo dinâmico é personalizado para um usuário individual, como itens de notícias são ajustadas tooa perfil de usuário. Conteúdo dinâmico não está armazenada em cache porque ele é o usuário tooeach exclusivo, como o conteúdo do carrinho de compras. A distribuição na Web geral pode otimizar todo o site. 

> [!NOTE]
> Se você usar o hello Azure rede de entrega de conteúdo do Akamai, convém toouse essa otimização se o tamanho médio de arquivos for menor do que 10 MB. Se o tamanho médio de arquivo é maior que 10 MB, selecione **download de arquivo grande** de saudação **otimizado para** lista suspensa.

### <a name="general-media-streaming"></a>Streaming de mídia geral

Se precisar de ponto de extremidade toouse Olá para transmissão ao vivo e streaming de vídeo sob demanda, é recomendável geral otimização de streaming de mídia.

Streaming de mídia é tempo confidencial, como os pacotes que chegam tarde no cliente Olá podem causar uma experiência de exibição degradada, como buffer frequentes de conteúdo de vídeo. Otimização de streaming de mídia reduz a latência de saudação do fornecimento de conteúdo de mídia e fornece uma experiência de streaming suave para os usuários. 

Esse cenário é comum para clientes do serviço de mídia do Azure. Quando você usa os serviços de mídia do Azure, você pode obter um ponto de extremidade de streaming, que pode ser usado para streaming sob demanda e ao vivo. Com esse cenário, os clientes não é necessário o ponto de extremidade do tooswitch tooanother quando eles mudam de streaming ao vivo tooon por demanda. A otimização de streaming de mídia geral dá suporte a esse tipo de cenário.

Hello Azure Content Delivery Network da Verizon usa Olá web geral entrega otimização tipo toodeliver streaming conteúdo de mídia.

toolearn mais sobre a otimização, o streaming de mídia consulte [otimização de streaming de mídia](cdn-media-streaming-optimization.md).

### <a name="video-on-demand-media-streaming"></a>Streaming de mídia de vídeo por demanda

A otimização de streaming de mídia de vídeo por demanda melhora o conteúdo de streaming de vídeo por demanda. Se você usar um ponto de extremidade de streaming de vídeo sob demanda, você poderá toouse essa opção.

Hello Azure Content Delivery Network da Verizon usa Olá web geral entrega otimização tipo toodeliver streaming conteúdo de mídia.

toolearn mais sobre a otimização, o streaming de mídia consulte [otimização de streaming de mídia](cdn-media-streaming-optimization.md).

> [!NOTE]
> Se o ponto de extremidade Olá serve principalmente o conteúdo de vídeo sob demanda, use este tipo de otimização. Olá principal diferença entre essa otimização e otimização de streaming de mídia geral Olá é tempo limite de repetição de conexão hello. tempo limite de saudação é muito mais curto toowork com cenários de streaming ao vivo.

### <a name="large-file-download"></a>Download de arquivos grandes

Se você usar o hello Azure rede de entrega de conteúdo do Akamai, você deve usar arquivos de toodeliver de download de grandes arquivos maiores do que 1,8 GB. Olá rede de entrega de conteúdo do Azure da Verizon não tem uma limitação no arquivo de tamanho na otimização de entrega da web geral do download.

Se você usar o hello Azure Content Delivery Network do Akamai, downloads de arquivos grandes são otimizados para conteúdo de mais de 10 MB. Se o tamanho médio do arquivo é menor do que 10 MB, você poderá toouse fornecimento de web geral. Se os tamanhos de arquivos médio são consistentemente maiores que 10 MB, talvez seja mais eficiente toocreate um ponto de extremidade separado para arquivos grandes. Por exemplo, atualizações de firmware ou software geralmente são arquivos grandes.

Hello Azure Content Delivery Network da Verizon usa Olá web geral entrega otimização tipo toodeliver streaming conteúdo de mídia.

toolearn mais sobre a otimização de arquivos grandes, consulte [otimização de arquivo grande](cdn-large-file-optimization.md).

### <a name="dynamic-site-acceleration"></a>Aceleração de site dinâmica

 A aceleração de site dinâmica está disponível nos perfis da Rede de Distribuição de Conteúdo da Akamai e da Verizon. Essa otimização envolve toouse uma taxa adicional. Para obter mais informações, consulte Olá página de preços.

Aceleração de site dinâmico inclui várias técnicas que se beneficiam de latência de saudação e o desempenho de conteúdo dinâmico. As técnicas incluem otimização de rota e de rede, otimização de TCP e muito mais. 

Você pode usar este tooaccelerate otimização um aplicativo web que inclui várias respostas que não são armazenável em cache. Entre os exemplos estão resultados da pesquisa, transações de check-out ou dados em tempo real. Você pode continuar toouse core CDN recursos de cache para dados estáticos. 



