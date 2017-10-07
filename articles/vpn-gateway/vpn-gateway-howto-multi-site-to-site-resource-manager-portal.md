---
title: "Adicionar várias tooa de conexões de gateway Site a Site VPN VNet: Portal do Azure: o Gerenciador de recursos | Microsoft Docs"
description: "Adicionar vários S2S conexões tooa gateway VPN de site que tem uma conexão existente"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a>Adicionar um tooa de conexão Site a Site VNet com uma conexão de gateway VPN existente

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (clássico)](vpn-gateway-multi-site.md)
>
> 

Este artigo orienta você a usar o hello tooadd portal do Azure Site a Site (S2S) conexões tooa gateway VPN que tenha uma conexão existente. Esse tipo de conexão geralmente é chamado tooas uma configuração de "multissite". Você pode adicionar uma conexão de S2S tooa VNet que já tem uma conexão S2S, uma conexão ponto a Site ou uma conexão de rede virtual a rede. Existem algumas limitações ao adicionar conexões. Verificar Olá [antes de começar](#before) seção tooverify este artigo antes de iniciar a configuração. 

Este artigo se aplica a tooVNets criado usando o modelo de implantação do Gerenciador de recursos de saudação que têm um gateway VPN RouteBased. Essas etapas não se aplicam a configurações de conexão coexistentes tooExpressRoute/Site a Site. Confira [Conexões coexistentes ExpressRoute/S2S](../expressroute/expressroute-howto-coexist-resource-manager.md) para obter informações sobre conexões coexistentes.

### <a name="deployment-models-and-methods"></a>Modelos e métodos de implantação
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Atualizamos esta tabela conforme novos artigos e ferramentas adicionais ficam disponíveis para esta configuração. Quando um artigo está disponível, vinculamos diretamente tooit desta tabela.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a>Antes de começar
Verifique se Olá itens a seguir:

* Você não está criando uma conexão ExpressRoute/S2S coexistente.
* Você tem uma rede virtual que foi criada usando o modelo de implantação do Gerenciador de recursos de saudação com uma conexão existente.
* Olá o gateway de rede virtual para sua rede virtual é RouteBased. Se você tiver um gateway PolicyBased VPN, você deve excluir gateway de rede virtual hello e criar um novo gateway VPN como RouteBased.
* Nenhum dos intervalos de endereços de saudação sobrepor para qualquer Olá VNets esta rede está se conectando.
* Você tem o dispositivo VPN compatível e alguém que é capaz de tooconfigure-lo. Confira [Sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md). Se você não estiver familiarizado com a configuração de seu dispositivo VPN ou não estiver familiarizado com os intervalos de endereços IP de saudação localizados em sua configuração de rede local, será necessário toocoordinate com alguém que possa fornecer os detalhes para você.
* Você possui um endereço IP público voltado para o exterior para seu dispositivo VPN. Esse endereço IP não pode estar localizado atrás de um NAT.

## <a name="part1"></a>Parte 1 - Configurar uma conexão
1. Em um navegador, navegue toohello [portal do Azure](http://portal.azure.com) e, se necessário, entre com sua conta do Azure.
2. Clique em **todos os recursos** e localize seu **gateway de rede virtual** da lista de saudação de recursos e clique nele.
3. Em Olá **gateway de rede Virtual** folha, clique em **conexões**.
   
    ![Folha Conexões](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Folha Conexões")<br>
4. Em Olá **conexões** folha, clique em **+ adicionar**.
   
    ![Botão de conexão adicionar](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "adicionar botão de conexão")<br>
5. Em Olá **Adicionar conexão** folha, preencha Olá campos a seguir:
   
   * **Nome:** Olá nome toogive toohello site criar conexão Olá para.
   * **Tipo de conexão:** selecione **Site a site (IPsec)**.
     
     ![Adicionar folha de conexão](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Adicionar folha de conexão")<br>

## <a name="part2"></a>Parte 2 - Adicionar um gateway de rede local
1. Clique em **Gateway de rede Local** ***Escolher um gateway de rede local***. Isso abrirá o hello **gateway de rede local Choose** folha.
   
    ![Gateway de rede local Choose](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "escolher gateway de rede local")<br>
2. Clique em **criar novo** tooopen Olá **criar gateway de rede local** folha.
   
    ![Criar folha de gateway de rede local](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "criar gateway de rede local")<br>
3. Em Olá **criar gateway de rede local** folha, preencha Olá campos a seguir:
   
   * **Nome:** nome hello você deseja que o recurso de gateway de rede local toogive toohello.
   * **Endereço IP:** Olá endereço IP público do dispositivo VPN Olá no site de saudação que você deseja tooconnect para.
   * **Espaço de endereço:** espaço de endereço de saudação que você deseja toobe roteadas toohello novo site de rede local.
4. Clique em **Okey** em Olá **criar gateway de rede local** alterações de saudação toosave folha.

## <a name="part3"></a>Parte 3 - Adicionar chave compartilhada hello e criar conexão Olá
1. Em Olá **Adicionar conexão** folha, adicionar Olá chave compartilhada que você deseja toouse toocreate sua conexão. Você pode obter chave compartilhada de saudação do seu dispositivo VPN, ou criar uma aqui e, em seguida, configure a saudação de toouse do dispositivo VPN mesma chave compartilhada. Olá importante coisa é que as chaves de saudação são exatamente Olá mesmo.
   
    ![Chave compartilhada](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Chave compartilhada")<br>
2. Na parte inferior de saudação da folha de saudação, clique em **Okey** toocreate conexão de saudação.

## <a name="part4"></a>Parte 4 - Verifique se a conexão de VPN Olá


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a>Próximas etapas

Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Consulte as máquinas virtuais de saudação [aprendizado](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) para obter mais informações.
