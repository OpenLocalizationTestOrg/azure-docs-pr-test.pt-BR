---
title: "aaaManage suas máquinas virtuais usando o PowerShell do Azure | Microsoft Docs"
description: "Saiba mais sobre comandos que você pode usar tarefas tooautomate no gerenciamento de suas máquinas virtuais."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a>Gerenciar suas máquinas virtuais usando o Azure PowerShell
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Para comandos comuns do PowerShell usando o modelo do Gerenciador de recursos de hello, consulte [aqui](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Muitas tarefas que você executa a cada dia toomanage suas VMs podem ser automatizadas usando cmdlets do PowerShell do Azure. Este artigo fornece comandos de exemplo para as tarefas mais simples e tooarticles links que mostram comandos Olá para tarefas mais complexas.

> [!NOTE]
> Se você ainda não tiver instalado e configurado o Azure PowerShell, você pode obter as instruções no artigo Olá [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
> 
> 

## <a name="how-toouse-hello-example-commands"></a>Como toouse Olá comandos de exemplo
Você precisará tooreplace parte do texto de saudação em Olá comandos com o texto que é apropriado para seu ambiente. Olá < e > símbolos indicam texto necessário tooreplace. Quando você substituir o texto de saudação, remover Olá símbolos, mas deixe Olá aspas no lugar.

## <a name="get-a-vm"></a>Obter uma VM
Essa é uma tarefa básica que você usará com frequência. Usá-lo tooget informações sobre uma VM, executar tarefas em uma máquina virtual ou obter saída toostore em uma variável.

tooget informações sobre Olá VM, execute este comando, substituindo tudo entre aspas hello, incluindo hello < e > caracteres:

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

Olá toostore de saída em uma variável $vm, execute:

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a>Faça logon no tooa VM baseado no Windows
Execute estes comandos:

> [!NOTE]
> Você pode obter a máquina virtual de saudação e o nome do serviço de nuvem da exibição de saudação do hello **Get-AzureVM** comando.
> 
> $svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< unidade e a pasta toostore de local Olá baixado arquivo RDP, exemplo: c:\temp >" $localFile = $localPath + "\" + $vmname +". rdp"Get-AzureRemoteDesktopFile - ServiceName $svcName-nome $vmName - LocalPath $localFile-iniciar
> 
> 

## <a name="stop-a-vm"></a>Parar uma VM
Execute este comando:

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> Use este Olá tookeep de parâmetro IP virtual (VIP) da nuvem de saudação do serviço caso ele esteja Olá última VM no serviço em nuvem. <br><br> Se você usar o parâmetro de StayProvisioned hello, você ainda será cobrado por Olá VM.
> 
> 

## <a name="start-a-vm"></a>Iniciar uma VM
Execute este comando:

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a>Anexar um disco de dados
Essa tarefa requer algumas etapas. Primeiro, você pode usar hello * Add-AzureDataDisk * cmdlet tooadd Olá toohello $vm objeto de disco. Em seguida, você use **Update-AzureVM** configuração de saudação do cmdlet tooupdate de saudação VM.

Você também precisará toodecide se tooattach um novo disco ou uma que contém dados. Para um novo disco, o comando de saudação cria o arquivo. vhd de saudação e anexa-o.

tooattach um novo disco, execute este comando:

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

tooattach um disco de dados existente, execute este comando:

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

tooattach discos de dados de um arquivo. vhd existente no armazenamento de blob, execute este comando:

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a>Criar uma VM baseada no Windows
toocreate uma nova máquina de virtual baseado no Windows no Azure, use as instruções de saudação no [toocreate de usar o Azure PowerShell e pré-configurar máquinas virtuais baseadas em Windows](create-powershell.md). Este tópico apresenta etapas você na criação de saudação de um comando set que do PowerShell do Azure cria uma VM com base em Windows que pode ser pré-configurados:

* Com associação de domínio do Active Directory.
* Com discos adicionais.
* Como membro de um conjunto de balanceamento de carga existente.
* Com um endereço IP estático.

