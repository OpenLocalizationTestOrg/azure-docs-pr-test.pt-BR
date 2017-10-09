### <a name="is-bgp-supported-on-all-azure-vpn-gateway-skus"></a>O BGP tem suporte em todas as SKUs de Gateway de VPN do Azure?
Não, o BGP tem suporte nos gateways de VPN **Standard** e **HighPerformance** do Azure. **Basic** não tem suporte.

### <a name="can-i-use-bgp-with-azure-policy-based-vpn-gateways"></a>Posso usar o BGP com gateways de VPN Baseados em Política do Azure?
Não, há suporte ao o BGP somente em gateways de VPN Baseados em Rota.

### <a name="can-i-use-private-asns-autonomous-system-numbers"></a>Posso usar ASNs (Números de Sistema Autônomo) privados?
Sim, você pode usar seu próprio ASNs públicos ou privados para suas redes locais e para redes virtuais do Azure.

### <a name="are-there-asns-reserved-by-azure"></a>Há ASNs reservados pelo Azure?
Sim, hello ASNs seguintes são reservados pelo Azure para emparelhamentos internos e externos:

* ASNs públicos: 8075, 8076, 12076
* ASNs privados: 65515, 65517, 65518, 65519, 65520

Você não pode especificar essas ASNs para seus dispositivos VPN locais ao conectar-se tooAzure gateways de VPN.

### <a name="are-there-any-other-asns-that-i-cant-use"></a>Há outros ASNs que eu não posso usar?
Sim, Olá ASNs a seguir é [reservado pelo IANA](http://www.iana.org/assignments/iana-as-numbers-special-registry/iana-as-numbers-special-registry.xhtml) e não é possível configurar o Gateway de VPN do Azure:

23456, 64496-64511, 65535-65551 e 429496729

### <a name="can-i-use-hello-same-asn-for-both-on-premises-vpn-networks-and-azure-vnets"></a>É possível usar Olá mesmo ASN para ambos os locais redes VPN e VNets do Azure?
Não, você deverá atribuir ASNs diferentes entre suas redes locais e as VNets do Azure se os estiver conectando junto com o BGP. Os Gateways de VPN do Azure têm um ASN padrão de 65515 atribuído, quer o BGP esteja habilitado ou não para a conectividade entre locais. Você pode substituir esse padrão, atribuindo um ASN diferente durante a criação de gateway VPN hello, ou alterar Olá ASN depois de criar o gateway de saudação. Você precisará tooassign toohello de ASNs o local correspondente Gateways de rede Local do Azure.

### <a name="what-address-prefixes-will-azure-vpn-gateways-advertise-toome"></a>O endereço de prefixo serão toome de anúncio de gateways de VPN do Azure?
Gateway VPN do Azure anunciará Olá dispositivos BGP rotas tooyour locais a seguir:

* Seus prefixos de endereços de VNet
* Prefixos de endereço para cada gateway de VPN do Azure conectado toohello Gateways de rede Local
* Rotas aprendidas de outros BGP emparelhamento sessões conectadas toohello gateway VPN do Azure, **exceto padrão ou mais rotas sobrepostas com qualquer prefixo de rede virtual**.

### <a name="can-i-advertise-default-route-00000-tooazure-vpn-gateways"></a>Posso anunciar gateways VPN padrão (0.0.0.0/0) de rota tooAzure?
Sim.

Observação Isso forçará todos os tráfego de saída de rede virtual para seu site local e impedirá Olá VNet VMs de aceitar comunicação pública de saudação Internet diretamente, esses RDP ou SSH de saudação Internet toohello VMs.

### <a name="can-i-advertise-hello-exact-prefixes-as-my-virtual-network-prefixes"></a>Pode anunciar prefixos exata hello como meu prefixos de rede Virtual?

Não, Olá publicidade mesmo prefixos como qualquer um dos seus prefixos de endereço de rede Virtual será bloqueado ou filtrado por Olá plataforma Windows Azure. No entanto, você pode anunciar um prefixo que é um superconjunto do que você tem em sua Rede Virtual. 

Por exemplo, se sua rede virtual usada Olá endereço espaço 10.0.0.0/16, você pode anunciar 10.0.0.0/8. Mas você não pode anunciar 10.0.0.0/16 ou 10.0.0.0/24.

### <a name="can-i-use-bgp-with-my-vnet-to-vnet-connections"></a>Posso usar o BGP com minhas conexões VNet para VNet?
Sim, você pode usar o BGP para conexões entre locais e conexões de VNet para VNet.

### <a name="can-i-mix-bgp-with-non-bgp-connections-for-my-azure-vpn-gateways"></a>Posso combinar o BGP a conexões não BGP para meu gateways de VPN do Azure?
Sim, você pode combinar as duas BGP e conexões não BGP para Olá mesmo gateway VPN do Azure.

### <a name="does-azure-vpn-gateway-support-bgp-transit-routing"></a>O gateway de VPN do Azure dá suporte ao roteamento de trânsito de BGP?
Sim, o roteamento de tráfego BGP é compatível, com exceção de saudação gateways de VPN do Azure serão **não** anunciar padrão roteia tooother pares de BGP. tooenable trânsito roteamento entre vários gateways de VPN do Azure, você deve habilitar o BGP em todas as conexões de rede virtual a rede intermediárias.

### <a name="can-i-have-more-than-one-tunnel-between-azure-vpn-gateway-and-my-on-premises-network"></a>Posso ter mais de um túnel entre meu gateway de VPN do Azure e minha rede local?
Sim, você pode estabelecer mais de um túnel de VPN S2S entre um gateway de VPN do Azure e sua rede local. Observe que todos esses túneis serão contabilizados em número total de saudação de túneis para seus gateways de VPN do Azure e você deve habilitar o BGP em ambos os túneis.

Por exemplo, se você tiver dois túneis redundantes entre o gateway de VPN do Azure e uma das suas redes locais, eles irão consumir 2 túneis fora da cota total de saudação do seu gateway de VPN do Azure (10 padrão) e 30 de alto desempenho.

### <a name="can-i-have-multiple-tunnels-between-two-azure-vnets-with-bgp"></a>Posso ter vários túneis entre duas VNets do Azure com o BGP?
Sim, mas pelo menos um dos gateways de rede virtual Olá deve estar na configuração ativa-ativa.

### <a name="can-i-use-bgp-for-s2s-vpn-in-an-expressroutes2s-vpn-co-existence-configuration"></a>Posso usar BGP para VPN S2S em uma configuração de coexistência de VPN S2S/ExpressRoute?
Sim. 

### <a name="what-address-does-azure-vpn-gateway-use-for-bgp-peer-ip"></a>Que endereço o gateway de VPN do Azure usa para o IP de Par de BGP?
gateway de VPN do Azure Olá alocará um único endereço IP do hello GatewaySubnet intervalo definido para a rede virtual hello. Por padrão, é Olá segundo último endereço do intervalo de saudação. Por exemplo, se o GatewaySubnet é 10.12.255.0/27, variando de 10.12.255.0 too10.12.255.31, Olá endereço IP do par de BGP no gateway de VPN do Azure Olá será 10.12.255.30. Você pode encontrar essas informações quando você listar informações de saudação do gateway VPN do Azure.

### <a name="what-are-hello-requirements-for-hello-bgp-peer-ip-addresses-on-my-vpn-device"></a>Quais são os requisitos de saudação para endereços de IP de par de BGP Olá em meu dispositivo VPN?
Seu endereço de par BGP local **não deve** Olá mesmo como o endereço IP público de saudação do seu dispositivo VPN. Use um endereço IP diferente no dispositivo VPN Olá para o IP de par de BGP. Pode ser um endereço atribuído a interface de loopback toohello no dispositivo de saudação. Especifique esse endereço em Olá Gateway de rede Local representando Olá local correspondente.

### <a name="what-should-i-specify-as-my-address-prefixes-for-hello-local-network-gateway-when-i-use-bgp"></a>O que deve especifico como meu prefixos de endereço de Gateway de rede Local da saudação quando uso o BGP?
Gateway de rede Local do Azure Especifica prefixos de endereço inicial Olá para rede de local de saudação. Com BGP, você deve alocar o prefixo de host da saudação (/ 32 prefixo) de seu endereço de IP de par de BGP como o espaço de endereço Olá para essa rede local. Se o IP de par de BGP é 10.52.255.254, você deve especificar "10.52.255.254/32" como Olá localNetworkAddressSpace de saudação Gateway de rede Local que representa essa rede local. Isso é tooensure que Olá VPN do Azure gateway estabelece a sessão BGP de saudação por meio de túnel de VPN S2S hello.

### <a name="what-should-i-add-toomy-on-premises-vpn-device-for-hello-bgp-peering-session"></a>O que devo adicionar dispositivo VPN local toomy para a sessão de emparelhamento Olá BGP?
Você deve adicionar uma rota de host de saudação endereço IP de par de BGP do Azure no seu dispositivo VPN apontando toohello túnel de VPN S2S de IPsec. Por exemplo, se Olá IP de par de VPN do Azure é "10.12.255.30", você deverá adicionar uma rota de host para "10.12.255.30" com uma interface nexthop da interface de túnel IPsec correspondente Olá em seu dispositivo VPN.

