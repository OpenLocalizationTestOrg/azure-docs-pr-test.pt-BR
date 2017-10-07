---
title: 'Como tooconfigure roteamento para um circuito de rota expressa do Azure: CLI | Microsoft Docs'
description: "Este artigo ajuda você a criar e provisionar Olá privado, público e emparelhamento da Microsoft de um circuito de rota expressa. Este artigo também mostra como status de saudação toocheck, atualizar ou excluir emparelhamentos para o seu circuito."
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a>Criar e modificar o roteamento de um circuito da ExpressRoute usando CLI

Este artigo ajuda você a criar e gerenciar a configuração de roteamento para um circuito de rota expressa no modelo de implantação do Gerenciador de recursos do hello usando a CLI. Você também pode verificar status hello, update ou delete e desprovisionar emparelhamentos de um circuito de rota expressa. Se você quiser toouse toowork um método diferente com o circuito, selecione um artigo de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [CLI do Azure](howto-routing-cli.md)
> * [Vídeo – Emparelhamento privado](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Vídeo – Emparelhamento público](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Vídeo – Emparelhamento da Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Pré-requisitos de configuração

* Antes de começar, instale a versão mais recente Olá de comandos CLI hello (2.0 ou posteriores). Para obter informações sobre como instalar os comandos CLI hello, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).
* Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxo de trabalho](expressroute-workflows.md) páginas antes de começar a configuração.
* Você deve ter um circuito do ExpressRoute ativo. Siga as instruções de saudação muito[criar um circuito de rota expressa](howto-circuit-cli.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar. Olá circuito de rota expressa deve estar no estado habilitado e configurado para você comandos de saudação capaz de toorun toobe neste artigo.

Essas instruções se aplicam somente a toocircuits criado com provedores de serviço oferece serviços de conectividade de camada 2. Se você estiver usando um provedor de serviços que ofereça serviços gerenciados de Camada 3 (normalmente um IPVPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.

Você pode configurar um, dois ou todos os três emparelhamentos (privado e público do Azure e da Microsoft) para um circuito da ExpressRoute. Você pode configurar emparelhamentos em qualquer ordem escolhida. No entanto, você deve garantir que você conclua a configuração de saudação de cada um emparelhamento de cada vez.

## <a name="azure-private-peering"></a>Emparelhamento privado do Azure

Esta seção ajuda você a criar, obter, atualizar e excluir Olá configuração emparelhamento particular do Azure para um circuito de rota expressa.

### <a name="toocreate-azure-private-peering"></a>toocreate emparelhamento particular do Azure

1. Instale a versão mais recente de saudação do CLI do Azure. Você deve usar a versão mais recente de saudação do hello Azure Interface de linha de comando (CLI). * hello revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.

  ```azurecli
  az login
  ```

  Selecionar assinatura Olá deseja toocreate circuito de rota expressa

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Criar um circuito do ExpressRoute. Siga Olá instruções toocreate um [circuito de rota expressa](howto-circuit-cli.md) e fornecidos pelo provedor de conectividade de saudação.

  Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você. Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello. No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, continue a configuração usando as próximas etapas hello.
3. Verifique toomake de circuito de rota expressa de saudação se ele está configurado e também está habilitado. Use Olá exemplo a seguir:

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configure o emparelhamento particular do Azure para o circuito de saudação. Certifique-se de que você tenha Olá itens a seguir antes de prosseguir com as próximas etapas hello:

  * Um /30 sub-rede para o link primário hello. subrede Olá não deve fazer parte de qualquer espaço de endereço reservado para redes virtuais.
  * Um /30 sub-rede para o link secundário hello. subrede Olá não deve fazer parte de qualquer espaço de endereço reservado para redes virtuais.
  * Um tooestablish de ID de VLAN válida esse emparelhamento. Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.
  * Número de AS para emparelhamento. Você pode usar um número de AS de 2 e de 4 bytes. Você pode usar um número de AS privado para esse emparelhamento. Não use 65515.
  * **Opcional -** um hash MD5 se você escolher toouse um.

  Use hello Azure privado de emparelhamento para o circuito de tooconfigure de exemplo a seguir:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  Se você escolher toouse um hash MD5, use Olá exemplo a seguir:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a>tooview privado emparelhamento detalhes do Azure

Você pode obter os detalhes de configuração usando Olá exemplo a seguir:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

saudação de saída é similar toohello exemplo a seguir:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuração emparelhamento particular do Azure

Você pode atualizar qualquer parte da configuração de saudação usando Olá exemplo a seguir. Neste exemplo, Olá VLAN ID de circuito hello está sendo atualizado do too500 100.

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a>toodelete emparelhamento particular do Azure

Você pode remover a configuração do emparelhamento executando Olá exemplo a seguir:

> [!WARNING]
> Certifique-se de que todas as redes virtuais são desvinculadas do hello circuito de rota expressa antes de executar este exemplo. 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a>Emparelhamento público do Azure

Esta seção ajuda você a criar, obter, atualizar e excluir Olá a configuração de emparelhamento pública do Azure para um circuito de rota expressa.

### <a name="toocreate-azure-public-peering"></a>toocreate emparelhamento público do Azure

1. Instale a versão mais recente de saudação do CLI do Azure. Você deve usar a versão mais recente de saudação do hello Azure Interface de linha de comando (CLI). * hello revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.

  ```azurecli
  az login
  ```

  Selecione a assinatura de saudação do qual você deseja que o circuito de rota expressa toocreate.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Criar um circuito do ExpressRoute.  Siga Olá instruções toocreate um [circuito de rota expressa](howto-circuit-cli.md) e fornecidos pelo provedor de conectividade de saudação.

  Caso seu provedor de conectividade ofereça serviços gerenciados de Camada 3, você pode solicitar a ele a habilitação do emparelhamento privado do Azure. Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello. No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, continue a configuração usando as próximas etapas hello.
3. Verifique tooensure de circuito de rota expressa Olá provisionado e também está habilitado. Use Olá exemplo a seguir:

  ```azurecli
  az network express-route list
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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configure o emparelhamento público do Azure para o circuito de saudação. Certifique-se de que você tenha Olá informações a seguir antes de você continuar.

  * Um /30 sub-rede para o link primário hello. Precisa ser um prefixo IPv4 público válido.
  * Um /30 sub-rede para o link secundário hello. Precisa ser um prefixo IPv4 público válido.
  * Um tooestablish de ID de VLAN válida esse emparelhamento. Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.
  * Número de AS para emparelhamento. Você pode usar um número de AS de 2 e de 4 bytes.
  * **Opcional -** um hash MD5 se você escolher toouse um.

  Execute hello Azure público de emparelhamento para o circuito de tooconfigure de exemplo a seguir:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  Se você escolher toouse um hash MD5, use Olá exemplo a seguir:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.

### <a name="tooview-azure-public-peering-details"></a>tooview público emparelhamento detalhes do Azure

Você pode obter os detalhes de configuração usando Olá exemplo a seguir:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

saudação de saída é similar toohello exemplo a seguir:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuração de emparelhamento pública do Azure

Você pode atualizar qualquer parte da configuração de saudação usando Olá exemplo a seguir. Neste exemplo, Olá VLAN ID de circuito hello está sendo atualizado do too600 200.

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a>toodelete emparelhamento público do Azure

Você pode remover a configuração do emparelhamento executando Olá exemplo a seguir:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a>Emparelhamento da Microsoft

Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento Microsoft hello por um circuito de rota expressa.

> [!IMPORTANT]
> Emparelhamento da Microsoft de circuitos ExpressRoute que foram configurados anterior tooAugust 1, 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft hello, mesmo se os filtros de roteamento não estão definidos. Emparelhamento da Microsoft de circuitos de rota expressa configurados em ou após 1 de agosto de 2017 não terá quaisquer prefixos anunciados até que um filtro de rota é anexado toohello circuito. Para obter mais informações, consulte [Configurar um filtro de rota para o emparelhamento da Microsoft](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate emparelhamento da Microsoft

1. Instale a versão mais recente de saudação do CLI do Azure. Versão mais recente de saudação de uso do hello Azure Interface de linha de comando (CLI). * hello revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.

  ```azurecli
  az login
  ```

  Selecione a assinatura de saudação do qual você deseja que o circuito de rota expressa toocreate.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Criar um circuito do ExpressRoute. Siga Olá instruções toocreate um [circuito de rota expressa](howto-circuit-cli.md) e fornecidos pelo provedor de conectividade de saudação.

  Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você. Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello. No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, continue a configuração usando as próximas etapas hello.

3. Verifique toomake de circuito de rota expressa de saudação se ele está configurado e também está habilitado. Use Olá exemplo a seguir:

  ```azurecli
  az network express-route list
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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configure o emparelhamento do circuito de saudação do Microsoft. Certifique-se de que você tenha Olá seguintes informações antes de continuar.

  * Um /30 sub-rede para o link primário hello. Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.
  * Um /30 sub-rede para o link secundário hello. Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.
  * Um tooestablish de ID de VLAN válida esse emparelhamento. Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.
  * Número de AS para emparelhamento. Você pode usar um número de AS de 2 e de 4 bytes.
  * Anunciado prefixos: você deve fornecer uma lista de todos os prefixos planejar tooadvertise sobre a sessão BGP de saudação. Somente prefixos de endereços IP públicos são aceitos. Se você planejar toosend um conjunto de prefixos, você pode enviar uma lista separada por vírgulas. Esses prefixos devem ser registrado tooyou em um RIR / IRR.
  * **Opcional -** cliente ASN: se você estiver prefixos de anúncios que não são registrado toohello emparelhamento como número, você pode especificar hello como número toowhich, eles são registrados.
  * Nome de roteamento do registro: Você pode especificar Olá RIR / IRR no qual hello como número e prefixos estão registrados.
  * **Opcional -** um hash MD5 se você escolher toouse um.

   Execute Olá exemplo tooconfigure emparelhamento da Microsoft para o circuito a seguir:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a>tooget detalhes de emparelhamento da Microsoft

Você pode obter os detalhes de configuração usando Olá exemplo a seguir:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

saudação de saída é similar toohello exemplo a seguir:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate configuração de emparelhamento da Microsoft

Você pode atualizar qualquer parte da configuração de saudação. Olá anunciado prefixos de circuito Olá estão sendo atualizados no too124.1.0.0/24 123.1.0.0/24 em Olá exemplo a seguir:

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a>toodelete emparelhamento da Microsoft

Você pode remover a configuração do emparelhamento executando Olá exemplo a seguir:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a>Próximas etapas

Próxima etapa, [vincular um circuito de rota expressa do tooan de VNet](howto-linkvnet-cli.md).

* Para saber mais sobre fluxos de trabalho do ExpressRoute, confira [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).
* Para obter mais informações sobre o emparelhamento de circuito, veja [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).
* Para saber mais sobre redes virtuais, confira [Visão geral da rede virtual](../virtual-network/virtual-networks-overview.md).