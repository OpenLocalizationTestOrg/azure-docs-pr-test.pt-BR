---
title: aaaAzure exemplo de Script do PowerShell - criar uma VM do Windows | Microsoft Docs
description: "Amostra de script do Azure PowerShell – Criar uma VM Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 81f04ed88a968cb7ac540b0b4b874dcf230a8e1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a>Criar uma máquina virtual totalmente configurada com o PowerShell

Esse script cria uma Máquina Virtual do Azure que executa o Windows Server 2016. Depois de executar o script hello, você pode acessar a máquina virtual de saudação por RDP.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.ps1 "Create VM detailed")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá implantação de saudação toocreate comandos a seguir. Cada item na tabela de saudação vincula a documentação específica do toocommand.

| Command | Observações |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Cria uma configuração de sub-rede. Essa configuração é usada com o processo de criação de rede virtual hello. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Cria uma rede virtual. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Cria um endereço IP público. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Cria uma configuração de regra de grupo de segurança de rede. Essa configuração é usada toocreate uma regra NSG quando Olá NSG é criado. |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Cria um grupo de segurança de rede. |
| [Get-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | Obtém informações de sub-rede. Essas informações são usadas ao criar um adaptador de rede. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Cria um adaptador de rede. |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Cria uma configuração de VM. Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas. Olá configuração será usada durante a criação da VM. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Crie uma máquina virtual. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Remove um grupo de recursos e todos os recursos contidos nele. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
