---
title: "aaaCommon PowerShell comandos para máquinas virtuais do Azure | Microsoft Docs"
description: "Tooget comum de comandos do PowerShell é iniciado criando e gerenciando suas VMs do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ba3839a2-f3d5-4e19-a5de-95bfb1c0e61e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 3de9bd4d20259ced2c0aa8ef7a3f7d9520a071d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-creating-and-managing-azure-virtual-machines"></a>Comandos comuns do PowerShell para criar e gerenciar Máquinas Virtuais do Azure

Este artigo aborda algumas das Olá que comandos do PowerShell do Azure que você pode usar toocreate e gerenciar máquinas virtuais em sua assinatura do Azure.  Para obter uma ajuda mais detalhada com opções específicas de linha de comando, você pode usar o *comando* **Get-Help**.

Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter informações sobre como instalar a versão mais recente de saudação do PowerShell do Azure, selecione sua assinatura e tooyour conta de assinatura.

Essas variáveis podem ser úteis para que você se executando mais de um dos comandos de saudação neste artigo:

- $location - local de saudação da máquina virtual de saudação. Você pode usar [Get-AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind um [região geográfica](https://azure.microsoft.com/regions/) que funciona para você.
- $myResourceGroup - nome Olá Olá do grupo de recursos que contém a máquina virtual de saudação.
- $myVM - nome de saudação da máquina virtual de saudação.

## <a name="create-a-vm"></a>Criar uma máquina virtual

| Tarefa | Get-Help |
| ---- | ------- |
| Criar uma configuração de VM |$vm = [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig) -VMName $myVM -VMSize "Standard_D1_v1"<BR></BR><BR></BR>configuração da VM Hello é usadas as configurações toodefine ou atualização para Olá VM. Olá configuração é inicializada com o nome de saudação do hello VM e seus [tamanho](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| Adicionar definições de configuração |$vm = [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) -VM $vm -Windows -ComputerName $myVM -Credential $cred -ProvisionVMAgent -EnableAutoUpdate<BR></BR><BR></BR>Configurações do sistema operacional incluindo [credenciais](https://technet.microsoft.com/library/hh849815.aspx) são adicionados toohello objeto de configuração que você criou anteriormente usando New-AzureRmVMConfig. |
| Adicionar uma interface de rede |$vm = [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/Add-AzureRmVMNetworkInterface) -VM $vm -Id $nic.Id<BR></BR><BR></BR>Uma máquina virtual deve ter um [interface de rede](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocommunicate em uma rede virtual. Você também pode usar [Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooretrieve um objeto de interface de rede existente. |
| Especificar uma imagem de plataforma |$vm = [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage) -VM $vm -PublisherName "publisher_name" -Offer "publisher_offer" -Skus "product_sku" -Version "latest"<BR></BR><BR></BR>[Informações da imagem](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) é adicionado toohello objeto de configuração que você criou anteriormente usando New-AzureRmVMConfig. objeto Olá retornado deste comando é usado somente quando você define Olá OS disco toouse uma imagem de plataforma. |
| Definir uma imagem de plataforma de toouse de disco do sistema operacional |$vm = [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk) -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/myOSDisk.vhd" -CreateOption FromImage<BR></BR><BR></BR>nome de saudação do disco do sistema operacional hello e sua localização no [armazenamento](../../storage/common/storage-powershell-guide-full.md) é adicionado toohello objeto de configuração que você criou anteriormente. |
| Definir uma imagem generalizada de toouse de disco do sistema operacional |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -SourceImageUri "https://mystore1.blob.core.windows.net/system/Microsoft.Compute/Images/myimages/myprefix-osDisk.{guid}.vhd" -VhdUri "https://mystore1.blob.core.windows.net/vhds/disk_name.vhd" -CreateOption FromImage -Windows<BR></BR><BR></BR>nome de saudação do disco do sistema operacional Olá, o local de Olá Olá imagem de origem e o local do disco Olá no [armazenamento](../../storage/common/storage-powershell-guide-full.md) é adicionado toohello objeto de configuração. |
| Definir uma imagem especializada de toouse de disco do sistema operacional |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/" -CreateOption Attach -Windows |
| Criar uma máquina virtual |[New-AzureRmVM]() -ResourceGroupName $myResourceGroup -Location $location -VM $vm<BR></BR><BR></BR>Todos os recursos são criados em um [grupo de recursos](../../azure-resource-manager/powershell-azure-resource-manager.md). Antes de executar esse comando, execute New-AzureRmVMConfig, Set-AzureRmVMOperatingSystem, Set-AzureRmVMSourceImage, Add-AzureRmVMNetworkInterface e Set-AzureRmVMOSDisk. |

## <a name="get-information-about-vms"></a>Obter informações sobre VMs

| Tarefa | Command |
| ---- | ------- |
| Listar VMs em uma assinatura |[Get-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvm) |
| Listar VMs em um grupo de recursos |Get-AzureRmVM -ResourceGroupName $myResourceGroup<BR></BR><BR></BR>uma lista de recursos de tooget grupos em sua assinatura, use [Get-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermresourcegroup). |
| Obter informações sobre uma VM |Get-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM |

## <a name="manage-vms"></a>Gerenciar VMs
| Tarefa | Command |
| --- | --- |
| Iniciar uma VM |[Start-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/start-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Parar uma VM |[Stop-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/stop-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Reiniciar uma VM em execução |[Restart-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/restart-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Excluir uma VM |[Remove-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Generalizar uma VM |[Set-AzureRmVm](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM -Generalized<BR></BR><BR></BR>Execute esse comando antes de executar Save-AzureRmVMImage. |
| Capturar uma VM |[Save-AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) -ResourceGroupName $myResourceGroup -VMName $myVM -DestinationContainerName "myImageContainer" -VHDNamePrefix "myImagePrefix" -Path "C:\filepath\filename.json"<BR></BR><BR></BR>Uma máquina virtual deve ser [preparado, desligue e generalizado](prepare-for-upload-vhd-image.md) toocreate toobe usada uma imagem. Antes de executar esse comando, execute Set-AzureRmVm. |
| Atualizar uma VM |[Update-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvm) -ResourceGroupName $myResourceGroup -VM $vm<BR></BR><BR></BR>Obter configuração de VM atual hello usando Get-AzureRmVM, altere as definições de configuração no objeto da VM Olá e, em seguida, execute este comando. |
| Adicionar um disco de dados tooa VM |[Add-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk) -VM $vm -Name "myDataDisk" -VhdUri "https://mystore1.blob.core.windows.net/vhds/myDataDisk.vhd" -LUN # -Caching ReadWrite -DiskSizeinGB # -CreateOption Empty<BR></BR><BR></BR>Use Get-AzureRmVM tooget Olá VM objeto. Especifique o número LUN de saudação e tamanho de saudação do disco de saudação. Execute atualização AzureRmVM tooapply Olá configuração alterações toohello VM. disco de saudação que você adicionar não foi inicializado. |
| Remover um disco de dados de uma VM |[Remove-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmdatadisk) -VM $vm -Name "myDataDisk"<BR></BR><BR></BR>Use Get-AzureRmVM tooget Olá VM objeto. Execute atualização AzureRmVM tooapply Olá configuração alterações toohello VM. |
| Adicionar uma extensão tooa VM |[Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) -ResourceGroupName $myResourceGroup -Location $location -VMName $myVM -Name "extensionName" -Publisher "publisherName" -Type "extensionType" -TypeHandlerVersion "#.#" -Settings $Settings -ProtectedSettings $ProtectedSettings<BR></BR><BR></BR>Execute este comando com hello apropriado [informações de configuração](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) para extensão Olá que você deseja tooinstall. |
| Remover uma extensão de VM |[Remove-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmextension) -ResourceGroupName $myResourceGroup -Name "extensionName" -VMName $myVM |

## <a name="next-steps"></a>Próximas etapas
* Consulte as etapas básicas para criar uma máquina virtual no hello [criar uma VM do Windows usando o Gerenciador de recursos e o PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

