---
title: "Modificar um circuito ExpressRoute: PowerShell: Azure clássico | Microsoft Docs"
description: "Este artigo orienta você pelas etapas para verificar o status, atualização ou delete e desprovisionar o circuito de modelo de implantação clássico de ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/08/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 457bb74fa15d31fecbf668038ac880cafb8a897d
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="modify-an-expressroute-circuit-using-powershell-classic"></a>Modificar um circuito da ExpressRoute usando o PowerShell (clássico)

> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [CLI do Azure](howto-circuit-cli.md)
> * [Vídeo – Portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-circuit-classic.md)
>

Este artigo também mostra a você como verificar o status, atualizar ou excluir e desprovisionar um circuito da ExpressRoute.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Sobre modelos de implantação do Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a>Antes de começar

Instale as últimas versões do módulo de Gerenciamento de Serviço do Azure (SM) PowerShell Siga as instruções em [Introdução aos cmdlets do Azure PowerShell](/powershell/azure/overview) para obter orientações passo a passo sobre como configurar o computador para usar os módulos do Azure PowerShell.

## <a name="get-the-status-of-a-circuit"></a>Obter o status de um circuito

Você pode recuperar essas informações a qualquer momento usando o cmdlet `Get-AzureCircuit` . Fazer a chamada sem parâmetros listará todos os circuitos.

```powershell
Get-AzureDedicatedCircuit

Bandwidth                        : 200
CircuitName                      : MyTestCircuit
Location                         : Silicon Valley
ServiceKey                       : *********************************
ServiceProviderName              : equinix
ServiceProviderProvisioningState : Provisioned
Sku                              : Standard
Status                           : Enabled

Bandwidth                        : 1000
CircuitName                      : MyAsiaCircuit
Location                         : Singapore
ServiceKey                       : #################################
ServiceProviderName              : equinix
ServiceProviderProvisioningState : Provisioned
Sku                              : Standard
Status                           : Enabled
```

Você pode obter informações sobre um circuito do ExpressRoute específico passando a chave do serviço como um parâmetro para a chamada.

```powershell
Get-AzureDedicatedCircuit -ServiceKey "*********************************"

Bandwidth                        : 200
CircuitName                      : MyTestCircuit
Location                         : Silicon Valley
ServiceKey                       : *********************************
ServiceProviderName              : equinix
ServiceProviderProvisioningState : Provisioned
Sku                              : Standard
Status                           : Enabled
```

Você pode obter descrições detalhadas de todos os parâmetros executando o seguinte exemplo:

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify-a-circuit"></a>Modificar um circuito

Você pode modificar certas propriedades de um circuito do ExpressRoute sem afetar a conectividade.

É possível executar as seguintes tarefas sem tempo de inatividade:

* Como habilitar ou desabilitar o complemento premium do ExpressRoute para seu circuito do ExpressRoute.
* Aumente a largura de banda do circuito de ExpressRoute, desde que haja capacidade disponível na porta. Não há suporte para o downgrade da largura de banda de um circuito. 
* Altere o plano de medição de Dados Limitados para Dados Ilimitados. Não há suporte para alteração do plano de medição de Dados Ilimitados para Dados Limitados.
* Você pode habilitar e desabilitar *Permitir Operações Clássicas*.

Confira as [Perguntas frequentes sobre o ExpressRoute](expressroute-faqs.md) para saber mais sobre limites e limitações.

### <a name="enable-the-expressroute-premium-add-on"></a>Para habilitar o complemento premium do ExpressRoute

Você pode habilitar o complemento premium do ExpressRoute para o circuito existente usando o seguinte cmdlet do PowerShell:

```powershell
Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

Bandwidth                        : 1000
CircuitName                      : TestCircuit
Location                         : Silicon Valley
ServiceKey                       : *********************************
ServiceProviderName              : equinix
ServiceProviderProvisioningState : Provisioned
Sku                              : Premium
Status                           : Enabled
```

O seu circuito agora tem os recursos do complemento premium do ExpressRoute habilitados. Assim que o comando for executado com êxito, a cobrança pela funcionalidade do complemento Premium começará.

### <a name="disable-the-expressroute-premium-add-on"></a>Desabilitar o complemento premium do ExpressRoute

> [!IMPORTANT]
> Esta operação poderá falhar se você estiver usando recursos que ultrapassem o que é permitido para o circuito padrão.
> 
> 

#### <a name="considerations"></a>Considerações

* Verifique se o número de redes virtuais vinculadas ao circuito é menor do que 10 antes de fazer o downgrade de Premium para padrão. Se você não fizer isso, sua solicitação de atualização falhará e você será cobrado conforme as tarifas premium.
* Você precisa desvincular todas as redes virtuais em outras regiões geopolíticas. Se você não fizer isso, sua solicitação de atualização falhará e você será cobrado conforme as tarifas premium.
* Sua tabela de roteamento deve ter menos de 4.000 rotas para o emparelhamento privado. Se o tamanho da tabela de roteamento for maior que 4.000 rotas, a sessão BGP será descartada e não poderá ser reabilitada até que o número de prefixos anunciados fique abaixo de 4.000.

#### <a name="to-disable-the-premium-add-on"></a>Desabilitar o complemento premium

Você pode desabilitar o complemento premium do ExpressRoute para o circuito existente usando o seguinte cmdlet do PowerShell:

```powershell

Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

Bandwidth                        : 1000
CircuitName                      : TestCircuit
Location                         : Silicon Valley
ServiceKey                       : *********************************
ServiceProviderName              : equinix
ServiceProviderProvisioningState : Provisioned
Sku                              : Standard
Status                           : Enabled
```

### <a name="update-the-expressroute-circuit-bandwidth"></a>Atualizar a largura de banda do circuito do ExpressRoute

Confira as [Perguntas frequentes sobre o ExpressRoute](expressroute-faqs.md) para obter opções de largura de banda com suporte para seu provedor. Você pode escolher um tamanho maior do que o tamanho do circuito existente, desde que a porta física (na qual o circuito foi criado) permita.

> [!IMPORTANT]
> Talvez seja necessário recriar o circuito de ExpressRoute se não houver capacidade adequada na porta existente. Você não pode atualizar o circuito não se houver capacidade adicional disponível nesse local.
>
> Não é possível reduzir a largura de banda de um circuito do ExpressRoute sem interrupções. O downgrade da largura de banda exige o desprovisionamento do circuito do ExpressRoute e um reprovisionamento de um novo circuito do ExpressRoute.
> 
> 

#### <a name="resize-a-circuit"></a>Redimensionar um circuito

Após decidir de qual tamanho precisa, você pode usar o seguinte comando para redimensionar o circuito:

```powershell
Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

Bandwidth                        : 1000
CircuitName                      : TestCircuit
Location                         : Silicon Valley
ServiceKey                       : *********************************
ServiceProviderName              : equinix
ServiceProviderProvisioningState : Provisioned
Sku                              : Standard
Status                           : Enabled
```

Uma vez que o seu circuito está escalado ao lado Microsoft, contate seu provedor de conectividade para que faça a atualização das configurações no lado dele de modo a corresponder a essa alteração. Observe que passaremos a lhe cobrar pela opção de largura de banda atualizada a partir desse momento.

Se você vir o seguinte erro quando aumentar a largura de banda do circuito, isso significa que não há largura de banda suficiente restante na porta física onde o circuito existente foi criado. Será necessário excluir este circuito e criar um novo circuito do tamanho que você precisa.

```powershell
Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available to perform this circuit
update operation
At line:1 char:1
+ Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
  + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand
```

## <a name="deprovision-and-delete-a-circuit"></a>Desprovisionar e excluir um circuito

### <a name="considerations"></a>Considerações

* Você deve desvincular todas as redes virtuais do circuto do ExpressRoute para que a operação seja bem-sucedida. Se essa operação falhar, verifique se você tem redes virtuais vinculadas ao circuito.
* Se o estado de provisionamento do provedor de serviço de circuito de ExpressRoute for **Provisionando** ou **Provisionado**, você deverá trabalhar com seu provedor de serviços para que ele desprovisione o circuito. Continuaremos a reservar recursos e a cobrar de você até que o provedor de serviços complete o desprovisionamento do circuito e nos notifique.
* Se o provedor de serviços tiver desprovisionado o circuito (o estado de provisionamento do provedor de serviços estiver definido como **Não provisionado**), exclua o circuito. Isso interrompe a cobrança pelo circuito.

#### <a name="delete-a-circuit"></a>Excluir um circuito

Você pode excluir o circuito do ExpressRoute executando o comando a seguir:

```powershell
Remove-AzureDedicatedCircuit -ServiceKey "*********************************"
```