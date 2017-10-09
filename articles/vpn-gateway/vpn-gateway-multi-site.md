---
title: "Conectar sites de toomultiple uma rede virtual usando o PowerShell e o Gateway de VPN: clássico | Microsoft Docs"
description: "Este artigo lhe orientará conectar vários local no local sites tooa rede virtual usando um Gateway de VPN para o modelo de implantação clássico hello."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a>Adicionar um tooa de conexão Site a Site VNet com uma conexão de gateway VPN existente (clássico)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (clássico)](vpn-gateway-multi-site.md)
>
>

Este artigo orienta você a usar o PowerShell tooadd Site a Site (S2S) conexões tooa gateway VPN que tenha uma conexão existente. Esse tipo de conexão geralmente é chamado tooas uma configuração de "multissite". Olá etapas neste artigo se aplicam redes toovirtual criadas usando o modelo de implantação clássico hello (também conhecido como gerenciamento de serviço). Essas etapas não se aplicam a configurações de conexão coexistentes tooExpressRoute/Site a Site.

### <a name="deployment-models-and-methods"></a>Modelos e métodos de implantação

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Atualizamos esta tabela conforme novos artigos e ferramentas adicionais ficam disponíveis para esta configuração. Quando um artigo está disponível, vinculamos diretamente tooit desta tabela.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a>Sobre a conexão

Você pode se conectar a vários locais sites tooa única rede virtual. Isso é especialmente atraente para criar soluções de nuvem híbrida. Criar um gateway de rede virtual do Azure multissite conexão tooyour é toocreating semelhante a outras conexões Site a Site. Na verdade, você pode usar um gateway de VPN do Azure existente, desde que o gateway de saudação é dinâmico (baseado em rota).

Se você já tiver uma rede virtual do gateway estático tooyour conectado, você pode alterar Olá toodynamic de tipo de gateway sem a necessidade de rede virtual do toorebuild Olá em vários locais do pedido tooaccommodate. Antes de alterar o tipo de roteamento hello, certifique-se de que o gateway VPN local oferece suporte a configurações de VPN com base em rota.

![diagrama multissites](./media/vpn-gateway-multi-site/multisite.png "multi-site")

## <a name="points-tooconsider"></a>Pontos tooconsider

**Você não será capaz de toouse Olá toomake portal alterações toothis VPN.** É necessário um arquivo de configuração de rede toomake alterações toohello em vez de usar o portal de saudação. Se você fizer alterações no portal de hello, elas vão substituir as configurações de referência multilocal para essa rede virtual.

Você deve se sentir confortável usando o arquivo de configuração de rede de saudação pelo tempo de saudação você concluiu o procedimento de multissite hello. No entanto, se você tiver várias pessoas trabalhando em sua configuração de rede, será necessário toomake-se de que todos sabem desta limitação. Isso não significa que você não pode usar o portal de saudação em todos os. Você pode usá-lo para tudo, exceto fazer configuração alterações toothis rede virtual específico.

## <a name="before-you-begin"></a>Antes de começar

Antes de começar a configuração, verifique se Olá seguinte:

* Hardware de VPN compatível para cada caminho no local. Verificar [sobre dispositivos VPN para conectividade de rede Virtual](vpn-gateway-about-vpn-devices.md) tooverify se o dispositivo de saudação que você deseja toouse é algo que é conhecido toobe compatível.
* Um endereço IP IPv4 público voltado para o exterior para cada dispositivo VPN. endereço IP de saudação não pode ser localizado atrás de um NAT. Isso é obrigatório.
* Você precisará tooinstall Olá última versão do hello cmdlets do PowerShell do Azure. Verifique se que você instalou a versão de gerenciamento de serviço (SM) Olá na versão do Gerenciador de recursos de toohello de adição. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.
* Alguém que seja proficiente na configuração de seu hardware de VPN. Você terá toohave uma compreensão sólida de como tooconfigure seu dispositivo VPN ou trabalhar com alguém que pertença.
* intervalos de endereços IP Hello que você deseja toouse para sua rede virtual (se você ainda não tiver criado uma).
* intervalos de endereços IP de saudação para cada um dos sites de rede local Olá que você vai se conectar ao. Você precisará toomake-se de que os intervalos de endereço IP de saudação para cada um dos sites de rede local Olá que você deseja tooconnect toodo não se sobrepõem. Caso contrário, portal hello ou hello API REST rejeitará configuração hello está sendo carregada.<br>Por exemplo, se você tiver dois sites de rede local que contêm Olá IP endereço intervalo 10.2.3.0/24 e você tiver um pacote com um endereço de destino 10.2.3.3, o Azure não saberia qual site você deseja intervalos de endereços do toosend Olá pacote toobecause Olá são sobreposição. problemas de roteamento de tooprevent Azure não permite que você tooupload um arquivo de configuração com sobreposição de intervalos.

## <a name="1-create-a-site-to-site-vpn"></a>1. Criar uma VPN site a site
Se você já tiver uma VPN site a site com um gateway de roteamento dinâmico, ótimo! Você pode continuar muito[exportar definições de configuração de rede virtual Olá](#export). Se não, Olá a seguir:

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a>Se você já tiver uma rede virtual site a site, mas ela tiver um gateway de roteamento estático (baseado em política):
1. Altere o tipo de gateway toodynamic roteamento. Uma VPN multissites exige um gateway de roteamento dinâmico (também chamado de baseado em rota). tipo do toochange seu gateway, você precisa excluir de toofirst Olá gateway existente e criar um novo. Para obter instruções, consulte [como toochange Olá tipo de roteamento de VPN para o seu gateway](vpn-gateway-configure-vpn-gateway-mp.md).  
2. Configure seu novo gateway e crie seu túnel de VPN. Para obter instruções, consulte [configurar um Gateway de VPN no Portal clássico do Azure de saudação](vpn-gateway-configure-vpn-gateway-mp.md). Primeiro, altere o tipo de gateway toodynamic roteamento.

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a>Se você não tiver uma rede virtual site a site:
1. Criar sua rede virtual Site a Site usando estas instruções: [criar uma rede Virtual com uma Conexão de VPN Site a Site no Portal clássico do Azure de saudação](vpn-gateway-site-to-site-create.md).  
2. Configure um gateway de roteamento dinâmico usando estas instruções: [Configurar um gateway de VPN](vpn-gateway-configure-vpn-gateway-mp.md). Ser tooselect se **roteamento dinâmico** para seu tipo de gateway.

## <a name="export"></a>2. Exportar o arquivo de configuração de rede Olá
Exporte o arquivo de configuração de rede do Azure executando o comando a seguir de saudação. Você pode alterar o local de saudação do hello tooexport tooa diferentes local do arquivo se necessário.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a>3. Arquivo de configuração de rede Olá aberto
Abra o arquivo de configuração de rede de saudação que você baixou na última etapa do hello. Use qualquer editor de xml que desejar. arquivo Hello deve ser a seguir toohello semelhante:

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a>4. Adicionar referências a vários sites
Quando você adicionar ou remove informações de referência do site, você fará alterações de configuração toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef. Adicionando uma nova referência de site local aciona o Azure toocreate um novo túnel. O exemplo hello abaixo, a configuração de rede de saudação é para uma conexão de site único. Salve o arquivo de hello quando você terminar de fazer suas alterações.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

referências a sites adicionais tooadd (criar uma configuração de vários local), basta adicionar linhas "LocalNetworkSiteRef" adicionais, conforme mostrado no exemplo hello abaixo:

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a>5. Importar arquivo de configuração de rede Olá
Importar arquivo de configuração de rede hello. Quando você importar este arquivo com alterações hello, novos túneis de saudação serão adicionados. túneis Olá usará o gateway de dinâmico Olá que você criou anteriormente. Você pode usar portal clássico do hello, ou arquivo de saudação do PowerShell tooimport.

## <a name="6-download-keys"></a>6. Baixar chaves
Depois de adicionar os novos túneis, use Olá PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget Olá IPsec/IKE chaves pré-compartilhadas para cada túnel.

Por exemplo:

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

Se preferir, você também pode usar o hello *obter Gateway chave compartilhada rede Virtual* tooget da API REST Olá chaves pré-compartilhadas.

## <a name="7-verify-your-connections"></a>7. Verificar as conexões
Verificar o status do túnel multissites hello. Depois de baixar chaves Olá para cada túnel, você desejará tooverify conexões. Use 'Get-AzureVnetConnection' tooget túneis de uma lista de rede virtual, conforme mostrado no exemplo hello abaixo. VNet1 é o nome de saudação do hello VNet.

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

Exemplo de retorno:

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a>Próximas etapas

toolearn mais informações sobre Gateways VPN, consulte [sobre Gateways de VPN](vpn-gateway-about-vpngateways.md).
