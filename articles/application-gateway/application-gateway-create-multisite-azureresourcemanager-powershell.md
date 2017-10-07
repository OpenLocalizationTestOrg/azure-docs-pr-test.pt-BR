---
title: "aaaCreate um application gateway para hospedar vários sites | Microsoft Docs"
description: "Esta página fornece instruções toocreate, configure um gateway de aplicativo do Azure para hospedar vários aplicativos web em Olá mesmo gateway."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a>Criar um gateway de aplicativo para hospedar vários aplicativos Web

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-multisite-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-create-multisite-azureresourcemanager-powershell.md)

Várias opções de hospedagem de site permite que você toodeploy mais de um aplicativo web em Olá mesmo gateway de aplicativo. Ele depende da presença do cabeçalho de host na solicitação HTTP entrada hello, toodetermine o ouvinte deve receber tráfego. ouvinte de Hello, em seguida, direciona o pool de back-end do tráfego tooappropriate conforme configurado na definição de regras de saudação do gateway de saudação. Em aplicativos da web SSL habilitado, o gateway de aplicativo depende Olá indicação de nome de servidor (SNI) extensão toochoose Olá correto ouvinte para o tráfego da web hello. Um uso comum para várias opções de hospedagem de site é equilibrar solicitações de tooload para pools de servidor back-end da web diferentes domínios toodifferent. Da mesma forma diversos subdomínios de saudação mesmo domínio raiz também pode ser hospedado em Olá mesmo gateway de aplicativo.

## <a name="scenario"></a>Cenário

Em Olá exemplo a seguir, o gateway de aplicativo está servindo tráfego para contoso.com e fabrikam.com com dois grupos de servidor back-end: contoso pool de servidores e pool de servidores da fabrikam. Configuração semelhante pode ser usado toohost subdomínios como app.contoso.com e blog.contoso.com.

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a>Antes de começar

1. Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer. Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).
2. servidores de saudação adicionados gateway de aplicativo toohello pool de back-end toouse Olá deve existir ou tiveram seus pontos de extremidade criado na rede virtual de saudação em uma sub-rede separada ou com um IP público/VIP atribuído.

## <a name="requirements"></a>Requisitos

* **Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação. endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP. O FQDN também pode ser usado.
* **Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie. Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.
* **Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello. Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.
* **Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento). Para Application Gateways habilitados para vários sites, os indicadores de SNI e nome do host também são adicionados.
* **Regra:** regra Olá associa ouvinte hello, pool de servidores de back-end hello e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico. As regras são processadas na ordem Olá que estão listados e o tráfego será direcionado por meio de saudação primeira regra correspondente, independentemente de especificidade. Por exemplo, se você tiver uma regra usando um ouvinte básico e uma regra usando um ouvinte de multissite ambos em Olá mesma regra de porta, Olá com ouvinte de multissite Olá deverá ser listada antes regra Olá com o ouvinte de saudação básica em ordem para Olá multissite regra toofunction como esperado.

## <a name="create-an-application-gateway"></a>Criar um Gateway de Aplicativo

Olá seguem etapas Olá necessário toocreate um application gateway:

1. Criar um grupo de recursos para o Gerenciador de Recursos.
2. Crie uma rede virtual e sub-redes IP público para o gateway de aplicativo hello.
3. Criar um objeto de configuração do gateway de aplicativo.
4. Criar um recurso de gateway de aplicativo.

## <a name="create-a-resource-group-for-resource-manager"></a>Criar um grupo de recursos para o Gerenciador de Recursos

Certifique-se de que você estiver usando a versão mais recente de saudação do PowerShell do Azure. Há mais informações disponíveis em [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Etapa 1

Faça logon no tooAzure

```powershell
Login-AzureRmAccount
```
Você está tooauthenticate solicitado com suas credenciais.

### <a name="step-2"></a>Etapa 2

Verificar as assinaturas de saudação para conta de saudação.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Etapa 3

Escolha qual toouse suas assinaturas do Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Etapa 4

Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

Como alternativa, também é possível pode criar marcas para um grupo de recursos para o gateway de aplicativo:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local. Esse local é usado como o local padrão de saudação para recursos desse grupo de recursos. Certifique-se de que todos os comandos toocreate uma saudação de uso de gateway de aplicativo mesmo grupo de recursos.

O exemplo hello acima, criamos um grupo de recursos chamado **appgw RG** com um local de **Oeste dos EUA**.

> [!NOTE]
> Se você precisar tooconfigure uma investigação personalizada para o gateway de aplicativo, consulte [criar um gateway de aplicativos com testes personalizados usando o PowerShell](application-gateway-create-probe-ps.md). Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.

## <a name="create-a-virtual-network-and-subnets"></a>Crie a rede virtual e as sub-redes

Olá mostrado no exemplo a seguir como toocreate uma rede virtual usando o Gerenciador de recursos. Duas sub-redes são criadas nesta etapa. primeira sub-rede de saudação é para o próprio gateway de aplicativo hello. Gateway de aplicativo requer seu próprio toohold sub-rede suas instâncias. Somente outros gateways de aplicativo podem ser implantados na sub-rede. subrede segundo Olá é servidores de back-end de aplicativo usados toohold Olá.

### <a name="step-1"></a>Etapa 1

Atribua Olá endereço intervalo 10.0.0.0/24 toohello sub-rede toobe variável toohold usado Olá application gateway.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a>Etapa 2

Atribua subnet2 Olá endereço intervalo 10.0.1.0/24 toohello variável toobe usado para pools de back-end de saudação.

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a>Etapa 3

Criar uma rede virtual denominada **appgwvnet** no grupo de recursos **appgw rg** para a região do hello Oeste dos EUA com hello prefixo 10.0.0.0/16 sub-rede 10.0.0.0/24 e 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a>Etapa 4

Atribua uma variável de sub-rede para as próximas etapas hello, que cria um application gateway.

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Criar um endereço IP público para a configuração de front-end Olá

Criar um recurso IP público **publicIP01** no grupo de recursos **appgw rg** para região Oeste dos EUA de saudação.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Um endereço IP é atribuído gateway de aplicativo toohello quando Olá serviço é iniciado.

## <a name="create-application-gateway-configuration"></a>Criar uma configuração do gateway de aplicativo

Você tem tooset todos os itens de configuração antes de criar o gateway de aplicativo hello. Olá etapas a seguir criam Olá itens de configuração que são necessárias para um recurso do application gateway.

### <a name="step-1"></a>Etapa 1

Crie uma configuração de IP do gateway de aplicativo chamada **gatewayIP01**. Quando o gateway de aplicativo é iniciado, ele pega um endereço IP da sub-rede de saudação configurado e rotear os endereços IP de toohello de tráfego de rede no pool IP de back-end de saudação. Tenha em mente que cada instância usa um endereço IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a>Etapa 2

Configurar as pool de endereços IP back-end Olá denominada **pool01** e **pool2** com endereços IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** para **pool1** e **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  para **pool2**.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

Neste exemplo, há dois pools de back-end tooroute tráfego, com base no site solicitado hello. Um pool recebe o tráfego do site "contoso.com" e outro pool recebe o tráfego do site "fabrikam.com". Você tem Olá tooreplace anterior tooadd de endereços IP seus próprios pontos de extremidade do endereço IP do aplicativo. Em vez de endereços IP internos, você também pode usar endereços IP públicos, FQDN ou NIC da VM para instâncias de back-end. toospecify FQDNs em vez de IPs no PowerShell, use "-BackendFQDNs" parâmetro.

### <a name="step-3"></a>Etapa 3

Definir configuração de gateway do aplicativo **poolsetting01** e **poolsetting02** Olá com balanceamento de carga de tráfego de rede no pool de back-end de saudação. Neste exemplo, você definir as configurações de pool de back-end diferente para pools de back-end de saudação. Cada pool de back-end pode ter sua própria configuração de pool de back-end.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Etapa 4

Configure Olá IP de front-end com o ponto de extremidade IP público.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Etapa 5

Configure portas de front-end Olá para o application gateway.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a>Etapa 6

Configurar dois certificados SSL para Olá dois sites, vamos toosupport neste exemplo. Um certificado é para o tráfego de contoso.com e Olá outro é para o tráfego de fabrikam.com. Esses certificados devem ser certificados emitidos por uma Autoridade de Certificação para seus sites. Os certificados autoassinados têm suporte, mas não são recomendados para o tráfego de produção.

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a>Etapa 7

Configure dois ouvintes para dois sites Olá neste exemplo. Esta etapa configura ouvintes Olá para endereço IP público, porta e host usado tooreceive o tráfego de entrada. Parâmetro de nome de host é necessário para suporte a vários sites e deve ser o conjunto toohello site apropriado para o qual Olá tráfego é recebido. Parâmetro RequireServerNameIndication deve ser definido tootrue para que precisam de suporte para SSL em um cenário de host de vários sites. Suporte a SSL é necessário, também é necessário toospecify Olá SSL certificado que é usado toosecure tráfego para o aplicativo web. combinação de saudação de FrontendIPConfiguration, FrontendPort e nome de host deve ser exclusivo tooa ouvinte. Cada ouvinte pode dar suporte a um certificado.

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a>Etapa 8

Crie regra de dois definindo para Olá dois aplicativos web neste exemplo. Uma regra vincula ouvintes, pools de back-end e as configurações de http. Esta etapa configura Olá application gateway toouse básica regra de roteamento, uma para cada site. Tráfego tooeach site é recebida pelo seu ouvinte configurado e, em seguida, é direcionado tooits configurados de pool de back-end, usando as propriedades de saudação especificadas no hello BackendHttpSettings.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a>Etapa 9

Configure o número de saudação de instâncias e o tamanho para o gateway de aplicativo hello.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Criar um gateway de aplicativo

Crie um gateway de aplicativos com todos os objetos de configuração da saudação etapas anteriores.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> Provisionamento do Gateway de aplicativos é uma operação demorada e pode levar algum tempo toocomplete.
> 
> 

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

Saiba como tooprotect seus sites com [Application Gateway - Firewall do aplicativo Web](application-gateway-webapplicationfirewall-overview.md)

