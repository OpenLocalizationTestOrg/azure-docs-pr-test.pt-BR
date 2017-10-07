---
title: 'Conecte-se a sua rede de local tooan rede virtual do Azure: VPN Site a Site: CLI | Microsoft Docs'
description: "Etapas toocreate uma conexão IPsec de seu local de rede tooan rede virtual do Azure sobre Olá Internet pública. Essas etapas o ajudarão a criar uma conexão de Gateway de VPN Site a Site entre locais usando a CLI."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a>Criar uma rede virtual com uma conexão VPN Site a Site usando a CLI

Este artigo mostra como toouse Olá CLI do Azure toocreate uma conexão de gateway VPN Site a Site de sua toohello de rede local VNet. Olá etapas neste artigo se aplicam a modelo de implantação do Gerenciador de recursos de toohello. Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:<br>

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagrama de conexão Site a Site de Gateway de VPN entre locais](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

Uma conexão de gateway VPN Site a Site é usado tooconnect seu local de rede tooan rede virtual do Azure por um túnel VPN IPsec/IKE (IKEv1 ou IKEv2). Esse tipo de conexão exige um VPN de dispositivos localizado localmente que tenha uma tooit de endereço atribuído de IP público externamente. Para saber mais sobre os gateways de VPN, veja [Sobre o gateway de VPN](vpn-gateway-about-vpngateways.md).

## <a name="before-you-begin"></a>Antes de começar

Verifique se você atendeu a saudação critérios a seguir antes de iniciar a configuração:

* Verifique se você tem um dispositivo VPN compatível e alguém que é capaz de tooconfigure-lo. Para obter mais informações sobre dispositivos VPN compatíveis e a configuração de dispositivo, confira [Sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md).
* Verifique se você possui um endereço IPv4 público voltado para o exterior para seu dispositivo VPN. Esse endereço IP não pode estar localizado atrás de um NAT.
* Se você não estiver familiarizado com intervalos de endereços IP de saudação localizados na configuração de rede local, é necessário toocoordinate com alguém que possa fornecer os detalhes para você. Quando você criar essa configuração, você deve especificar os prefixos de intervalo endereço IP hello Azure encaminhe tooyour no local. Nenhuma das sub-redes Olá da sua rede local pode ser sobre colo com sub-redes de rede virtual Olá que você deseja tooconnect para.
* Verifique se você instalou a versão mais recente de comandos CLI hello (2.0 ou posteriores). Para obter informações sobre como instalar os comandos CLI hello, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli) e [Introdução ao Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).

### <a name="example"></a>Valores de exemplo

Você pode usar o hello valores toocreate um ambiente de teste a seguir, ou consulte valores toothese toobetter entender exemplos Olá neste artigo:

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <a name="Login"></a>1. Conecte-se a assinatura de tooyour

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="rg"></a>2. Criar um grupo de recursos

Olá, exemplo a seguir cria um grupo de recursos denominado TestRG1 no local de 'eastus' hello. Se você já tiver um grupo de recursos na região de saudação que você deseja toocreate sua rede virtual, você pode usar um em vez disso.

```azurecli
az group create --name TestRG1 --location eastus
```

## <a name="VNet"></a>3. Criar uma rede virtual

Se você ainda não tiver uma rede virtual, crie um usando Olá [criar redes de rede az](/cli/azure/network/vnet#create) comando. Ao criar uma rede virtual, certifique-se de que os espaços de endereço Olá que você especificar não se sobrepõem a nenhum Olá dos espaços de endereço que você tem em sua rede local.

Olá, exemplo a seguir cria uma rede virtual denominada 'TestVNet1' e uma sub-rede, 'Subnet1'.

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## 4. <a name="gwsub"></a>Criar uma sub-rede de gateway Olá

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

Para essa configuração, você também precisará de uma sub-rede de gateway. gateway de rede virtual Olá usa uma sub-rede de gateway que contém endereços IP de saudação que são usados pelos serviços de gateway VPN hello. Quando você cria uma sub-rede de gateway, ela deve ser nomeada como 'GatewaySubnet'. Se usar outro nome, você criará uma sub-rede, mas o Azure não a tratará como uma sub-rede de gateway.

tamanho de saudação da sub-rede de gateway de saudação que você especificar depende da configuração de gateway VPN Olá que você deseja toocreate. Embora seja possível toocreate tão pequenas quanto /29 uma sub-rede do gateway, é recomendável que você crie uma sub-rede maior que inclui mais endereços selecionando /27 ou /28. Usar uma sub-rede do gateway maior permite suficiente IP endereços tooaccommodate futuras configurações possíveis.

Saudação de uso [criar sub-rede de rede virtual de rede az](/cli/azure/network/vnet/subnet#create) sub-rede de gateway do comando toocreate hello.

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <a name="localnet"></a>5. Criar gateway de rede local Olá

Normalmente, o gateway de rede local Olá refere-se tooyour no local. Atribuir o site Olá um nome pelo qual Azure pode consulte tooit e especifique o endereço IP de saudação do hello toowhich de dispositivo VPN de local, você criará uma conexão. Você também pode especificar prefixos de endereço IP de saudação que serão encaminhados através do dispositivo de VPN toohello do gateway VPN hello. especificar os prefixos de endereço Olá são prefixos Olá localizados em sua rede local. Se sua rede local for alterada, você pode atualizar facilmente prefixos hello.

Use Olá valores a seguir:

* Olá *– endereço ip de gateway* é o endereço IP de saudação do seu dispositivo VPN local. O dispositivo VPN não pode estar localizado atrás de um NAT.
* Olá *– prefixos de endereço local* é espaços de endereço de seu local.

Saudação de uso [criar local de rede az gateway](/cli/azure/network/local-gateway#create) comando tooadd um gateway de rede local com vários prefixos de endereço:

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <a name="PublicIP"></a>6. Solicite um endereço IP público

Um gateway de VPN deve ter um endereço IP público. Você primeiro solicitar o recurso de endereço IP hello e, em seguida, consulte tooit ao criar o gateway de rede virtual. endereço IP de saudação é atribuído dinamicamente recursos toohello ao gateway de VPN Olá é criado. O gateway de VPN atualmente suporta apenas alocação de endereços IP público *Dinâmico*. Você não pode solicitar uma atribuição de endereço IP Público Estático. No entanto, isso não significa que o endereço IP de saudação alterado depois que ele foi atribuído tooyour gateway VPN. somente tempo de saudação alterações de endereço IP público hello quando é Olá gateway é excluído e criado novamente. Isso não altera o redimensionamento, a redefinição ou outras manutenções/atualizações internas do seu gateway de VPN.

Saudação de uso [criar az rede ip público](/cli/azure/network/public-ip#create) comando toorequest um endereço IP público dinâmico.

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <a name="CreateGateway"></a>7. Criar gateway VPN Olá

Crie gateway de VPN de rede virtual hello. Criar um gateway VPN pode demorar até too45 minutos ou mais toocomplete.

Use Olá valores a seguir:

* Olá *– tipo de gateway* para uma Site a Site configuração é *Vpn*. tipo de gateway Olá é sempre configuração toohello específico que você está implementando. Para obter mais informações, consulte [Tipos de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwtype).
* Olá *- vpn-tipo* pode ser *RouteBased* (conhecida tooas um Gateway dinâmico em alguns documentos), ou *PolicyBased* (chamado tooas um Gateway estático em alguns documentação). configuração de saudação é toorequirements específico de dispositivo de saudação que você está se conectando. Para obter mais informações sobre tipos de gateway de VPN, confira [Sobre definições de configuração de gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype).
* Selecione Olá SKU de Gateway que você deseja toouse. Há limitações de configuração para alguns SKUs. Para obter mais informações, confira [SKUs de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

Criar gateway VPN hello usando Olá [criar gateway de rede virtual az rede](/cli/azure/network/vnet-gateway#create) comando. Se você executar esse comando hello usando o parâmetro '-- Nenhum - wait', você não vir quaisquer comentários ou saída. Esse parâmetro permite Olá gateway toocreate no plano de fundo de saudação. Leva aproximadamente 45 minutos toocreate um gateway.

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <a name="VPNDevice"></a>8. Configurar o dispositivo de VPN

Rede de local de tooan conexões site a Site requer um dispositivo VPN. Nesta etapa, você deve configurar seu dispositivo VPN. Ao configurar seu dispositivo VPN, você precisa seguir hello:

- Uma chave compartilhada. Isso é Olá mesmo chave que você especificar ao criar sua conexão VPN Site a Site. Em nossos exemplos, usamos uma chave compartilhada básica. É recomendável que você gerar um toouse chave mais complexa.
- Olá endereço IP público do seu gateway de rede virtual. Você pode exibir o endereço IP público de saudação usando Olá portal do Azure, PowerShell ou CLI. toofind Olá endereço IP público do seu gateway de rede virtual, use Olá [lista de ip público de rede az](/cli/azure/network/public-ip#list) comando. Para facilitar a leitura, a saída de hello é formatado toodisplay lista de saudação de IPs públicos em formato de tabela.

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>9. Criar conexão de VPN Olá

Crie conexão de VPN Olá Site a Site entre o gateway de rede virtual e seu dispositivo VPN local. Preste atenção especial toohello compartilhado valor de chave, que deve corresponder ao Olá configurado compartilhado valor de chave para seu dispositivo VPN.

Criar conexão hello usando Olá [criar vpn-conexão de rede de az](/cli/azure/network/vpn-connection#create) comando.

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

Após um instante, Olá conexão será estabelecida.

## <a name="toverify"></a>10. Verifique se a conexão de VPN Olá

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

Se você quiser toouse tooverify de outro método sua conexão, consulte [verificar uma conexão de Gateway VPN](vpn-gateway-verify-connection-resource-manager.md).

## <a name="connectVM"></a>máquina de virtual tooa tooconnect

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="tasks"></a>Tarefas comuns

Esta seção contém os comandos comuns que são úteis ao trabalhar com configurações de site a site. Para Olá a lista completa de comandos de rede, consulte [CLI do Azure - rede](/cli/azure/network).

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a>Próximas etapas

* Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Para saber mais, veja [Máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Para obter informações sobre o BGP, consulte Olá [visão geral de BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Para saber mais sobre Túneis Forçados, confira [Sobre o Túnel Forçado](vpn-gateway-forced-tunneling-rm.md).
* Para obter informações sobre Conexões Altamente Disponíveis Ativo-Ativo, consulte [Conectividade Altamente Disponível entre locais e Rede Virtual para Rede Virtual](vpn-gateway-highlyavailable.md).
* Para obter uma lista de comandos da CLI do Azure de rede, confira [CLI do Azure](https://docs.microsoft.com/cli/azure/network).