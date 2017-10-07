---
title: aaaConfigure uma rede Virtual para um Premium do Azure Redis Cache | Microsoft Docs
description: "Saiba como toocreate e gerenciar o suporte de rede Virtual para suas instâncias de Cache Redis do Azure Premium da camada"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8b1e43a0-a70e-41e6-8994-0ac246d8bf7f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: sdanie
ms.openlocfilehash: fab715f4d9365ee4c2f8b89d2e2e58768c25b671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-virtual-network-support-for-a-premium-azure-redis-cache"></a>Como tooconfigure dar suporte a rede Virtual para um Premium do Azure Redis Cache
Cache Redis do Azure tem diferentes ofertas de cache, que fornecem flexibilidade na escolha de saudação do tamanho do cache e recursos, incluindo recursos de camada Premium, como clustering, persistência e suporte de rede virtual. Uma rede virtual é uma rede privada na nuvem hello. Quando uma instância de Cache Redis do Azure é configurada com uma rede virtual, não é publicamente endereçável e só pode ser acessado de máquinas virtuais e aplicativos em redes de saudação. Este artigo descreve como dar suporte a rede virtual tooconfigure para uma instância de Cache Redis do Azure premium.

> [!NOTE]
> O Cache Redis do Azure dá suporte a VNets clássicas e do Resource Manager.
> 
> 

Para obter informações sobre outros recursos de cache premium, consulte [camada de Azure Redis Cache Premium Introdução toohello](cache-premium-tier-intro.md).

## <a name="why-vnet"></a>Por que a VNet?
[Rede Virtual do Azure (VNet)](https://azure.microsoft.com/services/virtual-network/) implantação oferece maior segurança e isolamento para Cache Redis do Azure, bem como as sub-redes, políticas de controle de acesso, e outros recursos toofurther restringir o acesso.

## <a name="virtual-network-support"></a>Suporte de rede virtual
Suporte de rede virtual está configurado no hello **novo Cache Redis** folha durante a criação do cache. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Depois que você tiver selecionado um preço premium, você pode configurar a integração da VNet Redis selecionando uma rede virtual que está em Olá mesma assinatura e local que o cache. toouse uma nova rede virtual, criá-lo pela primeira vez, seguindo as etapas de saudação em [criar uma rede virtual usando o portal do Azure de saudação](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) ou [criar uma rede virtual (clássica) usando o portal do Azure de saudação](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) e, em seguida, retornar toohello **Novo Cache Redis** toocreate de folha e configure seu cache premium.

Olá tooconfigure redes para seu novo cache, clique em **rede Virtual** em Olá **novo Cache Redis** folha e selecione hello desejado VNet na lista suspensa de saudação.

![Rede virtual][redis-cache-vnet]

Selecione Olá sub-rede desejado da saudação **sub-rede** suspensa lista e especificar Olá desejado **endereço IP estático**. Se você estiver usando uma saudação de rede virtual clássica **endereço IP estático** campo é opcional e, se nenhum for especificado, um deles é escolhido da sub-rede de saudação selecionada.

> [!IMPORTANT]
> Ao implantar um Gerenciador de recursos de VNet de tooa do Cache Redis do Azure, cache Olá deve ser em uma sub-rede dedicada que não contém outros recursos, exceto as instâncias de Cache Redis do Azure. Se uma tentativa for feita toodeploy tooa um Cache Redis do Azure Resource Manager VNet tooa sub-rede que contém outros recursos, a implantação de saudação falhará.
> 
> 

![Rede virtual][redis-cache-vnet-ip]

> [!IMPORTANT]
> O Azure reserva alguns endereços IP em cada sub-rede, os quais não podem ser usados. Olá primeiro e últimos endereços IP das sub-redes Olá são reservados para conformidade de protocolo, juntamente com três endereços mais usados para serviços do Azure. Para obter mais informações, consulte [Existem restrições quanto ao uso de endereços IP dentro dessas sub-redes?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
> 
> Em adição toohello endereços IP usados pela infraestrutura de rede virtual do Azure hello, de cada Redis instância Olá sub-rede usa dois endereços IP por fragmento e um endereço IP adicional Olá balanceador de carga. Um cache sem cluster é considerado toohave um fragmento.
> 
> 

Após Olá cache é criado, você pode exibir configuração Olá Olá VNet clicando **rede Virtual** de saudação **menu recursos**.

![Rede virtual][redis-cache-vnet-info]

tooconnect tooyour Azure Redis cache instância ao usar uma rede virtual, especificar o nome de host de saudação do cache na cadeia de caracteres de conexão Olá conforme mostrado no exemplo a seguir de saudação:

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5premium.redis.cache.windows.net,abortConnect=false,ssl=true,password=password");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

## <a name="azure-redis-cache-vnet-faq"></a>Perguntas frequentes sobre a Vnet do Cache Redis do Azure
Olá lista a seguir contém as respostas toocommonly perguntas frequentes sobre o dimensionamento do Cache Redis do Azure de saudação.

* [Quais são alguns problemas comuns de configuração incorreta no Cache Redis do Azure e nas VNets?](#what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets)
* [Como verificar se o cache está funcionando em uma VNET?](#how-can-i-verify-that-my-cache-is-working-in-a-vnet)
* [Posso usar VNets com um cache básico ou Standard?](#can-i-use-vnets-with-a-standard-or-basic-cache)
* [Por que a criação de um cache Redis falha em algumas sub-redes, mas não em outras?](#why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others)
* [Quais são os requisitos de espaço de endereço de sub-rede Olá?](#what-are-the-subnet-address-space-requirements)
* [Todos os recursos de cache funcionam ao hospedar um cache em uma rede virtual?](#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)

## <a name="what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets"></a>Quais são alguns problemas comuns de configuração incorreta no Cache Redis do Azure e nas VNets?
Quando o Cache Redis do Azure está hospedado em uma rede virtual, portas Olá Olá tabelas a seguir são usadas. 

>[!IMPORTANT]
>Se portas Olá Olá tabelas a seguir são bloqueadas, cache Olá pode não funcionar corretamente. Tem um ou mais dessas portas bloqueados é o problema mais comum de má configuração Olá ao usar o Cache Redis do Azure em uma rede virtual.
> 
> 

- [Requisitos de porta de saída](#outbound-port-requirements)
- [Requisitos de porta de entrada](#inbound-port-requirements)

### <a name="outbound-port-requirements"></a>Requisitos de porta de saída

Há sete requisitos de porta de saída.

- Se desejar, todos os toohello de conexões de saída à internet pode ser feitas por meio de um cliente auditoria dispositivo local.
- Três das portas Olá rotear tráfego tooAzure os pontos de extremidade de serviço DNS do Azure e armazenamento do Azure.
- Olá restantes intervalos de porta e para comunicações de sub-rede internas do Redis. Não é necessária nenhuma regra do NSG da sub-rede para as comunicações internas de sub-rede Redis.

| Porta(s) | Direção | Protocolo de Transporte | Finalidade | IP local | IP Remoto |
| --- | --- | --- | --- | --- | --- |
| 80, 443 |Saída |TCP |Dependências de Redis no Armazenamento do Azure/PKI (Internet) | (Sub-rede Redis) |* |
| 53 |Saída |TCP/UDP |Dependências Redis no DNS (Internet/Rede Virtual) | (Sub-rede Redis) |* |
| 8443 |Saída |TCP |Comunicações internas para Redis | (Sub-rede Redis) | (Sub-rede Redis) |
| 10221-10231 |Saída |TCP |Comunicações internas para Redis | (Sub-rede Redis) | (Sub-rede Redis) |
| 20226 |Saída |TCP |Comunicações internas para Redis | (Sub-rede Redis) |(Sub-rede Redis) |
| 13000-13999 |Saída |TCP |Comunicações internas para Redis | (Sub-rede Redis) |(Sub-rede Redis) |
| 15000-15999 |Saída |TCP |Comunicações internas para Redis | (Sub-rede Redis) |(Sub-rede Redis) |


### <a name="inbound-port-requirements"></a>Requisitos de porta de entrada

Há oito requisitos de intervalo de portas de entrada. Solicitações de entrada nesses intervalos são entrada de outros serviços hospedados em Olá mesmo VNET ou toohello interno comunicações de sub-rede do Redis.

| Porta(s) | Direção | Protocolo de Transporte | Finalidade | IP local | IP Remoto |
| --- | --- | --- | --- | --- | --- |
| 6379, 6380 |Entrada |TCP |TooRedis de comunicação do cliente, Azure balanceamento de carga | (Sub-rede Redis) |Rede virtual, Azure Load Balancer |
| 8443 |Entrada |TCP |Comunicações internas para Redis | (Sub-rede Redis) |(Sub-rede Redis) |
| 8500 |Entrada |TCP/UDP |Balanceamento de Carga do Azure | (Sub-rede Redis) |Azure Load Balancer |
| 10221-10231 |Entrada |TCP |Comunicações internas para Redis | (Sub-rede Redis) |(Sub-rede Redus), Azure Load Balancer |
| 13000-13999 |Entrada |TCP |Comunicação de cliente tooRedis Clusters de balanceamento de carga do Azure | (Sub-rede Redis) |Rede virtual, Azure Load Balancer |
| 15000-15999 |Entrada |TCP |TooRedis de comunicação de cliente balanceamento de carga de Clusters, o Azure | (Sub-rede Redis) |Rede virtual, Azure Load Balancer |
| 16001 |Entrada |TCP/UDP |Balanceamento de Carga do Azure | (Sub-rede Redis) |Azure Load Balancer |
| 20226 |Entrada |TCP |Comunicações internas para Redis | (Sub-rede Redis) |(Sub-rede Redis) |

### <a name="additional-vnet-network-connectivity-requirements"></a>Requisitos de conectividade de rede VNET adicionais

Há requisitos de conectividade de rede para o Cache Redis do Azure que podem não ser atendidos inicialmente em uma rede virtual. Cache Redis do Azure requer que todos os Olá itens toofunction corretamente quando usados em uma rede virtual a seguir.

* Rede de saída conectividade tooAzure armazenamento pontos de extremidade em todo o mundo. Isso inclui os pontos de extremidade localizados em Olá mesma região que a instância de Cache Redis do Azure hello, bem como pontos de extremidade de armazenamento localizados na **outros** regiões do Azure. Pontos de extremidade de armazenamento do Azure resolver em Olá domínios DNS a seguir: *n e t*, *>.blob.Core.Windows.NET*, *queue.core.windows.net*e *file.core.windows.net*. 
* Saída conectividade de rede muito*ocsp.msocsp.com*, *mscrl.microsoft.com*, e *crl.microsoft.com*. Essa conectividade é necessário toosupport funcionalidade SSL.
* configuração de DNS Olá para rede virtual Olá deve ser capaz de resolver todos os pontos de extremidade hello e domínios mencionado na Olá pontos anteriores. Esses requisitos de DNS podem ser atendidos, garantindo uma infraestrutura DNS válida está configurada e mantida para rede virtual hello.
* Toohello de conectividade de rede de saída a seguir de monitoramento do Azure pontos de extremidade, resolver em Olá domínios DNS a seguir: shoebox2 black.shoebox2.metrics.nsatc.net, Norte-prod2.prod2.metrics.nsatc.net azglobal-black.azglobal.metrics.nsatc.net, shoebox2-red.shoebox2.metrics.nsatc.net, Leste-prod2.prod2.metrics.nsatc.net azglobal-red.azglobal.metrics.nsatc.net.

### <a name="how-can-i-verify-that-my-cache-is-working-in-a-vnet"></a>Como verificar se o cache está funcionando em uma VNET?

>[!IMPORTANT]
>Ao conectar-se a instância de Cache Redis do Azure tooan que é hospedada em uma rede virtual, os clientes devem estar em cache Olá mesma rede virtual, incluindo todos os aplicativos de teste ou ferramentas de diagnóstico do ping.
>
>

Depois que os requisitos de porta de saudação são configurados conforme descrito na seção anterior hello, você pode verificar se o cache está funcionando executando Olá etapas a seguir.

- [Reinicialize](cache-administration.md#reboot) todos Olá nós de cache. Se todos Olá necessários dependências de cache não podem ser acessadas (conforme documentado no [requisitos de porta de entrada](cache-how-to-premium-vnet.md#inbound-port-requirements) e [requisitos de porta de saída](cache-how-to-premium-vnet.md#outbound-port-requirements)), o cache de saudação não será capaz de toorestart com êxito.
- Depois de reiniciar nós de cache hello (conforme relatado pelo status do cache de saudação no Olá portal do Azure), você pode executar Olá testes a seguir:
  - executar ping Olá cache ponto de extremidade (usando a porta 6380) de um computador que está dentro de saudação mesmo VNET como Olá armazenar em cache, usando [tcping](https://www.elifulkerson.com/projects/tcping.php). Por exemplo:
    
    `tcping.exe contosocache.redis.cache.windows.net 6380`
    
    Se hello `tcping` ferramenta reporta que Olá a porta está aberta, o cache de saudação está disponível para a conexão de clientes em redes de saudação.

  - Tootest de outra maneira é um cliente de cache de teste de toocreate (que pode ser um simples aplicativo de console usando Stackexchange) que se conecta toohello cache e adiciona e recupera alguns itens do cache de saudação. Instalar o aplicativo de cliente de exemplo hello em uma máquina virtual que está em Olá mesmo VNET como cache hello e execute-o cache de toohello tooverify conectividade.


### <a name="can-i-use-vnets-with-a-standard-or-basic-cache"></a>Posso usar VNets com um cache básico ou Standard?
As VNets podem ser usadas apenas com os caches Premium.

### <a name="why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others"></a>Por que a criação de um cache Redis falha em algumas sub-redes, mas não em outras?
Se você estiver implantando um Gerenciador de recursos de VNet de tooa do Cache Redis do Azure, cache Olá deve ser em uma sub-rede dedicada que não contém a nenhum outro tipo de recurso. Se uma tentativa for feita toodeploy tooa um Cache Redis do Azure VNet Gerenciador de recursos de sub-rede que contém outros recursos, a implantação de saudação falhará. Você deve excluir os recursos existentes Olá Olá sub-rede antes de criar um novo cache Redis.

Você pode implantar vários tipos de recursos tooa VNet clássico desde que você tem suficiente IP endereços disponíveis.

### <a name="what-are-hello-subnet-address-space-requirements"></a>Quais são os requisitos de espaço de endereço de sub-rede Olá?
O Azure reserva alguns endereços IP em cada sub-rede, os quais não podem ser usados. Olá primeiro e últimos endereços IP das sub-redes Olá são reservados para conformidade de protocolo, juntamente com três endereços mais usados para serviços do Azure. Para obter mais informações, consulte [Existem restrições quanto ao uso de endereços IP dentro dessas sub-redes?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)

Em adição toohello endereços IP usados pela infraestrutura de rede virtual do Azure hello, de cada Redis instância Olá sub-rede usa dois endereços IP por fragmento e um endereço IP adicional Olá balanceador de carga. Um cache sem cluster é considerado toohave um fragmento.

### <a name="do-all-cache-features-work-when-hosting-a-cache-in-a-vnet"></a>Todos os recursos de cache funcionam ao hospedar um cache em uma rede virtual?
Quando o cache faz parte de uma rede virtual, somente a clientes em redes de saudação pode acessar o cache de saudação. Como resultado, hello seguintes recursos de gerenciamento de cache não funcionam no momento.

* Console de redis - como Redis Console é executado no navegador local, que está fora da saudação rede virtual, não é possível conectar-se tooyour cache.

## <a name="use-expressroute-with-azure-redis-cache"></a>Usar o ExpressRoute com Cache Redis do Azure
Os clientes podem conectar um [rota expressa do Azure](https://azure.microsoft.com/services/expressroute/) infraestrutura de rede virtual tootheir circuito, estendendo assim seu tooAzure de rede local. 

Por padrão, um circuito ExpressRoute recém-criado não executa túnel forçado (anúncio de uma rota padrão, 0.0.0.0/0) em uma VNET. Como resultado, conectividade de Internet de saída é permitida diretamente da saudação redes e aplicativos de cliente são capazes de tooconnect tooother do Azure pontos de extremidade incluindo Cache Redis do Azure.

No entanto, uma configuração de cliente comum é toouse túnel forçado (anuncia uma rota padrão) que força a saída da Internet tráfego tooinstead fluxo local. Este fluxo de tráfego quebras de conectividade com o Cache Redis do Azure se for o tráfego de saída hello e bloqueado no local, de modo que hello instância de Cache Redis do Azure não é capaz de toocommunicate com suas dependências.

solução de saudação é toodefine uma (ou mais) definidos pelo usuário rotas (UDRs) na sub-rede Olá que contém Olá Cache Redis do Azure. Um UDR define as rotas de sub-rede que serão cumpridas em vez de rota padrão de saudação.

Se possível, é recomendável Olá toouse seguinte configuração:

* configuração de rota expressa Olá anuncia 0.0.0.0/0 e todo o tráfego de saída no local de túneis de força por padrão.
* Olá, UDR aplicada toohello sub-rede contendo Olá Cache Redis do Azure define 0.0.0.0/0 com uma rota de trabalho para toohello de tráfego de TCP/IP internet pública. Por exemplo por configuração saudação do próximo salto too'Internet do tipo '.

Olá efeito combinado dessas etapas é que o nível de sub-rede Olá UDR tem precedência sobre Olá ExpressRoute forçada de túneis, garantindo, assim, o acesso de Internet de saída de hello Cache Redis do Azure.

Instância de Cache Redis do Azure tooan conexão de um aplicativo local usando o ExpressRoute não é um cenário de uso típico devido a motivos de tooperformance (para melhor desempenho de Cache Redis do Azure, os clientes devem estar no hello mesma região Olá Cache Redis do Azure).

>[!IMPORTANT] 
>Olá rotas definidas em um UDR **deve** ser específica o suficiente tootake precedência sobre todas as rotas anunciadas pela configuração de rota expressa hello. Hello exemplo a seguir usa o intervalo de endereços do hello amplo 0.0.0.0/0 e assim pode potencialmente ser acidentalmente substituído pelos anúncios de rota usando intervalos de endereços mais específicos.

>[!WARNING]  
>Não há suporte para o Cache Redis do Azure com configurações de rota expressa que **incorretamente entre-anunciar rotas de saudação emparelhamento caminho toohello privada caminho emparelhamento público**. As configurações de ExpressRoute com emparelhamento público definido receberão anúncios de rota da Microsoft para um grande conjunto de intervalos de endereços IP do Microsoft Azure. Se esses intervalos de endereços incorretamente entre anunciados no caminho de emparelhamento privado hello, Olá significa que todos os pacotes de saída de rede da sub-rede da instância de Cache Redis do Azure Olá estão rede do local do cliente tooa incorretamente túnel de força infraestrutura. Esse fluxo de rede interrompe o Cache Redis do Azure. problema de toothis solução Olá é toostop as rotas entre publicidade Olá emparelhamento caminho toohello privada caminho emparelhamento público.


Informações básicas sobre as rotas definidas pelo usuário estão disponíveis nesta [visão geral](../virtual-network/virtual-networks-udr-overview.md).

Para obter mais informações sobre o ExpressRoute, consulte [Visão geral técnica do ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="next-steps"></a>Próximas etapas
Saiba como toouse premium mais recursos de cache.

* [Camada de Azure Redis Cache Premium toohello Introdução](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-vnet]: ./media/cache-how-to-premium-vnet/redis-cache-vnet.png

[redis-cache-vnet-ip]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-ip.png

[redis-cache-vnet-info]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-info.png

