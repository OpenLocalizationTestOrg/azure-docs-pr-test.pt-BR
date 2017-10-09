### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>A política de IPsec/IKE personalizada tem suporte em todos os SKUs de Gateway de VPN do Azure?
A política de IPsec/IKE personalizada tem suporte nos gateways de VPN do Azure **VpnGw1, VpnGw2, VpnGw3, Standard** e **HighPerformance**. **Basic** não tem suporte.

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>Quantas políticas eu posso especificar em uma conexão?
Você só pode especificar ***uma*** combinação de políticas para uma determinada conexão.

### <a name="can-i-specify-a-partial-policy-on-a-connection-eg-only-ike-algorithms-but-not-ipsec"></a>Eu posso especificar uma política parcial em uma conexão? (Por exemplo, somente os algoritmos de IKE mas não IPsec)
Não, você deve especificar todos os algoritmos e parâmetros para IKE (modo principal) e IPsec (modo rápido). A especificação de política parcial não é permitida.

### <a name="what-are-hello-algorithms-and-key-strengths-supported-in-hello-custom-policy"></a>Quais são os algoritmos de saudação e restrições de chave com suporte em política personalizada do hello?
Olá tabela a seguir lista Olá suporte para algoritmos de criptografia e restrições de chave podem ser configuradas por clientes hello. Você deve selecionar uma opção para cada campo.

| **IPsec/IKEv2**  | **Opções**                                                                   |
| ---              | ---                                                                           |
| Criptografia IKEv2 | AES256, AES192, AES128, DES3, DES                                             |
| Integridade do IKEv2  | SHA384, SHA256, SHA1, MD5                                                     |
| Grupo DH         | DHGroup24, ECP384, ECP256, DHGroup14 (DHGroup2048), DHGroup2, DHGroup1, nenhum |
| Criptografia IPsec | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, nenhum      |
| Integridade do IPsec  | GCMAES256, GCMAES192, GCMAES128, SHA256, SHA1, MD5                            |
| Grupo PFS        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, nenhum                              |
| Tempo de vida da QM SA   | Segundos (inteiro; **mínimo de 300**/padrão de 27000 segundos)<br>KBytes (inteiro; **mín. de 1024** /padrão de 102400000 KBytes)           |
| Seletor de tráfego | UsePolicyBasedTrafficSelectors ($True/$False; default $False)                 |
|                  |                                                                               |

> [!IMPORTANT]
> 1. DHGroup2048 & PFS2048 são Olá mesmo como o grupo Diffie-Hellman **14** em IKE e IPsec PFS. Consulte [grupos Diffie-Hellman](#DH) para Olá concluir mapeamentos.
> 2. Para os algoritmos GCMAES, você deve especificar Olá mesmo comprimento GCMAES algoritmo e a chave de criptografia IPsec e integridade.
> 3. Tempo de vida do SA do modo principal IKEv2 é fixo em 28.800 segundos em gateways de VPN do Azure Olá
> 4. As Vidas Úteis de SA QM são parâmetros opcionais. Se nenhum for especificado, os valores padrão de 27.000 segundos (7,5 horas) e 102400000 KBytes (102 GB) são usados.
> 5. UsePolicyBasedTrafficSelector é um parâmetro de opção de conexão de saudação. Consulte Perguntas frequentes sobre o hello próximo item para "UsePolicyBasedTrafficSelectors"

### <a name="does-everything-need-toomatch-between-hello-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>Tudo o que é necessário toomatch entre hello política de gateway de VPN do Azure e Minhas configurações de dispositivo VPN local?
A configuração de dispositivo VPN local deve corresponder ou conter Olá algoritmos a seguir e parâmetros que você especificar na Olá diretiva IPsec/IKE do Azure:

* Algoritmo de criptografia IKE
* Algoritmo de integridade de IKE
* Grupo DH
* Algoritmo de criptografia IPsec
* Algoritmo de integridade de IPsec
* Grupo PFS
* Seletor de tráfego (*)

tempos de vida Olá SA especificações locais apenas, não é necessário toomatch.

Se você habilitar **UsePolicyBasedTrafficSelectors**, você precisa tooensure seu dispositivo VPN tem Olá correspondência seletores de tráfego definidos com todas as combinações de seu local (gateway de rede local) de prefixos de rede de saudação Prefixos de rede virtual do Azure, em vez de para qualquer. Por exemplo, se os prefixos de rede local são 10.1.0.0/16 e 10.2.0.0/16, e os prefixos de rede virtual são 192.168.0.0/16 e 172.16.0.0/16, você precisa toospecify Olá seletores de tráfego a seguir:
* 10.1.0.0/16 <====> 192.168.0.0/16
* 10.1.0.0/16 <====> 172.16.0.0/16
* 10.2.0.0/16 <====> 192.168.0.0/16
* 10.2.0.0/16 <====> 172.16.0.0/16

Consulte também[conectar dispositivos VPN baseado em políticas vários locais](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) para obter mais detalhes sobre como toouse essa opção.

### <a name ="DH"></a>Há suporte para quais grupos Diffie-Hellman?
Olá tabela a seguir lista Olá suporte para grupos de Diffie-Hellman IKE (DHGroup) e IPsec (PFSGroup):

| **Grupo Diffie-Hellman**  | **DHGroup**              | **PFSGroup** | **Comprimento da chave** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | MODP de 768 bits   |
| 2                         | DHGroup2                 | PFS2         | MODP de 1024 bits  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP de 2048 bits  |
| 19                        | ECP256                   | ECP256       | ECP de 256 bits    |
| 20                        | ECP384                   | ECP284       | ECP de 384 bits    |
| 24                        | DHGroup24                | PFS24        | MODP de 2048 bits  |
|                           |                          |              |                |

Consulte também[RFC3526](https://tools.ietf.org/html/rfc3526) e [RFC5114](https://tools.ietf.org/html/rfc5114) para obter mais detalhes.

### <a name="does-hello-custom-policy-replace-hello-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>Política personalizada do hello substituir conjuntos de diretiva de IPsec/IKE saudação padrão para gateways de VPN do Azure?
Sim, depois que uma política personalizada for especificada em uma conexão, gateway VPN do Azure só usará Olá política na conexão hello, como iniciador IKE e o respondedor IKE.

### <a name="if-i-remove-a-custom-ipsecike-policy-does-hello-connection-become-unprotected"></a>Se remover uma política personalizada do IPsec/IKE, conexão Olá ficará desprotegido?
Não, conexão Olá ainda será protegido pelo IPsec/IKE. Quando você remover a política personalizada de saudação de uma conexão, gateway de VPN do Azure Olá reverterá back toohello [lista padrão de propostas de IPsec/IKE](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md) e reinicie hello handshake IKE novamente com seu dispositivo VPN local.

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>Adicionar ou atualizar uma política de IPsec/IKE pode atrapalhar minha conexão VPN?
Sim, isso pode causar uma pequena interrupção (alguns segundos) como gateway de VPN do Azure Olá será subdividir a conexão existente hello e reinicie Olá IKE handshake toore-estabelecer o túnel IPsec de saudação com novos algoritmos de criptografia hello e parâmetros. Verifique se que o dispositivo VPN local também é configurado com algoritmos de correspondência de saudação e restrições de chave toominimize Olá de interrupção.

### <a name="can-i-use-different-policies-on-different-connections"></a>Eu posso usar políticas diferentes em conexões diferentes?
Sim. A política personalizada é aplicada em uma base por conexão. Você pode criar e aplicar políticas de IPsec/IKE diferentes em conexões diferentes. Você também pode escolher tooapply políticas personalizadas em um subconjunto de conexões. Olá os restantes irá usar conjuntos de diretiva de IPsec/IKE saudação padrão do Azure.

### <a name="can-i-use-hello-custom-policy-on-vnet-to-vnet-connection-as-well"></a>Pode usar política personalizada de saudação na conexão de rede virtual a rede também?
Sim, você pode aplicar a política personalizada em conexões entre locais de IPsec ou conexões de VNet para VNet.

### <a name="do-i-need-toospecify-hello-same-policy-on-both-vnet-to-vnet-connection-resources"></a>É necessário toospecify Olá política mesmo em ambos os recursos de conexão de VNet para VNet?
Sim. Um túnel de VNet para VNet consiste em dois recursos de conexão no Azure, uma para cada sentido. Você precisa tooensure tem ambos os recursos de conexão Olá a mesma diretiva, Olá othereise conexão de rede virtual a rede não estabelecerá.

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>A política de IPsec/IKE personalizada funciona em conexão de ExpressRoute?
Não. Diretiva IPsec/IKE só funciona em VPN S2S e conexões de rede virtual a rede por meio de gateways de VPN do Azure hello.
