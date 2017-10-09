Olá perguntas Frequentes de VNet para VNet se aplica a conexões de Gateway tooVPN. Se você estiver procurando o Emparelhamento de Rede Virtual, confira [Emparelhamento de Rede Virtual](../articles/virtual-network/virtual-network-peering-overview.md)

### <a name="does-azure-charge-for-traffic-between-vnets"></a>O Azure cobra pelo tráfego entre VNets?

Rede virtual a rede de tráfego dentro de saudação mesmo região é gratuita para ambas as direções ao usar uma conexão de gateway VPN. Cruzada região VNet para VNet saída tráfego é cobrado com taxas de transferência Olá inter-redes de saída dados com base em regiões de origem hello. Consulte toohello [página de preços de Gateway de VPN](https://azure.microsoft.com/pricing/details/vpn-gateway/) para obter detalhes. Se você estiver se conectando seus VNets usando o emparelhamento de rede virtual, em vez de Gateway de VPN, consulte Olá [página de preços de rede Virtual](https://azure.microsoft.com/pricing/details/virtual-network/).

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a>Tráfego de rede virtual a rede transportados por Olá Internet?

Não. Tráfego de rede virtual a rede percorrem Olá backbone do Microsoft Azure, Olá da Internet.

### <a name="is-vnet-to-vnet-traffic-secure"></a>O tráfego de VNet para VNet é seguro?

Sim, ele é protegido por criptografia IPsec/IKE.

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a>É necessário um dispositivo VPN tooconnect VNets juntas?

Não. A conexão de várias redes virtuais do Azure entre si não exige um dispositivo VPN, a menos que a conectividade entre locais seja necessária.

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a>Minhas VNets precisarem toobe em Olá mesma região?

Não. redes virtuais Olá podem estar em Olá mesmas ou em diferentes regiões do Azure (locais).

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a>Se Olá VNets não está no hello mesma assinatura, assinaturas de saudação necessário toobe associado Olá AD mesmo locatário?

Não.

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>Posso usar Rede Virtual para Rede Virtual com conexões multissite?

Sim. A conectividade de rede virtual pode ser usada simultaneamente com VPNs de multissite.

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>A quantos sites locais e redes virtuais uma rede virtual pode se conectar?

Veja a tabela [Requisitos de gateway](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a>Pode usar VNet para VNet tooconnect VMs ou serviços fora de uma rede virtual em nuvem?

Não. A rede virtual com rede virtual dá suporte à conexão de redes virtuais. Ele não dá suporte à conexão de máquinas virtuais ou serviços de nuvem que não estão em uma rede virtual.

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>Um serviço de nuvem ou um ponto de extremidade de balanceamento de carga pode abranger redes virtuais?

Não. Um serviço de nuvem ou um ponto de extremidade de balanceamento de carga não pode abranger redes virtuais, mesmo que elas estejam conectadas entre si.

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>Posso usar um tipo de VPN PolicyBased para conexões de Rede Virtual para Rede Virtual ou Multissite?

Não. As conexões de rede virtual para rede virtual e de vários sites exigem gateways de VPN com tipos de VPN RouteBased (anteriormente chamado de Roteamento Dinâmico).

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a>Posso conectar uma rede virtual com um tipo de VPN RouteBased de tooanother VNet com um tipo PolicyBased VPN?

Não, ambas as redes virtuais DEVEM estar usando VPNs baseadas em rota (anteriormente chamado de Roteamento Dinâmico).

### <a name="do-vpn-tunnels-share-bandwidth"></a>Os túneis de VPN compartilham largura de banda?

Sim. Todos os túneis VPN da rede virtual Olá compartilham largura de banda disponível no gateway de VPN do Azure Olá Olá e Olá mesmo SLA de tempo de atividade de gateway VPN no Azure.

### <a name="are-redundant-tunnels-supported"></a>Há suporte para túneis redundantes?

Os túneis redundantes entre um par de redes virtuais terão suporte quando um gateway de rede virtual estiver configurado como ativo.

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>Posso ter espaços de endereço sobrepostos para configurações de Rede Virtual para Rede Virtual?

Não. Você não pode ter intervalos de endereços IP sobrepostos.

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>Pode haver sobreposição de espaços de endereço entre as redes virtuais conectadas e sites local locais?

Não. Você não pode ter intervalos de endereços IP sobrepostos.



