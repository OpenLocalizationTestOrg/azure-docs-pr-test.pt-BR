---
title: "Considerações sobre a topologia aaaNetwork ao usar o Proxy de aplicativo do Azure Active Directory | Microsoft Docs"
description: "Cobre as considerações de topologia de rede ao usar o Proxy de Aplicativo do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a>Considerações de topologia de rede ao usar o Proxy de Aplicativo do Azure Active Directory

Este artigo explica as considerações de topologia de rede ao usar o Proxy de Aplicativo do Azure AD (Azure Active Directory) para publicar e acessar seus aplicativos remotamente.

## <a name="traffic-flow"></a>Fluxo de tráfego

Quando um aplicativo é publicado por meio do Proxy de aplicativo do Azure AD, o tráfego de aplicativos de toohello usuários Olá flui três conexões:

1. usuário Olá conecta toohello Proxy de aplicativo do Azure AD serviço ponto de extremidade público no Azure
2. Olá serviço Proxy de aplicativo se conecta toohello conector de Proxy de aplicativo
3. conector de Proxy de aplicativo Hello conecta-se o aplicativo de destino toohello

![Diagrama mostrando o fluxo de tráfego de aplicativo do usuário tootarget](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a>Local do locatário e serviço Proxy de Aplicativo

Quando você se inscrever para um locatário Azure AD, região de saudação do seu locatário é determinado pelo país Olá que você especificar. Quando você habilita o Proxy de aplicativo, instâncias de serviço de Proxy de aplicativo hello para seu locatário são escolhidas ou criadas no hello mesmo região do seu locatário do Azure AD ou Olá tooit de região mais próximo.

Por exemplo, se a região do seu locatário AD do Azure é hello (união), todos os conectores de Proxy de aplicativo usam instâncias de serviço em datacenters do Azure no hello da UE. Quando seus usuários acesso de aplicativos publicados, o tráfego passa por instâncias de serviço de Proxy de aplicativo hello neste local.

## <a name="considerations-for-reducing-latency"></a>Considerações para redução da latência

Todas as soluções de proxy introduzem a latência em sua conexão de rede. Não importa qual proxy ou solução VPN que desejar como sua solução de acesso remoto, ele sempre inclui um conjunto de servidores, permitindo a saudação conexão tooinside sua rede corporativa.

As organizações geralmente incluem pontos de extremidade do servidor em sua rede de perímetro. Com o Proxy de aplicativo do AD do Azure, no entanto, o tráfego passa pelo serviço de proxy de saudação na nuvem Olá enquanto conectores Olá residem em sua rede corporativa. Nenhuma rede de perímetro é necessária.

seções a seguir Olá contêm sugestões adicionais toohelp reduzir ainda mais a latência. 

### <a name="connector-placement"></a>Posicionamento do conector

Proxy de aplicativo escolhe local Olá de instâncias para você, com base em seu local de locatário. Porém, você obterá toodecide onde tooinstall conector de hello, fornecendo Olá power toodefine Olá latência de seu tráfego de rede.

Ao configurar o serviço Proxy de aplicativo de saudação, pergunte a saudação perguntas a seguir:

* Onde o aplicativo hello está localizado?
* Onde estão a maioria dos usuários que acessam o aplicativo hello localizado?
* Onde a instância do Proxy de aplicativo hello está localizada?
* Você já tem uma rede dedicada conexão tooAzure datacenters que configurar como o Azure ExpressRoute ou VPN semelhante?

conector de saudação tem toocommunicate com o Azure e seus aplicativos (etapas 2 e 3 no diagrama de fluxo de tráfego de saudação), portanto Olá posicionamento de latência de saudação do hello conector afeta essas duas conexões. Ao avaliar o posicionamento de saudação do conector hello, lembre-Olá mente pontos a seguir:

* Se você quiser toouse restrita de Kerberos (KCD) para o logon único, o conector Olá precisa um data center tooa de linha de visão. Além disso, o servidor de conector de saudação precisa toobe integrado ao domínio.  
* Em caso de dúvida, instale o aplicativo de toohello hello conector mais próximo.

### <a name="general-approach-toominimize-latency"></a>Latência de toominimize abordagem geral

Você pode minimizar a latência de saudação do tráfego de ponta a ponta Olá otimizando a cada conexão de rede. Cada conexão pode ser otimizada com:

* Reduzindo a distância de saudação entre duas extremidades de saudação do salto hello.
* Escolhendo Olá tootraverse de rede correto. Por exemplo, percorrendo uma rede privada em vez de saudação Internet pública pode ser mais rápida, devido a toodedicated links.

Se você tiver um link dedicado de rota expressa ou VPN entre o Azure e sua rede corporativa, convém toouse que.

## <a name="focus-your-optimization-strategy"></a>Concentrar-se em sua estratégia de otimização

Não há muito que você pode fazer a conexão de saudação toocontrol entre usuários e Olá serviço Proxy de aplicativo. Os usuários podem acessar seus aplicativos de uma rede doméstica, de uma cafeteria ou de um país diferente. Em vez disso, você pode otimizar as conexões de saudação do serviço de Proxy de aplicativo hello toohello Proxy de aplicativo conectores toohello aplicativos. Considere incorporar Olá padrões em seu ambiente a seguir.

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a>Padrão de 1: Put Olá conector toohello fechar aplicativo

Local Olá conector toohello fechar aplicativo de destino na rede de cliente hello. Essa configuração minimiza a etapa 3 no diagrama de topografia hello, como aplicativos e o conector de saudação são fechar. 

Se seu conector precisa de um controlador de domínio de toohello de linha de visão, é vantajoso esse padrão. A maioria de nossos clientes usa esse padrão, porque ele funciona bem para a maioria dos cenários. Esse padrão também pode ser combinado com o tráfego de toooptimize 2 padrão entre o serviço de saudação e conector hello.

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a>Padrão 2: Aproveitar o ExpressRoute com o emparelhamento público

Se você tiver configurado com o emparelhamento público de rota expressa, você pode usar a conexão de rota expressa mais rápido Olá para o tráfego entre o Proxy de aplicativo e o conector de saudação. conector Olá ainda está na sua rede, o aplicativo fechar toohello.

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a>Padrão 3: Aproveitar o ExpressRoute com o emparelhamento privado

Se você tiver uma configuração de VPN ou ExpressRoute dedicada com emparelhamento privado entre o Azure e sua rede corporativa, terá outra opção. Nessa configuração, a rede virtual Olá no Azure geralmente é considerada uma extensão da rede corporativa hello. Então você pode instalar o conector Olá Olá datacenter do Azure e ainda atender aos requisitos de baixa latência de saudação de conexão do conector para o aplicativo hello.

A latência não é comprometida, pois o tráfego está fluindo por uma conexão dedicada. Você também obtém maior latência de conector de serviço de Proxy de aplicativo porque o conector hello está instalado em tooyour de fechar um datacenter do Azure local do locatário do AD do Azure.

![Diagrama mostrando o conector instalado em um datacenter do Azure](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a>Outras abordagens

Embora Olá foco deste artigo é a instalação, você também pode alterar posicionamento Olá características tooget latência melhor aplicativo hello.

As organizações estão cada vez mais migrando suas redes para ambientes hospedados. Isso permite tooplace seus aplicativos em um ambiente hospedado que também faz parte de sua rede corporativa e ainda estar dentro do domínio de saudação. Nesse caso, padrões Olá abordados Olá anterior seções podem ser aplicado toohello novo aplicativo local. Se você estiver considerando essa opção, consulte [Serviços de Domínio do Azure AD](../active-directory-domain-services/active-directory-ds-overview.md).

Além disso, considere a possibilidade de organizar seus conectores usando [grupos de conector](active-directory-application-proxy-connectors.md) tootarget aplicativos que estão em diferentes locais e redes. 

## <a name="common-use-cases"></a>Casos de uso comuns

Nesta seção, veremos alguns cenários comuns. Suponha que Olá locatário do Azure AD (e, portanto, o ponto de extremidade de serviço proxy) está localizado no hello United States (US). Olá considerações discutidas esses casos de uso também se aplicam a regiões tooother mundo hello.

Nesses cenários, chamamos cada conexão de um "salto" e os numeramos para uma discussão mais fácil:

- **Saltar 1**: usuário toohello serviço Proxy de aplicativo
- **Saltar 2**: conector de Proxy de aplicativo de serviço toohello de Proxy de aplicativo
- **Saltar 3**: aplicativo de destino do Proxy de aplicativo conector toohello 

### <a name="use-case-1"></a>Caso de uso 1

**Cenário:** Olá aplicativo é na rede de uma organização da saudação nós, com usuários em Olá mesma região. Nenhuma rota expressa ou VPN existe entre hello datacenter do Azure e a rede corporativa hello.

**Recomendação:** siga padrão 1, explicado na seção anterior hello. Para melhorar a latência, considere o uso do ExpressRoute, se necessário.

Este é um padrão simples. Otimizar o salto 3 colocando conector Olá próximo aplicativo hello. Isso também é uma opção natural, porque o conector Olá geralmente é instalado com a linha de visão toohello aplicativo e toohello tooperform KCD operações do data center.

![Diagrama mostrando o que os usuários, proxy, conector e aplicativo estão todos em Olá nos](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a>Caso de uso 2

**Cenário:** Olá aplicativo é na rede de uma organização da saudação nós, com usuários distribuídos globalmente. Nenhuma rota expressa ou VPN existe entre hello datacenter do Azure e a rede corporativa hello.

**Recomendação:** siga padrão 1, explicado na seção anterior hello. 

Novamente, o padrão comum de saudação é toooptimize salto 3, onde você coloca o conector Olá próximo aplicativo hello. Salto 3 não será normalmente caro, se ele for Olá todos no mesmo região. No entanto, salto 1 pode ser mais caro, dependendo de onde está o usuário hello, pois os usuários em Olá, mundo devem acessar a instância do Proxy de aplicativo hello em Olá dos EUA. Vale a pena observar que qualquer solução de proxy tem características semelhantes sobre os usuários que estão sendo distribuídos globalmente.

![Diagrama mostrando que os usuários são distribuídos globalmente, mas o aplicativo, o conector e o proxy de saudação estão em Olá dos EUA](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a>Caso de uso 3

**Cenário:** aplicativo hello é na rede de uma organização da saudação nos. Rota expressa com emparelhamento público existe entre o Azure e hello rede corporativa.

**Recomendação:** siga padrões 1 e 2, como explicado na seção anterior hello.

Primeiro, coloque o conector hello mais próximo possível toohello aplicativo. Em seguida, Olá usar ExpressRoute de salto 2. 

Se estiver usando o link de rota expressa Olá emparelhamento público, fluxos de tráfego Olá entre o proxy de saudação e conector Olá nesse link. O salto 2 tem latência otimizada.

![Diagrama mostrando a rota expressa entre o conector e o proxy Olá](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a>Caso de uso 4

**Cenário:** aplicativo hello é na rede de uma organização da saudação nos. Rota expressa com emparelhamento privado existe entre o Azure e hello rede corporativa.

**Recomendação:** siga padrão 3, explicado na seção anterior hello.

Coloca o conector de saudação em Olá datacenter do Azure que está conectada toohello a rede corporativa por meio de emparelhamento privado da rota expressa. 

conector de saudação pode ser colocado em Olá datacenter do Azure. Como conector Olá ainda tem um aplicativo de toohello de linha de visão e Olá datacenter por meio da rede privada hello, salto 3 permanece otimizado. Além disso, o salto 2 é ainda mais otimizado.

![Diagrama mostrando o conector de saudação em um datacenter do Azure e rota expressa entre o aplicativo e o conector Olá](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a>Caso de uso 5

**Cenário:** aplicativo hello é na rede de uma organização da saudação da Europa, com a instância do Proxy de aplicativo hello e a maioria dos usuários em Olá nos.

**Recomendação:** conector de saudação do local próximo aplicativo hello. Como os usuários dos EUA estão acessando uma instância do Proxy de aplicativo que acontece toobe em Olá mesma região, salto 1 não é muito caro. O salto 3 está otimizado. Considere o uso de rota expressa toooptimize salto 2. 

![Diagrama mostrando o usuários e proxy Olá dos EUA, com conector hello e aplicativo hello da Europa](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

Você também pode considerar o uso de uma outra variante nessa situação. Se a maioria dos usuários na organização Olá estiverem em Olá nós, a probabilidade é que sua rede estende toohello nos também. Colocar o conector de saudação em Olá dos EUA e use o aplicativo de toohello de linha de rede corporativa interna de hello dedicado no hello da Europa. Desta forma, os saltos 2 e 3 são otimizados.

![Diagrama mostrando os usuários, o proxy e o conector em Olá dos EUA, o aplicativo hello da Europa](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a>Próximas etapas

- [Habilitar Proxy de aplicativo](active-directory-application-proxy-enable.md)
- [Habilitar o logon único](active-directory-application-proxy-sso-using-kcd.md)
- [Habilitar o acesso condicional](active-directory-application-proxy-conditional-access.md)
- [Solucionar problemas que surgirem com o Proxy de Aplicativo](active-directory-application-proxy-troubleshoot.md)
