---
title: "Exemplos do PowerShell de máquina Virtual de aaaAzure | Microsoft Docs"
description: "Amostras do PowerShell de máquina virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 89fd26aa979687cdcdf9ae4e60be7d0d2eaeae91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a>Amostras do PowerShell de máquina virtual do Azure

Olá, tabela a seguir inclui exemplos de scripts de tooPowerShell links que criar e gerenciar máquinas virtuais do Windows.

| | |
|---|---|
|**Criar máquinas virtuais**||
| [Criar uma máquina virtual totalmente configurada](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Cria um grupo de recursos, a máquina virtual e todos os recursos relacionados.|
| [Criar máquinas virtuais altamente disponíveis](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Cria várias máquinas virtuais em uma configuração altamente disponíveis e de balanceamento de carga.|
| [Criar uma máquina virtual e executar o script de configuração](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Cria uma máquina virtual e usa hello Azure personalizado Script extensão tooinstall IIS. |
| [Criar uma máquina virtual e executar a configuração da DSC](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Cria uma máquina virtual e usa tooinstall de extensão de configuração de estado desejado (DSC) da Azure Olá IIS. |
| [Carregar um VHD e criar VMs](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | Uplaods um VHD local tooAzure de arquivos, cria e imagem de VHD de saudação e, em seguida, cria uma VM da imagem. |
| [Criar VM por meio de um disco do sistema operacional gerenciado](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Cria uma máquina virtual anexando um disco gerenciado existente como disco do sistema operacional. |
| [Criar uma VM de um instantâneo](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Cria uma máquina virtual de um instantâneo criando primeiro um disco gerenciado de instantâneo e, em seguida, anexar o novo disco gerenciado hello como o disco do sistema operacional. |
|**Gerenciar armazenamento**||
| [Criar um disco gerenciado de um VHD na mesma assinatura ou em uma diferente](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Cria um disco gerenciado com base em um VHD especializado como um disco do sistema operacional ou com base em um VHD de dados como um disco de dados na mesma assinatura ou em uma diferente.  |
| [Criar um disco gerenciado com base em um instantâneo](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Cria um disco gerenciado com base em um instantâneo. |
| [Copiar toosame de disco gerenciado ou assinatura diferente](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Cópias gerenciadas disco toosame ou assinatura diferente, mas em Olá mesmo região pai Olá gerenciados em disco. 
| [Exportar um instantâneo como conta de armazenamento do VHD tooa](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Exporta um instantâneo gerenciado como conta de armazenamento tooa VHD em uma região diferente. |
| [Criar um instantâneo de um VHD](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Cria instantâneo de um VHD toocreate vários discos gerenciados idênticos de instantâneo em curto período de tempo.  |
| [Copiar toosame de instantâneo ou assinatura diferente](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Cópias snapshot toosame ou assinatura diferente mas Olá mesmo região como um instantâneo do hello pai. |
|**Proteger máquinas virtuais**||
| [Criptografar uma VM e discos de dados](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | Cria um Azure Key Vault, uma chave de criptografia e entidade de serviço e, em seguida, criptografa uma VM. |
|**Monitorar máquinas virtuais**||
| [Monitorar uma VM com o Operations Management Suite](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Cria uma máquina virtual, instala o agente do Operations Management Suite hello e registra Olá VM em um espaço de trabalho do OMS.  |
| | |

