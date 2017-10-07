---
title: "exemplo de script CLI aaaAzure - o tráfego de rede VM de filtro | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Filtrar o tráfego de entrada e saída de rede da VM."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a>Filtrar o tráfego de entrada e saída de rede da VM

Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end. O tráfego de rede de entrada sub-rede front-end toohello tooHTTP limitado, HTTPS e SSH, enquanto a saída de tráfego toohello Internet de sub-rede de back-end de saudação não é permitida. Depois de executar o script hello, você terá uma máquina virtual com dois NICs. Cada NIC é conectado tooa outra sub-rede.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá toocreate comandos a seguir, um grupo de recursos, a rede virtual e grupos de segurança de rede. Cada comando na tabela Olá vincula a documentação específica do toocommand.

| Command | Observações |
|---|---|
| [az group create](/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az network vnet create](/cli/azure/network/vnet#create) | Cria uma rede virtual do Azure e uma sub-rede front-end. |
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | Cria uma sub-rede back-end. |
| [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) | Associa os NSGs toosubnets. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Cria um tooaccess endereço IP público Olá VM de saudação à Internet. |
| [az network nic create](/cli/azure/network/nic#create) | Cria as interfaces de rede virtual e os conecta sub-redes da rede virtual toohello de front-end e back-end. |
| [az network nsg create](/cli/azure/network/nsg#create) | Cria grupos de segurança de rede (NSG) que estão associados toohello sub-redes de front-end e back-end. |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) |Cria regras NSG que permitam ou bloqueiem as sub-redes de toospecific portas específicas. |
| [az vm create](/cli/azure/vm#create) | Cria máquinas virtuais e anexa um tooeach NIC VM. Esse comando também especifica Olá toouse de imagem de máquina virtual e as credenciais administrativas. |
| [az group delete](/cli/azure/group#delete) | Exclui um grupo de recursos e todos os seus recursos contidos nele. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](/cli/azure/overview).

Exemplos de script CLI rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../cli-samples.md)
