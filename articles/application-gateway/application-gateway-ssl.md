---
title: "aaaConfigure SSL descarregar clássico - Gateway de aplicativo do Azure - PowerShell | Microsoft Docs"
description: "Este artigo fornece instruções toocreate descarregar um application gateway com SSL usando Olá modelo de implantação clássico do Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a>Configure um gateway de aplicativo para descarregamento SSL usando o modelo de implantação clássico Olá

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-ssl-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [CLI 2.0 do Azure](application-gateway-ssl-cli.md)

Gateway de aplicativo do Azure pode ser configurado tooterminate Olá Secure Sockets Layer (SSL) sessão Olá gateway tooavoid cara SSL descriptografia tarefas toohappen no farm de web hello. Descarregamento SSL também simplifica a configuração de servidor front-end do hello e gerenciamento de aplicativo da web hello.

## <a name="before-you-begin"></a>Antes de começar

1. Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer. Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).
2. Verifique se você tem uma rede virtual em funcionamento com uma sub-rede válida. Certifique-se de que não há máquinas ou implantações de nuvem usando sub-rede hello. gateway de aplicativo Hello deve ser sozinho em uma sub-rede de rede virtual.
3. servidores de saudação que você configure o gateway de aplicativo hello toouse devem existir ou seus pontos de extremidade criados na rede virtual hello ou com um IP público/VIP atribuídos.

tooconfigure SSL descarregar em um gateway de aplicativo, Olá etapas na ordem Olá listados a seguir:

1. [Criar um Application Gateway](#create-an-application-gateway)
2. [Carregar certificados SSL](#upload-ssl-certificates)
3. [Configurar o gateway de saudação](#configure-the-gateway)
4. [Configuração de gateway de saudação do conjunto](#set-the-gateway-configuration)
5. [Gateway de saudação inicial](#start-the-gateway)
6. [Verificar status do gateway Olá](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Criar um Gateway de Aplicativo

gateway toocreate Olá Olá use `New-AzureApplicationGateway` cmdlet, substituindo os valores hello com seus próprios. Cobrança para o gateway de saudação não funciona neste momento. A cobrança começa em uma etapa posterior, quando o gateway Olá foi iniciado com êxito.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate que Olá gateway foi criado, você pode usar o hello `Get-AzureApplicationGateway` cmdlet.

No exemplo hello, *descrição*, *InstanceCount*, e *GatewaySize* são parâmetros opcionais. Olá valor padrão para *InstanceCount* é 2, com um valor máximo de 10. Olá valor padrão para *GatewaySize* é médio. Small e Large são outros valore disponíveis. *VirtualIPs* e *DnsName* são mostrados como em branco porque o gateway Olá ainda não foi iniciado. Esses valores são criados depois que o gateway de hello está em estado de execução de saudação.

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a>Carregar certificados SSL

Use `Add-AzureApplicationGatewaySslCertificate` certificado do servidor de saudação tooupload no *pfx* gateway de formato de aplicativo toohello. nome do certificado Olá é um nome de usuário escolhido e deve ser exclusivo no gateway do aplicativo hello. Esse certificado é chamado tooby esse nome em todas as operações de gerenciamento de certificado no gateway do aplicativo hello.

Este exemplo a seguir mostra o cmdlet hello, substitua valores de saudação no exemplo hello com seus próprios.

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

Em seguida, valide o carregamento do certificado hello. Saudação de uso `Get-AzureApplicationGatewayCertificate` cmdlet.

Isso exemplo mostra Olá cmdlet na primeira linha de saudação, seguido de saída de hello.

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> senha do certificado Olá tem toobe entre 4 too12 caracteres, letras ou números. Caracteres especiais não são aceitos.

## <a name="configure-hello-gateway"></a>Configurar o gateway de saudação

Uma configuração de gateway de aplicativo consiste em vários valores. valores Hello podem ser restritos a configuração de saudação tooconstruct juntos.

Olá valores são:

* **Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação. endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP.
* **Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie. Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.
* **Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello. Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.
* **Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).
* **Regra:** regra Olá associa ouvinte hello e pool de saudação do servidor de back-end e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico. Atualmente, apenas Olá *básica* regra tem suporte. Olá *básica* regra é a distribuição de carga de round-robin.

**Observações adicionais sobre a configuração**

Para a configuração de certificados SSL, Olá protocolo em **HttpListener** devem alterar muito*Https* (com distinção entre maiusculas e minúsculas). Olá **SslCert** elemento é adicionado muito**HttpListener** com hello valor definido toohello mesmo nome como usado no carregamento de saudação das anteriores a seção de certificados SSL. porta de front-end Olá deve ser atualizado too443.

**afinidade de baseada em cookie tooenable**: um application gateway pode ser configurado tooensure que uma solicitação de uma sessão de cliente é sempre toohello direcionado mesma VM no farm de web hello. Este cenário é feito pela inclusão de um cookie de sessão que permite que o tráfego de toodirect gateway Olá adequadamente. Definir afinidade baseada em cookie tooenable, **CookieBasedAffinity** muito*habilitado* em Olá **BackendHttpSettings** elemento.

Você pode construir sua configuração criando um objeto de configuração ou usando um arquivo XML de configuração.
tooconstruct sua configuração por meio de uma configuração de arquivo XML, use Olá exemplo a seguir:

**Exemplo de XML de configuração**

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

## <a name="set-hello-gateway-configuration"></a>Configuração de gateway de saudação do conjunto

Em seguida, defina o gateway de aplicativo hello. Você pode usar o hello `Set-AzureApplicationGatewayConfig` cmdlet com um objeto de configuração ou com um arquivo XML de configuração.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a>Gateway de saudação inicial

Uma vez configurado o gateway hello, use Olá `Start-AzureApplicationGateway` gateway de saudação do cmdlet toostart. A cobrança por um application gateway iniciado após a saudação gateway foi iniciado com êxito.

> [!NOTE]
> Olá `Start-AzureApplicationGateway` cmdlet pode levar até toofinish too15 a 20 minutos.
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Verificar status do gateway Olá

Saudação de uso `Get-AzureApplicationGateway` status de saudação do cmdlet toocheck do gateway de saudação. Se `Start-AzureApplicationGateway` com êxito na etapa anterior de saudação, *estado* devem estar em execução, e *VirtualIPs* e *DnsName* devem ter entradas válidas.

Este exemplo mostra um application gateway, em execução, e o tráfego tootake pronto.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a>Próximas etapas

Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:

* [Balanceador de carga do Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gerenciador de Tráfego do Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

