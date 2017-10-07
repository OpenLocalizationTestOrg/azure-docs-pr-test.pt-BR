---
title: "Redefinir um tooreestablish de gateway de VPN do Azure túneis IPsec | Microsoft Docs"
description: "Este artigo o orienta por meio da redefinição os túneis do IPsec de tooreestablish Gateway de VPN do Azure. artigo Olá aplica gateways tooVPN Olá clássico e modelos de implantação do Gerenciador de recursos de saudação."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a>Redefinir um Gateway de VPN

Redefinir um gateway de VPN do Azure é útil se você perde a conectividade VPN entre locais em um ou mais túneis de VPN site a site. Nessa situação, os seus dispositivos VPN local são todos funcionando corretamente, mas são tooestablish não é possível túneis IPsec com gateways de VPN do Azure hello. Este artigo ajuda-o a redefinir o gateway de VPN.

### <a name="what-happens-during-a-reset"></a>O que acontece durante uma redefinição?

Um gateway de VPN é composto de duas instâncias de VM em execução em uma configuração de modo em espera ativo. Quando você redefinir o gateway hello, ela reinicia gateway Olá, e, em seguida, Olá reaplica entre locais tooit configurações. gateway Olá mantém o endereço IP público Olá já possui. Isso significa que você não precisará configuração do roteador tooupdate Olá VPN com um novo endereço IP público para o gateway de VPN do Azure.

Quando você emitir o gateway de Olá Olá comando tooreset, instância ativa atual de saudação do gateway de VPN do Azure Olá é reinicializada imediatamente. Haverá uma breve interrupção durante o failover de saudação do hello instância ativa (que está sendo reinicializado), instância de toohello em espera. intervalo de saudação deve ser menor que um minuto.

Se a conexão de saudação não é restaurado após a primeira reinicialização do hello, problema Olá mesmo comando novamente tooreboot instância VM segundo hello (Olá novo active gateway). Se duas reinicializações de saudação tooback back solicitada, haverá um pouco maior período em que as duas instâncias VM (ativas e em espera) estão sendo reinicializadas. Isso fará com que um intervalo mais conectividade VPN hello, backup too2 too4 minutos para reinicializações de saudação toocomplete VMs.

Depois de duas reinicializações, se você ainda tiver problemas de conectividade entre locais, abra uma solicitação de suporte de saudação portal do Azure.

## <a name="before"></a>Antes de começar

Antes de redefinir o gateway, verifique se itens importantes Olá listados abaixo para cada túnel VPN IPsec Site a Site (S2S). Qualquer incompatibilidade nos itens Olá resulta em Desconectar Olá de túneis de VPN S2S. Verificar e corrigir configurações de saudação para seu local e gateways de VPN do Azure evita que você reinicializações desnecessárias e interrupções de Olá outras conexões de trabalho em gateways de saudação.

Verifique se Olá itens a seguir antes de redefinir o gateway:

* Olá IP Internet endereços (VIPs) para o gateway de VPN do Azure ambos hello e Olá gateway VPN estão configurados corretamente em ambas as políticas hello Azure e hello local VPN ao local.
* chave pré-compartilhada Olá deve ser Olá mesmo em gateways VPN do Azure e no local.
* Se você aplicar configuração do IPsec/IKE específica, como criptografia, algoritmos de hash e PFS (sigilo), certifique-se de ambos hello Azure e gateways de VPN local têm Olá mesmas configurações.

## <a name="portal"></a>Portal do Azure

Você pode redefinir um gateway de VPN do Gerenciador de recursos usando Olá portal do Azure. Se você quiser tooreset um gateway clássico, consulte Olá [PowerShell](#resetclassic) etapas.

### <a name="resource-manager-deployment-model"></a>Modelo de implantação do Gerenciador de Recursos

1. Olá abrir [portal do Azure](https://portal.azure.com) e navegue gateway de rede virtual do Gerenciador de recursos do toohello que você deseja tooreset.
2. Na folha de saudação para gateway de rede virtual Olá, clique em 'Redefinir'.

  ![Folha Redefinir Gateway de VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. Na saudação redefinir folha, clique em Olá **redefinir** botão.

## <a name="ps"></a>PowerShell

### <a name="resource-manager-deployment-model"></a>Modelo de implantação do Gerenciador de Recursos

Olá cmdlet para redefinir um gateway é **AzureRmVirtualNetworkGateway redefinição**. Antes de executar uma redefinição, verifique se você tem a versão mais recente de saudação do hello [cmdlets do PowerShell do Gerenciador de recursos](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0). Olá, exemplo a seguir redefine um gateway de rede virtual denominado VNet1GW no grupo de recursos de TestRG1 hello:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

Resultado:

Quando você receber um resultado de retorno, você pode presumir Olá redefinição de gateway foi bem-sucedida. No entanto, há nada no resultado de retorno de saudação que indica explicitamente que redefinem Olá foi bem-sucedida. Se você quiser toolook perto na Olá histórico toosee exatamente quando redefinir gateway Olá ocorreu, você pode exibir essas informações no hello [portal do Azure](https://portal.azure.com). No portal de hello, navegue até muito**'GatewayName' -> integridade do recurso**.

### <a name="resetclassic"></a> Modelo de implantação clássico

Olá cmdlet para redefinir um gateway é **Reset-AzureVNetGateway**. Antes de executar uma redefinição, verifique se você tem a versão mais recente de saudação do hello [cmdlets do PowerShell de gerenciamento de serviço (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0). Olá, exemplo a seguir redefine gateway Olá para uma rede virtual denominada "ContosoVNet":

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

Resultado:

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <a name="cli"></a>Azure CLI

gateway tooreset Olá Olá use [vnet-gateway de rede az redefinir](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) comando. Olá, exemplo a seguir redefine um gateway de rede virtual denominado VNet5GW no grupo de recursos de TestRG5 hello:

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

Resultado:

Quando você receber um resultado de retorno, você pode presumir Olá redefinição de gateway foi bem-sucedida. No entanto, há nada no resultado de retorno de saudação que indica explicitamente que redefinem Olá foi bem-sucedida. Se você quiser toolook perto na Olá histórico toosee exatamente quando redefinir gateway Olá ocorreu, você pode exibir essas informações no hello [portal do Azure](https://portal.azure.com). No portal de hello, navegue até muito**'GatewayName' -> integridade do recurso**.
