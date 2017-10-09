---
title: maneiras de aaaDifferent toocreate uma VM do Windows Azure | Microsoft Docs
description: "Lista maneiras diferentes de saudação toocreate uma máquina virtual com o Gerenciador de recursos do Windows."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a>Diferentes maneiras toocreate uma máquina virtual do Windows

O Azure oferece toocreate de diferentes maneiras uma máquina virtual porque as máquinas virtuais são adequadas para fins e usuários diferentes. Isso significa que você precise toomake algumas opções sobre a máquina virtual de saudação e como toocreate-lo. Este artigo fornece um resumo dessas opções e links tooinstructions.

## <a name="azure-portal"></a>Portal do Azure
Usar o portal do Azure de saudação é tootry uma maneira simples-out de uma máquina virtual, especialmente se você estiver começando com o Azure. 

[Criar uma máquina virtual que executa o Windows usando o portal de saudação](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a>Modelo
As máquinas virtuais exigem uma combinação de recursos (como conjuntos de disponibilidade e contas de armazenamento). Em vez de implantar e gerenciar cada recurso separadamente, você pode criar um modelo de Gerenciador de recursos do Azure que implanta e provisiona todos os recursos de saudação em uma única operação coordenado.

* [Criar uma máquina virtual do Windows com um modelo do Gerenciador de Recursos](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a>Azure PowerShell
Se preferir trabalhar em um shell de comando, será possível usar o Azure PowerShell.

* [Criar uma VM do Windows usando o PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a>Visual Studio
Usar toobuild do Visual Studio, gerenciar, implantar VMs com hello Azure Tools para Visual Studio e Olá SDK do Azure.

[Ferramentas do Azure para Visual Studio](https://www.visualstudio.com/features/azure-tools-vs)

