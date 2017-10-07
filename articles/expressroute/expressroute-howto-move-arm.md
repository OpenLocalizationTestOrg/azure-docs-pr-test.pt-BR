---
title: "Mover circuitos ExpressRoute de tooResource clássico Manager: PowerShell: Azure | Microsoft Docs"
description: "Esta página descreve como toomove toohello um circuito clássico Gerenciador de recursos de implantação de modelo usando o PowerShell."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a>Mover circuitos ExpressRoute de modelo de implantação do hello clássico toohello Gerenciador de recursos usando o PowerShell

toouse um circuito de rota expressa para Olá clássico e modelos de implantação do Gerenciador de recursos, você deve mover o modelo de implantação do hello circuito toohello Gerenciador de recursos. Olá seções a seguir ajudarão-lo a mover seu circuito usando o PowerShell.

## <a name="before-you-begin"></a>Antes de começar

* Verifique se você tem a versão mais recente Olá dos módulos do PowerShell do Azure hello (pelo menos versão 1.0). Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
* Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.
* Revise as informações de saudação que são fornecidas em [movendo um circuito de rota expressa de tooResource clássico Manager](expressroute-move.md). Certifique-se de que você compreenda plenamente Olá limites e as limitações.
* Verifique se o circuito de saudação é totalmente operacional no modelo de implantação clássico hello.
* Certifique-se de que você tenha um grupo de recursos que foi criado no modelo de implantação do Gerenciador de recursos de saudação.

## <a name="move-an-expressroute-circuit"></a>Mover um circuito de ExpressRoute

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a>Etapa 1: Coletar detalhes de circuito de modelo de implantação clássico Olá

Entrar toohello ambiente clássico do Azure e obter chave de saudação do serviço.

1. Entre tooyour conta do Azure.

  ```powershell
  Add-AzureAccount
  ```

2. Selecione Olá assinatura apropriada do Azure.

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. Importe os módulos do PowerShell Olá para o Azure e rota expressa.

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. Use o cmdlet do hello abaixo chaves de serviço tooget Olá para todos os seus circuitos de rota expressa. Depois de recuperar chaves hello, copie Olá **chave de serviço** do circuito Olá que você deseja que o modelo de implantação do toomove toohello Gerenciador de recursos.

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a>Etapa 2: Entrar e criar um grupo de recursos

Entrar no ambiente do Gerenciador de recursos de toohello e crie um novo grupo de recursos.

1. Entrar no ambiente do Azure Resource Manager tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

2. Selecione Olá assinatura apropriada do Azure.

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. Modificar trecho Olá abaixo toocreate um novo grupo de recursos se você ainda não tiver um grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a>Etapa 3: Mover o modelo de implantação do hello rota expressa circuito toohello Gerenciador de recursos

Você é agora pronto toomove o circuito de rota expressa do modelo de implantação do hello implantação clássica modelo toohello Gerenciador de recursos. Antes de continuar, examine informações de saudação fornecidas no [mover um circuito de rota expressa do modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](expressroute-move.md).

toomove o seu circuito, modifique e execute Olá trecho de código a seguir:

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> Após mover hello, Olá novo nome está listado no cmdlet anterior Olá será usado tooaddress Olá recursos. circuito Olá essencialmente será renomeado.
> 

## <a name="modify-circuit-access"></a>Modificar o acesso de circuito

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a>tooenable acesso de circuito de rota expressa para ambos os modelos de implantação

Depois de mover o clássico modelo de implantação de rota expressa circuito toohello Gerenciador de recursos, você pode habilitar modelos de implantação do acesso tooboth. Execute Olá modelos de implantação cmdlets tooenable acesso tooboth a seguir:

1. Obter detalhes de circuito hello.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. Definir tooTRUE "Permitir operações clássico".

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. Atualize o circuito de saudação. Depois que a operação seja concluída com êxito, você será tooview capaz de circuito de saudação no modelo de implantação clássico hello.

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. Execute Olá cmdlet tooget Olá detalhes de saudação circuito de rota expressa a seguir. Você deve ser capaz de toosee chave de serviço de Olá listado.

  ```powershell
  get-azurededicatedcircuit
  ```

5. Agora você pode gerenciar o circuito de rota expressa toohello links usando comandos de modelo de implantação clássico Olá para VNets clássico e comandos do Gerenciador de recursos de saudação para VNets do Gerenciador de recursos. Olá artigos a seguir ajudam a gerenciar links toohello circuito de rota expressa:

    * [Vincular seu circuito de rota expressa no modelo de implantação do Gerenciador de recursos de saudação de tooyour de rede virtual](expressroute-howto-linkvnet-arm.md)
    * [Vincular sua rede virtual de tooyour circuito de rota expressa no modelo de implantação clássico Olá](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a>modelo de implantação clássico toohello do acesso de circuito de rota expressa toodisable

Execute Olá modelo de implantação clássico cmdlets toodisable acesso toohello a seguir.

1. Obter os detalhes de saudação circuito de rota expressa.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. Definir tooFALSE "Permitir operações clássico".

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. Atualize o circuito de saudação. Depois que a operação seja concluída com êxito, não será capaz de tooview circuito de Olá no modelo de implantação clássico hello.

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a>Próximas etapas

* [Criar e modificar o roteamento do circuito do ExpressRoute](expressroute-howto-routing-arm.md)
* [Vincular sua rede virtual de tooyour circuito de rota expressa](expressroute-howto-linkvnet-arm.md)
