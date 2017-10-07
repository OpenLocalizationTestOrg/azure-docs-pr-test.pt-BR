---
title: aaaCreate uma rede virtual - 2.0 do CLI do Azure | Microsoft Docs
description: "Saiba como toocreate usando uma rede virtual Olá 2.0 do CLI do Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a>Criar uma rede virtual usando Olá 2.0 do CLI do Azure

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

O Azure tem dois modelos de implantação: Azure Resource Manager e clássico. A Microsoft recomenda a criação de recursos por meio do modelo de implantação do Gerenciador de recursos de saudação. mais sobre toolearn Olá diferenças entre modelos de saudação dois ler Olá [modelos de implantação do Azure entender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](virtual-networks-create-vnet-cli-nodejs.md) – nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de Olá
- [2.0 do CLI do Azure](#create-a-virtual-network) -nossa próxima geração CLI para modelo de implantação de gerenciamento de recursos de saudação (Este artigo)'
 
    Você também pode criar uma rede virtual por meio de Gerenciador de recursos usando outras ferramentas ou criar uma rede virtual por meio do modelo de implantação clássico Olá selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [Modelo](virtual-networks-create-vnet-arm-template-click.md)
> * [Portal (clássico)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (Clássico)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [CLI (Clássica)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a>Criar uma rede virtual

toocreate usando uma rede virtual Olá 2.0 do CLI do Azure, Olá concluir as etapas a seguir:

1. Instalar e configurar hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).

2. Criar um grupo de recursos para sua VNet usando Olá [criar grupo az](/cli/azure/group#create) com hello `--name` e `--location` argumentos:

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. Crie uma VNet e uma sub-rede:

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    Saída esperada:
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    Parâmetros usados:

    - `--name TestVNet`: Nome da saudação VNet toobe criado.
    - `--resource-group TestRG`: # Olá recurso nome de grupo que controla o recurso de saudação. 
    - `--location centralus`: Olá local no qual toodeploy.
    - `--address-prefix 192.168.0.0/16`: Olá prefixo de endereço e o bloco.  
    - `--subnet-name FrontEnd`: nome de saudação da sub-rede de saudação.
    - `--subnet-prefix 192.168.1.0/24`: Olá prefixo de endereço e o bloco.

    toolist Olá informações básicas toouse em Olá próximo comando, você pode consultar Olá VNet usando um [filtro de consulta](/cli/azure/query-az-cli2):

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    Quais Olá produz saída a seguir:

        Where      Name      Group

        centralus  TestVNet  TestRG

4. Crie uma sub-rede:

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    Saída esperada:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    Parâmetros usados:

    - `--address-prefix 192.168.2.0/24`: bloco CIDR da sub-rede.
    - `--name BackEnd`: Nome da nova subrede hello.
    - `--resource-group TestRG`: o grupo de recursos hello.
    - `--vnet-name TestVNet`: nome de saudação do hello proprietária da rede virtual.

5. Propriedades de saudação de consulta de Olá nova rede virtual:

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    Saída esperada:

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. Propriedades de saudação de consulta de sub-redes hello:

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    Saída esperada:

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a>Próximas etapas

Saiba como tooconnect:

- Uma rede virtual de tooa de máquina virtual (VM) lendo Olá [criar uma VM do Linux](../virtual-machines/linux/quick-create-cli.md) artigo. Em vez de criar uma rede virtual e a sub-rede nas etapas de saudação de artigos hello, você pode selecionar uma rede virtual existente e a sub-rede tooconnect uma VM.
- Olá redes virtuais de tooother de rede virtual lendo Olá [VNets conectar](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artigo.
- Olá rede virtual tooan na rede local usando uma rede privada virtual (VPN) site a site ou um circuito de rota expressa. Saiba como lendo Olá [conectar uma rede de local de tooan de rede virtual usando uma VPN site a site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [vincular um circuito de rota expressa do tooan de VNet](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
