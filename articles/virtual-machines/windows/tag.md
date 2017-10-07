---
title: "aaaHow tootag um recurso de máquina virtual do Windows no Azure | Microsoft Docs"
description: "Saiba mais sobre a marcação de uma máquina virtual do Windows criada no Azure usando o modelo de implantação do Gerenciador de recursos de saudação"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a>Como tootag uma máquina virtual do Windows no Azure
Este artigo descreve as diferentes maneiras tootag uma máquina virtual do Windows no Azure por meio do modelo de implantação do Gerenciador de recursos de saudação. As marcas são pares de chave/valor definidos pelo usuário que podem ser colocados diretamente em um recurso ou grupo de recursos. Azure atualmente oferece suporte a marcas de too15 por grupo de recursos e recursos. Marcas podem ser colocadas em um recurso no tempo de saudação da criação ou adicionado o recurso existente tooan. Observe que as marcas são suportadas para recursos criados por meio do modelo de implantação de Gerenciador de recursos de saudação apenas. Se você quiser tootag uma máquina virtual Linux, consulte [como tootag uma máquina virtual do Linux no Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a>Marcação com o PowerShell
toocreate, adicionar e excluir marcas por meio do PowerShell, é necessário primeiro tooset o seu [ambiente do PowerShell do Azure Resource Manager][PowerShell environment with Azure Resource Manager]. Depois de concluir a instalação hello, você pode colocar marcas de recursos de computação, rede e armazenamento no momento da criação ou após Olá recurso for criado por meio do PowerShell. Este artigo se concentra na exibição/edição de marcas colocadas nas Máquinas Virtuais.

Navega pela primeira vez, tooa Máquina Virtual por meio de saudação `Get-AzureRmVM` cmdlet.

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

Se sua máquina Virtual já contém marcas, você verá todas as marcas de saudação no recurso:

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

Se você desejar marcas tooadd por meio do PowerShell, você pode usar o hello `Set-AzureRmResource` comando. Observe que, ao atualizar marcas pelo PowerShell, as marcas são atualizadas como um todo. Portanto, se você estiver adicionando um recurso de tooa de marca que já tem marcas, será necessário tooinclude todas as marcas de saudação que você deseja toobe colocado no recurso de saudação. Abaixo está um exemplo de como tooadd adicional marcas tooa recursos por meio de Cmdlets do PowerShell.

Esse cmdlet primeiro define todas Olá marcas colocadas em *MyTestVM* toohello *$tags* variável, usando Olá `Get-AzureRmResource` e `Tags` propriedade.

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

Olá segundo comando exibe marcas Olá para Olá dado variável.

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

Olá terceiro comando adiciona uma marca adicionais toohello *$tags* variável. Observe o uso de saudação do hello  **+=**  tooappend Olá toohello de par chave/valor novo *$tags* lista.

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

comando quarto Olá define todas as marcas de saudação definidas na saudação de *$tags* toohello variável considerando os recursos. Nesse caso, é MyTestVM.

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

Olá quinto comando exibe todas as marcas de saudação no recurso de saudação. Como você pode ver, *local* agora está definido como uma marca com *MyLocation* como valor de saudação.

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

Saiba mais sobre toolearn marcação por meio do PowerShell, check-out Olá [Cmdlets de recursos do Azure][Azure Resource Cmdlets].

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Próximas etapas
* toolearn mais informações sobre a marcação de recursos do Azure, consulte [visão geral do Gerenciador de recursos do Azure] [ Azure Resource Manager Overview] e [tooorganize marcas usando os recursos do Azure] [ Using Tags tooorganize your Azure Resources].
* toosee como marcas podem ajudá-lo a gerenciar o uso de recursos do Azure, consulte [Noções básicas sobre sua conta do Azure] [ Understanding your Azure Bill] e [obter ideias sobre o consumo de recursos do Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
