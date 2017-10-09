---
title: 'Conecte-se a rede virtual tooanother VNet: CLI do Azure | Microsoft Docs'
description: Este artigo mostra como conectar redes virtuais em conjunto usando o Azure Resource Manager e a CLI do Azure.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>Configurar uma conexão gateway de VPN de Vnet pra VNet usando a CLI do Azure

Este artigo mostra como toocreate uma conexão de gateway VPN entre redes virtuais. Olá redes virtuais podem ser Olá mesmas ou em diferentes regiões e de Olá mesmo ou em assinaturas diferentes. Quando conexão VNets de assinaturas diferentes, assinaturas de saudação não precisarem toobe associado Olá mesmo locatário do Active Directory. 

etapas de saudação neste artigo aplicam o modelo de implantação do Gerenciador de recursos de toohello e usar a CLI do Azure. Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [CLI do Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Conectar modelos de implantação diferentes – portal do Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Conectar modelos de implantação diferentes - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Conectar uma rede virtual tooanother VPN (rede virtual a rede) é semelhante tooconnecting uma VNet tooan no site local. Ambos os tipos de conectividade usam um gateway VPN tooprovide um túnel seguro usando IPsec/IKE. Se seus VNets estão em Olá mesma região, talvez você queira tooconsider conectá-los usando o emparelhamento de rede virtual. O emparelhamento Vnet não usa um gateway de VPN. Para obter mais informações, consulte [Emparelhamento da VNet](../virtual-network/virtual-network-peering-overview.md).

Você pode combinar a comunicação de VNet a VNet usando configurações multissite. Isso permite que você estabeleça topologias de rede que combinem conectividade entre instalações com conectividade de rede intervirtual, como mostrado no diagrama a seguir de saudação:

![Sobre as conexões](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <a name="why"></a>Por que conectar redes virtuais?

Você talvez queira redes virtuais tooconnect para Olá motivos a seguir:

* **Redundância geográfica entre regiões e presença geográfica**

  * Você pode configurar sua própria sincronização ou replicação geográfica com conectividade segura sem passar por pontos de extremidade voltados para a Internet.
  * Com o Balanceador de Carga e o Gerenciador de Tráfego do Azure você pode configurar a carga de trabalho de alta disponibilidade com redundância geográfica em várias regiões do Azure. Um exemplo importante é tooset backup SQL Always On com grupos de disponibilidade espalhados por várias regiões do Azure.
* **Aplicativos multicamadas regionais com limite administrativo ou de isolamento**

  * Olá na mesma região, você pode configurar aplicativos de várias camadas com várias redes virtuais conectadas devido tooisolation ou requisitos administrativos.

Para obter mais informações sobre conexões de rede virtual a rede, consulte Olá [perguntas Frequentes de VNet para VNet](#faq) final Olá deste artigo.

### <a name="which-set-of-steps-should-i-use"></a>Qual conjunto de etapas devo usar?

Neste artigo, você verá dois conjuntos de etapas diferentes. Um conjunto de etapas para [Olá de VNets que residem na mesma assinatura](#samesub)e outro para [VNets que residem em diferentes assinaturas](#difsub).

## <a name="samesub"></a>Conectar-se VNets que estão em Olá mesma assinatura

![Diagrama de v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a>Antes de começar

Antes de começar, instale a versão mais recente Olá de comandos CLI hello (2.0 ou posteriores). Para obter informações sobre como instalar os comandos CLI hello, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).

### <a name="Plan"></a>Planejar os intervalos de endereços IP

Olá etapas a seguir, criamos duas redes virtuais junto com suas configurações e sub-redes do respectivos gateway. Em seguida, criamos uma conexão VPN entre hello duas VNets. É importante tooplan intervalos de endereços IP Olá para sua configuração de rede. Lembre-se de que você deve garantir que nenhum de seus intervalos de VNet ou intervalos de rede local se sobreponham de forma alguma. Nestes exemplos, não incluímos um servidor DNS. Se você deseja resolução de nomes para suas redes virtuais, confira [a Resolução de nomes](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Usamos Olá valores nos exemplos Olá a seguir:

**Valores para TestVNet1:**

* Nome da rede virtual: TestVNet1
* Grupo de recursos: TestRG1
* Local: Leste dos EUA
* TestVNet1: 10.11.0.0/16 & 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* BackEnd: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* IP público: VNet1GWIP
* VpnType: RouteBased
* Connection(1to4): VNet1toVNet4
* Connection(1to5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Valores para TestVNet4:**

* Nome da rede virtual: TestVNet4
* TestVNet2: 10.41.0.0/16 & 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* BackEnd: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Grupo de recursos: TestRG4
* Local: Oeste dos EUA
* GatewayName: VNet4GW
* IP público: VNet4GWIP
* VpnType: RouteBased
* Conexão: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Connect"></a>Etapa 1: conectar tooyour assinatura

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>Etapa 2: Criar e configurar o TestVNet1

1. Crie um grupos de recursos.

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. Crie sub-redes TestVNet1 e hello para TestVNet1. O exemplo a seguir cria uma rede virtual chamada TestVNet1 e uma sub-rede chamada FrontEnd.

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. Crie um espaço de endereço adicional para a sub-rede de back-end de saudação. Observe que essa etapa, podemos especificar que ambos Olá espaço de endereço que criamos anteriormente e Olá adicional a que desejamos tooadd de espaço de endereço. Isso ocorre porque Olá [atualização da rede virtual de rede az](https://docs.microsoft.com/cli/azure/network/vnet#update) comando substitui configurações anteriores hello. Torne toospecify-se de que todos os prefixos de endereço Olá ao usar esse comando.

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. Crie uma sub-rede de back-end de saudação.
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. Crie uma sub-rede de gateway hello. Observe que essa sub-rede de gateway Olá é denominada 'GatewaySubnet'. Esse nome é obrigatório. Neste exemplo, a sub-rede de gateway de saudação está usando um /27. Embora seja possível toocreate tão pequenas quanto /29 uma sub-rede do gateway, é recomendável que você crie uma sub-rede maior que inclui mais endereços selecionando pelo menos /28 ou /27. Isso permitirá suficiente endereços tooaccommodate possíveis configurações adicionais que você pode em Olá futuras.

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. Solicite um público endereço toobe toohello alocado gateway IP que você criará para sua rede virtual. Observe que Olá AllocationMethod é dinâmico. Não é possível especificar o endereço IP de saudação que você deseja toouse. É gateway tooyour alocada dinamicamente.

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. Crie gateway de rede virtual Olá para TestVNet1. As configurações de rede virtual com rede virtual exigem um VpnType RouteBased. Se você executar esse comando hello usando o parâmetro '-- Nenhum - wait', você não vir quaisquer comentários ou saída. Olá '-- Nenhum - wait' parâmetro permite Olá gateway toocreate no plano de fundo de saudação. Isso não significa que esse gateway VPN Olá termina de criar imediatamente. Criar um gateway pode levar até 45 minutos ou mais, dependendo do gateway Olá SKU que você usa.

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="TestVNet4"></a>Etapa 3: criar e configurar TestVNet4

1. Crie um grupos de recursos.

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. Crie a TestVNet4.

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. Crie sub-redes adicionais para TestVNet4.

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. Crie uma sub-rede de gateway hello.

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. Solicite um endereço IP público.

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. Crie gateway de rede virtual TestVNet4 hello.

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>Etapa 4 - criar conexões Olá

Agora, você tem duas redes virtuais com gateways de VPN. Olá próxima etapa é toocreate conexões de gateway VPN entre os gateways de rede virtual hello. Se você usou exemplos de saudação acima, seus gateways de rede virtual estão em diferentes grupos de recursos. Quando os gateways estiverem em diferentes grupos de recursos, você precisa tooidentify e especifique IDs de recurso Olá para cada gateway ao fazer uma conexão. Se seus VNets estão em Olá mesmo grupo de recursos, você pode usar o hello [segundo conjunto de instruções](#samerg) porque você não precisa de IDs de recurso Olá toospecify.

### <a name="diffrg"></a>tooconnect VNets que residem em diferentes grupos de recursos

1. Obter ID do recurso de VNet1GW de saudação da saída de saudação de saudação comando a seguir:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Na saída de hello, localize Olá "id:" linha. os valores de Olá aspas Olá são necessários toocreate Olá conexão na próxima seção, Olá. Copie o editor de texto de tooa esses valores, como o bloco de notas, para que você possa colá-los facilmente ao criar sua conexão.

  Saída de exemplo:

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  Copiar os valores hello após **"id":** aspas hello.

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. Obter Olá ID do recurso de VNet4GW e cópia Olá valores tooa editor de texto.

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. Crie conexão de tooTestVNet4 TestVNet1 hello. Nesta etapa, você pode criar conexão de saudação do TestVNet1 tooTestVNet4. Há uma chave compartilhada referenciada nos exemplos de saudação. Você pode usar seus próprios valores para a chave compartilhada hello. Olá importante é chave compartilhada Olá deve corresponder para ambas as conexões. Criar uma conexão entra em um instante toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. Crie conexão de tooTestVNet1 TestVNet4 hello. Esta etapa é semelhante toohello mostrado acima, exceto que você está criando a conexão de saudação da TestVNet4 tooTestVNet1. Certifique-se de saudação compartilhada chaves correspondentes. Levará alguns minutos tooestablish conexão de saudação.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. Verifique as conexões. Confira [Verificar a conexão](#verify).

### <a name="samerg"></a>tooconnect VNets que residem no hello mesmo grupo de recursos

1. Crie conexão de tooTestVNet4 TestVNet1 hello. Nesta etapa, você pode criar conexão de saudação do TestVNet1 tooTestVNet4. Grupos de recursos de saudação de aviso são Olá mesmo nos exemplos de saudação. Você também pode ver uma chave compartilhada referenciada nos exemplos de saudação. Você pode usar seus próprios valores para a chave compartilhada Olá, no entanto, a chave compartilhada Olá deve corresponder para ambas as conexões. Criar uma conexão entra em um instante toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. Crie conexão de tooTestVNet1 TestVNet4 hello. Esta etapa é semelhante toohello mostrado acima, exceto que você está criando a conexão de saudação da TestVNet4 tooTestVNet1. Certifique-se de saudação compartilhada chaves correspondentes. Levará alguns minutos tooestablish conexão de saudação.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. Verifique as conexões. Confira [Verificar a conexão](#verify).

## <a name="difsub"></a>Conectar as VNets que estão em assinaturas diferentes

![Diagrama de v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

Nesse cenário, conectamos TestVNet1 e TestVNet5. Olá VNets residir assinaturas diferentes. Olá assinaturas não precisem toobe associado Olá mesmo locatário do Active Directory. etapas de saudação para essa configuração adicionam uma conexão de rede virtual a rede adicional na ordem tooconnect TestVNet1 tooTestVNet5.

### <a name="TestVNet1diff"></a>Etapa 5: criar e configurar o TestVNet1

Essas instruções continuam de etapas Olá Olá anterior seções. Você deve concluir [etapa 1](#Connect) e [etapa 2](#TestVNet1) toocreate configurar TestVNet1 e hello Gateway VPN para TestVNet1. Para essa configuração, você não é necessário toocreate TestVNet4 da seção anterior do hello, embora se você criá-lo, ele não está em conflito com estas etapas. Depois de concluir as Etapas 1 e 2, continue com a Etapa 6 (abaixo).

### <a name="verifyranges"></a>Etapa 6 - Verifique se os intervalos de endereços IP Olá

Ao criar conexões adicionais, é importante tooverify que o espaço de endereço IP de saudação da nova rede virtual de saudação não coincide com nenhum dos outros intervalos de VNet ou intervalos de gateway de rede local. Para este exercício, você pode usar Olá Olá TestVNet5 valores a seguir:

**Valores para TestVNet5:**

* Nome da rede virtual: TestVNet5
* Grupo de recursos: TestRG5
* Local: Leste do Japão
* TestVNet5: 10.51.0.0/16 & 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* BackEnd: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* IP público: VNet5GWIP
* VpnType: RouteBased
* Connection: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="TestVNet5"></a>Etapa 7: criar e configurar TestVNet5

Esta etapa deve ser feita no contexto de saudação da nova assinatura hello, 5 de assinatura. Esta parte pode ser executada pelo administrador Olá em uma organização diferente que possui assinatura hello. tooswitch entre o uso de assinaturas ' lista de contas az – todos os ' toolist Olá conta tooyour disponíveis de assinaturas, em seguida, use ' az conta conjunto – assinatura <subscriptionID>' tooswitch toohello assinatura que você deseja toouse.

1. Verifique se você estiver conectado tooSubscription 5, então, cria um grupo de recursos.

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. Crie a TestVNet5.

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. Adicione sub-redes.

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. Adicione sub-rede de gateway de saudação.

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. Solicite um endereço IP público.

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. Criar hello TestVNet5 gateway

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>Etapa 8 — criar conexões Olá

Dividiremos esta etapa em duas sessões CLI marcado como **[1 assinatura]**, e **[assinatura 5]** como gateways Olá estão em assinaturas diferentes hello. tooswitch entre o uso de assinaturas ' lista de contas az – todos os ' toolist Olá conta tooyour disponíveis de assinaturas, em seguida, use ' az conta conjunto – assinatura <subscriptionID>' tooswitch toohello assinatura que você deseja toouse.

1. **[Assinatura 1]**  Login e conecte-se tooSubscription 1. Comando a seguir de execução Olá tooget Olá nome e ID Olá Gateway de saída de hello:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Copiar saída hello "id:". Envie Olá ID e nome de saudação do Olá VNet (VNet1GW) toohello administrador do gateway de 5 de assinatura por email ou outro método.

  Saída de exemplo:

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[Assinatura 5]**  Login e conecte-se tooSubscription 5. Comando a seguir de execução Olá tooget Olá nome e ID Olá Gateway de saída de hello:

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  Copiar saída hello "id:". Envie Olá ID e nome de saudação do Olá VNet (VNet5GW) toohello administrador do gateway de 1 de assinatura por email ou outro método.

3. **[Assinatura 1]**  Nesta etapa, você criar conexão de saudação do TestVNet1 tooTestVNet5. Você pode usar seus próprios valores para a chave compartilhada Olá, no entanto, a chave compartilhada Olá deve corresponder para ambas as conexões. Criar uma conexão pode demorar um pouco ao toocomplete. Verifique se que você se conectar tooSubscription 1.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[Assinatura 5]**  Esta etapa é semelhante toohello mostrado acima, exceto que você está criando a conexão de saudação da TestVNet5 tooTestVNet1. Certifique-se de que Olá compartilhado correspondência de chaves e que você se conecte tooSubscription 5.

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>Verifique as conexões de saudação
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>Perguntas frequentes sobre Rede Virtual para Rede Virtual
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Próximas etapas

* Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Para obter mais informações, consulte Olá [documentação de máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Para obter informações sobre o BGP, consulte Olá [visão geral de BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
