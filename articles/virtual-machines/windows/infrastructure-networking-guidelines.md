---
title: aaaAzure rede diretrizes de infraestrutura - Windows | Microsoft Docs
description: "Saiba mais sobre Olá design e implementação diretrizes importantes para a implantação de rede virtual nos serviços de infraestrutura do Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e2d45973-5eba-4904-8ba0-1821f64feed7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 64c288957e7c7b89578d871a74ff45ce470ed922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-windows-vms"></a>Diretrizes de infraestrutura de rede do Azure para VMs Windows 

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Este artigo se concentra na compreensão Olá necessárias etapas de planejamento para a rede virtual no Azure e a conectividade entre ambientes locais existentes.

## <a name="implementation-guidelines-for-virtual-networks"></a>Diretrizes de implementação de redes virtuais
Decisões:

* O tipo de rede virtual você precisa toohost sua carga de trabalho TI ou infraestrutura (somente em nuvem ou entre locais)?
* Para redes virtuais entre locais quanto espaço de endereço você precisa de sub-redes de saudação toohost e VMs agora e de expansão razoável Olá para futuras?
* São sobre toocreate centralizado redes virtuais ou cria redes virtuais individuais para cada grupo de recursos?

Tarefas:

* Defina o espaço de endereço de saudação para Olá redes virtuais toobe criado.
* Defina o conjunto de saudação de sub-redes e espaço de endereço de saudação para cada.
* Para redes virtuais de vários locais, defina o conjunto de saudação de espaços de endereço de rede local para os locais de local Olá Olá VMs em Olá tooreach de necessidade de rede virtual.
* Trabalhar com rede team tooensure Olá roteamento apropriado é configurado quando criar entre locais redes virtuais no local.
* Crie rede virtual hello, usando a convenção de nomenclatura.

## <a name="virtual-networks"></a>Redes virtuais
Redes virtuais são necessárias toosupport comunicações entre máquinas virtuais (VMs). Você pode definir sub-redes, endereços IP personalizados, configurações de DNS, filtragem de segurança e balanceamento de carga, assim como em redes físicas. Usando um [gateway VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md) ou [circuito de rota expressa](../../expressroute/expressroute-introduction.md), você pode se conectar a redes de local de tooyour redes virtuais do Azure. Leia mais sobre [redes virtuais e seus componentes](../../virtual-network/virtual-networks-overview.md).

Com o uso de Grupos de Recursos, você tem flexibilidade para projetar os componentes da rede virtual. Máquinas virtuais podem se conectar a redes toovirtual fora de seu próprio grupo de recursos. Uma abordagem de design comum seria toocreate centralizado grupos de recursos que contêm sua infraestrutura de rede principal que pode ser gerenciada por uma equipe comuns e, em seguida, VMs e seus aplicativos implantados tooseparate grupos de recursos. Essa abordagem permite que os proprietários de aplicativos acesso toohello grupo de recursos que contém suas VMs sem abrir a configuração do acesso toohello de saudação mais ampla virtual recursos de rede.

## <a name="site-connectivity"></a>Conectividade de site
### <a name="cloud-only-virtual-networks"></a>Redes virtuais somente na nuvem
Se os computadores e usuários locais não exigem tooVMs contínuos de conectividade em uma rede virtual do Azure, seu design de rede virtual é muito simples:

![Diagrama básico de rede virtual somente na nuvem](./media/infrastructure-networking-guidelines/vnet01.png)

Essa abordagem costuma ser usada para cargas de trabalho para a Internet, como um servidor Web baseado na Internet. Você pode gerenciar essas VMs usando conexões RDP ou VPN ponto a site.

Porque eles não se conectar a rede de local de tooyour, redes virtuais somente no Azure podem usar qualquer parte do espaço de endereço IP privado hello, mesmo se usar o hello mesmo espaço privado está no local.

### <a name="cross-premises-virtual-networks"></a>Redes virtuais entre instalações
Se precisam de computadores e usuários locais tooVMs contínuos de conectividade em uma rede virtual do Azure, crie uma rede virtual entre locais.  Conecte-rede de local de tooyour com uma rota expressa ou conexão de VPN site a site.

![Diagrama de rede virtual entre instalações](./media/infrastructure-networking-guidelines/vnet02.png)

Nessa configuração, Olá rede virtual do Azure é essencialmente um extensão baseado em nuvem da rede local.

Como eles se conectam tooyour rede local, redes virtuais devem usar uma parte do espaço de endereço Olá usado pela sua organização que seja exclusiva entre locais. Em hello mesma forma que diferentes locais corporativos recebem uma sub-rede IP específica, o Azure torna-se outro local, você pode estender sua rede.

tooallow tootravel de pacotes de sua rede de local de tooyour de rede virtual entre locais, você deve configurar o conjunto de saudação de prefixos de endereço local relevante como parte da definição de rede local Olá para rede virtual hello. Dependendo do endereço Olá espaço Olá virtual rede e hello conjunto de relevantes local locais, pode haver muitos prefixos de endereço na rede local hello.

Você pode converter uma rede virtual do tooa entre locais de rede virtual somente em nuvem, mas provavelmente requer toore IP seu espaço de endereço de rede virtual e recursos do Azure. Portanto, considere cuidadosamente se uma rede virtual precisa de rede de local toobe tooyour conectado quando você atribui uma sub-rede IP.

## <a name="subnets"></a>Sub-redes
As sub-redes permitem tooorganize recursos que estão relacionados, ou logicamente (por exemplo, uma sub-rede para as VMs associadas toohello mesmo aplicativo), ou fisicamente (por exemplo, uma sub-rede por grupo de recursos). Você também pode usar técnicas de isolamento de sub-rede para aumentar a segurança.

Para redes virtuais de vários locais, você deve criar sub-redes com hello convenções mesmo que você usa para recursos locais. **Azure sempre usa Olá três primeiros endereços IP saudação do espaço de endereço para cada sub-rede**. número de saudação toodetermine de endereços necessários para a sub-rede Olá, iniciar contando Olá número de VMs que você precisa agora. Estimar o crescimento futuro e use Olá tamanho da saudação toodetermine tabela de sub-rede Olá a seguir.

| Número de VMs necessárias | Número de bits de host necessários | Tamanho da sub-rede Olá |
| --- | --- | --- |
| 1 – 3 |3 |/ 29 |
| 4 – 11 |4 |/ 28 |
| 12 – 27 |5 |/ 27 |
| 28-59 |6 |/ 26 |
| 60 – 123 |7 |/ 25 |

> [!NOTE]
> Para sub-redes locais normal, o número de máximo de saudação de endereços de host para uma sub-rede com os bits de host n é 2<sup> n </sup> – 2. Para uma sub-rede do Azure, o número máximo de saudação de endereços de host para uma sub-rede com os bits de host n é 2<sup> n </sup> – 5 (2 e 3 para endereços de saudação que usa o Azure em cada sub-rede).
> 
> 

Se você escolher um tamanho de sub-rede é muito pequeno, você tem toore IP e reimplanta Olá VMs na sub-rede hello.

## <a name="network-security-groups"></a>Grupos de segurança de rede
Você pode aplicar a filtragem regras toohello o tráfego que flui através de suas redes virtuais usando grupos de segurança de rede. Você pode criar toosecure de regras de filtragem granular seu ambiente de rede virtual, controle de entrada e saídos tráfego, origem e destino intervalos IP, permitido portas, etc. Grupos de segurança de rede pode ser aplicado toosubnets dentro de uma rede virtual ou diretamente tooa fornecido a interface de rede virtual. É recomendável toohave algum nível de filtragem de tráfego em suas redes virtuais do grupo de segurança de rede. Leia mais sobre [Grupos de segurança de rede](../../virtual-network/virtual-networks-nsg.md).

## <a name="additional-network-components"></a>Componentes de rede adicionais
Assim como acontece com uma infraestrutura de rede física local, a rede virtual do Azure pode conter mais do que sub-redes e endereçamento IP. Ao projetar a infra-estrutura de aplicativos, talvez você queira tooincorporate alguns desses componentes adicionais:

* [Gateways VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md) -conectar redes virtuais do Azure tooother virtuais do Azure redes ou se conectar a redes locais tooon por meio de uma conexão VPN Site a Site. Implementar conexões de Rota Expressa para conexões seguras e dedicadas. Você também pode fornecer acesso direto aos usuários com conexões VPN Ponto a Site.
* [Balanceador de carga](../../load-balancer/load-balancer-overview.md) - fornece balanceamento de carga de tráfego para o tráfego interno e externo, conforme o desejado.
* [Application Gateway](../../application-gateway/application-gateway-introduction.md) - HTTP balanceamento de carga na camada de aplicativo hello, fornecendo alguns benefícios adicionais para aplicativos da web em vez de implantação de Balanceador de carga do Azure hello.
* [Gerenciador de tráfego](../../traffic-manager/traffic-manager-overview.md) - baseado em DNS tráfego distribuição toodirect os usuários finais toohello mais próximo disponível extremidade do aplicativo, permitindo que você toohost seu aplicativo fora do Azure datacenters em regiões diferentes.

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

