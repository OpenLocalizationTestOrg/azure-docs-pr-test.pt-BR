---
title: aaaAzure CLI exemplos | Microsoft Docs
description: Exemplos de CLI do Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/08/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 776c947e6daca564242fc77b0527dcb124fa057d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-linux-virtual-machines"></a>Amostras da CLI do Azure para máquinas virtuais Linux

Olá, tabela a seguir inclui scripts de toobash links criados usando Olá CLI do Azure.

| | |
|---|---|
|**Criar máquinas virtuais**||
| [Criar uma máquina virtual](./../scripts/virtual-machines-linux-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | Cria uma máquina virtual Linux com configuração mínima. |
| [Criar uma máquina virtual totalmente configurada](./../scripts/virtual-machines-linux-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Cria um grupo de recursos, a máquina virtual e todos os recursos relacionados.|
| [Criar máquinas virtuais altamente disponíveis](./../scripts/virtual-machines-linux-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | Cria várias máquinas virtuais em uma configuração altamente disponíveis e de balanceamento de carga. |
| [Criar uma máquina virtual com o Docker habilitado](./../scripts/virtual-machines-linux-cli-sample-create-docker-host.md?toc=%2fcli%2fazure%2ftoc.json) | Cria uma máquina virtual, configura essa VM como um host Docker e executa um contêiner NGINX. |
| [Criar uma máquina virtual e executar o script de configuração](./../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md?toc=%2fcli%2fazure%2ftoc.json) | Cria uma máquina virtual e usa hello Azure personalizado Script extensão tooinstall NGINX. |
| [Criar uma máquina virtual com WordPress instalado](./../scripts/virtual-machines-linux-cli-sample-create-vm-wordpress.md?toc=%2fcli%2fazure%2ftoc.json) | Cria uma máquina virtual e usa hello Azure personalizado Script extensão tooinstall WordPress. |
| [Criar VM por meio de um disco do sistema operacional gerenciado](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json) | Cria uma máquina virtual anexando um disco gerenciado existente como disco do sistema operacional. |
| [Criar uma VM de um instantâneo](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | Cria uma máquina virtual de um instantâneo criando primeiro um disco gerenciado de instantâneo e, em seguida, anexar o novo disco gerenciado hello como o disco do sistema operacional. |
|**Gerenciar armazenamento**||
| [Criar um disco gerenciado com base em um VHD](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json) | Cria um disco gerenciado com base em um VHD especializado como um disco do sistema operacional ou com base em um VHD de dados como um disco de dados.  |
| [Criar um disco gerenciado com base em um instantâneo](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | Cria um disco gerenciado com base em um instantâneo. |
| [Copiar toosame de disco gerenciado ou assinatura diferente](../scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Cópias gerenciadas disco toosame ou assinatura diferente, mas em Olá mesmo região pai Olá gerenciados em disco. 
| [Exportar um instantâneo como conta de armazenamento do VHD tooa](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-storage-account.md?toc=%2fcli%2fmodule%2ftoc.json) | Exporta um instantâneo gerenciado como conta de armazenamento tooa VHD em uma região diferente. |
| [Copiar toosame de instantâneo ou assinatura diferente](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Cópias snapshot toosame ou assinatura diferente mas Olá mesmo região como um instantâneo do hello pai. |
|**Máquinas virtuais de rede**||
| [Proteger o tráfego de rede entre as máquinas virtuais](./../scripts/virtual-machines-linux-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | Cria duas máquinas virtuais, todos os recursos relacionados e grupos de segurança de rede (NSG) internos e externos. |
|**Proteger máquinas virtuais**||
| [Criptografar uma VM e discos de dados](./../scripts/virtual-machines-linux-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Cria um Azure Key Vault, uma chave de criptografia e entidade de serviço e, em seguida, criptografa uma VM. |
|**Monitorar máquinas virtuais**||
| [Monitorar uma VM com o Operations Management Suite](./../scripts/virtual-machines-linux-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | Cria uma máquina virtual, instala o agente do Operations Management Suite hello e registra Olá VM em um espaço de trabalho do OMS.  |
|**Solucionar problemas de máquinas virtuais**||
| [Solucionar problemas de um disco de sistema operacional de VMs](./../scripts/virtual-machines-linux-cli-sample-mount-os-disk.md?toc=%2fcli%2fazure%2ftoc.json) | Monta o disco do sistema operacional de saudação de uma máquina virtual como um disco de dados em uma segunda máquina virtual. |
| | |
