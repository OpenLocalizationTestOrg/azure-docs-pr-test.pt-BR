---
title: aaaConfigure SSL descarregar - Gateway de aplicativo do Azure - PowerShell | Microsoft Docs
description: "Esta página fornece instruções toocreate descarregar um application gateway com SSL usando o Gerenciador de recursos do Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>Configurar um gateway de aplicativo para descarregamento SSL usando o Gerenciador de Recursos do Azure

> [!div class="op_single_selector"]
> * [portal do Azure](application-gateway-ssl-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [CLI 2.0 do Azure](application-gateway-ssl-cli.md)

Gateway de aplicativo do Azure pode ser configurado tooterminate Olá Secure Sockets Layer (SSL) sessão Olá gateway tooavoid cara SSL descriptografia tarefas toohappen no farm de web hello. Descarregamento SSL também simplifica a configuração de servidor front-end do hello e gerenciamento de aplicativo da web hello.

## <a name="before-you-begin"></a>Antes de começar

1. Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer. Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).
2. Crie uma rede virtual e uma sub-rede para o gateway de aplicativo hello. Certifique-se de que não há máquinas ou implantações de nuvem usando sub-rede hello. O Gateway de Aplicativo deve estar sozinho em uma sub-rede de rede virtual.
3. servidores Olá configurar o gateway de aplicativo hello toouse devem existir ou tem seus pontos de extremidade criado na rede virtual hello ou com um IP público/VIP atribuído.

## <a name="what-is-required-toocreate-an-application-gateway"></a>O que é necessário toocreate um application gateway?

* **Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação. endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP.
* **Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie. Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.
* **Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello. Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.
* **Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, essas configurações diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).
* **Regra:** regra Olá associa ouvinte hello e pool de saudação do servidor de back-end e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico. Atualmente, apenas Olá *básica* regra tem suporte. Olá *básica* regra é a distribuição de carga de round-robin.

**Observações adicionais sobre a configuração**

Para a configuração de certificados SSL, Olá protocolo em **HttpListener** devem alterar muito*Https* (com distinção entre maiusculas e minúsculas). Olá **SslCertificate** elemento é adicionado muito**HttpListener** com valor de variável Olá configurado para o certificado SSL da saudação. porta de front-end Olá deve ser atualizado too443.

**afinidade de baseada em cookie tooenable**: um application gateway pode ser configurado tooensure que uma solicitação de uma sessão de cliente é sempre toohello direcionado mesma VM no farm de web hello. Este cenário é feito pela inclusão de um cookie de sessão que permite que o tráfego de toodirect gateway Olá adequadamente. Definir afinidade baseada em cookie tooenable, **CookieBasedAffinity** muito*habilitado* em Olá **BackendHttpSettings** elemento.

## <a name="create-an-application-gateway"></a>Criar um Gateway de Aplicativo

diferença de saudação entre usar o modelo de implantação clássico do Azure hello e Gerenciador de recursos do Azure é a ordem de saudação que você criar um aplicativo gateway e Olá itens que precisam toobe configurado.

Com o Gerenciador de recursos, todos os componentes de um application gateway são configurados individualmente e, em seguida, coloque junto toocreate um recurso do application gateway.

Aqui está Olá etapas necessárias toocreate um application gateway:

1. Criar um grupo de recursos para o Gerenciador de Recursos
2. Criar rede virtual, sub-rede e IP público para o gateway de aplicativo hello
3. Criar um objeto de configuração do gateway do aplicativo
4. Criar um recurso do gateway de aplicativo

## <a name="create-a-resource-group-for-resource-manager"></a>Criar um grupo de recursos para o Gerenciador de Recursos

Certifique-se de que você alterne os cmdlets do PowerShell modo toouse hello Azure Resource Manager. Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Etapa 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Etapa 2

Verificar as assinaturas de saudação para conta de saudação.

```powershell
Get-AzureRmSubscription
```

Você está tooauthenticate solicitado com suas credenciais.

### <a name="step-3"></a>Etapa 3

Escolha qual toouse suas assinaturas do Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Etapa 4

Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local. Essa configuração é usada como o local padrão de saudação para recursos desse grupo de recursos. Certifique-se de que todos os toocreate de comandos usa um application gateway Olá mesmo grupo de recursos.

O exemplo hello acima, criamos um grupo de recursos chamado **appgw RG** e local **Oeste dos EUA**.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Criar uma rede virtual e uma sub-rede para o gateway de aplicativo hello

Olá mostrado no exemplo a seguir como toocreate uma rede virtual usando o Gerenciador de recursos:

### <a name="step-1"></a>Etapa 1

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Este exemplo atribui o intervalo de endereço Olá 10.0.0.0/24 tooa sub-rede toobe variável usada toocreate uma rede virtual.

### <a name="step-2"></a>Etapa 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

Este exemplo cria uma rede virtual denominada **appgwvnet** no grupo de recursos **appgw rg** para a região do hello Oeste dos EUA com hello prefixo 10.0.0.0/16 10.0.0.0/24 sub-rede.

### <a name="step-3"></a>Etapa 3

```powershell
$subnet = $vnet.Subnets[0]
```

Este exemplo atribui Olá sub-rede objeto toovariable $subnet para as próximas etapas hello.

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Criar um endereço IP público para a configuração de front-end Olá

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Este exemplo cria um recurso IP público **publicIP01** no grupo de recursos **appgw rg** para região Oeste dos EUA de saudação.

## <a name="create-an-application-gateway-configuration-object"></a>Criar um objeto de configuração do gateway do aplicativo

### <a name="step-1"></a>Etapa 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Esta amostra cria uma configuração de IP do gateway de aplicativo chamada **gatewayIP01**. Quando Application Gateway iniciado, ele seleciona um endereço IP da sub-rede de saudação configurado e rotear os endereços IP de toohello de tráfego de rede no pool IP de back-end de saudação. Tenha em mente que cada instância usa um endereço IP.

### <a name="step-2"></a>Etapa 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

Este exemplo configura o pool de endereços do hello back-end IP denominado **pool01** com endereços IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** . Esses valores são endereços IP hello que recebem o tráfego de rede hello proveniente de um ponto de extremidade IP de front-end hello. Substitua os endereços IP de saudação da saudação anterior exemplo com endereços IP de saudação de seus pontos de extremidade do aplicativo web.

### <a name="step-3"></a>Etapa 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

Este exemplo configura a configuração de gateway do aplicativo **poolsetting01** tooload balanceada de tráfego de rede no pool de back-end de saudação.

### <a name="step-4"></a>Etapa 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

Este exemplo configura a porta IP front-end Olá chamada **frontendport01** ponto de extremidade IP pública hello.

### <a name="step-5"></a>Etapa 5

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

Este exemplo configura o certificado de saudação usado para a conexão SSL. certificado Olá precisa toobe no formato. pfx e senha Olá deve estar entre 4 too12 caracteres.

### <a name="step-6"></a>Etapa 6

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

Este exemplo cria a configuração de IP front-end Olá nomeada **fipconfig01** e associa Olá endereço IP público com configuração de IP de front-end de saudação.

### <a name="step-7"></a>Etapa 7

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

Este exemplo cria o nome do ouvinte Olá **listener01** e associa Olá certificado e configuração de IP de front-end da toohello de porta de front-end.

### <a name="step-8"></a>Etapa 8

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Este exemplo cria Olá regra balanceador de carga roteamento denominada **rule01** que define o comportamento de Balanceador de carga de saudação.

### <a name="step-9"></a>Etapa 9

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Este exemplo configura o tamanho de instância de saudação do gateway de aplicativo hello.

> [!NOTE]
> Olá valor padrão para *InstanceCount* é 2, com um valor máximo de 10. Olá valor padrão para *GatewaySize* é médio. Você pode escolher entre Standard_Small, Standard_Medium e Standard_Large.

### <a name="step-10"></a>Etapa 10

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

Esta etapa define Olá toouse de política SSL no gateway do aplicativo hello. Visite [versões de política de configurar SSL e conjuntos de codificação no Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn mais.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Criar um gateway de aplicativo usando New-AzureApplicationGateway

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

Este exemplo cria um application gateway com todos os itens de configuração do hello etapas anteriores. No exemplo hello, o gateway de aplicativo hello é chamado **appgwtest**.

## <a name="get-application-gateway-dns-name"></a>Obter um nome DNS de Gateway de Aplicativo

Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação. Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável. os usuários finais de tooensure pode pressionar o gateway de aplicativo hello, um registro CNAME pode ser usado toopoint toohello ponto de extremidade público do gateway de aplicativo hello. [Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo, detalhes de recuperar de gateway de aplicativo hello e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento toohello anexado application gateway. nome DNS do gateway do aplicativo Hello deve ser usado toocreate um registro CNAME, qual nome DNS pontos Olá duas web aplicativos toothis. uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do application gateway.


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

Se você quiser tooconfigure um toouse de gateway do aplicativo com um balanceador de carga interno (ILB), consulte [criar um gateway de aplicativo com um balanceador de carga interno (ILB)](application-gateway-ilb.md).

Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:

* [Balanceador de carga do Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gerenciador de Tráfego do Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

