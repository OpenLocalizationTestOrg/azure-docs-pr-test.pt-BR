---
title: "aaaCreate usando uma rede virtual Olá 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate usando uma rede virtual Olá 1.0 da CLI do Azure | Gerenciador de recursos."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a>Criar uma rede virtual usando Olá CLI do Azure

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

O Azure tem dois modelos de implantação: Azure Resource Manager e clássico. A Microsoft recomenda a criação de recursos por meio do modelo de implantação do Gerenciador de recursos de saudação. mais sobre toolearn Olá diferenças entre modelos de saudação dois ler Olá [modelos de implantação do Azure entender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [2.0 do CLI do Azure](virtual-networks-create-vnet-arm-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação
- [1.0 de CLI do Azure](#create-a-virtual-network) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>Criar uma rede virtual

toocreate usando uma rede virtual Olá CLI do Azure, Olá concluir as etapas a seguir:

1. Instalar e configurar Olá CLI do Azure por Olá seguir as etapas em Olá [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) artigo.

2. Crie uma VNet e uma sub-rede:

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    Saída esperada:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    Parâmetros usados:

   * **--vnet**. Nome da saudação VNet toobe criado. Para o nosso cenário, *TestVNet*
   * **-e (ou --address-space)**. Espaço de endereço da rede virtual. Para o nosso cenário, *192.168.0.0*
   * **-i (ou -cidr)**. Máscara de rede no formato CIDR. Para o nosso cenário, *16*.
   * **-n (ou --subnet-name**). Nome da sub-rede primeiro hello. Para o nosso cenário, *FrontEnd*.
   * **-p (ou --subnet-start-ip)**. Endereço IP inicial da sub-rede ou espaço de endereço da sub-rede. Em nosso cenário, *192.168.1.0*.
   * **-r (ou --subnet-cidr)**. Máscara de rede no formato CIDR para a sub-rede. Para o nosso cenário, *24*.
   * **-l (ou --location)**. Região do Azure onde Olá VNet é criada. Para o nosso cenário, *Central US*.

3. Crie uma sub-rede:

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    Saída esperada:

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    Parâmetros usados:

   * **-t (ou --vnet-name**. Nome da saudação redes onde sub-rede Olá será criado. Para o nosso cenário, *TestVNet*.
   * **-n (or --name)**. Nome da nova subrede hello. Para o nosso cenário, *BackEnd*.
   * **-a (ou --address-prefix)**. Bloco CIDR da sub-rede. Para o nosso cenário, *192.168.2.0/24*.
   
4. Propriedades de saudação tooview de Olá nova rede virtual:

    ```azurecli
    azure network vnet show
    ```
   
    Saída esperada:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a>Próximas etapas

Saiba como tooconnect:

- Uma rede virtual de tooa de máquina virtual (VM) lendo Olá [criar uma VM do Linux](../virtual-machines/linux/quick-create-cli.md) artigo. Em vez de criar uma rede virtual e a sub-rede nas etapas de saudação de artigos hello, você pode selecionar uma rede virtual existente e a sub-rede tooconnect uma VM.
- Olá redes virtuais de tooother de rede virtual lendo Olá [VNets conectar](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artigo.
- Olá rede virtual tooan na rede local usando uma rede privada virtual (VPN) site a site ou um circuito de rota expressa. Saiba como lendo Olá [conectar uma rede de local de tooan de rede virtual usando uma VPN site a site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [vincular um circuito de rota expressa do tooan de VNet](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
