---
title: "uma máquina virtual no portal do Azure de saudação do aaaCreate | Microsoft Docs"
description: "Crie uma máquina virtual Windows no hello portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a>Criar uma máquina virtual executando o Windows hello portal do Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](tutorial.md)
> * [PowerShell: Implantação clássica](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Saiba como muito[executar essas etapas usando o modelo de implantação do Gerenciador de recursos de saudação](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) usando Olá **portal do Azure**.

Este tutorial mostra como toocreate um Azure máquina virtual (VM) executando o Windows hello portal do Azure. Vamos usar uma imagem do Windows Server como um exemplo, mas isso é apenas uma de saudação muitas imagens ofertas do Azure. Observe que as opções de imagem dependem de sua assinatura. Por exemplo, imagens de área de trabalho do Windows podem ser assinantes tooMSDN disponíveis.

Esta seção mostra como Olá toouse **painel** em Olá tooselect portal do Azure e, em seguida, criar máquina virtual de saudação.

Também é possível criar VMs usando [suas próprias imagens](createupload-vhd.md). toolearn sobre este e outros métodos, consulte [toocreate de diferentes maneiras uma máquina virtual Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <a id="createvirtualmachine"></a>Criar máquina virtual de saudação
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[criar uma VM usando o modelo de implantação do Gerenciador de recursos de saudação](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) em Olá portal do Azure.
* Faça logon na máquina virtual de toohello. Para obter instruções, consulte [fazer logon na máquina virtual de tooa executando o Windows Server](connect-logon.md).
* Anexe um toostore de dados do disco. Você pode anexar tanto discos vazios como discos que contenham dados. Para obter instruções, consulte Olá [anexar dados disco tooa máquina virtual do Windows criada com o modelo de implantação clássico Olá](attach-disk.md).
