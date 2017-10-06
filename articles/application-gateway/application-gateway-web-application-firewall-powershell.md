---
title: firewall do aplicativo web aaaConfigure - Gateway de aplicativo do Azure | Microsoft Docs
description: "Este artigo fornece orientação sobre como usar toostart web firewall do aplicativo em um Gateway de aplicativo novo ou existente."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>Configurar o firewall do aplicativo Web em um Gateway de Aplicativo novo ou existente

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [CLI do Azure](application-gateway-web-application-firewall-cli.md)

Saiba como toocreate um firewall do aplicativo web habilitado Application Gateway ou adicionar tooan de firewall do aplicativo web existente do Application Gateway.

firewall do aplicativo web Hello (WAF) no Gateway de aplicativo do Azure protege os aplicativos da web comuns ataques baseados na web como injeção de SQL, ataques de script entre sites e sequestros de sessão.

O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7. Ele fornece failover, o roteamento de desempenho de solicitações HTTP entre diferentes servidores, independentemente de estarem em nuvem hello ou local. O Gateway de Aplicativo fornece muitos recursos do ADC (controlador de entrega de aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de protocolo SSL, as sondas de integridade personalizadas, suporte para vários sites e muitos outros. toofind uma lista completa de recursos com suporte, visite: [visão geral do Application Gateway](application-gateway-introduction.md).

Olá artigo a seguir mostra como muito[adicionar tooan de firewall do aplicativo web existente do Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) e [criar um Gateway de aplicativo que usa o firewall do aplicativo web](#create-an-application-gateway-with-web-application-firewall).

![imagem de cenário][scenario]

## <a name="waf-configuration-differences"></a>Diferenças de configuração do WAF

Se você leu [criar um Gateway de aplicativos com o PowerShell](application-gateway-create-gateway-arm.md), entender Olá SKU configurações tooconfigure durante a criação de um Application Gateway. WAF fornece configurações adicionais toodefine ao configurar um Application Gateway Olá SKU. Não há nenhuma outra alteração que você faz na Olá Application Gateway em si.

| **Configuração** | **Detalhes**
|---|---|
|**SKU** |Um Gateway de Aplicativo normal sem WAF dá suporte aos tamanhos **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**. Com a introdução de saudação do WAF, há duas SKUs adicionais, **WAF\_médio** e **WAF\_grande**. Não há suporte para WAF em Gateways de Aplicativo pequenos.|
|**Camada** | Olá os valores disponíveis são **padrão** ou **WAF**. Ao usar o firewall do aplicativo Web, **WAF** deve ser escolhido.|
|**Modo** | Essa configuração é o modo de saudação do WAF. Os valores permitidos são **detecção** e **prevenção**. Quando WAF estiver configurado no modo de detecção, todas as ameaças são armazenadas em um arquivo de log. No modo de prevenção, eventos ainda estão conectados, mas invasor Olá recebe uma resposta de não autorizado 403 da saudação Application Gateway.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Adicionar tooan de firewall do aplicativo web existente do Application Gateway

Certifique-se de que você estiver usando a versão mais recente de saudação do PowerShell do Azure. Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).

1. Faça logon no tooyour conta do Azure.

    ```powershell
    Login-AzureRmAccount
    ```

2. Selecione Olá toouse de assinatura para esse cenário.

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. Recupere gateway Olá que você está adicionando o firewall do aplicativo web para.

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. Configure Olá web aplicativo firewall sku. Olá os tamanhos disponíveis são **WAF\_grande** e **WAF\_médio**. Quando o firewall do aplicativo web é usada a camada de saudação deve ser **WAF**, capacidade Olá deve ser confirmada ao definir Olá sku.

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. Defina configurações de saudação WAF conforme definido no hello exemplo a seguir:

   Para **FirewallMode**, valores disponíveis Olá são detecção e prevenção.

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. Atualize Olá Application Gateway com hello definições de saudação anterior da etapa.

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

Esse comando atualiza Olá Application Gateway com o firewall do aplicativo web. Visite [diagnóstico do Gateway do aplicativo](application-gateway-diagnostics.md) toounderstand como tooview logs para o Application Gateway. Devido a natureza de segurança toohello de WAF, logs necessidade toobe revisado regularmente toounderstand postura de segurança de saudação de seus aplicativos web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Criar um Gateway de Aplicativo com o firewall do aplicativo Web

Hello etapas a seguir se você através de todo o processo de tooend de início para a criação de um Gateway de aplicativos com o firewall do aplicativo web hello.

Certifique-se de que você estiver usando a versão mais recente de saudação do PowerShell do Azure. Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).

1. Faça logon no tooAzure executando `Login-AzureRmAccount`, são solicitada tooauthenticate com suas credenciais.

1. Verificar assinaturas Olá conta hello, executando`Get-AzureRmSubscription`

1. Escolha qual toouse suas assinaturas do Azure.

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

Crie um grupo de recursos para Olá Application Gateway.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local. Esse local é usado como o local padrão de saudação para recursos desse grupo de recursos. Certifique-se de que todos os comandos toocreate um Application Gateway usa Olá mesmo grupo de recursos.

Em Olá anterior de exemplo, criamos um grupo de recursos chamado "Appgw-RG" e o local "Oeste dos EUA."

> [!NOTE]
> Se você precisar tooconfigure uma investigação personalizada para o Gateway de aplicativo, consulte [criar um Gateway de aplicativos com testes personalizados usando o PowerShell](application-gateway-create-probe-ps.md). Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.

### <a name="configure-virtual-network"></a>Configurar rede virtual

O Gateway de Aplicativo exige sua própria sub-rede. Nesta etapa, você deve criar uma rede virtual com um espaço de endereço de 10.0.0.0/16 e duas sub-redes, um para Olá Application Gateway e outra para membros do pool de back-end.

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>Configurar o endereço IP público

Em ordem toohandle as solicitações externas, o Application Gateway requer um endereço IP público. Este endereço IP público não deve ter um `DomainNameLabel` definido toobe usado pelo Olá Application Gateway.

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a>Configurar Olá Application Gateway

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> Gateways de aplicativo criados com a configuração de firewall de aplicativo Olá web básico são configurados com CRS 3.0 para proteção.

## <a name="get-application-gateway-dns-name"></a>Obter nome DNS do Gateway de Aplicativo

Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação. Ao usar um IP público, o Gateway de Aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável. os usuários finais de tooensure pode pressionar Olá Application Gateway, um registro CNAME pode ser usado toopoint toohello pública ponto de extremidade de saudação Application Gateway. [Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure um alias, recuperar detalhes da saudação Application Gateway e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento anexado toohello Application Gateway. nome DNS do Hello Application Gateway deve ser usado toocreate um registro CNAME, qual nome DNS pontos Olá duas web aplicativos toothis. uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do Application Gateway.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a>Próximas etapas

Saiba como log de diagnóstico tooconfigure, eventos de saudação toolog detectadas ou evitados com o firewall do aplicativo web visitando [diagnóstico de Gateway do aplicativo](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
