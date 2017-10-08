---
title: Gateway de aplicativo do Azure com o balanceador de carga interno de aaaUsing | Microsoft Docs
description: "Esta página fornece instruções tooconfigure um Gateway de aplicativo do Azure com um ponto de extremidade com balanceamento de carga interno"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a>Criar um Gateway de Aplicativo com um ILB (Balanceador de Carga Interno)

> [!div class="op_single_selector"]
> * [Azure Classic PowerShell](application-gateway-ilb.md)
> * [PowerShell do Azure Resource Manager](application-gateway-ilb-arm.md)

Application Gateway pode ser configurado com um IP virtual da internet ou com um toohello de ponto de extremidade interno não exposto à internet, também conhecido como ponto de extremidade de Balanceador de carga interno (ILB). Configurar gateway Olá com um ILB é útil para aplicativos de linha de negócios internos não expostos toointernet. Também é útil para camadas de serviço/dentro de um aplicativo de várias camada, que se encontra em um toointernet de limite não exposta de segurança, mas ainda requerem a distribuição de carga de round robin, persistência de sessão ou terminação SSL. Este artigo orienta Olá etapas tooconfigure um application gateway com um ILB.

## <a name="before-you-begin"></a>Antes de começar

1. Instale a versão mais recente dos cmdlets do PowerShell do Azure hello usando Olá Web Platform Installer. Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Download](https://azure.microsoft.com/downloads/).
2. Verifique se você tem uma rede virtual em funcionamento com uma sub-rede válida.
3. Verifique se você tem servidores de back-end na rede virtual hello, ou com um IP público/VIP atribuído.

toocreate um application gateway, execute Olá etapas na ordem Olá listados a seguir. 

1. [Criar um Application Gateway](#create-a-new-application-gateway)
2. [Configurar o gateway de saudação](#configure-the-gateway)
3. [Configuração de gateway de saudação do conjunto](#set-the-gateway-configuration)
4. [Gateway de saudação inicial](#start-the-gateway)
5. [Verifique se o gateway de saudação](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Criar um Application Gateway:

**gateway de saudação toocreate**, use Olá `New-AzureApplicationGateway` cmdlet, substituindo os valores hello com seus próprios. Observe que a cobrança por gateway Olá não iniciam neste momento. A cobrança começa em uma etapa posterior, quando o gateway Olá foi iniciado com êxito.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

**toovalidate** que Olá gateway foi criado, você pode usar o hello `Get-AzureApplicationGateway` cmdlet. 

No exemplo hello, *descrição*, *InstanceCount*, e *GatewaySize* são parâmetros opcionais. Olá valor padrão para *InstanceCount* é 2, com um valor máximo de 10. Olá valor padrão para *GatewaySize* é médio. Small e Large são outros valore disponíveis. *VIP* e *DnsName* são mostrados como em branco porque o gateway Olá ainda não foi iniciado. Eles são criados depois que o gateway de hello está em estado de execução de saudação. 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a>Configurar o gateway de saudação
Uma configuração de gateway de aplicativo consiste em vários valores. valores Hello podem ser restritos a configuração de saudação tooconstruct juntos.

Olá valores são:

* **Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação. endereços IP Hello listado ou devem pertencer a sub-rede de rede virtual toohello ou devem ser um IP público/VIP. 
* **Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookies. Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.
* **Porta de front-end:** essa porta é a porta pública de saudação aberta no gateway do aplicativo hello. Tráfego atinge a essa porta e, em seguida, obtém tooone redirecionado de servidores de back-end de saudação.
* **Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, eles diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento). 
* **Regra:** regra Olá associa ouvinte hello e pool de servidores de back-end hello e define qual tráfego Olá pool do servidor de back-end deve ser direcionado toowhen que ele atinja um ouvinte específico. Atualmente, apenas Olá *básica* regra tem suporte. Olá *básica* regra é a distribuição de carga de round-robin.

Você pode construir sua configuração criando um objeto de configuração ou usando um arquivo XML de configuração. tooconstruct de sua configuração por meio de um arquivo XML de configuração, use Olá exemplo abaixo.

Observe o seguinte hello:

* Olá *FrontendIPConfigurations* elemento descreve Olá ILB detalhes relevantes para configurar o Application Gateway com um ILB. 
* IP de front-end Hello *tipo* deve ser definido too'Private'
* Olá *StaticIPAddress* devem ser definidos no qual Olá gateway recebe o tráfego IP interno do toohello desejado. Observe que Olá *StaticIPAddress* elemento é opcional. Se não for definido, um IP interno disponível da sub-rede Olá implantado é escolhido. 
* Olá valor Olá *nome* elemento especificado no *FrontendIPConfiguration* devem ser usadas em Olá HTTPListener *FrontendIP* elemento toorefer toohello FrontendIPConfiguration.
  
  **Exemplo de XML de configuração**
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
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
            <FrontendIP>fip1</FrontendIP>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
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
Em seguida, você configurará o gateway de aplicativo hello. Você pode usar o hello `Set-AzureApplicationGatewayConfig` cmdlet com um objeto de configuração ou com um arquivo XML de configuração. 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a>Gateway de saudação inicial

Uma vez configurado o gateway hello, use Olá `Start-AzureApplicationGateway` gateway de saudação do cmdlet toostart. A cobrança por um application gateway iniciado após a saudação gateway foi iniciado com êxito. 

> [!NOTE]
> Olá `Start-AzureApplicationGateway` cmdlet pode levar até toocomplete too15 a 20 minutos. 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a>Verificar status do gateway Olá

Saudação de uso `Get-AzureApplicationGateway` status de saudação do cmdlet toocheck do gateway. Se `Start-AzureApplicationGateway` com êxito na etapa anterior hello, Olá estado deve ser *executando*, Olá Vip e DnsName deve ter entradas válidas. Isso exemplo mostra Olá cmdlet na primeira linha de saudação, seguido de saída de hello. Neste exemplo, gateway hello está em execução e o tráfego tootake pronto. 

> [!NOTE]
> Olá application gateway configurado tooaccept tráfego em Olá configurou o ponto de extremidade ILB de 10.0.0.10 neste exemplo.

```powershell
Get-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway 
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   : 
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a>Próximas etapas
Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:

* [Balanceador de carga do Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gerenciador de Tráfego do Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

