---
title: Criar uma VM no portal do Azure | Microsoft Docs
description: "Crie uma máquina virtual do Windows no Portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ROBOTS: NOINDEX
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 99a67821ab926983205e2327c428e854d20a0cf5
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="create-a-virtual-machine-running-windows-in-the-azure-portal"></a>Criar uma máquina virtual executando o Windows no portal do Azure
> [!div class="op_single_selector"]
> * [portal do Azure](tutorial.md)
> * [PowerShell: Implantação clássica](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda o uso do modelo de implantação Clássica. A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos. Saiba como [executar estas etapas usando o modelo de implantação do Resource Manager](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) no **portal do Azure**.
> [!INCLUDE [virtual-machines-common-classic-createportal](../../../../includes/virtual-machines-classic-portal.md)]

Este tutorial mostra como criar uma VM (máquina virtual) do Azure executando Windows no portal do Azure. Vamos usar uma imagem do Windows Server como exemplo, mas ela é apenas uma das muitas imagens que o Azure oferece. Observe que as opções de imagem dependem de sua assinatura. Por exemplo, imagens da área de trabalho do Windows podem estar disponíveis para assinantes do MSDN.

Esta seção mostra como usar o **Painel** no portal do Azure para selecionar e criar a máquina virtual.

Também é possível criar VMs usando [suas próprias imagens](createupload-vhd.md). Para saber mais sobre esse e outros métodos, consulte [Diferentes maneiras de criar uma máquina virtual do Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a id="createvirtualmachine"> </a>Criar a máquina virtual
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a>Próximas etapas
* Saiba como [criar uma VM usando o modelo de implantação do Resource Manager](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) no portal do Azure.
* Faça logon na máquina virtual. Para obter instruções, veja [Fazer logon em uma máquina virtual que executa o Windows Server](connect-logon.md).
* Anexe um disco para armazenar dados. Você pode anexar tanto discos vazios como discos que contenham dados. Para obter instruções, veja [Anexar um disco de dados a uma máquina virtual do Windows criada com o modelo de implantação clássico](attach-disk.md).
