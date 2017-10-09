Hello tabela a seguir mostra os tipos de gateway hello e Olá estimado taxa de transferência por SKU do gateway. Esta tabela se aplica a toohello Gerenciador de recursos e modelos de implantação clássico. 

Os preços diferem entre os SKUs de gateway. Para saber mais, veja [Preços do Gateway de VPN](https://azure.microsoft.com/pricing/details/vpn-gateway).

Observe o gateway UltraPerformance Olá que SKU não é representado nesta tabela. Para obter informações sobre Olá UltraPerformance SKU, consulte Olá [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentação.

|  | **Taxa de transferência de Gateway de VPN (1)** | **Túneis IPsec máximo de Gateway de VPN (2)** | **Taxa de transferência de Gateway de ExpressRoute** | **Coexistência de Gateway de VPN e o ExpressRoute** |
| --- | --- | --- | --- | --- |
| **SKU Básica (3)(5)(6)** |100 Mbps |10 |500 Mbps (6) |Não |
| **SKU padrão (4)(5)** |100 Mbps |10 |1000 Mbps |Sim |
| **SKU de Alto Desempenho (4)** |200 Mbps |30 |2000 Mbps |Sim |


(1) taxa de transferência VPN de saudação é uma estimativa aproximada com base em medidas Olá entre VNets Olá mesma região do Azure. Não é uma taxa de transferência garantida para conexões entre locais em Olá da Internet. É medida de taxa de transferência máxima possível hello.

(2) número de saudação de túneis consulte tooRouteBased VPNs. Uma VPN PolicyBased só pode dar suporte a um túnel de VPN de Site a Site.

(3) não há suporte para o BGP para Olá SKUS Basic.

(4) não há suporte para VPNs PolicyBased nesta SKU. Eles têm suporte para Olá somente no SKU básico.

(5) Não há suporte para conexões de Gateway de VPN S2S ativa-ativa para essa SKU. Olá HighPerformance SKU somente há suporte para ativo-ativo.

(6) A SKU básica é preterida para uso com ExpressRoute.
