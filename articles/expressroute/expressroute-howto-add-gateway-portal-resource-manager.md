---
title: 'Adicionar um gateway de rede virtual tooa VNet para o ExpressRoute: Portal: Azure | Microsoft Docs'
description: "Este artigo o orienta por meio de adicionar um tooan de gateway de rede virtual já criado VNet Gerenciador de recursos para o ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 9e922af1f3676eeebc569b57c3ae3a22d4e0b395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-hello-azure-portal"></a>Configurar um gateway de rede virtual para o ExpressRoute usando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Resource Manager - portal do Azure](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Clássico - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Vídeo – Portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Este artigo orienta Olá etapas tooadd um gateway de rede virtual para uma rede virtual já existente. Este artigo orienta Olá etapas tooadd, redimensionar e remover um gateway de rede virtual (VNet) para uma rede virtual já existente. etapas de saudação para essa configuração são específicas para VNets que foram criados usando o modelo de implantação do Gerenciador de recursos de saudação que será usado em uma configuração de rota expressa. Para obter mais informações sobre gateways de rede virtual e definições de configuração do ExpressRoute, consulte [Sobre gateways de rede virtual para ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Antes de começar

etapas de saudação para usar essa tarefa uma rede virtual com base nos valores Olá Olá lista de referências de configuração a seguir. Usamos essa lista em nosso exemplo de etapas. Você pode copiar Olá toouse de lista como referência, substituindo valores hello com seus próprios.

**Lista de referência de configuração**

* Nome da Rede Virtual = “TestVNet”
* Espaço de endereço da Rede Virtual = 192.168.0.0/16
* Nome da sub-rede = "FrontEnd" 
    * Espaço de endereço da sub-rede = "192.168.1.0/24"
* Grupo de recursos = “TestRG”
* Local = "Leste dos EUA"
* Nome da Sub-rede do Gateway: “GatewaySubnet” Deve-se sempre nomear uma sub-rede do gateway como *GatewaySubnet*.
    * Espaço de endereço da Sub-Rede do Gateway = “192.168.200.0/26”
* Nome do gateway = "ERGW"
* Nome de IP do gateway = "MyERGWVIP"
* Tipo de gateway = "ExpressRoute". Esse tipo é necessário para uma configuração de ExpressRoute.
* Nome do IP público do gateway = "MyERGWVIP"

Você pode exibir um [Vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) dessas etapas antes de iniciar sua configuração.

## <a name="create-hello-gateway-subnet"></a>Criar uma sub-rede de gateway Olá

1. Em Olá [portal](http://portal.azure.com), navegue de rede virtual do Gerenciador de recursos toohello para o qual você deseja toocreate um gateway de rede virtual.
2. Em Olá **configurações** seção da folha de sua rede virtual, clique em **sub-redes** tooexpand folha de sub-redes de saudação.
3. Em Olá **sub-redes** folha, clique em **+ sub-rede de Gateway** tooopen Olá **Adicionar sub-rede** folha. 
   
    ![Adicionar sub-rede de gateway Olá](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "Adicionar sub-rede de gateway Olá")


4. Olá **nome** para sua sub-rede é automaticamente preenchido com hello valor 'GatewaySubnet'. Esse valor é necessário para a sub-rede do Azure toorecognize Olá de sub-rede de gateway de saudação. Ajustar o preenchimento automático de saudação **um intervalo de endereços** valores toomatch seus requisitos de configuração. É recomendável criar uma sub-rede do gateway com um /27 ou maior (/ 26, / 25, etc.). Em seguida, clique em **Okey** toosave Olá valores e criar uma sub-rede de gateway hello.

    ![Adicionar sub-rede Olá](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "adicionando sub-rede Olá")

## <a name="create-hello-virtual-network-gateway"></a>Criar gateway de rede virtual Olá

1. No portal de hello, no lado esquerdo do hello, clique em ** + ** e digite 'Gateway de rede Virtual' na pesquisa. Localize **gateway de rede Virtual** na pesquisa de saudação retornar e clique em entrada hello. Em Olá **gateway de rede Virtual** folha, clique em **criar** na parte inferior da saudação da folha de saudação. Isso abre o hello **criar gateway de rede virtual** folha.
2. Em Olá **criar gateway de rede virtual** folha, preencha os valores de saudação do seu gateway de rede virtual.

    ![Criar campos na folha do gateway de rede virtual](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Criar campos na folha do gateway de rede virtual")
3. **Nome**: nomeie o seu gateway. Isso não é Olá igual ao nomear uma sub-rede de gateway. Nome de saudação do objeto de gateway Olá que você está criando-lo do.
4. **Tipo de gateway**: selecione **ExpressRoute**.
5. **SKU**: SKU do gateway Olá selecione na lista suspensa de saudação.
6. **Local**: ajustar Olá **local** campo toopoint toohello local onde sua rede virtual está localizada. Se o local de saudação não está apontando para toohello região onde reside a sua rede virtual, rede virtual Olá não aparece na lista suspensa de 'Escolha uma rede virtual' hello.
7. Escolha toowhich de rede virtual Olá deseja tooadd este gateway. Clique em **rede Virtual** tooopen Olá **escolha uma rede virtual** folha. Selecione Olá VNet. Se você não vir a sua rede virtual, verifique se Olá **local** campo está apontando toohello região na qual sua rede virtual está localizada.
9. Escolha um endereço IP público. Clique em **endereço IP público** tooopen Olá **escolher endereço IP público** folha. Clique em **+ criar novos** tooopen Olá **criar lâmina de endereço IP pública**. Dê um nome para o seu endereço IP público. Esta folha cria um toowhich de objeto de endereço IP público que um endereço IP público será atribuído dinamicamente. Clique em **Okey** toosave folha de toothis suas alterações.
10. **Assinatura**: Verifique se esse Olá correto de assinatura está selecionada.
11. **Grupo de recursos**: essa configuração é determinada pelo Olá rede Virtual que você selecionar.
12. Não ajustar Olá **local** depois que você especificou as configurações anteriores hello.
13. Verifique as configurações de saudação. Se você quiser tooappear seu gateway no painel hello, você pode selecionar **toodashboard Pin** na parte inferior da saudação da folha de saudação.
14. Clique em **criar** toobegin criando Olá gateway. configurações de saudação são validadas e implanta o gateway de saudação. A criação de gateway de rede virtual pode demorar até too45 toocomplete de minutos.

## <a name="next-steps"></a>Próximas etapas
Depois que você criou o gateway de rede virtual Olá, você pode vincular sua rede virtual tooan circuito de rota expressa. Consulte [vincular um circuito de rota expressa do tooan de rede Virtual](expressroute-howto-linkvnet-portal-resource-manager.md).
