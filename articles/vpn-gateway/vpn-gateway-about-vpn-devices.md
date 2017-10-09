---
title: "aaaAbout dispositivos VPN para conexões do Azure entre locais | Microsoft Docs"
description: "Este artigo discute dispositivos VPN e os parâmetros de IPsec para conexões de Gateway de VPN S2S entre locais. Links são fornecidos exemplos e instruções de tooconfiguration."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: ba449333-2716-4b7f-9889-ecc521e4d616
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: yushwang;cherylmc
ms.openlocfilehash: 8b84afbf93d807342ecd56ab369d5909a13343e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-devices-and-ipsecike-parameters-for-site-to-site-vpn-gateway-connections"></a>Sobre dispositivos VPN e os parâmetros IPsec/IKE para conexões do Gateway de VPN site a site

Um dispositivo VPN é tooconfigure necessária uma conexão de VPN Site a Site (S2S) entre locais usando um gateway VPN. Conexões site a Site podem ser usado toocreate uma solução híbrida ou sempre que quiser conexões seguras entre suas redes locais e suas redes virtuais. Este artigo fornece uma lista dispositivos de VPN validados e uma lista de parâmetros IPsec/IKE para gateways de VPN.

> [!IMPORTANT]
> Se você estiver tendo problemas de conectividade entre os dispositivos VPN de local e gateways de VPN, consulte muito[problemas de compatibilidade de dispositivo](#known).
>
>

### <a name="items-toonote-when-viewing-hello-tables"></a>Itens toonote ao exibir tabelas hello:

* Houve uma mudança de terminologia para os gateways de VPN do Azure. Somente os nomes de saudação foram alterados. Não há nenhuma alteração de funcionalidade.
  * Roteamento estático = PolicyBased
  * Roteamento dinâmico = RouteBased
* Especificações de gateway VPN HighPerformance e gateway VPN RouteBased são Olá mesmo, a menos que indicado o contrário. Por exemplo, dispositivos VPN Olá validado que são compatíveis com gateways de VPN RouteBased também são compatíveis com hello gateway HighPerformance VPN.

## <a name="devicetable"></a>Dispositivos VPN validados e guias de configuração do dispositivo

> [!NOTE]
> Ao configurar uma conexão Site a Site, um endereço IP IPv4 público é necessário para seu dispositivo VPN.
>

Validamos um conjunto de dispositivos VPN padrão em parceria com fornecedores de dispositivos. Todos os dispositivos de saudação em famílias de dispositivos de saudação em Olá lista a seguir devem funcionar com gateways de VPN. Consulte [sobre configurações de Gateway VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype) toounderstand Olá VPN digite use (PolicyBased ou RouteBased) para Olá deseja tooconfigure de solução de Gateway de VPN.

toohelp configurar seu dispositivo VPN, consulte os links de toohello que correspondem a família do dispositivo tooappropriate. são fornecidas instruções de tooconfiguration de links de saudação em uma base de melhor esforço. Para obter suporte ao dispositivo VPN, entre em contato com o fabricante do dispositivo.

|**Fornecedor**          |**Família do dispositivo**     |**Versão mínima do sistema operacional** |**Instruções de configuração PolicyBased** |**Instruções de configuração RouteBased** |
| ---                | ---                  | ---                   | ---            | ---           |
| A10 Networks, Inc. |Thunder CFW           |ACOS 4.1.1             |Incompatível  |[Guia de Configuração](https://www.a10networks.com/resources/deployment-guides/a10-thunder-cfw-ipsec-vpn-interoperability-azure-vpn-gateways)|
| Allied Telesis     |Série AR de roteadores VPN |2.9.2                  |Em breve     |Não compatível  |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall F-series |PolicyBased: 5.4.3<br>RouteBased: 6.2.0 |[Guia de Configuração](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[Guia de Configuração](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall X-series |Barracuda Firewall 6.5 |[Guia de Configuração](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |Não compatível |
| Brocade            |Vyatta 5400 vRouter   |Roteador virtual 6.6R3 GA|[Guia de Configuração](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |Não compatível |
| Ponto de Verificação |Gateway de segurança |R77.30 |[Guia de Configuração](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[Guia de Configuração](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| Cisco              |ASA       |8.3 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |Não compatível |
| Cisco |ASR |PolicyBased: IOS 15.1<br>RouteBased: IOS 15.2 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| Cisco |ISR |PolicyBased: IOS 15.0<br>RouteBased*: IOS 15.1 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[Exemplos de configuração*](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
| Citrix |NetScaler MPX, SDX, VPX |10.1 e acima |[Guia de Configuração](https://docs.citrix.com/en-us/netscaler/11-1/system/cloudbridge-connector-introduction/cloudbridge-connector-azure.html) |Não compatível |
| F5 |Série BIG-IP |12.0 |[Guia de Configuração](https://devcentral.f5.com/articles/connecting-to-windows-azure-with-the-big-ip) |[Guia de Configuração](https://devcentral.f5.com/articles/big-ip-to-azure-dynamic-ipsec-tunneling) |
| Fortinet |FortiGate |FortiOS 5.4.2 |  |[Guia de Configuração](http://cookbook.fortinet.com/ipsec-vpn-microsoft-azure-54) |
| Internet Initiative Japan (IIJ) |Série SEIL |SEIL/X 4.60<br>SEIL/B1 4.60<br>SEIL/x86 3.20 |[Guia de Configuração](http://www.iij.ad.jp/biz/seil/ConfigAzureSEILVPN.pdf) |Não compatível |
| Juniper |SRX |PolicyBased: JunOS 10.2<br>Routebased: JunOS 11.4 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |
| Juniper |Série J |PolicyBased: JunOS 10.4r9<br>RouteBased: JunOS 11.4 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |
| Juniper |ISG |ScreenOS 6.3 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |
| Juniper |SSG |ScreenOS 6.2 |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |[Exemplos de configuração](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |
| Microsoft |Serviço de Roteamento e Acesso Remoto |Windows Server 2012 |Não compatível |[Exemplos de configuração](http://go.microsoft.com/fwlink/p/?LinkId=717761) |
| AG de sistemas abertos |Gateway de Segurança de Controle de Missão |N/D |[Guia de Configuração](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |Não compatível |
| Openswan |Openswan |2.6.32 |(Em breve) |Não compatível |
| Redes Palo Alto |Todos os dispositivos executando PAN-OS |PAN-OS<br>PolicyBased: 6.1.5 ou posterior<br>RouteBased: 7.1.4 |[Guia de Configuração](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[Guia de Configuração](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| SonicWall |Série TZ, série NSA<br>Série SuperMassive<br>Série NSA E-Class |SonicOS 5.8.x<br>SonicOS 5.9.x<br>SonicOS 6.x |[Guia de configuração para o SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Guia de configuração para o SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |[Guia de configuração para o SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Guia de configuração para o SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |
| WatchGuard |Todos |Fireware XTM<br> PolicyBased: v11.11.x<br>RouteBased: v11.12.x |[Guia de Configuração](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA2F00000000LI7KAM&lang=en_US) |[Guia de Configuração](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA22A000000XZogSAG&lang=en_US)|

(*) Os roteadores da Série ISR 7200 só oferecem suporte a VPNs PolicyBased.

## <a name="additionaldevices"></a>Dispositivos VPN não validados

Se você não encontrar seu dispositivo listado na tabela de dispositivos VPN validados hello, seu dispositivo ainda pode trabalhar com uma conexão Site a Site. Entre em contato com o fabricante do dispositivo para obter instruções adicionais de configuração e suporte.

## <a name="editing"></a>Edição de exemplos de configuração de dispositivo

Depois de baixar o exemplo de configuração de dispositivo VPN Olá fornecido, será necessário tooreplace alguns Olá valores tooreflect configurações de saudação para seu ambiente.

### <a name="tooedit-a-sample"></a>tooedit um exemplo:

1. Abra o exemplo hello usando o bloco de notas.
2. Pesquisar e substituir tudo <*texto*> cadeias de caracteres com valores hello pertinentes tooyour ambiente. Ser tooinclude se < e >. Quando um nome é especificado, o nome de saudação que você selecionar deve ser exclusivo. Se um comando não funcionar, consulte a documentação do fabricante do dispositivo.

| **Texto de exemplo** | **Alterar para** |
| --- | --- |
| &lt;RP_OnPremisesNetwork&gt; |O nome que você escolheu para este objeto. Exemplo: myOnPremisesNetwork |
| &lt;RP_AzureNetwork&gt; |O nome que você escolheu para este objeto. Exemplo: myAzureNetwork |
| &lt;RP_AccessList&gt; |O nome que você escolheu para este objeto. Exemplo: myAzureAccessList |
| &lt;RP_IPSecTransformSet&gt; |O nome que você escolheu para este objeto. Exemplo: myIPSecTransformSet |
| &lt;RP_IPSecCryptoMap&gt; |O nome que você escolheu para este objeto. Exemplo: myIPSecCryptoMap |
| &lt;SP_AzureNetworkIpRange&gt; |Especifique o intervalo. Exemplo: 192.168.0.0 |
| &lt;SP_AzureNetworkSubnetMask&gt; |Especificar máscara de sub-rede. Exemplo: 255.255.0.0 |
| &lt;SP_OnPremisesNetworkIpRange&gt; |Especifique o intervalo local. Exemplo: 10.2.1.0 |
| &lt;SP_OnPremisesNetworkSubnetMask&gt; |Especifique a máscara de sub-rede local. Exemplo: 255.255.255.0 |
| &lt;SP_AzureGatewayIpAddress&gt; |Esta rede virtual de tooyour específicas de informações e está localizado no Portal de gerenciamento de saudação como **endereço IP do Gateway**. |
| &lt;SP_PresharedKey&gt; |Essas informações é a rede virtual específico tooyour e estão localizadas no Portal de gerenciamento como gerenciar chave de saudação. |

## <a name="ipsec"></a>Parâmetros IPsec/IKE

> [!NOTE]
> Embora Olá valores listados no Olá a tabela a seguir têm suporte pelo gateway VPN Olá, atualmente há não é nenhum mecanismo para que você toospecify ou selecione uma combinação específica de algoritmos ou parâmetros de gateway VPN hello. Você deve especificar quaisquer restrições de dispositivo VPN de local de saudação. Além disso, você deve fixar **MSS** em **1350**.
> 
>

Em Olá tabelas a seguir:

* SA = Associação de segurança
* Fase 1 de IKE também é chamada de "Modo Principal"
* Fase 2 de IKE também é chamada de "Modo Rápido"

### <a name="ike-phase-1-main-mode-parameters"></a>Parâmetros da Fase 1 de IKE (Modo Principal)

| **Propriedade**          |**PolicyBased**    | **RouteBased**    |
| ---                   | ---               | ---               |
| Versão IKE           |IKEv1              |IKEv2              |
| Grupo Diffie-Hellman  |Grupo 2 (1024 bits) |Grupo 2 (1024 bits) |
| Método de autenticação |Chave Pré-Compartilhada     |Chave Pré-Compartilhada     |
| Criptografia e algoritmos de hash |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |1. AES256, SHA1<br>2. AES256, SHA256<br>3. AES128, SHA1<br>4. AES128, SHA256<br>5. 3DES, SHA1<br>6. 3DES, SHA256 |
| Tempo de vida da SA           |28.800 segundos     |28.800 segundos     |

### <a name="ike-phase-2-quick-mode-parameters"></a>Parâmetros da Fase 2 de IKE (Modo Rápido)

| **Propriedade**                  |**PolicyBased**| **RouteBased**                              |
| ---                           | ---           | ---                                         |
| Versão IKE                   |IKEv1          |IKEv2                                        |
| Criptografia e algoritmos de hash |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |[Ofertas QM SA RouteBased](#RouteBasedOffers) |
| Tempo de vida da SA (Tempo)            |3.600 segundos  |27.000 segundos                                |
| Tempo de vida da SA (Bytes)           |102.400.000 KB | -                                           |
| PFS (Perfect Forward Secrecy) |Não             |[Ofertas QM SA RouteBased](#RouteBasedOffers) |
| Detecção de par inativo (DPD)     |Sem suporte  |Suportado                                    |


### <a name ="RouteBasedOffers"></a>Ofertas de associação de segurança de VPN RouteBased (SA IKE Modo Rápido)

Olá tabela a seguir lista as ofertas de SA do IPsec (IKE modo rápido). Ofertas são ordem Olá listados de preferência oferta Olá é apresentada ou aceita.

#### <a name="azure-gateway-as-initiator"></a>Gateway do Azure como iniciador

|-  |**Criptografia**|**Autenticação**|**Grupo PFS**|
|---| ---          |---               |---          |
| 1 |GCM AES256    |GCM (AES256)      |Nenhum         |
| 2 |AES256        |SHA1              |Nenhum         |
| 3 |3DES          |SHA1              |Nenhum         |
| 4 |AES256        |SHA256            |Nenhum         |
| 5 |AES128        |SHA1              |Nenhum         |
| 6 |3DES          |SHA256            |Nenhum         |

#### <a name="azure-gateway-as-responder"></a>Gateway do Azure como respondente

|-  |**Criptografia**|**Autenticação**|**Grupo PFS**|
|---| ---          | ---              |---          |
| 1 |GCM AES256    |GCM (AES256)      |Nenhum         |
| 2 |AES256        |SHA1              |Nenhum         |
| 3 |3DES          |SHA1              |Nenhum         |
| 4 |AES256        |SHA256            |Nenhum         |
| 5 |AES128        |SHA1              |Nenhum         |
| 6 |3DES          |SHA256            |Nenhum         |
| 7 |DES           |SHA1              |Nenhum         |
| 8 |AES256        |SHA1              |1            |
| 9 |AES256        |SHA1              |2            |
| 10|AES256        |SHA1              |14           |
| 11|AES128        |SHA1              |1            |
| 12|AES128        |SHA1              |2            |
| 13|AES128        |SHA1              |14           |
| 14|3DES          |SHA1              |1            |
| 15|3DES          |SHA1              |2            |
| 16|3DES          |SHA256            |2            |
| 17|AES256        |SHA256            |1            |
| 18|AES256        |SHA256            |2            |
| 19|AES256        |SHA256            |14           |
| 20|AES256        |SHA1              |24           |
| 21|AES256        |SHA256            |24           |
| 22|AES128        |SHA256            |Nenhum         |
| 23|AES128        |SHA256            |1            |
| 24|AES128        |SHA256            |2            |
| 25|AES128        |SHA256            |14           |
| 26|3DES          |SHA1              |14           |

* Você pode especificar a criptografia NULL de IPsec ESP com gateways de VPN RouteBased e de Alto Desempenho. Criptografia com base em nulo não oferece proteção toodata em trânsito e só deve ser usada quando o máximo é exigida latência mínima e de taxa de transferência. Clientes podem escolher toouse isso em cenários de comunicação VNet para VNet, ou quando a criptografia está sendo aplicada em outro lugar na solução de saudação.
* Para conectividade entre locais através de saudação à Internet, use configurações de gateway de VPN do Azure saudação padrão com criptografia e algoritmos de hash listados nas tabelas de saudação acima tooensure segurança da comunicação crítica.

## <a name="known"></a>Problemas conhecidos de compatibilidade de dispositivos

> [!IMPORTANT]
> Esses são Olá problemas de compatibilidade conhecidos entre dispositivos VPN de terceiros e gateways de VPN do Azure. Olá, equipe do Azure está trabalhando ativamente com fornecedores de saudação tooaddress Olá problemas listados aqui. Quando problemas de saudação são resolvidos, essa página será atualizada com as informações mais atualizadas hello. Verifique periodicamente.
>
>

### <a name="feb-16-2017"></a>16 de fevereiro de 2017

**Dispositivos de redes Palo Alto com too7.1.4 anterior da versão** para VPN do Azure baseadas em rota: se você estiver usando dispositivos VPN de redes Palo Alto com PAN-OS versão anterior too7.1.4 e estiver enfrentando conectividade emite tooAzure baseadas em rota gateways VPN, Execute Olá etapas a seguir:

1. Verificar a versão do firmware de saudação do seu dispositivo Palo Alto Networks. Se sua versão PAN-OS mais antigo que 7.1.4, atualize too7.1.4.
2. No dispositivo de redes Palo Alto hello, alterar Olá too28 tempo de vida do SA de fase 2 (ou SA de modo rápido), 800 segundos (8 horas) ao conectar-se toohello gateway de VPN do Azure.
3. Se você ainda estiver tendo problemas de conectividade, abra uma solicitação de suporte de saudação portal do Azure.
