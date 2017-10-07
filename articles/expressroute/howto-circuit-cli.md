---
title: 'Criar e modificar um circuito do Azure ExpressRoute: CLI | Microsoft Docs'
description: Este artigo descreve como toocreate, provisionar, verifique se, atualizar, excluir e cancelar o provisionamento de um circuito de rota expressa usando a CLI.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a>Criar e modificar um circuito do ExpressRoute usando a CLI


Este artigo descreve como toocreate um circuito de rota expressa do Azure usando Olá Interface de linha de comando (CLI). Este artigo também mostra como toocheck Olá status, atualizar, ou excluir e cancelar o provisionamento de um circuito. Se você quiser toouse toowork um método diferente com circuitos do ExpressRoute, você pode selecionar artigo Olá Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [CLI do Azure](howto-circuit-cli.md)
> * [Vídeo – Portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a>Antes de começar

* Antes de começar, instale a versão mais recente Olá de comandos CLI hello (2.0 ou posteriores). Para obter informações sobre como instalar os comandos CLI hello, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli) e [Introdução ao Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).
* Saudação de revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.

## <a name="create-and-provision-an-expressroute-circuit"></a>Criar e provisionar um circuito do ExpressRoute

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Entre no tooyour conta do Azure e selecione sua assinatura

toobegin sua configuração, entrar tooyour conta do Azure. Use Olá toohelp exemplos que você se conectar a seguir:

```azurecli
az login
```

Verificar as assinaturas de saudação para conta de saudação.

```azurecli
az account list
```

Selecione a assinatura de saudação do qual você deseja toocreate um circuito de rota expressa.

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Obter lista de saudação de provedores suportados, locais e larguras de banda

Antes de criar um circuito de rota expressa, você precisa de lista de saudação de provedores com suporte de conectividade, locais e as opções de largura de banda. Olá CLI comando 'az rota expressa lista-serviço-provedores de rede' retorna essas informações, que você usará em etapas posteriores:

```azurecli
az network express-route list-service-providers
```

resposta de saudação é semelhante toohello exemplo a seguir:

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

Verifique Olá resposta toosee se seu provedor de conectividade está listado. Anote Olá informações que você precisará criar um circuito a seguir:

* Nome
* PeeringLocations
* BandwidthsOffered

Agora você está pronto toocreate um circuito de rota expressa.

### <a name="3-create-an-expressroute-circuit"></a>3. Criar um circuito do ExpressRoute

> [!IMPORTANT]
> O circuito de rota expressa é cobrado do momento Olá que uma chave de serviço é emitida. Execute esta operação quando o provedor de conectividade de saudação circuito de saudação tooprovision pronto.
> 
> 

Se você ainda não tiver um grupo de recursos, deverá criar um antes de criar o circuito do ExpressRoute. Você pode criar um grupo de recursos executando Olá comando a seguir:

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

saudação de exemplo a seguir mostra como toocreate uma rota expressa de 200 Mbps de circuito por meio de Equinix no Vale do Silício. Se estiver usando um provedor diferente e configurações diferentes, substitua essas informações ao fazer a solicitação. 

Certifique-se de que você especifique a camada SKU correta hello e família SKU:

* A camada da SKU determina se um complemento padrão ou premium do ExpressRoute está habilitado. Você pode especificar 'Padrão' hello de tooget SKU standard ou 'Premium' para o complemento do premium Olá.
* A família SKU determina o tipo de cobrança de saudação. Você pode especificar 'Metereddata' para um plano de dados limitado e 'Unlimiteddata' para um plano de dados ilimitado. Você pode alterar o tipo de cobrança de saudação do ' Metereddata 'too'Unlimiteddata', mas você não pode alterar o tipo de saudação de 'Unlimiteddata' too'Metereddata'.


O circuito de rota expressa é cobrado do momento Olá que uma chave de serviço é emitida. saudação de exemplo a seguir é uma solicitação para uma nova chave de serviço:

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

resposta de Olá contém a chave de serviço de saudação.

### <a name="4-list-all-expressroute-circuits"></a>4. Listar todos os circuitos do ExpressRoute

tooget uma lista de todos os circuitos de rota expressa Olá que você criou, execute o comando a ''az rede rota expressa lista hello. Você pode recuperar essas informações a qualquer momento usando este comando. toolist todos os circuitos, verifique Olá chamada sem parâmetros.

```azurecli
az network express-route list
```

Sua chave de serviço está listada no hello *ServiceKey* campo de resposta de saudação.

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

Você pode obter descrições detalhadas de todos os parâmetros de saudação executando o comando hello usando Olá '-h' parâmetro.

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Enviar Olá tooyour chave conectividade provedor para provisionamento

'ServiceProviderProvisioningState' fornece informações sobre o estado atual de saudação do provisionamento no lado do provedor de serviços de saudação. status de Olá fornece estado Olá em Olá lado da Microsoft. Para obter mais informações, consulte Olá [artigo de fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states).

Quando você cria um novo circuito de rota expressa, circuito hello está em Olá estado a seguir:

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

Olá circuito alterações toohello estado a seguir quando o provedor de conectividade Olá está no processo de saudação de habilitá-la para você:

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

Para você toobe capaz de toouse um circuito de rota expressa, ele deve ser Olá estado a seguir:

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Verifique periodicamente o status de saudação e o estado de saudação da chave de circuito de saudação

Verificar o status de saudação e o estado de saudação da chave de circuito Olá permite que você saiba quando seu provedor habilitou o seu circuito. Depois que o circuito Olá tiver sido configurado, 'ServiceProviderProvisioningState' aparece como 'Provisionado', conforme mostrado no exemplo a seguir de saudação:

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

resposta de saudação é semelhante toohello exemplo a seguir:

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a>7. Criar sua configuração de roteamento

Para obter instruções passo a passo, consulte Olá [configuração de roteamento de circuito de rota expressa](howto-routing-cli.md) artigo toocreate e modificar os emparelhamentos de circuito.

> [!IMPORTANT]
> Essas instruções se aplicam somente a toocircuits que são criados com provedores de serviços que oferecem serviços da camada 2 de conectividade. Se você estiver usando um provedor de serviços que oferece serviços gerenciados de camada 3 (normalmente um IP VPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Vincular um circuito de rota expressa do tooan de rede virtual

Em seguida, vincule um circuito de rota expressa do tooyour de rede virtual. Saudação de uso [vinculação virtual redes circuitos tooExpressRoute](howto-linkvnet-cli.md) artigo.

## <a name="modify">
            </a>Modificar um circuito do ExpressRoute

Você pode modificar certas propriedades de um circuito do ExpressRoute sem afetar a conectividade. Você pode fazer as seguintes alterações sem tempo de inatividade de saudação:

* Você pode habilitar ou desabilitar o complemento ExpressRoute Premium para seu circuito do ExpressRoute.
* Você pode aumentar a largura de banda de saudação do circuito ExpressRoute desde que haja capacidade disponível na porta hello. No entanto, não há suporte para fazer o downgrade de largura de banda de saudação de um circuito. 
* Você pode alterar o plano de medição de saudação de dados limitados tooUnlimited dados. No entanto, a alteração Olá plano de dados ilimitado tooMetered não há suporte para dados de medição.
* Você pode habilitar e desabilitar *Permitir Operações Clássicas*.

Para obter mais informações sobre limitações e limites, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>complemento do premium tooenable Olá rota expressa

Você pode habilitar o complemento do premium Olá rota expressa para o circuito existente usando Olá comando a seguir:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

circuito Olá agora tem habilitados dos recursos de complemento de premium Olá rota expressa. Começamos a cobrança é para o recurso de complemento premium Olá assim que o comando Olá foi executado com êxito.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>complemento do premium toodisable Olá rota expressa

> [!IMPORTANT]
> Essa operação pode falhar se você estiver usando recursos que são maiores do que o que é permitido para o circuito de saudação padrão.
> 
> 

Antes de desabilitar o complemento do premium Olá rota expressa, compreenda Olá critérios a seguir:

* Antes de você fazer o downgrade de toostandard premium, você deve se certificar que você tem menos de 10 circuito toohello vinculado de redes virtuais. Se existirem mais de 10, sua solicitação de atualização falhará e você será cobrado de acordo com as tarifas Premium.
* Você precisa desvincular todas as redes virtuais em outras regiões geopolíticas. Se você não desvincular todas as redes virtuais, sua solicitação de atualização falhará e cobraremos de acordo com as tarifas premium.
* Sua tabela de roteamento deve ter menos de 4.000 rotas para o emparelhamento privado. Se o tamanho da tabela de rota for maior que 4.000 rotas, descarta a sessão BGP de saudação. sessão de saudação não ser habilitados novamente até que o número de saudação de prefixos anunciados está abaixo de 4.000.

Você pode desabilitar o complemento do premium Olá rota expressa para o circuito existente hello usando Olá exemplo a seguir:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>largura de banda de circuito ExpressRoute tooupdate Olá

Para opções de largura de banda Olá tem suportada para o seu provedor, verifique Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md). Você pode escolher qualquer tamanho maior do que o tamanho de saudação do circuito existente.

> [!IMPORTANT]
> Se não houver capacidade insuficiente na porta existente hello, você pode ter circuito de rota expressa toorecreate hello. Não é possível atualizar o circuito de saudação se não houver nenhuma capacidade adicional disponível nesse local.
>
> Você não pode reduzir a largura de banda de saudação de um circuito de rota expressa sem interrupções. Fazendo downgrade de largura de banda requer que você toodeprovision Olá circuito de rota expressa e, em seguida, Reprovisionar um novo circuito de rota expressa.
>

Depois de decidir tamanho Olá que é necessário usar o circuito de Olá tooresize de comando a seguir:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

O circuito será dimensionado para cima no lado do Microsoft hello. Em seguida, você deve entrar em contato com suas configurações de tooupdate do provedor de conectividade em seu toomatch lado essa alteração. Depois de fazer essa notificação, começamos a cobrança você para a opção de largura de banda Olá atualizado.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>Olá toomove SKU de toounlimited limitado

Você pode alterar Olá SKU de um circuito de rota expressa usando Olá exemplo a seguir:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>toocontrol clássico de toohello de acesso e ambientes do Gerenciador de recursos

Consulte as instruções de saudação em [circuitos ExpressRoute mover de modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](expressroute-howto-move-arm.md).

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Desprovisionamento e exclusão de um circuito do ExpressRoute

toodeprovision e excluir um circuito de rota expressa, certifique-se de entender Olá critérios a seguir:

* Você deve desvincular todas as redes virtuais da saudação circuito de rota expressa. Se essa operação falhar, verifique toosee se todas as redes virtuais são vinculados toohello circuito.
* Se o provedor de serviços de circuito ExpressRoute Olá estado de provisionamento é **provisionamento** ou **provisionado**, você deve trabalhar com o circuito de saudação do serviço provedor toodeprovision em seu lado. Vamos continuar tooreserve recursos e cobrar você até que o provedor de serviços Olá Complete desprovisionamento circuito de saudação e nos notifica.
* Você pode excluir o circuito de saudação se o provedor de serviços de saudação tem desprovisionada circuito hello. Quando um circuito desprovisionado, estado de provisionamento do provedor de serviços de saudação é definido muito**não provisionado**. Isso interrompe a cobrança para o circuito de saudação.

Você pode excluir o circuito de rota expressa executando Olá comando a seguir:

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Depois de criar o circuito, certifique-se de que você Olá seguintes tarefas:

* [Criar e modificar o roteamento do circuito do ExpressRoute](howto-routing-cli.md)
* [Vincular sua rede virtual de tooyour circuito de rota expressa](howto-linkvnet-cli.md)
