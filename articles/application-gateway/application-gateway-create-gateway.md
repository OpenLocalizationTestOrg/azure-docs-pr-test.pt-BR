---
title: aaaCreate, iniciar ou excluir um application gateway | Microsoft Docs
description: "Esta página fornece instruções toocreate, configurar, iniciar e excluir um gateway de aplicativo do Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a>Criar, iniciar ou excluir um gateway de aplicativo com o PowerShell 

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Modelo do Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [CLI do Azure](application-gateway-create-gateway-cli.md)

O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7. Ele fornece failover, o roteamento de desempenho de solicitações HTTP entre diferentes servidores, independentemente de estarem em nuvem hello ou local. O Gateway de Aplicativo fornece muitos recursos do ADC (Controlador de Entrega de Aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de SSL (Secure Sockets Layer), as sondas de integridade personalizadas, suporte para vários sites e muitos outros. toofind uma lista completa de recursos com suporte, visite [visão geral do Application Gateway](application-gateway-introduction.md)

Este artigo orienta Olá etapas toocreate, configurar, iniciar e excluir um application gateway.

## <a name="before-you-begin"></a>Antes de começar

1. Instale a versão mais recente Olá Olá Azure de cmdlets do PowerShell usando Olá Web Platform Installer. Você pode baixar e instalar a versão mais recente de saudação do hello **do Windows PowerShell** seção Olá [página de Downloads](https://azure.microsoft.com/downloads/).
2. Se você tiver uma rede virtual existente, selecione uma sub-rede vazia existente ou criar uma nova sub-rede na rede virtual existente unicamente para uso pelo gateway de aplicativo hello. Não é possível implantar Olá application gateway tooa rede virtual diferente de recursos de saudação pretende toodeploy por trás do gateway de aplicativo hello, a menos que o emparelhamento de rede virtual é usado. toolearn mais visitar [emparelhamento de rede virtual](../virtual-network/virtual-network-peering-overview.md)
3. Verifique se você tem uma rede virtual em funcionamento com uma sub-rede válida. Certifique-se de que não há máquinas ou implantações de nuvem usando sub-rede hello. gateway de aplicativo Hello deve ser sozinho em uma sub-rede de rede virtual.
4. servidores de saudação que você configure o gateway de aplicativo hello toouse devem existir ou seus pontos de extremidade criados na rede virtual hello ou com um IP público/VIP atribuídos.

## <a name="what-is-required-toocreate-an-application-gateway"></a>O que é necessário toocreate um application gateway?

Quando você usa Olá `New-AzureApplicationGateway` gateway de aplicativo do comando toocreate hello, nenhuma configuração é definida neste momento e recurso Olá recém-criado são configuradas usando XML ou um objeto de configuração.

Olá valores são:

* **Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação. endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP.
* **Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie. Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.
* **Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello. Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.
* **Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).
* **Regra:** regra Olá associa ouvinte hello e pool de saudação do servidor de back-end e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico.

## <a name="create-an-application-gateway"></a>Criar um Gateway de Aplicativo

toocreate um application gateway:

1. Criar um recurso de gateway de aplicativo.
2. Crie um arquivo XML de configuração ou um objeto de configuração.
3. Confirme Olá configuração toohello recém-criados em recursos de gateway do aplicativo.

> [!NOTE]
> Se você precisar tooconfigure uma investigação personalizada para o gateway de aplicativo, consulte [criar um gateway de aplicativos com testes personalizados usando o PowerShell](application-gateway-create-probe-classic-ps.md). Confira [investigações personalizadas e monitoramento de integridade](application-gateway-probe-overview.md) para saber mais.

![Cenário de exemplo][scenario]

### <a name="create-an-application-gateway-resource"></a>Criar um recurso do gateway de aplicativo

gateway toocreate Olá Olá use `New-AzureApplicationGateway` cmdlet, substituindo os valores hello com seus próprios. Cobrança para o gateway de saudação não funciona neste momento. A cobrança começa em uma etapa posterior, quando o gateway Olá foi iniciado com êxito.

Olá exemplo a seguir cria um application gateway usando uma rede virtual chamada "testvnet1" e uma sub-rede denominada "subnet-1":

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

*Description*, *InstanceCount* e *GatewaySize* são parâmetros opcionais.

toovalidate que Olá gateway foi criado, você pode usar o hello `Get-AzureApplicationGateway` cmdlet.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> Olá valor padrão para *InstanceCount* é 2, com um valor máximo de 10. Olá valor padrão para *GatewaySize* é médio. Você pode escolher entre Small, Medium e Large.

*VirtualIPs* e *DnsName* são mostrados como em branco porque o gateway Olá ainda não foi iniciado. Eles são criados depois que o gateway de hello está em estado de execução de saudação.

## <a name="configure-hello-application-gateway"></a>Configurar o gateway de aplicativo hello

Você pode configurar o gateway de aplicativo hello usando XML ou um objeto de configuração.

### <a name="configure-hello-application-gateway-by-using-xml"></a>Configurar o gateway de aplicativo hello usando XML

Em Olá exemplo a seguir, use um tooconfigure do arquivo XML todas as configurações de gateway do aplicativo e confirmá-las toohello recursos de gateway de aplicativo.  

#### <a name="step-1"></a>Etapa 1

Saudação de cópia tooNotepad de texto a seguir.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Edite valores de saudação entre parênteses Olá Olá para itens de configuração. Salve o arquivo de saudação com extensão. XML.

> [!IMPORTANT]
> item de protocolo Hello Http ou Https diferencia maiusculas de minúsculas.

saudação de exemplo a seguir mostra como toouse uma configuração de arquivo tooset o gateway de aplicativo hello. carga de exemplo Hello balanceia o tráfego HTTP na porta pública 80 e envia o tráfego de rede a porta 80 tooback ponta entre dois endereços IP.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
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

#### <a name="step-2"></a>Etapa 2

Em seguida, configure o gateway de aplicativo hello. Saudação de uso `Set-AzureApplicationGatewayConfig` cmdlet com um arquivo XML de configuração.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a>Configurar o gateway de aplicativo hello usando um objeto de configuração

saudação de exemplo a seguir mostra como tooconfigure Olá gateway de aplicativo por meio de objetos de configuração. Todos os itens de configuração devem ser configurados individualmente e, em seguida, adicionar objeto de configuração do tooan application gateway. Depois de criar o objeto de configuração hello, você usar Olá `Set-AzureApplicationGateway` comando toocommit Olá configuração toohello criado anteriormente o recurso do application gateway.

> [!NOTE]
> Antes de atribuir um objeto de configuração do valor tooeach, é necessário toodeclare que tipo de objeto PowerShell usa para armazenamento. itens individuais do Hello primeira linha toocreate Olá define quais `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` são usados.

#### <a name="step-1"></a>Etapa 1

Crie todos os itens de configuração individuais.

Crie IP de front-end hello, conforme mostrado no exemplo a seguir de saudação.

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

Crie a porta de front-end Olá conforme mostrado no exemplo a seguir de saudação.

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

Crie pool de saudação do servidor de back-end.

Defina Olá endereços IP que são adicionados o pool de servidores de back-end do toohello conforme mostrado no exemplo a seguir hello.

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

Use Olá $server tooadd Olá valores toohello pool de back-end de objeto ($pool).

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

Crie a configuração de pool do servidor back-end de saudação.

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

Crie um ouvinte de saudação.

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

Crie regra de saudação.

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a>Etapa 2

Atribua todas as configuração individual itens tooan aplicativo gateway configuração objeto ($appgwconfig).

Adicione configuração de toohello IP de front-end hello.

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

Adicione configuração de toohello de porta de front-end de saudação.

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
Adicione configuração de toohello do pool de servidor back-end de saudação.

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

Adicione toohello configuração de pool de back-end do hello.

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

Adicione configuração de toohello Olá ouvinte.

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

Adicione configuração da regra de saudação toohello.

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a>Etapa 3
Confirme o recurso de gateway de aplicativo hello configuração objeto toohello usando `Set-AzureApplicationGatewayConfig`.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a>Gateway de saudação inicial

Uma vez configurado o gateway hello, use Olá `Start-AzureApplicationGateway` gateway de saudação do cmdlet toostart. A cobrança por um application gateway iniciado após a saudação gateway foi iniciado com êxito.

> [!NOTE]
> Olá `Start-AzureApplicationGateway` cmdlet pode levar até toofinish too15 a 20 minutos.

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Verificar status do gateway Olá

Saudação de uso `Get-AzureApplicationGateway` status de saudação do cmdlet toocheck do gateway de saudação. Se `Start-AzureApplicationGateway` com êxito na etapa anterior de saudação, *estado* devem estar em execução, e *Vip* e *DnsName* devem ter entradas válidas.

Olá, exemplo a seguir mostra um application gateway é para cima, em execução, e tootake pronto tráfego destinado a `http://<generated-dns-name>.cloudapp.net`.

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
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a>Excluir o hello application gateway

gateway de aplicativo hello toodelete:

1. Saudação de uso `Stop-AzureApplicationGateway` gateway de saudação do cmdlet toostop.
2. Saudação de uso `Remove-AzureApplicationGateway` gateway de saudação do cmdlet tooremove.
3. Verificar gateway Olá foi removido usando Olá `Get-AzureApplicationGateway` cmdlet.

Olá, exemplo a seguir mostra Olá `Stop-AzureApplicationGateway` cmdlet na primeira linha de saudação, seguido pela saída de hello.

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Depois que o gateway de aplicativo hello está em um estado parado, use Olá `Remove-AzureApplicationGateway` serviço de saudação do cmdlet tooremove.

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

tooverify que Olá serviço foi removido, você pode usar o hello `Get-AzureApplicationGateway` cmdlet. Essa etapa não é necessária.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a>Próximas etapas

Se você quiser tooconfigure descarregamento de SSL, consulte [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl.md).

Se você quiser tooconfigure um toouse de gateway do aplicativo com um balanceador de carga interno, consulte [criar um gateway de aplicativo com um balanceador de carga interno (ILB)](application-gateway-ilb.md).

Se deseja obter mais informações sobre as opções de balanceamento de carga no geral, consulte:

* [Balanceador de carga do Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gerenciador de Tráfego do Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
