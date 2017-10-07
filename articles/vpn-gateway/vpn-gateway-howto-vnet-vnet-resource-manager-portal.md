---
title: 'Conectar uma rede virtual de tooanother de rede virtual do Azure: Portal | Microsoft Docs'
description: "Criar uma conexão de gateway VPN entre VNets usando o Gerenciador de recursos e Olá portal do Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7015cfc-764b-46a1-bfac-043d30a275df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: a529f90d976bee0f50403947d06e9da8a6c05349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-hello-azure-portal"></a>Configurar uma conexão de gateway VPN de VNet para VNet usando Olá portal do Azure

Este artigo mostra como toocreate uma conexão de gateway VPN entre redes virtuais. Olá redes virtuais podem ser Olá mesmas ou em diferentes regiões e de Olá mesmo ou em assinaturas diferentes. Quando conexão VNets de assinaturas diferentes, assinaturas de saudação não precisarem toobe associado Olá mesmo locatário do Active Directory. 

etapas Olá neste artigo se aplicam toohello modelo de implantação do Gerenciador de recursos e usam Olá portal do Azure. Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [CLI do Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Conectar modelos de implantação diferentes – portal do Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Conectar modelos de implantação diferentes - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![Diagrama de v2v](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

Conectar uma rede virtual tooanother VPN (rede virtual a rede) é semelhante tooconnecting uma VNet tooan no site local. Ambos os tipos de conectividade usam um gateway VPN tooprovide um túnel seguro usando IPsec/IKE. Se seus VNets estão em Olá mesma região, talvez você queira tooconsider conectá-los usando o emparelhamento de rede virtual. O emparelhamento Vnet não usa um gateway de VPN. Para obter mais informações, consulte [Emparelhamento da VNet](../virtual-network/virtual-network-peering-overview.md).

Você pode combinar a comunicação de VNet a VNet usando configurações multissite. Isso permite que você estabeleça topologias de rede que combinem conectividade entre instalações com conectividade de rede intervirtual, como mostrado no diagrama a seguir de saudação:

![Sobre conexões](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "Sobre conexões")

### <a name="why-connect-virtual-networks"></a>Por que conectar redes virtuais?

Você talvez queira redes virtuais tooconnect para Olá motivos a seguir:

* **Redundância geográfica entre regiões e presença geográfica**
  
  * Você pode configurar sua própria sincronização ou replicação geográfica com conectividade segura sem passar por pontos de extremidade voltados para a Internet.
  * Com o Balanceador de Carga e o Gerenciador de Tráfego do Azure você pode configurar a carga de trabalho de alta disponibilidade com redundância geográfica em várias regiões do Azure. Um exemplo importante é tooset backup SQL Always On com grupos de disponibilidade espalhados por várias regiões do Azure.
* **Aplicativos multicamadas regionais com limite administrativo ou de isolamento**
  
  * Olá na mesma região, você pode configurar aplicativos de várias camadas com várias redes virtuais conectadas devido tooisolation ou requisitos administrativos.

Para obter mais informações sobre conexões de rede virtual a rede, consulte Olá [perguntas Frequentes de VNet para VNet](#faq) final Olá deste artigo. Observe que, se seus VNets em assinaturas diferentes, não é possível criar conexão Olá no portal de saudação. Você pode usar o [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) ou a [CLI](vpn-gateway-howto-vnet-vnet-cli.md).

### <a name="values"></a>Configurações de exemplo

Ao usar estas etapas como um exercício, você pode usar valores de configurações do exemplo hello. Para fins de exemplo, podemos usar vários espaços de endereço para cada rede virtual. No entanto, as configurações de rede virtual para rede virtual não exigem vários espaços de endereço.

**Valores para TestVNet1:**

* Nome da rede virtual: TestVNet1
* Espaço de endereço: 10.11.0.0/16
  * Nome da sub-rede: FrontEnd
  * Intervalo de endereços da sub-rede: 10.11.0.0/24
* Grupo de recursos: TestRG1
* Local: Leste dos EUA
* Espaço de Endereço: 10.12.0.0/16
  * Nome da sub-rede: BackEnd
  * Intervalo de endereços da sub-rede: 10.12.0.0/24
* Nome da sub-rede de gateway: GatewaySubnet (Isso será o preenchimento automático no portal de saudação)
  * Espaço de endereço da Sub-Rede do Gateway: 10.11.255.0/27
* Servidor DNS: Usar o endereço IP de saudação do servidor DNS
* Nome do Gateway de Rede Virtua: TestVNet1GW
* Tipo de Gateway: VPN
* Tipo de VPN: baseada em rota
* SKU: Selecione Olá SKU de Gateway, você deseja toouse
* Nome do endereço IP público: TestVNet1GWIP
* Valores de conexão:
  * Nome: TestVNet1toTestVNet4
  * Chave compartilhada: você pode criar chave compartilhada hello. Para este exemplo, usaremos abc123. Olá importante é que, ao criar conexão Olá entre hello VNets, valor Olá deve corresponder.

**Valores para TestVNet4:**

* Nome da rede virtual: TestVNet4
* Espaço de endereço: 10.41.0.0/16
  * Nome da sub-rede: FrontEnd
  * Intervalo de endereços da sub-rede: 10.41.0.0/24
* Grupo de recursos: TestRG1
* Local: Oeste dos EUA
* Espaço de Endereço: 10.42.0.0/16
  * Nome da sub-rede: BackEnd
  * Intervalo de endereços da sub-rede: 10.42.0.0/24
* Nome GatewaySubnet: GatewaySubnet (Isso será o preenchimento automático no portal de saudação)
  * Intervalo de endereços da GatewaySubnet: 10.41.255.0/27
* Servidor DNS: Usar o endereço IP de saudação do servidor DNS
* Nome do Gateway de Rede Virtual: TestVNet4GW
* Tipo de Gateway: VPN
* Tipo de VPN: baseada em rota
* SKU: Selecione Olá SKU de Gateway, você deseja toouse
* Nome do endereço IP público: TestVNet4GWIP
* Valores de conexão:
  * Nome: TestVNet4toTestVNet1
  * Chave compartilhada: você pode criar chave compartilhada hello. Para este exemplo, usaremos abc123. Olá importante é que, ao criar conexão Olá entre hello VNets, valor Olá deve corresponder.

## <a name="CreatVNet"></a>1. Criar e configurar a TestVNet1
Se você já tiver uma rede virtual, verifique se as configurações de saudação compatíveis com seu design de gateway VPN. Preste muita atenção tooany sub-redes que podem se sobrepor a outras redes. Se você tiver uma sobreposição de sub-redes, a conexão não funcionará corretamente. Se sua rede virtual é configurada com as configurações corretas de saudação, você pode começar a etapas Olá Olá [especificar um servidor DNS](#dns) seção.

### <a name="toocreate-a-virtual-network"></a>toocreate uma rede virtual
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <a name="subnets"></a>2. Adicionar outro espaço de endereço e criar sub-redes
Você pode adicionar outro espaço de endereço e criar sub-redes após a criação da sua rede virtual.

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <a name="gatewaysubnet"></a>3. Criar uma sub-rede de gateway
Antes de conectar o gateway de rede virtual tooa, você primeiro precisa de sub-rede de gateway toocreate Olá Olá toowhich de rede virtual você deseja tooconnect. Se possível, é melhor toocreate uma sub-rede do gateway usando um bloco CIDR de /28 ou /27 em ordem tooprovide suficiente IP endereços tooaccommodate requisitos de configuração futura adicional.

Se você estiver criando esta configuração como um exercício, consulte toothese [as configurações de exemplo](#values) durante a criação de sua sub-rede do gateway.

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="toocreate-a-gateway-subnet"></a>toocreate uma sub-rede do gateway
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <a name="dns"></a>4. Especificar um servidor DNS (opcional)
O DNS não é necessário para as conexões VNet a VNet. No entanto, se você quiser toohave a resolução de nomes para recursos de rede virtual tooyour implantado, você deve especificar um servidor DNS. Essa configuração permite que você especifique o servidor DNS Olá que você deseja toouse para resolução de nome para essa rede virtual. Ela não cria um servidor DNS.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="VNetGateway"></a>5. Criar um gateway de rede virtual
Nesta etapa, você pode criar o gateway de rede virtual Olá para sua rede virtual. Criar um gateway pode levar até 45 minutos ou mais, dependendo da SKU do gateway Olá selecionado. Se você estiver criando esta configuração como um exercício, você pode consultar toohello [as configurações de exemplo](#values).

### <a name="toocreate-a-virtual-network-gateway"></a>toocreate um gateway de rede virtual
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <a name="CreateTestVNet4"></a>6. Criar e configurar TestVNet4
Depois de ter configurado TestVNet1, crie TestVNet4, repetindo as etapas anteriores hello, substituindo valores hello com aqueles TestVNet4. Você não precisa toowait até que o gateway de rede virtual Olá para TestVNet1 terminar a criação antes de configurar TestVNet4. Se você estiver usando seus próprios valores, certifique-se de que os espaços de endereço de saudação não coincide com nenhum dos Olá VNets que você deseja tooconnect para.

## <a name="TestVNet1Connection"></a>7. Configurar conexão Olá TestVNet1
Quando tem concluído a gateways de rede virtual Olá para TestVNet1 e TestVNet4, você pode criar sua rede virtual conexões de gateway. Nesta seção, você criará uma conexão de tooVNet4 VNet1. Estas etapas funcionam apenas para VNets Olá mesma assinatura. Se seus VNets em assinaturas diferentes, você deve usar a conexão do PowerShell toomake hello. Consulte Olá [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) artigo.

1. Em **todos os recursos**, navegar toohello gateway de rede virtual para sua rede virtual. Por exemplo, **TestVNet1GW**. Clique em **TestVNet1GW** folha de gateway de rede virtual tooopen hello.
   
    ![Folha Conexões](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Folha Conexões")
2. Clique em **+ adicionar** tooopen Olá **Adicionar conexão** folha.
3. Em Olá **Adicionar conexão** folha, no campo de nome hello, digite um nome para a conexão. Por exemplo, **TestVNet1toTestVNet4**.
   
    ![Nome da conexão](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Nome da conexão")
4. Para **Tipo de conexão**. Selecione **VNet para VNet** na lista suspensa de saudação.
5. Olá **primeiro gateway de rede virtual** valor do campo será preenchido automaticamente porque você está criando esta conexão de gateway de rede virtual especificado hello.
6. Olá **segundo gateway de rede virtual** campo é o gateway de rede virtual de saudação do hello VNet que você deseja toocreate uma conexão para. Clique em **escolha outro gateway de rede virtual** tooopen Olá **escolher gateway de rede virtual** folha.
   
    ![Adicionar conexão](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Adicionar uma conexão")
7. Exibição Olá gateways de rede virtual que estão listados nesta folha. Observe que somente os gateways de rede virtual que estão em sua assinatura são listados. Se desejar que o gateway de rede virtual do tooa tooconnect não está em sua assinatura, use Olá [PowerShell artigo](vpn-gateway-vnet-vnet-rm-ps.md). 
8. Clique em que você deseja tooconnect para gateway da rede virtual hello.
9. Em Olá **chave compartilhada** , digite uma chave compartilhada para a conexão. Você pode gerar ou criar essa chave. Em uma conexão site a site, chave Olá usada deve ser exatamente Olá mesmo para seu dispositivo no local e sua conexão de gateway de rede virtual. Olá conceito seja semelhante aqui, exceto que, em vez de dispositivo de VPN tooa conexão, você está se conectando tooanother gateway de rede virtual.
   
    ![Chave compartilhada](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Chave compartilhada")
10. Clique em **Okey** em Olá inferior da saudação folha toosave suas alterações.

## <a name="TestVNet4Connection"></a>8. Configurar conexão Olá TestVNet4
Em seguida, crie uma conexão TestVNet4 tooTestVNet1. Use Olá mesmo método que você usou toocreate conexão de saudação do TestVNet1 tooTestVNet4. Certifique-se de que você use Olá mesma chave compartilhada.

## <a name="VerifyConnection"></a>9. Verificar a conexão
Verifique se a conexão de saudação. Para cada gateway de rede virtual, Olá a seguir:

1. Localize a folha Olá para gateway de rede virtual hello. Por exemplo, **TestVNet4GW**. 
2. Na folha de gateway de rede virtual hello, clique em **conexões** tooview folha de conexões Olá para gateway de rede virtual hello.

Exibir conexões de saudação e verificar o status de saudação. Depois que a conexão de saudação é criado, você verá **êxito** e **conectado** como Olá valores de Status.

![Êxito](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Êxito")

Você pode clicar duas vezes cada conexão separadamente tooview obter mais informações sobre conexão hello.

![Essentials](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")

## <a name="faq"></a>Perguntas frequentes sobre Rede Virtual para Rede Virtual
Exibir detalhes de saudação perguntas Frequentes para obter informações adicionais sobre conexões de rede virtual a rede.

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Próximas etapas
Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Consulte Olá [documentação de máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para obter mais informações.
