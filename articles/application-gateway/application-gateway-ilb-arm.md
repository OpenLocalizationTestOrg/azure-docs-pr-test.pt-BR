---
title: aaaUsing Gateway de aplicativo do Azure com o balanceador de carga interno - PowerShell | Microsoft Docs
description: "Esta página fornece instruções toocreate, configurar, iniciar e excluir um gateway de aplicativo do Azure com o balanceador de carga interno (ILB) para o Gerenciador de recursos do Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a>Criar um gateway de aplicativo com um ILB (balanceador de carga interno) usando o Gerenciador de Recursos do Azure

> [!div class="op_single_selector"]
> * [Azure Classic PowerShell](application-gateway-ilb.md)
> * [PowerShell do Azure Resource Manager](application-gateway-ilb-arm.md)

Gateway de aplicativo do Azure pode ser configurado com um VIP da Internet ou com um ponto de extremidade interno não é toohello exposto à Internet, também conhecido como um ponto final (ILB) do balanceador de carga interno. Configurando o gateway Olá com um ILB é útil para aplicativos de linha de negócios internos que não são toohello exposto à Internet. Também é útil para serviços e níveis dentro de um aplicativo de várias camado que ficam em um limite de segurança que não seja toohello exposto à Internet, mas ainda precisam de round-robin carregam distribuição, persistência de sessão ou encerramento do Secure Sockets Layer (SSL).

Este artigo orienta Olá etapas tooconfigure um application gateway com um ILB.

## <a name="before-you-begin"></a>Antes de começar

1. Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer. Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).
2. Você cria uma rede virtual e uma sub-rede para o Gateway de Aplicativo. Certifique-se de que não há máquinas ou implantações de nuvem usando sub-rede hello. O Gateway de Aplicativo deve estar sozinho em uma sub-rede de rede virtual.
3. servidores de saudação que você configure o gateway de aplicativo hello toouse devem existir ou seus pontos de extremidade criados na rede virtual hello ou com um IP público/VIP atribuídos.

## <a name="what-is-required-toocreate-an-application-gateway"></a>O que é necessário toocreate um application gateway?

* **Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação. Olá endereços IP listados devem ou pertencer rede virtual toohello, mas em uma sub-rede diferente para o gateway de aplicativo hello ou deve ser um IP público/VIP.
* **Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie. Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.
* **Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello. Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.
* **Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, eles diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).
* **Regra:** regra Olá associa ouvinte hello e pool de saudação do servidor de back-end e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico. Atualmente, apenas Olá *básica* regra tem suporte. Olá *básica* regra é a distribuição de carga de round-robin.

## <a name="create-an-application-gateway"></a>Criar um Gateway de Aplicativo

diferença de saudação entre usar clássico do Azure e o Azure Resource Manager é a ordem de saudação no qual criar gateway de aplicativo hello e itens de saudação que precisam toobe configurado.
Com o Gerenciador de recursos, todos os itens que compõem um application gateway é configurada individualmente e, em seguida, juntar toocreate recurso de gateway de aplicativo hello.

Aqui estão as etapas de saudação que são necessária toocreate um application gateway:

1. Criar um grupo de recursos para o Gerenciador de Recursos
2. Criar uma rede virtual e uma sub-rede para o gateway de aplicativo hello
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

Crie um novo grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local. Isso é usado como o local padrão de saudação para recursos desse grupo de recursos. Certifique-se de que todos os toocreate de comandos usa um application gateway Olá mesmo grupo de recursos.

Olá anterior de exemplo, criamos um grupo de recursos chamado "Appgw-rg" e o local "Oeste dos EUA".

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Criar uma rede virtual e uma sub-rede para o gateway de aplicativo hello

Olá mostrado no exemplo a seguir como toocreate uma rede virtual usando o Gerenciador de recursos:

### <a name="step-1"></a>Etapa 1

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Esta etapa atribui o intervalo de endereço Olá 10.0.0.0/24 tooa sub-rede toobe variável usada toocreate uma rede virtual.

### <a name="step-2"></a>Etapa 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

Esta etapa cria uma rede virtual chamada "appgwvnet" no recurso grupo "appgw-rg" para a região do hello Oeste dos EUA com hello prefixo 10.0.0.0/16 10.0.0.0/24 sub-rede.

### <a name="step-3"></a>Etapa 3

```powershell
$subnet = $vnet.subnets[0]
```

Esta etapa atribui Olá sub-rede objeto toovariable $subnet para as próximas etapas hello.

## <a name="create-an-application-gateway-configuration-object"></a>Criar um objeto de configuração do gateway do aplicativo

### <a name="step-1"></a>Etapa 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Essa etapa cria uma configuração de IP do gateway de aplicativo chamada "gatewayIP01". Quando Application Gateway iniciado, ele seleciona um endereço IP da sub-rede de saudação configurado e rotear os endereços IP de toohello de tráfego de rede no pool IP de back-end de saudação. Tenha em mente que cada instância usa um endereço IP.

### <a name="step-2"></a>Etapa 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

Esta etapa configura as pool de endereços IP back-end Olá denominada "pool01" com o IP endereços "10.1.1.8, 10.1.1.9, 10.1.1.10". Esses são endereços IP hello que recebem o tráfego de rede hello proveniente de um ponto de extremidade IP de front-end hello. Substituir saudação anterior tooadd de endereços IP seus próprios pontos de extremidade do endereço IP do aplicativo.

### <a name="step-3"></a>Etapa 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Esta etapa configura o tráfego de rede do gateway configuração "poolsetting01" para a carga de saudação com balanceamento de aplicativo no pool de back-end de saudação.

### <a name="step-4"></a>Etapa 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

Esta etapa configura porta IP front-end Olá denominada "frontendport01" para Olá ILB.

### <a name="step-5"></a>Etapa 5

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

Esta etapa cria a configuração de IP front-end Olá chamada "fipconfig01" e associa um IP privado da sub-rede da rede virtual atual hello.

### <a name="step-6"></a>Etapa 6

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

Esta etapa cria um ouvinte Olá chamado "listener01" e associa a configuração de IP front-end do hello porta de front-end toohello.

### <a name="step-7"></a>Etapa 7

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Esta etapa cria Olá regra balanceador de carga roteamento chamada "rule01" que define o comportamento de Balanceador de carga de saudação.

### <a name="step-8"></a>Etapa 8

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Esta etapa configura o tamanho de instância de saudação do gateway de aplicativo hello.

> [!NOTE]
> Olá valor padrão para *InstanceCount* é 2, com um valor máximo de 10. Olá valor padrão para *GatewaySize* é médio. Você pode escolher entre Standard_Small, Standard_Medium e Standard_Large.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Criar um gateway de aplicativo usando New-AzureApplicationGateway

Cria um application gateway com todos os itens de configuração do hello etapas anteriores. Neste exemplo, o gateway de aplicativo hello é chamado "appgwtest".

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

Esta etapa cria um application gateway com todos os itens de configuração do hello etapas anteriores. No exemplo hello, o gateway de aplicativo hello é chamado "appgwtest".

## <a name="delete-an-application-gateway"></a>Excluir um gateway de aplicativo

toodelete um application gateway, você precisa Olá toodo etapas na ordem a seguir:

1. Saudação de uso `Stop-AzureRmApplicationGateway` gateway de saudação do cmdlet toostop.
2. Saudação de uso `Remove-AzureRmApplicationGateway` gateway de saudação do cmdlet tooremove.
3. Verificar gateway Olá foi removido usando Olá `Get-AzureApplicationGateway` cmdlet.

### <a name="step-1"></a>Etapa 1

Obter o objeto de gateway do aplicativo hello e associá-lo a variável tooa "$getgw".

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a>Etapa 2

Use `Stop-AzureRmApplicationGateway` gateway de aplicativo hello toostop. Este exemplo mostra Olá `Stop-AzureRmApplicationGateway` cmdlet na primeira linha de saudação, seguido pela saída de hello.

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Depois que o gateway de aplicativo hello está em um estado parado, use Olá `Remove-AzureRmApplicationGateway` serviço de saudação do cmdlet tooremove.

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> Olá **-force** switch pode ser uma mensagem de confirmação de remoção toosuppress usado Olá.

tooverify que Olá serviço foi removido, você pode usar o hello `Get-AzureRmApplicationGateway` cmdlet. Essa etapa não é necessária.

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a>Próximas etapas

Se você quiser tooconfigure descarregamento de SSL, consulte [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl.md).

Se você quiser tooconfigure um toouse de gateway do aplicativo com um ILB, consulte [criar um gateway de aplicativo com um balanceador de carga interno (ILB)](application-gateway-ilb.md).

Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:

* [Balanceador de carga do Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gerenciador de Tráfego do Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

