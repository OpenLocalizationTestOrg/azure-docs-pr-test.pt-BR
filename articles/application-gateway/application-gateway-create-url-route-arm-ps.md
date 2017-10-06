---
title: aaaCreate regras de um gateway de aplicativo usando o roteamento de URL | Microsoft Docs
description: "Esta página fornece instruções toocreate, configure um gateway de aplicativo do Azure usando regras de roteamento de URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a>Criar um gateway de aplicativo usando roteamento com base em caminho

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-url-route-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [CLI 2.0 do Azure](application-gateway-create-url-route-cli.md)

Roteamento baseado no caminho de URL permite que você tooassociate rotas com base no caminho de URL de saudação de uma solicitação Http. Ele verifica se há um pool de back-end de tooa rota configurado para a URL de saudação apresentado em Olá Application Gateway. Em seguida, envia Olá toohello de tráfego de rede definida pelo pool de back-end. Um uso comum para roteamento baseado em URL é equilibrar solicitações de tooload para pools de toodifferent de diferentes tipos de conteúdo do servidor de back-end.

Roteamento baseado em URL apresenta um novo gateway de tooapplication do tipo de regra. O gateway de aplicativo tem dois tipos de regra: básica e PathBasedRouting. Tipo de regra básica fornece serviço de round-robin para Olá back-end pools ao PathBasedRouting distribuição de rodízio tooround Além disso, também leva padrão de caminho da URL de solicitação de saudação em consideração ao escolher o pool de back-end de saudação.

## <a name="scenario"></a>Cenário

Em Olá exemplo a seguir, o Application Gateway está servindo tráfego para contoso.com com dois grupos de servidor back-end: pool de servidores de vídeo e pool de servidores de imagem.

As solicitações de http://contoso.com/image * são roteadas pool de servidores tooimage (pool1) e http://contoso.com/video * são roteadas pool de servidores toovideo (pool2). Se nenhum dos padrões de caminho Olá corresponder, um pool de servidores padrão (pool1) é selecionado.

![roteamento de url](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a>Antes de começar

1. Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer. Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).
2. Você cria uma rede virtual e uma sub-rede para o Gateway de Aplicativo. Certifique-se de que não há máquinas ou implantações de nuvem usando sub-rede hello. gateway de aplicativo Hello deve ser sozinho em uma sub-rede de rede virtual.
3. servidores de saudação adicionados gateway de aplicativo toohello pool de back-end toouse Olá deve existir ou tiveram seus pontos de extremidade criado na rede virtual hello ou com um IP público/VIP atribuído.

## <a name="what-is-required-toocreate-an-application-gateway"></a>O que é necessário toocreate um application gateway?

* **Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação. endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP.
* **Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie. Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.
* **Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello. Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.
* **Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).
* **Regra:** regra Olá associa ouvinte hello, pool de saudação do servidor de back-end e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico.

## <a name="create-an-application-gateway"></a>Criar um Gateway de Aplicativo

diferença de saudação entre usar clássico do Azure e o Azure Resource Manager é a ordem de saudação no qual criar gateway de aplicativo hello e itens de saudação que precisam toobe configurado.

Com o Gerenciador de recursos, todos os itens que compõem um application gateway são configurados individualmente e, em seguida, juntar toocreate recurso de gateway de aplicativo hello.

Aqui estão as etapas de saudação que são necessária toocreate um application gateway:

1. Criar um grupo de recursos para o Gerenciador de Recursos.
2. Crie uma rede virtual, sub-rede e IP público para o gateway de aplicativo hello.
3. Criar um objeto de configuração do gateway de aplicativo.
4. Criar um recurso de gateway de aplicativo.

## <a name="create-a-resource-group-for-resource-manager"></a>Criar um grupo de recursos para o Gerenciador de Recursos

Certifique-se de que você estiver usando a versão mais recente de saudação do PowerShell do Azure. Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Etapa 1

Faça logon no tooAzure

```powershell
Login-AzureRmAccount
```

Você está tooauthenticate solicitado com suas credenciais.<BR>

### <a name="step-2"></a>Etapa 2

Verificar as assinaturas de saudação para conta de saudação.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Etapa 3

Escolha qual toouse suas assinaturas do Azure. <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Etapa 4

Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

Como alternativa, também é possível pode criar marcas para um grupo de recursos para o gateway de aplicativo:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local. Este grupo de recursos é usado como o local padrão de saudação para recursos desse grupo de recursos. Certifique-se de que todos os comandos toocreate uma saudação de uso de gateway de aplicativo mesmo grupo de recursos.

O exemplo hello acima, criamos um grupo de recursos chamado "appgw-RG" e o local "Oeste US".

> [!NOTE]
> Se você precisar tooconfigure uma investigação personalizada para o gateway de aplicativo, consulte [criar um gateway de aplicativos com testes personalizados usando o PowerShell](application-gateway-create-probe-ps.md). Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Criar uma rede virtual e uma sub-rede para o gateway de aplicativo hello

Olá mostrado no exemplo a seguir como toocreate uma rede virtual usando o Gerenciador de recursos. Este exemplo cria uma rede virtual para Olá Application Gateway. Application Gateway requer seu próprio sub-rede, por esse motivo, sub-rede Olá criado para Olá Application Gateway é menor do que Olá espaço de endereço de rede virtual. Isso permite que outros recursos, incluindo, mas não limitado tooweb servidores toobe configurado no hello mesmo VNET.

### <a name="step-1"></a>Etapa 1

Atribua o intervalo de endereço Olá 10.0.0.0/24 toohello sub-rede toobe variável usada toocreate uma rede virtual.  Isso cria um objeto de configuração de sub-rede Olá para Olá Application Gateway, que é usada no exemplo a seguir hello.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a>Etapa 2

Criar uma rede virtual denominada **appgwvnet** no grupo de recursos **appgw rg** para a região do hello Oeste dos EUA com hello prefixo 10.0.0.0/16 10.0.0.0/24 sub-rede. Isso conclui a configuração de saudação da saudação VNET com uma única sub-rede para Olá Application Gateway tooreside.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a>Etapa 3

Atribuir a variável de sub-rede Olá para Olá próximas etapas, isso é passado toohello `New-AzureRMApplicationGateway` cmdlet em uma etapa futura.

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Criar um endereço IP público para a configuração de front-end Olá

Criar um recurso IP público **publicIP01** no grupo de recursos **appgw rg** para região Oeste dos EUA de saudação. Gateway de aplicativo pode usar um endereço IP público, o endereço IP interno ou ambas as solicitações de tooreceive para balanceamento de carga.  Este exemplo usa apenas um endereço IP público. No hello exemplo a seguir, nenhum nome DNS é configurado para a criação de endereço IP público de saudação.  O Gateway de Aplicativo não dá suporte a nomes DNS personalizados em endereços IP públicos.  Se um nome personalizado é necessário para o ponto de extremidade público hello, um registro CNAME deve ser criado para nome DNS toopoint toohello gerado automaticamente para o endereço IP público de saudação.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Um endereço IP é atribuído gateway de aplicativo toohello quando Olá serviço é iniciado.

## <a name="create-application-gateway-configuration"></a>Criar uma configuração do gateway de aplicativo

Todos os itens de configuração devem ser configurados antes de criar o gateway de aplicativo hello. Olá etapas a seguir criam Olá itens de configuração que são necessárias para um recurso do application gateway.

### <a name="step-1"></a>Etapa 1

Crie uma configuração de IP do gateway de aplicativo chamada **gatewayIP01**. Quando Application Gateway iniciado, ele seleciona um endereço IP da sub-rede de saudação configurado e rotear os endereços IP de toohello de tráfego de rede no pool IP de back-end de saudação. Tenha em mente que cada instância usa um endereço IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a>Etapa 2

Configurar as pool de endereços IP back-end Olá denominada **pool01** e **pool2** com endereços IP para **pool1** e **pool2**. Esses endereços IP são endereços IP de saudação de recursos de saudação que estão hospedando Olá toobe de aplicativo de web protegido pelo gateway de aplicativo hello. Esses membros do pool de back-end são todos os toobe validado Íntegro por testes sejam investigações básicas ou personalizadas investigações.  O tráfego é roteado, em seguida, toothem quando a solicitação chega no gateway de aplicativo hello. Pools de back-end podem ser usados por várias regras no gateway de aplicativo hello, que significa que um pool de back-end pode ser usado para vários aplicativos web que residem em Olá mesmo host.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

Neste exemplo, há dois pools de back-end tooroute o tráfego com base no caminho de URL hello. Um pool recebe o tráfego do caminho de URL "/video", e o outro pool recebe o tráfego do caminho "/image". Substitua saudação anterior tooadd de endereços IP seus próprios pontos de extremidade do endereço IP do aplicativo. 

### <a name="step-3"></a>Etapa 3

Definir configuração de gateway do aplicativo **poolsetting01** e **poolsetting02** Olá com balanceamento de carga de tráfego de rede no pool de back-end de saudação. Neste exemplo, você definir as configurações de pool de back-end diferente para pools de back-end de saudação. Cada pool de back-end pode ter sua própria configuração de pool de back-end.  Configurações de HTTP de back-end são usadas por membros do pool regras tooroute tráfego toohello correto de back-end. Isso determina o protocolo de saudação e a porta que é usada ao enviar tráfego toohello membros do pool de back-end. Sessões baseada em cookie também são determinadas pelas configurações de HTTP de back-end de saudação.  Se habilitada, a afinidade de sessão baseada em cookie envia tráfego toohello mesmo back-end como solicitações anteriores para cada pacote.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Etapa 4

Configure Olá IP de front-end com o ponto de extremidade IP público. objeto de configuração de IP de front-end Olá é usado por uma saudação toorelate de ouvinte para fora de voltada para o endereço IP com o ouvinte de saudação.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Etapa 5

Configure portas de front-end Olá para o application gateway. objeto de configuração de porta de front-end de saudação é usado por um ouvinte toodefine qual porta Olá Application Gateway escuta para o tráfego no ouvinte Olá.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a>Etapa 6

Configure o ouvinte de saudação. Esta etapa configura um ouvinte de Olá para o endereço IP público de saudação e a porta usada tooreceive tráfego de rede. saudação de exemplo a seguir usa a configuração de IP de front-end de Olá configurado anteriormente, a configuração de porta de front-end e um protocolo (http ou https) e configura o ouvinte hello. Neste exemplo, o ouvinte de saudação escuta tooHTTP tráfego na porta 80 no endereço IP público Olá criado anteriormente.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a>Etapa 7

Configure caminhos de regra de URL para pools de back-end de saudação. Esta etapa configura o caminho relativo do hello usado pelo gateway de aplicativo e define Olá mapeamento entre o caminho da URL hello e pool de back-end de saudação que recebe o tráfego de entrada hello toohandle.

> [!IMPORTANT]
> Cada caminho deve começar com / e coloque-Olá somente um "\*" é permitido, está na extremidade hello. Exemplos válidos são /xyz, /xyz* ou /xyz/*. Olá alimentada correspondente do caminho toohello de cadeia de caracteres não inclui qualquer texto após Olá primeiro "?" ou "#" e os caracteres não são permitidos. 

Olá, exemplo a seguir cria duas regras: um para "imagem /" caminho de roteamento de tráfego tooback-end "pool1" e outra para "vídeo /" caminho de roteamento de tráfego tooback-end "pool2". Essas regras Certifique-se de que o tráfego para cada conjunto de urls é roteado toohello back-end. Por exemplo, http://contoso.com/image/figure1.jpg vai toopool1 e http://contoso.com/video/example.mp4 vai toopool2.

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

Se o caminho Olá não corresponde a qualquer uma das regras de caminho predefinido Olá, configuração de mapa de caminho de regra Olá também configura um pool de endereços de back-end do padrão. Por exemplo, http://contoso.com/shoppingcart/test.html irá toopool1 conforme ele é definido como o pool padrão de saudação para tráfego não correspondente.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a>Etapa 8

Crie uma configuração de regra. Esta etapa configura Olá application gateway toouse baseadas em caminhos roteamento de URL. Olá `$urlPathMap` variável definida em Olá etapa anterior é baseado no caminho regra de saudação de toocreate usado agora. Nesta etapa, associamos regra Olá com um ouvinte e mapeamento de caminho de url Olá criado anteriormente.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a>Etapa 9

Configure o número de saudação de instâncias e o tamanho para o gateway de aplicativo hello.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Criar um Gateway de Aplicativo

Crie um gateway de aplicativos com todos os objetos de configuração da saudação etapas anteriores.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a>Obter um nome DNS de Gateway de Aplicativo

Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação. Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável. os usuários finais de tooensure pode pressionar o gateway de aplicativo hello, um registro CNAME pode ser usado toopoint toohello ponto de extremidade público do gateway de aplicativo hello. [Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure Olá front-end registro CNAME de IP, recuperar detalhes do gateway de aplicativo hello e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento toohello anexado application gateway. nome DNS do gateway do aplicativo Hello deve ser usado toocreate um registro CNAME. uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do application gateway.

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

Se você quiser toolearn descarregamento de SSL Secure Sockets Layer (), consulte [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl-arm.md).

