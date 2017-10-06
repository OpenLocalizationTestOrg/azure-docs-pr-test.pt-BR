---
title: "aaaCreate clássico de PowerShell uma investigação personalizada - Gateway de aplicativo do Azure - | Microsoft Docs"
description: "Saiba como toocreate um personalizado teste para o Application Gateway usando o PowerShell no modelo de implantação clássico Olá"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a>Criar uma investigação personalizada para o Gateway de Aplicativo (clássico) pelo uso do PowerShell

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-probe-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

Neste artigo, você deve adicionar um gateway de aplicativo existente do investigação personalizada tooan com o PowerShell. Testes personalizados são úteis para aplicativos que têm uma página de verificação de integridade específicas ou para aplicativos que não fornecem uma resposta bem-sucedida no aplicativo de web saudação padrão.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](application-gateway-create-probe-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a>Criar um Gateway de Aplicativo

toocreate um application gateway:

1. Criar um recurso de gateway de aplicativo.
2. Crie um arquivo XML de configuração ou um objeto de configuração.
3. Confirme Olá configuração toohello recém-criados em recursos de gateway do aplicativo.

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a>Criar um recurso de gateway de aplicativo com uma investigação personalizada

gateway toocreate Olá Olá use `New-AzureApplicationGateway` cmdlet, substituindo os valores hello com seus próprios. Cobrança para o gateway de saudação não funciona neste momento. A cobrança começa em uma etapa posterior, quando o gateway Olá foi iniciado com êxito.

Olá exemplo a seguir cria um application gateway usando uma rede virtual chamada "testvnet1" e uma sub-rede denominada "subnet-1".

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate que Olá gateway foi criado, você pode usar o hello `Get-AzureApplicationGateway` cmdlet.

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> Olá valor padrão para *InstanceCount* é 2, com um valor máximo de 10. Olá valor padrão para *GatewaySize* é médio. Você pode escolher entre Small, Medium e Large.
> 
> 

*VirtualIPs* e *DnsName* são mostrados como em branco porque o gateway Olá ainda não foi iniciado. Esses valores são criados depois que o gateway de hello está em estado de execução de saudação.

### <a name="configure-an-application-gateway-by-using-xml"></a>Configurar um Application Gateway usando XML

Em Olá exemplo a seguir, use um tooconfigure do arquivo XML todas as configurações de gateway do aplicativo e confirmá-las toohello recursos de gateway de aplicativo.  

Saudação de cópia tooNotepad de texto a seguir.

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Edite valores de saudação entre parênteses Olá Olá para itens de configuração. Salve o arquivo de saudação com extensão. XML.

Olá exemplo a seguir mostra como toouse um tooset do arquivo de configuração o tooload de gateway do aplicativo hello equilibrar o tráfego HTTP na porta pública 80 e enviar tráfego de rede a porta 80 tooback ponta entre dois endereços IP por meio de uma investigação personalizada.

> [!IMPORTANT]
> item de protocolo Hello Http ou Https diferencia maiusculas de minúsculas.

Um novo item de configuração \<investigação\> é adicionado investigações de tooconfigure personalizado.

parâmetros de configuração de saudação são:

|Parâmetro|Descrição|
|---|---|
|**Nome** |Nome de referência da investigação personalizada. |
* **Protocolo** | Protocolo usado (os valores possíveis são HTTP ou HTTPS).|
| **Host** e **Path** | Caminho completo do URL que é invocado com a integridade de Olá Olá aplicativos gateway toodetermine da instância de saudação. Por exemplo, se você tiver http://contoso.com/ um site, e a investigação personalizada Olá pode ser configurada para "http://contoso.com/path/custompath.htm" para teste verifica toohave uma resposta HTTP bem-sucedida.|
| **Intervalo** | Configura as verificações de intervalo de investigação de saudação em segundos.|
| **Tempo limite** | Define o tempo limite de investigação de saudação para uma verificação de resposta HTTP.|
| **UnhealthyThreshold** | Olá o número de respostas HTTP com falha necessário tooflag Olá back-end a instância como *Íntegro*.|

nome do teste Olá é referenciado em Olá \<BackendHttpSettings\> tooassign configuração qual pool de back-end usa configurações de investigação personalizada.

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a>Adicionar um gateway de aplicativo investigação personalizada tooan existente

Alteração da configuração atual Olá de um gateway de aplicativo requer três etapas: obter o arquivo de configuração XML atual hello, modificar toohave uma investigação personalizada e configurar o gateway de aplicativo hello com novas configurações de XML hello.

1. Obter o arquivo XML de saudação usando `Get-AzureApplicationGatewayConfig`. Esse cmdlet exporta Olá configuração XML toobe modificado tooadd uma configuração de teste.

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. Abra o arquivo XML de saudação em um editor de texto. Adicione uma seção `<probe>` após `<frontendport>`.

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  Na seção de backendHttpSettings de saudação da saudação XML, adicione o nome de investigação de saudação conforme mostrado no exemplo a seguir de saudação:

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  Salve o arquivo XML de saudação.

1. Configuração do gateway atualização Olá aplicativo com o novo arquivo XML hello usando `Set-AzureApplicationGatewayConfig`. Esse cmdlet atualiza seu gateway de aplicativo com a nova configuração de saudação.

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a>Próximas etapas

Se você quiser tooconfigure descarregamento de SSL Secure Sockets Layer (), consulte [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl.md).

Se você quiser tooconfigure um toouse de gateway do aplicativo com um balanceador de carga interno, consulte [criar um gateway de aplicativo com um balanceador de carga interno (ILB)](application-gateway-ilb.md).

