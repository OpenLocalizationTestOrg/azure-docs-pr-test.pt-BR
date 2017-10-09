---
title: Perguntas frequentes sobre o Gateway VPN de aaaAzure | Microsoft Docs
description: "Olá perguntas frequentes sobre o Gateway de VPN. Perguntas frequentes para conexões entre locais de Rede Virtual do Microsoft Azure, conexões de configuração híbrida e gateways de VPN."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6ce36765-250e-444b-bfc7-5f9ec7ce0742
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/30/2017
ms.author: cherylmc,yushwang
ms.openlocfilehash: e1737f5832728f513e31f97cc7e752147faaaeb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-faq"></a>Perguntas frequentes de gateway de VPN

## <a name="connecting"></a>Conectando redes toovirtual

### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a>Posso conectar redes virtuais em diferentes regiões do Azure?

Sim. Na verdade, não há nenhuma restrição de região. Uma rede virtual pode se conectar a rede virtual tooanother em Olá mesma região, ou em uma região do Azure diferente. 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a>Posso conectar redes virtuais em assinaturas diferentes?

Sim.

### <a name="can-i-connect-toomultiple-sites-from-a-single-virtual-network"></a>Pode conectar toomultiple sites de uma única rede virtual?

Você pode se conectar a sites toomultiple usando o Windows PowerShell e hello APIs REST do Azure. Consulte Olá [multissite e VNet para VNet conectividade](#V2VMulti) seção de perguntas Frequentes.

### <a name="what-are-my-cross-premises-connection-options"></a>Quais são minhas opções de conexão entre locais?

Olá a seguir entre locais suporte a conexões:

* Site a Site – conexão VPN no IPsec (IKE v1 e IKE v2). Esse tipo de conexão exige um dispositivo VPN ou RRAS. Para obter mais informações, consulte [Site a Site](vpn-gateway-howto-site-to-site-resource-manager-portal.md).
* Ponto a Site – conexão VPN no SSTP (Secure Socket Tunneling Protocol). Essa conexão não exige um dispositivo VPN. Para obter mais informações, consulte [Ponto a Site](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* VNet para VNet – esse tipo de conexão é Olá mesmo que uma configuração de Site a Site. TooVNet de rede virtual é uma conexão VPN sobre IPsec (IKE v1 e IKE v2). Ela não requer um dispositivo VPN. Para obter mais informações, consulte [VNet a VNet](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).
* Multissite – isso é uma variação de uma configuração de Site a Site que permite que você tooconnect vários sites tooa virtual rede local. Para obter mais informações, consulte [Multissite](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).
* Rota expressa – ExpressRoute é tooAzure uma conexão direta de sua WAN, não uma conexão VPN sobre Olá Internet pública. Para obter mais informações, consulte Olá [visão geral técnica do ExpressRoute](../expressroute/expressroute-introduction.md) e hello [perguntas Frequentes do ExpressRoute](../expressroute/expressroute-faqs.md).

Para saber mais sobre conexões de gateway de VPN, confira [Sobre gateway de VPN](vpn-gateway-about-vpngateways.md).

### <a name="what-is-hello-difference-between-a-site-to-site-connection-and-point-to-site"></a>Qual é a diferença Olá entre uma conexão Site a Site e ponto a Site?

**Site a Site** as configurações (túnel VPN IPsec/IKE) estão entre o local e o Azure. Isso significa que você pode se conectar de qualquer um dos seus computadores em sua máquina de virtual tooany local ou a instância de função dentro de sua rede virtual, dependendo de como você escolhe tooconfigure roteamento e permissões. É uma ótima opção para uma conexão entre locais sempre disponível e é bastante adequada para configurações híbridas. Esse tipo de conexão depende de um dispositivo de VPN IPsec (dispositivo de hardware ou dispositivo de disco), que deve ser implantado na borda de saudação da sua rede. toocreate esse tipo de conexão, você deve ter um endereço IPv4 externamente que não estiver por trás de um NAT.

**Ponto a Site** configurações (VPN sobre SSTP) permitem que você conecte-se de um único computador de qualquer lugar tooanything localizado em sua rede virtual. Ele usa o cliente VPN Olá Windows na caixa. Como parte da configuração de ponto para Site hello, você pode instalar um certificado e um pacote de configuração de cliente VPN, que contém as configurações de saudação que permitem que sua máquina virtual do computador tooconnect tooany ou instância de função dentro da rede virtual hello. É ótimo quando você deseja a rede virtual do tooconnect tooa, mas não está localizados no local. Também é uma boa opção quando você não tiver acesso tooVPN hardware ou um endereço IPv4 externamente, ambos são necessários para uma conexão Site a Site.

Você pode configurar sua rede virtual toouse ambos Site a Site e o tipo de ponto a Site simultaneamente, desde que você criar sua conexão Site a Site usando uma VPN baseada em rota para o gateway. Tipos VPN baseado em rotas são chamados de gateways dinâmicos no modelo de implantação clássico hello.

## <a name="gateways"></a>Gateways da rede virtual

### <a name="is-a-vpn-gateway-a-virtual-network-gateway"></a>Um gateway de VPN é um gateway de rede virtual?

Um gateway de VPN é um tipo de gateway de rede virtual. Um gateway de VPN envia o tráfego criptografado entre sua rede virtual e seu local em uma conexão pública. Você também pode usar um tráfego de toosend do gateway VPN entre redes virtuais. Quando você criar um gateway VPN, use Olá - GatewayType valor 'Vpn'. Para saber mais, veja [Sobre as configurações de Gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md).

### <a name="what-is-a-policy-based-static-routing-gateway"></a>O que é um gateway baseado em políticas (roteamento estático)?

Os gateways baseados em política implementam VPNs baseadas em política. As VPNs baseadas em política criptografar e direcionam pacotes por meio de túneis IPsec com base nas combinações de saudação de prefixos de endereço entre sua rede local e hello VNet do Azure. diretiva Hello (ou no seletor de tráfego) geralmente é definido como uma lista de acesso na configuração de VPN de saudação.

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a>O que é um gateway baseado em rotas (roteamento dinâmico)?

Implementar gateways baseadas em rota Olá VPNs baseadas em rota. VPNs baseadas em rota usam "rotas" hello IP encaminhamento ou pacotes de toodirect da tabela de roteamento em suas interfaces de túnel correspondente. interfaces de túnel Hello, em seguida, criptografar ou descriptografar os pacotes de saudação dentro e fora de túneis de saudação. Olá seletor de política ou tráfego para as VPNs baseadas em rota estiverem configuradas como para qualquer (ou caracteres curinga).

### <a name="do-i-need-a-gatewaysubnet"></a>É necessária uma 'GatewaySubnet'?

Sim. sub-rede de gateway Olá contém endereços IP de saudação que usam serviços de gateway de rede virtual hello. Você precisa toocreate uma sub-rede do gateway para sua rede virtual na ordem tooconfigure um gateway de rede virtual. Todas as sub-redes de gateway devem ser nomeadas 'GatewaySubnet' toowork corretamente. Não dê outro nome à sua sub-rede de gateway. E não implantar VMs ou qualquer outra transação toohello sub-rede de gateway.

Quando você cria a sub-rede de gateway hello, você especificar Olá número de endereços IP que Olá sub-rede contém. Olá endereços IP na sub-rede de gateway Olá alocados toohello o serviço de gateway. Algumas configurações exigem mais toobe de endereços IP alocados toohello serviços de gateway que outras pessoas. Você deseja toomake-se de que sua sub-rede de gateway contém suficiente crescimento futuro de tooaccommodate de endereços IP e as possíveis configurações adicionais de conexão de novo. Dessa forma, embora seja possível criar uma sub-rede de gateway tão pequena quanto /29, é recomendável criar uma sub-rede de gateway de /27 ou maior (/27, /26, /25 etc.). Examinar os requisitos de saudação para configuração de saudação que você deseja toocreate e verifique se essa sub-rede de gateway Olá que tiver atenderá a esses requisitos.

### <a name="can-i-deploy-virtual-machines-or-role-instances-toomy-gateway-subnet"></a>Posso implantar máquinas virtuais ou a sub-rede de gateway de toomy de instâncias de função?

Não.

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a>Posso obter o endereço IP do gateway de VPN antes de criá-lo?

Não. Você tem toocreate seu endereço de IP hello tooget primeiro gateway. Olá alterações de endereço IP se você excluir e recriar o gateway VPN.

### <a name="can-i-request-a-static-public-ip-address-for-my-vpn-gateway"></a>Eu posso solicitar um endereço IP Público Estático para o meu gateway de VPN?

Não. Somente a atribuição de endereço IP Dinâmico é suportada. No entanto, isso não significa que o endereço IP de saudação alterado depois que ele foi atribuído tooyour gateway VPN. somente tempo de saudação alterações de endereço IP do gateway VPN hello quando é Olá gateway é excluído e criado novamente. Olá endereço IP público de gateway VPN não é alterado em redimensionamento, redefinir ou outros internas manutenção/atualizações do seu gateway de VPN. 

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a>Como meu túnel de VPN é autenticado?

A VPN do Azure usa autenticação PSK (Chave Pré-Compartilhada). Podemos gerar uma chave pré-compartilhada (PSK) quando criamos o túnel VPN hello. Você pode alterar Olá gerado automaticamente PSK tooyour próprio com o cmdlet do PowerShell de chave pré-compartilhada definir hello ou a API REST.

### <a name="can-i-use-hello-set-pre-shared-key-api-tooconfigure-my-policy-based-static-routing-gateway-vpn"></a>É possível usar Olá API chave pré-compartilhada tooconfigure meu baseado em políticas (roteamento estático) gateway VPN?

Sim, Olá cmdlet de API chave pré-compartilhada e o PowerShell pode ser usado tooconfigure VPNs (estático) com base na política do Azure e baseadas em rota VPNs de roteamento (dinâmico).

### <a name="can-i-use-other-authentication-options"></a>É possível usar outras opções de autenticação?

Estamos toousing limitado pré-compartilhada PSK (chaves) para autenticação.

### <a name="how-do-i-specify-which-traffic-goes-through-hello-vpn-gateway"></a>Como especificar qual tráfego passa pelo gateway VPN Olá?

#### <a name="resource-manager-deployment-model"></a>Modelo de implantação do Gerenciador de Recursos

* PowerShell: use "AddressPrefix" toospecify tráfego para o gateway de rede local hello.
* Portal do Azure: Navegue gateway de rede Local toohello > Configuração > espaço de endereço.

#### <a name="classic-deployment-model"></a>Modelo de implantação clássica

* Portal do Azure: Navegue rede virtual clássica de toohello > conexões VPN > conexões VPN Site a site > nome do site Local > site Local > espaço de endereço do cliente. 
* Portal clássico: Adicione cada intervalo que você deseja que sejam enviados pelo gateway Olá para sua rede virtual na página de redes de saudação em redes locais. 

### <a name="can-i-configure-forced-tunneling"></a>Posso configurar o Túnel Forçado?

Sim. Consulte [Configurar o túnel forçado](vpn-gateway-about-forced-tunneling.md).

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-tooconnect-toomy-on-premises-network"></a>Posso configurar meu próprio servidor VPN no Azure e usá-lo a rede de local de toomy tooconnect?

Sim, você pode implantar sua própria gateways de VPN ou servidores no Azure do hello Azure Marketplace ou criar seus próprios roteadores VPN. Você precisa tooconfigure definida pelo usuário rotas em sua rede virtual tooensure tráfego é roteado corretamente entre as redes locais e suas sub-redes de rede virtual.

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a>Por que determinadas portas serão abertas no meu gateway VPN?

Elas são necessárias para a comunicação de infraestrutura do Azure. Elas são protegidas (bloqueadas) por certificados do Azure. Sem certificados adequados, entidades externas, incluindo clientes Olá os gateways, não será capaz de toocause qualquer efeito sobre os pontos de extremidade.

Um gateway de VPN é basicamente um dispositivo multihomed com uma NIC tocando em rede privada de cliente hello e uma NIC opostas Olá rede pública. Entidades de infraestrutura do Azure não podem tocar em redes privadas de cliente por motivos de conformidade, para que eles precisam tooutilize pontos de extremidade públicos para comunicação de infraestrutura. pontos de extremidade públicos Olá são verificados periodicamente por auditoria de segurança do Azure.

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a>Mais informações sobre tipos de gateway, requisitos e taxa de transferência

Para saber mais, veja [Sobre as configurações de Gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md).

## <a name="s2s"></a>Conexões Site a Site e dispositivos VPN

### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a>O que devo considerar ao escolher um dispositivo VPN?

Validamos um conjunto de dispositivos de VPN site a site padrão em parceria com fornecedores de dispositivos. Uma lista de dispositivos VPN compatíveis conhecidos, as instruções de configuração correspondente ou exemplos e especificações de dispositivo pode ser encontrada no hello [sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md) artigo. Todos os dispositivos em Olá famílias de dispositivos listadas como compatíveis conhecidos devem funcionar com a rede Virtual. toohelp configurar seu dispositivo VPN, consulte o exemplo de configuração de dispositivo toohello ou link que corresponde a tooappropriate da família do dispositivo.

### <a name="where-can-i-find-vpn-device-configuration-settings"></a>Onde posso encontrar as definições de configuração para o dispositivo VPN?

[!INCLUDE [vpn devices](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="how-do-i-edit-vpn-device-configuration-samples"></a>Como edito os exemplos de configuração do dispositivo VPN?

Para obter informações sobre a edição dos exemplos de configuração do dispositivo, consulte [Edição de exemplos](vpn-gateway-about-vpn-devices.md#editing).

### <a name="where-do-i-find-ipsec-and-ike-parameters"></a>Onde encontro os parâmetros IPsec e IKE?

Para obter os parâmetros IPsec/IKE, consulte [Parâmetros](vpn-gateway-about-vpn-devices.md#ipsec).

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a>Por que meu túnel VPN baseado em políticas é desativado quando o tráfego está ocioso?

Esse comportamento é esperado para gateways de VPN baseados em políticas (também conhecidos como roteamento estático). Quando o tráfego de saudação túnel Olá fica ocioso por mais de 5 minutos, o túnel de saudação será interrompido. Quando o tráfego começa a fluir em ambas as direções, túnel Olá será restabelecida imediatamente.

### <a name="can-i-use-software-vpns-tooconnect-tooazure"></a>É possível usar software VPNs tooconnect tooAzure?

Há suporte para servidores RRAS (Roteamento e Acesso Remoto) do Windows Server 2012 para configuração entre locais site a site.

Outras soluções VPN de software devem funcionar com nosso gateway desde que estejam em conformidade com as implementações de IPsec padrão tooindustry. Contate o fornecedor de saudação do software Olá para obter instruções de configuração e suporte.

## <a name="P2S"></a>Conexões Ponto a Site

[!INCLUDE [vpn-gateway-point-to-site-faq-include](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="V2VMulti"></a>Conexões Rede Virtual para Rede Virtual e Multissite

[!INCLUDE [vpn-gateway-vnet-vnet-faq-include](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

### <a name="can-i-use-azure-vpn-gateway-tootransit-traffic-between-my-on-premises-sites-or-tooanother-virtual-network"></a>Posso usar o tráfego de tootransit de gateway de VPN do Azure entre meus sites locais ou a rede virtual tooanother?

**Modelo de implantação do Resource Manager**<br>
Sim. Consulte Olá [BGP](#bgp) para obter mais informações.

**Modelo de implantação clássica**<br>
Tráfego de trânsito via gateway VPN do Azure é possível usando o modelo de implantação clássico hello, mas se baseia em espaços de endereço estaticamente definidos no arquivo de configuração de rede hello. BGP ainda não é suportado com gateways VPN e redes virtuais do Azure usando o modelo de implantação clássico hello. Sem BGP, a definição manual de espaços de endereço de trânsito é muito propensa a erros e não é recomendada.

### <a name="does-azure-generate-hello-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-hello-same-virtual-network"></a>O Azure gera Olá pré-compartilhada IPsec/IKE mesmo chave para todas as minhas conexões VPN para Olá mesmo rede virtual?

Não, por padrão, o Azure gera chaves pré-compartilhadas diferentes para conexões VPN diferentes. No entanto, você pode usar o hello definir API de REST chave de Gateway de VPN ou o PowerShell cmdlet tooset Olá valor chave que preferir. chave de saudação deve ser uma cadeia de caracteres alfanumérica de comprimento entre 1 too128 caracteres.

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a>Obtenho mais largura de banda com mais VPNs site a site do que com uma única rede virtual?

Não, todos os túneis VPN, incluindo VPNs ponto a Site, compartilham Olá mesmo VPN do Azure gateway e hello largura de banda disponível.

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a>Posso configurar vários túneis entre minha rede virtual e meu site local usando uma VPN multissite?

Sim, mas você deve configurar o BGP em ambos os túneis toohello mesmo local.

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a>Posso usar VPNs de ponto a site com minha rede virtual com vários túneis de VPN?

Sim, VPNs ponto a Site (P2S) podem ser usadas com os gateways de VPN Olá Conectando sites locais de toomultiple e outras redes virtuais.

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-toomy-expressroute-circuit"></a>Pode conectar uma rede virtual com VPNs IPsec toomy circuito ExpressRoute?

Sim, isso é suportado. Para obter mais informações, consulte [Configurar conexões de VPN Site a Site e de ExpressRoute que coexistam](../expressroute/expressroute-howto-coexist-classic.md).

## <a name="ipsecike"></a>Política do IPsec/IKE

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="bgp"></a>BGP

[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="vms"></a>Conectividade entre locais e VMs

### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-toohello-vm"></a>Se minha máquina virtual está em uma rede virtual e tenho uma conexão entre locais, como devo me conectar toohello VM?

Você tem algumas opções. Se você tiver um protocolo RDP habilitado para sua VM, você pode se conectar a máquina virtual de tooyour usando o endereço IP privado de saudação. Nesse caso, você deverá especificar o endereço IP privado de saudação e a porta de saudação que você deseja tooconnect muito (normalmente 3389). Você precisará tooconfigure porta de saudação em sua máquina virtual para o tráfego de saudação.

Você também pode conectar máquina virtual de tooyour por endereço IP privado de outra máquina virtual foi localizado no hello mesmo rede virtual. Não é possível RDP tooyour VM usando o endereço IP privado de saudação se você estiver se conectando de um local fora da sua rede virtual. Por exemplo, se você tiver uma rede virtual de ponto a Site configurado e não estabelecer uma conexão do seu computador, você não pode se conectar máquina virtual de toohello por endereço IP privado.

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-hello-traffic-from-my-vm-go-through-that-connection"></a>Se minha máquina virtual está em uma rede virtual com conectividade entre locais, todo o tráfego de saudação da minha VM percorrer essa conexão?

Não. Somente o tráfego de saudação que tem um destino de IP que está contida no hello rede virtual Local rede intervalos de endereços IP que você especificou passará pelo gateway de rede virtual hello. Tráfego tem um destino de IP localizado na rede virtual Olá permanece na rede virtual hello. Outro tráfego é enviada por meio de redes públicas de toohello Olá de Balanceador de carga, ou se for usado o túnel forçado, enviada pelo gateway de VPN do Azure de saudação.

### <a name="how-do-i-troubleshoot-an-rdp-connection-tooa-vm"></a>Como solucionar problemas de uma conexão de RDP tooa VM

[!INCLUDE [Troubleshoot VM connection](../../includes/vpn-gateway-connect-vm-troubleshoot-include.md)]


## <a name="faq"></a>Perguntas Frequentes da Rede Virtual

Exibir informações adicionais de rede virtual no hello [perguntas Frequentes de rede Virtual](../virtual-network/virtual-networks-faq.md).

## <a name="next-steps"></a>Próximas etapas

* Para saber mais sobre o Gateway de VPN, veja [Sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md).
* Para saber mais sobre definições de configuração de Gateway de VPN, veja [Sobre definições de configuração do Gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md).
