### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a>Quais sistemas operacionais de cliente posso usar com ponto a site?

Olá, sistemas operacionais a seguir têm suporte:

* Windows 7 (32 bits e 64 bits)
* Windows Server 2008 R2 (somente 64 bits)
* Windows 8 (32 bits e 64 bits)
* Windows 8.1 (32 bits e 64 bits)
* Windows Server 2012 (somente 64 bits)
* Windows Server 2012 R2 (somente 64 bits)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>Posso usar qualquer cliente de VPN de software para ponto a site que dê suporte a SSTP?

Não. O suporte é limitado somente toohello Windows versões de sistemas operacionais listadas acima.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>Quantos pontos de extremidade de cliente VPN posso ter em minha configuração ponto a site?

Oferecemos suporte too128 VPN clientes toobe capaz de tooconnect tooa rede virtual no hello mesmo tempo.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>Posso usar minha própria CA de raiz de PKI interna para a conectividade ponto a site?

Sim. Anteriormente, somente os certificados raiz autoassinados podiam ser usados. Você ainda pode carregar 20 certificados raiz.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>Posso atravessar proxies e firewalls usando o recurso de ponto a site?

Sim. Usamos tootunnel SSTP (Secure Socket Tunneling Protocol) por meio de firewalls. Esse túnel aparecerá como uma conexão HTTPs.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a>Se eu reiniciar um computador cliente configurado para ponto a Site, hello VPN reconectará automaticamente?

Por padrão, computador de cliente Olá não restabelecerá conexão de VPN Olá automaticamente.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a>Reconexão automática de suporte ponto a Site e DDNS nos clientes VPN de Olá?

A reconexão automática e o DDNS atualmente não têm suporte em VPNs ponto a site.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a>Posso ter Site a Site e configurações de ponto para Site coexistirem para Olá mesma rede virtual?

Sim. Essas duas soluções funcionarão se você tiver um tipo VPN Baseada em Rota para o gateway. Para o modelo de implantação clássico Olá, é necessário um gateway dinâmico. Podemos fazer não suporte ponto a Site para gateways de VPN de roteamento estático ou gateways usando Olá `-VpnType PolicyBased` cmdlet.

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a>Posso configurar um ponto para Site cliente tooconnect toomultiple as redes virtuais no hello simultaneamente?

Sim, isso é possível. Mas as redes virtuais Olá não podem ter prefixos IP sobrepostos e não devem se sobrepor os espaços de endereço Olá ponto a Site entre redes virtuais hello.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>Quanta taxa de transferência posso esperar por meio de conexões site a site ou ponto a site?

É difícil toomaintain Olá taxa de transferência exata Olá de túneis de VPN. IPsec e SSTP são protocolos VPN de criptografia pesada. Taxa de transferência também é limitada pela latência hello e largura de banda entre suas instalações e Olá Internet.
