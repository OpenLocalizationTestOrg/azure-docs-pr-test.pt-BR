---
title: aaaConfigure final tooend SSL com o Gateway de aplicativo do Azure | Microsoft Docs
description: Este artigo descreve como tooconfigure encerrar tooend SSL com o Application Gateway usando o PowerShell do Gerenciador de recursos do Azure
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a>Configurar final tooend SSL com o Application Gateway usando o PowerShell

## <a name="overview"></a>Visão geral

Oferece suporte ao Gateway de aplicativo final tooend criptografia de tráfego. Application Gateway faz isso encerrando a conexão de SSL Olá no gateway do aplicativo hello. gateway de Hello, em seguida, aplica regras de roteamento de saudação toohello tráfego, criptografa novamente o pacote de saudação e encaminha Olá pacote toohello apropriado back-end com base nas regras de roteamento Olá definidas. Qualquer resposta do servidor de web hello atravessa Olá mesmo processo toohello back end usuário.

Outro recurso ao qual o gateway de aplicativo dá suporte para definir opções personalizadas de SSL. Application Gateway oferece suporte à desabilitação Olá após a versão do protocolo; **TLSv1.0**, **TLSv1.1**, e **TLSv1.2** também definindo Olá que cipher suites toouse e Olá a ordem de preferência.  toolearn mais sobre as opções configuráveis de SSL, visite [visão geral da política de SSL](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> O SSL 2.0 e o SSL 3.0 estão desabilitados por padrão e não podem ser habilitados. Elas são consideradas inseguras e não são capaz toobe usado com o Application Gateway.

![imagem de cenário][scenario]

## <a name="scenario"></a>Cenário

Nesse cenário, você aprenderá como toocreate um gateway de aplicativo usando encerrar tooend SSL usando o PowerShell.

Este cenário:

* Criar um grupo de recursos denominado **appgw-rg**
* Criar uma rede virtual denominada **appgwvnet** com um espaço de endereço de 10.0.0.0/16.
* Crie duas sub-redes chamadas **appgwsubnet** e **appsubnet**.
* Crie uma pequeno aplicativo gateway suporte final tooend criptografia SSL que versões de protocolos SSL limites e o conjunto de codificação.

## <a name="before-you-begin"></a>Antes de começar

tooconfigure final tooend SSL com um gateway de aplicativo, um certificado é necessário para o gateway de saudação e são necessários certificados para servidores de back-end de saudação. certificado de gateway de saudação é usado tooencrypt e descriptografar Olá tráfego enviado tooit usando SSL. certificado de gateway Olá precisa toobe no formato de troca de informações pessoais (pfx). Esse formato de arquivo permite Olá privada toobe chave exportado que é exigido pelo Olá application gateway tooperform Olá criptografia e a descriptografia de tráfego.

Para final tooend SSL criptografia Olá back-end deve estar na lista de permissões com o application gateway. Isso é feito por carregar certificado público de saudação do gateway de aplicativo hello back-ends toohello. Isso garante que o gateway Olá aplicativo se comunica somente com instâncias de back-end conhecidos. Isso ainda mais protege a comunicação de tooend de término hello.

Esse processo é descrito em Olá etapas a seguir:

## <a name="create-hello-resource-group"></a>Criar hello grupo de recursos

Esta seção orienta você pelo processo de criação de um grupo de recursos, que contém o gateway de aplicativo hello.

### <a name="step-1"></a>Etapa 1

Faça logon no tooyour conta do Azure.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Etapa 2

Selecione Olá toouse de assinatura para esse cenário.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>Etapa 3

Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Criar uma rede virtual e uma sub-rede para o gateway de aplicativo hello

Olá exemplo a seguir cria uma rede virtual e duas sub-redes. Uma sub-rede é um gateway de aplicativo hello toohold usado. Olá outra sub-rede é usado para aplicativo web de saudação hospedagem hello back-ends.

### <a name="step-1"></a>Etapa 1

Atribua um intervalo de endereços para sub-rede Olá ser usada para Olá Application Gateway em si.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> As sub-redes configuradas para o gateway de aplicativo devem ser dimensionadas corretamente. O application gateway pode ser configurado para instâncias de too10. Cada instância usa um endereço IP da sub-rede hello. Uma sub-rede muito pequena pode afetar de forma adversa a ampliação de um gateway de aplicativo.
> 
> 

### <a name="step-2"></a>Etapa 2

Atribua um toobe de intervalo de endereço usado para Olá pool de endereços de back-end.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>Etapa 3

Crie uma rede virtual com sub-redes Olá definidos no hello etapas anteriores.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>Etapa 4

Recupere Olá rede virtual recursos e a sub-rede recursos toobe usado em Olá etapas a seguir:

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Criar um endereço IP público para a configuração de front-end Olá

Crie um toobe de recurso IP público usado para o gateway de aplicativo hello. Este endereço IP público será usado em uma etapa seguinte.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Application Gateway não suporta o uso de saudação de um endereço IP público criado com um rótulo de domínio definido. Há suporte para apenas para um endereço IP público com um rótulo de domínio criado dinamicamente. Se você precisar de um nome amigável de dns para o gateway de aplicativo hello, é recomendável toouse um CNAME registrar como um alias.

## <a name="create-an-application-gateway-configuration-object"></a>Criar um objeto de configuração do gateway do aplicativo

Todos os itens de configuração são definidos antes de criar o gateway de aplicativo hello. Olá etapas a seguir criam Olá itens de configuração que são necessárias para um recurso do application gateway.

### <a name="step-1"></a>Etapa 1

Criar uma configuração de IP de gateway do aplicativo, essa configuração define quais sub-rede Olá aplicativo gateway usa. Quando o gateway de aplicativo é iniciado, ele pega um endereço IP da sub-rede de saudação configurado e encaminha os endereços IP de toohello de tráfego de rede no pool IP de back-end de saudação. Tenha em mente que cada instância usa um endereço IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>Etapa 2

Criar uma configuração de IP de front-end, essa configuração mapeia um ip público ou privado endereço toohello front-end do gateway de aplicativo hello. Olá etapa a seguir associa o endereço IP público de saudação em Olá anterior etapa com configuração de IP de front-end de saudação.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>Etapa 3

Configure o pool de endereços IP de back-end Olá com endereços IP de Olá dos servidores de web de back-end de saudação. Esses endereços IP são endereços IP hello que recebem o tráfego de rede hello proveniente de um ponto de extremidade IP de front-end hello. Substituir saudação tooadd de endereços IP a seguir seus próprios pontos de extremidade do endereço IP do aplicativo.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> Um nome de domínio totalmente qualificado (FQDN) também é um valor válido no lugar de um endereço ip para servidores de back-end hello usando Olá - BackendFqdns switch. 

### <a name="step-4"></a>Etapa 4

Configure porta IP front-end de Olá para o ponto de extremidade de IP público hello. Esta porta é Olá que os usuários finais se conectem.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>Etapa 5

Configure certificado Olá para o gateway de aplicativo hello. Esse certificado é usado toodecrypt e criptografar novamente o tráfego no gateway do aplicativo hello hello.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> Este exemplo configura o certificado de saudação usado para a conexão SSL. certificado Olá precisa toobe no formato. pfx e senha Olá deve estar entre 4 too12 caracteres.

### <a name="step-6"></a>Etapa 6

Crie ouvinte HTTP Olá para o gateway de aplicativo hello. Atribua a configuração de ip de front-end hello, porta e toouse do certificado SSL.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>Etapa 7

Carregar certificado Olá toobe usado em Olá SSL habilitado recursos do pool de back-end.

> [!NOTE]
> investigação de padrão de saudação obtém a chave pública de saudação do hello **padrão** associação SSL no endereço IP do hello back-end e compara Olá valor da chave pública recebe toohello valor da chave pública fornecidos aqui. Hello recuperados de chave pública não ser necessariamente fluxos de tráfego Olá pretendido site toowhich **se** você estiver usando cabeçalhos de host e SNI Olá back-end. Em caso de dúvida, visite https://127.0.0.1/ tooconfirm de back-ends Olá qual certificado será usado para Olá **padrão** associação SSL. Use a chave pública de saudação do que a solicitação nesta seção. Se você estiver usando cabeçalhos de host e SNI em associações de HTTPS e você não receber uma resposta e o certificado de um navegador manual solicitação toohttps://127.0.0.1/ em Olá back-ends, você deve configurar uma associação de SSL padrão em Olá back-ends. Se você não fizer isso, a falha de testes e Olá back-end não está autorizado.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> certificado de saudação fornecido nesta etapa deve ser a chave pública de saudação do cert. pfx Olá presente no back-end de saudação. Exporte o certificado de saudação (não o certificado raiz de saudação) instalado no servidor de back-end Olá no. CER Formatar e usá-lo nesta etapa. Esta etapa brancas Olá back-end com o gateway de aplicativo hello.

### <a name="step-8"></a>Etapa 8

Defina configurações de http de back-end do gateway de aplicativo hello. Atribua Olá certificado carregado no hello anterior etapa toohello http configurações.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>Etapa 9

Crie uma regra de roteamento de Balanceador de carga que configura o comportamento de Balanceador de carga de saudação. Neste exemplo, é criada uma regra básica de round robin.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>Etapa 10

Configure o tamanho de instância de saudação do gateway de aplicativo hello.  Olá os tamanhos disponíveis são **padrão\_pequeno**, **padrão\_médio**, e **padrão\_grande**.  Capacidade, valores disponíveis Olá variam de 1 a 10.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> É possível escolher uma contagem de instâncias de 1 para fins de teste. É importante tooknow qualquer instância de contagem em duas instâncias não é coberto por Olá SLA e, portanto, não recomendável. Os gateways pequenos são toobe usado para desenvolvimento de teste e não para fins de produção.

### <a name="step-11"></a>Etapa 11

Configure Olá toobe de política SSL usado em Olá Application Gateway. Application Gateway oferece suporte a saudação capacidade tooset uma versão mínima para versões do protocolo SSL.

Hello valores a seguir estão uma lista das versões de protocolo que podem ser definidas.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

Conjuntos de Olá versão mínima do protocolo muito**TLSv1_2** e permite **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**e **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** somente.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a>Criar hello Application Gateway

Usando Olá todas as etapas anteriores, crie Olá Application Gateway. criação de saudação do gateway de saudação é um processo de execução longa.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>Limitar as versões de protocolo SSL em um Gateway de Aplicativo existente

Olá etapas anteriores levá-lo por meio de criar um aplicativo com final tooend SSL e desabilitando determinadas versões do protocolo SSL. Olá, exemplo a seguir desabilita certas políticas SSL em um gateway existente do aplicativo.

### <a name="step-1"></a>Etapa 1

Recupere Olá tooupdate de gateway de aplicativo.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>Etapa 2

Defina uma política de SSL. Saudação de exemplo a seguir, TLSv1.0 e TLSv1.1 são desabilitados e Olá conjuntos de codificação **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, e  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** é Olá únicos permitidos.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>Etapa 3

Por fim, atualize o gateway de saudação. É importante toonote nesta última etapa é uma tarefa demorada. Quando estiver pronto, tooend final SSL é configurada no gateway do aplicativo hello.

```powershell
$gw | Set-AzureRmApplicationGateway
```

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

Saiba mais sobre a proteção de segurança de saudação de seus aplicativos web com o Firewall do aplicativo Web por meio do Application Gateway visitando [visão geral do Firewall de aplicativo Web](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
