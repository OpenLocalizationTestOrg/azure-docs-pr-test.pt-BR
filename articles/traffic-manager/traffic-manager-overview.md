---
title: "aaaWhat é o Gerenciador de tráfego | Microsoft Docs"
description: "Este artigo o ajudará a entender o que é o Gerenciador de tráfego e se está opção de roteamento de tráfego direita Olá para seu aplicativo"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 8e63ed11cdcdc03ae9cd28f88f0d1f9dc2cd44ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-traffic-manager"></a>Visão Geral do Gerenciador de Tráfego

O Microsoft Azure Traffic Manager permite que você toocontrol distribuição de saudação do tráfego do usuário para pontos de extremidade de serviço em data centers diferentes. Os pontos de extremidade de serviço com suporte no Gerenciador de Tráfego incluem VMs do Azure, Aplicativos Web e serviços de nuvem. Você também pode usar o Gerenciador de Tráfego com pontos de extremidade externos e não do Azure.

O Traffic Manager usa Olá sistema de nome de domínio (DNS) toodirect cliente solicitações toohello mais apropriado ponto de extremidade com base em um método de roteamento de tráfego e integridade de saudação de pontos de extremidade de saudação. O Traffic Manager fornece uma variedade de [métodos de roteamento de tráfego](traffic-manager-routing-methods.md) e [opções de monitoramento de ponto de extremidade](traffic-manager-monitoring.md) aplicativo diferente toosuit necessidades e modelos de failover automático. Gerenciador de tráfego é toofailure resiliente, incluindo Olá falha de toda a uma região do Azure.

## <a name="traffic-manager-benefits"></a>Benefícios do Gerenciador de Tráfego

O Gerenciador de Tráfego pode ajudá-lo a:

* **Aumentar a disponibilidade de aplicativos críticos**

    O Gerenciador de Tráfego fornece alta disponibilidade para seus aplicativos monitorando seus pontos de extremidade e fornecendo failover automático quando um ponto de extremidade fica inativo.

* **Melhora a capacidade de resposta de aplicativos de alto desempenho**

    Azure permite que você toorun os serviços de nuvem ou sites em data centers espalhados Olá, mundo. Gerenciador de tráfego melhora a capacidade de resposta do aplicativo, direcionando o ponto de extremidade do tráfego toohello com menor latência de rede Olá para cliente hello.

* **Realizar manutenção de serviço sem tempo de inatividade**

    Você pode executar operações de manutenção planejada em seus aplicativos sem tempo de inatividade. Traffic Manager direciona os pontos de extremidade do tráfego tooalternative enquanto manutenção hello está em andamento.

* **Combinar aplicativos baseados em nuvem e locais**

    Traffic Manager suporta externo, pontos de extremidade do Azure não habilitá-la toobe usado com híbrido de nuvem e local implantações, incluindo hello "expandir para nuvem," "migrar para a nuvem," e cenários de "failover para nuvem".

* **Distribuir o tráfego para implantações grandes e complexas**

    Usando [aninhados perfis do Traffic Manager](traffic-manager-nested-profiles.md), métodos de roteamento de tráfego podem ser combinado toocreate sofisticados e precisa de saudação do toosupport regras flexíveis de implantações maiores e mais complexas.

## <a name="how-traffic-manager-works"></a>Como funciona o Gerenciador de Tráfego

O Azure Traffic Manager permite que você toocontrol distribuição de saudação do tráfego em seus pontos de extremidade do aplicativo. Um ponto de extremidade é qualquer serviço para a Internet hospedado dentro ou fora do Azure.

O Gerenciador de Tráfego oferece dois benefícios principais:

1. Distribuição do tráfego de acordo com o tooone de várias [métodos de roteamento de tráfego](traffic-manager-routing-methods.md)
2. [Monitoramento contínuo de integridade do ponto de extremidade](traffic-manager-monitoring.md) e failover automático quando os pontos de extremidade falharem

Quando um cliente tenta tooconnect tooa serviço, ele precisa primeiro resolver nome DNS Olá Olá tooan IP do endereço do serviço. cliente Hello, em seguida, conecta-se o serviço de saudação do toothat IP endereço tooaccess.

**Olá toounderstand de ponto mais importante é que o Traffic Manager funciona no nível DNS hello.**  Pontos de extremidade com base nas regras de saudação do método de roteamento de tráfego de saudação do serviço do Traffic Manager usa DNS toodirect clientes toospecific. Os clientes se conectam a ponto de extremidade toohello selecionado **diretamente**. O Gerenciador de Tráfego não é um proxy nem um gateway. Gerenciador de tráfego não vê tráfego Olá entre cliente hello e serviço de saudação.

### <a name="traffic-manager-example"></a>Exemplo de Gerenciador de Tráfego

A Contoso Corp desenvolveu um novo portal de parceiros. saudação URL para este portal é https://partners.contoso.com/login.aspx. aplicativo Hello é hospedado em três regiões do Azure. disponibilidade de tooimprove e maximizar o desempenho global, eles usam o Gerenciador de tráfego toodistribute cliente tráfego toohello mais próximo ponto de extremidade disponível.

tooachieve essa configuração, concluírem Olá etapas a seguir:

1. Implantam três instâncias de seu serviço. nomes DNS Olá dessas implantações são 'contoso-us.cloudapp .net', '.net eu.cloudapp contoso' e 'contoso-asia.cloudapp .net'.
2. Criar um perfil do Gerenciador de tráfego, chamado 'contoso.trafficmanager.net' e configurá-lo em método de saudação roteamento de tráfego 'Desempenho' toouse entre pontos de extremidade Olá três.
* Configurar seu nome de domínio banido, 'partners.contoso.com', toopoint too'contoso.trafficmanager.net', usando um registro DNS CNAME.

![Configuração DNS do Gerenciador de Tráfego][1]

> [!NOTE]
> Ao usar um domínio banido com o Azure Traffic Manager, você deve usar um CNAME toopoint seu nome de domínio banido domínio nome tooyour Gerenciador de tráfego. Padrões de DNS não permitem que você toocreate um CNAME no hello 'ápice' (ou raiz) de um domínio. Portanto, não é possível criar um CNAME para “contoso.com” (às vezes chamado de domínio raiz). Você só pode criar um CNAME para um domínio em “contoso.com”, como “www.contoso.com”. toowork com essa limitação, recomendamos o uso de uma simples solicitações de toodirect de redirecionamento HTTP para o nome alternativo do tooan 'contoso.com' como 'www.contoso.com'.

### <a name="how-clients-connect-using-traffic-manager"></a>Como os clientes se conectam usando o Gerenciador de Tráfego

Continuar do exemplo anterior de hello, quando um cliente solicita Olá página https://partners.contoso.com/login.aspx, o cliente Olá executa Olá após o nome DNS etapas tooresolve Olá e estabelecer uma conexão:

![Estabelecimento de conexão usando o Gerenciador de Tráfego][2]

1. cliente Olá envia DNS consulta tooits configurado recursiva DNS serviço tooresolve Olá nome 'partners.contoso.com'. Um serviço DNS recursivo, às vezes chamado de serviço “DNS local”, não hospeda domínios DNS diretamente. Em vez disso, o cliente Olá suaviza trabalho Olá de entrar em contato com o hello DNS autoritativos vários dos serviços entre Olá Internet necessário tooresolve um nome DNS.
2. nome DNS Olá tooresolve, serviço DNS recursivo Olá localiza servidores de nome de saudação para domínio de 'contoso.com' hello. Ele então contata os registro DNS do nome de servidores toorequest Olá 'partners.contoso.com'. os servidores DNS de contoso.com Olá retornam registro CNAME Olá pontos toocontoso.trafficmanager.net.
3. Em seguida, serviço DNS recursivo Olá localiza servidores de nome Olá para domínio de 'trafficmanager.net' hello, que são fornecidas por hello Azure Traffic Manager service. Ele então envia uma solicitação para Olá 'contoso.trafficmanager.net' DNS registro toothose servidores DNS.
4. servidores de nome do Gerenciador de tráfego Olá recebem a solicitação de saudação. Eles escolhem um ponto de extremidade que se baseia:

    - estado de saudação configurado de cada ponto de extremidade (pontos de extremidade desabilitados não são retornados)
    - verificações de integridade atual de saudação de cada ponto de extremidade, conforme determinado pela integridade de Gerenciador de tráfego de saudação. Para obter mais informações, consulte [Monitoramento do Ponto de Extremidade do Gerenciador de Tráfego](traffic-manager-monitoring.md).
    - Olá escolhido o método de roteamento de tráfego. Para obter mais informações, consulte [Métodos de roteamento de tráfego do Gerenciador de Tráfego](traffic-manager-routing-methods.md).

5. ponto de extremidade Olá escolhido é retornado como outro registro de DNS CNAME. Nesse caso, vamos supor que contoso-us.cloudapp.net seja retornado.
6. Em seguida, serviço DNS recursivo Olá localiza servidores de nome Olá para o domínio de 'cloudapp.net' hello. Ele entra em contato com esses Olá de toorequest de servidores de nome 'contoso-us.cloudapp .net' registro de DNS. Um registro DNS 'A' que contém o endereço IP de saudação do ponto de extremidade de serviço com base nos EUA Olá é retornado.
7. serviço DNS recursivo Olá consolida resultados hello e retorna um único cliente toohello de resposta DNS.
8. cliente Olá recebe os resultados de DNS hello e conecta toohello recebe o endereço IP. Olá cliente se conecta o ponto de extremidade de serviço de aplicativo toohello diretamente, não pelo Gerenciador de tráfego. Como é um ponto de extremidade HTTPS, cliente Olá executa handshake TLS/SSL necessário hello e, em seguida, faz uma solicitação HTTP GET para Olá ' / aspx ' página.

serviço DNS recursivo Olá armazena em cache as respostas DNS Olá recebe. resolvedor de DNS Olá no dispositivo de cliente Olá também armazena em cache os resultados de saudação. O cache permite que toobe de consultas DNS subsequente respondida mais rapidamente usando dados do cache de saudação em vez de consultar outros servidores de nomes. duração de saudação do cache de saudação é determinada pela propriedade de (vida útil TTL) 'time-to-live' hello de cada registro DNS. Valores menores resultam em mais rápida expiração de cache e, portanto, mais ciclos toohello Traffic Manager servidores de nome. Valores maiores significam que pode levar mais tráfego toodirect fora de um ponto de extremidade com falha. O Traffic Manager permite tooconfigure Olá TTL usado no DNS do Traffic Manager respostas toobe tão baixo quanto 0 segundos e de até 2.147.483.647 segundos (Olá intervalo máximo compatível com [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt)), permitindo que você toochoose valor de saudação que equilibra melhor as necessidades de saudação do seu aplicativo.

## <a name="pricing"></a>Preços

Para obter informações sobre preço, consulte [Preços do Gerenciador de Tráfego](https://azure.microsoft.com/pricing/details/traffic-manager/).

## <a name="faq"></a>Perguntas frequentes

Para conferir as perguntas frequentes sobre o Gerenciador de Tráfego, confira [Perguntas frequentes sobre o Gerenciador de Tráfego](traffic-manager-FAQs.md)

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre o [failover automático e monitoramento do ponto de extremidade](traffic-manager-monitoring.md)do Gerenciador de Tráfego.

Saiba mais sobre os [métodos de roteamento de tráfego](traffic-manager-routing-methods.md)do Gerenciador de Tráfego.

Saiba mais sobre alguns dos Olá outra chave [recursos de rede](../networking/networking-overview.md) do Azure.

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png

