---
title: Configurar o SSL de ponta a ponta no Gateway de Aplicativo do Azure | Microsoft Docs
description: Este artigo descreve como configurar o SSL de ponta a ponta com o Gateway de Aplicativo usando o Azure PowerShell Resource Manager
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
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a>Configurar o SSL de ponta a ponta com o Gateway de Aplicativo usando o PowerShell

## <a name="overview"></a>Visão geral

O Gateway de Aplicativo oferece suporte à criptografia de tráfego de ponta a ponta. O Gateway de Aplicativo faz isso ao encerrar a conexão SSL no gateway de aplicativo. O gateway, em seguida, aplica as regras de roteamento ao tráfego, criptografa o pacote novamente e encaminha o pacote para o back-end apropriado com base nas regras de roteamento definidas. Qualquer resposta do servidor Web passa pelo mesmo processo de volta para o usuário final.

Outro recurso ao qual o gateway de aplicativo dá suporte para definir opções personalizadas de SSL. O Gateway de Aplicativo oferece suporte a desabilitar a seguinte versão de protocolo; **TLSv1.0**, **TLSv1.1**, e **TLSv1.2** como também define quais conjuntos de uso e a ordem de preferência de criptografia.  Para saber mais sobre as opções configuráveis de SSL, visite [visão geral da política de SSL](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> O SSL 2.0 e o SSL 3.0 estão desabilitados por padrão e não podem ser habilitados. Eles são considerados não seguras e não podem ser usados com o Gateway de Aplicativo.

![imagem de cenário][scenario]

## <a name="scenario"></a>Cenário

Neste cenário, você aprenderá a criar um gateway de aplicativo usando o SSL de ponta a ponta usando o PowerShell.

Este cenário:

* Criar um grupo de recursos denominado **appgw-rg**
* Criar uma rede virtual denominada **appgwvnet** com um espaço de endereço de 10.0.0.0/16.
* Crie duas sub-redes chamadas **appgwsubnet** e **appsubnet**.
* Crie um gateway de aplicativo pequeno que oferece suporte à criptografia de SSL de ponta a ponta que versões de protocolos SSL limites e conjuntos de codificação.

## <a name="before-you-begin"></a>Antes de começar

Para configurar o SSL de ponta a ponta com um gateway de aplicativo, um certificado é necessário para o gateway e são necessários certificados para os servidores de back-end. O certificado de gateway é usado para criptografar e descriptografar o tráfego enviado para ele usando SSL. O certificado do gateway precisa estar no formato pfx (Troca de Informações Pessoais). Esse formato de arquivo permite que a chave privada seja exportada, o que é exigido pelo Gateway de Aplicativo para executar criptografia e descriptografia de tráfego.

Para criptografia SSL de ponta a ponta, o back-end deve estar na lista branca do gateway de aplicativo. Isso é feito por meio do upload do certificado público dos back-ends para o gateway de aplicativo. Isso garante que o gateway de aplicativo se comunique somente com instâncias de back-end conhecidas. Isso protege ainda mais a comunicação de ponta a ponta.

Cada atributo é descrito nas etapas a seguir:

## <a name="create-the-resource-group"></a>Criar o Grupo de recursos

Esta seção orienta você pela criação de um grupo de recursos que contenha o gateway de aplicativo.

### <a name="step-1"></a>Etapa 1

Faça logon na sua Conta do Azure.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Etapa 2

Selecione a assinatura a ser usada nesse cenário.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>Etapa 3

Crie um grupo de recursos (ignore esta etapa se você estiver usando um grupo de recursos existente).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a>Criar uma rede virtual e uma sub-rede para o gateway de aplicativo

O exemplo a seguir cria uma rede virtual e duas sub-redes. Uma sub-rede é usada para armazenar o gateway de aplicativo. A outra sub-rede é usada para os back-ends que hospedam o aplicativo Web.

### <a name="step-1"></a>Etapa 1

Atribua um intervalo de endereços para que a sub-rede seja usada para o próprio Gateway de Aplicativo.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> As sub-redes configuradas para o gateway de aplicativo devem ser dimensionadas corretamente. Um gateway de aplicativo pode ser configurado para até 10 instâncias. Cada instância usa um endereço IP da sub-rede. Uma sub-rede muito pequena pode afetar de forma adversa a ampliação de um gateway de aplicativo.
> 
> 

### <a name="step-2"></a>Etapa 2

Atribua um intervalo de endereços a ser usado para o pool de endereços do Back-end.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>Etapa 3

Crie uma rede virtual com as sub-redes definidas nas etapas anteriores.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>Etapa 4

Recupere o recurso de rede virtual e os recursos de sub-rede a serem usados nestas etapas:

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a>Criar um endereço IP público para a configuração de front-end

Crie um recurso IP público a ser usado para o gateway de aplicativo. Este endereço IP público será usado em uma etapa seguinte.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> O Gateway de Aplicativo não dá suporte ao uso de um endereço IP público criado com um rótulo de domínio definido. Há suporte para apenas para um endereço IP público com um rótulo de domínio criado dinamicamente. Se você precisar de um nome amigável de dns para o gateway de aplicativo, é recomendável usar um registro CNAME como alias.

## <a name="create-an-application-gateway-configuration-object"></a>Criar um objeto de configuração do gateway do aplicativo

Todos os itens de configuração são definidos antes da criação do gateway de aplicativo. As etapas a seguir criam os itens de configuração necessários para um recurso de gateway de aplicativo.

### <a name="step-1"></a>Etapa 1

Crie uma configuração de IP do gateway de aplicativo para configurar qual sub-rede será usada pelo gateway de aplicativo. Quando o Gateway de Aplicativo é iniciado, ele escolhe um endereço IP na sub-rede configurada e encaminha o tráfego de rede para os endereços IP no pool de IPs de back-end. Tenha em mente que cada instância usa um endereço IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>Etapa 2

Crie uma configuração de IP de front-end para mapear um endereço ip público ou privado para o front-end do gateway de aplicativo. A etapa a seguir associa o endereço IP público da etapa anterior à configuração de IP do front-end.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>Etapa 3

Configure o pool de endereços IP do back-end com os endereços IP dos servidores Web de back-end. Esses endereços IP são os que receberão o tráfego de rede proveniente do ponto de extremidade do IP de front-end. Você substitui os endereços IP a seguir para adicionar seus próprios pontos de extremidade de endereço IP do aplicativo.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> Um nome de domínio totalmente qualificado (FQDN) também é um valor válido no lugar de um endereço ip para os servidores de back-end usando a opção -BackendFqdns. 

### <a name="step-4"></a>Etapa 4

Configure a porta IP front-end para o ponto de extremidade IP público. Essa porta é a porta à qual os usuários finais se conectam.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>Etapa 5

Configure o certificado para o gateway de aplicativo. Esse certificado é usado para descriptografar e criptografar novamente o tráfego no gateway de aplicativo.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> Esta amostra configura o certificado usado para a conexão SSL. O certificado deve estar no formato .pfx e a senha deve ter entre 4 e 12 caracteres.

### <a name="step-6"></a>Etapa 6

Crie o ouvinte HTTP para o gateway de aplicativo. Atribua a configuração do ip, a porta e o certificado ssl do front-end a ser usado.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>Etapa 7

Carregue o certificado a ser usado nos recursos do pool de back-end habilitado para SSL.

> [!NOTE]
> A investigação padrão obtém a chave pública a associação SSL **padrão** no endereço IP do back-end e compara o valor da chave pública que recebe ao valor da chave pública fornecida aqui. A chave pública recuperada pode não ser necessariamente o local desejado para o qual o tráfego fluirá **se** você estiver usando cabeçalhos de host e SNI no back-end. Em caso de dúvida, visite https://127.0.0.1/ nos back-ends para confirmar qual certificado será usado para a associação SSL **padrão**. Use a chave pública dessa solicitação nesta seção. Se você estiver usando cabeçalhos de host e SNI em associações HTTPS e você não receberá uma resposta e um certificado de uma solicitação de navegador manual para https://127.0.0.1/ em back-ends, deverá configurar uma associação SSL padrão nos back-ends. Se você não fizer isso, as investigações falharão e o back-end não estará na lista branca.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> O certificado fornecido nesta etapa deve ser a chave pública do certificado pfx presente no back-end. Exporte o certificado (não o certificado raiz) instalado no servidor de back-end no formato .CER e use-o nesta etapa. Esta etapa coloca o back-end na lista branca do gateway de aplicativo.

### <a name="step-8"></a>Etapa 8

Defina as configurações de http de back-end do gateway de aplicativo. Atribua o certificado carregado na etapa anterior às configurações de http.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>Etapa 9

Crie uma regra de roteamento do balanceador de carga que configure o comportamento do balanceador de carga. Neste exemplo, é criada uma regra básica de round robin.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>Etapa 10

Configure o tamanho da instância do gateway de aplicativo.  Os tamanhos disponíveis são **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**.  Para a capacidade e os valores disponíveis são 1 a 10.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> É possível escolher uma contagem de instâncias de 1 para fins de teste. É importante saber que qualquer contagem de instâncias em duas instâncias não é coberta por um SLA e, portanto, não são recomendadas. Gateways pequenos devem ser usados para teste de desenvolvimento e não para fins de produção.

### <a name="step-11"></a>Etapa 11

Configure a política SSL a ser usada no Gateway de Aplicativo. O Gateway de Aplicativo oferece suporte a capacidade de definir uma versão mínima para versões de protocolo SSL.

Os valores a seguir são uma lista de versões do protocolo que podem ser definidas.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

Define a versão mínima do protocolo para **TLSv1_2** e permita **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, e **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** somente.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a>Criar o Application Gateway

Usando todas as etapas anteriores, crie o Gateway de Aplicativo. A criação do gateway é um processo de execução demorada.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>Limitar as versões de protocolo SSL em um Gateway de Aplicativo existente

As etapas anteriores levam você a criar um aplicativo com ssl de ponta a ponta e a desabilitar determinadas versões do protocolo SSL. O exemplo a seguir desabilita determinadas políticas de SSL em um gateway de aplicativo existente.

### <a name="step-1"></a>Etapa 1

Recupere o gateway de aplicativo para atualizar.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>Etapa 2

Defina uma política de SSL. No exemplo a seguir, TLSv1.0 e TLSv1.1 estão desabilitadas e os conjuntos de codificação **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, e **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** são os únicos permitidos.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>Etapa 3

Por fim, atualize o gateway. É importante observar que essa última etapa é uma tarefa de execução demorada. Quando estiver pronto, o SSL de ponta a ponta será configurado no gateway de aplicativo.

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a>Obter um nome DNS de Gateway de Aplicativo

Depois de criar o gateway, a próxima etapa será configurar o front-end para comunicação. Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável. Para garantir que os usuários finais possam alcançar o gateway de aplicativo, um registro CNAME pode ser usado para apontar para o ponto de extremidade público do gateway de aplicativo. [Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). Para isso, recupere detalhes do Gateway de Aplicativo e seu nome DNS/IP associado usando o elemento PublicIPAddress anexado ao Gateway de Aplicativo. O nome DNS do Gateway de Aplicativo deve ser usado para criar um registro CNAME que aponta os dois aplicativos Web para esse nome DNS. O uso de registros A não é recomendável, pois o VIP pode mudar na reinicialização do gateway de aplicativo.

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

Saiba mais sobre como otimizar a segurança dos seus aplicativos Web com o Firewall do Aplicativo Web por meio do Gateway de Aplicativo ao visitar [Visão geral do Firewall de Aplicativo Web](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
