---
title: 'Conecte-se a sua rede de local tooan rede virtual do Azure: VPN Site a Site: Portal | Microsoft Docs'
description: "Etapas toocreate uma conexão IPsec de seu local de rede tooan rede virtual do Azure sobre Olá Internet pública. Essas etapas ajudará você a criar uma conexão de Gateway VPN Site a Site entre locais usando o portal de saudação."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a>Criar uma conexão Site a Site no portal do Azure de saudação

Este artigo mostra como toouse Olá toocreate portal do Azure uma conexão de gateway VPN Site a Site de sua toohello de rede local VNet. Olá etapas neste artigo se aplicam a modelo de implantação do Gerenciador de recursos de toohello. Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Uma conexão de gateway VPN Site a Site é usado tooconnect seu local de rede tooan rede virtual do Azure por um túnel VPN IPsec/IKE (IKEv1 ou IKEv2). Esse tipo de conexão exige um VPN de dispositivos localizado localmente que tenha uma tooit de endereço atribuído de IP público externamente. Para saber mais sobre os gateways de VPN, veja [Sobre o gateway de VPN](vpn-gateway-about-vpngateways.md).

![Diagrama de conexão Site a Site de Gateway de VPN entre locais](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Antes de começar

Verifique se você atendeu a saudação critérios a seguir antes de começar a configuração:

* Verifique se você tem um dispositivo VPN compatível e alguém que é capaz de tooconfigure-lo. Para obter mais informações sobre dispositivos VPN compatíveis e a configuração de dispositivo, confira [Sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md).
* Verifique se você possui um endereço IPv4 público voltado para o exterior para seu dispositivo VPN. Esse endereço IP não pode estar localizado atrás de um NAT.
* Se você não estiver familiarizado com intervalos de endereços IP de saudação localizados na configuração de rede local, é necessário toocoordinate com alguém que possa fornecer os detalhes para você. Quando você criar essa configuração, você deve especificar os prefixos de intervalo endereço IP hello Azure encaminhe tooyour no local. Nenhuma das sub-redes Olá da sua rede local pode ser sobre colo com sub-redes de rede virtual Olá que você deseja tooconnect para. 

### <a name="values"></a>Valores de exemplo

Olá exemplos neste artigo usam Olá valores a seguir. Você pode usar esses valores toocreate um ambiente de teste, ou consulte toothem toobetter entender exemplos Olá neste artigo.

* **Nome da rede virtual:** TestVNet1
* **Espaço de endereço:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (opcional para este exercício)
* **Sub-redes:**
  * FrontEnd: 10.11.0.0/24
  * BackEnd: 10.12.0.0/24 (opcional para este exercício)
* **GatewaySubnet:** 10.11.255.0/27
* **Grupo de recursos:** TestRG1
* **Local:** Leste dos EUA
* **Servidor DNS:** opcional. endereço IP de saudação do servidor DNS.
* **Nome do gateway de rede virtual:** VNet1GW
* **IP público:** VNet1GWIP
* **Tipo de VPN:** baseada em rota
* **Tipo de Conexão:** site a site (IPsec)
* **Tipo de gateway:** VPN
* **Nome do Gateway de Rede Local:** Site2
* **Nome da conexão:** VNet1toSite2

## <a name="CreatVNet"></a>1. Criar uma rede virtual

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2. Especificar um servidor DNS

DNS não é necessário toocreate uma Site a Site de conexão. No entanto, se você quiser toohave a resolução de nomes para recursos de rede virtual tooyour implantado, você deve especificar um servidor DNS. Essa configuração permite que você especifique o servidor DNS Olá que você deseja toouse para resolução de nome para essa rede virtual. Ela não cria um servidor DNS. Para saber mais sobre a resolução de nomes, confira [Resolução de nomes para VMs e instâncias de função](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3. Criar uma sub-rede de gateway Olá

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4. Criar gateway VPN Olá

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5. Criar gateway de rede local Olá

Normalmente, o gateway de rede local Olá refere-se tooyour no local. Atribuir o site Olá um nome pelo qual Azure pode consulte tooit e especifique o endereço IP de saudação do hello toowhich de dispositivo VPN de local, você criará uma conexão. Você também pode especificar prefixos de endereço IP de saudação que serão encaminhados através do dispositivo de VPN toohello do gateway VPN hello. especificar os prefixos de endereço Olá são prefixos Olá localizados em sua rede local. Se as alterações de rede local ou precisar de endereço IP público de saudação toochange para dispositivo VPN hello, você pode atualizar facilmente valores hello mais tarde.

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6. Configurar o dispositivo de VPN

Rede de local de tooan conexões site a Site requer um dispositivo VPN. Nesta etapa, você deve configurar seu dispositivo VPN. Ao configurar seu dispositivo VPN, você precisa seguir hello:

- Uma chave compartilhada. Isso é Olá mesmo chave que você especificar ao criar sua conexão VPN Site a Site. Em nossos exemplos, usamos uma chave compartilhada básica. É recomendável que você gerar um toouse chave mais complexa.
- Olá endereço IP público do seu gateway de rede virtual. Você pode exibir o endereço IP público de saudação usando Olá portal do Azure, PowerShell ou CLI. Olá toofind endereço IP público do seu gateway VPN usando Olá portal do Azure, navegue muito**gateways de rede Virtual**, clique em nome de saudação do seu gateway.

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7. Criar conexão de VPN Olá

Crie conexão de VPN Olá Site a Site entre o gateway de rede virtual e seu dispositivo VPN local.

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8. Verifique se a conexão de VPN Olá

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="connectVM"></a>máquina de virtual tooa tooconnect

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="reset"></a>Como tooreset um gateway de VPN

Redefinir um gateway de VPN do Azure é útil se você perde a conectividade VPN entre locais em um ou mais túneis de VPN site a site. Nessa situação, os seus dispositivos VPN local são todos funcionando corretamente, mas são tooestablish não é possível túneis IPsec com gateways de VPN do Azure hello. Para obter as etapas, consulte [Redefinir um gateway de VPN](vpn-gateway-resetgw-classic.md).

## <a name="resize"></a>Como toochange um gateway de SKU (redimensionar um gateway)

Para as etapas de saudação toochange um SKU de gateway, consulte [SKUs de Gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="next-steps"></a>Próximas etapas

* Para obter informações sobre o BGP, consulte Olá [visão geral de BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Para saber mais sobre Túneis Forçados, confira [Sobre o Túnel Forçado](vpn-gateway-forced-tunneling-rm.md).
* Para obter informações sobre Conexões Altamente Disponíveis Ativo-Ativo, consulte [Conectividade Altamente Disponível entre locais e Rede Virtual para Rede Virtual](vpn-gateway-highlyavailable.md).
