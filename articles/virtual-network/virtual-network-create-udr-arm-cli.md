---
title: "dispositivos de roteamento e virtual de aaaControl usando Olá 2.0 do CLI do Azure | Microsoft Docs"
description: "Saiba como dispositivos de roteamento e virtual de toocontrol usando Olá 2.0 do CLI do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a>Criar rotas definidas pelo usuário (UDR) usando Olá 2.0 do CLI do Azure

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [CLI do Azure](virtual-network-create-udr-arm-cli.md)
> * [Modelo](virtual-network-create-udr-arm-template.md)
> * [PowerShell (Implantação clássica)](virtual-network-create-udr-classic-ps.md)
> * [CLI (Implantação clássica)](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete 

Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir: 

- [1.0 de CLI do Azure](virtual-network-create-udr-arm-cli-nodejs.md) – nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de Olá 
- [2.0 do CLI do Azure](#Create-the-UDR-for-the-front-end-subnet) -nossa próxima geração CLI para modelo de implantação de gerenciamento de recursos de saudação (Este artigo)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

comandos de CLI do Azure de exemplo Hello abaixo esperam um ambiente simples já criado com base no cenário de saudação acima. Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste Olá implantando [este modelo](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), clique em **implantar tooAzure**, substitua os valores de parâmetro padrão Olá Se necessário e siga as instruções de saudação em Olá portal.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Criar hello UDR para sub-rede front-end Olá
tabela de rotas toocreate hello e rotas necessárias para a sub-rede de front-end de saudação com base no cenário de saudação acima, siga as etapas de saudação abaixo.

1. Criar uma tabela de rotas para sub-rede front-end Olá com hello [criar tabela de rotas de rede de az](/cli/azure/network/route-table#create) comando:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    Saída:

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. Crie uma rota que envia todo o tráfego destinado toohello sub-rede de back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) usando Olá [criar rota de tabela de rotas de rede az](/cli/azure/network/route-table/route#create) comando:

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    Saída:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    Parâmetros:

    * **--route-table-name**. Nome da tabela de rota Olá onde rota Olá será adicionada. Para nosso cenário, *UDR-FrontEnd*.
    * **--address-prefix**. Prefixo de endereço de sub-rede Olá onde os pacotes são destinados a. Para nosso cenário, *192.168.2.0/24*.
    * **--next-hop-type**. Tipo de objeto ao qual o tráfego será enviado. Os valores possíveis são *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.
    * **--next-hop-ip-address**. Endereço IP do próximo salto. Para o nosso cenário, *192.168.0.4*.

3. Executar Olá [atualização de sub-rede da rede virtual de rede az](/cli/azure/network/vnet/subnet#update) tabela de rotas do comando tooassociate Olá criado acima com hello **front-end** sub-rede:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    Saída:

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    Parâmetros:
    
    * **--vnet-name**. Nome de rede virtual onde está localizada a sub-rede de saudação do hello. Para o nosso cenário, *TestVNet*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Criar hello UDR para a sub-rede de back-end Olá

tabela de rotas de saudação toocreate e rotear necessários para a sub-rede de back-end de saudação com base no cenário de saudação acima, Olá concluir as etapas a seguir:

1. Execute Olá toocreate de comando a seguir uma tabela de rotas para sub-rede de back-end hello:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. Executar Olá após o comando toocreate uma rota no toosend de tabela de rota Olá todo o tráfego destinado toohello sub-rede front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. Execução hello após a tabela de rotas do comando tooassociate Olá com hello **back-end** sub-rede:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>Habilite o encaminhamento de IP em FW1

encaminhamento de IP tooenable em Olá NIC usada por **FW1**completa Olá seguintes etapas:

1. Executar Olá [Mostrar de nic de rede az](/cli/azure/network/nic#show) com uma saudação de toodisplay JMESPATH filtro atual **ativar encaminhamento ip** valor para **encaminhamento IP habilitar**. Ele deve ser definido muito*false*.

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    Saída:

        false

2. Execute Olá encaminhamento de IP de tooenable de comando a seguir:

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    Você pode examinar o console de toohello em fluxo de saída de hello ou apenas testar novamente para Olá específico **enableIpForwarding** valor:

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    Saída:

        true

    Parâmetros:

    **--ip-forwarding**: *true* ou *false*.

