---
title: "aaaConfigure uma rede Virtual e o Gateway de rota expressa no portal clássico de Olá | Microsoft Docs"
description: "Este artigo orienta você pela configuração de uma rede virtual para o ExpressRoute usando o modelo de implantação clássico hello e o portal clássico do hello."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 688817d9-51c8-4372-9af8-33fa098c7c5a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/20/2016
ms.author: cherylmc
ms.openlocfilehash: dd1f6c5e85dbb3ad0a53ecd81c13b4d3f5c06e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-for-expressroute-in-hello-classic-portal"></a>Criar uma rede Virtual para o ExpressRoute no portal clássico Olá
etapas de saudação neste artigo guiarão você pela configuração de uma rede virtual e um gateway de rede virtual para uso com o ExpressRoute usando o modelo de implantação clássico hello e o portal clássico do hello.

Se você estiver procurando instruções para o modelo de implantação do Gerenciador de recursos de saudação, você pode usar o hello artigos a seguir: [criar uma rede virtual usando o PowerShell](../virtual-network/virtual-networks-create-vnet-arm-ps.md) e [adicionar um Gateway VPN de tooa VNet Gerenciador de recursos para Rota expressa](expressroute-howto-add-gateway-resource-manager.md).

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Sobre modelos de implantação do Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="create-a-classic-vnet-and-gateway"></a>Criar uma rede virtual clássica e um gateway
Olá etapas a seguir criam uma rede virtual clássica e um gateway de rede virtual. Se você já tiver uma rede virtual clássica, consulte Olá [configurar uma rede de virtual clássica existente](#config) seção neste artigo.

1. Faça logon no toohello [portal clássico do Azure](http://manage.windowsazure.com).
2. No hello canto inferior esquerdo da tela hello, clique em **novo**. No painel de navegação de saudação, clique em **serviços de rede**e, em seguida, clique em **rede Virtual**. Clique em **criação personalizada** toobegin Assistente de configuração de saudação.
3. Em Olá **detalhes da rede Virtual** página, digite Olá seguinte:
   
   * **Nome** – Nome da sua rede virtual. Você usará esse nome de rede virtual quando implantar suas VMs e instâncias de PaaS, portanto não é aconselhável toomake nome de saudação muito complicado.
   * **Local** – Olá local é diretamente relacionado toohello físico (região) onde você deseja que seu tooreside de recursos (VMs). Por exemplo, se você quiser Olá VMs que você implanta toobe de rede virtual toothis fisicamente localizado em Leste dos EUA, selecione esse local. Você não pode alterar a região Olá associado à sua rede virtual depois de criá-lo.
4. Em Olá **servidores DNS e conectividade VPN** página, digite Olá informações a seguir e clique Olá próxima seta no canto direito inferior hello. 
   
   * **Servidores DNS** - insira o nome do servidor DNS hello e endereço IP, ou selecione um servidor DNS previamente registrado no menu de atalho de saudação. Essa configuração não cria um servidor DNS. Ele permite que os servidores toospecify Olá DNS que você deseja toouse para resolução de nome para essa rede virtual.
   * **Conectividade site a Site** - selecione Olá a caixa de seleção **configurar uma VPN site a site**.
   * **Rota expressa** – selecione Olá a caixa de seleção **usar ExpressRoute**. Essa opção aparece somente se você tiver selecionado **Configurar uma VPN Site a Site**.
   * **Rede local** -são necessária toohave um site de rede local para o ExpressRoute. No entanto, no caso de saudação de uma conexão de rota expressa, prefixos de endereço de saudação especificado para Olá local site de rede será ignorado. Em vez disso, prefixos de endereço Olá anunciado tooMicrosoft por meio de saudação circuito ExpressRoute será usado para fins de roteamento.<BR>Se você já tiver uma rede local criada para sua conexão de rota expressa, você pode selecioná-lo na lista suspensa de saudação. Caso não tenha, escolha **Especificar uma Nova Rede Local**.
5. Olá **conectividade Site a Site** página será exibida se você selecionou toospecify uma nova rede local na etapa anterior hello. tooconfigure sua rede local, digite Olá informações a seguir e, em seguida, clique em seta Avançar hello. 
   
   * **Nome** -Olá nome toocall local (local) local de rede.
   * **Espaço de endereço** – Incluindo o IP Inicial e o CIDR (Contagem de Endereços). Você pode especificar qualquer intervalo de endereços, desde que ele não coincide com o intervalo de endereços Olá para sua rede virtual. Normalmente, isso seria especificar intervalos de endereços de saudação para suas redes locais, mas no caso de saudação de rota expressa, essas configurações não são usadas. No entanto, essa configuração é necessária na rede local da ordem toocreate hello quando você estiver usando o portal clássico do hello.
   * **Adicionar espaço de endereço** – Essa configuração não é relevante para o ExpressRoute.
6. Em Olá **espaços de endereço de rede Virtual** página, digite Olá informações a seguir e clique em marca de seleção Olá no tooconfigure direito inferior do hello sua rede. 
   
   * **Espaço de endereço** – incluindo o IP inicial e a contagem de endereços. Verifique se que os espaços de endereço Olá que você especificar não se sobrepõem a nenhum Olá dos espaços de endereço que você tem em sua rede local.
   * **Adicionar sub-rede** – incluindo o IP Inicial e a Contagem de Endereços. As sub-redes adicionais não são necessárias.
   * **Adicionar sub-rede de gateway** -clique tooadd Olá gateway sub-rede. sub-rede de gateway de saudação é usado apenas para o gateway de rede virtual hello e é necessária para essa configuração.<BR>Olá sub-rede CIDR (contagem de endereço) do gateway para ExpressRoute deve ser/28 ou maior (/ 27, / 26 etc.). Isso permite que endereços IP suficientes em toowork de configuração que sub-rede tooallow hello. No portal clássico do hello, se você tiver selecionado a caixa de seleção de saudação toouse rota expressa, portal de saudação especifica uma sub-rede de gateway com /28.  Você não pode ajustar a contagem de endereços CIDR Olá no portal clássico do hello. sub-rede de gateway Hello serão exibidos como **Gateway** no portal clássico do hello, embora hello nome real da sub-rede de gateway Olá criado é realmente **GatewaySubnet**. Você pode exibir esse nome usando o PowerShell ou em Olá portal do Azure.
7. Clique em Olá marca de seleção na parte inferior de saudação da página de saudação e sua rede virtual começará a toocreate. Quando concluído, você verá **criado** listado em **Status** em Olá **redes** página no portal clássico do hello.

## <a name="gw"></a>Criar gateway Olá
1. Em Olá **redes** página, clique Olá rede virtual que você acabou de criar e clique em **painel** na parte superior de saudação da página de saudação.
2. Na parte inferior de saudação da saudação **painel** , clique em **criar Gateway** e selecione **roteamento dinâmico**. Clique em **Sim** tooconfirm que você deseja toocreate um gateway.
3. Quando o gateway Olá começará a criar, você verá uma mensagem informando que Olá gateway foi iniciado. Pode levar até too45 minutos para Olá gateway toocreate.
4. Vincule seu circuito tooa de rede. Siga as instruções de saudação artigo Olá [como toolink VNets tooExpressRoute circuitos](expressroute-howto-linkvnet-classic.md).

## <a name="config">
            </a>Configurar uma rede virtual clássica existente para o ExpressRoute
Se você já tiver uma rede virtual clássica, você pode configurá-lo tooconnect tooExpressRoute no portal clássico do hello. configurações de saudação são Olá mesmo como seções de saudação acima, para que as configurações necessárias de leitura por meio desses toobecome seções familiarizado com hello. Se você quiser toocreate uma conexão coexistente do ExpressRoute/Site a Site, consulte [neste artigo](expressroute-howto-coexist-classic.md) para etapas de saudação. Eles são diferentes de saudação as etapas neste artigo.

1. Você precisa de rede de local de saudação do toocreate antes de atualizar o restante da saudação de suas configurações de rede virtual. toocreate uma nova rede local, que é necessária ao configurar rota expressa por meio do portal clássico hello, clique **novo**  **>**  **serviços de rede**  **>**  **Rede virtual**  **>**  **rede local adicionar**. Siga Olá Assistente etapas toocreate Olá rede local.
2. Use **configurar** página restante de saudação do tooupdate das configurações de saudação para sua rede virtual e tooassociate Olá VNet toohello rede local.
3. Depois de configurar as configurações de hello, vá toohello [criar gateway de saudação](#gw) seção desse gateway de saudação do artigo toocreate.

## <a name="next-steps"></a>Próximas etapas
* Máquinas virtuais de tooadd tooyour rede virtual, consulte [máquinas virtuais caminhos de aprendizado](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/).
* Se você quiser toolearn mais sobre a rota expressa, consulte Olá [visão geral do ExpressRoute](expressroute-introduction.md).

