---
title: "aaaResize uma VM do Windows no modelo de implantação clássico Olá - Azure | Microsoft Docs"
description: "Redimensione uma máquina virtual do Windows criada no modelo de implantação clássico hello, usando o Powershell do Azure."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a>Redimensionar uma VM do Windows criada no modelo de implantação clássico Olá
Este artigo mostra como tooresize uma VM do Windows criados no modelo de implantação clássico hello usando o Powershell do Azure.

Ao considerar Olá capacidade tooresize uma VM, há dois conceitos que controlam o intervalo de saudação da máquina virtual do tamanhos disponíveis tooresize hello. Olá primeiro conceito é região Olá sua VM é implantada. lista de saudação de tamanhos de VM disponíveis na região é na guia de serviços de saudação da página de web hello regiões do Azure. conceito segundo Olá é hardware físico de saudação hospedando sua VM. servidores físicos do Hello hospedando VMs são agrupados em clusters de hardware físico comum. método Hello de alterar o tamanho de uma VM é diferente dependendo se hello desejado novo tamanho da VM é suportado por cluster de hardware Olá hospedando Olá VM.

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Você também pode [redimensionar uma VM criada no modelo de implantação do Gerenciador de recursos de saudação](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="add-your-account"></a>Adicionar sua conta
Você deve configurar o Azure PowerShell toowork com clássicos recursos do Azure. Siga as próximas etapas, Olá recursos clássicos do toomanage tooconfigure PowerShell do Azure.

1. No prompt do PowerShell hello, digite `Add-AzureAccount` e clique em **Enter**. 
2. Digite hello endereço de email associado à sua assinatura do Azure e clique em **continuar**. 
3. Digite a senha Olá para sua conta. 
4. Clique em **Entrar**. 

## <a name="resize-in-hello-same-hardware-cluster"></a>Redimensionar em Olá mesmo cluster de hardware
tooresize um tamanho da VM tooa disponível no cluster de hardware Olá hospedagem Olá VM, execute Olá etapas a seguir.

1. Execute Olá Olá tamanhos de VM Olá toolist disponíveis no cluster de hardware Olá hospeda serviço de nuvem Olá que contém a VM de comando do PowerShell a seguir.
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. Execute Olá comandos tooresize Olá VM a seguir.
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a>Redimensionar em um novo cluster de hardware
tooresize um tamanho de tooa VM não está disponível no cluster de hardware Olá hospedando Olá VM, hello serviço de nuvem e todas as VMs no serviço de nuvem Olá devem ser recriadas. Cada serviço de nuvem é hospedado em um cluster de hardware única para que todas as VMs no serviço de nuvem Olá devem ser um tamanho que tenha suporte em um cluster de hardware. Olá etapas a seguir descrevem como tooresize uma VM excluindo e recriando, em seguida, Olá nuvem serviço.

1. Execute Olá PowerShell comando toolist Olá tamanhos de VM disponíveis na região Olá a seguir. 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. Anote todas as configurações para cada VM no serviço de nuvem Olá que contém a saudação VM toobe redimensionado. 
3. Exclua todas as VMs no serviço de nuvem Olá selecionar os discos de Olá Olá opção tooretain para cada VM.
4. Recrie Olá VM toobe redimensionado usando tamanho da VM Olá desejado.
5. Recrie todas as outras VMs que estavam no serviço de nuvem hello usando um tamanho VM disponível no cluster de hardware Olá agora hospedando o serviço de nuvem Olá.

Um exemplo de script para excluir e recriar um serviço de nuvem usando um novo tamanho VM pode ser encontrado [aqui](https://github.com/Azure/azure-vm-scripts). 

## <a name="next-steps"></a>Próximas etapas
* [Redimensionar uma VM criada no modelo de implantação do Gerenciador de recursos de saudação](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

