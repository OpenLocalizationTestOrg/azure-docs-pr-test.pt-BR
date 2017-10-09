---
title: "aaaDynamic aceleração do Site por meio do Azure CDN"
description: "Aprofundamento em aceleração de site dinâmico"
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
ms.date: 08/02/2017
ms.author: v-semcev
ms.openlocfilehash: 37e6312ae5e83448f2d87c95ef48c387355748bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a>Aceleração de site dinâmica por meio da Azure CDN

Com a explosão de saudação de mídia social, comércio eletrônico e Olá web hyper personalizada, uma porcentagem aumenta rápido do hello conteúdo servida tooend usuários é gerada em tempo real. Os usuários esperam experiências na Web rápidas, confiáveis e personalizadas, independentemente do seu navegador, localização, dispositivo ou rede. No entanto, Olá muito que tornam essas experiências assim envolvendo também reduzir downloads de página e inovações colocam em risco a qualidade de saudação da experiência do consumidor de saudação. 

Recurso CDN padrão inclui Olá capacidade toocache arquivos mais tooend usuários toospeed a entrega de arquivos estáticos. No entanto, com aplicativos web dinâmicos, armazenamento em cache o conteúdo em locais de borda não é possível porque o servidor de saudação gera conteúdo Olá no comportamento de toouser de resposta. Acelerar o fornecimento de saudação de tal conteúdo é mais complexo do que o cache de borda tradicional e exige uma solução de ponta a ponta que ajusta bem cada elemento do caminho Olá todo o data de início toodelivery. Com o Azure CDN dinâmico Site aceleração DSA (), o desempenho de saudação de páginas da web com conteúdo dinâmico, é aprimorado.

Azure CDN do Akamai e Verizon oferece otimização DSA por meio de saudação **otimizado para** menu durante a criação do ponto de extremidade.

## <a name="configuring-cdn-endpoint-tooaccelerate-delivery-of-dynamic-files"></a>Configurando a entrega de tooaccelerate de ponto de extremidade CDN de arquivos dinâmicos

Você pode configurar o fornecimento de toooptimize de ponto de extremidade CDN de arquivos dinâmicos por meio do portal do Azure, selecionando Olá **aceleração de site dinâmico** opção em Olá **otimizado para** seleção de propriedade durante criação de ponto de extremidade de saudação. Você também pode usar nossas APIs REST ou qualquer toodo de SDKs de cliente Olá Olá mesmo programaticamente. 

### <a name="probe-path"></a>Caminho de investigação
Caminho de investigação é um tooDynamic específico do recurso aceleração de Site e válido é necessário para a criação. DSA usa um pequeno *caminho de investigação* arquivo colocado em Olá origem toooptimize roteamento configurações de rede para Olá CDN. Você pode baixar e carregar nosso site de tooyour do arquivo de exemplo ou use um ativo existente em sua origem que é aproximadamente 10 KB para o caminho de investigação de saudação em vez disso, se existir ativo hello.

> [!Note]
> A DSA incorre em encargos adicionais. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/cdn/) para obter mais informações.

Olá capturas de tela a seguir ilustra o processo de saudação por meio do portal do Azure.
 
![Adicionar um novo ponto de extremidade CDN](./media/cdn-dynamic-site-acceleration/01_Endpoint_Profile.png) 

*Figura 1: Adicionando um novo ponto de extremidade CDN da saudação perfil CDN*
 
![Criar um novo ponto de extremidade CDN com DSA](./media/cdn-dynamic-site-acceleration/02_Optimized_DSA.png)  

*Figura 2: criar um ponto de extremidade CDN com a otimização de aceleração de site dinâmico selecionada*

Depois de criar o ponto de extremidade CDN hello, ela se aplica a otimizações de DSA Olá para todos os arquivos que correspondem a certos critérios. Olá seção a seguir descreve a otimização DSA em detalhes.

## <a name="dsa-optimization-using-azure-cdn"></a>Otimização de DSA usando a CDN do Azure

A aceleração de Site dinâmico no Azure CDN acelera a entrega de ativos dinâmicos usando Olá técnicas a seguir:

-   Otimização de Rota
-   Otimizações de TCP
-   Pré-busca do objeto (somente Akamai)
-   Compactação de Imagem Móvel (somente Akamai)

### <a name="route-optimization"></a>Otimização de Rota

Otimização da rota é importante porque Olá Internet é um lugar dinâmico, onde o tráfego e temporariamente interrupções são alterados constantemente topologia de rede de saudação. Olá Border Gateway Protocol (BGP) é o protocolo de roteamento de saudação de saudação à Internet, mas pode haver mais rápidas rotas por meio de servidores de ponto de presença (PoP) intermediários. 

Otimização da rota escolhe a origem da saudação melhor caminho toohello para que um site é continuamente conteúdo dinâmico e acessível é entregue tooend usuários por meio de hello mais rápido e mais confiável rota possíveis. 

rede do Akamai Olá usa dados em tempo real de toocollect técnicas e comparar vários caminhos em nós diferentes no servidor do Akamai hello, bem como roteamento BGP saudação padrão em Olá abra Internet toodetermine hello mais rápida rota entre origem hello e hello Borda da CDN. Essas técnicas evitam pontos de congestionamento da Internet e rotas longas. 

Da mesma forma, os usos de rede Verizon Olá uma combinação de Anycast DNS, de alta capacidade suporte PoPs e verificações de integridade, toodetermine Olá melhor gateways toobest dados de rota do hello origem do cliente toohello.
 
Como resultado, o conteúdo totalmente dinâmico e transacional é entregue mais rápida e mais confiável tooend usuários, mesmo quando ele é uncacheable. 

### <a name="tcp-optimizations"></a>Otimizações de TCP

Protocolo de controle de transmissão (TCP) é o padrão de saudação do conjunto de protocolos de Internet Olá usado toodeliver informações entre os aplicativos em uma rede IP.  Por padrão, há vários back e sucessivamente solicitações necessário tooset a uma conexão TCP, além de tooavoid congestions de rede limites, o que resulta em ineficiências em escala. A CDN do Azure da Akamai lida com esse problema otimizando em três áreas: 

 - eliminar o início lento
 - aproveitar as conexões persistentes
 - ajustar parâmetros de pacote TCP (somente Akamai)

#### <a name="eliminating-slow-start"></a>Eliminar o início lento

*Lenta início* faz parte do protocolo TCP Olá que impede o congestionamento de rede, limitando a quantidade de saudação de dados enviados pela rede hello. Ele começa com tamanhos de janela de congestionamento pequeno entre remetente e destinatário até Olá máximo for atingido ou perda de pacotes é detectada.

A CDN do Azure da Akamai e da Verizon elimina o início lento em três etapas:

1.  Rede Akamai e da Verizon usar largura de banda toomeasure largura de banda de saudação de conexões entre os servidores de borda PoP de monitoramento e integridade.
2. métricas de saudação são compartilhadas entre os servidores de borda PoP para que cada servidor está ciente das condições da rede hello e integridade do servidor de Olá outros PoPs ao redor deles.  
3. os servidores de borda CDN Olá agora são toomake capaz de suposições sobre alguns parâmetros de transmissão, como o tamanho da janela ideal Olá deve ser ao se comunicar com outros servidores de borda da CDN seu próximo. Esta etapa significa que tamanho da janela Olá congestionamento inicial pode ser aumentado se integridade Olá de conexão Olá entre servidores de borda CDN Olá é capaz de transferências de dados de pacote maior.  

#### <a name="leveraging-persistent-connections"></a>Aproveitar as conexões persistentes

Menos de máquinas exclusivas usando um CDN, se conectar a servidor de origem tooyour diretamente em comparação com usuários que se conectam diretamente tooyour origem. Azure CDN do Akamai e Verizon também pools tooestablish juntos de solicitações de usuário menos conexões com origens hello.

Como mencionado anteriormente, conexões TCP fazem várias solicitações de e para trás em um handshake tooestablish uma nova conexão. Conexões persistentes, também conhecido como "Keep-Alive de HTTP," reutilizar conexões TCP existentes para vários HTTP solicitações toosave ida e acelerar a entrega. 

rede de Verizon Olá também envia pacotes keep-alive periódicas pela Olá TCP conexão tooprevent uma conexão aberta seja fechada.

#### <a name="tuning-tcp-packet-parameters"></a>Ajustar parâmetros de pacote TCP

Azure CDN do Akamai também ajusta os parâmetros de saudação que controlam as conexões de servidor para servidor e reduz Olá duráveis round viagens necessárias tooretrieve conteúdo incorporado no site hello usando Olá técnicas a seguir:

1.  Aumentar a janela de congestionamento inicial Olá para que mais pacotes podem ser enviados sem esperar uma confirmação.
2.  Diminuindo o tempo limite de retransmissão inicial Olá para que uma perda é detectada e retransmissão ocorre mais rapidamente.
3.  Tempo limite de tooreduce Olá espera antes de assumir que pacotes foram perdidos durante a transmissão de retransmissão decrescente Olá mínimo e o máximo.

### <a name="object-prefetch-akamai-only"></a>Pré-busca do objeto (somente Akamai)

A maioria dos sites consistem em uma página HTML que faz referência a vários outros recursos, tais como imagens e scripts. Normalmente, quando um cliente solicita uma página da Web, Olá navegador primeiro baixa e analisa Olá HTML objeto e, em seguida, faz solicitações adicionais ativos toolinked toofully necessário carregar a página de saudação. 

*Pré-busca* é uma técnica tooretrieve imagens e scripts incorporados Olá página HTML enquanto hello HTML é servido toohello navegador e antes de saudação do navegador ainda faz a essas solicitações do objeto. 

Com hello **pré-buscar** opção ativada em tempo de saudação quando Olá CDN serve o navegador do cliente de toohello para a página de base Olá HTML, Olá CDN analisa o arquivo hello HTML e fazer solicitações adicionais para os recursos vinculados e armazená-lo em seu cache. Quando hello cliente faz solicitações Olá Olá vinculado ativos, servidor de borda CDN Olá já tem Olá objetos solicitados e pode servi-los imediatamente sem uma origem de toohello de ida e volta. Essa otimização beneficiará tanto o conteúdo armazenável em cache quanto o não armazenável em cache.

### <a name="adaptive-image-compression-akamai-only"></a>Compactação de Imagem Adaptável (somente Akamai)

Alguns dispositivos, especialmente aqueles móveis, experiência velocidades de rede de tootime de tempo. Nesses cenários, é mais útil para imagens menores de saudação usuário tooreceive em sua página da Web mais rapidamente, em vez de esperar muito tempo para imagens de alta resolução.

Esse recurso automaticamente monitora a qualidade da rede e utiliza métodos padrão de compactação de JPEG quando velocidades de rede são tempo de entrega tooimprove mais lento.

Compactação de imagem adaptável | Extensões de arquivo  
--- | ---  
Compactação JPEG | .jpg, .jpeg, .jpe, .jig, .jgig, .jgi

## <a name="caching"></a>Cache

Com o DSA, cache é desativado por padrão em Olá CDN, mesmo quando a origem de saudação inclui cabeçalhos de controle de cache/expira em resposta hello. Esse padrão foi desativada porque DSA é normalmente usado para dinâmicos ativos que não devem ter cache já que eles são exclusivos tooeach cliente e Ativar cache por padrão pode interromper esse comportamento.

Se você tiver um site com uma mistura de ativos estáticos e dinâmicos, é melhor tootake um híbrido abordagem tooget Olá melhor desempenho. 

Se você estiver usando ADN com Verizon Premium, você pode ativar novamente o cache para casos específicos usando o mecanismo de regras de saudação.  

Uma alternativa é toouse dois pontos de extremidade CDN. Com recursos dinâmicos de toodeliver DSA e outro ponto de extremidade com uma otimização estáticas tipo, como geral distribuição da web, ativos armazenável toodelivery. Tooaccomplish ordem nesse alternativo, você modificará o toolink de URLs de página da Web diretamente, ativo toohello Olá ponto de extremidade CDN planejar toouse. 

Por exemplo: `mydynamic.azureedge.net/index.html` é uma página dinâmica e é carregado do ponto de extremidade do hello DSA.  Olá página html faz referência a vários ativos estáticos como bibliotecas JavaScript ou imagens que são carregadas de Olá ponto de extremidade CDN estático, como `mystatic.azureedge.net/banner.jpg` e `mystatic.azureedge.net/scripts.js`. 

Você pode encontrar um exemplo [aqui](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller) em como controladores toouse uma ASP.NET web conteúdo tooserve do aplicativo por meio de uma URL específica da CDN.




