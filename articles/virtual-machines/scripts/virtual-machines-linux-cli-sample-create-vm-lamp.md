---
title: "aaaAzure exemplo de Script CLI - implantar Olá pilha LAMP em um conjunto de escala de Load-Balanced monitoramente Machin | Microsoft Docs"
description: "Use uma saudação de toodeploy de extensão do script personalizado pilha LAMP em uma carga = escala de VM com balanceamento definido no Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>Implantar a pilha de LÂMPADA Olá em um conjunto de escala de VM com balanceamento de carga

Este exemplo cria um conjunto de escala de máquinas virtuais e aplica uma extensão que executa uma pilha de LÂMPADA do script personalizado toodeploy Olá em cada máquina virtual no conjunto de escala de saudação.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a>Connect

Use este toosee código como tooconnect tooyour VMs e a escala definidas.

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, conjunto de escala hello e VMs e todos os recursos relacionados a seguir.

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos toocreate um grupo de recursos, máquina virtual, o conjunto de disponibilidade, balanceador de carga e todos os recursos relacionados a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az vmss create](https://docs.microsoft.com/cli/azure/vmss#create) | Criar um conjunto de dimensionamento de máquinas virtuais |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Adicionar um ponto de extremidade com balanceamento de carga |
| [az vmss extension set](https://docs.microsoft.com/cli/azure/vmss/extension#set) | Criar extensão Olá que executa o script personalizado Olá na implantação de uma VM |
| [az vmss update-instances](https://docs.microsoft.com/cli/azure/vmss#update-instances) | Executar script personalizado Olá em instâncias de VM Olá que foram implantadas antes da aplicação extensão Olá toohello conjunto de escala. |
| [az vmss scale](https://docs.microsoft.com/cli/azure/vmss#scale) | Escala verticalmente escala Olá definir, adicionando mais instâncias VM. script personalizado Olá é executado sobre estas configurações quando eles são implantados. |
| [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) | Obter endereços IP de saudação do hello VMs criadas pelo exemplo hello. |
| [az network lb show](https://docs.microsoft.com/cli/azure/network/lb#show) | Obtenha o back-end e front-end Olá portas usadas pelo Balanceador de carga de saudação. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
