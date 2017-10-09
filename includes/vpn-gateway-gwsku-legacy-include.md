herdado gateway VPN (antigo) Olá SKUs são:

* Basic
* Standard
* HighPerformance

Gateway de VPN não usar o gateway de UltraPerformance de saudação SKU. Para obter informações sobre Olá UltraPerformance SKU, consulte Olá [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentação.

Ao trabalhar com hello SKUs herdados, considere o seguinte hello:

* Se você quiser toouse um tipo PolicyBased VPN, você deve usar o hello SKUS Basic. VPNs PolicyBased (anteriormente chamadas de Roteamento Estático) não têm suporte em qualquer outro tipo de SKU.
* Não há suporte para BGP Olá SKUS Basic.
* Gateway VPN de rota expressa coexistir configurações não são suportadas em Olá SKUS Basic.
* Conexões de Gateway de VPN S2S ativo-ativo podem ser configurados em Olá HighPerformance SKU apenas.
