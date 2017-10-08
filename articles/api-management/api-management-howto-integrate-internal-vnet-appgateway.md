---
title: aaaHow toouse gerenciamento de API do Azure na rede Virtual com o Application Gateway | Microsoft Docs
description: Saiba como toosetup e configurar o gerenciamento de API do Azure na rede interna Virtual com o Application Gateway (WAF) como front-end
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a>Como integrar o gerenciamento de API em uma VNET interna com o gateway de aplicativo 

##<a name="overview"> </a> Visão geral
 
Olá serviço de gerenciamento de API pode ser configurado em uma rede Virtual no modo interno que é acessível somente dentro Olá rede Virtual. O Gateway de Aplicativo do Azure é um Serviço PAAS que fornece um balanceador de carga de Camada 7. Ele atua como um serviço de proxy reverso e fornece também um firewall do aplicativo Web (WAF).

Combinar provisionado em uma rede virtual interna com front-end Olá Application Gateway de gerenciamento de API permite Olá os seguintes cenários:

* Use Olá mesmo recurso de gerenciamento de API para consumo por clientes internos e externos consumidores.
* Usar um único recurso de Gerenciamento de API e ter uma sub-rede de APIs definida no Gerenciamento de API disponível para consumidores externos.
* Fornecem uma maneira de turnkey tooswitch acesso tooAPI gerenciamento de saudação Internet pública e desativar. 

##<a name="scenario"> </a> Cenário
Este artigo aborda como toouse uma única API de gerenciamento de serviço para clientes internos e externos e torná-la atuar como um único front-end para ambos os locais e APIs de nuvem. Você também verá como tooexpose apenas um subconjunto de suas APIs (por exemplo hello realçados em verde) para consumo externo usando a funcionalidade de PathBasedRouting Olá disponível no Application Gateway.

No primeiro exemplo hello todas as suas APIs são gerenciados somente de dentro de sua rede Virtual. Os consumidores internos (destacados em laranja) podem acessar todas as APIs internas e externas. Tráfego nunca sai tooInternet que um alto desempenho é fornecido por meio de circuitos de rota expressa.

![roteamento de url](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <a name="before-you-begin"> </a> Antes de começar

1. Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer. Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).
2. Crie uma rede virtual e sub-redes separadas para o gerenciamento de API e o gateway de aplicativo. 
3. Se você pretende toocreate um servidor DNS personalizado para Olá rede Virtual, você deve fazer isso antes de iniciar a implantação de saudação. Verifique que ele funciona, garantindo uma máquina virtual criada em uma nova sub-rede na rede Virtual de saudação pode resolver e acessar todos os pontos de extremidade de serviço do Azure.

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a>O que é necessário toocreate uma integração entre o gerenciamento de API e o Application Gateway?

* **Pool de servidores de back-end:** trata Olá virtual endereço IP interno do hello serviço de gerenciamento de API.
* **Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie. Essas configurações são aplicadas tooall servidores no pool de saudação.
* **Porta de front-end:** é Olá porta pública que é aberta no gateway do aplicativo hello. Tráfego atingi-lo obtém tooone redirecionado de saudação servidores back-end.
* **Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).
* **Regra:** regra Olá associa um pool de servidores de back-end de tooa de ouvinte.
* **Investigação de integridade personalizada:** Application Gateway, por padrão, usa toofigure de testes com base em endereços IP quais servidores de saudação BackendAddressPool estão ativos. Olá serviço de gerenciamento de API responde apenas toorequests que têm o cabeçalho de host correto hello, portanto, investigações de padrão de saudação falharem. Precisa de um teste de integridade personalizado toobe definido pelo gateway de aplicativo toohelp determinar que serviço hello está ativo e encaminhar solicitações.
* **Certificado de domínio personalizado:** tooaccess gerenciamento de API de saudação à internet, você precisa toocreate um mapeamento CNAME de seu nome DNS front-end do nome de host toohello Application Gateway. Isso garante que Olá hostname cabeçalho e um certificado enviado tooApplication Gateway é encaminhado tooAPI gerenciamento um que APIM possa reconhecer como válido.

## <a name="overview-steps"> </a> Etapas necessárias para integrar o Gerenciamento de API e o Gateway de Aplicativo 

1. Criar um grupo de recursos para o Gerenciador de Recursos.
2. Crie uma rede Virtual, sub-rede e IP público para Olá Application Gateway. Crie outra sub-rede para o gerenciamento de API.
3. Criar um serviço de gerenciamento de API dentro da sub-rede de rede virtual Olá criado acima e certifique-se de que você usa o modo de saudação interno.
4. Configure o nome de domínio personalizado de saudação em Olá serviço de gerenciamento de API.
5. Crie um objeto de configuração do Gateway de Aplicativo.
6. Crie um recurso de Gateway de Aplicativo.
7. Crie um CNAME do nome DNS público de saudação do host de proxy Olá Application Gateway toohello gerenciamento de API.

## <a name="create-a-resource-group-for-resource-manager"></a>Criar um grupo de recursos para o Gerenciador de Recursos

Certifique-se de que você estiver usando a versão mais recente de saudação do PowerShell do Azure. Há mais informações disponíveis em [Como usar o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Etapa 1

Faça logon no tooAzure

```powershell
Login-AzureRmAccount
```

Como autenticar com suas credenciais.<BR>

### <a name="step-2"></a>Etapa 2

Verificar as assinaturas de saudação conta hello e selecioná-lo.

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a>Etapa 3

Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local. Isso é usado como o local padrão de saudação para recursos desse grupo de recursos. Certifique-se de que todos os comandos toocreate uma saudação de uso de gateway de aplicativo mesmo grupo de recursos.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Criar uma rede Virtual e uma sub-rede para o gateway de aplicativo hello

saudação de exemplo a seguir mostra como toocreate usando uma rede Virtual Olá Gerenciador de recursos.

### <a name="step-1"></a>Etapa 1

Atribua a sub-rede Olá endereço intervalo 10.0.0.0/24 toohello variável toobe usada para o Gateway de aplicativo durante a criação de uma rede Virtual.

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a>Etapa 2

Atribua a sub-rede Olá endereço intervalo 10.0.1.0/24 toohello variável toobe usado para gerenciamento de API durante a criação de uma rede Virtual.

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a>Etapa 3

Criar uma rede Virtual denominado **appgwvnet** no grupo de recursos **apim-appGw-RG** para a região Oeste dos EUA de hello usando Olá prefixo 10.0.0.0/16 com sub-redes 10.0.0.0/24 e 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a>Etapa 4

Atribuir uma variável de sub-rede para as próximas etapas Olá

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a>Crie um serviço de Gerenciamento de API dentro de uma Vnet configurada no modo interno

Olá exemplo a seguir mostra como toocreate um serviço de gerenciamento de API em uma rede virtual configurado para acesso interno apenas.

### <a name="step-1"></a>Etapa 1
Crie um objeto de rede Virtual de gerenciamento de API usando Olá sub-rede $apimsubnetdata criado acima.

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a>Etapa 2
Crie um serviço de gerenciamento de API dentro Olá rede Virtual.

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
Após o êxito de saudação acima comando Consulte muito[tooaccess interno serviço de gerenciamento de API de rede virtual necessária a configuração de DNS](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess-lo.

## <a name="set-up-a-custom-domain-name-in-api-management"></a>Configure um nome de domínio personalizado no Gerenciamento de API

### <a name="step-1"></a>Etapa 1
Carregar certificado de saudação com chave privada para o domínio de saudação. Para este exemplo será `*.contoso.net`. 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a>Etapa 2
Depois que o certificado Olá é carregado, criar um objeto de configuração de nome de host para o proxy de saudação com um nome de host `api.contoso.net`, como certificado de exemplo hello fornece autoridade para Olá `*.contoso.net` domínio. 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Criar um endereço IP público para a configuração de front-end Olá

Criar um recurso IP público **publicIP01** no grupo de recursos **apim-appGw-RG** para região Oeste dos EUA de saudação.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

Um endereço IP é atribuído gateway de aplicativo toohello quando Olá serviço é iniciado.

## <a name="create-application-gateway-configuration"></a>Criar uma configuração do gateway de aplicativo

Todos os itens de configuração devem ser configurados antes de criar o gateway de aplicativo hello. Olá etapas a seguir criam Olá itens de configuração que são necessárias para um recurso do application gateway.

### <a name="step-1"></a>Etapa 1

Crie uma configuração de IP do gateway de aplicativo chamada **gatewayIP01**. Quando Application Gateway iniciado, ele seleciona um endereço IP da sub-rede de saudação configurado e rotear os endereços IP de toohello de tráfego de rede no pool IP de back-end de saudação. Tenha em mente que cada instância usa um endereço IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a>Etapa 2

Configure porta IP front-end de Olá para o ponto de extremidade de IP público hello. Esta porta é Olá que os usuários finais se conectem.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a>Etapa 3

Configure Olá IP de front-end com o ponto de extremidade IP público.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a>Etapa 4

Configurar certificado Olá para Application Gateway hello usado toodecrypt e criptografe novamente o tráfego de saudação passando.

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a>Etapa 5

Crie o ouvinte HTTP Olá Olá Application Gateway. Atribua a configuração de IP de front-end de hello, porta e tooit do certificado ssl.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a>Etapa 6

Criar um serviço de gerenciamento de API do toohello de investigação personalizada `ContosoApi` ponto de extremidade do proxy domínio. caminho de saudação `/status-0123456789abcdef` é um ponto de extremidade de integridade padrão hospedado em todos os serviços de gerenciamento de API de saudação. Definir `api.contoso.net` como um toosecure de nome de host de investigação personalizada com o certificado SSL.

> [!NOTE]
> Olá hostname `contosoapi.azure-api.net` nome do host proxy saudação padrão é configurado quando um serviço chamado `contosoapi` é criado no Azure público. 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a>Etapa 7

Carregar certificado Olá toobe usado em recursos do pool de back-end habilitado para SSL hello. Isso é hello mesmo certificado que você forneceu na etapa 4 acima.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a>Etapa 8

Defina configurações de back-end HTTP para Olá Application Gateway. Isso inclui a definição de um tempo limite para solicitação de back-end após o qual elas serão canceladas. Esse valor é diferente do tempo limite de investigação de saudação.

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a>Etapa 9

Configurar um pool de endereços IP de back-end denominado **apimbackend** com endereço IP virtual interno Olá endereço de serviço de gerenciamento de API do hello criado acima.

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a>Etapa 10

Crie configurações para um back-end fictício (inexistente). Caminhos de tooAPI de solicitações que não queremos tooexpose do gerenciamento de API por meio do Gateway do aplicativo será atingido esse back-end e retornar 404.

Defina configurações de HTTP de back-end de saudação fictício.

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Configurar um back-end fictício **dummyBackendPool**, que aponta o endereço FQDN que tooa **dummybackend.com**. Esse endereço FQDN não existe na rede virtual hello.

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

Criar uma regra de configuração que Olá Application Gateway usará por padrão que aponta o back-end do toohello inexistente **dummybackend.com** em Olá rede Virtual.

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a>Etapa 11

Configure caminhos de regra de URL para pools de back-end de saudação. Isso permite a seleção de apenas algumas das APIs de gerenciamento de API de saudação do que está sendo exposto toohello público. Por exemplo, se houver `Echo API` (/echo/), `Calculator API` (/calc/) etc., deixe somente `Echo API` acessível na Internet. 

Olá, exemplo a seguir cria uma regra simples para hello "echo /" caminho roteamento tráfego toohello back-end "apimProxyBackendPool".

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

Se o caminho de saudação não corresponder caminho Olá regras queremos tooenable do gerenciamento de API, regra Olá caminho de configuração de mapa também configura um pool de endereços de back-end do padrão chamado **dummyBackendPool**. Por exemplo, http://api.contoso.net/calc/ * vai muito**dummyBackendPool** conforme ele é definido como o pool padrão de saudação para tráfego não correspondente.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

Olá acima etapa garante que somente as solicitações de caminho hello "/ echo" são permitidos por meio de saudação Application Gateway. Solicitações tooother que APIs configurados no gerenciamento de API gerará 404 erros do Application Gateway quando acessados de saudação à Internet. 

### <a name="step-12"></a>Etapa 12

Crie uma configuração de regra para Olá Application Gateway toouse URL baseada no caminho de roteamento.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a>Etapa 13

Configure o número de saudação de instâncias e o tamanho de saudação Application Gateway. Aqui, estamos usando Olá [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) para aumentar a segurança de saudação recursos de gerenciamento de API.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a>Etapa 14

Configure WAF toobe no modo de "Prevenção".
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a>Criar um Gateway de Aplicativo

Crie um Gateway de aplicativos com todos os objetos de configuração de saudação da saudação etapas anteriores.

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a>CNAME Olá API de gerenciamento proxy hostname toohello nome DNS público do hello recurso do Application Gateway

Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação. Ao usar um IP público, o Application Gateway requer um nome DNS atribuído dinamicamente, o que pode não ser fácil toouse. 

Hello nome DNS do Application Gateway deve ser usado toocreate um registro CNAME que aponte o nome de host de proxy Olá APIM (por exemplo, `api.contoso.net` nos exemplos de saudação acima) toothis nome DNS. tooconfigure Olá front-end registro CNAME de IP, recuperar detalhes de saudação do hello Application Gateway e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento. uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do gateway.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<a name="summary"> </a> Resumo
Gerenciamento de API do Azure configurado em uma rede virtual fornece uma interface de único gateway para todas as APIs configuradas, se estiverem hospedados no local ou na nuvem de saudação. Integrando Application Gateway de gerenciamento de API fornece flexibilidade de saudação do seletivamente habilitar específico toobe APIs acessível na Internet de saudação, bem como fornecer um Firewall do aplicativo Web como uma instância de gerenciamento de API de tooyour de front-end.

##<a name="next-steps"> </a> Próximas etapas
* Saiba mais sobre o Gateway de Aplicativo do Azure
  * [Visão geral do Gateway de Aplicativo](../application-gateway/application-gateway-introduction.md)
  * [Firewall do Aplicativo Web do Gateway de Aplicativo (visualização)](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [Gateway de Aplicativo usando Roteamento com base em Caminho](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* Saiba mais sobre o gerenciamento de API nas VNETs
  * [Usando a API de gerenciamento disponíveis apenas no hello VNET](api-management-using-with-internal-vnet.md)
  * [Uso do Gerenciamento de API na rede virtual](api-management-using-with-vnet.md)
