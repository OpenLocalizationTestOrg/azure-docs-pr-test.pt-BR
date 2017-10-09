---
title: "aaaVPN Gateway clássico tooResource Gerenciador de migração | Microsoft Docs"
description: "Esta página fornece uma visão geral da saudação clássico de Gateway VPN tooResource migração do Gerenciador."
documentationcenter: na
services: vpn-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: caa8eb19-825a-4031-8b49-18fbf3ebc04e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: amsriva
ms.openlocfilehash: c1d84bf5315224c5c8faac53d7957b496ed205ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-classic-tooresource-manager-migration"></a>Gateway VPN clássico tooResource migração do Gerenciador
Gateways de VPN agora podem ser migrados do modelo de implantação do Gerenciador de tooResource clássico. É possível ler mais sobre os [Recursos e benefícios](../azure-resource-manager/resource-group-overview.md) do Azure Resource Manager. Neste artigo, vamos detalhes como toomigrate de implantações clássico toonewer Gerenciador de recursos com base em modelo. 

Gateways de VPN são migrados como parte da migração de rede virtual do clássico tooResource Manager. Essa migração é feita com uma VNet por vez. Não há nenhum requisito adicional em termos de toomigration ferramentas ou pré-requisitos. Etapas de migração são idênticos tooexisting VNet migração e são documentadas em [página de migração de recursos de IaaS](../virtual-machines/windows/migration-classic-resource-manager-ps.md). Não há nenhum tempo de inatividade do caminho de dados durante a migração e, portanto, as cargas de trabalho existentes continuará toofunction sem perda de conectividade local durante a migração. endereço IP público Olá associado com o gateway VPN Olá não altera durante o processo de migração hello. Isso implica que você não precisará tooreconfigure seu roteador local quando a saudação migração é concluída.  

modelo de saudação no Gerenciador de recursos é diferente do modelo clássico e é composto de gateways de rede virtual, gateways de rede local e os recursos de conexão. Eles representam o próprio gateway VPN hello, Olá representando respectivamente no espaço de endereço local e conectividade entre hello duas instalações locais. Quando a migração for concluída, seus gateways não estarão disponíveis no modelo clássico e todas as operações de gerenciamento em gateways de rede virtual, gateways de rede local e objetos de conexão deverão ser executadas usando o modelo do Gerenciador de Recursos.

## <a name="supported-scenarios"></a>Cenários com suporte
Cenários mais comuns de conectividade VPN são cobertos por tooResource clássico migração do Gerenciador. cenários de saudação com suporte incluem-

* Conectividade ponto toosite
* A conectividade com o Gateway de VPN toosite site conectado tooon local
* Rede virtual tooVNet conectividade entre dois VNets usando gateways VPN
* Múltiplas VNets conectado toosame no local
* Conectividade de vários sites
* VNets com diagrama do túnel forçado

Os cenários não compatíveis incluem -  

* VNet com ExpressRoute Gateway e VPN Gateway não é compatível atualmente.
* Cenários de trânsito onde as extensões de VM são servidores conectados tooon locais. As limitações de conectividade VPN de tráfego são detalhadas abaixo.

> [!NOTE]
> Validação de CIDR no modelo do Gerenciador de recursos é mais estrita que Olá um modelo clássico. Antes de migrar Certifique-se de que os intervalos de endereços clássico fornecidos está de acordo com formato CIDR toovalid antes de iniciar a migração de saudação. A CIDR pode ser validada usando qualquer validador de CIDR comum. VNet ou sites locais com intervalos CIDR inválidos resultariam em estado de falha quando migrados.
> 
> 

## <a name="vnet-toovnet-connectivity-migration"></a>Migração de conectividade de tooVNet de rede virtual
Rede virtual tooVNet conectividade em clássico foi obtida por meio da criação de um site local a representação de saudação conectados VNet. Os clientes foram toocreate necessários dois sites locais que representado Olá dois VNets que necessário toobe conectados. Elas eram então conectado toohello correspondente VNets usando a conectividade de tooestablish de túnel IPsec entre Olá duas VNets. Esse modelo tem desafios de gerenciamento, desde que as alterações de intervalo de endereço em uma VNet também devem ser mantidas no representação de site local correspondente hello. No modelo do Gerenciador de Recursos, essa solução alternativa não é mais necessária. Olá conexão entre hello que dois VNets pode ser obtidos diretamente usando o tipo de conexão 'Vnet2Vnet' no recurso de Conexão. 

![Captura de tela de VNet tooVNet migração.](./media/vpn-gateway-migration/migration1.png)

Durante a migração de rede virtual, é possível detectar que Olá entidade conectada gateway VPN da rede virtual toocurrent é outra VNet e certifique-se de uma vez concluída a migração de ambos os VNets, não verá dois sites locais representando Olá outras redes. modelo clássico de saudação de dois gateways VPN, dois sites locais e duas conexões entre eles é transformado tooResource Manager modelo com duas conexões do tipo Vnet2Vnet e dois gateways VPN.

## <a name="transit-vpn-connectivity"></a>Conectividade VPN de tráfego
Você pode configurar os gateways VPN em uma topologia, de modo que a conectividade local para uma rede virtual é obtida por meio da conexão tooanother VNet que está diretamente conectado tooon local. Isso é trânsito conectividade VPN onde instâncias na rede virtual primeiro são recursos de locais de tooon conectados por meio do gateway VPN toohello trânsito na rede virtual conectado que está diretamente conectado tooon local. tooachieve essa configuração no modelo de implantação clássico, você precisaria toocreate um site local que tem agregados prefixos que representa a ambos os espaço de endereço de rede virtual e local Olá conectado. Este site local representational for conectado toohello VNet tooachieve trânsito de conectividade. Esse modelo clássico também tem os desafios de gerenciamento semelhantes porque qualquer alteração no intervalo de endereço local também deve ser mantida no site local hello, que representa a agregação de saudação de rede virtual e local. Introdução de suporte do BGP em gateways do Gerenciador de recursos com suporte simplifica a capacidade de gerenciamento como hello gateways conectados aprende rotas de local sem modificação manual tooprefixes.

![Captura de tela do cenário de roteamento do tráfego.](./media/vpn-gateway-migration/migration2.png)

Como podemos transformar VNet tooVNet conectividade sem a necessidade de sites locais, cenário de trânsito Olá perde conectividade local para a rede virtual que está indiretamente conectado tooon local. Olá perda de conectividade pode ser reduzida em Olá dois modos, a seguir após a migração é concluída - 

* Habilite o BGP em gateways VPN que estão conectados e tooon local. A habilitação do BGP restaura a conectividade sem qualquer outra alteração de configuração, pois as rotas são aprendidas e anunciadas entre os gateways de VNet. Observe que a opção de BGP só está disponível em SKUs standard ou superiores.
* Estabelece uma conexão explícita de afetados gateway de rede local VNet toohello que representa o local. Isso também seria requer a alteração de configuração no hello local roteador toocreate e configurar o túnel IPsec de saudação.

## <a name="next-steps"></a>Próximas etapas
Depois de conhecer o suporte à migração de gateway VPN, vá muito[plataforma suportada migração de recursos de IaaS de tooResource clássico Manager](../virtual-machines/windows/migration-classic-resource-manager-ps.md) tooget iniciado.

