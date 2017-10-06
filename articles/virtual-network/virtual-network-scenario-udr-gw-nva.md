---
title: "aaaHybrid conexão com o aplicativo da camada 2 | Microsoft Docs"
description: "Saiba como toodeploy dispositivos virtuais e UDR toocreate um ambiente de aplicativo de várias camadas no Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 1f509bec-bdd1-470d-8aa4-3cf2bb7f6134
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/05/2016
ms.author: jdial
ms.openlocfilehash: 53599862289dbf9c6ab3289b0cb8dda6430f20f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-appliance-scenario"></a>Cenário de dispositivo virtual
Um cenário comum entre o cliente do Azure maior é Olá necessidade tooprovide toohello um aplicativo de duas camadas exposto à Internet, permitindo a camada de voltar de toohello acesso de um datacenter local. Este documento orientará você por meio de um cenário usando toodeploy de soluções de virtualização de rede, um Gateway de VPN e rotas de definida pelo usuário (UDR) um ambiente de duas camadas que atenda Olá requisitos a seguir:

* Aplicativo Web deve ser acessível de Olá somente Internet pública.
* Aplicativo hello hospedagem do servidor Web deve ser capaz de tooaccess um servidor de aplicativos back-end.
* Todo o tráfego de saudação aplicativo da web toohello Internet deve passar por um dispositivo virtual do firewall. Este dispositivo virtual será usado apenas para o tráfego de Internet.
* Todo o tráfego direcionado toohello servidor de aplicativos deve passar por um dispositivo virtual do firewall. Este dispositivo virtual será usado para o servidor final do acesso toohello back-end e vindos de rede do local de saudação por meio de um Gateway de VPN de acesso.
* Os administradores devem ser capaz de toomanage Olá firewall soluções de virtualização de seus computadores locais, por meio de um terceiro firewall usado exclusivamente para fins de gerenciamento de dispositivo virtual.

Esse é um cenário de DMZ padrão com um DMZ e uma rede protegida. Esse cenário pode ser criado no Azure usando NSGs, dispositivos virtuais de firewall ou uma combinação de ambos. Olá tabela a seguir mostra alguns dos profissionais hello e os contras entre NSGs e dispositivos virtuais do firewall.

|  | Prós | Contras |
| --- | --- | --- |
| NSG |Sem custo. <br/>Integrado ao RBAC do Azure. <br/>As regras podem ser criadas em modelos Aa ARM. |A complexidade pode variar em ambientes maiores. |
| Firewall |Controle total sobre o plano de dados. <br/>Gerenciamento central por meio do console do firewall. |Custo do dispositivo de firewall. <br/>Não é integrado ao RBAC do Azure. |

solução de saudação abaixo usa o firewall dispositivos virtuais tooimplement um cenário de rede DMZ/protegido.

## <a name="considerations"></a>Considerações
Você pode implantar o ambiente Olá explicado acima no Azure usando os diferentes recursos disponíveis hoje, da seguinte maneira.

* **Rede virtual (VNet)**. Uma rede virtual do Azure atua na rede de local de tooan de maneira semelhante e podem ser segmentada em um ou mais isolamento de tráfego tooprovide sub-redes e separação de preocupações.
* **Dispositivo virtual**. Vários parceiros fornecem soluções de virtualização em hello Azure Marketplace que pode ser usado para Olá três firewalls descritos acima. 
* **UDR (Rotas Definidas pelo Usuário)**. Tabelas de rotas podem conter UDRs usadas por fluxo de saudação toocontrol rede Azure de pacotes em uma rede virtual. Essas tabelas de rota podem ser aplicadas toosubnets. Um dos recursos mais recentes de saudação no Azure é Olá capacidade tooapply uma tabela de rota toohello GatewaySubnet, fornecendo Olá capacidade tooforward todo o tráfego entra Olá VNet do Azure de uma solução de virtualização de tooa de conexão híbrida.
* **Encaminhamento IP**. Por padrão, o hello Azure mecanismo rede encaminhar pacotes toovirtual placas de interface de rede (NICs) somente se o endereço IP de destino do pacote hello corresponde Olá endereço IP da NIC. Portanto, se um UDR define se um pacote deve ser enviado tooa dado dispositivo virtual, Olá mecanismo de rede do Azure deve cancelar esse pacote. pacote de saudação tooensure é entregue tooa VM (no caso um dispositivo virtual) que não é um destino de saudação real para o pacote de saudação, você precisa tooenable encaminhamento IP para o dispositivo virtual Olá.
* **NSGs (Grupos de Segurança de Rede)**. exemplo Hello abaixo não faz uso de NSGs, mas você pode usar os NSGs aplicados toohello sub-redes e/ou NICs nessa solução toofurther filtro Olá tráfego entra e sai os NICs e sub-redes.

![Conectividade IPv6](./media/virtual-network-scenario-udr-gw-nva/figure01.png)

Neste exemplo, há uma assinatura que contém Olá seguinte:

* 2 grupos de recursos, não é mostrados no diagrama de saudação. 
  * **ONPREMRG**. Contém todos os recursos toosimulate necessário uma rede local.
  * **AZURERG**. Contém todos os recursos necessários para o ambiente de rede virtual do Azure hello. 
* Uma rede virtual denominada **onpremvnet** usado toomimic um datacenter local segmentado como listado abaixo.
  * **onpremsn1**. Sub-rede que contém uma máquina virtual (VM) que executa o Ubuntu toomimic um servidor de local.
  * **onpremsn2**. Sub-rede que contém uma VM em execução Ubuntu toomimic um computador local usado por um administrador.
* Há um dispositivo virtual de firewall denominado **OPFW** na **onpremvnet** usado toomaintain um túnel muito**azurevnet**.
* Uma VNet denominada **azurevnet** segmentada como listado abaixo.
  * **azsn1**. Subrede firewall externo usado exclusivamente para firewall externo hello. Todo o tráfego da Internet será proveniente desta sub-rede. Essa sub-rede contém apenas um firewall externo de toohello NIC vinculado.
  * **azsn2**. Subrede front-end hospeda uma VM em execução como um servidor web que será acessado de saudação à Internet.
  * **azsn3**. Sub-rede de back-end que hospeda uma VM que executa um servidor de aplicativos back-end que será acessado pelo servidor de web de front-end de saudação.
  * **azsn4**. A sub-rede de gerenciamento usada exclusivamente tooprovide gerenciamento acesso tooall firewall dispositivos virtuais. Essa sub-rede contém apenas uma NIC para cada dispositivo virtual firewall usado na solução de saudação.
  * **GatewaySubnet**. Sub-rede de conexão híbrida do Azure necessário para Gateway de VPN e rota expressa conectividade tooprovide entre VNets do Azure e outras redes. 
* Há 3 dispositivos virtuais do firewall em Olá **azurevnet** rede. 
  * **AZF1**. Firewall externo exposto toohello Internet pública usando um recurso de endereço IP público no Azure. É necessário tooensure possui um modelo de saudação Marketplace ou diretamente de seu fornecedor de dispositivo, que provisiona um dispositivo virtual 3-NIC.
  * **AZF2**. Firewall interno usado toocontrol o tráfego entre **azsn2** e **azsn3**. Isso também é um dispositivo virtual de 3 NICs.
  * **AZF3**. Firewall de gerenciamento tooadministrators acessível de saudação datacenter local e sub-rede de gerenciamento conectado tooa usado toomanage todos os dispositivos de firewall. Você pode encontrar NIC 2 modelos de dispositivo virtual em Olá Marketplace ou solicitar uma diretamente de seu fornecedor de dispositivo.

## <a name="user-defined-routing-udr"></a>Roteamento definido pelo usuário (UDR)
Cada sub-rede no Azure pode ser vinculado tooa UDR tabela usada toodefine como tráfego iniciado nessa sub-rede é roteado. Se nenhum UDRs estiverem definidas, o Azure usa padrão rotas tooallow tráfego tooflow de tooanother de uma sub-rede. toobetter entender UDRs, visite [quais são rotas definidas pelo usuário e encaminhamento IP](virtual-networks-udr-overview.md#ip-forwarding).

comunicação tooensure é feita por meio do dispositivo de firewall correto hello, baseado no requisito de última de saudação acima, você precisa toocreate Olá seguinte tabela de rota contendo UDRs em **azurevnet**.

### <a name="azgwudr"></a>azgwudr
Nesse cenário, Olá somente tráfego que flui de tooAzure local será usado toomanage Olá firewalls conectando-se muito**AZF3**, e que o tráfego deve passar pelo firewall interno de Olá, **AZF2**. Portanto, apenas uma rota é necessária em Olá **GatewaySubnet** conforme mostrado abaixo.

| Destino | Próximo salto | Explicação |
| --- | --- | --- |
| 10.0.4.0/24 |10.0.3.11 |Permite que o firewall de gerenciamento local tráfego tooreach **AZF3** |

### <a name="azsn2udr"></a>azsn2udr
| Destino | Próximo salto | Explicação |
| --- | --- | --- |
| 10.0.3.0/24 |10.0.2.11 |Permite que a sub-rede de back-end do tráfego toohello hospeda o servidor de aplicativo hello por meio de **AZF2** |
| 0.0.0.0/0 |10.0.2.10 |Permite que todos os outros toobe do tráfego roteado por **AZF1** |

### <a name="azsn3udr"></a>azsn3udr
| Destino | Próximo salto | Explicação |
| --- | --- | --- |
| 10.0.2.0/24 |10.0.3.10 |Permite que o tráfego muito**azsn2** tooflow do servidor Web toohello de servidor do aplicativo por meio de **AZF2** |

Você também precisa toocreate tabelas de rotas para sub-redes Olá **onpremvnet** toomimic Olá datacenter local.

### <a name="onpremsn1udr"></a>onpremsn1udr
| Destino | Próximo salto | Explicação |
| --- | --- | --- |
| 192.168.2.0/24 |192.168.1.4 |Permite que o tráfego muito**onpremsn2** por meio de **OPFW** |

### <a name="onpremsn2udr"></a>onpremsn2udr
| Destino | Próximo salto | Explicação |
| --- | --- | --- |
| 10.0.3.0/24 |192.168.2.4 |Permite que o tráfego toohello feito sub-rede no Azure por meio de **OPFW** |
| 192.168.1.0/24 |192.168.2.4 |Permite que o tráfego muito**onpremsn1** por meio de **OPFW** |

## <a name="ip-forwarding"></a>encaminhamento IP
UDR e encaminhamento de IP são recursos que você pode usar em combinação tooallow dispositivos virtuais toobe usado toocontrol fluxo de tráfego em uma rede virtual do Azure.  Um dispositivo virtual é nada mais que uma VM que executa um tráfego de rede do aplicativo usado toohandle de alguma forma, como um firewall ou um dispositivo NAT.

Este dispositivo virtual que VM deve ser capaz de tooreceive tráfego de entrada que é não resolvidos tooitself. tooallow um tráfego de tooreceive VM endereçado tooother destinos, você deve habilitar o encaminhamento IP para Olá VM. Este é um Azure configuração, não é uma configuração no sistema de operacional convidado hello. Seu dispositivo virtual ainda necessidades toorun algum tipo de aplicativo toohandle Olá tráfego de entrada e encaminhá-lo adequadamente.

toolearn mais sobre o encaminhamento de IP, visite [quais são rotas definidas pelo usuário e encaminhamento IP](virtual-networks-udr-overview.md#ip-forwarding).

Por exemplo, imagine que você tenha Olá após a instalação em uma rede virtual do Azure:

* A sub-rede **onpremsn1** contém uma VM denominada **onpremvm1**.
* A sub-rede **onpremsn2** contém uma VM chamada **onpremvm2**.
* Um dispositivo virtual denominado **OPFW** está conectado muito**onpremsn1** e **onpremsn2**.
* Uma rota definida pelo usuário vinculado muito**onpremsn1** Especifica que todo o tráfego muito**onpremsn2** devem ser enviadas muito**OPFW**.

No ponto, se **onpremvm1** tenta uma conexão com a tooestablish **onpremvm2**, hello UDR será usado e o tráfego será enviado muito**OPFW** como próximo salto de saudação. Tenha em mente que Olá destino real do pacote não está sendo alterada, ela ainda apresenta **onpremvm2** é o destino de saudação. 

Sem o encaminhamento IP habilitado para **OPFW**, Olá lógica de rede virtual do Azure descartará o pacote hello, desde que ela só permita que pacotes enviado de toobe tooa VM se hello o endereço IP da VM é o destino de Olá para pacote de saudação.

Com o encaminhamento IP, Olá lógica da rede virtual do Azure encaminhará Olá pacotes tooOPFW, sem alterar seu endereço de destino original. **OPFW** deve manipular pacotes de saudação e determinar quais toodo com eles.

Para o cenário de saudação acima toowork, você deve habilitar o encaminhamento IP nas NICs hello para **OPFW**, **AZF1**, **AZF2**, e **AZF3** que são usados para roteamento de (todas as NICs exceto Olá aqueles toohello vinculado gerenciamento sub-rede). 

## <a name="firewall-rules"></a>Regras de firewall
Conforme descrito acima, somente encaminhamento de IP garante que os pacotes são enviados a dispositivos virtuais toohello. Seu dispositivo ainda precisa toodecide que toodo com esses pacotes. Cenário de saudação acima, você precisará Olá toocreate seguindo as regras em seus dispositivos:

### <a name="opfw"></a>OPFW
OPFW representa um dispositivo local que contém a saudação regras a seguir:

* **Rota**: todo o tráfego too10.0.0.0/16 (**azurevnet**) deve ser enviado por meio de túnel **ONPREMAZURE**.
* **Política**: permitir todo o tráfego bidirecional entre **port2** e **ONPREMAZURE**.

### <a name="azf1"></a>AZF1
AZF1 representa um dispositivo virtual do Azure que contém a saudação regras a seguir:

* **Política**: permitir todo o tráfego bidirecional entre **port1** e **port2**.

### <a name="azf2"></a>AZF2
AZF2 representa um dispositivo virtual do Azure que contém a saudação regras a seguir:

* **Rota**: todo o tráfego too10.0.0.0/16 (**onpremvnet**) deve ser enviado de endereço IP de gateway do Azure toohello (ou seja, 10.0.0.1) por meio de **port1**.
* **Política**: permitir todo o tráfego bidirecional entre **port1** e **port2**.

## <a name="network-security-groups-nsgs"></a>Grupos de segurança de rede (NSG)
Nesse cenário, os NSGs não estão sendo usados. No entanto, você pode aplicar os NSGs tooeach toorestrict entrado e saído o tráfego de sub-rede. Por exemplo, você pode aplicar Olá sub-rede toohello FW externa regras NSG a seguir.

**Entrada**

* Permitir todo o tráfego TCP de saudação Internet tooport 80 em qualquer máquina virtual na sub-rede hello.
* Nega todo o tráfego de saudação à Internet.

**Saída**

* Nega todas as toohello de tráfego da Internet.

## <a name="high-level-steps"></a>Etapas de alto nível
toodeploy neste cenário, siga Olá etapas de nível superior abaixo.

1. Logon tooyour assinatura do Azure.
2. Se você quiser toodeploy uma saudação de toomimic VNet rede local, provisionar os recursos de saudação que fazem parte do **ONPREMRG**.
3. Provisionar recursos de saudação que fazem parte do **AZURERG**.
4. Encapsulamento Olá provisionar **onpremvnet** muito**azurevnet**.
5. Depois que todos os recursos forem provisionados, faça logon muito**onpremvm2** e a conectividade do ping 10.0.3.101 tootest entre **onpremsn2** e **azsn3**.

