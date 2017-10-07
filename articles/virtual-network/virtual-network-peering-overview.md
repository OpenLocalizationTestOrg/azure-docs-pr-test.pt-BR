---
title: emparelhamento de rede Virtual aaaAzure | Microsoft Docs
description: Saiba mais sobre o emparelhamento de rede virtual no Azure.
services: virtual-network
documentationcenter: na
author: NarayanAnnamalai
manager: jefco
editor: tysonn
ms.assetid: eb0ba07d-5fee-4db0-b1cb-a569b7060d2a
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: narayan
ms.openlocfilehash: 46a14b416a7d4389f79a3cd7c55e388b5d312577
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network-peering"></a>Emparelhamento de rede virtual
Emparelhamento de rede virtual permite você tooconnect duas redes virtuais no mesma região por meio de hello Olá rede backbone do Azure. Depois de emparelhadas, duas redes virtuais de saudação aparecem como um, para fins de conectividade. redes virtuais Olá dois ainda são gerenciadas como recursos separados, mas as máquinas virtuais no hello emparelhadas redes virtuais podem se comunicar entre si diretamente, usando endereços IP privados.

o tráfego entre máquinas virtuais no Olá Olá emparelhadas redes virtuais é roteado por Olá infraestrutura do Azure, assim como o tráfego é roteado entre máquinas virtuais no hello mesma rede virtual. Alguns dos benefícios de saudação do uso do emparelhamento de rede virtual:

* Baixa latência, conexão com largura de banda alta entre os recursos em redes virtuais diferentes.
* recursos de toouse de capacidade de saudação como dispositivos de rede e gateways VPN, como pontos de trânsito em uma rede virtual peered.
* Olá capacidade toopeer duas redes virtuais criadas por meio do modelo de implantação do Azure Resource Manager hello ou toopeer uma rede virtual criada por meio tooa do Gerenciador de recursos de rede virtual que foi criada no modelo de implantação clássico Olá. Saudação de leitura [modelos de implantação do Azure entender](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo toolearn mais sobre as diferenças de saudação entre modelos de implantação do Azure Olá dois.

## <a name="requirements-constraints"></a>Requisitos e restrições

* Hello redes virtuais emparelhadas devem existir no hello mesma região do Azure. Você pode se conectar a redes virtuais em diferentes regiões do Azure usando um [Gateway de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V).
* Hello emparelhadas redes virtuais devem ter espaços de endereço IP sem sobreposição.
* Espaços de endereço não podem ser adicionados ao ou excluídos de uma rede virtual depois que ela é emparelhada com outra rede virtual.
* O emparelhamento de rede virtual é entre duas redes virtuais. Não há nenhuma relação transitiva derivada entre emparelhamentos. Por exemplo, se virtualNetworkA está emparelhada com virtualNetworkB e virtualNetworkB está emparelhada com virtualNetworkC, virtualNetworkA é *não* toovirtualNetworkC emparelhada.
* Você pode emparelhar redes virtuais que existem em duas assinaturas diferentes, como tempo um usuário privilegiado (consulte [permissões específicas](create-peering-different-deployment-models-subscriptions.md#permissions)) de ambos assinaturas autoriza o emparelhamento de saudação e assinaturas de saudação são toohello associado mesmo Locatário do Active Directory do Azure. Você pode usar um [Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect de redes virtuais em assinaturas associadas locatários do toodifferent do Active Directory.
* Redes virtuais podem ser emparelhadas se ambas são criadas por meio do modelo de implantação do Gerenciador de recursos de saudação ou uma rede virtual é criada por meio do modelo de implantação do Gerenciador de recursos de saudação e Olá outros é criado por meio do modelo de implantação clássico hello. Duas redes virtuais criadas por meio do modelo de implantação clássico Olá não podem ser emparelhada tooeach outro, porém. Você pode usar um [Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect dois as redes virtuais criadas por meio do modelo de implantação clássico hello.
* Embora a comunicação entre as máquinas virtuais em redes virtuais emparelhadas Olá não tem nenhuma restrição de largura de banda adicional, há uma largura de banda de rede máxima dependendo do tamanho da máquina virtual Olá que ainda se aplica. toolearn mais sobre a largura de banda de rede máxima para tamanhos de máquina virtual diferente, ler Olá [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigos de tamanhos de máquina virtual.
* A resolução de nome DNS interna fornecida pelo Azure para as Máquinas virtuais não funcionam nas redes virtuais emparelhadas. Máquinas virtuais têm nomes DNS internos pode ser resolvidos dentro de rede virtual local de saudação. No entanto, você pode configurar máquinas virtuais conectadas toopeered as redes virtuais como servidores DNS para uma rede virtual. Para obter mais detalhes, leia Olá [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) artigo.

![Emparelhamento básico de redes virtuais](./media/virtual-networks-peering-overview/figure01.png)

## <a name="connectivity"></a>Conectividade
Depois de duas redes virtuais estão pareadas, recursos em qualquer rede virtual podem conectar-se diretamente com recursos na rede virtual emparelhadas hello. redes virtuais Olá dois têm total no nível de IP conectividade.

latência de rede Olá para uma viagem de ida e entre as duas máquinas virtuais em redes virtuais emparelhadas é Olá mesmo o para uma viagem de ida e dentro de uma única rede virtual. taxa de transferência de rede Olá baseia-se a largura de banda de saudação que é permitida para a máquina virtual de hello, tamanho tooits proporcional. Não há qualquer restrição adicional na largura de banda no emparelhamento hello.

Olá o tráfego entre máquinas virtuais em redes virtuais emparelhadas é roteado diretamente por meio de saudação infraestrutura de back-end do Azure, não por meio de um gateway.

Máquinas virtuais conectadas tooa virtual rede pode acessar Olá com balanceamento de carga pontos de extremidade internos na rede virtual emparelhadas hello. Grupos de segurança de rede podem ser aplicados em redes virtuais a rede virtual tooblock acesso para tooother ou sub-redes, se desejado.

Ao configurar o emparelhamento de rede virtual, você pode abrir ou fechar regras de grupo de segurança de rede de saudação entre redes virtuais hello. Se você abrir total conectividade entre redes virtuais emparelhadas (que é a opção padrão de saudação), você pode aplicar rede segurança grupos toospecific sub-redes ou máquinas virtuais tooblock ou negar acesso específico. toolearn mais sobre grupos de segurança de rede ler Olá [visão geral de grupos de segurança de rede](virtual-networks-nsg.md) artigo.

## <a name="service-chaining"></a>Encadeamento de serviços
Você pode configurar que rotas definidas pelo usuário que máquinas de ponto toovirtual em redes virtuais emparelhadas como hello "próximo salto" o IP endereço tooenable serviço encadeamento. Encadeamento de serviço permite que você toodirect tráfego de uma rede virtual tooa solução de virtualização em uma rede virtual peered através de rotas definidas pelo usuário.

Você pode também efetivamente criar ambientes de tipo de hub e spoke, onde hub Olá pode hospedar os componentes de infraestrutura, como um dispositivo de rede virtual. Todas as redes virtuais spoke de hello, em seguida, podem emparelhar com a rede virtual do hello hub. Tráfego possa fluir através de dispositivos de rede virtual que estão em execução na rede virtual do hello hub. Em resumo, o emparelhamento de rede virtual permite que Olá próximo endereço IP no endereço IP de Olá Olá definido pelo usuário rota toobe de uma máquina virtual na rede virtual emparelhadas hello. toolearn mais sobre as rotas definidas pelo usuário, ler Olá [visão geral de rotas definidas pelo usuário](virtual-networks-udr-overview.md) artigo.

## <a name="gateways-and-on-premises-connectivity"></a>Gateways e conectividade local
Cada rede virtual, independentemente se ele está emparelhado com outra rede virtual, ainda pode ter seu próprio gateway e usá-lo a rede de local de tooan tooconnect. Você também pode configurar [conexões de rede virtual de rede Virtual](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json) usando gateways, mesmo que as redes virtuais Olá estão pareadas.

Quando as duas opções para interconectividade de rede virtual são configuradas, o tráfego entre redes virtuais Olá Olá flui por meio da configuração de emparelhamento hello (ou seja, a saudação backbone do Azure).

Quando as redes virtuais estão pareadas, você também pode configurar o gateway de saudação na rede virtual emparelhadas hello como uma rede de local de ponto tooan trânsito. Nesse caso, a rede virtual de saudação que está usando um gateway remoto não pode ter seu próprio gateway. Uma rede virtual pode ter apenas um gateway. gateway Olá pode ter um gateway local ou remoto (Olá emparelhadas rede virtual), conforme mostrado na figura abaixo de saudação:

![Trânsito de emparelhamento VNet](./media/virtual-networks-peering-overview/figure02.png)

Não há suporte para o tráfego de gateway na relação de emparelhamento Olá entre redes virtuais criadas por meio de diferentes modelos de implantação. As duas redes virtuais na relação de emparelhamento Olá devem ter sido criadas por meio do Gerenciador de recursos para um toowork de trânsito de gateway.

Quando as redes virtuais Olá compartilham uma única conexão de rota expressa do Azure estão pareadas, tráfego de saudação entre eles passa pelo relação de emparelhamento hello (ou seja, a saudação rede backbone do Azure). Você ainda pode usar gateways locais em cada circuito de local de toohello de tooconnect de rede virtual. Como alternativa, você pode usar um gateway compartilhado e configurar o trânsito para conectividade local.

## <a name="provisioning"></a>Provisionamento
O emparelhamento de rede virtual é uma operação privilegiada. É uma função separada sob Olá VirtualNetworks namespace. Um usuário pode receber direitos específicos tooauthorize emparelhamento. Um usuário que tenha acesso de leitura-gravação toohello virtual rede herda esses direitos automaticamente.

Um usuário que seja um administrador ou um usuário com privilégios de capacidade de emparelhamento Olá pode iniciar uma operação de emparelhamento em outra rede virtual. Se houver uma solicitação correspondente para emparelhamento Olá outro lado, e se outros requisitos forem atendidos, a saudação emparelhamento é estabelecido.

## <a name="limits"></a>limites
Há limites no número de saudação de emparelhamentos que são permitidos para uma única rede virtual. Para obter mais informações, examine Olá [limites de rede do Azure](../azure-subscription-service-limits.md#networking-limits).

## <a name="pricing"></a>Preços
Há um custo nominal para tráfego de entrada e saída que utiliza um emparelhamento de rede virtual. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/virtual-network).

## <a name="next-steps"></a>Próximas etapas

* Conclua o tutorial de emparelhamento de rede virtual. Um emparelhamento de rede virtual é criado entre redes virtuais criadas por meio de saudação iguais ou diferentes modelos de implantação que existem no hello iguais ou diferentes assinaturas. Conclua um tutorial para uma saudação os seguintes cenários:
 
    |Modelo de implantação do Azure  | Assinatura  |
    |---------|---------|
    |Ambos Resource Manager |[Idêntica](virtual-network-create-peering.md)|
    | |[Diferente](create-peering-different-subscriptions.md)|
    |Um Resource Manager, um clássico     |[Idêntica](create-peering-different-deployment-models.md)|
    | |[Diferente](create-peering-different-deployment-models-subscriptions.md)|

* Saiba como toocreate uma [topologia de rede de hub e spoke](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
* Saiba mais sobre todos os [as configurações de emparelhamento de rede virtual e como toochange-los](virtual-network-manage-peering.md)
